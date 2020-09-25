---
title: 以方法為基礎的查詢語法範例：排序 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8f9ce4fd-e84f-48c0-bb64-89e217236d3e
ms.openlocfilehash: 635b7f6e498e27ef8ca2e133df639f1010184a93
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197868"
---
# <a name="method-based-query-syntax-examples-ordering-linq-to-dataset"></a><span data-ttu-id="e0d3f-102">以方法為基礎的查詢語法範例：排序 (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="e0d3f-102">Method-Based Query Syntax Examples: Ordering (LINQ to DataSet)</span></span>

<span data-ttu-id="e0d3f-103">此主題中的範例將示範如何使用 <xref:System.Linq.Enumerable.OrderBy%2A>、<xref:System.Linq.Enumerable.Reverse%2A> 和 <xref:System.Linq.Enumerable.ThenBy%2A> 方法並搭配方法查詢語法來查詢 <xref:System.Data.DataSet> 以及排序結果。</span><span class="sxs-lookup"><span data-stu-id="e0d3f-103">The examples in this topic demonstrate how to use the <xref:System.Linq.Enumerable.OrderBy%2A>,  <xref:System.Linq.Enumerable.Reverse%2A>, and <xref:System.Linq.Enumerable.ThenBy%2A> methods to query a <xref:System.Data.DataSet> and order the results using the method query syntax.</span></span>  
  
 <span data-ttu-id="e0d3f-104">`FillDataSet`這些範例中使用的方法是在將[資料載入資料集](loading-data-into-a-dataset.md)時指定。</span><span class="sxs-lookup"><span data-stu-id="e0d3f-104">The `FillDataSet` method used in these examples is specified in [Loading Data Into a DataSet](loading-data-into-a-dataset.md).</span></span>  
  
 <span data-ttu-id="e0d3f-105">此主題中的範例將使用 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表。</span><span class="sxs-lookup"><span data-stu-id="e0d3f-105">The examples in this topic use the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="e0d3f-106">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="e0d3f-106">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP LINQ to DataSet Examples#ImportsUsing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#importsusing)]  
  
 <span data-ttu-id="e0d3f-107">如需詳細資訊，請參閱 [如何：在 Visual Studio 中建立 LINQ to DataSet 專案](how-to-create-a-linq-to-dataset-project-in-vs.md)。</span><span class="sxs-lookup"><span data-stu-id="e0d3f-107">For more information, see [How to: Create a LINQ to DataSet Project In Visual Studio](how-to-create-a-linq-to-dataset-project-in-vs.md).</span></span>  
  
## <a name="orderby"></a><span data-ttu-id="e0d3f-108">OrderBy</span><span class="sxs-lookup"><span data-stu-id="e0d3f-108">OrderBy</span></span>  
  
### <a name="example"></a><span data-ttu-id="e0d3f-109">範例</span><span class="sxs-lookup"><span data-stu-id="e0d3f-109">Example</span></span>  

 <span data-ttu-id="e0d3f-110">這則範例會使用 <xref:System.Linq.Enumerable.OrderBy%2A> 方法搭配自訂比較子 (Comparer) 來進行姓氏的不區分大小寫排序。</span><span class="sxs-lookup"><span data-stu-id="e0d3f-110">This example uses the <xref:System.Linq.Enumerable.OrderBy%2A> method with a custom comparer to do a case-insensitive sort of last names.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#OrderByComparer_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#orderbycomparer_mq)]
 [!code-vb[DP LINQ to DataSet Examples#OrderByComparer_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#orderbycomparer_mq)]  
  
## <a name="reverse"></a><span data-ttu-id="e0d3f-111">Reverse</span><span class="sxs-lookup"><span data-stu-id="e0d3f-111">Reverse</span></span>  
  
### <a name="example"></a><span data-ttu-id="e0d3f-112">範例</span><span class="sxs-lookup"><span data-stu-id="e0d3f-112">Example</span></span>  

 <span data-ttu-id="e0d3f-113">這則範例會使用 <xref:System.Linq.Enumerable.Reverse%2A> 方法來建立 `OrderDate` 早於 2002 年 2 月 20 日之訂單的清單。</span><span class="sxs-lookup"><span data-stu-id="e0d3f-113">This example uses the <xref:System.Linq.Enumerable.Reverse%2A> method to create a list of orders where `OrderDate` is earlier than Feb 20, 2002.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#Reverse](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#reverse)]
 [!code-vb[DP LINQ to DataSet Examples#Reverse](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#reverse)]  
  
## <a name="thenby"></a><span data-ttu-id="e0d3f-114">ThenBy</span><span class="sxs-lookup"><span data-stu-id="e0d3f-114">ThenBy</span></span>  
  
### <a name="example"></a><span data-ttu-id="e0d3f-115">範例</span><span class="sxs-lookup"><span data-stu-id="e0d3f-115">Example</span></span>  

 <span data-ttu-id="e0d3f-116">這則範例會使用 <xref:System.Linq.Enumerable.OrderBy%2A> 和 <xref:System.Linq.Enumerable.ThenBy%2A> 方法搭配自訂比較子，先依據標價排序，然後再執行產品名稱的不區分大小寫遞減排序。</span><span class="sxs-lookup"><span data-stu-id="e0d3f-116">This example uses <xref:System.Linq.Enumerable.OrderBy%2A> and <xref:System.Linq.Enumerable.ThenBy%2A> methods with a custom comparer to first sort by list price, and then perform a case-insensitive descending sort of the product names.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#ThenByDescendingComparer_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#thenbydescendingcomparer_mq)]
 [!code-vb[DP LINQ to DataSet Examples#ThenByDescendingComparer_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#thenbydescendingcomparer_mq)]  
  
## <a name="see-also"></a><span data-ttu-id="e0d3f-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e0d3f-117">See also</span></span>

- [<span data-ttu-id="e0d3f-118">將資料載入至資料集</span><span class="sxs-lookup"><span data-stu-id="e0d3f-118">Loading Data Into a DataSet</span></span>](loading-data-into-a-dataset.md)
- [<span data-ttu-id="e0d3f-119">LINQ to DataSet 範例</span><span class="sxs-lookup"><span data-stu-id="e0d3f-119">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)
- [<span data-ttu-id="e0d3f-120">標準查詢運算子概觀 (C#)</span><span class="sxs-lookup"><span data-stu-id="e0d3f-120">Standard Query Operators Overview (C#)</span></span>](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [<span data-ttu-id="e0d3f-121">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e0d3f-121">Standard Query Operators Overview (Visual Basic)</span></span>](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
