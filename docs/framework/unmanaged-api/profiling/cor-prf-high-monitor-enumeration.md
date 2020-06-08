---
title: COR_PRF_HIGH_MONITOR 列舉
ms.date: 04/10/2018
ms.assetid: 3ba543d8-15e5-4322-b6e7-1ebfc92ed7dd
ms.openlocfilehash: b813b32ef4522f1707812d337d20790ce75f3d55
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500841"
---
# <a name="cor_prf_high_monitor-enumeration"></a><span data-ttu-id="116bd-102">COR_PRF_HIGH_MONITOR 列舉</span><span class="sxs-lookup"><span data-stu-id="116bd-102">COR_PRF_HIGH_MONITOR Enumeration</span></span>

<span data-ttu-id="116bd-103">[.NET Framework 4.5.2 與更新版本提供支援]</span><span class="sxs-lookup"><span data-stu-id="116bd-103">[Supported in the .NET Framework 4.5.2 and later versions]</span></span>  
  
<span data-ttu-id="116bd-104">除了在[ICorProfilerInfo5：： SetEventMask2](icorprofilerinfo5-seteventmask2-method.md)方法載入時，分析工具可以指定的標記[COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)以外，還提供旗標。</span><span class="sxs-lookup"><span data-stu-id="116bd-104">Provides flags in addition to those found in the [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) enumeration that the profiler can specify to the [ICorProfilerInfo5::SetEventMask2](icorprofilerinfo5-seteventmask2-method.md) method when it is loading.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="116bd-105">語法</span><span class="sxs-lookup"><span data-stu-id="116bd-105">Syntax</span></span>  
  
```cpp
typedef enum {  
    COR_PRF_HIGH_MONITOR_NONE                     = 0x00000000,  
    COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES          = 0x00000001,  
    COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED        = 0x00000002,
    COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS = 0x00000004,
    COR_PRF_HIGH_DISABLE_TIERED_COMPILATION       = 0x00000008,
    COR_PRF_HIGH_BASIC_GC                         = 0x00000010,
    COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS         = 0x00000020,
    COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED    = 0x00000040,
    COR_PRF_HIGH_REQUIRE_PROFILE_IMAGE            = 0,  
    COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH           = COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED |
                                                    COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS |
                                                    COR_PRF_HIGH_BASIC_GC |
                                                    COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS |
                                                    COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED,  
    COR_PRF_HIGH_MONITOR_IMMUTABLE                = COR_PRF_HIGH_DISABLE_TIERED_COMPILATION  
} COR_PRF_HIGH_MONITOR;  
```  
  
## <a name="members"></a><span data-ttu-id="116bd-106">成員</span><span class="sxs-lookup"><span data-stu-id="116bd-106">Members</span></span>  
  
