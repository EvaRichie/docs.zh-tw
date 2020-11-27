---
title: NativeActivity 基底類別
ms.date: 03/30/2017
ms.assetid: 254a4c50-425b-426d-a32f-0f7234925bac
ms.openlocfilehash: d875f62dacadb2baf6b5d7e93ddb2933aed9cdb0
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96274955"
---
# <a name="nativeactivity-base-class"></a><span data-ttu-id="ab803-102">NativeActivity 基底類別</span><span class="sxs-lookup"><span data-stu-id="ab803-102">NativeActivity Base Class</span></span>

<span data-ttu-id="ab803-103"><xref:System.Activities.NativeActivity> 是具有受保護建構函式的抽象類別。</span><span class="sxs-lookup"><span data-stu-id="ab803-103"><xref:System.Activities.NativeActivity> is an abstract class with a protected constructor.</span></span> <span data-ttu-id="ab803-104">如同 <xref:System.Activities.CodeActivity>，<xref:System.Activities.NativeActivity> 會用於透過實作 <xref:System.Activities.NativeActivity.Execute%2A> 方法的方式寫入命令式行為。</span><span class="sxs-lookup"><span data-stu-id="ab803-104">Like <xref:System.Activities.CodeActivity>, <xref:System.Activities.NativeActivity> is used for writing imperative behavior by implementing an <xref:System.Activities.NativeActivity.Execute%2A> method.</span></span> <span data-ttu-id="ab803-105">不同於 <xref:System.Activities.CodeActivity> 的是，<xref:System.Activities.NativeActivity> 可透過傳遞至 <xref:System.Activities.NativeActivityContext> 方法的 <xref:System.Activities.NativeActivity.Execute%2A> 物件，存取工作流程執行階段的所有公開功能。</span><span class="sxs-lookup"><span data-stu-id="ab803-105">Unlike <xref:System.Activities.CodeActivity>, <xref:System.Activities.NativeActivity> has access to all of the exposed features of the workflow runtime through the <xref:System.Activities.NativeActivityContext> object passed to the <xref:System.Activities.NativeActivity.Execute%2A> method.</span></span>

## <a name="using-nativeactivitycontext"></a><span data-ttu-id="ab803-106">使用 NativeActivityContext</span><span class="sxs-lookup"><span data-stu-id="ab803-106">Using NativeActivityContext</span></span>

 <span data-ttu-id="ab803-107">工作流程執行階段的功能可透過 <xref:System.Activities.NativeActivity.Execute%2A> 方法內部存取，方法是使用 `context` 參數的成員 (型別為 <xref:System.Activities.NativeActivityContext>)。</span><span class="sxs-lookup"><span data-stu-id="ab803-107">Features of the workflow runtime can be accessed from within the <xref:System.Activities.NativeActivity.Execute%2A> method by using members of the `context` parameter, of type <xref:System.Activities.NativeActivityContext>.</span></span> <span data-ttu-id="ab803-108">透過 <xref:System.Activities.NativeActivityContext> 可使用的功能如下：</span><span class="sxs-lookup"><span data-stu-id="ab803-108">The features available through <xref:System.Activities.NativeActivityContext> include the following:</span></span>

- <span data-ttu-id="ab803-109">取得與設定引數和變數。</span><span class="sxs-lookup"><span data-stu-id="ab803-109">Getting and setting of arguments and variables.</span></span>

- <span data-ttu-id="ab803-110">使用 <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A> 排程子活動。</span><span class="sxs-lookup"><span data-stu-id="ab803-110">Scheduling child activities with <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A></span></span>

- <span data-ttu-id="ab803-111">使用 <xref:System.Activities.NativeActivityContext.Abort%2A> 中止活動執行。</span><span class="sxs-lookup"><span data-stu-id="ab803-111">Aborting activity execution using <xref:System.Activities.NativeActivityContext.Abort%2A>.</span></span>

