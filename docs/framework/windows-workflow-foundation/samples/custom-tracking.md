---
title: 自訂追蹤
ms.date: 03/30/2017
ms.assetid: 2d191c9f-62f4-4c63-92dd-cda917fcf254
ms.openlocfilehash: 3d125c59196cb2a7d33961e0f271aab8c5663a50
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96234566"
---
# <a name="custom-tracking"></a><span data-ttu-id="4ca1d-102">自訂追蹤</span><span class="sxs-lookup"><span data-stu-id="4ca1d-102">Custom Tracking</span></span>

<span data-ttu-id="4ca1d-103">這個範例示範如何建立自訂追蹤參與者，以及將追蹤資料的內容寫入主控台中。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-103">This sample demonstrates how to create a custom tracking participant and write the contents of the tracking data to console.</span></span> <span data-ttu-id="4ca1d-104">此外，範例還會示範如何發出其中填入使用者定義資料的 <xref:System.Activities.Tracking.CustomTrackingRecord> 物件。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-104">In addition, the sample demonstrates how to emit <xref:System.Activities.Tracking.CustomTrackingRecord> objects populated with user defined data.</span></span> <span data-ttu-id="4ca1d-105">主控台式追蹤參與者會使用程式碼中建立的追蹤設定檔物件，篩選工作流程所發出的 <xref:System.Activities.Tracking.TrackingRecord> 物件。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-105">The console-based tracking participant filters the <xref:System.Activities.Tracking.TrackingRecord> objects emitted by the workflow using a tracking profile object created in code.</span></span>

## <a name="sample-details"></a><span data-ttu-id="4ca1d-106">範例詳細資料</span><span class="sxs-lookup"><span data-stu-id="4ca1d-106">Sample Details</span></span>

 <span data-ttu-id="4ca1d-107">Windows Workflow Foundation (WF) 提供追蹤基礎結構來追蹤工作流程實例的執行。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-107">Windows Workflow Foundation (WF) provides a tracking infrastructure to track execution of a workflow instance.</span></span> <span data-ttu-id="4ca1d-108">追蹤執行階段會實作工作流程執行個體，以發出與工作流程生命週期相關的事件、工作流程活動的事件，以及自訂追蹤事件。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-108">The tracking runtime implements a workflow instance to emit events related to the workflow lifecycle, events from workflow activities and custom tracking events.</span></span> <span data-ttu-id="4ca1d-109">下表詳細說明追蹤基礎結構的主要元件。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-109">The following table details the primary components of the tracking infrastructure.</span></span>

|<span data-ttu-id="4ca1d-110">元件</span><span class="sxs-lookup"><span data-stu-id="4ca1d-110">Component</span></span>|<span data-ttu-id="4ca1d-111">描述</span><span class="sxs-lookup"><span data-stu-id="4ca1d-111">Description</span></span>|
|---------------|-----------------|
|<span data-ttu-id="4ca1d-112">追蹤執行階段</span><span class="sxs-lookup"><span data-stu-id="4ca1d-112">Tracking runtime</span></span>|<span data-ttu-id="4ca1d-113">提供基礎結構以發出追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-113">Provides the infrastructure to emit tracking records.</span></span>|
|<span data-ttu-id="4ca1d-114">追蹤參與者</span><span class="sxs-lookup"><span data-stu-id="4ca1d-114">Tracking participants</span></span>|<span data-ttu-id="4ca1d-115">耗用追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-115">Consumes the tracking records.</span></span> <span data-ttu-id="4ca1d-116">.NET Framework 4 隨附的追蹤參與者，會將追蹤記錄寫入為 Windows (ETW) 事件的事件追蹤。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-116">.NET Framework 4 ships with a tracking participant that writes tracking records as Event Tracing for Windows (ETW) events.</span></span>|
|<span data-ttu-id="4ca1d-117">追蹤設定檔</span><span class="sxs-lookup"><span data-stu-id="4ca1d-117">Tracking profile</span></span>|<span data-ttu-id="4ca1d-118">篩選機制，可讓追蹤參與者訂閱從工作流程執行個體發出之追蹤記錄的子集。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-118">A filtering mechanism that allows a tracking participant to subscribe for a subset of the tracking records emitted from a workflow instance.</span></span>|

 <span data-ttu-id="4ca1d-119">下表詳細說明工作流程執行階段發出的追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-119">The following table details the tracking records that the workflow runtime emits.</span></span>

