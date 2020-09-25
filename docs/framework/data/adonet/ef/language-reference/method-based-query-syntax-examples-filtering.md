---
title: 以方法為基礎的查詢語法範例：篩選
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e40e314c-eb30-4f44-a054-41e511e35832
ms.openlocfilehash: 392181f201c7b18b1b38f62f5f35c5657cbbe601
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91191992"
---
# <a name="method-based-query-syntax-examples-filtering"></a><span data-ttu-id="12376-102">以方法為基礎的查詢語法範例：篩選</span><span class="sxs-lookup"><span data-stu-id="12376-102">Method-Based Query Syntax Examples: Filtering</span></span>

<span data-ttu-id="12376-103">本主題中的範例將示範如何使用 `Where` 和 `Where…Contains` 方法，利用以方法為基礎的查詢語法來查詢 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 。</span><span class="sxs-lookup"><span data-stu-id="12376-103">The examples in this topic demonstrate how to use the `Where` and `Where…Contains` methods to query the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) using method-based query syntax.</span></span> <span data-ttu-id="12376-104">請注意，其中 .。。`Contains`</span><span class="sxs-lookup"><span data-stu-id="12376-104">Note, Where…`Contains`</span></span> <span data-ttu-id="12376-105">無法當做 [已編譯查詢](compiled-queries-linq-to-entities.md)的一部分使用。</span><span class="sxs-lookup"><span data-stu-id="12376-105">cannot be used as a part of a [compiled query](compiled-queries-linq-to-entities.md).</span></span>  
  
 <span data-ttu-id="12376-106">這些範例中使用的 AdventureWorks Sales Model 是根據 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表所建立。</span><span class="sxs-lookup"><span data-stu-id="12376-106">The AdventureWorks Sales model used in these examples is built from the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="12376-107">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="12376-107">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="where"></a><span data-ttu-id="12376-108">Where</span><span class="sxs-lookup"><span data-stu-id="12376-108">Where</span></span>  
  
### <a name="example"></a><span data-ttu-id="12376-109">範例</span><span class="sxs-lookup"><span data-stu-id="12376-109">Example</span></span>  

 <span data-ttu-id="12376-110">下列範例會傳回所有線上訂單。</span><span class="sxs-lookup"><span data-stu-id="12376-110">The following example returns all online orders.</span></span>  
  
 [!code-csharp[DP L2E Examples#Where1_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where1_mq)]
 [!code-vb[DP L2E Examples#Where1_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where1_mq)]  
  
### <a name="example"></a><span data-ttu-id="12376-111">範例</span><span class="sxs-lookup"><span data-stu-id="12376-111">Example</span></span>  

 <span data-ttu-id="12376-112">下列範例會傳回訂單數量大於 2 而小於 6 的訂單。</span><span class="sxs-lookup"><span data-stu-id="12376-112">The following example returns the orders where the order quantity is greater than 2 and less than 6.</span></span>  
  
 [!code-csharp[DP L2E Examples#Where2_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where2_mq)]
 [!code-vb[DP L2E Examples#Where2_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where2_mq)]  
  
### <a name="example"></a><span data-ttu-id="12376-113">範例</span><span class="sxs-lookup"><span data-stu-id="12376-113">Example</span></span>  

 <span data-ttu-id="12376-114">下列範例會傳回所有紅色的產品。</span><span class="sxs-lookup"><span data-stu-id="12376-114">The following example returns all red colored products.</span></span>  
  
 [!code-csharp[DP L2E Examples#Where3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#where3_mq)]
 [!code-vb[DP L2E Examples#Where3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#where3_mq)]  
  
### <a name="example"></a><span data-ttu-id="12376-115">範例</span><span class="sxs-lookup"><span data-stu-id="12376-115">Example</span></span>  

 <span data-ttu-id="12376-116">下列範例使用 `Where` 方法尋找在 2003 年 12 月 1 日之後下單的訂單，然後使用 `order.SalesOrderDetail` 導覽屬性取得每筆訂單的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="12376-116">The following example uses the `Where` method to find orders that were made after December 1, 2003 and then uses the `order.SalesOrderDetail` navigation property to get the details for each order.</span></span>  
  
 [!code-csharp[DP L2E Examples#WhereNavProperty_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#wherenavproperty_mq)]
 [!code-vb[DP L2E Examples#WhereNavProperty_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#wherenavproperty_mq)]  
  
## <a name="wherecontains"></a><span data-ttu-id="12376-117">Where…Contains</span><span class="sxs-lookup"><span data-stu-id="12376-117">Where…Contains</span></span>  
  
### <a name="example"></a><span data-ttu-id="12376-118">範例</span><span class="sxs-lookup"><span data-stu-id="12376-118">Example</span></span>  

 <span data-ttu-id="12376-119">下列範例以陣列為 `Where…Contains` 子句的一部分，尋找 `ProductModelID` 符合陣列中之值的所有產品。</span><span class="sxs-lookup"><span data-stu-id="12376-119">The following example uses an array as part of a `Where…Contains` clause to find all products that have a `ProductModelID` that matches a value in the array.</span></span>  
  
 [!code-csharp[DP L2E ArraysAndListsInQueries#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e arraysandlistsinqueries/cs/program.cs#3)]
 [!code-vb[DP L2E ArraysAndListsInQueries#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e arraysandlistsinqueries/vb/module1.vb#3)]  
  
> [!NOTE]
> <span data-ttu-id="12376-120">您可以將 `Where…Contains`、<xref:System.Array> 或實作 <xref:System.Collections.Generic.List%601> 介面的集合 (任何類型) 當作 <xref:System.Collections.Generic.IEnumerable%601> 子句中的部分述詞來使用。</span><span class="sxs-lookup"><span data-stu-id="12376-120">As part of the predicate in a `Where…Contains` clause, you can use an <xref:System.Array>, a <xref:System.Collections.Generic.List%601>, or a collection of any type that implements the <xref:System.Collections.Generic.IEnumerable%601> interface.</span></span> <span data-ttu-id="12376-121">您還可以宣告並初始化 LINQ to Entities 查詢中的集合。</span><span class="sxs-lookup"><span data-stu-id="12376-121">You can also declare and initialize a collection within a LINQ to Entities query.</span></span> <span data-ttu-id="12376-122">如需詳細資訊，請參閱下一個範例。</span><span class="sxs-lookup"><span data-stu-id="12376-122">See the next example for more information.</span></span>  
  
### <a name="example"></a><span data-ttu-id="12376-123">範例</span><span class="sxs-lookup"><span data-stu-id="12376-123">Example</span></span>  

 <span data-ttu-id="12376-124">下列範例會宣告並初始化 `Where…Contains` 子句中的陣列，以尋找具有 `ProductModelID` 或 `Size` 符合陣列中之值的所有產品。</span><span class="sxs-lookup"><span data-stu-id="12376-124">The following example declares and initializes arrays in a `Where…Contains` clause to find all products that have a `ProductModelID` or a `Size` that matches a value in the arrays.</span></span>  
  
 [!code-csharp[DP L2E ArraysAndListsInQueries#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp l2e arraysandlistsinqueries/cs/program.cs#4)]
 [!code-vb[DP L2E ArraysAndListsInQueries#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp l2e arraysandlistsinqueries/vb/module1.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="12376-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="12376-125">See also</span></span>

- [<span data-ttu-id="12376-126">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="12376-126">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
