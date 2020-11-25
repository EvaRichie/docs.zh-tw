---
title: COR_SEGMENT 結構
ms.date: 03/30/2017
api_name:
- COR_SEGMENT
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_SEGMENT
helpviewer_keywords:
- COR_SEGMENT structure [.NET Framework debugging]
ms.assetid: 93aeecb9-7fef-4545-8daf-f566dfc47084
topic_type:
- apiref
ms.openlocfilehash: 738e29fa15340c76b055b608140f3c3bfbd29611
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726349"
---
# <a name="cor_segment-structure"></a><span data-ttu-id="bf158-102">COR_SEGMENT 結構</span><span class="sxs-lookup"><span data-stu-id="bf158-102">COR_SEGMENT Structure</span></span>

<span data-ttu-id="bf158-103">包含 Managed 堆積中記憶體區域的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bf158-103">Contains information about a region of memory in the managed heap.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="bf158-104">語法</span><span class="sxs-lookup"><span data-stu-id="bf158-104">Syntax</span></span>  
  
```cpp  
typedef struct _COR_SEGMENT {  
    CORDB_ADDRESS start;
    CORDB_ADDRESS end;
    CorDebugGenerationTypes gen;
    ULONG heap;
} COR_SEGMENT;  
```  
  
## <a name="members"></a><span data-ttu-id="bf158-105">成員</span><span class="sxs-lookup"><span data-stu-id="bf158-105">Members</span></span>  
  
|<span data-ttu-id="bf158-106">member</span><span class="sxs-lookup"><span data-stu-id="bf158-106">Member</span></span>|<span data-ttu-id="bf158-107">描述</span><span class="sxs-lookup"><span data-stu-id="bf158-107">Description</span></span>|  
|------------|-----------------|  
|`start`|<span data-ttu-id="bf158-108">記憶體區域的起始位址。</span><span class="sxs-lookup"><span data-stu-id="bf158-108">The starting address of the memory region.</span></span>|  
|`end`|<span data-ttu-id="bf158-109">記憶體區域的結束位址。</span><span class="sxs-lookup"><span data-stu-id="bf158-109">The ending address of the memory region.</span></span>|  
|`gen`|<span data-ttu-id="bf158-110">[CorDebugGenerationTypes](cordebuggenerationtypes-enumeration.md) 列舉成員，表示記憶體區域的層代。</span><span class="sxs-lookup"><span data-stu-id="bf158-110">A [CorDebugGenerationTypes](cordebuggenerationtypes-enumeration.md) enumeration member that indicates the generation of the memory region.</span></span>|  
|`heap`|<span data-ttu-id="bf158-111">記憶體區域所在的堆積號碼。</span><span class="sxs-lookup"><span data-stu-id="bf158-111">The heap number in which the memory region resides.</span></span> <span data-ttu-id="bf158-112">如需詳細資訊，請參閱＜備註＞一節。</span><span class="sxs-lookup"><span data-stu-id="bf158-112">See the Remarks section for more information.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="bf158-113">備註</span><span class="sxs-lookup"><span data-stu-id="bf158-113">Remarks</span></span>  

 <span data-ttu-id="bf158-114">`COR_SEGMENTS` 結構代表受空控堆積中的記憶體區域。</span><span class="sxs-lookup"><span data-stu-id="bf158-114">The `COR_SEGMENTS` structure represents a region of memory in the managed heap.</span></span>  <span data-ttu-id="bf158-115">`COR_SEGMENTS` 物件是 [ICorDebugHeapRegionEnum](icordebugheapsegmentenum-interface.md) 集合物件的成員，集合物件的填入是藉由呼叫 [icordebugprocess5:: Enumerateheapregions](icordebugprocess5-enumerateheapregions-method.md) 方法。</span><span class="sxs-lookup"><span data-stu-id="bf158-115">`COR_SEGMENTS` objects are members of the [ICorDebugHeapRegionEnum](icordebugheapsegmentenum-interface.md) collection object, which is populated by calling the [ICorDebugProcess5::EnumerateHeapRegions](icordebugprocess5-enumerateheapregions-method.md) method.</span></span>  
  
 <span data-ttu-id="bf158-116">`heap` 欄位是處理器號碼，其對應到正在回報的堆積。</span><span class="sxs-lookup"><span data-stu-id="bf158-116">The `heap` field is the processor number, which corresponds to the heap being reported.</span></span> <span data-ttu-id="bf158-117">針對工作站記憶體回收行程，其值一律為零，因為工作站只有一個記憶體回收堆積。</span><span class="sxs-lookup"><span data-stu-id="bf158-117">For workstation garbage collectors, its value is always zero, because workstations have only one garbage collection heap.</span></span> <span data-ttu-id="bf158-118">針對伺服器記憶體回收行程，其值對應至堆積附加的處理器。</span><span class="sxs-lookup"><span data-stu-id="bf158-118">For server garbage collectors, its value corresponds to the processor the heap is attached to.</span></span> <span data-ttu-id="bf158-119">請注意，可能會有比實際處理器更多或更少記憶體回收堆積，這是因為記憶體回收行程的實作詳細資料所致。</span><span class="sxs-lookup"><span data-stu-id="bf158-119">Note that there may be more or fewer garbage collection heaps than there are actual processors due to the implementation details of the garbage collector.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="bf158-120">需求</span><span class="sxs-lookup"><span data-stu-id="bf158-120">Requirements</span></span>  

 <span data-ttu-id="bf158-121">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="bf158-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="bf158-122">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="bf158-122">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="bf158-123">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="bf158-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="bf158-124">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="bf158-124">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bf158-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bf158-125">See also</span></span>

- [<span data-ttu-id="bf158-126">偵錯結構</span><span class="sxs-lookup"><span data-stu-id="bf158-126">Debugging Structures</span></span>](debugging-structures.md)
- [<span data-ttu-id="bf158-127">偵錯</span><span class="sxs-lookup"><span data-stu-id="bf158-127">Debugging</span></span>](index.md)
