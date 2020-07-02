---
title: 如何對 CLR 啟用問題進行偵錯
description: 請參閱如何在 .NET 中偵測 common language runtime （CLR）的啟用問題。 查看和偵測 CLR 啟用記錄，這可能有助於判斷根本原因。
ms.date: 03/30/2017
helpviewer_keywords:
- CLR activation, debugging issues
ms.assetid: 4fe17546-d56e-4344-a930-6d8e4a545914
ms.openlocfilehash: 5215e82aebf93fa8d6d1937563ab348126a01d97
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622610"
---
# <a name="how-to-debug-clr-activation-issues"></a><span data-ttu-id="d0278-104">如何對 CLR 啟用問題進行偵錯</span><span class="sxs-lookup"><span data-stu-id="d0278-104">How to debug CLR activation issues</span></span>

<span data-ttu-id="d0278-105">如果以正確的通用語言執行平台 (CLR) 版本執行應用程式時發生問題，您可以檢視並偵錯 CLR 啟用記錄。</span><span class="sxs-lookup"><span data-stu-id="d0278-105">If you encounter problems in getting your application to run with the correct version of the common language runtime (CLR), you can view and debug CLR activation logs.</span></span> <span data-ttu-id="d0278-106">當您的應用程式載入不符預期的 CLR 版本，或完全不載入 CLR 時，這些記錄檔對判斷啟動問題的根本原因非常有幫助。</span><span class="sxs-lookup"><span data-stu-id="d0278-106">These logs can be very useful in determining the root cause of an activation issue, when your application either loads a different CLR version than expected or doesn't load the CLR at all.</span></span> <span data-ttu-id="d0278-107">[NET Framework 初始化錯誤：管理使用者經驗](initialization-errors-managing-the-user-experience.md) 會討論應用程式找不到任何 CLR 時的經驗。</span><span class="sxs-lookup"><span data-stu-id="d0278-107">The [.NET Framework Initialization Errors: Managing the User Experience](initialization-errors-managing-the-user-experience.md) discusses the experience when no CLR is found for an application.</span></span>

<span data-ttu-id="d0278-108">使用 HKEY_LOCAL_MACHINE 登錄機碼或系統環境變數可以啟用全系統的 CLR 啟動記錄。</span><span class="sxs-lookup"><span data-stu-id="d0278-108">CLR activation logging can be enabled system-wide by using an HKEY_LOCAL_MACHINE registry key or a system environment variable.</span></span> <span data-ttu-id="d0278-109">登錄項目或環境變數移除之前會一直產生記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d0278-109">The log will be generated until the registry entry or the environment variable is removed.</span></span> <span data-ttu-id="d0278-110">或者，您可以使用使用者或處理序本機環境變數，啟用不同範圍和持續時間的記錄。</span><span class="sxs-lookup"><span data-stu-id="d0278-110">Alternatively, you can use a user or process-local environment variable to enable logging with a different scope and duration.</span></span>

<span data-ttu-id="d0278-111">CLR 啟動記錄檔不應該與[assembly binding logs組件繫結記錄檔](../tools/fuslogvw-exe-assembly-binding-log-viewer.md)相混淆，兩者截然不同。</span><span class="sxs-lookup"><span data-stu-id="d0278-111">CLR activation logs shouldn't be confused with [assembly binding logs](../tools/fuslogvw-exe-assembly-binding-log-viewer.md), which are entirely different.</span></span>

## <a name="to-enable-clr-activation-logging"></a><span data-ttu-id="d0278-112">啟用 CLR 啟動記錄</span><span class="sxs-lookup"><span data-stu-id="d0278-112">To enable CLR activation logging</span></span>

### <a name="using-the-registry"></a><span data-ttu-id="d0278-113">使用登錄</span><span class="sxs-lookup"><span data-stu-id="d0278-113">Using the registry</span></span>

