---
title: 程式結構與程式碼慣例
ms.date: 07/20/2015
helpviewer_keywords:
- coding conventions
- Visual Basic code, coding conventions
- coding conventions [Visual Basic], Visual Basic
- programs [Visual Basic], structure
- program structure [Visual Basic]
- naming conventions [Visual Basic], Visual Basic
- best practices [Visual Basic], coding conventions
- conventions [Visual Basic], Visual Basic coding
- Visual Basic code
- programming [Visual Basic], Visual Basic coding conventions
ms.assetid: dd9be76f-6944-4e78-ad72-0b6084a3fc13
ms.openlocfilehash: c8d851afc33e7e898ab16abc941d8680f74145e3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398301"
---
# <a name="program-structure-and-code-conventions-visual-basic"></a><span data-ttu-id="c2c4c-102">程式結構和程式碼慣例 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c2c4c-102">Program Structure and Code Conventions (Visual Basic)</span></span>
<span data-ttu-id="c2c4c-103">本節介紹一般的 Visual Basic 程式結構，提供簡單的 Visual Basic 程式 "Hello，World"，並討論 Visual Basic 程式碼慣例。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-103">This section introduces the typical Visual Basic program structure, provides a simple Visual Basic program, "Hello, World", and discusses Visual Basic code conventions.</span></span> <span data-ttu-id="c2c4c-104">程式碼慣例是著重于不在程式邏輯上，但在其實體結構和外觀上的建議。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-104">Code conventions are suggestions that focus not on a program's logic but on its physical structure and appearance.</span></span> <span data-ttu-id="c2c4c-105">之後，您可以更輕鬆地閱讀、瞭解和維護您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-105">Following them makes your code easier to read, understand, and maintain.</span></span> <span data-ttu-id="c2c4c-106">程式碼慣例可以包含其他專案：</span><span class="sxs-lookup"><span data-stu-id="c2c4c-106">Code conventions can include, among others:</span></span>  
  
- <span data-ttu-id="c2c4c-107">標記和批註程式碼的標準化格式。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-107">Standardized formats for labeling and commenting code.</span></span>  
  
- <span data-ttu-id="c2c4c-108">間距、格式化和縮排程式碼的指導方針。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-108">Guidelines for spacing, formatting, and indenting code.</span></span>  
  
