---
title: <workflowRuntime>
ms.date: 03/30/2017
ms.assetid: 304c70fa-78d1-4d0f-b89f-0ca23d734c6f
ms.openlocfilehash: d12656b77fa219080382603fd04a542d2fa9064a
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399079"
---
# \<workflowRuntime>
<xref:System.Workflow.Runtime.WorkflowRuntime>針對裝載以工作流程為基礎的 Windows Communication Foundation （WCF）服務，指定實例的設定。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<workflowRuntime>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<workflowRuntime cachedInstanceExpiration="TimeSpan"
                 enablePerformanceCounters="Boolean"
                 name="String"
                 validateOnCreate="Boolean">
  <commonParameters>
    <add name="String"
         value="String" />
  </commonParameters>
  <services>
    <add type="String" />
  </services>
</workflowRuntime>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|cachedInstanceExpiration|選擇性 <xref:System.TimeSpan> 值，指定工作流程執行個體在遭到強制卸載或中止之前，能以閒置狀態存留在記憶體中的最長期間。 如果工作流程執行階段具有會執行 unloadOnIdle 的 `PersistenceService`，則會忽略此屬性。|  
|enablePerformanceCounters|選擇性布林值，指定是否啟用效能計數器。 效能計數器會提供各種工作流程的相關統計資料，但是當工作流程執行階段引擎啟動和工作流程執行個體正在執行時，會對效能帶來負面影響。 預設值是 `true`。|  
|NAME|字串，包含工作流程執行階段引擎的名稱。 名稱用於輸出以識別此執行階段及可能在系統執行的其他執行階段，例如在效能計數器中。<br /><br /> 預設值是空字串。|  
|validateOnCreate|選擇性布林值，指定當 WorkflowServiceHost 開啟時，是否會發生工作流程定義驗證。  當此屬性設定為 `true` 時，每次呼叫 `WorkflowServiceHost.Open` 都會執行一次工作流程驗證。 如果發現驗證錯誤，則會擲回 <xref:System.Workflow.ComponentModel.Compiler.WorkflowValidationFailedException> 錯誤。<br /><br /> 當此屬性設定為 `false` 時，將不會執行工作流程定義驗證。<br /><br /> 這個屬性的預設值為 `true`。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|commonParameters|服務所使用的一般參數集合。 這個集合通常會包含資料庫連線字串，這個字串可能會由長期服務所共用。|  
|服務|要加入至 <xref:System.Workflow.Runtime.WorkflowRuntime> 引擎之服務的集合。 此項目的型別為 <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>。  集合中所指定的服務會由工作流程執行階段引擎初始化，並在呼叫適當的 <xref:System.Workflow.Runtime.WorkflowRuntime> 建構函式時新增至其服務中。 因此，集合中所指定的服務必須遵循有關其建構函式之簽章的特定規則。 如需相關資訊，請參閱 <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<behavior>](behavior-of-endpointbehaviors.md)|指定行為項目。|  
  
## <a name="remarks"></a>備註  
 如需使用設定檔控制 <xref:System.Workflow.Runtime.WorkflowRuntime> Windows Workflow Foundation 主應用程式之物件行為的詳細資訊，請參閱[工作流程設定檔](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90))。  
  
## <a name="example"></a>範例  
  
```xml  
<serviceBehaviors>
   <behavior name="ServiceBehavior">
      <workflowRuntime name="WorkflowServiceHostRuntime"
                       validateOnCreate="true"
                       enablePerformanceCounters="true">
         <commonParameters>
            <add name="ConnectionString" value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;" />
            <add name="EnableRetries" value="True" />
         </commonParameters>
         <services>
             <add type="NetFx.Checkin.Scenario.WorkflowServices.WorkflowBasedServices.Common.TestPersistenceService.FilePersistenceService, NetFx.Checkin.Scenario.WorkflowServices.WorkflowBasedServices.Common"/>
         </services>
      </workflowRuntime>
   </behavior>
</serviceBehaviors>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.WorkflowRuntimeElement>
- <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>
- <xref:System.Workflow.Runtime.WorkflowRuntime>
- [工作流程組態檔](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90))
