---
title: 定義類別
ms.date: 07/20/2015
helpviewer_keywords:
- execution [Visual Basic], ending
- objects [Visual Basic], initializing
- Initialize event [Visual Basic]
- files [Visual Basic], closing
- programs [Visual Basic], quitting
- code, exiting
- objects [Visual Basic], creating
- program termination
- classes [Visual Basic], walkthroughs
- class modules, walkthroughs
- Terminate event [Visual Basic]
- execution [Visual Basic], stopping
ms.assetid: 07018828-2d49-4cf5-a44b-19fb15d9efea
ms.openlocfilehash: 646c6ce307131f3edba194af19920eade9c1753c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84389110"
---
# <a name="walkthrough-defining-classes-visual-basic"></a><span data-ttu-id="9c1eb-102">逐步解說：定義類別 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9c1eb-102">Walkthrough: Defining Classes (Visual Basic)</span></span>

<span data-ttu-id="9c1eb-103">本逐步解說示範如何定義類別，您可以用它來建立物件。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-103">This walkthrough demonstrates how to define classes, which you can then use to create objects.</span></span> <span data-ttu-id="9c1eb-104">它也會示範如何將屬性和方法新增至新的類別，以及如何初始化物件。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-104">It also shows you how to add properties and methods to the new class, and demonstrates how to initialize an object.</span></span>  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="to-define-a-class"></a><span data-ttu-id="9c1eb-105">若要定義類別</span><span class="sxs-lookup"><span data-stu-id="9c1eb-105">To define a class</span></span>
  
1. <span data-ttu-id="9c1eb-106">按一下 **[檔案**] 功能表上的 [**新增專案**] 來建立專案。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-106">Create a project by clicking **New Project** on the **File** menu.</span></span> <span data-ttu-id="9c1eb-107">[新增專案]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-107">The **New Project** dialog box appears.</span></span>  
  
2. <span data-ttu-id="9c1eb-108">從 Visual Basic 專案範本清單中選取 [Windows 應用程式]，以顯示新的專案。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-108">Select Windows Application from the list of Visual Basic project templates to display the new project.</span></span>  
  
3. <span data-ttu-id="9c1eb-109">按一下 [**專案**] 功能表上的 [**加入類別**]，將新的類別加入至專案。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-109">Add a new class to the project by clicking **Add Class** on the **Project** menu.</span></span> <span data-ttu-id="9c1eb-110">[加入新項目] \*\*\*\* 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-110">The **Add New Item** dialog box appears.</span></span>  
  
4. <span data-ttu-id="9c1eb-111">選取 [**類別**] 範本。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-111">Select the **Class** template.</span></span>  
  
