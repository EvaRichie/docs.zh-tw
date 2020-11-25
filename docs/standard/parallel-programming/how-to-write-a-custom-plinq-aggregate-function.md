---
title: 作法：撰寫自訂 PLINQ 彙總函式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to create aggregate function
ms.assetid: 5a70dd49-ab2a-4798-b551-196ee7042b1a
ms.openlocfilehash: dc03802c960c0926380d7b7fa44fdf436b8fea89
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734253"
---
# <a name="how-to-write-a-custom-plinq-aggregate-function"></a><span data-ttu-id="d9ec3-102">作法：撰寫自訂 PLINQ 彙總函式</span><span class="sxs-lookup"><span data-stu-id="d9ec3-102">How to: Write a Custom PLINQ Aggregate Function</span></span>

<span data-ttu-id="d9ec3-103">此範例示範如何使用 <xref:System.Linq.ParallelEnumerable.Aggregate%2A> 方法，將自訂彙總函式套用至來源序列。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-103">This example shows how to use the <xref:System.Linq.ParallelEnumerable.Aggregate%2A> method to apply a custom aggregation function to a source sequence.</span></span>  
  
> [!WARNING]
> <span data-ttu-id="d9ec3-104">這個範例是為了示範用法，執行速度可能比不上對應的循序 LINQ to Objects 查詢。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-104">This example is intended to demonstrate usage, and might not run faster than the equivalent sequential LINQ to Objects query.</span></span> <span data-ttu-id="d9ec3-105">如需加速的詳細資訊，請參閱[認識 PLINQ 中的加速](understanding-speedup-in-plinq.md)。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-105">For more information about speedup, see [Understanding Speedup in PLINQ](understanding-speedup-in-plinq.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="d9ec3-106">範例</span><span class="sxs-lookup"><span data-stu-id="d9ec3-106">Example</span></span>  

 <span data-ttu-id="d9ec3-107">下列範例會計算整數序列的標準差。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-107">The following example calculates the standard deviation of a sequence of integers.</span></span>  
  
 [!code-csharp[PLINQ#31](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#31)]
 [!code-vb[PLINQ#31](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#31)]  
  
 <span data-ttu-id="d9ec3-108">此範例會使用 PLINQ 特有之 Aggregate 標準查詢運算子的多載。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-108">This example uses an overload of the Aggregate standard query operator that is unique to PLINQ.</span></span> <span data-ttu-id="d9ec3-109">這個多載會採用額外的 <xref:System.Func%603?displayProperty=nameWithType> 做為第三個輸入參數。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-109">This overload takes an extra <xref:System.Func%603?displayProperty=nameWithType> as the third input parameter.</span></span> <span data-ttu-id="d9ec3-110">在執行彙總結果的最終計算之前，這個委派會合併所有執行緒的結果。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-110">This delegate combines the results from all threads before it performs the final calculation on the aggregated results.</span></span> <span data-ttu-id="d9ec3-111">在此範例中，我們加入所有執行緒的加總。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-111">In this example we add together the sums from all the threads.</span></span>  
  
 <span data-ttu-id="d9ec3-112">請注意，當 lambda 運算式主體包含單一運算式時，<xref:System.Func%602?displayProperty=nameWithType> 委派的傳回值即為運算式的值。</span><span class="sxs-lookup"><span data-stu-id="d9ec3-112">Note that when a lambda expression body consists of a single expression, the return value of the <xref:System.Func%602?displayProperty=nameWithType> delegate is the value of the expression.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d9ec3-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d9ec3-113">See also</span></span>

- <xref:System.Linq.ParallelEnumerable>
- [<span data-ttu-id="d9ec3-114">平行 LINQ (PLINQ)</span><span class="sxs-lookup"><span data-stu-id="d9ec3-114">Parallel LINQ (PLINQ)</span></span>](introduction-to-plinq.md)
