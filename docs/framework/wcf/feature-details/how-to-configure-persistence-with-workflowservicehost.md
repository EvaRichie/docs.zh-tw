---
title: HOW TO：以 WorkflowServiceHost 設定持續性
ms.date: 03/30/2017
ms.assetid: e31cd4df-13a3-4a9a-9be8-5243e0055356
ms.openlocfilehash: 4ed9c76f091e75cf6ba7658f0314d2e21bbe962e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599109"
---
# <a name="how-to-configure-persistence-with-workflowservicehost"></a><span data-ttu-id="86f4e-102">HOW TO：以 WorkflowServiceHost 設定持續性</span><span class="sxs-lookup"><span data-stu-id="86f4e-102">How to: Configure Persistence with WorkflowServiceHost</span></span>
<span data-ttu-id="86f4e-103">本主題描述如何設定 SQL 工作流程執行個體存放區功能，透過使用組態檔以啟用裝載於 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 中之工作流程的持續性。</span><span class="sxs-lookup"><span data-stu-id="86f4e-103">This topic describes how to configure the SQL Workflow Instance Store feature to enable persistence for workflows hosted in <xref:System.ServiceModel.Activities.WorkflowServiceHost> by using a configuration file.</span></span> <span data-ttu-id="86f4e-104">使用 SQL 工作流程執行個體存放區功能前，您必須建立一個用於保存工作流程執行個體的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="86f4e-104">Before using the SQL Workflow Instance Store feature you must create a SQL database that is used to persist workflow instances.</span></span> <span data-ttu-id="86f4e-105">如需詳細資訊，請參閱[如何：啟用工作流程和工作流程服務的 SQL 持續](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)性。</span><span class="sxs-lookup"><span data-stu-id="86f4e-105">For more information, see [How to: Enable SQL Persistence for Workflows and Workflow Services](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).</span></span>  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-configuration"></a><span data-ttu-id="86f4e-106">若要在組態中設定 SQL 工作流程執行個體存放區</span><span class="sxs-lookup"><span data-stu-id="86f4e-106">To Configure the SQL Workflow Instance Store in Configuration</span></span>  
  
1. <span data-ttu-id="86f4e-107">您可以透過 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 設定 SQL 工作流程執行個體存放區的屬性，這個服務行為可以讓您透過 XML 組態變更設定。</span><span class="sxs-lookup"><span data-stu-id="86f4e-107">The properties of the SQL workflow instance store can be configured through the <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>, a service behavior that allows you to change the settings through XML configuration.</span></span> <span data-ttu-id="86f4e-108">下列設定範例示範如何使用設定檔中的 <> 行為專案來設定 SQL 工作流程實例存放區 `sqlWorkflowInstanceStore` 。</span><span class="sxs-lookup"><span data-stu-id="86f4e-108">The following configuration example shows how to configure the SQL workflow instance store by using the <`sqlWorkflowInstanceStore`> behavior element in a configuration file.</span></span>  
  
    ```xml  
    <serviceBehaviors>  
        <behavior name="">  
            <sqlWorkflowInstanceStore
                 connectionString="provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                 instanceEncodingOption="GZip | None"  
                 instanceCompletionAction="DeleteAll | DeleteNothing"  
                 instanceLockedExceptionAction="NoRetry | SimpleRetry | AggressiveRetry"  
                 hostLockRenewalPeriod="00:00:30"
                 runnableInstancesDetectionPeriod="00:00:05">  
            </sqlWorkflowInstanceStore>  
        </behavior>  
    </serviceBehaviors>  
    ```  
  
     <span data-ttu-id="86f4e-109">如需有關如何設定 SQL 工作流程實例存放區的詳細資訊，請參閱[如何：啟用工作流程和工作流程服務的 SQL 持續](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)性。</span><span class="sxs-lookup"><span data-stu-id="86f4e-109">For more information about how to configure the SQL workflow instance store, see [How to: Enable SQL Persistence for Workflows and Workflow Services](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).</span></span> <span data-ttu-id="86f4e-110">如需 <> 行為元素之個別設定的詳細資訊 `sqlWorkflowInstanceStore` ，請參閱[SQL 工作流程實例存放區](../../windows-workflow-foundation/sql-workflow-instance-store.md)。</span><span class="sxs-lookup"><span data-stu-id="86f4e-110">For more information about the individual settings for the <`sqlWorkflowInstanceStore`> behavior element, see [SQL Workflow Instance Store](../../windows-workflow-foundation/sql-workflow-instance-store.md).</span></span> <span data-ttu-id="86f4e-111">Windows Server App Fabric 會提供它自己的持續性存放區。</span><span class="sxs-lookup"><span data-stu-id="86f4e-111">Windows Server App Fabric provides its own persistence store.</span></span> <span data-ttu-id="86f4e-112">如需詳細資訊，請參閱[Windows Server App Fabric 持續](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10))性。</span><span class="sxs-lookup"><span data-stu-id="86f4e-112">For more information, see [Windows Server App Fabric Persistence](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10)).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="86f4e-113">上述組態範例會使用簡化的組態。</span><span class="sxs-lookup"><span data-stu-id="86f4e-113">The preceding configuration example uses simplified configuration.</span></span> <span data-ttu-id="86f4e-114">如需詳細資訊，請參閱[簡化](../simplified-configuration.md)的設定</span><span class="sxs-lookup"><span data-stu-id="86f4e-114">For more information, see [Simplified Configuration](../simplified-configuration.md)</span></span>  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-code"></a><span data-ttu-id="86f4e-115">若要在程式碼中設定 SQL 工作流程執行個體存放區</span><span class="sxs-lookup"><span data-stu-id="86f4e-115">To Configure the SQL Workflow Instance Store in Code</span></span>  
  
