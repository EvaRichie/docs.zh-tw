---
title: ISymENCUnmanagedMethod::GetDocumentsForMethodCount 方法
ms.date: 03/30/2017
api_name:
- ISymENCUnmanagedMethod.GetDocumentsForMethodCount
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymENCUnmanagedMethod::GetDocumentsForMethodCount
helpviewer_keywords:
- GetDocumentsForMethodCount method [.NET Framework debugging]
- ISymENCUnmanagedMethod::GetDocumentsForMethodCount method [.NET Framework debugging]
ms.assetid: cc1a823a-3ff3-4a33-b641-96edc93d2b17
topic_type:
- apiref
ms.openlocfilehash: 53897b6f964afb1f8ca95bc8f93c532e148ad129
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95730509"
---
# <a name="isymencunmanagedmethodgetdocumentsformethodcount-method"></a><span data-ttu-id="c47c5-102">ISymENCUnmanagedMethod::GetDocumentsForMethodCount 方法</span><span class="sxs-lookup"><span data-stu-id="c47c5-102">ISymENCUnmanagedMethod::GetDocumentsForMethodCount Method</span></span>

<span data-ttu-id="c47c5-103">取得此方法具有行的檔數目。</span><span class="sxs-lookup"><span data-stu-id="c47c5-103">Gets the number of documents that this method has lines in.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c47c5-104">語法</span><span class="sxs-lookup"><span data-stu-id="c47c5-104">Syntax</span></span>  
  
```cpp  
HRESULT GetDocumentsForMethodCount(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c47c5-105">參數</span><span class="sxs-lookup"><span data-stu-id="c47c5-105">Parameters</span></span>  

 `pRetVal`  
 <span data-ttu-id="c47c5-106">擴展的指標 `ULONG32` ，會接收包含檔所需的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="c47c5-106">[out] A pointer to a `ULONG32` that receives the size of the buffer required to contain the documents.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="c47c5-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="c47c5-107">Return Value</span></span>  

 <span data-ttu-id="c47c5-108">如果方法成功，則為 S_OK;否則，E_FAIL 或其他一些錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="c47c5-108">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c47c5-109">需求</span><span class="sxs-lookup"><span data-stu-id="c47c5-109">Requirements</span></span>  

 <span data-ttu-id="c47c5-110">**標頭：** CorSym .idl、CorSym。h</span><span class="sxs-lookup"><span data-stu-id="c47c5-110">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c47c5-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c47c5-111">See also</span></span>

- [<span data-ttu-id="c47c5-112">ISymENCUnmanagedMethod 介面</span><span class="sxs-lookup"><span data-stu-id="c47c5-112">ISymENCUnmanagedMethod Interface</span></span>](isymencunmanagedmethod-interface.md)
