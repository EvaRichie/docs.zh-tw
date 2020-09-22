---
title: Not 運算子
ms.date: 07/20/2015
f1_keywords:
- vb.Not
helpviewer_keywords:
- Boolean expressions, negating
- operators [Visual Basic], bitwise
- negation operator [Visual Basic]
- inverse bit values in variables [Visual Basic]
- bitwise operators [Visual Basic], NOT operator
- bitwise comparison [Visual Basic]
- Not operator [Visual Basic]
- logical negation
- operators [Visual Basic], negation
ms.assetid: 8f2ea83c-d2ed-480a-a474-3042a1cad9b5
ms.openlocfilehash: 7d0beea16a2ac00be090c6a241f9790a0ba33390
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874800"
---
# <a name="not-operator-visual-basic"></a><span data-ttu-id="635c9-102">Not 運算子 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="635c9-102">Not Operator (Visual Basic)</span></span>

<span data-ttu-id="635c9-103">對運算式執行邏輯否定 `Boolean` ，或在數值運算式上執行位否定。</span><span class="sxs-lookup"><span data-stu-id="635c9-103">Performs logical negation on a `Boolean` expression, or bitwise negation on a numeric expression.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="635c9-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="635c9-104">Syntax</span></span>  
  
```vb  
result = Not expression  
```  
  
## <a name="parts"></a><span data-ttu-id="635c9-105">組件</span><span class="sxs-lookup"><span data-stu-id="635c9-105">Parts</span></span>  

 `result`  
 <span data-ttu-id="635c9-106">必要。</span><span class="sxs-lookup"><span data-stu-id="635c9-106">Required.</span></span> <span data-ttu-id="635c9-107">任何 `Boolean` 或數值運算式。</span><span class="sxs-lookup"><span data-stu-id="635c9-107">Any `Boolean` or numeric expression.</span></span>  
  
 `expression`  
 <span data-ttu-id="635c9-108">必要。</span><span class="sxs-lookup"><span data-stu-id="635c9-108">Required.</span></span> <span data-ttu-id="635c9-109">任何 `Boolean` 或數值運算式。</span><span class="sxs-lookup"><span data-stu-id="635c9-109">Any `Boolean` or numeric expression.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="635c9-110">備註</span><span class="sxs-lookup"><span data-stu-id="635c9-110">Remarks</span></span>  

 <span data-ttu-id="635c9-111">針對 `Boolean` 運算式，下表說明如何 `result` 決定。</span><span class="sxs-lookup"><span data-stu-id="635c9-111">For `Boolean` expressions, the following table illustrates how `result` is determined.</span></span>  
  
|<span data-ttu-id="635c9-112">如果 `expression` 為 </span><span class="sxs-lookup"><span data-stu-id="635c9-112">If `expression` is</span></span>|<span data-ttu-id="635c9-113">的值 `result` 為</span><span class="sxs-lookup"><span data-stu-id="635c9-113">The value of `result` is</span></span>|  
|------------------------|------------------------------|  
|`True`|`False`|  
|`False`|`True`|  
  
 <span data-ttu-id="635c9-114">若為數值運算式， `Not` 運算子會反轉任何數值運算式的位值，並根據下表設定對應的位 `result` 。</span><span class="sxs-lookup"><span data-stu-id="635c9-114">For numeric expressions, the `Not` operator inverts the bit values of any numeric expression and sets the corresponding bit in `result` according to the following table.</span></span>  
  
|<span data-ttu-id="635c9-115">如果中的位 `expression` 為</span><span class="sxs-lookup"><span data-stu-id="635c9-115">If bit in `expression` is</span></span>|<span data-ttu-id="635c9-116">中的位 `result` 為</span><span class="sxs-lookup"><span data-stu-id="635c9-116">The bit in `result` is</span></span>|  
|-------------------------------|----------------------------|  
|<span data-ttu-id="635c9-117">1</span><span class="sxs-lookup"><span data-stu-id="635c9-117">1</span></span>|<span data-ttu-id="635c9-118">0</span><span class="sxs-lookup"><span data-stu-id="635c9-118">0</span></span>|  
|<span data-ttu-id="635c9-119">0</span><span class="sxs-lookup"><span data-stu-id="635c9-119">0</span></span>|<span data-ttu-id="635c9-120">1</span><span class="sxs-lookup"><span data-stu-id="635c9-120">1</span></span>|  
  
> [!NOTE]
> <span data-ttu-id="635c9-121">由於邏輯和位運算子的優先順序比其他算術和關係運算子低，因此任何位運算都應以括弧括住，以確保正確執行。</span><span class="sxs-lookup"><span data-stu-id="635c9-121">Since the logical and bitwise operators have a lower precedence than other arithmetic and relational operators, any bitwise operations should be enclosed in parentheses to ensure accurate execution.</span></span>  
  
