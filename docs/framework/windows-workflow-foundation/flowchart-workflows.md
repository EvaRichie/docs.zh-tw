---
title: Flowchart 工作流程
description: 本文說明流程圖活動，通常用來在 Workflow Foundation 中執行非連續工作流程。
ms.date: 03/30/2017
ms.assetid: b0a3475c-d22f-49eb-8912-973c960aebf5
ms.openlocfilehash: ce0661653a1d50b3f7264246b810faabbd12bf5f
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2020
ms.locfileid: "83419911"
---
# <a name="flowchart-workflows"></a><span data-ttu-id="4946d-103">Flowchart 工作流程</span><span class="sxs-lookup"><span data-stu-id="4946d-103">Flowchart Workflows</span></span>

<span data-ttu-id="4946d-104">流程圖是設計程式的常見範例。</span><span class="sxs-lookup"><span data-stu-id="4946d-104">A flowchart is a well-known paradigm for designing programs.</span></span> <span data-ttu-id="4946d-105">Flowchart 活動通常用於實作非循序性的工作流程，但如果沒有使用 `FlowDecision` 節點，也可用於循序性的工作流程。</span><span class="sxs-lookup"><span data-stu-id="4946d-105">The Flowchart activity is typically used to implement non-sequential workflows, but can be used for sequential workflows if no `FlowDecision` nodes are used.</span></span>

## <a name="flowchart-workflow-structure"></a><span data-ttu-id="4946d-106">流程圖工作流程結構</span><span class="sxs-lookup"><span data-stu-id="4946d-106">Flowchart workflow structure</span></span>

 <span data-ttu-id="4946d-107">流程圖活動是包含所要執行之活動集合的活動。</span><span class="sxs-lookup"><span data-stu-id="4946d-107">A Flowchart activity is an activity that contains a collection of activities to be executed.</span></span>  <span data-ttu-id="4946d-108">流程圖還包含流程控制元素，例如 <xref:System.Activities.Statements.FlowDecision> 和 <xref:System.Activities.Statements.FlowSwitch%601>，可根據變數的值，在所包含的活動之間主導執行。</span><span class="sxs-lookup"><span data-stu-id="4946d-108">Flowcharts also contain flow control elements such as <xref:System.Activities.Statements.FlowDecision> and <xref:System.Activities.Statements.FlowSwitch%601> that direct execution between contained activities based on the values of variables.</span></span>

## <a name="types-of-flow-nodes"></a><span data-ttu-id="4946d-109">流程節點的類型</span><span class="sxs-lookup"><span data-stu-id="4946d-109">Types of flow nodes</span></span>

 <span data-ttu-id="4946d-110">使用的項目型別，要視項目執行時所需的流程控制型別而定。</span><span class="sxs-lookup"><span data-stu-id="4946d-110">Different types of elements are used depending on the type of flow control required when the element executes.</span></span> <span data-ttu-id="4946d-111">流程圖項目的型別有：</span><span class="sxs-lookup"><span data-stu-id="4946d-111">Types of flowchart elements include:</span></span>

- <span data-ttu-id="4946d-112">`FlowStep` - 建立流程圖中一個步驟執行的模型。</span><span class="sxs-lookup"><span data-stu-id="4946d-112">`FlowStep` - Models one step of execution in the flowchart.</span></span>

- <span data-ttu-id="4946d-113">`FlowDecision` - 根據 Boolean 條件執行的分支，與 <xref:System.Activities.Statements.If> 相似。</span><span class="sxs-lookup"><span data-stu-id="4946d-113">`FlowDecision` - Branches execution based on a Boolean condition, similar to <xref:System.Activities.Statements.If>.</span></span>

- <span data-ttu-id="4946d-114">`FlowSwitch` - 根據專有參數執行的分支，與 <xref:System.Activities.Statements.Switch%601> 相似。</span><span class="sxs-lookup"><span data-stu-id="4946d-114">`FlowSwitch` – Branches execution based on an exclusive switch, similar to <xref:System.Activities.Statements.Switch%601>.</span></span>

