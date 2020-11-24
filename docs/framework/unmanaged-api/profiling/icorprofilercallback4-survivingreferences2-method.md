---
title: ICorProfilerCallback4::SurvivingReferences2 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.SurvivingReferences2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::SurvivingReferences2
helpviewer_keywords:
- ICorProfilerCallback4::SurvivingReferences2 method [.NET Framework profiling]
- SurvivingReferences2 method, ICorProfilerCallback4 interface [.NET Framework profiling]
ms.assetid: 02b51888-5d89-4e50-a915-45b7e329aad9
topic_type:
- apiref
ms.openlocfilehash: fb10057a406bd2192e0da61f916f81697dfa4a7d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95689312"
---
# <a name="icorprofilercallback4survivingreferences2-method"></a><span data-ttu-id="4e82d-102">ICorProfilerCallback4::SurvivingReferences2 方法</span><span class="sxs-lookup"><span data-stu-id="4e82d-102">ICorProfilerCallback4::SurvivingReferences2 Method</span></span>

<span data-ttu-id="4e82d-103">報告非壓縮記憶體回收造成的堆積中物件配置。</span><span class="sxs-lookup"><span data-stu-id="4e82d-103">Reports the layout of objects in the heap as a result of a non-compacting garbage collection.</span></span> <span data-ttu-id="4e82d-104">如果分析工具已執行 [ICorProfilerCallback4](icorprofilercallback4-interface.md) 介面，則會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="4e82d-104">This method is called if the profiler has implemented the [ICorProfilerCallback4](icorprofilercallback4-interface.md) interface.</span></span> <span data-ttu-id="4e82d-105">此回呼會取代 [ICorProfilerCallback2：： SurvivingReferences](icorprofilercallback2-survivingreferences-method.md) 方法，因為它可以報告其長度超過 ULONG 中可表示之物件的較大範圍。</span><span class="sxs-lookup"><span data-stu-id="4e82d-105">This callback replaces the [ICorProfilerCallback2::SurvivingReferences](icorprofilercallback2-survivingreferences-method.md) method, because it can report larger ranges of objects whose lengths exceed what can be expressed in a ULONG.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4e82d-106">語法</span><span class="sxs-lookup"><span data-stu-id="4e82d-106">Syntax</span></span>  
  
