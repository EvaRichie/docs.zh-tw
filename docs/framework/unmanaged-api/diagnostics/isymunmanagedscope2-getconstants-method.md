---
title: ISymUnmanagedScope2::GetConstants 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedScope2.GetConstants
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedScope2::GetConstants
helpviewer_keywords:
- ISymUnmanagedScope2::GetConstants method [.NET Framework debugging]
- GetConstants method [.NET Framework debugging]
ms.assetid: f241b620-9ec5-42fd-92ef-3b22329db72a
topic_type:
- apiref
ms.openlocfilehash: f558d209d13fae93bd3a6f5e0e653afb91371a6a
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83615328"
---
# <a name="isymunmanagedscope2getconstants-method"></a><span data-ttu-id="2b8c1-102">ISymUnmanagedScope2::GetConstants 方法</span><span class="sxs-lookup"><span data-stu-id="2b8c1-102">ISymUnmanagedScope2::GetConstants Method</span></span>
<span data-ttu-id="2b8c1-103">取得在此範圍內定義的本機常數。</span><span class="sxs-lookup"><span data-stu-id="2b8c1-103">Gets the local constants defined within this scope.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2b8c1-104">語法</span><span class="sxs-lookup"><span data-stu-id="2b8c1-104">Syntax</span></span>  
  
```cpp  
HRESULT GetConstants(  
     [in]  ULONG32  cConstants,  
     [out] ULONG32  *pcConstants,  
     [out, size_is(cConstants),  
         length_is(*pcConstants)] ISymUnmanagedConstant*
             constants[]);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2b8c1-105">參數</span><span class="sxs-lookup"><span data-stu-id="2b8c1-105">Parameters</span></span>  
 `cConstants`  
 <span data-ttu-id="2b8c1-106">在參數所指向之緩衝區的長度 `pcConstants` 。</span><span class="sxs-lookup"><span data-stu-id="2b8c1-106">[in] The length of the buffer that the `pcConstants` parameter points to.</span></span>  
  
 `pcConstants`  
 <span data-ttu-id="2b8c1-107">脫銷的指標， `ULONG32` 接收包含常數所需的緩衝區大小（以字元為單位）。</span><span class="sxs-lookup"><span data-stu-id="2b8c1-107">[out] A pointer to a `ULONG32` that receives the size, in characters, of the buffer required to contain the constants.</span></span>  
  
 `constants`  
 <span data-ttu-id="2b8c1-108">脫銷儲存常數的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="2b8c1-108">[out] The buffer that stores the constants.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="2b8c1-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="2b8c1-109">Return Value</span></span>  
 <span data-ttu-id="2b8c1-110">如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="2b8c1-110">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2b8c1-111">需求</span><span class="sxs-lookup"><span data-stu-id="2b8c1-111">Requirements</span></span>  
 <span data-ttu-id="2b8c1-112">**標頭：** CorSym .idl，CorSym。h</span><span class="sxs-lookup"><span data-stu-id="2b8c1-112">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2b8c1-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2b8c1-113">See also</span></span>

- [<span data-ttu-id="2b8c1-114">ISymUnmanagedScope2 介面</span><span class="sxs-lookup"><span data-stu-id="2b8c1-114">ISymUnmanagedScope2 Interface</span></span>](isymunmanagedscope2-interface.md)
