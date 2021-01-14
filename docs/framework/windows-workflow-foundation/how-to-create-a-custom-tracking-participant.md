---
title: 作法：建立自訂追蹤參與者
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1b612c7e-2381-4a7c-b07a-77030415f2a3
ms.openlocfilehash: 6fc8584b979c606a32e70e971be30a4bed89bdc2
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98190503"
---
# <a name="how-to-create-a-custom-tracking-participant"></a>作法：建立自訂追蹤參與者

工作流程追蹤會提供工作流程執行狀態的可見性。 工作流程執行階段會發出追蹤記錄，其中描述工作流程開發週期事件、活動開發週期事件、書籤繼續及錯誤。 這些追蹤記錄由追蹤參與者使用。 Windows Workflow Foundation (WF) 包含標準的追蹤參與者，可將追蹤記錄寫入為 Windows 的事件追蹤 (ETW) 事件。 如果不符合需求，您也可以寫入自訂的追蹤參與者。 本教學課程步驟描述如何建立擷取 `WriteLine` 活動輸出的自訂追蹤參與者和追蹤設定檔，以便向使用者顯示這些項目。  
  
## <a name="to-create-the-custom-tracking-participant"></a>建立自訂追蹤參與者  
  
1. 以滑鼠右鍵按一下 **方案總管** 中的 **[numberguessworkflowhost]** ，然後選擇 [**新增**]、[**類別**]。 `StatusTrackingParticipant`在 [**名稱**] 方塊中輸入，然後按一下 [**新增**]。  
  
2. 將下列 `using` (或 `Imports`) 陳述式加入至檔案最上方的其他 `using` (或 `Imports`) 陳述式。  
  
    ```vb  
    Imports System.Activities.Tracking  
    Imports System.IO  
    ```  
  
    ```csharp  
    using System.Activities.Tracking;  
    using System.IO;  
    ```  
  
3. 修改 `StatusTrackingParticipant` 類別，使其繼承 `TrackingParticipant`。  
  
    ```vb  
    Public Class StatusTrackingParticipant  
        Inherits TrackingParticipant  
  
    End Class  
    ```  
  
    ```csharp  
    class StatusTrackingParticipant : TrackingParticipant  
    {  
    }  
    ```  
  
