---
title: ICorProfilerFunctionEnum::Next 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionEnum.Next Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionEnum::Next
helpviewer_keywords:
- ICorProfilerFunctionEnum::Next method [.NET Framework profiling]
- Next method, ICorProfilerFunctionEnum interface [.NET Framework profiling]
ms.assetid: 5ed4aa83-ce56-4b9f-9237-5da7587787fe
topic_type:
- apiref
ms.openlocfilehash: df62ad1af0ea91783cb62bb0590b6e36d812de3a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503064"
---
# <a name="icorprofilerfunctionenumnext-method"></a>ICorProfilerFunctionEnum::Next 方法
從循序函式集合中取得指定的連續函式數目，從序列中列舉值的目前位置開始。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT Next([in]  ULONG      celt,  
             [out, size_is(celt), length_is(*pceltFetched)]  
                    COR_PRF_FUNCTION ids[],  
             [out] ULONG *   pceltFetched);  
```  
  
## <a name="parameters"></a>參數  
 `celt`  
 [in] 要擷取的函式數目。  
  
 `ids`  
 [out] `COR_PRF_FUNCTION` 值的陣列，每個值各代表一個擷取的函式。  
  
 `pceltFetched`  
 [out] `ids` 陣列中實際傳回之函式數目的指標。  
  
## <a name="return-value"></a>傳回值  
 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|說明|  
|-------------|-----------------|  
|S_OK|已傳回 `celt` 項目。|  
|S_FALSE|傳回少於 `celt` 的項目數，表示列舉已完成。|  
  
## <a name="requirements"></a>規格需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorProfilerFunctionEnum 介面](icorprofilerfunctionenum-interface.md)
- [分析介面](profiling-interfaces.md)
