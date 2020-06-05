---
title: Char 資料類型
ms.date: 07/20/2015
f1_keywords:
- vb.Char
helpviewer_keywords:
- literal type characters [Visual Basic], C
- Char data type
- C literal type character [Visual Basic]
- data types [Visual Basic], assigning
- Char data type [Visual Basic], character literals
ms.assetid: cd7547a9-7855-4e8e-b216-35d74a362657
ms.openlocfilehash: 3dbbf9f6a2c4079775e05f5d2dcd8704c1ec4259
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387474"
---
# <a name="char-data-type-visual-basic"></a><span data-ttu-id="1be49-102">Char 資料類型 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="1be49-102">Char Data Type (Visual Basic)</span></span>

<span data-ttu-id="1be49-103">保留不帶正負號的16位（2位元組）程式碼點，範圍介於0到65535之間。</span><span class="sxs-lookup"><span data-stu-id="1be49-103">Holds unsigned 16-bit (2-byte) code points ranging in value from 0 through 65535.</span></span> <span data-ttu-id="1be49-104">每個程式*代碼點*或字元碼都代表一個 Unicode 字元。</span><span class="sxs-lookup"><span data-stu-id="1be49-104">Each *code point*, or character code, represents a single Unicode character.</span></span>

## <a name="remarks"></a><span data-ttu-id="1be49-105">備註</span><span class="sxs-lookup"><span data-stu-id="1be49-105">Remarks</span></span>

<span data-ttu-id="1be49-106">`Char`當您只需要保存單一字元，而且不需要的額外負荷時，請使用資料類型 `String` 。</span><span class="sxs-lookup"><span data-stu-id="1be49-106">Use the `Char` data type when you need to hold only a single character and do not need the overhead of `String`.</span></span> <span data-ttu-id="1be49-107">在某些情況下，您可以使用 `Char()` 元素陣列 `Char` 來保存多個字元。</span><span class="sxs-lookup"><span data-stu-id="1be49-107">In some cases you can use `Char()`, an array of `Char` elements, to hold multiple characters.</span></span>

<span data-ttu-id="1be49-108">的預設值 `Char` 是程式碼點為0的字元。</span><span class="sxs-lookup"><span data-stu-id="1be49-108">The default value of `Char` is the character with a code point of 0.</span></span>

## <a name="unicode-characters"></a><span data-ttu-id="1be49-109">Unicode 字元</span><span class="sxs-lookup"><span data-stu-id="1be49-109">Unicode Characters</span></span>

<span data-ttu-id="1be49-110">Unicode 的第一個128程式碼點（0–127）對應到標準美式鍵盤上的字母和符號。</span><span class="sxs-lookup"><span data-stu-id="1be49-110">The first 128 code points (0–127) of Unicode correspond to the letters and symbols on a standard U.S. keyboard.</span></span> <span data-ttu-id="1be49-111">這些前128個程式碼點與 ASCII 字元集所定義的相同。</span><span class="sxs-lookup"><span data-stu-id="1be49-111">These first 128 code points are the same as those the ASCII character set defines.</span></span> <span data-ttu-id="1be49-112">第二個128程式碼片段（128–255）代表特殊字元，例如以拉丁為基礎的字母、重音、貨幣符號和分數。</span><span class="sxs-lookup"><span data-stu-id="1be49-112">The second 128 code points (128–255) represent special characters, such as Latin-based alphabet letters, accents, currency symbols, and fractions.</span></span> <span data-ttu-id="1be49-113">Unicode 會針對各種不同的符號使用其餘的程式碼點（256-65535），包括全球文字字元、變音符號和數學和技術符號。</span><span class="sxs-lookup"><span data-stu-id="1be49-113">Unicode uses the remaining code points (256-65535) for a wide variety of symbols, including worldwide textual characters, diacritics, and mathematical and technical symbols.</span></span>

<span data-ttu-id="1be49-114">您可以 <xref:System.Char.IsDigit%2A> 在變數上使用和之類的方法 <xref:System.Char.IsPunctuation%2A> `Char` 來判斷其 Unicode 分類。</span><span class="sxs-lookup"><span data-stu-id="1be49-114">You can use methods like <xref:System.Char.IsDigit%2A> and <xref:System.Char.IsPunctuation%2A> on a `Char` variable to determine its Unicode classification.</span></span>

