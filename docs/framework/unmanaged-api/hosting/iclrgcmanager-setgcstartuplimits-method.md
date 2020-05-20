---
title: ICLRGCManager::SetGCStartupLimits 方法
ms.date: 03/30/2017
api_name:
- ICLRGCManager.SetGCStartupLimits
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRGCManager::SetGCStartupLimits
helpviewer_keywords:
- SetGCStartupLimits method, ICLRGCManager interface [.NET Framework hosting]
- ICLRGCManager::SetGCStartupLimits method [.NET Framework hosting]
ms.assetid: 1c8d9959-95b5-4131-be4a-556d97774014
topic_type:
- apiref
ms.openlocfilehash: 0dce86a12ed3e93983ee62620fa0ddf7dfbc48f5
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83616940"
---
# <a name="iclrgcmanagersetgcstartuplimits-method"></a><span data-ttu-id="24917-102">ICLRGCManager::SetGCStartupLimits 方法</span><span class="sxs-lookup"><span data-stu-id="24917-102">ICLRGCManager::SetGCStartupLimits Method</span></span>
<span data-ttu-id="24917-103">設定垃圾收集區段的大小，以及垃圾收集系統層代0的大小上限。</span><span class="sxs-lookup"><span data-stu-id="24917-103">Sets the size of a garbage collection segment and the maximum size of the garbage collection system's generation 0.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="24917-104">從 .NET Framework 4.5 開始，您可以 `DWORD` 使用[ICLRGCManager2：： SetGCStartupLimitsEx](iclrgcmanager2-setgcstartuplimitsex-method.md)方法，將區段大小和最大層代0的大小設定為大於的值。</span><span class="sxs-lookup"><span data-stu-id="24917-104">Starting with the .NET Framework 4.5, you can set segment size and maximum generation 0 size to values greater than `DWORD` by using the [ICLRGCManager2::SetGCStartupLimitsEx](iclrgcmanager2-setgcstartuplimitsex-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="24917-105">語法</span><span class="sxs-lookup"><span data-stu-id="24917-105">Syntax</span></span>  
  
```cpp  
HRESULT SetGCStartupLimits (  
    [in] DWORD SegmentSize,
    [in] DWORD MaxGen0Size  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="24917-106">參數</span><span class="sxs-lookup"><span data-stu-id="24917-106">Parameters</span></span>  
 `SegmentSize`  
 <span data-ttu-id="24917-107">在垃圾收集區段的指定大小。</span><span class="sxs-lookup"><span data-stu-id="24917-107">[in] The specified size of a garbage collection segment.</span></span>  
  
 <span data-ttu-id="24917-108">最社區段大小為 4 MB。</span><span class="sxs-lookup"><span data-stu-id="24917-108">The minimum segment size is 4 MB.</span></span> <span data-ttu-id="24917-109">區段可以增加 1 MB 或更大的增量。</span><span class="sxs-lookup"><span data-stu-id="24917-109">Segments can be increased in increments of 1 MB or larger.</span></span>  
  
 `MaxGen0Size`  
 <span data-ttu-id="24917-110">在層代0的指定大小上限。</span><span class="sxs-lookup"><span data-stu-id="24917-110">[in] The specified maximum size for generation 0.</span></span>  
  
 <span data-ttu-id="24917-111">層代0的最小值為 64 KB。</span><span class="sxs-lookup"><span data-stu-id="24917-111">The minimum generation 0 size is 64 KB.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="24917-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="24917-112">Return Value</span></span>  
  
|<span data-ttu-id="24917-113">HRESULT</span><span class="sxs-lookup"><span data-stu-id="24917-113">HRESULT</span></span>|<span data-ttu-id="24917-114">說明</span><span class="sxs-lookup"><span data-stu-id="24917-114">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="24917-115">S_OK</span><span class="sxs-lookup"><span data-stu-id="24917-115">S_OK</span></span>|<span data-ttu-id="24917-116">`SetGCStartupLimits`已成功傳回。</span><span class="sxs-lookup"><span data-stu-id="24917-116">`SetGCStartupLimits` returned successfully.</span></span>|  
|<span data-ttu-id="24917-117">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="24917-117">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="24917-118">Common language runtime （CLR）尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="24917-118">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="24917-119">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="24917-119">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="24917-120">呼叫超時。</span><span class="sxs-lookup"><span data-stu-id="24917-120">The call timed out.</span></span>|  
|<span data-ttu-id="24917-121">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="24917-121">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="24917-122">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="24917-122">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="24917-123">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="24917-123">HOST_E_ABANDONED</span></span>|<span data-ttu-id="24917-124">已封鎖的執行緒或光纖在等候時取消了事件。</span><span class="sxs-lookup"><span data-stu-id="24917-124">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="24917-125">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="24917-125">E_FAIL</span></span>|<span data-ttu-id="24917-126">發生不明的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="24917-126">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="24917-127">在方法傳回 E_FAIL 之後，CLR 就無法在進程內使用。</span><span class="sxs-lookup"><span data-stu-id="24917-127">After a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="24917-128">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="24917-128">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="24917-129">備註</span><span class="sxs-lookup"><span data-stu-id="24917-129">Remarks</span></span>  
 <span data-ttu-id="24917-130">設定的值 `SetGCStartupLimits` 只能指定一次。</span><span class="sxs-lookup"><span data-stu-id="24917-130">The values that `SetGCStartupLimits` sets can be specified only once.</span></span> <span data-ttu-id="24917-131">稍後對 `SetGCStartupLimits` 的呼叫會被忽略。</span><span class="sxs-lookup"><span data-stu-id="24917-131">Later calls to `SetGCStartupLimits` are ignored.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="24917-132">需求</span><span class="sxs-lookup"><span data-stu-id="24917-132">Requirements</span></span>  
 <span data-ttu-id="24917-133">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="24917-133">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="24917-134">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="24917-134">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="24917-135">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="24917-135">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="24917-136">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="24917-136">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="24917-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="24917-137">See also</span></span>

- [<span data-ttu-id="24917-138">自動記憶體管理</span><span class="sxs-lookup"><span data-stu-id="24917-138">Automatic Memory Management</span></span>](../../../standard/automatic-memory-management.md)
- [<span data-ttu-id="24917-139">記憶體回收</span><span class="sxs-lookup"><span data-stu-id="24917-139">Garbage Collection</span></span>](../../../standard/garbage-collection/index.md)
- [<span data-ttu-id="24917-140">ICLRControl 介面</span><span class="sxs-lookup"><span data-stu-id="24917-140">ICLRControl Interface</span></span>](iclrcontrol-interface.md)
- [<span data-ttu-id="24917-141">ICLRGCManager 介面</span><span class="sxs-lookup"><span data-stu-id="24917-141">ICLRGCManager Interface</span></span>](iclrgcmanager-interface.md)
