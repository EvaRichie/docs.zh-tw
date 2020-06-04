---
title: GoTo 陳述式
ms.date: 07/20/2015
f1_keywords:
- vb.GoTo
helpviewer_keywords:
- GoTo statement [Visual Basic]
- control flow [Visual Basic], branching
- unconditional branching [Visual Basic]
- branching [Visual Basic]
- branching [Visual Basic], unconditional
- branching [Visual Basic], conditional
- conditional statements [Visual Basic], GoTo statement
- GoTo statement [Visual Basic], syntax
ms.assetid: 313274c2-8ab3-4b9c-9ba3-0fd6798e4f6d
ms.openlocfilehash: eb6f48d04b7d14591003e340464451da7df45cd6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404611"
---
# <a name="goto-statement"></a><span data-ttu-id="b30a7-102">GoTo 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-102">GoTo Statement</span></span>
<span data-ttu-id="b30a7-103">無條件地分支到程式中的指定行。</span><span class="sxs-lookup"><span data-stu-id="b30a7-103">Branches unconditionally to a specified line in a procedure.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b30a7-104">語法</span><span class="sxs-lookup"><span data-stu-id="b30a7-104">Syntax</span></span>  
  
```vb  
GoTo line  
```  
  
## <a name="part"></a><span data-ttu-id="b30a7-105">部分</span><span class="sxs-lookup"><span data-stu-id="b30a7-105">Part</span></span>  
 `line`  
 <span data-ttu-id="b30a7-106">必要。</span><span class="sxs-lookup"><span data-stu-id="b30a7-106">Required.</span></span> <span data-ttu-id="b30a7-107">任何行標籤。</span><span class="sxs-lookup"><span data-stu-id="b30a7-107">Any line label.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b30a7-108">備註</span><span class="sxs-lookup"><span data-stu-id="b30a7-108">Remarks</span></span>  
 <span data-ttu-id="b30a7-109">`GoTo`語句只能分支至其出現所在程式中的行。</span><span class="sxs-lookup"><span data-stu-id="b30a7-109">The `GoTo` statement can branch only to lines in the procedure in which it appears.</span></span> <span data-ttu-id="b30a7-110">這一行必須有可以參考的行標籤 `GoTo` 。</span><span class="sxs-lookup"><span data-stu-id="b30a7-110">The line must have a line label that `GoTo` can refer to.</span></span> <span data-ttu-id="b30a7-111">如需詳細資訊，請參閱 how [to： Label 語句](../../programming-guide/program-structure/how-to-label-statements.md)。</span><span class="sxs-lookup"><span data-stu-id="b30a7-111">For more information, see [How to: Label Statements](../../programming-guide/program-structure/how-to-label-statements.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b30a7-112">`GoTo`語句可能會使程式碼更容易讀取和維護。</span><span class="sxs-lookup"><span data-stu-id="b30a7-112">`GoTo` statements can make code difficult to read and maintain.</span></span> <span data-ttu-id="b30a7-113">請盡可能改用控制結構。</span><span class="sxs-lookup"><span data-stu-id="b30a7-113">Whenever possible, use a control structure instead.</span></span> <span data-ttu-id="b30a7-114">如需詳細資訊，請參閱 [控制流程](../../programming-guide/language-features/control-flow/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b30a7-114">For more information, see [Control Flow](../../programming-guide/language-features/control-flow/index.md).</span></span>  
  
 <span data-ttu-id="b30a7-115">您不能使用 `GoTo` 語句從 [ `For` ... `Next` `For Each` `Next` `SyncLock` `End SyncLock` `Try` `Catch` ]、[...]、[...] 和 [...]... `Finally` 、 `With` ... `End With` 或 `Using` ... `End Using` 結構，到內的標籤。</span><span class="sxs-lookup"><span data-stu-id="b30a7-115">You cannot use a `GoTo` statement to branch from outside a `For`...`Next`, `For Each`...`Next`, `SyncLock`...`End SyncLock`, `Try`...`Catch`...`Finally`, `With`...`End With`, or `Using`...`End Using` construction to a label inside.</span></span>  
  
## <a name="branching-and-try-constructions"></a><span data-ttu-id="b30a7-116">分支和 Try 結構</span><span class="sxs-lookup"><span data-stu-id="b30a7-116">Branching and Try Constructions</span></span>  
 <span data-ttu-id="b30a7-117">在 `Try` ... `Catch`...`Finally`結構中，下列規則適用于使用語句的分支 `GoTo` 。</span><span class="sxs-lookup"><span data-stu-id="b30a7-117">Within a `Try`...`Catch`...`Finally` construction, the following rules apply to branching with the `GoTo` statement.</span></span>  
  
|<span data-ttu-id="b30a7-118">封鎖或區域</span><span class="sxs-lookup"><span data-stu-id="b30a7-118">Block or region</span></span>|<span data-ttu-id="b30a7-119">從外部分支</span><span class="sxs-lookup"><span data-stu-id="b30a7-119">Branching in from outside</span></span>|<span data-ttu-id="b30a7-120">從內部分支</span><span class="sxs-lookup"><span data-stu-id="b30a7-120">Branching out from inside</span></span>|  
|---------------------|-------------------------------|-------------------------------|  
|<span data-ttu-id="b30a7-121">`Try`總匯</span><span class="sxs-lookup"><span data-stu-id="b30a7-121">`Try` block</span></span>|<span data-ttu-id="b30a7-122">僅來自 `Catch` 相同結構<sup>1</sup>的區塊</span><span class="sxs-lookup"><span data-stu-id="b30a7-122">Only from a `Catch` block of the same construction <sup>1</sup></span></span>|<span data-ttu-id="b30a7-123">僅限於整個結構外</span><span class="sxs-lookup"><span data-stu-id="b30a7-123">Only to outside the whole construction</span></span>|  
|<span data-ttu-id="b30a7-124">`Catch`總匯</span><span class="sxs-lookup"><span data-stu-id="b30a7-124">`Catch` block</span></span>|<span data-ttu-id="b30a7-125">不允許</span><span class="sxs-lookup"><span data-stu-id="b30a7-125">Never allowed</span></span>|<span data-ttu-id="b30a7-126">僅限於整個結構外，或 `Try` 相同結構<sup>1</sup>的區塊</span><span class="sxs-lookup"><span data-stu-id="b30a7-126">Only to outside the whole construction, or to the `Try` block of the same construction <sup>1</sup></span></span>|  
|<span data-ttu-id="b30a7-127">`Finally`總匯</span><span class="sxs-lookup"><span data-stu-id="b30a7-127">`Finally` block</span></span>|<span data-ttu-id="b30a7-128">不允許</span><span class="sxs-lookup"><span data-stu-id="b30a7-128">Never allowed</span></span>|<span data-ttu-id="b30a7-129">不允許</span><span class="sxs-lookup"><span data-stu-id="b30a7-129">Never allowed</span></span>|  
  
 <span data-ttu-id="b30a7-130"><sup>1</sup> （如果 `Try` 有的話 `Catch` ）...`Finally`結構會在另一個內嵌套， `Catch` 區塊可以 `Try` 在自己的嵌套層級分支到區塊中，但不能放入任何其他 `Try` 區塊中。</span><span class="sxs-lookup"><span data-stu-id="b30a7-130"><sup>1</sup> If one `Try`...`Catch`...`Finally` construction is nested within another, a `Catch` block can branch into the `Try` block at its own nesting level, but not into any other `Try` block.</span></span> <span data-ttu-id="b30a7-131">Nested `Try` ... `Catch`...`Finally`結構必須完全包含在 `Try` 其所用的結構的或 `Catch` 區塊中。</span><span class="sxs-lookup"><span data-stu-id="b30a7-131">A nested `Try`...`Catch`...`Finally` construction must be contained completely in a `Try` or `Catch` block of the construction within which it is nested.</span></span>  
  
 <span data-ttu-id="b30a7-132">下圖顯示 `Try` 在另一個中嵌套的一個結構。</span><span class="sxs-lookup"><span data-stu-id="b30a7-132">The following illustration shows one `Try` construction nested within another.</span></span> <span data-ttu-id="b30a7-133">兩個結構的區塊之間的各種分支會指出為有效或無效。</span><span class="sxs-lookup"><span data-stu-id="b30a7-133">Various branches among the blocks of the two constructions are indicated as valid or invalid.</span></span>  
  
 ![Try 語法結構中的分支示意圖](./media/goto-statement/try-construction-branching.gif)  
  
## <a name="example"></a><span data-ttu-id="b30a7-135">範例</span><span class="sxs-lookup"><span data-stu-id="b30a7-135">Example</span></span>  
 <span data-ttu-id="b30a7-136">下列範例會使用 `GoTo` 語句，在程式中分支至行標籤。</span><span class="sxs-lookup"><span data-stu-id="b30a7-136">The following example uses the `GoTo` statement to branch to line labels in a procedure.</span></span>  
  
 [!code-vb[VbVbalrStatements#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#31)]  
  
## <a name="see-also"></a><span data-ttu-id="b30a7-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b30a7-137">See also</span></span>

- [<span data-ttu-id="b30a7-138">Do...Loop 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-138">Do...Loop Statement</span></span>](do-loop-statement.md)
- [<span data-ttu-id="b30a7-139">For...Next 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-139">For...Next Statement</span></span>](for-next-statement.md)
- [<span data-ttu-id="b30a7-140">For Each...Next 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-140">For Each...Next Statement</span></span>](for-each-next-statement.md)
- [<span data-ttu-id="b30a7-141">If...Then...Else 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-141">If...Then...Else Statement</span></span>](if-then-else-statement.md)
- [<span data-ttu-id="b30a7-142">Select...Case 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-142">Select...Case Statement</span></span>](select-case-statement.md)
- [<span data-ttu-id="b30a7-143">Try...Catch...Finally 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-143">Try...Catch...Finally Statement</span></span>](try-catch-finally-statement.md)
- [<span data-ttu-id="b30a7-144">While...End While 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-144">While...End While Statement</span></span>](while-end-while-statement.md)
- [<span data-ttu-id="b30a7-145">With...End With 陳述式</span><span class="sxs-lookup"><span data-stu-id="b30a7-145">With...End With Statement</span></span>](with-end-with-statement.md)
