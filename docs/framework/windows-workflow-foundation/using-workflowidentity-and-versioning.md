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
# <a name="using-workflowidentity-and-versioning"></a>使用 WorkflowIdentity 與版本控制

<xref:System.Activities.WorkflowIdentity> 提供一種方法，讓工作流程應用程式開發人員能夠將名稱和 <xref:System.Version> 與工作流程定義建立關聯，並為這項資訊與持續性的工作流程執行個體建立關聯。 此身分識別資訊可由工作流程應用程式開發人員使用以啟用案例 (例如並存執行多個版本的工作流程定義)，以及提供動態更新等其他功能的基礎。 本主題提供使用 <xref:System.Activities.WorkflowIdentity> 搭配 <xref:System.Activities.WorkflowApplication> 裝載的概觀。 如需在工作流程服務中並存執行工作流程定義的詳細資訊，請參閱[WorkflowServiceHost 中的並存版本控制](../wcf/feature-details/side-by-side-versioning-in-workflowservicehost.md)。 如需動態更新的詳細資訊，請參閱[動態更新](dynamic-update.md)。

## <a name="in-this-topic"></a>本主題內容

- [使用 WorkflowIdentity](using-workflowidentity-and-versioning.md#UsingWorkflowIdentity)

  - [使用 WorkflowIdentity 並存執行](using-workflowidentity-and-versioning.md#SxS)

- [升級 .NET Framework 4 持續性資料庫以支援工作流程版本控制](using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases)

  - [升級資料庫結構描述](using-workflowidentity-and-versioning.md#ToUpgrade)

## <a name="using-workflowidentity"></a><a name="UsingWorkflowIdentity"></a>使用 WorkflowIdentity

若要使用 <xref:System.Activities.WorkflowIdentity>，請建立執行個體、加以設定，並將其與 <xref:System.Activities.WorkflowApplication> 執行個體建立關聯。 <xref:System.Activities.WorkflowIdentity> 執行個體包含三項識別資訊。 <xref:System.Activities.WorkflowIdentity.Name%2A> 和 <xref:System.Activities.WorkflowIdentity.Version%2A> 包含名稱及 <xref:System.Version>，兩者都是必要項，而 <xref:System.Activities.WorkflowIdentity.Package%2A> 則是選用項，可用來指定包含資訊 (例如組件名稱或其他所需資訊) 的其他字串。 如果 <xref:System.Activities.WorkflowIdentity> 的三個屬性中有任何屬性與另一個 <xref:System.Activities.WorkflowIdentity> 的不同，則其為唯一識別。

> [!IMPORTANT]
> <xref:System.Activities.WorkflowIdentity> 不應包含任何個人可識別資訊 (PII)。 執行階段會在數個不同的活動生命週期點，將有關<xref:System.Activities.WorkflowIdentity> (用來建立執行個體) 的資訊發出到任何已設定的追蹤服務。 WF 追蹤沒有任何機制可隱藏 PII (機密的使用者資料)。 因此，<xref:System.Activities.WorkflowIdentity> 執行個體不應包含任何 PII 資料，因為執行階段會在追蹤記錄中發出這項資訊，因此存取檢視追蹤記錄的人有可能看見這項資訊。

在下列範例中，建立了 <xref:System.Activities.WorkflowIdentity>，並將其與使用 `MortgageWorkflow` 工作流程定義來建立的工作流程執行個體建立關聯。

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

重新載入並繼續工作流程時，所使用的 <xref:System.Activities.WorkflowIdentity> 必須設定為符合持續性工作流程執行個體的 <xref:System.Activities.WorkflowIdentity>。

```csharp
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identityV1);

// Configure the WorkflowApplication with persistence and desired workflow event handlers.
ConfigureWorkflowApplication(wfApp);

// Load the workflow.
wfApp.Load(instanceId);

// Resume the workflow...
```

如果在重新載入工作流程執行個體時，使用的 <xref:System.Activities.WorkflowIdentity> 與持續性 <xref:System.Activities.WorkflowIdentity> 不相符，會擲回 <xref:System.Activities.VersionMismatchException>。 在下列範例中，會在上一個範例中持續性 `MortgageWorkflow` 執行個體上載入。 這個載入嘗試是使用針對較新版抵押工作流程設定的 <xref:System.Activities.WorkflowIdentity>，該工作流程與持續性執行個體不相符。

```csharp
WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow_v2(), identityV2);

// Configure the WorkflowApplication with persistence and desired workflow event handlers.
ConfigureWorkflowApplication(wfApp);

// Attempt to load the workflow instance.
wfApp.Load(instanceId);

// Resume the workflow...
```

執行先前的程式碼時，會擲回 <xref:System.Activities.VersionMismatchException>。

```output
The WorkflowIdentity ('MortgageWorkflow v1; Version=1.0.0.0') of the loaded instance does not match the WorkflowIdentity ('MortgageWorkflow v2; Version=2.0.0.0') of the provided workflow definition. The instance can be loaded using a different definition, or updated using Dynamic Update.
```

### <a name="side-by-side-execution-using-workflowidentity"></a><a name="SxS"></a>使用 WorkflowIdentity 並存執行

<xref:System.Activities.WorkflowIdentity> 可加速並存執行多種版本的工作流程。 常見的案例之一是變更長時間執行工作流程的業務需求。 部署更新版本時，可以執行同一個工作流程的多個執行個體。 主應用程式可以設定為在啟動新執行個體時使用更新的工作流程定義，而且主應用程式必須在繼續執行個體時，負責提供正確的工作流程定義。 <xref:System.Activities.WorkflowIdentity> 可以在繼續工作流程執行個體時識別和提供相符的工作流程定義。

為了擷取持續性工作流程執行個體的 <xref:System.Activities.WorkflowIdentity>，會使用 <xref:System.Activities.WorkflowApplication.GetInstance%2A> 方法。 <xref:System.Activities.WorkflowApplication.GetInstance%2A> 方法會採用持續性工作流程執行個體的 <xref:System.Activities.WorkflowApplication.Id%2A> 及包含持續性執行個體的 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>，並且傳回 <xref:System.Activities.WorkflowApplicationInstance>。 <xref:System.Activities.WorkflowApplicationInstance> 包含持續性工作流程執行個體的相關資訊，包括與其相關聯的 <xref:System.Activities.WorkflowIdentity>。 載入及繼續工作流程執行個體時，主機可以使用此相關聯的 <xref:System.Activities.WorkflowIdentity> 來提供正確的工作流程定義。

> [!NOTE]
> Null <xref:System.Activities.WorkflowIdentity> 為有效，而且可讓主機用來將沒有相關聯 <xref:System.Activities.WorkflowIdentity> 的持續性執行個體，對應至適當的工作流程定義。 當工作流應用程式一開始不是以工作流程版本設定來撰寫，或從 .NET Framework 4 升級應用程式時，就可能發生此情況。 如需詳細資訊，請參閱[升級 .NET Framework 4 持續性資料庫以支援工作流程版本控制](using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases)。

在下列範例中 `Dictionary<WorkflowIdentity, Activity>` ，是用來將 <xref:System.Activities.WorkflowIdentity> 實例與其相符的工作流程定義產生關聯，並使用 `MortgageWorkflow` 與相關聯的工作流程定義來啟動工作流程 `identityV1` <xref:System.Activities.WorkflowIdentity> 。

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

在下列範例中，會呼叫 <xref:System.Activities.WorkflowApplication.GetInstance%2A>，以從上一個範例擷取持續性工作流程執行個體的相關資訊，並使用持續性 <xref:System.Activities.WorkflowIdentity> 資訊來擷取相符的工作流程定義。 此資訊可用來設定 <xref:System.Activities.WorkflowApplication>，然後載入工作流程。 請注意，因為使用 <xref:System.Activities.WorkflowApplication.Load%2A> 的 <xref:System.Activities.WorkflowApplicationInstance> 多載，<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 會使用在 <xref:System.Activities.WorkflowApplicationInstance> 上設定的 <xref:System.Activities.WorkflowApplication>，因此不需設定其 <xref:System.Activities.WorkflowApplication.InstanceStore%2A> 屬性。

> [!NOTE]
> 如果設定了<xref:System.Activities.WorkflowApplication.InstanceStore%2A> 屬性，必須以 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 使用的同一個 <xref:System.Activities.WorkflowApplicationInstance> 執行個體進行設定，否則會擲回 <xref:System.ArgumentException>，並出現下列訊息：`The instance is configured with a different InstanceStore than this WorkflowApplication.`。

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

## <a name="upgrading-net-framework-4-persistence-databases-to-support-workflow-versioning"></a><a name="UpdatingWF4PersistenceDatabases"></a>升級 .NET Framework 4 持續性資料庫以支援工作流程版本控制

提供 Sqlworkflowinstancestoreschemaupgrade.sql 的 sql database 腳本，以升級使用 .NET Framework 4 資料庫腳本所建立的持續性資料庫。 此腳本會更新資料庫，以支援 .NET Framework 4.5 中引進的新版本控制功能。 資料庫中的任何持續性工作流程執行個體，都會有版本控制預設值，並可以參與並存執行和動態更新。

如果 .NET Framework 4.5 工作流程應用程式嘗試在尚未使用所提供的腳本升級的持續性資料庫上使用新版本設定功能的任何持續性作業，則會擲回， <xref:System.Runtime.DurableInstancing.InstancePersistenceCommandException> 並顯示類似下列訊息的訊息。

```output
The SqlWorkflowInstanceStore has a database version of '4.0.0.0'. InstancePersistenceCommand 'System.Activities.DurableInstancing.CreateWorkflowOwnerWithIdentityCommand' cannot be run against this database version.  Please upgrade the database to '4.5.0.0'.
```

### <a name="to-upgrade-the-database-schema"></a><a name="ToUpgrade"></a>若要升級資料庫架構

1. 開啟 SQL Server Management Studio 並連接到持續性資料庫伺服器，例如 **.\SQLEXPRESS**。

2. 從 **[檔案**] 功能表中選擇 [**開啟** **]、[** 檔案]。 瀏覽至下列資料夾：`C:\Windows\Microsoft.NET\Framework\v4.0.30319\sql\en`

3. 選取**sqlworkflowinstancestoreschemaupgrade.sql** ，然後按一下 [**開啟**]。

4. 在 [**可用的資料庫**] 下拉式選單中，選取持續性資料庫的名稱。

5. 從 [**查詢**] 功能表中選擇 [**執行**]。

查詢完成時，資料庫結構描述即已升級，若有需要，可以檢視指派給持續性工作流程執行個體的預設工作流程識別。 在 [**物件總管**] 的 [**資料庫**] 節點中展開您的持續性資料庫，然後展開 [ **Views** ] 節點。 以滑鼠右鍵按一下 [ **DurableInstancing** ]，然後選擇 [**選取前 1000**個數據列]。 滾動到資料行的結尾，並請注意，有六個額外的資料行已加入至視圖： **IdentityName**、 **IdentityPackage**、 **Build**、**主要**、**次要**和**修訂**。 任何持續性的工作流程在這些欄位中都會有**null**值，代表 null 工作流程身分識別。
