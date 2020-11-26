---
title: 編碼慣例
ms.date: 07/20/2015
helpviewer_keywords:
- coding conventions [Visual Basic], Visual Basic
- examples [Visual Basic], coding conventions
- Visual Basic code, conventions
ms.assetid: c1df130b-fec6-49a5-becf-0a7e494a1d0f
ms.openlocfilehash: eae283c757ddeb1290c15d82a41c8028a8941e63
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91059154"
---
# <a name="visual-basic-coding-conventions"></a><span data-ttu-id="ca2b4-102">Visual Basic 編碼慣例</span><span class="sxs-lookup"><span data-stu-id="ca2b4-102">Visual Basic Coding Conventions</span></span>

<span data-ttu-id="ca2b4-103">Microsoft 會依照本主題中的指導方針來開發範例與檔。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-103">Microsoft develops samples and documentation that follow the guidelines in this topic.</span></span> <span data-ttu-id="ca2b4-104">如果您遵循相同的程式碼撰寫慣例，您可能會獲得下列優點：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-104">If you follow the same coding conventions, you may gain the following benefits:</span></span>  
  
- <span data-ttu-id="ca2b4-105">您的程式碼會有一致的外觀，讓讀者可以更專注于內容，而不是版面配置。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-105">Your code will have a consistent look, so that readers can better focus on content, not layout.</span></span>  
  
- <span data-ttu-id="ca2b4-106">讀者可以更快速地瞭解您的程式碼，因為它們可以根據先前的經驗進行假設。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-106">Readers understand your code more quickly because they can make assumptions based on previous experience.</span></span>  
  
- <span data-ttu-id="ca2b4-107">您可以更輕鬆地複製、變更和維護程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-107">You can copy, change, and maintain the code more easily.</span></span>  
  
- <span data-ttu-id="ca2b4-108">您可以協助確保您的程式碼會示範 Visual Basic 的「最佳作法」。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-108">You help ensure that your code demonstrates "best practices" for Visual Basic.</span></span>  
  
## <a name="naming-conventions"></a><span data-ttu-id="ca2b4-109">命名規範</span><span class="sxs-lookup"><span data-stu-id="ca2b4-109">Naming Conventions</span></span>  
  
- <span data-ttu-id="ca2b4-110">如需命名方針的詳細資訊，請參閱 [命名指導方針](../../../standard/design-guidelines/naming-guidelines.md) 主題。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-110">For information about naming guidelines, see [Naming Guidelines](../../../standard/design-guidelines/naming-guidelines.md) topic.</span></span>  
  
- <span data-ttu-id="ca2b4-111">請勿使用 "My" 或 "my" 作為變數名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-111">Do not use "My" or "my" as part of a variable name.</span></span> <span data-ttu-id="ca2b4-112">這種作法會與物件產生混淆 `My` 。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-112">This practice creates confusion with the `My` objects.</span></span>  
  
- <span data-ttu-id="ca2b4-113">您不需要在自動產生的程式碼中變更物件的名稱，使其符合指導方針。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-113">You do not have to change the names of objects in auto-generated code to make them fit the guidelines.</span></span>  
  
## <a name="layout-conventions"></a><span data-ttu-id="ca2b4-114">版面配置慣例</span><span class="sxs-lookup"><span data-stu-id="ca2b4-114">Layout Conventions</span></span>  
  
- <span data-ttu-id="ca2b4-115">以空格插入索引標籤，並使用具有四個空格縮排的智慧縮排。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-115">Insert tabs as spaces, and use smart indenting with four-space indents.</span></span>  
  
- <span data-ttu-id="ca2b4-116">使用 **整齊的清單 (重新格式化程式碼)** ，以在程式碼編輯器中重新格式化您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-116">Use **Pretty listing (reformatting) of code** to reformat your code in the code editor.</span></span> <span data-ttu-id="ca2b4-117">如需詳細資訊，請參閱 [ [選項]、[文字編輯器]、[基本 (Visual Basic) ](/visualstudio/ide/reference/options-text-editor-basic-visual-basic)。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-117">For more information, see [Options, Text Editor, Basic (Visual Basic)](/visualstudio/ide/reference/options-text-editor-basic-visual-basic).</span></span>  
  
