---
title: <workflow>WCF 的
ms.date: 03/30/2017
ms.assetid: c0443eba-d3b4-4fae-886e-9878daf77691
ms.openlocfilehash: c6c9e14a4ad3d9713ae2d35d6ade20690e0c3575
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "69932784"
---
# <a name="workflow-of-wcf"></a>\<workflow>WCF 的
設定追蹤參與者，這些參與者會接聽執行階段直接發出的追蹤記錄並處理記錄，無論記錄的設定為何。 這包括寫入至特定的輸出 (例如檔案、主控台、ETW)、處理/彙總記錄，或任何其他可能需要的組合。  
  
 如需工作流程追蹤和追蹤參與者的詳細資訊，請參閱[工作流程追蹤和](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)追蹤[參與者](../../../windows-workflow-foundation/tracking-participants.md)。  
  
 \<system.serviceModel>  
\<tracking>  
\<participants>  
\<add>  
  
## <a name="syntax"></a>語法  
  
```xml  
<tracking>
  <participants>
    <add name="String"
         profileName="String"
         type="String" />
  </participants>
</tracking>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|元素|描述|  
|-------------|-----------------|  
|NAME|指定追蹤參與者名稱的字串。|  
|profileName|指定追蹤設定檔名稱的字串，該設定檔定義了追蹤參與者已訂閱的追蹤記錄。|  
|type|指定追蹤參與者型別的字串。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<participants>](../windows-workflow-foundation/participants.md)|追蹤參與者的清單。|  
  
## <a name="remarks"></a>備註  
 追蹤參與者是用來取得自工作流程發出的追蹤資料，然後將資料儲存至不同的媒體。 同樣地，追蹤記錄的任何後期處理也可在追蹤參與者之中完成。  
  
 多個追蹤參與者可同時使用追蹤事件。 每個追蹤參與者都可以與不同的追蹤設定檔相關聯。  
  
 此處提供標準的追蹤參與者，可將追蹤記錄寫入至 ETW 工作階段。 透過在設定檔中加入特定追蹤的行為，您可以設定工作流程服務上的參與者。 啟用 ETW 追蹤參與者可在事件檢視器中檢視追蹤記錄。 如果不符合需求，您也可以寫入自訂的追蹤參與者。  
  
## <a name="example"></a>範例  
 以下組態範例顯示在 Web.config 檔案中設定的標準 ETW 追蹤參與者。  
  
 ETW 追蹤參與者用來寫入追蹤記錄至 ETW 的提供者識別碼會定義於 `<diagnostics>` 區段。 追蹤參與者擁有與其相關聯的設定檔，以指定已經訂閱的追蹤記錄。 這是由 `profileName` 項目的 `<add>` 屬性所定義。 一旦這些定義完成，追蹤參與者就會加入至 `<etwTracking>` 服務行為。 如此會將選取的追蹤參與者加入至工作流程執行個體的擴充，因此，追蹤參與者可開始接收追蹤記錄。  
  
```xml  
<configuration>
  <system.web>
    <compilation targetFrameworkMoniker=".NETFramework,Version=v4.0" />
  </system.web>
  <system.serviceModel>
    <diagnostics etwProviderId="52A3165D-4AD9-405C-B1E8-7D9A257EAC9F" />
    <tracking>
      <participants>
        <add name="EtwTrackingParticipant"
             type="System.Activities.Tracking.EtwTrackingParticipant, System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"
             profileName="HealthMonitoring_Tracking_Profile" />
      </participants>
    </tracking>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <etwTracking profileName="Sample Tracking Profile" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
</configuration>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Activities.Tracking.Configuration.TrackingSection>
- <xref:System.ServiceModel.Activities.Description.EtwTrackingBehavior>
- <xref:System.ServiceModel.Activities.Configuration.EtwTrackingBehaviorElement>
- [工作流程追蹤及追蹤](../../../windows-workflow-foundation/workflow-tracking-and-tracing.md)
- [追蹤參與者](../../../windows-workflow-foundation/tracking-participants.md)
