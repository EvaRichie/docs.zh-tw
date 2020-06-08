---
title: ICLRProfiling::AttachProfiler 方法
ms.date: 03/30/2017
api_name:
- IClrProfiling.AttachProfiler Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- IClrProfiling::AttachProfiler
helpviewer_keywords:
- AttachProfiler method [.NET Framework profiling]
- IClrProfiling::AttachProfiler method [.NET Framework profiling]
ms.assetid: 535a6839-c443-405b-a6f4-e2af90725d5b
topic_type:
- apiref
ms.openlocfilehash: 48ac09e1862ae58e79707235e891f72920de1251
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500555"
---
# <a name="iclrprofilingattachprofiler-method"></a><span data-ttu-id="b01e5-102">ICLRProfiling::AttachProfiler 方法</span><span class="sxs-lookup"><span data-stu-id="b01e5-102">ICLRProfiling::AttachProfiler Method</span></span>
<span data-ttu-id="b01e5-103">將指定的程式碼剖析工具附加至指定的處理序。</span><span class="sxs-lookup"><span data-stu-id="b01e5-103">Attaches the specified profiler to the specified process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b01e5-104">語法</span><span class="sxs-lookup"><span data-stu-id="b01e5-104">Syntax</span></span>  
  
```cpp  
HRESULT AttachProfiler(  
  [in] DWORD dwProfileeProcessID,  
  [in] DWORD dwMillisecondsMax,                     // optional  
  [in] const CLSID * pClsidProfiler,  
  [in] LPCWSTR wszProfilerPath,                     // optional  
  [in] size_is(cbClientData)] void * pvClientData,  // optional  
  [in] UINT cbClientData);                          // optional  
```  
  
## <a name="parameters"></a><span data-ttu-id="b01e5-105">參數</span><span class="sxs-lookup"><span data-stu-id="b01e5-105">Parameters</span></span>

- `dwProfileeProcessID`

  <span data-ttu-id="b01e5-106">\[in] 程式碼剖析工具應附加至進程的處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="b01e5-106">\[in] The process ID of the process to which the profiler should be attached.</span></span> <span data-ttu-id="b01e5-107">在 64 位元電腦上，已剖析程式碼的處理序的位元必須符合正在呼叫 `AttachProfiler` 的觸發處理序的位元。</span><span class="sxs-lookup"><span data-stu-id="b01e5-107">On a 64-bit machine, the profiled process's bitness must match the bitness of the trigger process that is calling `AttachProfiler`.</span></span> <span data-ttu-id="b01e5-108">如果呼叫 `AttachProfiler` 用的使用者帳戶具有系統管理權限，則目標處理序可以是系統上的任何處理序。</span><span class="sxs-lookup"><span data-stu-id="b01e5-108">If the user account under which `AttachProfiler` is called has administrative privileges, the target process may be any process on the system.</span></span> <span data-ttu-id="b01e5-109">否則目標處理序必須由相同的使用者帳戶所擁有。</span><span class="sxs-lookup"><span data-stu-id="b01e5-109">Otherwise, the target process must be owned by the same user account.</span></span>

- `dwMillisecondsMax`

  <span data-ttu-id="b01e5-110">\[in] 完成的持續時間（以毫秒為單位） `AttachProfiler` 。</span><span class="sxs-lookup"><span data-stu-id="b01e5-110">\[in] The time duration, in milliseconds, for `AttachProfiler` to complete.</span></span> <span data-ttu-id="b01e5-111">觸發處理序應該傳遞已知足以讓特定程式碼剖析工具完成初始化的逾時值。</span><span class="sxs-lookup"><span data-stu-id="b01e5-111">The trigger process should pass a timeout that is known to be sufficient for the particular profiler to complete its initialization.</span></span>
  
- `pClsidProfiler`

  <span data-ttu-id="b01e5-112">\[in] 要載入之 profiler 的 CLSID 指標。</span><span class="sxs-lookup"><span data-stu-id="b01e5-112">\[in] A pointer to the CLSID of the profiler to be loaded.</span></span> <span data-ttu-id="b01e5-113">`AttachProfiler` 傳回之後，觸發處理序可以重複使用此記憶體。</span><span class="sxs-lookup"><span data-stu-id="b01e5-113">The trigger process can reuse this memory after `AttachProfiler` returns.</span></span>

