---
title: WF 中的狀態機器活動
ms.date: 03/30/2017
ms.assetid: 93312eaf-07e0-4a55-b4f7-4cdbbc4dee2d
ms.openlocfilehash: dd0bfae1f24ecd9f98c0a2f04265581f880202a7
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96261718"
---
# <a name="state-machine-activities-in-wf"></a><span data-ttu-id="5f1c8-102">WF 中的狀態機器活動</span><span class="sxs-lookup"><span data-stu-id="5f1c8-102">State Machine Activities in WF</span></span>

<span data-ttu-id="5f1c8-103">.NET Framework 4.5 提供數種系統提供的活動和活動設計工具，可用來建立狀態機器工作流程。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-103">.NET Framework 4.5 provides several system-provided activities and activity designers for creating state machine workflows.</span></span>  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.StateMachine>|<span data-ttu-id="5f1c8-104">使用熟悉的狀態機器範例來執行包含的活動。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-104">Executes contained activities using the familiar state machine paradigm.</span></span>|  
|<xref:System.Activities.Statements.State>|<span data-ttu-id="5f1c8-105">代表狀態機器中的狀態。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-105">Represents a state in a state machine.</span></span>|  
|<xref:System.Activities.Core.Presentation.FinalState>|<span data-ttu-id="5f1c8-106">表示狀態機器中的終止狀態。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-106">Represents a terminating state in a state machine.</span></span> <span data-ttu-id="5f1c8-107"><xref:System.Activities.Core.Presentation.FinalState> 是活動設計工具，使用時會建立預先設定為終止狀態的 <xref:System.Activities.Statements.State>。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-107"><xref:System.Activities.Core.Presentation.FinalState> is an activity designer that when used creates a <xref:System.Activities.Statements.State> preconfigured as a terminating state.</span></span> <span data-ttu-id="5f1c8-108">如需詳細資訊，請參閱 [FinalState 活動設計](/visualstudio/workflow-designer/finalstate-activity-designer)工具。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-108">For more information, see [FinalState Activity Designer](/visualstudio/workflow-designer/finalstate-activity-designer).</span></span>|  
|<xref:System.Activities.Statements.Transition>|<span data-ttu-id="5f1c8-109">表示在兩個狀態之間轉換。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-109">Represents the transition between two states.</span></span> <span data-ttu-id="5f1c8-110">沒有的 [ **工具箱** ] 專案 <xref:System.Activities.Statements.Transition> ; 您可以在工作流程設計工具上，藉由在兩個狀態之間拖放線條來建立轉換，或在某個狀態停留在另一個狀態時，將狀態放置在出現的三角形上。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-110">There is no **Toolbox** item for <xref:System.Activities.Statements.Transition>; transitions are created on the workflow designer by dragging and dropping a line between two states, or by dropping a state on the triangles that appear when one state is hovered over another.</span></span> <span data-ttu-id="5f1c8-111">如需詳細資訊，請參閱 [轉換活動設計](/visualstudio/workflow-designer/transition-activity-designer)工具。</span><span class="sxs-lookup"><span data-stu-id="5f1c8-111">For more information, see [Transition Activity Designer](/visualstudio/workflow-designer/transition-activity-designer).</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="5f1c8-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5f1c8-112">See also</span></span>

- [<span data-ttu-id="5f1c8-113">快速入門教學課程</span><span class="sxs-lookup"><span data-stu-id="5f1c8-113">Getting Started Tutorial</span></span>](getting-started-tutorial.md)
