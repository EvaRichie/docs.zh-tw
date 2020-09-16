---
title: 傳輸：WSE 3.0 TCP 互通性
ms.date: 03/30/2017
ms.assetid: 5f7c3708-acad-4eb3-acb9-d232c77d1486
ms.openlocfilehash: f61d5037af0be6579d5110152ca070bec586fe87
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558962"
---
# <a name="transport-wse-30-tcp-interoperability"></a><span data-ttu-id="afffc-102">傳輸：WSE 3.0 TCP 互通性</span><span class="sxs-lookup"><span data-stu-id="afffc-102">Transport: WSE 3.0 TCP Interoperability</span></span>
<span data-ttu-id="afffc-103">WSE 3.0 TCP 互通性傳輸範例示範如何將 TCP 雙工會話實作為自訂 Windows Communication Foundation (WCF) 傳輸。</span><span class="sxs-lookup"><span data-stu-id="afffc-103">The WSE 3.0 TCP Interoperability Transport sample demonstrates how to implement a TCP duplex session as a custom Windows Communication Foundation (WCF) transport.</span></span> <span data-ttu-id="afffc-104">也會示範如何使用通道層的擴充性，透過網路與現有的已部署系統相連結。</span><span class="sxs-lookup"><span data-stu-id="afffc-104">It also demonstrates how you can use the extensibility of the channel layer to interface over the wire with existing deployed systems.</span></span> <span data-ttu-id="afffc-105">下列步驟示範如何建立這個自訂 WCF 傳輸：</span><span class="sxs-lookup"><span data-stu-id="afffc-105">The following steps show how to build this custom WCF transport:</span></span>  
  
1. <span data-ttu-id="afffc-106">從 TCP 通訊端 (Socket) 開始，建立會使用 DIME 框架來描述訊息界限之 <xref:System.ServiceModel.Channels.IDuplexSessionChannel> 的用戶端和伺服器實作。</span><span class="sxs-lookup"><span data-stu-id="afffc-106">Starting with a TCP socket, create client and server implementations of <xref:System.ServiceModel.Channels.IDuplexSessionChannel> that use DIME Framing to delineate message boundaries.</span></span>  
  
2. <span data-ttu-id="afffc-107">建立會連接至 WSE TCP 服務，並透過用戶端 <xref:System.ServiceModel.Channels.IDuplexSessionChannel>s 傳送框架處理訊息的通道處理站。</span><span class="sxs-lookup"><span data-stu-id="afffc-107">Create a channel factory that connects to a WSE TCP service and sends framed messages over the client <xref:System.ServiceModel.Channels.IDuplexSessionChannel>s.</span></span>  
  
3. <span data-ttu-id="afffc-108">建立通道接聽程式，以接受連入的 TCP 連線並產生對應的通道。</span><span class="sxs-lookup"><span data-stu-id="afffc-108">Create a channel listener to accept incoming TCP connections and produce corresponding channels.</span></span>  
  
4. <span data-ttu-id="afffc-109">確認已將所有網路特定例外狀況正規化為適當的 <xref:System.ServiceModel.CommunicationException> 衍生類別。</span><span class="sxs-lookup"><span data-stu-id="afffc-109">Ensure that any network-specific exceptions are normalized to the appropriate derived class of <xref:System.ServiceModel.CommunicationException>.</span></span>  
  
5. <span data-ttu-id="afffc-110">新增繫結項目，而此繫結項目會將自訂傳輸新增至通道堆疊。</span><span class="sxs-lookup"><span data-stu-id="afffc-110">Add a binding element that adds the custom transport to a channel stack.</span></span> <span data-ttu-id="afffc-111">如需詳細資訊，請參閱 [新增繫結項目]。</span><span class="sxs-lookup"><span data-stu-id="afffc-111">For more information, see [Adding a Binding Element].</span></span>  
  
