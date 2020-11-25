---
title: ICorDebugEval2::NewParameterizedArray 方法
ms.date: 03/30/2017
api_name:
- ICorDebugEval2.NewParameterizedArray
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2::NewParameterizedArray
helpviewer_keywords:
- ICorDebugEval2::NewParameterizedArray method [.NET Framework debugging]
- NewParameterizedArray method [.NET Framework debugging]
ms.assetid: 45efb8ba-c4de-4109-945f-e734d376b43c
topic_type:
- apiref
ms.openlocfilehash: 14274932461fa7a5278c9a09b421f50be098cb91
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95729658"
---
# <a name="icordebugeval2newparameterizedarray-method"></a><span data-ttu-id="76449-102">ICorDebugEval2::NewParameterizedArray 方法</span><span class="sxs-lookup"><span data-stu-id="76449-102">ICorDebugEval2::NewParameterizedArray Method</span></span>

<span data-ttu-id="76449-103">配置指定元素類型和維度的新陣列。</span><span class="sxs-lookup"><span data-stu-id="76449-103">Allocates a new array of the specified element type and dimensions.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="76449-104">語法</span><span class="sxs-lookup"><span data-stu-id="76449-104">Syntax</span></span>  
  
```cpp  
HRESULT NewParameterizedArray(  
    [in] ICorDebugType          *pElementType,  
    [in] ULONG32                rank,  
    [in, size_is(rank)] ULONG32 dims[],  
    [in, size_is(rank)] ULONG32 lowBounds[]  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="76449-105">參數</span><span class="sxs-lookup"><span data-stu-id="76449-105">Parameters</span></span>  

 `pElementType`  
 <span data-ttu-id="76449-106">在ICorDebugType 物件的指標，代表儲存在陣列中的元素類型。</span><span class="sxs-lookup"><span data-stu-id="76449-106">[in] A pointer to an ICorDebugType object that represents the type of element stored in the array.</span></span>  
  
 `rank`  
 <span data-ttu-id="76449-107">在陣列的維度數目。</span><span class="sxs-lookup"><span data-stu-id="76449-107">[in] The number of dimensions of the array.</span></span> <span data-ttu-id="76449-108">在 .NET Framework 2.0 版中，此值必須是1。</span><span class="sxs-lookup"><span data-stu-id="76449-108">In the .NET Framework version 2.0, this value must be 1.</span></span>  
  
 `dims`  
 <span data-ttu-id="76449-109">在陣列每個維度的大小（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="76449-109">[in] The size, in bytes, of each dimension of the array.</span></span>  
  
 `lowBounds`  
 <span data-ttu-id="76449-110">[in] 選用。</span><span class="sxs-lookup"><span data-stu-id="76449-110">[in] Optional.</span></span> <span data-ttu-id="76449-111">陣列的每個維度下限。</span><span class="sxs-lookup"><span data-stu-id="76449-111">The lower bound of each dimension of the array.</span></span> <span data-ttu-id="76449-112">如果省略此值，則會針對每個維度採用零下限。</span><span class="sxs-lookup"><span data-stu-id="76449-112">If this value is omitted, a lower bound of zero is assumed for each dimension.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="76449-113">備註</span><span class="sxs-lookup"><span data-stu-id="76449-113">Remarks</span></span>  

 <span data-ttu-id="76449-114">陣列的元素可以是泛型型別的實例。</span><span class="sxs-lookup"><span data-stu-id="76449-114">The elements of the array may be instances of a generic type.</span></span> <span data-ttu-id="76449-115">陣列一律會建立線上程目前執行所在的應用程式域中。</span><span class="sxs-lookup"><span data-stu-id="76449-115">The array is always created in the application domain in which the thread is currently running.</span></span> <span data-ttu-id="76449-116">在 .NET Framework 2.0 中，的值 `rank` 必須是1。</span><span class="sxs-lookup"><span data-stu-id="76449-116">In the .NET Framework 2.0, the value of `rank` must be 1.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="76449-117">需求</span><span class="sxs-lookup"><span data-stu-id="76449-117">Requirements</span></span>  

 <span data-ttu-id="76449-118">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="76449-118">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="76449-119">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="76449-119">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="76449-120">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="76449-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="76449-121">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="76449-121">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
