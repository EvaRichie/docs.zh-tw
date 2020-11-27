---
title: 使用自訂活動設計工具中的 ExpressionTextBox
ms.date: 03/30/2017
ms.assetid: f82e73e7-a256-4a4d-82b7-c0d62f4ab5e7
ms.openlocfilehash: dfb53096be59abd9924a024880d4125ca774d4b8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96267479"
---
# <a name="using-the-expressiontextbox-in-a-custom-activity-designer"></a><span data-ttu-id="a5660-102">使用自訂活動設計工具中的 ExpressionTextBox</span><span class="sxs-lookup"><span data-stu-id="a5660-102">Using the ExpressionTextBox in a Custom Activity Designer</span></span>

<span data-ttu-id="a5660-103">這個範例示範如何在自訂活動設計工具內使用 <xref:System.Activities.Presentation.View.ExpressionTextBox>。</span><span class="sxs-lookup"><span data-stu-id="a5660-103">This sample shows how to use the <xref:System.Activities.Presentation.View.ExpressionTextBox> in a custom activity designer.</span></span> <span data-ttu-id="a5660-104">自訂活動 `MultiAssign` 會將兩個字串值指派給兩個字串變數。</span><span class="sxs-lookup"><span data-stu-id="a5660-104">The custom activity, `MultiAssign`, assigns two string values to two string variables.</span></span> <span data-ttu-id="a5660-105">某些 <xref:System.Activities.Presentation.View.ExpressionTextBox> 控制項會繫結至 <xref:System.Activities.InArgument>，而某些則繫結至 <xref:System.Activities.OutArgument>。</span><span class="sxs-lookup"><span data-stu-id="a5660-105">Some <xref:System.Activities.Presentation.View.ExpressionTextBox> controls bind to <xref:System.Activities.InArgument>s and some bind to <xref:System.Activities.OutArgument>s.</span></span>

## <a name="sample-details"></a><span data-ttu-id="a5660-106">範例詳細資料</span><span class="sxs-lookup"><span data-stu-id="a5660-106">Sample details</span></span>

 <span data-ttu-id="a5660-107">`ArgumentToExpressionConverter` 是將運算式繫結至引數時所使用的型別轉換子。</span><span class="sxs-lookup"><span data-stu-id="a5660-107">The `ArgumentToExpressionConverter` is the type converter used when binding expressions to arguments.</span></span> <span data-ttu-id="a5660-108">`ConverterParameter` 必須適當地設定為 `In` 或 `Out`。</span><span class="sxs-lookup"><span data-stu-id="a5660-108">The `ConverterParameter` must be set to `In` or `Out` as appropriate.</span></span> <span data-ttu-id="a5660-109">不支援 `InOut`。</span><span class="sxs-lookup"><span data-stu-id="a5660-109">`InOut` is not supported.</span></span>

 <span data-ttu-id="a5660-110">在 `UseLocationExpression` 上使用屬性 `OutArgument` 來指定運算式應該是左值 ( 「左值」或「位置值」 ) 運算式。</span><span class="sxs-lookup"><span data-stu-id="a5660-110">The `UseLocationExpression` attribute is used on `OutArgument`s to specify that the expression should be an L-value ("left value" or "location value") expression.</span></span> <span data-ttu-id="a5660-111">在大多數情況下，L-value 運算式是有效的 Visual Basic 識別碼，用來指出傳回的 `OutArgument` 為變數或引數名稱。</span><span class="sxs-lookup"><span data-stu-id="a5660-111">In most cases, an L-value expression is a valid Visual Basic identifier used to indicate that the `OutArgument` being returned is a variable or argument name.</span></span>

 <span data-ttu-id="a5660-112">在這個範例中，`MaxLines` 屬性設定為一，而且未設定 `MinLines`。</span><span class="sxs-lookup"><span data-stu-id="a5660-112">The `MaxLines` attribute is set to one in this example and `MinLines` is not set.</span></span> <span data-ttu-id="a5660-113">這表示 <xref:System.Activities.Presentation.View.ExpressionTextBox> 的固定大小為一行，不論使用者輸入多少的文字數量。</span><span class="sxs-lookup"><span data-stu-id="a5660-113">This indicates that the <xref:System.Activities.Presentation.View.ExpressionTextBox> is a fixed size of one line regardless of the amount of text typed by the user.</span></span> <span data-ttu-id="a5660-114">若要允許 <xref:System.Activities.Presentation.View.ExpressionTextBox> 成長來符合使用者輸入，請將 `MaxLines` 設定為大於 `MinLines`。</span><span class="sxs-lookup"><span data-stu-id="a5660-114">To allow the <xref:System.Activities.Presentation.View.ExpressionTextBox> to grow to fit user input, set `MaxLines` greater than `MinLines`.</span></span>

 <span data-ttu-id="a5660-115">ExpressionTextBox 只能繫結至引數，無法繫結至 CLR 屬性。</span><span class="sxs-lookup"><span data-stu-id="a5660-115">An ExpressionTextBox can only be bound to arguments, and cannot be bound to CLR properties.</span></span>

