---
title: 設定工作流程的追蹤
ms.date: 03/30/2017
ms.assetid: 905adcc9-30a0-4918-acd6-563f86db988a
ms.openlocfilehash: 098b295be00b1b8283e26e79ea14e78634fdb504
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557550"
---
# <a name="configuring-tracking-for-a-workflow"></a>設定工作流程的追蹤

工作流程可透過三種方法執行：

- 裝載於 <xref:System.ServiceModel.Activities.WorkflowServiceHost>

- 當做 <xref:System.Activities.WorkflowApplication> 執行

- 使用 <xref:System.Activities.WorkflowInvoker> 直接執行

視工作流程裝載選項而定，追蹤參與者可以透過程式碼或組態檔加入。 本主題描述如何透過將追蹤參與者加入至 <xref:System.Activities.WorkflowApplication> 及 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 來設定追蹤，以及如何在使用 <xref:System.Activities.WorkflowInvoker> 時啟用追蹤。

## <a name="configuring-workflow-application-tracking"></a>設定工作流程應用程式追蹤

工作流程可透過 <xref:System.Activities.WorkflowApplication> 類別來執行。 本主題示範如何將追蹤參與者加入至 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 工作流程主機，以設定 <xref:System.Activities.WorkflowApplication> 工作流程應用程式的追蹤。 在這種情況下，工作流程會以工作流程應用程式的形式執行。 您要透過程式碼 (而不是使用組態檔) 設定工作流程應用程式，而該程式碼為使用 <xref:System.Activities.WorkflowApplication> 類別的自我裝載 .exe 檔案。 追蹤參與者會加入做為 <xref:System.Activities.WorkflowApplication> 執行個體的延伸。 將 <xref:System.Activities.Tracking.TrackingParticipant> 加入至 WorkflowApplication 執行個體的擴充集合，即可完成此步驟。

若為工作流程應用程式，您可以加入 <xref:System.Activities.Tracking.EtwTrackingParticipant> 行為擴充，如下列程式碼所示。

```csharp
LogActivity activity = new LogActivity();

WorkflowApplication instance = new WorkflowApplication(activity);
EtwTrackingParticipant trackingParticipant =
    new EtwTrackingParticipant
{

        TrackingProfile = new TrackingProfile
           {
               Name = "SampleTrackingProfile",
               ActivityDefinitionId = "ProcessOrder",
               Queries = new WorkflowInstanceQuery
               {
                  States = { "*" }
              }
          }
       };
instance.Extensions.Add(trackingParticipant);
```

### <a name="configuring-workflow-service-tracking"></a>設定工作流程服務追蹤

工作流程裝載于服務主機時，可以公開為 WCF 服務 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 。 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 是用於工作流程服務的特殊 .NET ServiceHost 實作。 本節說明如何為在 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 中執行的 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 工作流程服務設定追蹤。 此追蹤是透過 Web.config 檔案 (適用於 Web 裝載服務) 或 App.config 檔案 (適用於裝載於獨立應用程式中的服務，例如主控台應用程式) 指定服務行為而設定的，或是透過程式碼將追蹤特定行為加入至服務主機的 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 集合而設定的。

若為裝載于的工作流程服務， <xref:System.ServiceModel.WorkflowServiceHost> 您可以 <xref:System.Activities.Tracking.EtwTrackingParticipant> 使用設定檔中的 <> 專案來新增， `behavior` 如下列範例所示。

```xml
<behaviors>
   <serviceBehaviors>
        <behavior>
          <etwTracking profileName="Sample Tracking Profile" />
        </behavior>
   </serviceBehaviors>
</behaviors>
```

此外，對於裝載於 <xref:System.ServiceModel.WorkflowServiceHost> 中的工作流程服務，您可以透過程式碼加入 <xref:System.Activities.Tracking.EtwTrackingParticipant> 行為擴充。 若要加入自訂的追蹤參與者，請建立一個新的行為擴充，並將它加入至 <xref:System.ServiceModel.ServiceHost>，如下列範例程式碼所示。

> [!NOTE]
> 如果您想要查看示範如何建立加入自訂追蹤參與者之自訂行為專案的範例程式碼，請參閱 [追蹤](./samples/tracking.md) 範例。

```csharp
ServiceHost svcHost = new ServiceHost(typeof(WorkflowService), new
                                 Uri("http://localhost:8001/Sample"));
EtwTrackingBehavior trackingBehavior =
    new EtwTrackingBehavior
    {
        ProfileName = "Sample Tracking Profile"
    };
svcHost.Description.Behaviors.Add(trackingBehavior);
svcHost.Open();
```

追蹤參與者會做為行為的擴充，而加入至工作流程服務主機。