- `wszProfilerPath`

  <span data-ttu-id="b01e5-114">\[in] 要載入的分析工具 DLL 檔案的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="b01e5-114">\[in] The full path to the profiler’s DLL file to be loaded.</span></span> <span data-ttu-id="b01e5-115">此字串應該包含不超過 260 個字元，包括 null 結束字元。</span><span class="sxs-lookup"><span data-stu-id="b01e5-115">This string should contain no more than 260 characters, including the null terminator.</span></span> <span data-ttu-id="b01e5-116">如果 `wszProfilerPath` 是 null 或空字串，Common Language Runtime (CLR) 會嘗試在登錄中尋找 `pClsidProfiler` 指向的 CLSID，以尋找程式碼剖析工具 DLL 檔的位置。</span><span class="sxs-lookup"><span data-stu-id="b01e5-116">If `wszProfilerPath` is null or an empty string, the common language runtime (CLR) will try to find the location of the profiler’s DLL file by looking in the registry for the CLSID that `pClsidProfiler` points to.</span></span>

- `pvClientData`

  <span data-ttu-id="b01e5-117">\[in] [ICorProfilerCallback3：： InitializeForAttach](icorprofilercallback3-initializeforattach-method.md)方法傳遞至分析工具的資料指標。</span><span class="sxs-lookup"><span data-stu-id="b01e5-117">\[in] A pointer to data to be passed to the profiler by the [ICorProfilerCallback3::InitializeForAttach](icorprofilercallback3-initializeforattach-method.md) method.</span></span> <span data-ttu-id="b01e5-118">`AttachProfiler` 傳回之後，觸發處理序可以重複使用此記憶體。</span><span class="sxs-lookup"><span data-stu-id="b01e5-118">The trigger process can reuse this memory after `AttachProfiler` returns.</span></span> <span data-ttu-id="b01e5-119">如果 `pvClientData` 為 null，則 `cbClientData` 必須是 0 (零)。</span><span class="sxs-lookup"><span data-stu-id="b01e5-119">If `pvClientData` is null, `cbClientData` must be 0 (zero).</span></span>

- `cbClientData`

  <span data-ttu-id="b01e5-120">\[in] 指向的資料大小（以位元組為單位） `pvClientData` 。</span><span class="sxs-lookup"><span data-stu-id="b01e5-120">\[in] The size, in bytes, of the data that `pvClientData` points to.</span></span>

## <a name="return-value"></a><span data-ttu-id="b01e5-121">傳回值</span><span class="sxs-lookup"><span data-stu-id="b01e5-121">Return Value</span></span>  
 <span data-ttu-id="b01e5-122">這個方法會傳回下列 HRESULT。</span><span class="sxs-lookup"><span data-stu-id="b01e5-122">This method returns the following HRESULTs.</span></span>  
  
