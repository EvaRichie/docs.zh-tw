---
title: ICorDebugProcess5::GetArrayLayout 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.GetArrayLayout
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::GetArrayLayout
helpviewer_keywords:
- ICorDebugProcess5::GetArrayLayout method [.NET Framework debugging]
- GetArrayLayout method, ICorDebugProcess5 interface [.NET Framework debugging]
ms.assetid: 9a7393b9-9735-43c6-8616-afb103c432fd
topic_type:
- apiref
ms.openlocfilehash: aac3d54d25b50d0e2ce3e93cdfba5a17679e1f76
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209665"
---
# <a name="icordebugprocess5getarraylayout-method"></a>ICorDebugProcess5::GetArrayLayout 方法
提供陣列類型配置的相關資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetArrayLayout(    [in] COR_TYPEID id,     [out] COR_ARRAY_LAYOUT *pLayout);  
```  
  
## <a name="parameters"></a>參數  
 `id`  
 在[COR_TYPEID](cor-typeid-structure.md) token，指定需要其版面配置的陣列。  
  
 `pLayout`  
 脫銷[COR_ARRAY_LAYOUT](cor-array-layout-structure.md)結構的指標，其中包含記憶體中陣列版面配置的相關資訊。  
  
## <a name="remarks"></a>備註  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [ICorDebugProcess5 介面](icordebugprocess5-interface.md)
- [偵錯介面](debugging-interfaces.md)
