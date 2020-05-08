---
title: ICorDebugEval2::CreateValueForType 方法
ms.date: 03/30/2017
api_name:
- ICorDebugEval2.CreateValueForType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2::CreateValueForType
helpviewer_keywords:
- CreateValueForType method [.NET Framework debugging]
- ICorDebugEval2::CreateValueForType method [.NET Framework debugging]
ms.assetid: ea38ae20-7e0a-427a-be77-d78fae719d82
topic_type:
- apiref
ms.openlocfilehash: fd7acaa8bcb4d53893855bcd25ff68cf26e30354
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976157"
---
# <a name="icordebugeval2createvaluefortype-method"></a><span data-ttu-id="2865d-102">ICorDebugEval2::CreateValueForType 方法</span><span class="sxs-lookup"><span data-stu-id="2865d-102">ICorDebugEval2::CreateValueForType Method</span></span>
<span data-ttu-id="2865d-103">取得指定類型之新 ICorDebugValue 的指標，其初始值為零或 null。</span><span class="sxs-lookup"><span data-stu-id="2865d-103">Gets a pointer to a new ICorDebugValue of the specified type, with an initial value of zero or null.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2865d-104">語法</span><span class="sxs-lookup"><span data-stu-id="2865d-104">Syntax</span></span>  
  
```cpp  
HRESULT CreateValueForType (  
    [in] ICorDebugType         *pType,  
    [out] ICorDebugValue       **ppValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="2865d-105">參數</span><span class="sxs-lookup"><span data-stu-id="2865d-105">Parameters</span></span>  
 `pType`  
 <span data-ttu-id="2865d-106">在代表類型之 ICorDebugType 物件的指標。</span><span class="sxs-lookup"><span data-stu-id="2865d-106">[in] Pointer to an ICorDebugType object that represents the type.</span></span>  
  
 `ppValue`  
 <span data-ttu-id="2865d-107">脫銷表示值之`ICorDebugValue`物件的位址指標。</span><span class="sxs-lookup"><span data-stu-id="2865d-107">[out] Pointer to the address of an `ICorDebugValue` object that represents the value.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2865d-108">備註</span><span class="sxs-lookup"><span data-stu-id="2865d-108">Remarks</span></span>  
 <span data-ttu-id="2865d-109">`CreateValueForType`一般化[ICorDebugEval：： CreateValue](icordebugeval-createvalue-method.md) ，可讓您指定任意物件類型，包括之類的結構化類型`List<int>`。</span><span class="sxs-lookup"><span data-stu-id="2865d-109">`CreateValueForType` generalizes [ICorDebugEval::CreateValue](icordebugeval-createvalue-method.md) by allowing you to specify an arbitrary object type, including constructed types such as `List<int>`.</span></span> <span data-ttu-id="2865d-110">此方法的唯一目的是產生可傳遞至函數評估的值。</span><span class="sxs-lookup"><span data-stu-id="2865d-110">The only purpose of this method is to generate a value that can be passed to a function evaluation.</span></span>  
  
 <span data-ttu-id="2865d-111">型別必須是類別或實值型別。</span><span class="sxs-lookup"><span data-stu-id="2865d-111">The type must be a class or a value type.</span></span> <span data-ttu-id="2865d-112">您不能使用這個方法來建立陣列值或字串值。</span><span class="sxs-lookup"><span data-stu-id="2865d-112">You cannot use this method to create array values or string values.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2865d-113">需求</span><span class="sxs-lookup"><span data-stu-id="2865d-113">Requirements</span></span>  
 <span data-ttu-id="2865d-114">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="2865d-114">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2865d-115">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="2865d-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="2865d-116">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="2865d-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2865d-117">**.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2865d-117">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>
