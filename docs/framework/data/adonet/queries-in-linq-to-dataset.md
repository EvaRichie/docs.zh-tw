---
title: LINQ to DataSet 中的查詢
description: 瞭解如何在 LINQ to DataSet 中撰寫查詢，方法是取得資料來源、建立查詢，以及執行查詢。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c1a78fa8-9f0c-40bc-a372-5575a48708fe
ms.openlocfilehash: eee04959493914018904b61b0e5a289f172f2f18
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88063714"
---
# <a name="queries-in-linq-to-dataset"></a>LINQ to DataSet 中的查詢
查詢是指從資料來源中擷取資料的運算式。 查詢通常會以特定的查詢語言來表示，例如 SQL 用於關聯式資料庫，而 XQuery 用於 XML。 因此，開發人員必須針對他們所查詢的每種資料來源或資料格式，學習新的查詢語言。 Language-Integrated Query (LINQ) 提供了一種較簡單且一致的模型，可處理各種資料來源和格式的資料。 在 LINQ 查詢中，您一定會使用程式設計物件。  
  
 LINQ 查詢作業由三個動作構成：取得資料來源、建立查詢和執行查詢。  
  
 執行泛型介面的資料來源 <xref:System.Collections.Generic.IEnumerable%601> 可以透過 LINQ 查詢。 在上呼叫會傳回 <xref:System.Data.DataTableExtensions.AsEnumerable%2A> <xref:System.Data.DataTable> 物件，它會實 <xref:System.Collections.Generic.IEnumerable%601> 作為 LINQ to DataSet 查詢的資料來源。  
  
 在此查詢中，您可以精確地指定想要從資料來源中擷取的資訊。 此外，查詢也可以指定該項資訊傳回之前應該如何排序、分組和成形。 在 LINQ 中，查詢會儲存在變數內。 如果查詢設計成傳回值的序列 (Sequence)，查詢變數本身就必須是可列舉的型別。 這個查詢變數不會採取任何動作，也不會傳回任何資料。它只會儲存查詢資訊。 在您建立查詢之後，必須執行該查詢以便擷取任何資料。  
  
 在傳回值序列的查詢中，查詢變數本身絕不會保存查詢結果，只會儲存查詢命令而已。 查詢的執行會延後，直到在 `foreach` 或 `For Each` 迴圈 (Loop) 中反覆查看查詢變數為止。 這稱為「*延後執行*」;也就是說，查詢執行會在查詢經過一段時間之後發生。 這表示，您可以依照想要的頻率來執行查詢。 例如，當您擁有一個正由其他應用程式更新的資料庫時，這就很有用。 您可以在應用程式中建立擷取最新資訊的查詢，然後重複執行此查詢，以便每次都傳回更新的資訊。  
  
 相較於傳回值序列的延後查詢，傳回單一子句值的查詢會立即執行。 單一子句查詢的某些範例包括 <xref:System.Linq.Enumerable.Count%2A>、<xref:System.Linq.Enumerable.Max%2A>、<xref:System.Linq.Enumerable.Average%2A> 和 <xref:System.Linq.Enumerable.First%2A>。 這些查詢會立即執行，因為系統需要查詢結果來計算單一子句結果。 例如，若要尋找查詢結果的平均值，您必須執行查詢，如此平均函式才有輸入資料可處理。 此外，您也可以針對查詢使用 <xref:System.Linq.Enumerable.ToList%2A> 或 <xref:System.Linq.Enumerable.ToArray%2A> 方法，強制立即執行不會產生單一子句值的查詢。 當您想要快取查詢的結果時，這些強制立即執行的技巧就很有用。
  
## <a name="queries"></a>查詢  
 LINQ to DataSet 查詢可以用兩種不同的語法來撰寫：查詢運算式語法和以方法為基礎的查詢語法。  
  
