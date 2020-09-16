---
title: 作法：建立並執行簡單的 PLINQ 查詢
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to create
ms.assetid: 983b4213-bddd-4a44-9262-cbe59186df4c
ms.openlocfilehash: a5f6a26ada321bd351249c5179d050ee571b550c
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679332"
---
# <a name="how-to-create-and-execute-a-simple-plinq-query"></a><span data-ttu-id="f8190-102">作法：建立並執行簡單的 PLINQ 查詢</span><span class="sxs-lookup"><span data-stu-id="f8190-102">How to: Create and Execute a Simple PLINQ Query</span></span>

<span data-ttu-id="f8190-103">本文中的範例說明如何 <xref:System.Linq.ParallelEnumerable.AsParallel%2A?displayProperty=nameWithType> 在來源序列上使用擴充方法，並使用方法來執行查詢，以建立簡單的平行語言整合查詢 (LINQ) 查詢 <xref:System.Linq.ParallelEnumerable.ForAll%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="f8190-103">The example in this article shows how to create a simple Parallel Language Integrated Query (LINQ) query by using the <xref:System.Linq.ParallelEnumerable.AsParallel%2A?displayProperty=nameWithType> extension method on the source sequence and executing the query by using the <xref:System.Linq.ParallelEnumerable.ForAll%2A?displayProperty=nameWithType> method.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f8190-104">本文件使用 Lambda 運算式來定義 PLINQ 中的委派。</span><span class="sxs-lookup"><span data-stu-id="f8190-104">This documentation uses lambda expressions to define delegates in PLINQ.</span></span> <span data-ttu-id="f8190-105">如果您不熟悉 C# 或 Visual Basic 中的 Lambda 運算式，請參閱 [PLINQ 和 TPL 中的 Lambda 運算式](lambda-expressions-in-plinq-and-tpl.md)。</span><span class="sxs-lookup"><span data-stu-id="f8190-105">If you are not familiar with lambda expressions in C# or Visual Basic, see [Lambda Expressions in PLINQ and TPL](lambda-expressions-in-plinq-and-tpl.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="f8190-106">範例</span><span class="sxs-lookup"><span data-stu-id="f8190-106">Example</span></span>  
 [!code-csharp[PLINQ#11](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/create1.cs#11)]
 [!code-vb[PLINQ#11](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/create1.vb#11)]  
  
 <span data-ttu-id="f8190-107">此範例示範在結果序列的順序不重要的情況下，用來建立及執行任何平行 LINQ 查詢的基本模式。</span><span class="sxs-lookup"><span data-stu-id="f8190-107">This example demonstrates the basic pattern for creating and executing any Parallel LINQ query when the ordering of the result sequence is not important.</span></span> <span data-ttu-id="f8190-108">未排序的查詢通常比排序的查詢更快。</span><span class="sxs-lookup"><span data-stu-id="f8190-108">Unordered queries are generally faster than ordered queries.</span></span> <span data-ttu-id="f8190-109">查詢會將來源分割成在多個執行緒上非同步執行的工作。</span><span class="sxs-lookup"><span data-stu-id="f8190-109">The query partitions the source into tasks that are executed asynchronously on multiple threads.</span></span> <span data-ttu-id="f8190-110">每項工作的完成順序不僅取決於處理分割中的項目時所涉及的工作量，也取決於一些外部因素，例如作業系統排程每個執行緒的方式。</span><span class="sxs-lookup"><span data-stu-id="f8190-110">The order in which each task completes depends not only on the amount of work involved to process the elements in the partition, but also on external factors such as how the operating system schedules each thread.</span></span> <span data-ttu-id="f8190-111">這個範例是為了示範用法，執行速度可能比不上對應的循序 LINQ to Objects 查詢。</span><span class="sxs-lookup"><span data-stu-id="f8190-111">This example is intended to demonstrate usage, and might not run faster than the equivalent sequential LINQ to Objects query.</span></span> <span data-ttu-id="f8190-112">如需加速的詳細資訊，請參閱[認識 PLINQ 中的加速](understanding-speedup-in-plinq.md)。</span><span class="sxs-lookup"><span data-stu-id="f8190-112">For more information about speedup, see [Understanding Speedup in PLINQ](understanding-speedup-in-plinq.md).</span></span> <span data-ttu-id="f8190-113">如需如何在查詢中保留元素順序的詳細資訊，請參閱[如何：控制 PLINQ 查詢中的順序](how-to-control-ordering-in-a-plinq-query.md)。</span><span class="sxs-lookup"><span data-stu-id="f8190-113">For more information about how to preserve the ordering of elements in a query, see [How to: Control Ordering in a PLINQ Query](how-to-control-ordering-in-a-plinq-query.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f8190-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f8190-114">See also</span></span>

- [<span data-ttu-id="f8190-115">平行 LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="f8190-115">Parallel LINQ (PLINQ)</span></span>](introduction-to-plinq.md)
