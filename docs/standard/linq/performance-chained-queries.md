---
title: 連結的查詢效能-LINQ to XML
description: 深入瞭解連鎖查詢可執行檔工作，以及單一較大型且更複雜的查詢。
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b2f1d715-8946-4dc0-8d56-fb3d1bba54a6
ms.openlocfilehash: c1dae1eaf008a1f17c6884ef6b8e67d042719ad9
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552163"
---
# <a name="performance-of-chained-queries-linq-to-xml"></a><span data-ttu-id="470bb-103">連結的查詢效能 (LINQ to XML) </span><span class="sxs-lookup"><span data-stu-id="470bb-103">Performance of chained queries (LINQ to XML)</span></span>

<span data-ttu-id="470bb-104">LINQ (和 LINQ to XML) 最重要的優點之一，就是連結查詢可以執行，以及比連鎖查詢更大且更複雜的單一查詢。</span><span class="sxs-lookup"><span data-stu-id="470bb-104">One of the most important benefits of LINQ (and LINQ to XML) is that chained queries can perform as well as a single query that is larger and more complicated than the chained queries.</span></span>

<span data-ttu-id="470bb-105">鏈結查詢是指使用其他查詢當做其來源的查詢。</span><span class="sxs-lookup"><span data-stu-id="470bb-105">A chained query is a query that uses another query as its source.</span></span> <span data-ttu-id="470bb-106">例如，在下列簡單程式碼中，`query2` 具有 `query1` 當做其來源：</span><span class="sxs-lookup"><span data-stu-id="470bb-106">For example, in the following simple code, `query2` has `query1` as its source:</span></span>

```csharp
XElement root = new XElement("Root",
    new XElement("Child", 1),
    new XElement("Child", 2),
    new XElement("Child", 3),
    new XElement("Child", 4)
);

var query1 = from x in root.Elements("Child")
             where (int)x >= 3
             select x;

var query2 = from e in query1
             where (int)e % 2 == 0
             select e;

foreach (var i in query2)
    Console.WriteLine("{0}", (int)i);
```

```vb
Dim root As New XElement("Root", New XElement("Child", 1), New XElement("Child", 2), New XElement("Child", 3), New XElement("Child", 4))

Dim query1 = From x In root.Elements("Child") Where CInt(x) >= 3x

Dim query2 = From e In query1 Where CInt(e) Mod 2 = 0e

For Each i As var In query2
    Console.WriteLine("{0}", CInt(i))
Next
```

<span data-ttu-id="470bb-107">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="470bb-107">This example produces the following output:</span></span>

```output
4
```

<span data-ttu-id="470bb-108">這個鏈結查詢會與逐一查看連結串列 (Linked List) 提供相同的效能設定檔。</span><span class="sxs-lookup"><span data-stu-id="470bb-108">This chained query provides the same performance profile as iterating through a linked list.</span></span>

