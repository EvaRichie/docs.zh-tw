---
title: 使用追蹤來疑難排解應用程式
ms.date: 03/30/2017
ms.assetid: 8851adde-c3c2-4391-9523-d8eb831490af
ms.openlocfilehash: 62f2240831dd33bdaf78655199aad75b7e29c59c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293568"
---
# <a name="using-tracking-to-troubleshoot-applications"></a>使用追蹤來疑難排解應用程式

Windows Workflow Foundation (WF) 可讓您追蹤工作流程的相關資訊，以提供 Windows Workflow Foundation 應用程式或服務執行的詳細資料。 Windows Workflow Foundation 的主機可以在工作流程實例執行期間，捕捉工作流程事件。 如果您的工作流程產生錯誤或例外狀況，您可以使用 Windows Workflow Foundation 追蹤詳細資料來疑難排解其處理。  
  
## <a name="troubleshooting-a-wf-using-wf-tracking"></a>使用 WF 追蹤疑難排解 WF  

 若要偵測 Windows Workflow Foundation 活動處理中的錯誤，您可以使用追蹤設定檔來啟用追蹤，以查詢錯誤的 <xref:System.Activities.Tracking.ActivityStateRecord> 狀態。 下列程式碼中指定對應的查詢。  
  
```xml  
<activityStateQueries>  
              <activityStateQuery activityName="*">  
                <states>  
                  <state name="Faulted" />  
                </states>  
              </activityStateQuery>  
 </activityStateQueries>  
```  
  
 如果傳播錯誤，並在錯誤處理常式 (例如 <xref:System.Activities.Statements.TryCatch> 活動) 中處理該錯誤，則可使用 <xref:System.Activities.Tracking.FaultPropagationRecord> 偵測到此情形。 <xref:System.Activities.Tracking.FaultPropagationRecord> 會指出錯誤的來源活動，以及錯誤處理常式的名稱。 <xref:System.Activities.Tracking.FaultPropagationRecord>包含錯誤的錯誤詳細資料，其形式為錯誤的例外狀況堆疊。 <xref:System.Activities.Tracking.FaultPropagationRecord>下列範例會顯示訂閱的查詢。  
  
```xml  
<faultPropagationQueries>  
              <faultPropagationQuery faultSourceActivityName ="*" faultHandlerActivityName="*"/>  
 </faultPropagationQueries>  
```  
  
 如果未在工作流程中處理錯誤，會導致工作流程執行個體出現未處理的例外狀況，而且該工作流程執行個體會中止。 若要了解未處理例外狀況的詳細資訊，追蹤設定檔必須查詢具有 `state name="UnhandledException"` 的工作流程執行個體記錄，如下列範例所指定。  
  
```xml  
<workflowInstanceQueries>  
              <workflowInstanceQuery>  
                <states>  
                  <state name="UnhandledException" />  
                </states>  
              </workflowInstanceQuery>  
</workflowInstanceQueries>  
```  
  
 當工作流程實例遇到未處理的例外狀況時， <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord> 如果已啟用 Windows Workflow Foundation 追蹤，就會發出物件。  
  
 這個追蹤記錄包含例外狀況堆疊形式的錯誤詳細資料。 它包含錯誤來源的詳細資料 (例如，發生錯誤的活動) ，並導致未處理的例外狀況。若要從 Windows Workflow Foundation 訂閱錯誤事件，請藉由新增追蹤參與者來啟用追蹤。 使用會查詢 `ActivityStateQuery (state="Faulted")`、<xref:System.Activities.Tracking.FaultPropagationRecord> 和 `WorkflowInstanceQuery (state="UnhandledException")` 的追蹤設定檔來設定這個參與者。  
  
 如果使用 ETW 追蹤參與者啟用追蹤，會將錯誤事件發出至 ETW 工作階段。 使用事件檢視器即可檢視這些事件。 您可以在分析通道中 **事件檢視器 >應用程式和服務記錄檔->Microsoft >Windows->應用程式伺服器-應用程式** ] 節點下找到此功能。  
  
## <a name="see-also"></a>另請參閱

- [Windows Server App Fabric 監視](/previous-versions/appfabric/ee677251(v=azure.10))
- [使用 App Fabric 監視應用程式](/previous-versions/appfabric/ee677276(v=azure.10))