### <a name="query-expression-syntax"></a>查詢運算式語法  
 查詢運算式是宣告式查詢語法。 這種語法可讓開發人員使用類似 SQL 的格式，在 C# 或 Visual Basic 中撰寫查詢。 透過使用查詢運算式語法，您就可以利用最少的程式碼，針對資料來源執行同樣複雜的篩選、排序和分組作業。 如需詳細資訊，請參閱[LINQ 查詢運算式](../../../csharp/linq/index.md#query-expression-overview)和[基本查詢作業 (Visual Basic) ](../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md)。
  
 .NET Framework common language runtime (CLR) 無法讀取查詢運算式語法本身。 因此，在編譯期間，查詢運算式會轉譯為 CLR 可以了解的項目：即方法呼叫。 這些方法稱為*標準查詢運算子*。 身為開發人員，您可以選擇使用方法語法來直接呼叫它們，而非使用查詢語法。 如需詳細資訊，請參閱 [LINQ 中的查詢語法及方法語法](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md)。 如需標準查詢運算子的詳細資訊，請參閱[標準查詢運算子總覽](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
 下列範例會使用 <xref:System.Linq.Enumerable.Select%2A> 來傳回 `Product` 資料表中的所有資料列，並顯示產品名稱。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectSimple1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectsimple1)]
 [!code-vb[DP LINQ to DataSet Examples#SelectSimple1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectsimple1)]  
  
### <a name="method-based-query-syntax"></a>以方法為基礎的查詢語法  
 制訂 LINQ to DataSet 查詢的另一種方式是使用以方法為基礎的查詢。 以方法為基礎的查詢語法是對 LINQ 運算子方法之直接方法呼叫的序列，並傳遞 Lambda 運算式當做參數。 如需詳細資訊，請參閱[Lambda 運算式](../../../csharp/language-reference/operators/lambda-expressions.md)。  
  
 這則範例會使用 <xref:System.Linq.Enumerable.Select%2A> 來傳回 `Product` 資料表中的所有資料列，並顯示產品名稱。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectAnonymousTypes_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectanonymoustypes_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SelectAnonymousTypes_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectanonymoustypes_mq)]  
  
## <a name="composing-queries"></a>撰寫查詢  
 如本主題先前所述，當查詢設計為傳回值的序列時，查詢變數本身只會儲存查詢命令。 如果查詢沒有包含將導致立即執行的方法，查詢的實際執行將延後，直到您在 `foreach` 或 `For Each` 迴圈中反覆查看查詢變數為止。 延後執行可結合多個查詢或擴充單一查詢。 擴充單一查詢時，它會修改成包含新的作業，而且最終的執行將反映這些變更。 在下列範例中，第一個查詢會傳回所有產品。 第二個查詢會使用 `Where` 來擴充第一個查詢，以便傳回大小為 "L" 的所有產品：  
  
 [!code-csharp[DP LINQ to DataSet Examples#Composing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#composing)]
 [!code-vb[DP LINQ to DataSet Examples#Composing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#composing)]  
  
 執行查詢之後，就無法再撰寫任何查詢，而且所有後續的查詢都將使用記憶體中的 LINQ 運算子。 當您逐一查看或語句中的查詢變數 `foreach` `For Each` ，或是呼叫導致立即執行的其中一個 LINQ 轉換運算子時，就會執行查詢。 這些運算子包括：<xref:System.Linq.Enumerable.ToList%2A>、<xref:System.Linq.Enumerable.ToArray%2A>、<xref:System.Linq.Enumerable.ToLookup%2A> 和 <xref:System.Linq.Enumerable.ToDictionary%2A>。  
  
 在下列範例中，第一個查詢會傳回所有產品，並依照標價排序。 <xref:System.Linq.Enumerable.ToArray%2A> 方法是用來強制立即執行查詢：  
  
 [!code-csharp[DP LINQ to DataSet Examples#ToArray2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#toarray2)]
 [!code-vb[DP LINQ to DataSet Examples#ToArray2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#toarray2)]  
  
## <a name="see-also"></a>另請參閱

- [程式設計指南](programming-guide-linq-to-dataset.md)
- [查詢 DataSet](querying-datasets-linq-to-dataset.md)
- [開始使用 C# 中的 LINQ](../../../csharp/programming-guide/concepts/linq/index.md)
- [使用 Visual Basic 撰寫 LINQ 入門](../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
