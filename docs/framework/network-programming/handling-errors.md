---
title: 處理錯誤
description: 瞭解 WebRequest 和 WebResponse 擲回的系統和 web 特定例外狀況。 請使用 Status 屬性來瞭解及解決問題。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Internet, WebRequest and WebResponse classes exceptions
- Status property
- WebExceptions class, about WebExceptions class
- Timeout enumeration member
- ConnectFailure enumeration member
- TrustFailure enumeration member
- WebRequest class, exceptions
- requesting data from Internet, error handling
- Success enumeration member
- receiving data, errors
- ProtocolError enumeration member
- downloading Internet resources, error handling
- WebResponse class, exceptions
- SendFailure enumeration member
- errors [.NET Framework], WebRequest and WebResponse classes exceptions
- sending data, errors
- response to Internet request, error handling
- NameResolutionFailure enumeration member
- KeepAliveFailure enumeration member
- network resources, WebRequest and WebResponse classes exceptions
- RequestCanceled enumeration member
- ReceiveFailure enumeration member
- ServerProtocolViolation enumeration member
- ConnectionClosed enumeration member
- SecureChannelFailure enumeration member
ms.assetid: 657141cd-5cf5-4fdb-a4b2-4c040eba84b5
ms.openlocfilehash: 786b2bd8bc4d1b394bcfe920053b2f4f55d1cdea
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502570"
---
# <a name="handling-errors"></a><span data-ttu-id="87eec-104">處理錯誤</span><span class="sxs-lookup"><span data-stu-id="87eec-104">Handling Errors</span></span>

<span data-ttu-id="87eec-105"><xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse> 類別會擲回兩個系統例外狀況 (例如 <xref:System.ArgumentException>) 和 Web 特定例外狀況 (這些是 <xref:System.Net.WebRequest.GetResponse%2A> 方法所擲回的 <xref:System.Net.WebException>)。</span><span class="sxs-lookup"><span data-stu-id="87eec-105">The <xref:System.Net.WebRequest> and <xref:System.Net.WebResponse> classes throw both system exceptions (such as <xref:System.ArgumentException>) and Web-specific exceptions (which are <xref:System.Net.WebException> thrown by the <xref:System.Net.WebRequest.GetResponse%2A> method).</span></span>  
  
<span data-ttu-id="87eec-106">每個 **WebException** 包含一個 <xref:System.Net.WebException.Status%2A> 屬性，其中包含來自 <xref:System.Net.WebExceptionStatus> 列舉的值。</span><span class="sxs-lookup"><span data-stu-id="87eec-106">Each **WebException** includes a <xref:System.Net.WebException.Status%2A> property that contains a value from the <xref:System.Net.WebExceptionStatus> enumeration.</span></span> <span data-ttu-id="87eec-107">您可以檢查 **Status** 屬性來判斷發生的錯誤，並採取適當的步驟來解決這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="87eec-107">You can examine the **Status** property to determine the error that occurred and take the proper steps to resolve the error.</span></span>  
  
<span data-ttu-id="87eec-108">下表描述 **Status** 屬性的可能值。</span><span class="sxs-lookup"><span data-stu-id="87eec-108">The following table describes the possible values for the **Status** property.</span></span>  
  
