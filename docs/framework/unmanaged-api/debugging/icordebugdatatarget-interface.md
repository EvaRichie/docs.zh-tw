---
title: ICorDebugDataTarget 介面
ms.date: 03/30/2017
api_name:
- ICorDebugDataTarget
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugDataTarget
helpviewer_keywords:
- ICorDebugDataTarget interface [.NET Framework debugging]
ms.assetid: df5f05be-bed7-4f3c-bc89-dbb435d79a0b
topic_type:
- apiref
ms.openlocfilehash: 54272dd18a12715bab58ec1b1a4c1dc00e4bf12b
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976521"
---
# <a name="icordebugdatatarget-interface"></a>ICorDebugDataTarget 介面
提供回呼介面，該介面可供存取特定的目標處理序。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetPlatform 方法](icordebugdatatarget-getplatform-method.md)|提供目標進程執行所在平臺的相關資訊，包括處理器架構和作業系統。|  
|[ReadVirtual 方法](icordebugdatatarget-readvirtual-method.md)|從指定的位址開始，取得連續記憶體的區塊，並將它傳回給提供的緩衝區。|  
|[GetThreadContext 方法](icordebugdatatarget-getthreadcontext-method.md)|要求指定之執行緒的目前線程內容。|  
  
## <a name="remarks"></a>備註  
 `ICorDebugDataTarget`和其方法具有下列特性：  
  
- 偵錯工具會呼叫這個介面上的方法，以存取目標進程中的記憶體和其他資料。  
  
- 偵錯工具用戶端必須將此介面實作為特定目標的適當（例如，即時進程或記憶體傾印）。  
  
- 只能`ICorDebugDataTarget`從在其他`ICorDebug*`介面中實作為方法來叫用方法。 這可確保偵錯工具用戶端能夠控制要在哪一個執行緒上叫用它，以及何時。  
  
- `ICorDebugDataTarget`執行必須一律傳回有關目標的最新資訊。  
  
 在呼叫介面（也就是`ICorDebug*` `ICorDebugDataTarget`方法）時，目標進程應該會停止，而且不會以任何方式變更。 如果目標是即時進程且其狀態變更，必須再次呼叫[ICLRDebugging：： OpenVirtualProcess](iclrdebugging-openvirtualprocess-method.md)方法，以提供取代 ICorDebugProcess 實例。  
  
> [!NOTE]
> 這個介面不支援跨電腦或跨處理序的遠端呼叫。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