|<span data-ttu-id="b01e5-123">HRESULT</span><span class="sxs-lookup"><span data-stu-id="b01e5-123">HRESULT</span></span>|<span data-ttu-id="b01e5-124">說明</span><span class="sxs-lookup"><span data-stu-id="b01e5-124">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="b01e5-125">S_OK</span><span class="sxs-lookup"><span data-stu-id="b01e5-125">S_OK</span></span>|<span data-ttu-id="b01e5-126">指定的程式碼剖析工具已經成功附加至目標處理序。</span><span class="sxs-lookup"><span data-stu-id="b01e5-126">The specified profiler has successfully attached to the target process.</span></span>|  
|<span data-ttu-id="b01e5-127">CORPROF_E_PROFILER_ALREADY_ACTIVE</span><span class="sxs-lookup"><span data-stu-id="b01e5-127">CORPROF_E_PROFILER_ALREADY_ACTIVE</span></span>|<span data-ttu-id="b01e5-128">已經有程式碼剖析工具在作用中或附加至目標處理序。</span><span class="sxs-lookup"><span data-stu-id="b01e5-128">There is already a profiler active or attaching to the target process.</span></span>|  
|<span data-ttu-id="b01e5-129">CORPROF_E_PROFILER_NOT_ATTACHABLE</span><span class="sxs-lookup"><span data-stu-id="b01e5-129">CORPROF_E_PROFILER_NOT_ATTACHABLE</span></span>|<span data-ttu-id="b01e5-130">指定的程式碼剖析工具不支援附加作業。</span><span class="sxs-lookup"><span data-stu-id="b01e5-130">The specified profiler does not support attachment.</span></span> <span data-ttu-id="b01e5-131">觸發處理序可能會嘗試附加不同的程式碼剖析工具。</span><span class="sxs-lookup"><span data-stu-id="b01e5-131">The trigger process may attempt to attach a different profiler.</span></span>|  
|<span data-ttu-id="b01e5-132">CORPROF_E_PROFILEE_INCOMPATIBLE_WITH_TRIGGER</span><span class="sxs-lookup"><span data-stu-id="b01e5-132">CORPROF_E_PROFILEE_INCOMPATIBLE_WITH_TRIGGER</span></span>|<span data-ttu-id="b01e5-133">無法要求執行程式碼剖析工具附加，因為目標處理序的版本與目前正在呼叫 `AttachProfiler` 的處理序不相容。</span><span class="sxs-lookup"><span data-stu-id="b01e5-133">Unable to request a profiler attachment, because the version of the target process is incompatible with the current process that is calling `AttachProfiler`.</span></span>|  
|<span data-ttu-id="b01e5-134">HRESULT_FROM_WIN32(ERROR_ACCESS_DENIED)</span><span class="sxs-lookup"><span data-stu-id="b01e5-134">HRESULT_FROM_WIN32(ERROR_ACCESS_DENIED)</span></span>|<span data-ttu-id="b01e5-135">觸發處理序的使用者無法存取目標處理序。</span><span class="sxs-lookup"><span data-stu-id="b01e5-135">The user of the trigger process does not have access to the target process.</span></span>|  
|<span data-ttu-id="b01e5-136">HRESULT_FROM_WIN32(ERROR_PRIVILEGE_NOT_HELD)</span><span class="sxs-lookup"><span data-stu-id="b01e5-136">HRESULT_FROM_WIN32(ERROR_PRIVILEGE_NOT_HELD)</span></span>|<span data-ttu-id="b01e5-137">觸發處理序的使用者沒有將程式碼剖析工具附加至指定目標處理序的必要權限。</span><span class="sxs-lookup"><span data-stu-id="b01e5-137">The user of the trigger process does not have the privileges necessary to attach a profiler to the given target process.</span></span> <span data-ttu-id="b01e5-138">應用程式事件記錄檔可能包含更多的資訊。</span><span class="sxs-lookup"><span data-stu-id="b01e5-138">The application event log may contain more information.</span></span>|  
|<span data-ttu-id="b01e5-139">CORPROF_E_IPC_FAILED</span><span class="sxs-lookup"><span data-stu-id="b01e5-139">CORPROF_E_IPC_FAILED</span></span>|<span data-ttu-id="b01e5-140">與目標處理序通訊時發生失敗。</span><span class="sxs-lookup"><span data-stu-id="b01e5-140">A failure occurred when communicating with the target process.</span></span> <span data-ttu-id="b01e5-141">這通常發生於目標處理序正在關閉的時候。</span><span class="sxs-lookup"><span data-stu-id="b01e5-141">This commonly happens if the target process was shutting down.</span></span>|  
|<span data-ttu-id="b01e5-142">HRESULT_FROM_WIN32(ERROR_FILE_NOT_FOUND)</span><span class="sxs-lookup"><span data-stu-id="b01e5-142">HRESULT_FROM_WIN32(ERROR_FILE_NOT_FOUND)</span></span>|<span data-ttu-id="b01e5-143">目標處理序不存在或未執行支援附加作業的 CLR。</span><span class="sxs-lookup"><span data-stu-id="b01e5-143">The target process does not exist or is not running a CLR that supports attachment.</span></span> <span data-ttu-id="b01e5-144">這可能表示在呼叫執行階段列舉方法之後，CLR 已卸載。</span><span class="sxs-lookup"><span data-stu-id="b01e5-144">This may indicate that the CLR was unloaded since the call to the runtime enumeration method.</span></span>|  
|<span data-ttu-id="b01e5-145">HRESULT_FROM_WIN32(ERROR_TIMEOUT)</span><span class="sxs-lookup"><span data-stu-id="b01e5-145">HRESULT_FROM_WIN32(ERROR_TIMEOUT)</span></span>|<span data-ttu-id="b01e5-146">逾時已過期但未開始載入程式碼剖析工具。</span><span class="sxs-lookup"><span data-stu-id="b01e5-146">The timeout expired without beginning to load the profiler.</span></span> <span data-ttu-id="b01e5-147">您可以重試附加作業。</span><span class="sxs-lookup"><span data-stu-id="b01e5-147">You can retry the attach operation.</span></span> <span data-ttu-id="b01e5-148">目標處理序中的完成項執行時間超過逾時值時，就會發生逾時。</span><span class="sxs-lookup"><span data-stu-id="b01e5-148">Timeouts occur when a finalizer in the target process runs for a longer time than the timeout value.</span></span>|  
|<span data-ttu-id="b01e5-149">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="b01e5-149">E_INVALIDARG</span></span>|<span data-ttu-id="b01e5-150">一或多個參數具有無效的值。</span><span class="sxs-lookup"><span data-stu-id="b01e5-150">One or more parameters have invalid values.</span></span>|  
|<span data-ttu-id="b01e5-151">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="b01e5-151">E_FAIL</span></span>|<span data-ttu-id="b01e5-152">發生某個其他未指定的失敗。</span><span class="sxs-lookup"><span data-stu-id="b01e5-152">Some other, unspecified failure occurred.</span></span>|  
|<span data-ttu-id="b01e5-153">其他錯誤碼</span><span class="sxs-lookup"><span data-stu-id="b01e5-153">Other error codes</span></span>|<span data-ttu-id="b01e5-154">如果 profiler 的[ICorProfilerCallback3：： InitializeForAttach](icorprofilercallback3-initializeforattach-method.md)方法傳回表示失敗的 HRESULT，則 `AttachProfiler` 會傳回相同的 hresult。</span><span class="sxs-lookup"><span data-stu-id="b01e5-154">If the profiler’s [ICorProfilerCallback3::InitializeForAttach](icorprofilercallback3-initializeforattach-method.md) method returns an HRESULT that indicates failure, `AttachProfiler` returns that same HRESULT.</span></span> <span data-ttu-id="b01e5-155">在此情況下，E_NOTIMPL 會轉換成 CORPROF_E_PROFILER_NOT_ATTACHABLE。</span><span class="sxs-lookup"><span data-stu-id="b01e5-155">In this case, E_NOTIMPL is converted to CORPROF_E_PROFILER_NOT_ATTACHABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="b01e5-156">備註</span><span class="sxs-lookup"><span data-stu-id="b01e5-156">Remarks</span></span>  
  
