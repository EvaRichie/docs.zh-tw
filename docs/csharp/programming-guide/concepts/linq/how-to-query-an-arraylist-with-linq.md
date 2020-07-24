---
title: '如何使用 LINQ 查詢 ArrayList （c #）'
description: '這個範例會使用 LINQ 來查詢 c # 中的 ArrayList。 您必須宣告範圍變數的類型，以反映集合中的物件類型。'
ms.date: 07/20/2015
ms.assetid: 2bfb471c-6e9a-4e60-bd83-4a1778abde11
ms.openlocfilehash: 5c251e17de062a4578f06fc1a40ea3ede9f3ab67
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104602"
---
# <a name="how-to-query-an-arraylist-with-linq-c"></a><span data-ttu-id="1b199-104">如何使用 LINQ 查詢 ArrayList （c #）</span><span class="sxs-lookup"><span data-stu-id="1b199-104">How to query an ArrayList with LINQ (C#)</span></span>
<span data-ttu-id="1b199-105">使用 LINQ 查詢非泛型 <xref:System.Collections.IEnumerable> 集合時 (例如 <xref:System.Collections.ArrayList>)，您必須明確宣告範圍變數的類型，以反映集合中特定類型的物件。</span><span class="sxs-lookup"><span data-stu-id="1b199-105">When using LINQ to query non-generic <xref:System.Collections.IEnumerable> collections such as <xref:System.Collections.ArrayList>, you must explicitly declare the type of the range variable to reflect the specific type of the objects in the collection.</span></span> <span data-ttu-id="1b199-106">例如，如果您有 `Student` 物件的 <xref:System.Collections.ArrayList>，您的 [from 子句](../../../language-reference/keywords/from-clause.md)看起來應該如下：</span><span class="sxs-lookup"><span data-stu-id="1b199-106">For example, if you have an <xref:System.Collections.ArrayList> of `Student` objects, your [from clause](../../../language-reference/keywords/from-clause.md) should look like this:</span></span>  
  
```csharp
var query = from Student s in arrList  
//...
```  
  
 <span data-ttu-id="1b199-107">藉由指定範圍變數的類型，您就可以將 <xref:System.Collections.ArrayList> 中的每個項目轉換為 `Student`。</span><span class="sxs-lookup"><span data-stu-id="1b199-107">By specifying the type of the range variable, you are casting each item in the <xref:System.Collections.ArrayList> to a `Student`.</span></span>  
  
 <span data-ttu-id="1b199-108">在查詢運算式中使用具有明確類型的範圍變數，相當於呼叫 <xref:System.Linq.Enumerable.Cast%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="1b199-108">The use of an explicitly typed range variable in a query expression is equivalent to calling the <xref:System.Linq.Enumerable.Cast%2A> method.</span></span> <span data-ttu-id="1b199-109">如果無法執行指定的轉換，則 <xref:System.Linq.Enumerable.Cast%2A> 會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1b199-109"><xref:System.Linq.Enumerable.Cast%2A> throws an exception if the specified cast cannot be performed.</span></span> <span data-ttu-id="1b199-110"><xref:System.Linq.Enumerable.Cast%2A> 和 <xref:System.Linq.Enumerable.OfType%2A> 是對非泛型 <xref:System.Collections.IEnumerable> 類型執行的兩個標準查詢運算子方法。</span><span class="sxs-lookup"><span data-stu-id="1b199-110"><xref:System.Linq.Enumerable.Cast%2A> and <xref:System.Linq.Enumerable.OfType%2A> are the two Standard Query Operator methods that operate on non-generic <xref:System.Collections.IEnumerable> types.</span></span> <span data-ttu-id="1b199-111">如需詳細資訊，請參閱 [LINQ 查詢作業中的類型關聯性](./type-relationships-in-linq-query-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="1b199-111">For more information, see [Type Relationships in LINQ Query Operations](./type-relationships-in-linq-query-operations.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="1b199-112">範例</span><span class="sxs-lookup"><span data-stu-id="1b199-112">Example</span></span>  
 <span data-ttu-id="1b199-113">下列範例將顯示 <xref:System.Collections.ArrayList> 的簡單查詢。</span><span class="sxs-lookup"><span data-stu-id="1b199-113">The following example shows a simple query over an <xref:System.Collections.ArrayList>.</span></span> <span data-ttu-id="1b199-114">請注意，此範例會在程式碼呼叫 <xref:System.Collections.ArrayList.Add%2A> 方法時使用物件初始設定式，但這不是必要的。</span><span class="sxs-lookup"><span data-stu-id="1b199-114">Note that this example uses object initializers when the code calls the <xref:System.Collections.ArrayList.Add%2A> method, but this is not a requirement.</span></span>  
  
```csharp  
using System;  
using System.Collections;  
using System.Linq;  
  
namespace NonGenericLINQ  
{  
    public class Student  
    {  
        public string FirstName { get; set; }  
        public string LastName { get; set; }  
        public int[] Scores { get; set; }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ArrayList arrList = new ArrayList();  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Svetlana", LastName = "Omelchenko", Scores = new int[] { 98, 92, 81, 60 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Claire", LastName = "O’Donnell", Scores = new int[] { 75, 84, 91, 39 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Sven", LastName = "Mortensen", Scores = new int[] { 88, 94, 65, 91 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Cesar", LastName = "Garcia", Scores = new int[] { 97, 89, 85, 82 }  
                    });  
  
            var query = from Student student in arrList  
                        where student.Scores[0] > 95  
                        select student;  
  
            foreach (Student s in query)  
                Console.WriteLine(s.LastName + ": " + s.Scores[0]);  
  
            // Keep the console window open in debug mode.  
            Console.WriteLine("Press any key to exit.");  
            Console.ReadKey();  
        }  
    }  
}  
/* Output:
    Omelchenko: 98  
    Garcia: 97  
*/  
```  
  
## <a name="see-also"></a><span data-ttu-id="1b199-115">請參閱</span><span class="sxs-lookup"><span data-stu-id="1b199-115">See also</span></span>

- [<span data-ttu-id="1b199-116">LINQ to Objects (C#)</span><span class="sxs-lookup"><span data-stu-id="1b199-116">LINQ to Objects (C#)</span></span>](./linq-to-objects.md)
