---
title: ICorDebugStackWalk::SetContext 方法
ms.date: 03/30/2017
api_name:
- ICorDebugStackWalk.SetContext Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStackWalk::SetContext
helpviewer_keywords:
- SetContext method [.NET Framework debugging]
- ICorDebugStackWalk::SetContext method [.NET Framework debugging]
ms.assetid: bac0b156-31a3-4e7f-be4d-ab21789c81f1
topic_type:
- apiref
ms.openlocfilehash: 1ae9fc1f1154866945d40cd63042fa8a43b88905
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95677293"
---
# <a name="icordebugstackwalksetcontext-method"></a>ICorDebugStackWalk::SetContext 方法

將 [ICorDebugStackWalk](icordebugstackwalk-interface.md) 物件的目前內容設定為執行緒的有效內容。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SetContext([in] CorDebugSetContextFlag flag,  
                   [in] ULONG32 contextSize,  
                   [in, size_is(contextSize)] BYTE context[]);  
```  
  
## <a name="parameters"></a>參數  

 `flag`  
 在 [CorDebugSetCoNtextFlag](cordebugsetcontextflag-enumeration.md) 旗標，指出內容是否來自堆疊上的作用中框架，或回溯堆疊所取得的內容。  
  
 `contextSize`  
 在緩衝區的配置大小 `CONTEXT` 。  
  
 `context`  
 在 `CONTEXT` 緩衝區。  
  
## <a name="return-value"></a>傳回值  

 這個方法會傳回下列特定的 HRESULT，以及表示方法失敗的 HRESULT 錯誤。  
  
|HRESULT|描述|  
|-------------|-----------------|  
|S_OK|已 `ICorDebugStackWalk` 成功設定物件的內容。|  
|E_FAIL|`ICorDebugStackWalk`未設定物件的內容。|  
|E_INVALIDARG|內容為 null。|  
|HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER)|內容緩衝區太小。|  
  
## <a name="exceptions"></a>例外  
  
## <a name="remarks"></a>備註  

 這個方法不會改變執行緒的目前內容。  
  
 將目前的內容設定為不正確內容，可能會導致堆疊遍歷程式無法預期的結果。  
  
 您可以立即呼叫 [ICorDebugStackWalk：： GetCoNtext](icordebugstackwalk-getcontext-method.md) 方法，以取得此內容的精確位複製。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
