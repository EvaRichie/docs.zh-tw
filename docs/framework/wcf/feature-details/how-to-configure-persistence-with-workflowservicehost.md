---
title: 作法：以 WorkflowServiceHost 設定持續性
ms.date: 03/30/2017
ms.assetid: e31cd4df-13a3-4a9a-9be8-5243e0055356
ms.openlocfilehash: 3d8b7183b11c138b8da1f04d9084f8b94b7dcaa6
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96257336"
---
# <a name="how-to-configure-persistence-with-workflowservicehost"></a>作法：以 WorkflowServiceHost 設定持續性

本主題描述如何設定 SQL 工作流程執行個體存放區功能，透過使用組態檔以啟用裝載於 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 中之工作流程的持續性。 使用 SQL 工作流程執行個體存放區功能前，您必須建立一個用於保存工作流程執行個體的 SQL 資料庫。 如需詳細資訊，請參閱 [如何：啟用工作流程和工作流程服務的 SQL 持續](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)性。  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-configuration"></a>若要在組態中設定 SQL 工作流程執行個體存放區  
  
1. 您可以透過 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 設定 SQL 工作流程執行個體存放區的屬性，這個服務行為可以讓您透過 XML 組態變更設定。 下列設定範例示範如何使用設定檔中的 <> 行為專案來設定 SQL 工作流程實例存放區 `sqlWorkflowInstanceStore` 。  
  
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
  
     如需有關如何設定 SQL 工作流程實例存放區的詳細資訊，請參閱 [如何：啟用工作流程和工作流程服務的 SQL 持續](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)性。 如需 <> 行為元素個別設定的詳細資訊 `sqlWorkflowInstanceStore` ，請參閱 [SQL 工作流程實例存放區](../../windows-workflow-foundation/sql-workflow-instance-store.md)。 Windows Server App Fabric 會提供它自己的持續性存放區。 如需詳細資訊，請參閱 [Windows Server App Fabric 持續](/previous-versions/appfabric/ee677272(v=azure.10))性。  
  
    > [!NOTE]
    > 上述組態範例會使用簡化的組態。 如需詳細資訊，請參閱[簡化](../simplified-configuration.md)的設定  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-code"></a>若要在程式碼中設定 SQL 工作流程執行個體存放區  
  
1. 您可以透過 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 設定 SQL 工作流程執行個體存放區的屬性，這個服務行為可以讓您透過程式碼變更設定。 下列範例示範如何使用程式碼中的 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 行為項目來設定 SQL 工作流程執行個體存放區。  
  
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
  
     如需有關如何設定 SQL 工作流程實例存放區的詳細資訊，請參閱 [如何：啟用工作流程和工作流程服務的 SQL 持續](../../windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)性。 如需行為元素個別設定的詳細資訊 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> ，請參閱 [SQL 工作流程實例存放區](../../windows-workflow-foundation/sql-workflow-instance-store.md)。 Windows Server App Fabric 會提供它自己的持續性存放區。 如需詳細資訊，請參閱 [Windows Server App Fabric 持續](/previous-versions/appfabric/ee677272(v=azure.10))性。  
  
    > [!NOTE]
    > 上述組態範例會使用簡化的組態。 如需詳細資訊，請參閱[簡化](../simplified-configuration.md)的設定  
  
     如需如何以程式設計方式設定持續性的範例，請參閱 [如何：啟用工作流程和工作流程服務的持續](../../windows-workflow-foundation/how-to-enable-persistence-for-workflows-and-workflow-services.md)性。  
  
## <a name="see-also"></a>另請參閱

- [工作流程服務](workflow-services.md)
- [工作流程持續性](../../windows-workflow-foundation/workflow-persistence.md)
- [Windows Server App Fabric 持續性概念](/previous-versions/appfabric/ee677272(v=azure.10))
