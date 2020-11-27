---
title: 使用活動類別撰寫工作流程活動
ms.date: 03/30/2017
ms.assetid: 7b7b1c66-f093-43c3-b4d1-7173b46516da
ms.openlocfilehash: 21f1c8b1249d41029fa7a19360e96ad866c823a7
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293841"
---
# <a name="workflow-activity-authoring-using-the-activity-class"></a><span data-ttu-id="a1f3c-102">使用活動類別撰寫工作流程活動</span><span class="sxs-lookup"><span data-stu-id="a1f3c-102">Workflow Activity Authoring Using the Activity Class</span></span>

<span data-ttu-id="a1f3c-103">使用 Windows Workflow Foundation (WF) 建立活動的最基本方式， [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] 就是建立一個繼承自的類別，該類別會從 <xref:System.Activities.Activity> [內建活動程式庫](net-framework-4-5-built-in-activity-library.md)組合自訂活動或活動，以建立功能。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-103">The most basic way to create an activity using Windows Workflow Foundation (WF) in [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] is to create a class that inherits from <xref:System.Activities.Activity> that creates functionality by assembling custom activities or activities from the [Built-In Activity Library](net-framework-4-5-built-in-activity-library.md).</span></span> <span data-ttu-id="a1f3c-104">本主題示範如何建立會寫入兩個訊息至主控台的活動。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-104">This topic demonstrates how to create an activity that writes two messages to the console.</span></span>

### <a name="to-create-a-custom-activity-using-the-activity-designer"></a><span data-ttu-id="a1f3c-105">若要使用活動設計工具建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="a1f3c-105">To create a custom Activity using the activity designer</span></span>

1. <span data-ttu-id="a1f3c-106">開啟 Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-106">Open Visual Studio 2012.</span></span>

2. <span data-ttu-id="a1f3c-107">依序選取 [檔案]、[新增]、[專案]。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-107">Select File, New, Project.</span></span> <span data-ttu-id="a1f3c-108">在 [**專案類型**] 視窗中選取 [ **Visual c #** ] 底下的 **工作流程 4.0** ，然後選取 [ **v2010]** ] 節點。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-108">Select **Workflow 4.0** under **Visual C#** in the **Project Types** window, and select the **v2010** node.</span></span> <span data-ttu-id="a1f3c-109">選取 [**範本**] 視窗中的 [**活動程式庫**]。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-109">Select **Activity Library** in the **Templates** window.</span></span> <span data-ttu-id="a1f3c-110">將新專案命名為 HelloActivity。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-110">Name the new project HelloActivity.</span></span>

3. <span data-ttu-id="a1f3c-111">開啟新活動。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-111">Open the new activity.</span></span>  <span data-ttu-id="a1f3c-112">將 <xref:System.Activities.Statements.Sequence> 活動從工具箱拖曳至設計工具介面上。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-112">Drag a <xref:System.Activities.Statements.Sequence> activity from the toolbox onto the designer surface.</span></span>

4. <span data-ttu-id="a1f3c-113">將 <xref:System.Activities.Statements.WriteLine> 活動拖曳至 <xref:System.Activities.Statements.Sequence> 活動中。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-113">Drag a <xref:System.Activities.Statements.WriteLine> activity into the <xref:System.Activities.Statements.Sequence> activity.</span></span> <span data-ttu-id="a1f3c-114">`"Hello World"`在 [**文字**] 欄位中輸入具有引號的 () 。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-114">Enter `"Hello World"` (with quotes) into the **Text** field.</span></span>

5. <span data-ttu-id="a1f3c-115">將第二個 <xref:System.Activities.Statements.WriteLine> 活動拖曳至 <xref:System.Activities.Statements.Sequence> 活動，放在第一個活動下方。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-115">Drag a second <xref:System.Activities.Statements.WriteLine> activity into the <xref:System.Activities.Statements.Sequence> activity, below the first one.</span></span> <span data-ttu-id="a1f3c-116">`"Goodbye"`在 [**文字**] 欄位中輸入具有引號的 () 。</span><span class="sxs-lookup"><span data-stu-id="a1f3c-116">Enter `"Goodbye"` (with quotes) into the **Text** field.</span></span>
