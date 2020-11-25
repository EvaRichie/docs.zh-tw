---
title: IAssemblyCache 介面
ms.date: 03/30/2017
api_name:
- IAssemblyCache
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCache
helpviewer_keywords:
- IAssemblyCache interface [.NET Framework fusion]
ms.assetid: 71ea170f-872d-4fc5-81b6-27da1dec9b19
topic_type:
- apiref
ms.openlocfilehash: df4f0ba018b55202c22cb90b22b927a9c426c4ed
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95696852"
---
# <a name="iassemblycache-interface"></a>IAssemblyCache 介面

代表融合技術所使用的全域組件快取。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[CreateAssemblyCacheItem 方法](iassemblycache-createassemblycacheitem-method.md)|取得新 [IAssemblyCacheItem](iassemblycacheitem-interface.md)的參考。|  
|[CreateAssemblyScavenger 方法](iassemblycache-createassemblyscavenger-method.md)|保留供融合技術內部使用。|  
|[InstallAssembly 方法](iassemblycache-installassembly-method.md)|在全域組件快取中安裝指定的元件。|  
|[QueryAssemblyInfo 方法](iassemblycache-queryassemblyinfo-method.md)|取得所要求有關指定元件的資料。|  
|[UninstallAssembly 方法](iassemblycache-uninstallassembly-method.md)|從全域組件快取卸載指定的元件。|  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** 融合。h  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [融合介面](fusion-interfaces.md)
- [全域組件快取](../../app-domains/gac.md)
