---
title: ICLRRuntimeHost::GetCurrentAppDomainId 方法
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.GetCurrentAppDomainId
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::GetCurrentAppDomainId
helpviewer_keywords:
- ICLRRuntimeHost::GetCurrentAppDomainId method [.NET Framework hosting]
- GetCurrentAppDomainId method [.NET Framework hosting]
ms.assetid: 33800475-7815-4976-8aca-a1038761a2ef
topic_type:
- apiref
ms.openlocfilehash: 1c667b19ac4bfa0bea95b85cf099906e351e5b71
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703677"
---
# <a name="iclrruntimehostgetcurrentappdomainid-method"></a><span data-ttu-id="5b491-102">ICLRRuntimeHost::GetCurrentAppDomainId 方法</span><span class="sxs-lookup"><span data-stu-id="5b491-102">ICLRRuntimeHost::GetCurrentAppDomainId Method</span></span>
<span data-ttu-id="5b491-103">取得目前正在執行之的數值識別碼 <xref:System.AppDomain> 。</span><span class="sxs-lookup"><span data-stu-id="5b491-103">Gets the numeric identifier of the <xref:System.AppDomain> that is currently executing.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5b491-104">語法</span><span class="sxs-lookup"><span data-stu-id="5b491-104">Syntax</span></span>  
  
```cpp  
HRESULT GetCurrentAppDomainId(  
    [out] DWORD* pdwAppDomainId  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5b491-105">參數</span><span class="sxs-lookup"><span data-stu-id="5b491-105">Parameters</span></span>  
 `pdwAppDomainId`  
 <span data-ttu-id="5b491-106">脫銷目前正在執行之的數值識別碼 <xref:System.AppDomain> 。</span><span class="sxs-lookup"><span data-stu-id="5b491-106">[out] The numeric identifier of the <xref:System.AppDomain> that is currently executing.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="5b491-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="5b491-107">Return Value</span></span>  
  
|<span data-ttu-id="5b491-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="5b491-108">HRESULT</span></span>|<span data-ttu-id="5b491-109">說明</span><span class="sxs-lookup"><span data-stu-id="5b491-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="5b491-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="5b491-110">S_OK</span></span>|<span data-ttu-id="5b491-111">`GetCurrentAppDomainId`已成功傳回。</span><span class="sxs-lookup"><span data-stu-id="5b491-111">`GetCurrentAppDomainId` returned successfully.</span></span>|  
|<span data-ttu-id="5b491-112">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="5b491-112">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="5b491-113">Common language runtime （CLR）尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="5b491-113">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="5b491-114">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="5b491-114">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="5b491-115">呼叫超時。</span><span class="sxs-lookup"><span data-stu-id="5b491-115">The call timed out.</span></span>|  
|<span data-ttu-id="5b491-116">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="5b491-116">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="5b491-117">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="5b491-117">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="5b491-118">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="5b491-118">HOST_E_ABANDONED</span></span>|<span data-ttu-id="5b491-119">已封鎖的執行緒或光纖在等候時取消了事件。</span><span class="sxs-lookup"><span data-stu-id="5b491-119">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="5b491-120">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="5b491-120">E_FAIL</span></span>|<span data-ttu-id="5b491-121">發生不明的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="5b491-121">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="5b491-122">如果方法傳回 E_FAIL，就無法在進程內使用 CLR。</span><span class="sxs-lookup"><span data-stu-id="5b491-122">If a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="5b491-123">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="5b491-123">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="5b491-124">備註</span><span class="sxs-lookup"><span data-stu-id="5b491-124">Remarks</span></span>  
 <span data-ttu-id="5b491-125">`pdwAppDomainId`參數會設定為 <xref:System.AppDomain.Id%2A> <xref:System.AppDomain> 目前線程正在其中執行之的屬性值。</span><span class="sxs-lookup"><span data-stu-id="5b491-125">The `pdwAppDomainId` parameter is set to the value of the <xref:System.AppDomain.Id%2A> property of the <xref:System.AppDomain> in which the current thread is executing.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5b491-126">需求</span><span class="sxs-lookup"><span data-stu-id="5b491-126">Requirements</span></span>  
 <span data-ttu-id="5b491-127">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="5b491-127">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5b491-128">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="5b491-128">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="5b491-129">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="5b491-129">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="5b491-130">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="5b491-130">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5b491-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5b491-131">See also</span></span>

- <xref:System.AppDomain>
- <xref:System.AppDomainManager>
- [<span data-ttu-id="5b491-132">ICLRRuntimeHost 介面</span><span class="sxs-lookup"><span data-stu-id="5b491-132">ICLRRuntimeHost Interface</span></span>](iclrruntimehost-interface.md)
