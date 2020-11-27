---
title: SOAP 及 HTTP 端點
ms.date: 03/30/2017
ms.assetid: e3c8be75-9dda-4afa-89b6-a82cb3b73cf8
ms.openlocfilehash: 9e7ce32a0f5a2f37294db57659e2b30b364bef24
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268257"
---
# <a name="soap-and-http-endpoints"></a><span data-ttu-id="c4419-102">SOAP 及 HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="c4419-102">SOAP and HTTP Endpoints</span></span>

<span data-ttu-id="c4419-103">這個範例會示範如何使用 WCF Web 程式設計模型，以 SOAP 格式和「純舊 XML」 (POX) 格式來執行 RPC 型服務並以 SOAP 格式公開。</span><span class="sxs-lookup"><span data-stu-id="c4419-103">This sample demonstrates how to implement an RPC-based service and expose it in the SOAP format and the "Plain Old XML" (POX) format using the WCF Web Programming model.</span></span> <span data-ttu-id="c4419-104">如需服務的 HTTP 系結詳細資訊，請參閱 [基本 HTTP 服務](basic-http-service.md) 範例。</span><span class="sxs-lookup"><span data-stu-id="c4419-104">See the [Basic HTTP Service](basic-http-service.md) sample for more details about the HTTP binding for the service.</span></span> <span data-ttu-id="c4419-105">這個範例的重點在於，使用不同繫結透過 SOAP 和 HTTP 公開相同服務的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c4419-105">This sample focuses on the details that pertain to exposing the same service over SOAP and HTTP using different bindings.</span></span>  
  
## <a name="demonstrates"></a><span data-ttu-id="c4419-106">示範</span><span class="sxs-lookup"><span data-stu-id="c4419-106">Demonstrates</span></span>  

 <span data-ttu-id="c4419-107">使用 WCF 透過 SOAP 和 HTTP 公開 RPC 服務。</span><span class="sxs-lookup"><span data-stu-id="c4419-107">Exposing an RPC service over SOAP and HTTP using WCF.</span></span>  
  
## <a name="discussion"></a><span data-ttu-id="c4419-108">討論</span><span class="sxs-lookup"><span data-stu-id="c4419-108">Discussion</span></span>  

 <span data-ttu-id="c4419-109">這個範例是由兩個元件所組成：包含 WCF 服務的 Web 應用程式專案 (Service) ，以及使用 SOAP 和 HTTP 系結叫用服務作業的主控台應用程式 (用戶端) 。</span><span class="sxs-lookup"><span data-stu-id="c4419-109">This sample consists of two components: a Web Application project (Service) that contains a WCF service and a console application (Client) that invokes service operations using SOAP and HTTP bindings.</span></span>  
  
 <span data-ttu-id="c4419-110">WCF 服務會公開2個作業– `GetData` 和 `PutData` –回顯傳遞為輸入的字串。</span><span class="sxs-lookup"><span data-stu-id="c4419-110">The WCF service exposes 2 operations –`GetData` and `PutData` – that echo the string that was passed as input.</span></span> <span data-ttu-id="c4419-111">服務作業會以 <xref:System.ServiceModel.Web.WebGetAttribute> 和 <xref:System.ServiceModel.Web.WebInvokeAttribute> 標註。</span><span class="sxs-lookup"><span data-stu-id="c4419-111">The service operations are annotated with <xref:System.ServiceModel.Web.WebGetAttribute> and <xref:System.ServiceModel.Web.WebInvokeAttribute>.</span></span> <span data-ttu-id="c4419-112">這些屬性會控制這些作業的 HTTP 投射。</span><span class="sxs-lookup"><span data-stu-id="c4419-112">These attributes control the HTTP projection of these operations.</span></span> <span data-ttu-id="c4419-113">此外，這些作業還會以 <xref:System.ServiceModel.OperationContractAttribute> 標註，這個屬性可讓作業透過 SOAP 繫結公開。</span><span class="sxs-lookup"><span data-stu-id="c4419-113">In addition, they are annotated with <xref:System.ServiceModel.OperationContractAttribute>, which enables them to be exposed over SOAP bindings.</span></span> <span data-ttu-id="c4419-114">服務的 `PutData` 方法會擲回 <xref:System.ServiceModel.Web.WebFaultException>，它會使用 HTTP 狀態碼透過 HTTP 送回，以及透過 SOAP 做為 SOAP 錯誤送回。</span><span class="sxs-lookup"><span data-stu-id="c4419-114">The service’s `PutData` method throws a <xref:System.ServiceModel.Web.WebFaultException>, which gets sent back over HTTP using the HTTP status code and gets sent back over SOAP as a SOAP fault.</span></span>  
  
 <span data-ttu-id="c4419-115">Web.config 檔案會以3個端點設定 WCF 服務：</span><span class="sxs-lookup"><span data-stu-id="c4419-115">The Web.config file configures the WCF service with 3 endpoints:</span></span>  
  
