---
title: 進行非同步要求
description: 瞭解 System.Net 類別如何使用 .NET Framework 標準非同步程式設計模型，以非同步方式存取網際網路資源。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Internet, asynchronous access
- Networking
- asynchronous requests, Internet resources
- Network Resources
- WebRequest class, asynchronous access
ms.assetid: 735d3fce-f80c-437f-b02c-5c47f5739674
ms.openlocfilehash: 0af143b723c90b146dc5de8447d4a7e1866e7105
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502297"
---
# <a name="making-asynchronous-requests"></a><span data-ttu-id="586f1-103">進行非同步要求</span><span class="sxs-lookup"><span data-stu-id="586f1-103">Making Asynchronous Requests</span></span>
<span data-ttu-id="586f1-104"><xref:System.Net> 類別會使用 .NET Framework 的標準非同步程式設計模型，非同步存取網際網路資源。</span><span class="sxs-lookup"><span data-stu-id="586f1-104">The <xref:System.Net> classes use the .NET Framework's standard asynchronous programming model for asynchronous access to Internet resources.</span></span> <span data-ttu-id="586f1-105"><xref:System.Net.WebRequest> 類別的 <xref:System.Net.WebRequest.BeginGetResponse%2A> 和 <xref:System.Net.WebRequest.EndGetResponse%2A> 方法會啟動和完成網際網路資源的非同步要求。</span><span class="sxs-lookup"><span data-stu-id="586f1-105">The <xref:System.Net.WebRequest.BeginGetResponse%2A> and <xref:System.Net.WebRequest.EndGetResponse%2A> methods of the <xref:System.Net.WebRequest> class start and complete asynchronous requests for an Internet resource.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="586f1-106">在非同步回呼方法中使用同步呼叫可能會導致嚴重效能降低。</span><span class="sxs-lookup"><span data-stu-id="586f1-106">Using synchronous calls in asynchronous callback methods can result in severe performance penalties.</span></span> <span data-ttu-id="586f1-107">使用 **WebRequest** 和其子系所進行的內部要求，必須使用 <xref:System.IO.Stream.BeginRead%2A?displayProperty=nameWithType> 來讀取 <xref:System.Net.WebResponse.GetResponseStream%2A?displayProperty=nameWithType> 方法所傳回的資料流。</span><span class="sxs-lookup"><span data-stu-id="586f1-107">Internet requests made with **WebRequest** and its descendants must use <xref:System.IO.Stream.BeginRead%2A?displayProperty=nameWithType> to read the stream returned by the <xref:System.Net.WebResponse.GetResponseStream%2A?displayProperty=nameWithType> method.</span></span>  
  
 <span data-ttu-id="586f1-108">下列範例程式碼示範如何搭配使用非同步呼叫與 **WebRequest** 類別。</span><span class="sxs-lookup"><span data-stu-id="586f1-108">The following sample code demonstrates how to use asynchronous calls with the **WebRequest** class.</span></span> <span data-ttu-id="586f1-109">此範例是一種主控台程式，可從命令列接受 URI，並要求 URI 上的資源，然後將從網際網路收到的資料列印至主控台。</span><span class="sxs-lookup"><span data-stu-id="586f1-109">The sample is a console program that takes a URI from the command line, requests the resource at the URI, and then prints data to the console as it is received from the Internet.</span></span>  
  
 <span data-ttu-id="586f1-110">此程式定義兩個類別供它自己使用：**RequestState** 類別可跨非同步呼叫傳遞資料，以及 **ClientGetAsync** 類別可實作網際網路資源非同步要求。</span><span class="sxs-lookup"><span data-stu-id="586f1-110">The program defines two classes for its own use, the **RequestState** class, which passes data across asynchronous calls, and the **ClientGetAsync** class, which implements the asynchronous request to an Internet resource.</span></span>  
  
 <span data-ttu-id="586f1-111">**RequestState** 類別會跨提供要求的非同步方法呼叫來保留要求的狀態。</span><span class="sxs-lookup"><span data-stu-id="586f1-111">The **RequestState** class preserves the state of the request across calls to the asynchronous methods that service the request.</span></span> <span data-ttu-id="586f1-112">它所含的 **WebRequest** 和 <xref:System.IO.Stream> 執行個體包含目前資源要求以及基於回應而收到的資料流、所含的緩衝區包含目前從網際網路資源收到的資料，而且所含的 <xref:System.Text.StringBuilder> 包含完整回應。</span><span class="sxs-lookup"><span data-stu-id="586f1-112">It contains **WebRequest** and <xref:System.IO.Stream> instances that contain the current request to the resource and the stream received in response, a buffer that contains the data currently received from the Internet resource, and a <xref:System.Text.StringBuilder> that contains the complete response.</span></span> <span data-ttu-id="586f1-113">向 **WebRequest.BeginGetResponse** 註冊 <xref:System.AsyncCallback> 方法時，會將 **RequestState** 傳遞為 *state* 參數。</span><span class="sxs-lookup"><span data-stu-id="586f1-113">A **RequestState** is passed as the *state* parameter when the <xref:System.AsyncCallback> method is registered with **WebRequest.BeginGetResponse**.</span></span>  
  
 <span data-ttu-id="586f1-114">**ClientGetAsync** 類別實作網際網路資源非同步要求，並將產生的回應寫入主控台中。</span><span class="sxs-lookup"><span data-stu-id="586f1-114">The **ClientGetAsync** class implements an asynchronous request to an Internet resource and writes the resulting response to the console.</span></span> <span data-ttu-id="586f1-115">它包含下列清單所述的方法和屬性。</span><span class="sxs-lookup"><span data-stu-id="586f1-115">It contains the methods and properties described in the following list.</span></span>  
  
