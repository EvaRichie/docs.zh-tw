---
title: 標準查詢運算子概觀
ms.date: 07/20/2015
ms.assetid: 302bd39e-2ec1-495b-94bf-37d370d6f05f
ms.openlocfilehash: 7c229a576f6695282473352d6253d2c699c76604
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406777"
---
# <a name="standard-query-operators-overview-visual-basic"></a><span data-ttu-id="3084a-102">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3084a-102">Standard Query Operators Overview (Visual Basic)</span></span>

<span data-ttu-id="3084a-103">「標準查詢運算子」\*\* 是形成 LINQ 模式的方法。</span><span class="sxs-lookup"><span data-stu-id="3084a-103">The *standard query operators* are the methods that form the LINQ pattern.</span></span> <span data-ttu-id="3084a-104">這些方法大多會在序列上運作，而序列是指其類型會實作 <xref:System.Collections.Generic.IEnumerable%601> 介面或 <xref:System.Linq.IQueryable%601> 介面的物件。</span><span class="sxs-lookup"><span data-stu-id="3084a-104">Most of these methods operate on sequences, where a sequence is an object whose type implements the <xref:System.Collections.Generic.IEnumerable%601> interface or the <xref:System.Linq.IQueryable%601> interface.</span></span> <span data-ttu-id="3084a-105">標準查詢運算子所提供的查詢功能包括篩選、投影、彙總、排序等等。</span><span class="sxs-lookup"><span data-stu-id="3084a-105">The standard query operators provide query capabilities including filtering, projection, aggregation, sorting and more.</span></span>

<span data-ttu-id="3084a-106">有兩組 LINQ 標準查詢運算子，一個運作於類型 <xref:System.Collections.Generic.IEnumerable%601> 的物件，另一個則運作於類型 <xref:System.Linq.IQueryable%601> 的物件。</span><span class="sxs-lookup"><span data-stu-id="3084a-106">There are two sets of LINQ standard query operators, one that operates on objects of type <xref:System.Collections.Generic.IEnumerable%601> and the other that operates on objects of type <xref:System.Linq.IQueryable%601>.</span></span> <span data-ttu-id="3084a-107">構成每個集合的方法分別是 <xref:System.Linq.Enumerable> 和 <xref:System.Linq.Queryable> 類別的靜態成員。</span><span class="sxs-lookup"><span data-stu-id="3084a-107">The methods that make up each set are static members of the <xref:System.Linq.Enumerable> and <xref:System.Linq.Queryable> classes, respectively.</span></span> <span data-ttu-id="3084a-108">它們定義為其所運作的類型的「擴充方法」\*\*。</span><span class="sxs-lookup"><span data-stu-id="3084a-108">They are defined as *extension methods* of the type that they operate on.</span></span> <span data-ttu-id="3084a-109">這表示可以使用靜態方法語法或執行個體方法語法來呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="3084a-109">This means that they can be called by using either static method syntax or instance method syntax.</span></span>

<span data-ttu-id="3084a-110">此外，數個標準查詢運算子方法也會根據 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Linq.IQueryable%601> 之類型以外的類型運作。</span><span class="sxs-lookup"><span data-stu-id="3084a-110">In addition, several standard query operator methods operate on types other than those based on <xref:System.Collections.Generic.IEnumerable%601> or <xref:System.Linq.IQueryable%601>.</span></span> <span data-ttu-id="3084a-111"><xref:System.Linq.Enumerable> 類型定義同時在 <xref:System.Collections.IEnumerable> 類型的物件上運作的兩個這類方法。</span><span class="sxs-lookup"><span data-stu-id="3084a-111">The <xref:System.Linq.Enumerable> type defines two such methods that both operate on objects of type <xref:System.Collections.IEnumerable>.</span></span> <span data-ttu-id="3084a-112"><xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29> 和 <xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29> 這些方法可讓您查詢 LINQ 模式中的非參數化或非泛型集合。</span><span class="sxs-lookup"><span data-stu-id="3084a-112">These methods, <xref:System.Linq.Enumerable.Cast%60%601%28System.Collections.IEnumerable%29> and <xref:System.Linq.Enumerable.OfType%60%601%28System.Collections.IEnumerable%29>, let you enable a non-parameterized, or non-generic, collection to be queried in the LINQ pattern.</span></span> <span data-ttu-id="3084a-113">他們會藉由建立物件的強型別集合來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="3084a-113">They do this by creating a strongly typed collection of objects.</span></span> <span data-ttu-id="3084a-114"><xref:System.Linq.Queryable> 類別定義在 <xref:System.Linq.Queryable> 類型的物件上運作的兩個類似方法 <xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29> 和 <xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29>。</span><span class="sxs-lookup"><span data-stu-id="3084a-114">The <xref:System.Linq.Queryable> class defines two similar methods, <xref:System.Linq.Queryable.Cast%60%601%28System.Linq.IQueryable%29> and <xref:System.Linq.Queryable.OfType%60%601%28System.Linq.IQueryable%29>, that operate on objects of type <xref:System.Linq.Queryable>.</span></span>

