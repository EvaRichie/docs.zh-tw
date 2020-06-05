---
title: / 運算子
ms.date: 07/20/2015
f1_keywords:
- vb./
helpviewer_keywords:
- division operator [Visual Basic], floating point
- floating-point numbers [Visual Basic], division operator
- slash (/) operator
- zero, division by zero
- operators [Visual Basic], arithmetic
- arithmetic operators [Visual Basic], division
- division [Visual Basic], by zero
- operators [Visual Basic], division
- division operator [Visual Basic], syntax
- / operator [Visual Basic]
- math operators [Visual Basic]
ms.assetid: 335e97f2-c434-439e-9064-76973a051101
ms.openlocfilehash: e9400b50a84522f87a9a2ea4cd05b479d7a4538e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371164"
---
# <a name="-operator-visual-basic"></a><span data-ttu-id="dc712-102">/ 運算子 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="dc712-102">/ Operator (Visual Basic)</span></span>
<span data-ttu-id="dc712-103">兩數相除並傳回浮點結果。</span><span class="sxs-lookup"><span data-stu-id="dc712-103">Divides two numbers and returns a floating-point result.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="dc712-104">語法</span><span class="sxs-lookup"><span data-stu-id="dc712-104">Syntax</span></span>  
  
```vb  
expression1 / expression2  
```  
  
## <a name="parts"></a><span data-ttu-id="dc712-105">組件</span><span class="sxs-lookup"><span data-stu-id="dc712-105">Parts</span></span>  
 `expression1`  
 <span data-ttu-id="dc712-106">必要。</span><span class="sxs-lookup"><span data-stu-id="dc712-106">Required.</span></span> <span data-ttu-id="dc712-107">任何數值運算式。</span><span class="sxs-lookup"><span data-stu-id="dc712-107">Any numeric expression.</span></span>  
  
 `expression2`  
 <span data-ttu-id="dc712-108">必要。</span><span class="sxs-lookup"><span data-stu-id="dc712-108">Required.</span></span> <span data-ttu-id="dc712-109">任何數值運算式。</span><span class="sxs-lookup"><span data-stu-id="dc712-109">Any numeric expression.</span></span>  
  
## <a name="supported-types"></a><span data-ttu-id="dc712-110">支援的型別</span><span class="sxs-lookup"><span data-stu-id="dc712-110">Supported Types</span></span>  
 <span data-ttu-id="dc712-111">所有數數值型別，包括不帶正負號的和浮點類型，以及 `Decimal` 。</span><span class="sxs-lookup"><span data-stu-id="dc712-111">All numeric types, including the unsigned and floating-point types and `Decimal`.</span></span>  
  
## <a name="result"></a><span data-ttu-id="dc712-112">結果</span><span class="sxs-lookup"><span data-stu-id="dc712-112">Result</span></span>  
 <span data-ttu-id="dc712-113">結果是除以的完整商 `expression1` `expression2` ，包括任何餘數。</span><span class="sxs-lookup"><span data-stu-id="dc712-113">The result is the full quotient of `expression1` divided by `expression2`, including any remainder.</span></span>  
  
 <span data-ttu-id="dc712-114">[\ 運算子（Visual Basic）](integer-division-operator.md)會傳回整數商，這會捨棄餘數。</span><span class="sxs-lookup"><span data-stu-id="dc712-114">The [\ Operator (Visual Basic)](integer-division-operator.md) returns the integer quotient, which drops the remainder.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="dc712-115">備註</span><span class="sxs-lookup"><span data-stu-id="dc712-115">Remarks</span></span>  
 <span data-ttu-id="dc712-116">結果的資料類型取決於運算元的類型。</span><span class="sxs-lookup"><span data-stu-id="dc712-116">The data type of the result depends on the types of the operands.</span></span> <span data-ttu-id="dc712-117">下表顯示如何判斷結果的資料類型。</span><span class="sxs-lookup"><span data-stu-id="dc712-117">The following table shows how the data type of the result is determined.</span></span>  
  