1. <span data-ttu-id="d0278-114">在登錄編輯器中瀏覽至 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework (32 位元電腦) 或 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework 資料夾 (64 位元電腦)。</span><span class="sxs-lookup"><span data-stu-id="d0278-114">In the Registry Editor, navigate to HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework (on a 32-bit computer) or HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework folder (on a 64-bit computer).</span></span>

2. <span data-ttu-id="d0278-115">新增名為 `CLRLoadLogDir` 的字串值，將它設為現有目錄的完整路徑，這是您要儲存 CLR 啟動記錄的目錄。</span><span class="sxs-lookup"><span data-stu-id="d0278-115">Add a string value named `CLRLoadLogDir`, and set it to the full path of an existing directory where you'd like to store CLR activation logs.</span></span>

<span data-ttu-id="d0278-116">啟動記錄會一直保持啟用，直到您移除字串值為止。</span><span class="sxs-lookup"><span data-stu-id="d0278-116">Activation logging remains enabled until you remove the string value.</span></span>

### <a name="using-an-environment-variable"></a><span data-ttu-id="d0278-117">使用環境變數</span><span class="sxs-lookup"><span data-stu-id="d0278-117">Using an environment variable</span></span>

- <span data-ttu-id="d0278-118">將 `COMPLUS_CLRLoadLogDir` 環境變數設為字串，代表現有目錄的完整路徑，這是您要儲存 CLR 啟動記錄的目錄。</span><span class="sxs-lookup"><span data-stu-id="d0278-118">Set the `COMPLUS_CLRLoadLogDir` environment variable to a string that represents the full path of an existing directory where you'd like to store CLR activation logs.</span></span>

    <span data-ttu-id="d0278-119">環境變數的設定方式會決定其範圍︰</span><span class="sxs-lookup"><span data-stu-id="d0278-119">How you set the environment variable determines its scope:</span></span>

  - <span data-ttu-id="d0278-120">如果設定在系統層級，就會為該電腦上的所有 .NET Framework 應用程式啟用啟動記錄，直到移除環境變數為止。</span><span class="sxs-lookup"><span data-stu-id="d0278-120">If you set it at the system level, activation logging is enabled for all .NET Framework applications on that computer until the environment variable is removed.</span></span>

  - <span data-ttu-id="d0278-121">如果設定在使用者層級，就只為目前的使用者帳戶啟用啟動記錄。</span><span class="sxs-lookup"><span data-stu-id="d0278-121">If you set it at the user level, activation logging is enabled only for the current user account.</span></span> <span data-ttu-id="d0278-122">環境變數移除之前，會一直記錄。</span><span class="sxs-lookup"><span data-stu-id="d0278-122">Logging continues until the environment variable is removed.</span></span>

  - <span data-ttu-id="d0278-123">如果載入 CLR 之前，從處理序中設定它，就會啟用啟動記錄直到處理序終止為止。</span><span class="sxs-lookup"><span data-stu-id="d0278-123">If you set it from within the process before loading the CLR, activation logging is enabled until the process terminates.</span></span>

  - <span data-ttu-id="d0278-124">如果執行應用程式之前，在命令提示字元中設定它，就會啟用從該命令提示字元執行的所有應用程式的啟動記錄。</span><span class="sxs-lookup"><span data-stu-id="d0278-124">If you set it at a command prompt before you run an application, activation logging is enabled for any application that is run from that command prompt.</span></span>

    <span data-ttu-id="d0278-125">例如，您要先啟動記錄儲存在處理序層級範圍的 c:\clrloadlogs 目錄中，開啟 [命令提示字元] 視窗並鍵入下列命令，才能執行應用程式︰</span><span class="sxs-lookup"><span data-stu-id="d0278-125">For example, to store activation logs in the c:\clrloadlogs directory with process-level scope, open a Command Prompt window and type the following before you run the application:</span></span>

    ```console
    set COMPLUS_CLRLoadLogDir=c:\clrloadlogs
    ```

