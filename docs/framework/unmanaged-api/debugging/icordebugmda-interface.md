---
title: ICorDebugMDA 介面
ms.date: 03/30/2017
api_name:
- ICorDebugMDA
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA
helpviewer_keywords:
- ICorDebugMDA interface [.NET Framework debugging]
ms.assetid: 8ecbb854-295c-4dd4-b9fc-01ebeac46e06
topic_type:
- apiref
ms.openlocfilehash: c4ff28ff1019b5314902a4e71f6d02b5a2fd8d70
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95710827"
---
# <a name="icordebugmda-interface"></a>ICorDebugMDA 介面

表示 Managed 偵錯助理 (MDA) 訊息。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetDescription 方法](icordebugmda-getdescription-method.md)|取得字串，其中包含此 MDA 的描述。|  
|[GetFlags 方法](icordebugmda-getflags-method.md)|取得與此 MDA 相關聯的旗標。|  
|[GetName 方法](icordebugmda-getname-method.md)|取得字串，其中包含此 MDA 的名稱。|  
|[GetOSThreadId 方法](icordebugmda-getosthreadid-method.md)|取得此 MDA 執行時所依據的作業系統執行緒識別碼。|  
|[GetXML 方法](icordebugmda-getxml-method.md)|取得與此 MDA 相關聯的完整 XML 資料流程。|  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> 這個介面不支援跨電腦或跨處理序的遠端呼叫。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [偵錯介面](debugging-interfaces.md)
- [診斷 Managed 偵錯助理的錯誤](../../debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
