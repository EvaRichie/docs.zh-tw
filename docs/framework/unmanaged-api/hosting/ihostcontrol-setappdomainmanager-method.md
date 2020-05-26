---
title: IHostControl::SetAppDomainManager 方法
ms.date: 03/30/2017
api_name:
- IHostControl.SetAppDomainManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostControl::SetAppDomainManager
helpviewer_keywords:
- IHostControl::SetAppDomainManager method [.NET Framework hosting]
- SetAppDomainManager method [.NET Framework hosting]
ms.assetid: 6562bbe7-0d67-4c50-a958-3a18cf680375
topic_type:
- apiref
ms.openlocfilehash: 74ffc5c92402808ae566d7cb014d9d920c384ae8
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804941"
---
# <a name="ihostcontrolsetappdomainmanager-method"></a><span data-ttu-id="af33b-102">IHostControl::SetAppDomainManager 方法</span><span class="sxs-lookup"><span data-stu-id="af33b-102">IHostControl::SetAppDomainManager Method</span></span>
<span data-ttu-id="af33b-103">通知主機已建立應用程式域。</span><span class="sxs-lookup"><span data-stu-id="af33b-103">Notifies the host that an application domain has been created.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="af33b-104">語法</span><span class="sxs-lookup"><span data-stu-id="af33b-104">Syntax</span></span>  
  
```cpp  
HRESULT SetAppDomainManager (  
    [in] DWORD     dwAppDomainID,  
    [in] IUnknown* pUnkAppDomainManager  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="af33b-105">參數</span><span class="sxs-lookup"><span data-stu-id="af33b-105">Parameters</span></span>  
 `dwAppDomainID`  
 <span data-ttu-id="af33b-106">在所選取的的數值識別碼 <xref:System.AppDomain> 。</span><span class="sxs-lookup"><span data-stu-id="af33b-106">[in] The numeric identifier of the selected <xref:System.AppDomain>.</span></span>  
  
 `pUnkAppDomainManager`  
 <span data-ttu-id="af33b-107">在主機實作為之 <xref:System.AppDomainManager> 物件的指標 `IUnknown` 。</span><span class="sxs-lookup"><span data-stu-id="af33b-107">[in] A pointer to the <xref:System.AppDomainManager> object that the host implements as `IUnknown`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="af33b-108">傳回值</span><span class="sxs-lookup"><span data-stu-id="af33b-108">Return Value</span></span>  
  
|<span data-ttu-id="af33b-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="af33b-109">HRESULT</span></span>|<span data-ttu-id="af33b-110">描述</span><span class="sxs-lookup"><span data-stu-id="af33b-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="af33b-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="af33b-111">S_OK</span></span>|<span data-ttu-id="af33b-112">`SetAppDomainManager`已成功傳回。</span><span class="sxs-lookup"><span data-stu-id="af33b-112">`SetAppDomainManager` returned successfully.</span></span>|  
|<span data-ttu-id="af33b-113">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="af33b-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="af33b-114">Common language runtime （CLR）尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="af33b-114">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="af33b-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="af33b-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="af33b-116">呼叫超時。</span><span class="sxs-lookup"><span data-stu-id="af33b-116">The call timed out.</span></span>|  
|<span data-ttu-id="af33b-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="af33b-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="af33b-118">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="af33b-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="af33b-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="af33b-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="af33b-120">已封鎖的執行緒或光纖在等候時取消了事件。</span><span class="sxs-lookup"><span data-stu-id="af33b-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="af33b-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="af33b-121">E_FAIL</span></span>|<span data-ttu-id="af33b-122">發生不明的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="af33b-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="af33b-123">當方法傳回 E_FAIL 時，CLR 就無法在進程內使用。</span><span class="sxs-lookup"><span data-stu-id="af33b-123">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="af33b-124">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="af33b-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="af33b-125">備註</span><span class="sxs-lookup"><span data-stu-id="af33b-125">Remarks</span></span>  
 <span data-ttu-id="af33b-126">為 <xref:System.AppDomainManager> 主機提供了一種機制，可讓您在 managed 程式碼中啟動，並控制每一個的建立和設定 <xref:System.AppDomain> 。</span><span class="sxs-lookup"><span data-stu-id="af33b-126">The <xref:System.AppDomainManager> provides the host with a mechanism to bootstrap into managed code and to control the creation and settings of each <xref:System.AppDomain>.</span></span> <span data-ttu-id="af33b-127"><xref:System.AppDomainManager>建立時，會載入每個 <xref:System.AppDomain> <xref:System.AppDomain> 。</span><span class="sxs-lookup"><span data-stu-id="af33b-127">The <xref:System.AppDomainManager> is loaded into each <xref:System.AppDomain> when that <xref:System.AppDomain> is created.</span></span> <span data-ttu-id="af33b-128">如果選擇，CLR 會藉由設定參數的值，通知主機已建立應用程式域 `pUnkAppDomainManager` 。</span><span class="sxs-lookup"><span data-stu-id="af33b-128">If it chooses, the CLR notifies the host that the application domain has been created by setting the value of the `pUnkAppDomainManager` parameter.</span></span>  
  
 <span data-ttu-id="af33b-129">在它的方法執行中 `SetAppDomainManager` ，主機可以設定應用程式域管理員的元件名稱和類型。</span><span class="sxs-lookup"><span data-stu-id="af33b-129">In its implementation of the `SetAppDomainManager` method, the host can set the assembly name and type for the application domain manager.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="af33b-130">規格需求</span><span class="sxs-lookup"><span data-stu-id="af33b-130">Requirements</span></span>  
 <span data-ttu-id="af33b-131">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="af33b-131">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="af33b-132">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="af33b-132">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="af33b-133">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="af33b-133">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="af33b-134">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="af33b-134">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="af33b-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="af33b-135">See also</span></span>

- <xref:System.AppDomain>
- <xref:System.AppDomainManager>
- [<span data-ttu-id="af33b-136">IHostControl 介面</span><span class="sxs-lookup"><span data-stu-id="af33b-136">IHostControl Interface</span></span>](ihostcontrol-interface.md)