|<span data-ttu-id="87eec-109">狀態</span><span class="sxs-lookup"><span data-stu-id="87eec-109">Status</span></span>|<span data-ttu-id="87eec-110">描述</span><span class="sxs-lookup"><span data-stu-id="87eec-110">Description</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="87eec-111">ConnectFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-111">ConnectFailure</span></span>|<span data-ttu-id="87eec-112">無法在傳輸層級連絡遠端服務。</span><span class="sxs-lookup"><span data-stu-id="87eec-112">The remote service could not be contacted at the transport level.</span></span>|  
|<span data-ttu-id="87eec-113">ConnectionClosed</span><span class="sxs-lookup"><span data-stu-id="87eec-113">ConnectionClosed</span></span>|<span data-ttu-id="87eec-114">連線過早關閉。</span><span class="sxs-lookup"><span data-stu-id="87eec-114">The connection was closed prematurely.</span></span>|  
|<span data-ttu-id="87eec-115">KeepAliveFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-115">KeepAliveFailure</span></span>|<span data-ttu-id="87eec-116">伺服器已關閉使用保持連線標頭集合建立的連線。</span><span class="sxs-lookup"><span data-stu-id="87eec-116">The server closed a connection made with the Keep-alive header set.</span></span>|  
|<span data-ttu-id="87eec-117">NameResolutionFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-117">NameResolutionFailure</span></span>|<span data-ttu-id="87eec-118">名稱服務無法解析主機名稱。</span><span class="sxs-lookup"><span data-stu-id="87eec-118">The name service could not resolve the host name.</span></span>|  
|<span data-ttu-id="87eec-119">ProtocolError</span><span class="sxs-lookup"><span data-stu-id="87eec-119">ProtocolError</span></span>|<span data-ttu-id="87eec-120">從伺服器收到的回應已完成，但是指出通訊協定層級發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="87eec-120">The response received from the server was complete but indicated an error at the protocol level.</span></span>|  
|<span data-ttu-id="87eec-121">ReceiveFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-121">ReceiveFailure</span></span>|<span data-ttu-id="87eec-122">未從遠端伺服器收到完整的回應。</span><span class="sxs-lookup"><span data-stu-id="87eec-122">A complete response was not received from the remote server.</span></span>|  
|<span data-ttu-id="87eec-123">RequestCanceled</span><span class="sxs-lookup"><span data-stu-id="87eec-123">RequestCanceled</span></span>|<span data-ttu-id="87eec-124">已取消要求。</span><span class="sxs-lookup"><span data-stu-id="87eec-124">The request was canceled.</span></span>|  
|<span data-ttu-id="87eec-125">SecureChannelFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-125">SecureChannelFailure</span></span>|<span data-ttu-id="87eec-126">安全通道連結發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="87eec-126">An error occurred in a secure channel link.</span></span>|  
|<span data-ttu-id="87eec-127">SendFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-127">SendFailure</span></span>|<span data-ttu-id="87eec-128">無法將完整的要求傳送到遠端伺服器。</span><span class="sxs-lookup"><span data-stu-id="87eec-128">A complete request could not be sent to the remote server.</span></span>|  
|<span data-ttu-id="87eec-129">ServerProtocolViolation</span><span class="sxs-lookup"><span data-stu-id="87eec-129">ServerProtocolViolation</span></span>|<span data-ttu-id="87eec-130">伺服器回應不是有效的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="87eec-130">The server response was not a valid HTTP response.</span></span>|  
|<span data-ttu-id="87eec-131">成功</span><span class="sxs-lookup"><span data-stu-id="87eec-131">Success</span></span>|<span data-ttu-id="87eec-132">沒有遇到任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="87eec-132">No error was encountered.</span></span>|  
|<span data-ttu-id="87eec-133">逾時</span><span class="sxs-lookup"><span data-stu-id="87eec-133">Timeout</span></span>|<span data-ttu-id="87eec-134">在針對要求所設定的逾時內未收到任何回應。</span><span class="sxs-lookup"><span data-stu-id="87eec-134">No response was received within the time-out set for the request.</span></span>|  
|<span data-ttu-id="87eec-135">TrustFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-135">TrustFailure</span></span>|<span data-ttu-id="87eec-136">無法驗證伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="87eec-136">A server certificate could not be validated.</span></span>|  
|<span data-ttu-id="87eec-137">MessageLengthLimitExceeded</span><span class="sxs-lookup"><span data-stu-id="87eec-137">MessageLengthLimitExceeded</span></span>|<span data-ttu-id="87eec-138">從伺服器傳送要求或接收回應時，收到超過指定限制的訊息。</span><span class="sxs-lookup"><span data-stu-id="87eec-138">A message was received that exceeded the specified limit when sending a request or receiving a response from the server.</span></span>|  
|<span data-ttu-id="87eec-139">Pending</span><span class="sxs-lookup"><span data-stu-id="87eec-139">Pending</span></span>|<span data-ttu-id="87eec-140">內部非同步要求正在擱置中。</span><span class="sxs-lookup"><span data-stu-id="87eec-140">An internal asynchronous request is pending.</span></span>|  
|<span data-ttu-id="87eec-141">PipelineFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-141">PipelineFailure</span></span>|<span data-ttu-id="87eec-142">此值支援 .NET Framework 基礎結構，但不能直接用於您的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="87eec-142">This value supports the .NET Framework infrastructure and is not intended to be used directly in your code.</span></span>|  
|<span data-ttu-id="87eec-143">ProxyNameResolutionFailure</span><span class="sxs-lookup"><span data-stu-id="87eec-143">ProxyNameResolutionFailure</span></span>|<span data-ttu-id="87eec-144">名稱解析服務無法解析 Proxy 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="87eec-144">The name resolver service could not resolve the proxy host name.</span></span>|  
|<span data-ttu-id="87eec-145">UnknownError</span><span class="sxs-lookup"><span data-stu-id="87eec-145">UnknownError</span></span>|<span data-ttu-id="87eec-146">發生未知類型的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="87eec-146">An exception of unknown type has occurred.</span></span>|  
  
