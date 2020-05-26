---
title: IGCHost::GetStats 方法
ms.date: 03/30/2017
api_name:
- IGCHost.GetStats
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- GetStats
helpviewer_keywords:
- GetStats method, IGCHost interface [.NET Framework hosting]
- IGCHost::GetStats method [.NET Framework hosting]
ms.assetid: c4ae022c-46ac-4f19-9ddd-09b955f19412
topic_type:
- apiref
ms.openlocfilehash: 67668aa7ff9faf035a047e485a8a3c8a451f45b9
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2020
ms.locfileid: "83805242"
---
# <a name="igchostgetstats-method"></a><span data-ttu-id="2bf44-102">IGCHost::GetStats 方法</span><span class="sxs-lookup"><span data-stu-id="2bf44-102">IGCHost::GetStats Method</span></span>
<span data-ttu-id="2bf44-103">取得垃圾收集系統目前狀態的統計資料。</span><span class="sxs-lookup"><span data-stu-id="2bf44-103">Gets the statistics for the current state of the garbage collection system.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2bf44-104">語法</span><span class="sxs-lookup"><span data-stu-id="2bf44-104">Syntax</span></span>  
  
```cpp  
HRESULT GetStats (  
    [in, out] COR_GC_STATS *pStats  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2bf44-105">參數</span><span class="sxs-lookup"><span data-stu-id="2bf44-105">Parameters</span></span>  
 `pStats`  
 <span data-ttu-id="2bf44-106">[in、out][COR_GC_STATS](cor-gc-stats-structure.md)結構的指標，其中包含垃圾收集系統目前狀態的統計資料。</span><span class="sxs-lookup"><span data-stu-id="2bf44-106">[in, out] A pointer to a [COR_GC_STATS](cor-gc-stats-structure.md) structure that contains the statistics for the current state of the garbage collection system.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2bf44-107">備註</span><span class="sxs-lookup"><span data-stu-id="2bf44-107">Remarks</span></span>  
 <span data-ttu-id="2bf44-108">智慧配置系統可以使用統計資料來協助垃圾收集系統運作。</span><span class="sxs-lookup"><span data-stu-id="2bf44-108">The statistics can be used by a smart allocation system to help the garbage collection system operate.</span></span> <span data-ttu-id="2bf44-109">例如，配置系統可能會決定在檢查統計資料之後，它需要新增更多記憶體或強制集合。</span><span class="sxs-lookup"><span data-stu-id="2bf44-109">For example, the allocation system may determine, after reviewing the statistics, that it needs to add more memory or force a collection.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2bf44-110">規格需求</span><span class="sxs-lookup"><span data-stu-id="2bf44-110">Requirements</span></span>  
 <span data-ttu-id="2bf44-111">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2bf44-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2bf44-112">**標頭：** GCHost .idl，GCHost。h</span><span class="sxs-lookup"><span data-stu-id="2bf44-112">**Header:** GCHost.idl, GCHost.h</span></span>  
  
 <span data-ttu-id="2bf44-113">連結**庫：** 包含為 Mscoree.dll 中的資源</span><span class="sxs-lookup"><span data-stu-id="2bf44-113">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="2bf44-114">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2bf44-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2bf44-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2bf44-115">See also</span></span>

- [<span data-ttu-id="2bf44-116">IGCHost 介面</span><span class="sxs-lookup"><span data-stu-id="2bf44-116">IGCHost Interface</span></span>](igchost-interface.md)
