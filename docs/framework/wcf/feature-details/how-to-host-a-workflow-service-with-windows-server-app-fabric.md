---
title: HOW TO：使用 Windows Server App Fabric 裝載工作流程服務
ms.date: 03/30/2017
ms.assetid: 83b62cce-5fc2-4c6d-b27c-5742ba3bac73
ms.openlocfilehash: 519c76e3e46e01b5e8c696234e39fefbb9f8ad06
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593304"
---
# <a name="how-to-host-a-workflow-service-with-windows-server-app-fabric"></a><span data-ttu-id="d30f8-102">HOW TO：使用 Windows Server App Fabric 裝載工作流程服務</span><span class="sxs-lookup"><span data-stu-id="d30f8-102">How to: Host a Workflow Service with Windows Server App Fabric</span></span>

<span data-ttu-id="d30f8-103">在 AppFabric 中裝載工作流程服務與在 IIS/WAS 底下裝載很相似。</span><span class="sxs-lookup"><span data-stu-id="d30f8-103">Hosting workflow services in App Fabric is similar to hosting under IIS/WAS.</span></span> <span data-ttu-id="d30f8-104">唯一的差異在於 AppFabric 針對部署、監視和管理工作流程服務所提供的工具。</span><span class="sxs-lookup"><span data-stu-id="d30f8-104">The only difference is the tools App Fabric provides for deploying, monitoring, and managing workflow services.</span></span> <span data-ttu-id="d30f8-105">本主題使用建立[長期執行的工作流程服務](creating-a-long-running-workflow-service.md)中所建立的工作流程服務。</span><span class="sxs-lookup"><span data-stu-id="d30f8-105">This topic uses the workflow service created in the [Creating a Long-running Workflow Service](creating-a-long-running-workflow-service.md).</span></span> <span data-ttu-id="d30f8-106">該主題將逐步引導您建立工作流程服務。</span><span class="sxs-lookup"><span data-stu-id="d30f8-106">That topic will walk you through creating a workflow service.</span></span> <span data-ttu-id="d30f8-107">本主題會說明如何使用 AppFabric 來裝載工作流程服務。</span><span class="sxs-lookup"><span data-stu-id="d30f8-107">This topic will explain how to host the workflow service using App Fabric.</span></span> <span data-ttu-id="d30f8-108">如需 Windows Server App Fabric 的詳細資訊，請參閱[Windows Server App Fabric 檔](https://docs.microsoft.com/previous-versions/appfabric/ff384253(v=azure.10))。</span><span class="sxs-lookup"><span data-stu-id="d30f8-108">For more information about Windows Server App Fabric, see [Windows Server App Fabric Documentation](https://docs.microsoft.com/previous-versions/appfabric/ff384253(v=azure.10)).</span></span> <span data-ttu-id="d30f8-109">完成下列步驟之前，請先確定您已安裝 Windows Server AppFabric。</span><span class="sxs-lookup"><span data-stu-id="d30f8-109">Before completing the steps below make sure you have Windows Server App Fabric installed.</span></span>  <span data-ttu-id="d30f8-110">若要這麼做，請開啟 Internet Information Services （inetmgr），**在 [連線**] 視圖中按一下您的伺服器名稱，按一下 [網站]，然後按一下 [**預設的網站**]。</span><span class="sxs-lookup"><span data-stu-id="d30f8-110">To do this open up Internet Information Services (inetmgr.exe), click your server name in the **Connections** view, click Sites, and click **Default Web Site**.</span></span> <span data-ttu-id="d30f8-111">在畫面右手邊，您應該會看到一個稱為「**應用程式網狀架構**」的區段。</span><span class="sxs-lookup"><span data-stu-id="d30f8-111">In the right-hand side of the screen you should see a section called **App Fabric**.</span></span> <span data-ttu-id="d30f8-112">如果您沒有看見此區段 (位於右側窗格的頂端)，表示您沒有安裝 App Fabric。</span><span class="sxs-lookup"><span data-stu-id="d30f8-112">If you don’t see this section (it will be on the top of the right-hand pane) you do not have App Fabric installed.</span></span> <span data-ttu-id="d30f8-113">如需安裝 Windows Server App Fabric 的詳細資訊，請參閱[安裝 Windows Server App fabric](https://docs.microsoft.com/previous-versions/appfabric/ee790960(v=azure.10))。</span><span class="sxs-lookup"><span data-stu-id="d30f8-113">For more information about installing Windows Server App Fabric see [Installing Windows Server App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee790960(v=azure.10)).</span></span>  
  
### <a name="creating-a-simple-workflow-service"></a><span data-ttu-id="d30f8-114">建立簡單的工作流程服務</span><span class="sxs-lookup"><span data-stu-id="d30f8-114">Creating a Simple Workflow Service</span></span>  
  
1. <span data-ttu-id="d30f8-115">開啟 Visual Studio 2012，並載入您在[建立長時間執行的工作流程服務](creating-a-long-running-workflow-service.md)主題中建立的 OrderProcessing 解決方案。</span><span class="sxs-lookup"><span data-stu-id="d30f8-115">Open Visual Studio 2012 and load the OrderProcessing solution you created in the [Creating a Long-running Workflow Service](creating-a-long-running-workflow-service.md) topic.</span></span>  
  
2. <span data-ttu-id="d30f8-116">以滑鼠右鍵按一下**OrderService**專案，並選取 [**屬性**]，然後選取 [ **Web** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d30f8-116">Right click the **OrderService** project and select **Properties** and select the **Web** tab.</span></span>  
  
3. <span data-ttu-id="d30f8-117">在屬性頁的 [**起始動作**] 區段中，選取 [**特定頁面**]，然後在編輯方塊中輸入 Service1. service1.xamlx。</span><span class="sxs-lookup"><span data-stu-id="d30f8-117">In the **Start Action** section of the property page select **Specific Page** and type Service1.xamlx in the edit box.</span></span>  
  
4. <span data-ttu-id="d30f8-118">在屬性頁的 [**伺服器**] 區段中，選取 [**使用本機 IIS Web 服務器**]，然後輸入下列 URL： `http://localhost/OrderService` 。</span><span class="sxs-lookup"><span data-stu-id="d30f8-118">In the **Servers** section of the property page select **Use Local IIS Web Server** and type in the following URL: `http://localhost/OrderService`.</span></span>  
  
5. <span data-ttu-id="d30f8-119">按一下 [**建立虛擬目錄**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d30f8-119">Click the **Create Virtual Directory** button.</span></span> <span data-ttu-id="d30f8-120">這樣就會建立新的虛擬目錄並設定專案，以便在建置專案時，將所需的檔案複製到虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="d30f8-120">This will create a new virtual directory and set up the project to copy the needed files to the virtual directory when the project is built.</span></span>  <span data-ttu-id="d30f8-121">或者，您也可以將 .xamlx、web.config 和任何所需的 DLL 手動複製到虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="d30f8-121">Alternatively you could manually copy the .xamlx, the web.config, and any needed DLLs to the virtual directory.</span></span>  
  
### <a name="configuring-a-workflow-service-hosted-in-windows-server-app-fabric"></a><span data-ttu-id="d30f8-122">設定在 Windows Server AppFabric 中裝載的工作流程服務</span><span class="sxs-lookup"><span data-stu-id="d30f8-122">Configuring a Workflow Service Hosted in Windows Server App Fabric</span></span>  
  
1. <span data-ttu-id="d30f8-123">開啟 Internet Information Services 管理員 (inetmgr.exe)。</span><span class="sxs-lookup"><span data-stu-id="d30f8-123">Open Internet Information Services Manager (inetmgr.exe).</span></span>  
  
2. <span data-ttu-id="d30f8-124">在 [**連線] 窗格中，流覽**至 OrderService 虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="d30f8-124">Navigate to the OrderService virtual directory in the **Connections** pane.</span></span>  
  
3. <span data-ttu-id="d30f8-125">以滑鼠右鍵按一下 OrderService，並選取 [**管理 WCF 和 WF 服務**]、[**設定 ...**]。</span><span class="sxs-lookup"><span data-stu-id="d30f8-125">Right click OrderService and select **Manage WCF and WF Services**, **Configure…**.</span></span> <span data-ttu-id="d30f8-126">[**設定應用程式的 WCF 和 WF** ] 對話方塊隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-126">The **Configure WCF and WF for Application** dialog box is displayed.</span></span>  
  
4. <span data-ttu-id="d30f8-127">選取 [**一般**] 索引標籤，以顯示應用程式的一般資訊，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-127">Select the **General** tab to display general information about the application as shown in the following screenshot.</span></span>  
  
     <span data-ttu-id="d30f8-128">![App Fabric 組態對話方塊的 [一般] 索引標籤](media/appfabricconfiguration-general.gif "AppFabricConfiguration-一般")</span><span class="sxs-lookup"><span data-stu-id="d30f8-128">![General tab of the App Fabric Configuration dialog](media/appfabricconfiguration-general.gif "AppFabricConfiguration-General")</span></span>  
  
5. <span data-ttu-id="d30f8-129">選取 [**監視**] 索引標籤。這會顯示各種監視設定，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-129">Select the **Monitoring** tab. This shows various monitoring settings as shown in the following screenshot.</span></span>  
  
     <span data-ttu-id="d30f8-130">![App Fabric 組態監視索引標籤](media/appfabricconfiguration-monitoring.gif "AppFabricConfiguration-監視")</span><span class="sxs-lookup"><span data-stu-id="d30f8-130">![App Fabric Configuration Monitoring tab](media/appfabricconfiguration-monitoring.gif "AppFabricConfiguration-Monitoring")</span></span>  
  
     <span data-ttu-id="d30f8-131">如需有關在應用程式網狀架構中設定工作流程服務監視的詳細資訊，請參閱[使用 App fabric 設定監視](https://docs.microsoft.com/previous-versions/appfabric/ee677384(v=azure.10))。</span><span class="sxs-lookup"><span data-stu-id="d30f8-131">For more information about configuring workflow service monitoring in App Fabric see [Configuring monitoring with App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677384(v=azure.10)).</span></span>  
  
6. <span data-ttu-id="d30f8-132">選取 [**工作流程持續**性] 索引標籤。這可讓您將應用程式設定為使用 App Fabric 的預設持續性提供者，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-132">Select the **Workflow Persistence** tab. This allows you to configure your application to use App Fabric’s default persistence provider as shown in the following screenshot.</span></span>  
  
     <span data-ttu-id="d30f8-133">![應用程式網狀架構設定 &#45; 持續性](media/appfabricconfiguration-persistence.gif "AppFabricConfiguration-持續性")</span><span class="sxs-lookup"><span data-stu-id="d30f8-133">![App Fabric Configuration &#45; Persistence](media/appfabricconfiguration-persistence.gif "AppFabricConfiguration-Persistence")</span></span>  
  
     <span data-ttu-id="d30f8-134">如需在 Windows Server App Fabric 中設定工作流程持續性的詳細資訊，請參閱[在 App fabric 中設定工作流程持續](https://docs.microsoft.com/previous-versions/appfabric/ee677353(v=azure.10))性。</span><span class="sxs-lookup"><span data-stu-id="d30f8-134">For more information about configuring workflow persistence in Windows Server App Fabric see [Configuring Workflow Persistence in App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677353(v=azure.10)).</span></span>  
  
7. <span data-ttu-id="d30f8-135">選取 [**工作流程主機管理**] 索引標籤。這可讓您指定何時應卸載並保存閒置的工作流程服務實例，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-135">Select the **Workflow Host Management** tab. This allows you to specify when idle workflow service instances should be unloaded and persisted as shown in the following screenshot.</span></span>  
  
     <span data-ttu-id="d30f8-136">![App Fabric 設定工作流程主機管理](media/appfabricconfiguration-management.gif "AppFabricConfiguration-管理")</span><span class="sxs-lookup"><span data-stu-id="d30f8-136">![App Fabric Configuration  Workflow Host Management](media/appfabricconfiguration-management.gif "AppFabricConfiguration-Management")</span></span>  
  
     <span data-ttu-id="d30f8-137">如需工作流程主機管理設定的詳細資訊，請參閱[在 App Fabric 中設定工作流程主機管理](https://docs.microsoft.com/previous-versions/appfabric/ff383424(v=azure.10))。</span><span class="sxs-lookup"><span data-stu-id="d30f8-137">For more information about workflow host management configuration see [Configuring Workflow Host Management in App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ff383424(v=azure.10)).</span></span>  
  
8. <span data-ttu-id="d30f8-138">選取 [**自動啟動**] 索引標籤。這可讓您為應用程式中的工作流程服務指定自動啟動設定，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-138">Select the **Auto-Start** tab. This allows you to specify auto-start settings for the workflow services in the application as shown in the following screenshot.</span></span>  
  
     ![顯示 App Fabric 自動&#45;啟動設定的螢幕擷取畫面。](./media/how-to-host-a-workflow-service-with-windows-server-app-fabric/app-fabric-auto-start-configuration.gif)  
  
     <span data-ttu-id="d30f8-140">如需設定自動啟動的詳細資訊，請參閱[使用 App Fabric 設定自動啟動](https://docs.microsoft.com/previous-versions/appfabric/ee677261(v=azure.10))。</span><span class="sxs-lookup"><span data-stu-id="d30f8-140">For more information about configuring Auto-Start see [Configuring Auto-Start with App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677261(v=azure.10)).</span></span>  
  
9. <span data-ttu-id="d30f8-141">選取 [**節流**] 索引標籤。這可讓您設定工作流程服務的節流設定，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-141">Select the **Throttling** tab. This allows you to configure throttling settings for the workflow service as shown in the following screenshot.</span></span>  
  
     ![顯示 App Fabric 節流設定的螢幕擷取畫面。](./media/how-to-host-a-workflow-service-with-windows-server-app-fabric/app-fabric-throttling-configuration.gif)  
  
     <span data-ttu-id="d30f8-143">如需設定節流的詳細資訊，請參閱[使用 App Fabric 設定節流](https://docs.microsoft.com/previous-versions/appfabric/ee677261(v=azure.10))。</span><span class="sxs-lookup"><span data-stu-id="d30f8-143">For more information about configuring throttling see [Configuring Throttling with App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677261(v=azure.10)).</span></span>  
  
10. <span data-ttu-id="d30f8-144">選取 [**安全性**] 索引標籤。這可讓您設定應用程式的安全性設定，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-144">Select the **Security** tab. This allows you to configure security settings for the application as shown in the following screenshot.</span></span>  
  
     <span data-ttu-id="d30f8-145">![App Fabric 安全性設定](media/appfabricconfiguration-security.gif "AppFabricConfiguration-安全性")</span><span class="sxs-lookup"><span data-stu-id="d30f8-145">![App Fabric Security Configuration](media/appfabricconfiguration-security.gif "AppFabricConfiguration-Security")</span></span>  
  
     <span data-ttu-id="d30f8-146">如需使用 Windows Server App Fabric 設定安全性的詳細資訊，請參閱[使用 App fabric 設定安全性](https://docs.microsoft.com/previous-versions/appfabric/ee677278(v=azure.10))。</span><span class="sxs-lookup"><span data-stu-id="d30f8-146">For more information about configuring security with Windows Server App Fabric see [Configuring Security with App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677278(v=azure.10)).</span></span>  
  
### <a name="using-windows-server-app-fabric"></a><span data-ttu-id="d30f8-147">使用 Windows Server AppFabric</span><span class="sxs-lookup"><span data-stu-id="d30f8-147">Using Windows Server App Fabric</span></span>  
  
1. <span data-ttu-id="d30f8-148">建置方案，以便將必要的檔案複製到虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="d30f8-148">Build the solution to copy the necessary files to the virtual directory.</span></span>  
  
2. <span data-ttu-id="d30f8-149">以滑鼠右鍵按一下 [Orderclient]] 專案，然後選取 [ **Debug**，**啟動新的實例**] 來啟動用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="d30f8-149">Right click the OrderClient project and select **Debug**, **Start New Instance** to launch the client application.</span></span>  
  
3. <span data-ttu-id="d30f8-150">用戶端將會執行，Visual Studio 將會顯示 [**附加安全性警告**] 對話方塊中，按一下 [**不要附加**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d30f8-150">The client will run and Visual Studio will display an **Attach Security Warning** dialog box, click the **Don’t Attach** button.</span></span> <span data-ttu-id="d30f8-151">這樣會告知 Visual Studio 不要附加至 IIS 處理序進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="d30f8-151">This tells Visual Studio to not attach to the IIS process for debugging.</span></span>  
  
4. <span data-ttu-id="d30f8-152">用戶端應用程式會立即呼叫工作流程服務，然後等候。</span><span class="sxs-lookup"><span data-stu-id="d30f8-152">The client application will immediately call the Workflow service and then wait.</span></span> <span data-ttu-id="d30f8-153">工作流程服務將處於閒置狀態並保存。</span><span class="sxs-lookup"><span data-stu-id="d30f8-153">The workflow service will go idle and be persisted.</span></span> <span data-ttu-id="d30f8-154">您可以啟動 Internet Information Services (inetmgr.exe)、在 [連線] 窗格中巡覽至 OrderService，然後選取它，藉以確認這點。</span><span class="sxs-lookup"><span data-stu-id="d30f8-154">You can verify this by starting Internet Information Services (inetmgr.exe), navigating to the OrderService in the Connections pane and selecting it.</span></span> <span data-ttu-id="d30f8-155">接著，在右側窗格中，按一下 [AppFabric 儀表板] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-155">Next, click the App Fabric Dashboard icon in the right-hand pane.</span></span> <span data-ttu-id="d30f8-156">在持續性的 WF 實例底下，您會看到有一個持續性的工作流程服務實例，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-156">Under Persisted WF Instances you will see there is one persisted workflow service instance as shown in the following screenshot.</span></span>  
  
     ![顯示 App Fabric 儀表板的螢幕擷取畫面。](./media/how-to-host-a-workflow-service-with-windows-server-app-fabric/app-fabric-dashboard.gif)  
  
     <span data-ttu-id="d30f8-158">**WF 實例歷程記錄**會列出工作流程服務的相關資訊，例如工作流程服務啟動的數目、工作流程服務實例完成的數目，以及失敗的工作流程實例數目。</span><span class="sxs-lookup"><span data-stu-id="d30f8-158">The **WF Instance History** lists information about the workflow service such as the number of workflow service activations, the number of workflow service instance completions, and the number of workflow instances with failures.</span></span> <span data-ttu-id="d30f8-159">在 [作用中] 或 [閒置實例] 底下，會顯示連結，按一下此連結將會顯示有關閒置工作流程實例的詳細資訊，如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d30f8-159">Under Active or Idle instances a link will be displayed, clicking on the link will display more information about the idle workflow instances as shown in the following screenshot.</span></span>  
  
     ![顯示持續性工作流程實例詳細資料的螢幕擷取畫面。](./media/how-to-host-a-workflow-service-with-windows-server-app-fabric/persisted-workflow-instance-detail.gif)  
  
     <span data-ttu-id="d30f8-161">如需 Windows Server App Fabric 功能及其使用方式的詳細資訊，請參閱[Windows Server App Fabric 裝載功能](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="d30f8-161">For more information about Windows Server App Fabric features and how to use them see [Windows Server App Fabric Hosting Features](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d30f8-162">請參閱</span><span class="sxs-lookup"><span data-stu-id="d30f8-162">See also</span></span>

- [<span data-ttu-id="d30f8-163">建立長期執行的工作流程服務</span><span class="sxs-lookup"><span data-stu-id="d30f8-163">Creating a Long-running Workflow Service</span></span>](creating-a-long-running-workflow-service.md)
- <span data-ttu-id="d30f8-164">[Windows Server AppFabric 裝載功能](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="d30f8-164">[Windows Server App Fabric Hosting Features](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))</span></span>
- <span data-ttu-id="d30f8-165">[安裝 Windows Server App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee790960(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="d30f8-165">[Installing Windows Server App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee790960(v=azure.10))</span></span>
- <span data-ttu-id="d30f8-166">[Windows Server App Fabric 檔](https://docs.microsoft.com/previous-versions/appfabric/ff384253(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="d30f8-166">[Windows Server App Fabric Documentation](https://docs.microsoft.com/previous-versions/appfabric/ff384253(v=azure.10))</span></span>
