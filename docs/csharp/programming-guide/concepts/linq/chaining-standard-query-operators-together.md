---
title: 將標準查詢運算子鏈結在一起 (C#)
description: '這個範例會示範如何在 c # 中將標準查詢運算子連結在一起。 查詢不會具體化中繼結果。'
ms.date: 07/20/2015
ms.assetid: 66f2b0a9-2c23-4735-988e-bbc9dfb55c7b
ms.openlocfilehash: 41a7e4c7910c783d07181fe16254b0cac6902794
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104070"
---
# <a name="chaining-standard-query-operators-together-c"></a>將標準查詢運算子鏈結在一起 (C#)
這是[教學課程：將查詢鏈結在一起 (C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md) 教學課程中的最後一個主題。  
  
 標準的查詢運算子也可以鏈結在一起。 例如，您可以插入 <xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType> 運算子，也可以用延遲的方式操作。 但該運算子不會具體化任何中繼結果。  
  
## <a name="example"></a>範例  
 在此範例中，呼叫 <xref:System.Linq.Enumerable.Where%2A> 前，會先呼叫 `ConvertCollectionToUpperCase` 方法。 <xref:System.Linq.Enumerable.Where%2A> 方法會使用與本教學課程之前範例、`ConvertCollectionToUpperCase` 和 `AppendString` 中所使用之延遲方法幾乎完全相同的方式操作。  
  
 其中一種差異是，在這種情況下，<xref:System.Linq.Enumerable.Where%2A> 方法會逐一查看其來源集合、判斷第一個項目沒有傳遞述詞，然後取得下一個有傳遞的項目。 它接著會產生第二個項目。  
  
 不過，基本概念是一樣的：除非必要，否則系統不會具體化中繼集合。  
  
 使用查詢運算式時，會將這些運算式轉換為標準查詢運算子的呼叫，因此適用相同的原則。  
  
 本節中，查詢 Office Open XML 文件的所有範例都使用相同的原則。 延後執行與延遲評估是您必須了解的部分基礎概念，才能有效使用 LINQ (和 LINQ to XML)。  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source >{0}<", str);  
            yield return str.ToUpper();  
        }  
    }  
  
    public static IEnumerable<string>  
      AppendString(this IEnumerable<string> source, string stringToAppend)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("AppendString: source >{0}<", str);  
            yield return str + stringToAppend;  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        IEnumerable<string> q1 =  
            from s in stringArray.ConvertCollectionToUpperCase()  
            where s.CompareTo("D") >= 0  
            select s;  
  
        IEnumerable<string> q2 =  
            from s in q1.AppendString("!!!")  
            select s;  
  
        foreach (string str in q2)  
        {  
            Console.WriteLine("Main: str >{0}<", str);  
            Console.WriteLine();  
        }  
    }  
}  
```  
  
 這個範例會產生下列輸出：  
  
```output  
ToUpper: source >abc<  
ToUpper: source >def<  
AppendString: source >DEF<  
Main: str >DEF!!!<  
  
ToUpper: source >ghi<  
AppendString: source >GHI<  
Main: str >GHI!!!<  
```  