## <a name="creating-iduplexsessionchannel"></a><span data-ttu-id="afffc-112">建立 IDuplexSessionChannel</span><span class="sxs-lookup"><span data-stu-id="afffc-112">Creating IDuplexSessionChannel</span></span>  
 <span data-ttu-id="afffc-113">撰寫 WSE 3.0 TCP 互通性傳輸的第一個步驟，就是在 <xref:System.ServiceModel.Channels.IDuplexSessionChannel> 之上建立 <xref:System.Net.Sockets.Socket> 的實作。</span><span class="sxs-lookup"><span data-stu-id="afffc-113">The first step in writing the WSE 3.0 TCP Interoperability Transport is to create an implementation of <xref:System.ServiceModel.Channels.IDuplexSessionChannel> on top of a <xref:System.Net.Sockets.Socket>.</span></span> <span data-ttu-id="afffc-114">`WseTcpDuplexSessionChannel` 衍生自 <xref:System.ServiceModel.Channels.ChannelBase>。</span><span class="sxs-lookup"><span data-stu-id="afffc-114">`WseTcpDuplexSessionChannel` derives from <xref:System.ServiceModel.Channels.ChannelBase>.</span></span> <span data-ttu-id="afffc-115">傳送訊息的邏輯由兩個主要部分所組成：(1) 將訊息編碼成位元組，以及 (2) 框架處理這些位元組並在網路上傳送。</span><span class="sxs-lookup"><span data-stu-id="afffc-115">The logic of sending a message consists of two main pieces: (1) Encoding the message into bytes, and (2) framing those bytes and sending them on the wire.</span></span>  
  
 `ArraySegment<byte> encodedBytes = EncodeMessage(message);`  
  
 `WriteData(encodedBytes);`  
  
 <span data-ttu-id="afffc-116">此外也可使用鎖定，讓 Send() 呼叫可依序保留 IDuplexSessionChannel 保證，這樣便可正確地同步處理基礎通訊端的呼叫。</span><span class="sxs-lookup"><span data-stu-id="afffc-116">In addition, a lock is taken so that the Send() calls preserve the IDuplexSessionChannel in-order guarantee, and so that calls to the underlying socket are synchronized correctly.</span></span>  
  
 <span data-ttu-id="afffc-117">`WseTcpDuplexSessionChannel` 會使用 <xref:System.ServiceModel.Channels.MessageEncoder>，從 byte[] 來回轉換 <xref:System.ServiceModel.Channels.Message>。</span><span class="sxs-lookup"><span data-stu-id="afffc-117">`WseTcpDuplexSessionChannel` uses a <xref:System.ServiceModel.Channels.MessageEncoder> for translating a <xref:System.ServiceModel.Channels.Message> to and from byte[].</span></span> <span data-ttu-id="afffc-118">由於這是一種傳輸功能，`WseTcpDuplexSessionChannel` 也會負責套用設定通道所使用的遠端位址。</span><span class="sxs-lookup"><span data-stu-id="afffc-118">Because it is a transport, `WseTcpDuplexSessionChannel` is also responsible for applying the remote address that the channel was configured with.</span></span> <span data-ttu-id="afffc-119">`EncodeMessage` 會封裝這個轉換的邏輯。</span><span class="sxs-lookup"><span data-stu-id="afffc-119">`EncodeMessage` encapsulates the logic for this conversion.</span></span>  
  
 `this.RemoteAddress.ApplyTo(message);`  
  
 `return encoder.WriteMessage(message, maxBufferSize, bufferManager);`  
  
 <span data-ttu-id="afffc-120">一旦將 <xref:System.ServiceModel.Channels.Message> 編碼為位元組，就必須在網路上傳輸。</span><span class="sxs-lookup"><span data-stu-id="afffc-120">Once the <xref:System.ServiceModel.Channels.Message> is encoded into bytes, it must be transmitted on the wire.</span></span> <span data-ttu-id="afffc-121">此時需要系統來定義訊息界限。</span><span class="sxs-lookup"><span data-stu-id="afffc-121">This requires a system for defining message boundaries.</span></span> <span data-ttu-id="afffc-122">WSE 3.0 使用某個版本的 [DIME](/archive/msdn-magazine/2002/december/sending-files-attachments-and-soap-messages-via-dime) 作為其框架通訊協定。</span><span class="sxs-lookup"><span data-stu-id="afffc-122">WSE 3.0 uses a version of [DIME](/archive/msdn-magazine/2002/december/sending-files-attachments-and-soap-messages-via-dime) as its framing protocol.</span></span> <span data-ttu-id="afffc-123">`WriteData` 會封裝框架邏輯，以將 byte[] 包裝在一組 DIME 記錄中。</span><span class="sxs-lookup"><span data-stu-id="afffc-123">`WriteData` encapsulates the framing logic to wrap a byte[] into a set of DIME records.</span></span>  
  
 <span data-ttu-id="afffc-124">接收訊息的邏輯很類似。</span><span class="sxs-lookup"><span data-stu-id="afffc-124">The logic for receiving messages is similar.</span></span> <span data-ttu-id="afffc-125">主要的複雜性是處理通訊端讀取所傳回的位元組數少於所要求的數目。</span><span class="sxs-lookup"><span data-stu-id="afffc-125">The main complexity is handling the fact that a socket read can return fewer bytes than were requested.</span></span> <span data-ttu-id="afffc-126">若要接收訊息，`WseTcpDuplexSessionChannel` 會讀取網路上的位元組、解碼 DIME 框架，然後使用 <xref:System.ServiceModel.Channels.MessageEncoder> 將 byte[] 轉換為 <xref:System.ServiceModel.Channels.Message>。</span><span class="sxs-lookup"><span data-stu-id="afffc-126">To receive a message, `WseTcpDuplexSessionChannel` reads bytes off the wire, decodes the DIME framing, and then uses the <xref:System.ServiceModel.Channels.MessageEncoder> for turning the byte[] into a <xref:System.ServiceModel.Channels.Message>.</span></span>  
  
 <span data-ttu-id="afffc-127">基底 `WseTcpDuplexSessionChannel` 會假設是接收連線的通訊端。</span><span class="sxs-lookup"><span data-stu-id="afffc-127">The base `WseTcpDuplexSessionChannel` assumes that it receives a connected socket.</span></span> <span data-ttu-id="afffc-128">基底類別接著會處理通訊端關閉。</span><span class="sxs-lookup"><span data-stu-id="afffc-128">The base class handles socket shutdown.</span></span> <span data-ttu-id="afffc-129">有三個部分與通訊端關閉相關：</span><span class="sxs-lookup"><span data-stu-id="afffc-129">There are three places that interface with socket closure:</span></span>  
  
