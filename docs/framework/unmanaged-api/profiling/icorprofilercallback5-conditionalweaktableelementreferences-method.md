---
title: ICorProfilerCallback5::ConditionalWeakTableElementReferences 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback5.ConditionalWeakTableReferences
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ConditionalWeakTableElementReferences
helpviewer_keywords:
- ConditionalWeakTableElementReferences method, ICorProfilerCallback5 interface [.NET Framework profiling]
- ICorProfilerCallback5::ConditionalWeakTableElementReferences method [.NET Framework profiling]
ms.assetid: 532c7a02-a9de-4cea-bb2b-7f470da594de
topic_type:
- apiref
ms.openlocfilehash: 17fbc99b30921f795c1f7ff882ec73432aade8c6
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499242"
---
# <a name="icorprofilercallback5conditionalweaktableelementreferences-method"></a><span data-ttu-id="0cdb4-102">ICorProfilerCallback5::ConditionalWeakTableElementReferences 方法</span><span class="sxs-lookup"><span data-stu-id="0cdb4-102">ICorProfilerCallback5::ConditionalWeakTableElementReferences Method</span></span>

<span data-ttu-id="0cdb4-103">識別那些根目錄透過直接成員欄位參考以及透過 `ConditionalWeakTable` 相依性來參考之物件的可轉移結束。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-103">Identifies the transitive closure of objects referenced by those roots through both direct member field references and through `ConditionalWeakTable` dependencies.</span></span>

## <a name="syntax"></a><span data-ttu-id="0cdb4-104">語法</span><span class="sxs-lookup"><span data-stu-id="0cdb4-104">Syntax</span></span>

```cpp
HRESULT ConditionalWeakTableElementReferences(
     [in]                     ULONG    cRootRefs,
     [in, size_is(cRootRefs)] ObjectID keyRefIds[],
     [in, size_is(cRootRefs)] ObjectID valueRefIds[],
     [in, size_is(cRootRefs)] GCHandleID rootIds[]
);
```

## <a name="parameters"></a><span data-ttu-id="0cdb4-105">參數</span><span class="sxs-lookup"><span data-stu-id="0cdb4-105">Parameters</span></span>

`cRootRefs`\
<span data-ttu-id="0cdb4-106">[in] `keyRefIds`、`valueRefIds` 和 `rootIds` 陣列中的項目數。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-106">[in] The number of elements in the `keyRefIds`, `valueRefIds`, and `rootIds` arrays.</span></span>

`keyRefIds`\
<span data-ttu-id="0cdb4-107">[in] 物件 ID 陣列，針對相依性控制代碼配對中的主要項目，各包含一個 `ObjectID`。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-107">[in] An array of object IDs, each of which contains the `ObjectID` for the primary element in the dependent handle pair.</span></span>

`valueRefIds`\
<span data-ttu-id="0cdb4-108">[in] 物件 ID 陣列，針對相依性控制代碼配對中的次要項目，各包含一個 `ObjectID`。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-108">[in] An array of object IDs, each of which contains the `ObjectID` for the secondary element in the dependent handle pair.</span></span> <span data-ttu-id="0cdb4-109">（ `keyRefIds[i]` 保持運作 `valueRefIds[i]` 狀態）。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-109">(`keyRefIds[i]` keeps `valueRefIds[i]` alive.)</span></span>

`rootIds`\
<span data-ttu-id="0cdb4-110">[in] `GCHandleID` 值陣列，這些值會指向包含記憶體回收根目錄相關資訊的整數。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-110">[in] An array of `GCHandleID` values that point to an integer that contains additional information about the garbage collection root.</span></span>

<span data-ttu-id="0cdb4-111">`ObjectID` 方法在回呼自己期間所傳回的 `ConditionalWeakTableElementReferences` 值都無效，因為記憶體回收行程可能正在進行將物件從舊位置移至新位置的程序。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-111">None of the `ObjectID` values returned by the `ConditionalWeakTableElementReferences` method are valid during the callback itself, because the garbage collector may be in the process of moving objects from old to new locations.</span></span> <span data-ttu-id="0cdb4-112">因此，分析工具不應嘗試在 `ConditionalWeakTableElementReferences` 呼叫期間檢查物件。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-112">Therefore, profilers should not attempt to inspect objects during a `ConditionalWeakTableElementReferences` call.</span></span> <span data-ttu-id="0cdb4-113">在 `GarbageCollectionFinished` 時，所有物件都已移至其新位置，可能已完成檢查。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-113">At `GarbageCollectionFinished`, all objects have been moved to their new locations, and inspection may be done.</span></span>

