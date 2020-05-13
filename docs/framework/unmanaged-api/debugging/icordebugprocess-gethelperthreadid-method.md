---
title: ICorDebugProcess::GetHelperThreadID 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.GetHelperThreadID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::GetHelperThreadID
helpviewer_keywords:
- GetHelperThreadID method [.NET Framework debugging]
- ICorDebugProcess::GetHelperThreadID method [.NET Framework debugging]
ms.assetid: 84e1e605-37c1-49a5-8e12-35db85654622
topic_type:
- apiref
ms.openlocfilehash: fc4f4b56552c4db265d2ea123a84c7792ad53094
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213630"
---
# <a name="icordebugprocessgethelperthreadid-method"></a>ICorDebugProcess::GetHelperThreadID 方法
取得偵錯工具內部 helper 執行緒的作業系統（OS）執行緒識別碼。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetHelperThreadID (  
    [out] DWORD *pThreadID  
);  
```  
  
## <a name="parameters"></a>參數  
 `pThreadID`  
 脫銷偵錯工具內部 helper 執行緒的 OS 執行緒識別碼指標。  
  
## <a name="remarks"></a>備註  
 在受控和非受控的調試過程中，偵錯工具必須負責確保具有指定識別碼的執行緒在到達偵錯工具所放置的中斷點時，仍會繼續運作。 偵錯工具可能也會想要從使用者隱藏此執行緒。 如果進程中尚未有 helper 執行緒，此方法會 `GetHelperThreadID` 在 * 中傳回零 `pThreadID` 。  
  
 您無法快取 helper 執行緒的執行緒識別碼，因為它可能會隨著時間而改變。 您必須在每個停止事件時重新查詢執行緒識別碼。  
  
 偵錯工具 helper 執行緒的執行緒識別碼在每個非受控[ICorDebugManagedCallback：： CreateThread](icordebugmanagedcallback-createthread-method.md)事件中都是正確的，因此可讓偵錯工具判斷其 helper 執行緒的執行緒識別碼，並將其從使用者中隱藏。 在非受控事件期間識別為 helper 執行緒的執行緒， `ICorDebugManagedCallback::CreateThread` 將永遠不會執行 managed 使用者程式碼。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Cordebug.h .idl。 Cordebug.h。h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
