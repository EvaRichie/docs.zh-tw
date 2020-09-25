---
title: 查詢運算式語法範例：排序 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 653a4a97-1e4a-4b2d-8d24-7dbe1f2a5c84
ms.openlocfilehash: e29ce3a1cf666057ae717f0717af73db7be87e30
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91189067"
---
# <a name="query-expression-syntax-examples-ordering-linq-to-dataset"></a><span data-ttu-id="5fcf5-102">查詢運算式語法範例：排序 (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="5fcf5-102">Query Expression Syntax Examples: Ordering (LINQ to DataSet)</span></span>

<span data-ttu-id="5fcf5-103">此主題中的範例將示範如何使用 <xref:System.Linq.Enumerable.OrderBy%2A>、<xref:System.Linq.Enumerable.OrderByDescending%2A>、<xref:System.Linq.Enumerable.Reverse%2A> 和 <xref:System.Linq.Enumerable.ThenByDescending%2A> 方法並搭配查詢運算式語法來查詢 <xref:System.Data.DataSet> 以及排序結果。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-103">The examples in this topic demonstrate how to use the <xref:System.Linq.Enumerable.OrderBy%2A>, <xref:System.Linq.Enumerable.OrderByDescending%2A>, <xref:System.Linq.Enumerable.Reverse%2A>, and <xref:System.Linq.Enumerable.ThenByDescending%2A> methods to query a <xref:System.Data.DataSet> and order the results using the query expression syntax.</span></span>  
  
 <span data-ttu-id="5fcf5-104">`FillDataSet`這些範例中使用的方法是在將[資料載入資料集](loading-data-into-a-dataset.md)時指定。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-104">The `FillDataSet` method used in these examples is specified in [Loading Data Into a DataSet](loading-data-into-a-dataset.md).</span></span>  
  
 <span data-ttu-id="5fcf5-105">此主題中的範例將使用 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-105">The examples in this topic use the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="5fcf5-106">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="5fcf5-106">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 <span data-ttu-id="5fcf5-107">如需詳細資訊，請參閱 [如何：在 Visual Studio 中建立 LINQ to DataSet 專案](how-to-create-a-linq-to-dataset-project-in-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-107">For more information, see [How to: Create a LINQ to DataSet Project In Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).</span></span>  
  
## <a name="orderby"></a><span data-ttu-id="5fcf5-108">OrderBy</span><span class="sxs-lookup"><span data-stu-id="5fcf5-108">OrderBy</span></span>  
  
### <a name="example"></a><span data-ttu-id="5fcf5-109">範例</span><span class="sxs-lookup"><span data-stu-id="5fcf5-109">Example</span></span>  

 <span data-ttu-id="5fcf5-110">這則範例會使用 <xref:System.Linq.Enumerable.OrderBy%2A> 來傳回依據姓氏排序的連絡人清單。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-110">This example uses <xref:System.Linq.Enumerable.OrderBy%2A> to return a list of contacts ordered by last name.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#OrderBySimple1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#orderbysimple1)]
 [!code-vb[DP LINQ to DataSet Examples#OrderBySimple1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#orderbysimple1)]  
  
### <a name="example"></a><span data-ttu-id="5fcf5-111">範例</span><span class="sxs-lookup"><span data-stu-id="5fcf5-111">Example</span></span>  

 <span data-ttu-id="5fcf5-112">這則範例會使用 <xref:System.Linq.Enumerable.OrderBy%2A> 來依據姓氏的長度排序連絡人清單。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-112">This example uses <xref:System.Linq.Enumerable.OrderBy%2A> to sort a list of contacts by length of last name.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#OrderBySimple2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#orderbysimple2)]
 [!code-vb[DP LINQ to DataSet Examples#OrderBySimple2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#orderbysimple2)]  
  
## <a name="orderbydescending"></a><span data-ttu-id="5fcf5-113">OrderByDescending</span><span class="sxs-lookup"><span data-stu-id="5fcf5-113">OrderByDescending</span></span>  
  
### <a name="example"></a><span data-ttu-id="5fcf5-114">範例</span><span class="sxs-lookup"><span data-stu-id="5fcf5-114">Example</span></span>  

 <span data-ttu-id="5fcf5-115">這則範例會使用 `orderby… descending` (`Order By … Descending`，相當於 <xref:System.Linq.Enumerable.OrderByDescending%2A> 方法)，從最高到最低排序價格清單。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-115">This example uses `orderby… descending` (`Order By … Descending`), which is equivalent to the <xref:System.Linq.Enumerable.OrderByDescending%2A> method, to sort the price list from highest to lowest.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#OrderByDescendingSimple1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#orderbydescendingsimple1)]
 [!code-vb[DP LINQ to DataSet Examples#OrderByDescendingSimple1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#orderbydescendingsimple1)]  
  
## <a name="reverse"></a><span data-ttu-id="5fcf5-116">Reverse</span><span class="sxs-lookup"><span data-stu-id="5fcf5-116">Reverse</span></span>  
  
### <a name="example"></a><span data-ttu-id="5fcf5-117">範例</span><span class="sxs-lookup"><span data-stu-id="5fcf5-117">Example</span></span>  

 <span data-ttu-id="5fcf5-118">這則範例會使用 <xref:System.Linq.Enumerable.Reverse%2A> 來建立 `OrderDate` 早於 2002 年 2 月 20 日之訂單的清單。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-118">This example uses <xref:System.Linq.Enumerable.Reverse%2A> to create a list of orders where `OrderDate` is earlier than Feb 20, 2002.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#Reverse](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#reverse)]
 [!code-vb[DP LINQ to DataSet Examples#Reverse](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#reverse)]  
  
## <a name="thenbydescending"></a><span data-ttu-id="5fcf5-119">ThenByDescending</span><span class="sxs-lookup"><span data-stu-id="5fcf5-119">ThenByDescending</span></span>  
  
### <a name="example"></a><span data-ttu-id="5fcf5-120">範例</span><span class="sxs-lookup"><span data-stu-id="5fcf5-120">Example</span></span>  

 <span data-ttu-id="5fcf5-121">這則範例會使用 `OrderBy… Descending` (相當於 <xref:System.Linq.Enumerable.ThenByDescending%2A> 方法) 來排序產品的清單 (先依據名稱，然後再依據標價，從最高到最低)。</span><span class="sxs-lookup"><span data-stu-id="5fcf5-121">This example uses `OrderBy… Descending` , which is equivalent to the <xref:System.Linq.Enumerable.ThenByDescending%2A> method, to sort a list of products, first by name and then by list price, from highest to lowest.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#ThenByDescendingSimple](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#thenbydescendingsimple)]
 [!code-vb[DP LINQ to DataSet Examples#ThenByDescendingSimple](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#thenbydescendingsimple)]  
  
## <a name="see-also"></a><span data-ttu-id="5fcf5-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5fcf5-122">See also</span></span>

- [<span data-ttu-id="5fcf5-123">將資料載入至資料集</span><span class="sxs-lookup"><span data-stu-id="5fcf5-123">Loading Data Into a DataSet</span></span>](loading-data-into-a-dataset.md)
- [<span data-ttu-id="5fcf5-124">LINQ to DataSet 範例</span><span class="sxs-lookup"><span data-stu-id="5fcf5-124">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)
- [<span data-ttu-id="5fcf5-125">標準查詢運算子概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="5fcf5-125">Standard Query Operators Overview (C#)</span></span>](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [<span data-ttu-id="5fcf5-126">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="5fcf5-126">Standard Query Operators Overview (Visual Basic)</span></span>](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
