---
title: 含 JSON 和 XML 的 AJAX 服務範例
ms.date: 03/30/2017
ms.assetid: 8ea5860d-0c42-4ae9-941a-e07efdd8e29c
ms.openlocfilehash: 8f70b6aa2e61d01a075a6edb3fe490ef593e73b0
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84575949"
---
# <a name="ajax-service-with-json-and-xml-sample"></a><span data-ttu-id="f6264-102">含 JSON 和 XML 的 AJAX 服務範例</span><span class="sxs-lookup"><span data-stu-id="f6264-102">AJAX Service with JSON and XML Sample</span></span>

<span data-ttu-id="f6264-103">這個範例會示範如何使用 Windows Communication Foundation （WCF）來建立異步 JavaScript 和 XML （AJAX）服務，以傳回 JavaScript 物件標記法（JSON）或 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="f6264-103">This sample demonstrates how to use Windows Communication Foundation (WCF) to create an Asynchronous JavaScript and XML (AJAX) service that returns either JavaScript Object Notation (JSON) or XML data.</span></span> <span data-ttu-id="f6264-104">您可以從 Web 瀏覽器用戶端使用 JavaScript 程式碼存取 AJAX 服務。</span><span class="sxs-lookup"><span data-stu-id="f6264-104">You can access an AJAX service by using JavaScript code from a Web browser client.</span></span> <span data-ttu-id="f6264-105">這個範例是以[基本 AJAX 服務](basic-ajax-service.md)範例為基礎。</span><span class="sxs-lookup"><span data-stu-id="f6264-105">This sample builds on the [Basic AJAX Service](basic-ajax-service.md) sample.</span></span>

<span data-ttu-id="f6264-106">不像其他 AJAX 範例，這個範例不會使用 ASP.NET AJAX 以及 <xref:System.Web.UI.ScriptManager> 控制項。</span><span class="sxs-lookup"><span data-stu-id="f6264-106">Unlike the other AJAX samples, this sample does not use ASP.NET AJAX and the <xref:System.Web.UI.ScriptManager> control.</span></span> <span data-ttu-id="f6264-107">使用一些額外的設定，可以透過 JavaScript 從任何 HTML 網頁存取 WCF AJAX 服務，而此案例會顯示在這裡。</span><span class="sxs-lookup"><span data-stu-id="f6264-107">With some additional configuration, WCF AJAX services can be accessed from any HTML page through JavaScript, and this scenario is shown here.</span></span> <span data-ttu-id="f6264-108">如需搭配使用 WCF 與 ASP.NET AJAX 的範例，請參閱[AJAX 範例](ajax.md)。</span><span class="sxs-lookup"><span data-stu-id="f6264-108">For an example of using WCF with ASP.NET AJAX, see [AJAX Samples](ajax.md).</span></span>

<span data-ttu-id="f6264-109">這個範例會示範如何從 JSON 和 XML 之間切換作業的回應型別。</span><span class="sxs-lookup"><span data-stu-id="f6264-109">This sample shows how to switch the response type of an operation between JSON and XML.</span></span> <span data-ttu-id="f6264-110">不論是設定由 ASP.NET AJAX 或 HTML/JavaScript 用戶端頁面存取此服務，這項功能都會提供使用。</span><span class="sxs-lookup"><span data-stu-id="f6264-110">This functionality is available regardless of whether the service is configured to be accessed by ASP.NET AJAX or by an HTML/JavaScript client page.</span></span>

> [!NOTE]
> <span data-ttu-id="f6264-111">此範例的安裝程序與建置指示位於本主題的結尾。</span><span class="sxs-lookup"><span data-stu-id="f6264-111">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>

<span data-ttu-id="f6264-112">若要啟用非 ASP.NET AJAX 用戶端，請使用 .svc 檔案中的 <xref:System.ServiceModel.Activation.WebServiceHostFactory> (而非 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>)。</span><span class="sxs-lookup"><span data-stu-id="f6264-112">To enable the use of non-ASP.NET AJAX clients, use <xref:System.ServiceModel.Activation.WebServiceHostFactory> (not <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>) in the .svc file.</span></span> <span data-ttu-id="f6264-113"><xref:System.ServiceModel.Activation.WebServiceHostFactory> 會將 <xref:System.ServiceModel.Description.WebHttpEndpoint> 標準端點加入至服務。</span><span class="sxs-lookup"><span data-stu-id="f6264-113"><xref:System.ServiceModel.Activation.WebServiceHostFactory> adds a <xref:System.ServiceModel.Description.WebHttpEndpoint> standard endpoint to the service.</span></span> <span data-ttu-id="f6264-114">端點是在與 .svc 檔相對的空白位址上設定;這表示服務的位址是 `http://localhost/ServiceModelSamples/service.svc` ，沒有作業名稱以外的其他尾碼。</span><span class="sxs-lookup"><span data-stu-id="f6264-114">The endpoint is configured at an empty address relative to the .svc file; this means that the address of the service is `http://localhost/ServiceModelSamples/service.svc`, with no additional suffixes other than the operation name.</span></span>