- <span data-ttu-id="afffc-130">OnAbort -- 以非正常程序關閉通訊端 (強制關閉)。</span><span class="sxs-lookup"><span data-stu-id="afffc-130">OnAbort -- close the socket ungracefully (hard close).</span></span>  
  
- <span data-ttu-id="afffc-131">On[Begin]Close -- 以正常程序關閉通訊端 (軟關閉)。</span><span class="sxs-lookup"><span data-stu-id="afffc-131">On[Begin]Close -- close the socket gracefully (soft close).</span></span>  
  
- <span data-ttu-id="afffc-132">會話。CloseOutputSession--將輸出資料流程關閉 (半近) 。</span><span class="sxs-lookup"><span data-stu-id="afffc-132">session.CloseOutputSession -- shut down the outbound data stream (half close).</span></span>  
  
## <a name="channel-factory"></a><span data-ttu-id="afffc-133">通道處理站</span><span class="sxs-lookup"><span data-stu-id="afffc-133">Channel Factory</span></span>  
 <span data-ttu-id="afffc-134">撰寫 TCP 傳輸的下一個步驟為，建立用戶端通道的 <xref:System.ServiceModel.Channels.IChannelFactory> 實作。</span><span class="sxs-lookup"><span data-stu-id="afffc-134">The next step in writing the TCP transport is to create an implementation of <xref:System.ServiceModel.Channels.IChannelFactory> for client channels.</span></span>  
  