|<span data-ttu-id="116bd-107">成員</span><span class="sxs-lookup"><span data-stu-id="116bd-107">Member</span></span>|<span data-ttu-id="116bd-108">說明</span><span class="sxs-lookup"><span data-stu-id="116bd-108">Description</span></span>|  
|------------|-----------------|  
|`COR_PRF_HIGH_MONITOR_NONE`|<span data-ttu-id="116bd-109">沒有設定旗標。</span><span class="sxs-lookup"><span data-stu-id="116bd-109">No flags are set.</span></span>|  
|`COR_PRF_HIGH_ADD_ASSEMBLY_REFERENCES`|<span data-ttu-id="116bd-110">控制在 CLR 元件參考結束期間加入元件參考的[ICorProfilerCallback6：： GetAssemblyReference](icorprofilercallback6-getassemblyreferences-method.md)回呼。</span><span class="sxs-lookup"><span data-stu-id="116bd-110">Controls the [ICorProfilerCallback6::GetAssemblyReference](icorprofilercallback6-getassemblyreferences-method.md) callback for adding assembly references during the CLR assembly reference closure walk.</span></span>|  
|`COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED`|<span data-ttu-id="116bd-111">控制與記憶體中模組相關聯之符號資料流程更新的[ICorProfilerCallback7：： ModuleInMemorySymbolsUpdated](icorprofilercallback7-moduleinmemorysymbolsupdated-method.md)回呼。</span><span class="sxs-lookup"><span data-stu-id="116bd-111">Controls the [ICorProfilerCallback7::ModuleInMemorySymbolsUpdated](icorprofilercallback7-moduleinmemorysymbolsupdated-method.md) callback for updates to the symbol stream associated with an in-memory module.</span></span>|  
|`COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS`|<span data-ttu-id="116bd-112">控制[ICorProfilerCallback9：:D ynamicmethodunloaded](icorprofilercallback9-dynamicmethodunloaded-method.md)回呼，以指出動態方法何時已進行垃圾收集和卸載。</span><span class="sxs-lookup"><span data-stu-id="116bd-112">Controls the [ICorProfilerCallback9::DynamicMethodUnloaded](icorprofilercallback9-dynamicmethodunloaded-method.md) callback for indicating when a dynamic method has been garbage collected and unloaded.</span></span> <br/> [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]|
|`COR_PRF_HIGH_DISABLE_TIERED_COMPILATION`|<span data-ttu-id="116bd-113">僅限 .NET Core 3.0 和更新版本：停用分析工具的[分層式編譯](../../../core/whats-new/dotnet-core-3-0.md)。</span><span class="sxs-lookup"><span data-stu-id="116bd-113">.NET Core 3.0 and later versions only: Disables [tiered compilation](../../../core/whats-new/dotnet-core-3-0.md) for profilers.</span></span>|
|`COR_PRF_HIGH_BASIC_GC`|<span data-ttu-id="116bd-114">僅限 .NET Core 3.0 和更新版本：提供比更輕量的 GC 程式碼剖析選項 [`COR_PRF_MONITOR_GC`](cor-prf-monitor-enumeration.md) 。</span><span class="sxs-lookup"><span data-stu-id="116bd-114">.NET Core 3.0 and later versions only: Provides a lightweight GC profiling option compared to [`COR_PRF_MONITOR_GC`](cor-prf-monitor-enumeration.md).</span></span> <span data-ttu-id="116bd-115">僅控制[GarbageCollectionStarted](icorprofilercallback2-garbagecollectionstarted-method.md)、 [GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md)和[GetGenerationBounds](icorprofilerinfo2-getgenerationbounds-method.md)回呼。</span><span class="sxs-lookup"><span data-stu-id="116bd-115">Controls only the  [GarbageCollectionStarted](icorprofilercallback2-garbagecollectionstarted-method.md), [GarbageCollectionFinished](icorprofilercallback2-garbagecollectionfinished-method.md), and [GetGenerationBounds](icorprofilerinfo2-getgenerationbounds-method.md) callbacks.</span></span> <span data-ttu-id="116bd-116">不同于 `COR_PRF_MONITOR_GC` 旗標， `COR_PRF_HIGH_BASIC_GC` 並不會停用並行垃圾收集。</span><span class="sxs-lookup"><span data-stu-id="116bd-116">Unlike the `COR_PRF_MONITOR_GC` flag, `COR_PRF_HIGH_BASIC_GC` does not disable concurrent garbage collection.</span></span>|
|`COR_PRF_HIGH_MONITOR_GC_MOVED_OBJECTS`|<span data-ttu-id="116bd-117">僅限 .NET Core 3.0 和更新版本：僅啟用[MovedReferences](icorprofilercallback-movedreferences-method.md)和[MovedReferences2](icorprofilercallback4-movedreferences2-method.md)回呼來壓縮 gc。</span><span class="sxs-lookup"><span data-stu-id="116bd-117">.NET Core 3.0 and later versions only: Enables the [MovedReferences](icorprofilercallback-movedreferences-method.md) and [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) callbacks for compacting GCs only.</span></span>|
|`COR_PRF_HIGH_MONITOR_LARGEOBJECT_ALLOCATED`|<span data-ttu-id="116bd-118">僅限 .NET Core 3.0 和更新版本：類似 [`COR_PRF_MONITOR_OBJECT_ALLOCATED`](cor-prf-monitor-enumeration.md) ，但只提供大型物件堆積（LOH）之物件配置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="116bd-118">.NET Core 3.0 and later versions only: Similar to [`COR_PRF_MONITOR_OBJECT_ALLOCATED`](cor-prf-monitor-enumeration.md), but provides information on object allocations for the large object heap (LOH) only.</span></span>|
|`COR_PRF_HIGH_REQUIRE_PROFILE_IMAGE`|<span data-ttu-id="116bd-119">代表需要設定檔增強影像的所有 `COR_PRF_HIGH_MONITOR` 旗標。</span><span class="sxs-lookup"><span data-stu-id="116bd-119">Represents all `COR_PRF_HIGH_MONITOR` flags that require profile-enhanced images.</span></span> <span data-ttu-id="116bd-120">它會對應至 `COR_PRF_REQUIRE_PROFILE_IMAGE` [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md)列舉中的旗標。</span><span class="sxs-lookup"><span data-stu-id="116bd-120">It corresponds to the `COR_PRF_REQUIRE_PROFILE_IMAGE` flag in the [COR_PRF_MONITOR](cor-prf-monitor-enumeration.md) enumeration.</span></span>|  
|`COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH`|<span data-ttu-id="116bd-121">代表所有 `COR_PRF_HIGH_MONITOR` 旗標，這些旗標可在分析工具連結至執行中的應用程式之後加以設定。</span><span class="sxs-lookup"><span data-stu-id="116bd-121">Represents all `COR_PRF_HIGH_MONITOR` flags that can be set after the profiler is attached to a running app.</span></span>|  
|`COR_PRF_HIGH_MONITOR_IMMUTABLE`|<span data-ttu-id="116bd-122">代表所有 `COR_PRF_HIGH_MONITOR` 旗標，這些旗標只能在初始化期間加以設定。</span><span class="sxs-lookup"><span data-stu-id="116bd-122">Represents all `COR_PRF_HIGH_MONITOR` flags that can be set only during initialization.</span></span> <span data-ttu-id="116bd-123">嘗試在其他地方變更這些任何旗標，會產生 `HRESULT` 值來指出失敗。</span><span class="sxs-lookup"><span data-stu-id="116bd-123">Trying to change any of these flags elsewhere results in an `HRESULT` value that indicates failure.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="116bd-124">備註</span><span class="sxs-lookup"><span data-stu-id="116bd-124">Remarks</span></span>

