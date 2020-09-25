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
# <a name="how-to-intercept-data-service-messages-wcf-data-services"></a>如何：攔截資料服務訊息 (WCF 資料服務)

使用 WCF Data Services 時，您可以攔截要求訊息，以便將自訂邏輯加入至作業。 若要攔截訊息，您可以特別使用資料服務中的屬性化方法。 如需詳細資訊，請參閱 [攔截](interceptors-wcf-data-services.md)器。  
  
 本主題中的範例使用 Northwind 範例資料服務。 這項服務會在您完成 [WCF Data Services 快速入門](quickstart-wcf-data-services.md)時建立。  
  
### <a name="to-define-a-query-interceptor-for-the-orders-entity-set"></a>定義 Orders 實體集的查詢攔截器  
  
1. 在 Northwind 資料服務專案中，開啟 Northwind.svc 檔案。  
  
2. 在 `Northwind` 類別的字碼頁中，加入下列 `using` 陳述式 (在 Visual Basic 中是 `Imports`)。  
  
     [!code-csharp[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#usinglinqexpressions)]
     [!code-vb[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#usinglinqexpressions)]  
  
3. 在 `Northwind` 類別中，定義名為 `OnQueryOrders` 的服務作業方法，如下所示：  
  
     [!code-csharp[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#queryinterceptordef)]
     [!code-vb[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#queryinterceptordef)]  
  
### <a name="to-define-a-change-interceptor-for-the-products-entity-set"></a>定義 Products 實體集的變更攔截器  
  
1. 在 Northwind 資料服務專案中，開啟 Northwind.svc 檔案。  
  
2. 在 `Northwind` 類別中，定義名為 `OnChangeProducts` 的服務作業方法，如下所示：  
  
     [!code-csharp[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#changeinterceptordef)]
     [!code-vb[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#changeinterceptordef)]  
  
## <a name="example"></a>範例  

 這個範例定義 `Orders` 實體集的查詢攔截器方法，傳回 Lambda 運算式。 這個運算式包含的委派，可根據具有特定連絡人名稱的相關 `Orders`，篩選要求的 `Customers`。 名稱會根據要求的使用者依序判斷。 這個範例假設資料服務裝載於使用 WCF，並已啟用驗證的 ASP.NET Web 應用程式內。 <xref:System.Web.HttpContext> 類別會用來擷取目前要求的原則。  
  
 [!code-csharp[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#queryinterceptor)]
 [!code-vb[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#queryinterceptor)]  
  
## <a name="example"></a>範例  

 這個範例定義 `Products` 實體集的變更攔截器方法。 這個方法會驗證 <xref:System.Data.Services.UpdateOperations.Add> 或 <xref:System.Data.Services.UpdateOperations.Change> 作業服務的輸入，如果停售的產品進行變更，將會引發例外狀況。 同時產品的刪除動作也會遭到封鎖而成為不支援的作業。  
  
 [!code-csharp[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#changeinterceptor)]
 [!code-vb[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#changeinterceptor)]  
  
## <a name="see-also"></a>另請參閱

- [作法：定義服務作業](how-to-define-a-service-operation-wcf-data-services.md)
- [定義 WCF 資料服務](defining-wcf-data-services.md)