- <span data-ttu-id="470bb-109"><xref:System.Xml.Linq.XContainer.Elements%2A> 軸基本上與逐一查看連結串列具有相同的效能。</span><span class="sxs-lookup"><span data-stu-id="470bb-109">The <xref:System.Xml.Linq.XContainer.Elements%2A> axis has essentially the same performance as iterating through a linked list.</span></span> <span data-ttu-id="470bb-110"><xref:System.Xml.Linq.XContainer.Elements%2A> 會實作成延後執行的 Iterator。</span><span class="sxs-lookup"><span data-stu-id="470bb-110"><xref:System.Xml.Linq.XContainer.Elements%2A> is implemented as an iterator with deferred execution.</span></span> <span data-ttu-id="470bb-111">這表示，除了逐一查看連結串列以外，它會執行一些工作，例如配置 Iterator 物件和追蹤執行狀態。</span><span class="sxs-lookup"><span data-stu-id="470bb-111">This means that it does some work in addition to iterating through the linked list, such as allocating the iterator object and keeping track of execution state.</span></span> <span data-ttu-id="470bb-112">這項工作可分成兩個分類：在設定 Iterator 時完成的工作，以及在每次反覆運算期間完成的工作。</span><span class="sxs-lookup"><span data-stu-id="470bb-112">This work can be divided into two categories: the work that is done at the time the iterator is set up, and the work that is done during each iteration.</span></span> <span data-ttu-id="470bb-113">設定工作是小型且固定的工作量，而在每次反覆運算期間完成的工作則與來源集合中的項目數成正比。</span><span class="sxs-lookup"><span data-stu-id="470bb-113">The setup work is a small, fixed amount of work and the work done during each iteration is proportional to the number of items in the source collection.</span></span>
- <span data-ttu-id="470bb-114">在中 `query1` ， `where` 子句 (`Where` Visual Basic) 會讓查詢呼叫 <xref:System.Linq.Enumerable.Where%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="470bb-114">In `query1`, the `where` clause (`Where` in Visual Basic) causes the query to call the <xref:System.Linq.Enumerable.Where%2A> method.</span></span> <span data-ttu-id="470bb-115">這個方法也會實作成 Iterator。</span><span class="sxs-lookup"><span data-stu-id="470bb-115">This method is also implemented as an iterator.</span></span> <span data-ttu-id="470bb-116">設定工作包含具現化將參考 Lambda 運算式的委派 (Delegate)，以及進行 Iterator 的一般設定。</span><span class="sxs-lookup"><span data-stu-id="470bb-116">The setup work consists of instantiating the delegate that will reference the lambda expression, plus the normal setup for an iterator.</span></span> <span data-ttu-id="470bb-117">進行每次反覆運算時，系統會呼叫此委派來執行述詞 (Predicate)。</span><span class="sxs-lookup"><span data-stu-id="470bb-117">With each iteration, the delegate is called to execute the predicate.</span></span> <span data-ttu-id="470bb-118">設定工作和每次反覆運算期間完成的工作，類似于反覆運算軸時完成的工作。</span><span class="sxs-lookup"><span data-stu-id="470bb-118">The setup work and the work done during each iteration is similar to the work done while iterating through the axis.</span></span>
- <span data-ttu-id="470bb-119">在 `query1` 中，select 子句會讓查詢呼叫 <xref:System.Linq.Enumerable.Select%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="470bb-119">In `query1`, the select clause causes the query to call the <xref:System.Linq.Enumerable.Select%2A> method.</span></span> <span data-ttu-id="470bb-120">這個方法與 <xref:System.Linq.Enumerable.Where%2A> 方法具有相同的效能設定檔。</span><span class="sxs-lookup"><span data-stu-id="470bb-120">This method has the same performance profile as the <xref:System.Linq.Enumerable.Where%2A> method.</span></span>
- <span data-ttu-id="470bb-121">在中 `query2` ， `where` (`Where` Visual Basic) 和子句中的子句都具有與 `select` 中相同的效能設定檔 `query1` 。</span><span class="sxs-lookup"><span data-stu-id="470bb-121">In `query2`, both the `where` clause (`Where` in Visual Basic) and the `select` clause have the same performance profile as in `query1`.</span></span>

<span data-ttu-id="470bb-122">因此，逐一查看 `query2` 的作業會直接與第一個查詢之來源中的項目數成正比 (亦即，線性時間)。</span><span class="sxs-lookup"><span data-stu-id="470bb-122">The iteration through `query2` is therefore directly proportional to the number of items in the source of the first query, in other words, linear time.</span></span>

<span data-ttu-id="470bb-123">如需迭代器的詳細資訊，請參閱 [yield](../../csharp/language-reference/keywords/yield.md)。</span><span class="sxs-lookup"><span data-stu-id="470bb-123">For more information on iterators, see [yield](../../csharp/language-reference/keywords/yield.md).</span></span>

<span data-ttu-id="470bb-124">如需將查詢連結在一起的詳細教學課程，請參閱 [教學課程： (c # ) 一起使用連鎖查詢 ](chain-queries-example.md)。</span><span class="sxs-lookup"><span data-stu-id="470bb-124">For a more detailed tutorial on chaining queries together, see [Tutorial: Chain queries together (C#)](chain-queries-example.md).</span></span>