- <span data-ttu-id="afffc-135">`WseTcpChannelFactory`衍生自 <xref:System.ServiceModel.Channels.ChannelFactoryBase> \<IDuplexSessionChannel> 。</span><span class="sxs-lookup"><span data-stu-id="afffc-135">`WseTcpChannelFactory` derives from <xref:System.ServiceModel.Channels.ChannelFactoryBase>\<IDuplexSessionChannel>.</span></span> <span data-ttu-id="afffc-136">這是覆寫 `OnCreateChannel` 以產生用戶端通道的處理站。</span><span class="sxs-lookup"><span data-stu-id="afffc-136">It is a factory that overrides `OnCreateChannel` to produce client channels.</span></span>  
  
 `protected override IDuplexSessionChannel OnCreateChannel(EndpointAddress remoteAddress, Uri via)`  
  
 `{`  
  
 `return new ClientWseTcpDuplexSessionChannel(encoderFactory, bufferManager, remoteAddress, via, this);`  
  
 `}`  
  
- <span data-ttu-id="afffc-137">`ClientWseTcpDuplexSessionChannel` 將邏輯新增至基底 `WseTcpDuplexSessionChannel` ，以在一段時間連接到 TCP 伺服器 `channel.Open` 。</span><span class="sxs-lookup"><span data-stu-id="afffc-137">`ClientWseTcpDuplexSessionChannel` adds logic to the base `WseTcpDuplexSessionChannel` to connect to a TCP server at `channel.Open` time.</span></span> <span data-ttu-id="afffc-138">首先會將主機名稱解析為 IP 位址，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="afffc-138">First the hostname is resolved to an IP address, as shown in the following code.</span></span>  
  
 `hostEntry = Dns.GetHostEntry(Via.Host);`  
  
- <span data-ttu-id="afffc-139">接著將主機名稱連接至迴圈中第一個可用的 IP 位址，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="afffc-139">Then the hostname is connected to the first available IP address in a loop, as shown in the following code.</span></span>  
  
 `IPAddress address = hostEntry.AddressList[i];`  
  
 `socket = new Socket(address.AddressFamily, SocketType.Stream, ProtocolType.Tcp);`  
  
 `socket.Connect(new IPEndPoint(address, port));`  
  
- <span data-ttu-id="afffc-140">包裝網域特定的例外狀況，例如 `SocketException` 中的 <xref:System.ServiceModel.CommunicationException>，以充當為通道合約的一部分。</span><span class="sxs-lookup"><span data-stu-id="afffc-140">As part of the channel contract, any domain-specific exceptions are wrapped, such as `SocketException` in <xref:System.ServiceModel.CommunicationException>.</span></span>  
  
## <a name="channel-listener"></a><span data-ttu-id="afffc-141">通道接聽程式</span><span class="sxs-lookup"><span data-stu-id="afffc-141">Channel Listener</span></span>  
 <span data-ttu-id="afffc-142">撰寫 TCP 傳輸的下一個步驟為，建立可接受伺服器通道的 <xref:System.ServiceModel.Channels.IChannelListener> 實作。</span><span class="sxs-lookup"><span data-stu-id="afffc-142">The next step in writing the TCP transport is to create an implementation of <xref:System.ServiceModel.Channels.IChannelListener> for accepting server channels.</span></span>  
  
