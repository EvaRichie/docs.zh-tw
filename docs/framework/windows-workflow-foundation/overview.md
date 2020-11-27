---
title: Windows Workflow 概觀
description: 本文說明 Workflow Foundation 工作流程，這些工作流程是描述真實世界進程的模型。
ms.date: 03/30/2017
ms.assetid: fc44adbe-1412-49ae-81af-0298be44aae6
ms.openlocfilehash: f966aa2b62a743358d4c1ad18f237f988924014d
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268673"
---
# <a name="windows-workflow-overview"></a><span data-ttu-id="084f7-103">Windows Workflow 概觀</span><span class="sxs-lookup"><span data-stu-id="084f7-103">Windows Workflow Overview</span></span>

<span data-ttu-id="084f7-104">工作流程是一組稱為活動的 elemental 單位，這些 *活動* 會儲存為描述真實世界進程的模型。</span><span class="sxs-lookup"><span data-stu-id="084f7-104">A workflow is a set of elemental units called *activities* that are stored as a model that describes a real-world process.</span></span> <span data-ttu-id="084f7-105">工作流程能夠描述執行的順序，以及短期工作和長期工作之間的相依關係。</span><span class="sxs-lookup"><span data-stu-id="084f7-105">Workflows provide a way of describing the order of execution and dependent relationships between pieces of short- or long-running work.</span></span> <span data-ttu-id="084f7-106">這個工作會從頭到尾經過整個模型，而活動可能會由人員或系統功能執行。</span><span class="sxs-lookup"><span data-stu-id="084f7-106">This work passes through the model from start to finish, and activities might be executed by people or by system functions.</span></span>  
  
## <a name="workflow-run-time-engine"></a><span data-ttu-id="084f7-107">工作流程執行階段引擎</span><span class="sxs-lookup"><span data-stu-id="084f7-107">Workflow Run-time Engine</span></span>  

 <span data-ttu-id="084f7-108">每個執行中的工作流程執行個體是由同處理序執行階段引擎建立與維護的，主機處理序會透過以下其中一種方式與該引擎互動：</span><span class="sxs-lookup"><span data-stu-id="084f7-108">Every running workflow instance is created and maintained by an in-process run-time engine that the host process interacts with through one of the following:</span></span>  
  
- <span data-ttu-id="084f7-109"><xref:System.Activities.WorkflowInvoker>，如同方法一般叫用工作流程。</span><span class="sxs-lookup"><span data-stu-id="084f7-109">A <xref:System.Activities.WorkflowInvoker>, which invokes the workflow like a method.</span></span>  
  
- <span data-ttu-id="084f7-110"><xref:System.Activities.WorkflowApplication>，明確控制單一工作流程執行個體的執行。</span><span class="sxs-lookup"><span data-stu-id="084f7-110">A <xref:System.Activities.WorkflowApplication> for explicit control over the execution of a single workflow instance.</span></span>  
  
- <span data-ttu-id="084f7-111">在多個執行個體的案例中進行訊息式互動的 <xref:System.ServiceModel.WorkflowServiceHost>。</span><span class="sxs-lookup"><span data-stu-id="084f7-111">A <xref:System.ServiceModel.WorkflowServiceHost> for message-based interactions in multi-instance scenarios.</span></span>  
  
 <span data-ttu-id="084f7-112">這裡每個類別都會包含核心活動執行階段，此執行階段是以負責活動執行的 <xref:System.Activities.ActivityInstance> 來表示。</span><span class="sxs-lookup"><span data-stu-id="084f7-112">Each of these classes wraps the core activity runtime represented as a <xref:System.Activities.ActivityInstance> responsible for activity execution.</span></span> <span data-ttu-id="084f7-113">在並行執行的應用程式網域內可能有幾個 <xref:System.Activities.ActivityInstance> 物件。</span><span class="sxs-lookup"><span data-stu-id="084f7-113">There can be several <xref:System.Activities.ActivityInstance> objects within an application domain running concurrently.</span></span>  
  
 <span data-ttu-id="084f7-114">前三個主機互動物件是從稱為工作流程程式的活動樹狀結構中所建立。</span><span class="sxs-lookup"><span data-stu-id="084f7-114">Each of the preceding three host interaction objects is created from a tree of activities referred to as a workflow program.</span></span> <span data-ttu-id="084f7-115">使用這些類型或包裝的自訂主機 <xref:System.Activities.ActivityInstance> ，工作流程可以在任何 Windows 進程內部執行，包括主控台應用程式、表單架構應用程式、Windows 服務、ASP.NET 網站，以及 Windows Communication Foundation (WCF) Services。</span><span class="sxs-lookup"><span data-stu-id="084f7-115">Using these types or a custom host that wraps <xref:System.Activities.ActivityInstance>, workflows can be executed inside any Windows process including console applications, forms-based applications, Windows Services, ASP.NET Web sites, and Windows Communication Foundation (WCF) services.</span></span>  
  
 <span data-ttu-id="084f7-116">![主機處理序中的工作流程元件](./media/44c79d1d-178b-4487-87ed-3e33015a3842.gif "44c79d1d-178b-4487-87ed-3e33015a3842")</span><span class="sxs-lookup"><span data-stu-id="084f7-116">![Workflow components in the host process](./media/44c79d1d-178b-4487-87ed-3e33015a3842.gif "44c79d1d-178b-4487-87ed-3e33015a3842")</span></span>  
<span data-ttu-id="084f7-117">主機處理序中的工作流程元件</span><span class="sxs-lookup"><span data-stu-id="084f7-117">Workflow components in the host process</span></span>  
  
