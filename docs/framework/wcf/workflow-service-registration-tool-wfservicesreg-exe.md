---
title: WorkFlow 服務登錄工具 (WFServicesReg.exe)
ms.date: 03/30/2017
ms.assetid: 9e92c87b-99c5-4e8d-9d53-7944cc2b47d3
ms.openlocfilehash: 763b617a99c98383b5b873e4fb8646884f9b5253
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96261874"
---
# <a name="workflow-service-registration-tool-wfservicesregexe"></a><span data-ttu-id="5d941-102">WorkFlow 服務登錄工具 (WFServicesReg.exe)</span><span class="sxs-lookup"><span data-stu-id="5d941-102">WorkFlow Service Registration Tool (WFServicesReg.exe)</span></span>

<span data-ttu-id="5d941-103">Workflow 服務登錄工具 (WFServicesReg.exe) 是一個獨立工具，可用於新增、移除或修復 Windows Workflow Foundation (WF) 服務的組態項目。</span><span class="sxs-lookup"><span data-stu-id="5d941-103">Workflow Services Registration tool (WFServicesReg.exe) is a stand-alone tool that can be used to add, remove, or repair the configuration elements for Windows Workflow Foundation (WF) services.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5d941-104">語法</span><span class="sxs-lookup"><span data-stu-id="5d941-104">Syntax</span></span>  
  
```console  
WFServicesReg.exe [-c | -r | -v | -m | -i]  
```  
  
## <a name="remarks"></a><span data-ttu-id="5d941-105">備註</span><span class="sxs-lookup"><span data-stu-id="5d941-105">Remarks</span></span>  

 <span data-ttu-id="5d941-106">您可以在 .NET Framework 3.5 安裝位置（尤其是%windir%\Microsoft.NET\Framework\v3.5）或64位電腦的%windir%\Microsoft.NET\Framework64\v3.5 中找到此工具。</span><span class="sxs-lookup"><span data-stu-id="5d941-106">The tool can be found at the .NET Framework 3.5 installation location, specifically, %windir%\Microsoft.NET\Framework\v3.5, or at %windir%\Microsoft.NET\Framework64\v3.5 in 64-bit machines.</span></span>  
  
 <span data-ttu-id="5d941-107">下表描述可與 Workflow 服務登錄工具 (WFServicesReg.exe) 搭配使用的選項。</span><span class="sxs-lookup"><span data-stu-id="5d941-107">The following tables describe the options that can be used with the Workflow Services Registration tool (WFServicesReg.exe).</span></span>  
  
|<span data-ttu-id="5d941-108">選項</span><span class="sxs-lookup"><span data-stu-id="5d941-108">Option</span></span>|<span data-ttu-id="5d941-109">描述</span><span class="sxs-lookup"><span data-stu-id="5d941-109">Description</span></span>|  
|------------|-----------------|  
|`/c`|<span data-ttu-id="5d941-110">設定 Windows 工作流程服務。</span><span class="sxs-lookup"><span data-stu-id="5d941-110">Configures Windows Workflow Services.</span></span> <span data-ttu-id="5d941-111">用於安裝和修復案例中。</span><span class="sxs-lookup"><span data-stu-id="5d941-111">Used in install and repair scenarios.</span></span>|  
|`/r`|<span data-ttu-id="5d941-112">移除 Windows 工作流程服務組態。</span><span class="sxs-lookup"><span data-stu-id="5d941-112">Removes Windows Workflow Services Configuration.</span></span>|  
|`/v`|<span data-ttu-id="5d941-113">列印詳細資訊 (適用於設定或移除)。</span><span class="sxs-lookup"><span data-stu-id="5d941-113">Print verbose information (for either configuration or removal).</span></span>|  
|`/m`|<span data-ttu-id="5d941-114">啟用 MSI 記錄格式。</span><span class="sxs-lookup"><span data-stu-id="5d941-114">Enables MSI logging format.</span></span>|  
|`/i`|<span data-ttu-id="5d941-115">應用程式執行時，最小化視窗。</span><span class="sxs-lookup"><span data-stu-id="5d941-115">Minimizes the window when the application runs.</span></span>|  
  
## <a name="registration"></a><span data-ttu-id="5d941-116">註冊</span><span class="sxs-lookup"><span data-stu-id="5d941-116">Registration</span></span>  

 <span data-ttu-id="5d941-117">工具會檢查 Web.config 檔案並註冊下列項目：</span><span class="sxs-lookup"><span data-stu-id="5d941-117">The tool inspects the Web.config file and registers the following:</span></span>  
  
- <span data-ttu-id="5d941-118">.NET Framework 3.5 參考元件。</span><span class="sxs-lookup"><span data-stu-id="5d941-118">.NET Framework 3.5 reference assemblies.</span></span>  
  
- <span data-ttu-id="5d941-119">.xoml 檔案的組建提供者。</span><span class="sxs-lookup"><span data-stu-id="5d941-119">A build provider for .xoml files.</span></span>  
  
