---
title: ICLRSyncManager::GetRWLockOwnerNext 方法
ms.date: 03/30/2017
api_name:
- ICLRSyncManager.GetRWLockOwnerNext
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRSyncManager::GetRWLockOwnerNext
helpviewer_keywords:
- ICLRSyncManager::GetRWLockOwnerNext method [.NET Framework hosting]
- GetRWLockOwnerNext method [.NET Framework hosting]
ms.assetid: 0e025b6a-280e-40a2-a2d0-b15f58777b81
topic_type:
- apiref
ms.openlocfilehash: e5a8f69e66bb4b6373aea2c753bff9351bff8128
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762483"
---
# <a name="iclrsyncmanagergetrwlockownernext-method"></a><span data-ttu-id="8cbe7-102">ICLRSyncManager::GetRWLockOwnerNext 方法</span><span class="sxs-lookup"><span data-stu-id="8cbe7-102">ICLRSyncManager::GetRWLockOwnerNext Method</span></span>
<span data-ttu-id="8cbe7-103">取得目前讀取器寫入器鎖定上封鎖的下一個[IHostTask](ihosttask-interface.md)實例。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-103">Gets the next [IHostTask](ihosttask-interface.md) instance that is blocked on the current reader-writer lock.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8cbe7-104">語法</span><span class="sxs-lookup"><span data-stu-id="8cbe7-104">Syntax</span></span>  
  
```cpp
HRESULT GetRWLockOwnerNext (  
    [in] SIZE_T       Iterator,  
    [out] IHostTask  *ppOwnerHostTask  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="8cbe7-105">參數</span><span class="sxs-lookup"><span data-stu-id="8cbe7-105">Parameters</span></span>  
 `Iterator`  
 <span data-ttu-id="8cbe7-106">在使用[CreateRWLockOwnerIterator](iclrsyncmanager-createrwlockowneriterator-method.md)的呼叫所建立的反覆運算器。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-106">[in] The iterator that was created by using a call to [CreateRWLockOwnerIterator](iclrsyncmanager-createrwlockowneriterator-method.md).</span></span>  
  
 `ppOwnerHostTask`  
 <span data-ttu-id="8cbe7-107">脫銷下一個 `IHostTask` 正在等候鎖定的指標，如果沒有任何工作正在等候，則為 null。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-107">[out] A pointer to the next `IHostTask` that is waiting on the lock, or null if no task is waiting.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="8cbe7-108">傳回值</span><span class="sxs-lookup"><span data-stu-id="8cbe7-108">Return Value</span></span>  
  
|<span data-ttu-id="8cbe7-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="8cbe7-109">HRESULT</span></span>|<span data-ttu-id="8cbe7-110">Description</span><span class="sxs-lookup"><span data-stu-id="8cbe7-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="8cbe7-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="8cbe7-111">S_OK</span></span>|<span data-ttu-id="8cbe7-112">`GetRWLockOwnerNext`已成功傳回。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-112">`GetRWLockOwnerNext` returned successfully.</span></span>|  
|<span data-ttu-id="8cbe7-113">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="8cbe7-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="8cbe7-114">Common language runtime （CLR）尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-114">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="8cbe7-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="8cbe7-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="8cbe7-116">呼叫超時。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-116">The call timed out.</span></span>|  
|<span data-ttu-id="8cbe7-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="8cbe7-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="8cbe7-118">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="8cbe7-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="8cbe7-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="8cbe7-120">已封鎖的執行緒或光纖在等候時取消了事件。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="8cbe7-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="8cbe7-121">E_FAIL</span></span>|<span data-ttu-id="8cbe7-122">發生不明的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="8cbe7-123">當方法傳回 E_FAIL 時，CLR 就無法在進程內使用。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-123">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="8cbe7-124">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="8cbe7-125">備註</span><span class="sxs-lookup"><span data-stu-id="8cbe7-125">Remarks</span></span>  
 <span data-ttu-id="8cbe7-126">如果 `ppOwnerHostTask` 設定為 null，則反復專案會終止，而且主機應該呼叫[DeleteRWLockOwnerIterator](iclrsyncmanager-deleterwlockowneriterator-method.md)方法。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-126">If `ppOwnerHostTask` is set to null, the iteration has terminated, and the host should call the [DeleteRWLockOwnerIterator](iclrsyncmanager-deleterwlockowneriterator-method.md) method.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8cbe7-127">CLR 會在上呼叫，以便在 `AddRef` `IHostTask` 主機保有 `ppOwnerHostTask` 指標時，阻止這項工作結束。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-127">The CLR calls `AddRef` on the `IHostTask` to which `ppOwnerHostTask` points to prevent this task from exiting while the host holds the pointer.</span></span> <span data-ttu-id="8cbe7-128">主機完成時，必須呼叫 `Release` 以遞減參考計數。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-128">The host must call `Release` to decrement the reference count when it is finished.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8cbe7-129">規格需求</span><span class="sxs-lookup"><span data-stu-id="8cbe7-129">Requirements</span></span>  
 <span data-ttu-id="8cbe7-130">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="8cbe7-130">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8cbe7-131">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="8cbe7-131">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="8cbe7-132">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="8cbe7-132">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="8cbe7-133">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8cbe7-133">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8cbe7-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8cbe7-134">See also</span></span>

- [<span data-ttu-id="8cbe7-135">ICLRSyncManager 介面</span><span class="sxs-lookup"><span data-stu-id="8cbe7-135">ICLRSyncManager Interface</span></span>](iclrsyncmanager-interface.md)
- [<span data-ttu-id="8cbe7-136">IHostSyncManager 介面</span><span class="sxs-lookup"><span data-stu-id="8cbe7-136">IHostSyncManager Interface</span></span>](ihostsyncmanager-interface.md)
