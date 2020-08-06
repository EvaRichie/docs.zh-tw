---
title: 使用 WorkflowIdentity 與版本控制
ms.date: 03/30/2017
ms.assetid: b8451735-8046-478f-912b-40870a6c0c3a
ms.openlocfilehash: 1d31739c135dbb518f05c40ba802c782b6817bff
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855630"
---
# <a name="using-workflowidentity-and-versioning"></a><span data-ttu-id="54892-102">使用 WorkflowIdentity 與版本控制</span><span class="sxs-lookup"><span data-stu-id="54892-102">Using WorkflowIdentity and Versioning</span></span>

<span data-ttu-id="54892-103"><xref:System.Activities.WorkflowIdentity> 提供一種方法，讓工作流程應用程式開發人員能夠將名稱和 <xref:System.Version> 與工作流程定義建立關聯，並為這項資訊與持續性的工作流程執行個體建立關聯。</span><span class="sxs-lookup"><span data-stu-id="54892-103"><xref:System.Activities.WorkflowIdentity> provides a way for workflow application developers to associate a name and a <xref:System.Version> with a workflow definition, and for this information to be associated with a persisted workflow instance.</span></span> <span data-ttu-id="54892-104">此身分識別資訊可由工作流程應用程式開發人員使用以啟用案例 (例如並存執行多個版本的工作流程定義)，以及提供動態更新等其他功能的基礎。</span><span class="sxs-lookup"><span data-stu-id="54892-104">This identity information can be used by workflow application developers to enable scenarios such as side-by-side execution of multiple versions of a workflow definition, and provides the cornerstone for other functionality such as dynamic update.</span></span> <span data-ttu-id="54892-105">本主題提供使用 <xref:System.Activities.WorkflowIdentity> 搭配 <xref:System.Activities.WorkflowApplication> 裝載的概觀。</span><span class="sxs-lookup"><span data-stu-id="54892-105">This topic provides as overview of using <xref:System.Activities.WorkflowIdentity> with <xref:System.Activities.WorkflowApplication> hosting.</span></span> <span data-ttu-id="54892-106">如需在工作流程服務中並存執行工作流程定義的詳細資訊，請參閱[WorkflowServiceHost 中的並存版本控制](../wcf/feature-details/side-by-side-versioning-in-workflowservicehost.md)。</span><span class="sxs-lookup"><span data-stu-id="54892-106">For information on side-by-side execution of workflow definitions in a workflow service, see [Side by Side Versioning in WorkflowServiceHost](../wcf/feature-details/side-by-side-versioning-in-workflowservicehost.md).</span></span> <span data-ttu-id="54892-107">如需動態更新的詳細資訊，請參閱[動態更新](dynamic-update.md)。</span><span class="sxs-lookup"><span data-stu-id="54892-107">For information on dynamic update, see [Dynamic Update](dynamic-update.md).</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="54892-108">本主題內容</span><span class="sxs-lookup"><span data-stu-id="54892-108">In this topic</span></span>

