---
title: ICorDebugManagedCallback3 介面
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback3
helpviewer_keywords:
- ICorDebugManagedCallback3 interface [.NET Framework debugging]
ms.assetid: a95389d3-cf2e-47a4-9805-61426acc6b65
topic_type:
- apiref
ms.openlocfilehash: 63e3f166c4cbf17f4892dccf770343bfbf6e0284
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209743"
---
# <a name="icordebugmanagedcallback3-interface"></a>ICorDebugManagedCallback3 介面
提供回呼方法，表示已引發啟用的自訂偵錯工具通知。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[CustomNotification 方法](icordebugmanagedcallback3-customnotification-method.md)|表示已引發已啟用的自訂偵錯工具通知。|  
  
## <a name="remarks"></a>備註  
 這個介面是[ICorDebugManagedCallback](icordebugmanagedcallback-interface.md)和[ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)介面的邏輯擴充。  
  
> [!NOTE]
> 這個介面不支援跨電腦或跨處理序的遠端呼叫。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [ICorDebugManagedCallback 介面](icordebugmanagedcallback-interface.md)
- [ICorDebugManagedCallback2 介面](icordebugmanagedcallback2-interface.md)
- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
