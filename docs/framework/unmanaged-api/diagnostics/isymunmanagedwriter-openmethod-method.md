---
title: ISymUnmanagedWriter::OpenMethod 方法
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.OpenMethod
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::OpenMethod
helpviewer_keywords:
- ISymUnmanagedWriter::OpenMethod method [.NET Framework debugging]
- OpenMethod method [.NET Framework debugging]
ms.assetid: fb90cb7f-af88-45e8-a99f-80a0bbddb08b
topic_type:
- apiref
ms.openlocfilehash: deb3a28ffb73754b4c03496a6a72325418f1a4fc
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722904"
---
# <a name="isymunmanagedwriteropenmethod-method"></a><span data-ttu-id="2cee6-102">ISymUnmanagedWriter::OpenMethod 方法</span><span class="sxs-lookup"><span data-stu-id="2cee6-102">ISymUnmanagedWriter::OpenMethod Method</span></span>

<span data-ttu-id="2cee6-103">開啟用來發出符號資訊的方法。</span><span class="sxs-lookup"><span data-stu-id="2cee6-103">Opens a method into which symbol information is emitted.</span></span> <span data-ttu-id="2cee6-104">給定的方法會變成呼叫的目前方法，以定義序列點、參數和詞法範圍。</span><span class="sxs-lookup"><span data-stu-id="2cee6-104">The given method becomes the current method for calls to define sequence points, parameters, and lexical scopes.</span></span> <span data-ttu-id="2cee6-105">整個方法周圍都有隱含的詞法範圍。</span><span class="sxs-lookup"><span data-stu-id="2cee6-105">There is an implicit lexical scope around the entire method.</span></span> <span data-ttu-id="2cee6-106">重新開啟先前已關閉的方法，將會清除該方法的任何先前定義的符號。</span><span class="sxs-lookup"><span data-stu-id="2cee6-106">Reopening a method that was previously closed erases any previously defined symbols for that method.</span></span> <span data-ttu-id="2cee6-107">一次只能有一個開啟的方法。</span><span class="sxs-lookup"><span data-stu-id="2cee6-107">There can be only one open method at a time.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2cee6-108">語法</span><span class="sxs-lookup"><span data-stu-id="2cee6-108">Syntax</span></span>  
  
```cpp  
HRESULT OpenMethod(  
    [in] mdMethodDef method);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2cee6-109">參數</span><span class="sxs-lookup"><span data-stu-id="2cee6-109">Parameters</span></span>  

 `method`  
 <span data-ttu-id="2cee6-110">在要開啟之方法的元資料標記。</span><span class="sxs-lookup"><span data-stu-id="2cee6-110">[in] The metadata token for the method to be opened.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="2cee6-111">傳回值</span><span class="sxs-lookup"><span data-stu-id="2cee6-111">Return Value</span></span>  

 <span data-ttu-id="2cee6-112">如果方法成功，則為 S_OK;否則，E_FAIL 或其他一些錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="2cee6-112">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2cee6-113">需求</span><span class="sxs-lookup"><span data-stu-id="2cee6-113">Requirements</span></span>  

 <span data-ttu-id="2cee6-114">**標頭：** CorSym .idl、CorSym。h</span><span class="sxs-lookup"><span data-stu-id="2cee6-114">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2cee6-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2cee6-115">See also</span></span>

- [<span data-ttu-id="2cee6-116">ISymUnmanagedWriter 介面</span><span class="sxs-lookup"><span data-stu-id="2cee6-116">ISymUnmanagedWriter Interface</span></span>](isymunmanagedwriter-interface.md)
- [<span data-ttu-id="2cee6-117">CloseMethod 方法</span><span class="sxs-lookup"><span data-stu-id="2cee6-117">CloseMethod Method</span></span>](isymunmanagedwriter-closemethod-method.md)
- [<span data-ttu-id="2cee6-118">OpenMethod2 方法</span><span class="sxs-lookup"><span data-stu-id="2cee6-118">OpenMethod2 Method</span></span>](isymunmanagedwriter3-openmethod2-method.md)