```cpp  
HRESULT SurvivingReferences2(  
    [in] ULONG  cSurvivingObjectIDRanges,  
    [in, size_is(cSurvivingObjectIDRanges)] ObjectID  
                objectIDRangeStart[] ,  
    [in, size_is(cSurvivingObjectIDRanges)] SIZE_T  
                cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a><span data-ttu-id="4e82d-107">參數</span><span class="sxs-lookup"><span data-stu-id="4e82d-107">Parameters</span></span>  

 `cSurvivingObjectIDRanges`  
 <span data-ttu-id="4e82d-108">[in] 非壓縮記憶體回收後未被回收的連續物件區塊數目。</span><span class="sxs-lookup"><span data-stu-id="4e82d-108">[in] The number of blocks of contiguous objects that survived as the result of the non-compacting garbage collection.</span></span> <span data-ttu-id="4e82d-109">也就是說，`cSurvivingObjectIDRanges` 的值是 `objectIDRangeStart` 和 `cObjectIDRangeLength` 陣列的大小，會為每個物件區塊分別存放 `ObjectID` 和長度。</span><span class="sxs-lookup"><span data-stu-id="4e82d-109">That is, the value of `cSurvivingObjectIDRanges` is the size of the `objectIDRangeStart` and `cObjectIDRangeLength` arrays, which store an `ObjectID` and a length, respectively, for each block of objects.</span></span>  
  
 <span data-ttu-id="4e82d-110">`SurvivingReferences2` 的下兩個引數是平行陣列。</span><span class="sxs-lookup"><span data-stu-id="4e82d-110">The next two arguments of `SurvivingReferences2` are parallel arrays.</span></span> <span data-ttu-id="4e82d-111">換句話說，`objectIDRangeStart` 和 `cObjectIDRangeLength` 會考量連續物件的相同區塊。</span><span class="sxs-lookup"><span data-stu-id="4e82d-111">In other words, `objectIDRangeStart` and `cObjectIDRangeLength` concern the same block of contiguous objects.</span></span>  
  
 `objectIDRangeStart`  
 <span data-ttu-id="4e82d-112">[in] `ObjectID` 值的陣列，其中每一個都是記憶體中連續即時物件之區塊的開始位址。</span><span class="sxs-lookup"><span data-stu-id="4e82d-112">[in] An array of `ObjectID` values, each of which is the starting address of a block of contiguous, live objects in memory.</span></span>  
  
 `cObjectIDRangeLength`  
 <span data-ttu-id="4e82d-113">[in] 整數的陣列，其中每一個都是記憶體中連續物件之未被回收區塊的大小。</span><span class="sxs-lookup"><span data-stu-id="4e82d-113">[in] An array of integers, each of which is the size of a surviving block of contiguous objects in memory.</span></span>  
  
 <span data-ttu-id="4e82d-114">已為 `objectIDRangeStart` 陣列中被參考的每個區塊指定大小。</span><span class="sxs-lookup"><span data-stu-id="4e82d-114">A size is specified for each block that is referenced in the `objectIDRangeStart` array.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="4e82d-115">備註</span><span class="sxs-lookup"><span data-stu-id="4e82d-115">Remarks</span></span>  

 <span data-ttu-id="4e82d-116">`objectIDRangeStart` 和 `cObjectIDRangeLength` 陣列的項目應解譯如下，以判斷物件是否未被記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="4e82d-116">The elements of the `objectIDRangeStart` and `cObjectIDRangeLength` arrays should be interpreted as follows to determine whether an object survived the garbage collection.</span></span> <span data-ttu-id="4e82d-117">假定 `ObjectID` 的值 (`ObjectID`) 位於下列範圍內：</span><span class="sxs-lookup"><span data-stu-id="4e82d-117">Assume that an `ObjectID` value (`ObjectID`) lies within the following range:</span></span>  
  
 `ObjectIDRangeStart[i]` <= `ObjectID` < `ObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 <span data-ttu-id="4e82d-118">針對任何位於下列範圍內的 `i` 之值，該物件尚未被記憶體回收：</span><span class="sxs-lookup"><span data-stu-id="4e82d-118">For any value of `i` that is in the following range, the object has survived the garbage collection:</span></span>  
  
 <span data-ttu-id="4e82d-119">0 <= `i` < `cSurvivingObjectIDRanges`</span><span class="sxs-lookup"><span data-stu-id="4e82d-119">0 <= `i` < `cSurvivingObjectIDRanges`</span></span>  
  
 <span data-ttu-id="4e82d-120">非壓縮記憶體回收會回收「無作用」物件所佔用的記憶體，但是不會壓縮該釋放的空間。</span><span class="sxs-lookup"><span data-stu-id="4e82d-120">A non-compacting garbage collection reclaims the memory occupied by "dead" objects, but does not compact that freed space.</span></span> <span data-ttu-id="4e82d-121">因此，記憶體會傳回到堆積，但沒有移動「即時」物件。</span><span class="sxs-lookup"><span data-stu-id="4e82d-121">As a result, memory is returned to the heap, but no "live" objects are moved.</span></span>  
  
 <span data-ttu-id="4e82d-122">針對非壓縮記憶體回收，Common Language Runtime (CLR) 會呼叫 `SurvivingReferences2`。</span><span class="sxs-lookup"><span data-stu-id="4e82d-122">The common language runtime (CLR) calls `SurvivingReferences2` for non-compacting garbage collections.</span></span> <span data-ttu-id="4e82d-123">針對壓縮垃圾收集，會改為呼叫 [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) 。</span><span class="sxs-lookup"><span data-stu-id="4e82d-123">For compacting garbage collections, [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) is called instead.</span></span> <span data-ttu-id="4e82d-124">單一記憶體回收可以為了某個層代而壓縮，但另一個則不壓縮。</span><span class="sxs-lookup"><span data-stu-id="4e82d-124">A single garbage collection can be compacting for one generation and non-compacting for another.</span></span> <span data-ttu-id="4e82d-125">針對任何特定世代的垃圾收集，分析工具會收到 `SurvivingReferences2` 回呼或 [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) 回呼，但不能同時接收兩者。</span><span class="sxs-lookup"><span data-stu-id="4e82d-125">For a garbage collection on any particular generation, the profiler will receive either a `SurvivingReferences2` callback or a [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) callback, but not both.</span></span>  
  
 <span data-ttu-id="4e82d-126">因為有限的內部緩衝區、伺服器記憶體回收期間的多重回呼和其他原因，在特定記憶體回收期間可能接收多重 `SurvivingReferences2` 回呼。</span><span class="sxs-lookup"><span data-stu-id="4e82d-126">Multiple `SurvivingReferences2` callbacks might be received during a particular garbage collection, because of limited internal buffering, multiple callbacks during server garbage collection, and other reasons.</span></span> <span data-ttu-id="4e82d-127">在記憶體回收期間多個回呼的情況下，資訊是累計的；在任何 `SurvivingReferences2` 回呼中被報告的所有參考不會被記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="4e82d-127">In the case of multiple callbacks during a garbage collection, the information is cumulative; all references that are reported in any `SurvivingReferences2` callback survive the garbage collection.</span></span>  
  
 <span data-ttu-id="4e82d-128">如果 profiler 同時執行 [ICorProfilerCallback](icorprofilercallback-interface.md) 和 [ICorProfilerCallback4](icorprofilercallback4-interface.md) 介面，則 `SurvivingReferences2` 會在 [ICorProfilerCallback2：： SurvivingReferences](icorprofilercallback2-survivingreferences-method.md) 方法之前呼叫方法，但只有在成功傳回時才會呼叫方法 `SurvivingReferences2` 。</span><span class="sxs-lookup"><span data-stu-id="4e82d-128">If the profiler implements both the [ICorProfilerCallback](icorprofilercallback-interface.md) and the [ICorProfilerCallback4](icorprofilercallback4-interface.md) interfaces, the `SurvivingReferences2` method is called before the [ICorProfilerCallback2::SurvivingReferences](icorprofilercallback2-survivingreferences-method.md) method, but only if `SurvivingReferences2` returns successfully.</span></span> <span data-ttu-id="4e82d-129">分析工具可傳回 HRESULT，表示 `SurvivingReferences2` 方法中的失敗，以避免呼叫第二個方法。</span><span class="sxs-lookup"><span data-stu-id="4e82d-129">Profilers can return an HRESULT that indicates failure from the `SurvivingReferences2` method to avoid calling the second method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4e82d-130">需求</span><span class="sxs-lookup"><span data-stu-id="4e82d-130">Requirements</span></span>  

 <span data-ttu-id="4e82d-131">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="4e82d-131">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4e82d-132">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="4e82d-132">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="4e82d-133">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="4e82d-133">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="4e82d-134">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4e82d-134">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4e82d-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4e82d-135">See also</span></span>

- [<span data-ttu-id="4e82d-136">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="4e82d-136">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="4e82d-137">ICorProfilerCallback2 介面</span><span class="sxs-lookup"><span data-stu-id="4e82d-137">ICorProfilerCallback2 Interface</span></span>](icorprofilercallback2-interface.md)
- [<span data-ttu-id="4e82d-138">ICorProfilerCallback4 介面</span><span class="sxs-lookup"><span data-stu-id="4e82d-138">ICorProfilerCallback4 Interface</span></span>](icorprofilercallback4-interface.md)
