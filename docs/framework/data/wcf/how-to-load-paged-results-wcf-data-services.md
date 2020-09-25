---
title: 如何：載入已分頁的結果 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, deferred content
- WCF Data Services, loading data
ms.assetid: bb786ea4-f3ef-4ad3-9a41-3a0b7feb6a1f
ms.openlocfilehash: c49e0b170743332d6cc3aaef7e5503eabab52d97
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91182788"
---
# <a name="how-to-load-paged-results-wcf-data-services"></a>如何：載入已分頁的結果 (WCF 資料服務)

WCF Data Services 可讓資料服務限制單一回應摘要中傳回的實體數目。 執行此功能時，摘要中的最後一個項目會包含下一頁資料的連結。 呼叫於執行 <xref:System.Data.Services.Client.QueryOperationResponse%601.GetContinuation%2A> 時傳回之 <xref:System.Data.Services.Client.QueryOperationResponse%601> 的 <xref:System.Data.Services.Client.DataServiceQuery%601> 方法即可取得下一頁資料的 URI。 接著會使用此物件代表的 URI 來載入下一頁結果。 如需詳細資訊，請參閱 [載入延遲的內容](loading-deferred-content-wcf-data-services.md)。  
  
 本主題中的範例使用 Northwind 範例資料服務和自動產生的用戶端資料服務類別。 此服務和用戶端資料類別會在您完成 [WCF Data Services 快速入門](quickstart-wcf-data-services.md)時建立。  
  
## <a name="example"></a>範例  

 本範例使用 `do…while` 迴圈，從資料服務的分頁結果載入 `Customers` 實體。  
  
 [!code-csharp[Astoria Northwind Client#GetCustomersPaged](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getcustomerspaged)]
 [!code-vb[Astoria Northwind Client#GetCustomersPaged](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getcustomerspaged)]  
  
## <a name="example"></a>範例  

 本範例會隨每個 `Orders` 實體傳回相關的 `Customers` 實體，並使用 `do…while` 迴圈載入 `Customers` 實體頁，同時使用巢狀的 `while` 迴圈從資料服務載入相關 `Orders` 實體的頁面。  
  
 [!code-csharp[Astoria Northwind Client#GetCustomersPagedNested](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getcustomerspagednested)]
 [!code-vb[Astoria Northwind Client#GetCustomersPagedNested](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getcustomerspagednested)]  
  
## <a name="see-also"></a>另請參閱

- [載入延後內容](loading-deferred-content-wcf-data-services.md)
- [作法：載入相關實體](how-to-load-related-entities-wcf-data-services.md)
