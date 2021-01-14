---
title: 作法：建立工作流程
description: 完成本節中的三個選項之一，以建立工作流程作為此 Workflow Foundation 教學課程的一部分。
ms.date: 03/30/2017
ms.assetid: 87234108-8e21-4cb3-9340-4a1a13f3f98c
ms.openlocfilehash: ea9fd023ba15ae23a10f5b8cf6f82c49ca9af6c8
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98190438"
---
# <a name="how-to-create-a-workflow"></a><span data-ttu-id="70a2f-103">作法：建立工作流程</span><span class="sxs-lookup"><span data-stu-id="70a2f-103">How to: Create a Workflow</span></span>

<span data-ttu-id="70a2f-104">工作流程可以從內建活動建構，也可以從自訂活動建構。</span><span class="sxs-lookup"><span data-stu-id="70a2f-104">Workflows can be constructed from built-in activities as well as from custom activities.</span></span> <span data-ttu-id="70a2f-105">本節中的主題將逐步解說如何建立工作流程，以使用活動等內建活動 <xref:System.Activities.Statements.Flowchart> ，以及先前的 how [To：建立活動](how-to-create-an-activity.md) 主題的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="70a2f-105">The topics in this section step through creating a workflow that uses both built-in activities such as the <xref:System.Activities.Statements.Flowchart> activity, and the custom activities from the previous [How to: Create an Activity](how-to-create-an-activity.md) topic.</span></span> <span data-ttu-id="70a2f-106">此工作流程會以數字猜測遊戲為模型。</span><span class="sxs-lookup"><span data-stu-id="70a2f-106">The workflow models a number guessing game.</span></span> <span data-ttu-id="70a2f-107">只要閱讀本節其中一個主題即可完成教學課程；請選擇您感興趣的樣式並依照該步驟進行。</span><span class="sxs-lookup"><span data-stu-id="70a2f-107">Only one of the topics in this section is required to complete the tutorial; you should pick the style that interests you and follow that step.</span></span> <span data-ttu-id="70a2f-108">但是，您也可以完成所有的主題。</span><span class="sxs-lookup"><span data-stu-id="70a2f-108">However, you may complete all of the topics if desired.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="70a2f-109">「快速入門」教學課程中的每個主題都與之前的主題息息相關。</span><span class="sxs-lookup"><span data-stu-id="70a2f-109">Each topic in the Getting Started tutorial depends on the previous topics.</span></span> <span data-ttu-id="70a2f-110">若要完成本主題，您必須先完成 [如何：建立活動](how-to-create-an-activity.md)。</span><span class="sxs-lookup"><span data-stu-id="70a2f-110">To complete this topic, you must first complete [How to: Create an Activity](how-to-create-an-activity.md).</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="70a2f-111">本節內容</span><span class="sxs-lookup"><span data-stu-id="70a2f-111">In This Section</span></span>  

 [<span data-ttu-id="70a2f-112">作法：建立循序工作流程</span><span class="sxs-lookup"><span data-stu-id="70a2f-112">How to: Create a Sequential Workflow</span></span>](how-to-create-a-sequential-workflow.md)  
 <span data-ttu-id="70a2f-113">說明如何使用 <xref:System.Activities.Statements.Sequence> 活動建立循序工作流程。</span><span class="sxs-lookup"><span data-stu-id="70a2f-113">Describes how to create a sequential workflow using the <xref:System.Activities.Statements.Sequence> activity.</span></span>  
  
 [<span data-ttu-id="70a2f-114">作法：建立流程圖工作流程</span><span class="sxs-lookup"><span data-stu-id="70a2f-114">How to: Create a Flowchart Workflow</span></span>](how-to-create-a-flowchart-workflow.md)  
 <span data-ttu-id="70a2f-115">說明如何使用 <xref:System.Activities.Statements.Flowchart> 活動建立流程圖工作流程。</span><span class="sxs-lookup"><span data-stu-id="70a2f-115">Describes how to create a flowchart workflow using the <xref:System.Activities.Statements.Flowchart> activity.</span></span>  
  
 [<span data-ttu-id="70a2f-116">作法：建立狀態機器工作流程</span><span class="sxs-lookup"><span data-stu-id="70a2f-116">How to: Create a State Machine Workflow</span></span>](how-to-create-a-state-machine-workflow.md)  
 <span data-ttu-id="70a2f-117">說明如何使用 <xref:System.Activities.Statements.StateMachine> 活動建立狀態電腦工作流程。</span><span class="sxs-lookup"><span data-stu-id="70a2f-117">Describes how to create a state machine workflow using the <xref:System.Activities.Statements.StateMachine> activity.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="70a2f-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="70a2f-118">See also</span></span>

- [<span data-ttu-id="70a2f-119">Windows Workflow Foundation 程式設計</span><span class="sxs-lookup"><span data-stu-id="70a2f-119">Windows Workflow Foundation Programming</span></span>](programming.md)