<span data-ttu-id="87eec-147">當 **Status** 屬性是 **WebExceptionStatus.ProtocolError** 時，即可使用包含伺服器回應的 **WebResponse**。</span><span class="sxs-lookup"><span data-stu-id="87eec-147">When the **Status** property is **WebExceptionStatus.ProtocolError**, a **WebResponse** that contains the response from the server is available.</span></span> <span data-ttu-id="87eec-148">您可以檢查這個回應，以判斷實際的通訊協定錯誤來源。</span><span class="sxs-lookup"><span data-stu-id="87eec-148">You can examine this response to determine the actual source of the protocol error.</span></span>  
  
<span data-ttu-id="87eec-149">下列範例示範如何快取 **WebException**。</span><span class="sxs-lookup"><span data-stu-id="87eec-149">The following example shows how to catch a **WebException**.</span></span>  
  
```csharp  
try
{  
    // Create a request instance.  
    WebRequest myRequest =
    WebRequest.Create("http://www.contoso.com");  
    // Get the response.  
    WebResponse myResponse = myRequest.GetResponse();  
    //Get a readable stream from the server.
    Stream sr = myResponse.GetResponseStream();  
  
    //Read from the stream and write any data to the console.  
    bytesread = sr.Read( myBuffer, 0, length);  
    while( bytesread > 0 )
    {  
        for (int i=0; i<bytesread; i++) {  
            Console.Write( "{0}", myBuffer[i]);  
        }  
        Console.WriteLine();  
        bytesread = sr.Read( myBuffer, 0, length);  
    }  
    sr.Close();  
    myResponse.Close();  
}  
catch (WebException webExcp)
{  
    // If you reach this point, an exception has been caught.  
    Console.WriteLine("A WebException has been caught.");  
    // Write out the WebException message.  
    Console.WriteLine(webExcp.ToString());  
    // Get the WebException status code.  
    WebExceptionStatus status =  webExcp.Status;  
    // If status is WebExceptionStatus.ProtocolError,
    //   there has been a protocol error and a WebResponse
    //   should exist. Display the protocol error.  
    if (status == WebExceptionStatus.ProtocolError) {  
        Console.Write("The server returned protocol error ");  
        // Get HttpWebResponse so that you can check the HTTP status code.  
        HttpWebResponse httpResponse = (HttpWebResponse)webExcp.Response;  
        Console.WriteLine((int)httpResponse.StatusCode + " - "  
           + httpResponse.StatusCode);  
    }  
}  
catch (Exception e)
{  
    // Code to catch other exceptions goes here.  
}  
```  
  