- <span data-ttu-id="586f1-116">`allDone` 屬性包含發出要求完成訊號的 <xref:System.Threading.ManualResetEvent> 類別執行個體。</span><span class="sxs-lookup"><span data-stu-id="586f1-116">The `allDone` property contains an instance of the <xref:System.Threading.ManualResetEvent> class that signals the completion of the request.</span></span>  
  
- <span data-ttu-id="586f1-117">`Main()` 方法會讀取命令列，並開始所指定網際網路資源的要求。</span><span class="sxs-lookup"><span data-stu-id="586f1-117">The `Main()` method reads the command line and begins the request for the specified Internet resource.</span></span> <span data-ttu-id="586f1-118">它會建立 **WebRequest** `wreq` 和 **RequestState** `rs`，並呼叫 **BeginGetResponse** 開始處理要求，然後呼叫 `allDone.WaitOne()` 方法，讓應用程式不會在回呼完成之前結束。</span><span class="sxs-lookup"><span data-stu-id="586f1-118">It creates the **WebRequest** `wreq` and the **RequestState** `rs`, calls **BeginGetResponse** to begin processing the request, and then calls the `allDone.WaitOne()`method so that the application will not exit until the callback is complete.</span></span> <span data-ttu-id="586f1-119">讀取來自網際網路資源的回應之後，`Main()` 會將它寫入至主控台，而且應用程式會結束。</span><span class="sxs-lookup"><span data-stu-id="586f1-119">After the response is read from the Internet resource, `Main()` writes it to the console and the application ends.</span></span>  
  
- <span data-ttu-id="586f1-120">`showusage()` 方法會寫入主控台上的範例命令列。</span><span class="sxs-lookup"><span data-stu-id="586f1-120">The `showusage()` method writes an example command line on the console.</span></span> <span data-ttu-id="586f1-121">命令列上未提供任何 URI 時，它是由 `Main()` 所呼叫。</span><span class="sxs-lookup"><span data-stu-id="586f1-121">It is called by `Main()` when no URI is provided on the command line.</span></span>  
  
- <span data-ttu-id="586f1-122">`RespCallBack()` 方法會實作網際網路要求的非同步回呼方法。</span><span class="sxs-lookup"><span data-stu-id="586f1-122">The `RespCallBack()` method implements the asynchronous callback method for the Internet request.</span></span> <span data-ttu-id="586f1-123">它會建立包含網際網路資源回應的 **WebResponse** 執行個體，並取得回應資料流，然後開始非同步地讀取資料流中的資料。</span><span class="sxs-lookup"><span data-stu-id="586f1-123">It creates the **WebResponse** instance containing the response from the Internet resource, gets the response stream, and then starts reading the data from the stream asynchronously.</span></span>  
  
