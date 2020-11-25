---
title: ICLRPolicyManager::SetActionOnTimeout 方法
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager.SetActionOnTimeout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager::SetActionOnTimeout
helpviewer_keywords:
- SetActionOnTimeout method [.NET Framework hosting]
- ICLRPolicyManager::SetActionOnTimeout method [.NET Framework hosting]
ms.assetid: 38439fa1-2b99-4fa8-a6ec-08afc0f83b9c
topic_type:
- apiref
ms.openlocfilehash: 3ddd78ea35d5709abb30af085b2212a09b28c2ef
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95725556"
---
# <a name="iclrpolicymanagersetactionontimeout-method"></a><span data-ttu-id="fd7fd-102">ICLRPolicyManager::SetActionOnTimeout 方法</span><span class="sxs-lookup"><span data-stu-id="fd7fd-102">ICLRPolicyManager::SetActionOnTimeout Method</span></span>

<span data-ttu-id="fd7fd-103">指定當指定的作業超時時，common language runtime (CLR) 應採用的原則動作。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-103">Specifies the policy action the common language runtime (CLR) should take when the specified operation times out.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fd7fd-104">語法</span><span class="sxs-lookup"><span data-stu-id="fd7fd-104">Syntax</span></span>  
  
```cpp  
HRESULT SetActionOnTimeout (  
    [in] EClrOperation operation,  
    [in] EPolicyAction action  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="fd7fd-105">參數</span><span class="sxs-lookup"><span data-stu-id="fd7fd-105">Parameters</span></span>  

 `operation`  
 <span data-ttu-id="fd7fd-106">在其中一個 [EClrOperation](eclroperation-enumeration.md) 值，表示要指定其 timeout 動作的作業。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-106">[in] One of the [EClrOperation](eclroperation-enumeration.md) values, indicating the operation for which to specify the timeout action.</span></span> <span data-ttu-id="fd7fd-107">支援下列值：</span><span class="sxs-lookup"><span data-stu-id="fd7fd-107">The following values are supported:</span></span>  
  
- <span data-ttu-id="fd7fd-108">OPR_AppDomainUnload</span><span class="sxs-lookup"><span data-stu-id="fd7fd-108">OPR_AppDomainUnload</span></span>  
  
- <span data-ttu-id="fd7fd-109">OPR_ProcessExit</span><span class="sxs-lookup"><span data-stu-id="fd7fd-109">OPR_ProcessExit</span></span>  
  
- <span data-ttu-id="fd7fd-110">OPR_ThreadRudeAbortInCriticalRegion</span><span class="sxs-lookup"><span data-stu-id="fd7fd-110">OPR_ThreadRudeAbortInCriticalRegion</span></span>  
  
- <span data-ttu-id="fd7fd-111">OPR_ThreadRudeAbortInNonCriticalRegion</span><span class="sxs-lookup"><span data-stu-id="fd7fd-111">OPR_ThreadRudeAbortInNonCriticalRegion</span></span>  
  
 `action`  
 <span data-ttu-id="fd7fd-112">在其中一個 [EPolicyAction](epolicyaction-enumeration.md) 值，表示作業超時時要採取的原則動作。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-112">[in] One of the [EPolicyAction](epolicyaction-enumeration.md) values, indicating the policy action to be taken when the operation times out.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="fd7fd-113">傳回值</span><span class="sxs-lookup"><span data-stu-id="fd7fd-113">Return Value</span></span>  
  
|<span data-ttu-id="fd7fd-114">HRESULT</span><span class="sxs-lookup"><span data-stu-id="fd7fd-114">HRESULT</span></span>|<span data-ttu-id="fd7fd-115">描述</span><span class="sxs-lookup"><span data-stu-id="fd7fd-115">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="fd7fd-116">S_OK</span><span class="sxs-lookup"><span data-stu-id="fd7fd-116">S_OK</span></span>|<span data-ttu-id="fd7fd-117">`SetActionOnTimeout` 傳回成功。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-117">`SetActionOnTimeout` returned successfully.</span></span>|  
|<span data-ttu-id="fd7fd-118">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="fd7fd-118">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="fd7fd-119">CLR 尚未載入至進程，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-119">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="fd7fd-120">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="fd7fd-120">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="fd7fd-121">呼叫已超時。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-121">The call timed out.</span></span>|  
|<span data-ttu-id="fd7fd-122">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="fd7fd-122">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="fd7fd-123">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-123">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="fd7fd-124">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="fd7fd-124">HOST_E_ABANDONED</span></span>|<span data-ttu-id="fd7fd-125">當封鎖的執行緒或光纖正在等候時，已取消事件。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-125">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="fd7fd-126">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="fd7fd-126">E_FAIL</span></span>|<span data-ttu-id="fd7fd-127">發生未知的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-127">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="fd7fd-128">在方法傳回 E_FAIL 之後，就無法在進程中使用 CLR。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-128">After a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="fd7fd-129">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-129">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="fd7fd-130">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="fd7fd-130">E_INVALIDARG</span></span>|<span data-ttu-id="fd7fd-131">無法針對指定的設定 timeout `operation` ，或為提供的值無效 `operation` 。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-131">A timeout cannot be set for the specified `operation`, or an invalid value was supplied for `operation`.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="fd7fd-132">備註</span><span class="sxs-lookup"><span data-stu-id="fd7fd-132">Remarks</span></span>  

 <span data-ttu-id="fd7fd-133">Timeout 值可以是 CLR 所設定的預設超時時間，或是 [ICLRPolicyManager：： SetTimeout](iclrpolicymanager-settimeout-method.md) 方法呼叫中主機所指定的值。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-133">The timeout value can be either the default timeout set by the CLR, or a value specified by the host in a call to the [ICLRPolicyManager::SetTimeout](iclrpolicymanager-settimeout-method.md) method.</span></span>  
  
 <span data-ttu-id="fd7fd-134">並非所有的原則動作值都可以指定為 CLR 作業的超時行為。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-134">Not all policy action values can be specified as the timeout behavior for CLR operations.</span></span> <span data-ttu-id="fd7fd-135">`SetActionOnTimeout` 通常只會用來提升行為。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-135">`SetActionOnTimeout` is typically used only to escalate behavior.</span></span> <span data-ttu-id="fd7fd-136">例如，主機可以指定使執行緒中止成為強制執行緒中止，但無法指定相反的。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-136">For example, a host can specify that thread aborts be turned into rude thread aborts, but cannot specify the opposite.</span></span> <span data-ttu-id="fd7fd-137">下表描述 `action` 有效值的有效值 `operation` 。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-137">The table below describes the valid `action` values for valid `operation` values.</span></span>  
  
|<span data-ttu-id="fd7fd-138">的值 `operation`</span><span class="sxs-lookup"><span data-stu-id="fd7fd-138">Value for `operation`</span></span>|<span data-ttu-id="fd7fd-139">的有效值 `action`</span><span class="sxs-lookup"><span data-stu-id="fd7fd-139">Valid values for `action`</span></span>|  
|---------------------------|-------------------------------|  
|<span data-ttu-id="fd7fd-140">OPR_ThreadRudeAbortInNonCriticalRegion</span><span class="sxs-lookup"><span data-stu-id="fd7fd-140">OPR_ThreadRudeAbortInNonCriticalRegion</span></span><br /><br /> <span data-ttu-id="fd7fd-141">OPR_ThreadRudeAbortInCriticalRegion</span><span class="sxs-lookup"><span data-stu-id="fd7fd-141">OPR_ThreadRudeAbortInCriticalRegion</span></span>|<span data-ttu-id="fd7fd-142">- eRudeAbortThread</span><span class="sxs-lookup"><span data-stu-id="fd7fd-142">-   eRudeAbortThread</span></span><br /><span data-ttu-id="fd7fd-143">- eUnloadAppDomain</span><span class="sxs-lookup"><span data-stu-id="fd7fd-143">-   eUnloadAppDomain</span></span><br /><span data-ttu-id="fd7fd-144">- eRudeUnloadAppDomain</span><span class="sxs-lookup"><span data-stu-id="fd7fd-144">-   eRudeUnloadAppDomain</span></span><br /><span data-ttu-id="fd7fd-145">- eExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-145">-   eExitProcess</span></span><br /><span data-ttu-id="fd7fd-146">- eFastExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-146">-   eFastExitProcess</span></span><br /><span data-ttu-id="fd7fd-147">- eRudeExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-147">-   eRudeExitProcess</span></span><br /><span data-ttu-id="fd7fd-148">- eDisableRuntime</span><span class="sxs-lookup"><span data-stu-id="fd7fd-148">-   eDisableRuntime</span></span>|  
|<span data-ttu-id="fd7fd-149">OPR_AppDomainUnload</span><span class="sxs-lookup"><span data-stu-id="fd7fd-149">OPR_AppDomainUnload</span></span>|<span data-ttu-id="fd7fd-150">- eUnloadAppDomain</span><span class="sxs-lookup"><span data-stu-id="fd7fd-150">-   eUnloadAppDomain</span></span><br /><span data-ttu-id="fd7fd-151">- eRudeUnloadAppDomain</span><span class="sxs-lookup"><span data-stu-id="fd7fd-151">-   eRudeUnloadAppDomain</span></span><br /><span data-ttu-id="fd7fd-152">- eExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-152">-   eExitProcess</span></span><br /><span data-ttu-id="fd7fd-153">- eFastExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-153">-   eFastExitProcess</span></span><br /><span data-ttu-id="fd7fd-154">- eRudeExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-154">-   eRudeExitProcess</span></span><br /><span data-ttu-id="fd7fd-155">- eDisableRuntime</span><span class="sxs-lookup"><span data-stu-id="fd7fd-155">-   eDisableRuntime</span></span>|  
|<span data-ttu-id="fd7fd-156">OPR_ProcessExit</span><span class="sxs-lookup"><span data-stu-id="fd7fd-156">OPR_ProcessExit</span></span>|<span data-ttu-id="fd7fd-157">- eExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-157">-   eExitProcess</span></span><br /><span data-ttu-id="fd7fd-158">- eFastExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-158">-   eFastExitProcess</span></span><br /><span data-ttu-id="fd7fd-159">- eRudeExitProcess</span><span class="sxs-lookup"><span data-stu-id="fd7fd-159">-   eRudeExitProcess</span></span><br /><span data-ttu-id="fd7fd-160">- eDisableRuntime</span><span class="sxs-lookup"><span data-stu-id="fd7fd-160">-   eDisableRuntime</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="fd7fd-161">需求</span><span class="sxs-lookup"><span data-stu-id="fd7fd-161">Requirements</span></span>  

 <span data-ttu-id="fd7fd-162">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="fd7fd-162">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fd7fd-163">**標頭：** Mscoree.dll</span><span class="sxs-lookup"><span data-stu-id="fd7fd-163">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="fd7fd-164">連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="fd7fd-164">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="fd7fd-165">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="fd7fd-165">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fd7fd-166">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fd7fd-166">See also</span></span>

- [<span data-ttu-id="fd7fd-167">EClrOperation 列舉</span><span class="sxs-lookup"><span data-stu-id="fd7fd-167">EClrOperation Enumeration</span></span>](eclroperation-enumeration.md)
- [<span data-ttu-id="fd7fd-168">EPolicyAction 列舉</span><span class="sxs-lookup"><span data-stu-id="fd7fd-168">EPolicyAction Enumeration</span></span>](epolicyaction-enumeration.md)
- [<span data-ttu-id="fd7fd-169">ICLRControl 介面</span><span class="sxs-lookup"><span data-stu-id="fd7fd-169">ICLRControl Interface</span></span>](iclrcontrol-interface.md)
- [<span data-ttu-id="fd7fd-170">ICLRPolicyManager 介面</span><span class="sxs-lookup"><span data-stu-id="fd7fd-170">ICLRPolicyManager Interface</span></span>](iclrpolicymanager-interface.md)