`<%@ServiceHost language="c#" Debug="true" Service="Microsoft.Samples.XmlAjaxService.CalculatorService" Factory="System.ServiceModel.Activation.WebServiceHostFactory" %>`

<span data-ttu-id="f6264-115">Web.config 中的以下區段可用來針對端點進行其他組態變更。</span><span class="sxs-lookup"><span data-stu-id="f6264-115">The following section in Web.config can be used to make additional configuration changes to the endpoint.</span></span> <span data-ttu-id="f6264-116">如果不需要額外的變更，也可以加以移除。</span><span class="sxs-lookup"><span data-stu-id="f6264-116">It can be removed if no extra changes are needed.</span></span>

```xml
<system.serviceModel>
  <standardEndpoints>
    <webHttpEndpoint>
      <!-- Use this element to configure the endpoint -->
      <standardEndpoint name="" />
    </webHttpEndpoint>
  </standardEndpoints>
</system.serviceModel>
```

<span data-ttu-id="f6264-117">的預設資料格式為 <xref:System.ServiceModel.Description.WebHttpEndpoint> XML，而的預設資料格式為 <xref:System.ServiceModel.Description.WebScriptEndpoint> JSON。</span><span class="sxs-lookup"><span data-stu-id="f6264-117">The default data format for <xref:System.ServiceModel.Description.WebHttpEndpoint> is XML, while the default data format for <xref:System.ServiceModel.Description.WebScriptEndpoint> is JSON.</span></span> <span data-ttu-id="f6264-118">如需詳細資訊，請參閱[建立 WCF AJAX 服務而不 ASP.NET](../feature-details/creating-wcf-ajax-services-without-aspnet.md)。</span><span class="sxs-lookup"><span data-stu-id="f6264-118">For more information, see [Creating WCF AJAX Services without ASP.NET](../feature-details/creating-wcf-ajax-services-without-aspnet.md).</span></span>

<span data-ttu-id="f6264-119">下列範例中的服務是具有兩項作業的標準 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="f6264-119">The service in the following sample is a standard WCF service with two operations.</span></span> <span data-ttu-id="f6264-120">這兩種作業的 <xref:System.ServiceModel.Web.WebMessageBodyStyle.Wrapped> 或 <xref:System.ServiceModel.Web.WebGetAttribute> 屬性上都必須是 <xref:System.ServiceModel.Web.WebInvokeAttribute> 本文樣式，這是 `webHttp` 行為的特定需求，而且不會影響 JSON/XML 資料格式切換。</span><span class="sxs-lookup"><span data-stu-id="f6264-120">Both operations require the <xref:System.ServiceModel.Web.WebMessageBodyStyle.Wrapped> body style on the <xref:System.ServiceModel.Web.WebGetAttribute> or <xref:System.ServiceModel.Web.WebInvokeAttribute> attributes, which is specific to the `webHttp` behavior and has no bearing on the JSON/XML data format switch.</span></span>

```csharp
[OperationContract]
[WebInvoke(ResponseFormat = WebMessageFormat.Xml, BodyStyle = WebMessageBodyStyle.Wrapped)]
MathResult DoMathXml(double n1, double n2);
```

<span data-ttu-id="f6264-121">作業的回應格式會指定為 XML，這是行為的預設設定 [\<webHttp>](../../configure-apps/file-schema/wcf/webhttp.md) 。</span><span class="sxs-lookup"><span data-stu-id="f6264-121">The response format for the operation is specified as XML, which is the default setting for the [\<webHttp>](../../configure-apps/file-schema/wcf/webhttp.md) behavior.</span></span> <span data-ttu-id="f6264-122">然而，明確指定回應格式是較好的做法。</span><span class="sxs-lookup"><span data-stu-id="f6264-122">However, it is good practice explicitly specify the response format.</span></span>

<span data-ttu-id="f6264-123">其他作業會使用 `WebInvokeAttribute` 屬性，並且明確地指定回應型別為 JSON 而不是 XML。</span><span class="sxs-lookup"><span data-stu-id="f6264-123">The other operation uses the `WebInvokeAttribute` attribute and explicitly specifies JSON instead of XML for the response.</span></span>

```csharp
[OperationContract]
[WebInvoke(ResponseFormat = WebMessageFormat.Json, BodyStyle = WebMessageBodyStyle.Wrapped)]
MathResult DoMathJson(double n1, double n2);
```