|<span data-ttu-id="dc712-118">運算元資料類型</span><span class="sxs-lookup"><span data-stu-id="dc712-118">Operand data types</span></span>|<span data-ttu-id="dc712-119">結果資料類型</span><span class="sxs-lookup"><span data-stu-id="dc712-119">Result data type</span></span>|  
|------------------------|----------------------|  
|<span data-ttu-id="dc712-120">這兩個運算式都是整數資料類型（[SByte](../data-types/sbyte-data-type.md)、 [Byte](../data-types/byte-data-type.md)、 [Short](../data-types/short-data-type.md)、 [UShort](../data-types/ushort-data-type.md)、 [Integer](../data-types/integer-data-type.md)、 [UInteger](../data-types/uinteger-data-type.md)、 [Long](../data-types/long-data-type.md)、 [ULong](../data-types/ulong-data-type.md)）</span><span class="sxs-lookup"><span data-stu-id="dc712-120">Both expressions are integral data types ([SByte](../data-types/sbyte-data-type.md), [Byte](../data-types/byte-data-type.md), [Short](../data-types/short-data-type.md), [UShort](../data-types/ushort-data-type.md), [Integer](../data-types/integer-data-type.md), [UInteger](../data-types/uinteger-data-type.md), [Long](../data-types/long-data-type.md), [ULong](../data-types/ulong-data-type.md))</span></span>|`Double`|  
|<span data-ttu-id="dc712-121">一個運算式是[單一](../data-types/single-data-type.md)資料類型，另一個則不是[雙精度浮點數](../data-types/double-data-type.md)</span><span class="sxs-lookup"><span data-stu-id="dc712-121">One expression is a [Single](../data-types/single-data-type.md) data type and the other is not a [Double](../data-types/double-data-type.md)</span></span>|`Single`|  
|<span data-ttu-id="dc712-122">一個運算式是[Decimal](../data-types/decimal-data-type.md)資料型別，另一個則不是[單一](../data-types/single-data-type.md)或[雙精度浮點數](../data-types/double-data-type.md)</span><span class="sxs-lookup"><span data-stu-id="dc712-122">One expression is a [Decimal](../data-types/decimal-data-type.md) data type and the other is not a [Single](../data-types/single-data-type.md) or a [Double](../data-types/double-data-type.md)</span></span>|`Decimal`|  
|<span data-ttu-id="dc712-123">任一運算式是[Double](../data-types/double-data-type.md)資料類型</span><span class="sxs-lookup"><span data-stu-id="dc712-123">Either expression is a [Double](../data-types/double-data-type.md) data type</span></span>|`Double`|  
  
 <span data-ttu-id="dc712-124">在執行除法之前，任何整數數值運算式會擴展為 `Double` 。</span><span class="sxs-lookup"><span data-stu-id="dc712-124">Before division is performed, any integral numeric expressions are widened to `Double`.</span></span> <span data-ttu-id="dc712-125">如果您將結果指派給整數資料類型，Visual Basic 會嘗試將的結果從轉換成 `Double` 該類型。</span><span class="sxs-lookup"><span data-stu-id="dc712-125">If you assign the result to an integral data type, Visual Basic attempts to convert the result from `Double` to that type.</span></span> <span data-ttu-id="dc712-126">如果結果不符合該類型，這可能會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="dc712-126">This can throw an exception if the result does not fit in that type.</span></span> <span data-ttu-id="dc712-127">特別是，請參閱此說明頁面上的「嘗試除數為零」。</span><span class="sxs-lookup"><span data-stu-id="dc712-127">In particular, see "Attempted Division by Zero" on this Help page.</span></span>  
  
 <span data-ttu-id="dc712-128">如果 `expression1` 或 `expression2` 評估為[沒有任何](../nothing.md)值，則會將它視為零。</span><span class="sxs-lookup"><span data-stu-id="dc712-128">If `expression1` or `expression2` evaluates to [Nothing](../nothing.md), it is treated as zero.</span></span>  
  
## <a name="attempted-division-by-zero"></a><span data-ttu-id="dc712-129">嘗試除數為零</span><span class="sxs-lookup"><span data-stu-id="dc712-129">Attempted Division by Zero</span></span>  
 <span data-ttu-id="dc712-130">如果 `expression2` 評估為零，則 `/` 運算子的行為會因不同的運算元資料類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="dc712-130">If `expression2` evaluates to zero, the `/` operator behaves differently for different operand data types.</span></span> <span data-ttu-id="dc712-131">下表顯示可能的行為。</span><span class="sxs-lookup"><span data-stu-id="dc712-131">The following table shows the possible behaviors.</span></span>  
  
