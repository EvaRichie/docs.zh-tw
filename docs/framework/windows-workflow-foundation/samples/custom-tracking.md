---
title: 自訂追蹤
ms.date: 03/30/2017
ms.assetid: 2d191c9f-62f4-4c63-92dd-cda917fcf254
ms.openlocfilehash: 87f72359e16b4268d77148ec16a626c2bac5751c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557028"
---
# <a name="custom-tracking"></a>自訂追蹤
這個範例示範如何建立自訂追蹤參與者，以及將追蹤資料的內容寫入主控台中。 此外，範例還會示範如何發出其中填入使用者定義資料的 <xref:System.Activities.Tracking.CustomTrackingRecord> 物件。 主控台式追蹤參與者會使用程式碼中建立的追蹤設定檔物件，篩選工作流程所發出的 <xref:System.Activities.Tracking.TrackingRecord> 物件。

## <a name="sample-details"></a>範例詳細資料
 Windows Workflow Foundation (WF) 提供追蹤基礎結構來追蹤工作流程實例的執行。 追蹤執行階段會實作工作流程執行個體，以發出與工作流程生命週期相關的事件、工作流程活動的事件，以及自訂追蹤事件。 下表詳細說明追蹤基礎結構的主要元件。

|元件|描述|
|---------------|-----------------|
|追蹤執行階段|提供基礎結構以發出追蹤記錄。|
|追蹤參與者|耗用追蹤記錄。 .NET Framework 4 隨附的追蹤參與者，會將追蹤記錄寫入為 Windows (ETW) 事件的事件追蹤。|
|追蹤設定檔|篩選機制，可讓追蹤參與者訂閱從工作流程執行個體發出之追蹤記錄的子集。|

 下表詳細說明工作流程執行階段發出的追蹤記錄。

|追蹤記錄|描述|
|---------------------|-----------------|
|工作流程執行個體追蹤記錄。|描述在工作流程執行個體的生命週期。 例如，當工作流程開始或完成時，就會發出執行個體記錄。|
|活動狀態追蹤記錄。|活動執行詳細資訊。 這些記錄會指出工作流程活動的狀態，例如活動排程時間、活動完成時間，或是擲回錯誤的時間。|
|書籤繼續記錄。|只要工作流程執行個體中的書籤繼續，就會發出。|
|自訂追蹤記錄。|工作流程作者可建立自訂追蹤記錄，並在自訂活動中發出這些記錄。|

 追蹤參與者可使用追蹤設定檔訂閱所發出 <xref:System.Activities.Tracking.TrackingRecord> 物件的子集。 追蹤設定檔包含追蹤查詢，這些查詢允許訂閱特殊追蹤記錄類型。 追蹤設定檔可在程式碼或組態中指定。

### <a name="custom-tracking-participant"></a>自訂追蹤參與者
 追蹤參與者 API 允許以使用者提供的追蹤者來擴充追蹤執行階段，可包含自訂邏輯以處理工作流程執行階段發出的 <xref:System.Activities.Tracking.TrackingRecord> 物件。

 為了撰寫追蹤參與者，使用者必須實作 <xref:System.Activities.Tracking.TrackingParticipant>。 具體而言，<xref:System.Activities.Tracking.TrackingParticipant.Track%2A> 方法必須由自訂參與者實作。 這個方法會在工作流程執行階段發出 <xref:System.Activities.Tracking.TrackingRecord> 時呼叫。

```csharp
public abstract class TrackingParticipant
{
    protected TrackingParticipant();

    public virtual TrackingProfile TrackingProfile { get; set; }
    public abstract void Track(TrackingRecord record, TimeSpan timeout);
}
```

 完整的追蹤參與者會在 ConsoleTrackingParticipant.cs 檔案中執行。 下列程式碼範例是 <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> 自訂追蹤參與者的方法。

```csharp
protected override void Track(TrackingRecord record, TimeSpan timeout)
{
    ...
    WorkflowInstanceRecord workflowInstanceRecord = record as WorkflowInstanceRecord;
    if (workflowInstanceRecord != null)
    {
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,
            " Workflow InstanceID: {0} Workflow instance state: {1}",
            record.InstanceId, workflowInstanceRecord.State));
    }

    ActivityStateRecord activityStateRecord = record as ActivityStateRecord;
    if (activityStateRecord != null)
    {
        IDictionary<String, object> variables = activityStateRecord.Variables;
        StringBuilder vars = new StringBuilder();

        if (variables.Count > 0)
        {
            vars.AppendLine("\n\tVariables:");
            foreach (KeyValuePair<string, object> variable in variables)
            {
                vars.AppendLine(String.Format(
                    "\t\tName: {0} Value: {1}", variable.Key, variable.Value));
            }
        }
        Console.WriteLine(String.Format(CultureInfo.InvariantCulture,
            " :Activity DisplayName: {0} :ActivityInstanceState: {1} {2}",
                activityStateRecord.Activity.Name, activityStateRecord.State,
            ((variables.Count > 0) ? vars.ToString() : String.Empty)));
    }

    CustomTrackingRecord customTrackingRecord = record as CustomTrackingRecord;

    if ((customTrackingRecord != null) && (customTrackingRecord.Data.Count > 0))
    {
        ...
    }
    Console.WriteLine();

}
```

 下列程式碼範例會將主控台參與者加入至工作流程啟動程式。

```csharp
ConsoleTrackingParticipant customTrackingParticipant = new ConsoleTrackingParticipant()
{
    ...
    // The tracking profile is set here, refer to Program.CS
...
}

WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());
invoker.Extensions.Add(customTrackingParticipant);
```

### <a name="emitting-custom-tracking-records"></a>發出自訂追蹤記錄
 這個範例還會示範從自訂工作流程活動發出 <xref:System.Activities.Tracking.CustomTrackingRecord> 物件的能力。

- 除了會建立 <xref:System.Activities.Tracking.CustomTrackingRecord> 物件之外，還會在其中填入希望隨記錄發出的使用者定義資料。

- 藉 <xref:System.Activities.Tracking.CustomTrackingRecord> 由呼叫的 track 方法發出 <xref:System.Activities.ActivityContext> 。

 下列範例示範如何在自訂活動內發出 <xref:System.Activities.Tracking.CustomTrackingRecord> 物件。

```csharp
// Create the Custom Tracking Record
CustomTrackingRecord customRecord = new CustomTrackingRecord("OrderIn")
{
    Data =
    {
        {"OrderId", 200},
        {"OrderDate", "20 Aug 2001"}
    }
};

// Emit custom tracking record
context.Track(customRecord);
```

#### <a name="to-use-this-sample"></a>若要使用這個範例

1. 使用 Visual Studio 2010，開啟 CustomTrackingSample .sln 方案檔。

2. 若要建置此方案，請按 CTRL+SHIFT+B。

3. 若要執行此方案，請按下 CTRL+F5。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\CustomTracking`  
  
## <a name="see-also"></a>另請參閱

- [AppFabric 監控範例](/previous-versions/appfabric/ff383407(v=azure.10))