- <span data-ttu-id="ca2b4-118">每行只能使用一個語句。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-118">Use only one statement per line.</span></span> <span data-ttu-id="ca2b4-119">請勿使用 Visual Basic 行分隔字元 (： ) 。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-119">Don't use the Visual Basic line separator character (:).</span></span>  
  
- <span data-ttu-id="ca2b4-120">在語言允許的任何地方，請避免使用明確的行接續字元 "_" 來取代隱含行接續。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-120">Avoid using the explicit line continuation character "_" in favor of implicit line continuation wherever the language allows it.</span></span>  
  
- <span data-ttu-id="ca2b4-121">每行只能使用一個宣告。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-121">Use only one declaration per line.</span></span>  
  
- <span data-ttu-id="ca2b4-122">如果有很多 **的 (重新格式化) 的程式碼** 並不會自動將接續行格式化，請以手動方式將接續行縮排一次</span><span class="sxs-lookup"><span data-stu-id="ca2b4-122">If **Pretty listing (reformatting) of code** doesn't format continuation lines automatically, manually indent continuation lines one tab stop.</span></span> <span data-ttu-id="ca2b4-123">不過，一律會將清單中的專案靠左對齊。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-123">However, always left-align items in a list.</span></span>  
  
    ```vb  
    a As Integer,  
    b As Integer  
    ```  
  
- <span data-ttu-id="ca2b4-124">在方法與屬性定義之間加入至少一個空白行。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-124">Add at least one blank line between method and property definitions.</span></span>  
  
## <a name="commenting-conventions"></a><span data-ttu-id="ca2b4-125">註解慣例</span><span class="sxs-lookup"><span data-stu-id="ca2b4-125">Commenting Conventions</span></span>  
  
- <span data-ttu-id="ca2b4-126">將批註放在不同的行，而不是程式程式碼的結尾。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-126">Put comments on a separate line instead of at the end of a line of code.</span></span>  
  
- <span data-ttu-id="ca2b4-127">使用大寫字母來開始註解文字，並以句點結束註解文字。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-127">Start comment text with an uppercase letter, and end comment text with a period.</span></span>  
  
