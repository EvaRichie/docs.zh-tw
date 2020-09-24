---
title: 查詢運算式語法範例：導覽關聯性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0d4a7f41-c758-4059-8f83-d2e9c2745593
ms.openlocfilehash: c09a0458f5b0b7d313da3379b5dda9b969eaf7e4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156793"
---
# <a name="query-expression-syntax-examples-navigating-relationships"></a><span data-ttu-id="e89b9-102">查詢運算式語法範例：導覽關聯性</span><span class="sxs-lookup"><span data-stu-id="e89b9-102">Query Expression Syntax Examples: Navigating Relationships</span></span>

<span data-ttu-id="e89b9-103">Entity Framework 中的導覽屬性是用來尋找位於關聯兩端之實體的快捷方式屬性。</span><span class="sxs-lookup"><span data-stu-id="e89b9-103">Navigation properties in the Entity Framework are shortcut properties used to locate the entities at the ends of an association.</span></span> <span data-ttu-id="e89b9-104">導覽屬性可讓使用者在不同實體之間巡覽，或是透過關聯集從某個實體巡覽至相關的實體。</span><span class="sxs-lookup"><span data-stu-id="e89b9-104">Navigation properties allow a user to navigate from one entity to another, or from one entity to related entities through an association set.</span></span> <span data-ttu-id="e89b9-105">本主題提供查詢運算式語法的範例，說明如何透過 LINQ to Entities 查詢中的導覽屬性來導覽關聯性。</span><span class="sxs-lookup"><span data-stu-id="e89b9-105">This topic provides examples in query expression syntax of how to navigate relationships through navigation properties in LINQ to Entities queries.</span></span>  
  
 <span data-ttu-id="e89b9-106">這些範例中使用的 AdventureWorks Sales Model 是從 AdventureWorks 範例資料庫中的 Contact、Address、Product、SalesOrderHeader 和 SalesOrderDetail 資料表所建立。</span><span class="sxs-lookup"><span data-stu-id="e89b9-106">The AdventureWorks Sales Model used in these examples is built from the Contact, Address, Product, SalesOrderHeader, and SalesOrderDetail tables in the AdventureWorks sample database.</span></span>  
  
 <span data-ttu-id="e89b9-107">本主題中的範例使用下列 `using` / `Imports` 語句：</span><span class="sxs-lookup"><span data-stu-id="e89b9-107">The examples in this topic use the following `using`/`Imports` statements:</span></span>  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="example"></a><span data-ttu-id="e89b9-108">範例</span><span class="sxs-lookup"><span data-stu-id="e89b9-108">Example</span></span>  

 <span data-ttu-id="e89b9-109">下列範例會使用 <xref:System.Linq.Queryable.Select%2A> 方法來取得所有連絡人識別碼，以及姓氏為 "Zhou" 之每位連絡人總金額的總和。</span><span class="sxs-lookup"><span data-stu-id="e89b9-109">The following example uses the <xref:System.Linq.Queryable.Select%2A> method to get all the contact IDs and the sum of the total due for each contact whose last name is "Zhou".</span></span> <span data-ttu-id="e89b9-110">`Contact.SalesOrderHeader` 導覽屬性是用來取得每一個連絡人之 `SalesOrderHeader` 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="e89b9-110">The `Contact.SalesOrderHeader` navigation property is used to get the collection of `SalesOrderHeader` objects for each contact.</span></span> <span data-ttu-id="e89b9-111">`Sum` 方法會使用 `Contact.SalesOrderHeader` 導覽屬性來加總每位連絡人之所有訂單的應付總額。</span><span class="sxs-lookup"><span data-stu-id="e89b9-111">The `Sum` method uses the `Contact.SalesOrderHeader` navigation property to sum the total due of all the orders for each contact.</span></span>  
  
 [!code-csharp[DP L2E Examples#SelectEachContactsOrders2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selecteachcontactsorders2)]
 [!code-vb[DP L2E Examples#SelectEachContactsOrders2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selecteachcontactsorders2)]  
  
## <a name="example"></a><span data-ttu-id="e89b9-112">範例</span><span class="sxs-lookup"><span data-stu-id="e89b9-112">Example</span></span>  

 <span data-ttu-id="e89b9-113">下列範例會取得姓氏為 "Zhou" 之連絡人的所有訂單。</span><span class="sxs-lookup"><span data-stu-id="e89b9-113">The following example gets all the orders of the contacts whose last name is "Zhou".</span></span> <span data-ttu-id="e89b9-114">`Contact.SalesOrderHeader` 導覽屬性是用來取得每一個連絡人之 `SalesOrderHeader` 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="e89b9-114">The `Contact.SalesOrderHeader` navigation property is used to get the collection of `SalesOrderHeader` objects for each contact.</span></span> <span data-ttu-id="e89b9-115">該連絡人的名稱和訂單會以匿名型別的形式傳回。</span><span class="sxs-lookup"><span data-stu-id="e89b9-115">The contact's name and orders are returned in an anonymous type.</span></span>  
  
 [!code-csharp[DP L2E Examples#SelectEachContactsOrders3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selecteachcontactsorders3)]
 [!code-vb[DP L2E Examples#SelectEachContactsOrders3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selecteachcontactsorders3)]  
  
## <a name="example"></a><span data-ttu-id="e89b9-116">範例</span><span class="sxs-lookup"><span data-stu-id="e89b9-116">Example</span></span>  

 <span data-ttu-id="e89b9-117">下列範例會使用 `SalesOrderHeader.Address` 和 `SalesOrderHeader.Contact` 導覽屬性來取得與每筆訂單相關聯之 `Address` 和 `Contact` 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="e89b9-117">The following example uses the `SalesOrderHeader.Address` and `SalesOrderHeader.Contact` navigation properties get the collection of `Address` and `Contact` objects associated with each order.</span></span> <span data-ttu-id="e89b9-118">到西雅圖城市之每一筆訂單的連絡人姓氏、街道地址、銷售訂單編號及應付總額會以匿名型別的形式傳回。</span><span class="sxs-lookup"><span data-stu-id="e89b9-118">The last name of the contact, the street address, the sales order number, and the total due for each order to the city of Seattle are returned in an anonymous type.</span></span>  
  
 [!code-csharp[DP L2E Examples#GetOrderInfoThruRelationships](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#getorderinfothrurelationships)]
 [!code-vb[DP L2E Examples#GetOrderInfoThruRelationships](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#getorderinfothrurelationships)]  
  
### <a name="example"></a><span data-ttu-id="e89b9-119">範例</span><span class="sxs-lookup"><span data-stu-id="e89b9-119">Example</span></span>  

 <span data-ttu-id="e89b9-120">下列範例會使用 `Where` 方法來尋找在 2003 年 12 月 1 日之後下單的訂單，然後使用 `order.SalesOrderDetail` 導覽屬性來取得每筆訂單的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e89b9-120">The following example uses the `Where` method to find orders that were made after December 1, 2003, and then uses the `order.SalesOrderDetail` navigation property to get the details for each order.</span></span>  
  
 [!code-csharp[DP L2E Examples#WhereNavProperty](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#wherenavproperty)]
 [!code-vb[DP L2E Examples#WhereNavProperty](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#wherenavproperty)]  
  
## <a name="see-also"></a><span data-ttu-id="e89b9-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e89b9-121">See also</span></span>

- [<span data-ttu-id="e89b9-122">LINQ to Entities 中的查詢</span><span class="sxs-lookup"><span data-stu-id="e89b9-122">Queries in LINQ to Entities</span></span>](queries-in-linq-to-entities.md)
