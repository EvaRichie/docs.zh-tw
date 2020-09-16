---
title: 已編譯查詢 (LINQ to Entities)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8025ba1d-29c7-4407-841b-d5a3bed40b7a
ms.openlocfilehash: f3270147f0cf38a646efac603f058173daa78547
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90541131"
---
# <a name="compiled-queries--linq-to-entities"></a><span data-ttu-id="ae725-102">編譯的查詢 (LINQ to Entities) </span><span class="sxs-lookup"><span data-stu-id="ae725-102">Compiled queries  (LINQ to Entities)</span></span>

<span data-ttu-id="ae725-103">當您的應用程式執行了 Entity Framework 中結構類似的查詢多次時，您可經常增加效能，其方式是編譯查詢一次，然後使用不同的參數執行查詢多次。</span><span class="sxs-lookup"><span data-stu-id="ae725-103">When you have an application that executes structurally similar queries many times in the Entity Framework, you can frequently increase performance by compiling the query one time and executing it several times with different parameters.</span></span> <span data-ttu-id="ae725-104">例如，應用程式可能必須擷取特定城市中的所有客戶；此城市是使用者在執行階段於表單中所指定。</span><span class="sxs-lookup"><span data-stu-id="ae725-104">For example, an application might have to retrieve all the customers in a particular city; the city is specified at runtime by the user in a form.</span></span> <span data-ttu-id="ae725-105">LINQ to Entities 支援針對這個用途所編譯的查詢。</span><span class="sxs-lookup"><span data-stu-id="ae725-105">LINQ to Entities supports using compiled queries for this purpose.</span></span>  
  
 <span data-ttu-id="ae725-106">從 .NET Framework 4.5 開始，會自動快取 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="ae725-106">Starting with .NET Framework 4.5, LINQ queries are cached automatically.</span></span> <span data-ttu-id="ae725-107">不過，之後執行時您仍可以使用已編譯的 LINQ 查詢減少這種成本，且已編譯查詢可能比自動快取的 LINQ 查詢更有效率。</span><span class="sxs-lookup"><span data-stu-id="ae725-107">However, you can still use compiled LINQ queries to reduce this cost in later executions and compiled queries can be more efficient than LINQ queries that are automatically cached.</span></span> <span data-ttu-id="ae725-108">`Enumerable.Contains`不會自動快取將運算子套用至記憶體中集合的 LINQ to Entities 查詢。</span><span class="sxs-lookup"><span data-stu-id="ae725-108">LINQ to Entities queries that apply the `Enumerable.Contains` operator to in-memory collections are not automatically cached.</span></span> <span data-ttu-id="ae725-109">此外，也不允許在編譯的 LINQ 查詢中，將記憶體中的集合參數化。</span><span class="sxs-lookup"><span data-stu-id="ae725-109">Also, parameterizing in-memory collections in compiled LINQ queries is not allowed.</span></span>  
  
 <span data-ttu-id="ae725-110"><xref:System.Data.Objects.CompiledQuery> 類別提供查詢的編譯和快取以供重複使用。</span><span class="sxs-lookup"><span data-stu-id="ae725-110">The <xref:System.Data.Objects.CompiledQuery> class provides compilation and caching of queries for reuse.</span></span> <span data-ttu-id="ae725-111">就概念而言，這個類別包含數個多載之 <xref:System.Data.Objects.CompiledQuery> 的 `Compile` 方法。</span><span class="sxs-lookup"><span data-stu-id="ae725-111">Conceptually, this class contains a <xref:System.Data.Objects.CompiledQuery>'s `Compile` method with several overloads.</span></span> <span data-ttu-id="ae725-112">呼叫 `Compile` 方法可建立新委派來代表已編譯的查詢。</span><span class="sxs-lookup"><span data-stu-id="ae725-112">Call the `Compile` method to create a new delegate to represent the compiled query.</span></span> <span data-ttu-id="ae725-113">`Compile` 所提供的 <xref:System.Data.Objects.ObjectContext> 方法和參數值會傳回一個產生某個結果 (例如 <xref:System.Linq.IQueryable%601> 執行個體) 的委派。</span><span class="sxs-lookup"><span data-stu-id="ae725-113">The `Compile` methods, provided with a <xref:System.Data.Objects.ObjectContext> and parameter values, return a delegate that produces some result (such as an <xref:System.Linq.IQueryable%601> instance).</span></span> <span data-ttu-id="ae725-114">此查詢只會在第一次執行期間編譯一次。</span><span class="sxs-lookup"><span data-stu-id="ae725-114">The query compiles once during only the first execution.</span></span> <span data-ttu-id="ae725-115">不過，您之後無法變更在編譯階段中，針對查詢所設定的合併選項。</span><span class="sxs-lookup"><span data-stu-id="ae725-115">The merge options set for the query at the time of the compilation cannot be changed later.</span></span> <span data-ttu-id="ae725-116">一旦編譯查詢之後，您就只能提供基本類型的參數，但您無法取代會變更產生之 SQL 的查詢部分。</span><span class="sxs-lookup"><span data-stu-id="ae725-116">Once the query is compiled, you can only supply parameters of primitive type but you cannot replace parts of the query that would change the generated SQL.</span></span> <span data-ttu-id="ae725-117">如需詳細資訊，請參閱 [EF Merge 選項和編譯的查詢](/archive/blogs/dsimmons/ef-merge-options-and-compiled-queries)。</span><span class="sxs-lookup"><span data-stu-id="ae725-117">For more information, see [EF Merge Options and Compiled Queries](/archive/blogs/dsimmons/ef-merge-options-and-compiled-queries).</span></span>
  
 <span data-ttu-id="ae725-118">的方法所編譯的 LINQ to Entities 查詢運算式 <xref:System.Data.Objects.CompiledQuery> `Compile` 是由其中一個泛型 `Func` 委派（例如）表示 <xref:System.Func%605> 。</span><span class="sxs-lookup"><span data-stu-id="ae725-118">The LINQ to Entities query expression that the <xref:System.Data.Objects.CompiledQuery>'s `Compile` method compiles is represented by one of the generic `Func` delegates, such as <xref:System.Func%605>.</span></span> <span data-ttu-id="ae725-119">查詢運算式最多只能封裝一個 `ObjectContext` 參數、一個傳回參數和十六個查詢參數。</span><span class="sxs-lookup"><span data-stu-id="ae725-119">At most, the query expression can encapsulate an `ObjectContext` parameter, a return parameter, and 16 query parameters.</span></span> <span data-ttu-id="ae725-120">如果需要使用十六個以上的查詢參數，您可以建立其屬性代表查詢參數的結構。</span><span class="sxs-lookup"><span data-stu-id="ae725-120">If more than 16 query parameters are required, you can create a structure whose properties represent query parameters.</span></span> <span data-ttu-id="ae725-121">然後，當您設定這些參數之後，就可以將此結構的屬性用於查詢運算式中。</span><span class="sxs-lookup"><span data-stu-id="ae725-121">You can then use the properties on the structure in the query expression after you set the properties.</span></span>  
  
