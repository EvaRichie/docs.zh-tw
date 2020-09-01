---
description: from 子句 - C# 參考
title: from 子句 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- from_CSharpKeyword
- from
helpviewer_keywords:
- from clause [C#]
- from keyword [C#]
ms.assetid: 1aefd18c-1314-47f8-99ec-9bcefb09e699
ms.openlocfilehash: 474b22f5a9d8f12c8a4365159817f878761b563c
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89140785"
---
# <a name="from-clause-c-reference"></a><span data-ttu-id="929f7-103">from 子句 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="929f7-103">from clause (C# Reference)</span></span>

<span data-ttu-id="929f7-104">查詢運算式的開頭必須是 `from` 子句。</span><span class="sxs-lookup"><span data-stu-id="929f7-104">A query expression must begin with a `from` clause.</span></span> <span data-ttu-id="929f7-105">此外，查詢運算式可以包含子查詢，也是以 `from` 子句開頭。</span><span class="sxs-lookup"><span data-stu-id="929f7-105">Additionally, a query expression can contain sub-queries, which also begin with a `from` clause.</span></span> <span data-ttu-id="929f7-106">`from` 子句指定下列內容：</span><span class="sxs-lookup"><span data-stu-id="929f7-106">The `from` clause specifies the following:</span></span>

- <span data-ttu-id="929f7-107">會執行查詢或子查詢的資料來源。</span><span class="sxs-lookup"><span data-stu-id="929f7-107">The data source on which the query or sub-query will be run.</span></span>

- <span data-ttu-id="929f7-108">本機「範圍變數」\*\*，代表來源序列中的每個項目。</span><span class="sxs-lookup"><span data-stu-id="929f7-108">A local *range variable* that represents each element in the source sequence.</span></span>

<span data-ttu-id="929f7-109">範圍變數和資料來源都是強型別。</span><span class="sxs-lookup"><span data-stu-id="929f7-109">Both the range variable and the data source are strongly typed.</span></span> <span data-ttu-id="929f7-110">`from` 子句中參考的資料來源，必須有 <xref:System.Collections.IEnumerable>、<xref:System.Collections.Generic.IEnumerable%601> 類型，或 <xref:System.Linq.IQueryable%601> 等衍生類型。</span><span class="sxs-lookup"><span data-stu-id="929f7-110">The data source referenced in the `from` clause must have a type of <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, or a derived type such as <xref:System.Linq.IQueryable%601>.</span></span>

<span data-ttu-id="929f7-111">在下例中，`numbers` 是資料來源，而 `num` 是範圍變數。</span><span class="sxs-lookup"><span data-stu-id="929f7-111">In the following example, `numbers` is the data source and `num` is the range variable.</span></span> <span data-ttu-id="929f7-112">請注意，即使使用 [var](var.md) 關鍵字，這兩個變數都是強型別。</span><span class="sxs-lookup"><span data-stu-id="929f7-112">Note that both variables are strongly typed even though the [var](var.md) keyword is used.</span></span>

[!code-csharp[cscsrefQueryKeywords#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#1)]

## <a name="the-range-variable"></a><span data-ttu-id="929f7-113">範圍變數</span><span class="sxs-lookup"><span data-stu-id="929f7-113">The range variable</span></span>

<span data-ttu-id="929f7-114">當資料來源實作 <xref:System.Collections.Generic.IEnumerable%601> 時，編譯器會推斷範圍變數的類型。</span><span class="sxs-lookup"><span data-stu-id="929f7-114">The compiler infers the type of the range variable when the data source implements <xref:System.Collections.Generic.IEnumerable%601>.</span></span> <span data-ttu-id="929f7-115">例如，如果來源有類型 `IEnumerable<Customer>`，則範圍變數推斷為 `Customer`。</span><span class="sxs-lookup"><span data-stu-id="929f7-115">For example, if the source has a type of `IEnumerable<Customer>`, then the range variable is inferred to be `Customer`.</span></span> <span data-ttu-id="929f7-116">必須明確指定類型的時機，是當來源為非泛型的 `IEnumerable` 類型時，如 <xref:System.Collections.ArrayList>。</span><span class="sxs-lookup"><span data-stu-id="929f7-116">The only time that you must specify the type explicitly is when the source is a non-generic `IEnumerable` type such as <xref:System.Collections.ArrayList>.</span></span> <span data-ttu-id="929f7-117">如需詳細資訊，請參閱 [如何使用 LINQ 查詢 ArrayList](../../programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="929f7-117">For more information, see [How to query an ArrayList with LINQ](../../programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md).</span></span>

<span data-ttu-id="929f7-118">在前例中，`num` 推斷為類型 `int`。</span><span class="sxs-lookup"><span data-stu-id="929f7-118">In the previous example `num` is inferred to be of type `int`.</span></span> <span data-ttu-id="929f7-119">因為範圍變數是強型別，所以您可以對它呼叫方法，或在其他作業中使用它。</span><span class="sxs-lookup"><span data-stu-id="929f7-119">Because the range variable is strongly typed, you can call methods on it or use it in other operations.</span></span> <span data-ttu-id="929f7-120">例如，不寫入 `select num`，而是可以寫入 `select num.ToString()` 讓查詢運算式傳回一串字串，不是整數序列。</span><span class="sxs-lookup"><span data-stu-id="929f7-120">For example, instead of writing `select num`, you could write `select num.ToString()` to cause the query expression to return a sequence of strings instead of integers.</span></span> <span data-ttu-id="929f7-121">或者可以寫入 `select num + 10` 讓運算式傳回 14、11、13、12、10 序列。</span><span class="sxs-lookup"><span data-stu-id="929f7-121">Or you could write `select num + 10` to cause the expression to return the sequence 14, 11, 13, 12, 10.</span></span> <span data-ttu-id="929f7-122">如需詳細資訊，請參閱 [select 子句](select-clause.md)。</span><span class="sxs-lookup"><span data-stu-id="929f7-122">For more information, see [select clause](select-clause.md).</span></span>

<span data-ttu-id="929f7-123">範圍變數就像 [foreach](foreach-in.md) 陳述式中的反覆項目變數，但有一個非常重要的差異：範圍變數從不真正儲存來源的資料。</span><span class="sxs-lookup"><span data-stu-id="929f7-123">The range variable is like an iteration variable in a [foreach](foreach-in.md) statement except for one very important difference: a range variable never actually stores data from the source.</span></span> <span data-ttu-id="929f7-124">它只是用來提供語法上的便利性，為的是要讓查詢描述在執行查詢時會發生什麼。</span><span class="sxs-lookup"><span data-stu-id="929f7-124">It's just a syntactic convenience that enables the query to describe what will occur when the query is executed.</span></span> <span data-ttu-id="929f7-125">如需詳細資訊，請參閱 [LINQ 查詢簡介 (C#)](../../programming-guide/concepts/linq/introduction-to-linq-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="929f7-125">For more information, see [Introduction to LINQ Queries (C#)](../../programming-guide/concepts/linq/introduction-to-linq-queries.md).</span></span>

## <a name="compound-from-clauses"></a><span data-ttu-id="929f7-126">複合 from 子句</span><span class="sxs-lookup"><span data-stu-id="929f7-126">Compound from clauses</span></span>

<span data-ttu-id="929f7-127">在某些情況下，來源序列中的每個項目自己本身可能就是序列或包含序列。</span><span class="sxs-lookup"><span data-stu-id="929f7-127">In some cases, each element in the source sequence may itself be either a sequence or contain a sequence.</span></span> <span data-ttu-id="929f7-128">例如，您的資料來源可能是 `IEnumerable<Student>`，其中序列中的每個學生物件都包含測驗分數的清單。</span><span class="sxs-lookup"><span data-stu-id="929f7-128">For example, your data source may be an `IEnumerable<Student>` where each student object in the sequence contains a list of test scores.</span></span> <span data-ttu-id="929f7-129">若要存取每個 `Student` 項目內的內部清單，您可以使用複合 `from` 子句。</span><span class="sxs-lookup"><span data-stu-id="929f7-129">To access the inner list within each `Student` element, you can use compound `from` clauses.</span></span> <span data-ttu-id="929f7-130">技巧就像使用巢狀的 [foreach](foreach-in.md) 陳述式一樣。</span><span class="sxs-lookup"><span data-stu-id="929f7-130">The technique is like using nested [foreach](foreach-in.md) statements.</span></span> <span data-ttu-id="929f7-131">您可以將 [where](partial-method.md) 或 [orderby](orderby-clause.md) 子句新增至任一 `from` 子句來篩選結果。</span><span class="sxs-lookup"><span data-stu-id="929f7-131">You can add [where](partial-method.md) or [orderby](orderby-clause.md) clauses to either `from` clause to filter the results.</span></span> <span data-ttu-id="929f7-132">下例顯示一系列 `Student` 物件，每個都包含代表測試分數的整數內部 `List`。</span><span class="sxs-lookup"><span data-stu-id="929f7-132">The following example shows a sequence of `Student` objects, each of which contains an inner `List` of integers representing test scores.</span></span> <span data-ttu-id="929f7-133">若要存取內部清單，請使用複合 `from` 子句。</span><span class="sxs-lookup"><span data-stu-id="929f7-133">To access the inner list, use a compound `from` clause.</span></span> <span data-ttu-id="929f7-134">如有必要，您可以在兩個 `from` 子句之間插入子句。</span><span class="sxs-lookup"><span data-stu-id="929f7-134">You can insert clauses between the two `from` clauses if necessary.</span></span>

[!code-csharp[cscsrefQueryKeywords#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#2)]

## <a name="using-multiple-from-clauses-to-perform-joins"></a><span data-ttu-id="929f7-135">使用多個 from 子句執行聯結</span><span class="sxs-lookup"><span data-stu-id="929f7-135">Using Multiple from Clauses to Perform Joins</span></span>

<span data-ttu-id="929f7-136">複合 `from` 子句是用來存取單一資料來源中的內部集合。</span><span class="sxs-lookup"><span data-stu-id="929f7-136">A compound `from` clause is used to access inner collections in a single data source.</span></span> <span data-ttu-id="929f7-137">不過，查詢也可以包含多個 `from` 子句，從獨立的資料來源產生增補查詢。</span><span class="sxs-lookup"><span data-stu-id="929f7-137">However, a query can also contain multiple `from` clauses that generate supplemental queries from independent data sources.</span></span> <span data-ttu-id="929f7-138">這項技術可讓您執行特定的聯結作業類型，這些是使用 [join 子句](join-clause.md)都不可能執行的類型。</span><span class="sxs-lookup"><span data-stu-id="929f7-138">This technique enables you to perform certain types of join operations that are not possible by using the [join clause](join-clause.md).</span></span>

<span data-ttu-id="929f7-139">下例示範如何使用兩個 `from` 子句形成兩個資料來源的完整交叉聯結。</span><span class="sxs-lookup"><span data-stu-id="929f7-139">The following example shows how two `from` clauses can be used to form a complete cross join of two data sources.</span></span>

[!code-csharp[cscsrefQueryKeywords#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/From.cs#3)]

<span data-ttu-id="929f7-140">如需使用多個 `from` 子句的聯結作業詳細資訊，請參閱[執行左方外部聯結](../../linq/perform-left-outer-joins.md)。</span><span class="sxs-lookup"><span data-stu-id="929f7-140">For more information about join operations that use multiple `from` clauses, see [Perform left outer joins](../../linq/perform-left-outer-joins.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="929f7-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="929f7-141">See also</span></span>

- [<span data-ttu-id="929f7-142">LINQ)  (查詢關鍵字 </span><span class="sxs-lookup"><span data-stu-id="929f7-142">Query Keywords (LINQ)</span></span>](query-keywords.md)
- [<span data-ttu-id="929f7-143">Language Integrated Query (LINQ)</span><span class="sxs-lookup"><span data-stu-id="929f7-143">Language Integrated Query (LINQ)</span></span>](../../linq/index.md)