<span data-ttu-id="f6264-124">請注意，在這兩種情況下，作業都會傳回復雜型別， `MathResult` 這是標準的 WCF 資料合約型別。</span><span class="sxs-lookup"><span data-stu-id="f6264-124">Note that in both cases the operations return a complex type, `MathResult`, which is a standard WCF data contract type.</span></span>

<span data-ttu-id="f6264-125">用戶端網頁 Xmlajaxclientpage.htm 包含 JavaScript 程式碼，它會在使用者按一下頁面上的 [**執行計算（傳回 JSON）** ] 或 [**執行計算（傳回 XML）** ] 按鈕時，叫用上述兩項作業的其中一個。</span><span class="sxs-lookup"><span data-stu-id="f6264-125">The client Web page XmlAjaxClientPage.htm contains JavaScript code that invokes one of the preceding two operations when the user clicks the **Perform calculation (return JSON)** or **Perform calculation (return XML)** buttons on the page.</span></span> <span data-ttu-id="f6264-126">叫用此服務的程式碼會建構 JSON 本文，然後使用 HTTP POST 加以傳送。</span><span class="sxs-lookup"><span data-stu-id="f6264-126">The code to invoke the service constructs a JSON body and sends it using HTTP POST.</span></span> <span data-ttu-id="f6264-127">在 JavaScript 中，會以手動方式建立要求，不同于[基本 AJAX 服務](basic-ajax-service.md)範例，以及使用 ASP.NET AJAX 的其他範例。</span><span class="sxs-lookup"><span data-stu-id="f6264-127">The request is created manually in JavaScript, unlike the [Basic AJAX Service](basic-ajax-service.md) sample and the other samples using ASP.NET AJAX.</span></span>

```csharp
// Create HTTP request
var xmlHttp;
// Request instantiation code omitted…
// Result handler code omitted…

// Build the operation URL
var url = "service.svc/ajaxEndpoint/";
url = url + operation;

// Build the body of the JSON message
var body = '{"n1":';
body = body + document.getElementById("num1").value + ',"n2":';
body = body + document.getElementById("num2").value + '}';

// Send the HTTP request
xmlHttp.open("POST", url, true);
xmlHttp.setRequestHeader("Content-type", "application/json");
xmlHttp.send(body);
```

<span data-ttu-id="f6264-128">當服務回應時，回應會不經任何處理地顯示在頁面的文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="f6264-128">When the service responds, the response is displayed without any further processing in a textbox on the page.</span></span> <span data-ttu-id="f6264-129">這麼做是為了示範，以便您可直接觀察所使用的 XML 和 JSON 資料格式。</span><span class="sxs-lookup"><span data-stu-id="f6264-129">This is implemented for demonstration purposes to allow you to directly observe the XML and JSON data formats used.</span></span>

```javascript
// Create result handler
xmlHttp.onreadystatechange=function(){
     if(xmlHttp.readyState == 4){
          document.getElementById("result").value = xmlHttp.responseText;
     }
}
```

> [!IMPORTANT]
> <span data-ttu-id="f6264-130">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f6264-130">The samples may already be installed on your machine.</span></span> <span data-ttu-id="f6264-131">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="f6264-131">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="f6264-132">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="f6264-132">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="f6264-133">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="f6264-133">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\AJAX\XmlAjaxService`

#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="f6264-134">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="f6264-134">To set up, build, and run the sample</span></span>

1. <span data-ttu-id="f6264-135">請確定您已[針對 Windows Communication Foundation 範例執行一次安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="f6264-135">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](one-time-setup-procedure-for-the-wcf-samples.md).</span></span>

2. <span data-ttu-id="f6264-136">如[建立 Windows Communication Foundation 範例](building-the-samples.md)中所述，建立方案 XmlAjaxService。</span><span class="sxs-lookup"><span data-stu-id="f6264-136">Build the solution XmlAjaxService.sln as described in [Building the Windows Communication Foundation Samples](building-the-samples.md).</span></span>

3. <span data-ttu-id="f6264-137">流覽至 `http://localhost/ServiceModelSamples/XmlAjaxClientPage.htm` （請勿在瀏覽器中從專案目錄開啟 xmlajaxclientpage.htm）。</span><span class="sxs-lookup"><span data-stu-id="f6264-137">Navigate to `http://localhost/ServiceModelSamples/XmlAjaxClientPage.htm` (do not open XmlAjaxClientPage.htm in the browser from the project directory).</span></span>

## <a name="see-also"></a><span data-ttu-id="f6264-138">請參閱</span><span class="sxs-lookup"><span data-stu-id="f6264-138">See also</span></span>

- [<span data-ttu-id="f6264-139">使用 HTTP POST 的 AJAX 服務</span><span class="sxs-lookup"><span data-stu-id="f6264-139">AJAX Service Using HTTP POST</span></span>](ajax-service-using-http-post.md)
