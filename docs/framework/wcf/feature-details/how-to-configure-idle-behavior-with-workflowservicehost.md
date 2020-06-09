---
title: HOW TO：以 WorkflowServiceHost 設定閒置行為
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1bb93652-d687-46ff-bff6-69ecdcf97437
ms.openlocfilehash: 8b9fa36408d5f2bc5445ebeccba61f71417935e7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599122"
---
# <a name="how-to-configure-idle-behavior-with-workflowservicehost"></a>HOW TO：以 WorkflowServiceHost 設定閒置行為
工作流程遇到必須由外部刺激繼續執行的書籤時，例如工作流程執行個體正在等候訊息使用 <xref:System.ServiceModel.Activities.Receive> 活動加以傳遞時，工作流程就會進入閒置狀態。 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior> 是一種行為，可讓您指定從服務執行個體進入閒置到此執行個體保存或卸載的間隔時間。 其中包含兩個屬性，可用來設定這些時間範圍。 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A> 會指定從工作流程服務執行個體進入閒置到工作流程服務執行個體保存的時間範圍。 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> 會指定從工作流程服務執行個體進入閒置到工作流程服務執行個體卸載的時間範圍，而卸載的意義是將執行個體保存到執行個體儲存區並從記憶體中移除。 本主題說明如何設定組態檔中的 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior> 。  
  
### <a name="to-configure-workflowidlebehavior"></a>若要設定 WorkflowIdleBehavior  
  
1. 將 <`workflowIdle`> 元素新增至 <> 專案中的 <> 專案， `behavior` `serviceBehaviors` 如下列範例所示。  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowIdle timeToUnload="0:05:0" timeToPersist="0:04:0"/>
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
     `timeToUnload` 屬性會指定從工作流程服務執行個體進入閒置到工作流程服務卸載的時間間隔。 `timeToPersist` 屬性會指定從工作流程服務執行個體進入閒置到工作流程服務保存的時間間隔。 `timeToUnload` 的預設值為 1 分鐘。 `timeToPersist` 的預設值為 <xref:System.TimeSpan.MaxValue>。 如果您想要將閒置的執行個體保留在記憶體中，但保存它們以提供健全度，請設定下列值，讓 `timeToPersist` < `timeToUnload`。 如果您想要防止系統卸載閒置的執行個體，請將 `timeToUnload` 設定為 <xref:System.TimeSpan.MaxValue>。 如需的詳細資訊 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior> ，請參閱[工作流程服務主機](workflow-service-host-extensibility.md)擴充性  
  
    > [!NOTE]
    > 上述組態範例會使用簡化的組態。 如需詳細資訊，請參閱[簡化](../simplified-configuration.md)的設定。  
  
### <a name="to-change-idle-behavior-in-code"></a>若要在程式碼中變更閒置行為  
  
- 下列範例會以程式設計方式變更保存和卸載之前等候的時間。  
  
     [!code-csharp[Wf_SvcHost_Idle_persist#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/wf_svchost_idle_persist/cs/source.cs#1)]
     [!code-vb[Wf_SvcHost_Idle_persist#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/wf_svchost_idle_persist/vb/source.vb#1)]  
  
## <a name="see-also"></a>請參閱

- [工作流程服務主機擴充性](workflow-service-host-extensibility.md)
- [簡化設定](../simplified-configuration.md)
- [工作流程服務](workflow-services.md)
