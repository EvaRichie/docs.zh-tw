---
title: ICLRAssemblyIdentityManager::IsStronglyNamed 方法
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.IsStronglyNamed
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::IsStronglyNamed
helpviewer_keywords:
- IsStronglyNamed method [.NET Framework hosting]
- ICLRAssemblyIdentityManager::IsStronglyNamed method [.NET Framework hosting]
ms.assetid: 954bd386-2076-4d00-9d46-38c728aa9cab
topic_type:
- apiref
ms.openlocfilehash: 9ac3b2ae349a696ba0cea1bad3e3484bb1c113fa
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95679237"
---
# <a name="iclrassemblyidentitymanagerisstronglynamed-method"></a><span data-ttu-id="e1345-102">ICLRAssemblyIdentityManager::IsStronglyNamed 方法</span><span class="sxs-lookup"><span data-stu-id="e1345-102">ICLRAssemblyIdentityManager::IsStronglyNamed Method</span></span>

<span data-ttu-id="e1345-103">取得值，這個值會指出指定的元件是否為強式名稱。</span><span class="sxs-lookup"><span data-stu-id="e1345-103">Gets a value that indicates whether the specified assembly is strongly named.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e1345-104">語法</span><span class="sxs-lookup"><span data-stu-id="e1345-104">Syntax</span></span>  
  
```cpp  
RESULT IsStronglyNamed (  
    [in]  LPCWSTR  pwzAssemblyIdentity,  
    [out] BOOL    *pbIsStronglyNamed  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e1345-105">參數</span><span class="sxs-lookup"><span data-stu-id="e1345-105">Parameters</span></span>  

 `pwzAssemblyIdentity`  
 <span data-ttu-id="e1345-106">在要評估之元件的不透明標準元件身分識別資料。</span><span class="sxs-lookup"><span data-stu-id="e1345-106">[in] The opaque canonical assembly identity data of the assembly to be evaluated.</span></span>  
  
 `pbIsStronglyNamed`  
 <span data-ttu-id="e1345-107">[out] `true` ，如果參數所參考的元件 `pwzAssemblyIdentity` 是強式名稱，則為，否則為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="e1345-107">[out] `true`, if the assembly referenced by the `pwzAssemblyIdentity` parameter is strongly named; otherwise, `false`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="e1345-108">傳回值</span><span class="sxs-lookup"><span data-stu-id="e1345-108">Return Value</span></span>  
  
|<span data-ttu-id="e1345-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="e1345-109">HRESULT</span></span>|<span data-ttu-id="e1345-110">描述</span><span class="sxs-lookup"><span data-stu-id="e1345-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="e1345-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="e1345-111">S_OK</span></span>|<span data-ttu-id="e1345-112">此方法已成功傳回。</span><span class="sxs-lookup"><span data-stu-id="e1345-112">The method returned successfully.</span></span>|  
|<span data-ttu-id="e1345-113">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="e1345-113">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="e1345-114">Common language runtime (CLR) 尚未載入至進程，或 CLR 處於無法執行 managed 程式碼或成功處理呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="e1345-114">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="e1345-115">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="e1345-115">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="e1345-116">呼叫已超時。</span><span class="sxs-lookup"><span data-stu-id="e1345-116">The call timed out.</span></span>|  
|<span data-ttu-id="e1345-117">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="e1345-117">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="e1345-118">呼叫端沒有擁有鎖定。</span><span class="sxs-lookup"><span data-stu-id="e1345-118">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="e1345-119">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="e1345-119">HOST_E_ABANDONED</span></span>|<span data-ttu-id="e1345-120">當封鎖的執行緒或光纖正在等候時，已取消事件。</span><span class="sxs-lookup"><span data-stu-id="e1345-120">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="e1345-121">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="e1345-121">E_FAIL</span></span>|<span data-ttu-id="e1345-122">發生未知的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="e1345-122">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="e1345-123">如果方法傳回 E_FAIL，則 CLR 在進程內將無法再使用。</span><span class="sxs-lookup"><span data-stu-id="e1345-123">If a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="e1345-124">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="e1345-124">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="e1345-125">需求</span><span class="sxs-lookup"><span data-stu-id="e1345-125">Requirements</span></span>  

 <span data-ttu-id="e1345-126">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="e1345-126">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e1345-127">**標頭：** Mscoree.dll</span><span class="sxs-lookup"><span data-stu-id="e1345-127">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="e1345-128">連結 **庫：** 以資源的形式包含在 MSCorEE.dll 中</span><span class="sxs-lookup"><span data-stu-id="e1345-128">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="e1345-129">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e1345-129">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e1345-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e1345-130">See also</span></span>

- [<span data-ttu-id="e1345-131">ICLRAssemblyIdentityManager 介面</span><span class="sxs-lookup"><span data-stu-id="e1345-131">ICLRAssemblyIdentityManager Interface</span></span>](iclrassemblyidentitymanager-interface.md)
