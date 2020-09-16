---
title: SystemWebRouting 整合範例
ms.date: 03/30/2017
ms.assetid: f1c94802-95c4-49e4-b1e2-ee9dd126ff93
ms.openlocfilehash: 58d720f164c4c35f3de4c282e9aa983d11e4040b
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555220"
---
# <a name="systemwebrouting-integration-sample"></a><span data-ttu-id="50838-102">SystemWebRouting 整合範例</span><span class="sxs-lookup"><span data-stu-id="50838-102">SystemWebRouting Integration Sample</span></span>
<span data-ttu-id="50838-103">這個範例示範裝載層與 <xref:System.Web.Routing> 命名空間中的類別整合。</span><span class="sxs-lookup"><span data-stu-id="50838-103">This sample demonstrates the hosting layer’s integration with the classes in the <xref:System.Web.Routing> namespace.</span></span> <span data-ttu-id="50838-104"><xref:System.Web.Routing> 命名空間中的類別可讓應用程式使用不會直接回應實體資源的 URL。</span><span class="sxs-lookup"><span data-stu-id="50838-104">The classes in the <xref:System.Web.Routing> namespace allow an application to use URLs that do not directly correspond to a physical resource.</span></span> <span data-ttu-id="50838-105">使用 Web 路由可讓開發人員建立 HTTP 的虛擬位址，然後再對應回實際的 WCF 服務。</span><span class="sxs-lookup"><span data-stu-id="50838-105">Using Web routing allows the developer to create virtual addresses for HTTP that are then mapped back to actual WCF services.</span></span> <span data-ttu-id="50838-106">當 WCF 服務必須在不需要實體檔案或資源的情況下裝載，或是服務必須使用不包含 .html 或 .aspx 等檔案的 URL 存取時，這種方式會相當實用。</span><span class="sxs-lookup"><span data-stu-id="50838-106">This is useful when a WCF service must be hosted without requiring a physical file or resource, or when services must be accessed with URLs that do not contain files such as .html or .aspx.</span></span> <span data-ttu-id="50838-107">這個範例將示範如何使用 <xref:System.Web.Routing.RouteTable> 類別來建立虛擬 URI，以便對應至 global.asax 中所定義的執行中服務。</span><span class="sxs-lookup"><span data-stu-id="50838-107">This sample demonstrates how to utilize the <xref:System.Web.Routing.RouteTable> class to create virtual URIs that map to running services defined in global.asax.</span></span>

> [!NOTE]
> <span data-ttu-id="50838-108"><xref:System.Web.Routing> 命名空間中的類別只適用於透過 HTTP 裝載的服務。</span><span class="sxs-lookup"><span data-stu-id="50838-108">The classes in the <xref:System.Web.Routing> namespace only work for services hosted over HTTP.</span></span>  
  
<span data-ttu-id="50838-109">此範例會使用 WCF 來建立兩個 RSS 摘要：摘要 `movies` 和摘要 `channels` 。</span><span class="sxs-lookup"><span data-stu-id="50838-109">This example uses WCF to create two RSS feeds: a `movies` feed and a `channels` feed.</span></span> <span data-ttu-id="50838-110">用來啟動服務的 Url 不會包含副檔名，並且會在 `Application_Start` `Global` 衍生自類別之類別的方法中註冊 <xref:System.Web.HttpApplication> 。</span><span class="sxs-lookup"><span data-stu-id="50838-110">The URLs to activate the services do not contain an extension and are registered in the `Application_Start` method of the `Global` class derived from the <xref:System.Web.HttpApplication> class.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="50838-111">此範例僅適用于 (IIS) 7.0 和更新版本的 Internet Information Services，因為 IIS 6.0 使用不同的方法來支援無副檔名的 Url。</span><span class="sxs-lookup"><span data-stu-id="50838-111">This sample only works in Internet Information Services (IIS) 7.0 and later, as IIS 6.0 uses a different method for supporting extension-less URLs.</span></span>  

#### <a name="to-download-this-sample"></a><span data-ttu-id="50838-112">若要下載此範例</span><span class="sxs-lookup"><span data-stu-id="50838-112">To download this sample</span></span>
  
<span data-ttu-id="50838-113">此範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="50838-113">This sample may already be installed on your computer.</span></span> <span data-ttu-id="50838-114">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="50838-114">Check for the following (default) directory before continuing.</span></span>  

`<InstallDrive>:\WF_WCF_Samples`  

 <span data-ttu-id="50838-115">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="50838-115">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="50838-116">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="50838-116">This sample is located in the following directory.</span></span>  

`<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebRoutingIntegration`  
  
#### <a name="to-use-this-sample"></a><span data-ttu-id="50838-117">若要使用這個範例</span><span class="sxs-lookup"><span data-stu-id="50838-117">To use this sample</span></span>  
  
1. <span data-ttu-id="50838-118">使用 Visual Studio 開啟 WebRoutingIntegration .sln 檔案。</span><span class="sxs-lookup"><span data-stu-id="50838-118">Using Visual Studio, open the WebRoutingIntegration.sln file.</span></span>  
  
2. <span data-ttu-id="50838-119">若要執行方案並啟動 Web 程式開發伺服器，請按下 F5。</span><span class="sxs-lookup"><span data-stu-id="50838-119">To run the solution and start the Web development server, press F5.</span></span>  
  
     <span data-ttu-id="50838-120">範例的目錄清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="50838-120">A directory listing for the sample appears.</span></span> <span data-ttu-id="50838-121">請注意，沒有副檔名 .svc 的檔案。</span><span class="sxs-lookup"><span data-stu-id="50838-121">Note that there are no files with an .svc file extension.</span></span>  
  
