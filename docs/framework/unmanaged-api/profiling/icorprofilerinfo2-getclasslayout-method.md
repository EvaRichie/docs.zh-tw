---
title: ICorProfilerInfo2::GetClassLayout 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetClassLayout
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetClassLayout
helpviewer_keywords:
- ICorProfilerInfo2::GetClassLayout method [.NET Framework profiling]
- GetClassLayout method, ICorProfilerInfo2 interface [.NET Framework profiling]
ms.assetid: a3a36987-5666-4e2f-95b5-d0cb246502ec
topic_type:
- apiref
ms.openlocfilehash: a2bac05e7471a0df8d624bf5dfbe2aa58c25cf4c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95727168"
---
# <a name="icorprofilerinfo2getclasslayout-method"></a>ICorProfilerInfo2::GetClassLayout 方法

取得在記憶體中指定類別所定義欄位的配置相關資訊。 也就是說，這個方法會取得此類別的欄位之位移。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetClassLayout(  
    [in]  ClassID classID,  
    [in, out] COR_FIELD_OFFSET rFieldOffset[],  
    [in]  ULONG cFieldOffset,  
    [out] ULONG *pcFieldOffset,  
    [out] ULONG *pulClassSize);  
```  
  
## <a name="parameters"></a>參數  

 `classID`  
 [in] 要擷取配置的類別 ID。  
  
 `rFieldOffset`  
 [in，out] [COR_FIELD_OFFSET](../metadata/cor-field-offset-structure.md) 結構的陣列，其中每個結構都包含類別欄位的標記和位移。  
  
 `cFieldOffset`  
 [in] `rFieldOffset` 陣列的大小。  
  
 `pcFieldOffset`  
 [out] 可用的項目總數之指標。 如果 `cFieldOffset` 是 0，則這個值表示所需的項目數目。  
  
 `pulClassSize`  
 [out] 位置指標，其中包含此類別的大小，以位元組為單位。  
  
## <a name="remarks"></a>備註  

 `GetClassLayout` 方法僅傳回類別本身所定義的欄位。 如果類別的父類別也已經定義欄位，則分析工具必須呼叫父類別上的 `GetClassLayout` 來取得那些欄位。  
  
 如果您搭配字串類別使用 `GetClassLayout`，則該方法會失敗，伴隨錯誤碼 E_INVALIDARG。 使用 [ICorProfilerInfo2：： GetStringLayout](icorprofilerinfo2-getstringlayout-method.md) 取得字串配置的相關資訊。 以陣列類別呼叫 `GetClassLayout` 時也會失敗。  
  
 `GetClassLayout` 傳回之後，您必須確認 `rFieldOffset` 緩衝區夠大，可以包含所有可用的 `COR_FIELD_OFFSET` 結構。 若要這樣做，比對 `pcFieldOffset` 指向的值和 `rFieldOffset` 的大小除以 `COR_FIELD_OFFSET` 的結構大小。 如果 `rFieldOffset` 不夠大，則請配置一個更大的 `rFieldOffset` 緩衝區，以新的、較大的大小來更新 `cFieldOffset`，然後再呼叫 `GetClassLayout` 一次。  
  
 或者，您也可以先使用長度為零的 `rFieldOffset` 緩衝區來呼叫 `GetClassLayout`，以取得正確的緩衝區大小。 接著您就可以將緩衝區大小設定為 `pcFieldOffset` 中傳回的值，並再次呼叫 `GetClassLayout`。  
  
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
