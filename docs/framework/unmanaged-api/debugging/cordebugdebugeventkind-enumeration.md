---
title: CorDebugDebugEventKind 列舉
ms.date: 03/30/2017
api_name:
- CorDebugDebugEventKind
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 6075a6cd-97e6-4472-a090-0dd14860d1f3
topic_type:
- apiref
ms.openlocfilehash: b7db7c9e17d87b91e09d5d010d40431cba5385df
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795985"
---
# <a name="cordebugdebugeventkind-enumeration"></a>CorDebugDebugEventKind 列舉
表示[DecodeEvent](icordebugprocess6-decodeevent-method.md)方法解碼其資訊的事件種類。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum CorDebugDebugEventKind {  
    DEBUG_EVENT_KIND_MODULE_LOADED                          = 1,  
    DEBUG_EVENT_KIND_MODULE_UNLOADED                        = 2,  
    DEBUG_EVENT_KIND_MANAGED_EXCEPTION_FIRST_CHANCE         = 3,  
    DEBUG_EVENT_KIND_MANAGED_EXCEPTION_USER_FIRST_CHANCE    = 4,  
    DEBUG_EVENT_KIND_MANAGED_EXCEPTION_CATCH_HANDLER_FOUND  = 5,  
    DEBUG_EVENT_KIND_MANAGED_EXCEPTION_UNHANDLED            = 6  
} CorDebugRecordFormat;  
```  
  
## <a name="members"></a>成員  
  
|member|說明|  
|------------|-----------------|  
|`DEBUG_EVENT_KIND_MODULE_LOADED`|模組載入事件。|  
|`DEBUG_EVENT_KIND_MODULE_UNLOADED`|模組卸載事件。|  
|`DEBUG_EVENT_KIND_MANAGED_EXCEPTION_FIRST_CHANCE`|第一個可能發生的例外狀況。|  
|`DEBUG_EVENT_KIND_MANAGED_EXCEPTION_USER_FIRST_CHANCE`|第一個可能發生的使用者例外狀況。|  
|`DEBUG_EVENT_KIND_MANAGED_EXCEPTION_CATCH_HANDLER_FOUND`|存在 `catch` 處理常式的例外狀況。|  
|`DEBUG_EVENT_KIND_MANAGED_EXCEPTION_UNHANDLED`|未處理的例外狀況。|  
  
## <a name="remarks"></a>備註  
 `CorDebugDebugEventKind`列舉的成員會藉由呼叫[ICorDebugDebugEvent：： GetEventKind](icordebugdebugevent-geteventkind-method.md)方法來傳回。  
  
> [!NOTE]
> 這個列舉僅適用於 .NET Native 偵錯案例。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>請參閱

- [偵錯列舉](debugging-enumerations.md)
