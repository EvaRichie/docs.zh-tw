---
title: 以方法為基礎的查詢語法範例：分割 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a582c53f-f203-44ae-a797-d7f169a4fbb5
ms.openlocfilehash: 0ef7176ccffb7037a7d4496cc7d4da7991741d38
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91147927"
---
# <a name="method-based-query-syntax-examples-partitioning-linq"></a><span data-ttu-id="9e3e8-102">以方法為基礎的查詢語法範例：分割 (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="9e3e8-102">Method-Based Query Syntax Examples: Partitioning (LINQ</span></span>

<span data-ttu-id="9e3e8-103">此主題中的範例將示範如何使用 <xref:System.Linq.Enumerable.Skip%2A>、<xref:System.Linq.Enumerable.SkipWhile%2A>、<xref:System.Linq.Enumerable.Take%2A> 和 <xref:System.Linq.Enumerable.TakeWhile%2A> 方法並搭配查詢運算式語法來查詢 <xref:System.Data.DataSet>。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-103">The examples in this topic demonstrate how to use the <xref:System.Linq.Enumerable.Skip%2A>, <xref:System.Linq.Enumerable.SkipWhile%2A>, <xref:System.Linq.Enumerable.Take%2A>, and <xref:System.Linq.Enumerable.TakeWhile%2A> methods to query a <xref:System.Data.DataSet> using the query expression syntax.</span></span>  
  
 <span data-ttu-id="9e3e8-104">`FillDataSet`這些範例中使用的方法是在將[資料載入資料集](loading-data-into-a-dataset.md)時指定。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-104">The `FillDataSet` method used in these examples is specified in [Loading Data Into a DataSet](loading-data-into-a-dataset.md).</span></span>  
  
 <span data-ttu-id="9e3e8-105">此主題中的範例將使用 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-105">The examples in this topic use the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="9e3e8-106">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="9e3e8-106">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 <span data-ttu-id="9e3e8-107">如需詳細資訊，請參閱 [如何：在 Visual Studio 中建立 LINQ to DataSet 專案](how-to-create-a-linq-to-dataset-project-in-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-107">For more information, see [How to: Create a LINQ to DataSet Project In Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).</span></span>  
  
## <a name="skip"></a><span data-ttu-id="9e3e8-108">跳過</span><span class="sxs-lookup"><span data-stu-id="9e3e8-108">Skip</span></span>  
  
