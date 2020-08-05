---
title: '- 及 -= 運算子 - C# 參考'
ms.date: 05/27/2019
f1_keywords:
- -_CSharpKeyword
- -=_CSharpKeyword
helpviewer_keywords:
- subtraction operator [C#]
- delegate removal [C#]
- '- operator [C#]'
- subtraction assignment operator [C#]
- event unsubscription [C#]
- -= operator [C#]
ms.assetid: 4de7a4fa-c69d-48e6-aff1-3130af970b2d
ms.openlocfilehash: 0475e1be74af0b367785443224cd2e737d2f7301
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87555589"
---
# <a name="--and---operators-c-reference"></a><span data-ttu-id="ce9cf-102">- 及 -= 運算子 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="ce9cf-102">- and -= operators (C# reference)</span></span>

<span data-ttu-id="ce9cf-103">`-` `-=` 內建[整數](../builtin-types/integral-numeric-types.md)和[浮點](../builtin-types/floating-point-numeric-types.md)數數值型別和[委派](../builtin-types/reference-types.md#the-delegate-type)類型都支援和運算子。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-103">The `-` and `-=` operators are supported by the built-in [integral](../builtin-types/integral-numeric-types.md) and [floating-point](../builtin-types/floating-point-numeric-types.md) numeric types and [delegate](../builtin-types/reference-types.md#the-delegate-type) types.</span></span>

<span data-ttu-id="ce9cf-104">如需算術 `-` 運算子的資訊，請參閱[算術運算子](arithmetic-operators.md)一文中的[一元加號和減號運算子](arithmetic-operators.md#unary-plus-and-minus-operators)與[減法運算子 -](arithmetic-operators.md#subtraction-operator--) 章節。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-104">For information about the arithmetic `-` operator, see the [Unary plus and minus operators](arithmetic-operators.md#unary-plus-and-minus-operators) and [Subtraction operator -](arithmetic-operators.md#subtraction-operator--) sections of the [Arithmetic operators](arithmetic-operators.md) article.</span></span>

## <a name="delegate-removal"></a><span data-ttu-id="ce9cf-105">委派移除</span><span class="sxs-lookup"><span data-stu-id="ce9cf-105">Delegate removal</span></span>

<span data-ttu-id="ce9cf-106">針對相同 [delegate](../builtin-types/reference-types.md#the-delegate-type) 型別中的運算元，`-` 運算子會傳回委派執行個體，其計算方式如下：</span><span class="sxs-lookup"><span data-stu-id="ce9cf-106">For operands of the same [delegate](../builtin-types/reference-types.md#the-delegate-type) type, the `-` operator returns a delegate instance that is calculated as follows:</span></span>

- <span data-ttu-id="ce9cf-107">如果兩個運算元都為非 Null，且右邊運算元的引動過程清單是左邊運算元之引動過程清單的適當連續子清單，則作業結果會是新引動過程清單藉由從左邊運算元之引動過程清單來移除右邊運算元的項目所取得。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-107">If both operands are non-null and the invocation list of the right-hand operand is a proper contiguous sublist of the invocation list of the left-hand operand, the result of the operation is a new invocation list that is obtained by removing the right-hand operand's entries from the invocation list of the left-hand operand.</span></span> <span data-ttu-id="ce9cf-108">如果右邊運算元清單與左邊運算元清單中的多個連續子清單相符，則只會移除最右邊的相符子清單。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-108">If the right-hand operand's list matches multiple contiguous sublists in the left-hand operand's list, only the right-most matching sublist is removed.</span></span> <span data-ttu-id="ce9cf-109">如果移除導致空白清單，則結果是 `null`。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-109">If removal results in an empty list, the result is `null`.</span></span>

  [!code-csharp-interactive[delegate removal](snippets/SubtractionOperator.cs#DelegateRemoval)]

- <span data-ttu-id="ce9cf-110">如果右邊運算元的引動過程清單不是左邊運算元之引動過程清單的適當連續子清單，則作業的結果會是左邊運算元。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-110">If the invocation list of the right-hand operand is not a proper contiguous sublist of the invocation list of the left-hand operand, the result of the operation is the left-hand operand.</span></span> <span data-ttu-id="ce9cf-111">例如，移除不屬於多點傳送委派的委派就不會執行任何動作，而且會導致多點傳送委派不變。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-111">For example, removing a delegate that is not part of the multicast delegate does nothing and results in the unchanged multicast delegate.</span></span>

  [!code-csharp-interactive[delegate removal with no effect](snippets/SubtractionOperator.cs#DelegateRemovalNoChange)]

  <span data-ttu-id="ce9cf-112">上述範例也會示範在委派移除期間，系統會比較委派執行個體。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-112">The preceding example also demonstrates that during delegate removal delegate instances are compared.</span></span> <span data-ttu-id="ce9cf-113">例如，從評估相同 [lambda 運算式](../../programming-guide/statements-expressions-operators/lambda-expressions.md)所產生的委派不相等。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-113">For example, delegates that are produced from evaluation of identical [lambda expressions](../../programming-guide/statements-expressions-operators/lambda-expressions.md) are not equal.</span></span> <span data-ttu-id="ce9cf-114">如需有關委派等號比較的詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[委派等號比較運算子](~/_csharplang/spec/expressions.md#delegate-equality-operators)一節。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-114">For more information about delegate equality, see the [Delegate equality operators](~/_csharplang/spec/expressions.md#delegate-equality-operators) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

- <span data-ttu-id="ce9cf-115">如果左邊運算元是 `null`，則作業的結果是 `null`。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-115">If the left-hand operand is `null`, the result of the operation is `null`.</span></span> <span data-ttu-id="ce9cf-116">如果右邊運算元是 `null`，則作業的結果是左邊運算元。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-116">If the right-hand operand is `null`, the result of the operation is the left-hand operand.</span></span>

  [!code-csharp-interactive[delegate removal and null](snippets/SubtractionOperator.cs#DelegateRemovalAndNull)]

<span data-ttu-id="ce9cf-117">若要合併委派，請使用[ `+` 運算子](addition-operator.md#delegate-combination)。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-117">To combine delegates, use the [`+` operator](addition-operator.md#delegate-combination).</span></span>

<span data-ttu-id="ce9cf-118">如需委派型別的詳細資訊，請參閱[委派](../../programming-guide/delegates/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-118">For more information about delegate types, see [Delegates](../../programming-guide/delegates/index.md).</span></span>

## <a name="subtraction-assignment-operator--"></a><span data-ttu-id="ce9cf-119">減法指派運算子 -=</span><span class="sxs-lookup"><span data-stu-id="ce9cf-119">Subtraction assignment operator -=</span></span>

<span data-ttu-id="ce9cf-120">使用 `-=` 運算子的運算式，例如</span><span class="sxs-lookup"><span data-stu-id="ce9cf-120">An expression using the `-=` operator, such as</span></span>

```csharp
x -= y
```

<span data-ttu-id="ce9cf-121">相當於</span><span class="sxs-lookup"><span data-stu-id="ce9cf-121">is equivalent to</span></span>

```csharp
x = x - y
```

<span data-ttu-id="ce9cf-122">但只會評估 `x` 一次。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-122">except that `x` is only evaluated once.</span></span>

<span data-ttu-id="ce9cf-123">下列範例示範 `-=` 運算子的用法：</span><span class="sxs-lookup"><span data-stu-id="ce9cf-123">The following example demonstrates the usage of the `-=` operator:</span></span>

[!code-csharp-interactive[-= examples](snippets/SubtractionOperator.cs#SubtractAndAssign)]

<span data-ttu-id="ce9cf-124">當您取消訂閱[事件](../keywords/event.md)時，您也會使用 `-=` 來指定要移除的事件處理常式方法。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-124">You also use the `-=` operator to specify an event handler method to remove when you unsubscribe from an [event](../keywords/event.md).</span></span> <span data-ttu-id="ce9cf-125">如需詳細資訊，請參閱[如何訂閱及取消訂閱事件](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-125">For more information, see [How to subscribe to and unsubscribe from events](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="ce9cf-126">運算子是否可多載</span><span class="sxs-lookup"><span data-stu-id="ce9cf-126">Operator overloadability</span></span>

<span data-ttu-id="ce9cf-127">使用者定義型別可以[多載](operator-overloading.md)`-` 運算子。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-127">A user-defined type can [overload](operator-overloading.md) the `-` operator.</span></span> <span data-ttu-id="ce9cf-128">多載二元 `-` 運算子時，`-=` 運算子也會隱含地多載。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-128">When a binary `-` operator is overloaded, the `-=` operator is also implicitly overloaded.</span></span> <span data-ttu-id="ce9cf-129">使用者定義型別無法明確地多載 `-=` 運算子。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-129">A user-defined type cannot explicitly overload the `-=` operator.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="ce9cf-130">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="ce9cf-130">C# language specification</span></span>

<span data-ttu-id="ce9cf-131">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[一元減號運算子](~/_csharplang/spec/expressions.md#unary-minus-operator)與[減法運算子](~/_csharplang/spec/expressions.md#subtraction-operator)章節。</span><span class="sxs-lookup"><span data-stu-id="ce9cf-131">For more information, see the [Unary minus operator](~/_csharplang/spec/expressions.md#unary-minus-operator) and [Subtraction operator](~/_csharplang/spec/expressions.md#subtraction-operator) sections of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ce9cf-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ce9cf-132">See also</span></span>

- [<span data-ttu-id="ce9cf-133">C# 參考資料</span><span class="sxs-lookup"><span data-stu-id="ce9cf-133">C# reference</span></span>](../index.md)
- [<span data-ttu-id="ce9cf-134">C# 運算子與運算式</span><span class="sxs-lookup"><span data-stu-id="ce9cf-134">C# operators and expressions</span></span>](index.md)
- [<span data-ttu-id="ce9cf-135">事件</span><span class="sxs-lookup"><span data-stu-id="ce9cf-135">Events</span></span>](../../programming-guide/events/index.md)
- [<span data-ttu-id="ce9cf-136">算術運算子</span><span class="sxs-lookup"><span data-stu-id="ce9cf-136">Arithmetic operators</span></span>](arithmetic-operators.md)
- [<span data-ttu-id="ce9cf-137">+ 和 + = 運算子</span><span class="sxs-lookup"><span data-stu-id="ce9cf-137">+ and += operators</span></span>](addition-operator.md)