#### <a name="to-use-this-sample"></a><span data-ttu-id="a5660-116">若要使用這個範例</span><span class="sxs-lookup"><span data-stu-id="a5660-116">To use this sample</span></span>

1. <span data-ttu-id="a5660-117">使用 Visual Studio 2010 開啟 ExpressionTextBoxSample .sln 檔案。</span><span class="sxs-lookup"><span data-stu-id="a5660-117">Using Visual Studio 2010, open the ExpressionTextBoxSample.sln file.</span></span>

2. <span data-ttu-id="a5660-118">若要建置此方案，請按 CTRL+SHIFT+B。</span><span class="sxs-lookup"><span data-stu-id="a5660-118">To build the solution, press CTRL+SHIFT+B.</span></span>

#### <a name="to-run-this-sample"></a><span data-ttu-id="a5660-119">執行此範例</span><span class="sxs-lookup"><span data-stu-id="a5660-119">To run this sample</span></span>

1. <span data-ttu-id="a5660-120">將新的工作流程主控台應用程式加入至方案。</span><span class="sxs-lookup"><span data-stu-id="a5660-120">Add a new Workflow Console Application to the solution.</span></span>

2. <span data-ttu-id="a5660-121">從新的工作流程主控台應用程式專案加入 **ExpressionTextBoxSample** 專案的參考。</span><span class="sxs-lookup"><span data-stu-id="a5660-121">Add a reference to the **ExpressionTextBoxSample** project from the new Workflow Console Application project.</span></span>

3. <span data-ttu-id="a5660-122">建置方案。</span><span class="sxs-lookup"><span data-stu-id="a5660-122">Build the solution.</span></span>

4. <span data-ttu-id="a5660-123">從 [工具箱] 將 [ **MultiAssign** ] 活動拖放到工作流程中。</span><span class="sxs-lookup"><span data-stu-id="a5660-123">Drag the **MultiAssign** activity from the toolbox and drop it into the workflow.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5660-124">這些範例可能已安裝在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="a5660-124">The samples may already be installed on your machine.</span></span> <span data-ttu-id="a5660-125">請先檢查下列 (預設) 目錄，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="a5660-125">Check for the following (default) directory before continuing.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> <span data-ttu-id="a5660-126">如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。</span><span class="sxs-lookup"><span data-stu-id="a5660-126">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) to download all Windows Communication Foundation (WCF) and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="a5660-127">此範例位於下列目錄。</span><span class="sxs-lookup"><span data-stu-id="a5660-127">This sample is located in the following directory.</span></span>  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\ExpressionTextBox`  
  
## <a name="see-also"></a><span data-ttu-id="a5660-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a5660-128">See also</span></span>

- <xref:System.Activities.Presentation.View.ExpressionTextBox>
- [<span data-ttu-id="a5660-129">使用工作流程設計工具開發應用程式</span><span class="sxs-lookup"><span data-stu-id="a5660-129">Developing Applications with the Workflow Designer</span></span>](/visualstudio/workflow-designer/developing-applications-with-the-workflow-designer)
