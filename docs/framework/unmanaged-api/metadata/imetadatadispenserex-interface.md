---
title: IMetaDataDispenserEx 介面
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx
helpviewer_keywords:
- IMetaDataDispenserEx interface [.NET Framework metadata]
ms.assetid: 78b3629e-77a2-4406-89c3-56b5cc2c4594
topic_type:
- apiref
ms.openlocfilehash: 96f0c0c254ce255581ac2937c805096918ab29e8
ms.sourcegitcommit: 03fec33630b46e78d5e81e91b40518f32c4bd7b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/27/2020
ms.locfileid: "84008049"
---
# <a name="imetadatadispenserex-interface"></a>IMetaDataDispenserEx 介面
擴充[IMetaDataDispenser 介面](imetadatadispenser-interface.md)介面，以提供可控制中繼資料 api 如何在目前中繼資料範圍上運作的功能。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[FindAssembly 方法](imetadatadispenserex-findassembly-method.md)|這個方法尚未實作。 如果呼叫，它會傳回 E_NOTIMPL。|  
|[FindAssemblyModule 方法](imetadatadispenserex-findassemblymodule-method.md)|這個方法尚未實作。 如果呼叫，它會傳回 E_NOTIMPL。|  
|[GetCORSystemDirectory 方法](imetadatadispenserex-getcorsystemdirectory-method.md)|取得保存目前 common language runtime （CLR）的目錄。 這個方法僅支援跨進程偵錯工具使用。 如果從另一個元件呼叫，它會傳回 E_NOTIMPL。|  
|[GetOption 方法](imetadatadispenserex-getoption-method.md)|取得目前中繼資料範圍中指定之選項的值。 選項會控制如何處理對目前中繼資料範圍的呼叫。|  
|[OpenScopeOnITypeInfo 方法](imetadatadispenserex-openscopeonitypeinfo-method.md)|這個方法尚未實作。 如果呼叫，它會傳回 E_NOTIMPL。|  
|[SetOption 方法](imetadatadispenserex-setoption-method.md)|針對目前的中繼資料範圍，將指定的選項設定為指定的值。 選項會控制如何處理對目前中繼資料範圍的呼叫。|  
  
## <a name="requirements"></a>需求  
 **平臺：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Cor。h  
  
 連結**庫：** 做為 Mscoree.dll 中的資源使用  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [中繼資料介面](metadata-interfaces.md)
- [IMetaDataDispenser 介面](imetadatadispenser-interface.md)
- [IMetaDataEmit 介面](imetadataemit-interface.md)
- [IMetaDataImport 介面](imetadataimport-interface.md)