- <span data-ttu-id="5d941-120">.xoml 和 .rules 檔案的 HTTP 處理常式。</span><span class="sxs-lookup"><span data-stu-id="5d941-120">HTTP handlers for .xoml and .rules files.</span></span>  
  
 <span data-ttu-id="5d941-121">工具會檢查 Machine.config 檔案並註冊下列延伸項目：</span><span class="sxs-lookup"><span data-stu-id="5d941-121">The tool inspects the Machine.config file and registers the following extensions:</span></span>  
  
- <span data-ttu-id="5d941-122">behaviorExtensions</span><span class="sxs-lookup"><span data-stu-id="5d941-122">behaviorExtensions</span></span>  
  
- <span data-ttu-id="5d941-123">bindingElementExtensions</span><span class="sxs-lookup"><span data-stu-id="5d941-123">bindingElementExtensions</span></span>  
  
- <span data-ttu-id="5d941-124">bindingExtensions</span><span class="sxs-lookup"><span data-stu-id="5d941-124">bindingExtensions</span></span>  
  
 <span data-ttu-id="5d941-125">工具也會註冊下列用戶端中繼資料匯入工具：</span><span class="sxs-lookup"><span data-stu-id="5d941-125">The tool also registers the following client metadata importers:</span></span>  
  
- <span data-ttu-id="5d941-126">policyImporters</span><span class="sxs-lookup"><span data-stu-id="5d941-126">policyImporters</span></span>  
  
- <span data-ttu-id="5d941-127">wsdlImporters</span><span class="sxs-lookup"><span data-stu-id="5d941-127">wsdlImporters</span></span>  
  
 <span data-ttu-id="5d941-128">工具也會在 IIS Metabase 中註冊 .xoml 和 .rules Scriptmap 與處理常式。</span><span class="sxs-lookup"><span data-stu-id="5d941-128">The tool also registers .xoml and .rules scriptmaps and handlers in the IIS metabase.</span></span>  
  
 <span data-ttu-id="5d941-129">在 Windows Server 2003 和 Windows XP 電腦上 (IIS 5.1 和 IIS 6.0) ，會註冊一組 xoml 和。</span><span class="sxs-lookup"><span data-stu-id="5d941-129">On Windows Server 2003 and Windows XP machines (IIS 5.1 and IIS 6.0), one set of .xoml and .rules scriptmaps are registered.</span></span>  
  
 <span data-ttu-id="5d941-130">在 64 位元電腦上，如果已啟用 `Enable32BitAppOnWin64` 參數，此工具就會註冊 WOW 模式 Scriptmap，如果已停用 `Enable32BitAppOnWin64` 參數，則會註冊原生 64 位元 Scriptmap。</span><span class="sxs-lookup"><span data-stu-id="5d941-130">On 64-bit machines, the tool registers WOW mode scriptmaps if the `Enable32BitAppOnWin64` switch is enabled, or native 64-bit scriptmaps if the `Enable32BitAppOnWin64` switch is disabled.</span></span>  
  
 <span data-ttu-id="5d941-131">在 Windows Vista 和 Windows Server 2008 (IIS 7.0 和更新版本) 電腦上，會註冊兩組 xoml 和. 規則處理常式：一組用於整合模式，另一組用於傳統模式。</span><span class="sxs-lookup"><span data-stu-id="5d941-131">On Windows Vista and Windows Server 2008 (IIS 7.0 and above) machines, two sets of .xoml and .rules handlers are registered: one for Integrated mode and one for Classic mode.</span></span>  
  
 <span data-ttu-id="5d941-132">在 64 位元電腦上，會註冊三組處理常式 (無論 `Enable32BitAppOnWin64` 參數的狀態為何)：一組用於整合模式，一組用於 WOW 傳統模式，一組用於原生 64 位元傳統模式。</span><span class="sxs-lookup"><span data-stu-id="5d941-132">On 64-bit machines, three sets of handlers are registered (regardless of the state of the `Enable32BitAppOnWin64` switch): one for Integrated mode, one for WOW Classic mode and one for native 64-bit Classic mode.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="5d941-133">與 ServiceModelreg.exe 不同的是，WFServicesReg.exe 不允許新增、移除或修復用於特定網站的 Scriptmap 或處理常式。</span><span class="sxs-lookup"><span data-stu-id="5d941-133">Unlike ServiceModelreg.exe, WFServicesReg.exe does not allow adding, removing, or repairing scriptmaps or handlers for a particular Web site.</span></span> <span data-ttu-id="5d941-134">如需這個問題的解決方法，請參閱「修復 Scriptmap」一節。</span><span class="sxs-lookup"><span data-stu-id="5d941-134">For a workaround to this issue, see the "Repairing the Scriptmaps" section.</span></span>  
  
## <a name="usage-scenarios"></a><span data-ttu-id="5d941-135">使用案例</span><span class="sxs-lookup"><span data-stu-id="5d941-135">Usage Scenarios</span></span>  
  
