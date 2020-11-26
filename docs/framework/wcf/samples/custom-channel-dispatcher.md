---
title: 自訂通道發送器
ms.date: 03/30/2017
ms.assetid: 813acf03-9661-4d57-a3c7-eeab497321c6
ms.openlocfilehash: 38d39cbba15c95a43444108d634d3c30524c70f4
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96241768"
---
# <a name="custom-channel-dispatcher"></a><span data-ttu-id="0f88b-102">自訂通道發送器</span><span class="sxs-lookup"><span data-stu-id="0f88b-102">Custom Channel Dispatcher</span></span>

<span data-ttu-id="0f88b-103">此範例示範如何使用自訂的方式，直接實作 <xref:System.ServiceModel.ServiceHostBase> 來建立通道堆疊，以及如何在 Web 主機環境中建立自訂通道發送器。</span><span class="sxs-lookup"><span data-stu-id="0f88b-103">This sample demonstrates how to build the channel stack in a custom way by implementing <xref:System.ServiceModel.ServiceHostBase> directly and how to create a custom channel dispatcher in Web host environment.</span></span> <span data-ttu-id="0f88b-104">通道發送器會與 <xref:System.ServiceModel.Channels.IChannelListener> 互動，以接受通道並擷取來自通道堆疊的訊息。</span><span class="sxs-lookup"><span data-stu-id="0f88b-104">The channel dispatcher interacts with <xref:System.ServiceModel.Channels.IChannelListener> to accept channels and retrieves messages from the channel stack.</span></span> <span data-ttu-id="0f88b-105">此範例也提供基本範例，示範如何在 Web 主機環境中使用 <xref:System.ServiceModel.Activation.VirtualPathExtension> 建立通道堆疊。</span><span class="sxs-lookup"><span data-stu-id="0f88b-105">This sample also provides a basic sample to show how to build a channel stack in a Web host environment by using <xref:System.ServiceModel.Activation.VirtualPathExtension>.</span></span>  
  
## <a name="custom-servicehostbase"></a><span data-ttu-id="0f88b-106">自訂 ServiceHostBase</span><span class="sxs-lookup"><span data-stu-id="0f88b-106">Custom ServiceHostBase</span></span>  

 <span data-ttu-id="0f88b-107">這個範例會實作為基底型別， <xref:System.ServiceModel.ServiceHostBase> 而不是 <xref:System.ServiceModel.ServiceHost> 示範如何使用通道堆疊頂端的自訂訊息處理層來取代 WINDOWS COMMUNICATION FOUNDATION (WCF) 堆疊實作為取代。</span><span class="sxs-lookup"><span data-stu-id="0f88b-107">This sample implements the base type <xref:System.ServiceModel.ServiceHostBase> instead of <xref:System.ServiceModel.ServiceHost> to demonstrate how to replace the Windows Communication Foundation (WCF) stack implementation with a custom message handling layer on top of the channel stack.</span></span> <span data-ttu-id="0f88b-108">您要覆寫虛擬方法 <xref:System.ServiceModel.ServiceHostBase.InitializeRuntime%2A> 才能建立通道接聽項和通道發送器。</span><span class="sxs-lookup"><span data-stu-id="0f88b-108">You override the virtual method <xref:System.ServiceModel.ServiceHostBase.InitializeRuntime%2A> to build channel listeners and the channel dispatcher.</span></span>  
  
 <span data-ttu-id="0f88b-109">若要實作 Web 裝載的服務，請從 <xref:System.ServiceModel.Activation.VirtualPathExtension> 集合取得服務延伸 <xref:System.ServiceModel.ServiceHostBase.Extensions%2A>，並將其加入至 <xref:System.ServiceModel.Channels.BindingParameterCollection>，讓傳輸層知道如何根據裝載環境設定 (亦即，Internet Information Services (IIS)/Windows Process Activation Service (WAS) 設定) 來設定通道接聽項。</span><span class="sxs-lookup"><span data-stu-id="0f88b-109">To implement a Web-hosted service, get the service extension <xref:System.ServiceModel.Activation.VirtualPathExtension> from the <xref:System.ServiceModel.ServiceHostBase.Extensions%2A> collection and add it to the <xref:System.ServiceModel.Channels.BindingParameterCollection> so that the transport layer knows how to configure the channel listener based on the hosting environment settings, that is, the Internet Information Services (IIS)/Windows Process Activation Service (WAS) settings.</span></span>  
  
