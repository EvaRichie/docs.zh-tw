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
# <a name="icorprofilercallback4survivingreferences2-method"></a>ICorProfilerCallback4::SurvivingReferences2 方法

報告非壓縮記憶體回收造成的堆積中物件配置。 如果分析工具已執行 [ICorProfilerCallback4](icorprofilercallback4-interface.md) 介面，則會呼叫這個方法。 此回呼會取代 [ICorProfilerCallback2：： SurvivingReferences](icorprofilercallback2-survivingreferences-method.md) 方法，因為它可以報告其長度超過 ULONG 中可表示之物件的較大範圍。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SurvivingReferences2(  
    [in] ULONG  cSurvivingObjectIDRanges,  
    [in, size_is(cSurvivingObjectIDRanges)] ObjectID  
                objectIDRangeStart[] ,  
    [in, size_is(cSurvivingObjectIDRanges)] SIZE_T  
                cObjectIDRangeLength[] );  
```  
  
## <a name="parameters"></a>參數  

 `cSurvivingObjectIDRanges`  
 [in] 非壓縮記憶體回收後未被回收的連續物件區塊數目。 也就是說，`cSurvivingObjectIDRanges` 的值是 `objectIDRangeStart` 和 `cObjectIDRangeLength` 陣列的大小，會為每個物件區塊分別存放 `ObjectID` 和長度。  
  
 `SurvivingReferences2` 的下兩個引數是平行陣列。 換句話說，`objectIDRangeStart` 和 `cObjectIDRangeLength` 會考量連續物件的相同區塊。  
  
 `objectIDRangeStart`  
 [in] `ObjectID` 值的陣列，其中每一個都是記憶體中連續即時物件之區塊的開始位址。  
  
 `cObjectIDRangeLength`  
 [in] 整數的陣列，其中每一個都是記憶體中連續物件之未被回收區塊的大小。  
  
 已為 `objectIDRangeStart` 陣列中被參考的每個區塊指定大小。  
  
## <a name="remarks"></a>備註  

 `objectIDRangeStart` 和 `cObjectIDRangeLength` 陣列的項目應解譯如下，以判斷物件是否未被記憶體回收。 假定 `ObjectID` 的值 (`ObjectID`) 位於下列範圍內：  
  
 `ObjectIDRangeStart[i]` <= `ObjectID` < `ObjectIDRangeStart[i]` + `cObjectIDRangeLength[i]`  
  
 針對任何位於下列範圍內的 `i` 之值，該物件尚未被記憶體回收：  
  
 0 <= `i` < `cSurvivingObjectIDRanges`  
  
 非壓縮記憶體回收會回收「無作用」物件所佔用的記憶體，但是不會壓縮該釋放的空間。 因此，記憶體會傳回到堆積，但沒有移動「即時」物件。  
  
 針對非壓縮記憶體回收，Common Language Runtime (CLR) 會呼叫 `SurvivingReferences2`。 針對壓縮垃圾收集，會改為呼叫 [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) 。 單一記憶體回收可以為了某個層代而壓縮，但另一個則不壓縮。 針對任何特定世代的垃圾收集，分析工具會收到 `SurvivingReferences2` 回呼或 [MovedReferences2](icorprofilercallback4-movedreferences2-method.md) 回呼，但不能同時接收兩者。  
  
 因為有限的內部緩衝區、伺服器記憶體回收期間的多重回呼和其他原因，在特定記憶體回收期間可能接收多重 `SurvivingReferences2` 回呼。 在記憶體回收期間多個回呼的情況下，資訊是累計的；在任何 `SurvivingReferences2` 回呼中被報告的所有參考不會被記憶體回收。  
  
 如果 profiler 同時執行 [ICorProfilerCallback](icorprofilercallback-interface.md) 和 [ICorProfilerCallback4](icorprofilercallback4-interface.md) 介面，則 `SurvivingReferences2` 會在 [ICorProfilerCallback2：： SurvivingReferences](icorprofilercallback2-survivingreferences-method.md) 方法之前呼叫方法，但只有在成功傳回時才會呼叫方法 `SurvivingReferences2` 。 分析工具可傳回 HRESULT，表示 `SurvivingReferences2` 方法中的失敗，以避免呼叫第二個方法。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerCallback 介面](icorprofilercallback-interface.md)
- [ICorProfilerCallback2 介面](icorprofilercallback2-interface.md)
- [ICorProfilerCallback4 介面](icorprofilercallback4-interface.md)
