---
title: 如何：計算數值
ms.date: 07/20/2015
helpviewer_keywords:
- operator precedence
- operators [Visual Basic]
- expressions [Visual Basic], numeric
- calculations [Visual Basic], numeric expressions
- precedence [Visual Basic], of operators
- Visual Basic code, operators
- Visual Basic code, expressions
- numeric expressions
ms.assetid: ba6bf43d-bd96-49b8-b1de-4a7797551372
ms.openlocfilehash: 94b02693f308dcfcfa6983f2750a26d9d419f7be
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403455"
---
# <a name="how-to-calculate-numeric-values-visual-basic"></a><span data-ttu-id="ebae9-102">如何：計算數值 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="ebae9-102">How to: Calculate Numeric Values (Visual Basic)</span></span>
<span data-ttu-id="ebae9-103">您可以透過使用數值運算式來計算數值。</span><span class="sxs-lookup"><span data-stu-id="ebae9-103">You can calculate numeric values through the use of numeric expressions.</span></span> <span data-ttu-id="ebae9-104">*數值運算式*是一個運算式，其中包含代表數值的常值、常數和變數，以及作用於那些值的運算子。</span><span class="sxs-lookup"><span data-stu-id="ebae9-104">A *numeric expression* is an expression that contains literals, constants, and variables representing numeric values, and operators that act on those values.</span></span>  
  
## <a name="calculating-numeric-values"></a><span data-ttu-id="ebae9-105">計算數值</span><span class="sxs-lookup"><span data-stu-id="ebae9-105">Calculating Numeric Values</span></span>  
  
#### <a name="to-calculate-a-numeric-value"></a><span data-ttu-id="ebae9-106">計算數值</span><span class="sxs-lookup"><span data-stu-id="ebae9-106">To calculate a numeric value</span></span>  
  
- <span data-ttu-id="ebae9-107">將一個或多個數值常值、常數和變數結合成數值運算式。</span><span class="sxs-lookup"><span data-stu-id="ebae9-107">Combine one or more numeric literals, constants, and variables into a numeric expression.</span></span> <span data-ttu-id="ebae9-108">下列範例顯示一些有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="ebae9-108">The following example shows some valid numeric expressions.</span></span>  
  
     `93.217`  
  
     `System.Math.PI`  
  
     `counter`  
  
     `4 * (67 + i)`  
  
     <span data-ttu-id="ebae9-109">前三行顯示常值、常數和變數。</span><span class="sxs-lookup"><span data-stu-id="ebae9-109">The first three lines show a literal, a constant, and a variable.</span></span> <span data-ttu-id="ebae9-110">每一個都會單獨形成有效的數值運算式。</span><span class="sxs-lookup"><span data-stu-id="ebae9-110">Each one forms a valid numeric expression by itself.</span></span> <span data-ttu-id="ebae9-111">最後一行顯示具有兩個常值之變數的組合。</span><span class="sxs-lookup"><span data-stu-id="ebae9-111">The final line shows a combination of a variable with two literals.</span></span>  
  
     <span data-ttu-id="ebae9-112">請注意，數值運算式本身並不會形成完整的 Visual Basic 語句。</span><span class="sxs-lookup"><span data-stu-id="ebae9-112">Note that a numeric expression does not form a complete Visual Basic statement by itself.</span></span> <span data-ttu-id="ebae9-113">您必須使用運算式做為完整語句的一部分。</span><span class="sxs-lookup"><span data-stu-id="ebae9-113">You must use the expression as part of a complete statement.</span></span>  
  
#### <a name="to-store-a-numeric-value"></a><span data-ttu-id="ebae9-114">若要儲存數值</span><span class="sxs-lookup"><span data-stu-id="ebae9-114">To store a numeric value</span></span>  
  