- <span data-ttu-id="ab803-112">使用 <xref:System.Activities.NativeActivityContext.CancelChild%2A> 和 <xref:System.Activities.NativeActivityContext.CancelChildren%2A> 取消子執行。</span><span class="sxs-lookup"><span data-stu-id="ab803-112">Canceling child execution using <xref:System.Activities.NativeActivityContext.CancelChild%2A> and <xref:System.Activities.NativeActivityContext.CancelChildren%2A>.</span></span>

- <span data-ttu-id="ab803-113">使用 <xref:System.Activities.NativeActivityContext.CreateBookmark%2A>、<xref:System.Activities.NativeActivityContext.RemoveBookmark%2A> 和 <xref:System.Activities.NativeActivityContext.ResumeBookmark%2A> 之類的方法存取活動書籤。</span><span class="sxs-lookup"><span data-stu-id="ab803-113">Access to activity bookmarks using such methods as <xref:System.Activities.NativeActivityContext.CreateBookmark%2A>, <xref:System.Activities.NativeActivityContext.RemoveBookmark%2A>, and <xref:System.Activities.NativeActivityContext.ResumeBookmark%2A>.</span></span>

- <span data-ttu-id="ab803-114">使用 <xref:System.Activities.CodeActivityContext.Track%2A> 自訂追蹤功能。</span><span class="sxs-lookup"><span data-stu-id="ab803-114">Custom tracking features using <xref:System.Activities.CodeActivityContext.Track%2A>.</span></span>

- <span data-ttu-id="ab803-115">使用 <xref:System.Activities.CodeActivityContext.GetProperty%2A> 和 <xref:System.Activities.NativeActivityContext.GetValue%2A> 存取活動的執行屬性和值屬性。</span><span class="sxs-lookup"><span data-stu-id="ab803-115">Access to the activity’s execution properties and value properties using <xref:System.Activities.CodeActivityContext.GetProperty%2A> and <xref:System.Activities.NativeActivityContext.GetValue%2A>.</span></span>

- <span data-ttu-id="ab803-116">使用 <xref:System.Activities.NativeActivityContext.ScheduleAction%2A> 和 <xref:System.Activities.NativeActivityContext.ScheduleFunc%2A> 排訂活動動作與功能。</span><span class="sxs-lookup"><span data-stu-id="ab803-116">Scheduling activity actions and functions using <xref:System.Activities.NativeActivityContext.ScheduleAction%2A> and <xref:System.Activities.NativeActivityContext.ScheduleFunc%2A>.</span></span>

### <a name="to-create-a-custom-activity-that-inherits-from-nativeactivity"></a><span data-ttu-id="ab803-117">若要建立繼承自 NativeActivity 的自訂活動</span><span class="sxs-lookup"><span data-stu-id="ab803-117">To create a custom activity that inherits from NativeActivity</span></span>

1. <span data-ttu-id="ab803-118">OpenVisual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="ab803-118">OpenVisual Studio 2010.</span></span>

