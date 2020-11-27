---
title: 使用非同步伺服器通訊端
description: 此範例顯示非同步伺服器通訊端。 Socket 類別使用 .NET Framework 非同步程式設計來處理網路服務要求。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- Socket class, asynchronous server sockets
- data requests, sockets
- sockets, asynchronous server sockets
- requesting data from Internet, sockets
- server sockets
- receiving data, sockets
- asynchronous server sockets
- protocols, sockets
- Internet, sockets
ms.assetid: 813489a9-3efd-41b6-a33f-371d55397676
ms.openlocfilehash: 6800a1973d9eb65bbb7520f9db7a8f431656c685
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265202"
---
# <a name="using-an-asynchronous-server-socket"></a><span data-ttu-id="6cf7e-104">使用非同步伺服器通訊端</span><span class="sxs-lookup"><span data-stu-id="6cf7e-104">Using an Asynchronous Server Socket</span></span>

<span data-ttu-id="6cf7e-105">非同步伺服器通訊端會使用 .NET Framework 非同步程式設計模型來處理網路服務要求。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-105">Asynchronous server sockets use the .NET Framework asynchronous programming model to process network service requests.</span></span> <span data-ttu-id="6cf7e-106"><xref:System.Net.Sockets.Socket> 類別會遵循標準 .NET Framework 非同步命名模式；例如，同步 <xref:System.Net.Sockets.Socket.Accept%2A> 方法對應於非同步 <xref:System.Net.Sockets.Socket.BeginAccept%2A> 和 <xref:System.Net.Sockets.Socket.EndAccept%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-106">The <xref:System.Net.Sockets.Socket> class follows the standard .NET Framework asynchronous naming pattern; for example, the synchronous <xref:System.Net.Sockets.Socket.Accept%2A> method corresponds to the asynchronous <xref:System.Net.Sockets.Socket.BeginAccept%2A> and <xref:System.Net.Sockets.Socket.EndAccept%2A> methods.</span></span>  
  
 <span data-ttu-id="6cf7e-107">非同步伺服器通訊端需要一個用來開始接受網路連線要求的方法、一個用來處理連線要求並開始接收網路資料的回呼方法，以及一個用來結束接收資料的回呼方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-107">An asynchronous server socket requires a method to begin accepting connection requests from the network, a callback method to handle the connection requests and begin receiving data from the network, and a callback method to end receiving the data.</span></span> <span data-ttu-id="6cf7e-108">本節會進一步討論所有這些方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-108">All these methods are discussed further in this section.</span></span>  
  
 <span data-ttu-id="6cf7e-109">在下列範例中，若要開始接受網路的連線要求，`StartListening` 方法會初始化 **通訊端**，然後使用 **BeginAccept** 方法來開始接受新連線。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-109">In the following example, to begin accepting connection requests from the network, the method `StartListening` initializes the **Socket** and then uses the **BeginAccept** method to start accepting new connections.</span></span> <span data-ttu-id="6cf7e-110">在通訊端上收到新的連線要求時，就會呼叫接受回呼方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-110">The accept callback method is called when a new connection request is received on the socket.</span></span> <span data-ttu-id="6cf7e-111">它會負責取得將處理連線的 **通訊端** 執行個體，並將該 **通訊端** 移交給將處理要求的執行緒。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-111">It is responsible for getting the **Socket** instance that will handle the connection and handing that **Socket** off to the thread that will process the request.</span></span> <span data-ttu-id="6cf7e-112">接受回呼方法會實作 <xref:System.AsyncCallback> 委派；它會傳回 void，並採用 <xref:System.IAsyncResult> 類型的單一參數。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-112">The accept callback method implements the <xref:System.AsyncCallback> delegate; it returns a void and takes a single parameter of type <xref:System.IAsyncResult>.</span></span> <span data-ttu-id="6cf7e-113">下列範例是接受回呼方法的殼層。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-113">The following example is the shell of an accept callback method.</span></span>  
  
```vb  
Sub AcceptCallback(ar As IAsyncResult)  
    ' Add the callback code here.  
End Sub 'AcceptCallback  
```  
  
```csharp  
void AcceptCallback(IAsyncResult ar)
{  
    // Add the callback code here.  
}  
```  
  
 <span data-ttu-id="6cf7e-114">**BeginAccept** 方法採用兩個參數：指向接受回呼方法的 **AsyncCallback** 委派和用來將狀態資訊傳遞至回呼方法的物件。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-114">The **BeginAccept** method takes two parameters, an **AsyncCallback** delegate that points to the accept callback method and an object that is used to pass state information to the callback method.</span></span> <span data-ttu-id="6cf7e-115">在下列範例中，接聽 **通訊端** 會透過 *stat* 參數傳遞至回呼方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-115">In the following example, the listening **Socket** is passed to the callback method through the *state* parameter.</span></span> <span data-ttu-id="6cf7e-116">這個範例會建立 **AsyncCallback** 委派並開始接受來自網路的連線。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-116">This example creates an **AsyncCallback** delegate and starts accepting connections from the network.</span></span>  
  