- <span data-ttu-id="c2c4c-109">物件、變數和程式的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-109">Naming conventions for objects, variables, and procedures.</span></span>  
  
 <span data-ttu-id="c2c4c-110">下列主題提供一組 Visual Basic 程式的程式設計方針，以及良好使用方式的範例。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-110">The following topics present a set of programming guidelines for Visual Basic programs, along with examples of good usage.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="c2c4c-111">本節內容</span><span class="sxs-lookup"><span data-stu-id="c2c4c-111">In This Section</span></span>  
 [<span data-ttu-id="c2c4c-112">Visual Basic 程式的結構</span><span class="sxs-lookup"><span data-stu-id="c2c4c-112">Structure of a Visual Basic Program</span></span>](structure-of-a-visual-basic-program.md)  
 <span data-ttu-id="c2c4c-113">提供組成 Visual Basic 程式的元素總覽。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-113">Provides an overview of the elements that make up a Visual Basic program.</span></span>  
  
 [<span data-ttu-id="c2c4c-114">Visual Basic 中的 Main 程序</span><span class="sxs-lookup"><span data-stu-id="c2c4c-114">Main Procedure in Visual Basic</span></span>](main-procedure.md)  
 <span data-ttu-id="c2c4c-115">討論做為您應用程式之起點和整體控制的程式。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-115">Discusses the procedure that serves as the starting point and overall control for your application.</span></span>  
  
 [<span data-ttu-id="c2c4c-116">References 與 Imports 陳述式</span><span class="sxs-lookup"><span data-stu-id="c2c4c-116">References and the Imports Statement</span></span>](references-and-the-imports-statement.md)  
 <span data-ttu-id="c2c4c-117">討論如何參考其他元件中的物件。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-117">Discusses how to reference objects in other assemblies.</span></span>  
  
 [<span data-ttu-id="c2c4c-118">Visual Basic 中的命名空間</span><span class="sxs-lookup"><span data-stu-id="c2c4c-118">Namespaces in Visual Basic</span></span>](namespaces.md)  
 <span data-ttu-id="c2c4c-119">說明命名空間如何組織元件中的物件。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-119">Describes how namespaces organize objects within assemblies.</span></span>  
  
 [<span data-ttu-id="c2c4c-120">Visual Basic 命名慣例</span><span class="sxs-lookup"><span data-stu-id="c2c4c-120">Visual Basic Naming Conventions</span></span>](naming-conventions.md)  
 <span data-ttu-id="c2c4c-121">包含命名程式、常數、變數、引數和物件的一般指導方針。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-121">Includes general guidelines for naming procedures, constants, variables, arguments, and objects.</span></span>  
  
 [<span data-ttu-id="c2c4c-122">Visual Basic 編碼慣例</span><span class="sxs-lookup"><span data-stu-id="c2c4c-122">Visual Basic Coding Conventions</span></span>](coding-conventions.md)  
 <span data-ttu-id="c2c4c-123">回顧開發本檔中的範例所使用的指導方針。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-123">Reviews the guidelines used in developing the samples in this documentation.</span></span>  
  
 [<span data-ttu-id="c2c4c-124">條件式編譯</span><span class="sxs-lookup"><span data-stu-id="c2c4c-124">Conditional Compilation</span></span>](conditional-compilation.md)  
 <span data-ttu-id="c2c4c-125">描述如何選擇性地編譯特定的程式碼區塊，同時將編譯器設為忽略其他組塊。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-125">Describes how to compile particular blocks of code selectively while directing the compiler to ignore others.</span></span>  
  
 [<span data-ttu-id="c2c4c-126">作法：程式碼中的 Break 及 Combine 陳述式</span><span class="sxs-lookup"><span data-stu-id="c2c4c-126">How to: Break and Combine Statements in Code</span></span>](how-to-break-and-combine-statements-in-code.md)  
 <span data-ttu-id="c2c4c-127">示範如何將長語句分割成多行，並將 short 語句結合成一行。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-127">Shows how to divide long statements into multiple lines and combine short statements on one line.</span></span>  
  
 [<span data-ttu-id="c2c4c-128">作法：摺疊及隱藏程式碼區段</span><span class="sxs-lookup"><span data-stu-id="c2c4c-128">How to: Collapse and Hide Sections of Code</span></span>](how-to-collapse-and-hide-sections-of-code.md)  
 <span data-ttu-id="c2c4c-129">顯示如何在 Visual Basic 程式碼編輯器中折迭和隱藏程式碼區段。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-129">Shows how to collapse and hide sections of code in the Visual Basic code editor.</span></span>  
  
 [<span data-ttu-id="c2c4c-130">作法：Label 陳述式</span><span class="sxs-lookup"><span data-stu-id="c2c4c-130">How to: Label Statements</span></span>](how-to-label-statements.md)  
 <span data-ttu-id="c2c4c-131">示範如何標記程式程式碼，以識別它與語句搭配使用，例如 `On Error Goto` 。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-131">Shows how to mark a line of code to identify it for use with statements such as `On Error Goto`.</span></span>  
  
 [<span data-ttu-id="c2c4c-132">程式碼中的特殊字元</span><span class="sxs-lookup"><span data-stu-id="c2c4c-132">Special Characters in Code</span></span>](special-characters-in-code.md)  
 <span data-ttu-id="c2c4c-133">顯示使用非數值和非字母字元的方式和位置。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-133">Shows how and where to use non-numeric and non-alphabetic characters.</span></span>  
  
 [<span data-ttu-id="c2c4c-134">程式碼中的註解</span><span class="sxs-lookup"><span data-stu-id="c2c4c-134">Comments in Code</span></span>](comments-in-code.md)  
 <span data-ttu-id="c2c4c-135">討論如何將描述性批註新增至您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-135">Discusses how to add descriptive comments to your code.</span></span>  
  
 [<span data-ttu-id="c2c4c-136">程式碼中的項目名稱關鍵字</span><span class="sxs-lookup"><span data-stu-id="c2c4c-136">Keywords as Element Names in Code</span></span>](keywords-as-element-names-in-code.md)  
 <span data-ttu-id="c2c4c-137">描述如何使用方括弧（ `[]` ）來分隔也 Visual Basic 關鍵字的變數名稱。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-137">Describes how to use brackets (`[]`) to delimit variable names that are also Visual Basic keywords.</span></span>  
  
 [<span data-ttu-id="c2c4c-138">Me、My、MyBase 及 MyClass</span><span class="sxs-lookup"><span data-stu-id="c2c4c-138">Me, My, MyBase, and MyClass</span></span>](me-my-mybase-and-myclass.md)  
 <span data-ttu-id="c2c4c-139">說明用來參考 Visual Basic 程式元素的各種方式。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-139">Describes various ways to refer to elements of a Visual Basic program.</span></span>  
  
 [<span data-ttu-id="c2c4c-140">Visual Basic 的限制</span><span class="sxs-lookup"><span data-stu-id="c2c4c-140">Visual Basic Limitations</span></span>](limitations.md)  
 <span data-ttu-id="c2c4c-141">討論如何移除 Visual Basic 內已知的編碼限制。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-141">Discusses the removal of known coding limits within Visual Basic.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="c2c4c-142">相關章節</span><span class="sxs-lookup"><span data-stu-id="c2c4c-142">Related Sections</span></span>  
 [<span data-ttu-id="c2c4c-143">印刷樣式與程式碼慣例</span><span class="sxs-lookup"><span data-stu-id="c2c4c-143">Typographic and Code Conventions</span></span>](../../language-reference/typographic-and-code-conventions.md)  
 <span data-ttu-id="c2c4c-144">提供 Visual Basic 的標準編碼慣例。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-144">Provides standard coding conventions for Visual Basic.</span></span>  
  
 [<span data-ttu-id="c2c4c-145">撰寫程式碼</span><span class="sxs-lookup"><span data-stu-id="c2c4c-145">Writing Code</span></span>](/visualstudio/ide/writing-code-in-the-code-and-text-editor)  
 <span data-ttu-id="c2c4c-146">描述可讓您更輕鬆地撰寫和管理程式碼的功能。</span><span class="sxs-lookup"><span data-stu-id="c2c4c-146">Describes features that make it easier for you to write and manage your code.</span></span>
