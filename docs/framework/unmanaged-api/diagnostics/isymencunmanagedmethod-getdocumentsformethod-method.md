---
title: ISymENCUnmanagedMethod::GetDocumentsForMethod 方法
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetDocumentsForMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetDocumentsForMethod
helpviewer_keywords:
- GetDocumentsForMethod method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetDocumentsForMethod method [.NET Framework debugging]
ms.assetid: bd6ccde5-d578-48d8-abed-b474fbd48d13
topic_type:
- apiref
ms.openlocfilehash: d9fe18225dc27e93d4e97940cba878e4d73b4ed2
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730522"
---
# <a name="isymencunmanagedmethodgetdocumentsformethod-method"></a><span data-ttu-id="8f911-102">ISymENCUnmanagedMethod::GetDocumentsForMethod 方法</span><span class="sxs-lookup"><span data-stu-id="8f911-102">ISymENCUnmanagedMethod::GetDocumentsForMethod Method</span></span>

<span data-ttu-id="8f911-103">取得此方法具有行的檔。</span><span class="sxs-lookup"><span data-stu-id="8f911-103">Gets the documents that this method has lines in.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8f911-104">語法</span><span class="sxs-lookup"><span data-stu-id="8f911-104">Syntax</span></span>  
  
```cpp  
HRESULT GetDocumentsForMethod(  
    [in]  ULONG32  cDocs,  
    [out] ULONG32  *pcDocs,
    [in, size_is(cDocs)] ISymUnmanagedDocument* documents[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="8f911-105">參數</span><span class="sxs-lookup"><span data-stu-id="8f911-105">Parameters</span></span>  

 `cDocs`  
 <span data-ttu-id="8f911-106">在所指向的緩衝區長度 `pcDocs` 。</span><span class="sxs-lookup"><span data-stu-id="8f911-106">[in] The length of the buffer pointed to by `pcDocs`.</span></span>  
  
 `pcDocs`  
 <span data-ttu-id="8f911-107">擴展的指標， `ULONG32` 會接收包含檔所需的緩衝區大小（以字元為單位）。</span><span class="sxs-lookup"><span data-stu-id="8f911-107">[out] A pointer to a `ULONG32` that receives the size, in characters, of the buffer required to contain the documents.</span></span>  
  
 `documents`  
 <span data-ttu-id="8f911-108">在包含檔的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="8f911-108">[in] The buffer that contains the documents.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="8f911-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="8f911-109">Return Value</span></span>  

 <span data-ttu-id="8f911-110">如果方法成功，則為 S_OK;否則為錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="8f911-110">S_OK if the method succeeds; otherwise, an error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8f911-111">需求</span><span class="sxs-lookup"><span data-stu-id="8f911-111">Requirements</span></span>  

 <span data-ttu-id="8f911-112">**標頭：** CorSym .idl、CorSym。h</span><span class="sxs-lookup"><span data-stu-id="8f911-112">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8f911-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8f911-113">See also</span></span>

- [<span data-ttu-id="8f911-114">ISymENCUnmanagedMethod 介面</span><span class="sxs-lookup"><span data-stu-id="8f911-114">ISymENCUnmanagedMethod Interface</span></span>](isymencunmanagedmethod-interface.md)
