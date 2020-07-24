---
title: 延後執行範例 (C#)
description: '瞭解延後執行和延遲評估如何影響 c # 中 LINQ to XML 查詢的執行。'
ms.date: 07/20/2015
ms.assetid: 50f4fbac-81fe-4f26-aedf-506e21419b19
ms.openlocfilehash: 65ba4cc150f2fc9d8f44aee352987ea0eeaab0a5
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103952"
---
# <a name="deferred-execution-example-c"></a><span data-ttu-id="299ec-103">延後執行範例 (C#)</span><span class="sxs-lookup"><span data-stu-id="299ec-103">Deferred Execution Example (C#)</span></span>
<span data-ttu-id="299ec-104">本主題顯示延後執行與延遲評估如何影響您 LINQ to XML 查詢的執行。</span><span class="sxs-lookup"><span data-stu-id="299ec-104">This topic shows how deferred execution and lazy evaluation affect the execution of your LINQ to XML queries.</span></span>  
  
## <a name="example"></a><span data-ttu-id="299ec-105">範例</span><span class="sxs-lookup"><span data-stu-id="299ec-105">Example</span></span>  
 <span data-ttu-id="299ec-106">下列範例顯示利用使用延後執行的擴充方法時的執行順序。</span><span class="sxs-lookup"><span data-stu-id="299ec-106">The following example shows the order of execution when using an extension method that uses deferred execution.</span></span> <span data-ttu-id="299ec-107">此範例會宣告三個字串的陣列。</span><span class="sxs-lookup"><span data-stu-id="299ec-107">The example declares an array of three strings.</span></span> <span data-ttu-id="299ec-108">接著，它會逐一查看 `ConvertCollectionToUpperCase` 所傳回的集合。</span><span class="sxs-lookup"><span data-stu-id="299ec-108">It then iterates through the collection returned by `ConvertCollectionToUpperCase`.</span></span>  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source {0}", str);  
            yield return str.ToUpper();  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        var q = from str in stringArray.ConvertCollectionToUpperCase()  
                select str;  
  
        foreach (string str in q)  
            Console.WriteLine("Main: str {0}", str);  
    }  
}  
```  
  
 <span data-ttu-id="299ec-109">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="299ec-109">This example produces the following output:</span></span>  
  
```output  
ToUpper: source abc  
Main: str ABC  
ToUpper: source def  
Main: str DEF  
ToUpper: source ghi  
Main: str GHI  
```  
  
 <span data-ttu-id="299ec-110">請注意，逐一查看 `ConvertCollectionToUpperCase` 所傳回的集合時，會從來源字串陣列擷取每個項目，並在下一個項目從來源字串陣列擷取前，轉換為大寫。</span><span class="sxs-lookup"><span data-stu-id="299ec-110">Notice that when iterating through the collection returned by `ConvertCollectionToUpperCase`, each item is retrieved from the source string array and converted to uppercase before the next item is retrieved from the source string array.</span></span>  
  
 <span data-ttu-id="299ec-111">您可以看到在所傳回之集合中的每個項目在 `foreach` 的 `Main` 迴圈中處理前，字串的整個陣列都沒有轉換為大寫。</span><span class="sxs-lookup"><span data-stu-id="299ec-111">You can see that the entire array of strings is not converted to uppercase before each item in the returned collection is processed in the `foreach` loop in `Main`.</span></span>  
  
 <span data-ttu-id="299ec-112">本教學課程中的下一個主題說明將查詢鏈結在一起：</span><span class="sxs-lookup"><span data-stu-id="299ec-112">The next topic in this tutorial illustrates chaining queries together:</span></span>  
  
- [<span data-ttu-id="299ec-113">鏈結查詢範例 (C#)</span><span class="sxs-lookup"><span data-stu-id="299ec-113">Chaining Queries Example (C#)</span></span>](./chaining-queries-example.md)  
  
## <a name="see-also"></a><span data-ttu-id="299ec-114">請參閱</span><span class="sxs-lookup"><span data-stu-id="299ec-114">See also</span></span>

- [<span data-ttu-id="299ec-115">教學課程：將查詢鏈結在一起 (C#)</span><span class="sxs-lookup"><span data-stu-id="299ec-115">Tutorial: Chaining Queries Together (C#)</span></span>](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)