## <a name="example"></a><span data-ttu-id="d0278-126">範例</span><span class="sxs-lookup"><span data-stu-id="d0278-126">Example</span></span>

<span data-ttu-id="d0278-127">CLR 啟動記錄檔會提供大量有關 CLR 啟動的資料和裝載 API 的 CLR 用法。</span><span class="sxs-lookup"><span data-stu-id="d0278-127">CLR activation logs provide a large amount of data about CLR activation and the use of the CLR hosting APIs.</span></span> <span data-ttu-id="d0278-128">此資料大部分是由 Microsoft 內部使用，但某些部分也對開發人員很有用，如本文所述。</span><span class="sxs-lookup"><span data-stu-id="d0278-128">Most of this data is used internally by Microsoft, but some of the data can also be useful to developers, as described in this article.</span></span>

<span data-ttu-id="d0278-129">記錄會反映裝載 API 之 CLR 的呼叫順序。</span><span class="sxs-lookup"><span data-stu-id="d0278-129">The log reflects the order in which the CLR hosting APIs were called.</span></span> <span data-ttu-id="d0278-130">它也包含電腦上偵測到有關已安裝執行階段組的有用資料。</span><span class="sxs-lookup"><span data-stu-id="d0278-130">It also includes useful data about the set of installed runtimes detected on the computer.</span></span> <span data-ttu-id="d0278-131">CLR 啟動記錄格式不是其本身的記錄，但可用來協助需要解決 CLR 啟動問題的開發人員。</span><span class="sxs-lookup"><span data-stu-id="d0278-131">The CLR activation log format is not itself documented, but can be used to aid developers who need to resolve CLR activation issues.</span></span>

> [!NOTE]
> <span data-ttu-id="d0278-132">您無法開啟啟動記錄，直到使用 CLR 的處理序終止為止。</span><span class="sxs-lookup"><span data-stu-id="d0278-132">You cannot open an activation log until the process that uses the CLR has terminated.</span></span>

> [!NOTE]
> <span data-ttu-id="d0278-133">CLR 啟動記錄不會當地語系化，一律以英文產生。</span><span class="sxs-lookup"><span data-stu-id="d0278-133">CLR activation logs are not localized; they are always generated in the English language.</span></span>

<span data-ttu-id="d0278-134">在下例的啟動記錄中，最有用的資訊會在記錄後反白顯示及描述。</span><span class="sxs-lookup"><span data-stu-id="d0278-134">In the following example of an activation log, the most useful information is highlighted and described after the log.</span></span>

```output
532,205950.367,CLR Loading log for C:\Tests\myapp.exe
532,205950.367,Log started at 4:26:12 PM on 10/6/2011
532,205950.367,-----------------------------------
532,205950.382,FunctionCall: _CorExeMain
532,205950.382,FunctionCall: ClrCreateInstance, Clsid: {2EBCD49A-1B47-4A61-B13A-4A03701E594B}, Iid: {E2190695-77B2-492E-8E14-C4B3A7FDD593}
532,205950.382,MethodCall: ICLRMetaHostPolicy::GetRequestedRuntime. Version: (null), Metahost Policy Flags: 0x168, Binary: (null), Iid: {BD39D1D2-BA2F-486A-89B0-B4B0CB466891}
532,205950.382,Installed Runtime: v4.0.30319. VERSION_ARCHITECTURE: 0
532,205950.382,Input values for ComputeVersionString follow this line
532,205950.382,-----------------------------------
532,205950.382,Default Application Name: C:\Tests\myapp.exe
532,205950.382,IsLegacyBind is: 0
532,205950.382,IsCapped is 0
532,205950.382,SkuCheckFlags are 0
532,205950.382,ShouldEmulateExeLaunch is 0
532,205950.382,LegacyBindRequired is 0
532,205950.382,-----------------------------------
532,205950.382,Parsing config file: C:\Tests\myapp.exe
532,205950.382,UseLegacyV2RuntimeActivationPolicy is set to 0
532,205950.382,LegacyFunctionCall: GetFileVersion. Filename: C:\Tests\myapp.exe
532,205950.382,LegacyFunctionCall: GetFileVersion. Filename: C:\Tests\myapp.exe
532,205950.382,C:\Tests\myapp.exe was built with version: v2.0.50727
532,205950.382,ERROR: Version v2.0.50727 is not present on the machine.
532,205950.398,SEM_FAILCRITICALERRORS is set to 0
532,205950.398,Launching feature-on-demand installation. CmdLine: C:\Windows\system32\fondue.exe /enable-feature:NetFx3
532,205950.398,FunctionCall: RealDllMain. Reason: 0
532,205950.398,FunctionCall: OnShimDllMainCalled. Reason: 0
```

