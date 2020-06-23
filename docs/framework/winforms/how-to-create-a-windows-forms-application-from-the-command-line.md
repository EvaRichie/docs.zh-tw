---
title: 從命令列建立 Windows Forms 應用程式
titleSuffix: ''
description: 瞭解如何完成從命令列建立和執行 Windows Forms 應用程式的基本步驟。
ms.date: 03/14/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms, application development from command line
- Windows Forms, getting started
- Windows Forms, creating basic form
ms.assetid: 45ad3f8b-1c26-4c9f-91a9-3bb0759a47a4
ms.openlocfilehash: b63bf884b9fd03a0510c7f240f19d7a14196971a
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84903450"
---
# <a name="how-to-create-a-windows-forms-application-from-the-command-line"></a><span data-ttu-id="cfec1-103">如何：從命令列建立 Windows Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="cfec1-103">How to: Create a Windows Forms application from the command line</span></span>

<span data-ttu-id="cfec1-104">下列程序說明若要從命令列建立及執行 Windows Forms 應用程式，所必須完成的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="cfec1-104">The following procedures describe the basic steps that you must complete to create and run a Windows Forms application from the command line.</span></span> <span data-ttu-id="cfec1-105">在 Visual Studio 中，對這些程序有廣泛的支援。</span><span class="sxs-lookup"><span data-stu-id="cfec1-105">There is extensive support for these procedures in Visual Studio.</span></span>  <span data-ttu-id="cfec1-106">另請參閱[逐步解說：在 WPF 中裝載 Windows Forms 控制項](../wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)。</span><span class="sxs-lookup"><span data-stu-id="cfec1-106">Also see [Walkthrough: Hosting a Windows Forms Control in WPF](../wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md).</span></span>
  
## <a name="procedure"></a><span data-ttu-id="cfec1-107">程序</span><span class="sxs-lookup"><span data-stu-id="cfec1-107">Procedure</span></span>  
  
#### <a name="to-create-the-form"></a><span data-ttu-id="cfec1-108">建立表單</span><span class="sxs-lookup"><span data-stu-id="cfec1-108">To create the form</span></span>  
  
