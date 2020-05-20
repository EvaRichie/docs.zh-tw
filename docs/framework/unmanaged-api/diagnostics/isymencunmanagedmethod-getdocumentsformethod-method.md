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
ms.openlocfilehash: 89be772ee3d8a6fc5acb74d5ebe6d3c691764f89
ms.sourcegitcommit: 7b1497c1927cb449cefd313bc5126ae37df30746
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2020
ms.locfileid: "83441951"
---
# <a name="isymencunmanagedmethodgetdocumentsformethod-method"></a><span data-ttu-id="79041-102">ISymENCUnmanagedMethod::GetDocumentsForMethod 方法</span><span class="sxs-lookup"><span data-stu-id="79041-102">ISymENCUnmanagedMethod::GetDocumentsForMethod Method</span></span>
<span data-ttu-id="79041-103">取得此方法在中具有行的檔。</span><span class="sxs-lookup"><span data-stu-id="79041-103">Gets the documents that this method has lines in.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="79041-104">語法</span><span class="sxs-lookup"><span data-stu-id="79041-104">Syntax</span></span>  
  
```cpp  
HRESULT GetDocumentsForMethod(  
    [in]  ULONG32  cDocs,  
    [out] ULONG32  *pcDocs,
    [in, size_is(cDocs)] ISymUnmanagedDocument* documents[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="79041-105">參數</span><span class="sxs-lookup"><span data-stu-id="79041-105">Parameters</span></span>  
 `cDocs`  
 <span data-ttu-id="79041-106">在所指向之緩衝區的長度 `pcDocs` 。</span><span class="sxs-lookup"><span data-stu-id="79041-106">[in] The length of the buffer pointed to by `pcDocs`.</span></span>  
  
 `pcDocs`  
 <span data-ttu-id="79041-107">脫銷的指標， `ULONG32` 接收包含檔所需的緩衝區大小（以字元為單位）。</span><span class="sxs-lookup"><span data-stu-id="79041-107">[out] A pointer to a `ULONG32` that receives the size, in characters, of the buffer required to contain the documents.</span></span>  
  
 `documents`  
 <span data-ttu-id="79041-108">在包含檔的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="79041-108">[in] The buffer that contains the documents.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="79041-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="79041-109">Return Value</span></span>  
 <span data-ttu-id="79041-110">如果方法成功，則 S_OK;否則，錯誤碼為。</span><span class="sxs-lookup"><span data-stu-id="79041-110">S_OK if the method succeeds; otherwise, an error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="79041-111">需求</span><span class="sxs-lookup"><span data-stu-id="79041-111">Requirements</span></span>  
 <span data-ttu-id="79041-112">**標頭：** CorSym .idl，CorSym。h</span><span class="sxs-lookup"><span data-stu-id="79041-112">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="79041-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="79041-113">See also</span></span>

- [<span data-ttu-id="79041-114">ISymENCUnmanagedMethod 介面</span><span class="sxs-lookup"><span data-stu-id="79041-114">ISymENCUnmanagedMethod Interface</span></span>](isymencunmanagedmethod-interface.md)
