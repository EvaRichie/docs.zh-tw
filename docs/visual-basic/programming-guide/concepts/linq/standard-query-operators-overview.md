---
title: 標準查詢運算子概觀
ms.date: 07/20/2015
ms.assetid: 302bd39e-2ec1-495b-94bf-37d370d6f05f
ms.openlocfilehash: 7c229a576f6695282473352d6253d2c699c76604
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406777"
---
# <a name="standard-query-operators-overview-visual-basic"></a>標準查詢運算子概觀 (Visual Basic)

「標準查詢運算子」** 是形成 LINQ 模式的方法。 這些方法大多會在序列上運作，而序列是指其類型會實作 <xref:System.Collections.Generic.IEnumerable%601> 介面或 <xref:System.Linq.IQueryable%601> 介面的物件。 標準查詢運算子所提供的查詢功能包括篩選、投影、彙總、排序等等。

有兩組 LINQ 標準查詢運算子，一個運作於類型 <xref:System.Collections.Generic.IEnumerable%601> 的物件，另一個則運作於類型 <xref:System.Linq.IQueryable%601> 的物件。 構成每個集合的方法分別是 <xref:System.Linq.Enumerable> 和 <xref:System.Linq.Queryable> 類別的靜態成員。 它們定義為其所運作的類型的「擴充方法」**。 這表示可以使用靜態方法語法或執行個體方法語法來呼叫它們。

此外，數個標準查詢運算子方法也會根據 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Linq.IQueryable%601> 之類型以外的類型運作。 <xref:System.Linq.Enumerable> 類型定義同時在 <xref:System.Collections.IEnumerable> 類型的物件上運作的兩個這類方法。 <xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29> 和 <xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29> 這些方法可讓您查詢 LINQ 模式中的非參數化或非泛型集合。 他們會藉由建立物件的強型別集合來執行此動作。 <xref:System.Linq.Queryable> 類別定義在 <xref:System.Linq.Queryable> 類型的物件上運作的兩個類似方法 <xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29> 和 <xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29>。

根據傳回單一值還是一系列的值，標準查詢運算子的執行時機會不同。 這些傳回單一值的方法 (例如，<xref:System.Linq.Enumerable.Average%2A> 和 <xref:System.Linq.Enumerable.Sum%2A>) 就會立即執行。 傳回序列的方法會延後執行查詢，並傳回可列舉的物件。

如果是運作於記憶體內部集合的方法，即擴充 <xref:System.Collections.Generic.IEnumerable%601> 的方法，則傳回的可列舉物件會擷取已傳遞給方法的引數。 列舉該物件時，會採用查詢運算子的邏輯，並傳回查詢結果。

相反地，擴充 <xref:System.Linq.IQueryable%601> 的方法不會實作任何查詢行為，但會建置代表要執行查詢的運算式樹狀結構。 查詢處理是由來源 <xref:System.Linq.IQueryable%601> 物件所處理。

在一個查詢中，可以將查詢方法呼叫鏈結在一起，這樣會讓查詢變得更為複雜。

下列程式碼範例示範如何使用標準查詢運算子來取得序列的資訊。

```vb
Dim sentence = "the quick brown fox jumps over the lazy dog"
' Split the string into individual words to create a collection.
Dim words = sentence.Split(" "c)

Dim query = From word In words
            Group word.ToUpper() By word.Length Into gr = Group
            Order By Length _
            Select Length, GroupedWords = gr

Dim output As New System.Text.StringBuilder
For Each obj In query
    output.AppendLine(String.Format("Words of length {0}:", obj.Length))
    For Each word As String In obj.GroupedWords
        output.AppendLine(word)
    Next
Next

'Display the output
MsgBox(output.ToString())

' This code example produces the following output:
'
' Words of length 3:
' THE
' FOX
' THE
' DOG
' Words of length 4:
' OVER
' LAZY
' Words of length 5:
' QUICK
' BROWN
' JUMPS
```

## <a name="query-expression-syntax"></a>查詢運算式語法

某些更常用的標準查詢運算子具有專用 C# 和 Visual Basic 語言關鍵字語法，可將它們呼叫為「查詢運算式」** ** 的一部分。 如需具有專用關鍵字及其對應語法之標準查詢運算子的詳細資訊，請參閱[標準查詢運算子的查詢運算式語法（Visual Basic）](query-expression-syntax-for-standard-query-operators.md)。

## <a name="extending-the-standard-query-operators"></a>擴充標準查詢運算子

您可以建立適用於目標定義域或技術的定義域特定方法，來擴增一組標準查詢運算子。 您也可以將標準查詢運算子取代為提供額外服務的專屬實作，例如遠端評估、查詢轉譯和最佳化。 如需範例，請參閱 <xref:System.Linq.Enumerable.AsEnumerable%2A>。

## <a name="related-sections"></a>相關章節

下列連結會將您帶到根據功能而提供各種標準查詢運算子的其他資訊的主題。

- [排序資料](sorting-data.md)

- [設定作業（Visual Basic）](set-operations.md)

- [篩選資料（Visual Basic）](filtering-data.md)

- [數量詞作業（Visual Basic）](quantifier-operations.md)

- [投射作業（Visual Basic）](projection-operations.md)

- [分割資料（Visual Basic）](partitioning-data.md)

- [聯結作業（Visual Basic）](join-operations.md)

- [群組資料（Visual Basic）](grouping-data.md)

- [產生作業（Visual Basic）](generation-operations.md)

- [等號比較運算（Visual Basic）](equality-operations.md)

- [元素作業（Visual Basic）](element-operations.md)

- [轉換資料類型（Visual Basic）](converting-data-types.md)

- [串連作業（Visual Basic）](concatenation-operations.md)

- [匯總作業（Visual Basic）](aggregation-operations.md)

## <a name="see-also"></a>另請參閱

- <xref:System.Linq.Enumerable>
- <xref:System.Linq.Queryable>
- [LINQ 簡介 (Visual Basic)](introduction-to-linq.md)
- [標準查詢運算子的查詢運算式語法（Visual Basic）](query-expression-syntax-for-standard-query-operators.md)
- [依執行方式分類標準查詢運算子（Visual Basic）](classification-of-standard-query-operators-by-manner-of-execution.md)
- [擴充方法](../../language-features/procedures/extension-methods.md)
