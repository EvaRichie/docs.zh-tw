---
title: 作法：建立單向合約
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 85084cd9-31cc-4e95-b667-42ef01336622
ms.openlocfilehash: 7f0285ba4824ac842b3644d0834782139fd90657
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268686"
---
# <a name="how-to-create-a-one-way-contract"></a>作法：建立單向合約

本主題說明的基本步驟可用來建立使用單向合約的方法。 這類方法會從用戶端叫用 Windows Communication Foundation (WCF) 服務的作業，但不預期會有回復。 例如，您可以使用此合約類型，將通知發行給許多訂閱者。 您也可以在建立雙工 (雙向) 合約時使用單向合約，以供用戶端與伺服器彼此各自進行通訊，並方便任何一方初始化對另一方的呼叫。 這麼做可以特別允許伺服器對用戶端進行單向呼叫，而用戶端會將此呼叫視為事件。 如需指定單向方法的詳細資訊，請參閱 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性與 <xref:System.ServiceModel.OperationContractAttribute> 類別。  
  
 如需有關為雙工合約建立用戶端應用程式的詳細資訊，請參閱 [如何：使用 One-Way 和 Request-Reply 合約存取服務](how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)。 如需實用的範例，請參閱 [單向](../samples/one-way.md) 範例。  
  
### <a name="to-create-a-one-way-contract"></a>若要建立單向合約  
  
1. 將 <xref:System.ServiceModel.ServiceContractAttribute> 類別套用至用來定義服務要實作之方法的介面，以建立服務合約。  
  
2. 指出介面中可供用戶端叫用的方法，方法是將 <xref:System.ServiceModel.OperationContractAttribute> 類別套用到這些方法上。  
  
3. 將 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性設為 `true`，以便將不得包含輸出的作業 (沒有傳回值，也沒有 out 或 ref 參數) 指定為單向。 請注意，帶有 <xref:System.ServiceModel.OperationContractAttribute> 類別的作業預設都會滿足要求-回覆合約，因為 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性會預設為 `false`。 因此如果您希望方法使用單向合約，就必須明確地將屬性值指定為 `true`。  
  
## <a name="example"></a>範例  

 下列程式碼範例定義包含數個單向方法的服務合約。 所有的方法都具有單向合約，除了 `Equals` 以外，因為它會預設為要求-回覆，並傳回結果。  
  
 [!code-csharp[S_Service_Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [設計與實作服務](../designing-and-implementing-services.md)
- [如何：定義服務合約](../how-to-define-a-wcf-service-contract.md)
- [工作階段](../samples/session.md)
- [作法：建立雙面合約](how-to-create-a-duplex-contract.md)
