---
title: ISymUnmanagedWriter2::DefineGlobalVariable2 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter2.DefineGlobalVariable2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter2::DefineGlobalVariable2
helpviewer_keywords:
- ISymUnmanagedWriter2::DefineGlobalVariable2 method [.NET Framework debugging]
- DefineGlobalVariable2 method [.NET Framework debugging]
ms.assetid: 04d569d6-a151-4957-9872-f3f694c3e4a9
topic_type:
- apiref
ms.openlocfilehash: e417854f5f82ba2e0f16848f53b2b605dccf9eb5
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95683455"
---
# <a name="isymunmanagedwriter2defineglobalvariable2-method"></a><span data-ttu-id="86d3a-102">ISymUnmanagedWriter2::DefineGlobalVariable2 方法</span><span class="sxs-lookup"><span data-stu-id="86d3a-102">ISymUnmanagedWriter2::DefineGlobalVariable2 Method</span></span>

<span data-ttu-id="86d3a-103">定義單一全域變數。</span><span class="sxs-lookup"><span data-stu-id="86d3a-103">Defines a single global variable.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="86d3a-104">語法</span><span class="sxs-lookup"><span data-stu-id="86d3a-104">Syntax</span></span>  
  
```cpp  
HRESULT DefineGlobalVariable2(  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] mdSignature  sigToken,  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3);  
```  
  
## <a name="parameters"></a><span data-ttu-id="86d3a-105">參數</span><span class="sxs-lookup"><span data-stu-id="86d3a-105">Parameters</span></span>  

 `name`  
 <span data-ttu-id="86d3a-106">在全域變數名稱。</span><span class="sxs-lookup"><span data-stu-id="86d3a-106">[in] The global variable name.</span></span>  
  
 `attributes`  
 <span data-ttu-id="86d3a-107">在全域變數屬性。</span><span class="sxs-lookup"><span data-stu-id="86d3a-107">[in] The global variable attributes.</span></span>  
  
 `sigToken`  
 <span data-ttu-id="86d3a-108">在簽章的元資料標記。</span><span class="sxs-lookup"><span data-stu-id="86d3a-108">[in] The metadata token of the signature.</span></span>  
  
 `addrKind`  
 <span data-ttu-id="86d3a-109">在網址類別型。</span><span class="sxs-lookup"><span data-stu-id="86d3a-109">[in] The address type.</span></span>  
  
 `addr1`  
 <span data-ttu-id="86d3a-110">在參數規格的第一個位址。</span><span class="sxs-lookup"><span data-stu-id="86d3a-110">[in] The first address for the parameter specification.</span></span>  
  
 `addr2`  
 <span data-ttu-id="86d3a-111">在參數規格的第二個位址。</span><span class="sxs-lookup"><span data-stu-id="86d3a-111">[in] The second address for the parameter specification.</span></span>  
  
 `addr3`  
 <span data-ttu-id="86d3a-112">在參數規格的第三個位址。</span><span class="sxs-lookup"><span data-stu-id="86d3a-112">[in] The third address for the parameter specification.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="86d3a-113">傳回值</span><span class="sxs-lookup"><span data-stu-id="86d3a-113">Return Value</span></span>  

 <span data-ttu-id="86d3a-114">如果方法成功，則為 S_OK;否則，E_FAIL 或其他一些錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="86d3a-114">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="86d3a-115">需求</span><span class="sxs-lookup"><span data-stu-id="86d3a-115">Requirements</span></span>  

 <span data-ttu-id="86d3a-116">**標頭：** CorSym .idl</span><span class="sxs-lookup"><span data-stu-id="86d3a-116">**Header:** CorSym.idl</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="86d3a-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="86d3a-117">See also</span></span>

- [<span data-ttu-id="86d3a-118">ISymUnmanagedWriter2 介面</span><span class="sxs-lookup"><span data-stu-id="86d3a-118">ISymUnmanagedWriter2 Interface</span></span>](isymunmanagedwriter2-interface.md)
- [<span data-ttu-id="86d3a-119">DefineGlobalVariable 方法</span><span class="sxs-lookup"><span data-stu-id="86d3a-119">DefineGlobalVariable Method</span></span>](isymunmanagedwriter-defineglobalvariable-method.md)
