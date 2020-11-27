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
# <a name="workflow-activity-authoring-using-the-codeactivity-class"></a><span data-ttu-id="70f55-102">使用 CodeActivity 類別撰寫工作流程活動</span><span class="sxs-lookup"><span data-stu-id="70f55-102">Workflow Activity Authoring Using the CodeActivity Class</span></span>

<span data-ttu-id="70f55-103">繼承自 <xref:System.Activities.CodeActivity> 所建立的活動可藉由覆寫 <xref:System.Activities.CodeActivity.Execute%2A> 方法來實作基本命令式行為。</span><span class="sxs-lookup"><span data-stu-id="70f55-103">Activities created by inheriting from <xref:System.Activities.CodeActivity> can implement basic imperative behavior by overriding the <xref:System.Activities.CodeActivity.Execute%2A> method.</span></span>

## <a name="using-codeactivitycontext"></a><span data-ttu-id="70f55-104">使用 CodeActivityContext</span><span class="sxs-lookup"><span data-stu-id="70f55-104">Using CodeActivityContext</span></span>

 <span data-ttu-id="70f55-105">工作流程執行階段的功能可透過 <xref:System.Activities.CodeActivity.Execute%2A> 方法內部存取，方法是使用 `context` 參數的成員 (型別為 <xref:System.Activities.CodeActivityContext>)。</span><span class="sxs-lookup"><span data-stu-id="70f55-105">Features of the workflow runtime can be accessed from within the <xref:System.Activities.CodeActivity.Execute%2A> method by using members of the `context` parameter, of type <xref:System.Activities.CodeActivityContext>.</span></span> <span data-ttu-id="70f55-106">透過 <xref:System.Activities.CodeActivityContext> 可使用的功能如下：</span><span class="sxs-lookup"><span data-stu-id="70f55-106">The features available through <xref:System.Activities.CodeActivityContext> include the following:</span></span>

- <span data-ttu-id="70f55-107">取得與設定引數和變數的值。</span><span class="sxs-lookup"><span data-stu-id="70f55-107">Getting and setting the values of variables and arguments.</span></span>

- <span data-ttu-id="70f55-108">使用 <xref:System.Activities.CodeActivityContext.Track%2A> 自訂追蹤功能。</span><span class="sxs-lookup"><span data-stu-id="70f55-108">Custom tracking features using <xref:System.Activities.CodeActivityContext.Track%2A>.</span></span>

- <span data-ttu-id="70f55-109">使用 <xref:System.Activities.CodeActivityContext.GetProperty%2A> 存取活動的執行屬性。</span><span class="sxs-lookup"><span data-stu-id="70f55-109">Access to the activity’s execution properties using <xref:System.Activities.CodeActivityContext.GetProperty%2A>.</span></span>

#### <a name="to-create-a-custom-activity-that-inherits-from-codeactivity"></a><span data-ttu-id="70f55-110">若要建立繼承自 CodeActivity 的自訂活動</span><span class="sxs-lookup"><span data-stu-id="70f55-110">To create a custom activity that inherits from CodeActivity</span></span>

1. <span data-ttu-id="70f55-111">開啟 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="70f55-111">Open Visual Studio 2010.</span></span>

2. <span data-ttu-id="70f55-112">依 **序選取 [** 檔案]、[ **新增**] 和 [ **專案**]。</span><span class="sxs-lookup"><span data-stu-id="70f55-112">Select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="70f55-113">在 [**專案類型**] 視窗中選取 [ **Visual c #** ] 底下的 **工作流程 4.0** ，然後選取 [ **v2010]** ] 節點。</span><span class="sxs-lookup"><span data-stu-id="70f55-113">Select **Workflow 4.0** under **Visual C#** in the **Project Types** window, and select the **v2010** node.</span></span> <span data-ttu-id="70f55-114">選取 [**範本**] 視窗中的 [**活動程式庫**]。</span><span class="sxs-lookup"><span data-stu-id="70f55-114">Select **Activity Library** in the **Templates** window.</span></span> <span data-ttu-id="70f55-115">將新專案命名為 HelloActivity。</span><span class="sxs-lookup"><span data-stu-id="70f55-115">Name the new project HelloActivity.</span></span>

3. <span data-ttu-id="70f55-116">以滑鼠右鍵按一下 HelloActivity 專案中的 [Activity1]，然後選取 [ **刪除**]。</span><span class="sxs-lookup"><span data-stu-id="70f55-116">Right-click Activity1.xaml in the HelloActivity project and select **Delete**.</span></span>

4. <span data-ttu-id="70f55-117">以滑鼠右鍵按一下 HelloActivity 專案，然後依序選取 [ **加入** ] 和 [ **類別**]。</span><span class="sxs-lookup"><span data-stu-id="70f55-117">Right-click the HelloActivity project and select **Add** , and then **Class**.</span></span> <span data-ttu-id="70f55-118">將新類別命名為 HelloActivity.cs。</span><span class="sxs-lookup"><span data-stu-id="70f55-118">Name the new class HelloActivity.cs.</span></span>

5. <span data-ttu-id="70f55-119">在 HelloActivity.cs 檔案中加入下列 `using` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="70f55-119">In the HelloActivity.cs file, add the following `using` directives.</span></span>

    ```csharp
    using System.Activities;
    using System.Activities.Statements;
    ```

6. <span data-ttu-id="70f55-120">將基底類別加入至類別宣告，使新的類別繼承自 <xref:System.Activities.CodeActivity>。</span><span class="sxs-lookup"><span data-stu-id="70f55-120">Make the new class inherit from <xref:System.Activities.CodeActivity> by adding a base class to the class declaration.</span></span>

    ```csharp
    class HelloActivity : CodeActivity
    ```

7. <span data-ttu-id="70f55-121">加入 <xref:System.Activities.CodeActivity.Execute%2A> 方法，藉此將功能加入至類別中。</span><span class="sxs-lookup"><span data-stu-id="70f55-121">Add functionality to the class by adding an <xref:System.Activities.CodeActivity.Execute%2A> method.</span></span>

    ```csharp
    protected override void Execute(CodeActivityContext context)
    {
        Console.WriteLine("Hello World!");
    }
    ```

8. <span data-ttu-id="70f55-122">使用 <xref:System.Activities.CodeActivityContext> 建立追蹤記錄。</span><span class="sxs-lookup"><span data-stu-id="70f55-122">Use the <xref:System.Activities.CodeActivityContext> to create a tracking record.</span></span>

    ```csharp
    protected override void Execute(CodeActivityContext context)
    {
        Console.WriteLine("Hello World!");
        CustomTrackingRecord record = new CustomTrackingRecord("MyRecord");
        record.Data.Add(new KeyValuePair<String, Object>("ExecutionTime", DateTime.Now));
        context.Track(record);
    }
    ```