## <a name="example-1"></a><span data-ttu-id="ae725-122">範例 1</span><span class="sxs-lookup"><span data-stu-id="ae725-122">Example 1</span></span>  
 <span data-ttu-id="ae725-123">下列範例會先編譯然後再叫用接受 <xref:System.Decimal> 輸入參數的查詢，並且傳回訂單序列，其中的總到期金額大於或等於 $200.00：</span><span class="sxs-lookup"><span data-stu-id="ae725-123">The following example compiles and then invokes a query that accepts a <xref:System.Decimal> input parameter and returns a sequence of orders where the total due is greater than or equal to $200.00:</span></span>  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query 2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery2)]
 [!code-vb[DP L2E Conceptual Examples - compiled query2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery2)]  
  
## <a name="example-2"></a><span data-ttu-id="ae725-124">範例 2</span><span class="sxs-lookup"><span data-stu-id="ae725-124">Example 2</span></span>  
 <span data-ttu-id="ae725-125">下列範例會先編譯再叫用傳回 <xref:System.Data.Objects.ObjectQuery%601> 執行個體的查詢：</span><span class="sxs-lookup"><span data-stu-id="ae725-125">The following example compiles and then invokes a query that returns an <xref:System.Data.Objects.ObjectQuery%601> instance:</span></span>  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query1_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery1_mq)]
 [!code-vb[DP L2E Conceptual Examples - compiled query1_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery1_mq)]  
  
## <a name="example-3"></a><span data-ttu-id="ae725-126">範例 3</span><span class="sxs-lookup"><span data-stu-id="ae725-126">Example 3</span></span>  
 <span data-ttu-id="ae725-127">下列範例會先編譯再叫用一個查詢，此查詢會以 <xref:System.Decimal> 值形式傳回產品標價的平均值。</span><span class="sxs-lookup"><span data-stu-id="ae725-127">The following example compiles and then invokes a query that returns the average of the product list prices as a <xref:System.Decimal> value:</span></span>  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery3_mq)]
 [!code-vb[DP L2E Conceptual Examples - compiled query3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery3_mq)]  
  
## <a name="example-4"></a><span data-ttu-id="ae725-128">範例 4</span><span class="sxs-lookup"><span data-stu-id="ae725-128">Example 4</span></span>  
 <span data-ttu-id="ae725-129">下列範例會先編譯然後再叫用接受輸入參數的查詢，然後傳回 <xref:System.String> `Contact` 其電子郵件地址開頭為指定字串的：</span><span class="sxs-lookup"><span data-stu-id="ae725-129">The following example compiles and then invokes a query that accepts a <xref:System.String> input parameter and then returns a `Contact` whose email address starts with the specified string:</span></span>  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query4_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery4_mq)]
 [!code-vb[DP L2E Conceptual Examples - compiled query4_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery4_mq)]  
  
