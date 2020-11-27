---
title: 使用命令式程式碼撰寫工作流程、活動和運算式
description: Workflow Foundation 工作流程定義是已設定之活動物件的樹狀結構。 使用程式碼建立工作流程定義、活動和運算式。
ms.date: 03/30/2017
ms.assetid: cefc9cfc-2882-4eb9-8c94-7a6da957f2b2
ms.openlocfilehash: 5355f2090317a0bce3fec0f46550b202bd0af095
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96289122"
---
# <a name="authoring-workflows-activities-and-expressions-using-imperative-code"></a><span data-ttu-id="96e84-104">使用命令式程式碼撰寫工作流程、活動和運算式</span><span class="sxs-lookup"><span data-stu-id="96e84-104">Authoring Workflows, Activities, and Expressions Using Imperative Code</span></span>

<span data-ttu-id="96e84-105">工作流程定義是配置之活動物件的樹狀。</span><span class="sxs-lookup"><span data-stu-id="96e84-105">A workflow definition is a tree of configured activity objects.</span></span> <span data-ttu-id="96e84-106">有很多方式可定義這個活動的樹狀結構，包含手動編輯 XAML 或使用工作流程設計工具來產生 XAML。</span><span class="sxs-lookup"><span data-stu-id="96e84-106">This tree of activities can be defined many ways, including by hand-editing XAML or by using the Workflow Designer to produce XAML.</span></span> <span data-ttu-id="96e84-107">不過，XAML 並非必要條件。</span><span class="sxs-lookup"><span data-stu-id="96e84-107">Use of XAML, however, is not a requirement.</span></span> <span data-ttu-id="96e84-108">您也可以程式設計的方式建立工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="96e84-108">Workflow definitions can also be created programmatically.</span></span> <span data-ttu-id="96e84-109">本主題提供使用程式碼來建立工作流程定義、活動和運算式的概觀。</span><span class="sxs-lookup"><span data-stu-id="96e84-109">This topic provides an overview of creating workflow definitions, activities, and expressions by using code.</span></span> <span data-ttu-id="96e84-110">如需使用程式碼來處理 XAML 工作流程的範例，請參閱 [將工作流程和活動與 xaml 進行](serializing-workflows-and-activities-to-and-from-xaml.md)序列化。</span><span class="sxs-lookup"><span data-stu-id="96e84-110">For examples of working with XAML workflows using code, see [Serializing Workflows and Activities to and from XAML](serializing-workflows-and-activities-to-and-from-xaml.md).</span></span>  
  
## <a name="creating-workflow-definitions"></a><span data-ttu-id="96e84-111">建立工作流程定義</span><span class="sxs-lookup"><span data-stu-id="96e84-111">Creating Workflow Definitions</span></span>  

 <span data-ttu-id="96e84-112">具現化活動型別的執行個體，並設定活動物件的屬性，即可建立工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="96e84-112">A workflow definition can be created by instantiating an instance of an activity type and configuring the activity object’s properties.</span></span> <span data-ttu-id="96e84-113">對於不包含任何子活動的活動，這個部分僅需使用幾行程式碼便能完成。</span><span class="sxs-lookup"><span data-stu-id="96e84-113">For activities that do not contain child activities, this can be accomplished using a few lines of code.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#47](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#47)]  
  
> [!NOTE]
> <span data-ttu-id="96e84-114">本主題中的範例使用 <xref:System.Activities.WorkflowInvoker> 來執行範例工作流程。</span><span class="sxs-lookup"><span data-stu-id="96e84-114">The examples in this topic use <xref:System.Activities.WorkflowInvoker> to run the sample workflows.</span></span> <span data-ttu-id="96e84-115">如需叫用工作流程、傳遞引數，以及可用的不同裝載選項的詳細資訊，請參閱 [使用 WorkflowInvoker 和 WorkflowApplication](using-workflowinvoker-and-workflowapplication.md)。</span><span class="sxs-lookup"><span data-stu-id="96e84-115">For more information about invoking workflows, passing arguments, and the different hosting choices that are available, see [Using WorkflowInvoker and WorkflowApplication](using-workflowinvoker-and-workflowapplication.md).</span></span>  
  
 <span data-ttu-id="96e84-116">在這個範例中，會建立由單一 <xref:System.Activities.Statements.WriteLine> 活動構成的工作流程。</span><span class="sxs-lookup"><span data-stu-id="96e84-116">In this example, a workflow that consists of a single <xref:System.Activities.Statements.WriteLine> activity is created.</span></span> <span data-ttu-id="96e84-117"><xref:System.Activities.Statements.WriteLine> 活動的 <xref:System.Activities.Statements.WriteLine.Text%2A> 引數會進行設定，並叫用工作流程。</span><span class="sxs-lookup"><span data-stu-id="96e84-117">The <xref:System.Activities.Statements.WriteLine> activity’s <xref:System.Activities.Statements.WriteLine.Text%2A> argument is set, and the workflow is invoked.</span></span> <span data-ttu-id="96e84-118">如果活動包含子活動，則建構方式會相當類似。</span><span class="sxs-lookup"><span data-stu-id="96e84-118">If an activity contains child activities, the method of construction is similar.</span></span> <span data-ttu-id="96e84-119">下列範例會使用包含兩個 <xref:System.Activities.Statements.Sequence> 活動的 <xref:System.Activities.Statements.WriteLine> 活動。</span><span class="sxs-lookup"><span data-stu-id="96e84-119">The following example uses a <xref:System.Activities.Statements.Sequence> activity that contains two <xref:System.Activities.Statements.WriteLine> activities.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#48](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#48)]  
  
