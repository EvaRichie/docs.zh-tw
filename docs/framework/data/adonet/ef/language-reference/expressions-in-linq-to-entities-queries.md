---
title: LINQ to Entities 查詢中的運算式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d70b502f-6a15-4120-b4fe-500b173ad9cc
ms.openlocfilehash: f65759d37661271588d56965eadcccbe997623f4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91166647"
---
# <a name="expressions-in-linq-to-entities-queries"></a>LINQ to Entities 查詢中的運算式

運算式是可以評估為單一值、物件、方法或命名空間的程式碼片段。 運算式可以包含常值、方法呼叫、運算子及其運算元，或是簡單名稱。 簡單名稱可以是變數、型別成員、方法參數、命名空間或型別的名稱。 運算式可以使用運算子 (後者又可能使用其他運算式當做參數) 或方法呼叫 (它的參數又可能是其他方法呼叫)。 因此，運算式可以很簡單，也可以非常複雜。  
  
 在 LINQ to Entities 查詢中，運算式可以包含命名空間中的類型所允許的任何功能 <xref:System.Linq.Expressions> ，包括 lambda 運算式。 可以在 LINQ to Entities 查詢中使用的運算式是運算式的超集合，可用來查詢 Entity Framework。針對 Entity Framework 查詢的運算式僅限於 `ObjectQuery<T>` 和基礎資料來源所支援的作業。  
  
 在以下範例中，`Where` 子句中的比較就是個運算式：  
  
 [!code-csharp[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#whereexpression)]
 [!code-vb[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#whereexpression)]  
  
> [!NOTE]
> 特定語言結構（例如 c # `unchecked` ）在 LINQ to Entities 中沒有任何意義。  
  
## <a name="in-this-section"></a>本節內容  

 [常數運算式](constant-expressions.md)  
  
 [比較運算式](comparison-expressions.md)  
  
 [Null 比較](null-comparisons.md)  
  
 [初始化運算式](initialization-expressions.md)  
  
 [關聯性、導覽屬性和外鍵](/ef/ef6/fundamentals/relationships)  
  
## <a name="see-also"></a>另請參閱

- [ADO.NET Entity Framework](../index.md)
