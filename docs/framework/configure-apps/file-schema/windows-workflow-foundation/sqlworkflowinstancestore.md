---
title: <sqlWorkflowInstanceStore>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 8a4e4214-fc51-4f4d-b968-0427c37a9520
ms.openlocfilehash: 56a44fdb62062903ca3ad00f8105a66ccab02cca
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79151958"
---
# \<sqlWorkflowInstanceStore>
可讓您設定 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 功能的服務行為，該功能支援將工作流程服務執行個體的狀態資訊保存在 SQL Server 2005 或 SQL Server 2008 資料庫中。 如需這項功能的詳細資訊，請參閱[SQL 工作流程實例存放區](../../../windows-workflow-foundation/sql-workflow-instance-store.md)。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.ServiceModel>**](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<sqlWorkflowInstanceStore>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <sqlWorkflowInstanceStore connectionStringName="String"
                                hostLockRenewalPeriod="TimeSpan"
                                instanceCompletionAction="DeleteNothing/DeleteAll"
                                instanceEncodingAction="None/GZip"
                                instanceLockedExceptionAction="NoRetry/BasicRetry/AggressiveRetry"
                                runnableInstancesDetectionPeriod="TimeSpan" />
    </behavior>
  </serviceBehaviors>
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|connectionString|字串，其中包含用來連接至基礎持續性資料庫的連接字串。|  
|connectionStringName|字串，其中包含連接至資料庫伺服器的具名連接字串。 命名連接字串的範例為 "DefaultConnectionString"。|  
|hostLockRenewalPeriod|指定時間週期的 Timespan 值，在此時間週期內，主機必須更新執行個體上的鎖定。 如果主機未在指定的時間週期內更新鎖定，執行個體就會解除鎖定，且可讓另一個主機執行個體選取。<br /><br /> 卸載工作流程表示會同時保存該工作流程。 如果將這個屬性設定為零，則會在工作流程閒置之後，立刻保留及卸載工作流程執行個體。 將這個屬性設定為 TimeSpan.MaxValue 可有效地停用卸載作業。 閒置的工作流程執行個體永遠不會卸載。|  
|instanceCompletionAction|這個值會指定工作流程執行個體是否會在工作流程執行個體完成後保留在持續性存放區中，還是會在該時間點刪除。 這個值的型別為 <xref:System.Activities.DurableInstancing.InstanceCompletionAction>。<br /><br /> 列舉動作包括在執行個體完成其作業時，刪除持續性存放區中的執行個體資料，或者不刪除持續性存放區中的執行個體資料。<br /><br /> 若在完成後仍保留執行個體，會導致持續性資料庫快速成長，因而影響資料庫的效能。 請設定資料庫清除原則來定期刪除這些記錄，以確保資料庫的效能層級能夠持續滿足您的效能需求。|  
|instanceEncodingOption|這個選用值會指定將資訊儲存在持續性存放區之前，是否要使用 GZip 演算法壓縮執行個體狀態資訊。 這個值的型別為 <xref:System.Activities.DurableInstancing.InstanceEncodingOption>。 這個屬性的可能值為 <xref:System.Activities.DurableInstancing.InstanceEncodingOption.None> ，指定不壓縮，而則 <xref:System.Activities.DurableInstancing.InstanceEncodingOption.GZip> 指定實例資料會壓縮並使用 gzip 演算法。|  
|instanceLockedExceptionAction|這個值可在執行個體目前已由其他主機鎖定，而主機嘗試鎖定執行個體時，指定回應擲回例外狀況所發生的動作。 這個值的型別為 <xref:System.Activities.DurableInstancing.InstanceLockedExceptionAction>。<br /><br /> 此欄位可使用的選項包括：[None]、[Basic Retry] 及 [Aggressive Retry]。 預設值為 None。 下列清單提供這三種選項的描述：<br /><br /> -   無。 服務主機不會嘗試鎖定執行個體，以及傳遞 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 至呼叫端。<br />-基本重試。 服務主機以線性重試間隔，重新嘗試鎖定執行個體，並將例外狀況傳遞至位於順序結尾的呼叫端。<br />-積極重試。 服務主機以指數遞增延遲，重新嘗試鎖定執行個體，並將 <xref:System.Runtime.DurableInstancing.InstanceLockedException> 傳遞至位於順序結尾的呼叫端。|  
|runnableInstancesDetectionPeriod||  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<behavior>的\<serviceBehaviors>](behavior-of-servicebehaviors-of-workflow.md)|指定行為項目。|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>
- <xref:System.ServiceModel.Activities.Configuration.SqlWorkflowInstanceStoreElement>
- <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>
- [SQL 工作流程執行個體存放區](../../../windows-workflow-foundation/sql-workflow-instance-store.md)
