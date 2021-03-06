---
title: IMetaDataDispenser::DefineScope 方法
ms.date: 03/30/2017
api_name:
- IMetaDataDispenser.DefineScope
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenser::DefineScope
helpviewer_keywords:
- DefineScope method [.NET Framework metadata]
- IMetaDataDispenser::DefineScope method [.NET Framework metadata]
ms.assetid: af28db02-29af-45ac-aec6-8d6c6123c2ff
topic_type:
- apiref
ms.openlocfilehash: 87a39350986cb7bb62f76b0d9a6a9aae8f82e2f9
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726089"
---
# <a name="imetadatadispenserdefinescope-method"></a>IMetaDataDispenser::DefineScope 方法

在記憶體中建立新的區域，您可以在其中建立新的中繼資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT DefineScope (  
    [in]  REFCLSID    rclsid,  
    [in]  DWORD       dwCreateFlags,  
    [in]  REFIID      riid,
    [out] IUnknown    **ppIUnk  
);  
```  
  
## <a name="parameters"></a>參數  

 `rclsid`  
 在要建立之元資料結構版本的 CLSID。 此值必須是 .NET Framework 2.0 版的 CLSID_CorMetaDataRuntime。  
  
 `dwCreateFlags`  
 在指定選項的旗標。 .NET Framework 2.0 的這個值必須是零。  
  
 `riid`  
 在要傳回之所需中繼資料介面的 IID;呼叫端會使用介面來建立新的中繼資料。  
  
 的值 `riid` 必須指定其中一個「發出」介面。 有效的值為 IID_IMetaDataEmit、IID_IMetaDataAssemblyEmit 或 IID_IMetaDataEmit2。  
  
 `ppIUnk`  
 擴展傳回之介面的指標。  
  
## <a name="remarks"></a>備註  

 `DefineScope` 建立一組記憶體中的中繼資料資料表、產生唯一 GUID (模組版本識別碼，或中繼資料的 MVID) ，然後在模組資料表中為所發出的編譯單位建立一個專案。  
  
 您可以視需要使用 [IMetaDataEmit：： SetModuleProps](imetadataemit-setmoduleprops-method.md) 或 [IMetaDataEmit：:D efinecustomattribute](imetadataemit-definecustomattribute-method.md) 方法，將屬性附加至整個中繼資料範圍。  
  
## <a name="requirements"></a>需求  

 **平臺：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Cor。h  
  
 連結 **庫：** 當做 MsCorEE.dll 中的資源使用  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [IMetaDataDispenser 介面](imetadatadispenser-interface.md)
- [IMetaDataDispenserEx 介面](imetadatadispenserex-interface.md)
- [IMetaDataAssemblyEmit 介面](imetadataassemblyemit-interface.md)
- [IMetaDataEmit 介面](imetadataemit-interface.md)
- [IMetaDataEmit2 介面](imetadataemit2-interface.md)
