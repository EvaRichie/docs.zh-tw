---
title: 作法：將安裝程式新增至服務應用程式
description: 瞭解如何將安裝程式新增至您的服務應用程式。 Visual Studio 隨附的安裝元件可以安裝與服務應用程式相關聯的資源。
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, deploying
- installation components, adding to services
- installers, adding to services
- Windows Service applications, adding installers
- services, adding installers
- ServiceInstaller class, adding installers to services
- ServiceProcessInstaller class, adding installers to services
ms.assetid: 8b698e9a-b88e-4f44-ae45-e0c5ea0ae5a8
ms.openlocfilehash: 9a6954c75595f5297a31dcaf37e744e655733df4
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2020
ms.locfileid: "91608682"
---
# <a name="how-to-add-installers-to-your-service-application"></a><span data-ttu-id="fc948-104">作法：將安裝程式新增至服務應用程式</span><span class="sxs-lookup"><span data-stu-id="fc948-104">How to: Add Installers to Your Service Application</span></span>
<span data-ttu-id="fc948-105">Visual Studio 隨附安裝元件，可安裝與您服務應用程式相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="fc948-105">Visual Studio ships installation components that can install resources associated with your service applications.</span></span> <span data-ttu-id="fc948-106">安裝元件會在其安裝所在的系統上註冊個別服務，並讓服務控制管理員知道服務的存在。</span><span class="sxs-lookup"><span data-stu-id="fc948-106">Installation components register an individual service on the system to which it is being installed and let the Services Control Manager know that the service exists.</span></span> <span data-ttu-id="fc948-107">當您使用服務應用程式時，可以選取 [屬性] 視窗中的連結，以便自動將適當的安裝程式加入您的專案。</span><span class="sxs-lookup"><span data-stu-id="fc948-107">When you work with a service application, you can select a link in the Properties window to automatically add the appropriate installers to your project.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="fc948-108">適用於服務的屬性值會從服務類別複製到安裝程式類別。</span><span class="sxs-lookup"><span data-stu-id="fc948-108">Property values for your service are copied from the service class to the installer class.</span></span> <span data-ttu-id="fc948-109">如果您更新服務類別上的屬性值，不會在安裝程式中自動更新它們。</span><span class="sxs-lookup"><span data-stu-id="fc948-109">If you update the property values on the service class, they are not automatically updated in the installer.</span></span>  
  
 <span data-ttu-id="fc948-110">當您將安裝程式加入至專案時，新的類別 (預設命名為 `ProjectInstaller`) 會建立於專案中，並在其中建立適當安裝元件的執行個體。</span><span class="sxs-lookup"><span data-stu-id="fc948-110">When you add an installer to your project, a new class (which, by default, is named `ProjectInstaller`) is created in the project, and instances of the appropriate installation components are created within it.</span></span> <span data-ttu-id="fc948-111">此類別可用來作為專案所需全部安裝元件的中心點。</span><span class="sxs-lookup"><span data-stu-id="fc948-111">This class acts as a central point for all of the installation components your project needs.</span></span> <span data-ttu-id="fc948-112">例如，如果您將第二個服務加入至應用程式，然後按一下 [加入安裝程式] 連結，並不會建立第二個安裝程式類別；而是要將第二個服務所需的額外安裝元件加入至現有類別。</span><span class="sxs-lookup"><span data-stu-id="fc948-112">For example, if you add a second service to your application and click the Add Installer link, a second installer class is not created; instead, the necessary additional installation component for the second service is added to the existing class.</span></span>  
  
 <span data-ttu-id="fc948-113">您不需要在安裝程式內進行任何特殊編碼，即可正確安裝您的服務。</span><span class="sxs-lookup"><span data-stu-id="fc948-113">You do not need to do any special coding within the installers to make your services install correctly.</span></span> <span data-ttu-id="fc948-114">不過，如果您需要將特殊功能加入至安裝程序，偶爾可能需要修改安裝程式的內容。</span><span class="sxs-lookup"><span data-stu-id="fc948-114">However, you may occasionally need to modify the contents of the installers if you need to add special functionality to the installation process.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="fc948-115">您看到的對話方塊與功能表命令，可能會因您所使用的設定或版本，而與說明中所述不同。</span><span class="sxs-lookup"><span data-stu-id="fc948-115">The dialog boxes and menu commands you see might differ from those described in Help depending on your active settings or edition.</span></span> <span data-ttu-id="fc948-116">若要變更您的設定，請在 [工具]\*\*\*\* 功能表上選擇 [匯入和匯出設定]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="fc948-116">To change your settings, choose **Import and Export Settings** on the **Tools** menu.</span></span> <span data-ttu-id="fc948-117">如需詳細資訊，請參閱 [個人化 VISUAL STUDIO IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。</span><span class="sxs-lookup"><span data-stu-id="fc948-117">For more information, see [Personalize the Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide).</span></span>  
  
### <a name="to-add-installers-to-your-service-application"></a><span data-ttu-id="fc948-118">將安裝程式加入服務應用程式</span><span class="sxs-lookup"><span data-stu-id="fc948-118">To add installers to your service application</span></span>  
  
1. <span data-ttu-id="fc948-119">在 [方案總管]\*\*\*\* 中，針對您想要加入安裝元件的服務，存取服務的 [設計]\*\*\*\* 檢視。</span><span class="sxs-lookup"><span data-stu-id="fc948-119">In **Solution Explorer**, access **Design** view for the service for which you want to add an installation component.</span></span>  
  
2. <span data-ttu-id="fc948-120">按一下設計工具的背景以選取服務本身，而不是它的任何內容。</span><span class="sxs-lookup"><span data-stu-id="fc948-120">Click the background of the designer to select the service itself, rather than any of its contents.</span></span>  
  
3. <span data-ttu-id="fc948-121">以設計工具為焦點，按一下滑鼠右鍵，然後按一下 **[加入安裝程式]**。</span><span class="sxs-lookup"><span data-stu-id="fc948-121">With the designer in focus, right-click, and then click **Add Installer**.</span></span>  
  
     <span data-ttu-id="fc948-122">隨即會在您的專案中加入一個新類別 (`ProjectInstaller`) 和兩個安裝元件 (<xref:System.ServiceProcess.ServiceProcessInstaller> 與 <xref:System.ServiceProcess.ServiceInstaller>)，並將服務的屬性值複製到元件。</span><span class="sxs-lookup"><span data-stu-id="fc948-122">A new class, `ProjectInstaller`, and two installation components, <xref:System.ServiceProcess.ServiceProcessInstaller> and <xref:System.ServiceProcess.ServiceInstaller>, are added to your project, and property values for the service are copied to the components.</span></span>  
  
4. <span data-ttu-id="fc948-123">按一下 <xref:System.ServiceProcess.ServiceInstaller> 元件，並確認已將 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 屬性的值設定為與服務本身 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 屬性相同的值。</span><span class="sxs-lookup"><span data-stu-id="fc948-123">Click the <xref:System.ServiceProcess.ServiceInstaller> component and verify that the value of the <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> property is set to the same value as the <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> property on the service itself.</span></span>  
  
5. <span data-ttu-id="fc948-124">若要決定服務啟動方式，按一下 <xref:System.ServiceProcess.ServiceInstaller> 元件，並將 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 屬性設定為適當的值。</span><span class="sxs-lookup"><span data-stu-id="fc948-124">To determine how your service will be started, click the <xref:System.ServiceProcess.ServiceInstaller> component and set the <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> property to the appropriate value.</span></span>  
  
    |<span data-ttu-id="fc948-125">值</span><span class="sxs-lookup"><span data-stu-id="fc948-125">Value</span></span>|<span data-ttu-id="fc948-126">結果</span><span class="sxs-lookup"><span data-stu-id="fc948-126">Result</span></span>|  
    |-----------|------------|  
    |<xref:System.ServiceProcess.ServiceStartMode.Manual>|<span data-ttu-id="fc948-127">服務必須在安裝之後手動啟動。</span><span class="sxs-lookup"><span data-stu-id="fc948-127">The service must be manually started after installation.</span></span> <span data-ttu-id="fc948-128">如需詳細資訊，請參閱[如何：啟動服務](how-to-start-services.md)。</span><span class="sxs-lookup"><span data-stu-id="fc948-128">For more information, see [How to: Start Services](how-to-start-services.md).</span></span>|  
    |<xref:System.ServiceProcess.ServiceStartMode.Automatic>|<span data-ttu-id="fc948-129">服務將在電腦重新開機時自行啟動。</span><span class="sxs-lookup"><span data-stu-id="fc948-129">The service will start by itself whenever the computer reboots.</span></span>|  
    |<xref:System.ServiceProcess.ServiceStartMode.Disabled>|<span data-ttu-id="fc948-130">無法啟動服務。</span><span class="sxs-lookup"><span data-stu-id="fc948-130">The service cannot be started.</span></span>|  
  
6. <span data-ttu-id="fc948-131">若要決定服務將在其中執行的安全性內容，按一下 <xref:System.ServiceProcess.ServiceProcessInstaller> 元件，並設定適當的屬性值。</span><span class="sxs-lookup"><span data-stu-id="fc948-131">To determine the security context in which your service will run, click the <xref:System.ServiceProcess.ServiceProcessInstaller> component and set the appropriate property values.</span></span> <span data-ttu-id="fc948-132">如需詳細資訊，請參閱[如何：指定服務的安全性內容](how-to-specify-the-security-context-for-services.md)。</span><span class="sxs-lookup"><span data-stu-id="fc948-132">For more information, see [How to: Specify the Security Context for Services](how-to-specify-the-security-context-for-services.md).</span></span>  
  
7. <span data-ttu-id="fc948-133">覆寫任何您需要為其執行自訂處理的方法。</span><span class="sxs-lookup"><span data-stu-id="fc948-133">Override any methods for which you need to perform custom processing.</span></span>  
  
8. <span data-ttu-id="fc948-134">針對專案中的每個額外服務執行步驟 1 到 7。</span><span class="sxs-lookup"><span data-stu-id="fc948-134">Perform steps 1 through 7 for each additional service in your project.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="fc948-135">針對專案中的每個額外服務，您必須在專案的 `ProjectInstaller` 類別中加入額外的 <xref:System.ServiceProcess.ServiceInstaller> 元件。</span><span class="sxs-lookup"><span data-stu-id="fc948-135">For each additional service in your project, you must add an additional <xref:System.ServiceProcess.ServiceInstaller> component to the project's `ProjectInstaller` class.</span></span> <span data-ttu-id="fc948-136">在步驟三加入的 <xref:System.ServiceProcess.ServiceProcessInstaller> 元件適用於專案中所有的個別服務安裝程式。</span><span class="sxs-lookup"><span data-stu-id="fc948-136">The <xref:System.ServiceProcess.ServiceProcessInstaller> component added in step three works with all of the individual service installers in the project.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fc948-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fc948-137">See also</span></span>

- [<span data-ttu-id="fc948-138">Windows 服務應用程式簡介</span><span class="sxs-lookup"><span data-stu-id="fc948-138">Introduction to Windows Service Applications</span></span>](introduction-to-windows-service-applications.md)
- [<span data-ttu-id="fc948-139">作法：安裝和解除安裝服務</span><span class="sxs-lookup"><span data-stu-id="fc948-139">How to: Install and Uninstall Services</span></span>](how-to-install-and-uninstall-services.md)
- [<span data-ttu-id="fc948-140">作法：啟動服務</span><span class="sxs-lookup"><span data-stu-id="fc948-140">How to: Start Services</span></span>](how-to-start-services.md)
- [<span data-ttu-id="fc948-141">作法：指定服務的資訊安全內容</span><span class="sxs-lookup"><span data-stu-id="fc948-141">How to: Specify the Security Context for Services</span></span>](how-to-specify-the-security-context-for-services.md)
