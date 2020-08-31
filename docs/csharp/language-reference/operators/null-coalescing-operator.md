---
description: '?? 和？？= 運算子-c # 參考'
title: '?? 和？？= 運算子-c # 參考'
ms.date: 09/10/2019
f1_keywords:
- ??_CSharpKeyword
- ??=_CSharpKeyword
helpviewer_keywords:
- null-coalescing operator [C#]
- ?? operator [C#]
- null-coalescing assignment [C#]
- ??= operator [C#]
ms.assetid: 088b1f0d-c1af-4fe1-b4b8-196fd5ea9132
ms.openlocfilehash: 273bc6d3a4c65c09dc600621b435bf0d1baea9e4
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89118282"
---
# <a name="-and--operators-c-reference"></a><span data-ttu-id="4aecf-105">??</span><span class="sxs-lookup"><span data-stu-id="4aecf-105">??</span></span> <span data-ttu-id="4aecf-106">和？？= 運算子 (c # 參考) </span><span class="sxs-lookup"><span data-stu-id="4aecf-106">and ??= operators (C# reference)</span></span>

<span data-ttu-id="4aecf-107">如果 Null 聯合運算子 `??` 不是 `null`，會傳回其左方運算元的值；否則它會評估右方運算元，並傳回其結果。</span><span class="sxs-lookup"><span data-stu-id="4aecf-107">The null-coalescing operator `??` returns the value of its left-hand operand if it isn't `null`; otherwise, it evaluates the right-hand operand and returns its result.</span></span> <span data-ttu-id="4aecf-108">如果左側運算元評估為非 Null，則 `??` 運算子不會評估右側運算元。</span><span class="sxs-lookup"><span data-stu-id="4aecf-108">The `??` operator doesn't evaluate its right-hand operand if the left-hand operand evaluates to non-null.</span></span>

<span data-ttu-id="4aecf-109">在 c # 8.0 和更新版本中提供，null 聯合指派運算子 `??=` 只有在左運算元評估為時，才會將右邊運算元的值指派給左邊的運算元 `null` 。</span><span class="sxs-lookup"><span data-stu-id="4aecf-109">Available in C# 8.0 and later, the null-coalescing assignment operator `??=` assigns the value of its right-hand operand to its left-hand operand only if the left-hand operand evaluates to `null`.</span></span> <span data-ttu-id="4aecf-110">如果左側運算元評估為非 Null，則 `??=` 運算子不會評估右側運算元。</span><span class="sxs-lookup"><span data-stu-id="4aecf-110">The `??=` operator doesn't evaluate its right-hand operand if the left-hand operand evaluates to non-null.</span></span>

[!code-csharp[null-coalescing assignment](snippets/shared/NullCoalescingOperator.cs#Assignment)]

<span data-ttu-id="4aecf-111">運算子的左運算元 `??=` 必須是變數、 [屬性](../../programming-guide/classes-and-structs/properties.md)或 [索引子](../../programming-guide/indexers/index.md) 元素。</span><span class="sxs-lookup"><span data-stu-id="4aecf-111">The left-hand operand of the `??=` operator must be a variable, a [property](../../programming-guide/classes-and-structs/properties.md), or an [indexer](../../programming-guide/indexers/index.md) element.</span></span>

<span data-ttu-id="4aecf-112">在 c # 7.3 及更早版本中，運算子左邊運算元的類型 `??` 必須是 [參考型別](../keywords/reference-types.md) 或 [可為 null 的實值型](../builtin-types/nullable-value-types.md)別。</span><span class="sxs-lookup"><span data-stu-id="4aecf-112">In C# 7.3 and earlier, the type of the left-hand operand of the `??` operator must be either a [reference type](../keywords/reference-types.md) or a [nullable value type](../builtin-types/nullable-value-types.md).</span></span> <span data-ttu-id="4aecf-113">從 c # 8.0 開始，該需求會以下列內容取代：和運算子的左運算元型別 `??` `??=` 不能是不可為 null 的實值型別。</span><span class="sxs-lookup"><span data-stu-id="4aecf-113">Beginning with C# 8.0, that requirement is replaced with the following: the type of the left-hand operand of the `??` and `??=` operators cannot be a non-nullable value type.</span></span> <span data-ttu-id="4aecf-114">尤其是從 c # 8.0 開始，您可以使用 null 聯合運算子搭配不受限制的型別參數：</span><span class="sxs-lookup"><span data-stu-id="4aecf-114">In particular, beginning with C# 8.0, you can use the null-coalescing operators with unconstrained type parameters:</span></span>

[!code-csharp[unconstrained type parameter](snippets/shared/NullCoalescingOperator.cs#UnconstrainedType)]

<span data-ttu-id="4aecf-115">Null 聯合運算子是右向關聯。</span><span class="sxs-lookup"><span data-stu-id="4aecf-115">The null-coalescing operators are right-associative.</span></span> <span data-ttu-id="4aecf-116">也就是說，表單的運算式</span><span class="sxs-lookup"><span data-stu-id="4aecf-116">That is, expressions of the form</span></span>

```csharp
a ?? b ?? c
d ??= e ??= f
```

<span data-ttu-id="4aecf-117">會評估為</span><span class="sxs-lookup"><span data-stu-id="4aecf-117">are evaluated as</span></span>

```csharp
a ?? (b ?? c)
d ??= (e ??= f)
```

## <a name="examples"></a><span data-ttu-id="4aecf-118">範例</span><span class="sxs-lookup"><span data-stu-id="4aecf-118">Examples</span></span>

<span data-ttu-id="4aecf-119">`??`和 `??=` 運算子在下列案例中很有用：</span><span class="sxs-lookup"><span data-stu-id="4aecf-119">The `??` and `??=` operators can be useful in the following scenarios:</span></span>

- <span data-ttu-id="4aecf-120">在具有 [null 條件運算子？. 和？ []](member-access-operators.md#null-conditional-operators--and-)的運算式中，您可以使用 `??` 運算子來提供替代運算式，以便在具有 null 條件運算的運算式結果為時進行評估 `null` ：</span><span class="sxs-lookup"><span data-stu-id="4aecf-120">In expressions with the [null-conditional operators ?. and ?[]](member-access-operators.md#null-conditional-operators--and-), you can use the `??` operator to provide an alternative expression to evaluate in case the result of the expression with null-conditional operations is `null`:</span></span>

  [!code-csharp-interactive[with null-conditional](snippets/shared/NullCoalescingOperator.cs#WithNullConditional)]

- <span data-ttu-id="4aecf-121">當您使用 [可為 null](../builtin-types/nullable-value-types.md) 的實值型別，而且必須提供基礎實值型別的值時，請使用 `??` 運算子來指定要提供的值，以免可為 null 的型別值為 `null` ：</span><span class="sxs-lookup"><span data-stu-id="4aecf-121">When you work with [nullable value types](../builtin-types/nullable-value-types.md) and need to provide a value of an underlying value type, use the `??` operator to specify the value to provide in case a nullable type value is `null`:</span></span>

  [!code-csharp-interactive[with nullable types](snippets/shared/NullCoalescingOperator.cs#WithNullableTypes)]

  <span data-ttu-id="4aecf-122">如果可為 Null 型別的值為 `null` 時要使用的值為基礎實值型別的預設值，請使用 <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="4aecf-122">Use the <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> method if the value to be used when a nullable type value is `null` should be the default value of the underlying value type.</span></span>

- <span data-ttu-id="4aecf-123">從 c # 7.0 開始，您可以使用[ `throw` 運算式](../keywords/throw.md#the-throw-expression)作為運算子的右手運算元， `??` 讓引數檢查程式碼更簡潔：</span><span class="sxs-lookup"><span data-stu-id="4aecf-123">Beginning with C# 7.0, you can use a [`throw` expression](../keywords/throw.md#the-throw-expression) as the right-hand operand of the `??` operator to make the argument-checking code more concise:</span></span>

  [!code-csharp[with throw expression](snippets/shared/NullCoalescingOperator.cs#WithThrowExpression)]

  <span data-ttu-id="4aecf-124">上述範例中也會示範如何使用[運算式主體成員](../../programming-guide/statements-expressions-operators/expression-bodied-members.md)定義屬性。</span><span class="sxs-lookup"><span data-stu-id="4aecf-124">The preceding example also demonstrates how to use [expression-bodied members](../../programming-guide/statements-expressions-operators/expression-bodied-members.md) to define a property.</span></span>

- <span data-ttu-id="4aecf-125">從 c # 8.0 開始，您可以使用 `??=` 運算子取代表單的程式碼</span><span class="sxs-lookup"><span data-stu-id="4aecf-125">Beginning with C# 8.0, you can use the `??=` operator to replace the code of the form</span></span>

  ```csharp
  if (variable is null)
  {
      variable = expression;
  }
  ```

  <span data-ttu-id="4aecf-126">取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="4aecf-126">with the following code:</span></span>

  ```csharp
  variable ??= expression;
  ```

## <a name="operator-overloadability"></a><span data-ttu-id="4aecf-127">運算子是否可多載</span><span class="sxs-lookup"><span data-stu-id="4aecf-127">Operator overloadability</span></span>

<span data-ttu-id="4aecf-128">運算子無法多載 `??` `??=` 。</span><span class="sxs-lookup"><span data-stu-id="4aecf-128">The operators `??` and `??=` cannot be overloaded.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="4aecf-129">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="4aecf-129">C# language specification</span></span>

<span data-ttu-id="4aecf-130">如需運算子的詳細資訊 `??` ，請參閱[c # 語言規格](~/_csharplang/spec/introduction.md)的[null 聯合運算子](~/_csharplang/spec/expressions.md#the-null-coalescing-operator)一節。</span><span class="sxs-lookup"><span data-stu-id="4aecf-130">For more information about the `??` operator, see [The null coalescing operator](~/_csharplang/spec/expressions.md#the-null-coalescing-operator) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

<span data-ttu-id="4aecf-131">如需操作員的詳細資訊 `??=` ，請參閱 [功能提案注意事項](~/_csharplang/proposals/csharp-8.0/null-coalescing-assignment.md)。</span><span class="sxs-lookup"><span data-stu-id="4aecf-131">For more information about the `??=` operator, see the [feature proposal note](~/_csharplang/proposals/csharp-8.0/null-coalescing-assignment.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4aecf-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4aecf-132">See also</span></span>

- [<span data-ttu-id="4aecf-133">C# 參考資料</span><span class="sxs-lookup"><span data-stu-id="4aecf-133">C# reference</span></span>](../index.md)
- [<span data-ttu-id="4aecf-134">C# 運算子與運算式</span><span class="sxs-lookup"><span data-stu-id="4aecf-134">C# operators and expressions</span></span>](index.md)
- <span data-ttu-id="4aecf-135">[?.和？[] 運算子](member-access-operators.md#null-conditional-operators--and-)</span><span class="sxs-lookup"><span data-stu-id="4aecf-135">[?. and ?[] operators](member-access-operators.md#null-conditional-operators--and-)</span></span>
- [<span data-ttu-id="4aecf-136">？：運算子</span><span class="sxs-lookup"><span data-stu-id="4aecf-136">?: operator</span></span>](conditional-operator.md)
