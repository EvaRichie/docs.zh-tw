---
title: 設定程式碼剖析環境
ms.date: 03/30/2017
helpviewer_keywords:
- environment variables, profiling API
- profiling API [.NET Framework], setting up environment
- COR_PROFILER environment variable
- Windows Service applications, profiling
- profiling API [.NET Framework], Windows Service applications
- COR_ENABLE_PROFILING environment variable
- profiling API [.NET Framework], enabling
ms.assetid: fefca07f-7555-4e77-be86-3c542e928312
ms.openlocfilehash: 9c712c5efe8d6d79454b70d0bf4f3ca2fa83b637
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722475"
---
# <a name="setting-up-a-profiling-environment"></a><span data-ttu-id="f7b89-102">設定程式碼剖析環境</span><span class="sxs-lookup"><span data-stu-id="f7b89-102">Setting Up a Profiling Environment</span></span>

> [!NOTE]
> <span data-ttu-id="f7b89-103">在 .NET Framework 4 中，分析已有大量的變更。</span><span class="sxs-lookup"><span data-stu-id="f7b89-103">There have been substantial changes to profiling in the .NET Framework 4.</span></span>  
  
 <span data-ttu-id="f7b89-104">當 Managed 處理序 (應用程式或服務) 啟動時，會載入 Common Language Runtime (CLR)。</span><span class="sxs-lookup"><span data-stu-id="f7b89-104">When a managed process (application or service) starts, it loads the common language runtime (CLR).</span></span> <span data-ttu-id="f7b89-105">初始化 CLR 時，會評估下列兩個環境變數來決定程序是否應該連接至程式碼剖析工具：</span><span class="sxs-lookup"><span data-stu-id="f7b89-105">When the CLR is initialized, it evaluates the following two environmental variables to decide whether the process should connect to a profiler:</span></span>  
  
- <span data-ttu-id="f7b89-106">COR_ENABLE_PROFILING：只有在此環境變數存在，而且設為 1 時，CLR 才會連接到程式碼剖析工具。</span><span class="sxs-lookup"><span data-stu-id="f7b89-106">COR_ENABLE_PROFILING: The CLR connects to a profiler only if this environment variable exists and is set to 1.</span></span>  
  
- <span data-ttu-id="f7b89-107">COR_PROFILER：若 COR_ENABLE_PROFILING 檢查都通過，則 CLR 會連接到具有此 CLSID 或 ProgID 的程式碼剖析工具，該工具必須先前已儲存在登錄中。</span><span class="sxs-lookup"><span data-stu-id="f7b89-107">COR_PROFILER: If the COR_ENABLE_PROFILING check passes, the CLR connects to the profiler that has this CLSID or ProgID, which must have been stored previously in the registry.</span></span> <span data-ttu-id="f7b89-108">將 COR_PROFILER 環境變數定義為字串，如下列兩個範例所示。</span><span class="sxs-lookup"><span data-stu-id="f7b89-108">The COR_PROFILER environment variable is defined as a string, as shown in the following two examples.</span></span>  
  
    ```cpp  
    set COR_PROFILER={32E2F4DA-1BEA-47ea-88F9-C5DAF691C94A}  
    set COR_PROFILER="MyProfiler"  
    ```  
  
 <span data-ttu-id="f7b89-109">若要分析 CLR 應用程式，您必須先設定 COR_ENABLE_PROFILING 和 COR_PROFILER 環境變數，才能執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b89-109">To profile a CLR application, you must set the COR_ENABLE_PROFILING and COR_PROFILER environment variables before you run the application.</span></span> <span data-ttu-id="f7b89-110">您也必須確認已註冊程式碼剖析工具 DLL。</span><span class="sxs-lookup"><span data-stu-id="f7b89-110">You must also make sure that the profiler DLL is registered.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f7b89-111">從 .NET Framework 4 開始，不需要註冊分析工具。</span><span class="sxs-lookup"><span data-stu-id="f7b89-111">Starting with the .NET Framework 4, profilers do not have to be registered.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f7b89-112">若要在 .NET Framework 4 和更新版本中使用 .NET Framework 版本2.0、3.0 和3.5 分析工具，您必須設定 COMPLUS_ProfAPI_ProfilerCompatibilitySetting 的環境變數。</span><span class="sxs-lookup"><span data-stu-id="f7b89-112">To use .NET Framework versions 2.0, 3.0, and 3.5 profilers in the .NET Framework 4 and later versions, you must set the COMPLUS_ProfAPI_ProfilerCompatibilitySetting environment variable.</span></span>  
  