<span data-ttu-id="3084a-115">根據傳回單一值還是一系列的值，標準查詢運算子的執行時機會不同。</span><span class="sxs-lookup"><span data-stu-id="3084a-115">The standard query operators differ in the timing of their execution, depending on whether they return a singleton value or a sequence of values.</span></span> <span data-ttu-id="3084a-116">這些傳回單一值的方法 (例如，<xref:System.Linq.Enumerable.Average%2A> 和 <xref:System.Linq.Enumerable.Sum%2A>) 就會立即執行。</span><span class="sxs-lookup"><span data-stu-id="3084a-116">Those methods that return a singleton value (for example, <xref:System.Linq.Enumerable.Average%2A> and <xref:System.Linq.Enumerable.Sum%2A>) execute immediately.</span></span> <span data-ttu-id="3084a-117">傳回序列的方法會延後執行查詢，並傳回可列舉的物件。</span><span class="sxs-lookup"><span data-stu-id="3084a-117">Methods that return a sequence defer the query execution and return an enumerable object.</span></span>

<span data-ttu-id="3084a-118">如果是運作於記憶體內部集合的方法，即擴充 <xref:System.Collections.Generic.IEnumerable%601> 的方法，則傳回的可列舉物件會擷取已傳遞給方法的引數。</span><span class="sxs-lookup"><span data-stu-id="3084a-118">In the case of the methods that operate on in-memory collections, that is, those methods that extend <xref:System.Collections.Generic.IEnumerable%601>, the returned enumerable object captures the arguments that were passed to the method.</span></span> <span data-ttu-id="3084a-119">列舉該物件時，會採用查詢運算子的邏輯，並傳回查詢結果。</span><span class="sxs-lookup"><span data-stu-id="3084a-119">When that object is enumerated, the logic of the query operator is employed and the query results are returned.</span></span>

<span data-ttu-id="3084a-120">相反地，擴充 <xref:System.Linq.IQueryable%601> 的方法不會實作任何查詢行為，但會建置代表要執行查詢的運算式樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="3084a-120">In contrast, methods that extend <xref:System.Linq.IQueryable%601> do not implement any querying behavior, but build an expression tree that represents the query to be performed.</span></span> <span data-ttu-id="3084a-121">查詢處理是由來源 <xref:System.Linq.IQueryable%601> 物件所處理。</span><span class="sxs-lookup"><span data-stu-id="3084a-121">The query processing is handled by the source <xref:System.Linq.IQueryable%601> object.</span></span>

<span data-ttu-id="3084a-122">在一個查詢中，可以將查詢方法呼叫鏈結在一起，這樣會讓查詢變得更為複雜。</span><span class="sxs-lookup"><span data-stu-id="3084a-122">Calls to query methods can be chained together in one query, which enables queries to become arbitrarily complex.</span></span>

<span data-ttu-id="3084a-123">下列程式碼範例示範如何使用標準查詢運算子來取得序列的資訊。</span><span class="sxs-lookup"><span data-stu-id="3084a-123">The following code example demonstrates how the standard query operators can be used to obtain information about a sequence.</span></span>

```vb
Dim sentence = "the quick brown fox jumps over the lazy dog"
' Split the string into individual words to create a collection.
Dim words = sentence.Split(" "c)

Dim query = From word In words
            Group word.ToUpper() By word.Length Into gr = Group
            Order By Length _
            Select Length, GroupedWords = gr

Dim output As New System.Text.StringBuilder
For Each obj In query
    output.AppendLine(String.Format("Words of length {0}:", obj.Length))
    For Each word As String In obj.GroupedWords
        output.AppendLine(word)
    Next
Next

'Display the output
MsgBox(output.ToString())

' This code example produces the following output:
'
' Words of length 3:
' THE
' FOX
' THE
' DOG
' Words of length 4:
' OVER
' LAZY
' Words of length 5:
' QUICK
' BROWN
' JUMPS
```

## <a name="query-expression-syntax"></a><span data-ttu-id="3084a-124">查詢運算式語法</span><span class="sxs-lookup"><span data-stu-id="3084a-124">Query Expression Syntax</span></span>

<span data-ttu-id="3084a-125">某些更常用的標準查詢運算子具有專用 C# 和 Visual Basic 語言關鍵字語法，可將它們呼叫為「查詢運算式」\*\* \*\* 的一部分。</span><span class="sxs-lookup"><span data-stu-id="3084a-125">Some of the more frequently used standard query operators have dedicated C# and Visual Basic language keyword syntax that enables them to be called as part of a *query* *expression*.</span></span> <span data-ttu-id="3084a-126">如需具有專用關鍵字及其對應語法之標準查詢運算子的詳細資訊，請參閱[標準查詢運算子的查詢運算式語法（Visual Basic）](query-expression-syntax-for-standard-query-operators.md)。</span><span class="sxs-lookup"><span data-stu-id="3084a-126">For more information about standard query operators that have dedicated keywords and their corresponding syntaxes, see [Query Expression Syntax for Standard Query Operators (Visual Basic)](query-expression-syntax-for-standard-query-operators.md).</span></span>

