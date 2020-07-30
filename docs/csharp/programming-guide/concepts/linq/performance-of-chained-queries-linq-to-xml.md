---
title: 已鏈結之查詢的效能 (LINQ to XML) (C#)
description: 瞭解連鎖查詢的效能。 鏈結查詢是指使用其他查詢當做其來源的查詢。
ms.date: 07/20/2015
ms.assetid: b2f1d715-8946-4dc0-8d56-fb3d1bba54a6
ms.openlocfilehash: 1e9173e85845dd085f4d7bf6deec7eb498acd7f3
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302850"
---
# <a name="performance-of-chained-queries-linq-to-xml-c"></a><span data-ttu-id="01460-104">已鏈結之查詢的效能 (LINQ to XML) (C#)</span><span class="sxs-lookup"><span data-stu-id="01460-104">Performance of Chained Queries (LINQ to XML) (C#)</span></span>

<span data-ttu-id="01460-105">LINQ (和 LINQ to XML) 其中一個最重要的優點在於，鏈結查詢的執行效能就如同單一較大且更複雜的查詢。</span><span class="sxs-lookup"><span data-stu-id="01460-105">One of the most important benefits of LINQ (and LINQ to XML) is that chained queries can perform as well as a single larger, more complicated query.</span></span>

<span data-ttu-id="01460-106">鏈結查詢是指使用其他查詢當做其來源的查詢。</span><span class="sxs-lookup"><span data-stu-id="01460-106">A chained query is a query that uses another query as its source.</span></span> <span data-ttu-id="01460-107">例如，在下列簡單程式碼中，`query2` 具有 `query1` 當做其來源：</span><span class="sxs-lookup"><span data-stu-id="01460-107">For example, in the following simple code, `query2` has `query1` as its source:</span></span>

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

<span data-ttu-id="01460-108">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="01460-108">This example produces the following output:</span></span>

```output
4
```

<span data-ttu-id="01460-109">這個鏈結查詢會與逐一查看連結串列 (Linked List) 提供相同的效能設定檔。</span><span class="sxs-lookup"><span data-stu-id="01460-109">This chained query provides the same performance profile as iterating through a linked list.</span></span>

- <span data-ttu-id="01460-110"><xref:System.Xml.Linq.XContainer.Elements%2A> 軸基本上與逐一查看連結串列具有相同的效能。</span><span class="sxs-lookup"><span data-stu-id="01460-110">The <xref:System.Xml.Linq.XContainer.Elements%2A> axis has essentially the same performance as iterating through a linked list.</span></span> <span data-ttu-id="01460-111"><xref:System.Xml.Linq.XContainer.Elements%2A> 會實作成延後執行的 Iterator。</span><span class="sxs-lookup"><span data-stu-id="01460-111"><xref:System.Xml.Linq.XContainer.Elements%2A> is implemented as an iterator with deferred execution.</span></span> <span data-ttu-id="01460-112">這表示，除了逐一查看連結串列以外，它會執行一些工作，例如配置 Iterator 物件和追蹤執行狀態。</span><span class="sxs-lookup"><span data-stu-id="01460-112">This means that it does some work in addition to iterating through the linked list, such as allocating the iterator object and keeping track of execution state.</span></span> <span data-ttu-id="01460-113">這項工作可分成兩個分類：在設定 Iterator 時完成的工作，以及在每次反覆運算期間完成的工作。</span><span class="sxs-lookup"><span data-stu-id="01460-113">This work can be divided into two categories: the work that is done at the time the iterator is set up, and the work that is done during each iteration.</span></span> <span data-ttu-id="01460-114">設定工作是小型且固定的工作量，而在每次反覆運算期間完成的工作則與來源集合中的項目數成正比。</span><span class="sxs-lookup"><span data-stu-id="01460-114">The setup work is a small, fixed amount of work and the work done during each iteration is proportional to the number of items in the source collection.</span></span>

- <span data-ttu-id="01460-115">在 `query1` 中，`where` 子句會讓查詢呼叫 <xref:System.Linq.Enumerable.Where%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="01460-115">In `query1`, the `where` clause causes the query to call the <xref:System.Linq.Enumerable.Where%2A> method.</span></span> <span data-ttu-id="01460-116">這個方法也會實作成 Iterator。</span><span class="sxs-lookup"><span data-stu-id="01460-116">This method is also implemented as an iterator.</span></span> <span data-ttu-id="01460-117">設定工作包含具現化將參考 Lambda 運算式的委派 (Delegate)，以及進行 Iterator 的一般設定。</span><span class="sxs-lookup"><span data-stu-id="01460-117">The setup work consists of instantiating the delegate that will reference the lambda expression, plus the normal setup for an iterator.</span></span> <span data-ttu-id="01460-118">進行每次反覆運算時，系統會呼叫此委派來執行述詞 (Predicate)。</span><span class="sxs-lookup"><span data-stu-id="01460-118">With each iteration, the delegate is called to execute the predicate.</span></span> <span data-ttu-id="01460-119">設定工作以及在每次反覆運算期間完成的工作與逐一查看軸時完成的工作很相似。</span><span class="sxs-lookup"><span data-stu-id="01460-119">The setup work and the work done during each iteration is the similar to the work done while iterating through the axis.</span></span>

- <span data-ttu-id="01460-120">在 `query1` 中，select 子句會讓查詢呼叫 <xref:System.Linq.Enumerable.Select%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="01460-120">In `query1`, the select clause causes the query to call the <xref:System.Linq.Enumerable.Select%2A> method.</span></span> <span data-ttu-id="01460-121">這個方法與 <xref:System.Linq.Enumerable.Where%2A> 方法具有相同的效能設定檔。</span><span class="sxs-lookup"><span data-stu-id="01460-121">This method has the same performance profile as the <xref:System.Linq.Enumerable.Where%2A> method.</span></span>

- <span data-ttu-id="01460-122">在 `query2` 中，`where` 子句和 `select` 子句都具有相同的效能設定檔，如同 `query1`。</span><span class="sxs-lookup"><span data-stu-id="01460-122">In `query2`, both the `where` clause and the `select` clause have the same performance profile as in `query1`.</span></span>

<span data-ttu-id="01460-123">因此，逐一查看 `query2` 的作業會直接與第一個查詢之來源中的項目數成正比 (亦即，線性時間)。</span><span class="sxs-lookup"><span data-stu-id="01460-123">The iteration through `query2` is therefore directly proportional to the number of items in the source of the first query, in other words, linear time.</span></span> <span data-ttu-id="01460-124">對應的 Visual Basic 範例會具有相同的效能設定檔。</span><span class="sxs-lookup"><span data-stu-id="01460-124">A corresponding Visual Basic example would have the same performance profile.</span></span>

<span data-ttu-id="01460-125">如需迭代器的詳細資訊，請參閱 [yield](../../../language-reference/keywords/yield.md)。</span><span class="sxs-lookup"><span data-stu-id="01460-125">For more information on iterators, see [yield](../../../language-reference/keywords/yield.md).</span></span>

<span data-ttu-id="01460-126">如需將查詢鏈結在一起的詳細教學課程，請參閱[教學課程：將查詢鏈結在一起](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)。</span><span class="sxs-lookup"><span data-stu-id="01460-126">For a more detailed tutorial on chaining queries together, see [Tutorial: Chaining Queries Together](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).</span></span>
