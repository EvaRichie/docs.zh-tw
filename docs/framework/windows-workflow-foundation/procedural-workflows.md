---
title: 程序性工作流程
description: 在 Workflow Foundation 中，程式工作流程會使用類似于程式語言中的流程式控制制方法。
ms.date: 03/30/2017
ms.assetid: 52401de9-9115-472d-8fd9-047af6a072b9
ms.openlocfilehash: 97664c1352928e7d05c2ed15fc118dd21474cfc3
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421432"
---
# <a name="procedural-workflows"></a><span data-ttu-id="38f4b-103">程序性工作流程</span><span class="sxs-lookup"><span data-stu-id="38f4b-103">Procedural Workflows</span></span>
<span data-ttu-id="38f4b-104">程序式工作流程使用的流程控制方法類似於程序式語言中的流程控制方法。</span><span class="sxs-lookup"><span data-stu-id="38f4b-104">Procedural workflows use flow-control methods similar to those found in procedural languages.</span></span> <span data-ttu-id="38f4b-105">這些建構包括 `While` 和 `If`。</span><span class="sxs-lookup"><span data-stu-id="38f4b-105">These constructs include `While` and `If`.</span></span> <span data-ttu-id="38f4b-106">使用其他流程控制活動 (例如 <xref:System.Activities.Statements.Flowchart> 和 <xref:System.Activities.Statements.Sequence>) 即可自由撰寫這些工作流程。</span><span class="sxs-lookup"><span data-stu-id="38f4b-106">These workflows can be freely composed using other flow control activities such as <xref:System.Activities.Statements.Flowchart> and <xref:System.Activities.Statements.Sequence>.</span></span>  
  
## <a name="controlling-execution-flow"></a><span data-ttu-id="38f4b-107">控制執行流程</span><span class="sxs-lookup"><span data-stu-id="38f4b-107">Controlling Execution Flow</span></span>  
 <span data-ttu-id="38f4b-108">工作流程活動程式庫具有程序式語言中用於建立大多數流程控制方法之模型的活動，</span><span class="sxs-lookup"><span data-stu-id="38f4b-108">The workflow activity library has activities for modeling most flow-control methods used in procedural languages.</span></span> <span data-ttu-id="38f4b-109">這些包括：</span><span class="sxs-lookup"><span data-stu-id="38f4b-109">These include:</span></span>  
  
- <xref:System.Activities.Statements.While>  
  
- <xref:System.Activities.Statements.DoWhile>  
  
- <xref:System.Activities.Statements.ForEach%601>  
  
- <xref:System.Activities.Statements.Parallel>  
  
- <xref:System.Activities.Statements.ParallelForEach%601>  
  
- <xref:System.Activities.Statements.If>  
  
- <xref:System.Activities.Statements.Switch%601>  
  
- <xref:System.Activities.Statements.Pick>  
  
 <span data-ttu-id="38f4b-110">若要使用流程式控制制活動，請將其從 [**活動**] 工具箱拖放至設計工具視窗中的複合活動。</span><span class="sxs-lookup"><span data-stu-id="38f4b-110">To use flow control activities, drag and drop them from the **Activity** toolbox into a composite activity inside the designer window.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="38f4b-111">如果使用 Windows Server AppFabric 的裝載功能來裝載 Web 伺服陣列上的工作流程，AppFabric 會在不同的 AppFabric 伺服器之間移動實例。</span><span class="sxs-lookup"><span data-stu-id="38f4b-111">If using the hosting features of Windows Server AppFabric to host workflows on a Web farm, AppFabric will move instances between different AppFabric servers.</span></span> <span data-ttu-id="38f4b-112">所有節點必須能夠共用資源，才能這麼做。</span><span class="sxs-lookup"><span data-stu-id="38f4b-112">This requires that the resources are able to be shared between all nodes.</span></span>  <span data-ttu-id="38f4b-113">所有預設的 NET 4 工作流程活動皆不包含任何存取本機資源的作業。</span><span class="sxs-lookup"><span data-stu-id="38f4b-113">None of the default NET 4 workflow activities contain any operations that access local resources.</span></span> <span data-ttu-id="38f4b-114">由於 AppFabric 沒有提供任何機制可將工作流程標記為不可移動，因此開發人員不得建立會在工作流程移動時失敗的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="38f4b-114">Since AppFabric does not offer any mechanism to mark a workflow as immovable, a developer must not create custom activities that fail when a workflow is moved.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="38f4b-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="38f4b-115">See also</span></span>

- [<span data-ttu-id="38f4b-116">流程圖工作流程</span><span class="sxs-lookup"><span data-stu-id="38f4b-116">Flowchart Workflows</span></span>](flowchart-workflows.md)
