---
title: ICorDebugEval::NewArray 方法
ms.date: 03/30/2017
api_name:
- ICorDebugEval.NewArray
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::NewArray
helpviewer_keywords:
- NewArray method [.NET Framework debugging]
- ICorDebugEval::NewArray method [.NET Framework debugging]
ms.assetid: cc79a67d-5368-434d-a943-209db90491b9
topic_type:
- apiref
ms.openlocfilehash: 496a6a7e01dec8aa90ba4e849c431ccd499ef53d
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976196"
---
# <a name="icordebugevalnewarray-method"></a><span data-ttu-id="5c06b-102">ICorDebugEval::NewArray 方法</span><span class="sxs-lookup"><span data-stu-id="5c06b-102">ICorDebugEval::NewArray Method</span></span>
<span data-ttu-id="5c06b-103">配置指定之元素類型和維度的新陣列。</span><span class="sxs-lookup"><span data-stu-id="5c06b-103">Allocates a new array of the specified element type and dimensions.</span></span>  
  
 <span data-ttu-id="5c06b-104">這個方法在 .NET Framework 版本2.0 中已過時。</span><span class="sxs-lookup"><span data-stu-id="5c06b-104">This method is obsolete in the .NET Framework version 2.0.</span></span> <span data-ttu-id="5c06b-105">請改用[ICorDebugEval2：： NewParameterizedArray](icordebugeval2-newparameterizedarray-method.md) 。</span><span class="sxs-lookup"><span data-stu-id="5c06b-105">Use [ICorDebugEval2::NewParameterizedArray](icordebugeval2-newparameterizedarray-method.md) instead.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="5c06b-106">語法</span><span class="sxs-lookup"><span data-stu-id="5c06b-106">Syntax</span></span>  
  
```cpp  
HRESULT NewArray (  
    [in] CorElementType     elementType,  
    [in] ICorDebugClass     *pElementClass,  
    [in] ULONG32            rank,  
    [in, size_is(rank)] ULONG32 dims[],  
    [in, size_is(rank)] ULONG32 lowBounds[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="5c06b-107">參數</span><span class="sxs-lookup"><span data-stu-id="5c06b-107">Parameters</span></span>  
 `elementType`  
 <span data-ttu-id="5c06b-108">在CorElementType 列舉的值，指定陣列的元素類型。</span><span class="sxs-lookup"><span data-stu-id="5c06b-108">[in] A value of the CorElementType enumeration that specifies the element type of the array.</span></span>  
  
 `pElementClass`  
 <span data-ttu-id="5c06b-109">在ICorDebugClass 物件的指標，指定元素的類別。</span><span class="sxs-lookup"><span data-stu-id="5c06b-109">[in] A pointer to a ICorDebugClass object that specifies the class of the element.</span></span> <span data-ttu-id="5c06b-110">如果元素類型是基本類型，這個值可能是 null。</span><span class="sxs-lookup"><span data-stu-id="5c06b-110">This value may be null if the element type is a primitive type.</span></span>  
  
 `rank`  
 <span data-ttu-id="5c06b-111">在陣列的維度數目。</span><span class="sxs-lookup"><span data-stu-id="5c06b-111">[in] The number of dimensions of the array.</span></span> <span data-ttu-id="5c06b-112">在 .NET Framework 2.0 中，此值必須是1。</span><span class="sxs-lookup"><span data-stu-id="5c06b-112">In the .NET Framework 2.0, this value must be 1.</span></span>  
  
 `dims`  
 <span data-ttu-id="5c06b-113">在陣列的每個維度大小（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="5c06b-113">[in] The size, in bytes, of each dimension of the array.</span></span>  
  
 `lowBounds`  
 <span data-ttu-id="5c06b-114">[in] 選用。</span><span class="sxs-lookup"><span data-stu-id="5c06b-114">[in] Optional.</span></span> <span data-ttu-id="5c06b-115">陣列的每個維度下限。</span><span class="sxs-lookup"><span data-stu-id="5c06b-115">The lower bound of each dimension of the array.</span></span> <span data-ttu-id="5c06b-116">如果省略此值，則會假設每個維度的下限為零。</span><span class="sxs-lookup"><span data-stu-id="5c06b-116">If this value is omitted, a lower bound of zero is assumed for each dimension.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="5c06b-117">備註</span><span class="sxs-lookup"><span data-stu-id="5c06b-117">Remarks</span></span>  
 <span data-ttu-id="5c06b-118">陣列一律會建立線上程目前執行所在的應用程式域中。</span><span class="sxs-lookup"><span data-stu-id="5c06b-118">The array is always created in the application domain in which the thread is currently executing.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="5c06b-119">需求</span><span class="sxs-lookup"><span data-stu-id="5c06b-119">Requirements</span></span>  
 <span data-ttu-id="5c06b-120">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="5c06b-120">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="5c06b-121">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="5c06b-121">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="5c06b-122">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="5c06b-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="5c06b-123">**.NET Framework 版本：** 1.1、1。0</span><span class="sxs-lookup"><span data-stu-id="5c06b-123">**.NET Framework Versions:** 1.1, 1.0</span></span>
