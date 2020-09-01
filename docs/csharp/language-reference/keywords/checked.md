---
description: checked 關鍵字 - C# 參考
title: checked 關鍵字 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- checked_CSharpKeyword
- checked
helpviewer_keywords:
- checked keyword [C#]
ms.assetid: 718a1194-988d-48a3-b089-d6ee8bd1608d
ms.openlocfilehash: 4dd8bc02d3af89d6bab3aef55a88cb8b40704da6
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89138276"
---
# <a name="checked-c-reference"></a><span data-ttu-id="62ea7-103">checked (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="62ea7-103">checked (C# Reference)</span></span>

<span data-ttu-id="62ea7-104">`checked` 關鍵字是用來明確啟用整數型別算術運算和轉換的溢位檢查。</span><span class="sxs-lookup"><span data-stu-id="62ea7-104">The `checked` keyword is used to explicitly enable overflow checking for integral-type arithmetic operations and conversions.</span></span>

<span data-ttu-id="62ea7-105">根據預設，如果運算式產生超出目的地類型範圍的值，則只包含常數值的運算式會導致編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="62ea7-105">By default, an expression that contains only constant values causes a compiler error if the expression produces a value that is outside the range of the destination type.</span></span> <span data-ttu-id="62ea7-106">如果運算式包含一或多個非常數值，則編譯器偵測不到溢位。</span><span class="sxs-lookup"><span data-stu-id="62ea7-106">If the expression contains one or more non-constant values, the compiler does not detect the overflow.</span></span> <span data-ttu-id="62ea7-107">評估下列範例中指派給 `i2` 的運算式不會導致編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="62ea7-107">Evaluating the expression assigned to `i2` in the following example does not cause a compiler error.</span></span>

[!code-csharp[csrefKeywordsChecked#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#3)]

<span data-ttu-id="62ea7-108">根據預設，不會檢查這些非常數運算式是否在執行階段溢位，而且它們不會引發溢位例外狀況。</span><span class="sxs-lookup"><span data-stu-id="62ea7-108">By default, these non-constant expressions are not checked for overflow at run time either, and they do not raise overflow exceptions.</span></span> <span data-ttu-id="62ea7-109">先前的範例會顯示 -2,147,483,639 作為兩個正整數的總和。</span><span class="sxs-lookup"><span data-stu-id="62ea7-109">The previous example displays -2,147,483,639 as the sum of two positive integers.</span></span>

<span data-ttu-id="62ea7-110">可以透過編譯器選項、環境設定或使用 `checked` 關鍵字來啟用溢位檢查。</span><span class="sxs-lookup"><span data-stu-id="62ea7-110">Overflow checking can be enabled by compiler options, environment configuration, or use of the `checked` keyword.</span></span> <span data-ttu-id="62ea7-111">下列範例示範如何使用 `checked` 運算式或 `checked` 區塊，來偵測先前的總和在執行階段所產生的溢位。</span><span class="sxs-lookup"><span data-stu-id="62ea7-111">The following examples demonstrate how to use a `checked` expression or a `checked` block to detect the overflow that is produced by the previous sum at run time.</span></span> <span data-ttu-id="62ea7-112">這兩個範例都會引發溢位例外狀況。</span><span class="sxs-lookup"><span data-stu-id="62ea7-112">Both examples raise an overflow exception.</span></span>

[!code-csharp[csrefKeywordsChecked#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#4)]

<span data-ttu-id="62ea7-113">[unchecked](./unchecked.md) 關鍵字可以用來防止溢位檢查。</span><span class="sxs-lookup"><span data-stu-id="62ea7-113">The [unchecked](./unchecked.md) keyword can be used to prevent overflow checking.</span></span>

## <a name="example"></a><span data-ttu-id="62ea7-114">範例</span><span class="sxs-lookup"><span data-stu-id="62ea7-114">Example</span></span>

<span data-ttu-id="62ea7-115">這個範例示範如何使用 `checked`，以在執行階段啟用溢位檢查。</span><span class="sxs-lookup"><span data-stu-id="62ea7-115">This sample shows how to use `checked` to enable overflow checking at run time.</span></span>

[!code-csharp[csrefKeywordsChecked#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#1)]

## <a name="c-language-specification"></a><span data-ttu-id="62ea7-116">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="62ea7-116">C# language specification</span></span>

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="62ea7-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="62ea7-117">See also</span></span>

- [<span data-ttu-id="62ea7-118">C # 參考</span><span class="sxs-lookup"><span data-stu-id="62ea7-118">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="62ea7-119">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="62ea7-119">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="62ea7-120">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="62ea7-120">C# Keywords</span></span>](./index.md)
- [<span data-ttu-id="62ea7-121">Checked 與 Unchecked</span><span class="sxs-lookup"><span data-stu-id="62ea7-121">Checked and Unchecked</span></span>](./checked-and-unchecked.md)
- [<span data-ttu-id="62ea7-122">unchecked</span><span class="sxs-lookup"><span data-stu-id="62ea7-122">unchecked</span></span>](./unchecked.md)