- [<span data-ttu-id="54892-109">使用 WorkflowIdentity</span><span class="sxs-lookup"><span data-stu-id="54892-109">Using WorkflowIdentity</span></span>](using-workflowidentity-and-versioning.md#UsingWorkflowIdentity)

  - [<span data-ttu-id="54892-110">使用 WorkflowIdentity 並存執行</span><span class="sxs-lookup"><span data-stu-id="54892-110">Side-by-side Execution using WorkflowIdentity</span></span>](using-workflowidentity-and-versioning.md#SxS)

- [<span data-ttu-id="54892-111">升級 .NET Framework 4 持續性資料庫以支援工作流程版本控制</span><span class="sxs-lookup"><span data-stu-id="54892-111">Upgrading .NET Framework 4 Persistence Databases to Support Workflow Versioning</span></span>](using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases)

  - [<span data-ttu-id="54892-112">升級資料庫結構描述</span><span class="sxs-lookup"><span data-stu-id="54892-112">To upgrade the database schema</span></span>](using-workflowidentity-and-versioning.md#ToUpgrade)

## <a name="using-workflowidentity"></a><a name="UsingWorkflowIdentity"></a><span data-ttu-id="54892-113">使用 WorkflowIdentity</span><span class="sxs-lookup"><span data-stu-id="54892-113">Using WorkflowIdentity</span></span>

<span data-ttu-id="54892-114">若要使用 <xref:System.Activities.WorkflowIdentity>，請建立執行個體、加以設定，並將其與 <xref:System.Activities.WorkflowApplication> 執行個體建立關聯。</span><span class="sxs-lookup"><span data-stu-id="54892-114">To use <xref:System.Activities.WorkflowIdentity>, create an instance, configure it, and associate it with a <xref:System.Activities.WorkflowApplication> instance.</span></span> <span data-ttu-id="54892-115"><xref:System.Activities.WorkflowIdentity> 執行個體包含三項識別資訊。</span><span class="sxs-lookup"><span data-stu-id="54892-115">A <xref:System.Activities.WorkflowIdentity> instance contains three identifying pieces of information.</span></span> <span data-ttu-id="54892-116"><xref:System.Activities.WorkflowIdentity.Name%2A> 和 <xref:System.Activities.WorkflowIdentity.Version%2A> 包含名稱及 <xref:System.Version>，兩者都是必要項，而 <xref:System.Activities.WorkflowIdentity.Package%2A> 則是選用項，可用來指定包含資訊 (例如組件名稱或其他所需資訊) 的其他字串。</span><span class="sxs-lookup"><span data-stu-id="54892-116"><xref:System.Activities.WorkflowIdentity.Name%2A> and <xref:System.Activities.WorkflowIdentity.Version%2A> contain a name and a <xref:System.Version> and are required, and <xref:System.Activities.WorkflowIdentity.Package%2A> is optional and can be used to specify an additional string containing information such as assembly name or other desired information.</span></span> <span data-ttu-id="54892-117">如果 <xref:System.Activities.WorkflowIdentity> 的三個屬性中有任何屬性與另一個 <xref:System.Activities.WorkflowIdentity> 的不同，則其為唯一識別。</span><span class="sxs-lookup"><span data-stu-id="54892-117">A <xref:System.Activities.WorkflowIdentity> is unique if any of its three properties are different from another <xref:System.Activities.WorkflowIdentity>.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54892-118"><xref:System.Activities.WorkflowIdentity> 不應包含任何個人可識別資訊 (PII)。</span><span class="sxs-lookup"><span data-stu-id="54892-118">A <xref:System.Activities.WorkflowIdentity> should not contain any personally identifiable information (PII).</span></span> <span data-ttu-id="54892-119">執行階段會在數個不同的活動生命週期點，將有關<xref:System.Activities.WorkflowIdentity> (用來建立執行個體) 的資訊發出到任何已設定的追蹤服務。</span><span class="sxs-lookup"><span data-stu-id="54892-119">Information about the <xref:System.Activities.WorkflowIdentity> used to create an instance is emitted to any configured tracking services at several different points of the activity life-cycle by the runtime.</span></span> <span data-ttu-id="54892-120">WF 追蹤沒有任何機制可隱藏 PII (機密的使用者資料)。</span><span class="sxs-lookup"><span data-stu-id="54892-120">WF Tracking does not have any mechanism to hide PII (sensitive user data).</span></span> <span data-ttu-id="54892-121">因此，<xref:System.Activities.WorkflowIdentity> 執行個體不應包含任何 PII 資料，因為執行階段會在追蹤記錄中發出這項資訊，因此存取檢視追蹤記錄的人有可能看見這項資訊。</span><span class="sxs-lookup"><span data-stu-id="54892-121">Therefore, a <xref:System.Activities.WorkflowIdentity> instance should not contain any PII data as it will be emitted by the runtime in tracking records and may be visible to anyone with access to view the tracking records.</span></span>

<span data-ttu-id="54892-122">在下列範例中，建立了 <xref:System.Activities.WorkflowIdentity>，並將其與使用 `MortgageWorkflow` 工作流程定義來建立的工作流程執行個體建立關聯。</span><span class="sxs-lookup"><span data-stu-id="54892-122">In the following example, a <xref:System.Activities.WorkflowIdentity> is created and associated with an instance of a workflow created using a `MortgageWorkflow` workflow definition.</span></span>

```csharp
WorkflowIdentity identityV1 = new WorkflowIdentity
{
    Name = "MortgageWorkflow v1",
    Version = new Version(1, 0, 0, 0)
};

WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);

// Configure the WorkflowApplication with persistence and desired workflow event handlers.
ConfigureWorkflowApplication(wfApp);

// Run the workflow.
wfApp.Run();
```

<span data-ttu-id="54892-123">重新載入並繼續工作流程時，所使用的 <xref:System.Activities.WorkflowIdentity> 必須設定為符合持續性工作流程執行個體的 <xref:System.Activities.WorkflowIdentity>。</span><span class="sxs-lookup"><span data-stu-id="54892-123">When reloading and resuming a workflow, a <xref:System.Activities.WorkflowIdentity> that is configured to match the <xref:System.Activities.WorkflowIdentity> of the persisted workflow instance must be used.</span></span>

```csharp
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identityV1);

// Configure the WorkflowApplication with persistence and desired workflow event handlers.
ConfigureWorkflowApplication(wfApp);

// Load the workflow.
wfApp.Load(instanceId);

// Resume the workflow...
```

<span data-ttu-id="54892-124">如果在重新載入工作流程執行個體時，使用的 <xref:System.Activities.WorkflowIdentity> 與持續性 <xref:System.Activities.WorkflowIdentity> 不相符，會擲回 <xref:System.Activities.VersionMismatchException>。</span><span class="sxs-lookup"><span data-stu-id="54892-124">If the <xref:System.Activities.WorkflowIdentity> used when reloading the workflow instance does not match the persisted <xref:System.Activities.WorkflowIdentity>, a <xref:System.Activities.VersionMismatchException> is thrown.</span></span> <span data-ttu-id="54892-125">在下列範例中，會在上一個範例中持續性 `MortgageWorkflow` 執行個體上載入。</span><span class="sxs-lookup"><span data-stu-id="54892-125">In the following example a load attempt is made on the `MortgageWorkflow` instance that was persisted in the previous example.</span></span> <span data-ttu-id="54892-126">這個載入嘗試是使用針對較新版抵押工作流程設定的 <xref:System.Activities.WorkflowIdentity>，該工作流程與持續性執行個體不相符。</span><span class="sxs-lookup"><span data-stu-id="54892-126">This load attempt is made using a <xref:System.Activities.WorkflowIdentity> configured for a newer version of the mortgage workflow that does not match the persisted instance.</span></span>

```csharp
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow_v2(), identityV2);

// Configure the WorkflowApplication with persistence and desired workflow event handlers.
ConfigureWorkflowApplication(wfApp);

// Attempt to load the workflow instance.
wfApp.Load(instanceId);

// Resume the workflow...
```

<span data-ttu-id="54892-127">執行先前的程式碼時，會擲回 <xref:System.Activities.VersionMismatchException>。</span><span class="sxs-lookup"><span data-stu-id="54892-127">When the previous code is executed, the following <xref:System.Activities.VersionMismatchException> is thrown.</span></span>

```output
The WorkflowIdentity ('MortgageWorkflow v1; Version=1.0.0.0') of the loaded instance does not match the WorkflowIdentity ('MortgageWorkflow v2; Version=2.0.0.0') of the provided workflow definition. The instance can be loaded using a different definition, or updated using Dynamic Update.
```

### <a name="side-by-side-execution-using-workflowidentity"></a><a name="SxS"></a><span data-ttu-id="54892-128">使用 WorkflowIdentity 並存執行</span><span class="sxs-lookup"><span data-stu-id="54892-128">Side-by-side Execution using WorkflowIdentity</span></span>

<span data-ttu-id="54892-129"><xref:System.Activities.WorkflowIdentity> 可加速並存執行多種版本的工作流程。</span><span class="sxs-lookup"><span data-stu-id="54892-129"><xref:System.Activities.WorkflowIdentity> can be used to facilitate the execution of multiple versions of a workflow side-by-side.</span></span> <span data-ttu-id="54892-130">常見的案例之一是變更長時間執行工作流程的業務需求。</span><span class="sxs-lookup"><span data-stu-id="54892-130">One common scenario is changing business requirements on a long-running workflow.</span></span> <span data-ttu-id="54892-131">部署更新版本時，可以執行同一個工作流程的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="54892-131">Many instances of a workflow could be running when an updated version is deployed.</span></span> <span data-ttu-id="54892-132">主應用程式可以設定為在啟動新執行個體時使用更新的工作流程定義，而且主應用程式必須在繼續執行個體時，負責提供正確的工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="54892-132">The host application can be configured to use the updated workflow definition when starting new instances, and it is the responsibility of the host application to provide the correct workflow definition when resuming instances.</span></span> <span data-ttu-id="54892-133"><xref:System.Activities.WorkflowIdentity> 可以在繼續工作流程執行個體時識別和提供相符的工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="54892-133"><xref:System.Activities.WorkflowIdentity> can be used to identify and supply the matching workflow definition when resuming workflow instances.</span></span>

<span data-ttu-id="54892-134">為了擷取持續性工作流程執行個體的 <xref:System.Activities.WorkflowIdentity>，會使用 <xref:System.Activities.WorkflowApplication.GetInstance%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="54892-134">To retrieve the <xref:System.Activities.WorkflowIdentity> of a persisted workflow instance, the <xref:System.Activities.WorkflowApplication.GetInstance%2A> method is used.</span></span> <span data-ttu-id="54892-135"><xref:System.Activities.WorkflowApplication.GetInstance%2A> 方法會採用持續性工作流程執行個體的 <xref:System.Activities.WorkflowApplication.Id%2A> 及包含持續性執行個體的 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>，並且傳回 <xref:System.Activities.WorkflowApplicationInstance>。</span><span class="sxs-lookup"><span data-stu-id="54892-135">The <xref:System.Activities.WorkflowApplication.GetInstance%2A> method takes the <xref:System.Activities.WorkflowApplication.Id%2A> of the persisted workflow instance and the <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> that contains the persisted instance and returns a <xref:System.Activities.WorkflowApplicationInstance>.</span></span> <span data-ttu-id="54892-136"><xref:System.Activities.WorkflowApplicationInstance> 包含持續性工作流程執行個體的相關資訊，包括與其相關聯的 <xref:System.Activities.WorkflowIdentity>。</span><span class="sxs-lookup"><span data-stu-id="54892-136">A <xref:System.Activities.WorkflowApplicationInstance> contains information about a persisted workflow instance, including its associated <xref:System.Activities.WorkflowIdentity>.</span></span> <span data-ttu-id="54892-137">載入及繼續工作流程執行個體時，主機可以使用此相關聯的 <xref:System.Activities.WorkflowIdentity> 來提供正確的工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="54892-137">This associated <xref:System.Activities.WorkflowIdentity> can be used by the host to supply the correct workflow definition when loading and resuming the workflow instance.</span></span>

> [!NOTE]
> <span data-ttu-id="54892-138">Null <xref:System.Activities.WorkflowIdentity> 為有效，而且可讓主機用來將沒有相關聯 <xref:System.Activities.WorkflowIdentity> 的持續性執行個體，對應至適當的工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="54892-138">A null <xref:System.Activities.WorkflowIdentity> is valid, and can be used by the host to map instances that were persisted with no associated <xref:System.Activities.WorkflowIdentity> to the proper workflow definition.</span></span> <span data-ttu-id="54892-139">當工作流應用程式一開始不是以工作流程版本設定來撰寫，或從 .NET Framework 4 升級應用程式時，就可能發生此情況。</span><span class="sxs-lookup"><span data-stu-id="54892-139">This scenario can occur when a workflow application was not initially written with workflow versioning, or when an application is upgraded from .NET Framework 4.</span></span> <span data-ttu-id="54892-140">如需詳細資訊，請參閱[升級 .NET Framework 4 持續性資料庫以支援工作流程版本控制](using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases)。</span><span class="sxs-lookup"><span data-stu-id="54892-140">For more information, see [Upgrading .NET Framework 4 Persistence Databases to Support Workflow Versioning](using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases).</span></span>

<span data-ttu-id="54892-141">在下列範例中 `Dictionary<WorkflowIdentity, Activity>` ，是用來將 <xref:System.Activities.WorkflowIdentity> 實例與其相符的工作流程定義產生關聯，並使用 `MortgageWorkflow` 與相關聯的工作流程定義來啟動工作流程 `identityV1` <xref:System.Activities.WorkflowIdentity> 。</span><span class="sxs-lookup"><span data-stu-id="54892-141">In the following example a `Dictionary<WorkflowIdentity, Activity>` is used to associate <xref:System.Activities.WorkflowIdentity> instances with their matching workflow definitions, and a workflow is started using the `MortgageWorkflow` workflow definition, which is associated with the `identityV1` <xref:System.Activities.WorkflowIdentity>.</span></span>

```csharp
WorkflowIdentity identityV1 = new WorkflowIdentity
{
    Name = "MortgageWorkflow v1",
    Version = new Version(1, 0, 0, 0)
};

WorkflowIdentity identityV2 = new WorkflowIdentity
{
    Name = "MortgageWorkflow v2",
    Version = new Version(2, 0, 0, 0)
};

Dictionary<WorkflowIdentity, Activity> WorkflowVersionMap = new Dictionary<WorkflowIdentity, Activity>();
WorkflowVersionMap.Add(identityV1, new MortgageWorkflow());
WorkflowVersionMap.Add(identityV2, new MortgageWorkflow_v2());

WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identityV1);

// Configure the WorkflowApplication with persistence and desired workflow event handlers.
ConfigureWorkflowApplication(wfApp);

// Run the workflow.
wfApp.Run();
```

<span data-ttu-id="54892-142">在下列範例中，會呼叫 <xref:System.Activities.WorkflowApplication.GetInstance%2A>，以從上一個範例擷取持續性工作流程執行個體的相關資訊，並使用持續性 <xref:System.Activities.WorkflowIdentity> 資訊來擷取相符的工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="54892-142">In the following example, information about the persisted workflow instance from the previous example is retrieved by calling <xref:System.Activities.WorkflowApplication.GetInstance%2A>, and the persisted <xref:System.Activities.WorkflowIdentity> information is used to retrieve the matching workflow definition.</span></span> <span data-ttu-id="54892-143">此資訊可用來設定 <xref:System.Activities.WorkflowApplication>，然後載入工作流程。</span><span class="sxs-lookup"><span data-stu-id="54892-143">This information is used to configure the <xref:System.Activities.WorkflowApplication>, and then the workflow is loaded.</span></span> <span data-ttu-id="54892-144">請注意，因為使用 <xref:System.Activities.WorkflowApplication.Load%2A> 的 <xref:System.Activities.WorkflowApplicationInstance> 多載，<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 會使用在 <xref:System.Activities.WorkflowApplicationInstance> 上設定的 <xref:System.Activities.WorkflowApplication>，因此不需設定其 <xref:System.Activities.WorkflowApplication.InstanceStore%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="54892-144">Note that because the <xref:System.Activities.WorkflowApplication.Load%2A> overload that takes the <xref:System.Activities.WorkflowApplicationInstance> is used, the <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> that was configured on the <xref:System.Activities.WorkflowApplicationInstance> is used by the <xref:System.Activities.WorkflowApplication> and therefore its <xref:System.Activities.WorkflowApplication.InstanceStore%2A> property does not need to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="54892-145">如果設定了<xref:System.Activities.WorkflowApplication.InstanceStore%2A> 屬性，必須以 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 使用的同一個 <xref:System.Activities.WorkflowApplicationInstance> 執行個體進行設定，否則會擲回 <xref:System.ArgumentException>，並出現下列訊息：`The instance is configured with a different InstanceStore than this WorkflowApplication.`。</span><span class="sxs-lookup"><span data-stu-id="54892-145">If the <xref:System.Activities.WorkflowApplication.InstanceStore%2A> property is set, it must be set with the same <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> instance used by the <xref:System.Activities.WorkflowApplicationInstance> or else an <xref:System.ArgumentException> will be thrown with the following message: `The instance is configured with a different InstanceStore than this WorkflowApplication.`.</span></span>

```csharp
// Get the WorkflowApplicationInstance of the desired workflow from the specified
// SqlWorkflowInstanceStore.
WorkflowApplicationInstance instance = WorkflowApplication.GetInstance(instanceId, store);

// Use the persisted WorkflowIdentity to retrieve the correct workflow
// definition from the dictionary.
Activity definition = WorkflowVersionMap[instance.DefinitionIdentity];

WorkflowApplication wfApp = new WorkflowApplication(definition, instance.DefinitionIdentity);

// Configure the WorkflowApplication with persistence and desired workflow event handlers.
ConfigureWorkflowApplication(wfApp);

// Load the persisted workflow instance.
wfApp.Load(instance);

// Resume the workflow...
```

## <a name="upgrading-net-framework-4-persistence-databases-to-support-workflow-versioning"></a><a name="UpdatingWF4PersistenceDatabases"></a><span data-ttu-id="54892-146">升級 .NET Framework 4 持續性資料庫以支援工作流程版本控制</span><span class="sxs-lookup"><span data-stu-id="54892-146">Upgrading .NET Framework 4 Persistence Databases to Support Workflow Versioning</span></span>

<span data-ttu-id="54892-147">提供 Sqlworkflowinstancestoreschemaupgrade.sql 的 sql database 腳本，以升級使用 .NET Framework 4 資料庫腳本所建立的持續性資料庫。</span><span class="sxs-lookup"><span data-stu-id="54892-147">A SqlWorkflowInstanceStoreSchemaUpgrade.sql database script is provided to upgrade persistence databases created using the .NET Framework 4 database scripts.</span></span> <span data-ttu-id="54892-148">此腳本會更新資料庫，以支援 .NET Framework 4.5 中引進的新版本控制功能。</span><span class="sxs-lookup"><span data-stu-id="54892-148">This script updates the databases to support the new versioning capabilities introduced in .NET Framework 4.5.</span></span> <span data-ttu-id="54892-149">資料庫中的任何持續性工作流程執行個體，都會有版本控制預設值，並可以參與並存執行和動態更新。</span><span class="sxs-lookup"><span data-stu-id="54892-149">Any persisted workflow instances in the databases are given default versioning values, and can then participate in side-by-side execution and dynamic update.</span></span>

<span data-ttu-id="54892-150">如果 .NET Framework 4.5 工作流程應用程式嘗試在尚未使用所提供的腳本升級的持續性資料庫上使用新版本設定功能的任何持續性作業，則會擲回， <xref:System.Runtime.DurableInstancing.InstancePersistenceCommandException> 並顯示類似下列訊息的訊息。</span><span class="sxs-lookup"><span data-stu-id="54892-150">If a .NET Framework 4.5 workflow application attempts any persistence operations that use the new versioning features on a persistence database which has not been upgraded using the provided script, an <xref:System.Runtime.DurableInstancing.InstancePersistenceCommandException> is thrown with a message similar to the following message.</span></span>

```output
The SqlWorkflowInstanceStore has a database version of '4.0.0.0'. InstancePersistenceCommand 'System.Activities.DurableInstancing.CreateWorkflowOwnerWithIdentityCommand' cannot be run against this database version.  Please upgrade the database to '4.5.0.0'.
```

### <a name="to-upgrade-the-database-schema"></a><a name="ToUpgrade"></a><span data-ttu-id="54892-151">若要升級資料庫架構</span><span class="sxs-lookup"><span data-stu-id="54892-151">To upgrade the database schema</span></span>

1. <span data-ttu-id="54892-152">開啟 SQL Server Management Studio 並連接到持續性資料庫伺服器，例如 **.\SQLEXPRESS**。</span><span class="sxs-lookup"><span data-stu-id="54892-152">Open SQL Server Management Studio and connect to the persistence database server, for example **.\SQLEXPRESS**.</span></span>

2. <span data-ttu-id="54892-153">從 **[檔案**] 功能表中選擇 [**開啟** **]、[** 檔案]。</span><span class="sxs-lookup"><span data-stu-id="54892-153">Choose **Open**, **File** from the **File** menu.</span></span> <span data-ttu-id="54892-154">瀏覽至下列資料夾：`C:\Windows\Microsoft.NET\Framework\v4.0.30319\sql\en`</span><span class="sxs-lookup"><span data-stu-id="54892-154">Browse to the following folder: `C:\Windows\Microsoft.NET\Framework\v4.0.30319\sql\en`</span></span>

3. <span data-ttu-id="54892-155">選取**sqlworkflowinstancestoreschemaupgrade.sql** ，然後按一下 [**開啟**]。</span><span class="sxs-lookup"><span data-stu-id="54892-155">Select **SqlWorkflowInstanceStoreSchemaUpgrade.sql** and click **Open**.</span></span>

4. <span data-ttu-id="54892-156">在 [**可用的資料庫**] 下拉式選單中，選取持續性資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="54892-156">Select the name of the persistence database in the **Available Databases** drop-down.</span></span>

5. <span data-ttu-id="54892-157">從 [**查詢**] 功能表中選擇 [**執行**]。</span><span class="sxs-lookup"><span data-stu-id="54892-157">Choose **Execute** from the **Query** menu.</span></span>

<span data-ttu-id="54892-158">查詢完成時，資料庫結構描述即已升級，若有需要，可以檢視指派給持續性工作流程執行個體的預設工作流程識別。</span><span class="sxs-lookup"><span data-stu-id="54892-158">When the query completes, the database schema is upgraded, and if desired, you can view the default workflow identity that was assigned to the persisted workflow instances.</span></span> <span data-ttu-id="54892-159">在 [**物件總管**] 的 [**資料庫**] 節點中展開您的持續性資料庫，然後展開 [ **Views** ] 節點。</span><span class="sxs-lookup"><span data-stu-id="54892-159">Expand your persistence database in the **Databases** node of the **Object Explorer**, and then expand the **Views** node.</span></span> <span data-ttu-id="54892-160">以滑鼠右鍵按一下 [ **DurableInstancing** ]，然後選擇 [**選取前 1000**個數據列]。</span><span class="sxs-lookup"><span data-stu-id="54892-160">Right-click **System.Activities.DurableInstancing.Instances** and choose **Select Top 1000 Rows**.</span></span> <span data-ttu-id="54892-161">滾動到資料行的結尾，並請注意，有六個額外的資料行已加入至視圖： **IdentityName**、 **IdentityPackage**、 **Build**、**主要**、**次要**和**修訂**。</span><span class="sxs-lookup"><span data-stu-id="54892-161">Scroll to end of the columns and note that there are six additional columns added to the view: **IdentityName**, **IdentityPackage**, **Build**, **Major**, **Minor**, and **Revision**.</span></span> <span data-ttu-id="54892-162">任何持續性的工作流程在這些欄位中都會有**null**值，代表 null 工作流程身分識別。</span><span class="sxs-lookup"><span data-stu-id="54892-162">Any persisted workflows will have a value of **NULL** for these fields, representing a null workflow identity.</span></span>
