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
# <a name="bookmark-resolver-for-workflowhostingendpoint"></a>WorkflowHostingEndpoint 的書籤解析程式

這個範例示範 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 如何與 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 搭配使用以建立工作流程執行個體。  
  
## <a name="demonstrates"></a>示範  

 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>, <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
## <a name="discussion"></a>討論  

 這個範例使用 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 來建立以 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 裝載的工作流程執行個體。 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> 是 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的擴充點，可用於以下情形：  
  
- 建立新的工作流程執行個體。  
  
- 在裝載於 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的工作流程執行個體中繼續使用書籤。  
  
 包含的範例端點會公開合約，以提供作業來建立工作流程，以及傳回執行個體識別碼或建立具有特定識別碼的執行個體。 範例主控台應用程式會建立具有工作流程定義的 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 執行個體，並將 `CreationEndpoint` 加入至主機。 接著會在端點上呼叫 `Create` 作業，以建立新的工作流程執行個體。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 建置方案。  
  
2. 執行應用程式。 建立工作流程執行個體之後，`CreationEndpoint` 主控台會顯示包含執行個體識別碼的訊息。 "Hello World！" 訊息 由工作流程實例列印。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Execution\CreationEndpoint`
