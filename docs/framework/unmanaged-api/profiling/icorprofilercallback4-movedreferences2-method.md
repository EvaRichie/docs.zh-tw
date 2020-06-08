---
title: ICorProfilerCallback4::MovedReferences2 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback4.MovedReferences2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback4::MovedReferences2
helpviewer_keywords:
- MovedReferences2 method, ICorProfilerCallback4 interface [.NET Framework profiling]
- ICorProfilerCallback4::MovedReferences2 method [.NET Framework profiling]
ms.assetid: d17a065b-5bc6-4817-b3e1-1e413fcb33a8
topic_type:
- apiref
ms.openlocfilehash: 79e54cde8757bbe690f9b7c4344a2a3cb19cf627
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499378"
---
# <a name="icorprofilercallback4movedreferences2-method"></a><span data-ttu-id="abeed-102">ICorProfilerCallback4::MovedReferences2 方法</span><span class="sxs-lookup"><span data-stu-id="abeed-102">ICorProfilerCallback4::MovedReferences2 Method</span></span>
<span data-ttu-id="abeed-103">呼叫以報告壓縮記憶體回收造成的堆積中物件的新配置。</span><span class="sxs-lookup"><span data-stu-id="abeed-103">Called to report the new layout of objects in the heap as a result of a compacting garbage collection.</span></span> <span data-ttu-id="abeed-104">如果分析工具已實[ICorProfilerCallback4](icorprofilercallback4-interface.md)介面，則會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="abeed-104">This method is called if the profiler has implemented the [ICorProfilerCallback4](icorprofilercallback4-interface.md) interface.</span></span> <span data-ttu-id="abeed-105">此回呼會取代[ICorProfilerCallback：： MovedReferences](icorprofilercallback-movedreferences-method.md)方法，因為它可以報告較大範圍的物件，其長度超過可在 ULONG 中表示的數目。</span><span class="sxs-lookup"><span data-stu-id="abeed-105">This callback replaces the [ICorProfilerCallback::MovedReferences](icorprofilercallback-movedreferences-method.md) method, because it can report larger ranges of objects whose lengths exceed what can be expressed in a ULONG.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="abeed-106">語法</span><span class="sxs-lookup"><span data-stu-id="abeed-106">Syntax</span></span>  
  
