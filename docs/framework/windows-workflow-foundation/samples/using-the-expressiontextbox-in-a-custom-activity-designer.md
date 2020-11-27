---
title: 使用自訂活動設計工具中的 ExpressionTextBox
ms.date: 03/30/2017
ms.assetid: f82e73e7-a256-4a4d-82b7-c0d62f4ab5e7
ms.openlocfilehash: dfb53096be59abd9924a024880d4125ca774d4b8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96267479"
---
# <a name="using-the-expressiontextbox-in-a-custom-activity-designer"></a>使用自訂活動設計工具中的 ExpressionTextBox

這個範例示範如何在自訂活動設計工具內使用 <xref:System.Activities.Presentation.View.ExpressionTextBox>。 自訂活動 `MultiAssign` 會將兩個字串值指派給兩個字串變數。 某些 <xref:System.Activities.Presentation.View.ExpressionTextBox> 控制項會繫結至 <xref:System.Activities.InArgument>，而某些則繫結至 <xref:System.Activities.OutArgument>。

## <a name="sample-details"></a>範例詳細資料

 `ArgumentToExpressionConverter` 是將運算式繫結至引數時所使用的型別轉換子。 `ConverterParameter` 必須適當地設定為 `In` 或 `Out`。 不支援 `InOut`。

 在 `UseLocationExpression` 上使用屬性 `OutArgument` 來指定運算式應該是左值 ( 「左值」或「位置值」 ) 運算式。 在大多數情況下，L-value 運算式是有效的 Visual Basic 識別碼，用來指出傳回的 `OutArgument` 為變數或引數名稱。

 在這個範例中，`MaxLines` 屬性設定為一，而且未設定 `MinLines`。 這表示 <xref:System.Activities.Presentation.View.ExpressionTextBox> 的固定大小為一行，不論使用者輸入多少的文字數量。 若要允許 <xref:System.Activities.Presentation.View.ExpressionTextBox> 成長來符合使用者輸入，請將 `MaxLines` 設定為大於 `MinLines`。

 ExpressionTextBox 只能繫結至引數，無法繫結至 CLR 屬性。

#### <a name="to-use-this-sample"></a>若要使用這個範例

1. 使用 Visual Studio 2010 開啟 ExpressionTextBoxSample .sln 檔案。

2. 若要建置此方案，請按 CTRL+SHIFT+B。

#### <a name="to-run-this-sample"></a>執行此範例

1. 將新的工作流程主控台應用程式加入至方案。

2. 從新的工作流程主控台應用程式專案加入 **ExpressionTextBoxSample** 專案的參考。

3. 建置方案。

4. 從 [工具箱] 將 [ **MultiAssign** ] 活動拖放到工作流程中。

> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\ExpressionTextBox`  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Activities.Presentation.View.ExpressionTextBox>
- [使用工作流程設計工具開發應用程式](/visualstudio/workflow-designer/developing-applications-with-the-workflow-designer)