4. 加入下列 `Track` 方法覆寫。 追蹤記錄有多種不同型別。 我們對於 `WriteLine` 活動的輸出感興趣，該輸出包含在活動追蹤記錄中。 如果 `TrackingRecord` 是 `ActivityTrackingRecord` 活動的 `WriteLine`，則 `Text` 的 `WriteLine` 會附加在工作流程中以 `InstanceId` 命名的檔案裡。 在本教學課程中，該檔案儲存在主應用程式目前的資料夾中。  
  
    ```vb  
    Protected Overrides Sub Track(record As TrackingRecord, timeout As TimeSpan)  
        Dim asr As ActivityStateRecord = TryCast(record, ActivityStateRecord)  
  
        If Not asr Is Nothing Then  
            If asr.State = ActivityStates.Executing And _  
            asr.Activity.TypeName = "System.Activities.Statements.WriteLine" Then  
  
                'Append the WriteLine output to the tracking  
                'file for this instance.  
                Using writer As StreamWriter = File.AppendText(record.InstanceId.ToString())  
                    writer.WriteLine(asr.Arguments("Text"))  
                    writer.Close()  
                End Using  
            End If  
        End If  
    End Sub  
    ```  
  
    ```csharp  
    protected override void Track(TrackingRecord record, TimeSpan timeout)  
    {  
        ActivityStateRecord asr = record as ActivityStateRecord;  
  
        if (asr != null)  
        {  
            if (asr.State == ActivityStates.Executing &&  
                asr.Activity.TypeName == "System.Activities.Statements.WriteLine")  
            {  
                // Append the WriteLine output to the tracking  
                // file for this instance  
                using (StreamWriter writer = File.AppendText(record.InstanceId.ToString()))  
                {  
                    writer.WriteLine(asr.Arguments["Text"]);  
                    writer.Close();  
                }  
            }  
        }  
    }  
    ```  
  
     未指定任何追蹤設定檔時，會使用預設的追蹤設定檔。 使用預設追蹤設定檔時，會發出所有 `ActivityStates` 的追蹤記錄。 因為我們只需要擷取 `WriteLine` 活動開發週期當中某個時間的文字，我們只能從 `ActivityStates.Executing` 狀態擷取該文字。 在中， [若要建立追蹤設定檔並註冊追蹤參與者](#to-create-the-tracking-profile-and-register-the-tracking-participant)，則會建立追蹤設定檔，以指定只 `WriteLine` `ActivityStates.Executing` 發出追蹤記錄。  
  
## <a name="to-create-the-tracking-profile-and-register-the-tracking-participant"></a>建立追蹤設定檔並註冊追蹤參與者  
  
1. 以滑鼠右鍵按一下 **方案總管** 中的 [ **workflowhostform.vb** ]，然後選擇 [ **View Code**]。  
  
2. 將下列 `using` (或 `Imports`) 陳述式加入至檔案最上方的其他 `using` (或 `Imports`) 陳述式。  
  
    ```vb  
    Imports System.Activities.Tracking  
    ```  
  
    ```csharp  
    using System.Activities.Tracking;  
    ```  
  
3. 將下列程式碼加入至 `ConfigureWorkflowApplication`，就在將 `StringWriter` 加入至工作流程擴充的程式碼之後、工作流程開發週期處理常式之前。  
  
    ```vb  
    'Add the custom tracking participant with a tracking profile  
    'that only emits tracking records for WriteLine activities.  
    Dim query As New ActivityStateQuery()  
    query.ActivityName = "WriteLine"  
    query.States.Add(ActivityStates.Executing)  
    query.Arguments.Add("Text")  
  
    Dim profile As New TrackingProfile()  
    profile.Queries.Add(query)  
  
    Dim stp As New StatusTrackingParticipant()  
    stp.TrackingProfile = profile  
  
    wfApp.Extensions.Add(stp)  
    ```  
  
    ```csharp  
    // Add the custom tracking participant with a tracking profile  
    // that only emits tracking records for WriteLine activities.  
    StatusTrackingParticipant stp = new StatusTrackingParticipant  
    {  
        TrackingProfile = new TrackingProfile  
        {  
            Queries =
            {  
                new ActivityStateQuery  
                {  
                    ActivityName = "WriteLine",  
                    States = { ActivityStates.Executing },  
                    Arguments = { "Text" }  
                }  
            }  
        }  
    };  
  
    wfApp.Extensions.Add(stp);  
    ```  
  
     此追蹤設定檔指定將 `WriteLine` 狀態之 `Executing` 活動的唯一活動狀態記錄發出給自訂追蹤參與者。  
  
     加入程式碼後，`ConfigureWorkflowApplication` 的最上方看起來如下所示。  
  
    ```vb  
    Private Sub ConfigureWorkflowApplication(wfApp As WorkflowApplication)  
        'Configure the persistence store.  
        wfApp.InstanceStore = store  
  
        'Add a StringWriter to the extensions. This captures the output  
        'from the WriteLine activities so we can display it in the form.  
        Dim sw As New StringWriter()  
        wfApp.Extensions.Add(sw)  
  
        'Add the custom tracking participant with a tracking profile  
        'that only emits tracking records for WriteLine activities.  
        Dim query As New ActivityStateQuery()  
        query.ActivityName = "WriteLine"  
        query.States.Add(ActivityStates.Executing)  
        query.Arguments.Add("Text")  
  
        Dim profile As New TrackingProfile()  
        profile.Queries.Add(query)  
  
        Dim stp As New StatusTrackingParticipant()  
        stp.TrackingProfile = profile  
  
        wfApp.Extensions.Add(stp)  
  
        'Workflow lifecycle handlers...  
    ```  
  
    ```csharp  
    private void ConfigureWorkflowApplication(WorkflowApplication wfApp)  
    {  
        // Configure the persistence store.  
        wfApp.InstanceStore = store;  
  
        // Add a StringWriter to the extensions. This captures the output  
        // from the WriteLine activities so we can display it in the form.  
        StringWriter sw = new StringWriter();  
        wfApp.Extensions.Add(sw);  
  
        // Add the custom tracking participant with a tracking profile  
        // that only emits tracking records for WriteLine activities.  
        StatusTrackingParticipant stp = new StatusTrackingParticipant  
        {  
            TrackingProfile = new TrackingProfile  
            {  
                Queries =
                {  
                    new ActivityStateQuery  
                    {  
                        ActivityName = "WriteLine",  
                        States = { ActivityStates.Executing },  
                        Arguments = { "Text" }  
                    }  
                }  
            }  
        };  
  
        wfApp.Extensions.Add(stp);  
  
        // Workflow lifecycle handlers...  
    ```  
  
## <a name="to-display-the-tracking-information"></a>顯示追蹤資訊  
  
1. 以滑鼠右鍵按一下 **方案總管** 中的 [ **workflowhostform.vb** ]，然後選擇 [ **View Code**]。  
  
2. 在 `InstanceId_SelectedIndexChanged` 處理常式中，將下列程式碼加入至清除狀態視窗的程式碼之後。  
  
    ```vb  
    'If there is tracking data for this workflow, display it  
    'in the status window.  
    If File.Exists(WorkflowInstanceId.ToString()) Then  
        Dim status As String = File.ReadAllText(WorkflowInstanceId.ToString())  
        UpdateStatus(status)  
    End If  
    ```  
  
    ```csharp  
    // If there is tracking data for this workflow, display it  
    // in the status window.  
    if (File.Exists(WorkflowInstanceId.ToString()))  
    {  
        string status = File.ReadAllText(WorkflowInstanceId.ToString());  
        UpdateStatus(status);  
    }  
    ```  
  
     在工作流程清單中選取新的工作流程時，會載入該工作流程的追蹤記錄並顯示在狀態視窗中。 下列範例是已完成的 `InstanceId_SelectedIndexChanged` 處理常式。  
  
    ```vb  
    Private Sub InstanceId_SelectedIndexChanged(sender As Object, e As EventArgs) Handles InstanceId.SelectedIndexChanged  
        If InstanceId.SelectedIndex = -1 Then  
            Return  
        End If  
  
        'Clear the status window.  
        WorkflowStatus.Clear()  
  
        'If there is tracking data for this workflow, display it  
        'in the status window.  
        If File.Exists(WorkflowInstanceId.ToString()) Then  
            Dim status As String = File.ReadAllText(WorkflowInstanceId.ToString())  
            UpdateStatus(status)  
        End If  
  
        'Get the workflow version and display it.  
        'If the workflow is just starting then this info will not  
        'be available in the persistence store so do not try and retrieve it.  
        If Not WorkflowStarting Then  
            Dim instance As WorkflowApplicationInstance = _  
                WorkflowApplication.GetInstance(WorkflowInstanceId, store)  
  
            WorkflowVersion.Text = _  
                WorkflowVersionMap.GetIdentityDescription(instance.DefinitionIdentity)  
  
            'Unload the instance.  
            instance.Abandon()  
        End If  
    End Sub  
    ```  
  
    ```csharp  
    private void InstanceId_SelectedIndexChanged(object sender, EventArgs e)  
    {  
        if (InstanceId.SelectedIndex == -1)  
        {  
            return;  
        }  
  
        // Clear the status window.  
        WorkflowStatus.Clear();  
  
        // If there is tracking data for this workflow, display it  
        // in the status window.  
        if (File.Exists(WorkflowInstanceId.ToString()))  
        {  
            string status = File.ReadAllText(WorkflowInstanceId.ToString());  
            UpdateStatus(status);  
        }  
  
        // Get the workflow version and display it.  
        // If the workflow is just starting then this info will not  
        // be available in the persistence store so do not try and retrieve it.  
        if (!WorkflowStarting)  
        {  
            WorkflowApplicationInstance instance =  
                WorkflowApplication.GetInstance(this.WorkflowInstanceId, store);  
  
            WorkflowVersion.Text =  
                WorkflowVersionMap.GetIdentityDescription(instance.DefinitionIdentity);  
  
            // Unload the instance.  
            instance.Abandon();  
        }  
    }  
    ```  
  
## <a name="to-build-and-run-the-application"></a>若要建置並執行應用程式  
  
1. 按 Ctrl+Shift+B 建置應用程式。  
  
2. 按 Ctrl + F5 啟動應用程式。  
  
3. 選取猜測遊戲的範圍和要啟動的工作流程類型，然後按一下 [ **新遊戲**]。 在 [ **猜測** ] 方塊中輸入猜測，然後按一下 [ **移** 至] 來提交您的猜測。 請注意，工作流程的狀態會顯示在狀態視窗中。 此輸出是從 `WriteLine` 活動擷取的。 切換至不同的工作流程，方法是從 [ **工作流程實例識別碼** ] 下拉式方塊中選取一個工作流程，並注意目前的工作流程狀態已移除。 切換回上一個工作流程，注意其狀態已還原，類似下列範例。  
  
    > [!NOTE]
    > 如果您切換的工作流程在啟用追蹤之前就已經啟動，就不會顯示任何狀態。 但是，如果您做其他猜測，會儲存這些猜測的狀態，因為現在已啟用追蹤。  
  
    ```output
    Please enter a number between 1 and 10
    Your guess is too high.
    Please enter a number between 1 and 10
    ```

    > [!NOTE]
    > 此資訊可用於判斷隨機數字的範圍，但不包含任何先前猜測的相關資訊。 這項資訊會在下一個步驟中，也就是 [如何：並存裝載工作流程的多個版本](how-to-host-multiple-versions-of-a-workflow-side-by-side.md)。

    請記下工作流程執行個體識別碼，並玩遊戲直到結束。
  
4. 開啟 Windows 檔案總管，然後根據您的專案設定) ，流覽至 [ **numberguessworkflowhost\bin\debug]** ] 資料夾 (或 [ **bin\release** ]。 請注意，除了專案可執行檔外，還有些檔案具有 guid 檔案名稱。 在上一步驟完成的工作流程中，找出對應工作流程執行個體識別碼的檔案，並在 [記事本] 中開啟。 追蹤資訊包含如下的類似資訊。  
  
    ```output
    Please enter a number between 1 and 10
    Your guess is too high.
    Please enter a number between 1 and 10
    Your guess is too high.
    Please enter a number between 1 and 10
    ```

    除了使用者沒有猜測的情況外，此追蹤資料也不包含工作流程最後猜測的相關資訊。 這是因為追蹤資訊僅包含工作流程的 `WriteLine` 輸出，在工作流程完成後顯示的最後一個訊息，是由 `Completed` 處理常式完成的。 在本教學課程的下一個步驟中， [如何：並存裝載多個版本的工作流程](how-to-host-multiple-versions-of-a-workflow-side-by-side.md)、修改現有的 `WriteLine` 活動以顯示使用者的猜測，以及 `WriteLine` 加入會顯示最終結果的其他活動。 整合這些變更之後， [如何：並行裝載多個版本的工作流程](how-to-host-multiple-versions-of-a-workflow-side-by-side.md) ，示範如何同時裝載工作流程的多個版本。
