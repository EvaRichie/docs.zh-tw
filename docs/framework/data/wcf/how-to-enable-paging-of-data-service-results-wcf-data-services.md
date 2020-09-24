---
title: 如何：為資料服務結果啟用分頁功能 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- paging output [WCF Data Services]
ms.assetid: 9a316cbd-9612-4482-a541-a10bc78b2635
ms.openlocfilehash: 1c8bb8fe757c35f6096b139da6ca939b1ce1c283
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91150618"
---
# <a name="how-to-enable-paging-of-data-service-results-wcf-data-services"></a>如何：為資料服務結果啟用分頁功能 (WCF 資料服務)

WCF Data Services 可讓您限制資料服務查詢所傳回的實體數目。 當服務已初始化且可針對每個實體集分別設定服務時，分頁限制會定義於所呼叫的方法中。  
  
 啟用分頁時，摘要中的最後一個項目會包含下一頁資料的連結。 如需詳細資訊，請參閱設定 [資料服務](configuring-the-data-service-wcf-data-services.md)。  
  
 本主題顯示如何修改資料服務以啟用傳回之 `Customers` 和 `Orders` 實體集之分頁。 本主題中的範例使用 Northwind 範例資料服務。 這項服務會在您完成 [WCF Data Services 快速入門](quickstart-wcf-data-services.md)時建立。  
  
### <a name="how-to-enable-paging-of-returned-customers-and-orders-entity-sets"></a>如何啟用傳回之 Customers 和 Orders 實體集之分頁  
  
- 在資料服務的程式碼中，以下列程式碼取代 `InitializeService` 函數中的預留位置程式碼：  
  
     [!code-csharp[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind.svc.cs#dataserviceconfigpaging)]
     [!code-vb[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind.svc.vb#dataserviceconfigpaging)]  
  
## <a name="see-also"></a>另請參閱

- [載入延後內容](loading-deferred-content-wcf-data-services.md)
- [作法：載入分頁的結果](how-to-load-paged-results-wcf-data-services.md)