- <span data-ttu-id="586f1-124">`ReadCallBack()` 方法會實作非同步回呼方法來讀取回應資料流。</span><span class="sxs-lookup"><span data-stu-id="586f1-124">The `ReadCallBack()` method implements the asynchronous callback method for reading the response stream.</span></span> <span data-ttu-id="586f1-125">它會將接收自網際網路資源的資料傳送至 **RequestState** 執行個體的 **ResponseData** 屬性，接著對回應資料流啟動另一個非同步讀取，直到不再傳回其他資料為止。</span><span class="sxs-lookup"><span data-stu-id="586f1-125">It transfers data received from the Internet resource into the **ResponseData** property of the **RequestState** instance, then starts another asynchronous read of the response stream until no more data is returned.</span></span> <span data-ttu-id="586f1-126">已讀取所有資料之後，`ReadCallBack()` 會關閉回應資料流，並呼叫 `allDone.Set()` 方法，指出整個回應存在於 **ResponseData** 中。</span><span class="sxs-lookup"><span data-stu-id="586f1-126">Once all the data has been read, `ReadCallBack()` closes the response stream and calls the `allDone.Set()` method to indicate that the entire response is present in **ResponseData**.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="586f1-127">請務必關閉所有網路資料流。</span><span class="sxs-lookup"><span data-stu-id="586f1-127">It is critical that all network streams are closed.</span></span> <span data-ttu-id="586f1-128">如果您未關閉每個要求和回應資料流，應用程式就會耗盡與該伺服器的連線，而無法處理其他要求。</span><span class="sxs-lookup"><span data-stu-id="586f1-128">If you do not close each request and response stream, your application will run out of connections to the server and be unable to process additional requests.</span></span>  
  