1. <span data-ttu-id="86f4e-116">您可以透過 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 設定 SQL 工作流程執行個體存放區的屬性，這個服務行為可以讓您透過程式碼變更設定。</span><span class="sxs-lookup"><span data-stu-id="86f4e-116">The properties of the SQL workflow instance store can be configured through the <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>, a service behavior that allows you to change the settings through code.</span></span> <span data-ttu-id="86f4e-117">下列範例示範如何使用程式碼中的 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 行為項目來設定 SQL 工作流程執行個體存放區。</span><span class="sxs-lookup"><span data-stu-id="86f4e-117">The following example shows how to configure the SQL workflow instance store by using the <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> behavior element in a code</span></span>  
  
    ```csharp  
    host.Description.Behaviors.Add(new SqlWorkflowInstanceStoreBehavior  
    {  
       ConnectionString = "provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true",  
       InstanceEncodingOption = "GZip | None",  
       InstanceCompletionAction = "DeleteAll | DeleteNothing",  
       InstanceLockedExceptionAction = "NoRetry | SimpleRetry | AggressiveRetry",  
       HostLockRenewalPeriod = new TimeSpan(00, 00, 30),  
       RunnableInstancesDetectionPeriod = new TimeSpan(00, 00, 05)  
    });  
    ```  
  
     <span data-ttu-id="86f4e-118">如需有關如何設定 SQL 工作流程實例存放區的詳細資訊，請參閱[如何：啟用工作流程和工作流程服務的 SQL 持續](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)性。</span><span class="sxs-lookup"><span data-stu-id="86f4e-118">For more information about how to configure the SQL workflow instance store, see [How to: Enable SQL Persistence for Workflows and Workflow Services](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md).</span></span> <span data-ttu-id="86f4e-119">如需行為元素之個別設定的詳細資訊 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> ，請參閱[SQL 工作流程實例存放區](../../windows-workflow-foundation/sql-workflow-instance-store.md)。</span><span class="sxs-lookup"><span data-stu-id="86f4e-119">For more information about the individual settings for the <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> behavior element, see [SQL Workflow Instance Store](../../windows-workflow-foundation/sql-workflow-instance-store.md).</span></span> <span data-ttu-id="86f4e-120">Windows Server App Fabric 會提供它自己的持續性存放區。</span><span class="sxs-lookup"><span data-stu-id="86f4e-120">Windows Server App Fabric provides its own persistence store.</span></span> <span data-ttu-id="86f4e-121">如需詳細資訊，請參閱[Windows Server App Fabric 持續](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10))性。</span><span class="sxs-lookup"><span data-stu-id="86f4e-121">For more information, see [Windows Server App Fabric Persistence](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10)).</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="86f4e-122">上述組態範例會使用簡化的組態。</span><span class="sxs-lookup"><span data-stu-id="86f4e-122">The preceding configuration example uses simplified configuration.</span></span> <span data-ttu-id="86f4e-123">如需詳細資訊，請參閱[簡化](../simplified-configuration.md)的設定</span><span class="sxs-lookup"><span data-stu-id="86f4e-123">For more information, see [Simplified Configuration](../simplified-configuration.md)</span></span>  
  
     <span data-ttu-id="86f4e-124">如需如何以程式設計方式設定持續性的範例，請參閱[如何：啟用工作流程和工作流程服務的持續](../../windows-workflow-foundation/how-to-enable-persistence-for-workflows-and-workflow-services.md)性。</span><span class="sxs-lookup"><span data-stu-id="86f4e-124">For an example of how to configure persistence programmatically see [How to: Enable Persistence for Workflows and Workflow Services](../../windows-workflow-foundation/how-to-enable-persistence-for-workflows-and-workflow-services.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="86f4e-125">請參閱</span><span class="sxs-lookup"><span data-stu-id="86f4e-125">See also</span></span>

- [<span data-ttu-id="86f4e-126">工作流程服務</span><span class="sxs-lookup"><span data-stu-id="86f4e-126">Workflow Services</span></span>](workflow-services.md)
- [<span data-ttu-id="86f4e-127">工作流程持續性</span><span class="sxs-lookup"><span data-stu-id="86f4e-127">Workflow Persistence</span></span>](../../windows-workflow-foundation/workflow-persistence.md)
- <span data-ttu-id="86f4e-128">[Windows Server App Fabric 持續性概念](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="86f4e-128">[Windows Server App Fabric Persistence](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10))</span></span>