下列範例程式碼示範如何從組態檔讀取追蹤設定檔。

```csharp
TrackingProfile GetProfile(string profileName, string displayName)
        {
            TrackingProfile trackingProfile = null;
            TrackingSection trackingSection = (TrackingSection)WebConfigurationManager.GetSection("system.serviceModel/tracking");
            if (trackingSection == null)
            {
                return null;
            }

            profileName ??= "";

            //Find the profile with the specified profile name in the list of profile found in config
            var match = from p in new List<TrackingProfile>(trackingSection.TrackingProfiles)
                        where (p.Name == profileName) && ((p.ActivityDefinitionId == displayName) || (p.ActivityDefinitionId == "*"))
                        select p;

            if (match.Count() == 0)
            {
                //return an empty profile
                trackingProfile = new TrackingProfile()
                {
                    ActivityDefinitionId = displayName
                };

            }
            else
            {
                trackingProfile = match.First();
            }

            return trackingProfile;
```

下列範例程式碼示範如何將追蹤設定檔加入至工作流程主機。

```csharp
WorkflowServiceHost workflowServiceHost = serviceHostBase as WorkflowServiceHost;
if (null != workflowServiceHost)
{
    string workflowDisplayName = workflowServiceHost.Activity.DisplayName;
    TrackingProfile trackingProfile = GetProfile(this.profileName, workflowDisplayName);
    workflowServiceHost.WorkflowExtensions.Add(()  => new EtwTrackingParticipant {
        TrackingProfile = trackingProfile
    });
 }
```

> [!NOTE]
> 如需追蹤設定檔的詳細資訊，請參閱 [追蹤設定檔](tracking-profiles.md)。

### <a name="configuring-tracking-using-workflowinvoker"></a>使用 WorkflowInvoker 設定追蹤

若要為使用 <xref:System.Activities.WorkflowInvoker> 執行的工作流程設定追蹤，請加入追蹤提供者做為 <xref:System.Activities.WorkflowInvoker> 執行個體的延伸。 下列程式碼範例取自 [自訂追蹤](./samples/custom-tracking.md) 範例。

```csharp
WorkflowInvoker invoker = new WorkflowInvoker(BuildSampleWorkflow());
invoker.Extensions.Add(customTrackingParticipant);
invoker.Invoke();
```

### <a name="viewing-tracking-records-in-event-viewer"></a>在事件檢視器中檢視追蹤記錄

追蹤 WF 執行時，可以檢視兩個相關性特別大的事件檢視器記錄：分析記錄和偵錯記錄。 兩者都位於 Microsoft&#124;Windows&#124;應用程式伺服器-應用程式] 節點底下。 這個區段中的記錄包含單一應用程式的事件，而不包含對整個系統有影響的事件。

偵錯追蹤事件會寫入到偵錯記錄中。 若要收集事件檢視器中的 WF 偵錯追蹤事件，請啟用偵錯記錄。

1. 若要開啟事件檢視器，請按一下 [ **開始**]，然後按一下 [ **執行]。** 在 [執行] 對話方塊中，輸入 `eventvwr` 。

2. 在 [事件檢視器] 對話方塊中，展開 [ **應用程式及服務記錄** 檔] 節點。

3. 展開 [ **Microsoft**]、[ **Windows**] 和 [ **應用程式伺服器-應用程式** ] 節點。

4. 以滑鼠右鍵按一下 [**應用程式伺服器-應用程式**] 節點底下的 [**調試**程式] 節點，然後選取 [**啟用記錄**]。

5. 執行可啟用追蹤的應用程式，以產生追蹤事件。

6. 以滑鼠右鍵按一下 [ **Debug** ] 節點，然後選取 [重新整理] **。** 追蹤事件應該會顯示在中央窗格中。

WF 4 提供將追蹤記錄寫入至 ETW (Windows 事件追蹤) 工作階段的追蹤參與者。 ETW 追蹤參與者會設定追蹤設定檔來訂閱追蹤記錄。 當啟用追蹤時，會向 ETW 發出錯誤追蹤記錄。 對應至由 ETW 追蹤參與者所發出之追蹤事件的 ETW 追蹤事件 (範圍在 100-113 之間) 會寫入到分析記錄中。

若要檢視追蹤記錄，請遵循下列步驟。

1. 若要開啟事件檢視器，請按一下 [ **開始**]，然後按一下 [ **執行]。** 在 [執行] 對話方塊中，輸入 `eventvwr` 。

2. 在 [事件檢視器] 對話方塊中，展開 [ **應用程式及服務記錄** 檔] 節點。

3. 展開 [ **Microsoft**]、[ **Windows**] 和 [ **應用程式伺服器-應用程式** ] 節點。

