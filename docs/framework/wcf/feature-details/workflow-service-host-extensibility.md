---
title: 工作流程服務主機擴充性
ms.date: 03/30/2017
ms.assetid: c0e8f7bb-cb13-49ec-852f-b85d7c23972f
ms.openlocfilehash: 67a7830c564cabafb9441e86eb0d87164d854ee5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96258448"
---
# <a name="workflow-service-host-extensibility"></a>工作流程服務主機擴充性

[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 提供用於裝載工作流程服務的 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 類別。 若您要在 Managed 應用程式或 Windows 服務中自我裝載工作流程服務，則可使用此類別。 此類別還可在透過網際網路資訊服務 (IIS) 或 Windows Process Activation Service (WAS) 裝載工作流程時使用。 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 類別會提供擴充點，讓您加入自訂擴充、變更閒置行為，以及裝載非服務工作流程 (不使用訊息傳遞活動的工作流程)。  
  
## <a name="workflow-service-host-extensions"></a>工作流程服務主機延伸模組  

 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 包含 <xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A> 類型的 <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager> 屬性，可提供將延伸模組加入至 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的方法。 使用 <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager.Add%2A> 方法可為每個工作流程服務執行個體加入延伸模組。 建立或從持續性存放區載入工作流程服務執行個體時，會呼叫指定的委派建立新的延伸模組。 使用 <xref:System.Activities.Hosting.WorkflowInstanceExtensionManager.Add%2A> 方法可為每一部工作流程服務主機加入延伸模組，每個延伸模組執行個體可供所有工作流程服務執行個體共用。  
  
## <a name="react-to-unhandled-exceptions"></a>回應未處理的例外狀況  

 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> 可讓您指定工作流程服務內發生未處理的例外狀況時，所採取的動作。 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior.Action%2A> 屬性會指定其中一個 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction> 值：  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Abandon> – 中止工作流程服務執行個體。  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.AbandonAndSuspend> – 回復到最後保存的狀態，並且暫停工作流程服務執行個體。 只有在工作流程至少已保存一次時，才會發生此情況。 否則，就會中止工作流程執行個體。  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Cancel> – 取消執行個體。  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionAction.Terminate> – 終止執行個體。  
  
 此行為可以在程式碼中設定，如下列範例所示。  
  
```csharp  
host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.Abandon });  
```  
  
 此外，它也可以在組態檔中設定，如下列範例所示  
  
```xml
<behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
          <workflowUnhandledExceptionBehavior action="Abandon" />
        </behavior>  
      </serviceBehaviors>  
</behaviors>
```  
  
## <a name="hosting-non-service-workflows"></a>裝載非服務工作流程  

 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 可以用來裝載非服務工作流程，或者不是以 <xref:System.ServiceModel.Activities.Receive> 活動開始的工作流程，或不使用訊息傳遞活動的工作流程。 工作流程服務通常會以 <xref:System.ServiceModel.Activities.Receive> 活動開始。 當 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 接收工作流程服務的訊息時，如果尚未執行 (或已保存)，則會建立新的工作流程服務執行個體。 如果工作流程不是以接收活動開始，則無法藉由傳送訊息的方式啟動，因為沒有接收訊息的活動。 若要裝載非服務工作流程，請從 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 衍生類別，並且覆寫 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetInstanceId%2A>、<xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetCreationContext%2A> 和 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnResolveBookmark%2A>。 如果您要提供慣用的執行個體 ID，請覆寫 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetInstanceId%2A>。 覆寫 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnGetCreationContext%2A>，即可建立自訂的工作流程建立內容，或是填入現有 <xref:System.ServiceModel.Activities.WorkflowCreationContext> 的執行個體。 覆寫 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint.OnResolveBookmark%2A>，即可從傳入訊息手動擷取書籤。 如果您覆寫此方法，就必須在其主體中叫用 <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A>，以便回應傳送至 WorkflowHostingEndpoint 的訊息。 如果您沒有這樣做，最後可能會超過 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 限制。 在雙向合約中，您可以偵測由於用戶端無法接收回應所導致的 <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> 叫用失敗。 在單向合約中，您可能要等到超過 <xref:System.ServiceModel.Activities.WorkflowHostingResponseContext.SendResponse%2A> 節流閥限制之後，才能辨識無法呼叫 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> 的錯誤，但是卻為時已晚。 如需詳細資訊，請參閱 [WorkflowHostingEndpoint Resume 書簽](../../windows-workflow-foundation/samples/workflowhostingendpoint-resume-bookmark.md)以建立非服務工作流程的新實例、宣告服務合約，以定義建立新實例的作業。 建立作業應採用 IDictionary \<string, object> 來傳遞任何必要的工作流程參數。 此合約會由 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 衍生的類別以隱含方式實作。 裝載工作流程時，可呼叫 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>，將 <xref:System.ServiceModel.Activities.WorkflowServiceHost.AddServiceEndpoint%2A> 衍生類別的執行個體加入至主機，並且呼叫 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>。 若要建立工作流程的執行個體，請建立服務合約型別的 <xref:System.ServiceModel.ChannelFactory%601>，並且呼叫 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A>。 接著，您可以呼叫服務合約中定義的建立作業。  
  
## <a name="see-also"></a>另請參閱

- [工作流程服務](workflow-services.md)
- [傳訊活動](messaging-activities.md)
