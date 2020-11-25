---
title: 偵錯列舉
ms.date: 03/30/2017
helpviewer_keywords:
- debugging enumerations [.NET Framework]
- unmanaged enumerations [.NET Framework], debugging
- enumerations [.NET Framework debugging]
ms.assetid: 3af9f584-f1b4-4154-aeaa-8fce7c9f8b50
ms.openlocfilehash: bdd4b60d068677ae2a0874b589294ba220f0d854
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722995"
---
# <a name="debugging-enumerations"></a><span data-ttu-id="9819b-102">偵錯列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-102">Debugging Enumerations</span></span>

<span data-ttu-id="9819b-103">本節說明偵錯 API 所使用的 Unmanaged 列舉。</span><span class="sxs-lookup"><span data-stu-id="9819b-103">This section describes the unmanaged enumerations that the debugging API uses.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="9819b-104">本節內容</span><span class="sxs-lookup"><span data-stu-id="9819b-104">In This Section</span></span>  

 [<span data-ttu-id="9819b-105">CLR_DEBUGGING_PROCESS_FLAGS 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-105">CLR_DEBUGGING_PROCESS_FLAGS Enumeration</span></span>](clr-debugging-process-flags-enumeration.md)  
 <span data-ttu-id="9819b-106">提供 [ICLRDebugging：： OpenVirtualProcess](iclrdebugging-openvirtualprocess-method.md) 方法所使用的值。</span><span class="sxs-lookup"><span data-stu-id="9819b-106">Provides values that are used by the [ICLRDebugging::OpenVirtualProcess](iclrdebugging-openvirtualprocess-method.md) method.</span></span>  
  
 [<span data-ttu-id="9819b-107">CLRDataEnumMemoryFlags 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-107">CLRDataEnumMemoryFlags Enumeration</span></span>](clrdataenummemoryflags-enumeration.md)  
 <span data-ttu-id="9819b-108">指出呼叫 [ICLRDataEnumMemoryRegions：： EnumMemoryRegions](iclrdataenummemoryregions-enummemoryregions-method.md) 方法應該包含的記憶體區域。</span><span class="sxs-lookup"><span data-stu-id="9819b-108">Indicates which memory regions a call to the [ICLRDataEnumMemoryRegions::EnumMemoryRegions](iclrdataenummemoryregions-enummemoryregions-method.md) method should include.</span></span>  
  
 [<span data-ttu-id="9819b-109">COR_PUB_ENUMPROCESS 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-109">COR_PUB_ENUMPROCESS Enumeration</span></span>](cor-pub-enumprocess-enumeration.md)  
 <span data-ttu-id="9819b-110">識別所要列舉的類型。</span><span class="sxs-lookup"><span data-stu-id="9819b-110">Identifies the type of process to be enumerated.</span></span>  
  
 [<span data-ttu-id="9819b-111">CorDebugBlockingReason 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-111">CorDebugBlockingReason Enumeration</span></span>](cordebugblockingreason-enumeration.md)  
 <span data-ttu-id="9819b-112">指定給定物件上封鎖執行緒的原因。</span><span class="sxs-lookup"><span data-stu-id="9819b-112">Specifies the reasons why a thread may become blocked on a given object.</span></span>  
  
 <span data-ttu-id="9819b-113">CorDebugChainReason</span><span class="sxs-lookup"><span data-stu-id="9819b-113">CorDebugChainReason</span></span>  
 <span data-ttu-id="9819b-114">指出呼叫鏈結初始化的原因。</span><span class="sxs-lookup"><span data-stu-id="9819b-114">Indicates the reason or reasons for the initiation of a call chain.</span></span>  
  
 [<span data-ttu-id="9819b-115">CorDebugCodeInvokeKind 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-115">CorDebugCodeInvokeKind Enumeration</span></span>](cordebugcodeinvokekind-enumeration.md)  
 <span data-ttu-id="9819b-116">描述匯出函式如何叫用 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="9819b-116">Describes how an exported function invokes managed code.</span></span>  
  
 [<span data-ttu-id="9819b-117">CorDebugCodeInvokePurpose 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-117">CorDebugCodeInvokePurpose Enumeration</span></span>](cordebugcodeinvokepurpose-enumeration.md)  
 <span data-ttu-id="9819b-118">描述匯出函式呼叫 Managed 程式碼的原因。</span><span class="sxs-lookup"><span data-stu-id="9819b-118">Describes why an exported function calls managed code.</span></span>  
  
 <span data-ttu-id="9819b-119">CorDebugCreateProcessFlags</span><span class="sxs-lookup"><span data-stu-id="9819b-119">CorDebugCreateProcessFlags</span></span>  
 <span data-ttu-id="9819b-120">提供可用於呼叫 [ICorDebug：： CreateProcess](icordebug-createprocess-method.md) 方法的其他偵錯工具選項。</span><span class="sxs-lookup"><span data-stu-id="9819b-120">Provides additional debugging options that can be used in a call to the [ICorDebug::CreateProcess](icordebug-createprocess-method.md) method.</span></span>  
  
 [<span data-ttu-id="9819b-121">CorDebugDebugEventKind 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-121">CorDebugDebugEventKind Enumeration</span></span>](cordebugdebugeventkind-enumeration.md)  
 <span data-ttu-id="9819b-122">表示 [DecodeEvent](icordebugprocess6-decodeevent-method.md) 方法解碼其資訊的事件種類。</span><span class="sxs-lookup"><span data-stu-id="9819b-122">Indicates the type of event whose information is decoded by the [DecodeEvent](icordebugprocess6-decodeevent-method.md) method.</span></span>  
  
 [<span data-ttu-id="9819b-123">CorDebugDecodeEventFlagsWindows 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-123">CorDebugDecodeEventFlagsWindows Enumeration</span></span>](cordebugdecodeeventflagswindows-enumeration.md)  
 <span data-ttu-id="9819b-124">提供 Windows 平台上之偵錯事件的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="9819b-124">Provides additional information about debug events on the Windows platform.</span></span>  
  
 <span data-ttu-id="9819b-125">CorDebugExceptionCallbackType</span><span class="sxs-lookup"><span data-stu-id="9819b-125">CorDebugExceptionCallbackType</span></span>  
 <span data-ttu-id="9819b-126">指出從 [ICorDebugManagedCallback2：： Exception](icordebugmanagedcallback2-exception-method.md) 事件進行的回呼類型。</span><span class="sxs-lookup"><span data-stu-id="9819b-126">Indicates the type of callback that is made from an [ICorDebugManagedCallback2::Exception](icordebugmanagedcallback2-exception-method.md) event.</span></span>  
  
 [<span data-ttu-id="9819b-127">CorDebugExceptionFlags 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-127">CorDebugExceptionFlags Enumeration</span></span>](cordebugexceptionflags-enumeration.md)  
 <span data-ttu-id="9819b-128">提供例外狀況的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="9819b-128">Provides additional information about an exception.</span></span>  
  
 <span data-ttu-id="9819b-129">CorDebugExceptionUnwindCallbackType</span><span class="sxs-lookup"><span data-stu-id="9819b-129">CorDebugExceptionUnwindCallbackType</span></span>  
 <span data-ttu-id="9819b-130">指出回呼在回溯階段期間通知的事件。</span><span class="sxs-lookup"><span data-stu-id="9819b-130">Indicates the event that is being signaled by the callback during the unwind phase.</span></span>  
  
 [<span data-ttu-id="9819b-131">CorDebugGCType 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-131">CorDebugGCType Enumeration</span></span>](cordebuggctype-enumeration.md)  
 <span data-ttu-id="9819b-132">指出記憶體回收行程是在工作站或伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="9819b-132">Indicates whether the garbage collector is running on a workstation or a server.</span></span>  
  
 [<span data-ttu-id="9819b-133">CorDebugGenerationTypes 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-133">CorDebugGenerationTypes Enumeration</span></span>](cordebuggenerationtypes-enumeration.md)  
 <span data-ttu-id="9819b-134">指定 Managed 堆積上的記憶體區域產生方式。</span><span class="sxs-lookup"><span data-stu-id="9819b-134">Specifies the generation of a region of memory on the managed heap.</span></span>  
  
 <span data-ttu-id="9819b-135">CorDebugHandleType</span><span class="sxs-lookup"><span data-stu-id="9819b-135">CorDebugHandleType</span></span>  
 <span data-ttu-id="9819b-136">指出控制代碼類型。</span><span class="sxs-lookup"><span data-stu-id="9819b-136">Indicates the handle type.</span></span>  
  
 [<span data-ttu-id="9819b-137">CorDebugIlToNativeMappingTypes 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-137">CorDebugIlToNativeMappingTypes Enumeration</span></span>](cordebugiltonativemappingtypes-enumeration.md)  
 <span data-ttu-id="9819b-138">指出特定範圍的原生指令是否對應於特殊程式碼區域。</span><span class="sxs-lookup"><span data-stu-id="9819b-138">Indicates whether a particular range of native instructions corresponds to a special code region.</span></span>  
  
 <span data-ttu-id="9819b-139">CorDebugIntercept</span><span class="sxs-lookup"><span data-stu-id="9819b-139">CorDebugIntercept</span></span>  
 <span data-ttu-id="9819b-140">指出可以逐步執行的程式碼類型。</span><span class="sxs-lookup"><span data-stu-id="9819b-140">Indicates the types of code that can be stepped into.</span></span>  
  
 [<span data-ttu-id="9819b-141">CorDebugInterfaceVersion 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-141">CorDebugInterfaceVersion Enumeration</span></span>](cordebuginterfaceversion-enumeration.md)  
 <span data-ttu-id="9819b-142">指定 .NET Framework 版本，或是引進介面之 .NET Framework 的版本。</span><span class="sxs-lookup"><span data-stu-id="9819b-142">Specifies either a version of the .NET Framework, or the version of the .NET Framework in which an interface was introduced.</span></span>  
  
 <span data-ttu-id="9819b-143">CorDebugInternalFrameType</span><span class="sxs-lookup"><span data-stu-id="9819b-143">CorDebugInternalFrameType</span></span>  
 <span data-ttu-id="9819b-144">識別堆疊框架的類型。</span><span class="sxs-lookup"><span data-stu-id="9819b-144">Identifies the type of stack frame.</span></span>  
  
 [<span data-ttu-id="9819b-145">CorDebugJITCompilerFlags 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-145">CorDebugJITCompilerFlags Enumeration</span></span>](cordebugjitcompilerflags-enumeration.md)  
 <span data-ttu-id="9819b-146">包含會影響 Managed Just-In-Time (JIT) 編譯器行為的值。</span><span class="sxs-lookup"><span data-stu-id="9819b-146">Contains values that influence the behavior of the managed just-in-time (JIT) compiler.</span></span>  
  
 [<span data-ttu-id="9819b-147">CorDebugJITCompilerFlagsDeprecated 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-147">CorDebugJITCompilerFlagsDeprecated Enumeration</span></span>](cordebugjitcompilerflagsdeprecated-enumeration.md)  
 <span data-ttu-id="9819b-148">已過時。</span><span class="sxs-lookup"><span data-stu-id="9819b-148">Obsolete.</span></span> <span data-ttu-id="9819b-149">請改用 `CORDEBUG_JIT_DEFAULT` [CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md) 列舉的成員。</span><span class="sxs-lookup"><span data-stu-id="9819b-149">Use the `CORDEBUG_JIT_DEFAULT` member of the [CorDebugJITCompilerFlags](cordebugjitcompilerflags-enumeration.md) enumeration instead.</span></span>  
  
 <span data-ttu-id="9819b-150">CorDebugMappingResult</span><span class="sxs-lookup"><span data-stu-id="9819b-150">CorDebugMappingResult</span></span>  
 <span data-ttu-id="9819b-151">提供如何取得指令指標 (IP) 值的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9819b-151">Provides the details of how the value of the instruction pointer (IP) was obtained.</span></span>  
  
 [<span data-ttu-id="9819b-152">CorDebugMDAFlags 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-152">CorDebugMDAFlags Enumeration</span></span>](cordebugmdaflags-enumeration.md)  
 <span data-ttu-id="9819b-153">指定會引發 Managed 偵錯助理 (MDA) 的執行緒狀態。</span><span class="sxs-lookup"><span data-stu-id="9819b-153">Specifies the status of the thread on which the managed debugging assistant (MDA) is fired.</span></span>  
  
 [<span data-ttu-id="9819b-154">CorDebugNGenPolicy 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-154">CorDebugNGenPolicy Enumeration</span></span>](cordebugngenpolicy-enumeration.md)  
 <span data-ttu-id="9819b-155">提供用來判定偵錯工具是否從原生影像快取載入原生 (NGen) 影像的值。</span><span class="sxs-lookup"><span data-stu-id="9819b-155">Provides a value that determines whether a debugger loads native (NGen) images from the native image cache.</span></span>  
  
 [<span data-ttu-id="9819b-156">CorDebugPlatform 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-156">CorDebugPlatform Enumeration</span></span>](cordebugplatform-enumeration.md)  
 <span data-ttu-id="9819b-157">提供 [ICorDebugDataTarget：： GetPlatform](icordebugdatatarget-getplatform-method.md) 方法所使用的目標平臺值。</span><span class="sxs-lookup"><span data-stu-id="9819b-157">Provides target platform values that are used by the [ICorDebugDataTarget::GetPlatform](icordebugdatatarget-getplatform-method.md) method.</span></span>  
  
 [<span data-ttu-id="9819b-158">CorDebugRecordFormat 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-158">CorDebugRecordFormat Enumeration</span></span>](cordebugrecordformat-enumeration.md)  
 <span data-ttu-id="9819b-159">描述包含原生例外狀況偵錯事件相關資訊之位元組陣列中的資料格式。</span><span class="sxs-lookup"><span data-stu-id="9819b-159">Describes the format of the data in a byte array that contains information about a native exception debug event.</span></span>  
  
 <span data-ttu-id="9819b-160">CorDebugRegister</span><span class="sxs-lookup"><span data-stu-id="9819b-160">CorDebugRegister</span></span>  
 <span data-ttu-id="9819b-161">指定與給定處理器架構相關聯的暫存器。</span><span class="sxs-lookup"><span data-stu-id="9819b-161">Specifies the registers associated with a given processor architecture.</span></span>  
  
 [<span data-ttu-id="9819b-162">CorDebugSetContextFlag 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-162">CorDebugSetContextFlag Enumeration</span></span>](cordebugsetcontextflag-enumeration.md)  
 <span data-ttu-id="9819b-163">指出內容是來自堆疊的作用中 (或分葉) 框架，還是藉由從其他框架回溯而計算出來的。</span><span class="sxs-lookup"><span data-stu-id="9819b-163">Indicates whether the context is from the active (or leaf) frame on the stack or has been computed by unwinding from another frame.</span></span>  
  
 [<span data-ttu-id="9819b-164">CorDebugStateChange 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-164">CorDebugStateChange Enumeration</span></span>](cordebugstatechange-enumeration.md)  
 <span data-ttu-id="9819b-165">描述依據處理序變更而必須捨棄的快取資料量。</span><span class="sxs-lookup"><span data-stu-id="9819b-165">Describes the amount of cached data that must be discarded based on changes to the process.</span></span>  
  
 <span data-ttu-id="9819b-166">CorDebugStepReason</span><span class="sxs-lookup"><span data-stu-id="9819b-166">CorDebugStepReason</span></span>  
 <span data-ttu-id="9819b-167">指出個別步驟的結果。</span><span class="sxs-lookup"><span data-stu-id="9819b-167">Indicates the outcome of an individual step.</span></span>  
  
 <span data-ttu-id="9819b-168">CorDebugThreadState</span><span class="sxs-lookup"><span data-stu-id="9819b-168">CorDebugThreadState</span></span>  
 <span data-ttu-id="9819b-169">指定要偵錯的執行緒狀態。</span><span class="sxs-lookup"><span data-stu-id="9819b-169">Specifies the state of a thread for debugging.</span></span>  
  
 <span data-ttu-id="9819b-170">\>CorDebugUnmappedStop</span><span class="sxs-lookup"><span data-stu-id="9819b-170">\>CorDebugUnmappedStop</span></span>  
 <span data-ttu-id="9819b-171">指定可在步進器執行程式碼時觸發暫止的未對應程式碼類型。</span><span class="sxs-lookup"><span data-stu-id="9819b-171">Specifies the type of unmapped code that can trigger a halt in code execution by the stepper.</span></span>  
  
 <span data-ttu-id="9819b-172">CorDebugUserState</span><span class="sxs-lookup"><span data-stu-id="9819b-172">CorDebugUserState</span></span>  
 <span data-ttu-id="9819b-173">指出執行緒的使用者狀態。</span><span class="sxs-lookup"><span data-stu-id="9819b-173">Indicates the user state of a thread.</span></span>  
  
 [<span data-ttu-id="9819b-174">CorGCReferenceType 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-174">CorGCReferenceType Enumeration</span></span>](corgcreferencetype-enumeration.md)  
 <span data-ttu-id="9819b-175">識別要進行記憶體回收的物件來源。</span><span class="sxs-lookup"><span data-stu-id="9819b-175">Identifies the source of an object to be garbage-collected.</span></span>  
  
 [<span data-ttu-id="9819b-176">ILCodeKind 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-176">ILCodeKind Enumeration</span></span>](ilcodekind-enumeration.md)  
 <span data-ttu-id="9819b-177">提供值，指定偵錯工具是否能夠存取分析工具 ReJIT 檢測中加入的區域變數或程式碼。</span><span class="sxs-lookup"><span data-stu-id="9819b-177">Provides values that specify whether the debugger is able to access local variables or code added in profiler ReJIT instrumentation.</span></span>  
  
 [<span data-ttu-id="9819b-178">LoggingLevelEnum 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-178">LoggingLevelEnum Enumeration</span></span>](logginglevelenum-enumeration.md)  
 <span data-ttu-id="9819b-179">指出當 Managed 執行緒記錄事件時，寫入至事件記錄檔之描述性訊息的嚴重性層級。</span><span class="sxs-lookup"><span data-stu-id="9819b-179">Indicates the severity level of a descriptive message that is written to the event log when a managed thread logs an event.</span></span>  
  
 [<span data-ttu-id="9819b-180">LogSwitchCallReason 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-180">LogSwitchCallReason Enumeration</span></span>](logswitchcallreason-enumeration.md)  
 <span data-ttu-id="9819b-181">指出在切換偵錯/追蹤時所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="9819b-181">Indicates the operation that was performed on a debugging/tracing switch.</span></span>  
  
 [<span data-ttu-id="9819b-182">VariableLocationType 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-182">VariableLocationType Enumeration</span></span>](variablelocationtype-enumeration.md)  
 <span data-ttu-id="9819b-183">指出變數的原生位置型別。</span><span class="sxs-lookup"><span data-stu-id="9819b-183">Indicates the native location type of a variable.</span></span>  
  
 [<span data-ttu-id="9819b-184">WriteableMetadataUpdateMode 列舉</span><span class="sxs-lookup"><span data-stu-id="9819b-184">WriteableMetadataUpdateMode Enumeration</span></span>](writeablemetadataupdatemode-enumeration.md)  
 <span data-ttu-id="9819b-185">提供值來指定偵錯工具是否可以看見對中繼資料的記憶體中更新。</span><span class="sxs-lookup"><span data-stu-id="9819b-185">Provides values that specify whether in-memory updates to metadata are visible to a debugger.</span></span>

 <span data-ttu-id="9819b-186">[ClrDataSourceType 列舉](clrdatasourcetype-enumeration.md) 提供 CLRDATA_IL_ADDRESS_MAP 結構所使用的值。</span><span class="sxs-lookup"><span data-stu-id="9819b-186">[ClrDataSourceType Enumeration](clrdatasourcetype-enumeration.md) Provides values that are used by the CLRDATA_IL_ADDRESS_MAP structure.</span></span>

## <a name="related-sections"></a><span data-ttu-id="9819b-187">相關章節</span><span class="sxs-lookup"><span data-stu-id="9819b-187">Related Sections</span></span>  

 [<span data-ttu-id="9819b-188">偵錯 Coclass</span><span class="sxs-lookup"><span data-stu-id="9819b-188">Debugging Coclasses</span></span>](debugging-coclasses.md)  
  
 [<span data-ttu-id="9819b-189">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="9819b-189">Debugging Interfaces</span></span>](debugging-interfaces.md)  
  
 [<span data-ttu-id="9819b-190">偵錯全域靜態函式</span><span class="sxs-lookup"><span data-stu-id="9819b-190">Debugging Global Static Functions</span></span>](debugging-global-static-functions.md)  
  
 [<span data-ttu-id="9819b-191">偵錯結構</span><span class="sxs-lookup"><span data-stu-id="9819b-191">Debugging Structures</span></span>](debugging-structures.md)