- <span data-ttu-id="ca2b4-128">在批註分隔符號 ( ' ) 和註解文字之間插入一個空格。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-128">Insert one space between the comment delimiter (') and the comment text.</span></span>  
  
     [!code-vb[VbVbalrGuidelines#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#2)]  
  
- <span data-ttu-id="ca2b4-129">請勿以星號的格式化區塊括住批註。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-129">Do not surround comments with formatted blocks of asterisks.</span></span>  
  
## <a name="program-structure"></a><span data-ttu-id="ca2b4-130">程式結構</span><span class="sxs-lookup"><span data-stu-id="ca2b4-130">Program Structure</span></span>  
  
- <span data-ttu-id="ca2b4-131">當您使用 `Main` 方法時，請使用新的主控台應用程式的預設結構，並使用做 `My` 為命令列引數。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-131">When you use the `Main` method, use the default construct for new console applications, and use `My` for command-line arguments.</span></span>  
  
     [!code-vb[VbVbalrGuidelines#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#3)]  
  
## <a name="language-guidelines"></a><span data-ttu-id="ca2b4-132">語言指導方針</span><span class="sxs-lookup"><span data-stu-id="ca2b4-132">Language Guidelines</span></span>  
  
### <a name="string-data-type"></a><span data-ttu-id="ca2b4-133">String 資料類型</span><span class="sxs-lookup"><span data-stu-id="ca2b4-133">String Data Type</span></span>  
  
- <span data-ttu-id="ca2b4-134">使用[字串內插補點](../language-features/strings/interpolated-strings.md)串連短字串，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-134">Use [string interpolation](../language-features/strings/interpolated-strings.md) to concatenate short strings, as shown in the following code.</span></span>
  
     ```vb
     MsgBox($"hello{vbCrLf}goodbye")
     ```
  
- <span data-ttu-id="ca2b4-135">若要在迴圈中附加字串，請使用 <xref:System.Text.StringBuilder> 物件。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-135">To append strings in loops, use the <xref:System.Text.StringBuilder> object.</span></span>  
  
     [!code-vb[VbVbalrGuidelines#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#5)]  
  
### <a name="relaxed-delegates-in-event-handlers"></a><span data-ttu-id="ca2b4-136">事件處理常式中寬鬆的委派</span><span class="sxs-lookup"><span data-stu-id="ca2b4-136">Relaxed Delegates in Event Handlers</span></span>  

 <span data-ttu-id="ca2b4-137">請勿明確限定引數 (物件和 EventArgs) 至事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-137">Do not explicitly qualify the arguments (Object and EventArgs) to event handlers.</span></span> <span data-ttu-id="ca2b4-138">如果您不是使用傳遞至事件的事件引數 (例如，傳送者為物件、e 表示 EventArgs) ，請使用寬鬆的委派，並在程式碼中省略事件引數：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-138">If you are not using the event arguments that are passed to an event (for example, sender as Object, e as EventArgs), use relaxed delegates, and leave out the event arguments in your code:</span></span>  
  
 [!code-vb[VbVbalrGuidelines#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#7)]  
  
### <a name="unsigned-data-type"></a><span data-ttu-id="ca2b4-139">不帶正負號的資料類型</span><span class="sxs-lookup"><span data-stu-id="ca2b4-139">Unsigned Data Type</span></span>  
  
- <span data-ttu-id="ca2b4-140">使用 `Integer` 而非不帶正負號的類型，但不含符號類型。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-140">Use `Integer` rather than unsigned types, except where they are necessary.</span></span>  
  
### <a name="arrays"></a><span data-ttu-id="ca2b4-141">陣列</span><span class="sxs-lookup"><span data-stu-id="ca2b4-141">Arrays</span></span>  
  
- <span data-ttu-id="ca2b4-142">當您在宣告行上初始化陣列時，請使用簡短的語法。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-142">Use the short syntax when you initialize arrays on the declaration line.</span></span> <span data-ttu-id="ca2b4-143">例如，請使用下列語法。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-143">For example, use the following syntax.</span></span>  
  
     [!code-vb[VbVbalrGuidelines#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#8)]  
  
     <span data-ttu-id="ca2b4-144">請勿使用下列語法。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-144">Do not use the following syntax.</span></span>  
  
     [!code-vb[VbVbalrGuidelines#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#9)]  
  
- <span data-ttu-id="ca2b4-145">將陣列指示項放在型別上，而不是變數上。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-145">Put the array designator on the type, not on the variable.</span></span> <span data-ttu-id="ca2b4-146">例如，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-146">For example, use the following syntax:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#11)]  
  
     <span data-ttu-id="ca2b4-147">請勿使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-147">Do not use the following syntax:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#10)]  
  
- <span data-ttu-id="ca2b4-148">當您宣告並初始化基本資料類型的陣列時，請使用 {} 語法。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-148">Use the { } syntax when you declare and initialize arrays of basic data types.</span></span> <span data-ttu-id="ca2b4-149">例如，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-149">For example, use the following syntax:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#12)]  
  
     <span data-ttu-id="ca2b4-150">請勿使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-150">Do not use the following syntax:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#13)]  
  
### <a name="use-the-with-keyword"></a><span data-ttu-id="ca2b4-151">使用 With 關鍵字</span><span class="sxs-lookup"><span data-stu-id="ca2b4-151">Use the With Keyword</span></span>  

 <span data-ttu-id="ca2b4-152">當您對一個物件進行一連串的呼叫時，請考慮使用 `With` 關鍵字：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-152">When you make a series of calls to one object, consider using the `With` keyword:</span></span>  
  
 [!code-vb[VbVbalrGuidelines#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#15)]  
  
### <a name="use-the-trycatch-and-using-statements-when-you-use-exception-handling"></a><span data-ttu-id="ca2b4-153">使用 Try .。。當您使用例外狀況處理時的 Catch 和 Using 語句</span><span class="sxs-lookup"><span data-stu-id="ca2b4-153">Use the Try...Catch and Using Statements when you use Exception Handling</span></span>  

 <span data-ttu-id="ca2b4-154">請勿使用 `On Error Goto`。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-154">Do not use `On Error Goto`.</span></span>  
  
### <a name="use-the-isnot-keyword"></a><span data-ttu-id="ca2b4-155">使用 IsNot 關鍵字</span><span class="sxs-lookup"><span data-stu-id="ca2b4-155">Use the IsNot Keyword</span></span>  

 <span data-ttu-id="ca2b4-156">使用 `IsNot` 關鍵字而不是 `Not...Is Nothing` 。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-156">Use the `IsNot` keyword instead of `Not...Is Nothing`.</span></span>  
  
### <a name="new-keyword"></a><span data-ttu-id="ca2b4-157">New 關鍵字</span><span class="sxs-lookup"><span data-stu-id="ca2b4-157">New Keyword</span></span>  
  
- <span data-ttu-id="ca2b4-158">使用簡短具現化。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-158">Use short instantiation.</span></span> <span data-ttu-id="ca2b4-159">例如，請使用下列語法：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-159">For example, use the following syntax:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#21)]  
  
     <span data-ttu-id="ca2b4-160">上述程式程式碼相當於：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-160">The preceding line is equivalent to this:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#22)]  
  
- <span data-ttu-id="ca2b4-161">針對新物件使用物件初始化運算式，而不是無參數的函式：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-161">Use object initializers for new objects instead of the parameterless constructor:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#23)]  
  
### <a name="event-handling"></a><span data-ttu-id="ca2b4-162">事件處理</span><span class="sxs-lookup"><span data-stu-id="ca2b4-162">Event Handling</span></span>  
  
- <span data-ttu-id="ca2b4-163">使用 `Handles` 而不是 `AddHandler` ：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-163">Use `Handles` rather than `AddHandler`:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#24)]  
  
- <span data-ttu-id="ca2b4-164">使用 `AddressOf` ，而且不要明確地具現化委派：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-164">Use `AddressOf`, and do not instantiate the delegate explicitly:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#25)]  
  
- <span data-ttu-id="ca2b4-165">當您定義事件時，請使用簡短語法，然後讓編譯器定義委派：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-165">When you define an event, use the short syntax, and let the compiler define the delegate:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#26)]  
  
- <span data-ttu-id="ca2b4-166">`Nothing`在呼叫方法之前，請不要確認事件是否 (null) `RaiseEvent` 。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-166">Do not verify whether an event is `Nothing` (null) before you call the `RaiseEvent` method.</span></span> <span data-ttu-id="ca2b4-167">`RaiseEvent``Nothing`在引發事件之前檢查。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-167">`RaiseEvent` checks for `Nothing` before it raises the event.</span></span>  
  
### <a name="using-shared-members"></a><span data-ttu-id="ca2b4-168">使用共用成員</span><span class="sxs-lookup"><span data-stu-id="ca2b4-168">Using Shared Members</span></span>  

 <span data-ttu-id="ca2b4-169">`Shared`使用類別名稱呼叫成員，而不是從執行個體變數。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-169">Call `Shared` members by using the class name, not from an instance variable.</span></span>  
  
### <a name="use-xml-literals"></a><span data-ttu-id="ca2b4-170">使用 XML 常值</span><span class="sxs-lookup"><span data-stu-id="ca2b4-170">Use XML Literals</span></span>  

 <span data-ttu-id="ca2b4-171">XML 常值會簡化您使用 XML (時所遇到的最常見工作，例如載入、查詢和轉換) 。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-171">XML literals simplify the most common tasks that you encounter when you work with XML (for example, load, query, and transform).</span></span> <span data-ttu-id="ca2b4-172">當您使用 XML 進行開發時，請遵循下列指導方針：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-172">When you develop with XML, follow these guidelines:</span></span>  
  
- <span data-ttu-id="ca2b4-173">使用 XML 常值來建立 XML 檔和片段，而不是直接呼叫 XML Api。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-173">Use XML literals to create XML documents and fragments instead of calling XML APIs directly.</span></span>  
  
- <span data-ttu-id="ca2b4-174">匯入檔案或專案層級的 XML 命名空間，以利用 XML 常值的效能優化。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-174">Import XML namespaces at the file or project level to take advantage of the performance optimizations for XML literals.</span></span>  
  
- <span data-ttu-id="ca2b4-175">使用 XML 軸屬性來存取 XML 檔中的元素和屬性。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-175">Use the XML axis properties to access elements and attributes in an XML document.</span></span>  
  
- <span data-ttu-id="ca2b4-176">使用內嵌運算式來包含值，並從現有的值建立 XML，而不使用 API 呼叫（例如 `Add` 方法）：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-176">Use embedded expressions to include values and to create XML from existing values instead of using API calls such as the `Add` method:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#27)]  
  
### <a name="linq-queries"></a><span data-ttu-id="ca2b4-177">LINQ 查詢</span><span class="sxs-lookup"><span data-stu-id="ca2b4-177">LINQ Queries</span></span>  
  
- <span data-ttu-id="ca2b4-178">針對查詢變數使用有意義的名稱：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-178">Use meaningful names for query variables:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#28)]  
  
- <span data-ttu-id="ca2b4-179">提供查詢中專案的名稱，以確保匿名型別的屬性名稱使用 Pascal 大小寫正確地大寫：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-179">Provide names for elements in a query to make sure that property names of anonymous types are correctly capitalized using Pascal casing:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#29)]  
  
- <span data-ttu-id="ca2b4-180">當結果中的屬性名稱可能會造成混淆時，請重新命名屬性。</span><span class="sxs-lookup"><span data-stu-id="ca2b4-180">Rename properties when the property names in the result would be ambiguous.</span></span> <span data-ttu-id="ca2b4-181">例如，如果您的查詢傳回客戶名稱和訂單識別碼，請將其重新命名，而不是 `Name` `ID` 在結果中保留它們：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-181">For example, if your query returns a customer name and an order ID, rename them instead of leaving them as `Name` and `ID` in the result:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#30)]  
  
- <span data-ttu-id="ca2b4-182">在查詢變數和範圍變數的宣告中使用類型推斷：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-182">Use type inference in the declaration of query variables and range variables:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#31)]  
  
- <span data-ttu-id="ca2b4-183">在語句下對齊查詢子句 `From` ：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-183">Align query clauses under the `From` statement:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#32)]  
  
- <span data-ttu-id="ca2b4-184">在 `Where` 其他查詢子句之前使用子句，以便稍後的查詢子句在篩選過的資料集上運作：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-184">Use `Where` clauses before other query clauses so that later query clauses operate on the filtered set of data:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#33)]  
  
- <span data-ttu-id="ca2b4-185">使用 `Join` 子句來明確定義聯結作業，而不是使用 `Where` 子句來隱含地定義聯結操作：</span><span class="sxs-lookup"><span data-stu-id="ca2b4-185">Use the `Join` clause to explicitly define a join operation instead of using the `Where` clause to implicitly define a join operation:</span></span>  
  
     [!code-vb[VbVbalrGuidelines#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrGuidelines/VB/Class1.vb#34)]  
  
## <a name="see-also"></a><span data-ttu-id="ca2b4-186">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ca2b4-186">See also</span></span>

- [<span data-ttu-id="ca2b4-187">安全程式碼撰寫方針</span><span class="sxs-lookup"><span data-stu-id="ca2b4-187">Secure Coding Guidelines</span></span>](../../../standard/security/secure-coding-guidelines.md)