3. <span data-ttu-id="50838-122">在網址列中，新增 `movies` 至 URL，讓它讀取 `http://localhost:[port]/movies` 並按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="50838-122">In the address bar, add `movies` to the URL, so that it reads `http://localhost:[port]/movies` and press ENTER.</span></span>  
  
     <span data-ttu-id="50838-123">影片摘要會出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="50838-123">The movies feed appears in the browser.</span></span>  
  
4. <span data-ttu-id="50838-124">在網址列中，將新增 `channels` 至 URL， `http://localhost:[port]/channels` 然後按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="50838-124">In the address bar, add `channels` to the URL, so that is reads `http://localhost:[port]/channels` and press ENTER.</span></span>  
  
     <span data-ttu-id="50838-125">通道摘要會出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="50838-125">The channels feed appears in the browser.</span></span>  
  
5. <span data-ttu-id="50838-126">按 ALT+F4，關閉 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="50838-126">Close the Web browser, by pressing ALT+F4.</span></span>  
  
     <span data-ttu-id="50838-127">如果程式開發伺服器尚未結束，請以滑鼠右鍵按一下通知區域圖示，然後選取 [ **停止**]。</span><span class="sxs-lookup"><span data-stu-id="50838-127">If the development server has not exited, right-click the notification area icon and select **Stop**.</span></span>  
  
#### <a name="to-use-this-sample-when-hosted-in-iis"></a><span data-ttu-id="50838-128">若要在 IIS 中裝載時使用這個範例</span><span class="sxs-lookup"><span data-stu-id="50838-128">To use this sample when hosted in IIS</span></span>  
  
1. <span data-ttu-id="50838-129">使用 Visual Studio 開啟 WebRoutingIntegration .sln 檔案。</span><span class="sxs-lookup"><span data-stu-id="50838-129">Using Visual Studio, open the WebRoutingIntegration.sln file.</span></span>  
  
2. <span data-ttu-id="50838-130">按下 CTRL+SHIFT+B 建置此專案。</span><span class="sxs-lookup"><span data-stu-id="50838-130">Build the project, by pressing CTRL+SHIFT+B.</span></span>  
  
3. <span data-ttu-id="50838-131">在 [Internet Information Services (IIS) 管理員] 中建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="50838-131">Create a Web application in Internet Information Services (IIS) Manager.</span></span>  
  
    1. <span data-ttu-id="50838-132">在 [IIS 管理員] 中，以滑鼠右鍵按一下 [ **預設的網站** ]，然後選取 [ **加入應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="50838-132">In IIS Manager, right click the **Default Web Site** and select **Add an Application**.</span></span>  
  
    2. <span data-ttu-id="50838-133">在 [ **別名**] 中輸入 `WebRoutingIntegration` 。</span><span class="sxs-lookup"><span data-stu-id="50838-133">For the **alias**, type in `WebRoutingIntegration`.</span></span>  
  
    3. <span data-ttu-id="50838-134">在 [ **實體路徑**] 中，選取專案內的 [服務] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="50838-134">For the **Physical Path**, select the Service folder inside the project.</span></span>  
  
    4. <span data-ttu-id="50838-135">按下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="50838-135">Press **OK**.</span></span>  
  
4. <span data-ttu-id="50838-136">以滑鼠右鍵按一下 Web 應用程式，然後選取 [ **管理應用程式** ]，然後 **流覽**，以啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="50838-136">Start the application, by right-clicking the Web application and selecting **Manage Application** and then **Browse**.</span></span>  
  
5. <span data-ttu-id="50838-137">在網址列中，將新增 `movies` 至 URL， `http://localhost:[port]/movies` 然後按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="50838-137">In the address bar, add `movies` to the URL, so that is reads `http://localhost:[port]/movies` and press ENTER.</span></span>  
  
     <span data-ttu-id="50838-138">影片摘要會出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="50838-138">The movies feed appears in the browser.</span></span>  
  
6. <span data-ttu-id="50838-139">在網址列中，將新增 `channels` 至 URL， `http://localhost:[port]/channels` 然後按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="50838-139">In the address bar, add `channels` to the URL, so that is reads `http://localhost:[port]/channels` and press ENTER.</span></span>  
  
     <span data-ttu-id="50838-140">通道摘要會出現在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="50838-140">The channels feed appears in the browser.</span></span>  
  
7. <span data-ttu-id="50838-141">按 ALT+F4，關閉 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="50838-141">Close the Web browser, by pressing ALT+F4.</span></span>  
  
 <span data-ttu-id="50838-142">這個範例將示範裝載層能夠使用 <xref:System.Web.Routing> 命名空間中的類別撰寫，以便路由傳送透過 HTTP 裝載之服務的要求。</span><span class="sxs-lookup"><span data-stu-id="50838-142">This sample demonstrates that the hosting layer is capable of composing with the classes in the <xref:System.Web.Routing> namespace for routing the requests of services hosted over HTTP.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="50838-143">如果預設應用程式集區版本設定為第2版，則必須將預設應用程式集區版本更新為 .NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="50838-143">You must update the default application pool version to .NET Framework 4 if it’s set to version 2.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="50838-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="50838-144">See also</span></span>

- <span data-ttu-id="50838-145">[AppFabric 主控與持續性範例](/previous-versions/appfabric/ff383418(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="50838-145">[AppFabric Hosting and Persistence Samples](/previous-versions/appfabric/ff383418(v=azure.10))</span></span>