```csharp  
using System;  
using System.Net;  
using System.Threading;  
using System.Text;  
using System.IO;  
  
// The RequestState class passes data across async calls.  
public class RequestState  
{  
   const int BufferSize = 1024;  
   public StringBuilder RequestData;  
   public byte[] BufferRead;  
   public WebRequest Request;  
   public Stream ResponseStream;  
   // Create Decoder for appropriate enconding type.  
   public Decoder StreamDecode = Encoding.UTF8.GetDecoder();  
  
   public RequestState()  
   {  
      BufferRead = new byte[BufferSize];  
      RequestData = new StringBuilder(String.Empty);  
      Request = null;  
      ResponseStream = null;  
   }
}  
  
// ClientGetAsync issues the async request.  
class ClientGetAsync
{  
   public static ManualResetEvent allDone = new ManualResetEvent(false);  
   const int BUFFER_SIZE = 1024;  
  
   public static void Main(string[] args)
   {  
      if (args.Length < 1)
      {  
         showusage();  
         return;  
      }  
  
      // Get the URI from the command line.  
      Uri httpSite = new Uri(args[0]);  
  
      // Create the request object.  
      WebRequest wreq = WebRequest.Create(httpSite);  
  
      // Create the state object.  
      RequestState rs = new RequestState();  
  
      // Put the request into the state object so it can be passed around.  
      rs.Request = wreq;  
  
      // Issue the async request.  
      IAsyncResult r = (IAsyncResult) wreq.BeginGetResponse(  
         new AsyncCallback(RespCallback), rs);  
  
      // Wait until the ManualResetEvent is set so that the application
      // does not exit until after the callback is called.  
      allDone.WaitOne();  
  
      Console.WriteLine(rs.RequestData.ToString());  
   }  
  
   public static void showusage() {  
      Console.WriteLine("Attempts to GET a URL");  
      Console.WriteLine("\r\nUsage:");  
      Console.WriteLine("   ClientGetAsync URL");  
      Console.WriteLine("   Example:");  
      Console.WriteLine("      ClientGetAsync http://www.contoso.com/");  
   }  
  
   private static void RespCallback(IAsyncResult ar)  
   {  
      // Get the RequestState object from the async result.  
      RequestState rs = (RequestState) ar.AsyncState;  
  
      // Get the WebRequest from RequestState.  
      WebRequest req = rs.Request;  
  
      // Call EndGetResponse, which produces the WebResponse object  
      //  that came from the request issued above.  
      WebResponse resp = req.EndGetResponse(ar);
  
      //  Start reading data from the response stream.  
      Stream ResponseStream = resp.GetResponseStream();  
  
      // Store the response stream in RequestState to read
      // the stream asynchronously.  
      rs.ResponseStream = ResponseStream;  
  
      //  Pass rs.BufferRead to BeginRead. Read data into rs.BufferRead  
      IAsyncResult iarRead = ResponseStream.BeginRead(rs.BufferRead, 0,
         BUFFER_SIZE, new AsyncCallback(ReadCallBack), rs);
   }  
  
   private static void ReadCallBack(IAsyncResult asyncResult)  
   {  
      // Get the RequestState object from AsyncResult.  
      RequestState rs = (RequestState)asyncResult.AsyncState;  
  
      // Retrieve the ResponseStream that was set in RespCallback.
      Stream responseStream = rs.ResponseStream;  
  
      // Read rs.BufferRead to verify that it contains data.
      int read = responseStream.EndRead( asyncResult );  
      if (read > 0)  
      {  
         // Prepare a Char array buffer for converting to Unicode.  
         Char[] charBuffer = new Char[BUFFER_SIZE];  
  
         // Convert byte stream to Char array and then to String.  
         // len contains the number of characters converted to Unicode.  
      int len =
         rs.StreamDecode.GetChars(rs.BufferRead, 0, read, charBuffer, 0);  
  
         String str = new String(charBuffer, 0, len);  
  
         // Append the recently read data to the RequestData stringbuilder  
         // object contained in RequestState.  
         rs.RequestData.Append(  
            Encoding.ASCII.GetString(rs.BufferRead, 0, read));
  
         // Continue reading data until
         // responseStream.EndRead returns –1.  
         IAsyncResult ar = responseStream.BeginRead(
            rs.BufferRead, 0, BUFFER_SIZE,
            new AsyncCallback(ReadCallBack), rs);  
      }  
      else  
      {  
         if(rs.RequestData.Length>0)  
         {  
            //  Display data to the console.  
            string strContent;
            strContent = rs.RequestData.ToString();  
         }  
         // Close down the response stream.  
         responseStream.Close();
         // Set the ManualResetEvent so the main thread can exit.  
         allDone.Set();
      }  
      return;  
   }
}  
```  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Threading  
Imports System.Text  
Imports System.IO  
  
' The RequestState class passes data across async calls.  
Public Class RequestState  
  
      Public RequestData As New StringBuilder("")  
      Public BufferRead(1024) As Byte  
      Public Request As HttpWebRequest  
      Public ResponseStream As Stream  
      ' Create Decoder for appropriate encoding type.  
      Public StreamDecode As Decoder = Encoding.UTF8.GetDecoder()  
  
      Public Sub New  
         Request = Nothing  
         ResponseStream = Nothing  
      End Sub  
End Class  
  
