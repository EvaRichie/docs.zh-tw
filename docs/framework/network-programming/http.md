---
title: HTTP
description: 深入瞭解 .NET Framework 使用 HttpWebRequest 和 HttpWebResponse 類別所提供的 HTTP 完整支援。
ms.date: 03/30/2017
helpviewer_keywords:
- protocols, HTTP
- sending data, HTTP
- HttpWebResponse class, sending and receiving data
- HTTP
- receiving data, HTTP
- application protocols, HTTP
- Internet, HTTP
- network resources, HTTP
- HTTP, about HTTP
- HttpWebRequest class, sending and receiving data
ms.assetid: 985fe5d8-eb71-4024-b361-41fbdc1618d8
ms.openlocfilehash: ffb7a5d027ef7691d03caf0ac45d4a3dd9bdb652
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502414"
---
# <a name="http"></a><span data-ttu-id="74665-103">HTTP</span><span class="sxs-lookup"><span data-stu-id="74665-103">HTTP</span></span>
<span data-ttu-id="74665-104">.NET Framework 可透過 <xref:System.Net.HttpWebRequest> 和 <xref:System.Net.HttpWebResponse> 類別，對於佔據所有網際網路流量絕大部分的 HTTP 通訊協定提供全面的支援。</span><span class="sxs-lookup"><span data-stu-id="74665-104">The .NET Framework provides comprehensive support for the HTTP protocol, which makes up the majority of all Internet traffic, with the <xref:System.Net.HttpWebRequest> and <xref:System.Net.HttpWebResponse> classes.</span></span> <span data-ttu-id="74665-105">這些類別衍生自 <xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse>，每當靜態方法 <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> 碰到以 "http" 或 "https" 開頭的 URI 時，預設會傳回這些類別。</span><span class="sxs-lookup"><span data-stu-id="74665-105">These classes, derived from <xref:System.Net.WebRequest> and <xref:System.Net.WebResponse>, are returned by default whenever the static method <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> encounters a URI beginning with "http" or "https".</span></span> <span data-ttu-id="74665-106">在大部分情況下，**WebRequest** 和 **WebResponse** 類別提供了提出要求所需的一切功能，但是如果您需要存取以屬性方式公開的 HTTP 特定功能，則可以將這些類別轉型為 **HttpWebRequest** 或 **HttpWebResponse**。</span><span class="sxs-lookup"><span data-stu-id="74665-106">In most cases, the **WebRequest** and **WebResponse** classes provide all that is necessary to make the request, but if you need access to the HTTP-specific features exposed as properties, you can typecast these classes to **HttpWebRequest** or **HttpWebResponse**.</span></span>  
  
 <span data-ttu-id="74665-107">**HttpWebRequest** 和 **HttpWebResponse** 封裝了標準的 HTTP 要求與回應交易，並提供對一般 HTTP 標頭的存取。</span><span class="sxs-lookup"><span data-stu-id="74665-107">**HttpWebRequest** and **HttpWebResponse** encapsulate a standard HTTP request-and-response transaction and provide access to common HTTP headers.</span></span> <span data-ttu-id="74665-108">這些類別也支援大部分的 HTTP 1.1 功能，包括管線操作、以區塊方式傳送和接收資料 、驗證、預先驗證、加密、Proxy 支援、伺服器憑證驗證，以及連線管理。</span><span class="sxs-lookup"><span data-stu-id="74665-108">These classes also support most HTTP 1.1 features, including pipelining, sending and receiving data in chunks, authentication, preauthentication, encryption, proxy support, server certificate validation, and connection management.</span></span> <span data-ttu-id="74665-109">自訂標頭和未透過屬性提供的標頭則可透過 **Headers** 屬性來儲存和存取。</span><span class="sxs-lookup"><span data-stu-id="74665-109">Custom headers and headers not provided through properties can be stored in and accessed through the **Headers** property.</span></span>  
  
 <span data-ttu-id="74665-110">**HttpWebRequest** 是 **WebRequest** 所使用的預設類別，在您將 URI 傳遞至 **WebRequest.Create** 方法之前，不需要登錄此類別。</span><span class="sxs-lookup"><span data-stu-id="74665-110">**HttpWebRequest** is the default class used by **WebRequest** and does not need to be registered before you can pass a URI to the **WebRequest.Create** method.</span></span>  
  
 <span data-ttu-id="74665-111">您可以將 <xref:System.Net.HttpWebRequest.AllowAutoRedirect%2A> 屬性設定為 **true** (預設值)，讓您的應用程式自動遵循 HTTP 重新導向。</span><span class="sxs-lookup"><span data-stu-id="74665-111">You can make your application follow HTTP redirects automatically by setting the <xref:System.Net.HttpWebRequest.AllowAutoRedirect%2A> property to **true** (the default).</span></span> <span data-ttu-id="74665-112">應用程式將重新導向要求，而 **HttpWebResponse** 的 <xref:System.Net.HttpWebResponse.ResponseUri%2A> 屬性會包含回應要求的實際 Web 資源。</span><span class="sxs-lookup"><span data-stu-id="74665-112">The application will redirect requests, and the <xref:System.Net.HttpWebResponse.ResponseUri%2A> property of **HttpWebResponse** will contain the actual Web resource that responded to the request.</span></span> <span data-ttu-id="74665-113">如果將 **AllowAutoRedirect** 設定為 **false**，則您的應用程式必須能夠處理重新導向當成 HTTP 通訊協定錯誤。</span><span class="sxs-lookup"><span data-stu-id="74665-113">If you set **AllowAutoRedirect** to **false**, your application must be able to handle redirects as HTTP protocol errors.</span></span>  
  
 <span data-ttu-id="74665-114">應用程式藉由將 <xref:System.Net.WebException.Status%2A> 設為 <xref:System.Net.WebExceptionStatus> 來捕捉 <xref:System.Net.WebException>，以便接收 HTTP 通訊協定錯誤。</span><span class="sxs-lookup"><span data-stu-id="74665-114">Applications receive HTTP protocol errors by catching a <xref:System.Net.WebException> with the <xref:System.Net.WebException.Status%2A> set to <xref:System.Net.WebExceptionStatus>.</span></span> <span data-ttu-id="74665-115"><xref:System.Net.WebException.Response%2A> 屬性包含伺服器所傳送的 **WebResponse**，並指出實際發生的 HTTP 錯誤。</span><span class="sxs-lookup"><span data-stu-id="74665-115">The <xref:System.Net.WebException.Response%2A> property contains the **WebResponse** sent by the server and indicates the actual HTTP error encountered.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="74665-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="74665-116">See also</span></span>

- [<span data-ttu-id="74665-117">透過 Proxy 存取網際網路</span><span class="sxs-lookup"><span data-stu-id="74665-117">Accessing the Internet Through a Proxy</span></span>](accessing-the-internet-through-a-proxy.md)
- [<span data-ttu-id="74665-118">使用應用程式通訊協定</span><span class="sxs-lookup"><span data-stu-id="74665-118">Using Application Protocols</span></span>](using-application-protocols.md)
- [<span data-ttu-id="74665-119">何：存取 HTTP 特定屬性</span><span class="sxs-lookup"><span data-stu-id="74665-119">How to: Access HTTP-Specific Properties</span></span>](how-to-access-http-specific-properties.md)