### <a name="installing-iis-after-net-framework-35-is-installed"></a><span data-ttu-id="5d941-136">在安裝 .NET Framework 3.5 之後安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="5d941-136">Installing IIS after .NET Framework 3.5 is installed</span></span>  

 <span data-ttu-id="5d941-137">在 Windows Server 2003 電腦上，.NET Framework 3.5 會在安裝 IIS 之前安裝。</span><span class="sxs-lookup"><span data-stu-id="5d941-137">On a Windows Server 2003 machine, .NET Framework 3.5 is installed prior to IIS installation.</span></span> <span data-ttu-id="5d941-138">由於 IIS 的元資料庫無法使用，因此 .NET Framework 3.5 的安裝會成功，而不需要安裝 xoml 和. 規則腳本。</span><span class="sxs-lookup"><span data-stu-id="5d941-138">Due to the unavailability of the IIS metabase, installation of .NET Framework 3.5 succeeds without installing .xoml and .rules scriptmaps.</span></span>  
  
 <span data-ttu-id="5d941-139">安裝 IIS 之後，您可以使用 WFServicesReg.exe 工具搭配 `/c` 參數來安裝這些特定 Scriptmap。</span><span class="sxs-lookup"><span data-stu-id="5d941-139">After IIS is installed, you can use the WFServicesReg.exe tool with the `/c` switch to install these specific scriptmaps.</span></span>  
  
### <a name="repairing-the-scriptmaps"></a><span data-ttu-id="5d941-140">修復 Scriptmap</span><span class="sxs-lookup"><span data-stu-id="5d941-140">Repairing the Scriptmaps</span></span>  
  
#### <a name="scriptmap-deleted-under-web-sites-node"></a><span data-ttu-id="5d941-141">在網站節點下刪除的 Scriptmap</span><span class="sxs-lookup"><span data-stu-id="5d941-141">Scriptmap deleted under Web Sites node</span></span>  

 <span data-ttu-id="5d941-142">在 Windows Server 2003 電腦上，xoml 或。不小心刪除 [網站] 節點中的規則。</span><span class="sxs-lookup"><span data-stu-id="5d941-142">On a Windows Server 2003 machine, .xoml or .rules is accidentally deleted from the Web Sites node.</span></span> <span data-ttu-id="5d941-143">您可以使用 `/c` 參數執行 WFServicesReg.exe 工具修復這種情況。</span><span class="sxs-lookup"><span data-stu-id="5d941-143">This can be repaired by running the WFServicesReg.exe tool with the `/c` switch.</span></span>  
  
#### <a name="scriptmap-deleted-under-a-particular-web-site"></a><span data-ttu-id="5d941-144">在特定網站下刪除的 Scriptmap</span><span class="sxs-lookup"><span data-stu-id="5d941-144">Scriptmap deleted under a particular Web site</span></span>  

 <span data-ttu-id="5d941-145">在 Windows Server 2003 電腦上，xoml 或。不小心刪除特定網站 (例如，預設的網站) ，而不是從 [網站] 節點。</span><span class="sxs-lookup"><span data-stu-id="5d941-145">On a Windows Server 2003 machine, .xoml or .rules is accidentally deleted from a particular Web site (for example, the Default Web Site) rather than from the Web Sites node.</span></span>  
  
 <span data-ttu-id="5d941-146">若要修復特定網站的已刪除處理常式，您應該執行 "WFServicesReg.exe/r" 來移除所有網站的處理常式，然後執行 "WFServicesReg.exe/c" 來為所有網站建立適當的處理常式。</span><span class="sxs-lookup"><span data-stu-id="5d941-146">To repair deleted handlers for a particular Web site, you should run "WFServicesReg.exe /r" to remove handlers from all Web sites, then run "WFServicesReg.exe /c" to create the appropriate handlers for all Web sites.</span></span>  
  
### <a name="configuring-handlers-after-switching-iis-mode"></a><span data-ttu-id="5d941-147">在切換 IIS 模式之後設定處理常式</span><span class="sxs-lookup"><span data-stu-id="5d941-147">Configuring handlers after switching IIS mode</span></span>  

 <span data-ttu-id="5d941-148">當 IIS 處於共用設定模式，且安裝了 .NET Framework 3.5 時，就會在共用位置下設定 IIS 元資料庫。</span><span class="sxs-lookup"><span data-stu-id="5d941-148">When IIS is in shared configuration mode and .NET Framework 3.5 is installed, the IIS metabase is configured under a shared location.</span></span> <span data-ttu-id="5d941-149">如果將 IIS 切換為非共用組態模式，本機 Metabase 將不會包含所需的處理常式。</span><span class="sxs-lookup"><span data-stu-id="5d941-149">If you switch IIS to non-shared configuration mode, the local metabase will not contain the required handlers.</span></span> <span data-ttu-id="5d941-150">若要正確設定本機的元資料庫，您可以將共用的元資料庫匯入至本機，或執行 "WFServicesReg.exe/c"，以設定本機的元資料庫。</span><span class="sxs-lookup"><span data-stu-id="5d941-150">To configure the local metabase properly, you can either import the shared metabase to local, or run "WFServicesReg.exe /c", which configures the local metabase.</span></span>