## <a name="custom-channel-dispatcher"></a><span data-ttu-id="0f88b-110">自訂通道發送器</span><span class="sxs-lookup"><span data-stu-id="0f88b-110">Custom Channel Dispatcher</span></span>  

 <span data-ttu-id="0f88b-111">自訂通道發送器會延伸 <xref:System.ServiceModel.Dispatcher.ChannelDispatcherBase> 類型。</span><span class="sxs-lookup"><span data-stu-id="0f88b-111">The custom channel dispatcher extends the type <xref:System.ServiceModel.Dispatcher.ChannelDispatcherBase>.</span></span> <span data-ttu-id="0f88b-112">此類型會實作通道層的程式設計邏輯。</span><span class="sxs-lookup"><span data-stu-id="0f88b-112">This type implements the channel-layer programming logic.</span></span> <span data-ttu-id="0f88b-113">在此範例中，要求-回覆訊息交換模式只支援 <xref:System.ServiceModel.Channels.IReplyChannel>，但自訂通道發送器可以輕易地延伸到其他通道類型。</span><span class="sxs-lookup"><span data-stu-id="0f88b-113">In this sample, only <xref:System.ServiceModel.Channels.IReplyChannel> is supported for request-reply message exchange pattern, but the custom channel dispatcher can be easily extended to other channel types.</span></span>  
  
 <span data-ttu-id="0f88b-114">發送器會先開啟通道接聽項，然後接受單一回覆通道。</span><span class="sxs-lookup"><span data-stu-id="0f88b-114">The dispatcher first opens the channel listener and then accepts the singleton reply channel.</span></span> <span data-ttu-id="0f88b-115">它會利用通道，開始以無限迴圈傳送訊息 (要求)。</span><span class="sxs-lookup"><span data-stu-id="0f88b-115">With the channel, it starts to send messages (requests) in an infinite loop.</span></span> <span data-ttu-id="0f88b-116">針對每個要求，它都會建立一個回覆訊息，並將其傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="0f88b-116">For each request, it creates a reply message and sends it back to the client.</span></span>  
  
