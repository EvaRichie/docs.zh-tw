---
title: HOW TO：以 WorkflowServiceHost 設定工作流程服務的未處理例外狀況行為
ms.date: 03/30/2017
ms.assetid: 51b25c86-292c-43e4-8d13-273d2badc8ad
ms.openlocfilehash: 3881d1af21dcc0c211c6738162360e522648d949
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593590"
---
# <a name="how-to-configure-workflow-unhandled-exception-behavior-with-workflowservicehost"></a><span data-ttu-id="4226e-102">HOW TO：以 WorkflowServiceHost 設定工作流程服務的未處理例外狀況行為</span><span class="sxs-lookup"><span data-stu-id="4226e-102">How to: Configure Workflow Unhandled Exception Behavior with WorkflowServiceHost</span></span>
<span data-ttu-id="4226e-103"><xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> 是一項行為，可讓您指定裝載於 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的工作流程內發生未處理的例外狀況時，所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="4226e-103">The <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> is a behavior that enables you to specify the action to take if an unhandled exception occurs within a workflow hosted in <xref:System.ServiceModel.Activities.WorkflowServiceHost>.</span></span> <span data-ttu-id="4226e-104">本主題示範如何組態檔中設定此行為。</span><span class="sxs-lookup"><span data-stu-id="4226e-104">This topic shows how to configure this behavior in a configuration file.</span></span>  
  
### <a name="to-configure-workflowunhandledexceptionbehavior"></a><span data-ttu-id="4226e-105">若要設定 WorkflowUnhandledExceptionBehavior</span><span class="sxs-lookup"><span data-stu-id="4226e-105">To configure WorkflowUnhandledExceptionBehavior</span></span>  
  
1. <span data-ttu-id="4226e-106">`workflowUnhandledException`在 <> 專案內的 <> 專案中加入 <> 專案 `behavior` `serviceBehaviors` ，使用 `action` 屬性指定未處理的例外狀況發生時所採取的動作，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="4226e-106">Add a <`workflowUnhandledException`> element in a <`behavior`> element within a <`serviceBehaviors`> element, using the `action` attribute to specify the action to take when an unhandled exception occurs as shown in the following example.</span></span>  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowUnhandledException action="abandonAndSuspend"/>
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
    > [!NOTE]
    > <span data-ttu-id="4226e-107">上述組態範例會使用簡化的組態。</span><span class="sxs-lookup"><span data-stu-id="4226e-107">The preceding configuration sample is using simplified configuration.</span></span> <span data-ttu-id="4226e-108">如需詳細資訊，請參閱[簡化](../simplified-configuration.md)的設定。</span><span class="sxs-lookup"><span data-stu-id="4226e-108">For more information, see [Simplified Configuration](../simplified-configuration.md).</span></span>  
  
     <span data-ttu-id="4226e-109">此行為可以在程式碼中設定，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="4226e-109">This behavior can be configured in code as shown in the following example.</span></span>  
  
    ```csharp  
    host.Description.Behaviors.Add(new WorkflowUnhandledExceptionBehavior { Action = WorkflowUnhandledExceptionAction.AbandonAndSuspend });  
    ```  
  
     <span data-ttu-id="4226e-110">`action`<> 元素的屬性 `workflowUnhandledException` 可以設定為下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="4226e-110">The `action` attribute of the <`workflowUnhandledException`> element can be set to one of the following values:</span></span>  
  
     <span data-ttu-id="4226e-111">**放棄**</span><span class="sxs-lookup"><span data-stu-id="4226e-111">**abandon**</span></span>  
     <span data-ttu-id="4226e-112">不改變永續性執行個體的狀態，放棄記憶體中的執行個體 (亦即，回復到上一次的永續點)。</span><span class="sxs-lookup"><span data-stu-id="4226e-112">Aborts the instance in memory without touching the persisted instance state (that is, roll back to the last persist point).</span></span>  
  
     <span data-ttu-id="4226e-113">**abandonAndSuspend**</span><span class="sxs-lookup"><span data-stu-id="4226e-113">**abandonAndSuspend**</span></span>  
     <span data-ttu-id="4226e-114">放棄記憶體中的執行個體，並更新要暫停的永續執行個體。</span><span class="sxs-lookup"><span data-stu-id="4226e-114">Aborts the instance in memory and updates the persisted instance to be suspended.</span></span>  
  
     <span data-ttu-id="4226e-115">**cancel**</span><span class="sxs-lookup"><span data-stu-id="4226e-115">**cancel**</span></span>  
     <span data-ttu-id="4226e-116">呼叫執行個體的取消處理常式，然後完成記憶體中的執行個體，該記憶體可能也會將執行個體從執行個體庫中移除。</span><span class="sxs-lookup"><span data-stu-id="4226e-116">Calls cancellation handlers for the instance and then completes the instance in memory, which may also remove it from the instance store</span></span>  
  
     <span data-ttu-id="4226e-117">**終止**</span><span class="sxs-lookup"><span data-stu-id="4226e-117">**terminate**</span></span>  
     <span data-ttu-id="4226e-118">完成記憶體中的執行個體並將其從執行個體庫中移除。</span><span class="sxs-lookup"><span data-stu-id="4226e-118">Completes the instance in memory and removes it from the instance store.</span></span>  
  
     <span data-ttu-id="4226e-119">如需的詳細資訊 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> ，請參閱[工作流程服務主機](workflow-service-host-extensibility.md)擴充性。</span><span class="sxs-lookup"><span data-stu-id="4226e-119">For more information about <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>, see [Workflow Service Host Extensibility](workflow-service-host-extensibility.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4226e-120">請參閱</span><span class="sxs-lookup"><span data-stu-id="4226e-120">See also</span></span>

- [<span data-ttu-id="4226e-121">工作流程服務主機擴充性</span><span class="sxs-lookup"><span data-stu-id="4226e-121">Workflow Service Host Extensibility</span></span>](workflow-service-host-extensibility.md)
- [<span data-ttu-id="4226e-122">工作流程服務</span><span class="sxs-lookup"><span data-stu-id="4226e-122">Workflow Services</span></span>](workflow-services.md)
