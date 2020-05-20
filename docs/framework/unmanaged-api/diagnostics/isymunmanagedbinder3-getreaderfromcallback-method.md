---
title: ISymUnmanagedBinder3::GetReaderFromCallback 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedBinder3.GetReaderFromCallback
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedBinder3::GetReaderFromCallback
helpviewer_keywords:
- GetReaderFromCallback method [.NET Framework debugging]
- ISymUnmanagedBinder3::GetReaderFromCallback method [.NET Framework debugging]
ms.assetid: 4ef83bd2-3d8e-499e-8a12-d9d6fd6ced30
topic_type:
- apiref
ms.openlocfilehash: 4a23e9aa259f430c0d0579657952fc6aba4c307c
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441652"
---
# <a name="isymunmanagedbinder3getreaderfromcallback-method"></a>ISymUnmanagedBinder3::GetReaderFromCallback 方法
可讓使用者透過回呼來執行或提供， `IID_IDiaReadExeAtRVACallback` 或 `IID_IDiaReadExeAtOffsetCallback` 從記憶體取得 debug 目錄資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetReaderFromCallback(  
    [in]  IUnknown     *importer,  
    [in]  const WCHAR  *fileName,  
    [in]  const WCHAR  *searchPath,  
    [in]  ULONG32      searchPolicy,  
    [in]  IUnknown     *callback,  
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
  
 `callback`  
 在回呼函式的指標。  
  
 `pRetVal`  
 脫銷設定為所傳回[ISymUnmanagedReader](isymunmanagedreader-interface.md)介面的指標。  
  
## <a name="return-value"></a>傳回值  
 如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。  
  
## <a name="requirements"></a>需求  
 **標頭：** CorSym .idl  
  
## <a name="see-also"></a>另請參閱

- [ISymUnmanagedBinder3 介面](isymunmanagedbinder3-interface.md)
