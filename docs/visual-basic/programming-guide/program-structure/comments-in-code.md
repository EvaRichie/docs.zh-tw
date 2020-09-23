---
title: 程式碼中的註解
ms.date: 07/20/2015
helpviewer_keywords:
- Uncomment button
- REM statement [Visual Basic]
- comments [Visual Basic], in code
- comments [Visual Basic], Visual Basic code
- Comment button
- buttons [Visual Basic], Uncomment
- buttons [Visual Basic], Comment
- code comments [Visual Basic], Visual Basic
- Visual Basic code, comments
- comments
- code comments
ms.assetid: 90136fba-22eb-49f9-ba81-63db629b4a47
ms.openlocfilehash: b0077bdae3bad1d67c3d26e503d05f318982eb80
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91099017"
---
# <a name="comments-in-code-visual-basic"></a><span data-ttu-id="770bd-102">程式碼中的註解 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="770bd-102">Comments in Code (Visual Basic)</span></span>

<span data-ttu-id="770bd-103">當您閱讀程式碼範例時，常會遇到註解符號 (`'`)。</span><span class="sxs-lookup"><span data-stu-id="770bd-103">As you read the code examples, you often encounter the comment symbol (`'`).</span></span> <span data-ttu-id="770bd-104">此符號會告知 Visual Basic 編譯器忽略其後面的文字或 *批註*。</span><span class="sxs-lookup"><span data-stu-id="770bd-104">This symbol tells the Visual Basic compiler to ignore the text following it, or the *comment*.</span></span> <span data-ttu-id="770bd-105">註解是為了閱讀者方便而加入至程式碼的簡短說明。</span><span class="sxs-lookup"><span data-stu-id="770bd-105">Comments are brief explanatory notes added to code for the benefit of those reading it.</span></span>  
  
 <span data-ttu-id="770bd-106">以簡短註解做為所有程序開頭是良好的程式設計作法，此註解會描述程序的基本特性 (作用為何)。</span><span class="sxs-lookup"><span data-stu-id="770bd-106">It is good programming practice to begin all procedures with a brief comment describing the functional characteristics of the procedure (what it does).</span></span> <span data-ttu-id="770bd-107">這對於您自己以及對於其他檢查程式碼的人都有好處。</span><span class="sxs-lookup"><span data-stu-id="770bd-107">This is for your own benefit and the benefit of anyone else who examines the code.</span></span> <span data-ttu-id="770bd-108">您應該將描述功能特性的註解，與實作 (Implementation) 細節 (程序是如何運作) 分開。</span><span class="sxs-lookup"><span data-stu-id="770bd-108">You should separate the implementation details (how the procedure does it) from comments that describe the functional characteristics.</span></span> <span data-ttu-id="770bd-109">當您將實作細節包含在描述中，請記得在更新函式時，將實作細節一同更新。</span><span class="sxs-lookup"><span data-stu-id="770bd-109">When you include implementation details in the description, remember to update them when you update the function.</span></span>  
  
 <span data-ttu-id="770bd-110">註解可以跟隨在陳述式之後的同一行中，或者佔據一整行。</span><span class="sxs-lookup"><span data-stu-id="770bd-110">Comments can follow a statement on the same line, or occupy an entire line.</span></span> <span data-ttu-id="770bd-111">兩者皆會在以下程式碼中加以說明。</span><span class="sxs-lookup"><span data-stu-id="770bd-111">Both are illustrated in the following code.</span></span>  
  
 [!code-vb[VbVbcnConventions#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#16)]  
  
 <span data-ttu-id="770bd-112">如果需要有一行以上的註解，請在每一行中使用註解符號，如下列範例：</span><span class="sxs-lookup"><span data-stu-id="770bd-112">If your comment requires more than one line, use the comment symbol on each line, as the following example illustrates.</span></span>  
  
 [!code-vb[VbVbcnConventions#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnConventions/VB/Class1.vb#17)]  
  
## <a name="commenting-guidelines"></a><span data-ttu-id="770bd-113">註解方針</span><span class="sxs-lookup"><span data-stu-id="770bd-113">Commenting Guidelines</span></span>  

 <span data-ttu-id="770bd-114">下表提供哪些註解類型可以出現在一段程式碼之前的一般方針。</span><span class="sxs-lookup"><span data-stu-id="770bd-114">The following table provides general guidelines for what types of comments can precede a section of code.</span></span> <span data-ttu-id="770bd-115">這些都是建議事項;Visual Basic 不會強制新增批註的規則。</span><span class="sxs-lookup"><span data-stu-id="770bd-115">These are suggestions; Visual Basic does not enforce rules for adding comments.</span></span> <span data-ttu-id="770bd-116">撰寫對您自己與其他閱讀程式碼的人而言最有效的註解。</span><span class="sxs-lookup"><span data-stu-id="770bd-116">Write what works best, both for you and for anyone else who reads your code.</span></span>  
  
|||  
|---|---|  
|<span data-ttu-id="770bd-117">註解類型</span><span class="sxs-lookup"><span data-stu-id="770bd-117">Comment type</span></span>|<span data-ttu-id="770bd-118">註解說明</span><span class="sxs-lookup"><span data-stu-id="770bd-118">Comment description</span></span>|  
|<span data-ttu-id="770bd-119">目的</span><span class="sxs-lookup"><span data-stu-id="770bd-119">Purpose</span></span>|<span data-ttu-id="770bd-120">描述程序的功用 (非如何運作)</span><span class="sxs-lookup"><span data-stu-id="770bd-120">Describes what the procedure does (not how it does it)</span></span>|  
|<span data-ttu-id="770bd-121">假設</span><span class="sxs-lookup"><span data-stu-id="770bd-121">Assumptions</span></span>|<span data-ttu-id="770bd-122">列出每個外部變數、控制項、開啟檔案或其他程序存取的項目</span><span class="sxs-lookup"><span data-stu-id="770bd-122">Lists each external variable, control, open file, or other element accessed by the procedure</span></span>|  
|<span data-ttu-id="770bd-123">效果</span><span class="sxs-lookup"><span data-stu-id="770bd-123">Effects</span></span>|<span data-ttu-id="770bd-124">列出每個受影響的外部變數、控制項或檔案，以及其所受的影響 (僅限於不明顯的)</span><span class="sxs-lookup"><span data-stu-id="770bd-124">Lists each affected external variable, control, or file, and the effect it has (only if it is not obvious)</span></span>|  
|<span data-ttu-id="770bd-125">輸入</span><span class="sxs-lookup"><span data-stu-id="770bd-125">Inputs</span></span>|<span data-ttu-id="770bd-126">指定引數的用途</span><span class="sxs-lookup"><span data-stu-id="770bd-126">Specifies the purpose of the argument</span></span>|  
|<span data-ttu-id="770bd-127">傳回</span><span class="sxs-lookup"><span data-stu-id="770bd-127">Returns</span></span>|<span data-ttu-id="770bd-128">說明程序傳回的值</span><span class="sxs-lookup"><span data-stu-id="770bd-128">Explains the values returned by the procedure</span></span>|  
  
 <span data-ttu-id="770bd-129">請記住以下要點：</span><span class="sxs-lookup"><span data-stu-id="770bd-129">Remember the following points:</span></span>  
  
- <span data-ttu-id="770bd-130">每個重要的變數宣告之前都應該有註解，此註解會描述所宣告之變數的用途。</span><span class="sxs-lookup"><span data-stu-id="770bd-130">Every important variable declaration should be preceded by a comment describing the use of the variable being declared.</span></span>  
  
- <span data-ttu-id="770bd-131">變數、控制項和程序應該清楚命名，讓註解只需用於複雜的實作細節中。</span><span class="sxs-lookup"><span data-stu-id="770bd-131">Variables, controls, and procedures should be named clearly enough that commenting is needed only for complex implementation details.</span></span>  
  
- <span data-ttu-id="770bd-132">註解不可以跟隨在同一行的行接續序列之後。</span><span class="sxs-lookup"><span data-stu-id="770bd-132">Comments cannot follow a line-continuation sequence on the same line.</span></span>  
  
 <span data-ttu-id="770bd-133">您可以藉由選取一或多行程式碼，然後選擇 [Visual Studio 中的 [Visual Basic 批註] 按鈕 (**批註** ，來新增或移除程式碼區塊的批註符號 ![ 。 ](./media/comments-in-code/visual-basic-comment-button.gif)) 並 **取消** 批註 ([ ![ ](./media/comments-in-code/visual-basic-uncomment-button.gif) **編輯** ] 工具列上 Visual Basic 按鈕中的 [Visual Studio 取消批註] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="770bd-133">You can add or remove comment symbols for a block of code by selecting one or more lines of code and choosing the **Comment** (![The Visual Basic Comment button in Visual Studio.](./media/comments-in-code/visual-basic-comment-button.gif)) and **Uncomment** (![The Visual Basic Uncomment button in Visual Studio.](./media/comments-in-code/visual-basic-uncomment-button.gif)) buttons on the **Edit** toolbar.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="770bd-134">您也可以藉由在文字前方置入 `REM` 關鍵字，將註解加入至您的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="770bd-134">You can also add comments to your code by preceding the text with the `REM` keyword.</span></span> <span data-ttu-id="770bd-135">不過， `'` 符號和**批註批註** / **Uncomment**按鈕比較容易使用，而且需要較少的空間和記憶體。</span><span class="sxs-lookup"><span data-stu-id="770bd-135">However, the `'` symbol and the **Comment**/**Uncomment** buttons are easier to use and require less space and memory.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="770bd-136">另請參閱</span><span class="sxs-lookup"><span data-stu-id="770bd-136">See also</span></span>

- [<span data-ttu-id="770bd-137">基本技術-使用 XML 批註記錄您的程式碼</span><span class="sxs-lookup"><span data-stu-id="770bd-137">Basic Instincts - Documenting Your Code With XML Comments</span></span>](/archive/msdn-magazine/2009/may/documenting-your-code-with-xml-comments)
- [<span data-ttu-id="770bd-138">如何：建立 XML 文件</span><span class="sxs-lookup"><span data-stu-id="770bd-138">How to: Create XML Documentation</span></span>](how-to-create-xml-documentation.md)
- [<span data-ttu-id="770bd-139">XML 註解標籤</span><span class="sxs-lookup"><span data-stu-id="770bd-139">XML Comment Tags</span></span>](../../language-reference/xmldoc/index.md)
- [<span data-ttu-id="770bd-140">程式結構和程式碼慣例</span><span class="sxs-lookup"><span data-stu-id="770bd-140">Program Structure and Code Conventions</span></span>](program-structure-and-code-conventions.md)
- [<span data-ttu-id="770bd-141">REM 陳述式</span><span class="sxs-lookup"><span data-stu-id="770bd-141">REM Statement</span></span>](../../language-reference/statements/rem-statement.md)
