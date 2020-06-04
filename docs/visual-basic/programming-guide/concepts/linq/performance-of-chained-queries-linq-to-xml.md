---
title: 已鏈結查詢的效能 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 589f2adc-69f9-404d-b9d6-4c28dabea7f7
ms.openlocfilehash: 6b87f2744f663ebd45dceb036dcaac71b80765fc
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396385"
---
# <a name="performance-of-chained-queries-linq-to-xml-visual-basic"></a>連鎖查詢的效能（LINQ to XML）（Visual Basic）

LINQ (和 LINQ to XML) 其中一個最重要的優點在於，鏈結查詢的執行效能就如同單一較大且更複雜的查詢。

鏈結查詢是指使用其他查詢當做其來源的查詢。 例如，在下列簡單程式碼中，`query2` 具有 `query1` 當做其來源：

```vb
Dim root As New XElement("Root", New XElement("Child", 1), New XElement("Child", 2), New XElement("Child", 3), New XElement("Child", 4))

Dim query1 = From x In root.Elements("Child") Where CInt(x) >= 3x

Dim query2 = From e In query1 Where CInt(e) Mod 2 = 0e

For Each i As var In query2
    Console.WriteLine("{0}", CInt(i))
Next
```

這個範例會產生下列輸出：

```console
4
```

這個鏈結查詢會與逐一查看連結串列 (Linked List) 提供相同的效能設定檔。

- <xref:System.Xml.Linq.XContainer.Elements%2A> 軸基本上與逐一查看連結串列具有相同的效能。 <xref:System.Xml.Linq.XContainer.Elements%2A> 會實作成延後執行的 Iterator。 這表示，除了逐一查看連結串列以外，它會執行一些工作，例如配置 Iterator 物件和追蹤執行狀態。 這項工作可分成兩個分類：在設定 Iterator 時完成的工作，以及在每次反覆運算期間完成的工作。 設定工作是小型且固定的工作量，而在每次反覆運算期間完成的工作則與來源集合中的項目數成正比。

- 在 `query1` 中，`Where` 子句會讓查詢呼叫 <xref:System.Linq.Enumerable.Where%2A> 方法。 這個方法也會實作成 Iterator。 設定工作包含具現化將參考 Lambda 運算式的委派 (Delegate)，以及進行 Iterator 的一般設定。 進行每次反覆運算時，系統會呼叫此委派來執行述詞 (Predicate)。 設定工作以及在每次反覆運算期間完成的工作與逐一查看軸時完成的工作很相似。

- 在 `query1` 中，select 子句會讓查詢呼叫 <xref:System.Linq.Enumerable.Select%2A> 方法。 這個方法與 <xref:System.Linq.Enumerable.Where%2A> 方法具有相同的效能設定檔。

- 在 `query2` 中，`Where` 子句和 `Select` 子句都具有相同的效能設定檔，如同 `query1`。

 因此，逐一查看 `query2` 的作業會直接與第一個查詢之來源中的項目數成正比 (亦即，線性時間)。

## <a name="see-also"></a>另請參閱

- [效能（LINQ to XML）（Visual Basic）](performance-linq-to-xml.md)