```cpp  
HRESULT MovedReferences2(  
    [in]  ULONG  cMovedObjectIDRanges,  
    [in, size_is(cMovedObjectIDRanges)] ObjectID oldObjectIDRangeStart[] ,  
    [in, size_is(cMovedObjectIDRanges)] ObjectID newObjectIDRangeStart[] ,  
    [in, size_is(cMovedObjectIDRanges)] SIZE_T    cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a><span data-ttu-id="abeed-107">參數</span><span class="sxs-lookup"><span data-stu-id="abeed-107">Parameters</span></span>  
 `cMovedObjectIDRanges`  
 <span data-ttu-id="abeed-108">[in] 壓縮記憶體回收造成移動的連續物件區塊數目。</span><span class="sxs-lookup"><span data-stu-id="abeed-108">[in] The number of blocks of contiguous objects that moved as the result of the compacting garbage collection.</span></span> <span data-ttu-id="abeed-109">也就是 `cMovedObjectIDRanges` 的值是 `oldObjectIDRangeStart`、`newObjectIDRangeStart` 和 `cObjectIDRangeLength` 陣列的總大小。</span><span class="sxs-lookup"><span data-stu-id="abeed-109">That is, the value of `cMovedObjectIDRanges` is the total size of the `oldObjectIDRangeStart`, `newObjectIDRangeStart`, and `cObjectIDRangeLength` arrays.</span></span>  
  
 <span data-ttu-id="abeed-110">下面 `MovedReferences2` 的三個引數是平行陣列。</span><span class="sxs-lookup"><span data-stu-id="abeed-110">The next three arguments of `MovedReferences2` are parallel arrays.</span></span> <span data-ttu-id="abeed-111">換句話說，`oldObjectIDRangeStart[i]`、`newObjectIDRangeStart[i]` 和 `cObjectIDRangeLength[i]` 全都會考量連續物件的單一區塊。</span><span class="sxs-lookup"><span data-stu-id="abeed-111">In other words, `oldObjectIDRangeStart[i]`, `newObjectIDRangeStart[i]`, and `cObjectIDRangeLength[i]` all concern a single block of contiguous objects.</span></span>  
  
 `oldObjectIDRangeStart`  
 <span data-ttu-id="abeed-112">[in] 一個 `ObjectID` 值的陣列，其中每一個都是記憶體中連續即時物件之區塊舊的 (記憶體回收前) 開始位址。</span><span class="sxs-lookup"><span data-stu-id="abeed-112">[in] An array of `ObjectID` values, each of which is the old (pre-garbage collection) starting address of a block of contiguous, live objects in memory.</span></span>  
  
 `newObjectIDRangeStart`  
 <span data-ttu-id="abeed-113">[in] 一個 `ObjectID` 值的陣列，其中每一個都是記憶體中連續即時物件之區塊新的 (記憶體回收後) 開始位址。</span><span class="sxs-lookup"><span data-stu-id="abeed-113">[in] An array of `ObjectID` values, each of which is the new (post-garbage collection) starting address of a block of contiguous, live objects in memory.</span></span>  
  
 `cObjectIDRangeLength`  
 <span data-ttu-id="abeed-114">[in] 一個整數的陣列，其中每一個都是記憶體中連續物件區塊的大小。</span><span class="sxs-lookup"><span data-stu-id="abeed-114">[in] An array of integers, each of which is the size of a block of contiguous objects in memory.</span></span>  
  
 <span data-ttu-id="abeed-115">已指定大小給 `oldObjectIDRangeStart` 和 `newObjectIDRangeStart` 陣列中被參考的每個區塊。</span><span class="sxs-lookup"><span data-stu-id="abeed-115">A size is specified for each block that is referenced in the `oldObjectIDRangeStart` and `newObjectIDRangeStart` arrays.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="abeed-116">備註</span><span class="sxs-lookup"><span data-stu-id="abeed-116">Remarks</span></span>  
 <span data-ttu-id="abeed-117">壓縮記憶體回收行程會回收無作用物件所佔用的記憶體，且會壓縮釋放的空間。</span><span class="sxs-lookup"><span data-stu-id="abeed-117">A compacting garbage collector reclaims the memory occupied by dead objects and compacts that freed space.</span></span> <span data-ttu-id="abeed-118">如此一來，即時物件可能在堆積中移動，且先前通知所散發 `ObjectID` 的值可能會變更。</span><span class="sxs-lookup"><span data-stu-id="abeed-118">As a result, live objects might be moved within the heap, and `ObjectID` values distributed by previous notifications might change.</span></span>  
  
 <span data-ttu-id="abeed-119">假定現有 `ObjectID` 的值 (`oldObjectID`) 位於下列範圍內：</span><span class="sxs-lookup"><span data-stu-id="abeed-119">Assume that an existing `ObjectID` value (`oldObjectID`) lies within the following range:</span></span>  
  
 `oldObjectIDRangeStart[i]` <= `oldObjectID` < `oldObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 <span data-ttu-id="abeed-120">在此情況下，從範圍開頭到物件開頭的位移如下所示：</span><span class="sxs-lookup"><span data-stu-id="abeed-120">In this case, the offset from the start of the range to the start of the object is as follows:</span></span>  
  
 `oldObjectID` - `oldObjectRangeStart[i]`  
  
 <span data-ttu-id="abeed-121">對於位於下列範圍內的任何 `i` 值：</span><span class="sxs-lookup"><span data-stu-id="abeed-121">For any value of `i` that is in the following range:</span></span>  
  
 <span data-ttu-id="abeed-122">0 <=`i` < `cMovedObjectIDRanges`</span><span class="sxs-lookup"><span data-stu-id="abeed-122">0 <= `i` < `cMovedObjectIDRanges`</span></span>  
  
 <span data-ttu-id="abeed-123">您可以計算新的 `ObjectID`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="abeed-123">you can calculate the new `ObjectID` as follows:</span></span>  
  
 <span data-ttu-id="abeed-124">`newObjectID` = `newObjectIDRangeStart[i]`+ （ `oldObjectID` – `oldObjectIDRangeStart[i]` ）</span><span class="sxs-lookup"><span data-stu-id="abeed-124">`newObjectID` = `newObjectIDRangeStart[i]` + (`oldObjectID` – `oldObjectIDRangeStart[i]`)</span></span>  
  
 <span data-ttu-id="abeed-125">`MovedReferences2` 方法在回呼自己期間所傳遞的 `ObjectID` 值都無效，因為記憶體回收行程可能正在將物件從舊位置移至新位置。</span><span class="sxs-lookup"><span data-stu-id="abeed-125">None of the `ObjectID` values passed by `MovedReferences2` are valid during the callback itself, because the garbage collector might be in the middle of moving objects from old locations to new locations.</span></span> <span data-ttu-id="abeed-126">因此，分析工具不應嘗試在 `MovedReferences2` 呼叫期間檢查物件。</span><span class="sxs-lookup"><span data-stu-id="abeed-126">Therefore, profilers should not attempt to inspect objects during a `MovedReferences2` call.</span></span> <span data-ttu-id="abeed-127">[ICorProfilerCallback2：： GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)回呼表示所有物件都已移至其新位置，而且可以執行檢查。</span><span class="sxs-lookup"><span data-stu-id="abeed-127">A [ICorProfilerCallback2::GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md) callback indicates that all objects have been moved to their new locations and inspection can be performed.</span></span>  
  
 <span data-ttu-id="abeed-128">如果分析工具同時執行[ICorProfilerCallback](icorprofilercallback-interface.md)和[ICorProfilerCallback4](icorprofilercallback4-interface.md)介面，則會在 `MovedReferences2` [ICorProfilerCallback：： MovedReferences](icorprofilercallback-movedreferences-method.md)方法之前呼叫方法，但只有在方法成功傳回時才會呼叫 `MovedReferences2` 。</span><span class="sxs-lookup"><span data-stu-id="abeed-128">If the profiler implements both the [ICorProfilerCallback](icorprofilercallback-interface.md) and the [ICorProfilerCallback4](icorprofilercallback4-interface.md) interfaces, the `MovedReferences2` method is called before the [ICorProfilerCallback::MovedReferences](icorprofilercallback-movedreferences-method.md) method, but only if the `MovedReferences2` method returns successfully.</span></span> <span data-ttu-id="abeed-129">分析工具可傳回 HRESULT，表示 `MovedReferences2` 方法中的失敗，以避免呼叫第二個方法。</span><span class="sxs-lookup"><span data-stu-id="abeed-129">Profilers can return an HRESULT that indicates failure from the `MovedReferences2` method, to avoid calling the second method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="abeed-130">規格需求</span><span class="sxs-lookup"><span data-stu-id="abeed-130">Requirements</span></span>  
 <span data-ttu-id="abeed-131">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="abeed-131">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="abeed-132">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="abeed-132">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="abeed-133">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="abeed-133">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="abeed-134">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="abeed-134">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="abeed-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="abeed-135">See also</span></span>

- [<span data-ttu-id="abeed-136">ICorProfilerCallback 介面</span><span class="sxs-lookup"><span data-stu-id="abeed-136">ICorProfilerCallback Interface</span></span>](icorprofilercallback-interface.md)
- [<span data-ttu-id="abeed-137">MovedReferences 方法</span><span class="sxs-lookup"><span data-stu-id="abeed-137">MovedReferences Method</span></span>](icorprofilercallback-movedreferences-method.md)
- [<span data-ttu-id="abeed-138">ICorProfilerCallback4 介面</span><span class="sxs-lookup"><span data-stu-id="abeed-138">ICorProfilerCallback4 Interface</span></span>](icorprofilercallback4-interface.md)
- [<span data-ttu-id="abeed-139">分析介面</span><span class="sxs-lookup"><span data-stu-id="abeed-139">Profiling Interfaces</span></span>](profiling-interfaces.md)
- [<span data-ttu-id="abeed-140">程式碼剖析</span><span class="sxs-lookup"><span data-stu-id="abeed-140">Profiling</span></span>](index.md)
