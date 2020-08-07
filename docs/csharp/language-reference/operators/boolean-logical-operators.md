---
title: 布林值邏輯運算子 - C# 參考
description: 了解能搭配布林值運算元執行邏輯否定、結合 (AND) 及內含和互斥分離 (OR) 作業的 C# 運算子。
ms.date: 06/29/2020
author: pkulikov
f1_keywords:
- '!_CSharpKeyword'
- '&_CSharpKeyword'
- ^_CSharpKeyword
- '|_CSharpKeyword'
- '&&_CSharpKeyword'
- '||_CSharpKeyword'
- '|=_CSharpKeyword'
- ^=_CSharpKeyword
- '&=_CSharpKeyword'
helpviewer_keywords:
- logical operators [C#]
- short-circuiting operators [C#]
- logical negation operator [C#]
- NOT operator [C#]
- '! operator [C#]'
- AND operator [C#]
- ampersand operator [C#]
- conjunction operator [C#]
- '& operator [C#]'
- exclusive OR operator [C#]
- XOR operator [C#]
- ^ operator [C#]
- OR operator [C#]
- disjunction operator [C#]
- '| operator [C#]'
- conditional AND operator [C#]
- short-circuiting AND operator [C#]
- '&& operator [C#]'
- conditional OR operator [C#]
- short-circuiting OR operator [C#]
- '|| operator [C#]'
ms.openlocfilehash: 2a67542e25ddb258602b4005a71b565cf6522917
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855136"
---
# <a name="boolean-logical-operators-c-reference"></a><span data-ttu-id="318bd-103">布林值邏輯運算子 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="318bd-103">Boolean logical operators (C# reference)</span></span>

<span data-ttu-id="318bd-104">下列運算子會使用[bool](../builtin-types/bool.md)運算元執行邏輯作業：</span><span class="sxs-lookup"><span data-stu-id="318bd-104">The following operators perform logical operations with [bool](../builtin-types/bool.md) operands:</span></span>

- <span data-ttu-id="318bd-105">一元[ `!` (邏輯否定) ](#logical-negation-operator-)運算子。</span><span class="sxs-lookup"><span data-stu-id="318bd-105">Unary [`!` (logical negation)](#logical-negation-operator-) operator.</span></span>
- <span data-ttu-id="318bd-106">Binary [ `&` (邏輯 AND) ](#logical-and-operator-)、 [ `|` (邏輯 OR) ](#logical-or-operator-)，以及[ `^` (邏輯互斥 OR) ](#logical-exclusive-or-operator-)運算子。</span><span class="sxs-lookup"><span data-stu-id="318bd-106">Binary [`&` (logical AND)](#logical-and-operator-), [`|` (logical OR)](#logical-or-operator-), and [`^` (logical exclusive OR)](#logical-exclusive-or-operator-) operators.</span></span> <span data-ttu-id="318bd-107">那些運算子一律會評估兩個運算元。</span><span class="sxs-lookup"><span data-stu-id="318bd-107">Those operators always evaluate both operands.</span></span>
- <span data-ttu-id="318bd-108">二元[ `&&` (條件邏輯 AND) ](#conditional-logical-and-operator-)和[ `||` (條件式邏輯 OR) ](#conditional-logical-or-operator-)運算子。</span><span class="sxs-lookup"><span data-stu-id="318bd-108">Binary [`&&` (conditional logical AND)](#conditional-logical-and-operator-) and [`||` (conditional logical OR)](#conditional-logical-or-operator-) operators.</span></span> <span data-ttu-id="318bd-109">那些運算子只會在必要時才評估右邊的運算元。</span><span class="sxs-lookup"><span data-stu-id="318bd-109">Those operators evaluate the right-hand operand only if it's necessary.</span></span>

<span data-ttu-id="318bd-110">對於[整數數數值型別](../builtin-types/integral-numeric-types.md)的運算元， `&` 、 `|` 和 `^` 運算子會執行位邏輯運算。</span><span class="sxs-lookup"><span data-stu-id="318bd-110">For operands of the [integral numeric types](../builtin-types/integral-numeric-types.md), the `&`, `|`, and `^` operators perform bitwise logical operations.</span></span> <span data-ttu-id="318bd-111">如需詳細資訊，請參閱[位元與移位運算子](bitwise-and-shift-operators.md)。</span><span class="sxs-lookup"><span data-stu-id="318bd-111">For more information, see [Bitwise and shift operators](bitwise-and-shift-operators.md).</span></span>

## <a name="logical-negation-operator-"></a><span data-ttu-id="318bd-112">邏輯否定運算子 !</span><span class="sxs-lookup"><span data-stu-id="318bd-112">Logical negation operator !</span></span>

<span data-ttu-id="318bd-113">一元前置 `!` 運算子會計算其運算元的邏輯否定。</span><span class="sxs-lookup"><span data-stu-id="318bd-113">The unary prefix `!` operator computes logical negation of its operand.</span></span> <span data-ttu-id="318bd-114">也就是說，它會在運算元評估為 `false` 時產生 `true`，並在運算元評估為 `true` 時產生 `false`：</span><span class="sxs-lookup"><span data-stu-id="318bd-114">That is, it produces `true`, if the operand evaluates to `false`, and `false`, if the operand evaluates to `true`:</span></span>

[!code-csharp-interactive[logical negation](snippets/BooleanLogicalOperators.cs#Negation)]

<span data-ttu-id="318bd-115">從 c # 8.0 開始，一元 `!` 後置運算子是[null 容許運算子](null-forgiving.md)。</span><span class="sxs-lookup"><span data-stu-id="318bd-115">Beginning with C# 8.0, the unary postfix `!` operator is the [null-forgiving operator](null-forgiving.md).</span></span>

## <a name="logical-and-operator-amp"></a><a name="logical-and-operator-"></a><span data-ttu-id="318bd-116">邏輯 AND 運算子&amp;</span><span class="sxs-lookup"><span data-stu-id="318bd-116">Logical AND operator &amp;</span></span>

<span data-ttu-id="318bd-117">`&` 運算子會計算其運算元的邏輯 AND。</span><span class="sxs-lookup"><span data-stu-id="318bd-117">The `&` operator computes the logical AND of its operands.</span></span> <span data-ttu-id="318bd-118">若 `x` 及 `y` 皆求出 `true`，那麼 `x & y` 的結果會是 `true`。</span><span class="sxs-lookup"><span data-stu-id="318bd-118">The result of `x & y` is `true` if both `x` and `y` evaluate to `true`.</span></span> <span data-ttu-id="318bd-119">否則，結果為 `false`。</span><span class="sxs-lookup"><span data-stu-id="318bd-119">Otherwise, the result is `false`.</span></span>

<span data-ttu-id="318bd-120">`&`運算子會同時評估這兩個運算元，即使左邊的運算元評估為 `false` ，因此 `false` 不論右運算元的值為何，運算結果都是如此。</span><span class="sxs-lookup"><span data-stu-id="318bd-120">The `&` operator evaluates both operands even if the left-hand operand evaluates to `false`, so that the operation result is `false` regardless of the value of the right-hand operand.</span></span>

<span data-ttu-id="318bd-121">在下列範例中，`&` 運算子的右邊運算元是方法呼叫；無論左邊運算元的值為何，系統都會執行該呼叫：</span><span class="sxs-lookup"><span data-stu-id="318bd-121">In the following example, the right-hand operand of the `&` operator is a method call, which is performed regardless of the value of the left-hand operand:</span></span>

[!code-csharp-interactive[logical AND](snippets/BooleanLogicalOperators.cs#And)]

<span data-ttu-id="318bd-122">[條件邏輯 AND 運算子](#conditional-logical-and-operator-) `&&` 也會計算其運算元的邏輯 AND，但如果右邊運算元的值評估為 `false`，系統便不會評估左邊運算元。</span><span class="sxs-lookup"><span data-stu-id="318bd-122">The [conditional logical AND operator](#conditional-logical-and-operator-) `&&` also computes the logical AND of its operands, but doesn't evaluate the right-hand operand if the left-hand operand evaluates to `false`.</span></span>

<span data-ttu-id="318bd-123">對於[整數數數值型別](../builtin-types/integral-numeric-types.md)的運算元，運算子會 `&` 計算其運算元的[位邏輯 and](bitwise-and-shift-operators.md#logical-and-operator-) 。</span><span class="sxs-lookup"><span data-stu-id="318bd-123">For operands of the [integral numeric types](../builtin-types/integral-numeric-types.md), the `&` operator computes the [bitwise logical AND](bitwise-and-shift-operators.md#logical-and-operator-) of its operands.</span></span> <span data-ttu-id="318bd-124">一元的 `&` 運算子是 [address-of 運算子](pointer-related-operators.md#address-of-operator-)。</span><span class="sxs-lookup"><span data-stu-id="318bd-124">The unary `&` operator is the [address-of operator](pointer-related-operators.md#address-of-operator-).</span></span>

## <a name="logical-exclusive-or-operator-"></a><span data-ttu-id="318bd-125">邏輯互斥 OR 運算子 ^</span><span class="sxs-lookup"><span data-stu-id="318bd-125">Logical exclusive OR operator ^</span></span>

<span data-ttu-id="318bd-126">`^` 運算子會計算其運算元的邏輯互斥 OR，其也稱為邏輯 XOR。</span><span class="sxs-lookup"><span data-stu-id="318bd-126">The `^` operator computes the logical exclusive OR, also known as the logical XOR, of its operands.</span></span> <span data-ttu-id="318bd-127">如果 `x` 評估為 `true` 且 `y` 評估為 `false`，或是 `x` 評估為 `false` 且 `y` 評估為 `true` 時，`x ^ y` 的結果將會為 `true`。</span><span class="sxs-lookup"><span data-stu-id="318bd-127">The result of `x ^ y` is `true` if `x` evaluates to `true` and `y` evaluates to `false`, or `x` evaluates to `false` and `y` evaluates to `true`.</span></span> <span data-ttu-id="318bd-128">否則，結果為 `false`。</span><span class="sxs-lookup"><span data-stu-id="318bd-128">Otherwise, the result is `false`.</span></span> <span data-ttu-id="318bd-129">也就是說，針對 `bool` 運算元，`^` 運算子的計算結果會與[不等比較運算子](equality-operators.md#inequality-operator-) `!=` 相同。</span><span class="sxs-lookup"><span data-stu-id="318bd-129">That is, for the `bool` operands, the `^` operator computes the same result as the [inequality operator](equality-operators.md#inequality-operator-) `!=`.</span></span>

[!code-csharp-interactive[logical exclusive OR](snippets/BooleanLogicalOperators.cs#Xor)]

<span data-ttu-id="318bd-130">對於[整數數數值型別](../builtin-types/integral-numeric-types.md)的運算元，運算子會 `^` 計算其運算元的[位邏輯互斥 OR](bitwise-and-shift-operators.md#logical-exclusive-or-operator-) 。</span><span class="sxs-lookup"><span data-stu-id="318bd-130">For operands of the [integral numeric types](../builtin-types/integral-numeric-types.md), the `^` operator computes the [bitwise logical exclusive OR](bitwise-and-shift-operators.md#logical-exclusive-or-operator-) of its operands.</span></span>

## <a name="logical-or-operator-"></a><span data-ttu-id="318bd-131">邏輯 OR 運算子 |</span><span class="sxs-lookup"><span data-stu-id="318bd-131">Logical OR operator |</span></span>

<span data-ttu-id="318bd-132">`|` 運算子會計算其運算元的邏輯 OR。</span><span class="sxs-lookup"><span data-stu-id="318bd-132">The `|` operator computes the logical OR of its operands.</span></span> <span data-ttu-id="318bd-133">若 `x` 或 `y` 其中一項的值為 `true`，`x | y` 的結果會是 `true`。</span><span class="sxs-lookup"><span data-stu-id="318bd-133">The result of `x | y` is `true` if either `x` or `y` evaluates to `true`.</span></span> <span data-ttu-id="318bd-134">否則，結果為 `false`。</span><span class="sxs-lookup"><span data-stu-id="318bd-134">Otherwise, the result is `false`.</span></span>

<span data-ttu-id="318bd-135">`|`運算子會同時評估這兩個運算元，即使左邊的運算元評估為 `true` ，因此 `true` 不論右運算元的值為何，運算結果都是如此。</span><span class="sxs-lookup"><span data-stu-id="318bd-135">The `|` operator evaluates both operands even if the left-hand operand evaluates to `true`, so that the operation result is `true` regardless of the value of the right-hand operand.</span></span>

<span data-ttu-id="318bd-136">在下列範例中，`|` 運算子的右邊運算元是方法呼叫；無論左邊運算元的值為何，系統都會執行該呼叫：</span><span class="sxs-lookup"><span data-stu-id="318bd-136">In the following example, the right-hand operand of the `|` operator is a method call, which is performed regardless of the value of the left-hand operand:</span></span>

[!code-csharp-interactive[logical OR](snippets/BooleanLogicalOperators.cs#Or)]

<span data-ttu-id="318bd-137">[條件式邏輯 OR 運算子](#conditional-logical-or-operator-) `||` 也會計算其運算元的邏輯 OR，但如果左邊運算元的值評估為 `true`，系統便不會評估右邊運算元。</span><span class="sxs-lookup"><span data-stu-id="318bd-137">The [conditional logical OR operator](#conditional-logical-or-operator-) `||` also computes the logical OR of its operands, but doesn't evaluate the right-hand operand if the left-hand operand evaluates to `true`.</span></span>

<span data-ttu-id="318bd-138">對於[整數數數值型別](../builtin-types/integral-numeric-types.md)的運算元，運算子會 `|` 計算其運算元的[位邏輯 or](bitwise-and-shift-operators.md#logical-or-operator-) 。</span><span class="sxs-lookup"><span data-stu-id="318bd-138">For operands of the [integral numeric types](../builtin-types/integral-numeric-types.md), the `|` operator computes the [bitwise logical OR](bitwise-and-shift-operators.md#logical-or-operator-) of its operands.</span></span>

## <a name="conditional-logical-and-operator-ampamp"></a><a name="conditional-logical-and-operator-"></a><span data-ttu-id="318bd-139">條件邏輯 AND 運算子&amp;&amp;</span><span class="sxs-lookup"><span data-stu-id="318bd-139">Conditional logical AND operator &amp;&amp;</span></span>

<span data-ttu-id="318bd-140">條件邏輯 AND 運算子 `&&`，也稱為「捷徑運算」邏輯 AND 運算子，會計算其運算元的邏輯 AND。</span><span class="sxs-lookup"><span data-stu-id="318bd-140">The conditional logical AND operator `&&`, also known as the "short-circuiting" logical AND operator, computes the logical AND of its operands.</span></span> <span data-ttu-id="318bd-141">若 `x` 及 `y` 皆求出 `true`，那麼 `x && y` 的結果會是 `true`。</span><span class="sxs-lookup"><span data-stu-id="318bd-141">The result of `x && y` is `true` if both `x` and `y` evaluate to `true`.</span></span> <span data-ttu-id="318bd-142">否則，結果為 `false`。</span><span class="sxs-lookup"><span data-stu-id="318bd-142">Otherwise, the result is `false`.</span></span> <span data-ttu-id="318bd-143">如果 `x` 評估為 `false`，則不會評估 `y`。</span><span class="sxs-lookup"><span data-stu-id="318bd-143">If `x` evaluates to `false`, `y` is not evaluated.</span></span>

<span data-ttu-id="318bd-144">在下列範例中，`&&` 運算子的右邊運算元是方法呼叫；如果左邊運算元的值評估為 `false`，系統便不會執行該呼叫：</span><span class="sxs-lookup"><span data-stu-id="318bd-144">In the following example, the right-hand operand of the `&&` operator is a method call, which isn't performed if the left-hand operand evaluates to `false`:</span></span>

[!code-csharp-interactive[conditional logical AND](snippets/BooleanLogicalOperators.cs#ConditionalAnd)]

<span data-ttu-id="318bd-145">[邏輯 and 運算子](#logical-and-operator-) `&` 也會計算其運算元的邏輯 and，但一律會評估這兩個運算元。</span><span class="sxs-lookup"><span data-stu-id="318bd-145">The [logical AND operator](#logical-and-operator-) `&` also computes the logical AND of its operands, but always evaluates both operands.</span></span>

## <a name="conditional-logical-or-operator-"></a><span data-ttu-id="318bd-146">條件邏輯 OR 運算子 ||</span><span class="sxs-lookup"><span data-stu-id="318bd-146">Conditional logical OR operator ||</span></span>

<span data-ttu-id="318bd-147">條件邏輯 OR 運算子 `||`，也稱為「捷徑運算」邏輯 OR 運算子，會計算其運算元的邏輯 OR。</span><span class="sxs-lookup"><span data-stu-id="318bd-147">The conditional logical OR operator `||`, also known as the "short-circuiting" logical OR operator, computes the logical OR of its operands.</span></span> <span data-ttu-id="318bd-148">若 `x` 或 `y` 其中一項的值為 `true`，`x || y` 的結果會是 `true`。</span><span class="sxs-lookup"><span data-stu-id="318bd-148">The result of `x || y` is `true` if either `x` or `y` evaluates to `true`.</span></span> <span data-ttu-id="318bd-149">否則，結果為 `false`。</span><span class="sxs-lookup"><span data-stu-id="318bd-149">Otherwise, the result is `false`.</span></span> <span data-ttu-id="318bd-150">如果 `x` 評估為 `true`，則不會評估 `y`。</span><span class="sxs-lookup"><span data-stu-id="318bd-150">If `x` evaluates to `true`, `y` is not evaluated.</span></span>

<span data-ttu-id="318bd-151">在下列範例中，`||` 運算子的右邊運算元是方法呼叫；如果左邊運算元的值評估為 `true`，系統便不會執行該呼叫：</span><span class="sxs-lookup"><span data-stu-id="318bd-151">In the following example, the right-hand operand of the `||` operator is a method call, which isn't performed if the left-hand operand evaluates to `true`:</span></span>

[!code-csharp-interactive[conditional logical OR](snippets/BooleanLogicalOperators.cs#ConditionalOr)]

<span data-ttu-id="318bd-152">[邏輯 or 運算子](#logical-or-operator-) `|` 也會計算其運算元的邏輯 or，但一律會評估這兩個運算元。</span><span class="sxs-lookup"><span data-stu-id="318bd-152">The [logical OR operator](#logical-or-operator-) `|` also computes the logical OR of its operands, but always evaluates both operands.</span></span>

## <a name="nullable-boolean-logical-operators"></a><span data-ttu-id="318bd-153">可為 Null 的布林值邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="318bd-153">Nullable Boolean logical operators</span></span>

<span data-ttu-id="318bd-154">針對 `bool?` 運算元， [ `&` (邏輯 AND) ](#logical-and-operator-)和[ `|` (邏輯 OR) ](#logical-or-operator-)運算子支援三值邏輯，如下所示：</span><span class="sxs-lookup"><span data-stu-id="318bd-154">For `bool?` operands, the [`&` (logical AND)](#logical-and-operator-) and [`|` (logical OR)](#logical-or-operator-) operators support the three-valued logic as follows:</span></span>

- <span data-ttu-id="318bd-155">`&` `true` 只有當運算子的兩個運算元都評估為時，才會產生 `true` 。</span><span class="sxs-lookup"><span data-stu-id="318bd-155">The `&` operator produces `true` only if both its operands evaluate to `true`.</span></span> <span data-ttu-id="318bd-156">如果 `x` 或 `y` 評估為 `false` ， `x & y` `false` 即使另一個運算元評估為) ，也會產生 (`null` 。</span><span class="sxs-lookup"><span data-stu-id="318bd-156">If either `x` or `y` evaluates to `false`, `x & y` produces `false` (even if another operand evaluates to `null`).</span></span> <span data-ttu-id="318bd-157">否則，的結果 `x & y` 會是 `null` 。</span><span class="sxs-lookup"><span data-stu-id="318bd-157">Otherwise, the result of `x & y` is `null`.</span></span>

- <span data-ttu-id="318bd-158">`|` `false` 只有當運算子的兩個運算元都評估為時，才會產生 `false` 。</span><span class="sxs-lookup"><span data-stu-id="318bd-158">The `|` operator produces `false` only if both its operands evaluate to `false`.</span></span> <span data-ttu-id="318bd-159">如果 `x` 或 `y` 評估為 `true` ， `x | y` `true` 即使另一個運算元評估為) ，也會產生 (`null` 。</span><span class="sxs-lookup"><span data-stu-id="318bd-159">If either `x` or `y` evaluates to `true`, `x | y` produces `true` (even if another operand evaluates to `null`).</span></span> <span data-ttu-id="318bd-160">否則，的結果 `x | y` 會是 `null` 。</span><span class="sxs-lookup"><span data-stu-id="318bd-160">Otherwise, the result of `x | y` is `null`.</span></span>

<span data-ttu-id="318bd-161">下表顯示該語義：</span><span class="sxs-lookup"><span data-stu-id="318bd-161">The following table presents that semantics:</span></span>

|<span data-ttu-id="318bd-162">x</span><span class="sxs-lookup"><span data-stu-id="318bd-162">x</span></span>|<span data-ttu-id="318bd-163">y</span><span class="sxs-lookup"><span data-stu-id="318bd-163">y</span></span>|<span data-ttu-id="318bd-164">x&y</span><span class="sxs-lookup"><span data-stu-id="318bd-164">x&y</span></span>|<span data-ttu-id="318bd-165">x&#124;y</span><span class="sxs-lookup"><span data-stu-id="318bd-165">x&#124;y</span></span>|  
|----|----|----|----|  
|<span data-ttu-id="318bd-166">true</span><span class="sxs-lookup"><span data-stu-id="318bd-166">true</span></span>|<span data-ttu-id="318bd-167">true</span><span class="sxs-lookup"><span data-stu-id="318bd-167">true</span></span>|<span data-ttu-id="318bd-168">true</span><span class="sxs-lookup"><span data-stu-id="318bd-168">true</span></span>|<span data-ttu-id="318bd-169">true</span><span class="sxs-lookup"><span data-stu-id="318bd-169">true</span></span>|  
|<span data-ttu-id="318bd-170">true</span><span class="sxs-lookup"><span data-stu-id="318bd-170">true</span></span>|<span data-ttu-id="318bd-171">false</span><span class="sxs-lookup"><span data-stu-id="318bd-171">false</span></span>|<span data-ttu-id="318bd-172">false</span><span class="sxs-lookup"><span data-stu-id="318bd-172">false</span></span>|<span data-ttu-id="318bd-173">true</span><span class="sxs-lookup"><span data-stu-id="318bd-173">true</span></span>|  
|<span data-ttu-id="318bd-174">true</span><span class="sxs-lookup"><span data-stu-id="318bd-174">true</span></span>|<span data-ttu-id="318bd-175">null</span><span class="sxs-lookup"><span data-stu-id="318bd-175">null</span></span>|<span data-ttu-id="318bd-176">null</span><span class="sxs-lookup"><span data-stu-id="318bd-176">null</span></span>|<span data-ttu-id="318bd-177">true</span><span class="sxs-lookup"><span data-stu-id="318bd-177">true</span></span>|  
|<span data-ttu-id="318bd-178">false</span><span class="sxs-lookup"><span data-stu-id="318bd-178">false</span></span>|<span data-ttu-id="318bd-179">true</span><span class="sxs-lookup"><span data-stu-id="318bd-179">true</span></span>|<span data-ttu-id="318bd-180">false</span><span class="sxs-lookup"><span data-stu-id="318bd-180">false</span></span>|<span data-ttu-id="318bd-181">true</span><span class="sxs-lookup"><span data-stu-id="318bd-181">true</span></span>|  
|<span data-ttu-id="318bd-182">false</span><span class="sxs-lookup"><span data-stu-id="318bd-182">false</span></span>|<span data-ttu-id="318bd-183">false</span><span class="sxs-lookup"><span data-stu-id="318bd-183">false</span></span>|<span data-ttu-id="318bd-184">false</span><span class="sxs-lookup"><span data-stu-id="318bd-184">false</span></span>|<span data-ttu-id="318bd-185">false</span><span class="sxs-lookup"><span data-stu-id="318bd-185">false</span></span>|  
|<span data-ttu-id="318bd-186">false</span><span class="sxs-lookup"><span data-stu-id="318bd-186">false</span></span>|<span data-ttu-id="318bd-187">null</span><span class="sxs-lookup"><span data-stu-id="318bd-187">null</span></span>|<span data-ttu-id="318bd-188">false</span><span class="sxs-lookup"><span data-stu-id="318bd-188">false</span></span>|<span data-ttu-id="318bd-189">null</span><span class="sxs-lookup"><span data-stu-id="318bd-189">null</span></span>|  
|<span data-ttu-id="318bd-190">null</span><span class="sxs-lookup"><span data-stu-id="318bd-190">null</span></span>|<span data-ttu-id="318bd-191">true</span><span class="sxs-lookup"><span data-stu-id="318bd-191">true</span></span>|<span data-ttu-id="318bd-192">null</span><span class="sxs-lookup"><span data-stu-id="318bd-192">null</span></span>|<span data-ttu-id="318bd-193">true</span><span class="sxs-lookup"><span data-stu-id="318bd-193">true</span></span>|  
|<span data-ttu-id="318bd-194">null</span><span class="sxs-lookup"><span data-stu-id="318bd-194">null</span></span>|<span data-ttu-id="318bd-195">false</span><span class="sxs-lookup"><span data-stu-id="318bd-195">false</span></span>|<span data-ttu-id="318bd-196">false</span><span class="sxs-lookup"><span data-stu-id="318bd-196">false</span></span>|<span data-ttu-id="318bd-197">null</span><span class="sxs-lookup"><span data-stu-id="318bd-197">null</span></span>|  
|<span data-ttu-id="318bd-198">null</span><span class="sxs-lookup"><span data-stu-id="318bd-198">null</span></span>|<span data-ttu-id="318bd-199">null</span><span class="sxs-lookup"><span data-stu-id="318bd-199">null</span></span>|<span data-ttu-id="318bd-200">null</span><span class="sxs-lookup"><span data-stu-id="318bd-200">null</span></span>|<span data-ttu-id="318bd-201">null</span><span class="sxs-lookup"><span data-stu-id="318bd-201">null</span></span>|  

<span data-ttu-id="318bd-202">那些運算子的行為和具有可為 Null 實值類型之一般運算子的行為並不相同。</span><span class="sxs-lookup"><span data-stu-id="318bd-202">The behavior of those operators differs from the typical operator behavior with nullable value types.</span></span> <span data-ttu-id="318bd-203">一般而言，已針對某個實值類型之運算元定義的運算子，也可以搭配相對應可為 Null 實值類型的運算元使用。</span><span class="sxs-lookup"><span data-stu-id="318bd-203">Typically, an operator which is defined for operands of a value type can be also used with operands of the corresponding nullable value type.</span></span> <span data-ttu-id="318bd-204">`null`如果它的任何運算元評估為，則會產生這類運算子 `null` 。</span><span class="sxs-lookup"><span data-stu-id="318bd-204">Such an operator produces `null` if any of its operands evaluates to `null`.</span></span> <span data-ttu-id="318bd-205">不過， `&` `|` 即使其中一個運算元評估為，和運算子也可以產生非 null `null` 。</span><span class="sxs-lookup"><span data-stu-id="318bd-205">However, the `&` and `|` operators can produce non-null even if one of the operands evaluates to `null`.</span></span> <span data-ttu-id="318bd-206">如需可為 null 的實數值型別之運算子行為的詳細資訊，請參閱[可為 null 的實數值型別](../builtin-types/nullable-value-types.md)一文的「[提升運算子](../builtin-types/nullable-value-types.md#lifted-operators)」一節。</span><span class="sxs-lookup"><span data-stu-id="318bd-206">For more information about the operator behavior with nullable value types, see the [Lifted operators](../builtin-types/nullable-value-types.md#lifted-operators) section of the [Nullable value types](../builtin-types/nullable-value-types.md) article.</span></span>

<span data-ttu-id="318bd-207">您也可以使用 `!` 和 `^` 運算子搭配 `bool?` 運算元，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="318bd-207">You can also use the `!` and `^` operators with `bool?` operands, as the following example shows:</span></span>

[!code-csharp-interactive[lifted negation and xor](snippets/BooleanLogicalOperators.cs#WithNullableBoolean)]

<span data-ttu-id="318bd-208">條件式邏輯運算子 `&&` 和 `||` 不支援 `bool?` 運算元。</span><span class="sxs-lookup"><span data-stu-id="318bd-208">The conditional logical operators `&&` and `||` don't support `bool?` operands.</span></span>

## <a name="compound-assignment"></a><span data-ttu-id="318bd-209">複合指派</span><span class="sxs-lookup"><span data-stu-id="318bd-209">Compound assignment</span></span>

<span data-ttu-id="318bd-210">若是二元運算子 `op`，表單的複合指派運算式</span><span class="sxs-lookup"><span data-stu-id="318bd-210">For a binary operator `op`, a compound assignment expression of the form</span></span>

```csharp
x op= y
```

<span data-ttu-id="318bd-211">相當於</span><span class="sxs-lookup"><span data-stu-id="318bd-211">is equivalent to</span></span>

```csharp
x = x op y
```

<span data-ttu-id="318bd-212">但只會評估 `x` 一次。</span><span class="sxs-lookup"><span data-stu-id="318bd-212">except that `x` is only evaluated once.</span></span>

<span data-ttu-id="318bd-213">`&`、`|` 和 `^` 運算子支援複合指派，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="318bd-213">The `&`, `|`, and `^` operators support compound assignment, as the following example shows:</span></span>

[!code-csharp-interactive[compound assignment](snippets/BooleanLogicalOperators.cs#CompoundAssignment)]

> [!NOTE]
> <span data-ttu-id="318bd-214">條件邏輯運算子 `&&` 和 `||` 不支援複合指派。</span><span class="sxs-lookup"><span data-stu-id="318bd-214">The conditional logical operators `&&` and `||` don't support compound assignment.</span></span>

## <a name="operator-precedence"></a><span data-ttu-id="318bd-215">運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="318bd-215">Operator precedence</span></span>

<span data-ttu-id="318bd-216">下列清單會依優先順序將邏輯運算子排序 (從最高到最低)：</span><span class="sxs-lookup"><span data-stu-id="318bd-216">The following list orders logical operators starting from the highest precedence to the lowest:</span></span>

- <span data-ttu-id="318bd-217">邏輯負運算子 `!`</span><span class="sxs-lookup"><span data-stu-id="318bd-217">Logical negation operator `!`</span></span>
- <span data-ttu-id="318bd-218">邏輯 AND 運算子 `&`</span><span class="sxs-lookup"><span data-stu-id="318bd-218">Logical AND operator `&`</span></span>
- <span data-ttu-id="318bd-219">邏輯互斥 OR 運算子 `^`</span><span class="sxs-lookup"><span data-stu-id="318bd-219">Logical exclusive OR operator `^`</span></span>
- <span data-ttu-id="318bd-220">邏輯 OR 運算子 `|`</span><span class="sxs-lookup"><span data-stu-id="318bd-220">Logical OR operator `|`</span></span>
- <span data-ttu-id="318bd-221">條件邏輯 AND 運算子 `&&`</span><span class="sxs-lookup"><span data-stu-id="318bd-221">Conditional logical AND operator `&&`</span></span>
- <span data-ttu-id="318bd-222">條件邏輯 OR 運算子 `||`</span><span class="sxs-lookup"><span data-stu-id="318bd-222">Conditional logical OR operator `||`</span></span>

<span data-ttu-id="318bd-223">使用括號 `()` 來變更由運算子優先順序所強制執行的評估順序：</span><span class="sxs-lookup"><span data-stu-id="318bd-223">Use parentheses, `()`, to change the order of evaluation imposed by operator precedence:</span></span>

[!code-csharp-interactive[operator precedence](snippets/BooleanLogicalOperators.cs#Precedence)]

<span data-ttu-id="318bd-224">如需依優先順序層級排序之 c # 運算子的完整清單，請參閱[c # 運算子](index.md)一文的[運算子優先順序](index.md#operator-precedence)一節。</span><span class="sxs-lookup"><span data-stu-id="318bd-224">For the complete list of C# operators ordered by precedence level, see the [Operator precedence](index.md#operator-precedence) section of the [C# operators](index.md) article.</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="318bd-225">運算子是否可多載</span><span class="sxs-lookup"><span data-stu-id="318bd-225">Operator overloadability</span></span>

<span data-ttu-id="318bd-226">使用者定義型[別可以多](operator-overloading.md)載 `!` 、 `&` 、 `|` 和 `^` 運算子。</span><span class="sxs-lookup"><span data-stu-id="318bd-226">A user-defined type can [overload](operator-overloading.md) the `!`, `&`, `|`, and `^` operators.</span></span> <span data-ttu-id="318bd-227">當二元運算子多載時，對應的複合指派運算子也會隱含地多載。</span><span class="sxs-lookup"><span data-stu-id="318bd-227">When a binary operator is overloaded, the corresponding compound assignment operator is also implicitly overloaded.</span></span> <span data-ttu-id="318bd-228">使用者定義型別無法明確地多載複合指派運算子。</span><span class="sxs-lookup"><span data-stu-id="318bd-228">A user-defined type cannot explicitly overload a compound assignment operator.</span></span>

<span data-ttu-id="318bd-229">使用者定義類型無法多載條件邏輯運算子 `&&` 和 `||`。</span><span class="sxs-lookup"><span data-stu-id="318bd-229">A user-defined type cannot overload the conditional logical operators `&&` and `||`.</span></span> <span data-ttu-id="318bd-230">不過，若使用者定義類型以某種方式多載 [True 和 False 運算子](true-false-operators.md)以及 `&` 或 `|` 運算子，就可以針對該類型的運算元個別評估 `&&` 或 `||` 作業。</span><span class="sxs-lookup"><span data-stu-id="318bd-230">However, if a user-defined type overloads the [true and false operators](true-false-operators.md) and the `&` or `|` operator in a certain way, the `&&` or `||` operation, respectively, can be evaluated for the operands of that type.</span></span> <span data-ttu-id="318bd-231">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[使用者定義條件式邏輯運算子](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators)一節。</span><span class="sxs-lookup"><span data-stu-id="318bd-231">For more information, see the [User-defined conditional logical operators](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="318bd-232">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="318bd-232">C# language specification</span></span>

<span data-ttu-id="318bd-233">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的下列幾節：</span><span class="sxs-lookup"><span data-stu-id="318bd-233">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="318bd-234">邏輯否定運算子</span><span class="sxs-lookup"><span data-stu-id="318bd-234">Logical negation operator</span></span>](~/_csharplang/spec/expressions.md#logical-negation-operator)
- [<span data-ttu-id="318bd-235">邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="318bd-235">Logical operators</span></span>](~/_csharplang/spec/expressions.md#logical-operators)
- [<span data-ttu-id="318bd-236">條件邏輯運算子</span><span class="sxs-lookup"><span data-stu-id="318bd-236">Conditional logical operators</span></span>](~/_csharplang/spec/expressions.md#conditional-logical-operators)
- [<span data-ttu-id="318bd-237">複合指派</span><span class="sxs-lookup"><span data-stu-id="318bd-237">Compound assignment</span></span>](~/_csharplang/spec/expressions.md#compound-assignment)

## <a name="see-also"></a><span data-ttu-id="318bd-238">另請參閱</span><span class="sxs-lookup"><span data-stu-id="318bd-238">See also</span></span>

- [<span data-ttu-id="318bd-239">C# 參考資料</span><span class="sxs-lookup"><span data-stu-id="318bd-239">C# reference</span></span>](../index.md)
- [<span data-ttu-id="318bd-240">C# 運算子與運算式</span><span class="sxs-lookup"><span data-stu-id="318bd-240">C# operators and expressions</span></span>](index.md)
- [<span data-ttu-id="318bd-241">位元與移位運算子</span><span class="sxs-lookup"><span data-stu-id="318bd-241">Bitwise and shift operators</span></span>](bitwise-and-shift-operators.md)
