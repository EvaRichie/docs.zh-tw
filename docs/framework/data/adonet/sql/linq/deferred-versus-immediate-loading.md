---
title: 延後和立即載入的比較
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1d7247f-a3b7-460b-b342-5c1a2365aa1a
ms.openlocfilehash: 4e2cb7c90eb703985cbb1b8673522a9e253564d0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164294"
---
# <a name="deferred-versus-immediate-loading"></a>延後和立即載入的比較

當您查詢物件時，實際上只擷取了所要求的物件。 *相關*物件不會同時自動提取。  (需詳細資訊，請參閱 [跨關聯性查詢](querying-across-relationships.md)。 ) 您無法看到尚未載入相關物件的事實，因為嘗試存取它們會產生可抓取這些物件的要求。  
  
 例如，您可能想要查詢一組特定的訂單，然後只偶爾將電子郵件通知傳送給特定客戶。 因此並不需要一開始就擷取每筆訂單的所有客戶資料。 您可以使用延後載入，將確切資訊的擷取延後至絕對需要的時候才進行擷取。 請考慮下列範例：  
  
 [!code-csharp[DLinqQueryConcepts#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#1)]
 [!code-vb[DLinqQueryConcepts#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#1)]  
  
 反之亦然。 您的應用程式可能需要同時檢視客戶和訂單資料。 您知道您需要這兩組資料， 另外，一旦您取得結果，應用程式就需要每位客戶的訂單資訊。 但您不想要針對每位客戶的訂單分別送出個別查詢， 您實際想做的是在擷取客戶資料時一起擷取訂單資料。  
  
 [!code-csharp[DLinqQueryConcepts#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#2)]
 [!code-vb[DLinqQueryConcepts#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#2)]  
  
 您也可以建立叉積查詢，並將資料的所有相對位元都擷取為一個大型投影 (Projection)，以利用查詢來聯結 (Join) 客戶和訂單。 但這些結果不是實體 (Entity)   (需詳細資訊，請參閱 [LINQ to SQL 物件模型](the-linq-to-sql-object-model.md)) 。 實體是具有識別 (Identity) 而且可以修改的物件，而上述結果卻是無法變更和持續 (Persist) 的投影。 更糟的是，因為每位客戶會以簡維聯結輸出重複每筆訂單，所以您會擷取到許多多餘的資料。  
  
 您實際需要的是一種可以同時擷取一組相關物件的方式。 而這組物件是圖形的明確部分，因此您擷取到的資料就會是您所需要的資料。 基於這個目的， [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供 <xref:System.Data.Linq.DataLoadOptions> 立即載入物件模型的區域。 方法如下：  
  
- <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> 方法，可以立即載入與主要目標相關的資料。  
  
- <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> 方法，可以篩選針對特定關聯性 (Relationship) 所擷取的物件。  
  
## <a name="see-also"></a>另請參閱

- [查詢概念](query-concepts.md)
