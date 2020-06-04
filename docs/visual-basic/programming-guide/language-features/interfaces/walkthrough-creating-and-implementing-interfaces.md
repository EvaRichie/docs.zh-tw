---
title: 建立及實作介面
ms.date: 07/20/2015
helpviewer_keywords:
- interfaces [Visual Basic], walkthroughs
- interfaces [Visual Basic], testing
- interface implementation [Visual Basic], walkthrough
- interfaces [Visual Basic], creating
ms.assetid: ded82af2-9f52-4232-98ef-fe458180f112
ms.openlocfilehash: 89e8f91a04b25b84bc783d5c4f4b91cf12426f72
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405063"
---
# <a name="walkthrough-creating-and-implementing-interfaces-visual-basic"></a><span data-ttu-id="c50cd-102">逐步解說：建立和實作介面 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c50cd-102">Walkthrough: Creating and Implementing Interfaces (Visual Basic)</span></span>

<span data-ttu-id="c50cd-103">介面會描述屬性、方法和事件的特性，但會將執行詳細資料保持在結構或類別的最上方。</span><span class="sxs-lookup"><span data-stu-id="c50cd-103">Interfaces describe the characteristics of properties, methods, and events, but leave the implementation details up to structures or classes.</span></span>  
  
 <span data-ttu-id="c50cd-104">本逐步解說示範如何宣告和執行介面。</span><span class="sxs-lookup"><span data-stu-id="c50cd-104">This walkthrough demonstrates how to declare and implement an interface.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="c50cd-105">本逐步解說並未提供如何建立使用者介面的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c50cd-105">This walkthrough doesn't provide information about how to create a user interface.</span></span>  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="to-define-an-interface"></a><span data-ttu-id="c50cd-106">若要定義介面</span><span class="sxs-lookup"><span data-stu-id="c50cd-106">To define an interface</span></span>
  
1. <span data-ttu-id="c50cd-107">開啟新的 Visual Basic Windows 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="c50cd-107">Open a new Visual Basic Windows Application project.</span></span>  
  
2. <span data-ttu-id="c50cd-108">按一下 [**專案**] 功能表上的 [**加入模組**]，將新的模組加入至專案。</span><span class="sxs-lookup"><span data-stu-id="c50cd-108">Add a new module to the project by clicking **Add Module** on the **Project** menu.</span></span>  
  
3. <span data-ttu-id="c50cd-109">為新模組命名 `Module1.vb` ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c50cd-109">Name the new module `Module1.vb` and click **Add**.</span></span> <span data-ttu-id="c50cd-110">新模組的程式碼隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="c50cd-110">The code for the new module is displayed.</span></span>  
  
4. <span data-ttu-id="c50cd-111">`TestInterface`在 `Module1` `Interface TestInterface` `Module` 和語句之間輸入，然後 `End Module` 按 enter 鍵，以定義中名為的介面。</span><span class="sxs-lookup"><span data-stu-id="c50cd-111">Define an interface named `TestInterface` within `Module1` by typing `Interface TestInterface` between the `Module` and `End Module` statements, and then pressing ENTER.</span></span> <span data-ttu-id="c50cd-112">[程式**代碼編輯器**] 會縮排 `Interface` 關鍵字，並加入 `End Interface` 語句以形成程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="c50cd-112">The **Code Editor** indents the `Interface` keyword and adds an `End Interface` statement to form a code block.</span></span>  
  
