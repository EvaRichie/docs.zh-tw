---
title: ICorProfilerInfo4::RequestRevert 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.RequestRevert
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::RequestRevert
helpviewer_keywords:
- RequestRevert method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::RequestRevert method [.NET Framework profiling]
ms.assetid: 70261da5-5933-4e25-9de0-ddf51cba56cc
topic_type:
- apiref
ms.openlocfilehash: b80de5e0e03f6b3a424ac59a099e361dd6c50c86
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95733811"
---
# <a name="icorprofilerinfo4requestrevert-method"></a><span data-ttu-id="59d96-102">ICorProfilerInfo4::RequestRevert 方法</span><span class="sxs-lookup"><span data-stu-id="59d96-102">ICorProfilerInfo4::RequestRevert Method</span></span>

<span data-ttu-id="59d96-103">將指定函式的所有執行個體還原成其原始版本。</span><span class="sxs-lookup"><span data-stu-id="59d96-103">Reverts all instances of the specified functions to their original versions.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="59d96-104">語法</span><span class="sxs-lookup"><span data-stu-id="59d96-104">Syntax</span></span>  
  
```cpp  
HRESULT RequestRevert (  
   [in] ULONG    cFunctions,  
   [in, size_is(cFunctions)]  ModuleID    moduleIds[],  
   [in, size_is(cFunctions)]  mdMethodDef methodIds[],  
   [out, size_is(cFunctions)]  HRESULT status[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="59d96-105">參數</span><span class="sxs-lookup"><span data-stu-id="59d96-105">Parameters</span></span>  

 `cFunctions`  
 <span data-ttu-id="59d96-106">[in] 要還原的函式數目。</span><span class="sxs-lookup"><span data-stu-id="59d96-106">[in] The number of functions to revert.</span></span>  
  
 `moduleIds`  
 <span data-ttu-id="59d96-107">[in] 指定 (`module`, `methodDef`) 組的 `moduleId` 部分，這個部分可識別要還原的函式。</span><span class="sxs-lookup"><span data-stu-id="59d96-107">[in] Specifies the `moduleId` portion of the (`module`, `methodDef`) pairs that identify the functions to be reverted.</span></span>  
  
 `methodIds`  
 <span data-ttu-id="59d96-108">[in] 指定 (`module`, `methodDef`) 組的 `methodId` 部分，這個部分可識別要還原的函式。</span><span class="sxs-lookup"><span data-stu-id="59d96-108">[in] Specifies the `methodId` portion of the (`module`, `methodDef`) pairs that identify the functions to be reverted.</span></span>  
  
 `status`  
 <span data-ttu-id="59d96-109">[out] HRESULT 的陣列 (列於本主題稍後的＜狀態 HRESULT＞一節)。</span><span class="sxs-lookup"><span data-stu-id="59d96-109">[out] An array of HRESULTs listed in the "Status HRESULTs" section later in this topic.</span></span> <span data-ttu-id="59d96-110">每個 HRESULT 會指出嘗試還原平行陣列 `moduleIds` 和 `methodIds` 中所指定的每個函式是成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="59d96-110">Each HRESULT indicates the success or failure of trying to revert each function specified in the parallel arrays `moduleIds` and `methodIds`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="59d96-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="59d96-111">Return Value</span></span>  

 <span data-ttu-id="59d96-112">這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。</span><span class="sxs-lookup"><span data-stu-id="59d96-112">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="59d96-113">HRESULT</span><span class="sxs-lookup"><span data-stu-id="59d96-113">HRESULT</span></span>|<span data-ttu-id="59d96-114">描述</span><span class="sxs-lookup"><span data-stu-id="59d96-114">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="59d96-115">S_OK</span><span class="sxs-lookup"><span data-stu-id="59d96-115">S_OK</span></span>|<span data-ttu-id="59d96-116">嘗試還原所有要求；不過，必須檢查傳回的狀態陣列，以判斷哪些函式成功還原。</span><span class="sxs-lookup"><span data-stu-id="59d96-116">An attempt was made to revert all requests; however, the returned status array must be checked to determine which functions were successfully reverted.</span></span>|  
|<span data-ttu-id="59d96-117">CORPROF_E_CALLBACK4_REQUIRED</span><span class="sxs-lookup"><span data-stu-id="59d96-117">CORPROF_E_CALLBACK4_REQUIRED</span></span>|<span data-ttu-id="59d96-118">分析工具必須執行 [ICorProfilerCallback4](icorprofilercallback4-interface.md) 介面，才能支援此呼叫。</span><span class="sxs-lookup"><span data-stu-id="59d96-118">The profiler must implement the [ICorProfilerCallback4](icorprofilercallback4-interface.md) interface for this call to be supported.</span></span>|  
|<span data-ttu-id="59d96-119">CORPROF_E_REJIT_NOT_ENABLED</span><span class="sxs-lookup"><span data-stu-id="59d96-119">CORPROF_E_REJIT_NOT_ENABLED</span></span>|<span data-ttu-id="59d96-120">尚未啟用 JIT 重新編譯。</span><span class="sxs-lookup"><span data-stu-id="59d96-120">JIT recompilation has not been enabled.</span></span> <span data-ttu-id="59d96-121">您必須在初始化期間啟用 JIT 重新編譯，方法是使用 [ICorProfilerInfo：： SetEventMask](icorprofilerinfo-seteventmask-method.md) 方法來設定 `COR_PRF_ENABLE_REJIT` 旗標。</span><span class="sxs-lookup"><span data-stu-id="59d96-121">You must enable JIT recompilation during initialization by using the [ICorProfilerInfo::SetEventMask](icorprofilerinfo-seteventmask-method.md) method to set the `COR_PRF_ENABLE_REJIT` flag.</span></span>|  
|<span data-ttu-id="59d96-122">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="59d96-122">E_INVALIDARG</span></span>|<span data-ttu-id="59d96-123">`cFunctions` 為 0，或者 `moduleIds` 或 `methodIds` 為 `NULL`。</span><span class="sxs-lookup"><span data-stu-id="59d96-123">`cFunctions` is 0, or `moduleIds` or `methodIds` is `NULL`.</span></span>|  
|<span data-ttu-id="59d96-124">E_OUTOFMEMORY</span><span class="sxs-lookup"><span data-stu-id="59d96-124">E_OUTOFMEMORY</span></span>|<span data-ttu-id="59d96-125">CLR 無法完成要求，因為記憶體不足。</span><span class="sxs-lookup"><span data-stu-id="59d96-125">The CLR was unable to complete the request because it ran out of memory.</span></span>|  
  
## <a name="status-hresults"></a><span data-ttu-id="59d96-126">狀態 HRESULT</span><span class="sxs-lookup"><span data-stu-id="59d96-126">Status HRESULTS</span></span>  
  
|<span data-ttu-id="59d96-127">狀態陣列 HRESULT</span><span class="sxs-lookup"><span data-stu-id="59d96-127">Status array HRESULT</span></span>|<span data-ttu-id="59d96-128">描述</span><span class="sxs-lookup"><span data-stu-id="59d96-128">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="59d96-129">S_OK</span><span class="sxs-lookup"><span data-stu-id="59d96-129">S_OK</span></span>|<span data-ttu-id="59d96-130">已成功還原對應的函式。</span><span class="sxs-lookup"><span data-stu-id="59d96-130">The corresponding function was successfully reverted.</span></span>|  
|<span data-ttu-id="59d96-131">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="59d96-131">E_INVALIDARG</span></span>|<span data-ttu-id="59d96-132">`moduleID` 或 `methodDef` 參數為 `NULL`。</span><span class="sxs-lookup"><span data-stu-id="59d96-132">The `moduleID` or `methodDef` parameter is `NULL`.</span></span>|  
|<span data-ttu-id="59d96-133">CORPROF_E_DATAINCOMPLETE</span><span class="sxs-lookup"><span data-stu-id="59d96-133">CORPROF_E_DATAINCOMPLETE</span></span>|<span data-ttu-id="59d96-134">這個模組未完全載入，或正在進行卸載。</span><span class="sxs-lookup"><span data-stu-id="59d96-134">The module is not fully loaded yet, or it is in the process of being unloaded.</span></span>|  
|<span data-ttu-id="59d96-135">CORPROF_E_MODULE_IS_DYNAMIC</span><span class="sxs-lookup"><span data-stu-id="59d96-135">CORPROF_E_MODULE_IS_DYNAMIC</span></span>|<span data-ttu-id="59d96-136">已動態產生指定的模組 (例如透過 `Reflection.Emit`)，</span><span class="sxs-lookup"><span data-stu-id="59d96-136">The specified module was dynamically generated (for example by `Reflection.Emit`).</span></span> <span data-ttu-id="59d96-137">因此不受這個方法的支援。</span><span class="sxs-lookup"><span data-stu-id="59d96-137">Therefore, it is not supported by this method.</span></span>|  
|<span data-ttu-id="59d96-138">CORPROF_E_ACTIVE_REJIT_REQUEST_NOT_FOUND</span><span class="sxs-lookup"><span data-stu-id="59d96-138">CORPROF_E_ACTIVE_REJIT_REQUEST_NOT_FOUND</span></span>|<span data-ttu-id="59d96-139">CLR 無法還原指定的函式，因為找不到對應的作用中重新編譯要求。</span><span class="sxs-lookup"><span data-stu-id="59d96-139">The CLR could not revert the specified function, because a corresponding active recompilation request was not found.</span></span> <span data-ttu-id="59d96-140">從未要求重新編譯或已還原函式。</span><span class="sxs-lookup"><span data-stu-id="59d96-140">Either the recompilation was never requested or the function was already reverted.</span></span>|  
|<span data-ttu-id="59d96-141">其他</span><span class="sxs-lookup"><span data-stu-id="59d96-141">Other</span></span>|<span data-ttu-id="59d96-142">作業系統會傳回在 CLR 的控制項外發生的失敗。</span><span class="sxs-lookup"><span data-stu-id="59d96-142">The operating system returned a failure outside the control of the CLR.</span></span> <span data-ttu-id="59d96-143">例如，如果變更記憶體分頁之存取保護的系統呼叫失敗，則會顯示作業系統錯誤。</span><span class="sxs-lookup"><span data-stu-id="59d96-143">For example, if a system call to change the access protection of a page of memory fails, the operating system error will be displayed.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="59d96-144">備註</span><span class="sxs-lookup"><span data-stu-id="59d96-144">Remarks</span></span>  

 <span data-ttu-id="59d96-145">下次呼叫已還原的任何函式執行個體時，便會執行函式的原始版本。</span><span class="sxs-lookup"><span data-stu-id="59d96-145">The next time any of the revereted function instances are called, the original versions of the functions will be run.</span></span> <span data-ttu-id="59d96-146">如果函式已在執行中，則會結束執行正在執行的版本。</span><span class="sxs-lookup"><span data-stu-id="59d96-146">If a function is already running, it will finish executing the version that is running.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="59d96-147">需求</span><span class="sxs-lookup"><span data-stu-id="59d96-147">Requirements</span></span>  

 <span data-ttu-id="59d96-148">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="59d96-148">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="59d96-149">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="59d96-149">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="59d96-150">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="59d96-150">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="59d96-151">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="59d96-151">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="59d96-152">另請參閱</span><span class="sxs-lookup"><span data-stu-id="59d96-152">See also</span></span>

- [<span data-ttu-id="59d96-153">ICorProfilerInfo4 介面</span><span class="sxs-lookup"><span data-stu-id="59d96-153">ICorProfilerInfo4 Interface</span></span>](icorprofilerinfo4-interface.md)
- [<span data-ttu-id="59d96-154">分析介面</span><span class="sxs-lookup"><span data-stu-id="59d96-154">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="59d96-155">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="59d96-155">Profiling</span></span>](index.md)