- <span data-ttu-id="c4419-116">~/service.svc/mex 端點，這個端點會公開服務中繼資料讓 SOAP 用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="c4419-116">The ~/service.svc/mex endpoint that exposes the service metadata for access by SOAP-based clients.</span></span>  
  
- <span data-ttu-id="c4419-117">~/service.svc/http 端點，這個端點會讓用戶端使用 HTTP 繫結存取服務。</span><span class="sxs-lookup"><span data-stu-id="c4419-117">The ~/service.svc/http endpoint that enables clients to access the service using the HTTP binding.</span></span>  
  
- <span data-ttu-id="c4419-118">~/service.svc/soap 端點，這個端點可讓用戶端使用 SOAP over HTTP 繫結存取服務。</span><span class="sxs-lookup"><span data-stu-id="c4419-118">The ~/service.svc/soap endpoint that allows the clients to access the service using the SOAP over HTTP binding.</span></span>  
  
 <span data-ttu-id="c4419-119">HTTP 端點是以設定為的 <`webHttp`> 標準端點來設定 `helpEnabled` `true` 。</span><span class="sxs-lookup"><span data-stu-id="c4419-119">The HTTP endpoint is configured with a <`webHttp`> standard endpoint which has `helpEnabled` set to `true`.</span></span> <span data-ttu-id="c4419-120">因此，服務會在 HTTP 用戶端可用來存取服務的 ~/service.svc/http/help 公開 XHTML 說明頁。</span><span class="sxs-lookup"><span data-stu-id="c4419-120">As a result, the service exposes an XHTML based help page at ~/service.svc/http/help that HTTP-based clients can use to access the service.</span></span>  
  
 <span data-ttu-id="c4419-121">用戶端專案會示範如何使用 SOAP proxy 存取服務， (透過 **加入服務參考**) 產生，並使用來存取服務 <xref:System.Net.WebClient> 。</span><span class="sxs-lookup"><span data-stu-id="c4419-121">The client project demonstrates accessing the service using a SOAP proxy (generated through **Add Service Reference**) and accessing the service using <xref:System.Net.WebClient>.</span></span>  
  
 <span data-ttu-id="c4419-122">這個範例包含 Web 主控服務和主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4419-122">The sample consists of a Web-hosted service and a console application.</span></span> <span data-ttu-id="c4419-123">當主控台應用程式執行時，用戶端會對服務發出要求，然後將相關的資訊從回應寫入至主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="c4419-123">As the console application runs, the client makes requests to the service and writes the pertinent information from the responses to the console window.</span></span>  
  
#### <a name="to-run-the-sample"></a><span data-ttu-id="c4419-124">執行範例</span><span class="sxs-lookup"><span data-stu-id="c4419-124">To run the sample</span></span>  
  
1. <span data-ttu-id="c4419-125">開啟「SOAP 和 HTTP 端點範例」的方案。</span><span class="sxs-lookup"><span data-stu-id="c4419-125">Open the solution for the SOAP and HTTP Endpoints Sample.</span></span>  
  