## <a name="example"></a><span data-ttu-id="0cdb4-114">範例</span><span class="sxs-lookup"><span data-stu-id="0cdb4-114">Example</span></span>

<span data-ttu-id="0cdb4-115">下列程式碼範例示範如何執行[ICorProfilerCallback5](icorprofilercallback5-interface.md) ，並使用此方法。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-115">The following code example demonstrates how to implement [ICorProfilerCallback5](icorprofilercallback5-interface.md) and use this method.</span></span>

```cpp
HRESULT Callback5Impl::ConditionalWeakTableElementReferences(
    ULONG      cRootRefs,
    ObjectID   keyRefIds[],
    ObjectID   valueRefIds[],
    GCHandleID rootIds[])
{
    printf("Callback5Impl::ConditionalWeakTableElementReferences called\n");
    for (unsigned int i = 0; i < cRootRefs; ++i)
    {
        // Save dependency to XML for later retrieval
        PersistDependencyToXml(rootIds[i], keyRefIds[i], valueRefIds[i]);
        // or store dependency to an internal map
        m_cwt_deps->add_dep(rootIds[i], keyRefIds[i], valueRefIds[i]);
        // or add arc to object graph
        m_obj_graph->add_arc(keyRefIds[i], valueRefIds[i], rootIds[i]);
    }
    return S_OK;
}
```

## <a name="remarks"></a><span data-ttu-id="0cdb4-116">備註</span><span class="sxs-lookup"><span data-stu-id="0cdb4-116">Remarks</span></span>

<span data-ttu-id="0cdb4-117">.NET Framework 4.5 或更新版本的 profiler 會執行[ICorProfilerCallback5](icorprofilercallback5-interface.md)介面，並記錄方法所指定的相依性 `ConditionalWeakTableElementReferences` 。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-117">A profiler for the .NET Framework 4.5 or later versions implements the [ICorProfilerCallback5](icorprofilercallback5-interface.md) interface and records the dependencies specified by the `ConditionalWeakTableElementReferences` method.</span></span> <span data-ttu-id="0cdb4-118">`ICorProfilerCallback5`提供專案所代表之即時物件之間的完整相依性集合 `ConditionalWeakTable` 。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-118">`ICorProfilerCallback5` provides the complete set of dependencies among live objects represented by `ConditionalWeakTable` entries.</span></span> <span data-ttu-id="0cdb4-119">這些相依性和[ICorProfilerCallback：： ObjectReferences](icorprofilercallback-objectreferences-method.md)方法所指定的成員欄位參考，可讓 managed profiler 產生即時物件的完整物件圖形。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-119">These dependencies and the member field references specified by the [ICorProfilerCallback::ObjectReferences](icorprofilercallback-objectreferences-method.md) method enable a managed profiler to generate the full object graph of live objects.</span></span>

## <a name="requirements"></a><span data-ttu-id="0cdb4-120">規格需求</span><span class="sxs-lookup"><span data-stu-id="0cdb4-120">Requirements</span></span>

<span data-ttu-id="0cdb4-121">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="0cdb4-121">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>

<span data-ttu-id="0cdb4-122">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="0cdb4-122">**Header:** CorProf.idl, CorProf.h</span></span>

<span data-ttu-id="0cdb4-123">**.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0cdb4-123">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>

## <a name="see-also"></a><span data-ttu-id="0cdb4-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0cdb4-124">See also</span></span>

- [<span data-ttu-id="0cdb4-125">ICorProfilerCallback5 介面</span><span class="sxs-lookup"><span data-stu-id="0cdb4-125">ICorProfilerCallback5 Interface</span></span>](icorprofilercallback5-interface.md)
