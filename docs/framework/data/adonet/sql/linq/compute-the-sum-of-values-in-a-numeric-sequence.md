---
title: 如何：計算數值序列中各值的總和
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 24e335b0-984e-4825-8721-0a91b533b7c3
ms.openlocfilehash: 3d160e2cce5f3e0a7eea305657260b6fa4ded7fe
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164437"
---
# <a name="compute-the-sum-of-values-in-a-numeric-sequence"></a>如何：計算數值序列中各值的總和

使用 <xref:System.Linq.Enumerable.Sum%2A> 運算子，可以計算序列中的數值總和。  
  
 請注意，`Sum` 中的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 運算子有下列特性：  
  
- 標準查詢運算子的彙總 (Aggregate) 運算子 `Sum` 會將空序列或只包含 null 的序列評估為零。 在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中，SQL 的語意 (Semantics) 則不變。 因此，`Sum` 會將空序列或只包含 null 的序列評估為 null，而不是零。  
  
- SQL 對中繼結果的限制會套用至 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中的彙總。 32位整數數量的總和不是使用64位結果來計算，而且可能會發生溢位 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] `Sum` 。 即使標準查詢運算子的實作未使對應的記憶體中序列發生溢位，這個可能性還是存在。  
  
## <a name="example"></a>範例  

 下列範例會找出 `Order` 資料表中所有訂單的總運費。  
  
 如果您對 Northwind 範例資料庫執行這個查詢，則輸出為：`64942.6900`。  
  
 [!code-csharp[DLinqQueryExamples#12](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#12)]
 [!code-vb[DLinqQueryExamples#12](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#12)]  
  
## <a name="example"></a>範例  

 下列範例會找出所有產品的訂購單位總數。  
  
 如果您對 Northwind 範例資料庫執行這個查詢，則輸出為：`780`。  
  
 請注意，因為 `short` 沒有適用於 short 型別的多載，所以必須轉換 (Cast) `UnitsOnOrder` 型別 (例如，`Sum`)。  
  
 [!code-csharp[DLinqQueryExamples#13](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#13)]
 [!code-vb[DLinqQueryExamples#13](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#13)]  
  
## <a name="see-also"></a>另請參閱

- [彙總查詢](aggregate-queries.md)
- [下載範例資料庫](downloading-sample-databases.md)
