---
title: ICorDebugSymbolProvider2 介面
ms.date: 03/30/2017
ms.assetid: 1c9c3d92-f0de-4d4d-87f1-0c702a4808af
ms.openlocfilehash: 3bef03e9e85224058bc17e1f0ce8746e98aa30f6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95688337"
---
# <a name="icordebugsymbolprovider2-interface"></a>ICorDebugSymbolProvider2 介面

以邏輯方式擴充 [ICorDebugSymbolProvider](icordebugsymbolprovider-interface.md) 介面，以取得其他的 debug 符號資訊。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetFrameProps 方法](icordebugsymbolprovider2-getframeprops-method.md)|傳回某方法啟動相關的虛擬位址，以及被指定程式碼相關的虛擬位址的之父框架。|  
|[GetGenericDictionaryInfo 方法](icordebugsymbolprovider2-getgenericdictionaryinfo-method.md)|擷取泛型字典對應。|  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> 這個介面僅適用於 .NET 原生。 如果您在 .NET 原生之外針對 ICorDebug 案例實作這個介面，Common Language Runtime 會忽略這個介面。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [ICorDebugSymbolProvider 介面](icordebugsymbolprovider-interface.md)
- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
