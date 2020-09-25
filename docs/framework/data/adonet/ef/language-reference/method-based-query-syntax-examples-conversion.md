---
title: 以方法為基礎的查詢語法範例：轉換
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 19f66872-d5ab-49f8-969f-e53f9632a13d
ms.openlocfilehash: e2b5ae3b7c7733216f18914c497d080fe8d71a8e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91192083"
---
# <a name="method-based-query-syntax-examples-conversion"></a><span data-ttu-id="a9904-102">以方法為基礎的查詢語法範例：轉換</span><span class="sxs-lookup"><span data-stu-id="a9904-102">Method-Based Query Syntax Examples: Conversion</span></span>

<span data-ttu-id="a9904-103">本主題中的範例將示範如何使用 <xref:System.Linq.Enumerable.ToArray%2A> 、 <xref:System.Linq.Enumerable.ToDictionary%2A> 和方法， <xref:System.Linq.Enumerable.ToList%2A> 利用以方法為基礎的查詢語法來查詢 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 。</span><span class="sxs-lookup"><span data-stu-id="a9904-103">The examples in this topic demonstrate how to use the <xref:System.Linq.Enumerable.ToArray%2A>, <xref:System.Linq.Enumerable.ToDictionary%2A> and <xref:System.Linq.Enumerable.ToList%2A> methods to query the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) using method-based query syntax.</span></span> <span data-ttu-id="a9904-104">這些範例中使用的 AdventureWorks Sales Model 是從 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表所建立。</span><span class="sxs-lookup"><span data-stu-id="a9904-104">The AdventureWorks Sales Model used in these examples is built from the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="a9904-105">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="a9904-105">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="toarray"></a><span data-ttu-id="a9904-106">ToArray</span><span class="sxs-lookup"><span data-stu-id="a9904-106">ToArray</span></span>  
  
### <a name="example"></a><span data-ttu-id="a9904-107">範例</span><span class="sxs-lookup"><span data-stu-id="a9904-107">Example</span></span>  

 <span data-ttu-id="a9904-108">以下範例使用 <xref:System.Linq.Enumerable.ToArray%2A> 方法將序列立即評估為陣列。</span><span class="sxs-lookup"><span data-stu-id="a9904-108">The following example uses the <xref:System.Linq.Enumerable.ToArray%2A> method to immediately evaluate a sequence into an array.</span></span>  
  
 [!code-csharp[DP L2E Examples#ToArray](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#toarray)]
 [!code-vb[DP L2E Examples#ToArray](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#toarray)]  
  
## <a name="todictionary"></a><span data-ttu-id="a9904-109">ToDictionary</span><span class="sxs-lookup"><span data-stu-id="a9904-109">ToDictionary</span></span>  
  
### <a name="example"></a><span data-ttu-id="a9904-110">範例</span><span class="sxs-lookup"><span data-stu-id="a9904-110">Example</span></span>  

 <span data-ttu-id="a9904-111">下列範例會使用 <xref:System.Linq.Enumerable.ToDictionary%2A> 方法，立即將序列和相關的索引鍵運算式評估為字典。</span><span class="sxs-lookup"><span data-stu-id="a9904-111">The following example uses the <xref:System.Linq.Enumerable.ToDictionary%2A> method to immediately evaluate a sequence and a related key expression into a dictionary.</span></span>  
  
 [!code-csharp[DP L2E Examples#ToDictionary](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#todictionary)]
 [!code-vb[DP L2E Examples#ToDictionary](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#todictionary)]  
  
## <a name="tolist"></a><span data-ttu-id="a9904-112">ToList</span><span class="sxs-lookup"><span data-stu-id="a9904-112">ToList</span></span>  
  
### <a name="example"></a><span data-ttu-id="a9904-113">範例</span><span class="sxs-lookup"><span data-stu-id="a9904-113">Example</span></span>  

 <span data-ttu-id="a9904-114">下列範例會使用 <xref:System.Linq.Enumerable.ToList%2A> 方法，立即將序列評估為 <xref:System.Collections.Generic.List%601>，其中 `T` 的型別為 <xref:System.Data.DataRow>。</span><span class="sxs-lookup"><span data-stu-id="a9904-114">The following example uses the <xref:System.Linq.Enumerable.ToList%2A> method to immediately evaluate a sequence into a <xref:System.Collections.Generic.List%601>, where `T` is of type <xref:System.Data.DataRow>.</span></span>  
  
 [!code-csharp[DP L2E Examples#ToList](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#tolist)]
 [!code-vb[DP L2E Examples#ToList](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#tolist)]  
  
## <a name="see-also"></a><span data-ttu-id="a9904-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a9904-115">See also</span></span>

- [<span data-ttu-id="a9904-116">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="a9904-116">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
