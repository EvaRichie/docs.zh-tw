---
title: ISymUnmanagedMethod::GetRanges 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetRanges
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetRanges
helpviewer_keywords:
- ISymUnmanagedMethod::GetRanges method [.NET Framework debugging]
- GetRanges method [.NET Framework debugging]
ms.assetid: a85283d8-379c-417a-9736-ddeeef9bcf50
topic_type:
- apiref
ms.openlocfilehash: cd5d1f2d59d3e55ba454f23d2e5dd4b1316c0df4
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615172"
---
# <a name="isymunmanagedmethodgetranges-method"></a>ISymUnmanagedMethod::GetRanges 方法
指定檔中的位置時，會傳回開始和結束位移組的陣列，其對應于此方法內的位置所涵蓋的 Microsoft 中繼語言（MSIL）範圍。 陣列是整數的陣列，其格式為 [開始]、[結束]、[開始]、[結束]。 範圍配對的數目是陣列的長度除以2。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT GetRanges(  
    [in]  ISymUnmanagedDocument* document,  
    [in]  ULONG32                line,  
    [in]  ULONG32                column,  
    [in]  ULONG32                cRanges,  
    [out] ULONG32                *pcRanges,  
    [out, size_is(cRanges),  
        length_is(*pcRanges)] ULONG32 ranges[]);  
```  
  
## <a name="parameters"></a>參數  
 `document`  
 在要求位移的檔。  
  
 `line`  
 在對應到範圍的檔行。  
  
 `column`  
 在對應到範圍的檔資料行。  
  
 `cRanges`  
 [in] `ranges` 陣列的大小。  
  
 `pcRanges`  
 脫銷的指標 `ULONG32` ，接收包含範圍所需的緩衝區大小。  
  
 `ranges`  
 脫銷接收範圍之緩衝區的指標。  
  
## <a name="return-value"></a>傳回值  
 如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。  
  
## <a name="requirements"></a>需求  
 **標頭：** CorSym .idl，CorSym。h  
  
## <a name="see-also"></a>另請參閱

- [ISymUnmanagedMethod 介面](isymunmanagedmethod-interface.md)
