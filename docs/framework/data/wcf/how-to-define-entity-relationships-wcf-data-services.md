---
title: 如何：定義實體關聯性 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, changing data
ms.assetid: cc255524-1534-4fae-b83c-250933d5a72b
ms.openlocfilehash: dec22f2f1e1d259e341100bce2b99d71540797db
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91150631"
---
# <a name="how-to-define-entity-relationships-wcf-data-services"></a>如何：定義實體關聯性 (WCF 資料服務)

當您在 WCF Data Services 中加入新的實體時，不會自動定義新實體與相關實體之間的任何關聯性。 您可以建立和變更實體執行個體之間的關聯性，而且可以讓用戶端程式庫在資料服務中反映這些變更。 如需詳細資訊，請參閱 [更新資料服務](updating-the-data-service-wcf-data-services.md)。  
  
 本主題中的範例使用 Northwind 範例資料服務和自動產生的用戶端資料服務類別。 此服務和用戶端資料類別會在您完成 [WCF Data Services 快速入門](quickstart-wcf-data-services.md)時建立。  
  
## <a name="example"></a>範例  

 下列範例會建立一個新的物件執行個體，然後呼叫 <xref:System.Data.Services.Client.DataServiceContext.AddRelatedObject%2A> 的 <xref:System.Data.Services.Client.DataServiceContext> 方法，在內容中建立項目與相關訂單的連結。 呼叫 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 方法時，會將 HTTP POST 訊息傳送至資料服務。  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrderAuto](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addorderdetailtoorderauto)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrderAuto](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addorderdetailtoorderauto)]  
  
## <a name="example"></a>範例  

 下列範例示範如何使用 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A> 方法將 `Order_Details` 物件加入至相關的 `Orders` 物件 (包含特定 `Products` 物件的參考)。 <xref:System.Data.Services.Client.DataServiceContext.AddLink%2A> 和 <xref:System.Data.Services.Client.DataServiceContext.SetLink%2A> 方法可定義關聯性。 此範例中也會明確設定 `Order_Details` 物件的導覽屬性。  
  
 [!code-csharp[Astoria Northwind Client#AddOrderDetailToOrder](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addorderdetailtoorder)]
 [!code-vb[Astoria Northwind Client#AddOrderDetailToOrder](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addorderdetailtoorder)]  
  
## <a name="see-also"></a>另請參閱

- [WCF 資料服務用戶端程式庫](wcf-data-services-client-library.md)
- [作法：新增、修改和刪除實體](how-to-add-modify-and-delete-entities-wcf-data-services.md)