- <span data-ttu-id="d0278-135">**CLR 載入記錄**提供可執行檔路徑，啟動載入 Managed 程式碼的處理序。</span><span class="sxs-lookup"><span data-stu-id="d0278-135">**CLR Loading log** provides the path to the executable that started the process that loaded managed code.</span></span> <span data-ttu-id="d0278-136">請注意，這可能是原生的主機。</span><span class="sxs-lookup"><span data-stu-id="d0278-136">Note that this could be a native host.</span></span>

    ```output
    532,205950.367,CLR Loading log for C:\Tests\myapp.exe
    ```

- <span data-ttu-id="d0278-137">**已安裝的執行階段**是安裝在電腦上用來啟動要求的一組備選 CLR 版本。</span><span class="sxs-lookup"><span data-stu-id="d0278-137">**Installed Runtime** is the set of CLR versions installed on the computer that are candidates for the activation request.</span></span>

    ```output
    532,205950.382,Installed Runtime: v4.0.30319. VERSION_ARCHITECTURE: 0
    ```

- <span data-ttu-id="d0278-138">**以版本建置**是建置二進位檔所用的 CLR 版本，二進位檔會提供給類似 [ICLRMetaHostPolicy::GetRequestedRuntime](../unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md) 的方法。</span><span class="sxs-lookup"><span data-stu-id="d0278-138">**built with version** is the version of the CLR that was used to build the binary that was provided to a method such as [ICLRMetaHostPolicy::GetRequestedRuntime](../unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md).</span></span>

    ```output
    532,205950.382,C:\Tests\myapp.exe was built with version: v2.0.50727
    ```

- <span data-ttu-id="d0278-139">**功能隨選安裝**指的是在 Windows 8 上啟用 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="d0278-139">**feature-on-demand installation** refers to enabling the .NET Framework 3.5 on Windows 8.</span></span> <span data-ttu-id="d0278-140">如需此案例的詳細資訊，請參閱 [.NET Framework 初始化錯誤：管理使用者經驗](initialization-errors-managing-the-user-experience.md)。</span><span class="sxs-lookup"><span data-stu-id="d0278-140">See [.NET Framework Initialization Errors: Managing the User Experience](initialization-errors-managing-the-user-experience.md) for more information about this scenario.</span></span>

    ```output
    532,205950.398,Launching feature-on-demand installation. CmdLine: C:\Windows\system32\fondue.exe /enable-feature:NetFx3
    ```

## <a name="see-also"></a><span data-ttu-id="d0278-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d0278-141">See also</span></span>

- [<span data-ttu-id="d0278-142">部署</span><span class="sxs-lookup"><span data-stu-id="d0278-142">Deployment</span></span>](index.md)
- [<span data-ttu-id="d0278-143">如何：將應用程式設定為支援 .NET Framework 4 或更新版本</span><span class="sxs-lookup"><span data-stu-id="d0278-143">How to: Configure an app to support .NET Framework 4 or later versions</span></span>](../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
