---
title: '如何存取 Office interop 物件-c # 程式設計手冊'
description: '深入瞭解可簡化 Office API 物件存取的 c # 功能。 使用新功能來撰寫程式碼，以建立及顯示 Excel 工作表。'
ms.date: 07/20/2015
helpviewer_keywords:
- optional parameters [C#], Office programming
- named and optional arguments [C#], Office programming
- dynamic [C#], Office programming
- optional arguments [C#], Office programming
- named arguments [C#], Office programming
- Office programming [C#]
ms.assetid: 041b25c2-3512-4e0f-a4ea-ceb2999e4d5e
ms.openlocfilehash: bc4b5755bf56a013a0deb4efdb821df18db5a18e
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303019"
---
# <a name="how-to-access-office-interop-objects-c-programming-guide"></a><span data-ttu-id="10bc3-104">如何存取 Office interop 物件（c # 程式設計手冊）</span><span class="sxs-lookup"><span data-stu-id="10bc3-104">How to access Office interop objects (C# Programming Guide)</span></span>

<span data-ttu-id="10bc3-105">C # 具有可簡化 Office API 物件存取的功能。</span><span class="sxs-lookup"><span data-stu-id="10bc3-105">C# has features that simplify access to Office API objects.</span></span> <span data-ttu-id="10bc3-106">新功能包括具名引數和選擇性引數、稱為 `dynamic` 的新類型，以及傳遞引數以像是實值參數的形式，參考 COM 方法中參數的能力。</span><span class="sxs-lookup"><span data-stu-id="10bc3-106">The new features include named and optional arguments, a new type called `dynamic`, and the ability to pass arguments to reference parameters in COM methods as if they were value parameters.</span></span>

<span data-ttu-id="10bc3-107">在本主題中，您將使用新的功能撰寫可建立及顯示 Microsoft Office Excel 工作表的程式碼。</span><span class="sxs-lookup"><span data-stu-id="10bc3-107">In this topic you will use the new features to write code that creates and displays a Microsoft Office Excel worksheet.</span></span> <span data-ttu-id="10bc3-108">接著，您將要撰寫可加入 Office Word 文件的程式碼，而該文件包含連結至 Excel 工作表的圖示。</span><span class="sxs-lookup"><span data-stu-id="10bc3-108">You will then write code to add an Office Word document that contains an icon that is linked to the Excel worksheet.</span></span>

<span data-ttu-id="10bc3-109">若要完成這個逐步解說，電腦上必須安裝 Microsoft Office Excel 2007 和 Microsoft Office Word 2007 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="10bc3-109">To complete this walkthrough, you must have Microsoft Office Excel 2007 and Microsoft Office Word 2007, or later versions, installed on your computer.</span></span>

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-a-new-console-application"></a><span data-ttu-id="10bc3-110">建立新的主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="10bc3-110">To create a new console application</span></span>

1. <span data-ttu-id="10bc3-111">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="10bc3-111">Start Visual Studio.</span></span>

2. <span data-ttu-id="10bc3-112">在 **[檔案]** 功能表上，指向 **[開新檔案]**，然後按一下 **[專案]**。</span><span class="sxs-lookup"><span data-stu-id="10bc3-112">On the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="10bc3-113">[新增專案]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="10bc3-113">The **New Project** dialog box appears.</span></span>

3. <span data-ttu-id="10bc3-114">在 [已安裝的範本]\*\*\*\* 窗格中，展開 [Visual C#]\*\*\*\*，然後按一下 [Windows]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="10bc3-114">In the **Installed Templates** pane, expand **Visual C#**, and then click **Windows**.</span></span>

4. <span data-ttu-id="10bc3-115">查看 [新增專案]\*\*\*\* 對話方塊頂端，確定已選取 [.NET Framework 4]\*\*\*\* (或更新版本) 作為目標架構。</span><span class="sxs-lookup"><span data-stu-id="10bc3-115">Look at the top of the **New Project** dialog box to make sure that **.NET Framework 4** (or later version) is selected as a target framework.</span></span>

5. <span data-ttu-id="10bc3-116">按一下 [範本]\*\*\*\* 窗格中的 [主控台應用程式]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="10bc3-116">In the **Templates** pane, click **Console Application**.</span></span>

6. <span data-ttu-id="10bc3-117">在 [名稱]\*\*\*\* 欄位中鍵入專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="10bc3-117">Type a name for your project in the **Name** field.</span></span>

7. <span data-ttu-id="10bc3-118">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="10bc3-118">Click **OK**.</span></span>

     <span data-ttu-id="10bc3-119">新的專案隨即會出現在方案總管\*\*\*\* 中。</span><span class="sxs-lookup"><span data-stu-id="10bc3-119">The new project appears in **Solution Explorer**.</span></span>

## <a name="to-add-references"></a><span data-ttu-id="10bc3-120">加入參考</span><span class="sxs-lookup"><span data-stu-id="10bc3-120">To add references</span></span>

1. <span data-ttu-id="10bc3-121">在方案總管\*\*\*\* 中，於專案名稱上按一下滑鼠右鍵，然後按一下 [新增參考]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="10bc3-121">In **Solution Explorer**, right-click your project's name and then click **Add Reference**.</span></span> <span data-ttu-id="10bc3-122">[新增參考]\*\*\*\* 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="10bc3-122">The **Add Reference** dialog box appears.</span></span>

2. <span data-ttu-id="10bc3-123">在 [組件]\*\*\*\* 頁面的 [元件名稱]\*\*\*\* 清單中，選取 [Microsoft.Office.Interop.Word]\*\*\*\*，然後按住 CTRL 鍵並選取 [Microsoft.Office.Interop.Excel]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="10bc3-123">On the **Assemblies**  page, select **Microsoft.Office.Interop.Word** in the **Component Name** list, and then hold down the CTRL key and select **Microsoft.Office.Interop.Excel**.</span></span>  <span data-ttu-id="10bc3-124">如果您看不到元件，則可能需要確定它們已安裝並顯示。</span><span class="sxs-lookup"><span data-stu-id="10bc3-124">If you do not see the assemblies, you may need to ensure they are installed and displayed.</span></span> <span data-ttu-id="10bc3-125">請參閱[如何：安裝 Office 主要 Interop 元件](/visualstudio/vsto/how-to-install-office-primary-interop-assemblies)。</span><span class="sxs-lookup"><span data-stu-id="10bc3-125">See [How to: Install Office Primary Interop Assemblies](/visualstudio/vsto/how-to-install-office-primary-interop-assemblies).</span></span>

3. <span data-ttu-id="10bc3-126">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="10bc3-126">Click **OK**.</span></span>

## <a name="to-add-necessary-using-directives"></a><span data-ttu-id="10bc3-127">加入必要的 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="10bc3-127">To add necessary using directives</span></span>

1. <span data-ttu-id="10bc3-128">在方案總管\*\*\*\* 中，以滑鼠右鍵按一下 *Program.cs* 檔案，然後按一下 [檢視程式碼]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="10bc3-128">In **Solution Explorer**, right-click the *Program.cs* file and then click **View Code**.</span></span>

2. <span data-ttu-id="10bc3-129">將下列指示詞新增 `using` 至程式碼檔案的頂端：</span><span class="sxs-lookup"><span data-stu-id="10bc3-129">Add the following `using` directives to the top of the code file:</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#1)]

## <a name="to-create-a-list-of-bank-accounts"></a><span data-ttu-id="10bc3-130">建立銀行帳戶清單</span><span class="sxs-lookup"><span data-stu-id="10bc3-130">To create a list of bank accounts</span></span>

1. <span data-ttu-id="10bc3-131">將下列類別定義貼入 `Program` 類別下的 **Program.cs**。</span><span class="sxs-lookup"><span data-stu-id="10bc3-131">Paste the following class definition into **Program.cs**, under the `Program` class.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#2)]

2. <span data-ttu-id="10bc3-132">將下列程式碼加入 `Main` 方法，以建立含有兩個帳戶的 `bankAccounts` 清單。</span><span class="sxs-lookup"><span data-stu-id="10bc3-132">Add the following code to the `Main` method to create a `bankAccounts` list that contains two accounts.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#3)]

## <a name="to-declare-a-method-that-exports-account-information-to-excel"></a><span data-ttu-id="10bc3-133">宣告將帳戶資訊匯出至 Excel 的方法</span><span class="sxs-lookup"><span data-stu-id="10bc3-133">To declare a method that exports account information to Excel</span></span>

1. <span data-ttu-id="10bc3-134">將下列方法加入 `Program` 類別，以設定 Excel 試算表。</span><span class="sxs-lookup"><span data-stu-id="10bc3-134">Add the following method to the `Program` class to set up an Excel worksheet.</span></span>

     <span data-ttu-id="10bc3-135"><xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> 方法有用以指定特定範本的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-135">Method <xref:Microsoft.Office.Interop.Excel.Workbooks.Add%2A> has an optional parameter for specifying a particular template.</span></span> <span data-ttu-id="10bc3-136">如果您想要使用參數的預設值，則可利用選擇性參數 (C# 4 中的新功能) 省略該參數的引數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-136">Optional parameters, new in C# 4, enable you to omit the argument for that parameter if you want to use the parameter's default value.</span></span> <span data-ttu-id="10bc3-137">因為下列程式碼中未傳送引數，所以 `Add` 使用預設範本並建立新的活頁簿。</span><span class="sxs-lookup"><span data-stu-id="10bc3-137">Because no argument is sent in the following code, `Add` uses the default template and creates a new workbook.</span></span> <span data-ttu-id="10bc3-138">舊版 C# 中對等的陳述式需要有預留位置引數：`ExcelApp.Workbooks.Add(Type.Missing)`。</span><span class="sxs-lookup"><span data-stu-id="10bc3-138">The equivalent statement in earlier versions of C# requires a placeholder argument: `ExcelApp.Workbooks.Add(Type.Missing)`.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#4)]

2. <span data-ttu-id="10bc3-139">在 `DisplayInExcel` 結尾，加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="10bc3-139">Add the following code at the end of `DisplayInExcel`.</span></span> <span data-ttu-id="10bc3-140">程式碼會將值插入工作表第一個資料列的前兩個資料行。</span><span class="sxs-lookup"><span data-stu-id="10bc3-140">The code inserts values into the first two columns of the first row of the worksheet.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#5)]

3. <span data-ttu-id="10bc3-141">在 `DisplayInExcel` 結尾，加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="10bc3-141">Add the following code at the end of `DisplayInExcel`.</span></span> <span data-ttu-id="10bc3-142">`foreach` 迴圈會將帳戶清單中的資訊，放入工作表連續資料列的前兩個資料行。</span><span class="sxs-lookup"><span data-stu-id="10bc3-142">The `foreach` loop puts the information from the list of accounts into the first two columns of successive rows of the worksheet.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#7)]

4. <span data-ttu-id="10bc3-143">在 `DisplayInExcel` 結尾加入下列程式碼，以調整資料行寬度以容納內容。</span><span class="sxs-lookup"><span data-stu-id="10bc3-143">Add the following code at the end of `DisplayInExcel` to adjust the column widths to fit the content.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#13)]

     <span data-ttu-id="10bc3-144">因為 `ExcelApp.Columns[1]` 會傳回 `Object`，所以舊版 C# 需要明確轉換這些作業，而 `AutoFit` 是 Excel <xref:Microsoft.Office.Interop.Excel.Range> 方法。</span><span class="sxs-lookup"><span data-stu-id="10bc3-144">Earlier versions of C# require explicit casting for these operations because `ExcelApp.Columns[1]` returns an `Object`, and `AutoFit` is an Excel <xref:Microsoft.Office.Interop.Excel.Range> method.</span></span> <span data-ttu-id="10bc3-145">下列各行會顯示轉型。</span><span class="sxs-lookup"><span data-stu-id="10bc3-145">The following lines show the casting.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#14)]

     <span data-ttu-id="10bc3-146">C # 4 和更新版本會將傳回的轉換 `Object` 為， `dynamic` 如果元件是由[-link](../../language-reference/compiler-options/link-compiler-option.md)編譯器選項所參考，或者如果 [Excel**內嵌 Interop 類型**] 屬性設定為 true，則會使用同等的方式。</span><span class="sxs-lookup"><span data-stu-id="10bc3-146">C# 4, and later versions, converts the returned `Object` to `dynamic` automatically if the assembly is referenced by the [-link](../../language-reference/compiler-options/link-compiler-option.md) compiler option or, equivalently, if the Excel **Embed Interop Types** property is set to true.</span></span> <span data-ttu-id="10bc3-147">這個屬性的預設值為 True。</span><span class="sxs-lookup"><span data-stu-id="10bc3-147">True is the default value for this property.</span></span>

## <a name="to-run-the-project"></a><span data-ttu-id="10bc3-148">執行專案</span><span class="sxs-lookup"><span data-stu-id="10bc3-148">To run the project</span></span>

1. <span data-ttu-id="10bc3-149">在 `Main` 結尾，加入下行。</span><span class="sxs-lookup"><span data-stu-id="10bc3-149">Add the following line at the end of `Main`.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#8)]

2. <span data-ttu-id="10bc3-150">按下 CTRL+F5。</span><span class="sxs-lookup"><span data-stu-id="10bc3-150">Press CTRL+F5.</span></span>

     <span data-ttu-id="10bc3-151">隨即會出現內含兩個帳戶資料的 Excel 工作表。</span><span class="sxs-lookup"><span data-stu-id="10bc3-151">An Excel worksheet appears that contains the data from the two accounts.</span></span>

## <a name="to-add-a-word-document"></a><span data-ttu-id="10bc3-152">加入 Word 文件</span><span class="sxs-lookup"><span data-stu-id="10bc3-152">To add a Word document</span></span>

1. <span data-ttu-id="10bc3-153">為了說明 C# 4 和更新版本中加強 Office 程式設計的其他方法，下列程式碼會開啟 Word 應用程式，並建立 Excel 工作表連結的圖示。</span><span class="sxs-lookup"><span data-stu-id="10bc3-153">To illustrate additional ways in which C# 4, and later versions, enhances Office programming, the following code opens a Word application and creates an icon that links to the Excel worksheet.</span></span>

     <span data-ttu-id="10bc3-154">將本步驟稍後提供的 `CreateIconInWordDoc` 方法，貼入 `Program` 類別。</span><span class="sxs-lookup"><span data-stu-id="10bc3-154">Paste method `CreateIconInWordDoc`, provided later in this step, into the `Program` class.</span></span> <span data-ttu-id="10bc3-155">`CreateIconInWordDoc` 使用具名和選擇性引數來降低 <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> 和 <xref:Microsoft.Office.Interop.Word.Selection.PasteSpecial%2A> 方法呼叫的複雜性。</span><span class="sxs-lookup"><span data-stu-id="10bc3-155">`CreateIconInWordDoc` uses named and optional arguments to reduce the complexity of the method calls to <xref:Microsoft.Office.Interop.Word.Documents.Add%2A> and <xref:Microsoft.Office.Interop.Word.Selection.PasteSpecial%2A>.</span></span> <span data-ttu-id="10bc3-156">這些呼叫採用 C# 4 引進的兩個其他新功能，簡化了具有參考參數之 COM 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="10bc3-156">These calls incorporate two other new features introduced in C# 4 that simplify calls to COM methods that have reference parameters.</span></span> <span data-ttu-id="10bc3-157">首先，您可以將引數以實值參數的形式傳送到參考參數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-157">First, you can send arguments to the reference parameters as if they were value parameters.</span></span> <span data-ttu-id="10bc3-158">也就是說，可以直接傳送值而無須建立每個參考參數的變數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-158">That is, you can send values directly, without creating a variable for each reference parameter.</span></span> <span data-ttu-id="10bc3-159">編譯器會產生暫存變數來保存引數值，並在從呼叫返回時捨棄變數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-159">The compiler generates temporary variables to hold the argument values, and discards the variables when you return from the call.</span></span> <span data-ttu-id="10bc3-160">其次，您可以省略引數清單中的 `ref` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="10bc3-160">Second, you can omit the `ref` keyword in the argument list.</span></span>

     <span data-ttu-id="10bc3-161">`Add` 方法有四個參考參數，而且都是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-161">The `Add` method has four reference parameters, all of which are optional.</span></span> <span data-ttu-id="10bc3-162">在 C# 4.0 與更新版本中，如果想要使用其預設值，可以省略任何或所有參數的引數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-162">In C# 4.0 and later versions, you can omit arguments for any or all of the parameters if you want to use their default values.</span></span> <span data-ttu-id="10bc3-163">在 C# 3.0與舊版中，必須為每個參數提供引數，且引數必須是變數，因為參數是參考參數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-163">In C# 3.0 and earlier versions, an argument must be provided for each parameter, and the argument must be a variable because the parameters are reference parameters.</span></span>

     <span data-ttu-id="10bc3-164">`PasteSpecial` 方法會將內容插入剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="10bc3-164">The `PasteSpecial` method inserts the contents of the Clipboard.</span></span> <span data-ttu-id="10bc3-165">此方法有七個參考參數，且都是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-165">The method has seven reference parameters, all of which are optional.</span></span> <span data-ttu-id="10bc3-166">下列程式碼指定其中兩個的引數：`Link` 可建立剪貼簿的內容的來源連結，以及 `DisplayAsIcon` 可將連結顯示為圖示。</span><span class="sxs-lookup"><span data-stu-id="10bc3-166">The following code specifies arguments for two of them: `Link`, to create a link to the source of the Clipboard contents, and `DisplayAsIcon`, to display the link as an icon.</span></span> <span data-ttu-id="10bc3-167">在 C# 4.0 與更新版本中，可以為這兩者使用具名引數，並省略其他引數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-167">In C# 4.0 and later versions, you can use named arguments for those two and omit the others.</span></span> <span data-ttu-id="10bc3-168">雖然這些是參考參數，但是您不需要使用 `ref` 關鍵字，或建立傳送為引數的變數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-168">Although these are reference parameters, you do not have to use the `ref` keyword, or to create variables to send in as arguments.</span></span> <span data-ttu-id="10bc3-169">可以直接傳送值。</span><span class="sxs-lookup"><span data-stu-id="10bc3-169">You can send the values directly.</span></span> <span data-ttu-id="10bc3-170">在 C# 3.0 舊版中，必須為每個參考參數提供變數引數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-170">In C# 3.0 and earlier versions, you must supply a variable argument for each reference parameter.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#9)]

     <span data-ttu-id="10bc3-171">在 C# 3.0 與舊版語言中，需要有下列更為複雜的程式碼。</span><span class="sxs-lookup"><span data-stu-id="10bc3-171">In C# 3.0 and earlier versions of the language, the following more complex code is required.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#10)]

2. <span data-ttu-id="10bc3-172">在 `Main` 結尾，加入下列陳述式。</span><span class="sxs-lookup"><span data-stu-id="10bc3-172">Add the following statement at the end of `Main`.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#11)]

3. <span data-ttu-id="10bc3-173">在 `DisplayInExcel` 結尾，加入下列陳述式。</span><span class="sxs-lookup"><span data-stu-id="10bc3-173">Add the following statement at the end of `DisplayInExcel`.</span></span> <span data-ttu-id="10bc3-174">`Copy` 方法會將工作表加入剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="10bc3-174">The `Copy` method adds the worksheet to the Clipboard.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#12)]

4. <span data-ttu-id="10bc3-175">按下 CTRL+F5。</span><span class="sxs-lookup"><span data-stu-id="10bc3-175">Press CTRL+F5.</span></span>

     <span data-ttu-id="10bc3-176">隨即會出現含有圖示的 Word 文件。</span><span class="sxs-lookup"><span data-stu-id="10bc3-176">A Word document appears that contains an icon.</span></span> <span data-ttu-id="10bc3-177">按兩下圖示，即可將該工作表帶到前景。</span><span class="sxs-lookup"><span data-stu-id="10bc3-177">Double-click the icon to bring the worksheet to the foreground.</span></span>

## <a name="to-set-the-embed-interop-types-property"></a><span data-ttu-id="10bc3-178">設定內嵌 Interop 類型屬性</span><span class="sxs-lookup"><span data-stu-id="10bc3-178">To set the Embed Interop Types property</span></span>

1. <span data-ttu-id="10bc3-179">當您在執行階段呼叫不需要主要 Interop 組件 (PIA) 的 COM 類型時，可以使用其他增強功能。</span><span class="sxs-lookup"><span data-stu-id="10bc3-179">Additional enhancements are possible when you call a COM type that does not require a primary interop assembly (PIA) at run time.</span></span> <span data-ttu-id="10bc3-180">移除與 PIA 的相依性，可達成版本獨立且更容易進行部署。</span><span class="sxs-lookup"><span data-stu-id="10bc3-180">Removing the dependency on PIAs results in version independence and easier deployment.</span></span> <span data-ttu-id="10bc3-181">如需沒有 PIA 的程式設計優點的詳細資訊，請參閱[逐步解說：從 Managed 組件內嵌類型](../../../standard/assembly/embed-types-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="10bc3-181">For more information about the advantages of programming without PIAs, see [Walkthrough: Embedding Types from Managed Assemblies](../../../standard/assembly/embed-types-visual-studio.md).</span></span>

     <span data-ttu-id="10bc3-182">此外，程式設計會更為容易，因為 COM 方法所需和所傳回的類型可以使用類型 `dynamic` 而非 `Object` 加以呈現。</span><span class="sxs-lookup"><span data-stu-id="10bc3-182">In addition, programming is easier because the types that are required and returned by COM methods can be represented by using the type `dynamic` instead of `Object`.</span></span> <span data-ttu-id="10bc3-183">除非處於執行階段，否則不會評估類型為 `dynamic` 的變數，如此即無須明確轉型。</span><span class="sxs-lookup"><span data-stu-id="10bc3-183">Variables that have type `dynamic` are not evaluated until run time, which eliminates the need for explicit casting.</span></span> <span data-ttu-id="10bc3-184">如需詳細資訊，請參閱[使用動態類型](../types/using-type-dynamic.md)。</span><span class="sxs-lookup"><span data-stu-id="10bc3-184">For more information, see [Using Type dynamic](../types/using-type-dynamic.md).</span></span>

     <span data-ttu-id="10bc3-185">在 C# 4 中，預設行為是內嵌型別資訊，而非使用 PIA。</span><span class="sxs-lookup"><span data-stu-id="10bc3-185">In C# 4, embedding type information instead of using PIAs is default behavior.</span></span> <span data-ttu-id="10bc3-186">因為使用該預設值，已簡化了數個先前的範例，因為明確轉型已非必要。</span><span class="sxs-lookup"><span data-stu-id="10bc3-186">Because of that default, several of the previous examples are simplified because explicit casting is not required.</span></span> <span data-ttu-id="10bc3-187">例如，`worksheet` 中的 `DisplayInExcel` 宣告，撰寫為 `Excel._Worksheet workSheet = excelApp.ActiveSheet`，而非 `Excel._Worksheet workSheet = (Excel.Worksheet)excelApp.ActiveSheet`。</span><span class="sxs-lookup"><span data-stu-id="10bc3-187">For example, the declaration of `worksheet` in `DisplayInExcel` is written as `Excel._Worksheet workSheet = excelApp.ActiveSheet` rather than `Excel._Worksheet workSheet = (Excel.Worksheet)excelApp.ActiveSheet`.</span></span> <span data-ttu-id="10bc3-188">如果沒有預設值，則相同方法中的 `AutoFit` 呼叫也需要明確轉型，因為 `ExcelApp.Columns[1]` 會傳回 `Object`，而 `AutoFit` 是 Excel 方法。</span><span class="sxs-lookup"><span data-stu-id="10bc3-188">The calls to `AutoFit` in the same method also would require explicit casting without the default, because `ExcelApp.Columns[1]` returns an `Object`, and `AutoFit` is an Excel  method.</span></span> <span data-ttu-id="10bc3-189">下列程式碼會顯示轉型。</span><span class="sxs-lookup"><span data-stu-id="10bc3-189">The following code shows the casting.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#14)]

2. <span data-ttu-id="10bc3-190">若要變更預設值，並使用 PIA 而非內嵌類型資訊，請展開方案總管\*\*\*\* 中的 [參考]\*\*\*\* 節點，然後選取 **Microsoft.Office.Interop.Excel** 或 **Microsoft.Office.Interop.Word**。</span><span class="sxs-lookup"><span data-stu-id="10bc3-190">To change the default and use PIAs instead of embedding type information, expand the **References** node in **Solution Explorer** and then select **Microsoft.Office.Interop.Excel** or **Microsoft.Office.Interop.Word**.</span></span>

3. <span data-ttu-id="10bc3-191">如果看不到 [屬性]\*\*\*\* 視窗，請按 **F4** 鍵。</span><span class="sxs-lookup"><span data-stu-id="10bc3-191">If you cannot see the **Properties** window, press **F4**.</span></span>

4. <span data-ttu-id="10bc3-192">在屬性清單中尋找 [內嵌 Interop 類型]\*\*\*\*，並將其值變更為 **False**。</span><span class="sxs-lookup"><span data-stu-id="10bc3-192">Find **Embed Interop Types** in the list of properties, and change its value to **False**.</span></span> <span data-ttu-id="10bc3-193">同樣地，您可以在命令提示字元中使用[-reference](../../language-reference/compiler-options/reference-compiler-option.md)編譯器選項，而不是[-link](../../language-reference/compiler-options/link-compiler-option.md)來進行編譯。</span><span class="sxs-lookup"><span data-stu-id="10bc3-193">Equivalently, you can compile by using the [-reference](../../language-reference/compiler-options/reference-compiler-option.md) compiler option instead of [-link](../../language-reference/compiler-options/link-compiler-option.md) at a command prompt.</span></span>

## <a name="to-add-additional-formatting-to-the-table"></a><span data-ttu-id="10bc3-194">加入表格的其他格式</span><span class="sxs-lookup"><span data-stu-id="10bc3-194">To add additional formatting to the table</span></span>

1. <span data-ttu-id="10bc3-195">將 `AutoFit` 中對兩個 `DisplayInExcel` 的呼叫，取代為下列陳述式。</span><span class="sxs-lookup"><span data-stu-id="10bc3-195">Replace the two calls to `AutoFit` in `DisplayInExcel` with the following statement.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#15)]

     <span data-ttu-id="10bc3-196">這個方法 <xref:Microsoft.Office.Interop.Excel.Range.AutoFormat%2A> 有七個值參數，全部都是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-196">The <xref:Microsoft.Office.Interop.Excel.Range.AutoFormat%2A> method has seven value parameters, all of which are optional.</span></span> <span data-ttu-id="10bc3-197">您可利用具名引數和選擇性引數，提供零個引數、數個引數或所有引數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-197">Named and optional arguments enable you to provide arguments for none, some, or all of them.</span></span> <span data-ttu-id="10bc3-198">在前述陳述式中，只為其中一個參數 (`Format`) 提供引數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-198">In the previous statement, an argument is supplied for only one of the parameters, `Format`.</span></span> <span data-ttu-id="10bc3-199">因為 `Format` 是參數清單中的第一個參數，所以無須提供參數名稱。</span><span class="sxs-lookup"><span data-stu-id="10bc3-199">Because `Format` is the first parameter in the parameter list, you do not have to provide the parameter name.</span></span> <span data-ttu-id="10bc3-200">但如果包含參數名稱，則可能較容易了解該陳述式，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="10bc3-200">However, the statement might be easier to understand if the parameter name is included, as is shown in the following code.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#16)]

2. <span data-ttu-id="10bc3-201">按 CTRL + F5 鍵查看結果。</span><span class="sxs-lookup"><span data-stu-id="10bc3-201">Press CTRL+F5 to see the result.</span></span> <span data-ttu-id="10bc3-202">其他格式會列在 <xref:Microsoft.Office.Interop.Excel.XlRangeAutoFormat> 列舉中。</span><span class="sxs-lookup"><span data-stu-id="10bc3-202">Other formats are listed in the <xref:Microsoft.Office.Interop.Excel.XlRangeAutoFormat> enumeration.</span></span>

3. <span data-ttu-id="10bc3-203">請比較步驟 1 中的陳述式與下列程式碼，這樣會顯示 C# 3.0 或舊版中所需的引數。</span><span class="sxs-lookup"><span data-stu-id="10bc3-203">Compare the statement in step 1 with the following code, which shows the arguments that are required in C# 3.0 and earlier versions.</span></span>

     [!code-csharp[csProgGuideOfficeHowTo#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/program.cs#17)]

## <a name="example"></a><span data-ttu-id="10bc3-204">範例</span><span class="sxs-lookup"><span data-stu-id="10bc3-204">Example</span></span>

<span data-ttu-id="10bc3-205">下列程式碼顯示完整範例。</span><span class="sxs-lookup"><span data-stu-id="10bc3-205">The following code shows the complete example.</span></span>

[!code-csharp[csProgGuideOfficeHowTo#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideofficehowto/cs/walkthrough.cs#18)]

## <a name="see-also"></a><span data-ttu-id="10bc3-206">另請參閱</span><span class="sxs-lookup"><span data-stu-id="10bc3-206">See also</span></span>

- <xref:System.Type.Missing?displayProperty=nameWithType>
- [<span data-ttu-id="10bc3-207">動態</span><span class="sxs-lookup"><span data-stu-id="10bc3-207">dynamic</span></span>](../../language-reference/builtin-types/reference-types.md)
- [<span data-ttu-id="10bc3-208">使用動態類型</span><span class="sxs-lookup"><span data-stu-id="10bc3-208">Using Type dynamic</span></span>](../types/using-type-dynamic.md)
- [<span data-ttu-id="10bc3-209">具名和選擇性引數</span><span class="sxs-lookup"><span data-stu-id="10bc3-209">Named and Optional Arguments</span></span>](../classes-and-structs/named-and-optional-arguments.md)
- [<span data-ttu-id="10bc3-210">如何在 Office 程式設計中使用具名和選擇性引數</span><span class="sxs-lookup"><span data-stu-id="10bc3-210">How to use named and optional arguments in Office programming</span></span>](../classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)