2. <span data-ttu-id="c4419-126">按 CTRL+SHIFT+B 建置解決方案。</span><span class="sxs-lookup"><span data-stu-id="c4419-126">Press CTRL+SHIFT+B to build the solution.</span></span>  
  
3. <span data-ttu-id="c4419-127">如果尚未開啟，請按 CTRL + W、S 以開啟 **方案總管** 視窗。</span><span class="sxs-lookup"><span data-stu-id="c4419-127">If it is not already open, press CTRL+W, S to open the **Solution Explorer** window.</span></span>  
  
4. <span data-ttu-id="c4419-128">在 [ **方案總管** ] 視窗中，以滑鼠右鍵按一下 **服務** 專案，並將游標放在 [ **調試** 程式] 內容功能表選項上，如此就會出現 [ **開始新實例** ] 內容功能表。</span><span class="sxs-lookup"><span data-stu-id="c4419-128">From the **Solution Explorer** window, right-click the **Service** project and place the cursor over the **Debug** context menu option so that the **Start New Instance** context menu appears.</span></span> <span data-ttu-id="c4419-129">按一下 [ **開始新實例**]。</span><span class="sxs-lookup"><span data-stu-id="c4419-129">Click **Start New Instance**.</span></span> <span data-ttu-id="c4419-130">這樣會啟動裝載服務的 ASP.NET 程式開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="c4419-130">This launches the ASP.NET development server, which hosts the service.</span></span>  
  
5. <span data-ttu-id="c4419-131">從方案總管視窗中，以滑鼠右鍵按一下用戶端專案，並將游標放在 [ **調試** 程式] 內容功能表選項上，如此就會出現 [ **開始新實例** ] 內容功能表。</span><span class="sxs-lookup"><span data-stu-id="c4419-131">From the Solution Explorer windows, right-click the Client project and place the cursor over the **Debug** context menu option so that the **Start New Instance** context menu appears.</span></span> <span data-ttu-id="c4419-132">按一下 [ **開始新實例**]。</span><span class="sxs-lookup"><span data-stu-id="c4419-132">Click **Start New Instance**.</span></span>  
  
6. <span data-ttu-id="c4419-133">用戶端主控台視窗隨即出現，並提供執行中服務的 URI，以及執行中服務之 HTML 說明頁的 URI。</span><span class="sxs-lookup"><span data-stu-id="c4419-133">The client console window appears and provides the URI of the running service and the URI of the HTML help page for the running service.</span></span> <span data-ttu-id="c4419-134">您可以隨時在瀏覽器中輸入說明頁的 URI 來檢視 HTML 說明頁。</span><span class="sxs-lookup"><span data-stu-id="c4419-134">At any point in time you can view the HTML help page by typing the URI of the help page in a browser.</span></span>  
  
7. <span data-ttu-id="c4419-135">當範例執行時，用戶端會寫入目前活動的狀態。</span><span class="sxs-lookup"><span data-stu-id="c4419-135">As the sample runs, the client writes the status of the current activity.</span></span>  
  
8. <span data-ttu-id="c4419-136">按下任何按鍵可終止用戶端主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4419-136">Press any key to terminate the client console application.</span></span>  
  
9. <span data-ttu-id="c4419-137">按 SHIFT+F5 停止對服務偵錯。</span><span class="sxs-lookup"><span data-stu-id="c4419-137">Press SHIFT+F5 to stop debugging the service.</span></span>  
  
10. <span data-ttu-id="c4419-138">在 Windows 通知區域中，以滑鼠右鍵按一下 ASP.NET 開發伺服器圖示，然後從內容功能表中選取 [ **停止** ]。</span><span class="sxs-lookup"><span data-stu-id="c4419-138">In the Windows Notification Area, right-click the ASP.NET development server icon and select **Stop** from the context menu.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="c4419-139">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="c4419-139">The samples may already be installed on your machine.</span></span> <span data-ttu-id="c4419-140">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="c4419-140">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="c4419-141">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="c4419-141">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="c4419-142">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="c4419-142">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\SoapAndHttpEndpoints`
