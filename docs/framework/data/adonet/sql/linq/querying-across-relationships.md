---
title: 跨關聯性查詢
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 297878d0-685b-4c01-b2e0-9d731b7322bc
ms.openlocfilehash: 24ab13a1d67eac39c7b3d7be8cb1c16ec7265d5e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91184874"
---
# <a name="querying-across-relationships"></a>跨關聯性查詢

對類別定義中其他物件或其他物件集合的參考，會直接對應到資料庫中的外部索引鍵關聯性。 您可以在使用點標記法進行查詢時使用這些關聯性，進而存取關聯性屬性以及從某個物件巡覽到另一個物件。 這些存取作業會轉譯成對等 SQL 中更複雜的聯結或相關聯的子查詢 (Subquery)。  
  
 例如，下列查詢會從訂單巡覽至客戶，而將查詢結果限制在位於倫敦 (London) 之客戶的訂單。  
  
 [!code-csharp[DLinqQueryConcepts#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#3)]
 [!code-vb[DLinqQueryConcepts#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#3)]  
  
 如果關聯性屬性不存在，您就必須以 *手動方式將*它們撰寫為聯結，就像在 SQL 查詢中所做的一樣，如下列程式碼所示：  
  
 [!code-csharp[DLinqQueryConcepts#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#4)]
 [!code-vb[DLinqQueryConcepts#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#4)]  
  
 您可以使用 [ *關聯* 性] 屬性來定義此特定關聯性一次。 然後，您就可以使用更為方便的點語法。 但是關聯性屬性的存在更加重要，因為網域指定的物件模型 (Object Model) 通常會定義為階層架構或圖形。 您進行程式設計的物件會具有對其他物件的參考。 物件對物件的關聯性會對應到資料庫中的外部索引鍵樣式關聯性，只是純屬巧合。 屬性存取則提供了撰寫聯結的簡便方法。  
  
 關於這點，相較於成為查詢本身的一部分，關聯性屬性對於查詢的結果而言更加重要。 在查詢已擷取特定客戶的相關資料後，類別定義會表示客戶具有訂單。 換句話說，您會預期特定客戶的 `Orders` 屬性成為已填入 (Populate) 該客戶所有訂單的集合。 事實上，這就是您透過這種方式定義類別而宣告的合約。 即使查詢並未要求訂單，您仍預期會在此看見訂單。 您期望物件模型能維持某種假象，那就是資料庫的記憶體中擴充具有立即可用的相關物件。  
  
 您目前具有關聯性，因此可藉由參考類別中定義的關聯性屬性，進而撰寫查詢。 這些關聯性參考會對應至資料庫中的外部索引鍵關聯性。 使用這些關聯性的作業會轉譯成對等 SQL 中更複雜的聯結。 只要您已定義關聯性 (使用 <xref:System.Data.Linq.Mapping.AssociationAttribute> 屬性 (Attribute))，就不必在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中編寫明確聯結。  
  
 為了協助維持這種假像，會 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 執行一個稱為 *延後載入*的技巧。 如需詳細資訊，請參閱 [延後和立即載入](deferred-versus-immediate-loading.md)。  
  
 請考慮使用下列 SQL 查詢來投影成對清單 `CustomerID` - `OrderID` ：  
  
```sql
SELECT t0.CustomerID, t1.OrderID  
FROM   Customers AS t0 INNER JOIN  
          Orders AS t1 ON t0.CustomerID = t1.CustomerID  
WHERE  (t0.City = @p0)  
```  
  
 若要使用 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 取得相同的結果，您可使用已存在於 `Orders` 類別中的 `Customer` 屬性參考。 `Orders`參考提供執行查詢並投射配對的必要資訊 `CustomerID` - `OrderID` ，如下列程式碼所示：  
  
 [!code-csharp[DLinqQueryConcepts#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#5)]
 [!code-vb[DLinqQueryConcepts#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#5)]  
  
 您也可以進行反轉。 也就是說，您可以查詢 `Orders`，並使用其 `Customer` 關聯性參考來存取關聯之 `Customer` 物件的相關資訊。 下列程式碼會投射與之前相同的 `CustomerID` - `OrderID` 配對，但這次是透過查詢 `Orders` 而非 `Customers` 。  
  
 [!code-csharp[DLinqQueryConcepts#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#6)]
 [!code-vb[DLinqQueryConcepts#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#6)]  
  
## <a name="see-also"></a>另請參閱

- [查詢概念](query-concepts.md)
