---
title: ICorDebugManagedCallback::LoadModule 方法
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.LoadModule
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::LoadModule
helpviewer_keywords:
- ICorDebugManagedCallback::LoadModule method [.NET Framework debugging]
- LoadModule method [.NET Framework debugging]
ms.assetid: 66ec04e9-87cb-42ce-9720-81522abb5d5a
topic_type:
- apiref
ms.openlocfilehash: cd4a16bc8b48f147ed03555b51eee5f42a445bc6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212694"
---
# <a name="icordebugmanagedcallbackloadmodule-method"></a>ICorDebugManagedCallback::LoadModule 方法
通知偵錯工具已成功載入 common language runtime （CLR）模組。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT LoadModule (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugModule    *pModule  
);  
```  
  
## <a name="parameters"></a>參數  
 `pAppDomain`  
 在代表已載入模組之應用程式域的 ICorDebugAppDomain 物件指標。  
  
 `pModule`  
 在代表 CLR 模組之 ICorDebugModule 物件的指標。  
  
## <a name="remarks"></a>備註  
 `LoadModule`回呼會提供適當時間來檢查模組的中繼資料、設定即時（JIT）編譯器旗標，或啟用或停用模組的類別載入回呼。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [UnloadModule 方法](icordebugmanagedcallback-unloadmodule-method.md)
- [ICorDebugManagedCallback 介面](icordebugmanagedcallback-interface.md)
