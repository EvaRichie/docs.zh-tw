---
title: 排序資料 (C#)
description: '瞭解在 c # 中以 LINQ 執行排序作業的排序作業和標準查詢運算子方法。'
ms.date: 07/20/2015
ms.assetid: d93fa055-2f19-46d2-9898-e2aed628f1c9
ms.openlocfilehash: 5feeb0e2229fc370fdcb9608817f41832bffd7cc
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302330"
---
# <a name="sorting-data-c"></a>排序資料 (C#)
排序作業會根據一個或多個屬性來排序序列的項目。 第一個排序準則會執行元素的主要排序； 您可以藉由指定第二個排序準則來排序每一個主要排序群組內的元素。  
  
 下圖顯示對一系列字元執行字母順序排序作業的結果：
  
 ![顯示依字母順序排序作業的圖形。](./media/sorting-data/alphabetical-sort-operation.png)  
  
 下節列出可排序資料的標準查詢運算子方法。  
  
## <a name="methods"></a>方法  
  
|方法名稱|描述|C# 查詢運算式語法|相關資訊|  
|-----------------|-----------------|---------------------------------|----------------------|  
|OrderBy|依遞增順序排序值。|`orderby`|<xref:System.Linq.Enumerable.OrderBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OrderBy%2A?displayProperty=nameWithType>|  
|OrderByDescending|依遞減順序排序值。|`orderby … descending`|<xref:System.Linq.Enumerable.OrderByDescending%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OrderByDescending%2A?displayProperty=nameWithType>|  
|ThenBy|依遞增順序執行次要排序。|`orderby …, …`|<xref:System.Linq.Enumerable.ThenBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ThenBy%2A?displayProperty=nameWithType>|  
|ThenByDescending|依遞減順序執行次要排序。|`orderby …, … descending`|<xref:System.Linq.Enumerable.ThenByDescending%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ThenByDescending%2A?displayProperty=nameWithType>|  
|Reverse|反轉集合中項目的順序。|不適用。|<xref:System.Linq.Enumerable.Reverse%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Reverse%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-examples"></a>查詢運算式語法範例  
  
### <a name="primary-sort-examples"></a>主要排序範例  
  
#### <a name="primary-ascending-sort"></a>主要遞增排序  
 下列範例示範如何在 LINQ 查詢中使用 `orderby` 子句，依字串長度以遞增順序來排序陣列中的字串。  
  
```csharp  
string[] words = { "the", "quick", "brown", "fox", "jumps" };  
  
IEnumerable<string> query = from word in words  
                            orderby word.Length  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
    quick  
    brown  
    jumps  
*/  
```  
  
#### <a name="primary-descending-sort"></a>主要遞減排序  
 下一個範例示範如何在 LINQ 查詢中使用 `orderby descending` 子句，依其第一個字母以遞減順序來排序字串。  
  
```csharp  
string[] words = { "the", "quick", "brown", "fox", "jumps" };  
  
IEnumerable<string> query = from word in words  
                            orderby word.Substring(0, 1) descending  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    quick  
    jumps  
    fox  
    brown  
*/  
```  
  
### <a name="secondary-sort-examples"></a>次要排序範例  
  
#### <a name="secondary-ascending-sort"></a>次要遞增排序  
 下列範例示範如何在 LINQ 查詢中使用 `orderby` 子句，對陣列中的字串執行主要和次要排序。 字串主要是依長度進行排序，其次依字串的第一個字母進行排序，而兩者都是遞增排序。  
  
```csharp  
string[] words = { "the", "quick", "brown", "fox", "jumps" };  
  
IEnumerable<string> query = from word in words  
                            orderby word.Length, word.Substring(0, 1)  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    fox  
    the  
    brown  
    jumps  
    quick  
*/  
```  
  
#### <a name="secondary-descending-sort"></a>次要遞減排序  
 下一個範例示範如何在 LINQ 查詢中使用 `orderby descending` 子句，執行依遞增順序的主要排序以及依遞減順序的次要排序。 字串主要是依長度進行排序，其次依字串的第一個字母進行排序。  
  
```csharp  
string[] words = { "the", "quick", "brown", "fox", "jumps" };  
  
IEnumerable<string> query = from word in words  
                            orderby word.Length, word.Substring(0, 1) descending  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
    quick  
    jumps  
    brown  
*/  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Linq>
- [標準查詢運算子概觀 (C#)](./standard-query-operators-overview.md)
- [orderby 子句](../../../language-reference/keywords/orderby-clause.md)
- [排序 join 子句的結果](../../../linq/order-the-results-of-a-join-clause.md)
- [如何依任何字或欄位排序或篩選文字資料（LINQ）（c #）](./how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
