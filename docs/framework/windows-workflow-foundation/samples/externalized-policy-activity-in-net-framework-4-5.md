---
title: .NET Framework 4.5 中的外顯化原則活動
ms.date: 03/30/2017
ms.assetid: 92fd6f92-23a1-4adf-b96a-2754ea93ad3e
ms.openlocfilehash: 00b671f169696728610e8ee32f874b44fbff9e33
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90556911"
---
# <a name="externalized-policy-activity-in-net-framework-45"></a>.NET Framework 4.5 中的外顯化原則活動

此範例示範 ExternalizedPolicy4 活動如何 <xref:System.Workflow.Activities.Rules.RuleSet> [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 使用 wf 3.5 中隨附的規則引擎，直接在 WINDOWS WORKFLOW FOUNDATION (wf 4.5) 中執行現有的 .NET Framework 3.5 WINDOWS WORKFLOW FOUNDATION (WF 3.5) 物件。 您可以使用這個活動來開啟及執行任何現有的 WF 3.5 <xref:System.Workflow.Activities.Rules.RuleSet>。 如需隨附于 Windows Workflow Foundation 的 WF 3.5 規則引擎的詳細資訊，請參閱 [Windows Workflow Foundation 規則引擎簡介](/previous-versions/dotnet/articles/aa480193(v=msdn.10))。 如需將規則遷移至中的詳細資訊 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] ，請參閱 [遷移指引](../migration-guidance.md)。

## <a name="projects-in-this-sample"></a>這個範例中的專案

|專案名稱|描述|主要檔案|
|-|-|-|
|ExternalizedPolicy4|包含 ExternalizedPolicy4 活動及其 WF 4.5 設計工具。|**ExternalizedPolicy4.cs**：活動定義。<br /><br /> **ExternalizedPolicy4Designer**： ExternalizedPolicy4 活動的自訂設計工具。 它使用 WF 3.5 規則引擎中的規則編輯器 (<xref:System.Workflow.Activities.Rules.Design.RuleSetDialog>)。|
|ImperativeCodeClientSample|範例用戶端應用程式，透過使用命令式 C# 程式碼 (未使用設計工具) 的 ExternalizedPolicy4 應用程式，來設定及執行工作流程。|**Applydiscount.rules**：具有 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 規則定義的檔案。<br /><br /> **Order.cs**：代表客戶訂單的型別。 規則套用至這個類型的物件。<br /><br /> **Program.cs**：設定和執行具有 Policy4 活動的工作流程，以將 applydiscount.rules 中定義的規則套用至 Order 物件的實例。<br /><br /> App.config：具有規則檔路徑的組態檔。|
|DesignerClientSample|範例用戶端應用程式，透過使用 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 設計工具的 ExternalPolicy4 應用程式，來設定及執行工作流程。|**Sequence1**：使用 Policy4 活動執行規則評估的連續工作流程。<br /><br /> **Program.cs**：執行 Sequence1 中定義之工作流程的實例。|

## <a name="the-externalizedpolicy4-activity"></a>ExternalizedPolicy4 活動

ExternalizedPolicy4 活動是 <xref:System.Activities.NativeActivity>，允許在 WF 4.5 工作流程中執行 WF 3.5 <xref:System.Workflow.Activities.Rules.RuleSet> 物件。 下列範例是活動的公用物件模型簡化定義。

```csharp
public class ExternalizedPolicy4Activity<TResult>: CodeActivity
{
    public string RulesFilePath

    public string RuleSetName

    [RequiredArgument]
    public InArgument<T> TargetObject

    [RequiredArgument]
    public OutArgument<T> ResultObject

    public OutArgument<ValidationErrorCollection> ValidationErrors
}
```

|屬性|描述|
|-|-|
|RuleSetFilePath|當活動執行時，要評估之 .NET Framework 3.5 <xref:System.Workflow.Activities.Rules.RuleSet> 檔案的路徑。|
|RuleSetName|.rules 檔案中使用之 <xref:System.Workflow.Activities.Rules.RuleSet> 的名稱。|
|TargetObject|評估 <xref:System.Workflow.Activities.Rules.Rule> 中之 <xref:System.Workflow.Activities.Rules.RuleSet> 物件的目標物件。|
|ResultObject|套用規則之後的結果物件 (例如，對 Input 引數套用規則後，結果會儲存在 Result 引數中)。|
|ValidationError|執行前對目標物件驗證 <xref:System.Workflow.Activities.Rules.RuleSet> 時，WF 3.5 規則引擎傳回的驗證錯誤清單。|

## <a name="externalizedpolicy4-activity-designer"></a>ExternalizedPolicy4 活動設計工具

ExternalizedPolicy4 設計工具讓您不需要撰寫程式碼，即可設定活動使用現有的 RuleSet。 只要設定 .rules 檔案所在路徑，並指定您要使用的 <xref:System.Workflow.Activities.Rules.RuleSet> 名稱。 它也可以讓您修改 <xref:System.Workflow.Activities.Rules.RuleSet>。 在建置方案之後，可在工具箱的 Microsoft.Samples.Activities.Rules 區段中找到它。 此設計工具可讓您選取 .rules 檔案和 <xref:System.Workflow.Activities.Rules.RuleSet>。 按一下 [ **編輯規則集** ] 按鈕時， <xref:System.Workflow.Activities.Rules.Design.RuleSetDialog> 會顯示 WF 3.5。 這個對話方塊是重新裝載的 WF 3.5 規則編輯器，可用來檢視及編輯 ExternalizedPolicy4 活動執行的規則。

## <a name="policy4-and-externalpolicy4"></a>Policy4 和 ExternalPolicy4

原則活動可讓您在 WF 4.5 工作流程中建立和執行 .NET Framework 3.5 規則集。 <xref:System.Workflow.Activities.Rules.RuleSet> 已序列化，內嵌於 Policy4 活動 XAML 定義中。 ExternalizedPolicy4 範例示範如何使用現有的外部 <xref:System.Workflow.Activities.Rules.RuleSet> (包含在 .rules 檔案中)。

## <a name="use-this-sample"></a>使用此範例

不需要特殊設定即可執行此範例。 在 Visual Studio 中開啟方案，然後按 **F5** 執行應用程式。

這個範例包含兩個用戶端應用程式：ImperativeCodeClientSample 和 DesignerClientSample。 ImperativeCodeClientSample 用戶端示範如何透過 C# 命令式程式碼來設定及執行 ExternalizedPolicy4 活動。 DesignerClientSample 示範如何透過設計工具來設定及執行 ExternalizedPolicy4 活動。

### <a name="run-the-imperativecodeclientsample-application"></a>執行 ImperativeCodeClientSample 應用程式

1. 使用 Visual Studio 開啟 *policy4sample.sln .sln* 方案檔。

2. 在 **方案總管**中，以滑鼠右鍵按一下 **ImperativeCodeClientSample** 專案，然後選取 [ **設定為啟始專案**]。

3. 若要執行專案，請按下**Ctrl** + **F5**。

### <a name="run-the-designerclientsample-application"></a>執行 DesignerClientSample 應用程式

1. 使用 Visual Studio 開啟 *policy4sample.sln .sln* 方案檔。

2. 在 **方案總管**中，以滑鼠右鍵按一下 **DesignerClientSample** 專案，然後選取 [ **設定為啟始專案**]。

3. 按**Ctrl** + **Shift** + **B**以編譯專案。

4. 按下**Ctrl** + **F5**來執行專案。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。
>
> 此範例位於下列目錄：
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Rules-ExternalizedPolicy4`
