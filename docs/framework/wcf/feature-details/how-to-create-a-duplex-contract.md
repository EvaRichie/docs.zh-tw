---
title: HOW TO：建立雙工合約
description: 瞭解如何建立雙工合約，讓 WCF 用戶端和伺服器彼此獨立進行通訊。 可以起始對另一個的呼叫。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- duplex contracts [WCF]
ms.assetid: 500a75b6-998a-47d5-8e3b-24e3aba2a434
ms.openlocfilehash: 9320e5b36b8faba3602fbe1df1b95c05dcc7fa7e
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247087"
---
# <a name="how-to-create-a-duplex-contract"></a>HOW TO：建立雙工合約
本主題說明的基本步驟可用來建立使用雙工 (雙向) 合約的方法。 雙工合約可供用戶端與伺服器彼此各自進行通訊，方便任何一方初始化對另一方的呼叫。 雙工合約是 Windows Communication Foundation （WCF）服務可用的三種訊息模式之一。 其他兩種訊息模式分別是單向和要求-回覆。 雙工合約是由用戶端和伺服器之間的兩個單向合約組成，而且不需要相互關聯方法呼叫。 當您的服務必須查詢用戶端以獲得更多資訊，或是明確地在用戶端上引發事件時，請使用這種合約。 如需建立雙工合約之用戶端應用程式的詳細資訊，請參閱[如何：使用雙工合約來存取服務](how-to-access-services-with-a-duplex-contract.md)。 如需實用範例，請參閱[雙工](../samples/duplex.md)範例。  
  
### <a name="to-create-a-duplex-contract"></a>若要建立雙工合約  
  
1. 建立可組成雙工合約伺服器端的介面。  
  
2. 將 <xref:System.ServiceModel.ServiceContractAttribute> 類別套用到介面。  
  
     [!code-csharp[S_WS_DualHttp#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#3)]
     [!code-vb[S_WS_DualHttp#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#3)]  
  
3. 在介面中宣告方法簽章。  
  
4. 將 <xref:System.ServiceModel.OperationContractAttribute> 類別套用到每個必須是公用合約一部分的方法簽章上。  
  
5. 建立可定義作業集合 (供服務在用戶端上加以叫用) 的回呼介面。  
  
     [!code-csharp[S_WS_DualHttp#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#4)]
     [!code-vb[S_WS_DualHttp#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#4)]  
  
6. 在回呼介面中宣告方法簽章。  
  
7. 將 <xref:System.ServiceModel.OperationContractAttribute> 類別套用到每個必須是公用合約一部分的方法簽章上。  
  
8. 將主要介面中的 <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A> 屬性設為回呼介面的型別，以將兩個介面連接至雙工合約。  
  
### <a name="to-call-methods-on-the-client"></a>若要在用戶端上呼叫方法  
  
1. 在服務的主要合約實作中，宣告回呼介面的變數。  
  
2. 將變數設為由 <xref:System.ServiceModel.OperationContext.GetCallbackChannel%2A> 類別之 <xref:System.ServiceModel.OperationContext> 方法傳回的物件參考。  
  
     [!code-csharp[S_WS_DualHttp#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#1)]
     [!code-vb[S_WS_DualHttp#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#1)]  
  
     [!code-csharp[S_WS_DualHttp#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#2)]
     [!code-vb[S_WS_DualHttp#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#2)]  
  
3. 呼叫回呼介面定義的方法。  
  
## <a name="example"></a>範例  
 下列程式碼範例會示範雙工通訊。 服務合約包含可往前與往後的服務作業。 用戶端合約包含可報告自身位置的服務作業。  
  
 [!code-csharp[S_WS_DualHttp#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#5)]
 [!code-vb[S_WS_DualHttp#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#5)]  
  
- 套用 <xref:System.ServiceModel.ServiceContractAttribute> 和 <xref:System.ServiceModel.OperationContractAttribute> 屬性可自動產生 Web 服務描述語言 (WSDL) 格式的服務合約定義。  
  
- 使用[System.servicemodel 中繼資料公用程式工具（Svcutil.exe）](../servicemodel-metadata-utility-tool-svcutil-exe.md)來抓取 WSDL 檔案和（選擇性）用戶端的程式碼和設定。  
  
- 您必須保護公開雙工服務的端點安全。 當服務收到雙工訊息時，會查看該傳入訊息中的 ReplyTo 項目，以判斷傳送回覆的位置。 如果通道不安全，那麼未受信任的用戶端可能會傳送惡意訊息，其中包含目標電腦的 ReplyTo，而導致該目標電腦發生阻絕服務。 如果是一般的要求-回覆訊息，這根本不是問題，因為電腦會忽略 ReplyTo 並且在原始傳入訊息所用的通道上傳送回應。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [如何：使用雙面合約存取服務](how-to-access-services-with-a-duplex-contract.md)
- [雙工](../samples/duplex.md)
- [設計與實作服務](../designing-and-implementing-services.md)
- [如何：定義服務合約](../how-to-define-a-wcf-service-contract.md)
- [本次](../samples/session.md)
