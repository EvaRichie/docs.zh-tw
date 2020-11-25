---
title: ImportFileEx 方法
ms.date: 03/30/2017
api_name:
- IALink2.ImportFileEx
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ImportFileEx
helpviewer_keywords:
- ImportFileEx method
ms.assetid: ad276f3f-b303-46ac-97e0-66a377adaa4f
topic_type:
- apiref
ms.openlocfilehash: 9e373f133830a5bc1f3cf7bdc8034cb67725d797
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95705198"
---
# <a name="importfileex-method"></a>ImportFileEx 方法

匯入指定的元件或未系結的模組。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT ImportFileEx(  
    LPCWSTR pszFilename,  
    LPCWSTR pszTargetName,  
    BOOL fSmartImport,  
    DWORD dwOpenFlags,  
    mdToken* pImportToken,  
    IMetaDataAssemblyImport** ppAssemblyScope,  
    DWORD* pdwCountOfScopes  
) PURE;  
```  
  
## <a name="parameters"></a>參數  

 `pszFilename`  
 要匯入之檔案的完整名稱。  
  
 `pszTargetName`  
 目的檔案名的選擇性名稱。  
  
 `fSmartImport`  
 若為 TRUE，則會使用 ImportTypes，否則必須手動執行匯入。  
  
 `dwOpenFlags`  
 要傳遞至 [OpenScope 方法](../metadata/imetadatadispenser-openscope-method.md)的旗標。  
  
 `pImportToken`  
 接收正在匯入之檔案的識別碼。  
  
 `ppAssemblyScope`  
 接收元件匯入範圍 [IMetaDataAssemblyImport 介面](../metadata/imetadataassemblyimport-interface.md) 介面。 如果檔案不是元件，則設定為 Null。  
  
 `pdwCountOfScopes`  
 接收已匯入檔案和/或範圍的計數。  
  
## <a name="return-value"></a>傳回值  

 如果方法成功，則傳回 S_OK。  
  
## <a name="requirements"></a>需求  

 需要 alink. h。  
  
## <a name="see-also"></a>另請參閱

- [IALink2 介面](ialink2-interface.md)
- [IALink 介面](ialink-interface.md)
- [ALink API](index.md)