### <a name="example"></a><span data-ttu-id="9e3e8-109">範例</span><span class="sxs-lookup"><span data-stu-id="9e3e8-109">Example</span></span>  

 <span data-ttu-id="9e3e8-110">這則範例會使用 <xref:System.Linq.Enumerable.Skip%2A> 方法來取得 `Contact` 資料表的所有連絡人 (前五位連絡人除外)。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-110">This example uses the <xref:System.Linq.Enumerable.Skip%2A> method to get all but the first five contacts of the `Contact` table.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipsimple)]
 [!code-vb[DP LINQ to DataSet Examples#SkipSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipsimple)]  
  
### <a name="example"></a><span data-ttu-id="9e3e8-111">範例</span><span class="sxs-lookup"><span data-stu-id="9e3e8-111">Example</span></span>  

 <span data-ttu-id="9e3e8-112">這則範例會使用 <xref:System.Linq.Enumerable.Skip%2A> 方法來取得西雅圖的所有地址 (前兩筆地址除外)。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-112">This example uses the <xref:System.Linq.Enumerable.Skip%2A> method to get all but the first two addresses in Seattle.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipNested](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipnested)]
 [!code-vb[DP LINQ to DataSet Examples#SkipNested](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipnested)]  
  
## <a name="skipwhile"></a><span data-ttu-id="9e3e8-113">SkipWhile</span><span class="sxs-lookup"><span data-stu-id="9e3e8-113">SkipWhile</span></span>  
  
### <a name="example"></a><span data-ttu-id="9e3e8-114">範例</span><span class="sxs-lookup"><span data-stu-id="9e3e8-114">Example</span></span>  

 <span data-ttu-id="9e3e8-115">這則範例會使用 <xref:System.Linq.Enumerable.OrderBy%2A> 和 <xref:System.Linq.Enumerable.SkipWhile%2A> 方法，從 `Product` 資料表中傳回標價大於 300.00 的產品。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-115">This example uses <xref:System.Linq.Enumerable.OrderBy%2A> and <xref:System.Linq.Enumerable.SkipWhile%2A> methods to return products from the `Product` table with a list price greater than 300.00.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#SkipWhileSimple_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#skipwhilesimple_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SkipWhileSimple_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#skipwhilesimple_mq)]  
  
## <a name="take"></a><span data-ttu-id="9e3e8-116">Take</span><span class="sxs-lookup"><span data-stu-id="9e3e8-116">Take</span></span>  
  
### <a name="example"></a><span data-ttu-id="9e3e8-117">範例</span><span class="sxs-lookup"><span data-stu-id="9e3e8-117">Example</span></span>  

 <span data-ttu-id="9e3e8-118">這則範例會使用 <xref:System.Linq.Enumerable.Take%2A> 方法，單獨從 `Contact` 資料表中取得前五位連絡人。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-118">This example uses the <xref:System.Linq.Enumerable.Take%2A> method to get only the first five contacts from the `Contact` table.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takesimple)]
 [!code-vb[DP LINQ to DataSet Examples#TakeSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takesimple)]  
  
### <a name="example"></a><span data-ttu-id="9e3e8-119">範例</span><span class="sxs-lookup"><span data-stu-id="9e3e8-119">Example</span></span>  

 <span data-ttu-id="9e3e8-120">這則範例會使用 <xref:System.Linq.Enumerable.Take%2A> 方法來取得西雅圖的前三筆地址。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-120">This example uses the <xref:System.Linq.Enumerable.Take%2A> method to get the first three addresses in Seattle.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeNested](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takenested)]
 [!code-vb[DP LINQ to DataSet Examples#TakeNested](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takenested)]  
  
## <a name="takewhile"></a><span data-ttu-id="9e3e8-121">TakeWhile</span><span class="sxs-lookup"><span data-stu-id="9e3e8-121">TakeWhile</span></span>  
  
### <a name="example"></a><span data-ttu-id="9e3e8-122">範例</span><span class="sxs-lookup"><span data-stu-id="9e3e8-122">Example</span></span>  

 <span data-ttu-id="9e3e8-123">這則範例會使用 <xref:System.Linq.Enumerable.OrderBy%2A> 和 <xref:System.Linq.Enumerable.TakeWhile%2A> 方法，從 `Product` 資料表中傳回標價小於 300.00 的產品。</span><span class="sxs-lookup"><span data-stu-id="9e3e8-123">This example uses <xref:System.Linq.Enumerable.OrderBy%2A> and <xref:System.Linq.Enumerable.TakeWhile%2A> to return products from the `Product` table with a list price less than 300.00.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#TakeWhileSimple_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#takewhilesimple_mq)]
 [!code-vb[DP LINQ to DataSet Examples#TakeWhileSimple_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#takewhilesimple_mq)]  
  
## <a name="see-also"></a><span data-ttu-id="9e3e8-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9e3e8-124">See also</span></span>

- [<span data-ttu-id="9e3e8-125">將資料載入至資料集</span><span class="sxs-lookup"><span data-stu-id="9e3e8-125">Loading Data Into a DataSet</span></span>](loading-data-into-a-dataset.md)
- [<span data-ttu-id="9e3e8-126">LINQ to DataSet 範例</span><span class="sxs-lookup"><span data-stu-id="9e3e8-126">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)
- [<span data-ttu-id="9e3e8-127">標準查詢運算子概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="9e3e8-127">Standard Query Operators Overview (C#)</span></span>](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [<span data-ttu-id="9e3e8-128">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9e3e8-128">Standard Query Operators Overview (Visual Basic)</span></span>](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
