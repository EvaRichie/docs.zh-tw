---
title: ^ 運算子
ms.date: 07/20/2015
f1_keywords:
- vb.^
helpviewer_keywords:
- raising numbers to powers
- ^ operator [Visual Basic], exponentiation
- square operator [Visual Basic]
- ^ operator [Visual Basic]
- exponentiation operator [Visual Basic]
- exponent
- numbers [Visual Basic], rasing
- powers
- arithmetic operators [Visual Basic], exponentiation
ms.assetid: d89a1ca8-83da-4784-a87b-a9d7dceb3f62
ms.openlocfilehash: e139becf74ae367266a23513e18d0bdbdd24cdea
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371384"
---
# <a name="-operator-visual-basic"></a><span data-ttu-id="fb2e7-102">^ 運算子 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="fb2e7-102">^ Operator (Visual Basic)</span></span>

<span data-ttu-id="fb2e7-103">將一數值對另一數值做乘冪運算。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-103">Raises a number to the power of another number.</span></span>

## <a name="syntax"></a><span data-ttu-id="fb2e7-104">語法</span><span class="sxs-lookup"><span data-stu-id="fb2e7-104">Syntax</span></span>

```vb
number ^ exponent
```

## <a name="parts"></a><span data-ttu-id="fb2e7-105">組件</span><span class="sxs-lookup"><span data-stu-id="fb2e7-105">Parts</span></span>

`number`\
<span data-ttu-id="fb2e7-106">必要。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-106">Required.</span></span> <span data-ttu-id="fb2e7-107">任何數值運算式。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-107">Any numeric expression.</span></span>

`exponent`\
<span data-ttu-id="fb2e7-108">必要。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-108">Required.</span></span> <span data-ttu-id="fb2e7-109">任何數值運算式。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-109">Any numeric expression.</span></span>

## <a name="result"></a><span data-ttu-id="fb2e7-110">結果</span><span class="sxs-lookup"><span data-stu-id="fb2e7-110">Result</span></span>

<span data-ttu-id="fb2e7-111">結果會提高 `number` 至的乘冪 `exponent` ，一律為 `Double` 值。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-111">The result is `number` raised to the power of `exponent`, always as a `Double` value.</span></span>

## <a name="supported-types"></a><span data-ttu-id="fb2e7-112">支援的型別</span><span class="sxs-lookup"><span data-stu-id="fb2e7-112">Supported Types</span></span>

<span data-ttu-id="fb2e7-113">`Double`.</span><span class="sxs-lookup"><span data-stu-id="fb2e7-113">`Double`.</span></span> <span data-ttu-id="fb2e7-114">任何不同類型的運算元都會轉換成 `Double` 。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-114">Operands of any different type are converted to `Double`.</span></span>

## <a name="remarks"></a><span data-ttu-id="fb2e7-115">備註</span><span class="sxs-lookup"><span data-stu-id="fb2e7-115">Remarks</span></span>

<span data-ttu-id="fb2e7-116">Visual Basic 一律會執行[Double 資料類型](../data-types/double-data-type.md)的乘冪。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-116">Visual Basic always performs exponentiation in the [Double Data Type](../data-types/double-data-type.md).</span></span>

<span data-ttu-id="fb2e7-117">的值 `exponent` 可以是小數、負數或兩者。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-117">The value of `exponent` can be fractional, negative, or both.</span></span>

<span data-ttu-id="fb2e7-118">在單一運算式中執行多個乘冪時，會在 `^` 從左至右發現運算子時進行評估。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-118">When more than one exponentiation is performed in a single expression, the `^` operator is evaluated as it is encountered from left to right.</span></span>

> [!NOTE]
> <span data-ttu-id="fb2e7-119">`^`運算子可以多載*overloaded*，這表示當運算元具有該類別或結構的類型時，類別或結構可以重新定義其行為。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-119">The `^` operator can be *overloaded*, which means that a class or structure can redefine its behavior when an operand has the type of that class or structure.</span></span> <span data-ttu-id="fb2e7-120">如果您的程式碼在這類類別或結構上使用這個運算子，請務必瞭解其已重新定義的行為。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-120">If your code uses this operator on such a class or structure, be sure you understand its redefined behavior.</span></span> <span data-ttu-id="fb2e7-121">如需詳細資訊，請參閱 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-121">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>

## <a name="example"></a><span data-ttu-id="fb2e7-122">範例</span><span class="sxs-lookup"><span data-stu-id="fb2e7-122">Example</span></span>

