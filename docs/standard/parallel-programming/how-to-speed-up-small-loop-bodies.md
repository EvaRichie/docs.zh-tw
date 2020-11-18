---
title: 作法：加速小型迴圈主體
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to speed up
ms.assetid: c7a66677-cb59-4cbf-969a-d2e8fc61a6ce
ms.openlocfilehash: 0e6e32386992a5dc4ac4556bc9d0489d0fd9d289
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826823"
---
# <a name="how-to-speed-up-small-loop-bodies"></a>作法：加速小型迴圈主體
當 <xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 迴圈有小型的主體時，其執行速度可能會比同等的循序迴圈更慢，例如 C# 中的 [for](../../csharp/language-reference/keywords/for.md) 迴圈和 Visual Basic 中的 [For](/previous-versions/visualstudio/visual-studio-2008/44kykk21(v=vs.90)) 迴圈。 效能較慢的起因是分割資料時相關的負擔，以及在每次迴圈反覆運算上叫用委派的成本。 為了解決這類情況，<xref:System.Collections.Concurrent.Partitioner> 類別提供 <xref:System.Collections.Concurrent.Partitioner.Create%2A?displayProperty=nameWithType> 方法，可讓您提供循序迴圈給委派主體，讓每個資料分割只叫用一次委派，而不會每個反覆項目叫用一次。 如需詳細資訊，請參閱 [PLINQ 和 TPL 的自訂 Partitioner](custom-partitioners-for-plinq-and-tpl.md)。  
  
## <a name="example"></a>範例  
 [!code-csharp[TPL_Partitioners#01](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioner01.cs#01)]
 [!code-vb[TPL_Partitioners#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_partitioners/vb/partitionercreate01.vb#01)]  
  
 在此範例中示範的方法適用於迴圈執行最少量工作的情況。 當工作變得更運算密集時，藉由使用 <xref:System.Threading.Tasks.Parallel.For%2A> 或 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 迴圈與預設 Partitioner，您可能會取得相同或更高的效能。  
  
## <a name="see-also"></a>請參閱

- [資料平行處理](data-parallelism-task-parallel-library.md)
- [PLINQ 和 TPL 的自訂 Partitioner](custom-partitioners-for-plinq-and-tpl.md)
- [迭代器 (C#)](../../csharp/programming-guide/concepts/iterators.md)
- [迭代器 (Visual Basic)](../../visual-basic/programming-guide/concepts/iterators.md)
- [PLINQ 和 TPL 中的 Lambda 運算式](lambda-expressions-in-plinq-and-tpl.md)