## <a name="environment-variable-scope"></a><span data-ttu-id="f7b89-113">環境變數範圍</span><span class="sxs-lookup"><span data-stu-id="f7b89-113">Environment Variable Scope</span></span>  

 <span data-ttu-id="f7b89-114">您設定 COR_ENABLE_PROFILING 和 COR_PROFILER 環境變數的方式將會決定其影響範圍。</span><span class="sxs-lookup"><span data-stu-id="f7b89-114">How you set the COR_ENABLE_PROFILING and COR_PROFILER environment variables will determine their scope of influence.</span></span> <span data-ttu-id="f7b89-115">您可以使用下列其中一種方式來設定這些變數：</span><span class="sxs-lookup"><span data-stu-id="f7b89-115">You can set these variables in one of the following ways:</span></span>  
  
- <span data-ttu-id="f7b89-116">如果您在 [ICorDebug：： CreateProcess](../debugging/icordebug-createprocess-method.md) 呼叫中設定變數，它們只會套用到您當時執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b89-116">If you set the variables in an [ICorDebug::CreateProcess](../debugging/icordebug-createprocess-method.md) call, they will apply only to the application that you are running at the time.</span></span> <span data-ttu-id="f7b89-117">(它們也會套用到繼承此環境之應用程式所啟動的其他應用程式。)</span><span class="sxs-lookup"><span data-stu-id="f7b89-117">(They will also apply to other applications started by that application that inherit the environment.)</span></span>  
  
- <span data-ttu-id="f7b89-118">如果您在 [命令提示字元] 視窗中設定變數，則變數會套用到從該視窗啟動的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b89-118">If you set the variables in a Command Prompt window, they will apply to all applications that are started from that window.</span></span>  
  
- <span data-ttu-id="f7b89-119">如果您在使用者層次上設定變數，它們會套用至您使用 [檔案總管] 啟動的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b89-119">If you set the variables at the user level, they will apply to all applications that you start with File Explorer.</span></span> <span data-ttu-id="f7b89-120">您在設定變數之後所開啟的 [命令提示字元] 視窗中會有這些環境設定，您從該視窗所啟動的任何應用程式也是。</span><span class="sxs-lookup"><span data-stu-id="f7b89-120">A Command Prompt window that you open after you set the variables will have these environment settings, and so will any application that you start from that window.</span></span> <span data-ttu-id="f7b89-121">若要在使用者層級設定環境變數，請以滑鼠右鍵按一下 [ **我的電腦**，按一下 [ **屬性**]，按一下 [ **Advanced** ] 索引標籤，按一下 [ **環境變數**]，然後將變數新增至 [ **使用者變數** ] 清單。</span><span class="sxs-lookup"><span data-stu-id="f7b89-121">To set environment variables at the user level, right-click **My Computer**, click **Properties**, click the **Advanced** tab, click **Environment Variables**, and add the variables to the **User variables** list.</span></span>  
  