' ClientGetAsync issues the async request.  
Class ClientGetAsync  
   Shared allDone As New ManualResetEvent(False)  
      Const BUFFER_SIZE As Integer = 1024  
  
    Shared Sub Main()  
        Dim Args As String() = Environment.GetCommandLineArgs()  
  
        If Args.Length < 2 Then  
            ShowUsage()  
            Return  
        End If  
  
      ' Get the URI from the command line.  
        Dim HttpSite As Uri = New Uri(Args(1))  
  
      ' Create the request object.  
        Dim wreq As HttpWebRequest = _  
           CType(WebRequest.Create(HttpSite), HttpWebRequest)  
  
      ' Create the state object.  
      Dim rs As RequestState = New RequestState()  
  
      ' Put the request into the state so it can be passed around.  
      rs.Request = wreq  
  
      ' Issue the async request.  
        Dim r As IAsyncResult = _  
           CType(wreq.BeginGetResponse( _  
           New AsyncCallback(AddressOf RespCallback), rs), IAsyncResult)  
  
      ' Wait until the ManualResetEvent is set so that the application  
      ' does not exit until after the callback is called.  
        allDone.WaitOne()  
    End Sub  
  
    Shared Sub ShowUsage()  
        Console.WriteLine("Attempts to GET a URI")  
        Console.WriteLine()  
        Console.WriteLine("Usage:")  
        Console.WriteLine("ClientGetAsync URI")  
        Console.WriteLine("Examples:")  
        Console.WriteLine("ClientGetAsync http://www.contoso.com/")  
    End Sub  
  
    Shared Sub RespCallback(ar As IAsyncResult)  
       ' Get the RequestState object from the async result.  
       Dim rs As RequestState = CType(ar.AsyncState, RequestState)  
  
       ' Get the HttpWebRequest from RequestState.  
       Dim req As HttpWebRequest= rs.Request  
  
       ' Call EndGetResponse, which returns the HttpWebResponse object  
       ' that came from the request issued above.  
       Dim resp As HttpWebResponse = _  
           CType(req.EndGetResponse(ar), HttpWebResponse)  
  
       ' Start reading data from the response stream.  
       Dim ResponseStream As Stream = resp.GetResponseStream()  
  
       ' Store the reponse stream in RequestState to read  
       ' the stream asynchronously.  
       rs.ResponseStream = ResponseStream  
  
       ' Pass rs.BufferRead to BeginRead. Read data into rs.BufferRead.  
       Dim iarRead As IAsyncResult = _  
          ResponseStream.BeginRead(rs.BufferRead, 0, BUFFER_SIZE, _  
          New AsyncCallback(AddressOf ReadCallBack), rs)  
    End Sub  
  
   Shared Sub ReadCallBack(asyncResult As IAsyncResult)  
      ' Get the RequestState object from the AsyncResult.  
      Dim rs As RequestState = CType(asyncResult.AsyncState, RequestState)  
  
      ' Retrieve the ResponseStream that was set in RespCallback.  
      Dim responseStream As Stream = rs.ResponseStream  
  
      ' Read rs.BufferRead to verify that it contains data.  
      Dim read As Integer = responseStream.EndRead( asyncResult )  
      If read > 0 Then  
         ' Prepare a Char array buffer for converting to Unicode.  
         Dim charBuffer(1024) As Char  
  
         ' Convert byte stream to Char array and then String.  
         ' len contains the number of characters converted to Unicode.  
         Dim len As Integer = _  
           rs.StreamDecode.GetChars(rs.BufferRead, 0, read, charBuffer, 0)  
         Dim str As String = new String(charBuffer, 0, len)
  
         ' Append the recently read data to the RequestData stringbuilder
         ' object contained in RequestState.  
         rs.RequestData.Append( _  
            Encoding.ASCII.GetString(rs.BufferRead, 0, read))  
  
         ' Continue reading data until responseStream.EndRead  
         ' returns –1.  
         Dim ar As IAsyncResult = _  
            responseStream.BeginRead(rs.BufferRead, 0, BUFFER_SIZE, _  
            New AsyncCallback(AddressOf ReadCallBack), rs)  
      Else  
          If rs.RequestData.Length > 1 Then  
            ' Display data to the console.  
            Dim strContent As String  
            strContent = rs.RequestData.ToString()  
            Console.WriteLine(strContent)  
         End If  
  
         ' Close down the response stream.  
         responseStream.Close()  
  
         ' Set the ManualResetEvent so the main thread can exit.  
         allDone.Set()  
      End If  
  
      Return  
   End Sub  
End Class  
```  
  
## <a name="see-also"></a><span data-ttu-id="586f1-129">另請參閱</span><span class="sxs-lookup"><span data-stu-id="586f1-129">See also</span></span>

- [<span data-ttu-id="586f1-130">要求資料</span><span class="sxs-lookup"><span data-stu-id="586f1-130">Requesting Data</span></span>](requesting-data.md)
