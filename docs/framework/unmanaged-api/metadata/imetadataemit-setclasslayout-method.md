---
title: IMetaDataEmit::SetClassLayout 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetClassLayout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetClassLayout
helpviewer_keywords:
- IMetaDataEmit::SetClassLayout method [.NET Framework metadata]
- SetClassLayout method [.NET Framework metadata]
ms.assetid: 2576c449-388d-4434-a0e1-9f53991e11b6
topic_type:
- apiref
ms.openlocfilehash: ee10907fb7f5d90db1bdce845272cd3de38e35a6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95718692"
---
# <a name="imetadataemitsetclasslayout-method"></a>IMetaDataEmit::SetClassLayout 方法

完成先前呼叫 [DefineTypeDef 方法](imetadataemit-definetypedef-method.md)所定義之類別的欄位版面配置。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT SetClassLayout (  
    [in]  mdTypeDef           td,
    [in]  DWORD               dwPackSize,
    [in]  COR_FIELD_OFFSET    rFieldOffsets[],
    [in]  ULONG               ulClassSize
);  
```  
  
## <a name="parameters"></a>參數  

 `td`  
 在 `mdTypeDef` 指定要配置之類別的權杖。  
  
 `dwPackSize`  
 在封裝大小：1、2、4、8或16位元組。 封裝大小是相鄰欄位之間的位元組數目。  
  
 `rFieldOffsets`  
 在 [COR_FIELD_OFFSET](cor-field-offset-structure.md) 結構的陣列，其中每個結構會指定類別的欄位，以及類別內欄位的位移。 使用結束陣列 `mdTokenNil` 。  
  
 `ulClassSize`  
 在類別的大小（以位元組為單位）。  
  
## <a name="remarks"></a>備註  

 此類別一開始是透過呼叫 [IMetaDataEmit：:D efinetypedef](imetadataemit-definetypedef-method.md) 方法來定義，並為類別的欄位指定三個配置的其中一個：自動、連續或明確。 一般來說，您會使用自動版面配置，並讓執行時間選擇配置欄位的最佳方式。  
  
 不過，您可能會想要根據非受控碼所使用的相片順序來配置欄位。 在此情況下，請選擇連續或明確的版面配置，並呼叫 `SetClassLayout` 以完成欄位的版面配置：  
  
- 順序配置：指定封裝大小。 欄位會根據其自然大小或封裝大小對齊，以較小的欄位位移為准。 將 `rFieldOffsets` 設定 `ulClassSize` 為零。  
  
- 明確配置：請指定每個欄位的位移，或指定類別大小和封裝大小。  
  
## <a name="requirements"></a>需求  

 **平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** Cor。h  
  
 連結 **庫：** 當做 MSCorEE.dll 中的資源使用  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [IMetaDataEmit 介面](imetadataemit-interface.md)
- [IMetaDataEmit2 介面](imetadataemit2-interface.md)
