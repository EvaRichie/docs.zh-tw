---
title: WorkflowHostingEndpoint 的書籤解析程式
ms.date: 03/30/2017
ms.assetid: 97fd5816-935e-4625-ad04-e6f6befa07de
ms.openlocfilehash: 6bcf1c1ac7c0ac9e385c4259ba085ab63afd7cfa
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96274604"
---
# <a name="bookmark-resolver-for-workflowhostingendpoint"></a><span data-ttu-id="97b27-102">WorkflowHostingEndpoint 的書籤解析程式</span><span class="sxs-lookup"><span data-stu-id="97b27-102">Bookmark Resolver for WorkflowHostingEndpoint</span></span>

<span data-ttu-id="97b27-103">這個範例示範 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 如何與 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 搭配使用以建立工作流程執行個體。</span><span class="sxs-lookup"><span data-stu-id="97b27-103">This sample demonstrates how the <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> can be used with <xref:System.ServiceModel.Activities.WorkflowServiceHost> to create workflow instances.</span></span>  
  
## <a name="demonstrates"></a><span data-ttu-id="97b27-104">示範</span><span class="sxs-lookup"><span data-stu-id="97b27-104">Demonstrates</span></span>  

 <span data-ttu-id="97b27-105"><xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>, <xref:System.ServiceModel.Activities.WorkflowServiceHost></span><span class="sxs-lookup"><span data-stu-id="97b27-105"><xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>, <xref:System.ServiceModel.Activities.WorkflowServiceHost></span></span>  
  
## <a name="discussion"></a><span data-ttu-id="97b27-106">討論</span><span class="sxs-lookup"><span data-stu-id="97b27-106">Discussion</span></span>  

 <span data-ttu-id="97b27-107">這個範例使用 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 來建立以 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 裝載的工作流程執行個體。</span><span class="sxs-lookup"><span data-stu-id="97b27-107">This sample uses the <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> to create workflow instances hosted using <xref:System.ServiceModel.Activities.WorkflowServiceHost>.</span></span> <span data-ttu-id="97b27-108"><xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 是 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的擴充點，可用於以下情形：</span><span class="sxs-lookup"><span data-stu-id="97b27-108"><xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> is an extensibility point for <xref:System.ServiceModel.Activities.WorkflowServiceHost> that can be used in the following scenarios:</span></span>  
  
- <span data-ttu-id="97b27-109">建立新的工作流程執行個體。</span><span class="sxs-lookup"><span data-stu-id="97b27-109">Creating new workflow instances.</span></span>  
  
- <span data-ttu-id="97b27-110">在裝載於 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的工作流程執行個體中繼續使用書籤。</span><span class="sxs-lookup"><span data-stu-id="97b27-110">Resuming bookmarks on workflow instance hosted in a <xref:System.ServiceModel.Activities.WorkflowServiceHost>.</span></span>  
  
 <span data-ttu-id="97b27-111">包含的範例端點會公開合約，以提供作業來建立工作流程，以及傳回執行個體識別碼或建立具有特定識別碼的執行個體。</span><span class="sxs-lookup"><span data-stu-id="97b27-111">The sample endpoint that is included exposes a contract that provides operations to create a workflow and returns the instance ID or creates an instance with a specific ID.</span></span> <span data-ttu-id="97b27-112">範例主控台應用程式會建立具有工作流程定義的 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 執行個體，並將 `CreationEndpoint` 加入至主機。</span><span class="sxs-lookup"><span data-stu-id="97b27-112">The sample console application creates a <xref:System.ServiceModel.Activities.WorkflowServiceHost> instance with a workflow definition and adds a `CreationEndpoint` to the host.</span></span> <span data-ttu-id="97b27-113">接著會在端點上呼叫 `Create` 作業，以建立新的工作流程執行個體。</span><span class="sxs-lookup"><span data-stu-id="97b27-113">It then calls the `Create` operation on the endpoint to create a new workflow instance.</span></span>  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="97b27-114">若要安裝、建置及執行範例</span><span class="sxs-lookup"><span data-stu-id="97b27-114">To set up, build, and run the sample</span></span>  
  
1. <span data-ttu-id="97b27-115">建置方案。</span><span class="sxs-lookup"><span data-stu-id="97b27-115">Build the solution.</span></span>  
  
2. <span data-ttu-id="97b27-116">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="97b27-116">Run the application.</span></span> <span data-ttu-id="97b27-117">建立工作流程執行個體之後，`CreationEndpoint` 主控台會顯示包含執行個體識別碼的訊息。</span><span class="sxs-lookup"><span data-stu-id="97b27-117">The `CreationEndpoint` console shows a message that includes the instance ID when the workflow instance is created.</span></span> <span data-ttu-id="97b27-118">"Hello World！" 訊息</span><span class="sxs-lookup"><span data-stu-id="97b27-118">The message "Hello World!"</span></span> <span data-ttu-id="97b27-119">由工作流程實例列印。</span><span class="sxs-lookup"><span data-stu-id="97b27-119">is printed by the workflow instance.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="97b27-120">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="97b27-120">The samples may already be installed on your machine.</span></span> <span data-ttu-id="97b27-121">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="97b27-121">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="97b27-122">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="97b27-122">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="97b27-123">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="97b27-123">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Execution\CreationEndpoint`
