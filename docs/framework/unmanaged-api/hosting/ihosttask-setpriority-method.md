---
title: IHostTask::SetPriority 方法
ms.date: 03/30/2017
api_name:
- IHostTask.SetPriority
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask::SetPriority
helpviewer_keywords:
- IHostTask::SetPriority method [.NET Framework hosting]
- SetPriority method [.NET Framework hosting]
ms.assetid: cd8c379b-c7a0-434f-8e23-899bd26be75d
topic_type:
- apiref
ms.openlocfilehash: ac3a8479cdf05e55885bd55d4e4fb8e6e47686f9
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842394"
---
# <a name="ihosttasksetpriority-method"></a><span data-ttu-id="4cfd4-102">IHostTask::SetPriority 方法</span><span class="sxs-lookup"><span data-stu-id="4cfd4-102">IHostTask::SetPriority Method</span></span>
<span data-ttu-id="4cfd4-103">要求主機針對目前[IHostTask](ihosttask-interface.md)實例所代表的工作，調整執行緒優先順序層級。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-103">Requests that the host adjust the thread priority level for the task represented by the current [IHostTask](ihosttask-interface.md) instance.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4cfd4-104">語法</span><span class="sxs-lookup"><span data-stu-id="4cfd4-104">Syntax</span></span>  
  