4. 以滑鼠右鍵按一下 [**應用程式伺服器-應用程式**] 節點底下的 [**分析**] 節點，然後選取 [**啟用記錄**]。

5. 執行您的啟用追蹤的應用程式，以產生追蹤記錄。

6. 以滑鼠右鍵按一下 [ **分析** ] 節點，然後選取 [重新整理] **。** 追蹤記錄應該會顯示在中央窗格中。

下圖顯示事件檢視器中的追蹤事件：

![顯示追蹤記錄之事件檢視器的螢幕擷取畫面。](./media/configuring-tracking-for-a-workflow/tracking-event-viewer.png)

### <a name="registering-an-application-specific-provider-id"></a>註冊應用程式特定的提供者識別碼

如果事件必須寫入至特定應用程式記錄檔，請遵循下列步驟註冊新提供者資訊清單。

1. 在應用程式的組態檔中宣告提供者識別碼。

    ```xml
    <system.serviceModel>
        <diagnostics etwProviderId="2720e974-9fe9-477a-bb60-81fe3bf91eec"/>
    </system.serviceModel>
    ```

2. 將資訊清單檔從%windir%\Microsoft.NET\Framework \\ \<latest version of [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]> \Microsoft.Windows.ApplicationServer.Applications.man 複製到暫存位置，然後將它重新命名為 ApplicationServer. Applications_Provider1

3. 將資訊清單檔中的 GUID 變更為新的 GUID。

    ```xml
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" />
    ```

4. 如果您不要解除安裝預設提供者，請變更提供者名稱。

    ```xml
    <provider name="Microsoft-Windows-Application Server-Applications" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" />
    ```

5. 如果您在上一個步驟中變更提供者名稱，請將資訊清單檔中的通道名稱變更為新的提供者名稱。

    ```xml
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Admin" chid="ADMIN_CHANNEL" symbol="ADMIN_CHANNEL" type="Admin" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ADMIN_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Operational" chid="OPERATIONAL_CHANNEL" symbol="OPERATIONAL_CHANNEL" type="Operational" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.OPERATIONAL_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Debug" chid="DEBUG_CHANNEL" symbol="DEBUG_CHANNEL" type="Debug" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.DEBUG_CHANNEL.message)" />
    <channel name="Microsoft-Windows-Application Server-Applications_Provider1/Perf" chid="PERF_CHANNEL" symbol="PERF_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.PERF_CHANNEL.message)" />
    ```

6. 遵循下列步驟產生資源 DLL。

    1. 安裝 Windows SDK。 Windows SDK 包含 ([mc.exe](/windows/win32/wes/message-compiler--mc-exe-)) 和資源 [ 編譯器 (rc.exe) 的 ](/windows/win32/menurc/using-rc-the-rc-command-line-) 訊息編譯器。

    2. 在 Windows SDK 命令提示字元中，對新的資訊清單檔執行 mc.exe。

        ```console
        mc.exe Microsoft.Windows.ApplicationServer.Applications_Provider1.man
        ```

    3. 對上一個步驟中產生的資源檔執行 rc.exe。

        ```console
        rc.exe  Microsoft.Windows.ApplicationServer.Applications_Provider1.rc
        ```

    4. 建立名為 NewProviderReg.cs 的空白 cs 檔案。

    5. 使用 C# 編輯器建立資源 DLL。

        ```console
        csc /target:library /win32res:Microsoft.Windows.ApplicationServer.Applications_Provider1.res NewProviderReg.cs /out:Microsoft.Windows.ApplicationServer.Applications_Provider1.dll
        ```

    6. 將資訊清單檔中的資源和訊息 dll 名稱變更 `Microsoft.Windows.ApplicationServer.Applications.Provider1.man` 為新的 dll 名稱。

        ```xml
        <provider name="Microsoft-Windows-Application Server-Applications_Provider1" guid="{2720e974-9fe9-477a-bb60-81fe3bf91eec}" symbol="Microsoft_Windows_ApplicationServer_ApplicationEvents" resourceFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll" messageFileName="<dll directory>\Microsoft.Windows.ApplicationServer.Applications_Provider1.dll" />
        ```

    7. 使用 [wevtutil](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732848(v=ws.10)) 註冊資訊清單。

        ```console
        wevtutil im Microsoft.Windows.ApplicationServer.Applications_Provider1.man
        ```

## <a name="see-also"></a>另請參閱

- [Windows Server App Fabric 監視](/previous-versions/appfabric/ee677251(v=azure.10))
- [使用 App Fabric 監視應用程式](/previous-versions/appfabric/ee677276(v=azure.10))