## <a name="type-conversions"></a><span data-ttu-id="1be49-115">類型轉換</span><span class="sxs-lookup"><span data-stu-id="1be49-115">Type Conversions</span></span>

<span data-ttu-id="1be49-116">Visual Basic 不會直接在 `Char` 和數數值型別之間進行轉換。</span><span class="sxs-lookup"><span data-stu-id="1be49-116">Visual Basic does not convert directly between `Char` and the numeric types.</span></span> <span data-ttu-id="1be49-117">您可以使用 <xref:Microsoft.VisualBasic.Strings.Asc%2A> 或函 <xref:Microsoft.VisualBasic.Strings.AscW%2A> 式，將 `Char` 值轉換為 `Integer` 代表其程式碼點的。</span><span class="sxs-lookup"><span data-stu-id="1be49-117">You can use the <xref:Microsoft.VisualBasic.Strings.Asc%2A> or <xref:Microsoft.VisualBasic.Strings.AscW%2A> function to convert a `Char` value to an `Integer` that represents its code point.</span></span> <span data-ttu-id="1be49-118">您可以使用 <xref:Microsoft.VisualBasic.Strings.Chr%2A> 或 <xref:Microsoft.VisualBasic.Strings.ChrW%2A> 函數，將值轉換成 `Integer` `Char` 具有該程式碼點的。</span><span class="sxs-lookup"><span data-stu-id="1be49-118">You can use the <xref:Microsoft.VisualBasic.Strings.Chr%2A> or <xref:Microsoft.VisualBasic.Strings.ChrW%2A> function to convert an `Integer` value to a `Char` that has that code point.</span></span>

<span data-ttu-id="1be49-119">如果類型檢查參數（ [Option Strict 語句](../statements/option-strict-statement.md)）為 on，您就必須將常數值型別字元附加至單一字元字串常值，以將它識別為 `Char` 資料類型。</span><span class="sxs-lookup"><span data-stu-id="1be49-119">If the type checking switch (the [Option Strict Statement](../statements/option-strict-statement.md)) is on, you must append the literal type character to a single-character string literal to identify it as the `Char` data type.</span></span> <span data-ttu-id="1be49-120">下列範例將說明這點。</span><span class="sxs-lookup"><span data-stu-id="1be49-120">The following example illustrates this.</span></span> <span data-ttu-id="1be49-121">第一次指派變數時， `charVar` 會產生編譯器錯誤[BC30512](../../misc/bc30512.md) ，因為 `Option Strict` 是 on。</span><span class="sxs-lookup"><span data-stu-id="1be49-121">The first assignment to the `charVar` variable generates compiler error [BC30512](../../misc/bc30512.md) because `Option Strict` is on.</span></span> <span data-ttu-id="1be49-122">第二個編譯成功，因為 `c` 常數值型別字元會將常 `Char` 值識別為值。</span><span class="sxs-lookup"><span data-stu-id="1be49-122">The second compiles successfully because the `c` literal type character identifies the literal as a `Char` value.</span></span>

```vb
Option Strict On

Module CharType
    Public Sub Main()
        Dim charVar As Char

        ' This statement generates compiler error BC30512 because Option Strict is On.  
        charVar = "Z"  

        ' The following statement succeeds because it specifies a Char literal.  
        charVar = "Z"c
    End Sub
End Module
```

## <a name="programming-tips"></a><span data-ttu-id="1be49-123">程式設計提示</span><span class="sxs-lookup"><span data-stu-id="1be49-123">Programming Tips</span></span>

- <span data-ttu-id="1be49-124">**負數。**</span><span class="sxs-lookup"><span data-stu-id="1be49-124">**Negative Numbers.**</span></span> <span data-ttu-id="1be49-125">`Char`是不帶正負號的類型，而且不能代表負值。</span><span class="sxs-lookup"><span data-stu-id="1be49-125">`Char` is an unsigned type and cannot represent a negative value.</span></span> <span data-ttu-id="1be49-126">在任何情況下，您都不應該使用 `Char` 來保存數值。</span><span class="sxs-lookup"><span data-stu-id="1be49-126">In any case, you should not use `Char` to hold numeric values.</span></span>