- <span data-ttu-id="f7b89-122">如果您在電腦層級設定變數，變數會套用到該電腦啟動的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b89-122">If you set the variables at the computer level, they will apply to all applications that are started on that computer.</span></span> <span data-ttu-id="f7b89-123">您在該電腦開啟的 [命令提示字元] 視窗會有這些環境設定，從該視窗啟動的任何應用程式也是。</span><span class="sxs-lookup"><span data-stu-id="f7b89-123">A Command Prompt window that you open on that computer will have these environment settings, and so will any application that you start from that window.</span></span> <span data-ttu-id="f7b89-124">這表示在該電腦上的每個 Managed 處理序將以您的程式碼剖析工具做為起始。</span><span class="sxs-lookup"><span data-stu-id="f7b89-124">This means that every managed process on that computer will start with your profiler.</span></span> <span data-ttu-id="f7b89-125">若要在電腦層級設定環境變數，請在 [ **我的電腦**] **上按一下滑鼠** 右鍵，按一下 [內容]，按一下 [ **Advanced** ] 索引標籤，按一下 [ **環境變數**]，將變數新增至 **系統變數** 清單，然後重新開機電腦。</span><span class="sxs-lookup"><span data-stu-id="f7b89-125">To set environment variables at the computer level, right-click **My Computer**, click **Properties**, click the **Advanced** tab, click **Environment Variables**, add the variables to the **System variables** list, and then restart your computer.</span></span> <span data-ttu-id="f7b89-126">重新啟動後，變數就可供系統範圍使用。</span><span class="sxs-lookup"><span data-stu-id="f7b89-126">After restarting, the variables will be available system-wide.</span></span>  
  
 <span data-ttu-id="f7b89-127">如果您正在程式碼剖析 Windows 服務，您必須在設定環境變數及註冊程式碼剖析工具 DLL 之後重新啟動電腦。</span><span class="sxs-lookup"><span data-stu-id="f7b89-127">If you are profiling a Windows Service, you must restart your computer after you set the environment variables and register the profiler DLL.</span></span> <span data-ttu-id="f7b89-128">如需有關這些考慮的詳細資訊，請參閱程式碼 [剖析 Windows 服務](#windows_service)一節。</span><span class="sxs-lookup"><span data-stu-id="f7b89-128">For more information about these considerations, see the section [Profiling a Windows Service](#windows_service).</span></span>  
  
## <a name="additional-considerations"></a><span data-ttu-id="f7b89-129">其他考量</span><span class="sxs-lookup"><span data-stu-id="f7b89-129">Additional Considerations</span></span>  
  
- <span data-ttu-id="f7b89-130">Profiler 類別會執行 [ICorProfilerCallback](icorprofilercallback-interface.md) 和 [ICorProfilerCallback2](icorprofilercallback2-interface.md) 介面。</span><span class="sxs-lookup"><span data-stu-id="f7b89-130">The profiler class implements the [ICorProfilerCallback](icorprofilercallback-interface.md) and [ICorProfilerCallback2](icorprofilercallback2-interface.md) interfaces.</span></span> <span data-ttu-id="f7b89-131">在 .NET Framework 2.0 版中，程式碼剖析工具必須實作 `ICorProfilerCallback2`。</span><span class="sxs-lookup"><span data-stu-id="f7b89-131">In the .NET Framework version 2.0, a profiler must implement `ICorProfilerCallback2`.</span></span> <span data-ttu-id="f7b89-132">如果沒有實作，就不會載入 `ICorProfilerCallback2`。</span><span class="sxs-lookup"><span data-stu-id="f7b89-132">If it does not, `ICorProfilerCallback2` will not be loaded.</span></span>  
  
- <span data-ttu-id="f7b89-133">在指定環境中一次只能使用一個程式碼剖析工具來分析處理序。</span><span class="sxs-lookup"><span data-stu-id="f7b89-133">Only one profiler can profile a process at one time in a given environment.</span></span> <span data-ttu-id="f7b89-134">您可以在不同環境中註冊兩個不同的程式碼剖析工具，但這兩個工具必須分析不同的處理序。</span><span class="sxs-lookup"><span data-stu-id="f7b89-134">You can register two different profilers in different environments, but each must profile separate processes.</span></span> <span data-ttu-id="f7b89-135">程式碼剖析工具必須實作為同處理序 COM 伺服器 DLL (其與剖析中之處理序的相同位址空間對應)。</span><span class="sxs-lookup"><span data-stu-id="f7b89-135">The profiler must be implemented as an in-process COM server DLL, which is mapped into the same address space as the process that is being profiled.</span></span> <span data-ttu-id="f7b89-136">這表示程式碼剖析工具執行同處理序。</span><span class="sxs-lookup"><span data-stu-id="f7b89-136">This means that the profiler runs in-process.</span></span> <span data-ttu-id="f7b89-137">.NET Framework 不支援任何其他類型的 COM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f7b89-137">The .NET Framework does not support any other type of COM server.</span></span> <span data-ttu-id="f7b89-138">例如，如果程式碼剖析工具想要從遠端電腦監視應用程式，就必須在每一部電腦上實作收集器代理程式。</span><span class="sxs-lookup"><span data-stu-id="f7b89-138">For example, if a profiler wants to monitor applications from a remote computer, it must implement collector agents on each computer.</span></span> <span data-ttu-id="f7b89-139">這些代理程式將會批次結果，並讓結果與中央資料收集電腦通訊。</span><span class="sxs-lookup"><span data-stu-id="f7b89-139">These agents will batch results and communicate them to the central data collection computer.</span></span>  
  
- <span data-ttu-id="f7b89-140">由於程式碼剖析工具是可具現化同處理序的 COM 物件，所以每個經剖析的應用程式會有自己的程式碼剖析工具複本。</span><span class="sxs-lookup"><span data-stu-id="f7b89-140">Because the profiler is a COM object that is instantiated in-process, each profiled application will have its own copy of the profiler.</span></span> <span data-ttu-id="f7b89-141">因此，單一程式碼剖析工具執行個體不須處理來自多個應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="f7b89-141">Therefore, a single profiler instance does not have to handle data from multiple applications.</span></span> <span data-ttu-id="f7b89-142">不過，您必須將邏輯加入程式碼剖析工具的記錄程式碼，以防止記錄檔從其他經剖析的應用程式覆寫。</span><span class="sxs-lookup"><span data-stu-id="f7b89-142">However, you will have to add logic to the profiler's logging code to prevent log file overwrites from other profiled applications.</span></span>  
  
## <a name="initializing-the-profiler"></a><span data-ttu-id="f7b89-143">初始化程式碼剖析工具</span><span class="sxs-lookup"><span data-stu-id="f7b89-143">Initializing the Profiler</span></span>  

 <span data-ttu-id="f7b89-144">當這兩個環境變數都檢查通過時，CLR 會以與 COM `CoCreateInstance` 函式類似的方式建立程式碼剖析工具的執行個體。</span><span class="sxs-lookup"><span data-stu-id="f7b89-144">When both environment variable checks pass, the CLR creates an instance of the profiler in a similar manner to the COM `CoCreateInstance` function.</span></span> <span data-ttu-id="f7b89-145">程式碼剖析工具不會透過直接呼叫載入至 `CoCreateInstance`。</span><span class="sxs-lookup"><span data-stu-id="f7b89-145">The profiler is not loaded through a direct call to `CoCreateInstance`.</span></span> <span data-ttu-id="f7b89-146">因此會避免呼叫必須設定執行緒模型的 `CoInitialize`。</span><span class="sxs-lookup"><span data-stu-id="f7b89-146">Therefore, a call to `CoInitialize`, which requires setting the threading model, is avoided.</span></span> <span data-ttu-id="f7b89-147">然後，CLR 會在分析工具中呼叫 [ICorProfilerCallback：： Initialize](icorprofilercallback-initialize-method.md) 方法。</span><span class="sxs-lookup"><span data-stu-id="f7b89-147">The CLR then calls the [ICorProfilerCallback::Initialize](icorprofilercallback-initialize-method.md) method in the profiler.</span></span> <span data-ttu-id="f7b89-148">這個方法的簽章如下所示。</span><span class="sxs-lookup"><span data-stu-id="f7b89-148">The signature of this method is as follows.</span></span>  
  
```cpp  
HRESULT Initialize(IUnknown *pICorProfilerInfoUnk)  
```  
  
 <span data-ttu-id="f7b89-149">分析工具必須查詢 `pICorProfilerInfoUnk` [ICorProfilerInfo](icorprofilerinfo-interface.md) 或 [ICorProfilerInfo2](icorprofilerinfo2-interface.md) 介面指標，並加以儲存，以便稍後在分析期間要求更多資訊。</span><span class="sxs-lookup"><span data-stu-id="f7b89-149">The profiler must query `pICorProfilerInfoUnk` for an [ICorProfilerInfo](icorprofilerinfo-interface.md) or [ICorProfilerInfo2](icorprofilerinfo2-interface.md) interface pointer and save it so that it can request more information later during profiling.</span></span>  
  
## <a name="setting-event-notifications"></a><span data-ttu-id="f7b89-150">設定事件通知</span><span class="sxs-lookup"><span data-stu-id="f7b89-150">Setting Event Notifications</span></span>  

 <span data-ttu-id="f7b89-151">分析工具接著會呼叫 [ICorProfilerInfo：： SetEventMask](icorprofilerinfo-seteventmask-method.md) 方法，以指定其感興趣的通知類別。</span><span class="sxs-lookup"><span data-stu-id="f7b89-151">The profiler then calls the [ICorProfilerInfo::SetEventMask](icorprofilerinfo-seteventmask-method.md) method to specify which categories of notifications it is interested in.</span></span> <span data-ttu-id="f7b89-152">例如，如果程式碼剖析工具只對函式進入及離開通知和記憶體回收通知感興趣，會指定下列項目。</span><span class="sxs-lookup"><span data-stu-id="f7b89-152">For example, if the profiler is interested only in function enter and leave notifications and garbage collection notifications, it specifies the following.</span></span>  
  
```cpp  
ICorProfilerInfo* pInfo;  
pICorProfilerInfoUnk->QueryInterface(IID_ICorProfilerInfo, (void**)&pInfo);  
pInfo->SetEventMask(COR_PRF_MONITOR_ENTERLEAVE | COR_PRF_MONITOR_GC)  
```  
  
 <span data-ttu-id="f7b89-153">藉由以這種方式設定通知遮罩，程式碼剖析工具可以限制所接收的通知。</span><span class="sxs-lookup"><span data-stu-id="f7b89-153">By setting the notifications mask in this manner, the profiler can limit which notifications it receives.</span></span> <span data-ttu-id="f7b89-154">這種方法可協助使用者建置簡單或特殊用途的程式碼剖析工具。</span><span class="sxs-lookup"><span data-stu-id="f7b89-154">This approach helps the user build a simple or special-purpose profiler.</span></span> <span data-ttu-id="f7b89-155">它也會減少浪費在程式碼剖析工具會略過之傳送通知的 CPU 時間。</span><span class="sxs-lookup"><span data-stu-id="f7b89-155">It also reduces CPU time that would be wasted sending notifications that the profiler would just ignore.</span></span>  
  
 <span data-ttu-id="f7b89-156">某些程式碼剖析工具事件為不可變。</span><span class="sxs-lookup"><span data-stu-id="f7b89-156">Certain profiler events are immutable.</span></span> <span data-ttu-id="f7b89-157">這表示，只要這些事件是在 `ICorProfilerCallback::Initialize` 回呼中設定，就無法關閉這些事件，也無法開啟新的事件。</span><span class="sxs-lookup"><span data-stu-id="f7b89-157">This means that as soon as these events are set in the `ICorProfilerCallback::Initialize` callback, they cannot be turned off and new events cannot be turned on.</span></span> <span data-ttu-id="f7b89-158">嘗試變更不可變的事件將會導致 `ICorProfilerInfo::SetEventMask` 傳回失敗的 HRESULT。</span><span class="sxs-lookup"><span data-stu-id="f7b89-158">Attempts to change an immutable event will result in `ICorProfilerInfo::SetEventMask` returning a failed HRESULT.</span></span>  
  
<a name="windows_service"></a>

## <a name="profiling-a-windows-service"></a><span data-ttu-id="f7b89-159">程式碼剖析 Windows 服務</span><span class="sxs-lookup"><span data-stu-id="f7b89-159">Profiling a Windows Service</span></span>  

 <span data-ttu-id="f7b89-160">程式碼剖析 Windows 服務就像是在程式碼剖析通用語言執行階段應用程式。</span><span class="sxs-lookup"><span data-stu-id="f7b89-160">Profiling a Windows Service is like profiling a common language runtime application.</span></span> <span data-ttu-id="f7b89-161">這兩種程式碼剖析作業皆會透過環境變數啟用。</span><span class="sxs-lookup"><span data-stu-id="f7b89-161">Both profiling operations are enabled through environment variables.</span></span> <span data-ttu-id="f7b89-162">因為作業系統啟動時會啟動 Windows 服務，所以本主題先前所討論的環境變數在系統啟動前必須存在並設為所需的值。</span><span class="sxs-lookup"><span data-stu-id="f7b89-162">Because a Windows Service is started when the operating system starts, the environment variables discussed previously in this topic must already be present and set to the required values before the system starts.</span></span> <span data-ttu-id="f7b89-163">此外，程式碼剖析的 DLL 必須已登錄在系統上。</span><span class="sxs-lookup"><span data-stu-id="f7b89-163">In addition, the profiling DLL must already be registered on the system.</span></span>  
  
 <span data-ttu-id="f7b89-164">設定完 COR_ENABLE_PROFILING 和 COR_PROFILER 環境變數，並註冊分析工具 DLL 之後，應該重新啟動目標電腦，使 Windows 服務偵測到這些變更。</span><span class="sxs-lookup"><span data-stu-id="f7b89-164">After you set the COR_ENABLE_PROFILING and COR_PROFILER environment variables and register the profiler DLL, you should restart the target computer so that the Windows Service can detect those changes.</span></span>  
  
 <span data-ttu-id="f7b89-165">請注意這些變更將會啟用以系統範圍為基礎的程式碼剖析。</span><span class="sxs-lookup"><span data-stu-id="f7b89-165">Note that these changes will enable profiling on a system-wide basis.</span></span> <span data-ttu-id="f7b89-166">若要防止進行後續執行之所有 Managed 應用程式的程式碼剖析，您應該在重新啟動目標電腦之後刪除系統環境變數。</span><span class="sxs-lookup"><span data-stu-id="f7b89-166">To prevent every managed application that subsequently runs from being profiled, you should delete the system environment variables after you restart the target computer.</span></span>  
  
 <span data-ttu-id="f7b89-167">這項技術也會使每個 CLR 程序進行程式碼剖析。</span><span class="sxs-lookup"><span data-stu-id="f7b89-167">This technique also leads to every CLR process getting profiled.</span></span> <span data-ttu-id="f7b89-168">分析工具應該將邏輯新增至其 [ICorProfilerCallback：： Initialize](icorprofilercallback-initialize-method.md) 回呼，以偵測目前的進程是否感興趣。</span><span class="sxs-lookup"><span data-stu-id="f7b89-168">The profiler should add logic to its [ICorProfilerCallback::Initialize](icorprofilercallback-initialize-method.md) callback to detect whether the current process is of interest.</span></span> <span data-ttu-id="f7b89-169">如果不是，程式碼剖析工具可以使回呼失敗，而不需執行初始化。</span><span class="sxs-lookup"><span data-stu-id="f7b89-169">If it is not, the profiler can fail the callback without performing the initialization.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f7b89-170">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f7b89-170">See also</span></span>

- [<span data-ttu-id="f7b89-171">分析概觀</span><span class="sxs-lookup"><span data-stu-id="f7b89-171">Profiling Overview</span></span>](profiling-overview.md)
