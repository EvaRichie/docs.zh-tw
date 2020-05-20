---
title: ISymUnmanagedBinder2::GetReaderForFile2 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder2.GetReaderForFile2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder2::GetReaderForFile2
helpviewer_keywords:
- ISymUnmanagedBinder2::GetReaderForFile2 method [.NET Framework debugging]
- GetReaderForFile2 method [.NET Framework debugging]
ms.assetid: dd92dcaf-403c-464d-a254-21594985dddd
topic_type:
- apiref
ms.openlocfilehash: 97b9fa537fdd9147d6d9eda036013add5393e33c
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441704"
---
# <a name="isymunmanagedbinder2getreaderforfile2-method"></a>ISymUnmanagedBinder2::GetReaderForFile2 方法
提供中繼資料介面和檔案名，會傳回正確的[ISymUnmanagedReader](isymunmanagedreader-interface.md)介面，以便讀取與模組相關聯的偵錯工具符號。  
  
 這個方法比[ISymUnmanagedBinder：： GetReaderForFile](isymunmanagedbinder-getreaderforfile-method.md)方法提供更廣泛的程式資料庫（PDB）檔案搜尋。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetReaderForFile2(  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *fileName,  
    [in]  const WCHAR  *searchPath,  
    [in]  ULONG32      searchPolicy,  
    [out,retval] ISymUnmanagedReader  **pRetVal);  
```  
  
## <a name="parameters"></a>參數  
 `importer`  
 在中繼資料匯入介面的指標。  
  
 `fileName`  
 在檔案名的指標。  
  
 `searchPath`  
 在搜尋路徑的指標。  
  
 `searchPolicy`  
 在[CorSymSearchPolicyAttributes](corsymsearchpolicyattributes-enumeration.md)列舉的值，指定搜尋符號讀取器時要使用的原則。  
  
 `pRetVal`  
 脫銷設定為所傳回[ISymUnmanagedReader](isymunmanagedreader-interface.md)介面的指標。  
  
## <a name="return-value"></a>傳回值  
 如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。  
  
## <a name="requirements"></a>需求  
 **標頭：** CorSym .idl，CorSym。h  
  
## <a name="remarks"></a>備註  
 這個版本的方法可以在模組旁邊的區域中搜尋 PDB 檔案。 搜尋原則可以藉由結合[CorSymSearchPolicyAttributes](corsymsearchpolicyattributes-enumeration.md)來控制。 例如， `AllowReferencePathAccess | AllowSymbolServerAccess` 會在可執行檔和符號伺服器上尋找 PDB，但不會查詢登錄或使用可執行檔中的路徑。 如果 `searchPath` 提供參數，則一律會搜尋這些目錄。  
  
## <a name="see-also"></a>另請參閱

- [ISymUnmanagedBinder2 介面](isymunmanagedbinder2-interface.md)
- [GetReaderForFile 方法](isymunmanagedbinder-getreaderforfile-method.md)
