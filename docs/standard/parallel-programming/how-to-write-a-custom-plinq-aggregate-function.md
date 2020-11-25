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
# <a name="how-to-write-a-custom-plinq-aggregate-function"></a>作法：撰寫自訂 PLINQ 彙總函式

此範例示範如何使用 <xref:System.Linq.ParallelEnumerable.Aggregate%2A> 方法，將自訂彙總函式套用至來源序列。  
  
> [!WARNING]
> 這個範例是為了示範用法，執行速度可能比不上對應的循序 LINQ to Objects 查詢。 如需加速的詳細資訊，請參閱[認識 PLINQ 中的加速](understanding-speedup-in-plinq.md)。  
  
## <a name="example"></a>範例  

 下列範例會計算整數序列的標準差。  
  
 [!code-csharp[PLINQ#31](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#31)]
 [!code-vb[PLINQ#31](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#31)]  
  
 此範例會使用 PLINQ 特有之 Aggregate 標準查詢運算子的多載。 這個多載會採用額外的 <xref:System.Func%603?displayProperty=nameWithType> 做為第三個輸入參數。 在執行彙總結果的最終計算之前，這個委派會合併所有執行緒的結果。 在此範例中，我們加入所有執行緒的加總。  
  
 請注意，當 lambda 運算式主體包含單一運算式時，<xref:System.Func%602?displayProperty=nameWithType> 委派的傳回值即為運算式的值。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Linq.ParallelEnumerable>
- [平行 LINQ (PLINQ)](introduction-to-plinq.md)
