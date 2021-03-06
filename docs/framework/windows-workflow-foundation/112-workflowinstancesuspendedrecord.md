---
title: 112 - WorkflowInstanceSuspendedRecord
ms.date: 03/30/2017
ms.assetid: bc825c7c-8c90-48f7-9336-9a978a8246c6
ms.openlocfilehash: 697dfe18fdb4ae6c05ae758077c1c2d9198e053c
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265813"
---
# <a name="112---workflowinstancesuspendedrecord"></a>112 - WorkflowInstanceSuspendedRecord

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|Id|112|  
|關鍵字|EndToEndMonitoring、Troubleshooting、HealthMonitoring、WFTracking|  
|層級|資訊|  
|通路|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>描述  

 此事件是當工作流程執行個體發出 WorkflowInstanceSuspended Record 時，由 ETW 追蹤參與者發出。  
  
## <a name="message"></a>訊息  

 TrackRecord = WorkflowInstanceSuspendedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, Reason = %5, Annotations = %6, ProfileName = %7  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|工作流程的執行個體 ID。|  
|RecordNumber|xs:long|發出之記錄的序號。|  
|EventTime|xs:dateTime|發出事件時的 UTC 時間。|  
|ActivityDefinitionId|xs:string|工作流程中根活動的名稱。|  
|原因|xs:string|工作流程暫止的原因。|  
|註解|xs:string|加入至此事件中的附註。  這些值會以 a 格式儲存在 xml 元素中 \<items> \< item  name = "annotationName" type="System.String"> \</item> \</items> 。  如果未指定任何批註，則字串會包含 \<items/> 。 ETW 事件大小會受到 ETW 緩衝區大小或 ETW 事件的最大承載所限制。 如果事件大小超過 ETW 限制，則會捨棄注釋並以 ... 取代注釋值來截斷事件。 \<items> \</items>|  
|ProfileName|xs:string|造成發送這個事件的名稱或追蹤設定檔。|  
|HostReference|xs:string|若為 Web 主控服務，此欄位會唯一識別 Web 階層架構中的服務。  其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName ' 範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