## <a name="extending-the-standard-query-operators"></a><span data-ttu-id="3084a-127">擴充標準查詢運算子</span><span class="sxs-lookup"><span data-stu-id="3084a-127">Extending the Standard Query Operators</span></span>

<span data-ttu-id="3084a-128">您可以建立適用於目標定義域或技術的定義域特定方法，來擴增一組標準查詢運算子。</span><span class="sxs-lookup"><span data-stu-id="3084a-128">You can augment the set of standard query operators by creating domain-specific methods that are appropriate for your target domain or technology.</span></span> <span data-ttu-id="3084a-129">您也可以將標準查詢運算子取代為提供額外服務的專屬實作，例如遠端評估、查詢轉譯和最佳化。</span><span class="sxs-lookup"><span data-stu-id="3084a-129">You can also replace the standard query operators with your own implementations that provide additional services such as remote evaluation, query translation, and optimization.</span></span> <span data-ttu-id="3084a-130">如需範例，請參閱 <xref:System.Linq.Enumerable.AsEnumerable%2A>。</span><span class="sxs-lookup"><span data-stu-id="3084a-130">See <xref:System.Linq.Enumerable.AsEnumerable%2A> for an example.</span></span>

## <a name="related-sections"></a><span data-ttu-id="3084a-131">相關章節</span><span class="sxs-lookup"><span data-stu-id="3084a-131">Related Sections</span></span>

<span data-ttu-id="3084a-132">下列連結會將您帶到根據功能而提供各種標準查詢運算子的其他資訊的主題。</span><span class="sxs-lookup"><span data-stu-id="3084a-132">The following links take you to topics that provide additional information about the various standard query operators based on functionality.</span></span>

- [<span data-ttu-id="3084a-133">排序資料</span><span class="sxs-lookup"><span data-stu-id="3084a-133">Sorting Data</span></span>](sorting-data.md)

- [<span data-ttu-id="3084a-134">設定作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-134">Set Operations (Visual Basic)</span></span>](set-operations.md)

- [<span data-ttu-id="3084a-135">篩選資料（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-135">Filtering Data (Visual Basic)</span></span>](filtering-data.md)

- [<span data-ttu-id="3084a-136">數量詞作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-136">Quantifier Operations (Visual Basic)</span></span>](quantifier-operations.md)

- [<span data-ttu-id="3084a-137">投射作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-137">Projection Operations (Visual Basic)</span></span>](projection-operations.md)

- [<span data-ttu-id="3084a-138">分割資料（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-138">Partitioning Data (Visual Basic)</span></span>](partitioning-data.md)

- [<span data-ttu-id="3084a-139">聯結作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-139">Join Operations (Visual Basic)</span></span>](join-operations.md)

- [<span data-ttu-id="3084a-140">群組資料（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-140">Grouping Data (Visual Basic)</span></span>](grouping-data.md)

- [<span data-ttu-id="3084a-141">產生作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-141">Generation Operations (Visual Basic)</span></span>](generation-operations.md)

- [<span data-ttu-id="3084a-142">等號比較運算（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-142">Equality Operations (Visual Basic)</span></span>](equality-operations.md)

- [<span data-ttu-id="3084a-143">元素作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-143">Element Operations (Visual Basic)</span></span>](element-operations.md)

- [<span data-ttu-id="3084a-144">轉換資料類型（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-144">Converting Data Types (Visual Basic)</span></span>](converting-data-types.md)

- [<span data-ttu-id="3084a-145">串連作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-145">Concatenation Operations (Visual Basic)</span></span>](concatenation-operations.md)

- [<span data-ttu-id="3084a-146">匯總作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-146">Aggregation Operations (Visual Basic)</span></span>](aggregation-operations.md)

## <a name="see-also"></a><span data-ttu-id="3084a-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3084a-147">See also</span></span>

- <xref:System.Linq.Enumerable>
- <xref:System.Linq.Queryable>
- [<span data-ttu-id="3084a-148">LINQ 簡介 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="3084a-148">Introduction to LINQ (Visual Basic)</span></span>](introduction-to-linq.md)
- [<span data-ttu-id="3084a-149">標準查詢運算子的查詢運算式語法（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-149">Query Expression Syntax for Standard Query Operators (Visual Basic)</span></span>](query-expression-syntax-for-standard-query-operators.md)
- [<span data-ttu-id="3084a-150">依執行方式分類標準查詢運算子（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="3084a-150">Classification of Standard Query Operators by Manner of Execution (Visual Basic)</span></span>](classification-of-standard-query-operators-by-manner-of-execution.md)
- [<span data-ttu-id="3084a-151">擴充方法</span><span class="sxs-lookup"><span data-stu-id="3084a-151">Extension Methods</span></span>](../../language-features/procedures/extension-methods.md)