## <a name="data-types"></a><span data-ttu-id="635c9-122">資料類型</span><span class="sxs-lookup"><span data-stu-id="635c9-122">Data Types</span></span>  

 <span data-ttu-id="635c9-123">若為布林值否定，則結果的資料類型為 `Boolean` 。</span><span class="sxs-lookup"><span data-stu-id="635c9-123">For a Boolean negation, the data type of the result is `Boolean`.</span></span> <span data-ttu-id="635c9-124">針對位否定，結果資料類型與的結果相同 `expression` 。</span><span class="sxs-lookup"><span data-stu-id="635c9-124">For a bitwise negation, the result data type is the same as that of `expression`.</span></span> <span data-ttu-id="635c9-125">但是，如果 expression 為 `Decimal` ，則結果為 `Long` 。</span><span class="sxs-lookup"><span data-stu-id="635c9-125">However, if expression is `Decimal`, the result is `Long`.</span></span>  
  
## <a name="overloading"></a><span data-ttu-id="635c9-126">多載化</span><span class="sxs-lookup"><span data-stu-id="635c9-126">Overloading</span></span>  

 <span data-ttu-id="635c9-127">可以多載 `Not` 運算子*overloaded*，這表示類別或結構在其運算元具有該類別或結構的型別時，可以重新定義其行為。</span><span class="sxs-lookup"><span data-stu-id="635c9-127">The `Not` operator can be *overloaded*, which means that a class or structure can redefine its behavior when its operand has the type of that class or structure.</span></span> <span data-ttu-id="635c9-128">如果您的程式碼在這類類別或結構上使用這個運算子，請務必瞭解其重新定義的行為。</span><span class="sxs-lookup"><span data-stu-id="635c9-128">If your code uses this operator on such a class or structure, be sure you understand its redefined behavior.</span></span> <span data-ttu-id="635c9-129">如需詳細資訊，請參閱 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。</span><span class="sxs-lookup"><span data-stu-id="635c9-129">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="635c9-130">範例</span><span class="sxs-lookup"><span data-stu-id="635c9-130">Example</span></span>  

 <span data-ttu-id="635c9-131">下列範例會使用 `Not` 運算子來執行運算式的邏輯否定 `Boolean` 。</span><span class="sxs-lookup"><span data-stu-id="635c9-131">The following example uses the `Not` operator to perform logical negation on a `Boolean` expression.</span></span> <span data-ttu-id="635c9-132">結果是 `Boolean` 代表運算式值反轉的值。</span><span class="sxs-lookup"><span data-stu-id="635c9-132">The result is a `Boolean` value that represents the reverse of the value of the expression.</span></span>  
  
 [!code-vb[VbVbalrOperators#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#33)]  
  
 <span data-ttu-id="635c9-133">上述範例會分別產生和的結果 `False` `True` 。</span><span class="sxs-lookup"><span data-stu-id="635c9-133">The preceding example produces results of `False` and `True`, respectively.</span></span>  
  
## <a name="example"></a><span data-ttu-id="635c9-134">範例</span><span class="sxs-lookup"><span data-stu-id="635c9-134">Example</span></span>  

 <span data-ttu-id="635c9-135">下列範例會使用 `Not` 運算子來執行數值運算式之個別位的邏輯否定。</span><span class="sxs-lookup"><span data-stu-id="635c9-135">The following example uses the `Not` operator to perform logical negation of the individual bits of a numeric expression.</span></span> <span data-ttu-id="635c9-136">結果模式中的位會設定為運算元模式中對應位的反向，包括正負號位。</span><span class="sxs-lookup"><span data-stu-id="635c9-136">The bit in the result pattern is set to the reverse of the corresponding bit in the operand pattern, including the sign bit.</span></span>  
  
 [!code-vb[VbVbalrOperators#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#34)]  
  
 <span data-ttu-id="635c9-137">上述範例會分別產生–11、-9 和–7的結果。</span><span class="sxs-lookup"><span data-stu-id="635c9-137">The preceding example produces results of –11, –9, and –7, respectively.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="635c9-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="635c9-138">See also</span></span>

- [<span data-ttu-id="635c9-139">邏輯/位元運算子 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="635c9-139">Logical/Bitwise Operators (Visual Basic)</span></span>](logical-bitwise-operators.md)
- [<span data-ttu-id="635c9-140">Visual Basic 中的運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="635c9-140">Operator Precedence in Visual Basic</span></span>](operator-precedence.md)
- [<span data-ttu-id="635c9-141">依功能列出運算子</span><span class="sxs-lookup"><span data-stu-id="635c9-141">Operators Listed by Functionality</span></span>](operators-listed-by-functionality.md)
- [<span data-ttu-id="635c9-142">Visual Basic 中的邏輯運算子和位元運算子</span><span class="sxs-lookup"><span data-stu-id="635c9-142">Logical and Bitwise Operators in Visual Basic</span></span>](../../programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
