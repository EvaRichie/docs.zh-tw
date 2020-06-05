---
title: '\ 運算子'
ms.date: 07/20/2015
f1_keywords:
- vb.\
- '\'
helpviewer_keywords:
- division operator [Visual Basic], integer
- integer division operator [Visual Basic]
- zero, division by zero
- arithmetic operators [Visual Basic], division
- division [Visual Basic], by zero
- backslash (\) [Visual Basic]
- '\ operator [Visual Basic]'
- integer quotient
- math operators [Visual Basic]
- quotients, integer
- truncation [Visual Basic], integer division
ms.assetid: 4b0ee347-950c-45c9-8e23-54bc85df208e
ms.openlocfilehash: 1f8095afc5f096928b946607adc715af49827022
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370878"
---
# <a name="-operator-visual-basic"></a><span data-ttu-id="b9cd1-102">\ 運算子 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b9cd1-102">\ Operator (Visual Basic)</span></span>
<span data-ttu-id="b9cd1-103">兩數相除並傳回整數結果。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-103">Divides two numbers and returns an integer result.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b9cd1-104">語法</span><span class="sxs-lookup"><span data-stu-id="b9cd1-104">Syntax</span></span>  
  
```vb  
expression1 \ expression2  
```  
  
## <a name="parts"></a><span data-ttu-id="b9cd1-105">組件</span><span class="sxs-lookup"><span data-stu-id="b9cd1-105">Parts</span></span>  
 `expression1`  
 <span data-ttu-id="b9cd1-106">必要。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-106">Required.</span></span> <span data-ttu-id="b9cd1-107">任何數值運算式。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-107">Any numeric expression.</span></span>  
  
 `expression2`  
 <span data-ttu-id="b9cd1-108">必要。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-108">Required.</span></span> <span data-ttu-id="b9cd1-109">任何數值運算式。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-109">Any numeric expression.</span></span>  
  
## <a name="supported-types"></a><span data-ttu-id="b9cd1-110">支援的型別</span><span class="sxs-lookup"><span data-stu-id="b9cd1-110">Supported Types</span></span>  
 <span data-ttu-id="b9cd1-111">所有數數值型別，包括不帶正負號的和浮點類型，以及 `Decimal` 。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-111">All numeric types, including the unsigned and floating-point types and `Decimal`.</span></span>  
  
## <a name="result"></a><span data-ttu-id="b9cd1-112">結果</span><span class="sxs-lookup"><span data-stu-id="b9cd1-112">Result</span></span>  
 <span data-ttu-id="b9cd1-113">結果是除以的整數商 `expression1` `expression2` ，這會捨棄任何餘數，而且只會保留整數部分。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-113">The result is the integer quotient of `expression1` divided by `expression2`, which discards any remainder and retains only the integer portion.</span></span> <span data-ttu-id="b9cd1-114">這就是所謂的*截斷*。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-114">This is known as *truncation*.</span></span>  
  
 <span data-ttu-id="b9cd1-115">結果資料類型是適用于和之資料類型的數數值型別 `expression1` `expression2` 。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-115">The result data type is a numeric type appropriate for the data types of `expression1` and `expression2`.</span></span> <span data-ttu-id="b9cd1-116">請參閱[運算子結果的資料類型](data-types-of-operator-results.md)中的「整數算術」資料表。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-116">See the "Integer Arithmetic" tables in [Data Types of Operator Results](data-types-of-operator-results.md).</span></span>  
  
 <span data-ttu-id="b9cd1-117">[/運算子（Visual Basic）](floating-point-division-operator.md)會傳回完整商，這會保留分數部分中的餘數。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-117">The [/ Operator (Visual Basic)](floating-point-division-operator.md) returns the full quotient, which retains the remainder in the fractional portion.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b9cd1-118">備註</span><span class="sxs-lookup"><span data-stu-id="b9cd1-118">Remarks</span></span>  
 <span data-ttu-id="b9cd1-119">在執行除法之前，Visual Basic 嘗試將任何浮點數值運算式轉換成 `Long` 。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-119">Before performing the division, Visual Basic attempts to convert any floating-point numeric expression to `Long`.</span></span> <span data-ttu-id="b9cd1-120">如果 `Option Strict` 為 `On` ，則會發生編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-120">If `Option Strict` is `On`, a compiler error occurs.</span></span> <span data-ttu-id="b9cd1-121">如果 `Option Strict` 是 `Off` ， <xref:System.OverflowException> 如果值超出[LONG 資料型別](../data-types/long-data-type.md)的範圍，就可能發生。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-121">If `Option Strict` is `Off`, an <xref:System.OverflowException> is possible if the value is outside the range of the [Long Data Type](../data-types/long-data-type.md).</span></span> <span data-ttu-id="b9cd1-122">轉換為 `Long` 時，也會受限於四*進位*。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-122">The conversion to `Long` is also subject to *banker's rounding*.</span></span> <span data-ttu-id="b9cd1-123">如需詳細資訊，請參閱[類型轉換函數](../functions/type-conversion-functions.md)中的「小數部分」。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-123">For more information, see "Fractional Parts" in [Type Conversion Functions](../functions/type-conversion-functions.md).</span></span>  
  
 <span data-ttu-id="b9cd1-124">如果 `expression1` 或 `expression2` 評估為[沒有任何](../nothing.md)值，則會將它視為零。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-124">If `expression1` or `expression2` evaluates to [Nothing](../nothing.md), it is treated as zero.</span></span>  
  
