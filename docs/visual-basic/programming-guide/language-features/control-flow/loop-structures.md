---
title: 迴圈結構
ms.date: 07/20/2015
helpviewer_keywords:
- control flow [Visual Basic], loops
- For keyword [Visual Basic], loop structures
- loops
- loop structures [Visual Basic]
- statements [Visual Basic], loop
- Do statement [Visual Basic], Do loops
- conditional statements [Visual Basic], loop structures
ms.assetid: ecacb09b-a4c9-42be-98b2-a15d368b5db8
ms.openlocfilehash: 5019eaf219ad70f9c667356636d05ab69fc5a187
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91077211"
---
# <a name="loop-structures-visual-basic"></a><span data-ttu-id="805af-102">迴圈結構 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="805af-102">Loop Structures (Visual Basic)</span></span>

<span data-ttu-id="805af-103">Visual Basic 迴圈結構可讓您重複執行一或多行程式碼。</span><span class="sxs-lookup"><span data-stu-id="805af-103">Visual Basic loop structures allow you to run one or more lines of code repetitively.</span></span> <span data-ttu-id="805af-104">您可以重複執行迴圈結構中的語句，直到條件為、 `True` `False` 指定的次數，或針對集合中的每個元素一次為止。</span><span class="sxs-lookup"><span data-stu-id="805af-104">You can repeat the statements in a loop structure until a condition is `True`, until a condition is `False`, a specified number of times, or once for each element in a collection.</span></span>  
  
 <span data-ttu-id="805af-105">下圖顯示的迴圈結構會執行一組語句，直到條件變成 true 為止：</span><span class="sxs-lookup"><span data-stu-id="805af-105">The following illustration shows a loop structure that runs a set of statements until a condition becomes true:</span></span>  
  
 ![顯示 ... 的流程圖Until 迴圈。](./media/loop-structures/do-until-loop-true-condition.gif)  
  
## <a name="while-loops"></a><span data-ttu-id="805af-107">While 迴圈</span><span class="sxs-lookup"><span data-stu-id="805af-107">While Loops</span></span>  

 <span data-ttu-id="805af-108">`While` `End While` 只要語句中指定的條件為，就會執行一組語句。 `While` `True`</span><span class="sxs-lookup"><span data-stu-id="805af-108">The `While`...`End While` construction runs a set of statements as long as the condition specified in the `While` statement is `True`.</span></span> <span data-ttu-id="805af-109">如需詳細資訊，請參閱 [.。。End While 語句](../../../language-reference/statements/while-end-while-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="805af-109">For more information, see [While...End While Statement](../../../language-reference/statements/while-end-while-statement.md).</span></span>  
  
## <a name="do-loops"></a><span data-ttu-id="805af-110">Do 迴圈</span><span class="sxs-lookup"><span data-stu-id="805af-110">Do Loops</span></span>  

 <span data-ttu-id="805af-111">「 `Do` ... 結構」可 `Loop` 讓您在迴圈結構的開頭或結尾測試條件。</span><span class="sxs-lookup"><span data-stu-id="805af-111">The `Do`...`Loop` construction allows you to test a condition at either the beginning or the end of a loop structure.</span></span> <span data-ttu-id="805af-112">您也可以指定在條件維持或變成之前，是否要重複執行迴圈 `True` `True` 。</span><span class="sxs-lookup"><span data-stu-id="805af-112">You can also specify whether to repeat the loop while the condition remains `True` or until it becomes `True`.</span></span> <span data-ttu-id="805af-113">如需詳細資訊， [請參閱 .。。迴圈語句](../../../language-reference/statements/do-loop-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="805af-113">For more information, see [Do...Loop Statement](../../../language-reference/statements/do-loop-statement.md).</span></span>  
  
## <a name="for-loops"></a><span data-ttu-id="805af-114">For 迴圈</span><span class="sxs-lookup"><span data-stu-id="805af-114">For Loops</span></span>  

 <span data-ttu-id="805af-115">`For`... 結構會在 `Next` 設定的次數內執行迴圈。</span><span class="sxs-lookup"><span data-stu-id="805af-115">The `For`...`Next` construction performs the loop a set number of times.</span></span> <span data-ttu-id="805af-116">它使用迴圈控制變數（也稱為 *計數器*）來追蹤重複的進度。</span><span class="sxs-lookup"><span data-stu-id="805af-116">It uses a loop control variable, also called a *counter*, to keep track of the repetitions.</span></span> <span data-ttu-id="805af-117">您可以指定這個計數器的開始和結束值，也可以選擇性地指定它從一次重複到下一次的增加量。</span><span class="sxs-lookup"><span data-stu-id="805af-117">You specify the starting and ending values for this counter, and you can optionally specify the amount by which it increases from one repetition to the next.</span></span> <span data-ttu-id="805af-118">如需詳細資訊，請參閱 [.。。下一個語句](../../../language-reference/statements/for-next-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="805af-118">For more information, see [For...Next Statement](../../../language-reference/statements/for-next-statement.md).</span></span>  
  
## <a name="for-each-loops"></a><span data-ttu-id="805af-119">針對每個迴圈</span><span class="sxs-lookup"><span data-stu-id="805af-119">For Each Loops</span></span>  

 <span data-ttu-id="805af-120">`For Each`... `Next` 結構會針對集合中的每個元素執行一組語句。</span><span class="sxs-lookup"><span data-stu-id="805af-120">The `For Each`...`Next` construction runs a set of statements once for each element in a collection.</span></span> <span data-ttu-id="805af-121">您可以指定迴圈控制變數，但不需要判斷其開始或結束值。</span><span class="sxs-lookup"><span data-stu-id="805af-121">You specify the loop control variable, but you do not have to determine starting or ending values for it.</span></span> <span data-ttu-id="805af-122">如需詳細資訊，請參閱 [For Each .。。下一個語句](../../../language-reference/statements/for-each-next-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="805af-122">For more information, see [For Each...Next Statement](../../../language-reference/statements/for-each-next-statement.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="805af-123">另請參閱</span><span class="sxs-lookup"><span data-stu-id="805af-123">See also</span></span>

- [<span data-ttu-id="805af-124">控制流程</span><span class="sxs-lookup"><span data-stu-id="805af-124">Control Flow</span></span>](index.md)
- [<span data-ttu-id="805af-125">決策結構</span><span class="sxs-lookup"><span data-stu-id="805af-125">Decision Structures</span></span>](decision-structures.md)
- [<span data-ttu-id="805af-126">其他控制結構</span><span class="sxs-lookup"><span data-stu-id="805af-126">Other Control Structures</span></span>](other-control-structures.md)
- [<span data-ttu-id="805af-127">巢狀控制結構</span><span class="sxs-lookup"><span data-stu-id="805af-127">Nested Control Structures</span></span>](nested-control-structures.md)
