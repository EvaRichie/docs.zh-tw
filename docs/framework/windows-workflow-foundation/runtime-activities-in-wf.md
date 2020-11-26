---
title: WF 中的執行階段活動
ms.date: 03/30/2017
ms.assetid: e5ae8c31-19bc-4655-88b3-6b75cd6a1bd5
ms.openlocfilehash: b0472c669d69d9397843a004bee1bb2c15e139c4
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96245692"
---
# <a name="runtime-activities-in-wf"></a><span data-ttu-id="6867f-102">WF 中的執行階段活動</span><span class="sxs-lookup"><span data-stu-id="6867f-102">Runtime Activities in WF</span></span>

[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] <span data-ttu-id="6867f-103">提供幾種系統供應的活動以存取工作流程執行階段的功能，例如持續性和終止。</span><span class="sxs-lookup"><span data-stu-id="6867f-103">provides several system-provided activities for accessing the features of the workflow runtime, such as persistence and termination.</span></span>  
  
|<span data-ttu-id="6867f-104">活動</span><span class="sxs-lookup"><span data-stu-id="6867f-104">Activity</span></span>|<span data-ttu-id="6867f-105">描述</span><span class="sxs-lookup"><span data-stu-id="6867f-105">Description</span></span>|  
|--------------|-----------------|  
|<xref:System.Activities.Statements.Persist>|<span data-ttu-id="6867f-106">明確要求工作流程保存其狀態。</span><span class="sxs-lookup"><span data-stu-id="6867f-106">Explicitly requests that the workflow persist its state.</span></span>|  
|<xref:System.Activities.Statements.TerminateWorkflow>|<span data-ttu-id="6867f-107">終止執行中的工作流程執行個體。</span><span class="sxs-lookup"><span data-stu-id="6867f-107">Terminates the running workflow instance.</span></span>|  
|<xref:System.Activities.Statements.NoPersistScope>|<span data-ttu-id="6867f-108">會防止任何子活動保存的容器活動。</span><span class="sxs-lookup"><span data-stu-id="6867f-108">A container activity that prevents child activities from persisting.</span></span>|