1. <span data-ttu-id="cfec1-109">在空白的程式碼檔案中，輸入下列 `Imports` 或 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="cfec1-109">In an empty code file, type the following `Imports` or `using` statements:</span></span>  
  
     [!code-csharp[System.Windows.Forms.BasicForm#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.BasicForm#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#2)]  
  
2. <span data-ttu-id="cfec1-110">宣告 `Form1` 繼承自表單類別且名為的類別：</span><span class="sxs-lookup"><span data-stu-id="cfec1-110">Declare a class named `Form1` that inherits from the Form class:</span></span>
  
     [!code-csharp[System.Windows.Forms.BasicForm#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.BasicForm#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#3)]  
  
3. <span data-ttu-id="cfec1-111">為建立無參數的函式 `Form1` 。</span><span class="sxs-lookup"><span data-stu-id="cfec1-111">Create a parameterless constructor for `Form1`.</span></span>
  
     <span data-ttu-id="cfec1-112">您在後續的程序中，會將更多程式碼加入建構函式中。</span><span class="sxs-lookup"><span data-stu-id="cfec1-112">You will add more code to the constructor in a subsequent procedure.</span></span>
  
     [!code-csharp[System.Windows.Forms.BasicForm#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.BasicForm#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#4)]  
  
4. <span data-ttu-id="cfec1-113">將 `Main` 方法加入類別中。</span><span class="sxs-lookup"><span data-stu-id="cfec1-113">Add a `Main` method to the class.</span></span>
  
    1. <span data-ttu-id="cfec1-114">將套用 <xref:System.STAThreadAttribute> 至 c # `Main` 方法，以指定您的 Windows Forms 應用程式是單一執行緒的單元。</span><span class="sxs-lookup"><span data-stu-id="cfec1-114">Apply the <xref:System.STAThreadAttribute> to the C# `Main` method to specify your Windows Forms application is a single-threaded apartment.</span></span> <span data-ttu-id="cfec1-115">（屬性在 Visual Basic 中不是必要的，因為使用 Visual Basic 開發的 Windows form 應用程式預設會使用單一執行緒的單元模型）。</span><span class="sxs-lookup"><span data-stu-id="cfec1-115">(The attribute is not necessary in Visual Basic, since Windows forms applications developed with Visual Basic use a single-threaded apartment model by default.)</span></span>  
  
    2. <span data-ttu-id="cfec1-116">呼叫 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 以將作業系統樣式套用至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cfec1-116">Call <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> to apply operating system styles to your application.</span></span>  
  
    3. <span data-ttu-id="cfec1-117">建立表單的執行個體，並加以執行。</span><span class="sxs-lookup"><span data-stu-id="cfec1-117">Create an instance of the form and run it.</span></span>  
  
     [!code-csharp[System.Windows.Forms.BasicForm#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/CS/Form1.cs#5)]
     [!code-vb[System.Windows.Forms.BasicForm#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BasicForm/VB/Form1.vb#5)]  
  
#### <a name="to-compile-and-run-the-application"></a><span data-ttu-id="cfec1-118">編譯和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="cfec1-118">To compile and run the application</span></span>  
  
1. <span data-ttu-id="cfec1-119">在 .NET Framework 命令提示字元中，巡覽至您建立 `Form1` 類別的目錄。</span><span class="sxs-lookup"><span data-stu-id="cfec1-119">At the .NET Framework command prompt, navigate to the directory you created the `Form1` class.</span></span>  
  
2. <span data-ttu-id="cfec1-120">編譯表單。</span><span class="sxs-lookup"><span data-stu-id="cfec1-120">Compile the form.</span></span>  
  
    - <span data-ttu-id="cfec1-121">如果您使用的是 c #，請輸入：`csc form1.cs`</span><span class="sxs-lookup"><span data-stu-id="cfec1-121">If you are using C#, type: `csc form1.cs`</span></span>  
  
         `-or-`  
  
    - <span data-ttu-id="cfec1-122">如果您使用 Visual Basic，請輸入：`vbc form1.vb`</span><span class="sxs-lookup"><span data-stu-id="cfec1-122">If you are using Visual Basic, type: `vbc form1.vb`</span></span>  
  
3. <span data-ttu-id="cfec1-123">在命令提示字元中，輸入：`Form1.exe`</span><span class="sxs-lookup"><span data-stu-id="cfec1-123">At the command prompt, type: `Form1.exe`</span></span>  
  
## <a name="adding-a-control-and-handling-an-event"></a><span data-ttu-id="cfec1-124">加入控制項和處理事件</span><span class="sxs-lookup"><span data-stu-id="cfec1-124">Adding a control and handling an event</span></span>

<span data-ttu-id="cfec1-125">先前的程序步驟示範只是如何建立可編譯和執行的基本 Windows Form。</span><span class="sxs-lookup"><span data-stu-id="cfec1-125">The previous procedure steps demonstrated how to just create a basic Windows Form that compiles and runs.</span></span> <span data-ttu-id="cfec1-126">下一個程序將會說明如何建立控制項並將其加入表單，以及處理控制項的事件。</span><span class="sxs-lookup"><span data-stu-id="cfec1-126">The next procedure will show you how to create and add a control to the form, and handle an event for the control.</span></span> <span data-ttu-id="cfec1-127">如需可加入至 Windows Forms 之控制項的詳細資訊，請參閱[Windows Forms 控制項](./controls/index.md)。</span><span class="sxs-lookup"><span data-stu-id="cfec1-127">For more information about the controls you can add to Windows Forms, see [Windows Forms Controls](./controls/index.md).</span></span>
  
 <span data-ttu-id="cfec1-128">除了了解如何建立 Windows Forms 應用程式，您還應該了解以事件為基礎的程式設計，以及如何處理使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="cfec1-128">In addition to understanding how to create Windows Forms applications, you should understand event-based programming and how to handle user input.</span></span> <span data-ttu-id="cfec1-129">如需詳細資訊，請參閱[在 Windows Forms 中建立事件處理常式](creating-event-handlers-in-windows-forms.md)和[處理使用者輸入](./controls/handling-user-input.md)</span><span class="sxs-lookup"><span data-stu-id="cfec1-129">For more information, see [Creating Event Handlers in Windows Forms](creating-event-handlers-in-windows-forms.md), and [Handling User Input](./controls/handling-user-input.md)</span></span>  
  
#### <a name="to-declare-a-button-control-and-handle-its-click-event"></a><span data-ttu-id="cfec1-130">宣告按鈕控制項及處理其 Click 事件</span><span class="sxs-lookup"><span data-stu-id="cfec1-130">To declare a button control and handle its click event</span></span>  
  
1. <span data-ttu-id="cfec1-131">宣告名為 `button1` 的按鈕控制項。</span><span class="sxs-lookup"><span data-stu-id="cfec1-131">Declare a button control named `button1`.</span></span>  
  
2. <span data-ttu-id="cfec1-132">在建構函式中，建立按鈕，並設定其 <xref:System.Windows.Forms.Control.Size%2A>、<xref:System.Windows.Forms.Control.Location%2A> 和 <xref:System.Windows.Forms.Control.Text%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="cfec1-132">In the constructor, create the button and set its <xref:System.Windows.Forms.Control.Size%2A>, <xref:System.Windows.Forms.Control.Location%2A> and <xref:System.Windows.Forms.Control.Text%2A> properties.</span></span>  
  
3. <span data-ttu-id="cfec1-133">將按鈕加入表單中。</span><span class="sxs-lookup"><span data-stu-id="cfec1-133">Add the button to the form.</span></span>  
  
     <span data-ttu-id="cfec1-134">下列程式碼範例示範如何宣告按鈕控制項：</span><span class="sxs-lookup"><span data-stu-id="cfec1-134">The following code example demonstrates how to declare the button control:</span></span>
  
     [!code-csharp[System.Windows.Forms.FormWithButton#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.FormWithButton#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#2)]  
  
4. <span data-ttu-id="cfec1-135">建立方法來處理按鈕的 <xref:System.Windows.Forms.Control.Click> 事件。</span><span class="sxs-lookup"><span data-stu-id="cfec1-135">Create a method to handle the <xref:System.Windows.Forms.Control.Click> event for the button.</span></span>  
  
5. <span data-ttu-id="cfec1-136">在 Click 事件處理常式中，顯示含有 "Hello World" 訊息的 <xref:System.Windows.Forms.MessageBox>。</span><span class="sxs-lookup"><span data-stu-id="cfec1-136">In the click event handler, display a <xref:System.Windows.Forms.MessageBox> with the message, "Hello World".</span></span>  
  
     <span data-ttu-id="cfec1-137">下列程式碼範例示範如何處理按鈕控制項的 click 事件：</span><span class="sxs-lookup"><span data-stu-id="cfec1-137">The following code example demonstrates how to handle the button control's click event:</span></span>
  
     [!code-csharp[System.Windows.Forms.FormWithButton#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.FormWithButton#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#3)]  
  
6. <span data-ttu-id="cfec1-138">使 <xref:System.Windows.Forms.Control.Click> 事件與您建立的方法產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cfec1-138">Associate the <xref:System.Windows.Forms.Control.Click> event with the method you created.</span></span>  
  
     <span data-ttu-id="cfec1-139">下列程式碼範例會示範如何將事件與方法產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cfec1-139">The following code example demonstrates how to associate the event with the method.</span></span>  
  
     [!code-csharp[System.Windows.Forms.FormWithButton#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.FormWithButton#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#4)]  
  
7. <span data-ttu-id="cfec1-140">依照先前程序的說明，編譯及執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cfec1-140">Compile and run the application as described in the previous procedure.</span></span>  
  
## <a name="example"></a><span data-ttu-id="cfec1-141">範例</span><span class="sxs-lookup"><span data-stu-id="cfec1-141">Example</span></span>  

<span data-ttu-id="cfec1-142">下列程式碼範例是先前程式的完整範例：</span><span class="sxs-lookup"><span data-stu-id="cfec1-142">The following code example is the complete example from the previous procedures:</span></span>
  
 [!code-csharp[System.Windows.Forms.FormWithButton#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.FormWithButton#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FormWithButton/VB/Form1.vb#1)]  
  
## <a name="see-also"></a><span data-ttu-id="cfec1-143">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cfec1-143">See also</span></span>

- <xref:System.Windows.Forms.Form>
- <xref:System.Windows.Forms.Control>
- [<span data-ttu-id="cfec1-144">變更 Windows Form 的外觀</span><span class="sxs-lookup"><span data-stu-id="cfec1-144">Changing the Appearance of Windows Forms</span></span>](changing-the-appearance-of-windows-forms.md)
- [<span data-ttu-id="cfec1-145">增強 Windows Forms 應用程式</span><span class="sxs-lookup"><span data-stu-id="cfec1-145">Enhancing Windows Forms Applications</span></span>](./advanced/index.md)
- [<span data-ttu-id="cfec1-146">使用 Windows Forms 的消費者入門</span><span class="sxs-lookup"><span data-stu-id="cfec1-146">Getting Started with Windows Forms</span></span>](getting-started-with-windows-forms.md)