|<span data-ttu-id="4ca1d-120">追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="4ca1d-120">Tracking Record</span></span>|<span data-ttu-id="4ca1d-121">描述</span><span class="sxs-lookup"><span data-stu-id="4ca1d-121">Description</span></span>|
|---------------------|-----------------|
|<span data-ttu-id="4ca1d-122">工作流程執行個體追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-122">Workflow instance tracking records.</span></span>|<span data-ttu-id="4ca1d-123">描述在工作流程執行個體的生命週期。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-123">Describes the life cycle of the workflow instance.</span></span> <span data-ttu-id="4ca1d-124">例如，當工作流程開始或完成時，就會發出執行個體記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-124">For example, an instance record is emitted when the workflow starts or completes.</span></span>|
|<span data-ttu-id="4ca1d-125">活動狀態追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-125">Activity state Tracking Records.</span></span>|<span data-ttu-id="4ca1d-126">活動執行詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-126">Details activity execution.</span></span> <span data-ttu-id="4ca1d-127">這些記錄會指出工作流程活動的狀態，例如活動排程時間、活動完成時間，或是擲回錯誤的時間。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-127">These records indicate the state of a workflow activity such as when an activity is scheduled or when the activity completes or when a fault is thrown.</span></span>|
|<span data-ttu-id="4ca1d-128">書籤繼續記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-128">Bookmark resumption record.</span></span>|<span data-ttu-id="4ca1d-129">只要工作流程執行個體中的書籤繼續，就會發出。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-129">Emitted whenever a bookmark within a workflow instance is resumed.</span></span>|
|<span data-ttu-id="4ca1d-130">自訂追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-130">Custom Tracking Records.</span></span>|<span data-ttu-id="4ca1d-131">工作流程作者可建立自訂追蹤記錄，並在自訂活動中發出這些記錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-131">A workflow author can create Custom Tracking Records and emit them within the custom activity.</span></span>|

 <span data-ttu-id="4ca1d-132">追蹤參與者可使用追蹤設定檔訂閱所發出 <xref:System.Activities.Tracking.TrackingRecord> 物件的子集。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-132">The tracking participant subscribes for a subset of the emitted <xref:System.Activities.Tracking.TrackingRecord> objects using tracking profiles.</span></span> <span data-ttu-id="4ca1d-133">追蹤設定檔包含追蹤查詢，這些查詢允許訂閱特殊追蹤記錄類型。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-133">A tracking profile contains tracking queries that allow subscribing for a particular tracking record type.</span></span> <span data-ttu-id="4ca1d-134">追蹤設定檔可在程式碼或組態中指定。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-134">Tracking profiles can be specified in code or in configuration.</span></span>

### <a name="custom-tracking-participant"></a><span data-ttu-id="4ca1d-135">自訂追蹤參與者</span><span class="sxs-lookup"><span data-stu-id="4ca1d-135">Custom Tracking Participant</span></span>

 <span data-ttu-id="4ca1d-136">追蹤參與者 API 允許以使用者提供的追蹤者來擴充追蹤執行階段，可包含自訂邏輯以處理工作流程執行階段發出的 <xref:System.Activities.Tracking.TrackingRecord> 物件。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-136">The tracking participant API allows extension of the tracking runtime with a user provided tracking participant that can include custom logic to handle <xref:System.Activities.Tracking.TrackingRecord> objects emitted by the workflow runtime.</span></span>

 <span data-ttu-id="4ca1d-137">為了撰寫追蹤參與者，使用者必須實作 <xref:System.Activities.Tracking.TrackingParticipant>。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-137">To write a tracking participant the user must implement <xref:System.Activities.Tracking.TrackingParticipant>.</span></span> <span data-ttu-id="4ca1d-138">具體而言，<xref:System.Activities.Tracking.TrackingParticipant.Track%2A> 方法必須由自訂參與者實作。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-138">Specifically, the <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> method has to be implemented by the custom participant.</span></span> <span data-ttu-id="4ca1d-139">這個方法會在工作流程執行階段發出 <xref:System.Activities.Tracking.TrackingRecord> 時呼叫。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-139">This method is called when a <xref:System.Activities.Tracking.TrackingRecord> is emitted by the workflow runtime.</span></span>