<span data-ttu-id="116bd-125">`COR_PRF_HIGH_MONITOR`旗標會搭配 `pdwEventsHigh` [ICorProfilerInfo5：： GetEventMask2](icorprofilerinfo5-geteventmask2-method.md)和[ICorProfilerInfo5：： SetEventMask2](icorprofilerinfo5-seteventmask2-method.md)方法的參數使用。</span><span class="sxs-lookup"><span data-stu-id="116bd-125">The `COR_PRF_HIGH_MONITOR` flags are used with the `pdwEventsHigh` parameter of the [ICorProfilerInfo5::GetEventMask2](icorprofilerinfo5-geteventmask2-method.md) and [ICorProfilerInfo5::SetEventMask2](icorprofilerinfo5-seteventmask2-method.md) methods.</span></span>  
  
<span data-ttu-id="116bd-126">從 .NET Framework 4.6.1 開始，的值 `COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH` 從0變更為 `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` （0x00000002）。</span><span class="sxs-lookup"><span data-stu-id="116bd-126">Starting with the .NET Framework 4.6.1, the value of the `COR_PRF_HIGH_ALLOWABLE_AFTER_ATTACH` changed from 0 to `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` (0x00000002).</span></span> <span data-ttu-id="116bd-127">從 .NET Framework 4.7.2 開始，其值已從變更 `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` 為 `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED | COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS` 。</span><span class="sxs-lookup"><span data-stu-id="116bd-127">Starting with the .NET Framework 4.7.2, its value changed from `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED` to `COR_PRF_HIGH_IN_MEMORY_SYMBOLS_UPDATED | COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS`.</span></span>

<span data-ttu-id="116bd-128">`COR_PRF_HIGH_MONITOR_IMMUTABLE`的目的是一個位元遮罩，代表只能在初始化期間設定的所有旗標。</span><span class="sxs-lookup"><span data-stu-id="116bd-128">`COR_PRF_HIGH_MONITOR_IMMUTABLE` is intended to be a bitmask that represents all flags that can only be set during initialization.</span></span> <span data-ttu-id="116bd-129">嘗試在其他位置變更任何旗標會導致失敗 `HRESULT` 。</span><span class="sxs-lookup"><span data-stu-id="116bd-129">Trying to change any of these flags elsewhere results in a failed `HRESULT`.</span></span>

## <a name="requirements"></a><span data-ttu-id="116bd-130">規格需求</span><span class="sxs-lookup"><span data-stu-id="116bd-130">Requirements</span></span>

<span data-ttu-id="116bd-131">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="116bd-131">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
<span data-ttu-id="116bd-132">**標頭：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="116bd-132">**Header:** CorProf.idl, CorProf.h</span></span>  
  
<span data-ttu-id="116bd-133">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="116bd-133">**Library:** CorGuids.lib</span></span>  
  
<span data-ttu-id="116bd-134">**.NET Framework 版本：**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="116bd-134">**.NET Framework Versions:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="116bd-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="116bd-135">See also</span></span>

- [<span data-ttu-id="116bd-136">分析列舉</span><span class="sxs-lookup"><span data-stu-id="116bd-136">Profiling Enumerations</span></span>](profiling-enumerations.md)
- [<span data-ttu-id="116bd-137">COR_PRF_MONITOR 列舉</span><span class="sxs-lookup"><span data-stu-id="116bd-137">COR_PRF_MONITOR Enumeration</span></span>](cor-prf-monitor-enumeration.md)
- [<span data-ttu-id="116bd-138">ICorProfilerInfo5 介面</span><span class="sxs-lookup"><span data-stu-id="116bd-138">ICorProfilerInfo5 Interface</span></span>](icorprofilerinfo5-interface.md)