```cpp  
HRESULT SetPriority (  
    [in] int newPriority  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="4cfd4-105">參數</span><span class="sxs-lookup"><span data-stu-id="4cfd4-105">Parameters</span></span>  
 `newPriority`  
 <span data-ttu-id="4cfd4-106">在整數，表示目前實例所代表之工作的要求的執行緒優先順序值 `IHostTask` 。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-106">[in] An integer that represents the requested thread priority value for the task represented by the current `IHostTask` instance.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="4cfd4-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="4cfd4-107">Return Value</span></span>  
  
|<span data-ttu-id="4cfd4-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="4cfd4-108">HRESULT</span></span>|<span data-ttu-id="4cfd4-109">描述</span><span class="sxs-lookup"><span data-stu-id="4cfd4-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="4cfd4-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="4cfd4-110">S_OK</span></span>|<span data-ttu-id="4cfd4-111">`SetPriority`已成功傳回。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-111">`SetPriority` returned successfully.</span></span>|  
|<span data-ttu-id="4cfd4-112">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="4cfd4-112">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="4cfd4-113">Common language runtime （CLR）尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-113">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="4cfd4-114">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="4cfd4-114">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="4cfd4-115">呼叫超時。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-115">The call timed out.</span></span>|  
|<span data-ttu-id="4cfd4-116">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="4cfd4-116">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="4cfd4-117">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-117">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="4cfd4-118">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="4cfd4-118">HOST_E_ABANDONED</span></span>|<span data-ttu-id="4cfd4-119">已封鎖的執行緒或光纖在等候時取消了事件。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-119">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="4cfd4-120">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="4cfd4-120">E_FAIL</span></span>|<span data-ttu-id="4cfd4-121">發生不明的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-121">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="4cfd4-122">當方法傳回 E_FAIL 時，CLR 就無法在進程內使用。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-122">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="4cfd4-123">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-123">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="4cfd4-124">備註</span><span class="sxs-lookup"><span data-stu-id="4cfd4-124">Remarks</span></span>  
 <span data-ttu-id="4cfd4-125">執行緒會使用迴圈配置資源系統（部分根據執行緒的優先權層級）來授與處理時間。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-125">Threads are granted processing time using a round-robin system that is partly based on a thread's priority level.</span></span> <span data-ttu-id="4cfd4-126">`SetPriority`允許 CLR 設定目前工作的執行緒優先權層級。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-126">`SetPriority` allows the CLR to set that thread priority level for the current task.</span></span> <span data-ttu-id="4cfd4-127">支援下列 `newPriority` 值。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-127">The following `newPriority` values are supported.</span></span>  
  
- <span data-ttu-id="4cfd4-128">THREAD_PRIORITY_ABOVE_NORMAL</span><span class="sxs-lookup"><span data-stu-id="4cfd4-128">THREAD_PRIORITY_ABOVE_NORMAL</span></span>  
  
- <span data-ttu-id="4cfd4-129">THREAD_PRIORITY_BELOW_NORMAL</span><span class="sxs-lookup"><span data-stu-id="4cfd4-129">THREAD_PRIORITY_BELOW_NORMAL</span></span>  
  
- <span data-ttu-id="4cfd4-130">THREAD_PRIORITY_HIGHEST</span><span class="sxs-lookup"><span data-stu-id="4cfd4-130">THREAD_PRIORITY_HIGHEST</span></span>  
  
- <span data-ttu-id="4cfd4-131">THREAD_PRIORITY_IDLE</span><span class="sxs-lookup"><span data-stu-id="4cfd4-131">THREAD_PRIORITY_IDLE</span></span>  
  
- <span data-ttu-id="4cfd4-132">THREAD_PRIORITY_LOWEST</span><span class="sxs-lookup"><span data-stu-id="4cfd4-132">THREAD_PRIORITY_LOWEST</span></span>  
  
- <span data-ttu-id="4cfd4-133">THREAD_PRIORITY_NORMAL</span><span class="sxs-lookup"><span data-stu-id="4cfd4-133">THREAD_PRIORITY_NORMAL</span></span>  
  
- <span data-ttu-id="4cfd4-134">THREAD_PRIORITY_TIME_CRITICAL</span><span class="sxs-lookup"><span data-stu-id="4cfd4-134">THREAD_PRIORITY_TIME_CRITICAL</span></span>  
  
 <span data-ttu-id="4cfd4-135">`SetPriority`當使用者程式碼修改的值時，CLR <xref:System.Threading.Thread.Priority%2A?displayProperty=nameWithType> 會呼叫。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-135">The CLR calls `SetPriority` when the value of the <xref:System.Threading.Thread.Priority%2A?displayProperty=nameWithType> is modified by user code.</span></span> <span data-ttu-id="4cfd4-136">主機可以針對執行緒優先順序指派定義自己的演算法，並可隨意忽略此要求。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-136">A host can define its own algorithms for thread priority assignment, and is free to ignore this request.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="4cfd4-137">`SetPriority`不會報告執行緒優先權層級是否已變更。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-137">`SetPriority` does not report whether the thread priority level was changed.</span></span> <span data-ttu-id="4cfd4-138">呼叫[IHostTask：： GetPriority](ihosttask-getpriority-method.md)以判斷工作的執行緒優先順序層級值。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-138">Call [IHostTask::GetPriority](ihosttask-getpriority-method.md) to determine the value of the task's thread priority level.</span></span>  
  
 <span data-ttu-id="4cfd4-139">執行緒優先權層級的值是由 Win32 `SetThreadPriority` 函數所定義。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-139">Thread priority level values are defined by the Win32 `SetThreadPriority` function.</span></span> <span data-ttu-id="4cfd4-140">如需執行緒優先順序的詳細資訊，請參閱 Windows 平臺檔。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-140">For more information about thread priority, see the Windows Platform documentation.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4cfd4-141">規格需求</span><span class="sxs-lookup"><span data-stu-id="4cfd4-141">Requirements</span></span>  
 <span data-ttu-id="4cfd4-142">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="4cfd4-142">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4cfd4-143">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="4cfd4-143">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="4cfd4-144">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="4cfd4-144">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="4cfd4-145">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4cfd4-145">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4cfd4-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4cfd4-146">See also</span></span>

- <xref:System.Threading.Thread>
- [<span data-ttu-id="4cfd4-147">ICLRTask 介面</span><span class="sxs-lookup"><span data-stu-id="4cfd4-147">ICLRTask Interface</span></span>](iclrtask-interface.md)
- [<span data-ttu-id="4cfd4-148">ICLRTaskManager 介面</span><span class="sxs-lookup"><span data-stu-id="4cfd4-148">ICLRTaskManager Interface</span></span>](iclrtaskmanager-interface.md)
- [<span data-ttu-id="4cfd4-149">IHostTask 介面</span><span class="sxs-lookup"><span data-stu-id="4cfd4-149">IHostTask Interface</span></span>](ihosttask-interface.md)
- [<span data-ttu-id="4cfd4-150">GetPriority 方法</span><span class="sxs-lookup"><span data-stu-id="4cfd4-150">GetPriority Method</span></span>](ihosttask-getpriority-method.md)
- [<span data-ttu-id="4cfd4-151">IHostTaskManager 介面</span><span class="sxs-lookup"><span data-stu-id="4cfd4-151">IHostTaskManager Interface</span></span>](ihosttaskmanager-interface.md)