- <span data-ttu-id="ebae9-115">您可以使用指派語句，將數值運算式所表示的值指派給變數，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="ebae9-115">You can use an assignment statement to assign the value represented by a numeric expression to a variable, as the following example demonstrates.</span></span>  
  
     [!code-vb[VbVbalrOperators#82](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#82)]  
  
     <span data-ttu-id="ebae9-116">在上述範例中，相等運算子（）右側的運算式值 `=` 會指派給 `j` 運算子左邊的變數，因此會 `j` 評估為276。</span><span class="sxs-lookup"><span data-stu-id="ebae9-116">In the preceding example, the value of the expression on the right side of the equal operator (`=`) is assigned to the variable `j` on the left side of the operator, so `j` evaluates to 276.</span></span>  
  
     <span data-ttu-id="ebae9-117">如需詳細資訊，請參閱[陳述式](../../../language-reference/statements/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ebae9-117">For more information, see [Statements](../../../language-reference/statements/index.md).</span></span>  
  
## <a name="multiple-operators"></a><span data-ttu-id="ebae9-118">多個運算子</span><span class="sxs-lookup"><span data-stu-id="ebae9-118">Multiple Operators</span></span>  
 <span data-ttu-id="ebae9-119">如果數值運算式包含多個運算子，則評估它們的順序是由運算子優先順序的規則所決定。</span><span class="sxs-lookup"><span data-stu-id="ebae9-119">If the numeric expression contains more than one operator, the order in which they are evaluated is determined by the rules of operator precedence.</span></span> <span data-ttu-id="ebae9-120">若要覆寫運算子優先順序的規則，請將運算式括在括弧中，如上述範例所示：會先評估括住的運算式。</span><span class="sxs-lookup"><span data-stu-id="ebae9-120">To override the rules of operator precedence, you enclose expressions in parentheses, as in the above example; the enclosed expressions are evaluated first.</span></span>  
  
#### <a name="to-override-normal-operator-precedence"></a><span data-ttu-id="ebae9-121">若要覆寫一般運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="ebae9-121">To override normal operator precedence</span></span>  
  
- <span data-ttu-id="ebae9-122">使用括弧括住您想要先執行的作業。</span><span class="sxs-lookup"><span data-stu-id="ebae9-122">Use parentheses to enclose the operations you want to be performed first.</span></span> <span data-ttu-id="ebae9-123">下列範例顯示兩個具有相同運算元和運算子的不同結果。</span><span class="sxs-lookup"><span data-stu-id="ebae9-123">The following example shows two different results with the same operands and operators.</span></span>  
  
     [!code-vb[VbVbalrOperators#83](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#83)]  
  
     <span data-ttu-id="ebae9-124">在上述範例中，的計算 `j` 會先執行加法運算子（ `+` ），因為前後的括弧 `(67 + i)` 會覆寫一般優先順序，而指派給的值 `j` 為276（4倍69）。</span><span class="sxs-lookup"><span data-stu-id="ebae9-124">In the preceding example, the calculation for `j` performs the addition operator (`+`) first because the parentheses around `(67 + i)` override normal precedence, and the value assigned to `j` is 276 (4 times 69).</span></span> <span data-ttu-id="ebae9-125">的計算 `k` 會以其一般優先順序（之前）來執行運算子 `*` `+` ，而指派給的值 `k` 為270（268加2）。</span><span class="sxs-lookup"><span data-stu-id="ebae9-125">The calculation for `k` performs the operators in their normal precedence (`*` before `+`), and the value assigned to `k` is 270 (268 plus 2).</span></span>  
  
     <span data-ttu-id="ebae9-126">如需詳細資訊，請參閱[Visual Basic 中的運算子優先順序](../../../language-reference/operators/operator-precedence.md)。</span><span class="sxs-lookup"><span data-stu-id="ebae9-126">For more information, see [Operator Precedence in Visual Basic](../../../language-reference/operators/operator-precedence.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ebae9-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ebae9-127">See also</span></span>

- [<span data-ttu-id="ebae9-128">運算子和運算式</span><span class="sxs-lookup"><span data-stu-id="ebae9-128">Operators and Expressions</span></span>](index.md)
- [<span data-ttu-id="ebae9-129">數值比較</span><span class="sxs-lookup"><span data-stu-id="ebae9-129">Value Comparisons</span></span>](value-comparisons.md)
- [<span data-ttu-id="ebae9-130">陳述式</span><span class="sxs-lookup"><span data-stu-id="ebae9-130">Statements</span></span>](../../../language-reference/statements/index.md)
- [<span data-ttu-id="ebae9-131">Visual Basic 中的運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="ebae9-131">Operator Precedence in Visual Basic</span></span>](../../../language-reference/operators/operator-precedence.md)
- [<span data-ttu-id="ebae9-132">算術運算子</span><span class="sxs-lookup"><span data-stu-id="ebae9-132">Arithmetic Operators</span></span>](../../../language-reference/operators/arithmetic-operators.md)
- [<span data-ttu-id="ebae9-133">有效的運算子組合</span><span class="sxs-lookup"><span data-stu-id="ebae9-133">Efficient Combination of Operators</span></span>](efficient-combination-of-operators.md)