5. <span data-ttu-id="c50cd-113">藉由將下列程式碼放在和語句之間，定義介面的屬性、方法和事件 `Interface` `End Interface` ：</span><span class="sxs-lookup"><span data-stu-id="c50cd-113">Define a property, method, and event for the interface by placing the following code between the `Interface` and `End Interface` statements:</span></span>  
  
     [!code-vb[VbVbalrOOP#98](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#98)]
  
## <a name="implementation"></a><span data-ttu-id="c50cd-114">實作</span><span class="sxs-lookup"><span data-stu-id="c50cd-114">Implementation</span></span>

 <span data-ttu-id="c50cd-115">您可能會注意到，用來宣告介面成員的語法與用來宣告類別成員的語法不同。</span><span class="sxs-lookup"><span data-stu-id="c50cd-115">You may notice that the syntax used to declare interface members is different from the syntax used to declare class members.</span></span> <span data-ttu-id="c50cd-116">這種差異反映了介面不能包含實作為程式碼的事實。</span><span class="sxs-lookup"><span data-stu-id="c50cd-116">This difference reflects the fact that interfaces cannot contain implementation code.</span></span>  
  
### <a name="to-implement-the-interface"></a><span data-ttu-id="c50cd-117">若要執行介面</span><span class="sxs-lookup"><span data-stu-id="c50cd-117">To implement the interface</span></span>
  
1. <span data-ttu-id="c50cd-118">加入名為 `ImplementationClass` 的類別，方法是將下列語句加入至 `Module1` `End Interface` 語句之後但在 `End Module` 語句之前，然後按 enter 鍵：</span><span class="sxs-lookup"><span data-stu-id="c50cd-118">Add a class named `ImplementationClass` by adding the following statement to `Module1`, after the `End Interface` statement but before the `End Module` statement, and then pressing ENTER:</span></span>  
  
     [!code-vb[VbVbalrOOP#99](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#99)]
  
     <span data-ttu-id="c50cd-119">如果您是在整合式開發環境中工作，則當您按下 ENTER 時，程式**代碼編輯器**會提供相符的 `End Class` 語句。</span><span class="sxs-lookup"><span data-stu-id="c50cd-119">If you are working within the integrated development environment, the **Code Editor** supplies a matching `End Class` statement when you press ENTER.</span></span>  
  
2. <span data-ttu-id="c50cd-120">將下列 `Implements` 語句新增至 `ImplementationClass` ，以命名類別所要執行的介面：</span><span class="sxs-lookup"><span data-stu-id="c50cd-120">Add the following `Implements` statement to `ImplementationClass`, which names the interface the class implements:</span></span>  
  
     [!code-vb[VbVbalrOOP#100](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#100)]
  
     <span data-ttu-id="c50cd-121">與類別或結構頂端的其他專案分開列出時， `Implements` 語句會指出類別或結構會執行介面。</span><span class="sxs-lookup"><span data-stu-id="c50cd-121">When listed separately from other items at the top of a class or structure, the `Implements` statement indicates that the class or structure implements an interface.</span></span>  
  
     <span data-ttu-id="c50cd-122">如果您在整合式開發環境中工作，程式**代碼編輯器**會在您按下 enter 時，執行所需的類別成員 `TestInterface` ，而您可以略過下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="c50cd-122">If you are working within the integrated development environment, the **Code Editor** implements the class members required by `TestInterface` when you press ENTER, and you can skip the next step.</span></span>  
  
3. <span data-ttu-id="c50cd-123">如果您不是在整合式開發環境中工作，則必須執行介面的所有成員 `MyInterface` 。</span><span class="sxs-lookup"><span data-stu-id="c50cd-123">If you are not working within the integrated development environment, you must implement all the members of the interface `MyInterface`.</span></span> <span data-ttu-id="c50cd-124">將下列程式碼新增至 `ImplementationClass` ，以執行 `Event1` 、 `Method1` 和 `Prop1` ：</span><span class="sxs-lookup"><span data-stu-id="c50cd-124">Add the following code to `ImplementationClass` to implement `Event1`, `Method1`, and `Prop1`:</span></span>  
  
     [!code-vb[VbVbalrOOP#101](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#101)]
  
     <span data-ttu-id="c50cd-125">`Implements`語句會命名要實作為介面和介面成員。</span><span class="sxs-lookup"><span data-stu-id="c50cd-125">The `Implements` statement names the interface and interface member being implemented.</span></span>  
  
4. <span data-ttu-id="c50cd-126">藉 `Prop1` 由將私用欄位新增至儲存屬性值的類別，完成的定義：</span><span class="sxs-lookup"><span data-stu-id="c50cd-126">Complete the definition of `Prop1` by adding a private field to the class that stored the property value:</span></span>  
  
     [!code-vb[VbVbalrOOP#102](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#102)]
  
     <span data-ttu-id="c50cd-127">`pval`從屬性 get 存取子傳回的值。</span><span class="sxs-lookup"><span data-stu-id="c50cd-127">Return the value of the `pval` from the property get accessor.</span></span>  
  
     [!code-vb[VbVbalrOOP#103](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#103)]
  
     <span data-ttu-id="c50cd-128">`pval`在屬性集存取子中設定的值。</span><span class="sxs-lookup"><span data-stu-id="c50cd-128">Set the value of `pval` in the property set accessor.</span></span>  
  
     [!code-vb[VbVbalrOOP#104](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#104)]
  
5. <span data-ttu-id="c50cd-129">`Method1`新增下列程式碼，以完成的定義。</span><span class="sxs-lookup"><span data-stu-id="c50cd-129">Complete the definition of `Method1` by adding the following code.</span></span>  
  
     [!code-vb[VbVbalrOOP#105](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#105)]
  
### <a name="to-test-the-implementation-of-the-interface"></a><span data-ttu-id="c50cd-130">測試介面的執行</span><span class="sxs-lookup"><span data-stu-id="c50cd-130">To test the implementation of the interface</span></span>
  
1. <span data-ttu-id="c50cd-131">在 [**方案總管**中，以滑鼠右鍵按一下專案的 [啟動] 表單，然後按一下 [**查看程式碼**]。</span><span class="sxs-lookup"><span data-stu-id="c50cd-131">Right-click the startup form for your project in the **Solution Explorer**, and click **View Code**.</span></span> <span data-ttu-id="c50cd-132">編輯器會顯示您的啟動表單的類別。</span><span class="sxs-lookup"><span data-stu-id="c50cd-132">The editor displays the class for your startup form.</span></span> <span data-ttu-id="c50cd-133">根據預設，會呼叫啟動表單 `Form1` 。</span><span class="sxs-lookup"><span data-stu-id="c50cd-133">By default, the startup form is called `Form1`.</span></span>  
  
2. <span data-ttu-id="c50cd-134">將下列 `testInstance` 欄位新增至 `Form1` 類別：</span><span class="sxs-lookup"><span data-stu-id="c50cd-134">Add the following `testInstance` field to the `Form1` class:</span></span>  
  
     [!code-vb[VbVbalrOOP#120](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#120)]
  
     <span data-ttu-id="c50cd-135">藉由宣告 `testInstance` 為 `WithEvents` ， `Form1` 類別可以處理其事件。</span><span class="sxs-lookup"><span data-stu-id="c50cd-135">By declaring `testInstance` as `WithEvents`, the `Form1` class can handle its events.</span></span>  
  
3. <span data-ttu-id="c50cd-136">將下列事件處理常式新增至 `Form1` 類別，以處理所引發的事件 `testInstance` ：</span><span class="sxs-lookup"><span data-stu-id="c50cd-136">Add the following event handler to the `Form1` class to handle events raised by `testInstance`:</span></span>  
  
     [!code-vb[VbVbalrOOP#106](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#106)]
  
4. <span data-ttu-id="c50cd-137">將名為的副程式新增 `Test` 至 `Form1` 類別，以測試執行類別：</span><span class="sxs-lookup"><span data-stu-id="c50cd-137">Add a subroutine named `Test` to the `Form1` class to test the implementation class:</span></span>  
  
     [!code-vb[VbVbalrOOP#107](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#107)]
  
     <span data-ttu-id="c50cd-138">程式 `Test` 會建立執行之類別的實例、將 `MyInterface` 該實例指派給 `testInstance` 欄位、設定屬性，以及透過介面執行方法。</span><span class="sxs-lookup"><span data-stu-id="c50cd-138">The `Test` procedure creates an instance of the class that implements `MyInterface`, assigns that instance to the `testInstance` field, sets a property, and runs a method through the interface.</span></span>  
  
5. <span data-ttu-id="c50cd-139">新增程式碼，以 `Test` 從 `Form1 Load` 啟動表單的程式呼叫程式：</span><span class="sxs-lookup"><span data-stu-id="c50cd-139">Add code to call the `Test` procedure from the `Form1 Load` procedure of your startup form:</span></span>  
  
     [!code-vb[VbVbalrOOP#108](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#108)]
  
6. <span data-ttu-id="c50cd-140">`Test`按 F5 鍵執行程式。</span><span class="sxs-lookup"><span data-stu-id="c50cd-140">Run the `Test` procedure by pressing F5.</span></span> <span data-ttu-id="c50cd-141">[Prop1 已設定為 9] 訊息隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="c50cd-141">The message "Prop1 was set to 9" is displayed.</span></span> <span data-ttu-id="c50cd-142">按一下 [確定] 之後，就會顯示「Method1 的 X 參數是5」的訊息。</span><span class="sxs-lookup"><span data-stu-id="c50cd-142">After you click OK, the message "The X parameter for Method1 is 5" is displayed.</span></span> <span data-ttu-id="c50cd-143">按一下 [確定]，就會顯示 [事件處理常式攔截事件] 訊息。</span><span class="sxs-lookup"><span data-stu-id="c50cd-143">Click OK, and the message "The event handler caught the event" is displayed.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c50cd-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c50cd-144">See also</span></span>

- [<span data-ttu-id="c50cd-145">Implements 陳述式</span><span class="sxs-lookup"><span data-stu-id="c50cd-145">Implements Statement</span></span>](../../../language-reference/statements/implements-statement.md)
- [<span data-ttu-id="c50cd-146">介面</span><span class="sxs-lookup"><span data-stu-id="c50cd-146">Interfaces</span></span>](index.md)
- [<span data-ttu-id="c50cd-147">Interface 陳述式</span><span class="sxs-lookup"><span data-stu-id="c50cd-147">Interface Statement</span></span>](../../../language-reference/statements/interface-statement.md)
- [<span data-ttu-id="c50cd-148">Event 陳述式</span><span class="sxs-lookup"><span data-stu-id="c50cd-148">Event Statement</span></span>](../../../language-reference/statements/event-statement.md)
