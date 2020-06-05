---
title: 串連運算子
ms.date: 07/20/2015
helpviewer_keywords:
- '& operator [Visual Basic], concatenation'
- concatenation operators [Visual Basic]
- operators [Visual Basic], concatenation
- Visual Basic code, operators
- + operator [Visual Basic], concatenation
- concatenation operators [Visual Basic]
ms.assetid: e59908c3-89e0-41ae-933d-3e8826c16a04
ms.openlocfilehash: c123438a86a2c3293a99770107d970535fcdbdf8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388786"
---
# <a name="concatenation-operators-in-visual-basic"></a><span data-ttu-id="79757-102">Visual Basic 中的串連運算子</span><span class="sxs-lookup"><span data-stu-id="79757-102">Concatenation Operators in Visual Basic</span></span>

<span data-ttu-id="79757-103">串連運算子會將多個字串連成單一字串。</span><span class="sxs-lookup"><span data-stu-id="79757-103">Concatenation operators join multiple strings into a single string.</span></span> <span data-ttu-id="79757-104">串連運算子有兩種：`+` 和 `&`。</span><span class="sxs-lookup"><span data-stu-id="79757-104">There are two concatenation operators, `+` and `&`.</span></span> <span data-ttu-id="79757-105">兩者都會進行基本的串連作業，如下例所示。</span><span class="sxs-lookup"><span data-stu-id="79757-105">Both carry out the basic concatenation operation, as the following example shows.</span></span>

```vb
Dim x As String = "Mic" & "ro" & "soft"
Dim y As String = "Mic" + "ro" + "soft"
' The preceding statements set both x and y to "Microsoft".
```

<span data-ttu-id="79757-106">這些運算子也可以串連 `String` 變數，如下列所示。</span><span class="sxs-lookup"><span data-stu-id="79757-106">These operators can also concatenate `String` variables, as the following example shows.</span></span>

[!code-vb[VbVbalrOperators#76](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#76)]

## <a name="differences-between-the-two-concatenation-operators"></a><span data-ttu-id="79757-107">兩種串連運算子之間的差異</span><span class="sxs-lookup"><span data-stu-id="79757-107">Differences Between the Two Concatenation Operators</span></span>

<span data-ttu-id="79757-108">[+ 運算子](../../../language-reference/operators/addition-operator.md)的主要目的是要加入兩個數字。</span><span class="sxs-lookup"><span data-stu-id="79757-108">The [+ Operator](../../../language-reference/operators/addition-operator.md) has the primary purpose of adding two numbers.</span></span> <span data-ttu-id="79757-109">不過，它也可以串連數值運算元與字串運算元。</span><span class="sxs-lookup"><span data-stu-id="79757-109">However, it can also concatenate numeric operands with string operands.</span></span> <span data-ttu-id="79757-110">`+` 運算子有一組複雜的規則，可判斷是要相加、串連、通知編譯器錯誤，還是擲回執行階段 <xref:System.InvalidCastException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="79757-110">The `+` operator has a complex set of rules that determine whether to add, concatenate, signal a compiler error, or throw a run-time <xref:System.InvalidCastException> exception.</span></span>

<span data-ttu-id="79757-111">[& 運算子](../../../language-reference/operators/concatenation-operator.md)只會針對運算元定義 `String` ，而且不論的設定為何，它一律會將其運算元擴大為 `String` `Option Strict` 。</span><span class="sxs-lookup"><span data-stu-id="79757-111">The [& Operator](../../../language-reference/operators/concatenation-operator.md) is defined only for `String` operands, and it always widens its operands to `String`, regardless of the setting of `Option Strict`.</span></span> <span data-ttu-id="79757-112">建議使用 `&` 運算元進行字串串連，因為它的定義為專門針對字串，且能減少您產生意外轉換的機會。</span><span class="sxs-lookup"><span data-stu-id="79757-112">The `&` operator is recommended for string concatenation because it is defined exclusively for strings and reduces your chances of generating an unintended conversion.</span></span>

## <a name="performance-string-and-stringbuilder"></a><span data-ttu-id="79757-113">效能：String 和 StringBuilder</span><span class="sxs-lookup"><span data-stu-id="79757-113">Performance: String and StringBuilder</span></span>

<span data-ttu-id="79757-114">如果您對字串進行大量的操作，例如串連、刪除和取代，可能可以藉由 <xref:System.Text.StringBuilder> 命名空間中的 <xref:System.Text> 類別而使效能獲得助益。</span><span class="sxs-lookup"><span data-stu-id="79757-114">If you do a significant number of manipulations on a string, such as concatenations, deletions, and replacements, your performance might profit from the <xref:System.Text.StringBuilder> class in the <xref:System.Text> namespace.</span></span> <span data-ttu-id="79757-115">建立和初始化 <xref:System.Text.StringBuilder> 物件需要額外的指令，將其最終值轉換成 `String` 又再需要一個指令，但您可以彌補這個時間，因為 <xref:System.Text.StringBuilder> 執行地更快速。</span><span class="sxs-lookup"><span data-stu-id="79757-115">It takes an extra instruction to create and initialize a <xref:System.Text.StringBuilder> object, and another instruction to convert its final value to a `String`, but you might recover this time because <xref:System.Text.StringBuilder> can perform faster.</span></span>

## <a name="see-also"></a><span data-ttu-id="79757-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="79757-116">See also</span></span>

- [<span data-ttu-id="79757-117">Long</span><span class="sxs-lookup"><span data-stu-id="79757-117">Option Strict Statement</span></span>](../../../language-reference/statements/option-strict-statement.md)
- [<span data-ttu-id="79757-118">Visual Basic 中字串管理方法的類型</span><span class="sxs-lookup"><span data-stu-id="79757-118">Types of String Manipulation Methods in Visual Basic</span></span>](../strings/types-of-string-manipulation-methods.md)
- [<span data-ttu-id="79757-119">Visual Basic 的算術運算子</span><span class="sxs-lookup"><span data-stu-id="79757-119">Arithmetic Operators in Visual Basic</span></span>](arithmetic-operators.md)
- [<span data-ttu-id="79757-120">Comparison Operators in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="79757-120">Comparison Operators in Visual Basic</span></span>](comparison-operators.md)
- [<span data-ttu-id="79757-121">Visual Basic 中的邏輯運算子和位元運算子</span><span class="sxs-lookup"><span data-stu-id="79757-121">Logical and Bitwise Operators in Visual Basic</span></span>](logical-and-bitwise-operators.md)
