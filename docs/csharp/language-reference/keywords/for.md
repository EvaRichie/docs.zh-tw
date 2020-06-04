---
title: 'for 語句-c # 參考'
ms.date: 06/13/2018
f1_keywords:
- for
- for_CSharpKeyword
helpviewer_keywords:
- for keyword [C#]
ms.assetid: 34041a40-2c87-467a-9ffb-a0417d8f67a8
ms.openlocfilehash: db7cecc697a9cc9e5ff6b94b78747b799ed7e505
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401897"
---
# <a name="for-c-reference"></a><span data-ttu-id="92e06-102">for (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="92e06-102">for (C# reference)</span></span>

<span data-ttu-id="92e06-103">當指定的布林運算式評估為 `true` 時，`for` 陳述式會執行某個陳述式或陳述式區塊。</span><span class="sxs-lookup"><span data-stu-id="92e06-103">The `for` statement executes a statement or a block of statements while a specified Boolean expression evaluates to `true`.</span></span>

<span data-ttu-id="92e06-104">您可以在 `for` 陳述式區塊內的任何位置，使用 [break](break.md) 陳述式跳出迴圈，或使用 [continue](continue.md) 陳述式逐步執行到迴圈中的下一個反覆運算。</span><span class="sxs-lookup"><span data-stu-id="92e06-104">At any point within the `for` statement block, you can break out of the loop by using the [break](break.md) statement, or step to the next iteration in the loop by using the [continue](continue.md) statement.</span></span> <span data-ttu-id="92e06-105">您也可以使用 `for` [goto](goto.md)、 [return](return.md)或[throw](throw.md)語句來結束迴圈。</span><span class="sxs-lookup"><span data-stu-id="92e06-105">You can also exit a `for` loop by the [goto](goto.md), [return](return.md), or [throw](throw.md) statements.</span></span>

## <a name="structure-of-the-for-statement"></a><span data-ttu-id="92e06-106">`for` 陳述式的結構</span><span class="sxs-lookup"><span data-stu-id="92e06-106">Structure of the `for` statement</span></span>

<span data-ttu-id="92e06-107">`for` 陳述式會定義「初始設定式」**、「條件」** 和「迭代器」\*\* 區段：</span><span class="sxs-lookup"><span data-stu-id="92e06-107">The `for` statement defines *initializer*, *condition*, and *iterator* sections:</span></span>

```csharp
for (initializer; condition; iterator)
    body
```

<span data-ttu-id="92e06-108">三個區段都是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="92e06-108">All three sections are optional.</span></span> <span data-ttu-id="92e06-109">迴圈的主體是陳述式或陳述式區塊。</span><span class="sxs-lookup"><span data-stu-id="92e06-109">The body of the loop is either a statement or a block of statements.</span></span>

<span data-ttu-id="92e06-110">下列範例顯示 `for` 陳述式，並已定義所有區段：</span><span class="sxs-lookup"><span data-stu-id="92e06-110">The following example shows the `for` statement with all of the sections defined:</span></span>

[!code-csharp-interactive[for loop example](snippets/IterationKeywordsExamples.cs#5)]

### <a name="the-initializer-section"></a><span data-ttu-id="92e06-111">「初始設定式」\*\* 區段</span><span class="sxs-lookup"><span data-stu-id="92e06-111">The *initializer* section</span></span>

<span data-ttu-id="92e06-112">「初始設定式」\*\* 區段中的陳述式只執行一次，在進入迴圈之前。</span><span class="sxs-lookup"><span data-stu-id="92e06-112">The statements in the *initializer* section are executed only once, before entering the loop.</span></span> <span data-ttu-id="92e06-113">「初始設定式」\*\* 區段是下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="92e06-113">The *initializer* section is either of the following:</span></span>

- <span data-ttu-id="92e06-114">本機迴圈變數的宣告和初始化，這無法從迴圈外存取。</span><span class="sxs-lookup"><span data-stu-id="92e06-114">The declaration and initialization of a local loop variable, which can't be accessed from outside the loop.</span></span>

- <span data-ttu-id="92e06-115">下列清單中的零個以上陳述式運算式，並以逗號分隔：</span><span class="sxs-lookup"><span data-stu-id="92e06-115">Zero or more statement expressions from the following list, separated by commas:</span></span>

  - <span data-ttu-id="92e06-116">[指派](../operators/assignment-operator.md)陳述式</span><span class="sxs-lookup"><span data-stu-id="92e06-116">[assignment](../operators/assignment-operator.md) statement</span></span>

  - <span data-ttu-id="92e06-117">方法的引動過程</span><span class="sxs-lookup"><span data-stu-id="92e06-117">invocation of a method</span></span>

  - <span data-ttu-id="92e06-118">前置或後置[遞增](../operators/arithmetic-operators.md#increment-operator-)運算式，例如 `++i` 或 `i++`</span><span class="sxs-lookup"><span data-stu-id="92e06-118">prefix or postfix [increment](../operators/arithmetic-operators.md#increment-operator-) expression, such as `++i` or `i++`</span></span>

  - <span data-ttu-id="92e06-119">前置或後置[遞減](../operators/arithmetic-operators.md#decrement-operator---)運算式，例如 `--i` 或 `i--`</span><span class="sxs-lookup"><span data-stu-id="92e06-119">prefix or postfix [decrement](../operators/arithmetic-operators.md#decrement-operator---) expression, such as `--i` or `i--`</span></span>

  - <span data-ttu-id="92e06-120">使用 [new](../operators/new-operator.md) 運算子建立物件</span><span class="sxs-lookup"><span data-stu-id="92e06-120">creation of an object by using the [new](../operators/new-operator.md) operator</span></span>

  - <span data-ttu-id="92e06-121">[await](../operators/await.md) 運算式</span><span class="sxs-lookup"><span data-stu-id="92e06-121">[await](../operators/await.md) expression</span></span>

<span data-ttu-id="92e06-122">上述範例中的「初始設定式」\*\* 區段會宣告及初始化本機迴圈變數 `i`：</span><span class="sxs-lookup"><span data-stu-id="92e06-122">The *initializer* section in the example above declares and initializes the local loop variable `i`:</span></span>

```csharp
int i = 0
```

### <a name="the-condition-section"></a><span data-ttu-id="92e06-123">「條件」\*\* 區段</span><span class="sxs-lookup"><span data-stu-id="92e06-123">The *condition* section</span></span>

<span data-ttu-id="92e06-124">「條件」\*\* 區段如果存在的話，必須是布林運算式。</span><span class="sxs-lookup"><span data-stu-id="92e06-124">The *condition* section, if present, must be a boolean expression.</span></span> <span data-ttu-id="92e06-125">該運算式會在每次迴圈反覆運算之前評估。</span><span class="sxs-lookup"><span data-stu-id="92e06-125">That expression is evaluated before every loop iteration.</span></span> <span data-ttu-id="92e06-126">如果「條件」\*\* 區段不存在，或是布林運算式會評估為 `true`，就會執行下次迴圈反覆運算；否則迴圈會結束。</span><span class="sxs-lookup"><span data-stu-id="92e06-126">If the *condition* section is not present or the boolean expression evaluates to `true`, the next loop iteration is executed; otherwise, the loop is exited.</span></span>

<span data-ttu-id="92e06-127">上述範例中的「條件」\*\* 區段，會根據本機迴圈變數的值決定是否迴圈終止：</span><span class="sxs-lookup"><span data-stu-id="92e06-127">The *condition* section in the example above determines if the loop terminates based on the value of the local loop variable:</span></span>

```csharp
i < 5
```

### <a name="the-iterator-section"></a><span data-ttu-id="92e06-128">「迭代器」\*\* 區段</span><span class="sxs-lookup"><span data-stu-id="92e06-128">The *iterator* section</span></span>

<span data-ttu-id="92e06-129">「迭代器」\*\* 區段會定義迴圈主體每次反覆運算之後的狀況。</span><span class="sxs-lookup"><span data-stu-id="92e06-129">The *iterator* section defines what happens after each iteration of the body of the loop.</span></span> <span data-ttu-id="92e06-130">「迭代器」\*\* 區段包含下列零個以上陳述式運算式，並以逗號分隔：</span><span class="sxs-lookup"><span data-stu-id="92e06-130">The *iterator* section contains zero or more of the following statement expressions, separated by commas:</span></span>

- <span data-ttu-id="92e06-131">[指派](../operators/assignment-operator.md)陳述式</span><span class="sxs-lookup"><span data-stu-id="92e06-131">[assignment](../operators/assignment-operator.md) statement</span></span>

- <span data-ttu-id="92e06-132">方法的引動過程</span><span class="sxs-lookup"><span data-stu-id="92e06-132">invocation of a method</span></span>

- <span data-ttu-id="92e06-133">前置或後置[遞增](../operators/arithmetic-operators.md#increment-operator-)運算式，例如 `++i` 或 `i++`</span><span class="sxs-lookup"><span data-stu-id="92e06-133">prefix or postfix [increment](../operators/arithmetic-operators.md#increment-operator-) expression, such as `++i` or `i++`</span></span>

- <span data-ttu-id="92e06-134">前置或後置[遞減](../operators/arithmetic-operators.md#decrement-operator---)運算式，例如 `--i` 或 `i--`</span><span class="sxs-lookup"><span data-stu-id="92e06-134">prefix or postfix [decrement](../operators/arithmetic-operators.md#decrement-operator---) expression, such as `--i` or `i--`</span></span>

- <span data-ttu-id="92e06-135">使用 [new](../operators/new-operator.md) 運算子建立物件</span><span class="sxs-lookup"><span data-stu-id="92e06-135">creation of an object by using the [new](../operators/new-operator.md) operator</span></span>

- <span data-ttu-id="92e06-136">[await](../operators/await.md) 運算式</span><span class="sxs-lookup"><span data-stu-id="92e06-136">[await](../operators/await.md) expression</span></span>

<span data-ttu-id="92e06-137">上述範例中的「迭代器」\*\* 區段會遞增本機迴圈變數：</span><span class="sxs-lookup"><span data-stu-id="92e06-137">The *iterator* section in the example above increments the local loop variable:</span></span>

```csharp
i++
```

## <a name="examples"></a><span data-ttu-id="92e06-138">範例</span><span class="sxs-lookup"><span data-stu-id="92e06-138">Examples</span></span>

<span data-ttu-id="92e06-139">下列範例描述幾個較少見的 `for` 陳述式用法︰將值指派給「初始設定式」\*\* 區段中的外部迴圈變數、在「初始設定式」\*\* 和「迭代器」\*\* 區段中叫用方法，以及在「迭代器」\*\* 區段中變更兩個變數的值。</span><span class="sxs-lookup"><span data-stu-id="92e06-139">The following example illustrates several less common usages of the `for` statement sections: assigning a value to an external loop variable in the *initializer* section, invoking a method in both the *initializer* and the *iterator* sections, and changing the values of two variables in the *iterator* section.</span></span> <span data-ttu-id="92e06-140">選取 [執行]\*\*\*\* 執行範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="92e06-140">Select **Run** to run the example code.</span></span> <span data-ttu-id="92e06-141">之後，您可以修改程式碼，然後再次執行它。</span><span class="sxs-lookup"><span data-stu-id="92e06-141">After that you can modify the code and run it again.</span></span>

[!code-csharp-interactive[not typical for loop example](snippets/IterationKeywordsExamples.cs#6)]

<span data-ttu-id="92e06-142">下列範例會定義無限迴圈 `for`：</span><span class="sxs-lookup"><span data-stu-id="92e06-142">The following example defines the infinite `for` loop:</span></span>

[!code-csharp[infinite for loop example](snippets/IterationKeywordsExamples.cs#7)]

## <a name="c-language-specification"></a><span data-ttu-id="92e06-143">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="92e06-143">C# language specification</span></span>

<span data-ttu-id="92e06-144">如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)的 [for 陳述式](~/_csharplang/spec/statements.md#the-for-statement)一節。</span><span class="sxs-lookup"><span data-stu-id="92e06-144">For more information, see [The for statement](~/_csharplang/spec/statements.md#the-for-statement) section of the [C# language specification](/dotnet/csharp/language-reference/language-specification/introduction).</span></span>

## <a name="see-also"></a><span data-ttu-id="92e06-145">另請參閱</span><span class="sxs-lookup"><span data-stu-id="92e06-145">See also</span></span>

- [<span data-ttu-id="92e06-146">C # 參考</span><span class="sxs-lookup"><span data-stu-id="92e06-146">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="92e06-147">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="92e06-147">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="92e06-148">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="92e06-148">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="92e06-149">foreach、in</span><span class="sxs-lookup"><span data-stu-id="92e06-149">foreach, in</span></span>](foreach-in.md)
