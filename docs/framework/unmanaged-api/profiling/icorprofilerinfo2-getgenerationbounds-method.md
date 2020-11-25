---
title: ICorProfilerInfo2::GetGenerationBounds 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetGenerationBounds
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetGenerationBounds
helpviewer_keywords:
- ICorProfilerInfo2::GetGenerationBounds method [.NET Framework profiling]
- GetGenerationBounds method [.NET Framework profiling]
ms.assetid: 9c37185f-d1e0-4a6e-8b99-707f7df61d88
topic_type:
- apiref
ms.openlocfilehash: 2b9bf1a9f40764f6d0544bafb91f967905eb40c7
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95703903"
---
# <a name="icorprofilerinfo2getgenerationbounds-method"></a>ICorProfilerInfo2::GetGenerationBounds 方法

取得記憶體區域，也就是堆積的區段，會組成各種記憶體回收層代。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetGenerationBounds(  
    [in]  ULONG cObjectRanges,  
    [out] ULONG *pcObjectRanges,  
    [out, size_is(cObjectRanges), length_is(*pcObjectRanges)] COR_PRF_GC_GENERATION_RANGE ranges[]);  
```  
  
## <a name="parameters"></a>參數  

 `cObjectRanges`  
 [in] 對於 `ranges` 陣列，呼叫端所配置的項目數目 。  
  
 `pcObjectRanges`  
 [out] 指定範圍總數的整數指標，其中某些或全部都將在 `ranges` 陣列傳回。  
  
 `ranges`  
 擴展 [COR_PRF_GC_GENERATION_RANGE](cor-prf-gc-generation-range-structure.md) 結構的陣列，其中每一個都描述一個範圍 (也就是封鎖產生中進行垃圾收集的記憶體) 。  
  
## <a name="remarks"></a>備註  

 `GetGenerationBounds` 方法可以從任何分析工具回呼中呼叫，前提是尚未進行記憶體回收。

 多數層代移位發生在記憶體回收期間。 層代可能會在回收之間成長，但通常不會移動。 因此，呼叫 `GetGenerationBounds` 最有趣的地方位於 `ICorProfilerCallback2::GarbageCollectionStarted` 和 `ICorProfilerCallback2::GarbageCollectionFinished`。  
  
 在程式啟動期間，某些物件會由 Common Language Runtime (CLR) 本身所配置，通常在層代 3 和 0 中。 因此，Managed 程式碼開始執行時，這些層代將已包含物件。 除了由記憶體回收行程所產生的 Dummy 物件之外，層代 1 和 2 通常是空的。  (虛擬物件的大小為 CLR 32 位執行中的12個位元組;64位的實值中的大小較大。 ) 您也可能會在原生映射產生器所產生的模組中看到層代2範圍 ( # A0) 。 在此情況下，層代2中的物件是 *凍結的物件*，當 NGen.exe 執行時（而不是由垃圾收集行程所配置）。  
  
 這個函式會使用呼叫端配置的緩衝區。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerInfo 介面](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 介面](icorprofilerinfo2-interface.md)
- [分析介面](profiling-interfaces.md)
- [程式碼剖析](index.md)
