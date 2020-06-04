---
title: << 運算子
ms.date: 07/20/2015
f1_keywords:
- vb.<<
helpviewer_keywords:
- bit shift operators [Visual Basic]
- << operator [Visual Basic]
- operator <<, Visual Basic left shift operator
ms.assetid: fdb93d25-81ba-417f-b808-41207bfb8440
ms.openlocfilehash: 1128b32a739e7dbf3893dcd19b37247cd4643c85
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370631"
---
# <a name="-operator-visual-basic"></a><span data-ttu-id="f9c09-102">\<\<運算子（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="f9c09-102">\<\< Operator (Visual Basic)</span></span>
<span data-ttu-id="f9c09-103">在位模式上執行算術左移位。</span><span class="sxs-lookup"><span data-stu-id="f9c09-103">Performs an arithmetic left shift on a bit pattern.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f9c09-104">語法</span><span class="sxs-lookup"><span data-stu-id="f9c09-104">Syntax</span></span>  
  
```vb  
result = pattern << amount  
```  
  
## <a name="parts"></a><span data-ttu-id="f9c09-105">組件</span><span class="sxs-lookup"><span data-stu-id="f9c09-105">Parts</span></span>  
 `result`  
 <span data-ttu-id="f9c09-106">必要。</span><span class="sxs-lookup"><span data-stu-id="f9c09-106">Required.</span></span> <span data-ttu-id="f9c09-107">整數數值。</span><span class="sxs-lookup"><span data-stu-id="f9c09-107">Integral numeric value.</span></span> <span data-ttu-id="f9c09-108">位元模式移位的結果。</span><span class="sxs-lookup"><span data-stu-id="f9c09-108">The result of shifting the bit pattern.</span></span> <span data-ttu-id="f9c09-109">資料型別與 `pattern` 的型別相同。</span><span class="sxs-lookup"><span data-stu-id="f9c09-109">The data type is the same as that of `pattern`.</span></span>  
  
 `pattern`  
 <span data-ttu-id="f9c09-110">必要。</span><span class="sxs-lookup"><span data-stu-id="f9c09-110">Required.</span></span> <span data-ttu-id="f9c09-111">整數值運算式。</span><span class="sxs-lookup"><span data-stu-id="f9c09-111">Integral numeric expression.</span></span> <span data-ttu-id="f9c09-112">要移位的位元模式。</span><span class="sxs-lookup"><span data-stu-id="f9c09-112">The bit pattern to be shifted.</span></span> <span data-ttu-id="f9c09-113">資料型別必須是整數類資料型別 (Integral Type) (`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long` 或 `ULong`)。</span><span class="sxs-lookup"><span data-stu-id="f9c09-113">The data type must be an integral type (`SByte`, `Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, or `ULong`).</span></span>  
  
 `amount`  
 <span data-ttu-id="f9c09-114">必要。</span><span class="sxs-lookup"><span data-stu-id="f9c09-114">Required.</span></span> <span data-ttu-id="f9c09-115">數值運算式。</span><span class="sxs-lookup"><span data-stu-id="f9c09-115">Numeric expression.</span></span> <span data-ttu-id="f9c09-116">位元模式移位的位元數。</span><span class="sxs-lookup"><span data-stu-id="f9c09-116">The number of bits to shift the bit pattern.</span></span> <span data-ttu-id="f9c09-117">資料型別必須是 `Integer` 或擴展至 `Integer`。</span><span class="sxs-lookup"><span data-stu-id="f9c09-117">The data type must be `Integer` or widen to `Integer`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f9c09-118">備註</span><span class="sxs-lookup"><span data-stu-id="f9c09-118">Remarks</span></span>  
 <span data-ttu-id="f9c09-119">算術移位不是迴圈的，這表示不會在另一端重新進入從結果的一端移位的位。</span><span class="sxs-lookup"><span data-stu-id="f9c09-119">Arithmetic shifts are not circular, which means the bits shifted off one end of the result are not reintroduced at the other end.</span></span> <span data-ttu-id="f9c09-120">在算術左移位中，會捨棄超出結果資料類型範圍的位，而且右邊空出的位位置會設定為零。</span><span class="sxs-lookup"><span data-stu-id="f9c09-120">In an arithmetic left shift, the bits shifted beyond the range of the result data type are discarded, and the bit positions vacated on the right are set to zero.</span></span>  
  
 <span data-ttu-id="f9c09-121">為了避免比結果所能保存的位數更多，Visual Basic 會以 `amount` 對應至資料類型的大小遮罩來遮罩的值 `pattern` 。</span><span class="sxs-lookup"><span data-stu-id="f9c09-121">To prevent a shift by more bits than the result can hold, Visual Basic masks the value of `amount` with a size mask that corresponds to the data type of `pattern`.</span></span> <span data-ttu-id="f9c09-122">這些值的二進位和會用於移位量。</span><span class="sxs-lookup"><span data-stu-id="f9c09-122">The binary AND of these values is used for the shift amount.</span></span> <span data-ttu-id="f9c09-123">大小遮罩如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9c09-123">The size masks are as follows:</span></span>  
  
|<span data-ttu-id="f9c09-124">的資料類型`pattern`</span><span class="sxs-lookup"><span data-stu-id="f9c09-124">Data type of `pattern`</span></span>|<span data-ttu-id="f9c09-125">大小遮罩（十進位）</span><span class="sxs-lookup"><span data-stu-id="f9c09-125">Size mask (decimal)</span></span>|<span data-ttu-id="f9c09-126">大小遮罩（十六進位）</span><span class="sxs-lookup"><span data-stu-id="f9c09-126">Size mask (hexadecimal)</span></span>|  
|----------------------------|---------------------------|-------------------------------|  
|<span data-ttu-id="f9c09-127">`SByte`, `Byte`</span><span class="sxs-lookup"><span data-stu-id="f9c09-127">`SByte`, `Byte`</span></span>|<span data-ttu-id="f9c09-128">7</span><span class="sxs-lookup"><span data-stu-id="f9c09-128">7</span></span>|<span data-ttu-id="f9c09-129">&H00000007</span><span class="sxs-lookup"><span data-stu-id="f9c09-129">&H00000007</span></span>|  
|<span data-ttu-id="f9c09-130">`Short`, `UShort`</span><span class="sxs-lookup"><span data-stu-id="f9c09-130">`Short`, `UShort`</span></span>|<span data-ttu-id="f9c09-131">15</span><span class="sxs-lookup"><span data-stu-id="f9c09-131">15</span></span>|<span data-ttu-id="f9c09-132">&H0000000F</span><span class="sxs-lookup"><span data-stu-id="f9c09-132">&H0000000F</span></span>|  
|<span data-ttu-id="f9c09-133">`Integer`, `UInteger`</span><span class="sxs-lookup"><span data-stu-id="f9c09-133">`Integer`, `UInteger`</span></span>|<span data-ttu-id="f9c09-134">31</span><span class="sxs-lookup"><span data-stu-id="f9c09-134">31</span></span>|<span data-ttu-id="f9c09-135">&H0000001F</span><span class="sxs-lookup"><span data-stu-id="f9c09-135">&H0000001F</span></span>|  
|<span data-ttu-id="f9c09-136">`Long`, `ULong`</span><span class="sxs-lookup"><span data-stu-id="f9c09-136">`Long`, `ULong`</span></span>|<span data-ttu-id="f9c09-137">63</span><span class="sxs-lookup"><span data-stu-id="f9c09-137">63</span></span>|<span data-ttu-id="f9c09-138">&H0000003F</span><span class="sxs-lookup"><span data-stu-id="f9c09-138">&H0000003F</span></span>|  
  
 <span data-ttu-id="f9c09-139">如果 `amount` 為零，則的值與的 `result` 值相同 `pattern` 。</span><span class="sxs-lookup"><span data-stu-id="f9c09-139">If `amount` is zero, the value of `result` is identical to the value of `pattern`.</span></span> <span data-ttu-id="f9c09-140">如果 `amount` 是負數，則會將它視為不帶正負號的值，並以適當的大小遮罩加以遮罩。</span><span class="sxs-lookup"><span data-stu-id="f9c09-140">If `amount` is negative, it is taken as an unsigned value and masked with the appropriate size mask.</span></span>  
  
 <span data-ttu-id="f9c09-141">算術移位絕不會產生溢位例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f9c09-141">Arithmetic shifts never generate overflow exceptions.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="f9c09-142">`<<`運算子可以多載*overloaded*，這表示當運算元具有該類別或結構的類型時，類別或結構可以重新定義其行為。</span><span class="sxs-lookup"><span data-stu-id="f9c09-142">The `<<` operator can be *overloaded*, which means that a class or structure can redefine its behavior when an operand has the type of that class or structure.</span></span> <span data-ttu-id="f9c09-143">如果您的程式碼在這類類別或結構上使用這個運算子，請確定您瞭解其已重新定義的行為。</span><span class="sxs-lookup"><span data-stu-id="f9c09-143">If your code uses this operator on such a class or structure, be sure that you understand its redefined behavior.</span></span> <span data-ttu-id="f9c09-144">如需詳細資訊，請參閱 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。</span><span class="sxs-lookup"><span data-stu-id="f9c09-144">For more information, see [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="f9c09-145">範例</span><span class="sxs-lookup"><span data-stu-id="f9c09-145">Example</span></span>  
 <span data-ttu-id="f9c09-146">下列範例會使用 `<<` 運算子來執行整數值的算術左移位。</span><span class="sxs-lookup"><span data-stu-id="f9c09-146">The following example uses the `<<` operator to perform arithmetic left shifts on integral values.</span></span> <span data-ttu-id="f9c09-147">結果的資料類型一律會與移動的運算式相同。</span><span class="sxs-lookup"><span data-stu-id="f9c09-147">The result always has the same data type as that of the expression being shifted.</span></span>  
  
 [!code-vb[VbVbalrOperators#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#12)]  
  
 <span data-ttu-id="f9c09-148">上一個範例的結果如下所示：</span><span class="sxs-lookup"><span data-stu-id="f9c09-148">The results of the previous example are as follows:</span></span>  
  
- <span data-ttu-id="f9c09-149">`result1`為192（0000 0000 1100 0000）。</span><span class="sxs-lookup"><span data-stu-id="f9c09-149">`result1` is 192 (0000 0000 1100 0000).</span></span>  
  
- <span data-ttu-id="f9c09-150">`result2`為3072（0000 1100 0000 0000）。</span><span class="sxs-lookup"><span data-stu-id="f9c09-150">`result2` is 3072 (0000 1100 0000 0000).</span></span>  
  
- <span data-ttu-id="f9c09-151">`result3`為-32768 （1000 0000 0000 0000）。</span><span class="sxs-lookup"><span data-stu-id="f9c09-151">`result3` is -32768 (1000 0000 0000 0000).</span></span>  
  
- <span data-ttu-id="f9c09-152">`result4`為384（0000 0001 1000 0000）。</span><span class="sxs-lookup"><span data-stu-id="f9c09-152">`result4` is 384 (0000 0001 1000 0000).</span></span>  
  
- <span data-ttu-id="f9c09-153">`result5`為0（向左移動15個位置）。</span><span class="sxs-lookup"><span data-stu-id="f9c09-153">`result5` is 0 (shifted 15 places to the left).</span></span>  
  
 <span data-ttu-id="f9c09-154">的移位量 `result4` 會計算為17和15，這等於1。</span><span class="sxs-lookup"><span data-stu-id="f9c09-154">The shift amount for `result4` is calculated as 17 AND 15, which equals 1.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f9c09-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f9c09-155">See also</span></span>

- [<span data-ttu-id="f9c09-156">位元移位運算子</span><span class="sxs-lookup"><span data-stu-id="f9c09-156">Bit Shift Operators</span></span>](bit-shift-operators.md)
- [<span data-ttu-id="f9c09-157">指派運算子</span><span class="sxs-lookup"><span data-stu-id="f9c09-157">Assignment Operators</span></span>](assignment-operators.md)
- [<span data-ttu-id="f9c09-158"><<= 運算子</span><span class="sxs-lookup"><span data-stu-id="f9c09-158"><<= Operator</span></span>](left-shift-assignment-operator.md)
- [<span data-ttu-id="f9c09-159">Visual Basic 中的運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="f9c09-159">Operator Precedence in Visual Basic</span></span>](operator-precedence.md)
- [<span data-ttu-id="f9c09-160">依功能列出運算子</span><span class="sxs-lookup"><span data-stu-id="f9c09-160">Operators Listed by Functionality</span></span>](operators-listed-by-functionality.md)
- [<span data-ttu-id="f9c09-161">Visual Basic 的算術運算子</span><span class="sxs-lookup"><span data-stu-id="f9c09-161">Arithmetic Operators in Visual Basic</span></span>](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
