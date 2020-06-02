---
title: 作法：取消 PLINQ 查詢
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to cancel
- cancellation, PLINQ
ms.assetid: 80b14640-edfa-4153-be1b-3e003d3e9c1a
ms.openlocfilehash: 09405a8a9f5d96d80454bcc98cbf29db54df6725
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288208"
---
# <a name="how-to-cancel-a-plinq-query"></a><span data-ttu-id="58bbd-102">作法：取消 PLINQ 查詢</span><span class="sxs-lookup"><span data-stu-id="58bbd-102">How to: Cancel a PLINQ Query</span></span>
<span data-ttu-id="58bbd-103">下列範例說明取消 PLINQ 查詢的兩種方式。</span><span class="sxs-lookup"><span data-stu-id="58bbd-103">The following examples show two ways to cancel a PLINQ query.</span></span> <span data-ttu-id="58bbd-104">第一個範例示範如何取消大部分由資料周遊所組成的查詢。</span><span class="sxs-lookup"><span data-stu-id="58bbd-104">The first example shows how to cancel a query that consists mostly of data traversal.</span></span> <span data-ttu-id="58bbd-105">第二個範例示範如何取消包含需要大量計算之使用者函式的查詢。</span><span class="sxs-lookup"><span data-stu-id="58bbd-105">The second example shows how to cancel a query that contains a user function that is computationally expensive.</span></span>

> [!NOTE]
> <span data-ttu-id="58bbd-106">啟用 [Just My Code] 時，Visual Studio 會在擲回例外狀況的字行上中斷，並顯示錯誤訊息，指出「使用者程式碼未處理例外狀況」。</span><span class="sxs-lookup"><span data-stu-id="58bbd-106">When "Just My Code" is enabled, Visual Studio will break on the line that throws the exception and display an error message that says "exception not handled by user code."</span></span> <span data-ttu-id="58bbd-107">這個錯誤是良性的。</span><span class="sxs-lookup"><span data-stu-id="58bbd-107">This error is benign.</span></span> <span data-ttu-id="58bbd-108">您可以按 F5 鍵繼續，並查看下面範例中示範的例外狀況處理行為。</span><span class="sxs-lookup"><span data-stu-id="58bbd-108">You can press F5 to continue from it, and see the exception-handling behavior that is demonstrated in the examples below.</span></span> <span data-ttu-id="58bbd-109">若要防止 Visual Studio 在遇到第一個錯誤時就中斷，只要取消核取 [工具]、[選項]、[偵錯]、[一般]\*\*\*\* 下的 [Just My Code] 核取方塊即可。</span><span class="sxs-lookup"><span data-stu-id="58bbd-109">To prevent Visual Studio from breaking on the first error, just uncheck the "Just My Code" checkbox under **Tools, Options, Debugging, General**.</span></span>
>
> <span data-ttu-id="58bbd-110">這個範例是為了示範用法，執行速度可能比不上對應的循序 LINQ to Objects 查詢。</span><span class="sxs-lookup"><span data-stu-id="58bbd-110">This example is intended to demonstrate usage, and might not run faster than the equivalent sequential LINQ to Objects query.</span></span> <span data-ttu-id="58bbd-111">如需加速的詳細資訊，請參閱[認識 PLINQ 中的加速](understanding-speedup-in-plinq.md)。</span><span class="sxs-lookup"><span data-stu-id="58bbd-111">For more information about speedup, see [Understanding Speedup in PLINQ](understanding-speedup-in-plinq.md).</span></span>

## <a name="example"></a><span data-ttu-id="58bbd-112">範例</span><span class="sxs-lookup"><span data-stu-id="58bbd-112">Example</span></span>