<span data-ttu-id="fb2e7-123">下列範例會使用 `^` 運算子，將數位提高至指數的乘冪。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-123">The following example uses the `^` operator to raise a number to the power of an exponent.</span></span> <span data-ttu-id="fb2e7-124">結果是第一個運算元會引發到第二個運算元的乘冪。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-124">The result is the first operand raised to the power of the second.</span></span>

[!code-vb[VbVbalrOperators#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#20)]

<span data-ttu-id="fb2e7-125">上述範例會產生下列結果：</span><span class="sxs-lookup"><span data-stu-id="fb2e7-125">The preceding example produces the following results:</span></span>

<span data-ttu-id="fb2e7-126">`exp1`設定為4（2平方）。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-126">`exp1` is set to 4 (2 squared).</span></span>

<span data-ttu-id="fb2e7-127">`exp2`設定為19683（3個立方，而該值為立方）。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-127">`exp2` is set to 19683 (3 cubed, then that value cubed).</span></span>

<span data-ttu-id="fb2e7-128">`exp3`設定為-125 （-5 的立方）。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-128">`exp3` is set to -125 (-5 cubed).</span></span>

<span data-ttu-id="fb2e7-129">`exp4`設定為625（-5 到第四個乘冪）。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-129">`exp4` is set to 625 (-5 to the fourth power).</span></span>

<span data-ttu-id="fb2e7-130">`exp5`設定為2（8的 cube 根）。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-130">`exp5` is set to 2 (cube root of 8).</span></span>

<span data-ttu-id="fb2e7-131">`exp6`設定為0.5 （1.0 除以8的 cube 根）。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-131">`exp6` is set to 0.5 (1.0 divided by the cube root of 8).</span></span>

<span data-ttu-id="fb2e7-132">請注意上述範例中運算式的括弧重要性。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-132">Note the importance of the parentheses in the expressions in the preceding example.</span></span> <span data-ttu-id="fb2e7-133">由於*運算子的優先順序*，Visual Basic 通常會在 `^` 任何其他專案之前執行運算子，甚至是一元 `–` 運算子。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-133">Because of *operator precedence*, Visual Basic normally performs the `^` operator before any others, even the unary `–` operator.</span></span> <span data-ttu-id="fb2e7-134">如果 `exp4` 和都 `exp6` 是以不含括弧的方式計算，它們就會產生下列結果：</span><span class="sxs-lookup"><span data-stu-id="fb2e7-134">If `exp4` and `exp6` had been calculated without parentheses, they would have produced the following results:</span></span>

<span data-ttu-id="fb2e7-135">`exp4 = -5 ^ 4`會計算為–（5到第四個電源），這會產生-625。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-135">`exp4 = -5 ^ 4` would be calculated as –(5 to the fourth power), which would result in -625.</span></span>

<span data-ttu-id="fb2e7-136">`exp6 = 8 ^ -1.0 / 3.0`會計算為（8到-1 電源，或0.125）除以3.0，這會導致0.041666666666666666666666666666667。</span><span class="sxs-lookup"><span data-stu-id="fb2e7-136">`exp6 = 8 ^ -1.0 / 3.0` would be calculated as (8 to the –1 power, or 0.125) divided by 3.0, which would result in 0.041666666666666666666666666666667.</span></span>

## <a name="see-also"></a><span data-ttu-id="fb2e7-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="fb2e7-137">See also</span></span>

- [<span data-ttu-id="fb2e7-138">^ = 運算子</span><span class="sxs-lookup"><span data-stu-id="fb2e7-138">^= Operator</span></span>](exponentiation-assignment-operator.md)
- [<span data-ttu-id="fb2e7-139">算術運算子</span><span class="sxs-lookup"><span data-stu-id="fb2e7-139">Arithmetic Operators</span></span>](arithmetic-operators.md)
- [<span data-ttu-id="fb2e7-140">Visual Basic 中的運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="fb2e7-140">Operator Precedence in Visual Basic</span></span>](operator-precedence.md)
- [<span data-ttu-id="fb2e7-141">依功能列出運算子</span><span class="sxs-lookup"><span data-stu-id="fb2e7-141">Operators Listed by Functionality</span></span>](operators-listed-by-functionality.md)
- [<span data-ttu-id="fb2e7-142">Visual Basic 的算術運算子</span><span class="sxs-lookup"><span data-stu-id="fb2e7-142">Arithmetic Operators in Visual Basic</span></span>](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
