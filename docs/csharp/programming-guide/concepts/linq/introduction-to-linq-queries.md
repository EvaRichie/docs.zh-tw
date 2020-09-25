---
title: LINQ 查詢簡介 (C#)
description: LINQ 提供一致的模型，讓您查詢各種資料來源和格式的資料。 在 LINQ 查詢中，您永遠都是使用物件。
ms.date: 07/20/2015
helpviewer_keywords:
- deferred execution [LINQ]
- LINQ, queries
- LINQ, deferred execution
- queries [LINQ], about LINQ queries
ms.assetid: 37895c02-268c-41d5-be39-f7d936fa88a8
ms.openlocfilehash: f81c3f4e355215f1a750a764c617ad47430adc31
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91170567"
---
# <a name="introduction-to-linq-queries-c"></a><span data-ttu-id="3bf3e-104">LINQ 查詢簡介 (C#)</span><span class="sxs-lookup"><span data-stu-id="3bf3e-104">Introduction to LINQ Queries (C#)</span></span>

<span data-ttu-id="3bf3e-105">「查詢」\*\* 是指從資料來源中擷取資料的運算式。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-105">A *query* is an expression that retrieves data from a data source.</span></span> <span data-ttu-id="3bf3e-106">查詢通常以特定的查詢語言來表示。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-106">Queries are usually expressed in a specialized query language.</span></span> <span data-ttu-id="3bf3e-107">針對各種資料來源類型開發不同的語言已有一段時間，例如用於關聯式資料庫的 SQL，以及用於 XML 的 XQuery。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-107">Different languages have been developed over time for the various types of data sources, for example SQL for relational databases and XQuery for XML.</span></span> <span data-ttu-id="3bf3e-108">因此，開發人員在過去必須針對所需支援的每種資料來源類型或資料格式，學習新的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-108">Therefore, developers have had to learn a new query language for each type of data source or data format that they must support.</span></span> <span data-ttu-id="3bf3e-109">LINQ 藉由提供一致的模型來處理各種資料來源和格式的資料，來簡化這種情況。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-109">LINQ simplifies this situation by offering a consistent model for working with data across various kinds of data sources and formats.</span></span> <span data-ttu-id="3bf3e-110">在 LINQ 查詢中，您永遠都是使用物件。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-110">In a LINQ query, you are always working with objects.</span></span> <span data-ttu-id="3bf3e-111">您可以使用相同的基本程式碼撰寫模式來查詢及轉換 XML 檔、SQL 資料庫、ADO.NET 資料集、.NET 集合，以及可使用 LINQ 提供者的任何其他格式的資料。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-111">You use the same basic coding patterns to query and transform data in XML documents, SQL databases, ADO.NET Datasets, .NET collections, and any other format for which a LINQ provider is available.</span></span>  
  
## <a name="three-parts-of-a-query-operation"></a><span data-ttu-id="3bf3e-112">查詢作業的三個部分</span><span class="sxs-lookup"><span data-stu-id="3bf3e-112">Three Parts of a Query Operation</span></span>  

 <span data-ttu-id="3bf3e-113">所有 LINQ 查詢作業都包含三個不同的動作：</span><span class="sxs-lookup"><span data-stu-id="3bf3e-113">All LINQ query operations consist of three distinct actions:</span></span>  
  
1. <span data-ttu-id="3bf3e-114">取得資料來源。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-114">Obtain the data source.</span></span>  
  
2. <span data-ttu-id="3bf3e-115">建立查詢。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-115">Create the query.</span></span>  
  
3. <span data-ttu-id="3bf3e-116">執行查詢。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-116">Execute the query.</span></span>  
  
 <span data-ttu-id="3bf3e-117">下列範例示範查詢作業的三個部分在原始程式碼中的表示方式。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-117">The following example shows how the three parts of a query operation are expressed in source code.</span></span> <span data-ttu-id="3bf3e-118">為了方便起見，此範例使用整數陣列作為資料來源；不過，相同的概念也適用於其他資料來源。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-118">The example uses an integer array as a data source for convenience; however, the same concepts apply to other data sources also.</span></span> <span data-ttu-id="3bf3e-119">本主題的其他部分都會參考此範例。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-119">This example is referred to throughout the rest of this topic.</span></span>  
  
 [!code-csharp[CsLINQGettingStarted#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#1)]  
  
 <span data-ttu-id="3bf3e-120">下圖顯示完整的查詢作業。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-120">The following illustration shows the complete query operation.</span></span> <span data-ttu-id="3bf3e-121">在 LINQ 中，查詢的執行與查詢本身不同。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-121">In LINQ, the execution of the query is distinct from the query itself.</span></span> <span data-ttu-id="3bf3e-122">換句話說，您不只是藉由建立查詢變數來取出任何資料。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-122">In other words, you have not retrieved any data just by creating a query variable.</span></span>  
  
 ![完整 LINQ 查詢作業的圖表。](./media/introduction-to-linq-queries/linq-query-complete-operation.png)  
  
## <a name="the-data-source"></a><span data-ttu-id="3bf3e-124">資料來源</span><span class="sxs-lookup"><span data-stu-id="3bf3e-124">The Data Source</span></span>  

 <span data-ttu-id="3bf3e-125">在上述範例中，因為資料來源來自陣列，意味著其也支援泛型 <xref:System.Collections.Generic.IEnumerable%601> 介面。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-125">In the previous example, because the data source is an array, it implicitly supports the generic <xref:System.Collections.Generic.IEnumerable%601> interface.</span></span> <span data-ttu-id="3bf3e-126">這表示可以使用 LINQ 進行查詢。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-126">This fact means it can be queried with LINQ.</span></span> <span data-ttu-id="3bf3e-127">查詢會在 `foreach` 陳述式中執行，而 `foreach` 則需要<xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-127">A query is executed in a `foreach` statement, and `foreach` requires <xref:System.Collections.IEnumerable> or <xref:System.Collections.Generic.IEnumerable%601>.</span></span> <span data-ttu-id="3bf3e-128">支援 <xref:System.Collections.Generic.IEnumerable%601> 或衍生介面的類型，例如泛型 <xref:System.Linq.IQueryable%601> 稱為*可查詢的類型*。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-128">Types that support <xref:System.Collections.Generic.IEnumerable%601> or a derived interface such as the generic <xref:System.Linq.IQueryable%601> are called *queryable types*.</span></span>  
  
 <span data-ttu-id="3bf3e-129">可查詢的型別不需要修改或特殊處理來作為 LINQ 資料來源。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-129">A queryable type requires no modification or special treatment to serve as a LINQ data source.</span></span> <span data-ttu-id="3bf3e-130">如果來源資料不是以可查詢型別的形式存在於記憶體中，LINQ 提供者必須將它表示為。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-130">If the source data is not already in memory as a queryable type, the LINQ provider must represent it as such.</span></span> <span data-ttu-id="3bf3e-131">例如 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會將 XML 文件載入可查詢的 <xref:System.Xml.Linq.XElement> 類型：</span><span class="sxs-lookup"><span data-stu-id="3bf3e-131">For example, [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] loads an XML document into a queryable <xref:System.Xml.Linq.XElement> type:</span></span>  
  
 [!code-csharp[CsLINQGettingStarted#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#2)]  
  
 <span data-ttu-id="3bf3e-132">在中 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] ，您會先以手動方式或使用 [Visual Studio 中的 LINQ to SQL 工具](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)，在設計階段建立物件關聯式對應。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-132">With [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)], you first create an object-relational mapping at design time either manually or by using the [LINQ to SQL Tools in Visual Studio](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2).</span></span> <span data-ttu-id="3bf3e-133">您可以針對物件撰寫查詢，而 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 則會在執行階段處理與資料庫之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-133">You write your queries against the objects, and at run-time [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] handles the communication with the database.</span></span> <span data-ttu-id="3bf3e-134">在下列範例中，`Customers` 代表資料庫中特定的資料表，而查詢結果 <xref:System.Linq.IQueryable%601> 的類型則衍生自 <xref:System.Collections.Generic.IEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-134">In the following example, `Customers` represents a specific table in the database, and the type of the query result, <xref:System.Linq.IQueryable%601>, derives from <xref:System.Collections.Generic.IEnumerable%601>.</span></span>  
  
```csharp  
Northwnd db = new Northwnd(@"c:\northwnd.mdf");  
  
// Query for customers in London.  
IQueryable<Customer> custQuery =  
    from cust in db.Customers  
    where cust.City == "London"  
    select cust;  
```  
  
 <span data-ttu-id="3bf3e-135">如需有關如何建立特定資料來源類型的詳細資訊，請參閱各種 LINQ 提供者的檔。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-135">For more information about how to create specific types of data sources, see the documentation for the various LINQ providers.</span></span> <span data-ttu-id="3bf3e-136">不過，基本規則非常簡單： LINQ 資料來源是支援泛型介面的任何物件 <xref:System.Collections.Generic.IEnumerable%601> ，或是繼承自它的介面。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-136">However, the basic rule is very simple: a LINQ data source is any object that supports the generic <xref:System.Collections.Generic.IEnumerable%601> interface, or an interface that inherits from it.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3bf3e-137"><xref:System.Collections.ArrayList>支援非泛型介面的類型 <xref:System.Collections.IEnumerable> 也可以當做 LINQ 資料來源使用。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-137">Types such as <xref:System.Collections.ArrayList> that support the non-generic <xref:System.Collections.IEnumerable> interface can also be used as a LINQ data source.</span></span> <span data-ttu-id="3bf3e-138">如需詳細資訊，請參閱 [如何使用 LINQ (c # ) 查詢 ArrayList ](./how-to-query-an-arraylist-with-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-138">For more information, see [How to query an ArrayList with LINQ (C#)](./how-to-query-an-arraylist-with-linq.md).</span></span>  
  
## <a name="the-query"></a><a name="query"></a> <span data-ttu-id="3bf3e-139">查詢</span><span class="sxs-lookup"><span data-stu-id="3bf3e-139">The Query</span></span>  

 <span data-ttu-id="3bf3e-140">查詢可指定要從一或多個資料來源擷取的資訊。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-140">The query specifies what information to retrieve from the data source or sources.</span></span> <span data-ttu-id="3bf3e-141">查詢也可選擇性地指定該項資訊傳回之前應該如何排序、分組和成形。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-141">Optionally, a query also specifies how that information should be sorted, grouped, and shaped before it is returned.</span></span> <span data-ttu-id="3bf3e-142">查詢是儲存在查詢變數中，並以查詢運算式初始化。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-142">A query is stored in a query variable and initialized with a query expression.</span></span> <span data-ttu-id="3bf3e-143">為了簡化撰寫查詢的作業，C# 已引進新的查詢語法。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-143">To make it easier to write queries, C# has introduced new query syntax.</span></span>  
  
 <span data-ttu-id="3bf3e-144">上述範例中的查詢會傳回整數陣列中的所有偶數。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-144">The query in the previous example returns all the even numbers from the integer array.</span></span> <span data-ttu-id="3bf3e-145">此查詢運算式包含三個子句︰`from`、`where` 和 `select`</span><span class="sxs-lookup"><span data-stu-id="3bf3e-145">The query expression contains three clauses: `from`, `where` and `select`.</span></span> <span data-ttu-id="3bf3e-146"> (如果您熟悉 SQL，您將會注意到子句的順序與 SQL 中的順序相反。 ) `from` 子句會指定資料來源， `where` 子句會套用篩選，而且子句會指定傳回專案的型別 `select` 。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-146">(If you are familiar with SQL, you will have noticed that the ordering of the clauses is reversed from the order in SQL.) The `from` clause specifies the data source, the `where` clause applies the filter, and the `select` clause specifies the type of the returned elements.</span></span> <span data-ttu-id="3bf3e-147">[ (LINQ) ](../../../linq/index.md)一節的語言整合式查詢中會詳細討論這些和其他查詢子句。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-147">These and the other query clauses are discussed in detail in the [Language Integrated Query (LINQ)](../../../linq/index.md) section.</span></span> <span data-ttu-id="3bf3e-148">目前，重點是在 LINQ 中，查詢變數本身不會採取任何動作，也不會傳回任何資料。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-148">For now, the important point is that in LINQ, the query variable itself takes no action and returns no data.</span></span> <span data-ttu-id="3bf3e-149">它只會儲存稍後執行查詢以產生結果時所需要的資訊。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-149">It just stores the information that is required to produce the results when the query is executed at some later point.</span></span> <span data-ttu-id="3bf3e-150">如需如何在幕後建構查詢的詳細資訊，請參閱[標準查詢運算子概觀 (C#)](./standard-query-operators-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-150">For more information about how queries are constructed behind the scenes, see [Standard Query Operators Overview (C#)](./standard-query-operators-overview.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3bf3e-151">查詢也可以使用方法語法來表示。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-151">Queries can also be expressed by using method syntax.</span></span> <span data-ttu-id="3bf3e-152">如需詳細資訊，請參閱 [LINQ 中的查詢語法及方法語法](./query-syntax-and-method-syntax-in-linq.md)。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-152">For more information, see [Query Syntax and Method Syntax in LINQ](./query-syntax-and-method-syntax-in-linq.md).</span></span>  
  
## <a name="query-execution"></a><span data-ttu-id="3bf3e-153">查詢執行</span><span class="sxs-lookup"><span data-stu-id="3bf3e-153">Query Execution</span></span>  
  
### <a name="deferred-execution"></a><span data-ttu-id="3bf3e-154">延後執行</span><span class="sxs-lookup"><span data-stu-id="3bf3e-154">Deferred Execution</span></span>  

 <span data-ttu-id="3bf3e-155">如前所述，查詢變數本身只會儲存查詢命令。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-155">As stated previously, the query variable itself only stores the query commands.</span></span> <span data-ttu-id="3bf3e-156">查詢的實際執行必須等到您逐一查看 `foreach` 陳述式中的查詢變數之後才會進行。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-156">The actual execution of the query is deferred until you iterate over the query variable in a `foreach` statement.</span></span> <span data-ttu-id="3bf3e-157">此概念稱為「延後執行」\*\*，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3bf3e-157">This concept is referred to as *deferred execution* and is demonstrated in the following example:</span></span>  
  
 [!code-csharp[csLinqGettingStarted#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#4)]  
  
 <span data-ttu-id="3bf3e-158">`foreach` 陳述式也是擷取查詢結果的位置。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-158">The `foreach` statement is also where the query results are retrieved.</span></span> <span data-ttu-id="3bf3e-159">例如，在上述查詢中，反覆運算變數 `num` 會保留傳回序列中的每個值 (一次一個)。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-159">For example, in the previous query, the iteration variable `num` holds each value (one at a time) in the returned sequence.</span></span>  
  
 <span data-ttu-id="3bf3e-160">因為查詢變數本身絕不會保留查詢結果，所以您可以視需要多次執行。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-160">Because the query variable itself never holds the query results, you can execute it as often as you like.</span></span> <span data-ttu-id="3bf3e-161">例如，您可以擁有會由個別應用程式持續更新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-161">For example, you may have a database that is being updated continually by a separate application.</span></span> <span data-ttu-id="3bf3e-162">您可以在應用程式中建立一個擷取最新資料的查詢，然後依特定時間間隔反覆執行，每次擷取不同的結果。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-162">In your application, you could create one query that retrieves the latest data, and you could execute it repeatedly at some interval to retrieve different results every time.</span></span>  
  
### <a name="forcing-immediate-execution"></a><span data-ttu-id="3bf3e-163">強制立即執行</span><span class="sxs-lookup"><span data-stu-id="3bf3e-163">Forcing Immediate Execution</span></span>  

 <span data-ttu-id="3bf3e-164">針對某個來源項目範圍執行彙總函式的查詢必須先逐一查看這些項目。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-164">Queries that perform aggregation functions over a range of source elements must first iterate over those elements.</span></span> <span data-ttu-id="3bf3e-165">這類查詢的範例包括 `Count`、`Max`、`Average` 和 `First`。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-165">Examples of such queries are `Count`, `Max`, `Average`, and `First`.</span></span> <span data-ttu-id="3bf3e-166">這些查詢執行時並未使用明確的 `foreach` 陳述式，因為查詢本身必須使用 `foreach` 才能傳回結果。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-166">These execute without an explicit `foreach` statement because the query itself must use `foreach` in order to return a result.</span></span> <span data-ttu-id="3bf3e-167">另外也請注意，這些查詢類型傳回的是單一的值，而不是 `IEnumerable` 集合。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-167">Note also that these types of queries return a single value, not an `IEnumerable` collection.</span></span> <span data-ttu-id="3bf3e-168">下列查詢會傳回來源陣列中的偶數計數：</span><span class="sxs-lookup"><span data-stu-id="3bf3e-168">The following query returns a count of the even numbers in the source array:</span></span>  
  
 [!code-csharp[csLinqGettingStarted#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#5)]  
  
 <span data-ttu-id="3bf3e-169">若要立即強制執行任何查詢，並快取其結果，可以呼叫 <xref:System.Linq.Enumerable.ToList%2A> 或 <xref:System.Linq.Enumerable.ToArray%2A>方法。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-169">To force immediate execution of any query and cache its results, you can call the <xref:System.Linq.Enumerable.ToList%2A> or <xref:System.Linq.Enumerable.ToArray%2A> methods.</span></span>  
  
 [!code-csharp[csLinqGettingStarted#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#6)]  
  
 <span data-ttu-id="3bf3e-170">您也可以將 `foreach` 迴圈放在緊接著查詢運算式後方的位置，以強制執行查詢。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-170">You can also force execution by putting the `foreach` loop immediately after the query expression.</span></span> <span data-ttu-id="3bf3e-171">不過，藉由呼叫 `ToList` 或 `ToArray`，您也可以快取單一集合物件中的所有資料。</span><span class="sxs-lookup"><span data-stu-id="3bf3e-171">However, by calling `ToList` or `ToArray` you also cache all the data in a single collection object.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3bf3e-172">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3bf3e-172">See also</span></span>

- [<span data-ttu-id="3bf3e-173">開始使用 C# 中的 LINQ</span><span class="sxs-lookup"><span data-stu-id="3bf3e-173">Getting Started with LINQ in C#</span></span>](index.md)
- [<span data-ttu-id="3bf3e-174">逐步解說：在 C# 中撰寫查詢</span><span class="sxs-lookup"><span data-stu-id="3bf3e-174">Walkthrough: Writing Queries in C#</span></span>](./walkthrough-writing-queries-linq.md)
- [<span data-ttu-id="3bf3e-175">Language Integrated Query (LINQ)</span><span class="sxs-lookup"><span data-stu-id="3bf3e-175">Language Integrated Query (LINQ)</span></span>](../../../linq/index.md)
- [<span data-ttu-id="3bf3e-176">foreach、in</span><span class="sxs-lookup"><span data-stu-id="3bf3e-176">foreach, in</span></span>](../../../language-reference/keywords/foreach-in.md)
- [<span data-ttu-id="3bf3e-177">LINQ)  (查詢關鍵字 </span><span class="sxs-lookup"><span data-stu-id="3bf3e-177">Query Keywords (LINQ)</span></span>](../../../language-reference/keywords/query-keywords.md)