### <a name="using-object-initializers"></a><span data-ttu-id="96e84-120">使用物件初始設定式</span><span class="sxs-lookup"><span data-stu-id="96e84-120">Using Object Initializers</span></span>  

 <span data-ttu-id="96e84-121">本主題的範例會使用物件初始化語法。</span><span class="sxs-lookup"><span data-stu-id="96e84-121">The examples in this topic use object initialization syntax.</span></span> <span data-ttu-id="96e84-122">物件初始化語法在使用程式碼建立工作流程定義時會很有用，因為它會在工作流程中提供活動的階層式檢視，並顯示活動之間的關係。</span><span class="sxs-lookup"><span data-stu-id="96e84-122">Object initialization syntax can be a useful way to create workflow definitions in code because it provides a hierarchical view of the activities in the workflow and shows the relationship between the activities.</span></span> <span data-ttu-id="96e84-123">當您以程式設計方式來建立工作流程時，不一定非得使用物件初始化語法。</span><span class="sxs-lookup"><span data-stu-id="96e84-123">There is no requirement to use object initialization syntax when you programmatically create workflows.</span></span> <span data-ttu-id="96e84-124">下列範例在功能上等同於先前的範例。</span><span class="sxs-lookup"><span data-stu-id="96e84-124">The following example is functionally equivalent to the previous example.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#49](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#49)]  
  
 <span data-ttu-id="96e84-125">如需物件初始化運算式的詳細資訊，請參閱 [如何：在不呼叫函式的情況下初始化物件 (c # 程式設計手冊) ](../../csharp/programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer.md) 和 how [To：使用物件初始化運算式宣告物件](../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)。</span><span class="sxs-lookup"><span data-stu-id="96e84-125">For more information about object initializers, see [How to: Initialize Objects without Calling a Constructor (C# Programming Guide)](../../csharp/programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer.md) and [How to: Declare an Object by Using an Object Initializer](../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md).</span></span>  
  
### <a name="working-with-variables-literal-values-and-expressions"></a><span data-ttu-id="96e84-126">處理變數、常值和運算式</span><span class="sxs-lookup"><span data-stu-id="96e84-126">Working with Variables, Literal Values, and Expressions</span></span>  

 <span data-ttu-id="96e84-127">使用程式碼建立工作流程定義時，請注意哪個程式碼是做為建立工作流程定義的一部分，以及哪個程式碼是做為該工作流程執行個體的一部分執行。</span><span class="sxs-lookup"><span data-stu-id="96e84-127">When creating a workflow definition using code, be aware of what code executes as part of the creation of the workflow definition and what code executes as part of the execution of an instance of that workflow.</span></span> <span data-ttu-id="96e84-128">例如，下列工作流程目的是要產生隨機號碼，並將它寫入主控台。</span><span class="sxs-lookup"><span data-stu-id="96e84-128">For example, the following workflow is intended to generate a random number and write it to the console.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#50](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#50)]  
  
 <span data-ttu-id="96e84-129">當執行此工作流程定義程式碼時，會呼叫 `Random.Next`，且會將結果儲存於工作流程定義做為常值。</span><span class="sxs-lookup"><span data-stu-id="96e84-129">When this workflow definition code is executed, the call to `Random.Next` is made and the result is stored in the workflow definition as a literal value.</span></span> <span data-ttu-id="96e84-130">此工作流程的許多執行個體都可加以叫用，且所有的執行個體都會顯示相同的號碼。</span><span class="sxs-lookup"><span data-stu-id="96e84-130">Many instances of this workflow can be invoked, and all would display the same number.</span></span> <span data-ttu-id="96e84-131">若要在工作流程執行期間產生隨機號碼，必須使用每當工作流程執行時所計算的運算式。</span><span class="sxs-lookup"><span data-stu-id="96e84-131">To have the random number generation occur during workflow execution, an expression must be used that is evaluated each time the workflow runs.</span></span> <span data-ttu-id="96e84-132">在下列範例中，會將 Visual Basic 運算式與 <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="96e84-132">In the following example, a Visual Basic expression is used with a <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#51](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#51)]  
  
 <span data-ttu-id="96e84-133">前面範例中的運算式也可以使用 <xref:Microsoft.CSharp.Activities.CSharpValue%601> 和 C# 運算式實作。</span><span class="sxs-lookup"><span data-stu-id="96e84-133">The expression in the previous example could also be implemented using a <xref:Microsoft.CSharp.Activities.CSharpValue%601> and a C# expression.</span></span>  
  
```csharp  
new Assign<int>  
{  
    To = n,  
    Value = new CSharpValue<int>("new Random().Next(1, 101)")  
}  
```  
  
 <span data-ttu-id="96e84-134">C# 運算式必須先編譯，才能叫用在包含該 C# 運算式的工作流程。</span><span class="sxs-lookup"><span data-stu-id="96e84-134">C# expressions must be compiled before the workflow containing them is invoked.</span></span> <span data-ttu-id="96e84-135">如果未編譯 c # 運算式，則會在 <xref:System.NotSupportedException> 使用類似如下的訊息來叫用工作流程時擲回。 ``Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`` 在大部分情況下，會自動編譯 c # 運算式 Visual Studio 中建立的工作流程，但在某些情況下（例如程式碼工作流程），必須手動編譯 c # 運算式。</span><span class="sxs-lookup"><span data-stu-id="96e84-135">If the C# expressions are not compiled, a <xref:System.NotSupportedException> is thrown when the workflow is invoked with a message similar to the following: ``Expression Activity type 'CSharpValue`1' requires compilation in order to run.  Please ensure that the workflow has been compiled.`` In most scenarios involving workflows created in Visual Studio the C# expressions are compiled automatically, but in some scenarios, such as code workflows, the C# expressions must be manually compiled.</span></span> <span data-ttu-id="96e84-136">如需如何編譯 c # 運算式的範例，請參閱[c # 運算式](csharp-expressions.md)主題的在程式[代碼工作流程中使用 c # 運算式](csharp-expressions.md#CodeWorkflows)一節。</span><span class="sxs-lookup"><span data-stu-id="96e84-136">For an example of how to compile C# expressions, see the [Using C# expressions in code workflows](csharp-expressions.md#CodeWorkflows) section of the [C# Expressions](csharp-expressions.md) topic.</span></span>  
  
 <span data-ttu-id="96e84-137"><xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> 是以 Visual Basic 語法表示的運算式，可用來當做運算式中的右值 (r-value)，而 <xref:Microsoft.CSharp.Activities.CSharpValue%601> 是以 C# 語法表示的運算式，可用來當做運算式中的右值。</span><span class="sxs-lookup"><span data-stu-id="96e84-137">A <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> represents an expression in Visual Basic syntax that can be used as an r-value in an expression, and a <xref:Microsoft.CSharp.Activities.CSharpValue%601> represents an expression in C# syntax that can be used as an r-value in an expression.</span></span> <span data-ttu-id="96e84-138">每次執行包含的活動時會評估這些運算式。</span><span class="sxs-lookup"><span data-stu-id="96e84-138">These expressions are evaluated each time the containing activity is executed.</span></span> <span data-ttu-id="96e84-139">運算式的結果會指派至工作流程變數 `n`，且會由工作流程中的下一個活動使用這些結果。</span><span class="sxs-lookup"><span data-stu-id="96e84-139">The result of the expression is assigned to the workflow variable `n`, and these results are used by the next activity in the workflow.</span></span> <span data-ttu-id="96e84-140">若要在執行階段時存取工作流程變數 `n` 的值，必須要有 <xref:System.Activities.ActivityContext>。</span><span class="sxs-lookup"><span data-stu-id="96e84-140">To access the value of the workflow variable `n` at runtime, the <xref:System.Activities.ActivityContext> is required.</span></span> <span data-ttu-id="96e84-141">這可以使用下列 Lambda 運算式來進行存取。</span><span class="sxs-lookup"><span data-stu-id="96e84-141">This can be accessed by using the following lambda expression.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="96e84-142">請注意這兩個程式碼都是使用 C# 做為程式設計語言的範例，但一個是使用 <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>，另一個則是使用 <xref:Microsoft.CSharp.Activities.CSharpValue%601>。</span><span class="sxs-lookup"><span data-stu-id="96e84-142">Note that both of these code are examples are using C# as the programming language, but one uses a <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> and one uses a <xref:Microsoft.CSharp.Activities.CSharpValue%601>.</span></span> <span data-ttu-id="96e84-143"><xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> 和 <xref:Microsoft.CSharp.Activities.CSharpValue%601> 可以用在 Visual Basic 和 C# 專案中。</span><span class="sxs-lookup"><span data-stu-id="96e84-143"><xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> and <xref:Microsoft.CSharp.Activities.CSharpValue%601> can be used in both Visual Basic and C# projects.</span></span> <span data-ttu-id="96e84-144">根據預設，在工作流程設計工具中所建立的運算式符合裝載專案的語言。</span><span class="sxs-lookup"><span data-stu-id="96e84-144">By default, expressions created in the workflow designer match the language of the hosting project.</span></span> <span data-ttu-id="96e84-145">以程式碼建立工作流程時，由工作流程作者自行決定要使用的語言。</span><span class="sxs-lookup"><span data-stu-id="96e84-145">When creating workflows in code, the desired language is at the discretion of the workflow author.</span></span>  
  
 <span data-ttu-id="96e84-146">在這些範例中，運算式的結果會指派至工作流程變數 `n`，且會由工作流程中的下一個活動使用這些結果。</span><span class="sxs-lookup"><span data-stu-id="96e84-146">In these examples the result of the expression is assigned to the workflow variable `n`, and these results are used by the next activity in the workflow.</span></span> <span data-ttu-id="96e84-147">若要在執行階段時存取工作流程變數 `n` 的值，必須要有 <xref:System.Activities.ActivityContext>。</span><span class="sxs-lookup"><span data-stu-id="96e84-147">To access the value of the workflow variable `n` at runtime, the <xref:System.Activities.ActivityContext> is required.</span></span> <span data-ttu-id="96e84-148">這可以使用下列 Lambda 運算式來進行存取。</span><span class="sxs-lookup"><span data-stu-id="96e84-148">This can be accessed by using the following lambda expression.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#52](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#52)]  
  
 <span data-ttu-id="96e84-149">如需 lambda 運算式的詳細資訊，請參閱 [Lambda 運算式 (c # 參考) ](../../csharp/language-reference/operators/lambda-expressions.md) 或 [lambda 運算式 (Visual Basic) ](../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="96e84-149">For more information about lambda expressions, see [Lambda Expressions (C# reference)](../../csharp/language-reference/operators/lambda-expressions.md) or [Lambda Expressions (Visual Basic)](../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).</span></span>  
  
 <span data-ttu-id="96e84-150">Lambda 運算式不可序列化為 XAML 格式。</span><span class="sxs-lookup"><span data-stu-id="96e84-150">Lambda expressions are not serializable to XAML format.</span></span> <span data-ttu-id="96e84-151">如果嘗試序列化內含 Lambda 運算式的工作流程，會擲回 <xref:System.Activities.Expressions.LambdaSerializationException> 和下列訊息：「此工作流程包含程式碼中指定的 Lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="96e84-151">If an attempt to serialize a workflow with lambda expressions is made, a <xref:System.Activities.Expressions.LambdaSerializationException> is thrown with the following message: "This workflow contains lambda expressions specified in code.</span></span> <span data-ttu-id="96e84-152">這些運算式並非 XAML 可序列化。</span><span class="sxs-lookup"><span data-stu-id="96e84-152">These expressions are not XAML serializable.</span></span> <span data-ttu-id="96e84-153">若要讓您的工作流程成為 XAML 可序列化，請使用 VisualBasicValue/VisualBasicReference 或 ExpressionServices.Convert(lambda)。</span><span class="sxs-lookup"><span data-stu-id="96e84-153">In order to make your workflow XAML-serializable, either use VisualBasicValue/VisualBasicReference or ExpressionServices.Convert(lambda).</span></span> <span data-ttu-id="96e84-154">這會將您的 Lambda 運算式轉換成運算式活動。」</span><span class="sxs-lookup"><span data-stu-id="96e84-154">This will convert your lambda expressions into expression activities."</span></span> <span data-ttu-id="96e84-155">若要讓此運算式相容於 XAML，請使用 <xref:System.Activities.Expressions.ExpressionServices> 與 <xref:System.Activities.Expressions.ExpressionServices.Convert%2A>，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="96e84-155">To make this expression compatible with XAML, use <xref:System.Activities.Expressions.ExpressionServices> and <xref:System.Activities.Expressions.ExpressionServices.Convert%2A>, as shown in the following example.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#53](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#53)]  
  
 <span data-ttu-id="96e84-156">也可以使用 <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>。</span><span class="sxs-lookup"><span data-stu-id="96e84-156">A <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> could also be used.</span></span> <span data-ttu-id="96e84-157">請注意，使用 Visual Basic 運算式時，不需要 Lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="96e84-157">Note that no lambda expression is required when using a Visual Basic expression.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#54](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#54)]  
  
 <span data-ttu-id="96e84-158">Visual Basic 運算式會在執行階段編譯成 LINQ 運算式。</span><span class="sxs-lookup"><span data-stu-id="96e84-158">At run time, Visual Basic expressions are compiled into LINQ expressions.</span></span> <span data-ttu-id="96e84-159">前面兩個範例都可序列化為 XAML，但是如果已序列化的 XAML 是要在工作流程設計工具中檢視和編輯，則在運算式使用 <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>。</span><span class="sxs-lookup"><span data-stu-id="96e84-159">Both of the previous examples are serializable to XAML, but if the serialized XAML is intended to be viewed and edited in the workflow designer, use <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601> for your expressions.</span></span> <span data-ttu-id="96e84-160">使用 `ExpressionServices.Convert` 的序列化工作流程可在設計工具中開啟，但運算式的值會是空白的。</span><span class="sxs-lookup"><span data-stu-id="96e84-160">Serialized workflows that use `ExpressionServices.Convert` can be opened in the designer, but the value of the expression will be blank.</span></span> <span data-ttu-id="96e84-161">如需將工作流程序列化為 XAML 的詳細資訊，請參閱 [將工作流程和活動序列化為 xaml](serializing-workflows-and-activities-to-and-from-xaml.md)。</span><span class="sxs-lookup"><span data-stu-id="96e84-161">For more information about serializing workflows to XAML, see [Serializing Workflows and Activities to and from XAML](serializing-workflows-and-activities-to-and-from-xaml.md).</span></span>  
  
#### <a name="literal-expressions-and-reference-types"></a><span data-ttu-id="96e84-162">常值運算式及參考類型</span><span class="sxs-lookup"><span data-stu-id="96e84-162">Literal Expressions and Reference Types</span></span>  

 <span data-ttu-id="96e84-163">常值運算式在工作流程中由 <xref:System.Activities.Expressions.Literal%601> 活動表示。</span><span class="sxs-lookup"><span data-stu-id="96e84-163">Literal expressions are represented in workflows by the <xref:System.Activities.Expressions.Literal%601> activity.</span></span> <span data-ttu-id="96e84-164">下列 <xref:System.Activities.Statements.WriteLine> 活動的功能相同。</span><span class="sxs-lookup"><span data-stu-id="96e84-164">The following <xref:System.Activities.Statements.WriteLine> activities are functionally equivalent.</span></span>  
  
```csharp  
new WriteLine  
{  
    Text = "Hello World."  
},  
new WriteLine  
{  
    Text = new Literal<string>("Hello World.")  
}  
```  
  
 <span data-ttu-id="96e84-165">初始化含任何參考類型 (<xref:System.String> 除外) 的常值運算式皆無效。</span><span class="sxs-lookup"><span data-stu-id="96e84-165">It is invalid to initialize a literal expression with any reference type except <xref:System.String>.</span></span> <span data-ttu-id="96e84-166">在下列範例中，<xref:System.Activities.Statements.Assign> 活動的 <xref:System.Activities.Statements.Assign.Value%2A> 屬性是以使用 `List<string>` 的常值運算式初始化。</span><span class="sxs-lookup"><span data-stu-id="96e84-166">In the following example, an <xref:System.Activities.Statements.Assign> activity's <xref:System.Activities.Statements.Assign.Value%2A> property is initialized with a literal expression using a `List<string>`.</span></span>  
  
```csharp  
new Assign  
{  
    To = new OutArgument<List<string>>(items),  
    Value = new InArgument<List<string>>(new List<string>())  
},  
```  
  
 <span data-ttu-id="96e84-167">當驗證內含此活動的工作流程時，會傳回下列驗證錯誤：「常值只支援值型別和不可變型別 System.String。</span><span class="sxs-lookup"><span data-stu-id="96e84-167">When the workflow containing this activity is validated, the following validation error is returned: "Literal only supports value types and the immutable type System.String.</span></span> <span data-ttu-id="96e84-168">System.Collections.Generic.List\`1[System.String] 型別不能用做常值。」</span><span class="sxs-lookup"><span data-stu-id="96e84-168">The type System.Collections.Generic.List\`1[System.String] cannot be used as a literal."</span></span> <span data-ttu-id="96e84-169">如果叫用工作流程，會擲回 <xref:System.Activities.InvalidWorkflowException>，其中包含驗證錯誤的文字。</span><span class="sxs-lookup"><span data-stu-id="96e84-169">If the workflow is invoked, an <xref:System.Activities.InvalidWorkflowException> is thrown that contains the text of the validation error.</span></span> <span data-ttu-id="96e84-170">這是驗證錯誤，因為建立內含參考類型的常值運算式，並不會針對工作流程的每個執行個體建立新的參考類型執行個體。</span><span class="sxs-lookup"><span data-stu-id="96e84-170">This is a validation error because creating a literal expression with a reference type does not create a new instance of the reference type for each instance of the workflow.</span></span> <span data-ttu-id="96e84-171">若要解決此問題，請將常值運算式換成可以建立和傳回新參考類型執行個體的運算式。</span><span class="sxs-lookup"><span data-stu-id="96e84-171">To resolve this, replace the literal expression with one that creates and returns a new instance of the reference type.</span></span>  
  
```csharp  
new Assign  
{  
    To = new OutArgument<List<string>>(items),  
    Value = new InArgument<List<string>>(new VisualBasicValue<List<string>>("New List(Of String)"))  
},  
```  
  
 <span data-ttu-id="96e84-172">如需運算式的詳細資訊，請參閱 [運算式](expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="96e84-172">For more information about expressions, see [Expressions](expressions.md).</span></span>  
  
#### <a name="invoking-methods-on-objects-using-expressions-and-the-invokemethod-activity"></a><span data-ttu-id="96e84-173">在物件上使用運算式和 InvokeMethod 活動的叫用方法</span><span class="sxs-lookup"><span data-stu-id="96e84-173">Invoking Methods on Objects using Expressions and the InvokeMethod Activity</span></span>  

 <span data-ttu-id="96e84-174"><xref:System.Activities.Expressions.InvokeMethod%601> 活動可以用來在 .NET Framework 中叫用類別的靜態和執行個體方法。</span><span class="sxs-lookup"><span data-stu-id="96e84-174">The <xref:System.Activities.Expressions.InvokeMethod%601> activity can be used to invoke static and instance methods of classes in the .NET Framework.</span></span> <span data-ttu-id="96e84-175">在本主題先前的範例中，已使用 <xref:System.Random> 類別來產生隨機數字。</span><span class="sxs-lookup"><span data-stu-id="96e84-175">In a previous example in this topic, a random number was generated using the <xref:System.Random> class.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#51](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#51)]  
  
 <span data-ttu-id="96e84-176"><xref:System.Activities.Expressions.InvokeMethod%601> 活動也可以用來呼叫 <xref:System.Random.Next%2A> 類別的 <xref:System.Random> 方法。</span><span class="sxs-lookup"><span data-stu-id="96e84-176">The <xref:System.Activities.Expressions.InvokeMethod%601> activity could also have been used to call the <xref:System.Random.Next%2A> method of the <xref:System.Random> class.</span></span>  
  
```csharp  
new InvokeMethod<int>  
{  
    TargetObject = new InArgument<Random>(new VisualBasicValue<Random>("New Random()")),  
    MethodName = "Next",  
    Parameters =
    {  
        new InArgument<int>(1),  
        new InArgument<int>(101)  
    },  
    Result = n  
}  
```  
  
 <span data-ttu-id="96e84-177">由於 <xref:System.Random.Next%2A> 不是靜態方法，因此會提供 <xref:System.Random> 類別的執行個體給 <xref:System.Activities.Expressions.InvokeMethod%601.TargetObject%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="96e84-177">Since <xref:System.Random.Next%2A> is not a static method, an instance of the <xref:System.Random> class is supplied for the <xref:System.Activities.Expressions.InvokeMethod%601.TargetObject%2A> property.</span></span> <span data-ttu-id="96e84-178">在此範例中，會使用 Visual Basic 運算式建立新執行個體，但是該執行個體也可能已建立並儲存在工作流程變數中。</span><span class="sxs-lookup"><span data-stu-id="96e84-178">In this example a new instance is created using a Visual Basic expression, but it could also have been created previously and stored in a workflow variable.</span></span> <span data-ttu-id="96e84-179">在此範例中，使用 <xref:System.Activities.Statements.Assign%601> 活動而不是 <xref:System.Activities.Expressions.InvokeMethod%601> 活動會比較簡單。</span><span class="sxs-lookup"><span data-stu-id="96e84-179">In this example, it would be simpler to use the <xref:System.Activities.Statements.Assign%601> activity instead of the <xref:System.Activities.Expressions.InvokeMethod%601> activity.</span></span> <span data-ttu-id="96e84-180">如果最終由 <xref:System.Activities.Statements.Assign%601> 或 <xref:System.Activities.Expressions.InvokeMethod%601> 活動叫用的方法呼叫為長期執行，則 <xref:System.Activities.Expressions.InvokeMethod%601> 具有優勢，因為它有 <xref:System.Activities.Expressions.InvokeMethod%601.RunAsynchronously%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="96e84-180">If the method call ultimately invoked by either the <xref:System.Activities.Statements.Assign%601> or <xref:System.Activities.Expressions.InvokeMethod%601> activities is long running, <xref:System.Activities.Expressions.InvokeMethod%601> has an advantage since it has a <xref:System.Activities.Expressions.InvokeMethod%601.RunAsynchronously%2A> property.</span></span> <span data-ttu-id="96e84-181">當此屬性設為 `true` 時，叫用的方法會以非同步方式執行 (與工作流程有關)。</span><span class="sxs-lookup"><span data-stu-id="96e84-181">When this property is set to `true`, the invoked method will run asynchronously with regard to the workflow.</span></span> <span data-ttu-id="96e84-182">如果有其他活動平行，當方法以非同步方式執行時，那些活動不會被封鎖。</span><span class="sxs-lookup"><span data-stu-id="96e84-182">If other activities are in parallel, they will not be blocked while the method is asynchronously executing.</span></span> <span data-ttu-id="96e84-183">此外，如果所要叫用的方法沒有傳回值，那麼 <xref:System.Activities.Expressions.InvokeMethod%601> 會是叫用方法的適當方式。</span><span class="sxs-lookup"><span data-stu-id="96e84-183">Also, if the method to be invoked has no return value, then <xref:System.Activities.Expressions.InvokeMethod%601> is the appropriate way to invoke the method.</span></span>  
  
## <a name="arguments-and-dynamic-activities"></a><span data-ttu-id="96e84-184">引數與動態活動</span><span class="sxs-lookup"><span data-stu-id="96e84-184">Arguments and Dynamic Activities</span></span>  

 <span data-ttu-id="96e84-185">工作流程定義是藉由將活動組裝在活動樹狀目錄中，並設定任何屬性與引數，而建立在程式碼中。</span><span class="sxs-lookup"><span data-stu-id="96e84-185">A workflow definition is created in code by assembling activities into an activity tree and configuring any properties and arguments.</span></span> <span data-ttu-id="96e84-186">可繫結現有的引數，但無法新增新引數至活動。</span><span class="sxs-lookup"><span data-stu-id="96e84-186">Existing arguments can be bound, but new arguments cannot be added to activities.</span></span> <span data-ttu-id="96e84-187">這包含傳遞至根活動的工作流程引數。</span><span class="sxs-lookup"><span data-stu-id="96e84-187">This includes workflow arguments passed to the root activity.</span></span> <span data-ttu-id="96e84-188">在命令式程式碼中，會將工作流程引數指定為新 CLR 型別的屬性，並且在 XAML 中使用 `x:Class` 與 `x:Member` 來宣告它們。</span><span class="sxs-lookup"><span data-stu-id="96e84-188">In imperative code, workflow arguments are specified as properties on a new CLR type, and in XAML they are declared by using `x:Class` and `x:Member`.</span></span> <span data-ttu-id="96e84-189">因為將工作流程定義建立為記憶體內物件的樹狀時，並未建立任何新 CLR 型別，所以無法新增引數。</span><span class="sxs-lookup"><span data-stu-id="96e84-189">Because there is no new CLR type created when a workflow definition is created as a tree of in-memory objects, arguments cannot be added.</span></span> <span data-ttu-id="96e84-190">但是，可新增引數至 <xref:System.Activities.DynamicActivity>。</span><span class="sxs-lookup"><span data-stu-id="96e84-190">However, arguments can be added to a <xref:System.Activities.DynamicActivity>.</span></span> <span data-ttu-id="96e84-191">在此範例中會建立 <xref:System.Activities.DynamicActivity%601>，它採用兩個整數引數並將其同時加入，然後傳回結果。</span><span class="sxs-lookup"><span data-stu-id="96e84-191">In this example, a <xref:System.Activities.DynamicActivity%601> is created that takes two integer arguments, adds them together, and returns the result.</span></span> <span data-ttu-id="96e84-192">不僅會針對每個引數建立 <xref:System.Activities.DynamicActivityProperty>，且會將作業的結果指派至 <xref:System.Activities.Activity%601.Result%2A> 的 <xref:System.Activities.DynamicActivity%601> 引數。</span><span class="sxs-lookup"><span data-stu-id="96e84-192">A <xref:System.Activities.DynamicActivityProperty> is created for each argument, and the result of the operation is assigned to the <xref:System.Activities.Activity%601.Result%2A> argument of the <xref:System.Activities.DynamicActivity%601>.</span></span>  
  
 [!code-csharp[CFX_WorkflowApplicationExample#55](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#55)]  
  
 <span data-ttu-id="96e84-193">如需動態活動的詳細資訊，請參閱 [在執行時間建立活動](creating-an-activity-at-runtime-with-dynamicactivity.md)。</span><span class="sxs-lookup"><span data-stu-id="96e84-193">For more information about dynamic activities, see [Creating an Activity at Runtime](creating-an-activity-at-runtime-with-dynamicactivity.md).</span></span>  
  
## <a name="compiled-activities"></a><span data-ttu-id="96e84-194">已編譯的活動</span><span class="sxs-lookup"><span data-stu-id="96e84-194">Compiled Activities</span></span>  

 <span data-ttu-id="96e84-195">動態活動是使用程式碼來定義包含引數之活動的一種方法，但活動也可以用程式碼建立，並編譯成型別。</span><span class="sxs-lookup"><span data-stu-id="96e84-195">Dynamic activities are one way to define an activity that contains arguments using code, but activities can also be created in code and compiled into types.</span></span> <span data-ttu-id="96e84-196">可以建立衍生自 <xref:System.Activities.CodeActivity> 的簡單活動，以及衍生自 <xref:System.Activities.AsyncCodeActivity> 的非同步活動。</span><span class="sxs-lookup"><span data-stu-id="96e84-196">Simple activities can be created that derive from <xref:System.Activities.CodeActivity>, and asynchronous activities that derive from <xref:System.Activities.AsyncCodeActivity>.</span></span> <span data-ttu-id="96e84-197">這些活動可以具有引數、傳回值，並使用命令式程式碼定義其邏輯。</span><span class="sxs-lookup"><span data-stu-id="96e84-197">These activities can have arguments, return values, and define their logic using imperative code.</span></span> <span data-ttu-id="96e84-198">如需建立這類活動的範例，請參閱 [CodeActivity 基類](workflow-activity-authoring-using-the-codeactivity-class.md) 和 [建立異步活動](creating-asynchronous-activities-in-wf.md)。</span><span class="sxs-lookup"><span data-stu-id="96e84-198">For examples of creating these types of activities, see [CodeActivity Base Class](workflow-activity-authoring-using-the-codeactivity-class.md) and [Creating Asynchronous Activities](creating-asynchronous-activities-in-wf.md).</span></span>  
  
 <span data-ttu-id="96e84-199">衍生自 <xref:System.Activities.NativeActivity> 的活動可以使用命令式程式碼來定義其邏輯，而且也可以包含定義邏輯的子活動。</span><span class="sxs-lookup"><span data-stu-id="96e84-199">Activities that derive from <xref:System.Activities.NativeActivity> can define their logic using imperative code and they can also contain child activities that define the logic.</span></span> <span data-ttu-id="96e84-200">這些活動也可以完整存取執行階段的功能，例如建立書籤。</span><span class="sxs-lookup"><span data-stu-id="96e84-200">They also have full access to the features of the runtime such as creating bookmarks.</span></span> <span data-ttu-id="96e84-201">如需建立 <xref:System.Activities.NativeActivity> 基礎活動的範例，請參閱 [NativeActivity 基類](nativeactivity-base-class.md)、 [如何：建立活動](how-to-create-an-activity.md)和 [使用原生活動的自訂複合](./samples/custom-composite-using-native-activity.md) 範例。</span><span class="sxs-lookup"><span data-stu-id="96e84-201">For examples of creating a <xref:System.Activities.NativeActivity>-based activity, see [NativeActivity Base Class](nativeactivity-base-class.md), [How to: Create an Activity](how-to-create-an-activity.md), and the [Custom Composite using Native Activity](./samples/custom-composite-using-native-activity.md) sample.</span></span>  
  
 <span data-ttu-id="96e84-202">衍生自 <xref:System.Activities.Activity> 的活動可以藉由使用子活動，只定義其邏輯。</span><span class="sxs-lookup"><span data-stu-id="96e84-202">Activities that derive from <xref:System.Activities.Activity> define their logic solely through the use of child activities.</span></span> <span data-ttu-id="96e84-203">這些活動通常是使用工作流程設計工具來建立，但也可以使用程式碼來定義。</span><span class="sxs-lookup"><span data-stu-id="96e84-203">These activities are typically created by using the workflow designer, but can also be defined by using code.</span></span> <span data-ttu-id="96e84-204">在下列範例中，會定義衍生自 `Square` 的 `Activity<int>` 活動。</span><span class="sxs-lookup"><span data-stu-id="96e84-204">In the following example, a `Square` activity is defined that derives from `Activity<int>`.</span></span> <span data-ttu-id="96e84-205">`Square` 活動具有名為 <xref:System.Activities.InArgument%601> 的單一 `Value`，並使用 <xref:System.Activities.Statements.Sequence> 屬性來指定 <xref:System.Activities.Activity.Implementation%2A> 活動，以定義其邏輯。</span><span class="sxs-lookup"><span data-stu-id="96e84-205">The `Square` activity has a single <xref:System.Activities.InArgument%601> named `Value`, and defines its logic by specifying a <xref:System.Activities.Statements.Sequence> activity using the <xref:System.Activities.Activity.Implementation%2A> property.</span></span> <span data-ttu-id="96e84-206"><xref:System.Activities.Statements.Sequence> 活動包含 <xref:System.Activities.Statements.WriteLine> 活動和 <xref:System.Activities.Statements.Assign%601> 活動。</span><span class="sxs-lookup"><span data-stu-id="96e84-206">The <xref:System.Activities.Statements.Sequence> activity contains a <xref:System.Activities.Statements.WriteLine> activity and an <xref:System.Activities.Statements.Assign%601> activity.</span></span> <span data-ttu-id="96e84-207">這三個活動在一起可實作 `Square` 活動的邏輯。</span><span class="sxs-lookup"><span data-stu-id="96e84-207">Together, these three activities implement the logic of the `Square` activity.</span></span>  
  
```csharp  
class Square : Activity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Value { get; set; }  
  
    public Square()  
    {  
        this.Implementation = () => new Sequence  
        {  
            Activities =  
            {  
                new WriteLine  
                {  
                    Text = new InArgument<string>((env) => "Squaring the value: " + this.Value.Get(env))  
                },  
                new Assign<int>  
                {  
                    To = new OutArgument<int>((env) => this.Result.Get(env)),  
                    Value = new InArgument<int>((env) => this.Value.Get(env) * this.Value.Get(env))  
                }  
            }  
        };  
    }  
}  
```  
  
 <span data-ttu-id="96e84-208">在下列範例中，會使用 `Square` 來叫用由單一 <xref:System.Activities.WorkflowInvoker> 活動組成的工作流程定義。</span><span class="sxs-lookup"><span data-stu-id="96e84-208">In the following example, a workflow definition consisting of a single `Square` activity is invoked using <xref:System.Activities.WorkflowInvoker>.</span></span>  
  
```csharp  
Dictionary<string, object> inputs = new Dictionary<string, object> {{ "Value", 5}};  
int result = WorkflowInvoker.Invoke(new Square(), inputs);  
Console.WriteLine("Result: {0}", result);  
```  
  
 <span data-ttu-id="96e84-209">當叫用此工作流程時，主控台會顯示下列輸出：</span><span class="sxs-lookup"><span data-stu-id="96e84-209">When the workflow is invoked, the following output is displayed to the console:</span></span>  
  
 <span data-ttu-id="96e84-210">**求得此值的平方：5**</span><span class="sxs-lookup"><span data-stu-id="96e84-210">**Squaring the value: 5**</span></span>  
<span data-ttu-id="96e84-211">**結果：25**</span><span class="sxs-lookup"><span data-stu-id="96e84-211">**Result: 25**</span></span>