## <a name="creating-a-response-message"></a><span data-ttu-id="0f88b-117">建立回應訊息</span><span class="sxs-lookup"><span data-stu-id="0f88b-117">Creating a Response Message</span></span>  

 <span data-ttu-id="0f88b-118">訊息處理是以 `MyServiceManager` 類型實作。</span><span class="sxs-lookup"><span data-stu-id="0f88b-118">The message processing is implemented in the type `MyServiceManager`.</span></span> <span data-ttu-id="0f88b-119">在 `HandleRequest` 方法中，會先檢查訊息的 `Action` 標頭，以查看是否支援要求。</span><span class="sxs-lookup"><span data-stu-id="0f88b-119">In the `HandleRequest` method, the `Action` header of the message is first checked to see whether the request is supported.</span></span> <span data-ttu-id="0f88b-120">定義了預先定義的 SOAP 動作 " http://tempuri.org/HelloWorld/Hello "，以提供訊息篩選。</span><span class="sxs-lookup"><span data-stu-id="0f88b-120">A predefined SOAP action "http://tempuri.org/HelloWorld/Hello" is defined to provide message filtering.</span></span> <span data-ttu-id="0f88b-121">這與的 WCF 執行中的服務合約概念類似 <xref:System.ServiceModel.ServiceHost> 。</span><span class="sxs-lookup"><span data-stu-id="0f88b-121">This is similar to the service contract concept in the WCF implementation of <xref:System.ServiceModel.ServiceHost>.</span></span>  
  
 <span data-ttu-id="0f88b-122">若是正確的 SOAP 動作案例，此範例會擷取要求的訊息資料，並針對要求產生類似於 <xref:System.ServiceModel.ServiceHost> 案例中看到的對應回應。</span><span class="sxs-lookup"><span data-stu-id="0f88b-122">For the correct SOAP action case, the sample retrieves the requested message data and generates a corresponding response to the request similar to what is seen in the <xref:System.ServiceModel.ServiceHost> case.</span></span>  
  
 <span data-ttu-id="0f88b-123">在此情況下，您要透過傳回自訂 HTML 訊息來明確地處理 HTTP-GET 動詞命令，讓您可以從瀏覽器瀏覽服務，以查看它是否正確編譯。</span><span class="sxs-lookup"><span data-stu-id="0f88b-123">You specially handled the HTTP-GET verb by returning a custom HTML message, in this, case so that you can browse the service from a browser to see that it is compiled correctly.</span></span> <span data-ttu-id="0f88b-124">如果 SOAP 動作不相符，請傳回錯誤訊息以指出此要求不受到支援。</span><span class="sxs-lookup"><span data-stu-id="0f88b-124">If the SOAP action does not match, send a fault message back to indicate that the request is not supported.</span></span>  
  
 <span data-ttu-id="0f88b-125">此範例的用戶端是一般的 WCF 用戶端，不會假設服務中的任何服務。</span><span class="sxs-lookup"><span data-stu-id="0f88b-125">The client of this sample is a normal WCF client that does not assume anything from the service.</span></span> <span data-ttu-id="0f88b-126">因此，此服務是特別設計來符合您從一般 WCF 執行所取得的內容 <xref:System.ServiceModel.ServiceHost> 。</span><span class="sxs-lookup"><span data-stu-id="0f88b-126">So, the service is specially designed to match what you get from a normal WCF<xref:System.ServiceModel.ServiceHost> implementation.</span></span> <span data-ttu-id="0f88b-127">所以，在用戶端上只需要一個服務合約。</span><span class="sxs-lookup"><span data-stu-id="0f88b-127">As a result, only a service contract is required on the client.</span></span>  
  
## <a name="using-the-sample"></a><span data-ttu-id="0f88b-128">使用範例</span><span class="sxs-lookup"><span data-stu-id="0f88b-128">Using the sample</span></span>  

 <span data-ttu-id="0f88b-129">執行用戶端應用程式會直接產生下列輸出。</span><span class="sxs-lookup"><span data-stu-id="0f88b-129">Running the client application directly produces the following output.</span></span>  
  
```output  
Client is talking to a request/reply WCF service.
Type what you want to say to the server: Howdy  
Server replied: You said: Howdy. Message id: 1  
Server replied: You said: Howdy. Message id: 2  
Server replied: You said: Howdy. Message id: 3  
Server replied: You said: Howdy. Message id: 4  
Server replied: You said: Howdy. Message id: 5  
```  
  
 <span data-ttu-id="0f88b-130">您也可以從瀏覽器瀏覽服務，讓 HTTP-GET 訊息在伺服器上繼續執行。</span><span class="sxs-lookup"><span data-stu-id="0f88b-130">You can also browse the service from a browser so that an HTTP-GET message gets processed on the server.</span></span> <span data-ttu-id="0f88b-131">如此會回覆您正確格式的 HTML 文字。</span><span class="sxs-lookup"><span data-stu-id="0f88b-131">This gets you well-formatted HTML text back.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="0f88b-132">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0f88b-132">The samples may already be installed on your machine.</span></span> <span data-ttu-id="0f88b-133">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="0f88b-133">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="0f88b-134">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="0f88b-134">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="0f88b-135">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="0f88b-135">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Channels\CustomChannelDispatcher`
