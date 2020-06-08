---
title: 如何：使用 WebRequest 類別傳送資料
description: 瞭解如何使用 .NET Framework 中的 WebRequest 類別，將資料傳送至伺服器。 這個程式通常用來將資料張貼到網頁上。
ms.date: 03/25/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WebRequest class, sending data to a host
- Sending data to a host, using WebRequest class
ms.assetid: 66686878-38ac-4aa6-bf42-ffb568ffc459
ms.openlocfilehash: 4b353250fec778ee8b352f13de6d7faaf15c13ee
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502440"
---
# <a name="how-to-send-data-by-using-the-webrequest-class"></a><span data-ttu-id="19731-104">如何：使用 WebRequest 類別傳送資料</span><span class="sxs-lookup"><span data-stu-id="19731-104">How to: Send data by using the WebRequest class</span></span>

<span data-ttu-id="19731-105">下列程序描述將資料傳送到伺服器的步驟。</span><span class="sxs-lookup"><span data-stu-id="19731-105">The following procedure describes the steps to send data to a server.</span></span> <span data-ttu-id="19731-106">本程序通常用於在網頁上張貼資料。</span><span class="sxs-lookup"><span data-stu-id="19731-106">This procedure is commonly used to post data to a Web page.</span></span>

## <a name="to-send-data-to-a-host-server"></a><span data-ttu-id="19731-107">將資料傳送到主機伺服器</span><span class="sxs-lookup"><span data-stu-id="19731-107">To send data to a host server</span></span>

