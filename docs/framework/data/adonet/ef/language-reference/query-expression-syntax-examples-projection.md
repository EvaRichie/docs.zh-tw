---
title: 查詢運算式語法範例：投影
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 079926c5-e6b5-4fb9-b4cf-9c63886dd626
ms.openlocfilehash: 82395b79cb5b2834a79356cbdfb1087603a9ae77
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91175573"
---
# <a name="query-expression-syntax-examples-projection"></a><span data-ttu-id="19c03-102">查詢運算式語法範例：投影</span><span class="sxs-lookup"><span data-stu-id="19c03-102">Query Expression Syntax Examples: Projection</span></span>

<span data-ttu-id="19c03-103">本主題中的範例將示範如何使用 `Select` 方法和 `From … From …` 關鍵字，利用查詢運算式語法來查詢 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 。</span><span class="sxs-lookup"><span data-stu-id="19c03-103">The examples in this topic demonstrate how to use the `Select` method and the `From … From …` keywords to query the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) using query expression syntax.</span></span> <span data-ttu-id="19c03-104">`From … From …` 以查詢為基礎，等同於 `SelectMany` 方法。</span><span class="sxs-lookup"><span data-stu-id="19c03-104">`From … From …` is the query based equivalent of the `SelectMany` method.</span></span> <span data-ttu-id="19c03-105">這些範例中使用的 AdventureWorks Sales Model 是根據 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表所建立。</span><span class="sxs-lookup"><span data-stu-id="19c03-105">The AdventureWorks Sales model used in these examples is built from the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="19c03-106">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="19c03-106">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="select"></a><span data-ttu-id="19c03-107">選取</span><span class="sxs-lookup"><span data-stu-id="19c03-107">Select</span></span>  
  
### <a name="example"></a><span data-ttu-id="19c03-108">範例</span><span class="sxs-lookup"><span data-stu-id="19c03-108">Example</span></span>  

 <span data-ttu-id="19c03-109">下列範例會使用 <xref:System.Linq.Enumerable.Select%2A> 方法來傳回 `Product` 資料表中的所有資料列，並顯示產品名稱。</span><span class="sxs-lookup"><span data-stu-id="19c03-109">The following example uses the <xref:System.Linq.Enumerable.Select%2A> method to return all the rows from the `Product` table and display the product names.</span></span>  
  
 [!code-csharp[DP L2E Examples#SelectSimple1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectsimple1)]
 [!code-vb[DP L2E Examples#SelectSimple1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectsimple1)]  
  
### <a name="example"></a><span data-ttu-id="19c03-110">範例</span><span class="sxs-lookup"><span data-stu-id="19c03-110">Example</span></span>  

 <span data-ttu-id="19c03-111">下列範例會使用 <xref:System.Linq.Enumerable.Select%2A> 來單獨傳回產品名稱的序列 (Sequence)。</span><span class="sxs-lookup"><span data-stu-id="19c03-111">The following example uses <xref:System.Linq.Enumerable.Select%2A> to return a sequence of only product names.</span></span>  
  
 [!code-csharp[DP L2E Examples#SelectSimple2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectsimple2)]
 [!code-vb[DP L2E Examples#SelectSimple2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectsimple2)]  
  
### <a name="example"></a><span data-ttu-id="19c03-112">範例</span><span class="sxs-lookup"><span data-stu-id="19c03-112">Example</span></span>  

 <span data-ttu-id="19c03-113">下列範例會使用 <xref:System.Linq.Queryable.Select%2A> 方法，將 `Product.Name` 和 `Product.ProductID` 屬性投影到匿名型別的序列中。</span><span class="sxs-lookup"><span data-stu-id="19c03-113">The following example uses the <xref:System.Linq.Queryable.Select%2A> method to project the `Product.Name` and `Product.ProductID` properties into a sequence of anonymous types.</span></span>  
  
 [!code-csharp[DP L2E Examples#SelectAnonymousTypes](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectanonymoustypes)]
 [!code-vb[DP L2E Examples#SelectAnonymousTypes](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectanonymoustypes)]  
  
## <a name="from--from--selectmany"></a><span data-ttu-id="19c03-114">從。。。</span><span class="sxs-lookup"><span data-stu-id="19c03-114">From …</span></span> <span data-ttu-id="19c03-115">從。。。</span><span class="sxs-lookup"><span data-stu-id="19c03-115">From …</span></span> <span data-ttu-id="19c03-116"> (SelectMany) </span><span class="sxs-lookup"><span data-stu-id="19c03-116">(SelectMany)</span></span>  
  
### <a name="example"></a><span data-ttu-id="19c03-117">範例</span><span class="sxs-lookup"><span data-stu-id="19c03-117">Example</span></span>  

 <span data-ttu-id="19c03-118">下列範例會使用 `From … From …` (<xref:System.Linq.Enumerable.SelectMany%2A> 方法的對等項目) 來選取 `TotalDue` 少於 500.00 的所有訂單。</span><span class="sxs-lookup"><span data-stu-id="19c03-118">The following example uses `From … From …` (the equivalent of the <xref:System.Linq.Enumerable.SelectMany%2A> method) to select all orders where `TotalDue` is less than 500.00.</span></span>  
  
 [!code-csharp[DP L2E Examples#SelectManyCompoundFrom](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectmanycompoundfrom)]
 [!code-vb[DP L2E Examples#SelectManyCompoundFrom](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectmanycompoundfrom)]  
  
### <a name="example"></a><span data-ttu-id="19c03-119">範例</span><span class="sxs-lookup"><span data-stu-id="19c03-119">Example</span></span>  

 <span data-ttu-id="19c03-120">下列範例會使用 `From … From …` (<xref:System.Linq.Enumerable.SelectMany%2A> 方法的對等項目) 來選取在 2002 年 10 月 1 日或之後下單的所有訂單。</span><span class="sxs-lookup"><span data-stu-id="19c03-120">The following example uses `From … From …` (the equivalent of the <xref:System.Linq.Enumerable.SelectMany%2A> method) to select all orders where the order was made on October 1, 2002 or later.</span></span>  
  
 [!code-csharp[DP L2E Examples#SelectManyCompoundFrom2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectmanycompoundfrom2)]
 [!code-vb[DP L2E Examples#SelectManyCompoundFrom2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectmanycompoundfrom2)]  
  
### <a name="example"></a><span data-ttu-id="19c03-121">範例</span><span class="sxs-lookup"><span data-stu-id="19c03-121">Example</span></span>  

 <span data-ttu-id="19c03-122">下列範例會使用 `From … From …` (<xref:System.Linq.Enumerable.SelectMany%2A> 方法的對等項目) 來選取訂單總金額超過 10000.00 的所有訂單，並使用 `From` 指派來避免要求總金額兩次。</span><span class="sxs-lookup"><span data-stu-id="19c03-122">The following example uses a `From … From …` (the equivalent of the <xref:System.Linq.Enumerable.SelectMany%2A> method) to select all orders where the order total is greater than 10000.00 and uses `From` assignment to avoid requesting the total twice.</span></span>  
  
 [!code-csharp[DP L2E Examples#SelectManyFromAssignment](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selectmanyfromassignment)]
 [!code-vb[DP L2E Examples#SelectManyFromAssignment](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selectmanyfromassignment)]  
  
## <a name="see-also"></a><span data-ttu-id="19c03-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="19c03-123">See also</span></span>

- [<span data-ttu-id="19c03-124">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="19c03-124">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