[!code-csharp[PLINQ#16](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#16)]
[!code-vb[PLINQ#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#16)]

<span data-ttu-id="58bbd-113">PLINQ 架構不會將單一 <xref:System.OperationCanceledException> 累計到 <xref:System.AggregateException?displayProperty=nameWithType>；<xref:System.OperationCanceledException> 必須在個別的 catch 區塊中處理。</span><span class="sxs-lookup"><span data-stu-id="58bbd-113">The PLINQ framework does not roll a single <xref:System.OperationCanceledException> into an <xref:System.AggregateException?displayProperty=nameWithType>; the <xref:System.OperationCanceledException> must be handled in a separate catch block.</span></span> <span data-ttu-id="58bbd-114">如果一或多個使用者委派擲回 OperationCanceledException(externalCT) (使用外部 <xref:System.Threading.CancellationToken?displayProperty=nameWithType>)，但沒有其他例外狀況，而查詢定義為 `AsParallel().WithCancellation(externalCT)`，PLINQ 將會發出單一 <xref:System.OperationCanceledException> (externalCT) 而不是 <xref:System.AggregateException?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="58bbd-114">If one or more user delegates throws an OperationCanceledException(externalCT) (by using an external <xref:System.Threading.CancellationToken?displayProperty=nameWithType>) but no other exception, and the query was defined as `AsParallel().WithCancellation(externalCT)`, then PLINQ will issue a single <xref:System.OperationCanceledException> (externalCT) rather than an <xref:System.AggregateException?displayProperty=nameWithType>.</span></span> <span data-ttu-id="58bbd-115">不過，如果一位使用者委派擲回 <xref:System.OperationCanceledException>，另一個委派擲回其他例外狀況類型，則這兩個例外狀況將會累計到 <xref:System.AggregateException>。</span><span class="sxs-lookup"><span data-stu-id="58bbd-115">However, if one user delegate throws an <xref:System.OperationCanceledException>, and another delegate throws another exception type, then both exceptions will be rolled into an <xref:System.AggregateException>.</span></span>

<span data-ttu-id="58bbd-116">取消作業的一般指引如下：</span><span class="sxs-lookup"><span data-stu-id="58bbd-116">The general guidance on cancellation is as follows:</span></span>

1. <span data-ttu-id="58bbd-117">如果您執行使用者委派取消，您應該通知 PLINQ 有關外部的， <xref:System.Threading.CancellationToken> 並擲回 <xref:System.OperationCanceledException> （externalCT）。</span><span class="sxs-lookup"><span data-stu-id="58bbd-117">If you perform user-delegate cancellation, you should inform PLINQ about the external <xref:System.Threading.CancellationToken> and throw an <xref:System.OperationCanceledException>(externalCT).</span></span>

2. <span data-ttu-id="58bbd-118">如果發生取消，而且沒有擲回其他例外狀況，則會處理， <xref:System.OperationCanceledException> 而非 <xref:System.AggregateException> 。</span><span class="sxs-lookup"><span data-stu-id="58bbd-118">If cancellation occurs and no other exceptions are thrown, then handle an <xref:System.OperationCanceledException> rather than an <xref:System.AggregateException>.</span></span>

## <a name="example"></a><span data-ttu-id="58bbd-119">範例</span><span class="sxs-lookup"><span data-stu-id="58bbd-119">Example</span></span>

<span data-ttu-id="58bbd-120">下列範例示範當使用者程式碼中含有計算成本很高之函數時，應如何處理取消作業。</span><span class="sxs-lookup"><span data-stu-id="58bbd-120">The following example shows how to handle cancellation when you have a computationally expensive function in user code.</span></span>

[!code-csharp[PLINQ#17](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#17)]
[!code-vb[PLINQ#17](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#17)]

<span data-ttu-id="58bbd-121">處理使用者程式碼中的取消作業時，不需在查詢定義中使用 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A>。</span><span class="sxs-lookup"><span data-stu-id="58bbd-121">When you handle the cancellation in user code, you do not have to use <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> in the query definition.</span></span> <span data-ttu-id="58bbd-122">不過，我們建議您務必使用 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> ，因為 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> 不會影響查詢效能，而且可讓查詢運算子和您的使用者程式碼來處理取消作業。</span><span class="sxs-lookup"><span data-stu-id="58bbd-122">However, we recommended that you do use <xref:System.Linq.ParallelEnumerable.WithCancellation%2A>, because <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> has no effect on query performance and it enables the cancellation to be handled by query operators and your user code.</span></span>

<span data-ttu-id="58bbd-123">為確保系統回應能力，建議您每毫秒檢查一次是否有取消作業；不過，系統可以接受最多 10 毫秒的任何週期。</span><span class="sxs-lookup"><span data-stu-id="58bbd-123">In order to ensure system responsiveness, we recommend that you check for cancellation around once per millisecond; however, any period up to 10 milliseconds is considered acceptable.</span></span> <span data-ttu-id="58bbd-124">此頻率對您的程式碼效能應該沒有負面影響。</span><span class="sxs-lookup"><span data-stu-id="58bbd-124">This frequency should not have a negative impact on your code's performance.</span></span>

<span data-ttu-id="58bbd-125">在處置枚舉器時（例如，當程式碼在反復查看查詢結果的 foreach （針對 Visual Basic 中的每個）迴圈中中斷時，會取消查詢，但不會擲回任何例外狀況。</span><span class="sxs-lookup"><span data-stu-id="58bbd-125">When an enumerator is disposed, for example when code breaks out of a foreach (For Each in Visual Basic) loop that is iterating over query results, then the query is canceled, but no exception is thrown.</span></span>

## <a name="see-also"></a><span data-ttu-id="58bbd-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="58bbd-126">See also</span></span>

- <xref:System.Linq.ParallelEnumerable>
- [<span data-ttu-id="58bbd-127">平行 LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="58bbd-127">Parallel LINQ (PLINQ)</span></span>](introduction-to-plinq.md)
- [<span data-ttu-id="58bbd-128">Managed 執行緒中的取消作業</span><span class="sxs-lookup"><span data-stu-id="58bbd-128">Cancellation in Managed Threads</span></span>](../threading/cancellation-in-managed-threads.md)
