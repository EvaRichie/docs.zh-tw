---
title: ICorDebugBlockingObjectEnum::Next 方法
ms.date: 03/30/2017
api_name:
- ICorDebugBlockingObjectEnum.Next Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBlockingObjectEnum::Next
helpviewer_keywords:
- Next method, ICorDebugBlockingObjectEnum interface [.NET Framework debugging]
- ICorDebugBlockingObjectEnum::Next method [.NET Framework debugging]
ms.assetid: 0121753f-ebea-48d0-aeb2-ed7fda76dc60
topic_type:
- apiref
ms.openlocfilehash: 0ef49d2d833841eac62b2b964a0fdc902b4fb6a9
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894764"
---
# <a name="icordebugblockingobjectenumnext-method"></a>ICorDebugBlockingObjectEnum::Next 方法
從列舉中取得指定數目的[CorDebugBlockingObject](cordebugblockingobject-structure.md)物件，從目前位置開始。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT Next([in] ULONG  celt,  
             [out, size_is(celt), length_is(*pceltFetched)]  
                           CorDebugBlockingObject values[],  
             [out] ULONG *pceltFetched;  
```  
  
## <a name="parameters"></a>參數  
 `celt`  
 在要取得的物件數目。  
  
 `values`  
 脫銷[CorDebugBlockingObject](cordebugblockingobject-structure.md)物件的指標陣列。  
  
 `pceltFetched`  
 脫銷已抓取物件數目的指標。  
  
## <a name="return-value"></a>傳回值  
 這個方法會傳回下列特定的 HRESULT。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|已成功完成命令。|  
|S_FALSE|`pceltFetched` 不等於 `celt`。|  
  
## <a name="remarks"></a>備註  
 這個方法的功能就像一般的 COM 列舉值。  
  
 輸入陣列值的大小`celt`至少必須為。 陣列將會填入列舉中的下一個`celt`值，或所有剩餘的值（如果少於`celt`保留）。 當這個方法傳回時`pceltFetched` ，將會填入已抓取的值數目。 如果`values`包含不正確指標或指向小於`celt`的緩衝區，或如果`pceltFetched`是不正確指標，則結果會是未定義的。  
  
> [!NOTE]
> 雖然不需要釋放[CorDebugBlockingObject](cordebugblockingobject-structure.md)結構，但它裡面的 "ICorDebugValue" 介面必須釋放。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorDebugDataTarget 介面](icordebugdatatarget-interface.md)
- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
