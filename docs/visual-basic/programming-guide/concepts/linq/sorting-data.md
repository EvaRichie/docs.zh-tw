---
title: 排序資料
ms.date: 07/20/2015
ms.assetid: 6f81065c-0c89-4bf3-a6d8-442273f8810e
ms.openlocfilehash: a5ccff745995ed7f41731cf98fb7c49d3247d994
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406790"
---
# <a name="sorting-data-visual-basic"></a>排序資料（Visual Basic）

排序作業會根據一個或多個屬性來排序序列的項目。 第一個排序準則會執行元素的主要排序； 您可以藉由指定第二個排序準則來排序每一個主要排序群組內的元素。

下圖顯示對一系列字元執行字母順序排序作業的結果。

![顯示依字母順序排序作業的圖形。](./media/sorting-data/alphabetical-sort-operation.png)

下節列出可排序資料的標準查詢運算子方法。

## <a name="methods"></a>方法

|方法名稱|Description|Visual Basic 查詢運算式語法|相關資訊|
|-----------------|-----------------|------------------------------------------|----------------------|
|OrderBy|依遞增順序排序值。|`Order By`|<xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OrderBy%2A?displayProperty=nameWithType>|
|OrderByDescending|依遞減順序排序值。|`Order By … Descending`|<xref:System.Linq.Enumerable.OrderByDescending%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OrderByDescending%2A?displayProperty=nameWithType>|
|ThenBy|依遞增順序執行次要排序。|`Order By …, …`|<xref:System.Linq.Enumerable.ThenBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ThenBy%2A?displayProperty=nameWithType>|
|ThenByDescending|依遞減順序執行次要排序。|`Order By …, … Descending`|<xref:System.Linq.Enumerable.ThenByDescending%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ThenByDescending%2A?displayProperty=nameWithType>|
|Reverse|反轉集合中項目的順序。|不適用。|<xref:System.Linq.Enumerable.Reverse%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Reverse%2A?displayProperty=nameWithType>|

## <a name="query-expression-syntax-examples"></a>查詢運算式語法範例

### <a name="primary-sort-examples"></a>主要排序範例

#### <a name="primary-ascending-sort"></a>主要遞增排序

下列範例示範如何在 LINQ 查詢中使用 `Order By` 子句，依字串長度以遞增順序來排序陣列中的字串。

```vb
Dim words = {"the", "quick", "brown", "fox", "jumps"}

Dim sortQuery = From word In words
                Order By word.Length
                Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In sortQuery
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' the
' fox
' quick
' brown
' jumps
```

#### <a name="primary-descending-sort"></a>主要遞減排序

下一個範例示範如何在 LINQ 查詢中使用 `Order By Descending` 子句，依其第一個字母以遞減順序來排序字串。

```vb
Dim words = {"the", "quick", "brown", "fox", "jumps"}

Dim sortQuery = From word In words
                Order By word.Substring(0, 1) Descending
                Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In sortQuery
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' the
' quick
' jumps
' fox
' brown
```

### <a name="secondary-sort-examples"></a>次要排序範例

#### <a name="secondary-ascending-sort"></a>次要遞增排序

下列範例示範如何在 LINQ 查詢中使用 `Order By` 子句，對陣列中的字串執行主要和次要排序。 字串主要是依長度進行排序，其次依字串的第一個字母進行排序，而兩者都是遞增排序。

```vb
Dim words = {"the", "quick", "brown", "fox", "jumps"}

Dim sortQuery = From word In words
                Order By word.Length, word.Substring(0, 1)
                Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In sortQuery
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' fox
' the
' brown
' jumps
' quick
```

#### <a name="secondary-descending-sort"></a>次要遞減排序

下一個範例示範如何在 LINQ 查詢中使用 `Order By Descending` 子句，執行依遞增順序的主要排序以及依遞減順序的次要排序。 字串主要是依長度進行排序，其次依字串的第一個字母進行排序。

```vb
Dim words = {"the", "quick", "brown", "fox", "jumps"}

Dim sortQuery = From word In words
                Order By word.Length, word.Substring(0, 1) Descending
                Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In sortQuery
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' fox
' the
' quick
' jumps
' brown
```

## <a name="see-also"></a>另請參閱

- <xref:System.Linq>
- [標準查詢運算子概觀 (Visual Basic)](standard-query-operators-overview.md)
- [Order By 子句](../../../language-reference/queries/order-by-clause.md)
- [如何：排序查詢結果](../../language-features/linq/how-to-sort-query-results-by-using-linq.md)
- [如何：依任何字或欄位排序或篩選文字資料 (LINQ) (Visual Basic)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
