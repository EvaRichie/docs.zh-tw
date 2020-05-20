---
title: ISymUnmanagedReader::GetDocuments 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader.GetDocuments
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetDocuments
helpviewer_keywords:
- GetDocuments method [.NET Framework debugging]
- ISymUnmanagedReader::GetDocuments method [.NET Framework debugging]
ms.assetid: e3b73a3f-d089-4101-a9a9-5e0765d05b61
topic_type:
- apiref
ms.openlocfilehash: b8a3a74888a3caae03da6f88a003bd277939ae59
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615042"
---
# <a name="isymunmanagedreadergetdocuments-method"></a><span data-ttu-id="28acd-102">ISymUnmanagedReader::GetDocuments 方法</span><span class="sxs-lookup"><span data-stu-id="28acd-102">ISymUnmanagedReader::GetDocuments Method</span></span>
<span data-ttu-id="28acd-103">傳回符號存放區中定義之所有檔的陣列。</span><span class="sxs-lookup"><span data-stu-id="28acd-103">Returns an array of all the documents defined in the symbol store.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="28acd-104">語法</span><span class="sxs-lookup"><span data-stu-id="28acd-104">Syntax</span></span>  
  
```cpp  
HRESULT GetDocuments (  
    [in]  ULONG32  cDocs,  
    [out] ULONG32  *pcDocs,  
    [out, size_is (cDocs),  
        length_is (*pcDocs)] ISymUnmanagedDocument *pDocs[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="28acd-105">參數</span><span class="sxs-lookup"><span data-stu-id="28acd-105">Parameters</span></span>  
 `cDocs`  
 <span data-ttu-id="28acd-106">[in] `pDocs` 陣列的大小。</span><span class="sxs-lookup"><span data-stu-id="28acd-106">[in] The size of the `pDocs` array.</span></span>  
  
 `pcDocs`  
 <span data-ttu-id="28acd-107">脫銷接收陣列長度之變數的指標。</span><span class="sxs-lookup"><span data-stu-id="28acd-107">[out] A pointer to a variable that receives the array length.</span></span>  
  
 `pDocs`  
 <span data-ttu-id="28acd-108">脫銷接收檔陣列之變數的指標。</span><span class="sxs-lookup"><span data-stu-id="28acd-108">[out] A pointer to a variable that receives the document array.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="28acd-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="28acd-109">Return Value</span></span>  
 <span data-ttu-id="28acd-110">如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="28acd-110">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="28acd-111">需求</span><span class="sxs-lookup"><span data-stu-id="28acd-111">Requirements</span></span>  
 <span data-ttu-id="28acd-112">**標頭：** CorSym .idl，CorSym。h</span><span class="sxs-lookup"><span data-stu-id="28acd-112">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="28acd-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="28acd-113">See also</span></span>

- [<span data-ttu-id="28acd-114">ISymUnmanagedReader 介面</span><span class="sxs-lookup"><span data-stu-id="28acd-114">ISymUnmanagedReader Interface</span></span>](isymunmanagedreader-interface.md)
