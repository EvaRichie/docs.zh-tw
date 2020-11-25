---
title: ICorDebugModule3 介面
ms.date: 03/30/2017
api_name:
- ICorDebugModule3
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule3
helpviewer_keywords:
- ICorDebugModule3 interface [.NET Framework debugging]
ms.assetid: 0b69f945-263a-4e11-8512-89d27f6ea296
topic_type:
- apiref
ms.openlocfilehash: 543a1a3c79b6cf3eb799da5844f35286dfa91940
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95709553"
---
# <a name="icordebugmodule3-interface"></a>ICorDebugModule3 介面

建立動態模組的符號讀取器。  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
interface ICorDebugModule3 : IUnknown  
{  
    HRESULT CreateReaderForInMemorySymbols  
      (  
      [in] REFIID riid,  
      [out][iid_is(riid)] void **  ppObj  
      );  
};  
```  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[ICorDebugModule3::CreateReaderForInMemorySymbols 方法](icordebugmodule3-createreaderforinmemorysymbols-method.md)|建立符號讀取器 (通常會 ISymUnmanagedReader 動態模組的 [介面](../diagnostics/isymunmanagedreader-interface.md)) 。|  
  
## <a name="remarks"></a>備註  

 這個介面會以邏輯方式擴充 "ICorDebugModule" 和 "ICorDebugModule2" 介面。  
  
> [!NOTE]
> 這個介面不支援跨電腦或跨處理序的遠端呼叫。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：** 4.5、4、3.5 SP1
  
## <a name="see-also"></a>另請參閱

- [ICorDebugRemoteTarget 介面](icordebugremotetarget-interface.md)
- [ICorDebug 介面](icordebug-interface.md)

- [偵錯介面](debugging-interfaces.md)
