---
title: CorDebugIntercept 列舉
ms.date: 03/30/2017
api_name:
- CorDebugIntercept
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugIntercept
helpviewer_keywords:
- CorDebugIntercept enumeration [.NET Framework debugging]
ms.assetid: 3d5b642e-7ef2-428b-a5ae-509c35ed461a
topic_type:
- apiref
ms.openlocfilehash: 3d3d4af8e9ee073c0aefec418a3b53c4589adf0d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729105"
---
# <a name="cordebugintercept-enumeration"></a>CorDebugIntercept 列舉

表示可以攔截這類型的程式碼 (也就是逐步執行)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum CorDebugIntercept {  
    INTERCEPT_NONE                = 0x0,  
    INTERCEPT_CLASS_INIT          = 0x01,  
    INTERCEPT_EXCEPTION_FILTER    = 0x02,  
    INTERCEPT_SECURITY            = 0x04,  
    INTERCEPT_CONTEXT_POLICY      = 0x08,  
    INTERCEPT_INTERCEPTION        = 0x10,  
    INTERCEPT_ALL                 = 0xffff  
} CorDebugIntercept;  
```  
  
## <a name="members"></a>成員  
  
|member|描述|  
|------------|-----------------|  
|`INTERCEPT_NONE`|無法攔截任何程式碼。|  
|`INTERCEPT_CLASS_INIT`|可以攔截建構函式。|  
|`INTERCEPT_EXCEPTION_FILTER`|可以攔截例外狀況篩選條件。|  
|`INTERCEPT_SECURITY`|可以攔截會強制執行安全性的程式碼。|  
|`INTERCEPT_CONTEXT_POLICY`|可以攔截內容原則。|  
|`INTERCEPT_INTERCEPTION`|未使用。|  
|`INTERCEPT_ALL`|可以攔截所有的程式碼。|  
  
## <a name="remarks"></a>備註  

 您可以使用 [ICorDebugStepper：： SetInterceptMask](icordebugstepper-setinterceptmask-method.md) 方法來建立可攔截的程式碼類型。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [偵錯列舉](debugging-enumerations.md)
