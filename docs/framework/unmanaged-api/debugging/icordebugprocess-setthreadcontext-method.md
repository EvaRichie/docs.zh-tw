---
title: ICorDebugProcess::SetThreadContext 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.SetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::SetThreadContext
helpviewer_keywords:
- ICorDebugProcess::SetThreadContext method [.NET Framework debugging]
- SetThreadContext method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: a7b50175-2bf1-40be-8f65-64aec7aa1247
topic_type:
- apiref
ms.openlocfilehash: c9e403dc8cbb75a1e93c426a9e0b3a2083f1f10e
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210458"
---
# <a name="icordebugprocesssetthreadcontext-method"></a>ICorDebugProcess::SetThreadContext 方法
設定這個進程中指定執行緒的內容。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SetThreadContext(  
    [in] DWORD threadID,  
    [in] ULONG32 contextSize,  
    [in, length_is(contextSize), size_is(contextSize)]  
    BYTE context[]);  
```  
  
## <a name="parameters"></a>參數  
 `threadID`  
 在要設定內容的執行緒識別碼。  
  
 `contextSize`  
 [in] `context` 陣列的大小。  
  
 `context`  
 在描述執行緒內容的位元組陣列。  
  
 內容會指定執行緒在其上執行的處理器架構。  
  
## <a name="remarks"></a>備註  
 偵錯工具應該呼叫這個方法，而不是 Win32 函式 `SetThreadContext` ，因為執行緒實際上可能處於「被攔截」狀態，而其內容已暫時變更。 只有線上程是機器碼時，才應該使用這個方法。 針對 managed 程式碼中的執行緒使用[ICorDebugRegisterSet](icordebugregisterset-interface.md) 。 您應該永遠不需要在頻外（OOB） debug 事件期間修改執行緒的內容。  
  
 傳遞的資料必須是目前平臺的內容結構。  
  
 如果未正確使用，這個方法可能會損毀執行時間。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
