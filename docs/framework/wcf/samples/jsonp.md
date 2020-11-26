---
title: JSONP
ms.date: 03/30/2017
ms.assetid: c13b4d7b-dac7-4ffd-9f84-765c903511e1
ms.openlocfilehash: 9e27d4e73f43f004ac1de078db6a73cd42b24bbc
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96237660"
---
# <a name="jsonp"></a><span data-ttu-id="d50f4-102">JSONP</span><span class="sxs-lookup"><span data-stu-id="d50f4-102">JSONP</span></span>

<span data-ttu-id="d50f4-103">此範例示範如何在 WCF REST 服務中支援 JSON with Padding (JSONP)。</span><span class="sxs-lookup"><span data-stu-id="d50f4-103">This sample demonstrates how to support JSON with Padding (JSONP) in WCF REST services.</span></span> <span data-ttu-id="d50f4-104">JSONP 是一項慣例，透過在目前文件中產生指令碼標記，用來叫用 (Invoke) 跨網域指令碼。</span><span class="sxs-lookup"><span data-stu-id="d50f4-104">JSONP is a convention used to invoke cross-domain scripts by generating script tags in the current document.</span></span> <span data-ttu-id="d50f4-105">結果會傳回到指定的回呼函式 (Callback Function)。</span><span class="sxs-lookup"><span data-stu-id="d50f4-105">The result is returned in a specified callback function.</span></span> <span data-ttu-id="d50f4-106">JSONP 是以這種概念為基礎，例如 `<script src="http://..." >` 可以從任何網域評估腳本，而這些標記所抓取的腳本會在可能已定義其他函式的範圍內進行評估。</span><span class="sxs-lookup"><span data-stu-id="d50f4-106">JSONP is based on the idea that tags such as `<script src="http://..." >` can evaluate scripts from any domain and the script retrieved by those tags is evaluated within a scope in which other functions may already be defined.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="d50f4-107">示範</span><span class="sxs-lookup"><span data-stu-id="d50f4-107">Demonstrates</span></span>

 <span data-ttu-id="d50f4-108">使用 JSONP 撰寫的跨網域指令碼。</span><span class="sxs-lookup"><span data-stu-id="d50f4-108">Cross-domain scripting with JSONP.</span></span>

## <a name="discussion"></a><span data-ttu-id="d50f4-109">討論</span><span class="sxs-lookup"><span data-stu-id="d50f4-109">Discussion</span></span>

 <span data-ttu-id="d50f4-110">此範例包含的網頁會在該網頁呈現在瀏覽器中之後，以動態方式加入指令碼區塊。</span><span class="sxs-lookup"><span data-stu-id="d50f4-110">The sample includes a Web page that dynamically adds a script block after the page has been rendered in the browser.</span></span> <span data-ttu-id="d50f4-111">此指令碼區塊會呼叫具有單一作業 `GetCustomer` 的 WCF REST 服務。</span><span class="sxs-lookup"><span data-stu-id="d50f4-111">This script block calls a WCF REST service that has a single operation, `GetCustomer`.</span></span> <span data-ttu-id="d50f4-112">WCF REST 服務會傳回回呼函式名稱中所包裝的客戶名稱和位址。</span><span class="sxs-lookup"><span data-stu-id="d50f4-112">The WCF REST service returns a customer’s name and address wrapped in a callback function name.</span></span> <span data-ttu-id="d50f4-113">當 WCF REST 服務回應時，系統會使用客戶資料叫用網頁上的回呼函式，而且回呼函式會將資料顯示在網頁上。</span><span class="sxs-lookup"><span data-stu-id="d50f4-113">When the WCF REST service responds, the callback function on the Web page is invoked with the customer data and the callback function displays the data on the Web page.</span></span> <span data-ttu-id="d50f4-114">插入指令碼標記與執行回呼函式是由 ASP.NET AJAX ScriptManager 控制項自動處理。</span><span class="sxs-lookup"><span data-stu-id="d50f4-114">The injection of the script tag and the execution of the callback function is automatically handled by the ASP.NET AJAX ScriptManager control.</span></span> <span data-ttu-id="d50f4-115">使用模式與使用所有 ASP.NET AJAX Proxy 相同，但是要加入一行來啟用 JSONP，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="d50f4-115">The usage pattern is the same as with all ASP.NET AJAX proxies, with the addition of one line to enable JSONP, as shown in the following code:</span></span>

```csharp
var proxy = new JsonpAjaxService.CustomerService();
proxy.set_enableJsonp(true);
proxy.GetCustomer(onSuccess, onFail, null);
```

 <span data-ttu-id="d50f4-116">網頁可以呼叫 WCF REST 服務，因為此服務使用的是 <xref:System.ServiceModel.Description.WebScriptEndpoint>，且 `crossDomainScriptAccessEnabled` 設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="d50f4-116">The Web page can call the WCF REST service because the service is using the <xref:System.ServiceModel.Description.WebScriptEndpoint> with `crossDomainScriptAccessEnabled` set to `true`.</span></span> <span data-ttu-id="d50f4-117">這兩個設定都是在元素底下的 Web.config 檔案中完成 \<system.serviceModel> 。</span><span class="sxs-lookup"><span data-stu-id="d50f4-117">Both of these configurations are done in the Web.config file under the \<system.serviceModel> element.</span></span>

