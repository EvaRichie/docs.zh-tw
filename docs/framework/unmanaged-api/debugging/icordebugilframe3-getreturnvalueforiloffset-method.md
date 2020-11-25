---
title: ICorDebugILFrame3::GetReturnValueForILOffset 方法
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
api_name:
- ICorDebugILFrame3.GetReturnValueForILOffset
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 06522727-5f64-4391-9331-11386883c352
topic_type:
- apiref
ms.openlocfilehash: 11207298b071527151535144330790df767c2101
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95724997"
---
# <a name="icordebugilframe3getreturnvalueforiloffset-method"></a><span data-ttu-id="9750e-102">ICorDebugILFrame3::GetReturnValueForILOffset 方法</span><span class="sxs-lookup"><span data-stu-id="9750e-102">ICorDebugILFrame3::GetReturnValueForILOffset Method</span></span>

<span data-ttu-id="9750e-103">取得 "ICorDebugValue" 物件，此物件會封裝函式的傳回值。</span><span class="sxs-lookup"><span data-stu-id="9750e-103">Gets an "ICorDebugValue" object that encapsulates the return value of a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="9750e-104">語法</span><span class="sxs-lookup"><span data-stu-id="9750e-104">Syntax</span></span>  
  
```cpp
HRESULT GetReturnValueForILOffset(  
    ULONG32 ILoffset,
    [out] ICorDebugValue **ppReturnValue  
);  
```  
  
