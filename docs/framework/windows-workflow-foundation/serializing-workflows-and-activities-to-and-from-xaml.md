---
title: '序列化工作流程及 XAML 之間的活動 '
description: 本文概述如何在 Workflow Foundation 中序列化工作流程定義以及使用 XAML 工作流程定義。
ms.date: 03/30/2017
ms.assetid: 37685b32-24e3-4d72-88d8-45d5fcc49ec2
ms.openlocfilehash: 168dbc9a36cfa80c15fddc7481e986d1ce383adb
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421341"
---
# <a name="serialize-workflows-and-activities-to-and-from-xaml"></a>將工作流程和活動序列化為 XAML

除了將工作流程定義編譯成包含在組件中的類型之外，工作流程定義也可以序列化為 XAML。 這些序列化的定義可重新載入以供編輯或檢閱、傳遞至建置系統以進行編譯，或載入及叫用。 本主題提供序列化工作流程定義以及使用 XAML 工作流程定義的概觀。

## <a name="work-with-xaml-workflow-definitions"></a>使用 XAML 工作流程定義

若要建立要序列化的工作流程定義，請使用 <xref:System.Activities.ActivityBuilder> 類別。 建立 <xref:System.Activities.ActivityBuilder> 與建立 <xref:System.Activities.DynamicActivity> 十分類似。 您要指定任何所需的引數，以及設定構成行為的活動。 在下列範例中，會建立 `Add` 活動，它接受兩個輸入引數、加總這些引數，然後傳回結果。 因為這個活動會傳回結果，所以要使用泛型 <xref:System.Activities.ActivityBuilder%601> 類別。

[!code-csharp[CFX_WorkflowApplicationExample#41](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#41)]

每個 <xref:System.Activities.DynamicActivityProperty> 執行個體代表工作流程的一個輸入引數，而 <xref:System.Activities.ActivityBuilder.Implementation%2A> 包含形成工作流程邏輯的活動。 請注意，此範例中的右值 (r-value) 運算式是 Visual Basic 運算式。 Lambda 運算式不可序列化成 XAML，除非使用 <xref:System.Activities.Expressions.ExpressionServices.Convert%2A>。 如果要在工作流程設計工具中開啟或編輯序列化的工作流程，則應該使用 Visual Basic 運算式。 如需詳細資訊，請參閱[使用命令式程式碼撰寫工作流程、活動和運算式](authoring-workflows-activities-and-expressions-using-imperative-code.md)。

若要將 <xref:System.Activities.ActivityBuilder> 執行個體代表的工作流程定義序列化為 XAML，請使用 <xref:System.Activities.XamlIntegration.ActivityXamlServices> 建立 <xref:System.Xaml.XamlWriter>，然後使用 <xref:System.Xaml.XamlServices> 將工作流程定義序列化 (使用 <xref:System.Xaml.XamlWriter>)。 <xref:System.Activities.XamlIntegration.ActivityXamlServices>有方法可將 <xref:System.Activities.ActivityBuilder> 實例對應至 xaml，以及載入 xaml 工作流程，並傳回可叫用的 <xref:System.Activities.DynamicActivity> 。 在下列範例中， <xref:System.Activities.ActivityBuilder> 上一個範例中的實例會序列化為字串，並儲存至檔案。

```csharp
// Serialize the workflow to XAML and store it in a string.
StringBuilder sb = new StringBuilder();
StringWriter tw = new StringWriter(sb);
XamlWriter xw = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(tw, new XamlSchemaContext()));
XamlServices.Save(xw, ab);
string serializedAB = sb.ToString();

// Display the XAML to the console.
Console.WriteLine(serializedAB);

// Serialize the workflow to XAML and save it to a file.
StreamWriter sw = File.CreateText(@"C:\Workflows\add.xaml");
XamlWriter xw2 = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(sw, new XamlSchemaContext()));
XamlServices.Save(xw2, ab);
sw.Close();
```

下列範例代表序列化的工作流程。

```xaml
<Activity
  x:TypeArguments="x:Int32"
  x:Class="Add"
  xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
  <x:Members>
    <x:Property Name="Operand1" Type="InArgument(x:Int32)" />
    <x:Property Name="Operand2" Type="InArgument(x:Int32)" />
  </x:Members>
  <Sequence>
    <WriteLine Text="[Operand1.ToString() + " + " + Operand2.ToString()]" />
    <Assign x:TypeArguments="x:Int32" Value="[Operand1 + Operand2]">
      <Assign.To>
        <OutArgument x:TypeArguments="x:Int32">
          <ArgumentReference x:TypeArguments="x:Int32" ArgumentName="Result" />
          </OutArgument>
      </Assign.To>
    </Assign>
  </Sequence>
</Activity>
```

若要載入序列化的工作流程，請使用 <xref:System.Activities.XamlIntegration.ActivityXamlServices> <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> 方法。 這個方法接受序列化的工作流程定義，並傳回代表工作流程定義的 <xref:System.Activities.DynamicActivity>。 請注意，等到驗證程序期間呼叫 <xref:System.Activities.Activity.CacheMetadata%2A> 主體上的 <xref:System.Activities.DynamicActivity> 時，XAML 才會還原序列化。 如果未明確呼叫驗證，則會在叫用工作流程時執行。 如果 XAML 工作流程定義無效，則會擲回 <xref:System.ArgumentException> 例外狀況。 從 <xref:System.Activities.Activity.CacheMetadata%2A> 擲回的任何例外狀況會從 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 呼叫中逸出，而且必須由呼叫端處理。 在下列範例中，會載入上一個範例的序列化工作流程，並透過 <xref:System.Activities.WorkflowInvoker> 叫用它。

[!code-csharp[CFX_WorkflowApplicationExample#43](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#43)]

當叫用這個工作流程時，主控台就會顯示下列輸出。

**25 + 15**\
**40**

> [!NOTE]
> 如需使用輸入和輸出引數叫用工作流程的詳細資訊，請參閱[使用 WorkflowInvoker 和 WorkflowApplication](using-workflowinvoker-and-workflowapplication.md)和 <xref:System.Activities.WorkflowInvoker.Invoke%2A> 。

如果序列化的工作流程包含 c # 運算式，則將 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings> 其 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> 屬性設為的實例 `true` 必須當做參數傳遞至 <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A?displayProperty=nameWithType> ，否則會擲回， <xref:System.NotSupportedException> 並顯示類似下列的訊息： **Expression 活動類型 ' CSharpValue ' 1 ' 需要編譯才能執行。 請確定已編譯工作流程。**

```csharp
ActivityXamlServicesSettings settings = new ActivityXamlServicesSettings
{
    CompileExpressions = true
};

DynamicActivity<int> wf = ActivityXamlServices.Load(new StringReader(serializedAB), settings) as DynamicActivity<int>;
```

如需詳細資訊，請參閱[c # 運算式](csharp-expressions.md)。

您也可以使用方法，將序列化的工作流程定義載入至 <xref:System.Activities.ActivityBuilder> 實例 <xref:System.Activities.XamlIntegration.ActivityXamlServices> <xref:System.Activities.XamlIntegration.ActivityXamlServices.CreateBuilderReader%2A> 。 將序列化的工作流程載入實例之後 <xref:System.Activities.ActivityBuilder> ，即可加以檢查和修改。 對自訂工作流程設計工具作者來說，這項功能很實用，在設計過程中提供了儲存及重新載入工作流程定義的機制。 在下列範例中，會載入上一個範例的序列化工作流程定義，並檢查其屬性。

[!code-csharp[CFX_WorkflowApplicationExample#44](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#44)]