- <span data-ttu-id="afffc-143">`WseTcpChannelListener`衍生自 <xref:System.ServiceModel.Channels.ChannelListenerBase> \<IDuplexSessionChannel> 和覆寫于 [開始] 開啟且在 [開始] 上，關閉以控制其接聽通訊端的存留期。</span><span class="sxs-lookup"><span data-stu-id="afffc-143">`WseTcpChannelListener` derives from <xref:System.ServiceModel.Channels.ChannelListenerBase>\<IDuplexSessionChannel> and overrides On[Begin]Open and On[Begin]Close to control the lifetime of its listen socket.</span></span> <span data-ttu-id="afffc-144">在 OnOpen 中，您會建立通訊端以接聽 IP_ANY。</span><span class="sxs-lookup"><span data-stu-id="afffc-144">In OnOpen, a socket is created to listen on IP_ANY.</span></span> <span data-ttu-id="afffc-145">更進階的實作則可以建立第二個通訊端，就也可以階聽 IPv6。</span><span class="sxs-lookup"><span data-stu-id="afffc-145">More advanced implementations can create a second socket to listen on IPv6 as well.</span></span> <span data-ttu-id="afffc-146">這些實作也允許在主機名稱中指定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="afffc-146">They can also allow the IP address to be specified in the hostname.</span></span>  
  
 `IPEndPoint localEndpoint = new IPEndPoint(IPAddress.Any, uri.Port);`  
  
 `this.listenSocket = new Socket(localEndpoint.AddressFamily, SocketType.Stream, ProtocolType.Tcp);`  
  
 `this.listenSocket.Bind(localEndpoint);`  
  
 `this.listenSocket.Listen(10);`  
  
 <span data-ttu-id="afffc-147">接受新的通訊端時，就會使用此通訊端初始化伺服器通道。</span><span class="sxs-lookup"><span data-stu-id="afffc-147">When a new socket is accepted, a server channel is initialized with this socket.</span></span> <span data-ttu-id="afffc-148">在基底類別中已實作所有輸入和輸出，因此這個通道可以負責初始化通訊端。</span><span class="sxs-lookup"><span data-stu-id="afffc-148">All the input and output is already implemented in the base class, so this channel is responsible for initializing the socket.</span></span>  
  
## <a name="adding-a-binding-element"></a><span data-ttu-id="afffc-149">新增繫結項目</span><span class="sxs-lookup"><span data-stu-id="afffc-149">Adding a Binding Element</span></span>  
 <span data-ttu-id="afffc-150">現在已建置處理站和通道，就必須透過繫結公開至 ServiceModel 執行階段。</span><span class="sxs-lookup"><span data-stu-id="afffc-150">Now that the factories and channels are built, they must be exposed to the ServiceModel runtime through a binding.</span></span> <span data-ttu-id="afffc-151">繫結是繫結項目的集合，表示與服務位址相關聯的通訊堆疊。</span><span class="sxs-lookup"><span data-stu-id="afffc-151">A binding is a collection of binding elements that represents the communication stack associated with a service address.</span></span> <span data-ttu-id="afffc-152">堆疊中的每個項目都是由繫結項目表示。</span><span class="sxs-lookup"><span data-stu-id="afffc-152">Each element in the stack is represented by a binding element.</span></span>  
  
 <span data-ttu-id="afffc-153">在此範例中，繫結項目為 `WseTcpTransportBindingElement`，其衍生自 <xref:System.ServiceModel.Channels.TransportBindingElement>。</span><span class="sxs-lookup"><span data-stu-id="afffc-153">In the sample, the binding element is `WseTcpTransportBindingElement`, which derives from <xref:System.ServiceModel.Channels.TransportBindingElement>.</span></span> <span data-ttu-id="afffc-154">此繫結項目支援 <xref:System.ServiceModel.Channels.IDuplexSessionChannel> 並會覆寫下列方法，以建置與繫結相關聯的處理站。</span><span class="sxs-lookup"><span data-stu-id="afffc-154">It supports <xref:System.ServiceModel.Channels.IDuplexSessionChannel> and overrides the following methods to build the factories associated with our binding.</span></span>  
  
 `public IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)`  
  
 `{`  
  
 `return (IChannelFactory<TChannel>)(object)new WseTcpChannelFactory(this, context);`  
  
 `}`  
  
 `public IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)`  
  
 `{`  
  
 `return (IChannelListener<TChannel>)(object)new WseTcpChannelListener(this, context);`  
  
 `}`  
  
 <span data-ttu-id="afffc-155">它還包含可以用來複製 `BindingElement` 以及傳回結構描述 (wse.tcp) 的成員。</span><span class="sxs-lookup"><span data-stu-id="afffc-155">It also contains members for cloning the `BindingElement` and returning our scheme (wse.tcp).</span></span>  
  
