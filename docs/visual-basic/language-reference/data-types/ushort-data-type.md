---
title: UShort 資料類型
ms.date: 01/31/2018
f1_keywords:
- vb.ushort
helpviewer_keywords:
- numbers [Visual Basic], whole
- literal type characters [Visual Basic], US
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- UShort data type
- US literal type characters [Visual Basic]
ms.assetid: 138db892-665d-4ba8-9cae-d8d91c4a8f39
ms.openlocfilehash: ee31156e00059699125fd72a7f091afbb21beab0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415475"
---
# <a name="ushort-data-type-visual-basic"></a><span data-ttu-id="f2f6c-102">UShort 資料類型（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="f2f6c-102">UShort data type (Visual Basic)</span></span>

<span data-ttu-id="f2f6c-103">保留不帶正負號的16位（2位元組）整數，範圍介於0到65535之間。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-103">Holds unsigned 16-bit (2-byte) integers ranging in value from 0 through 65,535.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f2f6c-104">備註</span><span class="sxs-lookup"><span data-stu-id="f2f6c-104">Remarks</span></span>

 <span data-ttu-id="f2f6c-105">使用 `UShort` 資料類型可包含對而言太大的二進位資料 `Byte` 。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-105">Use the `UShort` data type to contain binary data too large for `Byte`.</span></span>  
  
 <span data-ttu-id="f2f6c-106">`UShort` 的預設值為 0。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-106">The default value of `UShort` is 0.</span></span>  

## <a name="literal-assignments"></a><span data-ttu-id="f2f6c-107">常值指派</span><span class="sxs-lookup"><span data-stu-id="f2f6c-107">Literal assignments</span></span>

