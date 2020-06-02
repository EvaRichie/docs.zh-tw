---
title: 作法：加速小型迴圈主體
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to speed up
ms.assetid: c7a66677-cb59-4cbf-969a-d2e8fc61a6ce
ms.openlocfilehash: 4983cafb9d4a72262dc7a6a6c37fab23937b3274
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288078"
---
# <a name="how-to-speed-up-small-loop-bodies"></a><span data-ttu-id="96636-102">作法：加速小型迴圈主體</span><span class="sxs-lookup"><span data-stu-id="96636-102">How to: Speed Up Small Loop Bodies</span></span>
<span data-ttu-id="96636-103">當 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 迴圈有小型的主體時，其執行速度可能會比同等的循序迴圈更慢，例如 C# 中的 [for](../../csharp/language-reference/keywords/for.md) 迴圈和 Visual Basic 中的 [For](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/44kykk21(v=vs.90)) 迴圈。</span><span class="sxs-lookup"><span data-stu-id="96636-103">When a <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> loop has a small body, it might perform more slowly than the equivalent sequential loop, such as the [for](../../csharp/language-reference/keywords/for.md) loop in C# and the [For](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/44kykk21(v=vs.90)) loop in Visual Basic.</span></span> <span data-ttu-id="96636-104">效能較慢的起因是分割資料時相關的負擔，以及在每次迴圈反覆運算上叫用委派的成本。</span><span class="sxs-lookup"><span data-stu-id="96636-104">Slower performance is caused by the overhead involved in partitioning the data and the cost of invoking a delegate on each loop iteration.</span></span> <span data-ttu-id="96636-105">為了解決這類情況，<xref:System.Collections.Concurrent.Partitioner> 類別提供 <xref:System.Collections.Concurrent.Partitioner.Create%2A?displayProperty=nameWithType> 方法，可讓您提供循序迴圈給委派主體，讓每個資料分割只叫用一次委派，而不會每個反覆項目叫用一次。</span><span class="sxs-lookup"><span data-stu-id="96636-105">To address such scenarios, the <xref:System.Collections.Concurrent.Partitioner> class provides the <xref:System.Collections.Concurrent.Partitioner.Create%2A?displayProperty=nameWithType> method, which enables you to provide a sequential loop for the delegate body, so that the delegate is invoked only once per partition, instead of once per iteration.</span></span> <span data-ttu-id="96636-106">如需詳細資訊，請參閱 [PLINQ 和 TPL 的自訂 Partitioner](custom-partitioners-for-plinq-and-tpl.md)。</span><span class="sxs-lookup"><span data-stu-id="96636-106">For more information, see [Custom Partitioners for PLINQ and TPL](custom-partitioners-for-plinq-and-tpl.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="96636-107">範例</span><span class="sxs-lookup"><span data-stu-id="96636-107">Example</span></span>  
 [!code-csharp[TPL_Partitioners#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioner01.cs#01)]
 [!code-vb[TPL_Partitioners#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionercreate01.vb#01)]  
  
 <span data-ttu-id="96636-108">在此範例中示範的方法適用於迴圈執行最少量工作的情況。</span><span class="sxs-lookup"><span data-stu-id="96636-108">The approach demonstrated in this example is useful when the loop performs a minimal amount of work.</span></span> <span data-ttu-id="96636-109">當工作變得更運算密集時，藉由使用 <xref:System.Threading.Tasks.Parallel.For%2A> 或 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 迴圈與預設 Partitioner，您可能會取得相同或更高的效能。</span><span class="sxs-lookup"><span data-stu-id="96636-109">As the work becomes more computationally expensive, you will probably get the same or better performance by using a <xref:System.Threading.Tasks.Parallel.For%2A> or <xref:System.Threading.Tasks.Parallel.ForEach%2A> loop with the default partitioner.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="96636-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="96636-110">See also</span></span>

- [<span data-ttu-id="96636-111">資料平行處理</span><span class="sxs-lookup"><span data-stu-id="96636-111">Data Parallelism</span></span>](data-parallelism-task-parallel-library.md)
- [<span data-ttu-id="96636-112">PLINQ 和 TPL 的自訂 Partitioner</span><span class="sxs-lookup"><span data-stu-id="96636-112">Custom Partitioners for PLINQ and TPL</span></span>](custom-partitioners-for-plinq-and-tpl.md)
- [<span data-ttu-id="96636-113">迭代器 (C#)</span><span class="sxs-lookup"><span data-stu-id="96636-113">Iterators (C#)</span></span>](../../csharp/programming-guide/concepts/iterators.md)
- [<span data-ttu-id="96636-114">迭代器 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="96636-114">Iterators (Visual Basic)</span></span>](../../visual-basic/programming-guide/concepts/iterators.md)
- [<span data-ttu-id="96636-115">PLINQ 和 TPL 中的 Lambda 運算式</span><span class="sxs-lookup"><span data-stu-id="96636-115">Lambda Expressions in PLINQ and TPL</span></span>](lambda-expressions-in-plinq-and-tpl.md)
