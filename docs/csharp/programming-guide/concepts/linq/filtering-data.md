---
title: 篩選資料 (C#)
description: '篩選（也稱為選取）會根據條件來限制結果。 瞭解在 c # 中執行篩選的 LINQ 中的標準查詢運算子方法。'
ms.date: 07/20/2015
ms.assetid: fbaece0d-0f23-47f7-89c5-f3ea8db692b6
ms.openlocfilehash: f9f6d691da73b566e5135f6692c87ba3a8978005
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103922"
---
# <a name="filtering-data-c"></a>篩選資料 (C#)
篩選指的是將結果集限制為只包含符合指定條件之元素的作業， 也稱為選取。  
  
 下圖顯示字元序列的篩選結果。 篩選作業的述詞指定字元必須為 'A'。  
  
 ![顯示 LINQ 篩選作業的圖表](./media/filtering-data/linq-filter-operation.png)  
  
 執行選取的標準查詢運算子方法詳列於下一節。  
  
## <a name="methods"></a>方法  
  
|方法名稱|說明|C# 查詢運算式語法|相關資訊|  
|-----------------|-----------------|---------------------------------|----------------------|  
|OfType|根據可轉換為所指定類型的能力來選取值。|不適用。|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=nameWithType>|  
|Where|根據述詞函式來選取值。|`where`|<xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>查詢運算式語法範例  
 下列範例使用 `where` 子句從陣列篩選出具有特定長度的字串。  
  
```csharp  
string[] words = { "the", "quick", "brown", "fox", "jumps" };  
  
IEnumerable<string> query = from word in words  
                            where word.Length == 3  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
*/  
```  
  
## <a name="see-also"></a>請參閱

- <xref:System.Linq>
- [標準查詢運算子概觀 (C#)](./standard-query-operators-overview.md)
- [where 子句](../../../language-reference/keywords/where-clause.md)
- [在執行階段動態指定述詞篩選](../../../linq/dynamically-specify-predicate-filters-at-runtime.md)
- [如何使用反映查詢元件的中繼資料（LINQ）（c #）](./how-to-query-an-assembly-s-metadata-with-reflection-linq.md)
- [如何查詢具有指定屬性或名稱的檔案（c #）](./how-to-query-for-files-with-a-specified-attribute-or-name.md)
- [如何依任何字或欄位排序或篩選文字資料（LINQ）（c #）](./how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
