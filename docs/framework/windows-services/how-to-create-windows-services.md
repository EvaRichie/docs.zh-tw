---
title: 作法：建立 Windows 服務
description: 使用 [Windows 服務] 專案範本來建立服務。 設定 ServiceName 屬性、建立安裝程式，以及覆寫 OnStart 和 OnStop 方法。
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, creating
- templates, Windows Service
ms.assetid: 0f5e2cbb-d95d-477c-b2b5-4b990e6b86ff
author: ghogen
ms.openlocfilehash: 6918225e39c15a52710fd0d56342aae869b42325
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925770"
---
# <a name="how-to-create-windows-services"></a><span data-ttu-id="8d9f0-104">作法：建立 Windows 服務</span><span class="sxs-lookup"><span data-stu-id="8d9f0-104">How to: Create Windows Services</span></span>
<span data-ttu-id="8d9f0-105">當您建立服務時，可以使用稱為 **Windows 服務**的 Visual Studio 專案範本。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-105">When you create a service, you can use a Visual Studio project template called **Windows Service**.</span></span> <span data-ttu-id="8d9f0-106">這個範本會透過參考適當的類別和命名空間、設定繼承自服務的基底類別，以及覆寫您可能想要覆寫的其中幾個方法，來自動為您執行大部分的工作。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-106">This template automatically does much of the work for you by referencing the appropriate classes and namespaces, setting up the inheritance from the base class for services, and overriding several of the methods you're likely to want to override.</span></span>  
  
> [!WARNING]
> <span data-ttu-id="8d9f0-107">您無法在 Express 版的 Visual Studio 中使用 Windows 服務專案範本。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-107">The Windows Services project template is not available in the Express edition of Visual Studio.</span></span>  
  
 <span data-ttu-id="8d9f0-108">若要建立可運作的服務，您必須至少：</span><span class="sxs-lookup"><span data-stu-id="8d9f0-108">At a minimum, to create a functional service you must:</span></span>  
  
- <span data-ttu-id="8d9f0-109">設定 <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-109">Set the <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> property.</span></span>  
  
- <span data-ttu-id="8d9f0-110">建立服務應用程式的必要安裝程式。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-110">Create the necessary installers for your service application.</span></span>  
  
- <span data-ttu-id="8d9f0-111">覆寫並指定 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 和 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 方法的程式碼，以自訂服務的運作方式。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-111">Override and specify code for the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> and <xref:System.ServiceProcess.ServiceBase.OnStop%2A> methods to customize the ways in which your service behaves.</span></span>  
  
### <a name="to-create-a-windows-service-application"></a><span data-ttu-id="8d9f0-112">建立 Windows 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="8d9f0-112">To create a Windows Service application</span></span>  
  
1. <span data-ttu-id="8d9f0-113">建立 **Windows 服務**專案。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-113">Create a **Windows Service** project.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="8d9f0-114">如需不使用範本撰寫服務的指示，請參閱[如何：以程式設計方式撰寫服務](how-to-write-services-programmatically.md)。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-114">For instructions on writing a service without using the template, see [How to: Write Services Programmatically](how-to-write-services-programmatically.md).</span></span>  
  
2. <span data-ttu-id="8d9f0-115">在 [屬性]\*\*\*\* 視窗中，設定服務的 <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-115">In the **Properties** window, set the <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> property for your service.</span></span>  
  
     <span data-ttu-id="8d9f0-116">![設定 ServiceName 屬性。](./media/windowsservice-servicename.PNG "WindowsService_ServiceName")</span><span class="sxs-lookup"><span data-stu-id="8d9f0-116">![Set the ServiceName property.](./media/windowsservice-servicename.PNG "WindowsService_ServiceName")</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="8d9f0-117"><xref:System.ServiceProcess.ServiceBase.ServiceName%2A> 屬性的值必須一律符合安裝程式類別中所記錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-117">The value of the <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> property must always match the name recorded in the installer classes.</span></span> <span data-ttu-id="8d9f0-118">如果您變更這個屬性，也必須更新安裝程式類別的 <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-118">If you change this property, you must update the <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> property of installer classes as well.</span></span>  
  
