---
title: ICorDebugValue2 介面
ms.date: 03/30/2017
api_name:
- ICorDebugValue2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue2
helpviewer_keywords:
- ICorDebugValue2 interface [.NET Framework debugging]
ms.assetid: 3ff2ad2a-da5a-461b-8627-1a8eba49df9c
topic_type:
- apiref
ms.openlocfilehash: d036ddf353aa3a622ade05e1e2daa7f170d28f63
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396782"
---
# <a name="icordebugvalue2-interface"></a>ICorDebugValue2 介面
擴充 "ICorDebugValue" 介面，以提供對 "ICorDebugType" 物件的支援。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetExactType 方法](icordebugvalue2-getexacttype-method.md)|取得 `ICorDebugType` 物件的介面指標，表示 <xref:System.Type> 這個值的。|  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> 這個介面不支援跨電腦或跨處理序的遠端呼叫。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [偵錯介面](debugging-interfaces.md)

- [ICorDebugValue3 介面](icordebugvalue3-interface.md)
