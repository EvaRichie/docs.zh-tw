---
title: <activityStateQuery>
ms.date: 03/30/2017
ms.topic: reference
ms.assetid: 9f8c3e4f-e2e3-4402-9760-03bf918ece7b
ms.openlocfilehash: 5d3c35589330ab5bed5f89c0dafac006b9e3af55
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70398943"
---
# \<activityStateQuery>
代表查詢，可用來追蹤活動的生命週期之變更，這些活動將構成工作流程執行個體。 例如，您可能想要追蹤在工作流程實例中完成「傳送電子郵件」活動的每次。 追蹤參與者必須要具備這個查詢，才能訂閱活動狀態記錄物件。 可供訂閱的狀態可於 ActivityStates 中指定。  
  
 如需追蹤設定檔查詢的詳細資訊，請參閱[追蹤設定檔](../../../windows-workflow-foundation/tracking-profiles.md)。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.ServiceModel>**](system-servicemodel-of-workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<tracking>**](tracking.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<trackingProfile>**](trackingprofile.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<workflow>**](workflow.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<activityStateQueries>**](activitystatequeries.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<activityStateQuery>**  
  
## <a name="syntax"></a>語法  
  
```xml
<tracking>
  <trackingProfile name="Name">
    <workflow>
      <activityStateQueries>
        <activityStateQuery activityName="String" />
        <arguments>
          <argument name="String"/>
        </arguments>
        <states>
          <state name="String"/>
        </states>
        <variables>
          <variable name="String"/>
        </variables>
      </activityStateQueries>
    </workflow>
  </trackingProfile>
</tracking>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|activityName|字串，這個字串會指定活動的名稱，以篩選 <xref:System.Activities.Tracking.ActivityStateRecord> 執行個體。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<arguments>](arguments.md)|與此活動查詢相關聯之引數的集合。|  
|[\<states>](states.md)|組態元素的集合，其中包含應該發出追蹤記錄之已訂閱活動的狀態。|  
|[\<states>](states.md)|與此活動查詢相關聯之變數的集合。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<faultPropagationQuery>](faultpropagationquery.md)|代表組態項目的清單，這個清單可用來追蹤由父活動取消子活動的要求。 追蹤參與者必須要具備這個查詢，才能訂閱取消要求記錄物件。|  
  
## <a name="remarks"></a>備註  
 ActivityStateQuery 的一項獨特功能，就是可在追蹤工作流程的執行時擷取資料。 它可在存取追蹤記錄後期執行時，提供額外的內容。 您可以使用 [\<arguments>](arguments.md) 、和專案， [\<states>](states.md) [\<states>](states.md) 從工作流程中的任何活動中解壓縮任何變數或引數。 下列範例示範活動狀態查詢，此查詢會在發出活動的 `Closed` 追蹤記錄時擷取變數及引數。 只能使用 ActivityStateRecord 來解壓縮變數和引數，因此會使用在追蹤設定檔內訂閱 [\<activityStateQuery>](activitystatequery.md) 。  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <variables>  
    <variable name="FromAddress"/>  
  </variables>  
  <arguments>  
    <argument name="Result"/>  
  </arguments>  
</activityStateQuery>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Activities.Tracking.Configuration.ActivityStateQueryElement?displayProperty=nameWithType>
- <xref:System.Activities.Tracking.ActivityStateQuery?displayProperty=nameWithType>
- [工作流程追蹤及追蹤](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [追蹤設定檔](../../../windows-workflow-foundation/tracking-profiles.md)
