---
title: ISymUnmanagedVariable::GetEndOffset 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedVariable.GetEndOffset
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedVariable::GetEndOffset
helpviewer_keywords:
- ISymUnmanagedVariable::GetEndOffset method [.NET Framework debugging]
- GetEndOffset method, ISymUnmanagedVariable interface [.NET Framework debugging]
ms.assetid: e5d777c5-d450-4c0f-999c-b3953ee22cfb
topic_type:
- apiref
ms.openlocfilehash: 91117eae23d38f3bc608f3203ebe53f92516c9c9
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610492"
---
# <a name="isymunmanagedvariablegetendoffset-method"></a><span data-ttu-id="22002-102">ISymUnmanagedVariable::GetEndOffset 方法</span><span class="sxs-lookup"><span data-stu-id="22002-102">ISymUnmanagedVariable::GetEndOffset Method</span></span>
<span data-ttu-id="22002-103">取得這個變數在其父系內的結束位移。</span><span class="sxs-lookup"><span data-stu-id="22002-103">Gets the end offset of this variable within its parent.</span></span> <span data-ttu-id="22002-104">如果這是範圍內的本機變數，則結束位移會落在為範圍定義的位移內。</span><span class="sxs-lookup"><span data-stu-id="22002-104">If this is a local variable within a scope, the end offset will fall within the offsets defined for the scope.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="22002-105">語法</span><span class="sxs-lookup"><span data-stu-id="22002-105">Syntax</span></span>  
  
```cpp  
HRESULT GetEndOffset(  
    [out, retval] ULONG32* pRetVal);  
```  
  
## <a name="parameters"></a><span data-ttu-id="22002-106">參數</span><span class="sxs-lookup"><span data-stu-id="22002-106">Parameters</span></span>  
 `pRetVal`  
 <span data-ttu-id="22002-107">脫銷`ULONG32`接收結束位移之的指標。</span><span class="sxs-lookup"><span data-stu-id="22002-107">[out] A pointer to a `ULONG32` that receives the end offset.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="22002-108">傳回值</span><span class="sxs-lookup"><span data-stu-id="22002-108">Return Value</span></span>  
 <span data-ttu-id="22002-109">如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="22002-109">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="22002-110">需求</span><span class="sxs-lookup"><span data-stu-id="22002-110">Requirements</span></span>  
 <span data-ttu-id="22002-111">**標頭：** CorSym .idl，CorSym。h</span><span class="sxs-lookup"><span data-stu-id="22002-111">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="22002-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="22002-112">See also</span></span>

- [<span data-ttu-id="22002-113">ISymUnmanagedVariable 介面</span><span class="sxs-lookup"><span data-stu-id="22002-113">ISymUnmanagedVariable Interface</span></span>](isymunmanagedvariable-interface.md)
- [<span data-ttu-id="22002-114">GetStartOffset 方法</span><span class="sxs-lookup"><span data-stu-id="22002-114">GetStartOffset Method</span></span>](isymunmanagedvariable-getstartoffset-method.md)
