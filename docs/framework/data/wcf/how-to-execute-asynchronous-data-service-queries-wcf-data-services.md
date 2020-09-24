---
title: 如何：執行非同步資料服務查詢 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, asynchronous operations
- asynchronous operations [WCF Data Services]
ms.assetid: 902a2dc1-d0e9-4b00-90a8-becc4cb1f6a7
ms.openlocfilehash: 84eb88695580598d41615653723c137d3f766a47
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91150605"
---
# <a name="how-to-execute-asynchronous-data-service-queries-wcf-data-services"></a>如何：執行非同步資料服務查詢 (WCF 資料服務)

您可以使用 WCF Data Services 用戶端程式庫，以非同步方式執行用戶端伺服器作業，例如執行查詢和儲存變更。 如需詳細資訊，請參閱 [非同步作業](asynchronous-operations-wcf-data-services.md)。  
  
> [!NOTE]
> 在必須於特定執行緒上叫用回呼的應用程式中，您必須明確地封送處理 <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 方法的執行。 如需詳細資訊，請參閱 [非同步作業](asynchronous-operations-wcf-data-services.md)。  
  
 本主題中的範例使用 Northwind 範例資料服務和自動產生的用戶端資料服務類別。 此服務和用戶端資料類別會在您完成 [WCF Data Services 快速入門](quickstart-wcf-data-services.md)時建立。  
  
## <a name="example"></a>範例  

 下列範例示範如何透過呼叫 <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> 方法啟動查詢來執行非同步查詢。 內嵌委派會呼叫 <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 方法以顯示查詢結果。  
  
 [!code-csharp[Astoria Northwind Client#ExecuteQueryAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#executequeryasync)]
 [!code-vb[Astoria Northwind Client#ExecuteQueryAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#executequeryasync)]  
  
## <a name="see-also"></a>另請參閱

- [WCF 資料服務用戶端程式庫](wcf-data-services-client-library.md)
