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
ms.openlocfilehash: 169d344975762b97f89e8dc32d72f2b9c95fea11
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95678164"
---
# <a name="iclrgcmanagersetgcstartuplimits-method"></a><span data-ttu-id="db5cd-102">ICLRGCManager::SetGCStartupLimits 方法</span><span class="sxs-lookup"><span data-stu-id="db5cd-102">ICLRGCManager::SetGCStartupLimits Method</span></span>

<span data-ttu-id="db5cd-103">設定垃圾收集區段的大小，以及垃圾收集系統之層代0的大小上限。</span><span class="sxs-lookup"><span data-stu-id="db5cd-103">Sets the size of a garbage collection segment and the maximum size of the garbage collection system's generation 0.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="db5cd-104">從 .NET Framework 4.5 開始，您可以 `DWORD` 使用 [ICLRGCManager2：： SetGCStartupLimitsEx](iclrgcmanager2-setgcstartuplimitsex-method.md) 方法，將區段大小和最大層代0大小設定為大於的值。</span><span class="sxs-lookup"><span data-stu-id="db5cd-104">Starting with the .NET Framework 4.5, you can set segment size and maximum generation 0 size to values greater than `DWORD` by using the [ICLRGCManager2::SetGCStartupLimitsEx](iclrgcmanager2-setgcstartuplimitsex-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="db5cd-105">語法</span><span class="sxs-lookup"><span data-stu-id="db5cd-105">Syntax</span></span>  
  
```cpp  
HRESULT SetGCStartupLimits (  
    [in] DWORD SegmentSize,
    [in] DWORD MaxGen0Size  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="db5cd-106">參數</span><span class="sxs-lookup"><span data-stu-id="db5cd-106">Parameters</span></span>  

 `SegmentSize`  
 <span data-ttu-id="db5cd-107">在指定的垃圾收集區段大小。</span><span class="sxs-lookup"><span data-stu-id="db5cd-107">[in] The specified size of a garbage collection segment.</span></span>  
  
 <span data-ttu-id="db5cd-108">最社區段大小為 4 MB。</span><span class="sxs-lookup"><span data-stu-id="db5cd-108">The minimum segment size is 4 MB.</span></span> <span data-ttu-id="db5cd-109">區段可以 1 MB 或更大的遞增方式增加。</span><span class="sxs-lookup"><span data-stu-id="db5cd-109">Segments can be increased in increments of 1 MB or larger.</span></span>  
  
 `MaxGen0Size`  
 <span data-ttu-id="db5cd-110">在層代0的指定大小上限。</span><span class="sxs-lookup"><span data-stu-id="db5cd-110">[in] The specified maximum size for generation 0.</span></span>  
  
 <span data-ttu-id="db5cd-111">層代0的最小值為 64 KB。</span><span class="sxs-lookup"><span data-stu-id="db5cd-111">The minimum generation 0 size is 64 KB.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="db5cd-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="db5cd-112">Return Value</span></span>  
  
|<span data-ttu-id="db5cd-113">HRESULT</span><span class="sxs-lookup"><span data-stu-id="db5cd-113">HRESULT</span></span>|<span data-ttu-id="db5cd-114">描述</span><span class="sxs-lookup"><span data-stu-id="db5cd-114">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="db5cd-115">S_OK</span><span class="sxs-lookup"><span data-stu-id="db5cd-115">S_OK</span></span>|<span data-ttu-id="db5cd-116">`SetGCStartupLimits` 傳回成功。</span><span class="sxs-lookup"><span data-stu-id="db5cd-116">`SetGCStartupLimits` returned successfully.</span></span>|  
|<span data-ttu-id="db5cd-117">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="db5cd-117">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="db5cd-118">Common language runtime (CLR) 尚未載入至進程，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="db5cd-118">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="db5cd-119">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="db5cd-119">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="db5cd-120">呼叫已超時。</span><span class="sxs-lookup"><span data-stu-id="db5cd-120">The call timed out.</span></span>|  
|<span data-ttu-id="db5cd-121">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="db5cd-121">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="db5cd-122">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="db5cd-122">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="db5cd-123">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="db5cd-123">HOST_E_ABANDONED</span></span>|<span data-ttu-id="db5cd-124">當封鎖的執行緒或光纖正在等候時，已取消事件。</span><span class="sxs-lookup"><span data-stu-id="db5cd-124">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="db5cd-125">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="db5cd-125">E_FAIL</span></span>|<span data-ttu-id="db5cd-126">發生未知的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="db5cd-126">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="db5cd-127">在方法傳回 E_FAIL 之後，就無法在進程中使用 CLR。</span><span class="sxs-lookup"><span data-stu-id="db5cd-127">After a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="db5cd-128">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="db5cd-128">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="db5cd-129">備註</span><span class="sxs-lookup"><span data-stu-id="db5cd-129">Remarks</span></span>  

 <span data-ttu-id="db5cd-130">設定的值只能 `SetGCStartupLimits` 指定一次。</span><span class="sxs-lookup"><span data-stu-id="db5cd-130">The values that `SetGCStartupLimits` sets can be specified only once.</span></span> <span data-ttu-id="db5cd-131">稍後的呼叫 `SetGCStartupLimits` 會被忽略。</span><span class="sxs-lookup"><span data-stu-id="db5cd-131">Later calls to `SetGCStartupLimits` are ignored.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="db5cd-132">需求</span><span class="sxs-lookup"><span data-stu-id="db5cd-132">Requirements</span></span>  

 <span data-ttu-id="db5cd-133">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="db5cd-133">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="db5cd-134">**標頭：** Mscoree.dll</span><span class="sxs-lookup"><span data-stu-id="db5cd-134">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="db5cd-135">連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="db5cd-135">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="db5cd-136">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="db5cd-136">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="db5cd-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="db5cd-137">See also</span></span>

- [<span data-ttu-id="db5cd-138">自動記憶體管理</span><span class="sxs-lookup"><span data-stu-id="db5cd-138">Automatic Memory Management</span></span>](../../../standard/automatic-memory-management.md)
- [<span data-ttu-id="db5cd-139">記憶體回收</span><span class="sxs-lookup"><span data-stu-id="db5cd-139">Garbage Collection</span></span>](../../../standard/garbage-collection/index.md)
- [<span data-ttu-id="db5cd-140">ICLRControl 介面</span><span class="sxs-lookup"><span data-stu-id="db5cd-140">ICLRControl Interface</span></span>](iclrcontrol-interface.md)
- [<span data-ttu-id="db5cd-141">ICLRGCManager 介面</span><span class="sxs-lookup"><span data-stu-id="db5cd-141">ICLRGCManager Interface</span></span>](iclrgcmanager-interface.md)
