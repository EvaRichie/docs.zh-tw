---
title: 基本 Windows Workflow 概念
description: 本文說明某些開發人員可能不熟悉的 .NET Framework 4.6.1 中的工作流程開發概念。
ms.date: 03/30/2017
ms.assetid: 0e930e80-5060-45d2-8a7a-95c0690105d4
ms.openlocfilehash: a7683791c7aed54beed9256ab08010dfeebe9936
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96265293"
---
# <a name="fundamental-windows-workflow-concepts"></a><span data-ttu-id="e06f1-103">基本 Windows Workflow 概念</span><span class="sxs-lookup"><span data-stu-id="e06f1-103">Fundamental Windows Workflow Concepts</span></span>

<span data-ttu-id="e06f1-104">[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 中的工作流程開發運用了一些開發人員可能未曾使用過的概念。</span><span class="sxs-lookup"><span data-stu-id="e06f1-104">Workflow development in the [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] uses concepts that may be new to some developers.</span></span> <span data-ttu-id="e06f1-105">本主題描述其中的部分概念及其實作方式。</span><span class="sxs-lookup"><span data-stu-id="e06f1-105">This topic describes some of the concepts and how they are implemented.</span></span>  
  
## <a name="workflows-and-activities"></a><span data-ttu-id="e06f1-106">工作流程與活動</span><span class="sxs-lookup"><span data-stu-id="e06f1-106">Workflows and Activities</span></span>  

 <span data-ttu-id="e06f1-107">工作流程是結構化的動作集合，這些動作會以處理序為模型。</span><span class="sxs-lookup"><span data-stu-id="e06f1-107">A workflow is a structured collection of actions that models a process.</span></span> <span data-ttu-id="e06f1-108">工作流程中的每一個活動都會製作成活動的模型。</span><span class="sxs-lookup"><span data-stu-id="e06f1-108">Each action in the workflow is modeled as an activity.</span></span> <span data-ttu-id="e06f1-109">主機與工作流程互動的方式，是使用 <xref:System.Activities.WorkflowInvoker> 將工作流程當成方法來叫用，以 <xref:System.Activities.WorkflowApplication> 明確控制單一工作流程執行個體的執行，並以 <xref:System.ServiceModel.WorkflowServiceHost> 在多執行個體案例中進行以訊息為基礎的互動。</span><span class="sxs-lookup"><span data-stu-id="e06f1-109">A host interacts with a workflow by using <xref:System.Activities.WorkflowInvoker> for invoking a workflow as if it were a method,  <xref:System.Activities.WorkflowApplication> for explicit control over the execution of a single workflow instance, and <xref:System.ServiceModel.WorkflowServiceHost> for message-based interactions in multi-instance scenarios.</span></span> <span data-ttu-id="e06f1-110">由於工作流程的步驟定義為活動的階層，因此階層中最上方的活動可說是用於定義工作流程本身。</span><span class="sxs-lookup"><span data-stu-id="e06f1-110">Because steps of the workflow are defined as a hierarchy of activities, the topmost activity in the hierarchy can be said to define the workflow itself.</span></span> <span data-ttu-id="e06f1-111">這個階層模型取代了舊版中明確的 `SequentialWorkflow` 及 `StateMachineWorkflow` 類別。</span><span class="sxs-lookup"><span data-stu-id="e06f1-111">This hierarchy model takes the place of the explicit `SequentialWorkflow` and `StateMachineWorkflow` classes from previous versions.</span></span> <span data-ttu-id="e06f1-112">活動本身會開發做為其他活動的集合 (使用 <xref:System.Activities.Activity> 類別做為基底，通常使用 XAML 來定義)，或是使用 <xref:System.Activities.CodeActivity> 類別 (可以使用執行階段進行資料存取) 或 <xref:System.Activities.NativeActivity> 類別 (會向活動作者公開工作執行階段的廣度)，以自訂方式來建立。</span><span class="sxs-lookup"><span data-stu-id="e06f1-112">Activities themselves are developed as collections of other activities (using the <xref:System.Activities.Activity> class as a base, usually defined by using XAML) or are custom created by using the <xref:System.Activities.CodeActivity> class, which can use the runtime for data access, or by using the <xref:System.Activities.NativeActivity> class, which exposes the breadth of the workflow runtime to the activity author.</span></span> <span data-ttu-id="e06f1-113">使用 <xref:System.Activities.CodeActivity> 和 <xref:System.Activities.NativeActivity> 來開發的活動，是使用 CLR 相容語言 (例如 C#) 開發而成。</span><span class="sxs-lookup"><span data-stu-id="e06f1-113">Activities developed by using <xref:System.Activities.CodeActivity> and <xref:System.Activities.NativeActivity> are created by using CLR-compliant languages such as C#.</span></span>  
  
## <a name="activity-data-model"></a><span data-ttu-id="e06f1-114">活動資料模型</span><span class="sxs-lookup"><span data-stu-id="e06f1-114">Activity Data Model</span></span>  

 <span data-ttu-id="e06f1-115">活動會使用下表顯示的型別來儲存及共用資料。</span><span class="sxs-lookup"><span data-stu-id="e06f1-115">Activities store and share data by using the types shown in the following table.</span></span>  
  
|||  
|-|-|  
|<span data-ttu-id="e06f1-116">變數</span><span class="sxs-lookup"><span data-stu-id="e06f1-116">Variable</span></span>|<span data-ttu-id="e06f1-117">將資料儲存在活動中。</span><span class="sxs-lookup"><span data-stu-id="e06f1-117">Stores data in an activity.</span></span>|  
|<span data-ttu-id="e06f1-118">引數</span><span class="sxs-lookup"><span data-stu-id="e06f1-118">Argument</span></span>|<span data-ttu-id="e06f1-119">將資料移入與移出活動。</span><span class="sxs-lookup"><span data-stu-id="e06f1-119">Moves data into and out of an activity.</span></span>|  
|<span data-ttu-id="e06f1-120">運算式</span><span class="sxs-lookup"><span data-stu-id="e06f1-120">Expression</span></span>|<span data-ttu-id="e06f1-121">具有提升用於引數繫結之傳回值的活動。</span><span class="sxs-lookup"><span data-stu-id="e06f1-121">An activity with an elevated return value used in argument bindings.</span></span>|  
  
## <a name="workflow-runtime"></a><span data-ttu-id="e06f1-122">工作流程執行階段</span><span class="sxs-lookup"><span data-stu-id="e06f1-122">Workflow Runtime</span></span>  

 <span data-ttu-id="e06f1-123">工作流程執行階段是工作流程的執行環境。</span><span class="sxs-lookup"><span data-stu-id="e06f1-123">The workflow runtime is the environment in which workflows execute.</span></span> <span data-ttu-id="e06f1-124"><xref:System.Activities.WorkflowInvoker> 是執行工作流程最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="e06f1-124"><xref:System.Activities.WorkflowInvoker> is the simplest way to execute a workflow.</span></span> <span data-ttu-id="e06f1-125">主機會使用 <xref:System.Activities.WorkflowInvoker> 進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="e06f1-125">The host uses <xref:System.Activities.WorkflowInvoker> for the following:</span></span>  
  
- <span data-ttu-id="e06f1-126">同步叫用工作流程。</span><span class="sxs-lookup"><span data-stu-id="e06f1-126">To synchronously invoke a workflow.</span></span>  
  
- <span data-ttu-id="e06f1-127">提供輸入至工作流程，或從工作流程擷取輸出。</span><span class="sxs-lookup"><span data-stu-id="e06f1-127">To provide input to, or retrieve output from a workflow.</span></span>  
  
- <span data-ttu-id="e06f1-128">加入活動所使用的擴充。</span><span class="sxs-lookup"><span data-stu-id="e06f1-128">To add extensions to be used by activities.</span></span>  
  
 <span data-ttu-id="e06f1-129"><xref:System.Activities.ActivityInstance> 是具備執行緒安全的 Proxy，主機可利用它來與執行階段互動。</span><span class="sxs-lookup"><span data-stu-id="e06f1-129"><xref:System.Activities.ActivityInstance> is the thread-safe proxy that hosts can use to interact with the runtime.</span></span> <span data-ttu-id="e06f1-130">主機會使用 <xref:System.Activities.ActivityInstance> 進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="e06f1-130">The host uses <xref:System.Activities.ActivityInstance> for the following:</span></span>  
  
- <span data-ttu-id="e06f1-131">透過建立執行個體，或從執行個體存放區載入來取得執行個體。</span><span class="sxs-lookup"><span data-stu-id="e06f1-131">To acquire an instance by creating it or loading it from an instance store.</span></span>  
  
- <span data-ttu-id="e06f1-132">收到執行個體開發週期事件通知。</span><span class="sxs-lookup"><span data-stu-id="e06f1-132">To be notified of instance life-cycle events.</span></span>  
  
- <span data-ttu-id="e06f1-133">控制工作流程的執行。</span><span class="sxs-lookup"><span data-stu-id="e06f1-133">To control workflow execution.</span></span>  
  
- <span data-ttu-id="e06f1-134">提供輸入至工作流程，或從工作流程擷取輸出。</span><span class="sxs-lookup"><span data-stu-id="e06f1-134">To provide input to, or retrieve output from a workflow.</span></span>  
  
- <span data-ttu-id="e06f1-135">發出工作流程接續的訊號並將值傳入工作流程中。</span><span class="sxs-lookup"><span data-stu-id="e06f1-135">To signal a workflow continuation and pass values into the workflow.</span></span>  
  
- <span data-ttu-id="e06f1-136">保存工作流程資料。</span><span class="sxs-lookup"><span data-stu-id="e06f1-136">To persist workflow data.</span></span>  
  
- <span data-ttu-id="e06f1-137">加入活動所使用的擴充。</span><span class="sxs-lookup"><span data-stu-id="e06f1-137">To add extensions to be used by activities.</span></span>  
  
 <span data-ttu-id="e06f1-138">藉由使用適當的 <xref:System.Activities.ActivityContext> 衍生類別 (例如 <xref:System.Activities.NativeActivityContext> 或 <xref:System.Activities.CodeActivityContext>)，活動可以存取工作流程執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="e06f1-138">Activities gain access to the workflow runtime environment by using the appropriate <xref:System.Activities.ActivityContext> derived class, such as <xref:System.Activities.NativeActivityContext> or <xref:System.Activities.CodeActivityContext>.</span></span> <span data-ttu-id="e06f1-139">並且會利用這種方式解析引數與變數、排程子活動，以及用於許多其他用途。</span><span class="sxs-lookup"><span data-stu-id="e06f1-139">They use this for resolving arguments and variables, for scheduling child activities, and for many other purposes.</span></span>  
  
## <a name="services"></a><span data-ttu-id="e06f1-140">服務</span><span class="sxs-lookup"><span data-stu-id="e06f1-140">Services</span></span>  

 <span data-ttu-id="e06f1-141">工作流程利用傳訊活動，提供自然的方式來實作及存取鬆散耦合服務。</span><span class="sxs-lookup"><span data-stu-id="e06f1-141">Workflows provide a natural way to implement and access loosely-coupled services, using messaging activities.</span></span> <span data-ttu-id="e06f1-142">訊息活動是以 WCF 為基礎，而且是用來將資料傳入和傳出工作流程的主要機制。</span><span class="sxs-lookup"><span data-stu-id="e06f1-142">Messaging activities are built on WCF and are the primary mechanism used to get data into and out of a workflow.</span></span> <span data-ttu-id="e06f1-143">您可以一起撰寫傳訊活動，針對您所需的任何傳訊交換型式建立模型。</span><span class="sxs-lookup"><span data-stu-id="e06f1-143">You can compose messaging activities together to model any kind of message exchange pattern you wish.</span></span> <span data-ttu-id="e06f1-144">如需詳細資訊，請參閱 [訊息活動](../wcf/feature-details/messaging-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="e06f1-144">For more information, see [Messaging Activities](../wcf/feature-details/messaging-activities.md).</span></span> <span data-ttu-id="e06f1-145">工作流程服務是使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 類別裝載的。</span><span class="sxs-lookup"><span data-stu-id="e06f1-145">Workflow services are hosted using the <xref:System.ServiceModel.Activities.WorkflowServiceHost> class.</span></span> <span data-ttu-id="e06f1-146">如需詳細資訊，請參閱 [裝載工作流程服務總覽](../wcf/feature-details/hosting-workflow-services-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e06f1-146">For more information, see [Hosting Workflow Services Overview](../wcf/feature-details/hosting-workflow-services-overview.md).</span></span> <span data-ttu-id="e06f1-147">如需工作流程服務的詳細資訊，請參閱 [工作流程服務](../wcf/feature-details/workflow-services.md)</span><span class="sxs-lookup"><span data-stu-id="e06f1-147">For more information about workflow services see [Workflow Services](../wcf/feature-details/workflow-services.md)</span></span>  
  
## <a name="persistence-unloading-and-long-running-workflows"></a><span data-ttu-id="e06f1-148">持續性工作流程、卸載工作流程，以及長期執行工作流程</span><span class="sxs-lookup"><span data-stu-id="e06f1-148">Persistence, Unloading, and Long-Running Workflows</span></span>  

 <span data-ttu-id="e06f1-149">Windows 工作流程透過提供下列功能，簡化長期執行反應式程式的製作：</span><span class="sxs-lookup"><span data-stu-id="e06f1-149">Windows Workflow simplifies the authoring of long-running reactive programs by providing:</span></span>  
  
- <span data-ttu-id="e06f1-150">存取外部輸入的活動。</span><span class="sxs-lookup"><span data-stu-id="e06f1-150">Activities that access external input.</span></span>  
  
- <span data-ttu-id="e06f1-151">建立可由主機接聽程式接續之 <xref:System.Activities.Bookmark> 物件的能力。</span><span class="sxs-lookup"><span data-stu-id="e06f1-151">The ability to create <xref:System.Activities.Bookmark> objects that can be resumed by a host listener.</span></span>  
  
- <span data-ttu-id="e06f1-152">保存工作流程的資料並卸載該工作流程，然後重新載入及重新啟動工作流程以回應 <xref:System.Activities.Bookmark> 物件之接續的能力。</span><span class="sxs-lookup"><span data-stu-id="e06f1-152">The ability to persist a workflow’s data and unload the workflow, and then reload and reactivate the workflow in response to the resumption of <xref:System.Activities.Bookmark> objects in a particular workflow.</span></span>  
  
 <span data-ttu-id="e06f1-153">工作流程會持續執行活動，直到沒有其他可執行的活動，或者直到目前所有執行中的活動均在等候輸入為止。</span><span class="sxs-lookup"><span data-stu-id="e06f1-153">A workflow continuously executes activities until there are no more activities to execute or until all currently executing activities are waiting for input.</span></span> <span data-ttu-id="e06f1-154">在第二種狀態中，工作流程是閒置的。</span><span class="sxs-lookup"><span data-stu-id="e06f1-154">In this latter state, the workflow is idle.</span></span> <span data-ttu-id="e06f1-155">主機通常會卸載閒置的工作流程，並在訊息抵達時重新載入該工作流程以繼續執行。</span><span class="sxs-lookup"><span data-stu-id="e06f1-155">It is common for a host to unload workflows that have gone idle and to reload them to continue execution when a message arrives.</span></span> <span data-ttu-id="e06f1-156"><xref:System.ServiceModel.Activities.WorkflowServiceHost> 提供此特性的功能，並且提供可延伸的卸載原則。</span><span class="sxs-lookup"><span data-stu-id="e06f1-156"><xref:System.ServiceModel.Activities.WorkflowServiceHost> provides functionality for this feature and provides an extensible unload policy.</span></span> <span data-ttu-id="e06f1-157">針對使用變動性狀態資料或其他無法保存之資料的執行區塊，活動可以使用 <xref:System.Activities.NoPersistHandle> 向主機指示不應保存資料。</span><span class="sxs-lookup"><span data-stu-id="e06f1-157">For blocks of execution that use volatile state data or other data that cannot be persisted, an activity can indicate to a host that it should not be persisted by using the <xref:System.Activities.NoPersistHandle>.</span></span> <span data-ttu-id="e06f1-158">工作流程也可以利用 <xref:System.Activities.Statements.Persist> 活動，將其資料明確地保存至長期性的儲存媒體中。</span><span class="sxs-lookup"><span data-stu-id="e06f1-158">A workflow can also explicitly persist its data to a durable storage medium by using the <xref:System.Activities.Statements.Persist> activity.</span></span>
