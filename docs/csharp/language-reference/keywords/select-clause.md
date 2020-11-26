---
description: select 子句 - C# 參考
title: select 子句 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- select_CSharpKeyword
- select
helpviewer_keywords:
- select keyword [C#]
- select clause [C#]
ms.assetid: df01e266-5781-4aaa-80c4-67cf28ea093f
ms.openlocfilehash: d67c99cc841c08a63cc83843a07a46e80199b9d1
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "89136898"
---
# <a name="select-clause-c-reference"></a><span data-ttu-id="1e36c-103">select 子句 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="1e36c-103">select clause (C# Reference)</span></span>

<span data-ttu-id="1e36c-104">在查詢運算式中，`select` 子句指定將在執行查詢時產生之值的類型。</span><span class="sxs-lookup"><span data-stu-id="1e36c-104">In a query expression, the `select` clause specifies the type of values that will be produced when the query is executed.</span></span> <span data-ttu-id="1e36c-105">結果是根據評估所有先前子句以及 `select` 子句本身中的任何運算式而來。</span><span class="sxs-lookup"><span data-stu-id="1e36c-105">The result is based on the evaluation of all the previous clauses and on any expressions in the `select` clause itself.</span></span> <span data-ttu-id="1e36c-106">查詢運算式必須以 `select` 子句或 [group](group-clause.md) 子句來終止。</span><span class="sxs-lookup"><span data-stu-id="1e36c-106">A query expression must terminate with either a `select` clause or a [group](group-clause.md) clause.</span></span>

<span data-ttu-id="1e36c-107">下列範例示範查詢運算式中的簡單 `select` 子句。</span><span class="sxs-lookup"><span data-stu-id="1e36c-107">The following example shows a simple `select` clause in a query expression.</span></span>

[!code-csharp[cscsrefQueryKeywords#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Select.cs#8)]  

<span data-ttu-id="1e36c-108">`select` 子句所產生的序列類型可決定查詢變數 `queryHighScores` 的類型。</span><span class="sxs-lookup"><span data-stu-id="1e36c-108">The type of the sequence produced by the `select` clause determines the type of the query variable `queryHighScores`.</span></span> <span data-ttu-id="1e36c-109">在最簡單的情況下，`select` 子句只會指定範圍變數。</span><span class="sxs-lookup"><span data-stu-id="1e36c-109">In the simplest case, the `select` clause just specifies the range variable.</span></span> <span data-ttu-id="1e36c-110">這會導致傳回的序列將相同類型的項目包含為資料來源。</span><span class="sxs-lookup"><span data-stu-id="1e36c-110">This causes the returned sequence to contain elements of the same type as the data source.</span></span> <span data-ttu-id="1e36c-111">如需詳細資訊，請參閱 [LINQ 查詢作業中的類型關聯性](../../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="1e36c-111">For more information, see [Type Relationships in LINQ Query Operations](../../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).</span></span> <span data-ttu-id="1e36c-112">不過，`select` 子句也提供功能強大的機制，將來源資料轉換 (或「投影」) 為新的類型。</span><span class="sxs-lookup"><span data-stu-id="1e36c-112">However, the `select` clause also provides a powerful mechanism for transforming (or *projecting*) source data into new types.</span></span> <span data-ttu-id="1e36c-113">如需詳細資訊，請參閱[使用 LINQ 轉換資料 (C#)](../../programming-guide/concepts/linq/data-transformations-with-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="1e36c-113">For more information, see [Data Transformations with LINQ (C#)](../../programming-guide/concepts/linq/data-transformations-with-linq.md).</span></span>

## <a name="example"></a><span data-ttu-id="1e36c-114">範例</span><span class="sxs-lookup"><span data-stu-id="1e36c-114">Example</span></span>

<span data-ttu-id="1e36c-115">下列範例示範 `select` 子句可接受的所有不同形式。</span><span class="sxs-lookup"><span data-stu-id="1e36c-115">The following example shows all the different forms that a `select` clause may take.</span></span> <span data-ttu-id="1e36c-116">在每個查詢中，請注意子句之間的關聯性， `select` 以及 *查詢變數* 的類型 (`studentQuery1` 、 `studentQuery2` 和等) 。</span><span class="sxs-lookup"><span data-stu-id="1e36c-116">In each query, note the relationship between the `select` clause and the type of the *query variable* (`studentQuery1`, `studentQuery2`, and so on).</span></span>

[!code-csharp[cscsrefQueryKeywords#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Select.cs#9)]

<span data-ttu-id="1e36c-117">如前一個範例中的 `studentQuery8` 所示，您有時可能想要所傳回序列的項目只包含來源項目的屬性子集。</span><span class="sxs-lookup"><span data-stu-id="1e36c-117">As shown in `studentQuery8` in the previous example, sometimes you might want the elements of the returned sequence to contain only a subset of the properties of the source elements.</span></span> <span data-ttu-id="1e36c-118">盡量保持最少的所傳回序列，以降低記憶體需求，並提高查詢的執行速度。</span><span class="sxs-lookup"><span data-stu-id="1e36c-118">By keeping the returned sequence as small as possible you can reduce the memory requirements and increase the speed of the execution of the query.</span></span> <span data-ttu-id="1e36c-119">做法是在 `select` 子句中建立匿名型別，並使用物件初始設定式以利用來源項目中的適當屬性來初始化它。</span><span class="sxs-lookup"><span data-stu-id="1e36c-119">You can accomplish this by creating an anonymous type in the `select` clause and using an object initializer to initialize it with the appropriate properties from the source element.</span></span> <span data-ttu-id="1e36c-120">如需如何執行此作業的範例，請參閱[物件和集合初始設定式](../../programming-guide/classes-and-structs/object-and-collection-initializers.md)。</span><span class="sxs-lookup"><span data-stu-id="1e36c-120">For an example of how to do this, see [Object and Collection Initializers](../../programming-guide/classes-and-structs/object-and-collection-initializers.md).</span></span>

## <a name="remarks"></a><span data-ttu-id="1e36c-121">備註</span><span class="sxs-lookup"><span data-stu-id="1e36c-121">Remarks</span></span>

<span data-ttu-id="1e36c-122">在編譯時間，`select` 子句會轉譯為 <xref:System.Linq.Enumerable.Select%2A> 標準查詢運算子的方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="1e36c-122">At compile time, the `select` clause is translated to a method call to the <xref:System.Linq.Enumerable.Select%2A> standard query operator.</span></span>

## <a name="see-also"></a><span data-ttu-id="1e36c-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1e36c-123">See also</span></span>

- [<span data-ttu-id="1e36c-124">C # 參考</span><span class="sxs-lookup"><span data-stu-id="1e36c-124">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="1e36c-125">LINQ)  (查詢關鍵字 </span><span class="sxs-lookup"><span data-stu-id="1e36c-125">Query Keywords (LINQ)</span></span>](query-keywords.md)
- [<span data-ttu-id="1e36c-126">from 子句</span><span class="sxs-lookup"><span data-stu-id="1e36c-126">from clause</span></span>](from-clause.md)
- [<span data-ttu-id="1e36c-127">partial (方法) (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="1e36c-127">partial (Method) (C# Reference)</span></span>](partial-method.md)
- [<span data-ttu-id="1e36c-128">匿名類型</span><span class="sxs-lookup"><span data-stu-id="1e36c-128">Anonymous Types</span></span>](../../programming-guide/classes-and-structs/anonymous-types.md)
- [<span data-ttu-id="1e36c-129">C# 中的 LINQ</span><span class="sxs-lookup"><span data-stu-id="1e36c-129">LINQ in C#</span></span>](../../linq/index.md)
- [<span data-ttu-id="1e36c-130">Language Integrated Query (LINQ)</span><span class="sxs-lookup"><span data-stu-id="1e36c-130">Language Integrated Query (LINQ)</span></span>](../../programming-guide/concepts/linq/index.md)
