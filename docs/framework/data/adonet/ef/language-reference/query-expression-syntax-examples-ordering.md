---
title: 查詢運算式語法範例：排序
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: bcbc9625-7cf7-476e-85d2-058f12682f54
ms.openlocfilehash: ed03fc248ed48f56998bc27f7e880b1e8aa443d2
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156780"
---
# <a name="query-expression-syntax-examples-ordering"></a><span data-ttu-id="5c109-102">查詢運算式語法範例：排序</span><span class="sxs-lookup"><span data-stu-id="5c109-102">Query Expression Syntax Examples: Ordering</span></span>

<span data-ttu-id="5c109-103">本主題中的範例將示範如何使用 `OrderBy` 和 `OrderByDescending` 方法，利用查詢運算式語法來查詢 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 。</span><span class="sxs-lookup"><span data-stu-id="5c109-103">The examples in this topic demonstrate how to use the `OrderBy` and `OrderByDescending` methods to query the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) using query expression syntax.</span></span> <span data-ttu-id="5c109-104">這些範例中使用的 AdventureWorks Sales Model 是從 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表所建立。</span><span class="sxs-lookup"><span data-stu-id="5c109-104">The AdventureWorks Sales Model used in these examples is built from the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="5c109-105">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="5c109-105">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="orderby"></a><span data-ttu-id="5c109-106">OrderBy</span><span class="sxs-lookup"><span data-stu-id="5c109-106">OrderBy</span></span>  
  
### <a name="example"></a><span data-ttu-id="5c109-107">範例</span><span class="sxs-lookup"><span data-stu-id="5c109-107">Example</span></span>  

 <span data-ttu-id="5c109-108">下列範例會使用 <xref:System.Linq.Enumerable.OrderBy%2A> 來傳回依據姓氏排序的連絡人清單。</span><span class="sxs-lookup"><span data-stu-id="5c109-108">The following example uses <xref:System.Linq.Enumerable.OrderBy%2A> to return a list of contacts ordered by last name.</span></span>  
  
 [!code-csharp[DP L2E Examples#OrderBySimple1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbysimple1)]
 [!code-vb[DP L2E Examples#OrderBySimple1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbysimple1)]  
  
### <a name="example"></a><span data-ttu-id="5c109-109">範例</span><span class="sxs-lookup"><span data-stu-id="5c109-109">Example</span></span>  

 <span data-ttu-id="5c109-110">下列範例會使用 <xref:System.Linq.Enumerable.OrderBy%2A> 來依據姓氏的長度排序連絡人清單。</span><span class="sxs-lookup"><span data-stu-id="5c109-110">The following example uses <xref:System.Linq.Enumerable.OrderBy%2A> to sort a list of contacts by length of last name.</span></span>  
  
 [!code-csharp[DP L2E Examples#OrderBySimple2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbysimple2)]
 [!code-vb[DP L2E Examples#OrderBySimple2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbysimple2)]  
  
## <a name="orderbydescending"></a><span data-ttu-id="5c109-111">OrderByDescending</span><span class="sxs-lookup"><span data-stu-id="5c109-111">OrderByDescending</span></span>  
  
### <a name="example"></a><span data-ttu-id="5c109-112">範例</span><span class="sxs-lookup"><span data-stu-id="5c109-112">Example</span></span>  

 <span data-ttu-id="5c109-113">下列範例會使用 `orderby… descending`(Visual Basic 中的 `Order By … Descending`，相當於 <xref:System.Linq.Enumerable.OrderByDescending%2A> 方法)，從最高到最低排序價格清單。</span><span class="sxs-lookup"><span data-stu-id="5c109-113">The following example uses `orderby… descending` (`Order By … Descending` in Visual Basic), which is equivalent to the <xref:System.Linq.Enumerable.OrderByDescending%2A> method, to sort the price list from highest to lowest.</span></span>  
  
 [!code-csharp[DP L2E Examples#OrderByDescendingSimple1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbydescendingsimple1)]
 [!code-vb[DP L2E Examples#OrderByDescendingSimple1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbydescendingsimple1)]  
  
## <a name="thenby"></a><span data-ttu-id="5c109-114">ThenBy</span><span class="sxs-lookup"><span data-stu-id="5c109-114">ThenBy</span></span>  
  
### <a name="example"></a><span data-ttu-id="5c109-115">範例</span><span class="sxs-lookup"><span data-stu-id="5c109-115">Example</span></span>  

 <span data-ttu-id="5c109-116">下列範例會使用 <xref:System.Linq.Queryable.OrderBy%2A> 和 <xref:System.Linq.Queryable.ThenBy%2A> 來傳回先依據姓氏再依據名字排序的連絡人清單。</span><span class="sxs-lookup"><span data-stu-id="5c109-116">The following example uses <xref:System.Linq.Queryable.OrderBy%2A> and <xref:System.Linq.Queryable.ThenBy%2A> to return a list of contacts ordered by last name and then by first name.</span></span>  
  
 [!code-csharp[DP L2E Examples#OrderByThenBy](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#orderbythenby)]
 [!code-vb[DP L2E Examples#OrderByThenBy](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#orderbythenby)]  
  
## <a name="thenbydescending"></a><span data-ttu-id="5c109-117">ThenByDescending</span><span class="sxs-lookup"><span data-stu-id="5c109-117">ThenByDescending</span></span>  
  
### <a name="example"></a><span data-ttu-id="5c109-118">範例</span><span class="sxs-lookup"><span data-stu-id="5c109-118">Example</span></span>  

 <span data-ttu-id="5c109-119">下列範例會使用 `OrderBy… Descending` (相當於 <xref:System.Linq.Enumerable.ThenByDescending%2A> 方法) 來排序產品的清單 (先依據名稱，再依據標價，從最高到最低排序)。</span><span class="sxs-lookup"><span data-stu-id="5c109-119">The following example uses `OrderBy… Descending`, which is equivalent to the <xref:System.Linq.Enumerable.ThenByDescending%2A> method, to sort a list of products, first by name and then by list price from highest to lowest.</span></span>  
  
 [!code-csharp[DP L2E Examples#ThenByDescendingSimple](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#thenbydescendingsimple)]
 [!code-vb[DP L2E Examples#ThenByDescendingSimple](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#thenbydescendingsimple)]  
  
## <a name="see-also"></a><span data-ttu-id="5c109-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5c109-120">See also</span></span>

- [<span data-ttu-id="5c109-121">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="5c109-121">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
