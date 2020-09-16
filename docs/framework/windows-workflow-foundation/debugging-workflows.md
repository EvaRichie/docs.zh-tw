---
title: 偵錯工作流程
ms.date: 03/30/2017
ms.assetid: b23b4814-ebb1-4c51-b7a9-469f4da7a96d
ms.openlocfilehash: 31c688f5f45b41f337176108486ec2074e1915a7
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90543832"
---
# <a name="debugging-workflows"></a><span data-ttu-id="58246-102">偵錯工作流程</span><span class="sxs-lookup"><span data-stu-id="58246-102">Debugging Workflows</span></span>

[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]<span data-ttu-id="58246-103">提供一些從開發環境進行偵錯工作流程的選項。</span><span class="sxs-lookup"><span data-stu-id="58246-103">offers several options for debugging running workflows from the development environment.</span></span> <span data-ttu-id="58246-104">可在設計工具、XAML 與程式碼中將工作流程偵錯。</span><span class="sxs-lookup"><span data-stu-id="58246-104">Workflows can be debugged in the designer, in XAML, and in code.</span></span>

## <a name="debugging-in-the-workflow-designer"></a><span data-ttu-id="58246-105">在工作流程設計工具中偵錯</span><span class="sxs-lookup"><span data-stu-id="58246-105">Debugging in the Workflow Designer</span></span>

<span data-ttu-id="58246-106">您可以在工作流程設計工具中的活動上設定中斷點，方法是反白顯示活動，然後按下 <kbd>F9</kbd> 或使用活動的內容功能表。</span><span class="sxs-lookup"><span data-stu-id="58246-106">Breakpoints can be set on activities in the workflow designer by either highlighting the activity and pressing <kbd>F9</kbd> or by using the activity’s context menu.</span></span> <span data-ttu-id="58246-107">執行工作流程，然後當工作流程主機正在偵錯模式中執行時中斷。</span><span class="sxs-lookup"><span data-stu-id="58246-107">Execution of the workflow then breaks when the workflow host is run in debug mode.</span></span> <span data-ttu-id="58246-108">在下列螢幕擷取畫面中，工作流程的執行已暫停於一個中斷點。</span><span class="sxs-lookup"><span data-stu-id="58246-108">In the following screenshot, workflow execution is paused at a breakpoint.</span></span> <span data-ttu-id="58246-109">如需詳細資訊，請參閱 [使用工作流程設計工具來調試工作流程](/visualstudio/workflow-designer/debugging-workflows-with-the-workflow-designer)。</span><span class="sxs-lookup"><span data-stu-id="58246-109">For more information, see [Debugging Workflows with the Workflow Designer](/visualstudio/workflow-designer/debugging-workflows-with-the-workflow-designer).</span></span>

## <a name="debugging-in-xaml"></a><span data-ttu-id="58246-110">在 XAML 中偵錯</span><span class="sxs-lookup"><span data-stu-id="58246-110">Debugging in XAML</span></span>

<span data-ttu-id="58246-111">如果工作流程在設計工具中的中斷點上暫停，即可在 XAML 中偵錯工作流程。</span><span class="sxs-lookup"><span data-stu-id="58246-111">If a workflow has paused at a breakpoint in the designer, the workflow can also be debugged in XAML.</span></span> <span data-ttu-id="58246-112">若要在 XAML 中查看執行的點，請在工作流程執行暫停時，于工作流程設計工具中選取 [ **XAML 視圖** ]。</span><span class="sxs-lookup"><span data-stu-id="58246-112">To view the point of execution in XAML, select **XAML View** in the workflow designer when workflow execution is paused.</span></span> <span data-ttu-id="58246-113">從解決方案總管的設計工具中重新開啟工作流程，即可將偵錯切換回設計工具。</span><span class="sxs-lookup"><span data-stu-id="58246-113">Debugging can be switched back to the designer by re-opening the workflow in the designer from the solution explorer.</span></span> <span data-ttu-id="58246-114">如需詳細資訊，請參閱 [如何：使用工作流程設計工具進行 XAML 的調試](/visualstudio/workflow-designer/how-to-debug-xaml-with-the-workflow-designer)程式。</span><span class="sxs-lookup"><span data-stu-id="58246-114">For more information, see [How to: Debug XAML with the Workflow Designer](/visualstudio/workflow-designer/how-to-debug-xaml-with-the-workflow-designer).</span></span>