<span data-ttu-id="4946d-115">每個連結都有 `Action` 屬性，會定義可用來執行子活動的 <xref:System.Activities.ActivityAction>，以及一個或多個 `Next` 屬性，以定義當目前的元素完成執行時，要執行哪個或哪些元素。</span><span class="sxs-lookup"><span data-stu-id="4946d-115">Each link has an `Action` property that defines a <xref:System.Activities.ActivityAction> that can be used to execute child activities, and one or more `Next` properties that define which element or elements to execute when the current element finishes execution.</span></span>

### <a name="creating-a-basic-activity-sequence-with-a-flowstep-node"></a><span data-ttu-id="4946d-116">使用 FlowStep 節點建立基本活動順序</span><span class="sxs-lookup"><span data-stu-id="4946d-116">Creating a basic activity sequence with a FlowStep node</span></span>

<span data-ttu-id="4946d-117">若要建立讓兩個活動從中輪流執行的基礎序列，就要使用 `FlowStep` 項目。</span><span class="sxs-lookup"><span data-stu-id="4946d-117">To model a basic sequence in which two activities execute in turn, the `FlowStep` element is used.</span></span> <span data-ttu-id="4946d-118">在下列範例中，會使用兩個 `FlowStep` 項目來依序執行兩個活動。</span><span class="sxs-lookup"><span data-stu-id="4946d-118">In the following example, two `FlowStep` elements are used to execute two activities in sequence.</span></span>

```xml
<Flowchart>
  <FlowStep>
    <Assign DisplayName="Get Name">
      <Assign.To>
        <OutArgument x:TypeArguments="x:String">[result]</OutArgument>
      </Assign.To>
      <Assign.Value>
        <InArgument x:TypeArguments="x:String">["User"]</InArgument>
      </Assign.Value>
    </Assign>
    <FlowStep.Next>
      <FlowStep>
        <WriteLine Text="Hello, " & [result]/>
      </FlowStep>
    </FlowStep.Next>
  </FlowStep>
</Flowchart>
```

### <a name="creating-a-conditional-flowchart-with-a-flowdecision-node"></a><span data-ttu-id="4946d-119">建立具有 FlowDecision 節點的條件式流程圖</span><span class="sxs-lookup"><span data-stu-id="4946d-119">Creating a conditional flowchart with a FlowDecision node</span></span>

