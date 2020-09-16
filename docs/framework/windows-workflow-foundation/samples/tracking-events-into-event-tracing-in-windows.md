---
title: 在 Windows 事件追蹤中追蹤事件
ms.date: 03/30/2017
ms.assetid: f812659b-0943-45ff-9430-4defa733182b
ms.openlocfilehash: 4350287aedae73a7ca9556de7ae3f597950e32ea
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90549610"
---
# <a name="tracking-events-into-event-tracing-in-windows"></a>在 Windows 事件追蹤中追蹤事件

這個範例示範如何在工作流程服務上啟用 Windows Workflow Foundation (WF) 追蹤，以及在 Windows 的事件追蹤 (ETW) 中發出追蹤事件。 為了將工作流程追蹤記錄發出到 ETW，此範例會使用 ETW 追蹤參與者 (<xref:System.Activities.Tracking.EtwTrackingParticipant>)。

範例中的工作流程會接收要求、將對等的輸入資料指派給輸入變數，並將對等項目傳回用戶端。 當輸入資料為 0 時，將會發生除以零的例外狀況而無法處理，所以導致工作流程中止。 當啟用追蹤時，錯誤追蹤記錄會發出到 ETW，有助於之後的疑難排解。 ETW 追蹤參與者會設定追蹤設定檔來訂閱追蹤記錄。 追蹤設定檔會定義於 Web.config 檔案中，並當做組態參數提供給 ETW 追蹤參與者。 ETW 追蹤參與者會在工作流程服務的 Web.config 檔案中設定，而且會當做服務行為套用到此服務。 在這個範例中，您會使用事件檢視器檢視事件記錄檔中的追蹤事件。

## <a name="workflow-tracking-details"></a>工作流程追蹤詳細資料

Windows Workflow Foundation 提供追蹤基礎結構來追蹤工作流程實例的執行。 追蹤執行階段會建立工作流程執行個體，以發出與工作流程開發週期相關的事件、來自工作流程活動的事件和自訂事件。 下表詳細說明追蹤基礎結構的主要元件。

|元件|描述|
|---------------|-----------------|
|追蹤執行階段|提供基礎結構以發出追蹤記錄。|
|追蹤參與者|存取追蹤記錄。 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] 隨附追蹤參與者，可將追蹤記錄當做 Windows 事件追蹤 (ETW) 事件撰寫。|
|追蹤設定檔|篩選機制，可讓追蹤參與者訂閱從工作流程執行個體發出之追蹤記錄的子集。|

下表詳細說明工作流程執行階段發出的追蹤記錄。

|追蹤記錄|描述|
|---------------------|-----------------|
|工作流程執行個體追蹤記錄。|描述工作流程執行個體的開發週期。 例如，當工作流程開始或完成時，就會發出執行個體記錄。|
|活動狀態追蹤記錄。|活動執行詳細資訊。 這些記錄會指出工作流程活動的狀態，例如活動排程時間、活動完成時間，或是擲回錯誤的時間。|
|書籤繼續記錄。|只要工作流程執行個體中的書籤繼續，就會發出。|
|自訂追蹤記錄。|工作流程作者可建立自訂追蹤記錄，並在自訂活動中發出這些記錄。|
|<xref:System.Activities.Tracking.ActivityScheduledRecord>|當活動排程另一個活動時，就會發出這個記錄。|
|<xref:System.Activities.Tracking.FaultPropagationRecord>|從活動中傳播錯誤時，就會發出這個記錄。|
|<xref:System.Activities.Tracking.CancelRequestedRecord>|當另一個活動取消原本的活動時，就會發出這個記錄。|

追蹤參與者可使用追蹤設定檔訂閱所發出之追蹤記錄的子集。 追蹤設定檔包含追蹤查詢，這些查詢允許訂閱特殊追蹤記錄類型。 追蹤設定檔可在程式碼或組態中指定。

#### <a name="to-use-this-sample"></a>若要使用這個範例

1. 使用 Visual Studio 2010，開啟 EtwTrackingParticipantSample .sln 方案檔。

2. 若要建置此方案，請按 CTRL+SHIFT+B。

3. 若要執行此方案，請按 F5。

    根據預設，服務會在埠53797上接聽 (`http://localhost:53797/SampleWorkflowService.xamlx`) 。