## <a name="memory-management"></a><span data-ttu-id="b01e5-157">記憶體管理</span><span class="sxs-lookup"><span data-stu-id="b01e5-157">Memory Management</span></span>  
 <span data-ttu-id="b01e5-158">保持 COM 慣例，`AttachProfiler` 的呼叫端 (例如，程式碼剖析工具開發人員撰寫的觸發程序程式碼) 會負責配置與取消配置 `pvClientData` 參數所指向資料的記憶體。</span><span class="sxs-lookup"><span data-stu-id="b01e5-158">In keeping with COM conventions, the caller of `AttachProfiler` (for example, the trigger code authored by the profiler developer) is responsible for allocating and de-allocating the memory for the data that the `pvClientData` parameter points to.</span></span> <span data-ttu-id="b01e5-159">當 CLR 執行 `AttachProfiler` 呼叫時，它會建立一份 `pvClientData` 指向的記憶體，並將其傳送至目標處理序。</span><span class="sxs-lookup"><span data-stu-id="b01e5-159">When the CLR executes the `AttachProfiler` call, it makes a copy of the memory that `pvClientData` points to and transmits it to the target process.</span></span> <span data-ttu-id="b01e5-160">當目標處理序內的 CLR 收到自己的 `pvClientData` 區塊複本時，它會將區塊透過 `InitializeForAttach` 方法傳遞給程式碼剖析工具，然後再從目標處理序取消配置其 `pvClientData` 區塊複本。</span><span class="sxs-lookup"><span data-stu-id="b01e5-160">When the CLR inside the target process receives its own copy of the `pvClientData` block, it passes the block to the profiler through the `InitializeForAttach` method, and then deallocates its copy of the `pvClientData` block from the target process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b01e5-161">規格需求</span><span class="sxs-lookup"><span data-stu-id="b01e5-161">Requirements</span></span>  
 <span data-ttu-id="b01e5-162">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="b01e5-162">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b01e5-163">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="b01e5-163">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="b01e5-164">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b01e5-164">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b01e5-165">**.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b01e5-165">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b01e5-166">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b01e5-166">See also</span></span>

- [<span data-ttu-id="b01e5-167">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="b01e5-167">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="b01e5-168">ICorProfilerInfo3 介面</span><span class="sxs-lookup"><span data-stu-id="b01e5-168">ICorProfilerInfo3 Interface</span></span>](icorprofilerinfo3-interface.md)
- [<span data-ttu-id="b01e5-169">分析介面</span><span class="sxs-lookup"><span data-stu-id="b01e5-169">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="b01e5-170">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="b01e5-170">Profiling</span></span>](index.md)
