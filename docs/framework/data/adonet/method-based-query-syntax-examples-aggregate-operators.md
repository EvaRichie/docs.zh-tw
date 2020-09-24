---
title: 以方法為基礎的查詢語法範例：彙總運算子 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5ed5f01d-acb2-4dd4-be60-f04c2d570fa8
ms.openlocfilehash: f702506e648c73dc179cf1755a467b13afce4bc6
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164658"
---
# <a name="method-based-query-syntax-examples-aggregate-operators-linq-to-dataset"></a><span data-ttu-id="d4517-102">以方法為基礎的查詢語法範例：彙總運算子 (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="d4517-102">Method-Based Query Syntax Examples: Aggregate Operators (LINQ to DataSet)</span></span>

<span data-ttu-id="d4517-103">此主題中的範例將示範如何使用 <xref:System.Linq.Enumerable.Aggregate%2A>、<xref:System.Linq.Enumerable.Average%2A>、<xref:System.Linq.Enumerable.Count%2A>、<xref:System.Linq.Enumerable.LongCount%2A>、<xref:System.Linq.Enumerable.Max%2A>、<xref:System.Linq.Enumerable.Min%2A> 和 <xref:System.Linq.Enumerable.Sum%2A> 運算子並搭配方法查詢語法來查詢 <xref:System.Data.DataSet> 以及彙總資料。</span><span class="sxs-lookup"><span data-stu-id="d4517-103">The examples in this topic demonstrate how to use the <xref:System.Linq.Enumerable.Aggregate%2A>, <xref:System.Linq.Enumerable.Average%2A>, <xref:System.Linq.Enumerable.Count%2A>, <xref:System.Linq.Enumerable.LongCount%2A>, <xref:System.Linq.Enumerable.Max%2A>, <xref:System.Linq.Enumerable.Min%2A>, and <xref:System.Linq.Enumerable.Sum%2A> operators to query a <xref:System.Data.DataSet> and aggregate data using method query syntax.</span></span>  
  
 <span data-ttu-id="d4517-104">`FillDataSet`這些範例中使用的方法是在將[資料載入資料集](loading-data-into-a-dataset.md)時指定。</span><span class="sxs-lookup"><span data-stu-id="d4517-104">The `FillDataSet` method used in these examples is specified in [Loading Data Into a DataSet](loading-data-into-a-dataset.md).</span></span>  
  
 <span data-ttu-id="d4517-105">此主題中的範例將使用 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表。</span><span class="sxs-lookup"><span data-stu-id="d4517-105">The examples in this topic use the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="d4517-106">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="d4517-106">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 <span data-ttu-id="d4517-107">如需詳細資訊，請參閱 [如何：在 Visual Studio 中建立 LINQ to DataSet 專案](how-to-create-a-linq-to-dataset-project-in-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="d4517-107">For more information, see [How to: Create a LINQ to DataSet Project In Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).</span></span>  
  
## <a name="aggregate"></a><span data-ttu-id="d4517-108">Aggregate</span><span class="sxs-lookup"><span data-stu-id="d4517-108">Aggregate</span></span>  
  
### <a name="example"></a><span data-ttu-id="d4517-109">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-109">Example</span></span>  

 <span data-ttu-id="d4517-110">這則範例會使用 <xref:System.Linq.Enumerable.Aggregate%2A> 方法，從 `Contact` 資料表中取得前 5 位連絡人並建立姓氏的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="d4517-110">This example uses the <xref:System.Linq.Enumerable.Aggregate%2A> method to get the first 5 contacts from the `Contact` table and build a comma-delimited list of the last names.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#Aggregate_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#aggregate_mq)]
 [!code-vb[DP LINQ to DataSet Examples#Aggregate_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#aggregate_mq)]  
  
## <a name="average"></a><span data-ttu-id="d4517-111">Average</span><span class="sxs-lookup"><span data-stu-id="d4517-111">Average</span></span>  
  
### <a name="example"></a><span data-ttu-id="d4517-112">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-112">Example</span></span>  

 <span data-ttu-id="d4517-113">這則範例會使用 <xref:System.Linq.Enumerable.Average%2A> 方法來尋找產品的平均標價。</span><span class="sxs-lookup"><span data-stu-id="d4517-113">This example uses the <xref:System.Linq.Enumerable.Average%2A> method to find the average list price of the products.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#Average_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#average_mq)]
 [!code-vb[DP LINQ to DataSet Examples#Average_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#average_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-114">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-114">Example</span></span>  

 <span data-ttu-id="d4517-115">這則範例會使用 <xref:System.Linq.Enumerable.Average%2A> 方法來尋找每種樣式之產品的平均標價。</span><span class="sxs-lookup"><span data-stu-id="d4517-115">This example uses the <xref:System.Linq.Enumerable.Average%2A> method to find the average list price of the products of each style.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#Average2_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#average2_mq)]
 [!code-vb[DP LINQ to DataSet Examples#Average2_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#average2_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-116">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-116">Example</span></span>  

 <span data-ttu-id="d4517-117">這則範例會使用 <xref:System.Linq.Enumerable.Average%2A> 方法來尋找平均總金額。</span><span class="sxs-lookup"><span data-stu-id="d4517-117">This example uses the <xref:System.Linq.Enumerable.Average%2A> method to find the average total due.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#AverageProjection_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#averageprojection_mq)]
 [!code-vb[DP LINQ to DataSet Examples#AverageProjection_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#averageprojection_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-118">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-118">Example</span></span>  

 <span data-ttu-id="d4517-119">這則範例會使用 <xref:System.Linq.Enumerable.Average%2A> 方法來取得每個連絡人識別碼的平均總金額。</span><span class="sxs-lookup"><span data-stu-id="d4517-119">This example uses the <xref:System.Linq.Enumerable.Average%2A> method to get the average total due for each contact ID.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#AverageGrouped_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#averagegrouped_mq)]
 [!code-vb[DP LINQ to DataSet Examples#AverageGrouped_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#averagegrouped_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-120">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-120">Example</span></span>  

 <span data-ttu-id="d4517-121">這則範例會使用 <xref:System.Linq.Enumerable.Average%2A> 方法來取得含有每位連絡人之平均 `TotalDue` 的訂單。</span><span class="sxs-lookup"><span data-stu-id="d4517-121">This example uses the <xref:System.Linq.Enumerable.Average%2A> method to get the orders with the average `TotalDue` for each contact.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#AverageElements_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#averageelements_mq)]
 [!code-vb[DP LINQ to DataSet Examples#AverageElements_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#averageelements_mq)]  
  
## <a name="count"></a><span data-ttu-id="d4517-122">計數</span><span class="sxs-lookup"><span data-stu-id="d4517-122">Count</span></span>  
  
### <a name="example"></a><span data-ttu-id="d4517-123">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-123">Example</span></span>  

 <span data-ttu-id="d4517-124">這則範例會使用 <xref:System.Linq.Enumerable.Count%2A> 方法來傳回 `Product` 資料表中的產品數目。</span><span class="sxs-lookup"><span data-stu-id="d4517-124">This example uses the <xref:System.Linq.Enumerable.Count%2A> method to return the number of products in the `Product` table.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#Count](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#count)]
 [!code-vb[DP LINQ to DataSet Examples#Count](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#count)]  
  
### <a name="example"></a><span data-ttu-id="d4517-125">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-125">Example</span></span>  

 <span data-ttu-id="d4517-126">這則範例會使用 <xref:System.Linq.Enumerable.Count%2A> 方法來傳回連絡人識別碼以及每個連絡人識別碼擁有多少訂單的清單。</span><span class="sxs-lookup"><span data-stu-id="d4517-126">This example uses the <xref:System.Linq.Enumerable.Count%2A> method to return a list of contact IDs and how many orders each has.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#CountNested](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#countnested)]
 [!code-vb[DP LINQ to DataSet Examples#CountNested](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#countnested)]  
  
### <a name="example"></a><span data-ttu-id="d4517-127">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-127">Example</span></span>  

 <span data-ttu-id="d4517-128">這則範例會依據色彩來分組產品並使用 <xref:System.Linq.Enumerable.Count%2A> 方法來傳回每個色彩群組中的產品數目。</span><span class="sxs-lookup"><span data-stu-id="d4517-128">This example groups products by color and uses the <xref:System.Linq.Enumerable.Count%2A> method to return the number of products in each color group.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#CountGrouped](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#countgrouped)]
 [!code-vb[DP LINQ to DataSet Examples#CountGrouped](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#countgrouped)]  
  
## <a name="longcount"></a><span data-ttu-id="d4517-129">LongCount</span><span class="sxs-lookup"><span data-stu-id="d4517-129">LongCount</span></span>  
  
### <a name="example"></a><span data-ttu-id="d4517-130">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-130">Example</span></span>  

 <span data-ttu-id="d4517-131">這則範例會取得連絡人計數當做長整數 (Long Integer)。</span><span class="sxs-lookup"><span data-stu-id="d4517-131">This example gets the contact count as a long integer.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#LongCountSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#longcountsimple)]
 [!code-vb[DP LINQ to DataSet Examples#LongCountSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#longcountsimple)]  
  
## <a name="max"></a><span data-ttu-id="d4517-132">最大值</span><span class="sxs-lookup"><span data-stu-id="d4517-132">Max</span></span>  
  
### <a name="example"></a><span data-ttu-id="d4517-133">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-133">Example</span></span>  

 <span data-ttu-id="d4517-134">這則範例會使用 <xref:System.Linq.Enumerable.Max%2A> 方法來取得最大總金額。</span><span class="sxs-lookup"><span data-stu-id="d4517-134">This example uses the <xref:System.Linq.Enumerable.Max%2A> method to get the largest total due.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#MaxProjection_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#maxprojection_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MaxProjection_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#maxprojection_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-135">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-135">Example</span></span>  

 <span data-ttu-id="d4517-136">這則範例會使用 <xref:System.Linq.Enumerable.Max%2A> 方法來取得每個連絡人識別碼的最大總金額。</span><span class="sxs-lookup"><span data-stu-id="d4517-136">This example uses the <xref:System.Linq.Enumerable.Max%2A> method to get the largest total due for each contact ID.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#MaxGrouped_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#maxgrouped_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MaxGrouped_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#maxgrouped_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-137">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-137">Example</span></span>  

 <span data-ttu-id="d4517-138">這則範例會使用 <xref:System.Linq.Enumerable.Max%2A> 方法來取得含有每個連絡人識別碼之最大 `TotalDue` 的訂單。</span><span class="sxs-lookup"><span data-stu-id="d4517-138">This example uses the <xref:System.Linq.Enumerable.Max%2A> method to get the orders with the largest `TotalDue` for each contact ID.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#MaxElements_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#maxelements_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MaxElements_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#maxelements_mq)]  
  
## <a name="min"></a><span data-ttu-id="d4517-139">最小值</span><span class="sxs-lookup"><span data-stu-id="d4517-139">Min</span></span>  
  
### <a name="example"></a><span data-ttu-id="d4517-140">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-140">Example</span></span>  

 <span data-ttu-id="d4517-141">這則範例會使用 <xref:System.Linq.Enumerable.Min%2A> 方法來取得最小總金額。</span><span class="sxs-lookup"><span data-stu-id="d4517-141">This example uses the <xref:System.Linq.Enumerable.Min%2A> method to get the smallest total due.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#MinProjection_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#minprojection_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MinProjection_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#minprojection_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-142">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-142">Example</span></span>  

 <span data-ttu-id="d4517-143">這則範例會使用 <xref:System.Linq.Enumerable.Min%2A> 方法來取得每個連絡人識別碼的最小總金額。</span><span class="sxs-lookup"><span data-stu-id="d4517-143">This example uses the <xref:System.Linq.Enumerable.Min%2A> method to get the smallest total due for each contact ID.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#MinGrouped_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#mingrouped_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MinGrouped_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#mingrouped_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-144">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-144">Example</span></span>  

 <span data-ttu-id="d4517-145">這則範例會使用 <xref:System.Linq.Enumerable.Min%2A> 方法來取得含有每位連絡人之最小總金額的訂單。</span><span class="sxs-lookup"><span data-stu-id="d4517-145">This example uses the <xref:System.Linq.Enumerable.Min%2A> method to get the orders with the smallest total due for each contact.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#MinElements_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#minelements_mq)]
 [!code-vb[DP LINQ to DataSet Examples#MinElements_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#minelements_mq)]  
  
## <a name="sum"></a><span data-ttu-id="d4517-146">Sum</span><span class="sxs-lookup"><span data-stu-id="d4517-146">Sum</span></span>  
  
### <a name="example"></a><span data-ttu-id="d4517-147">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-147">Example</span></span>  

 <span data-ttu-id="d4517-148">這則範例會使用 <xref:System.Linq.Enumerable.Sum%2A> 方法來取得 `SalesOrderDetail` 資料表中訂單數量的總數。</span><span class="sxs-lookup"><span data-stu-id="d4517-148">This example uses the <xref:System.Linq.Enumerable.Sum%2A> method to get the total number of order quantities in the `SalesOrderDetail` table.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#SumProjection_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#sumprojection_mq)]  
  
### <a name="example"></a><span data-ttu-id="d4517-149">範例</span><span class="sxs-lookup"><span data-stu-id="d4517-149">Example</span></span>  

 <span data-ttu-id="d4517-150">這則範例會使用 <xref:System.Linq.Enumerable.Sum%2A> 方法來取得每個連絡人識別碼的總金額。</span><span class="sxs-lookup"><span data-stu-id="d4517-150">This example uses the <xref:System.Linq.Enumerable.Sum%2A> method to get the total due for each contact ID.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#SumGrouped_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#sumgrouped_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SumGrouped_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#sumgrouped_mq)]  
  
## <a name="see-also"></a><span data-ttu-id="d4517-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d4517-151">See also</span></span>

- [<span data-ttu-id="d4517-152">將資料載入至資料集</span><span class="sxs-lookup"><span data-stu-id="d4517-152">Loading Data Into a DataSet</span></span>](loading-data-into-a-dataset.md)
- [<span data-ttu-id="d4517-153">LINQ to DataSet 範例</span><span class="sxs-lookup"><span data-stu-id="d4517-153">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)
- [<span data-ttu-id="d4517-154">標準查詢運算子概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="d4517-154">Standard Query Operators Overview (C#)</span></span>](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [<span data-ttu-id="d4517-155">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d4517-155">Standard Query Operators Overview (Visual Basic)</span></span>](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
