---
title: ASP.NET 快取整合
ms.date: 03/30/2017
ms.assetid: f581923a-8a72-42fc-bd6a-46de2aaeecc1
ms.openlocfilehash: c541f3caad8a500b9fdb33d00b58706bac876e37
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594747"
---
# <a name="aspnet-caching-integration"></a><span data-ttu-id="8ff9e-102">ASP.NET 快取整合</span><span class="sxs-lookup"><span data-stu-id="8ff9e-102">ASP.NET Caching Integration</span></span>

<span data-ttu-id="8ff9e-103">這個範例示範如何使用 ASP.NET 輸出快取搭配 WCF WEB HTTP 程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-103">This sample demonstrates how to utilize the ASP.NET output cache with the WCF WEB HTTP programming model.</span></span> <span data-ttu-id="8ff9e-104">本主題著重在 ASP.NET 輸出快取整合功能。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-104">This topic focuses on the ASP.NET output cache integration feature.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="8ff9e-105">示範</span><span class="sxs-lookup"><span data-stu-id="8ff9e-105">Demonstrates</span></span>

<span data-ttu-id="8ff9e-106">與 ASP.NET 輸出快取整合</span><span class="sxs-lookup"><span data-stu-id="8ff9e-106">Integration with the ASP.NET Output Cache</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ff9e-107">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-107">The samples may already be installed on your machine.</span></span> <span data-ttu-id="8ff9e-108">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-108">Check for the following (default) directory before continuing.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> <span data-ttu-id="8ff9e-109">如果此目錄不存在，請移至[.NET Framework 4 的 Windows Communication Foundation （wcf）和 Windows Workflow Foundation （WF）範例](https://www.microsoft.com/download/details.aspx?id=21459)，以下載所有 WINDOWS COMMUNICATION FOUNDATION （wcf）和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-109">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="8ff9e-110">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-110">This sample is located in the following directory.</span></span>
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\AspNetCachingIntegration`

## <a name="discussion"></a><span data-ttu-id="8ff9e-111">討論區</span><span class="sxs-lookup"><span data-stu-id="8ff9e-111">Discussion</span></span>

<span data-ttu-id="8ff9e-112">此範例會使用 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 來利用 ASP.NET 輸出快取搭配 Windows Communication Foundation （WCF）服務。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-112">The sample uses the <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> to utilize ASP.NET output caching with the Windows Communication Foundation (WCF) service.</span></span> <span data-ttu-id="8ff9e-113"><xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> 會套用至服務作業，並提供應套用至所指作業之回應的組態檔中快取設定檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-113">The <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> is applied to service operations, and provides the name of a cache profile in a configuration file that should be applied to responses from the given operation.</span></span>

<span data-ttu-id="8ff9e-114">在範例服務專案的 Service.cs 檔案中， `GetCustomer` 和 `GetCustomers` 作業都以標示 <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> ，這會提供快取設定檔名稱 "CacheFor60Seconds"。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-114">In the Service.cs file of the sample Service project, both the `GetCustomer` and `GetCustomers` operations are marked with the <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute>, which provides the cache profile name "CacheFor60Seconds".</span></span> <span data-ttu-id="8ff9e-115">在服務專案的 web.config 檔案中，快取設定檔 "CacheFor60Seconds" 是在 `caching` < > 的 < > 元素底下提供 `system.web` 。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-115">In the Web.config file of the Service project, the cache profile "CacheFor60Seconds" is provided under the <`caching`> element of <`system.web`>.</span></span> <span data-ttu-id="8ff9e-116">此快取設定檔的 `duration` 屬性值為 "60"，因此與此設定檔相關聯的回應會在 ASP.NET 輸出快取中快取60秒。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-116">For this cache profile, the value of the `duration` attribute is "60", so responses associated with this profile are cached in the ASP.NET output cache for 60 seconds.</span></span> <span data-ttu-id="8ff9e-117">此外，此快取設定檔的 `varmByParam` 屬性設定為 "format"，因此查詢字串參數具有不同值的要求 `format` 會分別快取其回應。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-117">Also, for this cache profile, the `varmByParam` attribute is set to "format" so requests with different values for the `format` query string parameter have their responses cached separately.</span></span> <span data-ttu-id="8ff9e-118">最後，快取設定檔的 `varyByHeader` 屬性會設定為「接受」，因此具有不同 Accept 標頭值的要求會分別快取其回應。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-118">Lastly, the cache profile’s `varyByHeader` attribute is set to "Accept", so requests with different Accept header values have their responses cached separately.</span></span>

<span data-ttu-id="8ff9e-119">用戶端專案中的 Program.cs 會示範如何使用 <xref:System.Net.HttpWebRequest> 編寫這種用戶端。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-119">Program.cs in the Client project demonstrates how such a client can be authored using <xref:System.Net.HttpWebRequest>.</span></span> <span data-ttu-id="8ff9e-120">請注意，這只是存取 WCF 服務的其中一種方式。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-120">Note that this is just one way to access a WCF service.</span></span> <span data-ttu-id="8ff9e-121">您也可以使用其他 .NET Framework 類別（例如 WCF 通道處理站和）來存取服務 <xref:System.Net.WebClient> 。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-121">It is also possible to access the service using other .NET Framework classes like the WCF channel factory and <xref:System.Net.WebClient>.</span></span> <span data-ttu-id="8ff9e-122">SDK 中的其他範例（例如[基本 HTTP 服務](basic-http-service.md)範例）說明如何使用這些類別與 WCF 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-122">Other samples in the SDK (such as the [Basic HTTP Service](basic-http-service.md) sample) illustrate how to use these classes to communicate with a WCF service.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="8ff9e-123">執行範例</span><span class="sxs-lookup"><span data-stu-id="8ff9e-123">To run the sample</span></span>

<span data-ttu-id="8ff9e-124">此範例包含三個專案：</span><span class="sxs-lookup"><span data-stu-id="8ff9e-124">The sample consists of three projects:</span></span>

- <span data-ttu-id="8ff9e-125">**服務**：包含裝載于 ASP.NET 之 WCF HTTP 服務的 Web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-125">**Service**: A Web Application project that includes a WCF HTTP service hosted in ASP.NET.</span></span>

- <span data-ttu-id="8ff9e-126">**用戶端**：會呼叫服務的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-126">**Client**: A console application project that makes calls to the service.</span></span>

- <span data-ttu-id="8ff9e-127">**通用**：包含用戶端和服務所使用之客戶類型的共用程式庫。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-127">**Common**: A shared library that contains the Customer type used by the client and service.</span></span>

<span data-ttu-id="8ff9e-128">當用戶端主控台應用程式執行時，用戶端會對服務發出要求，然後將相關的資訊從回應寫入至主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-128">As the Client console application runs, the client makes requests to the service and writes the pertinent information from the responses to the console window.</span></span>

#### <a name="to-run-the-sample"></a><span data-ttu-id="8ff9e-129">執行範例</span><span class="sxs-lookup"><span data-stu-id="8ff9e-129">To run the sample</span></span>

1. <span data-ttu-id="8ff9e-130">開啟「ASP.NET 快取整合範例」的方案。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-130">Open the solution for the ASP.NET Caching Integration Sample.</span></span>

2. <span data-ttu-id="8ff9e-131">按 CTRL+SHIFT+B 建置解決方案。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-131">Press CTRL+SHIFT+B to build the solution.</span></span>

3. <span data-ttu-id="8ff9e-132">如果 [**方案總管**] 視窗尚未開啟，請按 CTRL + W + S。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-132">If the **Solution Explorer** window is not already open, press CTRL+W+S.</span></span>

4. <span data-ttu-id="8ff9e-133">從 [**方案總管**] 視窗中，以滑鼠右鍵按一下**服務**專案，然後選取 [**開始新實例**]。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-133">From the **Solution Explorer** window, right click the **Service** project and select **Start New Instance**.</span></span> <span data-ttu-id="8ff9e-134">這樣會啟動裝載服務的 ASP.NET 程式開發伺服器。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-134">This launches the ASP.NET development server, which hosts the service.</span></span>

5. <span data-ttu-id="8ff9e-135">從 [**方案總管**] 視窗中，以滑鼠右鍵按一下**用戶端**專案，然後選取 [**開始新實例**]。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-135">From the **Solution Explorer** window, right click the **Client** project and select **Start New Instance**.</span></span>

6. <span data-ttu-id="8ff9e-136">用戶端主控台視窗隨即出現，並提供執行中服務的 URI，以及執行中服務之 HTML 說明頁的 URI。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-136">The client console window appears and provides the URI of the running service and the URI of the HTML help page for the running service.</span></span> <span data-ttu-id="8ff9e-137">您可以隨時在瀏覽器中輸入說明頁的 URI 來檢視 HTML 說明頁。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-137">At any point in time you can view the HTML help page by typing the URI of the help page in a browser.</span></span>

7. <span data-ttu-id="8ff9e-138">當範例執行時，用戶端會寫入目前活動的狀態。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-138">As the sample runs, the client writes the status of the current activity.</span></span>

8. <span data-ttu-id="8ff9e-139">按下任何按鍵可終止用戶端主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-139">Press any key to terminate the client console application.</span></span>

9. <span data-ttu-id="8ff9e-140">按 SHIFT+F5 停止對服務偵錯。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-140">Press SHIFT+F5 to stop debugging the service.</span></span>

10. <span data-ttu-id="8ff9e-141">在 Windows 通知區域中，以滑鼠右鍵按一下 ASP.NET 開發伺服器圖示，然後選取 [**停止**]。</span><span class="sxs-lookup"><span data-stu-id="8ff9e-141">In the Windows Notification Area, right click the ASP.NET development server icon and select **Stop**.</span></span>
