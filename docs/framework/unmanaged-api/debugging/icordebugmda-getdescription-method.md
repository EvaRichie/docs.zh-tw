---
title: ICorDebugMDA::GetDescription 方法
ms.date: 03/30/2017
api_name:
- ICorDebugMDA.GetDescription
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA::GetDescription
helpviewer_keywords:
- GetDescription method [.NET Framework debugging]
- ICorDebugMDA::GetDescription method [.NET Framework debugging]
ms.assetid: 01d1b481-ca67-4712-8744-d342ec0df639
topic_type:
- apiref
ms.openlocfilehash: 522e992e6d7e9a64f7590bbec0e9106e0e1f8f47
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212135"
---
# <a name="icordebugmdagetdescription-method"></a>ICorDebugMDA::GetDescription 方法
取得字串，其中包含[ICorDebugMDA](icordebugmda-interface.md)所代表的 managed 偵錯工具（MDA）的描述。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetDescription (  
    [in] ULONG32   cchName,  
    [out] ULONG32  *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
        WCHAR      szName[]  
);  
```  
  
## <a name="parameters"></a>參數  
 `cchName`  
 在將儲存描述的字串緩衝區大小。  
  
 `pcchName`  
 脫銷字串緩衝區中傳回之位元組數的指標。  
  
 `szName`  
 脫銷包含 MDA 描述的字串緩衝區。  
  
## <a name="remarks"></a>備註  
 字串的長度可以是零。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [ICorDebugMDA 介面](icordebugmda-interface.md)
- [使用 Managed 偵錯助理診斷錯誤](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