|<span data-ttu-id="dc712-132">運算元資料類型</span><span class="sxs-lookup"><span data-stu-id="dc712-132">Operand data types</span></span>|<span data-ttu-id="dc712-133">當 `expression2` 為零時的行為</span><span class="sxs-lookup"><span data-stu-id="dc712-133">Behavior if `expression2` is zero</span></span>|  
|------------------------|---------------------------------------|  
|<span data-ttu-id="dc712-134">浮點（ `Single` 或 `Double` ）</span><span class="sxs-lookup"><span data-stu-id="dc712-134">Floating-point (`Single` or `Double`)</span></span>|<span data-ttu-id="dc712-135"><xref:System.Double.PositiveInfinity> <xref:System.Double.NegativeInfinity> <xref:System.Double.NaN> 如果 `expression1` 同時為零，則傳回無限大（或），或（不是數位）</span><span class="sxs-lookup"><span data-stu-id="dc712-135">Returns infinity (<xref:System.Double.PositiveInfinity> or <xref:System.Double.NegativeInfinity>), or <xref:System.Double.NaN> (not a number) if `expression1` is also zero</span></span>|  
|`Decimal`|<span data-ttu-id="dc712-136">引發<xref:System.DivideByZeroException></span><span class="sxs-lookup"><span data-stu-id="dc712-136">Throws <xref:System.DivideByZeroException></span></span>|  
|<span data-ttu-id="dc712-137">整數（帶正負號或不帶正負號）</span><span class="sxs-lookup"><span data-stu-id="dc712-137">Integral (signed or unsigned)</span></span>|<span data-ttu-id="dc712-138"><xref:System.OverflowException>因為整數類型無法接受 <xref:System.Double.PositiveInfinity> 、或，所以嘗試轉換回整數類資料類型 <xref:System.Double.NegativeInfinity><xref:System.Double.NaN></span><span class="sxs-lookup"><span data-stu-id="dc712-138">Attempted conversion back to integral type throws <xref:System.OverflowException> because integral types cannot accept <xref:System.Double.PositiveInfinity>, <xref:System.Double.NegativeInfinity>, or <xref:System.Double.NaN></span></span>|  
  
> [!NOTE]
> <span data-ttu-id="dc712-139">`/`運算子可以多載*overloaded*，這表示當運算元具有該類別或結構的類型時，類別或結構可以重新定義其行為。</span><span class="sxs-lookup"><span data-stu-id="dc712-139">The `/` operator can be *overloaded*, which means that a class or structure can redefine its behavior when an operand has the type of that class or structure.</span></span> <span data-ttu-id="dc712-140">如果您的程式碼在這類類別或結構上使用這個運算子，請務必瞭解其已重新定義的行為。</span><span class="sxs-lookup"><span data-stu-id="dc712-140">If your code uses this operator on such a class or structure, be sure you understand its redefined behavior.</span></span> <span data-ttu-id="dc712-141">如需詳細資訊，請參閱 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。</span><span class="sxs-lookup"><span data-stu-id="dc712-141">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="dc712-142">範例</span><span class="sxs-lookup"><span data-stu-id="dc712-142">Example</span></span>  
 <span data-ttu-id="dc712-143">這個範例會使用 `/` 運算子來執行浮點除法。</span><span class="sxs-lookup"><span data-stu-id="dc712-143">This example uses the `/` operator to perform floating-point division.</span></span> <span data-ttu-id="dc712-144">結果為兩個運算元的商。</span><span class="sxs-lookup"><span data-stu-id="dc712-144">The result is the quotient of the two operands.</span></span>  
  
 [!code-vb[VbVbalrOperators#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#16)]  
  
 <span data-ttu-id="dc712-145">上述範例中的運算式會傳回2.5 和3.333333 的值。</span><span class="sxs-lookup"><span data-stu-id="dc712-145">The expressions in the preceding example return values of 2.5 and 3.333333.</span></span> <span data-ttu-id="dc712-146">請注意， `Double` 即使兩個運算元都是整數常數，結果一律是浮點（）。</span><span class="sxs-lookup"><span data-stu-id="dc712-146">Note that the result is always floating-point (`Double`), even though both operands are integer constants.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="dc712-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="dc712-147">See also</span></span>

- [<span data-ttu-id="dc712-148">/= 運算子（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="dc712-148">/= Operator (Visual Basic)</span></span>](floating-point-division-assignment-operator.md)
- [<span data-ttu-id="dc712-149">\ 運算子（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="dc712-149">\ Operator (Visual Basic)</span></span>](integer-division-operator.md)
- [<span data-ttu-id="dc712-150">運算子結果的資料類型</span><span class="sxs-lookup"><span data-stu-id="dc712-150">Data Types of Operator Results</span></span>](data-types-of-operator-results.md)
- [<span data-ttu-id="dc712-151">算術運算子</span><span class="sxs-lookup"><span data-stu-id="dc712-151">Arithmetic Operators</span></span>](arithmetic-operators.md)
- [<span data-ttu-id="dc712-152">Visual Basic 中的運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="dc712-152">Operator Precedence in Visual Basic</span></span>](operator-precedence.md)
- [<span data-ttu-id="dc712-153">依功能列出運算子</span><span class="sxs-lookup"><span data-stu-id="dc712-153">Operators Listed by Functionality</span></span>](operators-listed-by-functionality.md)
- [<span data-ttu-id="dc712-154">Visual Basic 的算術運算子</span><span class="sxs-lookup"><span data-stu-id="dc712-154">Arithmetic Operators in Visual Basic</span></span>](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