## <a name="attempted-division-by-zero"></a><span data-ttu-id="b9cd1-125">嘗試除數為零</span><span class="sxs-lookup"><span data-stu-id="b9cd1-125">Attempted Division by Zero</span></span>  
 <span data-ttu-id="b9cd1-126">如果 `expression2` 評估為零，則運算子會擲回 `\` <xref:System.DivideByZeroException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-126">If `expression2` evaluates to zero, the `\` operator throws a <xref:System.DivideByZeroException> exception.</span></span> <span data-ttu-id="b9cd1-127">這適用于運算元的所有數值資料類型。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-127">This is true for all numeric data types of the operands.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b9cd1-128">`\`運算子可以多載*overloaded*，這表示當運算元具有該類別或結構的類型時，類別或結構可以重新定義其行為。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-128">The `\` operator can be *overloaded*, which means that a class or structure can redefine its behavior when an operand has the type of that class or structure.</span></span> <span data-ttu-id="b9cd1-129">如果您的程式碼在這類類別或結構上使用這個運算子，請務必瞭解其已重新定義的行為。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-129">If your code uses this operator on such a class or structure, be sure you understand its redefined behavior.</span></span> <span data-ttu-id="b9cd1-130">如需詳細資訊，請參閱 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-130">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="b9cd1-131">範例</span><span class="sxs-lookup"><span data-stu-id="b9cd1-131">Example</span></span>  
 <span data-ttu-id="b9cd1-132">下列範例會使用 `\` 運算子來執行整數除法。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-132">The following example uses the `\` operator to perform integer division.</span></span> <span data-ttu-id="b9cd1-133">結果是一個整數，代表兩個運算元的整數商，餘數會被捨棄。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-133">The result is an integer that represents the integer quotient of the two operands, with the remainder discarded.</span></span>  
  
 [!code-vb[VbVbalrOperators#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#18)]  
  
 <span data-ttu-id="b9cd1-134">上述範例中的運算式會分別傳回2、3、33和-22 的值。</span><span class="sxs-lookup"><span data-stu-id="b9cd1-134">The expressions in the preceding example return values of 2, 3, 33, and -22, respectively.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b9cd1-135">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b9cd1-135">See also</span></span>

- [<span data-ttu-id="b9cd1-136">\\= 運算子</span><span class="sxs-lookup"><span data-stu-id="b9cd1-136">\\= Operator</span></span>](integer-division-assignment-operator.md)
- [<span data-ttu-id="b9cd1-137">/運算子（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="b9cd1-137">/ Operator (Visual Basic)</span></span>](floating-point-division-operator.md)
- [<span data-ttu-id="b9cd1-138">Long</span><span class="sxs-lookup"><span data-stu-id="b9cd1-138">Option Strict Statement</span></span>](../statements/option-strict-statement.md)
- [<span data-ttu-id="b9cd1-139">算術運算子</span><span class="sxs-lookup"><span data-stu-id="b9cd1-139">Arithmetic Operators</span></span>](arithmetic-operators.md)
- [<span data-ttu-id="b9cd1-140">Visual Basic 中的運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="b9cd1-140">Operator Precedence in Visual Basic</span></span>](operator-precedence.md)
- [<span data-ttu-id="b9cd1-141">依功能列出運算子</span><span class="sxs-lookup"><span data-stu-id="b9cd1-141">Operators Listed by Functionality</span></span>](operators-listed-by-functionality.md)
- [<span data-ttu-id="b9cd1-142">Visual Basic 的算術運算子</span><span class="sxs-lookup"><span data-stu-id="b9cd1-142">Arithmetic Operators in Visual Basic</span></span>](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