- <span data-ttu-id="1be49-127">**Interop 考量：**</span><span class="sxs-lookup"><span data-stu-id="1be49-127">**Interop Considerations.**</span></span> <span data-ttu-id="1be49-128">如果您使用不是針對 .NET Framework 所撰寫的元件（例如 Automation 或 COM 物件）來進行介面，請記住，在其他環境中，字元類型具有不同的資料寬度（8位）。</span><span class="sxs-lookup"><span data-stu-id="1be49-128">If you interface with components not written for the .NET Framework, for example Automation or COM objects, remember that character types have a different data width (8 bits) in other environments.</span></span> <span data-ttu-id="1be49-129">如果您將8位引數傳遞至這類元件，請 `Byte` `Char` 在新的 Visual Basic 程式碼中將它宣告為而不是。</span><span class="sxs-lookup"><span data-stu-id="1be49-129">If you pass an 8-bit argument to such a component, declare it as `Byte` instead of `Char` in your new Visual Basic code.</span></span>

- <span data-ttu-id="1be49-130">**加寬.**</span><span class="sxs-lookup"><span data-stu-id="1be49-130">**Widening.**</span></span> <span data-ttu-id="1be49-131">`Char`資料類型會擴大為 `String` 。</span><span class="sxs-lookup"><span data-stu-id="1be49-131">The `Char` data type widens to `String`.</span></span> <span data-ttu-id="1be49-132">這表示您可以將轉換成 `Char` `String` ，而且不會遇到 <xref:System.OverflowException?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="1be49-132">This means you can convert `Char` to `String` and will not encounter a <xref:System.OverflowException?displayProperty=nameWithType>.</span></span>

- <span data-ttu-id="1be49-133">**輸入字元。**</span><span class="sxs-lookup"><span data-stu-id="1be49-133">**Type Characters.**</span></span> <span data-ttu-id="1be49-134">將常數值型別字元附加 `C` 至單一字元字串常值，會強制其成為 `Char` 資料類型。</span><span class="sxs-lookup"><span data-stu-id="1be49-134">Appending the literal type character `C` to a single-character string literal forces it to the `Char` data type.</span></span> <span data-ttu-id="1be49-135">`Char`沒有識別項型別字元。</span><span class="sxs-lookup"><span data-stu-id="1be49-135">`Char` has no identifier type character.</span></span>

- <span data-ttu-id="1be49-136">**架構類型：**</span><span class="sxs-lookup"><span data-stu-id="1be49-136">**Framework Type.**</span></span> <span data-ttu-id="1be49-137">在 .NET Framework 中對應的類型為 <xref:System.Char?displayProperty=nameWithType> 結構。</span><span class="sxs-lookup"><span data-stu-id="1be49-137">The corresponding type in the .NET Framework is the <xref:System.Char?displayProperty=nameWithType> structure.</span></span>

## <a name="see-also"></a><span data-ttu-id="1be49-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1be49-138">See also</span></span>

- <xref:System.Char?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- [<span data-ttu-id="1be49-139">資料類型</span><span class="sxs-lookup"><span data-stu-id="1be49-139">Data Types</span></span>](index.md)
- [<span data-ttu-id="1be49-140">String 資料類型</span><span class="sxs-lookup"><span data-stu-id="1be49-140">String Data Type</span></span>](string-data-type.md)
- [<span data-ttu-id="1be49-141">Type Conversion Functions</span><span class="sxs-lookup"><span data-stu-id="1be49-141">Type Conversion Functions</span></span>](../functions/type-conversion-functions.md)
- [<span data-ttu-id="1be49-142">轉換摘要</span><span class="sxs-lookup"><span data-stu-id="1be49-142">Conversion Summary</span></span>](../keywords/conversion-summary.md)
- [<span data-ttu-id="1be49-143">作法：呼叫不帶正負號的類型的 Windows 函式</span><span class="sxs-lookup"><span data-stu-id="1be49-143">How to: Call a Windows Function that Takes Unsigned Types</span></span>](../../programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [<span data-ttu-id="1be49-144">有效率地使用資料類型</span><span class="sxs-lookup"><span data-stu-id="1be49-144">Efficient Use of Data Types</span></span>](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
