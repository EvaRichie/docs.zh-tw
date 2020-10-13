---
description: switch (C# 參考)
title: C# switch 陳述式
ms.date: 04/09/2019
f1_keywords:
- switch_CSharpKeyword
- switch
- case
- case_CSharpKeyword
- defaultcase_CSharpKeyword
helpviewer_keywords:
- switch statement [C#]
- switch keyword [C#]
- case statement [C#]
- default keyword [C#]
ms.assetid: 44bae8b8-8841-4d85-826b-8a94277daecb
ms.openlocfilehash: 2d12091f3c3f10048a98f5f0ecf6a381087faf41
ms.sourcegitcommit: e078b7540a8293ca1b604c9c0da1ff1506f0170b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91997687"
---
# <a name="switch-c-reference"></a><span data-ttu-id="7ac38-103">switch (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="7ac38-103">switch (C# reference)</span></span>

<span data-ttu-id="7ac38-104">本文涵蓋 `switch` 語句。</span><span class="sxs-lookup"><span data-stu-id="7ac38-104">This article covers the `switch` statement.</span></span> <span data-ttu-id="7ac38-105">如需 `switch` c # 8.0) 中所引進運算式 (的詳細資訊，請參閱「[運算式和運算子](../operators/index.md)」一節中有關[ `switch` 運算式](../operators/switch-expression.md)的文章。</span><span class="sxs-lookup"><span data-stu-id="7ac38-105">For information on the `switch` expression (introduced in C# 8.0), see the article on [`switch` expressions](../operators/switch-expression.md) in the [expressions and operators](../operators/index.md) section.</span></span>

<span data-ttu-id="7ac38-106">`switch`這是選取範圍語句，可根據符合*運算式*的模式比對，從候選項清單中選擇要執行的單一*參數區段*。</span><span class="sxs-lookup"><span data-stu-id="7ac38-106">`switch` is a selection statement that chooses a single *switch section* to execute from a list of candidates based on a pattern match with the *match expression*.</span></span>

[!code-csharp[switch#1](~/samples/snippets/csharp/language-reference/keywords/switch/switch1.cs#1)]

<span data-ttu-id="7ac38-107">如果針對三個或多個條件測試單一運算式，則通常會使用 `switch` 陳述式來替代 [if-else](if-else.md) 建構。</span><span class="sxs-lookup"><span data-stu-id="7ac38-107">The `switch` statement is often used as an alternative to an [if-else](if-else.md) construct if a single expression is tested against three or more conditions.</span></span> <span data-ttu-id="7ac38-108">例如，下列 `switch` 陳述式判斷 `Color` 類型的變數是否有三個值之一︰</span><span class="sxs-lookup"><span data-stu-id="7ac38-108">For example, the following `switch` statement determines whether a variable of type `Color` has one of three values:</span></span>

[!code-csharp[switch#3](~/samples/snippets/csharp/language-reference/keywords/switch/switch3.cs#1)]

<span data-ttu-id="7ac38-109">它等同於下列使用 `if`-`else` 建構的範例。</span><span class="sxs-lookup"><span data-stu-id="7ac38-109">It's equivalent to the following example that uses an `if`-`else` construct.</span></span>

[!code-csharp[switch#3a](~/samples/snippets/csharp/language-reference/keywords/switch/switch3a.cs#1)]

## <a name="the-match-expression"></a><span data-ttu-id="7ac38-110">比對運算式</span><span class="sxs-lookup"><span data-stu-id="7ac38-110">The match expression</span></span>

<span data-ttu-id="7ac38-111">比對運算式提供要與 `case` 標籤中的模式進行比對的值。</span><span class="sxs-lookup"><span data-stu-id="7ac38-111">The match expression provides the value to match against the patterns in `case` labels.</span></span> <span data-ttu-id="7ac38-112">其語法如下：</span><span class="sxs-lookup"><span data-stu-id="7ac38-112">Its syntax is:</span></span>

```csharp
   switch (expr)
```

<span data-ttu-id="7ac38-113">在 C# 6 和更早坂本中，比對運算式必須是傳回下列類型之值的運算式︰</span><span class="sxs-lookup"><span data-stu-id="7ac38-113">In C# 6 and earlier, the match expression must be an expression that returns a value of the following types:</span></span>

- <span data-ttu-id="7ac38-114">[char](../builtin-types/char.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac38-114">a [char](../builtin-types/char.md).</span></span>
- <span data-ttu-id="7ac38-115">[字串](../builtin-types/reference-types.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac38-115">a [string](../builtin-types/reference-types.md).</span></span>
- <span data-ttu-id="7ac38-116">[bool](../builtin-types/bool.md)。</span><span class="sxs-lookup"><span data-stu-id="7ac38-116">a [bool](../builtin-types/bool.md).</span></span>
- <span data-ttu-id="7ac38-117">[整數](../builtin-types/integral-numeric-types.md)值，例如 `int` 或 `long` 。</span><span class="sxs-lookup"><span data-stu-id="7ac38-117">an [integral](../builtin-types/integral-numeric-types.md) value, such as an `int` or a `long`.</span></span>
- <span data-ttu-id="7ac38-118">[列舉](../builtin-types/enum.md)值。</span><span class="sxs-lookup"><span data-stu-id="7ac38-118">an [enum](../builtin-types/enum.md) value.</span></span>

<span data-ttu-id="7ac38-119">從 C# 7.0 開始，比對運算式可以是任何非 Null 運算式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-119">Starting with C# 7.0, the match expression can be any non-null expression.</span></span>

## <a name="the-switch-section"></a><span data-ttu-id="7ac38-120">參數區段</span><span class="sxs-lookup"><span data-stu-id="7ac38-120">The switch section</span></span>

<span data-ttu-id="7ac38-121">`switch` 陳述式包含一個或多個參數區段。</span><span class="sxs-lookup"><span data-stu-id="7ac38-121">A `switch` statement includes one or more switch sections.</span></span> <span data-ttu-id="7ac38-122">每個參數區段都包含一或多個 *case 標籤* (案例或預設標籤，) 後面接著一個或多個語句。</span><span class="sxs-lookup"><span data-stu-id="7ac38-122">Each switch section contains one or more *case labels* (either a case or default label) followed by one or more statements.</span></span> <span data-ttu-id="7ac38-123">`switch` 陳述式在任何參數區段中最多只能放置一個預設標籤。</span><span class="sxs-lookup"><span data-stu-id="7ac38-123">The `switch` statement may include at most one default label placed in any switch section.</span></span> <span data-ttu-id="7ac38-124">下列範例示範擁有三個參數區段的簡單 `switch` 陳述式，每個區段包含兩個陳述式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-124">The following example shows a simple `switch` statement that has three switch sections, each containing two statements.</span></span> <span data-ttu-id="7ac38-125">第二個參數區段包含 `case 2:` 和 `case 3:` 標籤。</span><span class="sxs-lookup"><span data-stu-id="7ac38-125">The second switch section contains the `case 2:` and `case 3:` labels.</span></span>

<span data-ttu-id="7ac38-126">`switch` 陳述式可包含任意數目的參數區段，而每個區段都可以擁有一或多個 case 標籤，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="7ac38-126">A `switch` statement can include any number of switch sections, and each section can have one or more case labels, as shown in the following example.</span></span> <span data-ttu-id="7ac38-127">不過，不可以有兩個 case 標籤包含相同的運算式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-127">However, no two case labels may contain the same expression.</span></span>

[!code-csharp[switch#2](~/samples/snippets/csharp/language-reference/keywords/switch/switch2.cs#1)]

<span data-ttu-id="7ac38-128">switch 陳述式中只會執行一個參數區段。</span><span class="sxs-lookup"><span data-stu-id="7ac38-128">Only one switch section in a switch statement executes.</span></span> <span data-ttu-id="7ac38-129">C# 不允許從某個參數區段繼續執行至另一個參數區段。</span><span class="sxs-lookup"><span data-stu-id="7ac38-129">C# doesn't allow execution to continue from one switch section to the next.</span></span> <span data-ttu-id="7ac38-130">因此，下列程式碼會產生編譯器錯誤 CS0163：「程式控制權無法從一個 case 標籤 (\<case label>) 繼續到另一個」。</span><span class="sxs-lookup"><span data-stu-id="7ac38-130">Because of this, the following code generates a compiler error, CS0163: "Control cannot fall through from one case label (\<case label>) to another."</span></span>

```csharp
switch (caseSwitch)
{
    // The following switch section causes an error.
    case 1:
        Console.WriteLine("Case 1...");
        // Add a break or other jump statement here.
    case 2:
        Console.WriteLine("... and/or Case 2");
        break;
}
```

<span data-ttu-id="7ac38-131">使用 [break](break.md)、[goto](goto.md) 或 [return](return.md) 陳述式明確地結束參數區段，通常會符合這項需求。</span><span class="sxs-lookup"><span data-stu-id="7ac38-131">This requirement is usually met by explicitly exiting the switch section by using a [break](break.md), [goto](goto.md), or [return](return.md) statement.</span></span> <span data-ttu-id="7ac38-132">不過，下列程式碼也是有效，因為它可確保程式控制權無法切換到 `default` 參數區段。</span><span class="sxs-lookup"><span data-stu-id="7ac38-132">However, the following code is also valid, because it ensures that program control can't fall through to the `default` switch section.</span></span>

[!code-csharp[switch#4](~/samples/snippets/csharp/language-reference/keywords/switch/switch4.cs#1)]

<span data-ttu-id="7ac38-133">在 case 標籤符合比對運算式的參數區段中，陳述式清單是從第一個陳述式開始執行，然後繼續進行整份陳述式清單，通常會進行直到跳躍陳述式為止，例如到達 `break`、`goto case`、`goto label`、`return` 或 `throw`。</span><span class="sxs-lookup"><span data-stu-id="7ac38-133">Execution of the statement list in the switch section with a case label that matches the match expression begins with the first statement and proceeds through the statement list, typically until a jump statement, such as a `break`, `goto case`, `goto label`, `return`, or `throw`, is reached.</span></span> <span data-ttu-id="7ac38-134">到達該點時，控制項會在 `switch` 陳述式之外傳輸，或傳輸至另一個 case 標籤。</span><span class="sxs-lookup"><span data-stu-id="7ac38-134">At that point, control is transferred outside the `switch` statement or to another case label.</span></span> <span data-ttu-id="7ac38-135">如果使用 `goto` 陳述式，就必須將控制權轉移到常數標籤。</span><span class="sxs-lookup"><span data-stu-id="7ac38-135">A `goto` statement, if it's used, must transfer control to a constant label.</span></span> <span data-ttu-id="7ac38-136">這項限制是必要的，因為嘗試將控制項傳送至非常數標籤，會將控制項傳送至程式碼中非預期的位置或建立無止盡的迴圈，出現非預期的副作用。</span><span class="sxs-lookup"><span data-stu-id="7ac38-136">This restriction is necessary, since attempting to transfer control to a non-constant label can have undesirable side-effects, such transferring control to an unintended location in code or creating an endless loop.</span></span>

## <a name="case-labels"></a><span data-ttu-id="7ac38-137">case 標籤</span><span class="sxs-lookup"><span data-stu-id="7ac38-137">Case labels</span></span>

<span data-ttu-id="7ac38-138">每個 case 標籤都會指定要與比對運算式比較的模式 (先前範例中的 `caseSwitch` 變數)。</span><span class="sxs-lookup"><span data-stu-id="7ac38-138">Each case label specifies a pattern to compare to the match expression (the `caseSwitch` variable in the previous examples).</span></span> <span data-ttu-id="7ac38-139">如果相符，控制權會轉移至包含「第一個」\*\*\*\* 相符 case 標籤的參數區段。</span><span class="sxs-lookup"><span data-stu-id="7ac38-139">If they match, control is transferred to the switch section that contains the **first** matching case label.</span></span> <span data-ttu-id="7ac38-140">若無任何狀況標籤模式符合比對運算式，會將控制權轉移到具有 `default` 狀況標籤的區段 (如有此區段)。</span><span class="sxs-lookup"><span data-stu-id="7ac38-140">If no case label pattern matches the match expression, control is transferred to the section with the `default` case label, if there's one.</span></span> <span data-ttu-id="7ac38-141">如果沒有 `default` 狀況，則不會執行任何參數區段中的陳述式，而且控制權會轉移到 `switch` 陳述式外部。</span><span class="sxs-lookup"><span data-stu-id="7ac38-141">If there's no `default` case, no statements in any switch section are executed, and control is transferred outside the `switch` statement.</span></span>

<span data-ttu-id="7ac38-142">如需 `switch` 陳述式和模式比對的資訊，請參閱[模式比對與 `switch` 陳述式](#pattern-matching-with-the-switch-statement)一節。</span><span class="sxs-lookup"><span data-stu-id="7ac38-142">For information on the `switch` statement and pattern matching, see the [Pattern matching with the `switch` statement](#pattern-matching-with-the-switch-statement) section.</span></span>

<span data-ttu-id="7ac38-143">因為 C# 6 只支援常數模式，且不允許重複常數值，所以狀況標籤會定義互斥值，而且只有一個模式可以符合比對運算式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-143">Because C# 6 supports only the constant pattern and doesn't allow the repetition of constant values, case labels define mutually exclusive values, and only one pattern can match the match expression.</span></span> <span data-ttu-id="7ac38-144">因此，`case` 陳述式的出現順序並不重要。</span><span class="sxs-lookup"><span data-stu-id="7ac38-144">As a result, the order in which `case` statements appear is unimportant.</span></span>

<span data-ttu-id="7ac38-145">不過，在 C# 7.0 中，因為支援其他模式，所以 case 標籤不需要定義互斥值，而且可以有多個模式符合比對運算式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-145">In C# 7.0, however, because other patterns are supported, case labels need not define mutually exclusive values, and multiple patterns can match the match expression.</span></span> <span data-ttu-id="7ac38-146">因為只會執行包含相符模式之第一個參數區段中的陳述式，所以 `case` 陳述式的出現順序現在十分重要。</span><span class="sxs-lookup"><span data-stu-id="7ac38-146">Because only the statements in the first switch section that contains the matching pattern are executed, the order in which `case` statements appear is now important.</span></span> <span data-ttu-id="7ac38-147">如果 C# 偵測到一或多個 case 陳述式等於或為先前陳述式子集的參數區段，則會產生編譯器錯誤 CS8120：「先前的案例已處理切換案例。」</span><span class="sxs-lookup"><span data-stu-id="7ac38-147">If C# detects a switch section whose case statement or statements are equivalent to or are subsets of previous statements, it generates a compiler error, CS8120, "The switch case has already been handled by a previous case."</span></span>

<span data-ttu-id="7ac38-148">下列範例說明使用各種非互斥模式的 `switch` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-148">The following example illustrates a `switch` statement that uses a variety of non-mutually exclusive patterns.</span></span> <span data-ttu-id="7ac38-149">如果您移動 `case 0:` 參數區段，讓它不再是 `switch` 陳述式中的第一個區段，則 C# 會產生編譯器錯誤，因為值為零的整數是所有整數的子集，而這是 `case int val` 陳述式所定義的模式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-149">If you move the `case 0:` switch section so that it's no longer the first section in the `switch` statement, C# generates a compiler error because an integer whose value is zero is a subset of all integers, which is the pattern defined by the `case int val` statement.</span></span>

[!code-csharp[switch#5](~/samples/snippets/csharp/language-reference/keywords/switch/switch5.cs#1)]

<span data-ttu-id="7ac38-150">您可以更正此問題，並使用兩種方式之一來排除編譯器警告︰</span><span class="sxs-lookup"><span data-stu-id="7ac38-150">You can correct this issue and eliminate the compiler warning in one of two ways:</span></span>

- <span data-ttu-id="7ac38-151">變更參數區段的順序。</span><span class="sxs-lookup"><span data-stu-id="7ac38-151">By changing the order of the switch sections.</span></span>

- <span data-ttu-id="7ac38-152">在 `case` 標籤中使用 [when 子句](#the-case-statement-and-the-when-clause)。</span><span class="sxs-lookup"><span data-stu-id="7ac38-152">By using a [when clause](#the-case-statement-and-the-when-clause) in the `case` label.</span></span>

## <a name="the-default-case"></a><span data-ttu-id="7ac38-153">`default` case</span><span class="sxs-lookup"><span data-stu-id="7ac38-153">The `default` case</span></span>

<span data-ttu-id="7ac38-154">如果比對運算式不符合任何其他 `case` 標籤，則 `default` 狀況會指定要執行的參數區段。</span><span class="sxs-lookup"><span data-stu-id="7ac38-154">The `default` case specifies the switch section to execute if the match expression doesn't match any other `case` label.</span></span> <span data-ttu-id="7ac38-155">如果 `default` 狀況不存在，而且比對運算式不符合任何其他 `case` 標籤，則程式流程會落到 `switch` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-155">If a `default` case is not present and the match expression doesn't match any other `case` label, program flow falls through the `switch` statement.</span></span>

<span data-ttu-id="7ac38-156">`default` case 可以依任何順序出現在 `switch` 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="7ac38-156">The `default` case can appear in any order in the `switch` statement.</span></span> <span data-ttu-id="7ac38-157">不論它在原始程式碼中的順序為何，一律都會在評估過所有 `case` 標籤之後最後才進行評估。</span><span class="sxs-lookup"><span data-stu-id="7ac38-157">Regardless of its order in the source code, it's always evaluated last, after all `case` labels have been evaluated.</span></span>

## <a name="pattern-matching-with-the-switch-statement"></a><span data-ttu-id="7ac38-158">使用  陳述式進行的 `switch` 模式比對</span><span class="sxs-lookup"><span data-stu-id="7ac38-158">Pattern matching with the `switch` statement</span></span>

<span data-ttu-id="7ac38-159">每個 `case` 陳述式都會定義一個模式，並在模式符合比對運算式時，執行其包含參數區段。</span><span class="sxs-lookup"><span data-stu-id="7ac38-159">Each `case` statement defines a pattern that, if it matches the match expression, causes its  containing switch section to be executed.</span></span> <span data-ttu-id="7ac38-160">所有版本的 C# 都支援常數模式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-160">All versions of C# support the constant pattern.</span></span> <span data-ttu-id="7ac38-161">從 C# 7.0 開始，支援其餘的模式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-161">The remaining patterns are supported beginning with C# 7.0.</span></span>

### <a name="constant-pattern"></a><span data-ttu-id="7ac38-162">常數模式</span><span class="sxs-lookup"><span data-stu-id="7ac38-162">Constant pattern</span></span>

<span data-ttu-id="7ac38-163">常數模式會測試比對運算式是否等於指定的常數。</span><span class="sxs-lookup"><span data-stu-id="7ac38-163">The constant pattern tests whether the match expression equals a specified constant.</span></span> <span data-ttu-id="7ac38-164">其語法如下：</span><span class="sxs-lookup"><span data-stu-id="7ac38-164">Its syntax is:</span></span>

```csharp
   case constant:
```

<span data-ttu-id="7ac38-165">其中，*constant* 是用來測試的值。</span><span class="sxs-lookup"><span data-stu-id="7ac38-165">where *constant* is the value to test for.</span></span> <span data-ttu-id="7ac38-166">*constant* 可以是下列任何常數運算式：</span><span class="sxs-lookup"><span data-stu-id="7ac38-166">*constant* can be any of the following constant expressions:</span></span>

- <span data-ttu-id="7ac38-167">[Bool](../builtin-types/bool.md)常值： `true` 或 `false` 。</span><span class="sxs-lookup"><span data-stu-id="7ac38-167">A [bool](../builtin-types/bool.md) literal: either `true` or `false`.</span></span>
- <span data-ttu-id="7ac38-168">任何 [整數](../builtin-types/integral-numeric-types.md) 常數，例如 `int` 、 `long` 或 `byte` 。</span><span class="sxs-lookup"><span data-stu-id="7ac38-168">Any [integral](../builtin-types/integral-numeric-types.md) constant, such as an `int`, a `long`, or a `byte`.</span></span>
- <span data-ttu-id="7ac38-169">所宣告之 `const` 變數的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ac38-169">The name of a declared `const` variable.</span></span>
- <span data-ttu-id="7ac38-170">列舉常數。</span><span class="sxs-lookup"><span data-stu-id="7ac38-170">An enumeration constant.</span></span>
- <span data-ttu-id="7ac38-171">[char](../builtin-types/char.md) 常值。</span><span class="sxs-lookup"><span data-stu-id="7ac38-171">A [char](../builtin-types/char.md) literal.</span></span>
- <span data-ttu-id="7ac38-172">[string](../builtin-types/reference-types.md) 常值。</span><span class="sxs-lookup"><span data-stu-id="7ac38-172">A [string](../builtin-types/reference-types.md) literal.</span></span>

<span data-ttu-id="7ac38-173">常數運算式評估如下：</span><span class="sxs-lookup"><span data-stu-id="7ac38-173">The constant expression is evaluated as follows:</span></span>

- <span data-ttu-id="7ac38-174">如果 *expr* 和 *constant* 是整數型別，則 C# 等號比較運算子會判斷運算式是否傳回 `true` (亦即是否 `expr == constant`)。</span><span class="sxs-lookup"><span data-stu-id="7ac38-174">If *expr* and *constant* are integral types, the C# equality operator determines whether the expression returns `true` (that is, whether `expr == constant`).</span></span>

- <span data-ttu-id="7ac38-175">否則，會呼叫靜態 [Object.Equals(expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) 方法來判斷運算式的值。</span><span class="sxs-lookup"><span data-stu-id="7ac38-175">Otherwise, the value of the expression is determined by a call to the static [Object.Equals(expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) method.</span></span>

<span data-ttu-id="7ac38-176">下列範例使用常數模式，來判斷特定日期是週末、工作週的第一天、工作週的最後一天，還是工作週的中間一天。</span><span class="sxs-lookup"><span data-stu-id="7ac38-176">The following example uses the constant pattern to determine whether a particular date is a weekend, the first day of the work week, the last day of the work week, or the middle of the work week.</span></span> <span data-ttu-id="7ac38-177">其會依據 <xref:System.DayOfWeek> 列舉的成員，評估當日的 <xref:System.DateTime.DayOfWeek?displayProperty=nameWithType> 屬性。</span><span class="sxs-lookup"><span data-stu-id="7ac38-177">It evaluates the <xref:System.DateTime.DayOfWeek?displayProperty=nameWithType> property of the current day against the members of the <xref:System.DayOfWeek> enumeration.</span></span>

[!code-csharp[switch#7](~/samples/snippets/csharp/language-reference/keywords/switch/const-pattern.cs#1)]

<span data-ttu-id="7ac38-178">下列範例使用常數模式，來處理模擬自動咖啡機之主控台應用程式中的使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="7ac38-178">The following example uses the constant pattern to handle user input in a console application that simulates an automatic coffee machine.</span></span>

[!code-csharp[switch#6](~/samples/snippets/csharp/language-reference/keywords/switch/switch6.cs)]

### <a name="type-pattern"></a><span data-ttu-id="7ac38-179">類型模式</span><span class="sxs-lookup"><span data-stu-id="7ac38-179">Type pattern</span></span>

<span data-ttu-id="7ac38-180">類型模式會啟用精簡類型評估和轉換。</span><span class="sxs-lookup"><span data-stu-id="7ac38-180">The type pattern enables concise type evaluation and conversion.</span></span> <span data-ttu-id="7ac38-181">與 `switch` 陳述式搭配使用來執行模式比對時，會測試運算式是否可轉換成指定的類型；如果可以的話，則會將它轉換成該類型的變數。</span><span class="sxs-lookup"><span data-stu-id="7ac38-181">When used with the `switch` statement to perform pattern matching, it tests whether an expression can be converted to a specified type and, if it can be, casts it to a variable of that type.</span></span> <span data-ttu-id="7ac38-182">其語法如下：</span><span class="sxs-lookup"><span data-stu-id="7ac38-182">Its syntax is:</span></span>

```csharp
   case type varname
```

<span data-ttu-id="7ac38-183">其中，如果比對成功，則 *type* 是 *expr* 的結果要轉換的目標類型名稱，而 *varname* 是 *expr* 的結果所轉換的目標物件。</span><span class="sxs-lookup"><span data-stu-id="7ac38-183">where *type* is the name of the type to which the result of *expr* is to be converted, and *varname* is the object to which the result of *expr* is converted if the match succeeds.</span></span> <span data-ttu-id="7ac38-184">從 C# 7.1 開始，編譯時間類型的 *expr* 可以是泛型類型參數。</span><span class="sxs-lookup"><span data-stu-id="7ac38-184">The compile-time type of *expr* may be a generic type parameter, starting with C# 7.1.</span></span>

<span data-ttu-id="7ac38-185">如果符合下列任一項，則 `case` 運算式為`true`：</span><span class="sxs-lookup"><span data-stu-id="7ac38-185">The `case` expression is `true` if any of the following is true:</span></span>

- <span data-ttu-id="7ac38-186">*expr* 是其類型與 *type* 相同的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ac38-186">*expr* is an instance of the same type as *type*.</span></span>

- <span data-ttu-id="7ac38-187">*expr* 是衍生自 *type* 的類型執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ac38-187">*expr* is an instance of a type that derives from *type*.</span></span> <span data-ttu-id="7ac38-188">換句話說，*expr* 的結果可向上轉型成 *type* 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ac38-188">In other words, the result of *expr* can be upcast to an instance of *type*.</span></span>

- <span data-ttu-id="7ac38-189">*expr* 的編譯時期類型為 *type* 的基底類別，而 *expr* 的執行階段類型為 *type* 或衍生自 *type*。</span><span class="sxs-lookup"><span data-stu-id="7ac38-189">*expr* has a compile-time type that is a base class of *type*, and *expr* has a runtime type that is *type* or is derived from *type*.</span></span> <span data-ttu-id="7ac38-190">變數的「編譯時期類型」\*\* 是定義於其型別宣告的變數類型。</span><span class="sxs-lookup"><span data-stu-id="7ac38-190">The *compile-time type* of a variable is the variable's type as defined in its type declaration.</span></span> <span data-ttu-id="7ac38-191">變數的「執行階段類型」\*\* 是指派給該變數的執行個體類型。</span><span class="sxs-lookup"><span data-stu-id="7ac38-191">The *runtime type* of a variable is the type of the instance that is assigned to that variable.</span></span>

- <span data-ttu-id="7ac38-192">*expr* 是實作 *type* 介面的類型執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ac38-192">*expr* is an instance of a type that implements the *type* interface.</span></span>

<span data-ttu-id="7ac38-193">如果 case 運算式為 true，則 *varname* 會明確地進行指派，並且只具有參數區段內的區域範圍。</span><span class="sxs-lookup"><span data-stu-id="7ac38-193">If the case expression is true, *varname* is definitely assigned and has local scope within the switch section only.</span></span>

<span data-ttu-id="7ac38-194">請注意，`null` 不會符合類型。</span><span class="sxs-lookup"><span data-stu-id="7ac38-194">Note that `null` doesn't match a type.</span></span> <span data-ttu-id="7ac38-195">若要比對 `null`，請使用下列 `case` 標籤︰</span><span class="sxs-lookup"><span data-stu-id="7ac38-195">To match a `null`, you use the following `case` label:</span></span>

```csharp
case null:
```

<span data-ttu-id="7ac38-196">下列範例使用類型模式提供各種集合類型的資訊。</span><span class="sxs-lookup"><span data-stu-id="7ac38-196">The following example uses the type pattern to provide information about various kinds of collection types.</span></span>

[!code-csharp[type-pattern#1](~/samples/snippets/csharp/language-reference/keywords/switch/type-pattern.cs#1)]

<span data-ttu-id="7ac38-197">與其使用 `object`，您可以建立泛型方法，使用集合的類型作為類型參數，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="7ac38-197">Instead of `object`, you could make a generic method, using the type of the collection as the type parameter, as shown in the following code:</span></span>

[!code-csharp[type-pattern#3](~/samples/snippets/csharp/language-reference/keywords/switch/type-pattern3.cs#1)]

<span data-ttu-id="7ac38-198">泛型版本與第一個範例之間有兩個差異。</span><span class="sxs-lookup"><span data-stu-id="7ac38-198">The generic version is different than the first sample in two ways.</span></span> <span data-ttu-id="7ac38-199">首先，您無法使用 `null` 狀況。</span><span class="sxs-lookup"><span data-stu-id="7ac38-199">First, you can't use the `null` case.</span></span> <span data-ttu-id="7ac38-200">您無法使用任何常數狀況，因為編譯器無法將任何任意類型 `T` 轉換為 `object`以外的任何其他類型。</span><span class="sxs-lookup"><span data-stu-id="7ac38-200">You can't use any constant case because the compiler can't convert any arbitrary type `T` to any type other than `object`.</span></span> <span data-ttu-id="7ac38-201">先前的 `default` 狀況現在會針對非 Null `object`進行測試。</span><span class="sxs-lookup"><span data-stu-id="7ac38-201">What had been the `default` case now tests for a non-null `object`.</span></span> <span data-ttu-id="7ac38-202">這代表 `default` 狀況只會針對 `null` 進行測試。</span><span class="sxs-lookup"><span data-stu-id="7ac38-202">That means the `default` case tests only for `null`.</span></span>

<span data-ttu-id="7ac38-203">如果沒有模式比對，此程式碼可能會撰寫如下。</span><span class="sxs-lookup"><span data-stu-id="7ac38-203">Without pattern matching, this code might be written as follows.</span></span> <span data-ttu-id="7ac38-204">使用類型模式比對時，不需要測試轉換的結果是否為 `null` 或執行重複轉換，因此會產生更精簡且容易閱讀的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ac38-204">The use of type pattern matching produces more compact, readable code by eliminating the need to test whether the result of a conversion is a `null` or to perform repeated casts.</span></span>

[!code-csharp[type-pattern2#1](~/samples/snippets/csharp/language-reference/keywords/switch/type-pattern2.cs#1)]

## <a name="the-case-statement-and-the-when-clause"></a><span data-ttu-id="7ac38-205">`case` 陳述式和 `when` 子句</span><span class="sxs-lookup"><span data-stu-id="7ac38-205">The `case` statement and the `when` clause</span></span>

<span data-ttu-id="7ac38-206">從 C# 7.0 開始，因為 case 陳述式不需要互斥，所以您可以新增 `when` 子句來指定其他條件，您必須滿足這些條件，case 陳述式才會評估為 true。</span><span class="sxs-lookup"><span data-stu-id="7ac38-206">Starting with C# 7.0, because case statements need not be mutually exclusive, you can add a `when` clause to specify an additional condition that must be satisfied for the case statement to evaluate to true.</span></span> <span data-ttu-id="7ac38-207">`when` 子句可以是任何傳回布林值的運算式。</span><span class="sxs-lookup"><span data-stu-id="7ac38-207">The `when` clause can be any expression that returns a Boolean value.</span></span>

<span data-ttu-id="7ac38-208">下面範例定義基底 `Shape` 類別、衍生自 `Shape` 的 `Rectangle` 類別，以及衍生自 `Rectangle` 的 `Square` 類別。</span><span class="sxs-lookup"><span data-stu-id="7ac38-208">The following example defines a base `Shape` class, a `Rectangle` class that derives from `Shape`, and a `Square` class that derives from `Rectangle`.</span></span> <span data-ttu-id="7ac38-209">它會使用 `when` 子句，確保 `ShowShapeInfo` 將已指派相等長度和寬度的 `Rectangle` 物件視為 `Square`，即使尚未具現化為 `Square` 物件也是一樣。</span><span class="sxs-lookup"><span data-stu-id="7ac38-209">It uses the `when` clause to ensure that the `ShowShapeInfo` treats a `Rectangle` object that has been assigned equal lengths and widths as a `Square` even if it hasn't been instantiated as a `Square` object.</span></span> <span data-ttu-id="7ac38-210">此方法不會嘗試顯示為 `null` 的物件或區域為零之組織結構的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ac38-210">The method doesn't attempt to display information either about an object that is `null` or a shape whose area is zero.</span></span>

[!code-csharp[when-clause#1](~/samples/snippets/csharp/language-reference/keywords/switch/when-clause.cs#1)]

<span data-ttu-id="7ac38-211">請注意，不會執行範例中嘗試測試 `Shape` 物件是否為 `null` 的 `when` 子句。</span><span class="sxs-lookup"><span data-stu-id="7ac38-211">Note that the `when` clause in the example that attempts to test whether a `Shape` object is `null` doesn't execute.</span></span> <span data-ttu-id="7ac38-212">要測試是否為 `null` 的正確類型模式是 `case null:`。</span><span class="sxs-lookup"><span data-stu-id="7ac38-212">The correct type pattern to test for a `null` is `case null:`.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="7ac38-213">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="7ac38-213">C# language specification</span></span>

<span data-ttu-id="7ac38-214">如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)中的 [switch 陳述式](~/_csharplang/spec/statements.md#the-switch-statement)。</span><span class="sxs-lookup"><span data-stu-id="7ac38-214">For more information, see [The switch statement](~/_csharplang/spec/statements.md#the-switch-statement) in the [C# Language Specification](/dotnet/csharp/language-reference/language-specification/introduction).</span></span> <span data-ttu-id="7ac38-215">語言規格是 C# 語法及用法的限定來源。</span><span class="sxs-lookup"><span data-stu-id="7ac38-215">The language specification is the definitive source for C# syntax and usage.</span></span>

## <a name="see-also"></a><span data-ttu-id="7ac38-216">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7ac38-216">See also</span></span>

- [<span data-ttu-id="7ac38-217">C # 參考</span><span class="sxs-lookup"><span data-stu-id="7ac38-217">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="7ac38-218">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="7ac38-218">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="7ac38-219">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="7ac38-219">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="7ac38-220">如果-else</span><span class="sxs-lookup"><span data-stu-id="7ac38-220">if-else</span></span>](if-else.md)
- [<span data-ttu-id="7ac38-221">模式比對</span><span class="sxs-lookup"><span data-stu-id="7ac38-221">Pattern Matching</span></span>](../../pattern-matching.md)