3. <span data-ttu-id="8d9f0-119">設定下列任何屬性，以決定服務的運作方式。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-119">Set any of the following properties to determine how your service will function.</span></span>  
  
    |<span data-ttu-id="8d9f0-120">屬性</span><span class="sxs-lookup"><span data-stu-id="8d9f0-120">Property</span></span>|<span data-ttu-id="8d9f0-121">設定</span><span class="sxs-lookup"><span data-stu-id="8d9f0-121">Setting</span></span>|  
    |--------------|-------------|  
    |<xref:System.ServiceProcess.ServiceBase.CanStop%2A>|<span data-ttu-id="8d9f0-122">如果為 `True`，則表示服務會接受停止執行的要求；如果為 `false`，則不會停止服務。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-122">`True` to indicate that the service will accept requests to stop running; `false` to prevent the service from being stopped.</span></span>|  
    |<xref:System.ServiceProcess.ServiceBase.CanShutdown%2A>|<span data-ttu-id="8d9f0-123">如果為 `True`，則表示當服務所在的電腦關機時，服務想要收到通知，以便呼叫 <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> 程序。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-123">`True` to indicate that the service wants to receive notification when the computer on which it lives shuts down, enabling it to call the <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> procedure.</span></span>|  
    |<xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A>|<span data-ttu-id="8d9f0-124">如果為 `True`，則表示服務會接受暫停或繼續執行的要求；如果為 `false`，則表示不會暫停及繼續服務。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-124">`True` to indicate that the service will accept requests to pause or to resume running; `false` to prevent the service from being paused and resumed.</span></span>|  
    |<xref:System.ServiceProcess.ServiceBase.CanHandlePowerEvent%2A>|<span data-ttu-id="8d9f0-125">`True` 表示服務可以處理電腦電源狀態變更的通知；`false` 則會防止服務收到這些變更的通知。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-125">`True` to indicate that the service can handle notification of changes to the computer's power status; `false` to prevent the service from being notified of these changes.</span></span>|  
    |<xref:System.ServiceProcess.ServiceBase.AutoLog%2A>|<span data-ttu-id="8d9f0-126">如果為 `True`，則會在服務執行動作時，將資訊項目寫入應用程式事件記錄檔；如果為 `false`，則會停用這項功能。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-126">`True` to write informational entries to the Application event log when your service performs an action; `false` to disable this functionality.</span></span> <span data-ttu-id="8d9f0-127">如需詳細資訊，請參閱[如何：記錄關於服務的資訊](how-to-log-information-about-services.md)。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-127">For more information, see [How to: Log Information About Services](how-to-log-information-about-services.md).</span></span> <span data-ttu-id="8d9f0-128">**注意：** 預設會將 <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> 設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-128">**Note:**  By default, <xref:System.ServiceProcess.ServiceBase.AutoLog%2A> is set to `true`.</span></span>|  
  
    > [!NOTE]
    > <span data-ttu-id="8d9f0-129">當 <xref:System.ServiceProcess.ServiceBase.CanStop%2A> 或 <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> 設定為 `false` 時，**服務控制管理員**將會停用對應的功能表選項，以停止、暫停或繼續服務。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-129">When <xref:System.ServiceProcess.ServiceBase.CanStop%2A> or <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> are set to `false`, the **Service Control Manager** will disable the corresponding menu options to stop, pause, or continue the service.</span></span>  
  
4. <span data-ttu-id="8d9f0-130">存取程式碼編輯器，然後填入您想要對 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 和 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 程序進行的處理。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-130">Access the Code Editor and fill in the processing you want for the <xref:System.ServiceProcess.ServiceBase.OnStart%2A> and <xref:System.ServiceProcess.ServiceBase.OnStop%2A> procedures.</span></span>  
  
5. <span data-ttu-id="8d9f0-131">覆寫您想要定義功能的其他任何方法。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-131">Override any other methods for which you want to define functionality.</span></span>  
  
6. <span data-ttu-id="8d9f0-132">為服務應用程式加入必要的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-132">Add the necessary installers for your service application.</span></span> <span data-ttu-id="8d9f0-133">如需詳細資訊，請參閱[如何：將安裝程式加入服務應用程式](how-to-add-installers-to-your-service-application.md)。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-133">For more information, see [How to: Add Installers to Your Service Application](how-to-add-installers-to-your-service-application.md).</span></span>  
  
7. <span data-ttu-id="8d9f0-134">從 [建置]\*\*\*\* 功能表選取 [建置方案]\*\*\*\*，以建置您的專案。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-134">Build your project by selecting **Build Solution** from the **Build** menu.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="8d9f0-135">請勿按 F5 執行您的專案，您無法透過這個方法來執行服務專案。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-135">Do not press F5 to run your project — you cannot run a service project in this way.</span></span>  
  
8. <span data-ttu-id="8d9f0-136">安裝服務。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-136">Install the service.</span></span> <span data-ttu-id="8d9f0-137">如需詳細資訊，請參閱 [How to: Install and Uninstall Services](how-to-install-and-uninstall-services.md)。</span><span class="sxs-lookup"><span data-stu-id="8d9f0-137">For more information, see [How to: Install and Uninstall Services](how-to-install-and-uninstall-services.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8d9f0-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8d9f0-138">See also</span></span>

- [<span data-ttu-id="8d9f0-139">Windows 服務應用程式簡介</span><span class="sxs-lookup"><span data-stu-id="8d9f0-139">Introduction to Windows Service Applications</span></span>](introduction-to-windows-service-applications.md)
- [<span data-ttu-id="8d9f0-140">作法：以程式設計方式撰寫服務</span><span class="sxs-lookup"><span data-stu-id="8d9f0-140">How to: Write Services Programmatically</span></span>](how-to-write-services-programmatically.md)
- [<span data-ttu-id="8d9f0-141">作法：將安裝程式新增至服務應用程式</span><span class="sxs-lookup"><span data-stu-id="8d9f0-141">How to: Add Installers to Your Service Application</span></span>](how-to-add-installers-to-your-service-application.md)
- [<span data-ttu-id="8d9f0-142">作法：記錄關於服務的資訊</span><span class="sxs-lookup"><span data-stu-id="8d9f0-142">How to: Log Information About Services</span></span>](how-to-log-information-about-services.md)
- [<span data-ttu-id="8d9f0-143">作法：啟動服務</span><span class="sxs-lookup"><span data-stu-id="8d9f0-143">How to: Start Services</span></span>](how-to-start-services.md)
- [<span data-ttu-id="8d9f0-144">作法：指定服務的資訊安全內容</span><span class="sxs-lookup"><span data-stu-id="8d9f0-144">How to: Specify the Security Context for Services</span></span>](how-to-specify-the-security-context-for-services.md)
- [<span data-ttu-id="8d9f0-145">作法：安裝和解除安裝服務</span><span class="sxs-lookup"><span data-stu-id="8d9f0-145">How to: Install and Uninstall Services</span></span>](how-to-install-and-uninstall-services.md)
- [<span data-ttu-id="8d9f0-146">逐步解說：在元件設計工具中建立 Windows 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="8d9f0-146">Walkthrough: Creating a Windows Service Application in the Component Designer</span></span>](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)
