---
title: SQL 工作流程執行個體存放區
ms.date: 03/30/2017
ms.assetid: 8cd2f8a5-4bf8-46ea-8909-c7fdb314fabc
ms.openlocfilehash: e0989e4ed5d9e256d3570b0c3ee2bb35a95b410a
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96261744"
---
# <a name="sql-workflow-instance-store"></a><span data-ttu-id="669ac-102">SQL 工作流程執行個體存放區</span><span class="sxs-lookup"><span data-stu-id="669ac-102">SQL Workflow Instance Store</span></span>

<span data-ttu-id="669ac-103">[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 隨附於 SQL 工作流程執行個體存放區，可讓工作流程將有關工作流程執行個體的狀態資訊保存在 SQL Server 2005 或 SQL Server 2008 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="669ac-103">The [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] ships with the SQL Workflow Instance Store, which allows workflows to persist state information about workflow instances in a SQL Server 2005 or SQL Server 2008 database.</span></span> <span data-ttu-id="669ac-104">這項功能主要是以 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 類別的形式實作，該類別衍生自持續性架構的抽象 <xref:System.Runtime.DurableInstancing.InstanceStore> 類別。</span><span class="sxs-lookup"><span data-stu-id="669ac-104">This feature is primarily implemented in the form of the <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> class, which derives from the abstract <xref:System.Runtime.DurableInstancing.InstanceStore> class of the persistence framework.</span></span> <span data-ttu-id="669ac-105">SQL 工作流程執行個體存放區功能會構成 SQL 持續性提供者，該提供者是持續性 API 的具象實作，主機會運用此 API 將持續性命令傳送至存放區。</span><span class="sxs-lookup"><span data-stu-id="669ac-105">The SQL Workflow Instance Store feature constitutes a SQL persistence provider, which is a concrete implementation of the persistence API that a host uses to send persistence commands to the store.</span></span>  
  
 <span data-ttu-id="669ac-106">SQL 工作流程執行個體存放區支援使用 <xref:System.Activities.WorkflowApplication> 或 <xref:System.ServiceModel.WorkflowServiceHost> 的自我裝載工作流程或工作流程服務，以及使用 <xref:System.ServiceModel.WorkflowServiceHost> 裝載於 WAS 中的服務。</span><span class="sxs-lookup"><span data-stu-id="669ac-106">The SQL Workflow Instance Store supports both self-hosted workflows or workflow services that use <xref:System.Activities.WorkflowApplication> or <xref:System.ServiceModel.WorkflowServiceHost> as well as services hosted in WAS using <xref:System.ServiceModel.WorkflowServiceHost>.</span></span> <span data-ttu-id="669ac-107">您可以使用這項功能所公開的物件模型，以程式設計方式設定自我裝載服務的 SQL 工作流程執行個體存放區功能。</span><span class="sxs-lookup"><span data-stu-id="669ac-107">You can configure the SQL Workflow Instance Store feature for self-hosted services programmatically by using the object model exposed by the feature.</span></span> <span data-ttu-id="669ac-108">您可以使用物件模型及 XML 組態檔，以程式設計方式，針對由 <xref:System.ServiceModel.WorkflowServiceHost> 裝載的服務，設定這項功能。</span><span class="sxs-lookup"><span data-stu-id="669ac-108">You can configure this feature for services hosted by <xref:System.ServiceModel.WorkflowServiceHost> both programmatically by using the object model and also by using an XML configuration file.</span></span>  
  
 <span data-ttu-id="669ac-109">SQL 工作流程實例存放區功能 (**SqlWorkflowInstanceStore** 類別) 不會執行 <xref:System.ServiceModel.Persistence.PersistenceProviderFactory> ，因此不會提供持久的非工作流程 WCF 服務的持續性支援。</span><span class="sxs-lookup"><span data-stu-id="669ac-109">The SQL Workflow Instance Store feature (**SqlWorkflowInstanceStore** class) does not implement <xref:System.ServiceModel.Persistence.PersistenceProviderFactory> and hence does not offer persistence support for durable non-workflow WCF services.</span></span> <span data-ttu-id="669ac-110">此外，該功能也不會實作 <xref:System.Workflow.Runtime.Hosting.WorkflowPersistenceService>，因此不針對 3.x 工作流程提供持續性支援。</span><span class="sxs-lookup"><span data-stu-id="669ac-110">It also does not implement <xref:System.Workflow.Runtime.Hosting.WorkflowPersistenceService> and hence does not offer persistence support for 3.x workflows.</span></span> <span data-ttu-id="669ac-111">這項功能僅支援 WF 4.0 (和更新版本) 工作流程及工作流程服務的持續性。</span><span class="sxs-lookup"><span data-stu-id="669ac-111">The feature supports persistence for only WF 4.0 (and later) workflows and workflow services.</span></span> <span data-ttu-id="669ac-112">除了 SQL Server 2005 和 SQL Server 2008 以外，此功能亦不支援其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="669ac-112">The feature also does not support any databases other than SQL Server 2005 and SQL Server 2008.</span></span>  
  
 <span data-ttu-id="669ac-113">本節中的主題描述 SQL 工作流程執行個體存放區的屬性和功能，同時說明關於設定存放區的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="669ac-113">The topics in this section describe properties and features of the SQL Workflow Instance Store and provide you with details on configuring the store.</span></span>  
  
 <span data-ttu-id="669ac-114">Windows Server App Fabric 提供其本身的執行個體存放區和工具，可簡化執行個體存放區的設定和使用。</span><span class="sxs-lookup"><span data-stu-id="669ac-114">Windows Server App Fabric provides its own instance store and tooling to simplify the configuration and use of the instance store.</span></span> <span data-ttu-id="669ac-115">如需詳細資訊，請參閱 [Windows Server App Fabric 實例存放區](/previous-versions/appfabric/ff383417(v=azure.10))。</span><span class="sxs-lookup"><span data-stu-id="669ac-115">For more information, see [Windows Server App Fabric Instance Store](/previous-versions/appfabric/ff383417(v=azure.10)).</span></span> <span data-ttu-id="669ac-116">如需 App Fabric SQL Server 持續性資料庫的詳細資訊，請參閱 [App fabric SQL Server 持續性資料庫](/previous-versions/appfabric/ee790819(v=azure.10))</span><span class="sxs-lookup"><span data-stu-id="669ac-116">For more information about the App Fabric SQL Server Persistence Database see [App Fabric SQL Server Persistence Database](/previous-versions/appfabric/ee790819(v=azure.10))</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="669ac-117">本節內容</span><span class="sxs-lookup"><span data-stu-id="669ac-117">In This Section</span></span>  
  
- [<span data-ttu-id="669ac-118">SQL 工作流程執行個體存放區的屬性</span><span class="sxs-lookup"><span data-stu-id="669ac-118">Properties of SQL Workflow Instance Store</span></span>](properties-of-sql-workflow-instance-store.md)  
  
- [<span data-ttu-id="669ac-119">作法：啟用工作流程與工作流程服務的 SQL 持續性</span><span class="sxs-lookup"><span data-stu-id="669ac-119">How to: Enable SQL Persistence for Workflows and Workflow Services</span></span>](how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)  
  
- [<span data-ttu-id="669ac-120">執行個體啟動</span><span class="sxs-lookup"><span data-stu-id="669ac-120">Instance Activation</span></span>](instance-activation.md)  
  
- [<span data-ttu-id="669ac-121">支援查詢</span><span class="sxs-lookup"><span data-stu-id="669ac-121">Support for Queries</span></span>](support-for-queries.md)  
  
- [<span data-ttu-id="669ac-122">存放區擴充性</span><span class="sxs-lookup"><span data-stu-id="669ac-122">Store Extensibility</span></span>](store-extensibility.md)  
  
- [<span data-ttu-id="669ac-123">安全性</span><span class="sxs-lookup"><span data-stu-id="669ac-123">Security</span></span>](security.md)  
  
- [<span data-ttu-id="669ac-124">SQL Server 持續性資料庫</span><span class="sxs-lookup"><span data-stu-id="669ac-124">SQL Server Persistence Database</span></span>](sql-server-persistence-database.md)  
  
## <a name="see-also"></a><span data-ttu-id="669ac-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="669ac-125">See also</span></span>

- <span data-ttu-id="669ac-126">[持續性範例](/previous-versions/dotnet/netframework-4.0/dd699769(v=vs.100))</span><span class="sxs-lookup"><span data-stu-id="669ac-126">[Persistence Samples](/previous-versions/dotnet/netframework-4.0/dd699769(v=vs.100))</span></span>
