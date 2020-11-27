---
title: 作法：與 WCF 端點交換佇列訊息
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 938e7825-f63a-4c3d-b603-63772fabfdb3
ms.openlocfilehash: 3f69286a2b4d4ec55f18931f9156c20a38da9c34
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265423"
---
# <a name="how-to-exchange-queued-messages-with-wcf-endpoints"></a>作法：與 WCF 端點交換佇列訊息

佇列可確保用戶端和 Windows Communication Foundation (WCF) 服務之間可進行可靠的訊息處理，即使服務在通訊時無法使用也是一樣。 下列程式示範如何在執行 WCF 服務時，使用標準佇列系結來確保用戶端與服務之間的持久通訊。  
  
 本節說明如何用於 <xref:System.ServiceModel.NetMsmqBinding> wcf 用戶端與 wcf 服務之間的佇列通訊。  
  
### <a name="to-use-queuing-in-a-wcf-service"></a>若要在 WCF 服務中使用佇列  
  
1. 使用以 <xref:System.ServiceModel.ServiceContractAttribute>標記的介面定義服務合約。 在屬於服務合約部分的介面中標示作業為 <xref:System.ServiceModel.OperationContractAttribute> 並指定它們為單向，因為此方法不用傳回任何回應。 下列程式碼提供範例服務合約以及其作業定義。  
  
     [!code-csharp[S_Msmq_Transacted#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#1)]
     [!code-vb[S_Msmq_Transacted#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#1)]  
  
2. 當服務合約通過使用者定義型別，您必須為這些型別定義資料合約。 下列程式碼示範兩份資料合約：`PurchaseOrder` 和 `PurchaseOrderLineItem`。 這兩個型別定義了傳送至服務的資料  (請注意，定義這類資料合約的類別也定義許多方法。 這些方法不被視為資料合約的部分。 只有以 <xref:System.Runtime.Serialization.DataMemberAttribute> 屬性宣告的成員才屬於資料合約的部分)。  
  
     [!code-csharp[S_Msmq_Transacted#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#2)]
     [!code-vb[S_Msmq_Transacted#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#2)]  
  
3. 實作在類別中之介面所定義的服務合約方法。  
  
     [!code-csharp[S_Msmq_Transacted#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#3)]
     [!code-vb[S_Msmq_Transacted#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#3)]  
  
     請注意，<xref:System.ServiceModel.OperationBehaviorAttribute> 放置在 `SubmitPurchaseOrder` 方法上。 其用意是指定必須在異動內呼叫此作業，而且異動會隨著方法完成而自動完成。  
  
4. 使用 <xref:System.Messaging> 來建立交易式佇列。 您可以選擇使用 Microsoft Message Queuing (MSMQ) Microsoft Management Console (MMC) 建立佇列。 若是這樣，請確定您建立異動式佇列。  
  
     [!code-csharp[S_Msmq_Transacted#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#4)]
     [!code-vb[S_Msmq_Transacted#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#4)]  
  
5. 在組態中定義 <xref:System.ServiceModel.Description.ServiceEndpoint>，以指定服務位址，並使用標準 <xref:System.ServiceModel.NetMsmqBinding> 繫結。 如需使用 WCF 設定的詳細資訊，請參閱設定 [wcf 服務](../configuring-services.md)。  

6. 使用從佇列讀取訊息並加以處理的 `OrderProcessing` 建立 <xref:System.ServiceModel.ServiceHost> 服務的主機。 開啟服務主機來提供服務。 顯示一則訊息，指示使用者按任意鍵終止服務。 呼叫 `ReadLine` 以等待按鍵動作，隨後關閉服務。  
  
     [!code-csharp[S_Msmq_Transacted#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#6)]
     [!code-vb[S_Msmq_Transacted#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#6)]  
  
### <a name="to-create-a-client-for-the-queued-service"></a>若要建立佇列服務的用戶端  
  
1. 下列範例示範如何執行裝載應用程式，並使用 Svcutil.exe 工具來建立 WCF 用戶端。  
  
    ```console
    svcutil http://localhost:8000/ServiceModelSamples/service  
    ```  
  
2. 在組態中定義 <xref:System.ServiceModel.Description.ServiceEndpoint>，藉以指定位址並使用標準 <xref:System.ServiceModel.NetMsmqBinding> 繫結，如下列範例所示。  

3. 建立要寫入至交易式佇列的交易範圍、呼叫作業 `SubmitPurchaseOrder` 並關閉 WCF 用戶端，如下列範例所示。  
  
     [!code-csharp[S_Msmq_Transacted#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/client.cs#8)]
     [!code-vb[S_Msmq_Transacted#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/client.vb#8)]  
  
## <a name="example"></a>範例  

 以下內容顯示本範例所囊括的服務程式碼、裝載應用程式、App.config 檔案和用戶端程式碼。  
  
 [!code-csharp[S_Msmq_Transacted#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#9)]
 [!code-vb[S_Msmq_Transacted#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#9)]  
  
 [!code-csharp[S_Msmq_Transacted#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#10)]
 [!code-vb[S_Msmq_Transacted#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#10)]  

 [!code-csharp[S_Msmq_Transacted#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/client.cs#12)]
 [!code-vb[S_Msmq_Transacted#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/client.vb#12)]  

## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.NetMsmqBinding>
- [交易 MSMQ 繫結](../samples/transacted-msmq-binding.md)
- [WCF 中的佇列](queuing-in-wcf.md)
- [作法：與 WCF 端點和訊息佇列應用程式交換訊息](how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- [Windows Communication Foundation 至訊息佇列](../samples/wcf-to-message-queuing.md)
- [安裝訊息佇列 (MSMQ)](../samples/installing-message-queuing-msmq.md)
- [訊息佇列至 Windows Communication Foundation](../samples/message-queuing-to-wcf.md)
- [訊息佇列上的訊息安全性](../samples/message-security-over-message-queuing.md)
