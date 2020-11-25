---
title: COR_GC_STAT_TYPES 列舉
ms.date: 03/30/2017
api_name:
- COR_GC_STAT_TYPES
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_STAT_TYPES
helpviewer_keywords:
- COR_GC_STAT_TYPES enumeration [.NET Framework hosting]
ms.assetid: fc51d6db-f7f8-408b-b93d-c166fc712c99
topic_type:
- apiref
ms.openlocfilehash: c14e27b67fc600e2684f8c967af30bb9a5cee126
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716734"
---
# <a name="cor_gc_stat_types-enumeration"></a><span data-ttu-id="fad62-102">COR_GC_STAT_TYPES 列舉</span><span class="sxs-lookup"><span data-stu-id="fad62-102">COR_GC_STAT_TYPES Enumeration</span></span>

<span data-ttu-id="fad62-103">指定要記錄的垃圾收集統計資料。</span><span class="sxs-lookup"><span data-stu-id="fad62-103">Specifies the statistics to be recorded for a garbage collection.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="fad62-104">語法</span><span class="sxs-lookup"><span data-stu-id="fad62-104">Syntax</span></span>  
  
```cpp  
typedef enum {  
    COR_GC_COUNTS                 = 0x00000001  
    COR_GC_MEMORYUSAGE            = 0x00000002  
} COR_GC_STAT_TYPES;  
```  
  
## <a name="remarks"></a><span data-ttu-id="fad62-105">備註</span><span class="sxs-lookup"><span data-stu-id="fad62-105">Remarks</span></span>  

 <span data-ttu-id="fad62-106">此列舉會指定[ICLRGCManager：： GetStats](iclrgcmanager-getstats-method.md)方法要設定[COR_GC_STATS](cor-gc-stats-structure.md)結構中的統計資料。</span><span class="sxs-lookup"><span data-stu-id="fad62-106">This enumeration specifies which statistics in the [COR_GC_STATS](cor-gc-stats-structure.md) structure are to be set by [ICLRGCManager::GetStats](iclrgcmanager-getstats-method.md) method.</span></span>  
  
## <a name="members"></a><span data-ttu-id="fad62-107">成員</span><span class="sxs-lookup"><span data-stu-id="fad62-107">Members</span></span>  
  
|<span data-ttu-id="fad62-108">member</span><span class="sxs-lookup"><span data-stu-id="fad62-108">Member</span></span>|<span data-ttu-id="fad62-109">描述</span><span class="sxs-lookup"><span data-stu-id="fad62-109">Description</span></span>|  
|------------|-----------------|  
|`COR_GC_COUNTS`|<span data-ttu-id="fad62-110">記錄針對每個層代執行的垃圾收集數目。</span><span class="sxs-lookup"><span data-stu-id="fad62-110">Records the number of garbage collections performed for each generation.</span></span>|  
|`COR_GC_MEMORYUSAGE`|<span data-ttu-id="fad62-111">記錄記憶體使用量和垃圾收集大小統計資料。</span><span class="sxs-lookup"><span data-stu-id="fad62-111">Records memory usage and garbage collection size statistics.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="fad62-112">需求</span><span class="sxs-lookup"><span data-stu-id="fad62-112">Requirements</span></span>  

 <span data-ttu-id="fad62-113">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="fad62-113">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="fad62-114">**標頭：** GCHost .idl、GCHost。h</span><span class="sxs-lookup"><span data-stu-id="fad62-114">**Header:** GCHost.idl, GCHost.h</span></span>  
  
 <span data-ttu-id="fad62-115">**.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="fad62-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="fad62-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fad62-116">See also</span></span>

- [<span data-ttu-id="fad62-117">COR_GC_STATS 結構</span><span class="sxs-lookup"><span data-stu-id="fad62-117">COR_GC_STATS Structure</span></span>](cor-gc-stats-structure.md)
- [<span data-ttu-id="fad62-118">裝載列舉</span><span class="sxs-lookup"><span data-stu-id="fad62-118">Hosting Enumerations</span></span>](hosting-enumerations.md)