5. <span data-ttu-id="9c1eb-112">將新類別命名為 `UserNameInfo.vb` ，然後按一下**Add** [新增] 以顯示新類別的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-112">Name the new class `UserNameInfo.vb`, and then click **Add** to display the code for the new class.</span></span>  
  
     [!code-vb[VbVbalrOOP#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#5)]
  
    > [!NOTE]
    > <span data-ttu-id="9c1eb-113">您可以使用 [Visual Basic 程式**代碼編輯器**]，輸入 `Class` 關鍵字並在後面加上新類別的名稱，以將類別新增至啟動表單。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-113">You can use the Visual Basic **Code Editor** to add a class to your startup form by typing the `Class` keyword followed by the name of the new class.</span></span> <span data-ttu-id="9c1eb-114">[程式**代碼編輯器**] `End Class` 會為您提供對應的語句。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-114">The **Code Editor** provides a corresponding `End Class` statement for you.</span></span>  
  
6. <span data-ttu-id="9c1eb-115">在和語句之間加入下列程式碼，以定義類別的私用欄位 `Class` `End Class` ：</span><span class="sxs-lookup"><span data-stu-id="9c1eb-115">Define a private field for the class by adding the following code between the `Class` and `End Class` statements:</span></span>  
  
     [!code-vb[VbVbalrOOP#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#7)]
  
     <span data-ttu-id="9c1eb-116">將欄位宣告為， `Private` 表示它只能在類別中使用。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-116">Declaring the field as `Private` means it can be used only within the class.</span></span> <span data-ttu-id="9c1eb-117">您可以使用存取修飾詞（例如 `Public` ，提供更多存取權），將欄位從類別外部提供。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-117">You can make fields available from outside a class by using access modifiers such as `Public` that provide more access.</span></span> <span data-ttu-id="9c1eb-118">如需詳細資訊，請參閱[Visual Basic 中的存取層級](../declared-elements/access-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-118">For more information, see [Access levels in Visual Basic](../declared-elements/access-levels.md).</span></span>  
  
7. <span data-ttu-id="9c1eb-119">藉由新增下列程式碼來定義類別的屬性：</span><span class="sxs-lookup"><span data-stu-id="9c1eb-119">Define a property for the class by adding the following code:</span></span>  
  
     [!code-vb[VbVbalrOOP#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#8)]
  
8. <span data-ttu-id="9c1eb-120">藉由新增下列程式碼來定義類別的方法：</span><span class="sxs-lookup"><span data-stu-id="9c1eb-120">Define a method for the class by adding the following code:</span></span>  
  
     [!code-vb[VbVbalrOOP#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#9)]
  
9. <span data-ttu-id="9c1eb-121">藉由新增名為的程式，為新的類別定義參數化的函式 `Sub New` ：</span><span class="sxs-lookup"><span data-stu-id="9c1eb-121">Define a parameterized constructor for the new class by adding a procedure named `Sub New`:</span></span>  
  
     [!code-vb[VbVbalrOOP#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#10)]
  
     <span data-ttu-id="9c1eb-122">`Sub New`建立以這個類別為基礎的物件時，會自動呼叫此函式。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-122">The `Sub New` constructor is called automatically when an object based on this class is created.</span></span> <span data-ttu-id="9c1eb-123">此函式會設定保留使用者名稱的欄位值。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-123">This constructor sets the value of the field that holds the user name.</span></span>  
  
## <a name="to-create-a-button-to-test-the-class"></a><span data-ttu-id="9c1eb-124">若要建立按鈕來測試類別</span><span class="sxs-lookup"><span data-stu-id="9c1eb-124">To create a button to test the class</span></span>
  
1. <span data-ttu-id="9c1eb-125">將 [啟動表單] 變更為 [設計] 模式，方法是以滑鼠右鍵按一下**方案總管**中的名稱，然後按一下 [ **View Designer**]。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-125">Change the startup form to design mode by right-clicking its name in **Solution Explorer** and then clicking **View Designer**.</span></span> <span data-ttu-id="9c1eb-126">根據預設，Windows 應用程式專案的啟動表單名為 form1.vb。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-126">By default, the startup form for Windows Application projects is named Form1.vb.</span></span> <span data-ttu-id="9c1eb-127">然後會出現主要表單。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-127">The main form will then appear.</span></span>  
  
2. <span data-ttu-id="9c1eb-128">將按鈕新增至主要表單，然後按兩下以顯示 `Button1_Click` 事件處理常式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-128">Add a button to the main form and double-click it to display the code for the `Button1_Click` event handler.</span></span> <span data-ttu-id="9c1eb-129">新增下列程式碼以呼叫測試程式：</span><span class="sxs-lookup"><span data-stu-id="9c1eb-129">Add the following code to call the test procedure:</span></span>  
  
     [!code-vb[VbVbalrOOP#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#12)]
  
## <a name="to-run-your-application"></a><span data-ttu-id="9c1eb-130">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="9c1eb-130">To run your application</span></span>
  
1. <span data-ttu-id="9c1eb-131">按 F5 鍵執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-131">Run your application by pressing F5.</span></span> <span data-ttu-id="9c1eb-132">按一下表單上的按鈕以呼叫測試程式。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-132">Click the button on the form to call the test procedure.</span></span> <span data-ttu-id="9c1eb-133">它會顯示一則訊息，說明原始的 `UserName` 是 "摩爾，胡，"，因為程式呼叫了 `Capitalize` 物件的方法。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-133">It displays a message stating that the original `UserName` is "MOORE, BOBBY", because the procedure called the `Capitalize` method of the object.</span></span>  
  
2. <span data-ttu-id="9c1eb-134">按一下 [確定]\*\*\*\* 來解除訊息方塊。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-134">Click **OK** to dismiss the message box.</span></span> <span data-ttu-id="9c1eb-135">此程式 `Button1 Click` 會變更屬性的值 `UserName` ，並顯示一則訊息，指出的新值 `UserName` 為 "Worden，Joe"。</span><span class="sxs-lookup"><span data-stu-id="9c1eb-135">The `Button1 Click` procedure changes the value of the `UserName` property and displays a message stating that the new value of `UserName` is "Worden, Joe".</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9c1eb-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9c1eb-136">See also</span></span>

- [<span data-ttu-id="9c1eb-137">物件導向程式設計 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9c1eb-137">Object-Oriented Programming (Visual Basic)</span></span>](../../concepts/object-oriented-programming.md)
- [<span data-ttu-id="9c1eb-138">物件和類別</span><span class="sxs-lookup"><span data-stu-id="9c1eb-138">Objects and Classes</span></span>](index.md)
