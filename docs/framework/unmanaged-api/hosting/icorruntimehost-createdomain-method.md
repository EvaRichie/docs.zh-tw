---
title: ICorRuntimeHost::CreateDomain 方法
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost.CreateDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost::CreateDomain
helpviewer_keywords:
- CreateDomain method [.NET Framework hosting]
- ICorRuntimeHost::CreateDomain method [.NET Framework hosting]
ms.assetid: b96c5ef3-a9df-4c7c-9952-432d3272cb5c
topic_type:
- apiref
ms.openlocfilehash: 74f17c77e74edb1226dda2d9ebaa9486e1769ce4
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762353"
---
# <a name="icorruntimehostcreatedomain-method"></a><span data-ttu-id="87e65-102">ICorRuntimeHost::CreateDomain 方法</span><span class="sxs-lookup"><span data-stu-id="87e65-102">ICorRuntimeHost::CreateDomain Method</span></span>
<span data-ttu-id="87e65-103">建立應用程式域。</span><span class="sxs-lookup"><span data-stu-id="87e65-103">Creates an application domain.</span></span> <span data-ttu-id="87e65-104">呼叫端會接收類型的介面指標 <xref:System._AppDomain> ，類型為的實例 <xref:System.AppDomain?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="87e65-104">The caller receives an interface pointer of type <xref:System._AppDomain> to an instance of type <xref:System.AppDomain?displayProperty=nameWithType>.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="87e65-105">語法</span><span class="sxs-lookup"><span data-stu-id="87e65-105">Syntax</span></span>  
  
```cpp  
HRESULT CreateDomain (  
    [in] LPWSTR    pwzFriendlyName,  
    [in] IUnknown* pIdentityArray,  
    [out] void   **pAppDomain  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="87e65-106">參數</span><span class="sxs-lookup"><span data-stu-id="87e65-106">Parameters</span></span>  
 `pwzFriendlyName`  
 <span data-ttu-id="87e65-107">在選擇性參數，用來為定義域提供易記名稱。</span><span class="sxs-lookup"><span data-stu-id="87e65-107">[in] An optional parameter used to give a friendly name to the domain.</span></span> <span data-ttu-id="87e65-108">這個易記名稱可以在使用者介面（例如偵錯工具）中顯示，以識別網域。</span><span class="sxs-lookup"><span data-stu-id="87e65-108">This friendly name can be displayed in user interfaces such as debuggers to identify the domain.</span></span>  
  
 `pIdentityArray`  
 <span data-ttu-id="87e65-109">在指向實例的選擇性陣列， `IIdentity` 表示透過安全性原則對應的辨識項，以建立許可權集合。</span><span class="sxs-lookup"><span data-stu-id="87e65-109">[in] An optional array of pointers to `IIdentity` instances that represent evidence mapped through security policy to establish a  permission set.</span></span> <span data-ttu-id="87e65-110">您 `IIdentity` 可以藉由呼叫[CreateEvidence](icorruntimehost-createevidence-method.md)方法來取得物件。</span><span class="sxs-lookup"><span data-stu-id="87e65-110">An `IIdentity` object can be obtained by calling the [CreateEvidence](icorruntimehost-createevidence-method.md) method.</span></span>  
  
 `pAppDomain`  
 <span data-ttu-id="87e65-111">脫銷實例之類型的介面指標， <xref:System._AppDomain> <xref:System.AppDomain?displayProperty=nameWithType> 可用於進一步控制定義域。</span><span class="sxs-lookup"><span data-stu-id="87e65-111">[out] An interface pointer of type <xref:System._AppDomain> to an instance of <xref:System.AppDomain?displayProperty=nameWithType> that can be used to further control the domain.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="87e65-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="87e65-112">Return Value</span></span>  
  
|<span data-ttu-id="87e65-113">HRESULT</span><span class="sxs-lookup"><span data-stu-id="87e65-113">HRESULT</span></span>|<span data-ttu-id="87e65-114">Description</span><span class="sxs-lookup"><span data-stu-id="87e65-114">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="87e65-115">S_OK</span><span class="sxs-lookup"><span data-stu-id="87e65-115">S_OK</span></span>|<span data-ttu-id="87e65-116">作業成功。</span><span class="sxs-lookup"><span data-stu-id="87e65-116">The operation was successful.</span></span>|  
|<span data-ttu-id="87e65-117">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="87e65-117">S_FALSE</span></span>|<span data-ttu-id="87e65-118">作業無法完成。</span><span class="sxs-lookup"><span data-stu-id="87e65-118">The operation failed to complete.</span></span>|  
|<span data-ttu-id="87e65-119">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="87e65-119">E_FAIL</span></span>|<span data-ttu-id="87e65-120">發生未知的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="87e65-120">An unknown, catastrophic failure occurred.</span></span> <span data-ttu-id="87e65-121">如果方法傳回 E_FAIL，則 common language runtime （CLR）就無法在進程中使用。</span><span class="sxs-lookup"><span data-stu-id="87e65-121">If a method returns E_FAIL, the common language runtime (CLR) is no longer usable in the process.</span></span> <span data-ttu-id="87e65-122">後續對任何裝載 Api 的呼叫都會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="87e65-122">Subsequent calls to any hosting APIs return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="87e65-123">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="87e65-123">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="87e65-124">CLR 尚未載入進程中，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="87e65-124">The CLR has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="87e65-125">規格需求</span><span class="sxs-lookup"><span data-stu-id="87e65-125">Requirements</span></span>  
 <span data-ttu-id="87e65-126">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="87e65-126">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="87e65-127">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="87e65-127">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="87e65-128">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="87e65-128">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="87e65-129">**.NET Framework 版本：** 1.0、1。1</span><span class="sxs-lookup"><span data-stu-id="87e65-129">**.NET Framework Versions:** 1.0, 1.1</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="87e65-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="87e65-130">See also</span></span>

- <xref:System._AppDomain>
- <xref:System.AppDomain>
- [<span data-ttu-id="87e65-131">ICorRuntimeHost 介面</span><span class="sxs-lookup"><span data-stu-id="87e65-131">ICorRuntimeHost Interface</span></span>](icorruntimehost-interface.md)
