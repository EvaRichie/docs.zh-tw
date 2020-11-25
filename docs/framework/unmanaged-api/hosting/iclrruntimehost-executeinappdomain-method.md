---
title: ICLRRuntimeHost::ExecuteInAppDomain 方法
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.ExecuteInAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::ExecuteInAppDomain
helpviewer_keywords:
- ICLRRuntimeHost::ExecuteInAppDomain method [.NET Framework hosting]
- ExecuteInAppDomain method [.NET Framework hosting]
ms.assetid: e2b0e2db-3fae-4b56-844e-d30a125a660c
topic_type:
- apiref
ms.openlocfilehash: 4c28c4a5cc64b20c9ac9c57e1aef5e7b90a20e01
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728884"
---
# <a name="iclrruntimehostexecuteinappdomain-method"></a><span data-ttu-id="e3e08-102">ICLRRuntimeHost::ExecuteInAppDomain 方法</span><span class="sxs-lookup"><span data-stu-id="e3e08-102">ICLRRuntimeHost::ExecuteInAppDomain Method</span></span>

<span data-ttu-id="e3e08-103">指定 <xref:System.AppDomain> 要在其中執行指定 managed 程式碼的。</span><span class="sxs-lookup"><span data-stu-id="e3e08-103">Specifies the <xref:System.AppDomain> in which to execute the specified managed code.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e3e08-104">語法</span><span class="sxs-lookup"><span data-stu-id="e3e08-104">Syntax</span></span>  
  
```cpp  
HRESULT ExecuteInAppDomain(  
    [in] DWORD AppDomainId,
    [in] FExecuteInDomainCallback pCallback,
    [in] void* cookie  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e3e08-105">參數</span><span class="sxs-lookup"><span data-stu-id="e3e08-105">Parameters</span></span>  

 `AppDomainId`  
 <span data-ttu-id="e3e08-106">在 <xref:System.AppDomain> 要在其中執行指定方法的數位識別碼。</span><span class="sxs-lookup"><span data-stu-id="e3e08-106">[in] The numeric ID of the <xref:System.AppDomain> in which to execute the specified method.</span></span>  
  
 `pCallback`  
 <span data-ttu-id="e3e08-107">在要在指定的內執行之函式的指標 <xref:System.AppDomain> 。</span><span class="sxs-lookup"><span data-stu-id="e3e08-107">[in] A pointer to the function to execute within the specified <xref:System.AppDomain>.</span></span>  
  
 `cookie`  
 <span data-ttu-id="e3e08-108">在不透明呼叫端配置記憶體的指標。</span><span class="sxs-lookup"><span data-stu-id="e3e08-108">[in] A pointer to opaque caller-allocated memory.</span></span> <span data-ttu-id="e3e08-109">這個參數是由 common language runtime (CLR) 傳遞至網域回呼。</span><span class="sxs-lookup"><span data-stu-id="e3e08-109">This parameter is passed by the common language runtime (CLR) to the domain callback.</span></span> <span data-ttu-id="e3e08-110">它不是運行時間管理的堆積記憶體;這個記憶體的配置和存留期都是由呼叫端控制。</span><span class="sxs-lookup"><span data-stu-id="e3e08-110">It is not runtime-managed heap memory; both the allocation and lifetime of this memory are controlled by the caller.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="e3e08-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="e3e08-111">Return Value</span></span>  
  
|<span data-ttu-id="e3e08-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="e3e08-112">HRESULT</span></span>|<span data-ttu-id="e3e08-113">描述</span><span class="sxs-lookup"><span data-stu-id="e3e08-113">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="e3e08-114">S_OK</span><span class="sxs-lookup"><span data-stu-id="e3e08-114">S_OK</span></span>|<span data-ttu-id="e3e08-115">`ExecuteInAppDomain` 傳回成功。</span><span class="sxs-lookup"><span data-stu-id="e3e08-115">`ExecuteInAppDomain` returned successfully.</span></span>|  
|<span data-ttu-id="e3e08-116">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="e3e08-116">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="e3e08-117">CLR 尚未載入至進程，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="e3e08-117">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="e3e08-118">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="e3e08-118">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="e3e08-119">呼叫已超時。</span><span class="sxs-lookup"><span data-stu-id="e3e08-119">The call timed out.</span></span>|  
|<span data-ttu-id="e3e08-120">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="e3e08-120">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="e3e08-121">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="e3e08-121">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="e3e08-122">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="e3e08-122">HOST_E_ABANDONED</span></span>|<span data-ttu-id="e3e08-123">當封鎖的執行緒或光纖正在等候時，已取消事件。</span><span class="sxs-lookup"><span data-stu-id="e3e08-123">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="e3e08-124">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="e3e08-124">E_FAIL</span></span>|<span data-ttu-id="e3e08-125">發生未知的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="e3e08-125">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="e3e08-126">如果方法傳回 E_FAIL，則 CLR 在進程內將無法再使用。</span><span class="sxs-lookup"><span data-stu-id="e3e08-126">If a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="e3e08-127">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="e3e08-127">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e3e08-128">備註</span><span class="sxs-lookup"><span data-stu-id="e3e08-128">Remarks</span></span>  

 <span data-ttu-id="e3e08-129">`ExecuteInAppDomain` 允許主控制項對要在其中執行 managed <xref:System.AppDomain> 指定 managed 方法的控制進行練習。</span><span class="sxs-lookup"><span data-stu-id="e3e08-129">`ExecuteInAppDomain` allows the host to exercise control over which managed <xref:System.AppDomain> the specified managed method should be executed in.</span></span> <span data-ttu-id="e3e08-130">您可以藉 <xref:System.AppDomain.Id%2A> 由呼叫 [GetCurrentAppDomainId 方法](iclrruntimehost-getcurrentappdomainid-method.md)，取得應用程式域識別碼的值，其對應至屬性的值。</span><span class="sxs-lookup"><span data-stu-id="e3e08-130">You can get the value of an application domain's identifier, which corresponds to the value of the <xref:System.AppDomain.Id%2A> property, by calling [GetCurrentAppDomainId Method](iclrruntimehost-getcurrentappdomainid-method.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e3e08-131">需求</span><span class="sxs-lookup"><span data-stu-id="e3e08-131">Requirements</span></span>  

 <span data-ttu-id="e3e08-132">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e3e08-132">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e3e08-133">**標頭：** Mscoree.dll</span><span class="sxs-lookup"><span data-stu-id="e3e08-133">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="e3e08-134">連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="e3e08-134">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="e3e08-135">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e3e08-135">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e3e08-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e3e08-136">See also</span></span>

- [<span data-ttu-id="e3e08-137">ICLRRuntimeHost 介面</span><span class="sxs-lookup"><span data-stu-id="e3e08-137">ICLRRuntimeHost Interface</span></span>](iclrruntimehost-interface.md)
