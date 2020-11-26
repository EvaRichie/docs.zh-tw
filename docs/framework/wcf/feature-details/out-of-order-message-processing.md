---
title: 不按照順序的訊息處理
ms.date: 03/30/2017
ms.assetid: 33fc62a5-5d59-461c-a37a-0e1b51ac763d
ms.openlocfilehash: 7a5042e390231498de4f98abfc0e863cba199943
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96248001"
---
# <a name="out-of-order-message-processing"></a>不按照順序的訊息處理

工作流程服務可能取決於訊息以特定順序傳送。 工作流程服務包含一個或多個 <xref:System.ServiceModel.Activities.Receive> 活動，各個 <xref:System.ServiceModel.Activities.Receive> 活動會預期某個特定的訊息。 要是沒有特定的傳輸傳遞保證，用戶端傳送的訊息可能會延遲，因而傳遞的順序可能不符合工作流程服務的預期。 實作不要求訊息以特定順序傳送的工作流程服務，通常會使用平行活動來完成。 若為更複雜的應用程式通訊協定，工作流程很快就會變得非常複雜。  Windows Communication Foundation (WCF) 的非順序訊息處理功能，可讓您建立這類工作流程，而不需要所有複雜的嵌套平行活動。 只有支援的通道（例如 WCF MSMQ 系結）才支援不按照順序的訊息處理 <xref:System.ServiceModel.Channels.ReceiveContext> 。  
  
## <a name="enabling-out-of-order-message-processing"></a>啟用不按照順序的訊息處理  

 若要啟用不按照順序的訊息處理，請將 WorkflowService 上的 <xref:System.ServiceModel.Activities.WorkflowService.AllowBufferedReceive%2A> 屬性設定為 `true`。 下列範例示範如何利用程式碼設定 <xref:System.ServiceModel.Activities.WorkflowService.AllowBufferedReceive%2A> 屬性。  
  
```csharp  
// Code: Opt-in to Buffered Receive processing...  
WorkflowService service = new WorkflowService  
{  
    Name="MyService",  
    Body = workflow,  
    AllowBufferedReceive = true  
};  
```  
  
 您也可以利用 XAML，將 `AllowBufferedReceive` 屬性套用到工作流程服務，如下列範例所示。  
  
```xaml  
// Xaml: Opt-in to Buffered Receive processing...  
<WorkflowService AllowBufferedReceive="True">  
   <!--the actual children activities -->  
</Sequence>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Channels.ReceiveContext>
- [工作流程服務](workflow-services.md)
- [佇列和可靠的工作階段](queues-and-reliable-sessions.md)
