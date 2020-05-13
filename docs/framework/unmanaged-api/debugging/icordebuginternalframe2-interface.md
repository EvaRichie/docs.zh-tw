---
title: ICorDebugInternalFrame2 介面
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame2
helpviewer_keywords:
- ICorDebugInternalFrame2 interface [.NET Framework debugging]
ms.assetid: d4755569-85b8-4ff4-bf50-0e608e76429f
topic_type:
- apiref
ms.openlocfilehash: ce3ca4745727a1738fdc1a526480d70ffc55ccf8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209899"
---
# <a name="icordebuginternalframe2-interface"></a>ICorDebugInternalFrame2 介面
提供內部框架的相關資訊，包括堆疊位址，以及相對於 ICorDebugFrame 物件的位置。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetFrameAddress 方法](icordebuginternalframe2-getframeaddress-method.md)|傳回內部框架的堆疊位址。|  
|[IsCloserToLeaf 方法](icordebuginternalframe2-isclosertoleaf-method.md)|檢查 `this` 內部框架是否比指定的 ICorDebugFrame 物件更接近分葉。|  
  
## <a name="remarks"></a>備註  
 這個介面會擴充 ICorDebugInternalFrame 介面。  
  
> [!NOTE]
> 這個介面不支援跨電腦或跨處理序的遠端呼叫。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
