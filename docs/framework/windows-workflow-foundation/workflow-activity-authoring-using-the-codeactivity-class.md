---
title: 使用 CodeActivity 類別撰寫工作流程活動
ms.date: 03/30/2017
ms.assetid: cfe315c1-f86d-43ec-b9ce-2f8c469b1106
ms.openlocfilehash: 714e0971a006db20d002b0f3a486533b1357fba7
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293815"
---
# <a name="workflow-activity-authoring-using-the-codeactivity-class"></a>使用 CodeActivity 類別撰寫工作流程活動

繼承自 <xref:System.Activities.CodeActivity> 所建立的活動可藉由覆寫 <xref:System.Activities.CodeActivity.Execute%2A> 方法來實作基本命令式行為。

## <a name="using-codeactivitycontext"></a>使用 CodeActivityContext

 工作流程執行階段的功能可透過 <xref:System.Activities.CodeActivity.Execute%2A> 方法內部存取，方法是使用 `context` 參數的成員 (型別為 <xref:System.Activities.CodeActivityContext>)。 透過 <xref:System.Activities.CodeActivityContext> 可使用的功能如下：

- 取得與設定引數和變數的值。

- 使用 <xref:System.Activities.CodeActivityContext.Track%2A> 自訂追蹤功能。

- 使用 <xref:System.Activities.CodeActivityContext.GetProperty%2A> 存取活動的執行屬性。

#### <a name="to-create-a-custom-activity-that-inherits-from-codeactivity"></a>若要建立繼承自 CodeActivity 的自訂活動

1. 開啟 Visual Studio 2010。

2. 依 **序選取 [** 檔案]、[ **新增**] 和 [ **專案**]。 在 [**專案類型**] 視窗中選取 [ **Visual c #** ] 底下的 **工作流程 4.0** ，然後選取 [ **v2010]** ] 節點。 選取 [**範本**] 視窗中的 [**活動程式庫**]。 將新專案命名為 HelloActivity。

3. 以滑鼠右鍵按一下 HelloActivity 專案中的 [Activity1]，然後選取 [ **刪除**]。

4. 以滑鼠右鍵按一下 HelloActivity 專案，然後依序選取 [ **加入** ] 和 [ **類別**]。 將新類別命名為 HelloActivity.cs。

5. 在 HelloActivity.cs 檔案中加入下列 `using` 指示詞。

    ```csharp
    using System.Activities;
    using System.Activities.Statements;
    ```

6. 將基底類別加入至類別宣告，使新的類別繼承自 <xref:System.Activities.CodeActivity>。

    ```csharp
    class HelloActivity : CodeActivity
    ```

7. 加入 <xref:System.Activities.CodeActivity.Execute%2A> 方法，藉此將功能加入至類別中。

    ```csharp
    protected override void Execute(CodeActivityContext context)
    {
        Console.WriteLine("Hello World!");
    }
    ```

8. 使用 <xref:System.Activities.CodeActivityContext> 建立追蹤記錄。

    ```csharp
    protected override void Execute(CodeActivityContext context)
    {
        Console.WriteLine("Hello World!");
        CustomTrackingRecord record = new CustomTrackingRecord("MyRecord");
        record.Data.Add(new KeyValuePair<String, Object>("ExecutionTime", DateTime.Now));
        context.Track(record);
    }
    ```