```xml
<system.serviceModel>
  <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>
  <standardEndpoints>
    <webScriptEndpoint>
      <standardEndpoint name="" crossDomainScriptAccessEnabled="true"/>
    </webScriptEndpoint>
  </standardEndpoints>
</system.serviceModel>
```

 <span data-ttu-id="d50f4-118">ScriptManager 會管理與服務的互動，並隱藏手動實作 JSONP 存取的複雜度。</span><span class="sxs-lookup"><span data-stu-id="d50f4-118">ScriptManager manages the interaction with the service and hides away the complexity of manually implementing JSONP access.</span></span> <span data-ttu-id="d50f4-119">當 `crossDomainScriptAccessEnabled` 設定為 `true` 且作業的回應格式為 JSON 時，WCF 基礎結構會檢查回呼查詢字串參數的要求 URI，並以回呼查詢字串參數的值來包裝 JSON 回應。</span><span class="sxs-lookup"><span data-stu-id="d50f4-119">When `crossDomainScriptAccessEnabled` is set to `true` and the response format for an operation is JSON, the WCF infrastructure inspects the URI of the request for a callback query string parameter and wraps the JSON response with the value of the callback query string parameter.</span></span> <span data-ttu-id="d50f4-120">在此範例中，網頁會使用下列 URI 呼叫 WCF REST 服務。</span><span class="sxs-lookup"><span data-stu-id="d50f4-120">In the sample, the Web page calls the WCF REST service with the following URI.</span></span>

```http
http://localhost:33695/CustomerService/GetCustomer?callback=Sys._json0
```

 <span data-ttu-id="d50f4-121">回呼查詢字串參數的值為 `JsonPCallback`，因此 WCF 服務會傳回 JSONP 回應，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="d50f4-121">Because the callback query string parameter has a value of `JsonPCallback`, the WCF service returns a JSONP response shown in the following example.</span></span>

```json
Sys._json0({"__type":"Customer:#Microsoft.Samples.Jsonp","Address":"1 Example Way","Name":"Bob"});
```

 <span data-ttu-id="d50f4-122">這個 JSONP 回應包含格式化為 JSON，且以網頁要求之回呼函式名稱包裝的客戶資料。</span><span class="sxs-lookup"><span data-stu-id="d50f4-122">This JSONP response includes the customer data formatted as JSON, wrapped with the callback function name that the Web page requested.</span></span> <span data-ttu-id="d50f4-123">ScriptManager 將會使用指令碼標記執行這個回呼以達成跨網域要求，然後將結果傳遞到 onSuccess 標頭，這個標頭會傳遞到 ASP.NET AJAX Proxy 的 GetCustomer 作業。</span><span class="sxs-lookup"><span data-stu-id="d50f4-123">ScriptManager will execute this callback using a script tag to accomplish the cross-domain request, and then pass the result to the onSuccess handler that was passed to the GetCustomer operation of the ASP.NET AJAX proxy.</span></span>

 <span data-ttu-id="d50f4-124">此範例包含兩個 ASP.NET web 應用程式：一個只包含 WCF 服務，另一個則包含呼叫服務的 .aspx 網頁。</span><span class="sxs-lookup"><span data-stu-id="d50f4-124">The sample consists of two ASP.NET web applications: one contains just a WCF service, and another one contains the .aspx webpage, which calls the service.</span></span> <span data-ttu-id="d50f4-125">執行解決方案時，Visual Studio 2012 會在不同的埠上裝載兩個網站，這會建立服務和用戶端存留在不同網域上的環境。</span><span class="sxs-lookup"><span data-stu-id="d50f4-125">When running the solution, Visual Studio 2012 will host the two websites on different ports, which creates an environment where the service and client live on different domains.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d50f4-126">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="d50f4-126">The samples may already be installed on your machine.</span></span> <span data-ttu-id="d50f4-127">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="d50f4-127">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="d50f4-128">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="d50f4-128">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="d50f4-129">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="d50f4-129">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\AJAX\JSONP`  
  
#### <a name="to-run-the-sample"></a><span data-ttu-id="d50f4-130">執行範例</span><span class="sxs-lookup"><span data-stu-id="d50f4-130">To run the sample</span></span>  
  
1. <span data-ttu-id="d50f4-131">開啟 JSONP 範例的方案。</span><span class="sxs-lookup"><span data-stu-id="d50f4-131">Open the solution for the JSONP Sample.</span></span>  
  
2. <span data-ttu-id="d50f4-132">按 F5 以 `http://localhost:26648/JSONPClientPage.aspx` 在瀏覽器中啟動。</span><span class="sxs-lookup"><span data-stu-id="d50f4-132">Press F5 to launch `http://localhost:26648/JSONPClientPage.aspx` in the browser.</span></span>  
  
3. <span data-ttu-id="d50f4-133">請注意，在頁面載入之後，"Name" 和 "Address" 的文字輸入會以值填入。</span><span class="sxs-lookup"><span data-stu-id="d50f4-133">Notice that after the page loads, the text inputs for "Name" and "Address" are populated by values.</span></span>  <span data-ttu-id="d50f4-134">這些值是在瀏覽器完成頁面呈現之後，從呼叫 WCF 服務所提供。</span><span class="sxs-lookup"><span data-stu-id="d50f4-134">These values were supplied from a call to the WCF service after the browser finished rendering the page.</span></span>
