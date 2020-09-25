---
title: 如何：攔截資料服務訊息 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, customizing
- query interceptors [WCF Data Services]
ms.assetid: 24b9df1b-b54b-4795-a033-edf333675de6
ms.openlocfilehash: 8cc8bdcf776befafba967ee2649a6ada789d07c5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91194358"
---
# <a name="how-to-intercept-data-service-messages-wcf-data-services"></a><span data-ttu-id="ba9de-102">如何：攔截資料服務訊息 (WCF 資料服務)</span><span class="sxs-lookup"><span data-stu-id="ba9de-102">How to: Intercept Data Service Messages (WCF Data Services)</span></span>

<span data-ttu-id="ba9de-103">使用 WCF Data Services 時，您可以攔截要求訊息，以便將自訂邏輯加入至作業。</span><span class="sxs-lookup"><span data-stu-id="ba9de-103">With WCF Data Services, you can intercept request messages so that you can add custom logic to an operation.</span></span> <span data-ttu-id="ba9de-104">若要攔截訊息，您可以特別使用資料服務中的屬性化方法。</span><span class="sxs-lookup"><span data-stu-id="ba9de-104">To intercept a message, you use specially attributed methods in the data service.</span></span> <span data-ttu-id="ba9de-105">如需詳細資訊，請參閱 [攔截](interceptors-wcf-data-services.md)器。</span><span class="sxs-lookup"><span data-stu-id="ba9de-105">For more information, see [Interceptors](interceptors-wcf-data-services.md).</span></span>  
  
 <span data-ttu-id="ba9de-106">本主題中的範例使用 Northwind 範例資料服務。</span><span class="sxs-lookup"><span data-stu-id="ba9de-106">The example in this topic uses the Northwind sample data service.</span></span> <span data-ttu-id="ba9de-107">這項服務會在您完成 [WCF Data Services 快速入門](quickstart-wcf-data-services.md)時建立。</span><span class="sxs-lookup"><span data-stu-id="ba9de-107">This service is created when you complete the [WCF Data Services quickstart](quickstart-wcf-data-services.md).</span></span>  
  
### <a name="to-define-a-query-interceptor-for-the-orders-entity-set"></a><span data-ttu-id="ba9de-108">定義 Orders 實體集的查詢攔截器</span><span class="sxs-lookup"><span data-stu-id="ba9de-108">To define a query interceptor for the Orders entity set</span></span>  
  
1. <span data-ttu-id="ba9de-109">在 Northwind 資料服務專案中，開啟 Northwind.svc 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba9de-109">In the Northwind data service project, open the Northwind.svc file.</span></span>  
  