## <a name="example-5"></a><span data-ttu-id="ae725-130">範例 5</span><span class="sxs-lookup"><span data-stu-id="ae725-130">Example 5</span></span>  
 <span data-ttu-id="ae725-131">下列範例會先編譯然後再叫用接受 <xref:System.DateTime> 和 <xref:System.Decimal> 輸入參數的查詢，並且傳回訂單序列，其中的訂單日期晚於 2003 年 3 月 8 日，總應付金額則少於 $300.00：</span><span class="sxs-lookup"><span data-stu-id="ae725-131">The following example compiles and then invokes a query that accepts <xref:System.DateTime> and <xref:System.Decimal> input parameters and returns a sequence of orders where the order date is later than March 8, 2003, and the total due is less than $300.00:</span></span>  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery5)]
 [!code-vb[DP L2E Conceptual Examples - compiled query5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery5)]  
  
## <a name="example-6"></a><span data-ttu-id="ae725-132">範例 6</span><span class="sxs-lookup"><span data-stu-id="ae725-132">Example 6</span></span>  
 <span data-ttu-id="ae725-133">下列範例會先編譯然後再叫用接受 <xref:System.DateTime> 輸入參數的查詢，並且傳回訂單序列，其中的訂單日期晚於 2004 年 3 月 8 日。</span><span class="sxs-lookup"><span data-stu-id="ae725-133">The following example compiles and then invokes a query that accepts a <xref:System.DateTime> input parameter and returns a sequence of orders where the order date is later than March 8, 2004.</span></span> <span data-ttu-id="ae725-134">此查詢會傳回匿名型別序列形式的訂單資訊。</span><span class="sxs-lookup"><span data-stu-id="ae725-134">This query returns the order information as a sequence of anonymous types.</span></span> <span data-ttu-id="ae725-135">匿名型別是由編譯器所推斷，所以您無法在 <xref:System.Data.Objects.CompiledQuery> 的 `Compile` 方法中指定型別參數，而且此型別會在查詢本身定義。</span><span class="sxs-lookup"><span data-stu-id="ae725-135">Anonymous types are inferred by the compiler, so you cannot specify type parameters in the <xref:System.Data.Objects.CompiledQuery>'s `Compile` method and the type is defined in the query itself.</span></span>  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery6)]
 [!code-vb[DP L2E Conceptual Examples - compiled query6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery6)]  
  
## <a name="example-7"></a><span data-ttu-id="ae725-136">範例 7</span><span class="sxs-lookup"><span data-stu-id="ae725-136">Example 7</span></span>  
 <span data-ttu-id="ae725-137">下列範例會先編譯然後再叫用接受使用者定義結構輸入參數的查詢，並且傳回訂單序列。</span><span class="sxs-lookup"><span data-stu-id="ae725-137">The following example compiles and then invokes a query that accepts a user-defined structure input parameter and returns a sequence of orders.</span></span> <span data-ttu-id="ae725-138">此結構會定義開始日期、結束日期和應付總額查詢參數，而且此查詢會傳回在 2003 年 3 月 3 日與 3 月 8 日之間出貨而且應付總額超過 $700.00 的訂單。</span><span class="sxs-lookup"><span data-stu-id="ae725-138">The structure defines start date, end date, and total due query parameters, and the query returns orders shipped between March 3 and March 8, 2003 with a total due greater than $700.00.</span></span>  
  
 [!code-csharp[DP L2E Conceptual Examples - compiled query7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#compiledquery7)]
 [!code-vb[DP L2E Conceptual Examples - compiled query7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#compiledquery7)]  
  
 <span data-ttu-id="ae725-139">定義查詢參數的結構：</span><span class="sxs-lookup"><span data-stu-id="ae725-139">The structure that defines the query parameters:</span></span>  
  
 [!code-csharp[DP L2E Conceptual Examples - MyParamsStruct](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#myparamsstruct)]
 [!code-vb[DP L2E Conceptual Examples - MyParamsStruct](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#myparamsstruct)]  
  
## <a name="see-also"></a><span data-ttu-id="ae725-140">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ae725-140">See also</span></span>

- [<span data-ttu-id="ae725-141">ADO.NET Entity Framework</span><span class="sxs-lookup"><span data-stu-id="ae725-141">ADO.NET Entity Framework</span></span>](../index.md)
- [<span data-ttu-id="ae725-142">LINQ to Entities</span><span class="sxs-lookup"><span data-stu-id="ae725-142">LINQ to Entities</span></span>](linq-to-entities.md)
- [<span data-ttu-id="ae725-143">EF 合併選項和編譯的查詢</span><span class="sxs-lookup"><span data-stu-id="ae725-143">EF Merge Options and Compiled Queries</span></span>](/archive/blogs/dsimmons/ef-merge-options-and-compiled-queries)
