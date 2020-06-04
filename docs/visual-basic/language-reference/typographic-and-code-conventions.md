---
title: 印刷樣式與程式碼慣例
ms.date: 07/20/2015
helpviewer_keywords:
- coding conventions [Visual Basic], Visual Basic
- best practices [Visual Basic], coding conventions
- conventions [Visual Basic], Visual Basic coding
- typographic conventions [Visual Basic]
- document conventions [Visual Basic]
- conventions [Visual Basic], documentation
- Visual Basic code, conventions
ms.assetid: 1916cd81-ea9d-4faa-81f7-4a0d864b60f4
ms.openlocfilehash: 0e36d9d61b0dd2701210ce614d15fd38f08f5401
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401351"
---
# <a name="typographic-and-code-conventions-visual-basic"></a><span data-ttu-id="0beff-102">印刷樣式與程式碼慣例 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0beff-102">Typographic and Code Conventions (Visual Basic)</span></span>

<span data-ttu-id="0beff-103">Visual Basic 檔會使用下列印刷樣式和程式碼慣例。</span><span class="sxs-lookup"><span data-stu-id="0beff-103">Visual Basic documentation uses the following typographic and code conventions.</span></span>  
  
## <a name="typographic-conventions"></a><span data-ttu-id="0beff-104">印刷樣式慣例</span><span class="sxs-lookup"><span data-stu-id="0beff-104">Typographic Conventions</span></span>  
  