<span data-ttu-id="4946d-120">若要在流程圖工作流程中建立條件式流程節點 (也就是，建立做為傳統流程圖決策符號的連結)，就要使用 <xref:System.Activities.Statements.FlowDecision> 節點。</span><span class="sxs-lookup"><span data-stu-id="4946d-120">To model a conditional flow node in a flowchart workflow (that is, to create a link that functions as a traditional flowchart's decision symbol), a <xref:System.Activities.Statements.FlowDecision> node is used.</span></span> <span data-ttu-id="4946d-121">節點的 <xref:System.Activities.Statements.FlowDecision.Condition%2A> 屬性設定為定義條件的運算式，而且 <xref:System.Activities.Statements.FlowDecision.True%2A> 和 <xref:System.Activities.Statements.FlowDecision.False%2A> 屬性設定為當運算式評估為 <xref:System.Activities.Statements.FlowNode> 或 `true` 時所要執行的 `false` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="4946d-121">The <xref:System.Activities.Statements.FlowDecision.Condition%2A> property of the node is set to an expression that defines the condition, and the <xref:System.Activities.Statements.FlowDecision.True%2A> and <xref:System.Activities.Statements.FlowDecision.False%2A> properties are set to <xref:System.Activities.Statements.FlowNode> instances to be executed if the expression evaluates to `true` or `false`.</span></span> <span data-ttu-id="4946d-122">下列範例示範如何定義使用 <xref:System.Activities.Statements.FlowDecision> 節點的工作流程。</span><span class="sxs-lookup"><span data-stu-id="4946d-122">The following example shows how to define a workflow that uses a <xref:System.Activities.Statements.FlowDecision> node.</span></span>

```xml
<Flowchart>
  <FlowStep>
    <Read Result="[s]"/>
    <FlowStep.Next>
      <FlowDecision>
        <IsEmpty Input="[s]" />
        <FlowDecision.True>
          <FlowStep>
            <Write Text="Empty"/>
          </FlowStep>
        </FlowDecision.True>
        <FlowDecision.False>
          <FlowStep>
            <Write Text="Non-Empty"/>
          </FlowStep>
        </FlowDecision.False>
      </FlowDecision>
    </FlowStep.Next>
  </FlowStep>
</Flowchart>
```

### <a name="creating-an-exclusive-switch-with-a-flowswitch-node"></a><span data-ttu-id="4946d-123">建立具有 FlowSwitch-節點的獨佔交換器</span><span class="sxs-lookup"><span data-stu-id="4946d-123">Creating an exclusive switch with a FlowSwitch node</span></span>

<span data-ttu-id="4946d-124">若要建立其中根據相符值選取之獨佔路徑流程圖的模型，就要使用 <xref:System.Activities.Statements.FlowSwitch%601> 節點。</span><span class="sxs-lookup"><span data-stu-id="4946d-124">To model a flowchart in which one exclusive path is selected based on a matching value, the <xref:System.Activities.Statements.FlowSwitch%601> node is used.</span></span> <span data-ttu-id="4946d-125"><xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> 屬性設為 <xref:System.Activities.Activity%601>，且型別參數為 <xref:System.Object>，可定義用來比對選擇的值。</span><span class="sxs-lookup"><span data-stu-id="4946d-125">The <xref:System.Activities.Statements.FlowSwitch%601.Expression%2A> property is set to a <xref:System.Activities.Activity%601> with a type parameter of <xref:System.Object> that defines the value to match choices against.</span></span> <span data-ttu-id="4946d-126"><xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> 屬性會定義用來比對條件運算式的索引鍵字典和 <xref:System.Activities.Statements.FlowNode> 物件，以及另一組 <xref:System.Activities.Statements.FlowNode> 物件，以定義當給定個案符合條件運算式時，執行的流程為何。</span><span class="sxs-lookup"><span data-stu-id="4946d-126">The <xref:System.Activities.Statements.FlowSwitch%601.Cases%2A> property defines a dictionary of keys and <xref:System.Activities.Statements.FlowNode> objects to match against the conditional expression, and a set of <xref:System.Activities.Statements.FlowNode> objects that define how execution should flow if the given case matches the conditional expression.</span></span> <span data-ttu-id="4946d-127"><xref:System.Activities.Statements.FlowSwitch%601> 也會定義 <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> 屬性，此屬性會定義如果沒有符合條件運算式的情況時，應該要如何進行執行的流程。</span><span class="sxs-lookup"><span data-stu-id="4946d-127">The <xref:System.Activities.Statements.FlowSwitch%601> also defines a <xref:System.Activities.Statements.FlowSwitch%601.Default%2A> property that defines how execution should flow if no cases match the condition expression.</span></span> <span data-ttu-id="4946d-128">下列範例示範如何定義使用 <xref:System.Activities.Statements.FlowSwitch%601> 項目的工作流程。</span><span class="sxs-lookup"><span data-stu-id="4946d-128">The following example demonstrates how to define a workflow that uses a <xref:System.Activities.Statements.FlowSwitch%601> element.</span></span>

```xml
<Flowchart>
  <FlowSwitch>
    <FlowStep x:Key="Red">
      <WriteRed/>
    </FlowStep>
    <FlowStep x:Key="Blue">
      <WriteBlue/>
    </FlowStep>
    <FlowStep x:Key="Green">
      <WriteGreen/>
    </FlowStep>
  </FlowSwitch>
</Flowchart>
```
