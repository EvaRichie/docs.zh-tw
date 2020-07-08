---
title: invalidCERCall MDA
description: 檢查 invalidCERCall managed 偵錯工具（MDA），這是在限制的執列區域（CER）圖形中有不正確呼叫時啟動的。
ms.date: 03/30/2017
helpviewer_keywords:
- invalid CER calls
- InvalidCERCall MDA
- MDAs (managed debugging assistants), CER calls
- constrained execution regions
- CER calls
- managed debugging assistants (MDAs), CER calls
ms.assetid: c4577410-602e-44e5-9dab-fea7c55bcdfe
ms.openlocfilehash: dec32a81929d72274757b75cb03d6615d9fa948b
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051788"
---
# <a name="invalidcercall-mda"></a><span data-ttu-id="76cf9-103">invalidCERCall MDA</span><span class="sxs-lookup"><span data-stu-id="76cf9-103">invalidCERCall MDA</span></span>
<span data-ttu-id="76cf9-104">當方法的限制執行區域 (CER) 圖形內的呼叫沒有可靠性合約或過度弱式合約時，就會啟動 `invalidCERCall` Managed 偵錯助理 (MDA)。</span><span class="sxs-lookup"><span data-stu-id="76cf9-104">The `invalidCERCall` managed debugging assistant (MDA) is activated when there is a call within the constrained execution region (CER) graph to a method that has no reliability contract or an excessively weak contract.</span></span> <span data-ttu-id="76cf9-105">弱式合約是宣告最差狀態損毀範圍超過執行個體傳遞至呼叫的範圍，也就是 <xref:System.AppDomain> 或處理序狀態可能會損毀，或在 CER 內呼叫時，其結果不一定是決定性可計算結果。</span><span class="sxs-lookup"><span data-stu-id="76cf9-105">A weak contract is a contract that declares that the worst case state corruption is of greater scope than the instance passed to the call, that is, the <xref:System.AppDomain> or process state may become corrupted or that its result is not always deterministically computable when called within a CER.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="76cf9-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="76cf9-106">Symptoms</span></span>  
 <span data-ttu-id="76cf9-107">在 CER 中執行程式碼時出現非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="76cf9-107">Unexpected results when executing code in a CER.</span></span> <span data-ttu-id="76cf9-108">沒有特定的徵兆。</span><span class="sxs-lookup"><span data-stu-id="76cf9-108">The symptoms are not specific.</span></span> <span data-ttu-id="76cf9-109">它們可能是未預期的 <xref:System.OutOfMemoryException>、<xref:System.Threading.ThreadAbortException> 或在呼叫不可靠的方法時發生的其他例外狀況，因為執行階段未事先準備或保護它免於執行階段的 <xref:System.Threading.ThreadAbortException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="76cf9-109">They could be an unexpected <xref:System.OutOfMemoryException>, a <xref:System.Threading.ThreadAbortException>, or other exceptions at the call into the unreliable method because the runtime did not prepare it ahead of time or protect it from <xref:System.Threading.ThreadAbortException> exceptions at run time.</span></span> <span data-ttu-id="76cf9-110">更大的威脅就是，在執行階段因方法造成的任何例外狀況，都可能讓 <xref:System.AppDomain> 或處理序處於不穩定的狀態，違反 CER 目標。</span><span class="sxs-lookup"><span data-stu-id="76cf9-110">A greater threat is that any exception resulting from the method at run time could leave the <xref:System.AppDomain> or process in an unstable state, which is contrary to the objective of a CER.</span></span> <span data-ttu-id="76cf9-111">建立 CER 的原因是為了避免這類的狀態損毀。</span><span class="sxs-lookup"><span data-stu-id="76cf9-111">The reason a CER is created is to avoid state corruptions such as this.</span></span> <span data-ttu-id="76cf9-112">損毀狀態的徵兆隨應用程式而異，因為應用程式之間的一致狀態定義各不相同。</span><span class="sxs-lookup"><span data-stu-id="76cf9-112">The symptoms of corrupt state are application specific because the definition of consistent state is different between applications.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="76cf9-113">原因</span><span class="sxs-lookup"><span data-stu-id="76cf9-113">Cause</span></span>  
 <span data-ttu-id="76cf9-114">CER 中的程式碼要呼叫沒有 <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> 的函式，或使用與 CER 中所執行者不相容之弱式 <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> 的函式。</span><span class="sxs-lookup"><span data-stu-id="76cf9-114">Code within a CER is calling a function with no <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> or with a weak <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> that is not compatible with running in a CER.</span></span>  
  
 <span data-ttu-id="76cf9-115">就可靠性合約語法而言，弱式合約是未指定 <xref:System.Runtime.ConstrainedExecution.Consistency> 列舉值或指定 <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptProcess>、<xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptAppDomain> 或 <xref:System.Runtime.ConstrainedExecution.Cer.None> 之 <xref:System.Runtime.ConstrainedExecution.Consistency> 值的合約。</span><span class="sxs-lookup"><span data-stu-id="76cf9-115">In terms of reliability contract syntax, a weak contract is a contract that does not specify a <xref:System.Runtime.ConstrainedExecution.Consistency> enumeration value or specifies a <xref:System.Runtime.ConstrainedExecution.Consistency> value of <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptProcess>, <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptAppDomain>, or <xref:System.Runtime.ConstrainedExecution.Cer.None>.</span></span> <span data-ttu-id="76cf9-116">任何這些狀況都指出，呼叫的程式碼可能會阻礙 CER 中其他程式碼的工作，以維護一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="76cf9-116">Any of these conditions indicates that the code called may impede the efforts of the other code in the CER to maintain consistent state.</span></span>  <span data-ttu-id="76cf9-117">CER 允許程式碼以非常確定的方式處理錯誤，維護對應用程式相當重要的內部非變異值，並讓它繼續在記憶體不足例外狀況等暫時性錯誤的情況下執行。</span><span class="sxs-lookup"><span data-stu-id="76cf9-117">CERs allow code to treat errors in a very deterministic manner, maintaining internal invariants that are important to the application and allowing it to continue running in the face of transient errors such as out-of-memory exceptions.</span></span>  
  
 <span data-ttu-id="76cf9-118">啟動此 MDA 指出在 CER 中呼叫方法，可能會因為呼叫端未預期的方式，或讓 <xref:System.AppDomain> 或處理序保持損毀或無法修復的狀態而失敗。</span><span class="sxs-lookup"><span data-stu-id="76cf9-118">The activation of this MDA indicates a possibility the method being called in the CER can fail in a way that the caller did not expect or that leaves the <xref:System.AppDomain> or process state corrupted or unrecoverable.</span></span> <span data-ttu-id="76cf9-119">當然，呼叫的程式碼可能會正確執行，而此問題只是遺漏合約。</span><span class="sxs-lookup"><span data-stu-id="76cf9-119">Of course, the called code might execute correctly and the problem is simply a missing contract.</span></span> <span data-ttu-id="76cf9-120">不過，有關撰寫可靠程式碼的問題是很微妙的，缺少合約明顯表示程式碼可能不會正確執行。</span><span class="sxs-lookup"><span data-stu-id="76cf9-120">However, the issues involved in writing reliable code are subtle and the absence of a contract is a good indicator the code might not execute correctly.</span></span> <span data-ttu-id="76cf9-121">合約表示程式設計人員是以可靠方式編寫程式碼，並承諾在未來修訂程式碼時也不會變更這些保證。</span><span class="sxs-lookup"><span data-stu-id="76cf9-121">The contracts are indicators that the programmer has coded reliably and also promises that these guarantees will not change in future revisions of the code.</span></span>  <span data-ttu-id="76cf9-122">也就是說，合約宣告的是意圖，而不僅是實作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="76cf9-122">That is, the contracts are declarations of intent and not just implementation details.</span></span>  
  
 <span data-ttu-id="76cf9-123">因為任何具有弱式或不存在合約的方法，可能以許多無法預測的方式失敗，所以執行階段不會嘗試從方法中移除任何它本身無法預測的失敗；例如，從延遲的 JIT 編譯、泛型字典母體擴展或執行緒中止所導入的失敗。</span><span class="sxs-lookup"><span data-stu-id="76cf9-123">Because any method with a weak or nonexistent contract can potentially fail in many unpredictable ways, the runtime does not attempt to remove any of its own unpredictable failures from the method  that are introduced by lazy JIT-compiling, generics dictionary population, or thread aborts, for example.</span></span> <span data-ttu-id="76cf9-124">亦即，啟動此 MDA 時，它會指出執行階段未包含要定義之 CER 中的呼叫方法；這個節點已終止呼叫歷程圖，因為繼續準備此子樹狀結構會幫助遮罩潛在的錯誤。</span><span class="sxs-lookup"><span data-stu-id="76cf9-124">That is, when this MDA is activated, it indicates that the runtime did not include the called method in the CER being defined; the call graph was terminated at this node because continuing to prepare this subtree would help mask the potential error.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="76cf9-125">解決方案</span><span class="sxs-lookup"><span data-stu-id="76cf9-125">Resolution</span></span>  
 <span data-ttu-id="76cf9-126">將有效的可靠性合約新增至函式，或避免使用該函式呼叫。</span><span class="sxs-lookup"><span data-stu-id="76cf9-126">Add a valid reliability contract to the function or avoid using that function call.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="76cf9-127">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="76cf9-127">Effect on the Runtime</span></span>  
 <span data-ttu-id="76cf9-128">從 CER 呼叫弱式合約的效果，可能會讓 CER 無法完成其作業。</span><span class="sxs-lookup"><span data-stu-id="76cf9-128">The effect of calling a weak contract from a CER could be the CER failure to complete its operations.</span></span> <span data-ttu-id="76cf9-129">這可能會導致 <xref:System.AppDomain> 處理序狀態損毀。</span><span class="sxs-lookup"><span data-stu-id="76cf9-129">This could lead to corruption of the <xref:System.AppDomain> process state.</span></span>  
  
## <a name="output"></a><span data-ttu-id="76cf9-130">輸出</span><span class="sxs-lookup"><span data-stu-id="76cf9-130">Output</span></span>  
 <span data-ttu-id="76cf9-131">下列是來自此 MDA 的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="76cf9-131">The following is sample output from this MDA.</span></span>  
  
 `Method 'MethodWithCer', while executing within a constrained execution region, makes a call at IL offset 0x000C to 'MethodWithWeakContract', which does not have a sufficiently strong reliability contract and might cause non-deterministic results.`  
  
## <a name="configuration"></a><span data-ttu-id="76cf9-132">組態</span><span class="sxs-lookup"><span data-stu-id="76cf9-132">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="76cf9-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="76cf9-133">See also</span></span>

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>
- <xref:System.Runtime.ConstrainedExecution>
- [<span data-ttu-id="76cf9-134">使用 Managed 偵錯助理診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="76cf9-134">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
