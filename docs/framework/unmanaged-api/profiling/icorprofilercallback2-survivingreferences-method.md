---
title: ICorProfilerCallback2::SurvivingReferences 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback2.SurvivingReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback2::SurvivingReferences
helpviewer_keywords:
- ICorProfilerCallback2::SurvivingReferences method [.NET Framework profiling]
- SurvivingReferences method [.NET Framework profiling]
ms.assetid: f165200e-3a91-47f7-88fc-13ff10c8babc
topic_type:
- apiref
ms.openlocfilehash: 3681106bca94f1fefb2f24a1aa4254eb2b1b0531
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499736"
---
# <a name="icorprofilercallback2survivingreferences-method"></a><span data-ttu-id="1772a-102">ICorProfilerCallback2::SurvivingReferences 方法</span><span class="sxs-lookup"><span data-stu-id="1772a-102">ICorProfilerCallback2::SurvivingReferences Method</span></span>
<span data-ttu-id="1772a-103">報告非壓縮記憶體回收造成的堆積中物件配置。</span><span class="sxs-lookup"><span data-stu-id="1772a-103">Reports the layout of objects in the heap as a result of a non-compacting garbage collection.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1772a-104">語法</span><span class="sxs-lookup"><span data-stu-id="1772a-104">Syntax</span></span>  
  
