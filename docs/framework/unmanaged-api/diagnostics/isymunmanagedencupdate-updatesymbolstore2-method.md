---
title: ISymUnmanagedENCUpdate::UpdateSymbolStore2 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedENCUpdate.UpdateSymbolStore2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedENCUpdate::UpdateSymbolStore2
helpviewer_keywords:
- ISymUnmanagedENCUpdate::UpdateSymbolStore2 method [.NET Framework debugging]
- UpdateSymbolStore2 method [.NET Framework debugging]
ms.assetid: 35588317-6184-485c-ab41-4b15fc1765d9
topic_type:
- apiref
ms.openlocfilehash: c68cf632b789a523b19cc78d8d919c2278b1befa
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95699569"
---
# <a name="isymunmanagedencupdateupdatesymbolstore2-method"></a><span data-ttu-id="0c21e-102">ISymUnmanagedENCUpdate::UpdateSymbolStore2 方法</span><span class="sxs-lookup"><span data-stu-id="0c21e-102">ISymUnmanagedENCUpdate::UpdateSymbolStore2 Method</span></span>

<span data-ttu-id="0c21e-103">允許編譯器省略尚未從程式資料庫修改的函式 (PDB) stream，前提是行資訊符合需求。</span><span class="sxs-lookup"><span data-stu-id="0c21e-103">Allows a compiler to omit functions that have not been modified from the program database (PDB) stream, provided the line information meets the requirements.</span></span> <span data-ttu-id="0c21e-104">您可以使用舊的 PDB 行資訊，以及函式中所有行的一個差異來判斷正確的行資訊。</span><span class="sxs-lookup"><span data-stu-id="0c21e-104">The correct line information can be determined with the old PDB line information and one delta for all lines in the function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0c21e-105">語法</span><span class="sxs-lookup"><span data-stu-id="0c21e-105">Syntax</span></span>  
  
```cpp  
HRESULT UpdateSymbolStore2(  
    [in]  IStream      *pIStream,  
    [in]  SYMLINEDELTA* pDeltaLines,  
    [in]  ULONG         cDeltaLines);  
```  
  
## <a name="parameters"></a><span data-ttu-id="0c21e-106">參數</span><span class="sxs-lookup"><span data-stu-id="0c21e-106">Parameters</span></span>  

 `pIStream`  
 <span data-ttu-id="0c21e-107">在包含行資訊的 [IStream](/windows/desktop/api/objidl/nn-objidl-istream) 指標。</span><span class="sxs-lookup"><span data-stu-id="0c21e-107">[in] A pointer to an [IStream](/windows/desktop/api/objidl/nn-objidl-istream) that contains the line information.</span></span>  
  
 `pDeltaLines`  
 <span data-ttu-id="0c21e-108">在 [SYMLINEDELTA](symlinedelta-structure.md) 結構的指標，其中包含已變更的行。</span><span class="sxs-lookup"><span data-stu-id="0c21e-108">[in] A pointer to a [SYMLINEDELTA](symlinedelta-structure.md) structure that contains the lines that have changed.</span></span>  
  
 `cDeltaLines`  
 <span data-ttu-id="0c21e-109">在 `ULONG` ，代表已變更的行數。</span><span class="sxs-lookup"><span data-stu-id="0c21e-109">[in] A `ULONG` that represents the number of lines that have changed.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="0c21e-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="0c21e-110">Return Value</span></span>  

 <span data-ttu-id="0c21e-111">如果方法成功，則為 S_OK;否則，E_FAIL 或其他一些錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="0c21e-111">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="0c21e-112">需求</span><span class="sxs-lookup"><span data-stu-id="0c21e-112">Requirements</span></span>  

 <span data-ttu-id="0c21e-113">**標頭：** CorSym .idl、CorSym。h</span><span class="sxs-lookup"><span data-stu-id="0c21e-113">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0c21e-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0c21e-114">See also</span></span>

- [<span data-ttu-id="0c21e-115">ISymUnmanagedENCUpdate 介面</span><span class="sxs-lookup"><span data-stu-id="0c21e-115">ISymUnmanagedENCUpdate Interface</span></span>](isymunmanagedencupdate-interface.md)