```vb  
listener.BeginAccept( _  
    New AsyncCallback(SocketListener.AcceptCallback),_  
    listener)  
```  
  
```csharp  
listener.BeginAccept(new AsyncCallback(SocketListener.AcceptCallback), listener);  
```  
  
 <span data-ttu-id="6cf7e-117">非同步通訊端使用系統執行緒集區中的執行緒來處理連入連線。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-117">Asynchronous sockets use threads from the system thread pool to process incoming connections.</span></span> <span data-ttu-id="6cf7e-118">其中一個執行緒負責接受連線、另一個執行緒用來處理每個連入連線，還有一個執行緒負責接收來自連線的資料。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-118">One thread is responsible for accepting connections, another thread is used to handle each incoming connection, and another thread is responsible for receiving data from the connection.</span></span> <span data-ttu-id="6cf7e-119">這些可能是相同的執行緒，視執行緒集區所指派的執行緒而定。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-119">These could be the same thread, depending on which thread is assigned by the thread pool.</span></span> <span data-ttu-id="6cf7e-120">在下列範例中，<xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> 類別會暫停執行主執行緒，並在可以繼續執行時發出訊號。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-120">In the following example, the <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> class suspends execution of the main thread and signals when execution can continue.</span></span>  
  
 <span data-ttu-id="6cf7e-121">下列範例示範非同步方法，用來在本機電腦上建立非同步的 TCP/IP 通訊端，並開始接受連接。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-121">The following example shows an asynchronous method that creates an asynchronous TCP/IP socket on the local computer and begins accepting connections.</span></span> <span data-ttu-id="6cf7e-122">它假設有一個名為 `allDone` 的全域 **ManualResetEvent** 且該方法是 `SocketListener` 類別的成員，以及已定義名為 `AcceptCallback` 的回呼方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-122">It assumes that there is a global **ManualResetEvent** named `allDone`, that the method is a member of a class named `SocketListener`, and that a callback method named `AcceptCallback` is defined.</span></span>  
  
```vb  
Public Sub StartListening()  
    Dim ipHostInfo As IPHostEntry = Dns.Resolve(Dns.GetHostName())  
    Dim localEP = New IPEndPoint(ipHostInfo.AddressList(0), 11000)  
  
    Console.WriteLine($"Local address and port : {localEP.ToString()}")  
  
    Dim listener As New Socket(localEP.Address.AddressFamily, _  
       SocketType.Stream, ProtocolType.Tcp)  
  
    Try  
        listener.Bind(localEP)  
        listener.Listen(10)  
  
        While True  
            allDone.Reset()  
  
            Console.WriteLine("Waiting for a connection...")  
            listener.BeginAccept(New _  
                AsyncCallback(SocketListener.AcceptCallback), _  
                listener)  
  
            allDone.WaitOne()  
        End While  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
    Console.WriteLine("Closing the listener...")  
End Sub 'StartListening  
```  
  
```csharp  
public void StartListening()
{  
    IPHostEntry ipHostInfo = Dns.Resolve(Dns.GetHostName());  
    IPEndPoint localEP = new IPEndPoint(ipHostInfo.AddressList[0], 11000);  
  
    Console.WriteLine($"Local address and port : {localEP.ToString()}");  
  
    Socket listener = new Socket(localEP.Address.AddressFamily, SocketType.Stream, ProtocolType.Tcp);  
  
    try
    {  
        listener.Bind(localEP);  
        listener.Listen(10);  
  
        while (true)
        {  
            allDone.Reset();  
  
            Console.WriteLine("Waiting for a connection...");  
            listener.BeginAccept(new AsyncCallback(SocketListener.AcceptCallback), listener);  
  
            allDone.WaitOne();  
        }  
    }
    catch (Exception e)
    {  
        Console.WriteLine(e.ToString());  
    }  
  
    Console.WriteLine("Closing the listener...");  
}  
```  
  
 <span data-ttu-id="6cf7e-123">接受回呼方法 (在上述範例中為 `AcceptCallback`) 負責指示主要應用程式執行緒繼續處理、建立與用戶端的連線，以及開始從用戶端非同步讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-123">The accept callback method (`AcceptCallback` in the preceding example) is responsible for signaling the main application thread to continue processing, establishing the connection with the client, and starting the asynchronous read of data from the client.</span></span> <span data-ttu-id="6cf7e-124">下列範例是 `AcceptCallback` 方法實作的第一部分。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-124">The following example is the first part of an implementation of the `AcceptCallback` method.</span></span> <span data-ttu-id="6cf7e-125">該方法的這個區段會指示主要應用程式執行緒繼續處理，並建立與用戶端的連線。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-125">This section of the method signals the main application thread to continue processing and establishes the connection to the client.</span></span> <span data-ttu-id="6cf7e-126">它會假設一個名為 `allDone` 的全域 **ManualResetEvent**。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-126">It assumes a global **ManualResetEvent** named `allDone`.</span></span>  
  
