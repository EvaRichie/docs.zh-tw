---
title: LinkResource 方法
ms.date: 03/30/2017
api_name:
- IALink.LinkResource
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- LinkResource
helpviewer_keywords:
- LinkResource method
ms.assetid: c404acb3-4c59-4100-9a4c-483cbdb1d736
topic_type:
- apiref
ms.openlocfilehash: 4f2f13976dfd4e5601bf8b54bed7b851884fbb9d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95690443"
---
# <a name="linkresource-method"></a>LinkResource 方法

資源中的連結。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT LinkResource(  
    mdAssembly  AssemblyID,  
    LPCWSTR     pszFileName,  
    LPCWSTR     pszNewLocation,  
    LPCWSTR     pszResourceName,  
    DWORD       dwFlags  
) PURE;  
```  
  
## <a name="parameters"></a>參數  

 `AssemblyID`  
 元件的識別碼。  
  
 `pszFileName`  
 檔案的名稱。  
  
 `pszNewLocation`  
 選用的新檔案名。 如果非 Null， `pszFileName` 將會複製到 pszNewLocation。  
  
 `pszResourceName`  
 資源名稱。  
  
 `dwFlags`  
 協助工具旗標 `mrPublic` ，例如和 `mrPrivate` 。 這個參數可以傳遞給 [DefineManifestResource 方法](../metadata/imetadataassemblyemit-definemanifestresource-method.md)。  
  
## <a name="return-value"></a>傳回值  

 如果方法成功，則傳回 S_OK。  
  
## <a name="requirements"></a>需求  

 需要 alink. h。  
  
## <a name="see-also"></a>另請參閱

- [IALink 介面](ialink-interface.md)
- [IALink2 介面](ialink2-interface.md)
- [ALink API](index.md)