## <a name="interaction-between-workflow-components"></a><span data-ttu-id="084f7-118">工作流程元件之間的互動</span><span class="sxs-lookup"><span data-stu-id="084f7-118">Interaction between Workflow Components</span></span>  

 <span data-ttu-id="084f7-119">下圖顯示工作流程元件之間的互動方式。</span><span class="sxs-lookup"><span data-stu-id="084f7-119">The following diagram demonstrates how workflow components interact with one another.</span></span>  
  
 ![此圖顯示工作流程元件的互動方式。](./media/overview/workflow-component-interatction.gif)  
  
 <span data-ttu-id="084f7-121">在上圖中，<xref:System.Activities.WorkflowInvoker.Invoke%2A> 類別的 <xref:System.Activities.WorkflowInvoker> 方法是用於叫用幾個工作流程執行個體。</span><span class="sxs-lookup"><span data-stu-id="084f7-121">In the preceding diagram, the <xref:System.Activities.WorkflowInvoker.Invoke%2A> method of the <xref:System.Activities.WorkflowInvoker> class is used to invoke several workflow instances.</span></span> <span data-ttu-id="084f7-122"><xref:System.Activities.WorkflowInvoker> 是用於不需要從主機管理的輕量工作流程，需要從主機 (例如 <xref:System.Activities.Bookmark> 繼續) 管理的工作流程則必須改用 <xref:System.Activities.WorkflowApplication.Run%2A> 來執行。</span><span class="sxs-lookup"><span data-stu-id="084f7-122"><xref:System.Activities.WorkflowInvoker> is used for lightweight workflows that do not need management from the host; workflows that need management from the host (such as <xref:System.Activities.Bookmark> resumption) must be executed using <xref:System.Activities.WorkflowApplication.Run%2A> instead.</span></span> <span data-ttu-id="084f7-123">不一定要先等候一個工作流程完成，才能叫用另一個工作流程，執行階段引擎支援同時執行多個工作流程執行個體。</span><span class="sxs-lookup"><span data-stu-id="084f7-123">It isn’t required to wait for one workflow instance to complete before invoking another; the runtime engine supports running multiple workflow instances simultaneously.</span></span>  <span data-ttu-id="084f7-124">叫用的工作流程如下：</span><span class="sxs-lookup"><span data-stu-id="084f7-124">The workflows invoked are as follows:</span></span>  
  
- <span data-ttu-id="084f7-125">包含 <xref:System.Activities.Statements.Sequence> 子活動的 <xref:System.Activities.Statements.WriteLine> 活動。</span><span class="sxs-lookup"><span data-stu-id="084f7-125">A <xref:System.Activities.Statements.Sequence> activity that contains a <xref:System.Activities.Statements.WriteLine> child activity.</span></span> <span data-ttu-id="084f7-126">父活動的 <xref:System.Activities.Variable> 會繫結至子活動的 <xref:System.Activities.InArgument>。</span><span class="sxs-lookup"><span data-stu-id="084f7-126">A <xref:System.Activities.Variable> of the parent activity is bound to an <xref:System.Activities.InArgument> of the child activity.</span></span> <span data-ttu-id="084f7-127">如需有關變數、引數和系結的詳細資訊，請參閱 [變數和自](variables-and-arguments.md)變數。</span><span class="sxs-lookup"><span data-stu-id="084f7-127">For more information about on variables, arguments, and binding, see [Variables and Arguments](variables-and-arguments.md).</span></span>  
  
- <span data-ttu-id="084f7-128">稱為 `ReadLine` 的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="084f7-128">A custom activity called `ReadLine`.</span></span> <span data-ttu-id="084f7-129"><xref:System.Activities.OutArgument> 活動的 `ReadLine` 會傳回，以呼叫 <xref:System.Activities.WorkflowInvoker.Invoke%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="084f7-129">An <xref:System.Activities.OutArgument> of the `ReadLine` activity is returned to the calling <xref:System.Activities.WorkflowInvoker.Invoke%2A> method.</span></span>  
  
- <span data-ttu-id="084f7-130">衍生自 <xref:System.Activities.CodeActivity>抽象類別的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="084f7-130">A custom activity that derives from the <xref:System.Activities.CodeActivity> abstract class.</span></span> <span data-ttu-id="084f7-131"><xref:System.Activities.CodeActivity> 可存取使用 <xref:System.Activities.CodeActivityContext> 而可用來做為 <xref:System.Activities.CodeActivity.Execute%2A> 方法之參數的執行階段功能 (例如追蹤與屬性)。</span><span class="sxs-lookup"><span data-stu-id="084f7-131">The <xref:System.Activities.CodeActivity> can access run-time features (such as tracking and properties) using the <xref:System.Activities.CodeActivityContext> that is available as a parameter of the <xref:System.Activities.CodeActivity.Execute%2A> method.</span></span> <span data-ttu-id="084f7-132">如需這些執行時間功能的詳細資訊，請參閱 [工作流程追蹤和追蹤](workflow-tracking-and-tracing.md) 和 [工作流程執行屬性](workflow-execution-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="084f7-132">For more information about these run-time features, see [Workflow Tracking and Tracing](workflow-tracking-and-tracing.md) and [Workflow Execution Properties](workflow-execution-properties.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="084f7-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="084f7-133">See also</span></span>

- <span data-ttu-id="084f7-134">[BizTalk Server 2006 或 WF？為您的專案選擇正確的工作流程工具](/previous-versions/dotnet/articles/cc303238(v=msdn.10))</span><span class="sxs-lookup"><span data-stu-id="084f7-134">[BizTalk Server 2006 or WF? Choosing the Right Workflow Tool for Your Project](/previous-versions/dotnet/articles/cc303238(v=msdn.10))</span></span>
