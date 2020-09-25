---
title: 以方法為基礎的查詢語法範例：項目運算子
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 8438b995-bd07-4223-b22d-13adadef33fb
ms.openlocfilehash: 96d393a34af69935e75582ef1954ddd661a355f0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91192044"
---
# <a name="method-based-query-syntax-examples-element-operators"></a><span data-ttu-id="aa5e4-102">以方法為基礎的查詢語法範例：項目運算子</span><span class="sxs-lookup"><span data-stu-id="aa5e4-102">Method-Based Query Syntax Examples: Element Operators</span></span>

<span data-ttu-id="aa5e4-103">本主題中的範例將示範如何使用方法 <xref:System.Linq.Enumerable.First%2A> ，透過以方法為基礎的查詢語法來查詢 [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) 。</span><span class="sxs-lookup"><span data-stu-id="aa5e4-103">The examples in this topic demonstrate how to use the <xref:System.Linq.Enumerable.First%2A> method to query the [AdventureWorks Sales Model](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) using method-based query syntax.</span></span> <span data-ttu-id="aa5e4-104">這些範例中使用的 AdventureWorks Sales Model 是從 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表所建立。</span><span class="sxs-lookup"><span data-stu-id="aa5e4-104">The AdventureWorks Sales Model used in these examples is built from the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="aa5e4-105">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="aa5e4-105">The example in this topic uses the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="first"></a><span data-ttu-id="aa5e4-106">First</span><span class="sxs-lookup"><span data-stu-id="aa5e4-106">First</span></span>  
  
### <a name="example"></a><span data-ttu-id="aa5e4-107">範例</span><span class="sxs-lookup"><span data-stu-id="aa5e4-107">Example</span></span>  

 <span data-ttu-id="aa5e4-108">下列範例 <xref:System.Linq.Enumerable.First%2A> 會使用方法來尋找以 ' caroline ' 開頭的第一個電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="aa5e4-108">The following example uses the <xref:System.Linq.Enumerable.First%2A> method to find the first email address that starts with 'caroline'.</span></span>  
  
 [!code-csharp[DP L2E Examples#FirstCondition_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#firstcondition_mq)]
 [!code-vb[DP L2E Examples#FirstCondition_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#firstcondition_mq)]  
  
## <a name="see-also"></a><span data-ttu-id="aa5e4-109">另請參閱</span><span class="sxs-lookup"><span data-stu-id="aa5e4-109">See also</span></span>

- [<span data-ttu-id="aa5e4-110">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="aa5e4-110">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
