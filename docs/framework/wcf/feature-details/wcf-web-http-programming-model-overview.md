---
title: WCF Web HTTP 程式設計模型概觀
ms.date: 03/30/2017
ms.assetid: 381fdc3a-6e6c-4890-87fe-91cca6f4b476
ms.openlocfilehash: 713dd05daa5071f253afd70e735475e49a986aa7
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96239012"
---
# <a name="wcf-web-http-programming-model-overview"></a><span data-ttu-id="f7017-102">WCF Web HTTP 程式設計模型概觀</span><span class="sxs-lookup"><span data-stu-id="f7017-102">WCF Web HTTP Programming Model Overview</span></span>

<span data-ttu-id="f7017-103">WCF) WEB HTTP 程式設計模型 Windows Communication Foundation (提供使用 WCF 建立 WEB HTTP 服務所需的基本元素。</span><span class="sxs-lookup"><span data-stu-id="f7017-103">The Windows Communication Foundation (WCF) WEB HTTP programming model provides the basic elements required to build WEB HTTP services with WCF.</span></span> <span data-ttu-id="f7017-104">WCF WEB HTTP 服務是設計來供最廣泛的可能用戶端（包括網頁瀏覽器）存取，並具有下列獨特需求：</span><span class="sxs-lookup"><span data-stu-id="f7017-104">WCF WEB HTTP services are designed to be accessed by the widest range of possible clients, including Web browsers and have the following unique requirements:</span></span>  
  
- <span data-ttu-id="f7017-105">**Uri 和 Uri 處理** Uri 在 WEB HTTP 服務的設計中扮演集中角色。</span><span class="sxs-lookup"><span data-stu-id="f7017-105">**URIs and URI Processing** URIs play a central role in the design of WEB HTTP services.</span></span> <span data-ttu-id="f7017-106">WCF WEB HTTP 程式設計模型使用 <xref:System.UriTemplate> 和 <xref:System.UriTemplateTable> 類別來提供 URI 處理功能。</span><span class="sxs-lookup"><span data-stu-id="f7017-106">The WCF WEB HTTP programming model uses the <xref:System.UriTemplate> and <xref:System.UriTemplateTable> classes to provide URI processing capabilities.</span></span>  
  
- <span data-ttu-id="f7017-107">**對 GET 和 POST 作業的支援** 除了資料修改和遠端叫用的各種調用動詞命令之外，WEB HTTP 服務還會使用 GET 動詞命令來進行資料抓取。</span><span class="sxs-lookup"><span data-stu-id="f7017-107">**Support for GET and POST operations** WEB HTTP services make use of the GET verb for data retrieval, in addition to various invoke verbs for data modification and remote invocation.</span></span> <span data-ttu-id="f7017-108">WCF WEB HTTP 程式設計模型使用 <xref:System.ServiceModel.Web.WebGetAttribute> 和， <xref:System.ServiceModel.Web.WebInvokeAttribute> 將服務作業與 GET 和其他 HTTP 動詞（例如 PUT、POST 和 DELETE）產生關聯。</span><span class="sxs-lookup"><span data-stu-id="f7017-108">The WCF WEB HTTP programming model uses the <xref:System.ServiceModel.Web.WebGetAttribute> and <xref:System.ServiceModel.Web.WebInvokeAttribute> to associate service operations with both GET and other HTTP verbs like PUT, POST, and DELETE.</span></span>  
  
- <span data-ttu-id="f7017-109">**多種資料格式** 除了 SOAP 訊息之外，Web 樣式服務還會處理許多種類的資料。</span><span class="sxs-lookup"><span data-stu-id="f7017-109">**Multiple data formats** Web-style services process many kinds of data in addition to SOAP messages.</span></span> <span data-ttu-id="f7017-110">WCF WEB HTTP 程式設計模型使用 <xref:System.ServiceModel.WebHttpBinding> 和 <xref:System.ServiceModel.Description.WebHttpBehavior> 來支援許多不同的資料格式，包括 XML 檔、JSON 資料物件，以及二進位內容（例如影像、影片檔案或純文字）的資料流程。</span><span class="sxs-lookup"><span data-stu-id="f7017-110">The WCF WEB HTTP programming model uses the <xref:System.ServiceModel.WebHttpBinding> and <xref:System.ServiceModel.Description.WebHttpBehavior> to support many different data formats including XML documents, JSON data object, and streams of binary content such as images, video files, or plain text.</span></span>  
  
 <span data-ttu-id="f7017-111">WCF WEB HTTP 程式設計模型可延伸 WCF 的範圍，以涵蓋 Web 樣式案例，包括 WEB HTTP 服務、AJAX 和 JSON 服務，以及新聞訂閱 (ATOM/RSS) 摘要。</span><span class="sxs-lookup"><span data-stu-id="f7017-111">The WCF WEB HTTP programming model extends the reach of WCF to cover Web-style scenarios that include WEB HTTP services, AJAX and JSON services, and Syndication (ATOM/RSS) feeds.</span></span> <span data-ttu-id="f7017-112">如需 AJAX 和 JSON 服務的詳細資訊，請參閱 [Ajax 整合與 Json 支援](ajax-integration-and-json-support.md)。</span><span class="sxs-lookup"><span data-stu-id="f7017-112">For more information about AJAX and JSON services, see [AJAX Integration and JSON Support](ajax-integration-and-json-support.md).</span></span> <span data-ttu-id="f7017-113">如需有關摘要整合的詳細資訊，請參閱 WCF 新聞訂閱 [總覽](wcf-syndication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f7017-113">For more information about Syndication, see [WCF Syndication Overview](wcf-syndication-overview.md).</span></span>  
  
 <span data-ttu-id="f7017-114">可從 WEB HTTP 服務傳回的資料型別沒有額外的限制。</span><span class="sxs-lookup"><span data-stu-id="f7017-114">There are no extra restrictions on the types of data that can be returned from a WEB HTTP service.</span></span> <span data-ttu-id="f7017-115">WEB HTTP 服務作業可傳回任何可序列化型別。</span><span class="sxs-lookup"><span data-stu-id="f7017-115">Any serializable type can be returned from an WEB HTTP service operation.</span></span> <span data-ttu-id="f7017-116">因為 WEB HTTP 服務作業可由 Web 瀏覽器叫用，所以可在 URL 中指定的資料型別具有一項限制。</span><span class="sxs-lookup"><span data-stu-id="f7017-116">Because WEB HTTP service operations can be invoke by a web browser there is a limitation on what data types can be specified in a URL.</span></span> <span data-ttu-id="f7017-117">如需預設支援哪些類型的詳細資訊，請參閱下面的 **UriTemplate 查詢字串參數和 url** 一節。</span><span class="sxs-lookup"><span data-stu-id="f7017-117">For more information on what types are supported by default see the **UriTemplate Query String Parameters and URLs** section below.</span></span> <span data-ttu-id="f7017-118">您可以提供自己的 T:System.ServiceModel.Dispatcher.QueryStringConverter 實作來變更預設行為，其中指定如何將 URL 中指定的參數轉換成實際的參數型別。</span><span class="sxs-lookup"><span data-stu-id="f7017-118">The default behavior can be changed by providing your own T:System.ServiceModel.Dispatcher.QueryStringConverter implementation which specifies how to convert the parameters specified in a URL to the actual parameter type.</span></span> <span data-ttu-id="f7017-119">如需詳細資訊，請參閱<xref:System.ServiceModel.Dispatcher.QueryStringConverter>。</span><span class="sxs-lookup"><span data-stu-id="f7017-119">For more information, see <xref:System.ServiceModel.Dispatcher.QueryStringConverter></span></span>  
  
> [!CAUTION]
> <span data-ttu-id="f7017-120">使用 WCF WEB HTTP 程式設計模型所撰寫的服務不會使用 SOAP 訊息。</span><span class="sxs-lookup"><span data-stu-id="f7017-120">Services written with the WCF WEB HTTP programming model do not use SOAP messages.</span></span> <span data-ttu-id="f7017-121">因為不使用 SOAP，所以無法使用 WCF 提供的安全性功能。</span><span class="sxs-lookup"><span data-stu-id="f7017-121">Because SOAP is not used, the security features provided by WCF cannot be used.</span></span> <span data-ttu-id="f7017-122">不過，您可透過以 HTTPS 裝載服務的方式來使用傳輸型安全性。</span><span class="sxs-lookup"><span data-stu-id="f7017-122">You can, however use transport-based security by hosting your service with HTTPS.</span></span> <span data-ttu-id="f7017-123">如需 WCF 安全性的詳細資訊，請參閱 [安全性概觀](security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f7017-123">For more information about WCF security, see [Security Overview](security-overview.md)</span></span>  
  
> [!WARNING]
> <span data-ttu-id="f7017-124">安裝適用於 IIS 的 WebDAV 延伸模組可能會導致 Web HTTP 服務傳回 HTTP 405 錯誤，因為 WebDAV 延伸模組會嘗試處理所有 PUT 要求。</span><span class="sxs-lookup"><span data-stu-id="f7017-124">Installing the WebDAV extension for IIS can cause Web HTTP services to return an HTTP 405 error as the WebDAV extension attempts to handle all PUT requests.</span></span> <span data-ttu-id="f7017-125">若要解決此問題，您可以解除安裝 WebDAV 延伸模組或停用網站的 WebDAV 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="f7017-125">To work around this issue you can uninstall the WebDAV extension or disable the WebDAV extension for your web site.</span></span> <span data-ttu-id="f7017-126">如需詳細資訊，請參閱 [IIS 和 WebDav](https://learn.iis.net/page.aspx/357/webdav-for-iis-70/)</span><span class="sxs-lookup"><span data-stu-id="f7017-126">For more information, see [IIS and WebDav](https://learn.iis.net/page.aspx/357/webdav-for-iis-70/)</span></span>  
  
## <a name="uri-processing-with-uritemplate-and-uritemplatetable"></a><span data-ttu-id="f7017-127">使用 UriTemplate 和 UriTemplateTable 來進行 URI 處理</span><span class="sxs-lookup"><span data-stu-id="f7017-127">URI Processing with UriTemplate and UriTemplateTable</span></span>  

 <span data-ttu-id="f7017-128">URI 範本提供一個有效的語法，以便表示大量結構上類似的 URI 集合。</span><span class="sxs-lookup"><span data-stu-id="f7017-128">URI templates provide an efficient syntax for expressing large sets of structurally similar URIs.</span></span> <span data-ttu-id="f7017-129">例如，下列範本會表示以 "a" 開頭及以 "c" 結尾的所有三段式 URI 集合 (不論是否有中繼區段：a/{segment}/c)。</span><span class="sxs-lookup"><span data-stu-id="f7017-129">For example, the following template expresses the set of all three-segment URIs that begin with "a" and end with "c" without regard to the value of the intermediate segment: a/{segment}/c</span></span>  
  
 <span data-ttu-id="f7017-130">此範本會說明類似下列的 URI：</span><span class="sxs-lookup"><span data-stu-id="f7017-130">This template describes URIs like the following:</span></span>  
  
- <span data-ttu-id="f7017-131">a/x/c</span><span class="sxs-lookup"><span data-stu-id="f7017-131">a/x/c</span></span>  
  
- <span data-ttu-id="f7017-132">a/y/c</span><span class="sxs-lookup"><span data-stu-id="f7017-132">a/y/c</span></span>  
  
- <span data-ttu-id="f7017-133">a/z/c</span><span class="sxs-lookup"><span data-stu-id="f7017-133">a/z/c</span></span>  
  
- <span data-ttu-id="f7017-134">依此類推。</span><span class="sxs-lookup"><span data-stu-id="f7017-134">and so on.</span></span>  
  
 <span data-ttu-id="f7017-135">在此範本中，大括號標記法 ("{segment}") 表示變數區段，而不是常值。</span><span class="sxs-lookup"><span data-stu-id="f7017-135">In this template, the curly brace notation ("{segment}") indicates a variable segment instead of a literal value.</span></span>  
  
 <span data-ttu-id="f7017-136">.NET Framework 提供可以使用 <xref:System.UriTemplate> 這種 URI 範本的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f7017-136">.NET Framework provides an API for working with URI templates called <xref:System.UriTemplate>.</span></span> <span data-ttu-id="f7017-137">`UriTemplates` 可讓您執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="f7017-137">`UriTemplates` allow you to do the following:</span></span>  
  
- <span data-ttu-id="f7017-138">您可以 `Bind` 使用一組參數來呼叫其中一個方法，以產生符合範本的 *完整關閉 URI* 。</span><span class="sxs-lookup"><span data-stu-id="f7017-138">You can call one of the `Bind` methods with a set of parameters to produce a *fully-closed URI* that matches the template.</span></span> <span data-ttu-id="f7017-139">意思就是，URI 範本中的所有變數都會以實際值來取代。</span><span class="sxs-lookup"><span data-stu-id="f7017-139">This means all variables within the URI template are replaced with actual values.</span></span>  
  
- <span data-ttu-id="f7017-140">您可以使用候選 URI 來呼叫 `Match`()，以便透過範本將候選 URI 切割為自身的構成部分，並傳回包含不同的 URI (已依據範本中的變數加上標籤) 部分的字典。</span><span class="sxs-lookup"><span data-stu-id="f7017-140">You can call `Match`() with a candidate URI, which uses a template to break up a candidate URI into its constituent parts and returns a dictionary that contains the different parts of the URI labeled according to the variables in the template.</span></span>  
  
- <span data-ttu-id="f7017-141">`Bind`() 和 `Match`() 都是反向值，因此您可以呼叫 `Match`( `Bind`( x ) ) 並從一開始的相同環境重新開始。</span><span class="sxs-lookup"><span data-stu-id="f7017-141">`Bind`() and `Match`() are inverses so that you can call `Match`( `Bind`( x ) ) and come back with the same environment you started with.</span></span>  
  
 <span data-ttu-id="f7017-142">在許多情況下 (特別是在伺服器上，需要根據 URI 將要求分派到服務作業時) 您都想要追蹤資料結構中可以獨立處理每一個包含的範本的 <xref:System.UriTemplate> 物件集合。</span><span class="sxs-lookup"><span data-stu-id="f7017-142">There are many times (especially on the server, where dispatching a request to a service operation based on the URI is necessary) that you want to keep track of a set of <xref:System.UriTemplate> objects in a data structure that can independently address each of the contained templates.</span></span> <span data-ttu-id="f7017-143"><xref:System.UriTemplateTable> 表示一組 URI 範本，並且依據一組指定的範本及候選 URI 選取最佳對象。</span><span class="sxs-lookup"><span data-stu-id="f7017-143"><xref:System.UriTemplateTable> represents a set of URI templates and selects the best match given a set of templates and a candidate URI.</span></span> <span data-ttu-id="f7017-144">這不會與任何特定的網路堆疊關聯 (WCF 包含) 因此您可以在必要時使用它。</span><span class="sxs-lookup"><span data-stu-id="f7017-144">This is not affiliated with any particular networking stack (WCF included) so you can use it wherever necessary.</span></span>  
  
 <span data-ttu-id="f7017-145">WCF 服務模型會透過 <xref:System.UriTemplate> 和 <xref:System.UriTemplateTable> 將服務作業與 <xref:System.UriTemplate> 所描述的 URI 集合關聯在一起。</span><span class="sxs-lookup"><span data-stu-id="f7017-145">The WCF Service Model makes use of <xref:System.UriTemplate> and <xref:System.UriTemplateTable> to associate service operations with a set of URIs described by a <xref:System.UriTemplate>.</span></span> <span data-ttu-id="f7017-146">服務作業會透過 <xref:System.UriTemplate> 或 <xref:System.ServiceModel.Web.WebGetAttribute>，與 <xref:System.ServiceModel.Web.WebInvokeAttribute> 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="f7017-146">A service operation is associated with a <xref:System.UriTemplate>, using either the <xref:System.ServiceModel.Web.WebGetAttribute> or the <xref:System.ServiceModel.Web.WebInvokeAttribute>.</span></span> <span data-ttu-id="f7017-147">如需和的詳細資訊 <xref:System.UriTemplate> <xref:System.UriTemplateTable> ，請參閱 [UriTemplate 和 UriTemplateTable](uritemplate-and-uritemplatetable.md)</span><span class="sxs-lookup"><span data-stu-id="f7017-147">For more information about <xref:System.UriTemplate> and <xref:System.UriTemplateTable>, see [UriTemplate and UriTemplateTable](uritemplate-and-uritemplatetable.md)</span></span>  
  
## <a name="webget-and-webinvoke-attributes"></a><span data-ttu-id="f7017-148">WebGet 和 WebInvoke 屬性</span><span class="sxs-lookup"><span data-stu-id="f7017-148">WebGet and WebInvoke Attributes</span></span>  

 <span data-ttu-id="f7017-149">WCF WEB HTTP 服務會使用抓取動詞 (例如 HTTP GET) ，以及各種調用動詞 (例如 HTTP POST、PUT 和 DELETE) 。</span><span class="sxs-lookup"><span data-stu-id="f7017-149">WCF WEB HTTP services make use of retrieval verbs (for example HTTP GET) in addition to various invoke verbs (for example HTTP POST, PUT, and DELETE).</span></span> <span data-ttu-id="f7017-150">WCF WEB HTTP 程式設計模型可讓服務開發人員使用和來控制與其服務作業相關聯的 URI 範本和動詞 <xref:System.ServiceModel.Web.WebGetAttribute> <xref:System.ServiceModel.Web.WebInvokeAttribute> 。</span><span class="sxs-lookup"><span data-stu-id="f7017-150">The WCF WEB HTTP programming model allows service developers to control the both the URI template and verb associated with their service operations with the <xref:System.ServiceModel.Web.WebGetAttribute> and <xref:System.ServiceModel.Web.WebInvokeAttribute>.</span></span> <span data-ttu-id="f7017-151"><xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 可讓您控制個別作業如何繫結至 URI 及與這些 URI 相關聯的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f7017-151">The <xref:System.ServiceModel.Web.WebGetAttribute> and the <xref:System.ServiceModel.Web.WebInvokeAttribute> allow you to control how individual operations get bound to URIs and the HTTP methods associated with those URIs.</span></span> <span data-ttu-id="f7017-152">例如，在下列程式碼中新增 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute>。</span><span class="sxs-lookup"><span data-stu-id="f7017-152">For example, adding <xref:System.ServiceModel.Web.WebGetAttribute> and <xref:System.ServiceModel.Web.WebInvokeAttribute> in the following code.</span></span>  
  
```csharp
[ServiceContract]  
interface ICustomer  
{  
  //"View It"  
  
  [WebGet]  
  Customer GetCustomer():  
  
  //"Do It"  
    [WebInvoke]  
  Customer UpdateCustomerName( string id,
                               string newName );  
}  
```  
  
 <span data-ttu-id="f7017-153">先前的程式碼可讓您進行下列 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="f7017-153">The preceding code allows you to make the following HTTP requests.</span></span>  
  
 `GET /GetCustomer`  
  
 `POST /UpdateCustomerName`  
  
 <span data-ttu-id="f7017-154"><xref:System.ServiceModel.Web.WebInvokeAttribute> 會預設為 POST，但是您還是可以用它來控制其他動詞。</span><span class="sxs-lookup"><span data-stu-id="f7017-154"><xref:System.ServiceModel.Web.WebInvokeAttribute> defaults to POST but you can use it for other verbs too.</span></span>  
  
```csharp
[ServiceContract]  
interface ICustomer  
{  
  //"View It" -> HTTP GET  
    [WebGet( UriTemplate="customers/{id}" )]  
  Customer GetCustomer( string id ):  
  
  //"Do It" -> HTTP PUT  
  [WebInvoke( UriTemplate="customers/{id}", Method="PUT" )]  
  Customer UpdateCustomer( string id, Customer newCustomer );  
}  
```  
  
 <span data-ttu-id="f7017-155">若要查看使用 WCF WEB HTTP 程式設計模型之 WCF 服務的完整範例，請參閱 how [to：建立基本 Wcf WEB Http 服務](how-to-create-a-basic-wcf-web-http-service.md)</span><span class="sxs-lookup"><span data-stu-id="f7017-155">To see a complete sample of a WCF service that uses the WCF WEB HTTP programming model, see [How to: Create a Basic WCF Web HTTP Service](how-to-create-a-basic-wcf-web-http-service.md)</span></span>  
  
## <a name="uritemplate-query-string-parameters-and-urls"></a><span data-ttu-id="f7017-156">UriTemplate 查詢字串參數和 URL</span><span class="sxs-lookup"><span data-stu-id="f7017-156">UriTemplate Query String Parameters and URLs</span></span>  

 <span data-ttu-id="f7017-157">您可以輸入與服務作業關聯的 URL，透過網頁瀏覽器呼叫 Web 樣式服務。</span><span class="sxs-lookup"><span data-stu-id="f7017-157">Web-style services can be called from a Web browser by typing a URL that is associated with a service operation.</span></span> <span data-ttu-id="f7017-158">這些服務作業可接受的查詢字串參數，必須在 URL 中以字串格式指定。</span><span class="sxs-lookup"><span data-stu-id="f7017-158">These service operations may take query string parameters that must be specified in a string form within the URL.</span></span> <span data-ttu-id="f7017-159">下表說明可由 URL 傳遞的型別及採用的格式。</span><span class="sxs-lookup"><span data-stu-id="f7017-159">The following table shows the types that can be passed within a URL and the format used.</span></span>  
  
|<span data-ttu-id="f7017-160">類型</span><span class="sxs-lookup"><span data-stu-id="f7017-160">Type</span></span>|<span data-ttu-id="f7017-161">格式</span><span class="sxs-lookup"><span data-stu-id="f7017-161">Format</span></span>|  
|----------|------------|  
|<xref:System.Byte>|<span data-ttu-id="f7017-162">0 - 255</span><span class="sxs-lookup"><span data-stu-id="f7017-162">0 - 255</span></span>|  
|<xref:System.SByte>|<span data-ttu-id="f7017-163">-128 - 127</span><span class="sxs-lookup"><span data-stu-id="f7017-163">-128 - 127</span></span>|  
|<xref:System.Int16>|<span data-ttu-id="f7017-164">-32768 - 32767</span><span class="sxs-lookup"><span data-stu-id="f7017-164">-32768 - 32767</span></span>|  
|<xref:System.Int32>|<span data-ttu-id="f7017-165">-2,147,483,648 - 2,147,483,647</span><span class="sxs-lookup"><span data-stu-id="f7017-165">-2,147,483,648 - 2,147,483,647</span></span>|  
|<xref:System.Int64>|<span data-ttu-id="f7017-166">-9,223,372,036,854,775,808 - 9,223,372,036,854,775,807</span><span class="sxs-lookup"><span data-stu-id="f7017-166">-9,223,372,036,854,775,808 - 9,223,372,036,854,775,807</span></span>|  
|<xref:System.UInt16>|<span data-ttu-id="f7017-167">0 - 65535</span><span class="sxs-lookup"><span data-stu-id="f7017-167">0 - 65535</span></span>|  
|<xref:System.UInt32>|<span data-ttu-id="f7017-168">0 - 4,294,967,295</span><span class="sxs-lookup"><span data-stu-id="f7017-168">0 - 4,294,967,295</span></span>|  
|<xref:System.UInt64>|<span data-ttu-id="f7017-169">0 - 18,446,744,073,709,551,615</span><span class="sxs-lookup"><span data-stu-id="f7017-169">0 - 18,446,744,073,709,551,615</span></span>|  
|<xref:System.Single>|<span data-ttu-id="f7017-170">-3.402823e38 - 3.402823e38 (不需要指數標記法)</span><span class="sxs-lookup"><span data-stu-id="f7017-170">-3.402823e38 - 3.402823e38 (exponent notation is not required)</span></span>|  
|<xref:System.Double>|<span data-ttu-id="f7017-171">-1.79769313486232e308 - 1.79769313486232e308 (不需要指數標記法)</span><span class="sxs-lookup"><span data-stu-id="f7017-171">-1.79769313486232e308 - 1.79769313486232e308 (exponent notation is not required)</span></span>|  
|<xref:System.Char>|<span data-ttu-id="f7017-172">任何單一字元</span><span class="sxs-lookup"><span data-stu-id="f7017-172">Any single character</span></span>|  
|<xref:System.Decimal>|<span data-ttu-id="f7017-173">標準標記法中任何一個小數 (不含指數)</span><span class="sxs-lookup"><span data-stu-id="f7017-173">Any decimal in standard notation (no exponent)</span></span>|  
|<xref:System.Boolean>|<span data-ttu-id="f7017-174">True 或 False (不區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="f7017-174">True or False (case insensitive)</span></span>|  
|<xref:System.String>|<span data-ttu-id="f7017-175">任何字串 (不支援 null 字串且不會進行逸出)</span><span class="sxs-lookup"><span data-stu-id="f7017-175">Any string (null string is not supported and no escaping is done)</span></span>|  
|<xref:System.DateTime>|<span data-ttu-id="f7017-176">MM/DD/YYYY</span><span class="sxs-lookup"><span data-stu-id="f7017-176">MM/DD/YYYY</span></span><br /><br /> <span data-ttu-id="f7017-177">MM/DD/YYYY HH： MM： SS [AM&#124;PM]</span><span class="sxs-lookup"><span data-stu-id="f7017-177">MM/DD/YYYY HH:MM:SS [AM&#124;PM]</span></span><br /><br /> <span data-ttu-id="f7017-178">月/日/年</span><span class="sxs-lookup"><span data-stu-id="f7017-178">Month Day Year</span></span><br /><br /> <span data-ttu-id="f7017-179">Month Day Year HH： MM： SS [AM&#124;PM]</span><span class="sxs-lookup"><span data-stu-id="f7017-179">Month Day Year HH:MM:SS [AM&#124;PM]</span></span>|  
|<xref:System.TimeSpan>|<span data-ttu-id="f7017-180">DD.HH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="f7017-180">DD.HH:MM:SS</span></span><br /><br /> <span data-ttu-id="f7017-181">其中 DD = 天數，HH = 小時，MM = 分鐘，SS = 秒數</span><span class="sxs-lookup"><span data-stu-id="f7017-181">Where DD = Days, HH = Hours, MM = minutes, SS = Seconds</span></span>|  
|<xref:System.Guid>|<span data-ttu-id="f7017-182">GUID，例如：</span><span class="sxs-lookup"><span data-stu-id="f7017-182">A GUID, for example:</span></span><br /><br /> <span data-ttu-id="f7017-183">936DA01F-9ABD-4d9d-80C7-02AF85C822A8</span><span class="sxs-lookup"><span data-stu-id="f7017-183">936DA01F-9ABD-4d9d-80C7-02AF85C822A8</span></span>|  
|<xref:System.DateTimeOffset>|<span data-ttu-id="f7017-184">MM/DD/YYYY HH:MM:SS MM:SS</span><span class="sxs-lookup"><span data-stu-id="f7017-184">MM/DD/YYYY HH:MM:SS MM:SS</span></span><br /><br /> <span data-ttu-id="f7017-185">其中 DD = 天數，HH = 小時，MM = 分鐘，SS = 秒數</span><span class="sxs-lookup"><span data-stu-id="f7017-185">Where DD = Days, HH = Hours, MM = minutes, SS = Seconds</span></span>|  
|<span data-ttu-id="f7017-186">列舉</span><span class="sxs-lookup"><span data-stu-id="f7017-186">Enumerations</span></span>|<span data-ttu-id="f7017-187">列舉值，依下列程式碼示範的方式定義列舉。</span><span class="sxs-lookup"><span data-stu-id="f7017-187">The enumeration value for example, which defines the enumeration as shown in the following code.</span></span><br /><br /> `public enum Days{ Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };`<br /><br /> <span data-ttu-id="f7017-188">任何個別的列舉值 (或其對應的整數值) 都可以在查詢字串中指定。</span><span class="sxs-lookup"><span data-stu-id="f7017-188">Any of the individual enumeration values (or their corresponding integer values) may be specified in the query string.</span></span>|  
|<span data-ttu-id="f7017-189">具有可以在型別和字串表示之間相互轉換之 `TypeConverterAttribute` 的型別。</span><span class="sxs-lookup"><span data-stu-id="f7017-189">Types that have a `TypeConverterAttribute` that can convert the type to and from a string representation.</span></span>|<span data-ttu-id="f7017-190">取決於型別轉換子。</span><span class="sxs-lookup"><span data-stu-id="f7017-190">Depends on the Type Converter.</span></span>|  
  
## <a name="formats-and-the-wcf-web-http-programming-model"></a><span data-ttu-id="f7017-191">格式與 WCF WEB HTTP 程式設計模型</span><span class="sxs-lookup"><span data-stu-id="f7017-191">Formats and the WCF WEB HTTP Programming Model</span></span>  

 <span data-ttu-id="f7017-192">WCF WEB HTTP 程式設計模型有新的功能，可使用許多不同的資料格式。</span><span class="sxs-lookup"><span data-stu-id="f7017-192">The WCF WEB HTTP programming model has new features to work with many different data formats.</span></span> <span data-ttu-id="f7017-193">在繫結層，<xref:System.ServiceModel.WebHttpBinding> 可以讀取並寫入下列不同種類的資料：</span><span class="sxs-lookup"><span data-stu-id="f7017-193">At the binding layer, the <xref:System.ServiceModel.WebHttpBinding> can read and write the following different kinds of data:</span></span>  
  
- <span data-ttu-id="f7017-194">XML</span><span class="sxs-lookup"><span data-stu-id="f7017-194">XML</span></span>  
  
- <span data-ttu-id="f7017-195">JSON</span><span class="sxs-lookup"><span data-stu-id="f7017-195">JSON</span></span>  
  
- <span data-ttu-id="f7017-196">不透明的二進位資料流</span><span class="sxs-lookup"><span data-stu-id="f7017-196">Opaque binary streams</span></span>  
  
 <span data-ttu-id="f7017-197">這表示 WCF WEB HTTP 程式設計模型可以處理任何類型的資料，但您可能會進行程式設計 <xref:System.IO.Stream> 。</span><span class="sxs-lookup"><span data-stu-id="f7017-197">This means the WCF WEB HTTP programming model can handle any type of data but, you may be programming against <xref:System.IO.Stream>.</span></span>  
  
 <span data-ttu-id="f7017-198">.NET Framework 3.5 提供 JSON 資料的支援 (AJAX) 以及新聞訂閱摘要 (包括 ATOM 和 RSS) 。</span><span class="sxs-lookup"><span data-stu-id="f7017-198">.NET Framework 3.5 provides support for JSON data (AJAX) as well as Syndication feeds (including ATOM and RSS).</span></span> <span data-ttu-id="f7017-199">如需這些功能的詳細資訊，請參閱 [Wcf WEB HTTP 格式](wcf-web-http-formatting.md)、 [Wcf 摘要整合總覽](wcf-syndication-overview.md)，以及 [AJAX 整合和 JSON 支援](ajax-integration-and-json-support.md)。</span><span class="sxs-lookup"><span data-stu-id="f7017-199">For more information about these features, see [WCF Web HTTP Formatting](wcf-web-http-formatting.md), [WCF Syndication Overview](wcf-syndication-overview.md), and [AJAX Integration and JSON Support](ajax-integration-and-json-support.md).</span></span>  
  
## <a name="wcf-web-http-programming-model-and-security"></a><span data-ttu-id="f7017-200">WCF WEB HTTP 程式設計模型和安全性</span><span class="sxs-lookup"><span data-stu-id="f7017-200">WCF WEB HTTP Programming Model and Security</span></span>  

<span data-ttu-id="f7017-201">因為 WCF WEB HTTP 程式設計模型不支援 WS-\* 通訊協定，保護 WCF WEB HTTP 服務的唯一方法是使用 SSL 透過 HTTPS 公開服務。</span><span class="sxs-lookup"><span data-stu-id="f7017-201">Because the WCF WEB HTTP programming model does not support the WS-\* protocols, the only way to secure a WCF WEB HTTP service is to expose the service over HTTPS using SSL.</span></span> <span data-ttu-id="f7017-202">如需使用 IIS 7.0 設定 SSL 的詳細資訊，請參閱 [如何在 iis 中執行 ssl](https://support.microsoft.com/help/299875/how-to-implement-ssl-in-iis)。</span><span class="sxs-lookup"><span data-stu-id="f7017-202">For more information about setting up SSL with IIS 7.0, see [How to implement SSL in IIS](https://support.microsoft.com/help/299875/how-to-implement-ssl-in-iis).</span></span>
  
## <a name="troubleshooting-the-wcf-web-http-programming-model"></a><span data-ttu-id="f7017-203">WCF WEB HTTP 程式設計模型疑難排解</span><span class="sxs-lookup"><span data-stu-id="f7017-203">Troubleshooting the WCF WEB HTTP Programming Model</span></span>  

 <span data-ttu-id="f7017-204">當呼叫 WCF WEB HTTP 服務以使用 <xref:System.ServiceModel.Channels.ChannelFactoryBase%601> 建立通道時，<xref:System.ServiceModel.Description.WebHttpBehavior> 會使用組態檔中設定的 <xref:System.ServiceModel.EndpointAddress>，即便傳遞至 <xref:System.ServiceModel.EndpointAddress> 的 <xref:System.ServiceModel.Channels.ChannelFactoryBase%601> 是另一個值亦然。</span><span class="sxs-lookup"><span data-stu-id="f7017-204">When calling WCF WEB HTTP services using a <xref:System.ServiceModel.Channels.ChannelFactoryBase%601> to create a channel, the <xref:System.ServiceModel.Description.WebHttpBehavior> uses the <xref:System.ServiceModel.EndpointAddress> set in the configuration file even if a different <xref:System.ServiceModel.EndpointAddress> is passed to the <xref:System.ServiceModel.Channels.ChannelFactoryBase%601>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f7017-205">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f7017-205">See also</span></span>

- [<span data-ttu-id="f7017-206">WCF 新聞訂閱</span><span class="sxs-lookup"><span data-stu-id="f7017-206">WCF Syndication</span></span>](wcf-syndication.md)
- [<span data-ttu-id="f7017-207">WCF Web HTTP 程式設計物件模型</span><span class="sxs-lookup"><span data-stu-id="f7017-207">WCF Web HTTP Programming Object Model</span></span>](wcf-web-http-programming-object-model.md)
- [<span data-ttu-id="f7017-208">WCF Web HTTP 程式設計模型</span><span class="sxs-lookup"><span data-stu-id="f7017-208">WCF Web HTTP Programming Model</span></span>](wcf-web-http-programming-model.md)