## <a name="debugging-in-code"></a><span data-ttu-id="58246-115">在程式碼中偵錯</span><span class="sxs-lookup"><span data-stu-id="58246-115">Debugging in Code</span></span>

<span data-ttu-id="58246-116">若要設定中斷點，請按一下程式碼窗格的左邊界，或在您要設定它的行上按 <kbd>F9</kbd> 。</span><span class="sxs-lookup"><span data-stu-id="58246-116">To set a breakpoint, click the left margin of the code pane, or press <kbd>F9</kbd> with the cursor at the line where you want to set it.</span></span>

## <a name="attaching-to-a-workflow-process"></a><span data-ttu-id="58246-117">附加至工作流程處理序</span><span class="sxs-lookup"><span data-stu-id="58246-117">Attaching to a Workflow Process</span></span>

<span data-ttu-id="58246-118">工作流程偵錯也支援使用 Visual Studio 的基礎結構來附加至處理序。</span><span class="sxs-lookup"><span data-stu-id="58246-118">Workflow debugging also supports using Visual Studio’s infrastructure to attach to a process.</span></span> <span data-ttu-id="58246-119">這可讓工作流程的作者在不同的主機環境中 (例如 Internet Information Services (IIS) 7.0) 執行時偵錯工作流程。</span><span class="sxs-lookup"><span data-stu-id="58246-119">This enables the workflow author to debug a workflow running in a different host environment such as Internet Information Services (IIS) 7.0.</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="58246-120">Remote Debugging</span><span class="sxs-lookup"><span data-stu-id="58246-120">Remote Debugging</span></span>

<span data-ttu-id="58246-121">Windows Workflow Foundation (WF) 遠端偵錯程式的功能，與其他 Visual Studio 元件的遠端偵錯程式相同。</span><span class="sxs-lookup"><span data-stu-id="58246-121">Windows Workflow Foundation (WF) remote debugging functions the same as remote debugging for other Visual Studio components.</span></span> <span data-ttu-id="58246-122">如需使用遠端偵錯程式的詳細資訊，請參閱 how [to：啟用遠端偵錯](/previous-versions/visualstudio/visual-studio-2010/febz73k0(v=vs.100))程式。</span><span class="sxs-lookup"><span data-stu-id="58246-122">For information on using remote debugging, see [How to: Enable Remote Debugging](/previous-versions/visualstudio/visual-studio-2010/febz73k0(v=vs.100)).</span></span>

> [!NOTE]
> <span data-ttu-id="58246-123">如果工作流程應用程式的目標為 x86 架構，並裝載在執行64位作業系統的電腦上，除非在遠端電腦上安裝 Visual Studio，或將工作流程應用程式的目標變更為 [ **任何 CPU**]，否則遠端偵錯程式將無法運作。</span><span class="sxs-lookup"><span data-stu-id="58246-123">If the workflow application targets the x86 architecture and is hosted on a computer running a 64 bit operating system, then remote debugging will not work unless Visual Studio is installed on the remote computer or the target for the workflow application is changed to **Any CPU**.</span></span>

## <a name="extending-the-workflow-debugging-service"></a><span data-ttu-id="58246-124">擴充工作流程偵錯服務</span><span class="sxs-lookup"><span data-stu-id="58246-124">Extending the Workflow Debugging Service</span></span>

<span data-ttu-id="58246-125">現在已公開工作流程偵錯程式服務，且可用於建立自訂應用程式，例如在重新裝載的設計工具中監控、模擬和偵錯。</span><span class="sxs-lookup"><span data-stu-id="58246-125">The workflow debugger service is now public and can be used to create custom applications such as monitoring, simulation, and debugging in a re-hosted designer.</span></span> <span data-ttu-id="58246-126">如需詳細資訊，請參閱 <xref:System.Activities.Presentation.Debug.DebuggerService> 文章。</span><span class="sxs-lookup"><span data-stu-id="58246-126">For more information, see the <xref:System.Activities.Presentation.Debug.DebuggerService> article.</span></span>
