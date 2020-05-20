---
title: ISymUnmanagedMethod::GetSequencePointCount 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedMethod.GetSequencePointCount
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedMethod::GetSequencePointCount
helpviewer_keywords:
- ISymUnmanagedMethod::GetSequencePointCount method [.NET Framework debugging]
- GetSequencePointCount method [.NET Framework debugging]
ms.assetid: 836133e8-6108-4b9b-b0a9-bce4e08dccda
topic_type:
- apiref
ms.openlocfilehash: a44f81deb2d57b49f1fd0650fa52c06383210352
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614431"
---
# <a name="isymunmanagedmethodgetsequencepointcount-method"></a><span data-ttu-id="34801-102">ISymUnmanagedMethod::GetSequencePointCount 方法</span><span class="sxs-lookup"><span data-stu-id="34801-102">ISymUnmanagedMethod::GetSequencePointCount Method</span></span>
<span data-ttu-id="34801-103">取得這個方法內的序列點計數。</span><span class="sxs-lookup"><span data-stu-id="34801-103">Gets the count of sequence points within this method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="34801-104">語法</span><span class="sxs-lookup"><span data-stu-id="34801-104">Syntax</span></span>  
  
```cpp  
HRESULT GetSequencePointCount(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a><span data-ttu-id="34801-105">參數</span><span class="sxs-lookup"><span data-stu-id="34801-105">Parameters</span></span>  
 `pRetVal`  
 <span data-ttu-id="34801-106">脫銷的指標 `ULONG32` ，接收包含序列點所需的緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="34801-106">[out] A pointer to a `ULONG32` that receives the size of the buffer required to contain the sequence points.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="34801-107">傳回值</span><span class="sxs-lookup"><span data-stu-id="34801-107">Return Value</span></span>  
 <span data-ttu-id="34801-108">如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="34801-108">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="34801-109">需求</span><span class="sxs-lookup"><span data-stu-id="34801-109">Requirements</span></span>  
 <span data-ttu-id="34801-110">**標頭：** CorSym .idl，CorSym。h</span><span class="sxs-lookup"><span data-stu-id="34801-110">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="34801-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="34801-111">See also</span></span>

- [<span data-ttu-id="34801-112">ISymUnmanagedMethod 介面</span><span class="sxs-lookup"><span data-stu-id="34801-112">ISymUnmanagedMethod Interface</span></span>](isymunmanagedmethod-interface.md)
