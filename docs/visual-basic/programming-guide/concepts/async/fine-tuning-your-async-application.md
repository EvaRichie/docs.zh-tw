---
title: 微調非同步應用程式
ms.date: 07/20/2015
ms.assetid: 4c3e7997-a95f-4fbe-a6ac-60ba042d30b9
ms.openlocfilehash: 6ad4f9a526e0497029ff8ddc3e93637a4f9acb00
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91075430"
---
# <a name="fine-tuning-your-async-application-visual-basic"></a><span data-ttu-id="506a8-102">微調非同步應用程式 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="506a8-102">Fine-Tuning Your Async Application (Visual Basic)</span></span>

<span data-ttu-id="506a8-103">您可以使用 <xref:System.Threading.Tasks.Task> 類型所提供的方法和屬性，來增加非同步應用程式的精確度和彈性。</span><span class="sxs-lookup"><span data-stu-id="506a8-103">You can add precision and flexibility to your async applications by using the methods and properties that the <xref:System.Threading.Tasks.Task> type makes available.</span></span> <span data-ttu-id="506a8-104">本節的主題會示範使用 <xref:System.Threading.CancellationToken> 以及 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> 等重要 `Task` 方法的範例。</span><span class="sxs-lookup"><span data-stu-id="506a8-104">The topics in this section show examples that use <xref:System.Threading.CancellationToken> and important `Task` methods such as <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> and <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType>.</span></span>  
  
 <span data-ttu-id="506a8-105">您可以使用 `WhenAny` 和 `WhenAll`，更輕鬆地啟動多個工作，並藉由監視單一工作等候其完成。</span><span class="sxs-lookup"><span data-stu-id="506a8-105">By using `WhenAny` and `WhenAll`, you can more easily start multiple tasks and await their completion by monitoring a single task.</span></span>  
  
- <span data-ttu-id="506a8-106">`WhenAny` 會在集合中的任何工作完成時，傳回一個完成的工作。</span><span class="sxs-lookup"><span data-stu-id="506a8-106">`WhenAny` returns a task that completes when any task in a collection is complete.</span></span>  
  
     <span data-ttu-id="506a8-107">如需使用的範例 `WhenAny` ，請參閱  [在完成前取消剩餘的非同步工作 (Visual Basic) ](cancel-remaining-async-tasks-after-one-is-complete.md)並 [啟動多個非同步工作，並在完成 (Visual Basic) 時進行處理 ](start-multiple-async-tasks-and-process-them-as-they-complete.md)。</span><span class="sxs-lookup"><span data-stu-id="506a8-107">For examples that use `WhenAny`, see  [Cancel Remaining Async Tasks after One Is Complete (Visual Basic)](cancel-remaining-async-tasks-after-one-is-complete.md)and [Start Multiple Async Tasks and Process Them As They Complete (Visual Basic)](start-multiple-async-tasks-and-process-them-as-they-complete.md).</span></span>  
  
- <span data-ttu-id="506a8-108">`WhenAll` 會在集合中的所有工作完成時，傳回一個完成的工作。</span><span class="sxs-lookup"><span data-stu-id="506a8-108">`WhenAll` returns a task that completes when all tasks in a collection are complete.</span></span>  
  
     <span data-ttu-id="506a8-109">如需詳細資訊和使用的範例 `WhenAll` ，請參閱 [如何：使用 System.threading.tasks.task.whenall 擴充非同步逐步解說 (Visual Basic) ](how-to-extend-the-async-walkthrough-by-using-task-whenall.md)。</span><span class="sxs-lookup"><span data-stu-id="506a8-109">For more information and an example that uses `WhenAll`, see [How to: Extend the Async Walkthrough by Using Task.WhenAll (Visual Basic)](how-to-extend-the-async-walkthrough-by-using-task-whenall.md).</span></span>  
  
 <span data-ttu-id="506a8-110">本節包含下列範例。</span><span class="sxs-lookup"><span data-stu-id="506a8-110">This section includes the following examples.</span></span>  
  
- <span data-ttu-id="506a8-111">[取消非同步工作或工作清單 (Visual Basic) ](cancel-an-async-task-or-a-list-of-tasks.md)。</span><span class="sxs-lookup"><span data-stu-id="506a8-111">[Cancel an Async Task or a List of Tasks (Visual Basic)](cancel-an-async-task-or-a-list-of-tasks.md).</span></span>  
  
- [<span data-ttu-id="506a8-112">在一段時間後取消非同步工作 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="506a8-112">Cancel Async Tasks after a Period of Time (Visual Basic)</span></span>](cancel-async-tasks-after-a-period-of-time.md)  
  
- [<span data-ttu-id="506a8-113">當其中一項工作完成時，取消剩餘的非同步工作 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="506a8-113">Cancel Remaining Async Tasks after One Is Complete (Visual Basic)</span></span>](cancel-remaining-async-tasks-after-one-is-complete.md)  
  
- [<span data-ttu-id="506a8-114">啟動多項非同步工作並在它們完成時進行處理 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="506a8-114">Start Multiple Async Tasks and Process Them As They Complete (Visual Basic)</span></span>](start-multiple-async-tasks-and-process-them-as-they-complete.md)  
  
> [!NOTE]
> <span data-ttu-id="506a8-115">若要執行範例，您必須在電腦上安裝 Visual Studio 2012 或更新版本以及 .NET Framework 4.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="506a8-115">To run the examples, you must have Visual Studio 2012 or newer and the .NET Framework 4.5 or newer installed on your computer.</span></span>  
  
 <span data-ttu-id="506a8-116">這些專案會建立 UI，其中包含一個啟動處理序的按鈕和一個取消處理序的按鈕，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="506a8-116">The projects create a UI that contains a button that starts the process and a button that cancels it, as the following image shows.</span></span> <span data-ttu-id="506a8-117">這兩個按鈕的名稱分別是 `startButton` 和 `cancelButton`。</span><span class="sxs-lookup"><span data-stu-id="506a8-117">The buttons are named `startButton` and `cancelButton`.</span></span>  
  
 <span data-ttu-id="506a8-118">![具有 [取消] 按鈕的 WPF 視窗](./media/fine-tuning-your-async-application/cancellation-and-start-button.png "具有 [開始] 和 [停止] 按鈕的對話方塊")</span><span class="sxs-lookup"><span data-stu-id="506a8-118">![WPF window with Cancel button](./media/fine-tuning-your-async-application/cancellation-and-start-button.png "Dialog box with a Start and Stop button")</span></span>  
  
 <span data-ttu-id="506a8-119">您可以從 [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea) (非同步範例：微調應用程式) 下載完整 Windows Presentation Foundation (WPF) 專案。</span><span class="sxs-lookup"><span data-stu-id="506a8-119">You can download the complete Windows Presentation Foundation (WPF) projects from [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="506a8-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="506a8-120">See also</span></span>

- [<span data-ttu-id="506a8-121">使用 Async 和 Await 進行非同步程式設計 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="506a8-121">Asynchronous Programming with Async and Await (Visual Basic)</span></span>](index.md)
