---
title: ISymUnmanagedWriter::DefineField 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineField
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineField
helpviewer_keywords:
- ISymUnmanagedWriter::DefineField method [.NET Framework debugging]
- DefineField method, ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: c6a1f797-dbf4-40f5-ab99-d9b4bfb26148
topic_type:
- apiref
ms.openlocfilehash: aba551a1973a41a909869316cda07e8d655e9882
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614834"
---
# <a name="isymunmanagedwriterdefinefield-method"></a><span data-ttu-id="e9b71-102">ISymUnmanagedWriter::DefineField 方法</span><span class="sxs-lookup"><span data-stu-id="e9b71-102">ISymUnmanagedWriter::DefineField Method</span></span>
<span data-ttu-id="e9b71-103">定義不在方法內的單一變數。</span><span class="sxs-lookup"><span data-stu-id="e9b71-103">Defines a single variable that is not within a method.</span></span> <span data-ttu-id="e9b71-104">這個方法會用於類別、位欄位等等的某些欄位。</span><span class="sxs-lookup"><span data-stu-id="e9b71-104">This method is used for certain fields in classes, bit fields, and so on.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e9b71-105">語法</span><span class="sxs-lookup"><span data-stu-id="e9b71-105">Syntax</span></span>  
  
```cpp  
HRESULT DefineField(  
    [in] mdTypeDef    parent,  
    [in] const WCHAR  *name,  
    [in] ULONG32      attributes,  
    [in] ULONG32      cSig,  
    [in, size_is(cSig)] unsigned char signature[],  
    [in] ULONG32      addrKind,  
    [in] ULONG32      addr1,  
    [in] ULONG32      addr2,  
    [in] ULONG32      addr3);  
```  
  
## <a name="parameters"></a><span data-ttu-id="e9b71-106">參數</span><span class="sxs-lookup"><span data-stu-id="e9b71-106">Parameters</span></span>  
 `parent`  
 <span data-ttu-id="e9b71-107">在元資料類型或方法 token。</span><span class="sxs-lookup"><span data-stu-id="e9b71-107">[in] The metadata type or method token.</span></span>  
  
 `name`  
 <span data-ttu-id="e9b71-108">在功能變數名稱。</span><span class="sxs-lookup"><span data-stu-id="e9b71-108">[in] The field name.</span></span>  
  
 `attributes`  
 <span data-ttu-id="e9b71-109">在欄位屬性。</span><span class="sxs-lookup"><span data-stu-id="e9b71-109">[in] The field attributes.</span></span>  
  
 `cSig`  
 <span data-ttu-id="e9b71-110">在， `ULONG32` 這是包含欄位簽章所需的緩衝區大小（以字元為單位）。</span><span class="sxs-lookup"><span data-stu-id="e9b71-110">[in] A `ULONG32` that is the size, in characters, of the buffer required to contain the field signature.</span></span>  
  
 `signature`  
 <span data-ttu-id="e9b71-111">在欄位簽章的陣列。</span><span class="sxs-lookup"><span data-stu-id="e9b71-111">[in] The array of field signatures.</span></span>  
  
 `addrKind`  
 <span data-ttu-id="e9b71-112">在網址類別型。</span><span class="sxs-lookup"><span data-stu-id="e9b71-112">[in] The address type.</span></span>  
  
 `addr1`  
 <span data-ttu-id="e9b71-113">在欄位規格的第一個位址。</span><span class="sxs-lookup"><span data-stu-id="e9b71-113">[in] The first address for the field specification.</span></span>  
  
 `addr2`  
 <span data-ttu-id="e9b71-114">在欄位規格的第二個位址。</span><span class="sxs-lookup"><span data-stu-id="e9b71-114">[in] The second address for the field specification.</span></span>  
  
 `addr3`  
 <span data-ttu-id="e9b71-115">在欄位規格的第三個位址。</span><span class="sxs-lookup"><span data-stu-id="e9b71-115">[in] The third address for the field specification.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="e9b71-116">傳回值</span><span class="sxs-lookup"><span data-stu-id="e9b71-116">Return Value</span></span>  
 <span data-ttu-id="e9b71-117">如果方法成功，則 S_OK;否則，E_FAIL 或一些其他錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="e9b71-117">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e9b71-118">需求</span><span class="sxs-lookup"><span data-stu-id="e9b71-118">Requirements</span></span>  
 <span data-ttu-id="e9b71-119">**標頭：** CorSym .idl，CorSym。h</span><span class="sxs-lookup"><span data-stu-id="e9b71-119">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e9b71-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e9b71-120">See also</span></span>

- [<span data-ttu-id="e9b71-121">ISymUnmanagedWriter 介面</span><span class="sxs-lookup"><span data-stu-id="e9b71-121">ISymUnmanagedWriter Interface</span></span>](isymunmanagedwriter-interface.md)