```cpp  
HRESULT SurvivingReferences(  
    [in] ULONG  cSurvivingObjectIDRanges,  
    [in, size_is(cSurvivingObjectIDRanges)] ObjectID  
                objectIDRangeStart[] ,  
    [in, size_is(cSurvivingObjectIDRanges)] ULONG  
                cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a><span data-ttu-id="1772a-105">參數</span><span class="sxs-lookup"><span data-stu-id="1772a-105">Parameters</span></span>  
 `cSurvivingObjectIDRanges`  
 <span data-ttu-id="1772a-106">[in] 非壓縮記憶體回收後未被回收的連續物件區塊數目。</span><span class="sxs-lookup"><span data-stu-id="1772a-106">[in] The number of blocks of contiguous objects that survived as the result of the non-compacting garbage collection.</span></span> <span data-ttu-id="1772a-107">也就是說，`cSurvivingObjectIDRanges` 的值是 `objectIDRangeStart` 和 `cObjectIDRangeLength` 陣列的大小，會為每個物件區塊分別存放 `ObjectID` 和長度。</span><span class="sxs-lookup"><span data-stu-id="1772a-107">That is, the value of `cSurvivingObjectIDRanges` is the size of the `objectIDRangeStart` and `cObjectIDRangeLength` arrays, which store an `ObjectID` and a length, respectively, for each block of objects.</span></span>  
  
 <span data-ttu-id="1772a-108">`SurvivingReferences` 的下兩個引數是平行陣列。</span><span class="sxs-lookup"><span data-stu-id="1772a-108">The next two arguments of `SurvivingReferences` are parallel arrays.</span></span> <span data-ttu-id="1772a-109">換句話說，`objectIDRangeStart` 和 `cObjectIDRangeLength` 會考量連續物件的相同區塊。</span><span class="sxs-lookup"><span data-stu-id="1772a-109">In other words, `objectIDRangeStart` and `cObjectIDRangeLength` concern the same block of contiguous objects.</span></span>  
  
 `objectIDRangeStart`  
 <span data-ttu-id="1772a-110">[in] `ObjectID` 值的陣列，其中每一個都是記憶體中連續即時物件之區塊的開始位址。</span><span class="sxs-lookup"><span data-stu-id="1772a-110">[in] An array of `ObjectID` values, each of which is the starting address of a block of contiguous, live objects in memory.</span></span>  
  
 `cObjectIDRangeLength`  
 <span data-ttu-id="1772a-111">[in] 整數的陣列，其中每一個都是記憶體中連續物件之未被回收區塊的大小。</span><span class="sxs-lookup"><span data-stu-id="1772a-111">[in] An array of integers, each of which is the size of a surviving block of contiguous objects in memory.</span></span>  
  
 <span data-ttu-id="1772a-112">已為 `objectIDRangeStart` 陣列中被參考的每個區塊指定大小。</span><span class="sxs-lookup"><span data-stu-id="1772a-112">A size is specified for each block that is referenced in the `objectIDRangeStart` array.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="1772a-113">備註</span><span class="sxs-lookup"><span data-stu-id="1772a-113">Remarks</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="1772a-114">對於在 64 位元平台上大於 4 GB 的物件，這個方法會報告大小為 `MAX_ULONG`。</span><span class="sxs-lookup"><span data-stu-id="1772a-114">This method reports sizes as `MAX_ULONG` for objects that are greater than 4 GB on 64-bit platforms.</span></span> <span data-ttu-id="1772a-115">對於大於 4 GB 的物件，請改用[ICorProfilerCallback4：： SurvivingReferences2](icorprofilercallback4-survivingreferences2-method.md)方法。</span><span class="sxs-lookup"><span data-stu-id="1772a-115">For objects that are larger than 4 GB, use the [ICorProfilerCallback4::SurvivingReferences2](icorprofilercallback4-survivingreferences2-method.md) method instead.</span></span>  
  
 <span data-ttu-id="1772a-116">`objectIDRangeStart` 和 `cObjectIDRangeLength` 陣列的項目應解譯如下，以判斷物件是否未被記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="1772a-116">The elements of the `objectIDRangeStart` and `cObjectIDRangeLength` arrays should be interpreted as follows to determine whether an object survived the garbage collection.</span></span> <span data-ttu-id="1772a-117">假定 `ObjectID` 的值 (`ObjectID`) 位於下列範圍內：</span><span class="sxs-lookup"><span data-stu-id="1772a-117">Assume that an `ObjectID` value (`ObjectID`) lies within the following range:</span></span>  
  
 `ObjectIDRangeStart[i]` <= `ObjectID` < `ObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 <span data-ttu-id="1772a-118">針對任何位於下列範圍內的 `i` 之值，該物件尚未被記憶體回收：</span><span class="sxs-lookup"><span data-stu-id="1772a-118">For any value of `i` that is in the following range, the object has survived the garbage collection:</span></span>  
  
 <span data-ttu-id="1772a-119">0 <=`i` < `cSurvivingObjectIDRanges`</span><span class="sxs-lookup"><span data-stu-id="1772a-119">0 <= `i` < `cSurvivingObjectIDRanges`</span></span>  
  
 <span data-ttu-id="1772a-120">非壓縮記憶體回收會回收「無作用」物件所佔用的記憶體，但是不會壓縮該釋放的空間。</span><span class="sxs-lookup"><span data-stu-id="1772a-120">A non-compacting garbage collection reclaims the memory occupied by "dead" objects, but does not compact that freed space.</span></span> <span data-ttu-id="1772a-121">因此，記憶體會傳回到堆積，但沒有移動「即時」物件。</span><span class="sxs-lookup"><span data-stu-id="1772a-121">As a result, memory is returned to the heap, but no "live" objects are moved.</span></span>  
  
 <span data-ttu-id="1772a-122">針對非壓縮記憶體回收，Common Language Runtime (CLR) 會呼叫 `SurvivingReferences`。</span><span class="sxs-lookup"><span data-stu-id="1772a-122">The common language runtime (CLR) calls `SurvivingReferences` for non-compacting garbage collections.</span></span> <span data-ttu-id="1772a-123">針對壓縮垃圾收集，會改為呼叫[ICorProfilerCallback：： MovedReferences](icorprofilercallback-movedreferences-method.md) 。</span><span class="sxs-lookup"><span data-stu-id="1772a-123">For compacting garbage collections, [ICorProfilerCallback::MovedReferences](icorprofilercallback-movedreferences-method.md) is called instead.</span></span> <span data-ttu-id="1772a-124">單一記憶體回收可以為了某個層代而壓縮，但另一個則不壓縮。</span><span class="sxs-lookup"><span data-stu-id="1772a-124">A single garbage collection can be compacting for one generation and non-compacting for another.</span></span> <span data-ttu-id="1772a-125">對於在任何特定層代上的記憶體回收，分析工具將接收 `SurvivingReferences` 回呼或 `MovedReferences` 回呼，但不可同時接收。</span><span class="sxs-lookup"><span data-stu-id="1772a-125">For a garbage collection on any particular generation, the profiler will receive either a `SurvivingReferences` callback or a `MovedReferences` callback, but not both.</span></span>  
  
 <span data-ttu-id="1772a-126">因為有限的內部緩衝區、在伺服器記憶體回收期間以及其他原因的多重執行緒報告，在特定記憶體回收期間可能接收多重 `SurvivingReferences` 回呼。</span><span class="sxs-lookup"><span data-stu-id="1772a-126">Multiple `SurvivingReferences` callbacks might be received during a particular garbage collection, due to limited internal buffering, multiple threads reporting in the case of server garbage collection, and other reasons.</span></span> <span data-ttu-id="1772a-127">在記憶體回收期間多個回呼的情況下，資訊是累計的；在任何 `SurvivingReferences` 回呼中被報告的所有參考不會被記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="1772a-127">In the case of multiple callbacks during a garbage collection, the information is cumulative — all references that are reported in any `SurvivingReferences` callback survive the garbage collection.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1772a-128">規格需求</span><span class="sxs-lookup"><span data-stu-id="1772a-128">Requirements</span></span>  
 <span data-ttu-id="1772a-129">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="1772a-129">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1772a-130">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="1772a-130">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="1772a-131">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="1772a-131">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="1772a-132">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1772a-132">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1772a-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1772a-133">See also</span></span>

- [<span data-ttu-id="1772a-134">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="1772a-134">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="1772a-135">ICorProfilerCallback2 介面</span><span class="sxs-lookup"><span data-stu-id="1772a-135">ICorProfilerCallback2 Interface</span></span>](icorprofilercallback2-interface.md)
- [<span data-ttu-id="1772a-136">SurvivingReferences2 方法</span><span class="sxs-lookup"><span data-stu-id="1772a-136">SurvivingReferences2 Method</span></span>](icorprofilercallback4-survivingreferences2-method.md)
