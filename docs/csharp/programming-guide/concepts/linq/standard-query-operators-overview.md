---
title: 標準查詢運算子概觀 (C#)
description: 'LINQ 標準查詢運算子提供查詢功能，包括 c # 中的篩選、投射、匯總和排序。'
ms.date: 07/20/2015
ms.assetid: 812fa119-5f65-4139-b4fa-55dccd8dc3ac
ms.openlocfilehash: 8a399f52881e10f8d94263843b5992101f96a5ea
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302317"
---
# <a name="standard-query-operators-overview-c"></a>標準查詢運算子概觀 (C#)
「標準查詢運算子」** 是形成 LINQ 模式的方法。 這些方法大多會在序列上運作，而序列是指其類型會實作 <xref:System.Collections.Generic.IEnumerable%601> 介面或 <xref:System.Linq.IQueryable%601> 介面的物件。 標準查詢運算子所提供的查詢功能包括篩選、投影、彙總、排序等等。  
  
 有兩組 LINQ 標準查詢運算子：一個是在類型的物件上運作，另一個則是在 <xref:System.Collections.Generic.IEnumerable%601> 類型的物件上運作 <xref:System.Linq.IQueryable%601> 。 構成每個集合的方法分別是 <xref:System.Linq.Enumerable> 和 <xref:System.Linq.Queryable> 類別的靜態成員。 它們定義為其所運作的類型的「擴充方法」**。 您可以使用靜態方法語法或實例方法語法來呼叫擴充方法。  
  
 此外，數個標準查詢運算子方法也會根據 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Linq.IQueryable%601> 之類型以外的類型運作。 <xref:System.Linq.Enumerable> 類型定義同時在 <xref:System.Collections.IEnumerable> 類型的物件上運作的兩個這類方法。 <xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29> 和 <xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29> 這些方法可讓您查詢 LINQ 模式中的非參數化或非泛型集合。 他們會藉由建立物件的強型別集合來執行此動作。 <xref:System.Linq.Queryable> 類別定義在 <xref:System.Linq.Queryable> 類型的物件上運作的兩個類似方法 <xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29> 和 <xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29>。  
  
 根據傳回單一值還是一系列的值，標準查詢運算子的執行時機會不同。 這些傳回單一值的方法 (例如，<xref:System.Linq.Enumerable.Average%2A> 和 <xref:System.Linq.Enumerable.Sum%2A>) 就會立即執行。 傳回序列的方法會延後執行查詢，並傳回可列舉的物件。  
  
 對於在記憶體內部集合上運作的方法（也就是擴充的方法）， <xref:System.Collections.Generic.IEnumerable%601> 傳回的可列舉物件會捕捉傳遞至方法的引數。 列舉該物件時，會採用查詢運算子的邏輯，並傳回查詢結果。  
  
 相反地，擴充的方法 <xref:System.Linq.IQueryable%601> 不會執行任何查詢行為。 它們會建立代表要執行之查詢的運算式樹狀架構。 查詢處理是由來源 <xref:System.Linq.IQueryable%601> 物件所處理。  
  
 在一個查詢中，可以將查詢方法呼叫鏈結在一起，這樣會讓查詢變得更為複雜。  
  
 下列程式碼範例示範如何使用標準查詢運算子來取得序列的資訊。  
  
```csharp  
string sentence = "the quick brown fox jumps over the lazy dog";  
// Split the string into individual words to create a collection.  
string[] words = sentence.Split(' ');  
  
// Using query expression syntax.  
var query = from word in words  
            group word.ToUpper() by word.Length into gr  
            orderby gr.Key  
            select new { Length = gr.Key, Words = gr };  
  
// Using method-based query syntax.  
var query2 = words.  
    GroupBy(w => w.Length, w => w.ToUpper()).  
    Select(g => new { Length = g.Key, Words = g }).  
    OrderBy(o => o.Length);  
  
foreach (var obj in query)  
{  
    Console.WriteLine("Words of length {0}:", obj.Length);  
    foreach (string word in obj.Words)  
        Console.WriteLine(word);  
}  
  
// This code example produces the following output:  
//  
// Words of length 3:  
// THE  
// FOX  
// THE  
// DOG  
// Words of length 4:  
// OVER  
// LAZY  
// Words of length 5:  
// QUICK  
// BROWN  
// JUMPS
```  
  
## <a name="query-expression-syntax"></a>查詢運算式語法  
 某些更常用的標準查詢運算子具有專用 C# 和 Visual Basic 語言關鍵字語法，可將它們呼叫為「查詢運算式」** ** 的一部分。 如需具有專用關鍵字和其對應語法之標準查詢運算子的詳細資訊，請參閱[標準查詢運算子的查詢運算式語法 (C#)](./query-expression-syntax-for-standard-query-operators.md)。  
  
## <a name="extending-the-standard-query-operators"></a>擴充標準查詢運算子  
 您可以建立適用於目標定義域或技術的定義域特定方法，來擴增一組標準查詢運算子。 您也可以將標準查詢運算子取代為提供額外服務的專屬實作，例如遠端評估、查詢轉譯和最佳化。 如需範例，請參閱 <xref:System.Linq.Enumerable.AsEnumerable%2A>。  
  
## <a name="related-sections"></a>相關章節  
 下列連結會帶您前往可根據功能提供各種標準查詢運算子之其他相關資訊的文章。  
  
 [排序資料 (C#)](./sorting-data.md)  
  
 [設定作業 (C#)](./set-operations.md)  
  
 [篩選資料 (C#)](./filtering-data.md)  
  
 [數量詞作業 (C#)](./quantifier-operations.md)  
  
 [投射作業 (C#)](./projection-operations.md)  
  
 [分割資料 (C#)](./partitioning-data.md)  
  
 [聯結作業 (C#)](./join-operations.md)  
  
 [分組資料 (C#)](./grouping-data.md)  
  
 [產生作業 (C#)](./generation-operations.md)  
  
 [相等比較作業 (C#)](./equality-operations.md)  
  
 [項目作業 (C#)](./element-operations.md)  
  
 [轉換資料類型 (C#)](./converting-data-types.md)  
  
 [串連作業 (C#)](./concatenation-operations.md)  
  
 [彙總作業 (C#)](./aggregation-operations.md)  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Linq.Enumerable>
- <xref:System.Linq.Queryable>
- [LINQ 查詢簡介 (C#)](./introduction-to-linq-queries.md)
- [標準查詢運算子的查詢運算式語法 (C#)](./query-expression-syntax-for-standard-query-operators.md)
- [依據執行方式將標準查詢運算子分類 (C#)](./classification-of-standard-query-operators-by-manner-of-execution.md)
- [擴充方法](../../classes-and-structs/extension-methods.md)