1. <span data-ttu-id="19731-108">使用接受資料之資源 (例如，指令碼或 ASP.NET 網頁) 的 URI 呼叫 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType>，以建立 <xref:System.Net.WebRequest> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="19731-108">Create a <xref:System.Net.WebRequest> instance by calling <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> with the URI of a resource, such as a script or ASP.NET page, that accepts data.</span></span> <span data-ttu-id="19731-109">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-109">For example:</span></span>

    ```csharp
    WebRequest request = WebRequest.Create("http://www.contoso.com/PostAccepter.aspx");
    ```

    ```vb
    Dim request as WebRequest = WebRequest.Create("http://www.contoso.com/PostAccepter.aspx")
    ```

    > [!NOTE]
    > <span data-ttu-id="19731-110">.NET Framework 針對以 *http:*、*https:*、*ftp:* 和 *file:* 開頭的 URI，提供了衍生自 <xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse> 類別的通訊協定專用類別。</span><span class="sxs-lookup"><span data-stu-id="19731-110">The .NET Framework provides protocol-specific classes derived from the <xref:System.Net.WebRequest> and <xref:System.Net.WebResponse> classes for URIs that begin with *http:*, *https:*, *ftp:*, and *file:*.</span></span>

    <span data-ttu-id="19731-111">如果您需要設定或讀取通訊協定專用屬性，必須將 <xref:System.Net.WebRequest> 或 <xref:System.Net.WebResponse> 物件轉換為通訊協定專用物件類型。</span><span class="sxs-lookup"><span data-stu-id="19731-111">If you need to set or read protocol-specific properties, you must cast your <xref:System.Net.WebRequest> or <xref:System.Net.WebResponse> object to a protocol-specific object type.</span></span> <span data-ttu-id="19731-112">如需詳細資訊，請參閱[可插式通訊協定程式設計](programming-pluggable-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="19731-112">For more information, see [Programming pluggable protocols](programming-pluggable-protocols.md).</span></span>

2. <span data-ttu-id="19731-113">在 `WebRequest` 物件中設定任何需要的屬性值。</span><span class="sxs-lookup"><span data-stu-id="19731-113">Set any property values that you need in your `WebRequest` object.</span></span> <span data-ttu-id="19731-114">例如，若要啟用驗證，請將 <xref:System.Net.WebRequest.Credentials%2A?displayProperty=nameWithType> 屬性設定為 <xref:System.Net.NetworkCredential> 類別的執行個體：</span><span class="sxs-lookup"><span data-stu-id="19731-114">For example, to enable authentication, set the <xref:System.Net.WebRequest.Credentials%2A?displayProperty=nameWithType> property to an instance of the <xref:System.Net.NetworkCredential> class:</span></span>

    ```csharp
    request.Credentials = CredentialCache.DefaultCredentials;
    ```

    ```vb
    request.Credentials = CredentialCache.DefaultCredentials
    ```

3. <span data-ttu-id="19731-115">指定允許資料與要求一起傳送的通訊協定方法，例如 HTTP `POST` 方法：</span><span class="sxs-lookup"><span data-stu-id="19731-115">Specify a protocol method that permits data to be sent with a request, such as the HTTP `POST` method:</span></span>

    ```csharp
    request.Method = "POST";
    ```

    ```vb
    request.Method = "POST"
    ```

4. <span data-ttu-id="19731-116">將 <xref:System.Web.HttpRequest.ContentLength> 屬性設定為您要求中包含的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="19731-116">Set the <xref:System.Web.HttpRequest.ContentLength> property to the number of bytes you're including with your request.</span></span> <span data-ttu-id="19731-117">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-117">For example:</span></span>

    ```csharp
    request.ContentLength = byteArray.Length;
    ```

    ```vb
    request.ContentLength = byteArray.Length
    ```

5. <span data-ttu-id="19731-118">將 <xref:System.Web.HttpRequest.ContentType> 屬性設定為適當值。</span><span class="sxs-lookup"><span data-stu-id="19731-118">Set the <xref:System.Web.HttpRequest.ContentType> property to an appropriate value.</span></span> <span data-ttu-id="19731-119">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-119">For example:</span></span>

    ```csharp
    request.ContentType = "application/x-www-form-urlencoded";
    ```

    ```vb
    request.ContentType = "application/x-www-form-urlencoded"
    ```

6. <span data-ttu-id="19731-120">藉由呼叫 <xref:System.Net.WebRequest.GetRequestStream%2A> 方法，取得保留要求資料的資料流。</span><span class="sxs-lookup"><span data-stu-id="19731-120">Get the stream that holds request data by calling the <xref:System.Net.WebRequest.GetRequestStream%2A> method.</span></span> <span data-ttu-id="19731-121">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-121">For example:</span></span>

    ```csharp
    Stream dataStream = request.GetRequestStream();
    ```

    ```vb
    Dim dataStream As Stream = request.GetRequestStream()
    ```

7. <span data-ttu-id="19731-122">將資料寫入 `GetRequestStream` 方法所傳回的 <xref:System.IO.Stream> 物件。</span><span class="sxs-lookup"><span data-stu-id="19731-122">Write the data to the <xref:System.IO.Stream> object returned by the `GetRequestStream` method.</span></span> <span data-ttu-id="19731-123">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-123">For example:</span></span>

    ```csharp
    dataStream.Write(byteArray, 0, byteArray.Length);
    ```

    ```vb
    dataStream.Write(byteArray, 0, byteArray.Length)
    ```

8. <span data-ttu-id="19731-124">呼叫 <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> 方法來關閉要求資料流。</span><span class="sxs-lookup"><span data-stu-id="19731-124">Close the request stream by calling the <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="19731-125">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-125">For example:</span></span>

    ```csharp
    dataStream.Close();
    ```

    ```vb
    dataStream.Close()
    ```

9. <span data-ttu-id="19731-126">藉由呼叫 <xref:System.Net.WebRequest.GetResponse%2A?displayProperty=nameWithType>，將要求傳送到伺服器。</span><span class="sxs-lookup"><span data-stu-id="19731-126">Send the request to the server by calling <xref:System.Net.WebRequest.GetResponse%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="19731-127">這個方法會傳回包含伺服器回應的物件。</span><span class="sxs-lookup"><span data-stu-id="19731-127">This method returns an object containing the server's response.</span></span> <span data-ttu-id="19731-128">傳回的 `WebResponse` 物件類型取決於要求 URI 的配置。</span><span class="sxs-lookup"><span data-stu-id="19731-128">The returned `WebResponse` object's type is determined by the scheme of the request's URI.</span></span> <span data-ttu-id="19731-129">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-129">For example:</span></span>

    ```csharp
    WebResponse response = request.GetResponse();
    ```

    ```vb
    Dim response As WebResponse = request.GetResponse()
    ```

10. <span data-ttu-id="19731-130">您可以存取 `WebResponse` 物件的屬性，或將其轉換為通訊協定專用執行個體，以讀取通訊協定專用屬性。</span><span class="sxs-lookup"><span data-stu-id="19731-130">You can access the properties of your `WebResponse` object or cast it to a protocol-specific instance to read protocol-specific properties.</span></span>

    <span data-ttu-id="19731-131">例如，若要存取 <xref:System.Net.HttpWebResponse> 的 HTTP 專用屬性，請將 `WebResponse` 物件轉換為 <xref:System.Net.HttpWebResponse> 參考。</span><span class="sxs-lookup"><span data-stu-id="19731-131">For example, to access the HTTP-specific properties of <xref:System.Net.HttpWebResponse>, cast your `WebResponse` object to an <xref:System.Net.HttpWebResponse> reference.</span></span> <span data-ttu-id="19731-132">下列程式碼範例示範如何顯示與回應一起傳送的 HTTP 專用 <xref:System.Net.HttpWebResponse.StatusDescription%2A?displayProperty=nameWithType> 屬性：</span><span class="sxs-lookup"><span data-stu-id="19731-132">The following code example shows how to display the HTTP-specific <xref:System.Net.HttpWebResponse.StatusDescription%2A?displayProperty=nameWithType> property sent with a response:</span></span>

    ```csharp
    Console.WriteLine(((HttpWebResponse)response).StatusDescription);
    ```

    ```vb
    Console.WriteLine(CType(response, HttpWebResponse).StatusDescription)
    ```

11. <span data-ttu-id="19731-133">若要取得含有伺服器所傳送之回應資料的資料流，請呼叫 `WebResponse` 物件的 <xref:System.Net.WebResponse.GetResponseStream%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="19731-133">To get the stream containing response data sent by the server, call the <xref:System.Net.WebResponse.GetResponseStream%2A?displayProperty=nameWithType> method of your `WebResponse` object.</span></span> <span data-ttu-id="19731-134">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-134">For example:</span></span>

    ```csharp
    Stream dataStream = response.GetResponseStream();
    ```

    ```vb
    Dim dataStream As Stream = response.GetResponseStream()
    ```

12. <span data-ttu-id="19731-135">從回應物件讀取資料之後，請使用 <xref:System.Net.WebResponse.Close%2A?displayProperty=nameWithType> 方法關閉它，或使用 <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> 方法關閉回應資料流。</span><span class="sxs-lookup"><span data-stu-id="19731-135">After you've read the data from the response object, either close it with the <xref:System.Net.WebResponse.Close%2A?displayProperty=nameWithType> method or close the response stream with the <xref:System.IO.Stream.Close%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="19731-136">如果不關閉回應或資料流，應用程式可能會耗盡伺服器連線，而變得無法處理其他要求。</span><span class="sxs-lookup"><span data-stu-id="19731-136">If you don't close either the response or the stream, your application can run out of server connections and become unable to process additional requests.</span></span> <span data-ttu-id="19731-137">`WebResponse.Close` 方法在關閉回應時會呼叫 `Stream.Close`，因此不需要對回應和資料流物件呼叫 `Close`，但是這麼做也不會造成損害。</span><span class="sxs-lookup"><span data-stu-id="19731-137">Because the `WebResponse.Close` method calls `Stream.Close` when it closes the response, it's not necessary to call `Close` on both the response and stream objects, although doing so isn't harmful.</span></span> <span data-ttu-id="19731-138">例如：</span><span class="sxs-lookup"><span data-stu-id="19731-138">For example:</span></span>

    ```csharp
    response.Close();
    ```

    ```vb
    response.Close()
    ```

## <a name="example"></a><span data-ttu-id="19731-139">範例</span><span class="sxs-lookup"><span data-stu-id="19731-139">Example</span></span>

<span data-ttu-id="19731-140">下列範例會示範如何將資料傳送到網頁伺服器，並讀取其回應中的資料：</span><span class="sxs-lookup"><span data-stu-id="19731-140">The following example shows how to send data to a web server and read the data in its response:</span></span>

[!code-csharp[SendDataUsingWebRequest](../../../samples/snippets/csharp/VS_Snippets_Network/SendDataUsingWebRequest/cs/WebRequestPostExample.cs)]
[!code-vb[SendDataUsingWebRequest](../../../samples/snippets/visualbasic/VS_Snippets_Network/SendDataUsingWebRequest/vb/WebRequestPostExample.vb)]

## <a name="see-also"></a><span data-ttu-id="19731-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="19731-141">See also</span></span>

- [<span data-ttu-id="19731-142">建立網際網路要求</span><span class="sxs-lookup"><span data-stu-id="19731-142">Creating internet requests</span></span>](creating-internet-requests.md)
- [<span data-ttu-id="19731-143">在網路上使用資料流程</span><span class="sxs-lookup"><span data-stu-id="19731-143">Using streams on the network</span></span>](using-streams-on-the-network.md)
- [<span data-ttu-id="19731-144">透過 Proxy 存取網際網路</span><span class="sxs-lookup"><span data-stu-id="19731-144">Accessing the internet through a proxy</span></span>](accessing-the-internet-through-a-proxy.md)
- [<span data-ttu-id="19731-145">要求資料</span><span class="sxs-lookup"><span data-stu-id="19731-145">Requesting data</span></span>](requesting-data.md)
- [<span data-ttu-id="19731-146">如何：使用 WebRequest 類別要求資料</span><span class="sxs-lookup"><span data-stu-id="19731-146">How to: Request data by using the WebRequest class</span></span>](how-to-request-data-using-the-webrequest-class.md)