2. <span data-ttu-id="ba9de-110">在 `Northwind` 類別的字碼頁中，加入下列 `using` 陳述式 (在 Visual Basic 中是 `Imports`)。</span><span class="sxs-lookup"><span data-stu-id="ba9de-110">In the code page for the `Northwind` class, add the following `using` statement (`Imports` in Visual Basic).</span></span>  
  
     [!code-csharp[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#usinglinqexpressions)]
     [!code-vb[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#usinglinqexpressions)]  
  
3. <span data-ttu-id="ba9de-111">在 `Northwind` 類別中，定義名為 `OnQueryOrders` 的服務作業方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ba9de-111">In the `Northwind` class, define a service operation method named `OnQueryOrders` as follows:</span></span>  
  
     [!code-csharp[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#queryinterceptordef)]
     [!code-vb[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#queryinterceptordef)]  
  
### <a name="to-define-a-change-interceptor-for-the-products-entity-set"></a><span data-ttu-id="ba9de-112">定義 Products 實體集的變更攔截器</span><span class="sxs-lookup"><span data-stu-id="ba9de-112">To define a change interceptor for the Products entity set</span></span>  
  
1. <span data-ttu-id="ba9de-113">在 Northwind 資料服務專案中，開啟 Northwind.svc 檔案。</span><span class="sxs-lookup"><span data-stu-id="ba9de-113">In the Northwind data service project, open the Northwind.svc file.</span></span>  
  
2. <span data-ttu-id="ba9de-114">在 `Northwind` 類別中，定義名為 `OnChangeProducts` 的服務作業方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ba9de-114">In the `Northwind` class, define a service operation method named `OnChangeProducts` as follows:</span></span>  
  
     [!code-csharp[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#changeinterceptordef)]
     [!code-vb[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#changeinterceptordef)]  
  
## <a name="example"></a><span data-ttu-id="ba9de-115">範例</span><span class="sxs-lookup"><span data-stu-id="ba9de-115">Example</span></span>  

 <span data-ttu-id="ba9de-116">這個範例定義 `Orders` 實體集的查詢攔截器方法，傳回 Lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="ba9de-116">This example defines a query interceptor method for the `Orders` entity set that returns a lambda expression.</span></span> <span data-ttu-id="ba9de-117">這個運算式包含的委派，可根據具有特定連絡人名稱的相關 `Orders`，篩選要求的 `Customers`。</span><span class="sxs-lookup"><span data-stu-id="ba9de-117">This expression contains a delegate that filters the requested `Orders` based on related `Customers` that have a specific contact name.</span></span> <span data-ttu-id="ba9de-118">名稱會根據要求的使用者依序判斷。</span><span class="sxs-lookup"><span data-stu-id="ba9de-118">The name is in turn determined based on the requesting user.</span></span> <span data-ttu-id="ba9de-119">這個範例假設資料服務裝載於使用 WCF，並已啟用驗證的 ASP.NET Web 應用程式內。</span><span class="sxs-lookup"><span data-stu-id="ba9de-119">This example assumes that the data service is hosted within an ASP.NET Web application that uses WCF, and that authentication is enabled.</span></span> <span data-ttu-id="ba9de-120"><xref:System.Web.HttpContext> 類別會用來擷取目前要求的原則。</span><span class="sxs-lookup"><span data-stu-id="ba9de-120">The <xref:System.Web.HttpContext> class is used to retrieve the principle of the current request.</span></span>  
  
 [!code-csharp[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#queryinterceptor)]
 [!code-vb[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#queryinterceptor)]  
  
## <a name="example"></a><span data-ttu-id="ba9de-121">範例</span><span class="sxs-lookup"><span data-stu-id="ba9de-121">Example</span></span>  

 <span data-ttu-id="ba9de-122">這個範例定義 `Products` 實體集的變更攔截器方法。</span><span class="sxs-lookup"><span data-stu-id="ba9de-122">This example defines a change interceptor method for the `Products` entity set.</span></span> <span data-ttu-id="ba9de-123">這個方法會驗證 <xref:System.Data.Services.UpdateOperations.Add> 或 <xref:System.Data.Services.UpdateOperations.Change> 作業服務的輸入，如果停售的產品進行變更，將會引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ba9de-123">This method validates input to the service for an <xref:System.Data.Services.UpdateOperations.Add> or <xref:System.Data.Services.UpdateOperations.Change> operation and raises an exception if a change is being made to a discontinued product.</span></span> <span data-ttu-id="ba9de-124">同時產品的刪除動作也會遭到封鎖而成為不支援的作業。</span><span class="sxs-lookup"><span data-stu-id="ba9de-124">It also blocks the deletion of products as an unsupported operation.</span></span>  
  
 [!code-csharp[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#changeinterceptor)]
 [!code-vb[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#changeinterceptor)]  
  
## <a name="see-also"></a><span data-ttu-id="ba9de-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ba9de-125">See also</span></span>

- [<span data-ttu-id="ba9de-126">作法：定義服務作業</span><span class="sxs-lookup"><span data-stu-id="ba9de-126">How to: Define a Service Operation</span></span>](how-to-define-a-service-operation-wcf-data-services.md)
- [<span data-ttu-id="ba9de-127">定義 WCF 資料服務</span><span class="sxs-lookup"><span data-stu-id="ba9de-127">Defining WCF Data Services</span></span>](defining-wcf-data-services.md)