## <a name="the-wse-tcp-test-console"></a><span data-ttu-id="afffc-156">WSE TCP 測試主控台</span><span class="sxs-lookup"><span data-stu-id="afffc-156">The WSE TCP Test Console</span></span>  
 <span data-ttu-id="afffc-157">您可以在 TestCode.cs 中找到使用這個範例傳輸的測試程式碼。</span><span class="sxs-lookup"><span data-stu-id="afffc-157">Test code for using this sample transport is available in TestCode.cs.</span></span> <span data-ttu-id="afffc-158">下列指示說明如何設定 WSE `TcpSyncStockService` 範例。</span><span class="sxs-lookup"><span data-stu-id="afffc-158">The following instructions show how to set up the WSE `TcpSyncStockService` sample.</span></span>  
  
 <span data-ttu-id="afffc-159">測試程式碼會建立使用 MTOM 做為編碼，並使用 `WseTcpTransport` 做為傳輸的自訂繫結。</span><span class="sxs-lookup"><span data-stu-id="afffc-159">The test code creates a custom binding that uses MTOM as the encoding and `WseTcpTransport` as the transport.</span></span> <span data-ttu-id="afffc-160">這也會將 AddressingVersion 設定為符合 WSE 3.0，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="afffc-160">It also sets up the AddressingVersion to be conformant with WSE 3.0, as shown in the following code.</span></span>  
  
 `CustomBinding binding = new CustomBinding();`  
  
 `MtomMessageEncodingBindingElement mtomBindingElement = new MtomMessageEncodingBindingElement();`  
  
 `mtomBindingElement.MessageVersion = MessageVersion.Soap11WSAddressingAugust2004;`  
  
 `binding.Elements.Add(mtomBindingElement);`  
  
 `binding.Elements.Add(new WseTcpTransportBindingElement());`  
  
 <span data-ttu-id="afffc-161">其中包含兩個測試：第一個測試會使用 WSE 3.0 WSDL 產生的程式碼來設定具型別的用戶端。</span><span class="sxs-lookup"><span data-stu-id="afffc-161">It consists of two tests—one test sets up a typed client using code generated from the WSE 3.0 WSDL.</span></span> <span data-ttu-id="afffc-162">第二項測試會使用 WCF 做為用戶端和伺服器，方法是直接在通道 Api 上傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="afffc-162">The second test uses WCF as both the client and the server by sending messages directly on top of the channel APIs.</span></span>  
  
 <span data-ttu-id="afffc-163">執行範例時，預期會產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="afffc-163">When running the sample, the following output is expected.</span></span>  
  
 <span data-ttu-id="afffc-164">用戶端：</span><span class="sxs-lookup"><span data-stu-id="afffc-164">Client:</span></span>  
  
```console  
Calling soap://stockservice.contoso.com/wse/samples/2003/06/TcpSyncStockService  
  
Symbol: FABRIKAM  
        Name: Fabrikam, Inc.  
        Last Price: 120  
  
Symbol: CONTOSO  
        Name: Contoso Corp.  
        Last Price: 50.07  
Press enter.  
  
Received Action: http://SayHello  
Received Body: to you.  
Hello to you.  
Press enter.  
  
Received Action: http://NotHello  
Received Body: to me.  
Press enter.  
```  
  
 <span data-ttu-id="afffc-165">伺服器：</span><span class="sxs-lookup"><span data-stu-id="afffc-165">Server:</span></span>  
  
```console  
Listening for messages at soap://stockservice.contoso.com/wse/samples/2003/06/TcpSyncStockService  
  
Press any key to exit when done...  
  
Request received.  
Symbols:  
        FABRIKAM  
        CONTOSO  
```  
  
## <a name="set-up-build-and-run-the-sample"></a><span data-ttu-id="afffc-166">設定、建立及執行範例</span><span class="sxs-lookup"><span data-stu-id="afffc-166">Set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="afffc-167">若要執行此範例，您必須有 [Web 服務增強功能 (wse) 3.0 （適用于 Microsoft .net](https://www.microsoft.com/download/details.aspx?id=14089) ）和 wse `TcpSyncStockService` 範例安裝。</span><span class="sxs-lookup"><span data-stu-id="afffc-167">To run this sample, you must have [Web Services Enhancements (WSE) 3.0 for Microsoft .NET](https://www.microsoft.com/download/details.aspx?id=14089) and the WSE `TcpSyncStockService` sample installed.</span></span>
  
