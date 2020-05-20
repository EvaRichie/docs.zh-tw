---
title: ICLRAssemblyReferenceList::IsStringAssemblyReferenceInList 方法
ms.date: 03/30/2017
api_name:
- ICLRAssemblyReferenceList.IsStringAssemblyReferenceInList
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyReferenceList::IsStringAssemblyReferenceInList
helpviewer_keywords:
- ICLRAssemblyReferenceList::IsStringAssemblyReferenceInList method [.NET Framework hosting]
- IsStringAssemblyReferenceInList method [.NET Framework hosting]
ms.assetid: e6121cc3-2f11-42c7-bdae-47808581ff71
topic_type:
- apiref
ms.openlocfilehash: 91f174cab4986882df795eb531baedfc0dd43962
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615861"
---
# <a name="iclrassemblyreferencelistisstringassemblyreferenceinlist-method"></a><span data-ttu-id="db615-102">ICLRAssemblyReferenceList::IsStringAssemblyReferenceInList 方法</span><span class="sxs-lookup"><span data-stu-id="db615-102">ICLRAssemblyReferenceList::IsStringAssemblyReferenceInList Method</span></span>
<span data-ttu-id="db615-103">取得值，指出提供的名稱是否符合清單中元件的名稱。</span><span class="sxs-lookup"><span data-stu-id="db615-103">Gets a value that indicates whether the supplied name matches the name of an assembly in the list.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="db615-104">語法</span><span class="sxs-lookup"><span data-stu-id="db615-104">Syntax</span></span>  
  
```cpp  
HRESULT IsStringAssemblyReferenceInList (  
    [in] LPCWSTR pwzAssemblyName  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="db615-105">參數</span><span class="sxs-lookup"><span data-stu-id="db615-105">Parameters</span></span>  
 `pwzAssemblyName`  
 <span data-ttu-id="db615-106">在要搜尋之元件的名稱。</span><span class="sxs-lookup"><span data-stu-id="db615-106">[in] The name of the assembly for which to search.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="db615-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="db615-107">Return Value</span></span>  
  
|<span data-ttu-id="db615-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="db615-108">HRESULT</span></span>|<span data-ttu-id="db615-109">說明</span><span class="sxs-lookup"><span data-stu-id="db615-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="db615-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="db615-110">S_OK</span></span>|<span data-ttu-id="db615-111">此字串會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="db615-111">The string appears in the list.</span></span>|  
|<span data-ttu-id="db615-112">S_FALSE</span><span class="sxs-lookup"><span data-stu-id="db615-112">S_FALSE</span></span>|<span data-ttu-id="db615-113">此字串不會出現在清單中。</span><span class="sxs-lookup"><span data-stu-id="db615-113">The string does not appear in the list.</span></span>|  
|<span data-ttu-id="db615-114">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="db615-114">E_FAIL</span></span>|<span data-ttu-id="db615-115">發生不明的嚴重失敗。</span><span class="sxs-lookup"><span data-stu-id="db615-115">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="db615-116">在方法傳回 E_FAIL 之後，通用語言執行時間就無法在進程內使用。</span><span class="sxs-lookup"><span data-stu-id="db615-116">After a method returns E_FAIL, the common language runtime is no longer usable within the process.</span></span> <span data-ttu-id="db615-117">對裝載方法的後續呼叫會傳回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="db615-117">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="db615-118">需求</span><span class="sxs-lookup"><span data-stu-id="db615-118">Requirements</span></span>  
 <span data-ttu-id="db615-119">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="db615-119">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="db615-120">**標頭：** Mscoree.dll. h</span><span class="sxs-lookup"><span data-stu-id="db615-120">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="db615-121">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="db615-121">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="db615-122">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="db615-122">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="db615-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="db615-123">See also</span></span>

- [<span data-ttu-id="db615-124">ICLRAssemblyIdentityManager 介面</span><span class="sxs-lookup"><span data-stu-id="db615-124">ICLRAssemblyIdentityManager Interface</span></span>](iclrassemblyidentitymanager-interface.md)
- [<span data-ttu-id="db615-125">ICLRAssemblyReferenceList 介面</span><span class="sxs-lookup"><span data-stu-id="db615-125">ICLRAssemblyReferenceList Interface</span></span>](iclrassemblyreferencelist-interface.md)
- [<span data-ttu-id="db615-126">IHostAssemblyManager 介面</span><span class="sxs-lookup"><span data-stu-id="db615-126">IHostAssemblyManager Interface</span></span>](ihostassemblymanager-interface.md)
- [<span data-ttu-id="db615-127">IHostAssemblyStore 介面</span><span class="sxs-lookup"><span data-stu-id="db615-127">IHostAssemblyStore Interface</span></span>](ihostassemblystore-interface.md)