|<span data-ttu-id="0beff-105">範例</span><span class="sxs-lookup"><span data-stu-id="0beff-105">Example</span></span>|<span data-ttu-id="0beff-106">描述</span><span class="sxs-lookup"><span data-stu-id="0beff-106">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="0beff-107">`Sub`, `If`, `ChDir`, `Print`, `True`, `Debug`</span><span class="sxs-lookup"><span data-stu-id="0beff-107">`Sub`, `If`, `ChDir`, `Print`, `True`, `Debug`</span></span>|<span data-ttu-id="0beff-108">特定語言的關鍵字和執行時間成員都有初始大寫字母，而且會格式化，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="0beff-108">Language-specific keywords and runtime members have initial uppercase letters and are formatted as shown in this example.</span></span>|  
|<span data-ttu-id="0beff-109">**SmallProject**、 **ButtonCollection**</span><span class="sxs-lookup"><span data-stu-id="0beff-109">**SmallProject**, **ButtonCollection**</span></span>|<span data-ttu-id="0beff-110">您所指示類型的單字和片語會格式化，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="0beff-110">Words and phrases you are instructed to type are formatted as shown in this example.</span></span>|  
|[<span data-ttu-id="0beff-111">Module 陳述式</span><span class="sxs-lookup"><span data-stu-id="0beff-111">Module Statement</span></span>](statements/module-statement.md)|<span data-ttu-id="0beff-112">如本範例所示，您可以按一下以移至另一個說明頁的連結。</span><span class="sxs-lookup"><span data-stu-id="0beff-112">Links you can click to go to another Help page are formatted as shown in this example.</span></span>|  
|<span data-ttu-id="0beff-113">*object*、 *variableName*、`argumentList`</span><span class="sxs-lookup"><span data-stu-id="0beff-113">*object*, *variableName*, `argumentList`</span></span>|<span data-ttu-id="0beff-114">如本範例所示，您所提供之資訊的預留位置會格式化。</span><span class="sxs-lookup"><span data-stu-id="0beff-114">Placeholders for information that you supply are formatted as shown in this example.</span></span>|  
|<span data-ttu-id="0beff-115">[Shadows]，[ *expressionList* ]</span><span class="sxs-lookup"><span data-stu-id="0beff-115">[ Shadows ], [ *expressionList* ]</span></span>|<span data-ttu-id="0beff-116">在語法中，選擇性專案會以方括弧括住。</span><span class="sxs-lookup"><span data-stu-id="0beff-116">In syntax, optional items are enclosed in brackets.</span></span>|  
|<span data-ttu-id="0beff-117">{ `Public` &#124; `Friend` &#124; `Private` }</span><span class="sxs-lookup"><span data-stu-id="0beff-117">{ `Public` &#124; `Friend` &#124; `Private` }</span></span>|<span data-ttu-id="0beff-118">在語法中，當您必須在兩個或多個專案之間進行選擇時，專案會以大括弧括住，並以分隔號分隔。</span><span class="sxs-lookup"><span data-stu-id="0beff-118">In syntax, when you must make a choice between two or more items, the items are enclosed in braces and separated by vertical bars.</span></span><br /><br /> <span data-ttu-id="0beff-119">您必須只選取一個專案。</span><span class="sxs-lookup"><span data-stu-id="0beff-119">You must select one, and only one, of the items.</span></span>|  
|<span data-ttu-id="0beff-120">[ `Protected` &#124; `Friend` ]</span><span class="sxs-lookup"><span data-stu-id="0beff-120">[ `Protected` &#124; `Friend` ]</span></span>|<span data-ttu-id="0beff-121">在語法中，當您可以選擇兩個或多個專案時，這些專案會以方括弧括住，並以分隔號分隔。</span><span class="sxs-lookup"><span data-stu-id="0beff-121">In syntax, when you have the option of selecting between two or more items, the items are enclosed in square brackets and separated by vertical bars.</span></span><br /><br /> <span data-ttu-id="0beff-122">您可以選取專案的任何組合，或沒有專案。</span><span class="sxs-lookup"><span data-stu-id="0beff-122">You can select any combination of the items, or no item.</span></span>|  
|<span data-ttu-id="0beff-123">[{ `ByVal` &#124; `ByRef` }]</span><span class="sxs-lookup"><span data-stu-id="0beff-123">[{ `ByVal` &#124; `ByRef` }]</span></span>|<span data-ttu-id="0beff-124">在語法中，如果您可以選取一個以上的專案，但也可以完全省略專案，則專案會以括弧括住，並以分隔號分隔。</span><span class="sxs-lookup"><span data-stu-id="0beff-124">In syntax, when you can select no more than one item, but you can also omit the items completely, the items are enclosed in square brackets surrounded by braces and separated by vertical bars.</span></span>|  
|<span data-ttu-id="0beff-125">*成員名稱*1、*成員名稱*2、*成員*名稱3</span><span class="sxs-lookup"><span data-stu-id="0beff-125">*memberName*1, *memberName*2, *memberName*3</span></span>|<span data-ttu-id="0beff-126">相同預留位置的多個實例會以注標區分，如範例中所示。</span><span class="sxs-lookup"><span data-stu-id="0beff-126">Multiple instances of the same placeholder are differentiated by subscripts, as shown in the example.</span></span>|  
|<span data-ttu-id="0beff-127">*成員名稱*</span><span class="sxs-lookup"><span data-stu-id="0beff-127">*memberName1*</span></span><br /><br /> <span data-ttu-id="0beff-128">...</span><span class="sxs-lookup"><span data-stu-id="0beff-128">...</span></span><br /><br /> <span data-ttu-id="0beff-129">*memberNameN*</span><span class="sxs-lookup"><span data-stu-id="0beff-129">*memberNameN*</span></span>|<span data-ttu-id="0beff-130">在語法中，省略號（...）是用來表示緊接在省略號前面的類型專案數不定。</span><span class="sxs-lookup"><span data-stu-id="0beff-130">In syntax, an ellipsis (...) is used to indicate an indefinite number of items of the kind immediately in front of the ellipsis.</span></span><br /><br /> <span data-ttu-id="0beff-131">在程式碼中，省略號表示為了清楚起見而省略的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0beff-131">In code, ellipses signify code omitted for the sake of clarity.</span></span>|  
|<span data-ttu-id="0beff-132">ESC 鍵，輸入</span><span class="sxs-lookup"><span data-stu-id="0beff-132">ESC, ENTER</span></span>|<span data-ttu-id="0beff-133">鍵盤上的索引鍵名稱和按鍵順序會以全部大寫字母顯示。</span><span class="sxs-lookup"><span data-stu-id="0beff-133">Key names and key sequences on the keyboard appear in all uppercase letters.</span></span>|  
|<span data-ttu-id="0beff-134">ALT+F1</span><span class="sxs-lookup"><span data-stu-id="0beff-134">ALT+F1</span></span>|<span data-ttu-id="0beff-135">當索引鍵名稱之間出現加號（+）時，您必須按住某個按鍵，同時按另一個鍵。</span><span class="sxs-lookup"><span data-stu-id="0beff-135">When plus signs (+) appear between key names, you must hold down one key while pressing the other.</span></span> <span data-ttu-id="0beff-136">例如，ALT + F1 表示在按下 F1 鍵時按住 ALT 鍵。</span><span class="sxs-lookup"><span data-stu-id="0beff-136">For example, ALT+F1 means hold down the ALT key while pressing the F1 key.</span></span>|  
  
## <a name="code-conventions"></a><span data-ttu-id="0beff-137">程式碼慣例</span><span class="sxs-lookup"><span data-stu-id="0beff-137">Code Conventions</span></span>  
  
|<span data-ttu-id="0beff-138">範例</span><span class="sxs-lookup"><span data-stu-id="0beff-138">Example</span></span>|<span data-ttu-id="0beff-139">描述</span><span class="sxs-lookup"><span data-stu-id="0beff-139">Description</span></span>|  
|-------------|-----------------|  
|`sampleString = "Hello, world!"`|<span data-ttu-id="0beff-140">程式碼範例會以固定音調的字型顯示，格式如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="0beff-140">Code samples appear in a fixed-pitch font and are formatted as shown in this example.</span></span>|  
|<span data-ttu-id="0beff-141">先前的語句會將的值設定 `sampleString` 為 "Hello，world！"</span><span class="sxs-lookup"><span data-stu-id="0beff-141">The previous statement sets the value of `sampleString` to "Hello, world!"</span></span>|<span data-ttu-id="0beff-142">解說文字中的程式碼專案會以固定音調的字型顯示，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="0beff-142">Code elements in explanatory text appear in a fixed-pitch font, as shown in this example.</span></span>|  
|`' This is a comment.`<br /><br /> `REM This is also a comment.`|<span data-ttu-id="0beff-143">程式碼批註是以單引號（'）或 REM 關鍵字引進。</span><span class="sxs-lookup"><span data-stu-id="0beff-143">Code comments are introduced by an apostrophe (') or the REM keyword.</span></span>|  
|`sampleVar = "This is an " _`<br /><br /> `& "example" _`<br /><br /> `& " of how to continue code."`|<span data-ttu-id="0beff-144">在行尾加上底線（_）的空格表示語句會繼續在下面這一行。</span><span class="sxs-lookup"><span data-stu-id="0beff-144">A space followed by an underscore ( _) at the end of a line indicates that the statement continues on the following line.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="0beff-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0beff-145">See also</span></span>

- [<span data-ttu-id="0beff-146">Visual Basic 語言參考</span><span class="sxs-lookup"><span data-stu-id="0beff-146">Visual Basic Language Reference</span></span>](index.md)
- [<span data-ttu-id="0beff-147">關鍵字</span><span class="sxs-lookup"><span data-stu-id="0beff-147">Keywords</span></span>](keywords/index.md)
- [<span data-ttu-id="0beff-148">Visual Basic 執行階段程式庫成員</span><span class="sxs-lookup"><span data-stu-id="0beff-148">Visual Basic Runtime Library Members</span></span>](runtime-library-members.md)
- [<span data-ttu-id="0beff-149">Visual Basic 命名慣例</span><span class="sxs-lookup"><span data-stu-id="0beff-149">Visual Basic Naming Conventions</span></span>](../programming-guide/program-structure/naming-conventions.md)
- [<span data-ttu-id="0beff-150">作法：程式碼中的 Break 及 Combine 陳述式</span><span class="sxs-lookup"><span data-stu-id="0beff-150">How to: Break and Combine Statements in Code</span></span>](../programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
- [<span data-ttu-id="0beff-151">程式碼中的註解</span><span class="sxs-lookup"><span data-stu-id="0beff-151">Comments in Code</span></span>](../programming-guide/program-structure/comments-in-code.md)