<span data-ttu-id="f2f6c-108">您可以藉 `UShort` 由指派十進位常值、十六進位常值、八進位常值，或二進位常值（從 Visual Basic 2017）來宣告和初始化變數。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-108">You can declare and initialize a `UShort` variable by assigning it a decimal literal, a hexadecimal literal, an octal literal, or (starting with Visual Basic 2017) a binary literal.</span></span> <span data-ttu-id="f2f6c-109">如果整數常值超出 `UShort` 的範圍 (亦即，如果小於 <xref:System.UInt16.MinValue?displayProperty=nameWithType> 或大於 <xref:System.UInt16.MaxValue?displayProperty=nameWithType>)，就會發生編譯錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-109">If the integer literal is outside the range of `UShort` (that is, if it is less than <xref:System.UInt16.MinValue?displayProperty=nameWithType> or greater than <xref:System.UInt16.MaxValue?displayProperty=nameWithType>, a compilation error occurs.</span></span>

<span data-ttu-id="f2f6c-110">在下列範例中，以十進位、十六進位和二進位常值表示的整數等於65034，會指派給 `UShort` 值。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-110">In the following example, integers equal to 65,034 that are represented as decimal, hexadecimal, and binary literals are assigned to `UShort` values.</span></span>
  
[!code-vb[UShort](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UShort)]

> [!NOTE]
> <span data-ttu-id="f2f6c-111">您可以使用前置詞 `&h` 或 `&H` 來表示十六進位常值、前置詞 `&b` 或表示 `&B` 二進位常值，以及前置詞 `&o` 或 `&O` 來表示八進位常值。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-111">You use the prefix `&h` or `&H` to denote a hexadecimal literal, the prefix `&b` or `&B` to denote a binary literal, and the prefix `&o` or `&O` to denote an octal literal.</span></span> <span data-ttu-id="f2f6c-112">十進位常值沒有前置詞。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-112">Decimal literals have no prefix.</span></span>

<span data-ttu-id="f2f6c-113">從 Visual Basic 2017 開始，您也可以使用底線字元 `_` 做為數位分隔符號來增強可讀性，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-113">Starting with Visual Basic 2017, you can also use the underscore character, `_`, as a digit separator to enhance readability, as the following example shows.</span></span>

[!code-vb[UShort](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UShortS)]

<span data-ttu-id="f2f6c-114">從 Visual Basic 15.5 開始，您也可以使用底線字元（ `_` ）做為前置詞和十六進位、二進位或八進位數位之間的前置分隔符號。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-114">Starting with Visual Basic 15.5, you can also use the underscore character (`_`) as a leading separator between the prefix and the hexadecimal, binary, or octal digits.</span></span> <span data-ttu-id="f2f6c-115">例如：</span><span class="sxs-lookup"><span data-stu-id="f2f6c-115">For example:</span></span>

```vb
Dim number As UShort = &H_FF8C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

<span data-ttu-id="f2f6c-116">數值常值也可以包含 `US` 或 `us` [類型字元](../../programming-guide/language-features/data-types/type-characters.md)來表示 `UShort` 資料類型，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-116">Numeric literals can also include the `US` or `us` [type character](../../programming-guide/language-features/data-types/type-characters.md) to denote the `UShort` data type, as the following example shows.</span></span>

```vb
Dim number = &H_5826us
```

## <a name="programming-tips"></a><span data-ttu-id="f2f6c-117">程式設計提示</span><span class="sxs-lookup"><span data-stu-id="f2f6c-117">Programming tips</span></span>
  
- <span data-ttu-id="f2f6c-118">**負數。**</span><span class="sxs-lookup"><span data-stu-id="f2f6c-118">**Negative Numbers.**</span></span> <span data-ttu-id="f2f6c-119">因為 `UShort` 是不帶正負號的類型，所以不能代表負數。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-119">Because `UShort` is an unsigned type, it cannot represent a negative number.</span></span> <span data-ttu-id="f2f6c-120">如果您 `-` 在評估為類型的運算式上使用一元減號（）運算子 `UShort` ，Visual Basic 會將運算式轉換為 `Integer` first。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-120">If you use the unary minus (`-`) operator on an expression that evaluates to type `UShort`, Visual Basic converts the expression to `Integer` first.</span></span>  
  
- <span data-ttu-id="f2f6c-121">**CLS 合規性。**</span><span class="sxs-lookup"><span data-stu-id="f2f6c-121">**CLS Compliance.**</span></span> <span data-ttu-id="f2f6c-122">`UShort`資料類型不是[Common Language Specification](https://www.ecma-international.org/publications/standards/Ecma-335.htm) （CLS）的一部分，因此符合 cls 標準的程式碼無法使用使用它的元件。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-122">The `UShort` data type is not part of the [Common Language Specification](https://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS), so CLS-compliant code cannot consume a component that uses it.</span></span>
  
- <span data-ttu-id="f2f6c-123">**加寬.**</span><span class="sxs-lookup"><span data-stu-id="f2f6c-123">**Widening.**</span></span> <span data-ttu-id="f2f6c-124">`UShort`資料類型會擴大為 `Integer` 、 `UInteger` 、 `Long` 、 `ULong` 、 `Decimal` 、 `Single` 和 `Double` 。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-124">The `UShort` data type widens to `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, and `Double`.</span></span> <span data-ttu-id="f2f6c-125">這表示您可以轉換 `UShort` 成這些類型的任何一種，而不會遇到 <xref:System.OverflowException?displayProperty=nameWithType> 錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-125">This means you can convert `UShort` to any of these types without encountering a <xref:System.OverflowException?displayProperty=nameWithType> error.</span></span>  
  
- <span data-ttu-id="f2f6c-126">**輸入字元。**</span><span class="sxs-lookup"><span data-stu-id="f2f6c-126">**Type Characters.**</span></span> <span data-ttu-id="f2f6c-127">將常數值型別字元附加 `US` 到常值，會強制其成為 `UShort` 資料類型。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-127">Appending the literal type characters `US` to a literal forces it to the `UShort` data type.</span></span> <span data-ttu-id="f2f6c-128">`UShort`沒有識別項型別字元。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-128">`UShort` has no identifier type character.</span></span>  
  
- <span data-ttu-id="f2f6c-129">**架構類型：**</span><span class="sxs-lookup"><span data-stu-id="f2f6c-129">**Framework Type.**</span></span> <span data-ttu-id="f2f6c-130">在 .NET Framework 中對應的類型為 <xref:System.UInt16?displayProperty=nameWithType> 結構。</span><span class="sxs-lookup"><span data-stu-id="f2f6c-130">The corresponding type in the .NET Framework is the <xref:System.UInt16?displayProperty=nameWithType> structure.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f2f6c-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f2f6c-131">See also</span></span>

- <xref:System.UInt16>
- [<span data-ttu-id="f2f6c-132">資料類型</span><span class="sxs-lookup"><span data-stu-id="f2f6c-132">Data Types</span></span>](index.md)
- [<span data-ttu-id="f2f6c-133">Type Conversion Functions</span><span class="sxs-lookup"><span data-stu-id="f2f6c-133">Type Conversion Functions</span></span>](../functions/type-conversion-functions.md)
- [<span data-ttu-id="f2f6c-134">轉換摘要</span><span class="sxs-lookup"><span data-stu-id="f2f6c-134">Conversion Summary</span></span>](../keywords/conversion-summary.md)
- [<span data-ttu-id="f2f6c-135">作法：呼叫不帶正負號的類型的 Windows 函式</span><span class="sxs-lookup"><span data-stu-id="f2f6c-135">How to: Call a Windows Function that Takes Unsigned Types</span></span>](../../programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [<span data-ttu-id="f2f6c-136">有效率地使用資料類型</span><span class="sxs-lookup"><span data-stu-id="f2f6c-136">Efficient Use of Data Types</span></span>](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