```csharp
public abstract class TrackingParticipant
{
    protected TrackingParticipant();

    public virtual TrackingProfile TrackingProfile { get; set; }
    public abstract void Track(TrackingRecord record, TimeSpan timeout);
}
```

 <span data-ttu-id="4ca1d-140">完整的追蹤參與者會在 ConsoleTrackingParticipant.cs 檔案中執行。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-140">The complete tracking participant is implemented in the ConsoleTrackingParticipant.cs file.</span></span> <span data-ttu-id="4ca1d-141">下列程式碼範例是 <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> 自訂追蹤參與者的方法。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-141">The following code example is the <xref:System.Activities.Tracking.TrackingParticipant.Track%2A> method for the custom tracking participant.</span></span>

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

 <span data-ttu-id="4ca1d-142">下列程式碼範例會將主控台參與者加入至工作流程啟動程式。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-142">The following code example adds the console participant to the workflow invoker.</span></span>

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

### <a name="emitting-custom-tracking-records"></a><span data-ttu-id="4ca1d-143">發出自訂追蹤記錄</span><span class="sxs-lookup"><span data-stu-id="4ca1d-143">Emitting Custom Tracking Records</span></span>

 <span data-ttu-id="4ca1d-144">這個範例還會示範從自訂工作流程活動發出 <xref:System.Activities.Tracking.CustomTrackingRecord> 物件的能力。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-144">This sample also demonstrates the ability to emit <xref:System.Activities.Tracking.CustomTrackingRecord> objects from a custom workflow activity:</span></span>

- <span data-ttu-id="4ca1d-145">除了會建立 <xref:System.Activities.Tracking.CustomTrackingRecord> 物件之外，還會在其中填入希望隨記錄發出的使用者定義資料。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-145">The <xref:System.Activities.Tracking.CustomTrackingRecord> objects are created and populated with user-defined data that is desired to be emitted with the record.</span></span>

- <span data-ttu-id="4ca1d-146">藉 <xref:System.Activities.Tracking.CustomTrackingRecord> 由呼叫的 track 方法發出 <xref:System.Activities.ActivityContext> 。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-146">The <xref:System.Activities.Tracking.CustomTrackingRecord> is emitted by calling the track method of the <xref:System.Activities.ActivityContext>.</span></span>

 <span data-ttu-id="4ca1d-147">下列範例示範如何在自訂活動內發出 <xref:System.Activities.Tracking.CustomTrackingRecord> 物件。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-147">The following example demonstrates how to emit <xref:System.Activities.Tracking.CustomTrackingRecord> objects within a custom activity.</span></span>

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

#### <a name="to-use-this-sample"></a><span data-ttu-id="4ca1d-148">若要使用這個範例</span><span class="sxs-lookup"><span data-stu-id="4ca1d-148">To use this sample</span></span>

1. <span data-ttu-id="4ca1d-149">使用 Visual Studio 2010，開啟 CustomTrackingSample .sln 方案檔。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-149">Using Visual Studio 2010, open the CustomTrackingSample.sln solution file.</span></span>

2. <span data-ttu-id="4ca1d-150">若要建置此方案，請按 CTRL+SHIFT+B。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-150">To build the solution, press CTRL+SHIFT+B.</span></span>

3. <span data-ttu-id="4ca1d-151">若要執行此方案，請按下 CTRL+F5。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-151">To run the solution, press CTRL+F5.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ca1d-152">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-152">The samples may already be installed on your computer.</span></span> <span data-ttu-id="4ca1d-153">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-153">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="4ca1d-154">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-154">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="4ca1d-155">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="4ca1d-155">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\CustomTracking`  
  
## <a name="see-also"></a><span data-ttu-id="4ca1d-156">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4ca1d-156">See also</span></span>

- <span data-ttu-id="4ca1d-157">[AppFabric 監控範例](/previous-versions/appfabric/ff383407(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="4ca1d-157">[AppFabric Monitoring Samples](/previous-versions/appfabric/ff383407(v=azure.10))</span></span>