## <a name="parameters"></a><span data-ttu-id="9750e-105">參數</span><span class="sxs-lookup"><span data-stu-id="9750e-105">Parameters</span></span>  

 `ILOffset`  
 <span data-ttu-id="9750e-106">IL 位移。</span><span class="sxs-lookup"><span data-stu-id="9750e-106">The IL offset.</span></span> <span data-ttu-id="9750e-107">請參閱＜備註＞一節。</span><span class="sxs-lookup"><span data-stu-id="9750e-107">See the Remarks section.</span></span>  
  
 `ppReturnValue`  
 <span data-ttu-id="9750e-108">"ICorDebugValue" 介面物件位址的指標，提供函式呼叫傳回值的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9750e-108">A pointer to the address of an "ICorDebugValue" interface object that provides information about the return value of a function call.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="9750e-109">備註</span><span class="sxs-lookup"><span data-stu-id="9750e-109">Remarks</span></span>  

 <span data-ttu-id="9750e-110">這個方法會搭配 [ICorDebugCode3：： GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) 方法使用，以取得方法的傳回值。</span><span class="sxs-lookup"><span data-stu-id="9750e-110">This method is used along with the [ICorDebugCode3::GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) method to get the return value of a method.</span></span> <span data-ttu-id="9750e-111">在會忽略傳回值的方法中，這種方法特別有用，如下列兩個程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="9750e-111">It is particularly useful in the case of methods whose return values are ignored, as in the following two code examples.</span></span> <span data-ttu-id="9750e-112">第一個範例會呼叫 <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> 方法，但會忽略方法的傳回值。</span><span class="sxs-lookup"><span data-stu-id="9750e-112">The first example calls the <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> method, but ignores the method's return value.</span></span>  
  
 [!code-csharp[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv1.cs#1)]
 [!code-vb[Unmanaged.Debugging.MRV#1](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv1.vb#1)]  
  
 <span data-ttu-id="9750e-113">第二個範例說明更常見的調試問題。</span><span class="sxs-lookup"><span data-stu-id="9750e-113">The second example illustrates a much more common problem in debugging.</span></span> <span data-ttu-id="9750e-114">由於方法會當做方法呼叫中的引數使用，因此只有在偵錯工具逐步執行呼叫的方法時，才能存取其傳回值。</span><span class="sxs-lookup"><span data-stu-id="9750e-114">Because a method is used as an argument in a method call, its return value is accessible only when the debugger steps through the called method.</span></span> <span data-ttu-id="9750e-115">在許多情況下，尤其是在外部程式庫中定義了被呼叫的方法時，就無法這麼做。</span><span class="sxs-lookup"><span data-stu-id="9750e-115">In many cases, particularly when the called method is defined in an external library, that is not possible.</span></span>  
  
 [!code-csharp[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/csharp/VS_Snippets_CLR/unmanaged.debugging.mrv/cs/mrv2.cs#2)]
 [!code-vb[Unmanaged.Debugging.MRV#2](../../../../samples/snippets/visualbasic/VS_Snippets_CLR/unmanaged.debugging.mrv/vb/mrv2.vb#2)]  
  
 <span data-ttu-id="9750e-116">如果您傳遞 [ICorDebugCode3：： GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) 方法至函式呼叫位置的 IL 位移，則會傳回一或多個原生位移。</span><span class="sxs-lookup"><span data-stu-id="9750e-116">If you pass the [ICorDebugCode3::GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) method an IL offset to a function call site, it returns one or more native offsets.</span></span> <span data-ttu-id="9750e-117">然後，偵錯工具可以在函式中的這些原生位移上設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="9750e-117">The debugger can then set breakpoints on these native offsets in the function.</span></span> <span data-ttu-id="9750e-118">當偵錯工具到達其中一個中斷點時，您便可以傳遞您傳遞給這個方法的相同 IL 位移，以取得傳回值。</span><span class="sxs-lookup"><span data-stu-id="9750e-118">When the debugger hits one of the breakpoints, you can then pass the same IL offset that you passed to this method to get the return value.</span></span> <span data-ttu-id="9750e-119">偵錯工具接著應清除其設定的所有中斷點。</span><span class="sxs-lookup"><span data-stu-id="9750e-119">The debugger should then clear all the breakpoints that it set.</span></span>  
  
> [!WARNING]
> <span data-ttu-id="9750e-120">[ICorDebugCode3：： GetReturnValueLiveOffset 方法](icordebugcode3-getreturnvalueliveoffset-method.md)和 `ICorDebugILFrame3::GetReturnValueForILOffset` 方法可讓您只取得參考型別的傳回值資訊。</span><span class="sxs-lookup"><span data-stu-id="9750e-120">The [ICorDebugCode3::GetReturnValueLiveOffset Method](icordebugcode3-getreturnvalueliveoffset-method.md) and `ICorDebugILFrame3::GetReturnValueForILOffset` methods allow you to get return value information for reference types only.</span></span> <span data-ttu-id="9750e-121">從實值型別中取出傳回值資訊 (也就是說，不支援衍生自) 的所有類型 <xref:System.ValueType> 。</span><span class="sxs-lookup"><span data-stu-id="9750e-121">Retrieving return value information from value types (that is, all types that derive from <xref:System.ValueType>) is not supported.</span></span>  
  
 <span data-ttu-id="9750e-122">參數所指定的 IL 位移 `ILOffset` 應該位於函式呼叫位置，而偵錯工具應該在針對相同 IL 位移的 [ICorDebugCode3：： GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) 方法所傳回的原生位移上設定的中斷點停止。</span><span class="sxs-lookup"><span data-stu-id="9750e-122">The IL offset specified by the `ILOffset` parameter should be at a function call site, and the debuggee should be stopped at a breakpoint set at the native offset returned by the [ICorDebugCode3::GetReturnValueLiveOffset](icordebugcode3-getreturnvalueliveoffset-method.md) method for the same IL offset.</span></span> <span data-ttu-id="9750e-123">如果偵錯工具未在指定之 IL 位移的正確位置停止，API 將會失敗。</span><span class="sxs-lookup"><span data-stu-id="9750e-123">If the debuggee is not stopped at the correct location for the specified IL offset, the API will fail.</span></span>  
  
 <span data-ttu-id="9750e-124">如果函式呼叫不會傳回值，API 將會失敗。</span><span class="sxs-lookup"><span data-stu-id="9750e-124">If the function call doesn't return a value, the API will fail.</span></span>  
  
 <span data-ttu-id="9750e-125">`ICorDebugILFrame3::GetReturnValueForILOffset`只有 x86 型和 AMD64 系統才能使用此方法。</span><span class="sxs-lookup"><span data-stu-id="9750e-125">The `ICorDebugILFrame3::GetReturnValueForILOffset` method is available only on x86-based and AMD64 systems.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="9750e-126">需求</span><span class="sxs-lookup"><span data-stu-id="9750e-126">Requirements</span></span>  

 <span data-ttu-id="9750e-127">**平台：** 請參閱 [系統需求](../../get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="9750e-127">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="9750e-128">**標頭：** CorDebug.idl、CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="9750e-128">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="9750e-129">**程式庫：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="9750e-129">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="9750e-130">**.NET Framework 版本：**[!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="9750e-130">**.NET Framework Versions:** [!INCLUDE[net_current_v451plus](../../../../includes/net-current-v451plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9750e-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9750e-131">See also</span></span>

- [<span data-ttu-id="9750e-132">GetReturnValueLiveOffset 方法</span><span class="sxs-lookup"><span data-stu-id="9750e-132">GetReturnValueLiveOffset Method</span></span>](icordebugcode3-getreturnvalueliveoffset-method.md)
- [<span data-ttu-id="9750e-133">ICorDebugILFrame3 介面</span><span class="sxs-lookup"><span data-stu-id="9750e-133">ICorDebugILFrame3 Interface</span></span>](icordebugilframe3-interface.md)