```vb  
Public Sub AcceptCallback(ar As IAsyncResult)  
    allDone.Set()  
  
    Dim listener As Socket = CType(ar.AsyncState, Socket)  
    Dim handler As Socket = listener.EndAccept(ar)  
  
    ' Additional code to read data goes here.  
End Sub 'AcceptCallback  
```  
  
```csharp  
public void AcceptCallback(IAsyncResult ar)
{  
    allDone.Set();  
  
    Socket listener = (Socket) ar.AsyncState;  
    Socket handler = listener.EndAccept(ar);  
  
    // Additional code to read data goes here.
}  
```  
  
 <span data-ttu-id="6cf7e-127">從用戶端通訊端讀取資料時，需要在非同步呼叫之間傳遞值的狀態物件。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-127">Reading data from a client socket requires a state object that passes values between asynchronous calls.</span></span> <span data-ttu-id="6cf7e-128">下列範例會實作從遠端用戶端接收字串的狀態物件。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-128">The following example implements a state object for receiving a string from the remote client.</span></span> <span data-ttu-id="6cf7e-129">其包含用於用戶端通訊端的欄位、用來接收資料的資料緩衝區，以及用來建立用戶端所傳送資料字串的 <xref:System.Text.StringBuilder>。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-129">It contains fields for the client socket, a data buffer for receiving data, and a <xref:System.Text.StringBuilder> for creating the data string sent by the client.</span></span> <span data-ttu-id="6cf7e-130">將這些欄位放置在狀態物件，可允許在多個呼叫間保留其值，以從用戶端通訊端讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-130">Placing these fields in the state object allows their values to be preserved across multiple calls to read data from the client socket.</span></span>  
  
```vb  
Public Class StateObject  
    Public workSocket As Socket = Nothing  
    Public BufferSize As Integer = 1024  
    Public buffer(BufferSize) As Byte  
    Public sb As New StringBuilder()  
End Class 'StateObject  
```  
  
```csharp  
public class StateObject
{  
    public Socket workSocket = null;  
    public const int BufferSize = 1024;  
    public byte[] buffer = new byte[BufferSize];  
    public StringBuilder sb = new StringBuilder();  
}  
```  
  
 <span data-ttu-id="6cf7e-131">開始從用戶端通訊端接收資料的 `AcceptCallback` 方法的個區段首先會初始化 `StateObject` 類別的執行個體，然後呼叫 <xref:System.Net.Sockets.Socket.BeginReceive%2A> 方法，開始以非同步方式從用戶端通訊端讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-131">The section of the `AcceptCallback` method that starts receiving the data from the client socket first initializes an instance of the `StateObject` class and then calls the <xref:System.Net.Sockets.Socket.BeginReceive%2A> method to start reading the data from the client socket asynchronously.</span></span>  
  
 <span data-ttu-id="6cf7e-132">下列範例示範完整的 `AcceptCallback` 方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-132">The following example shows the complete `AcceptCallback` method.</span></span> <span data-ttu-id="6cf7e-133">它假設有一個名為 `allDone,` 的全域 **ManualResetEvent**，且其 `StateObject` 類別已定義，以及已在名為 `SocketListener` 的類別中定義 `ReadCallback` 方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-133">It assumes that there is a global **ManualResetEvent** named `allDone,` that the `StateObject` class is defined, and that the `ReadCallback` method is defined in a class named `SocketListener`.</span></span>  
  
```vb  
Public Shared Sub AcceptCallback(ar As IAsyncResult)  
    ' Get the socket that handles the client request.  
    Dim listener As Socket = CType(ar.AsyncState, Socket)  
    Dim handler As Socket = listener.EndAccept(ar)  
  
    ' Signal the main thread to continue.  
    allDone.Set()  
  
    ' Create the state object.  
    Dim state As New StateObject()  
    state.workSocket = handler  
    handler.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
        AddressOf AsynchronousSocketListener.ReadCallback, state)  
End Sub 'AcceptCallback  
```  
  
