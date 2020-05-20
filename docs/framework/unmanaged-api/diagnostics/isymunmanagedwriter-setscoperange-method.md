---
title: ISymUnmanagedWriter::SetScopeRange 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.SetScopeRange
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::SetScopeRange
helpviewer_keywords:
- SetScopeRange method [.NET Framework debugging]
- ISymUnmanagedWriter::SetScopeRange method [.NET Framework debugging]
ms.assetid: d4d98676-444b-46ca-bfe6-0d827385cd22
topic_type:
- apiref
ms.openlocfilehash: b57bb549278f62cdce6ed5deaaa62f154ec919b5
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609361"
---
# <a name="isymunmanagedwritersetscoperange-method"></a><span data-ttu-id="59db7-102">ISymUnmanagedWriter::SetScopeRange 方法</span><span class="sxs-lookup"><span data-stu-id="59db7-102">ISymUnmanagedWriter::SetScopeRange Method</span></span>
<span data-ttu-id="59db7-103">定義指定語彙範圍的位移範圍。</span><span class="sxs-lookup"><span data-stu-id="59db7-103">Defines the offset range for the specified lexical scope.</span></span> <span data-ttu-id="59db7-104">範圍會變成新的目前範圍，並推送至範圍的堆疊。</span><span class="sxs-lookup"><span data-stu-id="59db7-104">The scope becomes the new current scope and is pushed onto a stack of scopes.</span></span> <span data-ttu-id="59db7-105">範圍必須形成階層。</span><span class="sxs-lookup"><span data-stu-id="59db7-105">Scopes must form a hierarchy.</span></span> <span data-ttu-id="59db7-106">同級不允許重迭。</span><span class="sxs-lookup"><span data-stu-id="59db7-106">Siblings are not allowed to overlap.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="59db7-107">語法</span><span class="sxs-lookup"><span data-stu-id="59db7-107">Syntax</span></span>  
  
```cpp  
HRESULT OpenScope(  
    [in] ULONG32  scopeID,  
    [in] ULONG32  startOffset,  
    [in] ULONG32  endOffset);  
```  
  
## <a name="parameters"></a><span data-ttu-id="59db7-108">參數</span><span class="sxs-lookup"><span data-stu-id="59db7-108">Parameters</span></span>  
 `scopeId`  
 <span data-ttu-id="59db7-109">在範圍的範圍識別碼。</span><span class="sxs-lookup"><span data-stu-id="59db7-109">[in] The scope identifier for the scope.</span></span>  
  
 `startOffset`  
 <span data-ttu-id="59db7-110">在在方法開頭的詞法範圍中，第一個指令的位移（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="59db7-110">[in] The offset, in bytes, of the first instruction in the lexical scope from the beginning of the method.</span></span>  
  
 `endOffset`  
 <span data-ttu-id="59db7-111">在從方法開頭的詞法範圍中，最後一個指令的位移（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="59db7-111">[in] The offset, in bytes, of the last instruction in the lexical scope from the beginning of the method.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="59db7-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="59db7-112">Return Value</span></span>  
 <span data-ttu-id="59db7-113">如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="59db7-113">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="59db7-114">備註</span><span class="sxs-lookup"><span data-stu-id="59db7-114">Remarks</span></span>  
 <span data-ttu-id="59db7-115">[ISymUnmanagedWriter：： OpenScope](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openscope-method.md)會傳回不透明的範圍識別碼，可與搭配使用 `ISymUnmanagedWriter::SetScopeRange` 以定義範圍的開始和結束位移。</span><span class="sxs-lookup"><span data-stu-id="59db7-115">[ISymUnmanagedWriter::OpenScope](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openscope-method.md) returns an opaque scope identifier that can be used with `ISymUnmanagedWriter::SetScopeRange` to define a scope's starting and ending offset at a later time.</span></span> <span data-ttu-id="59db7-116">在此情況下，傳遞至 `ISymUnmanagedWriter::OpenScope` 和[ISymUnmanagedWriter：： CloseScope](isymunmanagedwriter-closescope-method.md)的位移會被忽略。</span><span class="sxs-lookup"><span data-stu-id="59db7-116">In this case, the offsets passed to `ISymUnmanagedWriter::OpenScope` and [ISymUnmanagedWriter::CloseScope](isymunmanagedwriter-closescope-method.md) are ignored.</span></span> <span data-ttu-id="59db7-117">範圍識別碼只在目前的方法中有效。</span><span class="sxs-lookup"><span data-stu-id="59db7-117">Scope identifiers are only valid in the current method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="59db7-118">需求</span><span class="sxs-lookup"><span data-stu-id="59db7-118">Requirements</span></span>  
 <span data-ttu-id="59db7-119">**標頭：** CorSym .idl，CorSym。h</span><span class="sxs-lookup"><span data-stu-id="59db7-119">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="59db7-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="59db7-120">See also</span></span>

- [<span data-ttu-id="59db7-121">ISymUnmanagedWriter 介面</span><span class="sxs-lookup"><span data-stu-id="59db7-121">ISymUnmanagedWriter Interface</span></span>](isymunmanagedwriter-interface.md)