2. <span data-ttu-id="ab803-119">依 **序選取 [** 檔案]、[ **新增**] 和 [ **專案**]。</span><span class="sxs-lookup"><span data-stu-id="ab803-119">Select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="ab803-120">在 [**專案類型**] 視窗中選取 [ **Visual c #** ] 底下的 **工作流程 4.0** ，然後選取 [ **v2010]** ] 節點。</span><span class="sxs-lookup"><span data-stu-id="ab803-120">Select **Workflow 4.0** under **Visual C#** in the **Project Types** window, and select the **v2010** node.</span></span> <span data-ttu-id="ab803-121">選取 [**範本**] 視窗中的 [**活動程式庫**]。</span><span class="sxs-lookup"><span data-stu-id="ab803-121">Select **Activity Library** in the **Templates** window.</span></span> <span data-ttu-id="ab803-122">將新專案命名為 HelloActivity。</span><span class="sxs-lookup"><span data-stu-id="ab803-122">Name the new project HelloActivity.</span></span>

3. <span data-ttu-id="ab803-123">以滑鼠右鍵按一下 HelloActivity 專案中的 [Activity1]，然後選取 [ **刪除**]。</span><span class="sxs-lookup"><span data-stu-id="ab803-123">Right-click Activity1.xaml in the HelloActivity project and select **Delete**.</span></span>

4. <span data-ttu-id="ab803-124">以滑鼠右鍵按一下 HelloActivity 專案，然後依序選取 [ **加入**] 和 [ **類別**]。</span><span class="sxs-lookup"><span data-stu-id="ab803-124">Right-click the HelloActivity project and select **Add**, and then **Class**.</span></span> <span data-ttu-id="ab803-125">將新類別命名為 HelloActivity.cs。</span><span class="sxs-lookup"><span data-stu-id="ab803-125">Name the new class HelloActivity.cs.</span></span>

5. <span data-ttu-id="ab803-126">在 HelloActivity.cs 檔案中加入下列 `using` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="ab803-126">In the HelloActivity.cs file, add the following `using` directives.</span></span>

    ```csharp
    using System.Activities;
    using System.Activities.Statements;
    ```

6. <span data-ttu-id="ab803-127">將基底類別加入至類別宣告，使新的類別繼承自 <xref:System.Activities.NativeActivity>。</span><span class="sxs-lookup"><span data-stu-id="ab803-127">Make the new class inherit from <xref:System.Activities.NativeActivity> by adding a base class to the class declaration.</span></span>

    ```csharp
    class HelloActivity : NativeActivity
    ```

7. <span data-ttu-id="ab803-128">加入 <xref:System.Activities.NativeActivity.Execute%2A> 方法，藉此將功能加入至類別中。</span><span class="sxs-lookup"><span data-stu-id="ab803-128">Add functionality to the class by adding an <xref:System.Activities.NativeActivity.Execute%2A> method.</span></span>

    ```csharp
    protected override void Execute(NativeActivityContext context)
    {
        Console.WriteLine("Hello World!");
    }
    ```

8. <span data-ttu-id="ab803-129">覆寫 <xref:System.Activities.NativeActivity.CacheMetadata%2A> 方法，並呼叫適當的 Add 方法，讓工作流程執行階段知道自訂活動的變數、引數、子系和委派。</span><span class="sxs-lookup"><span data-stu-id="ab803-129">Override the <xref:System.Activities.NativeActivity.CacheMetadata%2A> method and call the appropriate Add method to let the workflow runtime know about the custom activity’s variables, arguments, children, and delegates.</span></span> <span data-ttu-id="ab803-130">如需詳細資訊，請參閱 <xref:System.Activities.NativeActivityMetadata> 類別。</span><span class="sxs-lookup"><span data-stu-id="ab803-130">For more information see the <xref:System.Activities.NativeActivityMetadata> class.</span></span>

9. <span data-ttu-id="ab803-131">使用 <xref:System.Activities.NativeActivityContext> 物件排程書籤。</span><span class="sxs-lookup"><span data-stu-id="ab803-131">Use the <xref:System.Activities.NativeActivityContext> object to schedule a bookmark.</span></span> <span data-ttu-id="ab803-132">如需如何建立、排程和繼續書籤的詳細資訊，請參閱 <xref:System.Activities.WorkflowApplicationIdleEventArgs.Bookmarks%2A>。</span><span class="sxs-lookup"><span data-stu-id="ab803-132">See <xref:System.Activities.WorkflowApplicationIdleEventArgs.Bookmarks%2A> for details on how to create, schedule, and resume a bookmark.</span></span>

    ```csharp
    protected override void Execute(NativeActivityContext context)
        {
            // Create a Bookmark and wait for it to be resumed.
            context.CreateBookmark(BookmarkName.Get(context),
                new BookmarkCallback(OnResumeBookmark));
        }
    ```