```vb  
Try  
    ' Create a request instance.  
    Dim myRequest As WebRequest = WebRequest.Create("http://www.contoso.com")  
    ' Get the response.  
    Dim myResponse As WebResponse = myRequest.GetResponse()  
    'Get a readable stream from the server.
    Dim sr As Stream = myResponse.GetResponseStream()  
  
    Dim i As Integer
    'Read from the stream and write any data to the console.  
    bytesread = sr.Read(myBuffer, 0, length)  
    While bytesread > 0  
        For i = 0 To bytesread - 1  
            Console.Write("{0}", myBuffer(i))  
        Next i  
        Console.WriteLine()  
        bytesread = sr.Read(myBuffer, 0, length)  
    End While  
    sr.Close()  
    myResponse.Close()  
Catch webExcp As WebException  
    ' If you reach this point, an exception has been caught.  
    Console.WriteLine("A WebException has been caught.")  
    ' Write out the WebException message.  
    Console.WriteLine(webExcp.ToString())  
    ' Get the WebException status code.  
    Dim status As WebExceptionStatus = webExcp.Status  
    ' If status is WebExceptionStatus.ProtocolError,
    '   there has been a protocol error and a WebResponse
    '   should exist. Display the protocol error.  
    If status = WebExceptionStatus.ProtocolError Then  
        Console.Write("The server returned protocol error ")  
        ' Get HttpWebResponse so that you can check the HTTP status code.  
        Dim httpResponse As HttpWebResponse = _  
           CType(webExcp.Response, HttpWebResponse)  
        Console.WriteLine(CInt(httpResponse.StatusCode).ToString() & _  
           " - " & httpResponse.StatusCode.ToString())  
    End If  
Catch e As Exception  
    ' Code to catch other exceptions goes here.  
End Try  
```  
  
<span data-ttu-id="87eec-150">當 Windows 通訊端發生錯誤時，使用 <xref:System.Net.Sockets.Socket> 類別的應用程式會擲回 <xref:System.Net.Sockets.SocketException>。</span><span class="sxs-lookup"><span data-stu-id="87eec-150">Applications that use the <xref:System.Net.Sockets.Socket> class throw <xref:System.Net.Sockets.SocketException> when errors occur on the Windows socket.</span></span> <span data-ttu-id="87eec-151"><xref:System.Net.Sockets.TcpClient>、<xref:System.Net.Sockets.TcpListener> 和 <xref:System.Net.Sockets.UdpClient> 類別都建置在 **Socket** 類別之上，因此也會擲回 **SocketExceptions**。</span><span class="sxs-lookup"><span data-stu-id="87eec-151">The <xref:System.Net.Sockets.TcpClient>, <xref:System.Net.Sockets.TcpListener>, and <xref:System.Net.Sockets.UdpClient> classes are built on top of the **Socket** class and throw **SocketExceptions** as well.</span></span>  
  
<span data-ttu-id="87eec-152">擲回 **SocketException** 時，**SocketException** 類別會將 <xref:System.Net.Sockets.SocketException.ErrorCode%2A> 屬性設定為最後發生的作業系統通訊端錯誤。</span><span class="sxs-lookup"><span data-stu-id="87eec-152">When a **SocketException** is thrown, the **SocketException** class sets the <xref:System.Net.Sockets.SocketException.ErrorCode%2A> property to the last operating system socket error that occurred.</span></span> <span data-ttu-id="87eec-153">如需通訊端錯誤碼的詳細資訊，請參閱 MSDN 中的 Winsock 2.0 API 錯誤碼文件。</span><span class="sxs-lookup"><span data-stu-id="87eec-153">For more information about socket error codes, see the Winsock 2.0 API error code documentation in MSDN.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="87eec-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="87eec-154">See also</span></span>

- [<span data-ttu-id="87eec-155">在 .NET 中處理和擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="87eec-155">Handling and throwing exceptions in .NET</span></span>](../../standard/exceptions/index.md)
- [<span data-ttu-id="87eec-156">要求資料</span><span class="sxs-lookup"><span data-stu-id="87eec-156">Requesting Data</span></span>](requesting-data.md)