4. 使用檔案總管，開啟 WCF 測試用戶端。

    WCF 測試用戶端 ( # A0) 位於 \<Visual Studio 2010 installation folder> \Common7\IDE\ 資料夾中。

    預設的 Visual Studio 2010 安裝資料夾是 C:\Program Files\Microsoft Visual Studio 10.0。

5. **在 [WCF**測試用戶端] 中，選取 [檔案] 功能表中的 [**加入服務**]。

    在輸入方塊中加入端點位址。 預設為 `http://localhost:53797/SampleWorkflowService.xamlx`。

6. 開啟 [事件檢視器] 應用程式。

    叫用服務之前，請從 [ **開始** ] 功能表開始事件檢視器，選取 [ **執行** ]，然後輸入 `eventvwr.exe` 。 確認事件記錄檔正在接聽從工作流程服務發出的追蹤事件。

7. 在事件檢視器的樹狀檢視中，流覽至 [ **事件檢視器**]、[ **應用程式及服務記錄**檔] 和 [ **Microsoft**]。 在 [ **Microsoft** ] 上按一下滑鼠右鍵，然後選取 [ **View** ]，然後 **顯示分析和調試記錄** ，以啟用分析和調試記錄

    確定已核取 [ **顯示分析和偵錯工具記錄** 檔] 選項。

8. 在事件檢視器的樹狀檢視中，流覽至 [**事件檢視器**]、[**應用程式及服務記錄**檔]、[ **Microsoft** **]、[****應用程式伺服器-應用**程式]。 以滑鼠右鍵按一下 [ **分析** ]，然後選取 [ **啟用記錄** ] 以啟用 **分析** 記錄。

9. 若要使用 WCF 測試用戶端測試此服務，請按兩下 `GetData`。

    這樣會開啟 `GetData` 方法。 此要求會接受一個參數，並確定值為 0 (預設值)。

     按一下 **[** 叫用]。

10. 請查看工作流程所發出的事件。

    切換回事件檢視器，然後流覽至 [**事件檢視器**]、[**應用程式及服務記錄**檔]、[ **Microsoft** **]、[****應用程式伺服器-應用**程式]。 以滑鼠右鍵按一下 [ **分析** ]， **然後選取 [** 重新整理]。

    工作流程事件會顯示在事件檢視器中。 請注意，將會顯示工作流程執行事件，而且其中一個是未處理的例外狀況且對應到工作流程中的錯誤。 此外，也會從工作流程活動發出警告事件，指出活動正在擲回錯誤。

11. 使用 0 以外的輸入資料重複步驟 9 和 10，如此一來就不會擲回任何錯誤。

追蹤設定檔可讓您訂閱執行階段在工作流程執行個體狀態變更時，所發出的事件。 根據您的監控需求，您可以建立初略的設定檔，使其訂閱工作流程上的一組小型高階狀態變更。 在另一方面，您也可以建立非常精確的設定檔，它的輸出非常豐富，足以讓您在日後重新建構執行。 此範例示範使用 `HealthMonitoring Tracking Profile` 從工作流程執行階段發出的事件，它會發出一組小型事件。 發出其他工作流程追蹤事件的另一個設定檔名為 `Troubleshooting Tracking Profile`，它也會在 Web.config 中提供。 當安裝 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] 時，Machine.config 檔案中會設定有空白名稱的預設設定檔。 當沒有設定檔名稱或者指定了空的設定檔名稱時，這個設定檔會由 ETW 追蹤行為組態所使用。

狀況監控追蹤設定檔會發出工作流程執行個體記錄及活動錯誤傳播記錄。 這個設定檔的建立方式，是將下列追蹤設定檔加入至 Web.config 組態檔。

```xml
<tracking>
  <profiles>
    <trackingProfile name="HealthMonitoring Tracking Profile">
      <workflow activityDefinitionId="*">
        <workflowInstanceQueries>
          <workflowInstanceQuery>
            <states>
              <state name="Started"/>
              <state name="Completed"/>
              <state name="Aborted"/>
              <state name="UnhandledException"/>
            </states>
          </workflowInstanceQuery>
        </workflowInstanceQueries>
        <faultPropagationQueries>
          <faultPropagationQuery faultSourceActivityName ="*" faultHandlerActivityName="*"/>
        </faultPropagationQueries>
      </workflow>
    </trackingProfile>
  </profiles>
</tracking>
```

 您可以將 `EtwTrackingParticipant` 組態變更為以下內容來變更此設定檔。

```xml
<behaviors>
  <serviceBehaviors>
    <behavior>
      <etwTracking profileName="HealthMonitoring Tracking Profile"/>
    </behavior>
  </serviceBehaviors>
</behaviors>
```

#### <a name="to-clean-up-optional"></a>若要清除 (選擇性)

1. 開啟 [事件檢視器]。

2. 流覽至 **事件檢視器**、 **應用程式和服務記錄**檔、 **Microsoft**、 **Windows**、 **應用程式伺服器-應用程式**。 以滑鼠右鍵按一下 [ **分析** ]，然後選取 [ **停用記錄**]。

3. 流覽至 **事件檢視器**、 **應用程式和服務記錄**檔、 **Microsoft**、 **Windows**、 **應用程式伺服器-應用程式**。 以滑鼠右鍵按一下 [ **分析** ]，然後選取 [ **清除記錄**檔]。

4. 選擇 [ **清除** ] 選項以清除事件。

## <a name="known-issue"></a>已知問題

> [!NOTE]
> 在 [事件檢視器] 中有一個可能無法為 ETW 事件解碼的已知問題。 您可能會看到類似下面的錯誤訊息。
>
> \<id>找不到來自來源 Microsoft Windows-應用程式伺服器的事件識別碼描述。 可能是引發此事件的元件未安裝在您的本機電腦上，或安裝已損毀。 您可以在本機電腦上安裝或修復該元件。
>
> 如果您遇到這個錯誤，請按一下執行窗格中的 [重新整理]。 現在，此事件應該就會正確解碼。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Tracking\EtwTracking`

## <a name="see-also"></a>另請參閱

- [AppFabric 監控範例](/previous-versions/appfabric/ff383407(v=azure.10))
