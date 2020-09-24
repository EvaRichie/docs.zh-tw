---
title: 已編譯查詢 (LINQ to Entities)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8025ba1d-29c7-4407-841b-d5a3bed40b7a
ms.openlocfilehash: b8bed63cda505ad8c26c9c69d880a077053b8d2e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153049"
---
# <a name="compiled-queries--linq-to-entities"></a>編譯的查詢 (LINQ to Entities) 

當您的應用程式執行了 Entity Framework 中結構類似的查詢多次時，您可經常增加效能，其方式是編譯查詢一次，然後使用不同的參數執行查詢多次。 例如，應用程式可能必須擷取特定城市中的所有客戶；此城市是使用者在執行階段於表單中所指定。 LINQ to Entities 支援針對這個用途所編譯的查詢。  
  
 從 .NET Framework 4.5 開始，會自動快取 LINQ 查詢。 不過，之後執行時您仍可以使用已編譯的 LINQ 查詢減少這種成本，且已編譯查詢可能比自動快取的 LINQ 查詢更有效率。 `Enumerable.Contains`不會自動快取將運算子套用至記憶體中集合的 LINQ to Entities 查詢。 此外，也不允許在編譯的 LINQ 查詢中，將記憶體中的集合參數化。  
  
 <xref:System.Data.Objects.CompiledQuery> 類別提供查詢的編譯和快取以供重複使用。 就概念而言，這個類別包含數個多載之 <xref:System.Data.Objects.CompiledQuery> 的 `Compile` 方法。 呼叫 `Compile` 方法可建立新委派來代表已編譯的查詢。 `Compile` 所提供的 <xref:System.Data.Objects.ObjectContext> 方法和參數值會傳回一個產生某個結果 (例如 <xref:System.Linq.IQueryable%601> 執行個體) 的委派。 此查詢只會在第一次執行期間編譯一次。 不過，您之後無法變更在編譯階段中，針對查詢所設定的合併選項。 一旦編譯查詢之後，您就只能提供基本類型的參數，但您無法取代會變更產生之 SQL 的查詢部分。 如需詳細資訊，請參閱 [EF Merge 選項和編譯的查詢](/archive/blogs/dsimmons/ef-merge-options-and-compiled-queries)。
  
 的方法所編譯的 LINQ to Entities 查詢運算式 <xref:System.Data.Objects.CompiledQuery> `Compile` 是由其中一個泛型 `Func` 委派（例如）表示 <xref:System.Func%605> 。 查詢運算式最多只能封裝一個 `ObjectContext` 參數、一個傳回參數和十六個查詢參數。 如果需要使用十六個以上的查詢參數，您可以建立其屬性代表查詢參數的結構。 然後，當您設定這些參數之後，就可以將此結構的屬性用於查詢運算式中。  
  
## <a name="example-1"></a>範例 1  

 下列範例會先編譯然後再叫用接受 <xref:System.Decimal> 輸入參數的查詢，並且傳回訂單序列，其中的總到期金額大於或等於 $200.00：  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query 2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery2)]
 [!code-vb[DP L2E Conceptual Examples - compiled query2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery2)]  
  
## <a name="example-2"></a>範例 2  

 下列範例會先編譯再叫用傳回 <xref:System.Data.Objects.ObjectQuery%601> 執行個體的查詢：  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query1_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery1_mq)]
 [!code-vb[DP L2E Conceptual Examples - compiled query1_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery1_mq)]  
  
## <a name="example-3"></a>範例 3  

 下列範例會先編譯再叫用一個查詢，此查詢會以 <xref:System.Decimal> 值形式傳回產品標價的平均值。  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery3_mq)]
 [!code-vb[DP L2E Conceptual Examples - compiled query3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery3_mq)]  
  
## <a name="example-4"></a>範例 4  

 下列範例會先編譯然後再叫用接受輸入參數的查詢，然後傳回 <xref:System.String> `Contact` 其電子郵件地址開頭為指定字串的：  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query4_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery4_mq)]
 [!code-vb[DP L2E Conceptual Examples - compiled query4_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery4_mq)]  
  
## <a name="example-5"></a>範例 5  

 下列範例會先編譯然後再叫用接受 <xref:System.DateTime> 和 <xref:System.Decimal> 輸入參數的查詢，並且傳回訂單序列，其中的訂單日期晚於 2003 年 3 月 8 日，總應付金額則少於 $300.00：  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery5)]
 [!code-vb[DP L2E Conceptual Examples - compiled query5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery5)]  
  
## <a name="example-6"></a>範例 6  

 下列範例會先編譯然後再叫用接受 <xref:System.DateTime> 輸入參數的查詢，並且傳回訂單序列，其中的訂單日期晚於 2004 年 3 月 8 日。 此查詢會傳回匿名型別序列形式的訂單資訊。 匿名型別是由編譯器所推斷，所以您無法在 <xref:System.Data.Objects.CompiledQuery> 的 `Compile` 方法中指定型別參數，而且此型別會在查詢本身定義。  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery6)]
 [!code-vb[DP L2E Conceptual Examples - compiled query6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery6)]  
  
## <a name="example-7"></a>範例 7  

 下列範例會先編譯然後再叫用接受使用者定義結構輸入參數的查詢，並且傳回訂單序列。 此結構會定義開始日期、結束日期和應付總額查詢參數，而且此查詢會傳回在 2003 年 3 月 3 日與 3 月 8 日之間出貨而且應付總額超過 $700.00 的訂單。  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery7)]
 [!code-vb[DP L2E Conceptual Examples - compiled query7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery7)]  
  
 定義查詢參數的結構：  
  
 [!code-csharp[DP L2E Conceptual Examples - MyParamsStruct](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#myparamsstruct)]
 [!code-vb[DP L2E Conceptual Examples - MyParamsStruct](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#myparamsstruct)]  
  
## <a name="see-also"></a>另請參閱

- [ADO.NET Entity Framework](../index.md)
- [LINQ to Entities](linq-to-entities.md)
- [EF 合併選項和編譯的查詢](/archive/blogs/dsimmons/ef-merge-options-and-compiled-queries)