```csharp  
public static void AcceptCallback(IAsyncResult ar)
{  
    // Get the socket that handles the client request.  
    Socket listener = (Socket) ar.AsyncState;  
    Socket handler = listener.EndAccept(ar);  
  
    // Signal the main thread to continue.  
    allDone.Set();  
  
    // Create the state object.  
    StateObject state = new StateObject();  
    state.workSocket = handler;  
    handler.BeginReceive(state.buffer, 0, StateObject.BufferSize, 0,  
        new AsyncCallback(AsynchronousSocketListener.ReadCallback), state);  
}  
```  
  
 <span data-ttu-id="6cf7e-134">非同步通訊端伺服器必須實作的最後一個方法是讀取回呼方法，以傳回用戶端所傳送的資料。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-134">The final method that needs to be implemented for the asynchronous socket server is the read callback method that returns the data sent by the client.</span></span> <span data-ttu-id="6cf7e-135">如同接受回呼方法一樣，讀取回呼方法是 **AsyncCallback** 委派。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-135">Like the accept callback method, the read callback method is an **AsyncCallback** delegate.</span></span> <span data-ttu-id="6cf7e-136">這個方法會從用戶端通訊端讀取一或多個位元組到資料緩衝區，然後重新呼叫 **BeginReceive** 方法，直到用戶端所傳送的資料完整為止。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-136">This method reads one or more bytes from the client socket into the data buffer and then calls the **BeginReceive** method again until the data sent by the client is complete.</span></span> <span data-ttu-id="6cf7e-137">從用戶端讀取整個訊息後，字串就會顯示在主控台上，並關閉處理用戶端連線的伺服器通訊端。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-137">Once the entire message has been read from the client, the string is displayed on the console and the server socket handling the connection to the client is closed.</span></span>  
  
 <span data-ttu-id="6cf7e-138">下列範例會實作 `ReadCallback` 方法。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-138">The following sample implements the `ReadCallback` method.</span></span> <span data-ttu-id="6cf7e-139">它假設已定義了 `StateObject` 類別。</span><span class="sxs-lookup"><span data-stu-id="6cf7e-139">It assumes that the `StateObject` class is defined.</span></span>  
  
```vb  
Public Shared Sub ReadCallback(ar As IAsyncResult)  
    Dim state As StateObject = CType(ar.AsyncState, StateObject)  
    Dim handler As Socket = state.workSocket  
  
    ' Read data from the client socket.
    Dim read As Integer = handler.EndReceive(ar)  
  
    ' Data was read from the client socket.  
    If read > 0 Then  
        state.sb.Append(Encoding.ASCII.GetString(state.buffer, 0, read))  
        handler.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
            AddressOf ReadCallback, state)  
    Else  
        If state.sb.Length > 1 Then  
            ' All the data has been read from the client;  
            ' display it on the console.  
            Dim content As String = state.sb.ToString()  
            Console.WriteLine($"Read {content.Length} bytes from socket. {ControlChars.Cr} Data : {content}")  
        End If  
    End If  
End Sub 'ReadCallback  
```  
  
```csharp  
public static void ReadCallback(IAsyncResult ar)
{  
    StateObject state = (StateObject) ar.AsyncState;  
    Socket handler = state.WorkSocket;  
  
    // Read data from the client socket.  
    int read = handler.EndReceive(ar);  
  
    // Data was read from the client socket.  
    if (read > 0)
    {  
        state.sb.Append(Encoding.ASCII.GetString(state.buffer,0,read));  
        handler.BeginReceive(state.buffer, 0, StateObject.BufferSize, 0,  
            new AsyncCallback(ReadCallback), state);  
    }
    else
    {  
        if (state.sb.Length > 1)
        {  
            // All the data has been read from the client;  
            // display it on the console.  
            string content = state.sb.ToString();  
            Console.WriteLine($"Read {content.Length} bytes from socket.\n Data : {content}");
        }  
        handler.Close();  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="6cf7e-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6cf7e-140">See also</span></span>

- [<span data-ttu-id="6cf7e-141">使用同步伺服器通訊端</span><span class="sxs-lookup"><span data-stu-id="6cf7e-141">Using a Synchronous Server Socket</span></span>](using-a-synchronous-server-socket.md)
- [<span data-ttu-id="6cf7e-142">非同步伺服器通訊端範例</span><span class="sxs-lookup"><span data-stu-id="6cf7e-142">Asynchronous Server Socket Example</span></span>](asynchronous-server-socket-example.md)
- [<span data-ttu-id="6cf7e-143">執行緒</span><span class="sxs-lookup"><span data-stu-id="6cf7e-143">Threading</span></span>](../../standard/threading/index.md)
- [<span data-ttu-id="6cf7e-144">透過通訊端接聽</span><span class="sxs-lookup"><span data-stu-id="6cf7e-144">Listening with Sockets</span></span>](listening-with-sockets.md)