> [!NOTE]
> <span data-ttu-id="afffc-168">因為 Windows Server 2008 不支援 WSE 3.0，所以您無法 `TcpSyncStockService` 在該作業系統上安裝或執行此範例。</span><span class="sxs-lookup"><span data-stu-id="afffc-168">Because WSE 3.0 is not supported on Windows Server 2008, you cannot install or run the `TcpSyncStockService` sample on that operating system.</span></span>  
  
1. <span data-ttu-id="afffc-169">在安裝 `TcpSyncStockService` 範例之後，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="afffc-169">Once you install the `TcpSyncStockService` sample, do the following:</span></span>  
  
    1. <span data-ttu-id="afffc-170">`TcpSyncStockService`在 Visual Studio 中開啟。</span><span class="sxs-lookup"><span data-stu-id="afffc-170">Open the `TcpSyncStockService` in Visual Studio.</span></span> <span data-ttu-id="afffc-171"> (TcpSyncStockService 範例是與 WSE 3.0 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="afffc-171">(The TcpSyncStockService sample is installed with WSE 3.0.</span></span> <span data-ttu-id="afffc-172">它不是此範例程式碼的一部分。 ) </span><span class="sxs-lookup"><span data-stu-id="afffc-172">It is not part of this sample's code.)</span></span>  
  
    2. <span data-ttu-id="afffc-173">將 StockService 專案設定為啟動專案。</span><span class="sxs-lookup"><span data-stu-id="afffc-173">Set the StockService project as the start-up project.</span></span>  
  
    3. <span data-ttu-id="afffc-174">開啟 StockService 專案中的 StockService.cs，並將 `StockService` 類別中的 [Policy] 屬性標記為註解。</span><span class="sxs-lookup"><span data-stu-id="afffc-174">Open StockService.cs in the StockService project and comment out the [Policy] attribute on the `StockService` class.</span></span> <span data-ttu-id="afffc-175">這樣就會停用範例的安全性。</span><span class="sxs-lookup"><span data-stu-id="afffc-175">This disables security from the sample.</span></span> <span data-ttu-id="afffc-176">雖然 WCF 可以與 WSE 3.0 安全端點交互操作，但會停用安全性，讓此範例著重于自訂 TCP 傳輸。</span><span class="sxs-lookup"><span data-stu-id="afffc-176">While WCF can interoperate with WSE 3.0 secure endpoints, security is disabled to keep this sample focused on the custom TCP transport.</span></span>  
  
    4. <span data-ttu-id="afffc-177">按 F5 以啟動 `TcpSyncStockService`。</span><span class="sxs-lookup"><span data-stu-id="afffc-177">Press F5 to start the `TcpSyncStockService`.</span></span> <span data-ttu-id="afffc-178">將在新主控台視窗中啟動服務。</span><span class="sxs-lookup"><span data-stu-id="afffc-178">The service starts in a new console window.</span></span>  
  
    5. <span data-ttu-id="afffc-179">在 Visual Studio 中開啟此 TCP 傳輸範例。</span><span class="sxs-lookup"><span data-stu-id="afffc-179">Open this TCP transport sample in Visual Studio.</span></span>  
  
    6. <span data-ttu-id="afffc-180">更新 TestCode.cs 中的 "hostname" 變數，以符合執行 `TcpSyncStockService` 的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="afffc-180">Update the "hostname" variable in TestCode.cs to match the machine name running the `TcpSyncStockService`.</span></span>  
  
    7. <span data-ttu-id="afffc-181">按 F5 以啟動 TCP 傳輸範例。</span><span class="sxs-lookup"><span data-stu-id="afffc-181">Press F5 to start the TCP transport sample.</span></span>  
  
    8. <span data-ttu-id="afffc-182">會在新主控台中啟動 TCP 傳輸測試用戶端。</span><span class="sxs-lookup"><span data-stu-id="afffc-182">The TCP transport test client starts in a new console.</span></span> <span data-ttu-id="afffc-183">用戶端要求積存會從服務進行引用，並在其主控台視窗中顯示結果。</span><span class="sxs-lookup"><span data-stu-id="afffc-183">The client requests stock quotes from the service and then displays the results in its console window.</span></span>
