---
title: ICorDebugCode4：： EnumerateVariableHomes 方法
ms.date: 03/30/2017
api_name:
- ICorDebugCode4.EnumerateVariableHomes
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode4::EnumerateVariableHomes
helpviewer_keywords:
- EnumerateVariableHomes method [.NET Framework debugging]
- ICorDebugCode4::EnumerateVariableHomes method [.NET Framework debugging]
ms.assetid: 802c01ff-8b80-4733-b6dd-03ab6ff7fa11
topic_type:
- apiref
ms.openlocfilehash: 5f731b1459542c3f5378790b21f2ea576e89ad97
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82893346"
---
# <a name="icordebugcode4enumeratevariablehomes-method"></a><span data-ttu-id="57f19-102">ICorDebugCode4：： EnumerateVariableHomes 方法</span><span class="sxs-lookup"><span data-stu-id="57f19-102">ICorDebugCode4::EnumerateVariableHomes Method</span></span>
<span data-ttu-id="57f19-103">取得函數中區域變數和引數的列舉值。</span><span class="sxs-lookup"><span data-stu-id="57f19-103">Gets an enumerator to the local variables and arguments in a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="57f19-104">語法</span><span class="sxs-lookup"><span data-stu-id="57f19-104">Syntax</span></span>  
  
```cpp  
HRESULT EnumerateVariableHomes(  
    [out] ICorDebugVariableHomeEnum **ppEnum  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="57f19-105">參數</span><span class="sxs-lookup"><span data-stu-id="57f19-105">Parameters</span></span>  
 `ppEnum`  
 <span data-ttu-id="57f19-106">[ICorDebugVariableHomeEnum](icordebugvariablehomeenum-interface.md)介面物件之位址的指標，這是函式中區域變數和引數的列舉值。</span><span class="sxs-lookup"><span data-stu-id="57f19-106">A pointer to the address of an [ICorDebugVariableHomeEnum](icordebugvariablehomeenum-interface.md) interface object that is an enumerator for the local variables and arguments in a function.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="57f19-107">備註</span><span class="sxs-lookup"><span data-stu-id="57f19-107">Remarks</span></span>  
 <span data-ttu-id="57f19-108">[ICorDebugVariableHomeEnum](icordebugvariablehomeenum-interface.md)介面物件是衍生自 "ICorDebugEnum" 介面的標準列舉值，可讓您列舉[ICorDebugVariableHome](icordebugvariablehome-interface.md)物件。</span><span class="sxs-lookup"><span data-stu-id="57f19-108">The [ICorDebugVariableHomeEnum](icordebugvariablehomeenum-interface.md) interface object is a standard enumerator derived from the "ICorDebugEnum" interface that allows you to enumerate [ICorDebugVariableHome](icordebugvariablehome-interface.md) objects.</span></span> <span data-ttu-id="57f19-109">如果相同的位置或引數索引在函式的不同點有不同的主物件，則該集合可能包含多個[ICorDebugVariableHome](icordebugvariablehome-interface.md)物件。</span><span class="sxs-lookup"><span data-stu-id="57f19-109">The collection may include multiple [ICorDebugVariableHome](icordebugvariablehome-interface.md) objects for the same slot or      argument index if they have different homes at different points in the      function.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="57f19-110">需求</span><span class="sxs-lookup"><span data-stu-id="57f19-110">Requirements</span></span>  
 <span data-ttu-id="57f19-111">**平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="57f19-111">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="57f19-112">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="57f19-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="57f19-113">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="57f19-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="57f19-114">**.NET Framework 版本：**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="57f19-114">**.NET Framework Versions:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="57f19-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="57f19-115">See also</span></span>

- [<span data-ttu-id="57f19-116">ICorDebugCode4 介面</span><span class="sxs-lookup"><span data-stu-id="57f19-116">ICorDebugCode4 Interface</span></span>](icordebugcode4-interface.md)
- [<span data-ttu-id="57f19-117">偵錯介面</span><span class="sxs-lookup"><span data-stu-id="57f19-117">Debugging Interfaces</span></span>](debugging-interfaces.md)
