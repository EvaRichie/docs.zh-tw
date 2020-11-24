---
title: '成員存取運算子和運算式-c # 參考'
description: 了解可用於存取類型成員的 C# 運算子。
ms.date: 11/13/2020
author: pkulikov
f1_keywords:
- ._CSharpKeyword
- '[]_CSharpKeyword'
- ()_CSharpKeyword
- ^_CSharpKeyword
- .._CSharpKeyword
helpviewer_keywords:
- member access operators [C#]
- member access operator [C#]
- dot operator [C#]
- . operator [C#]
- subscript operator [C#]
- square brackets [] operator [C#]
- indexer operator [C#]
- '[] operator [C#]'
- null-conditional operators [C#]
- Elvis operator [C#]
- ?. operator [C#]
- ?[] operator [C#]
- invocation operator [C#]
- method call [C#]
- method invocation [C#]
- delegate invocation [C#]
- () operator [C#]
- ^ operator [C#]
- index from end operator [C#]
- hat operator [C#]
- .. operator [C#]
- range operator [C#]
ms.openlocfilehash: 28d3d9c3261f1a852d16f2637309b21412611c10
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95691236"
---
# <a name="member-access-operators-and-expressions-c-reference"></a><span data-ttu-id="b284a-103">成員存取運算子和運算式 (c # 參考) </span><span class="sxs-lookup"><span data-stu-id="b284a-103">Member access operators and expressions (C# reference)</span></span>

<span data-ttu-id="b284a-104">當您存取型別成員時，可以使用下列運算子和運算式：</span><span class="sxs-lookup"><span data-stu-id="b284a-104">You can use the following operators and expressions when you access a type member:</span></span>

- <span data-ttu-id="b284a-105">[ `.` (成員存取) ](#member-access-expression-)：存取命名空間或類型的成員</span><span class="sxs-lookup"><span data-stu-id="b284a-105">[`.` (member access)](#member-access-expression-): to access a member of a namespace or a type</span></span>
- <span data-ttu-id="b284a-106">[ `[]` (陣列元素或索引子存取) ](#indexer-operator-)：用以存取陣列元素或型別索引子</span><span class="sxs-lookup"><span data-stu-id="b284a-106">[`[]` (array element or indexer access)](#indexer-operator-): to access an array element or a type indexer</span></span>
- <span data-ttu-id="b284a-107">[ `?.` 和 `?[]` (null 條件運算子) ](#null-conditional-operators--and-)：只有在運算元為非 null 時，才執行成員或元素存取作業</span><span class="sxs-lookup"><span data-stu-id="b284a-107">[`?.` and `?[]` (null-conditional operators)](#null-conditional-operators--and-): to perform a member or element access operation only if an operand is non-null</span></span>
- <span data-ttu-id="b284a-108">[ `()` (調用) ](#invocation-expression-)：呼叫存取的方法或叫用委派</span><span class="sxs-lookup"><span data-stu-id="b284a-108">[`()` (invocation)](#invocation-expression-): to call an accessed method or invoke a delegate</span></span>
- <span data-ttu-id="b284a-109">[ `^` 從 end)  (索引](#index-from-end-operator-)：指出元素位置是從序列的結尾處</span><span class="sxs-lookup"><span data-stu-id="b284a-109">[`^` (index from end)](#index-from-end-operator-): to indicate that the element position is from the end of a sequence</span></span>
- <span data-ttu-id="b284a-110">[ `..` (範圍) ](#range-operator-)：指定可供您用來取得 sequence 元素範圍的索引範圍</span><span class="sxs-lookup"><span data-stu-id="b284a-110">[`..` (range)](#range-operator-): to specify a range of indices that you can use to obtain a range of sequence elements</span></span>

## <a name="member-access-expression-"></a><span data-ttu-id="b284a-111">成員存取運算式。</span><span class="sxs-lookup"><span data-stu-id="b284a-111">Member access expression .</span></span>

<span data-ttu-id="b284a-112">您會使用 `.` 語彙基元來存取命名空間或類型的成員，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b284a-112">You use the `.` token to access a member of a namespace or a type, as the following examples demonstrate:</span></span>

- <span data-ttu-id="b284a-113">用 `.` 來存取命名空間內的嵌套命名空間，如下列指示[ `using` 詞的](../keywords/using-directive.md)範例所示：</span><span class="sxs-lookup"><span data-stu-id="b284a-113">Use `.` to access a nested namespace within a namespace, as the following example of a [`using` directive](../keywords/using-directive.md) shows:</span></span>

  [!code-csharp[nested namespaces](snippets/shared/MemberAccessOperators.cs#NestedNamespace)]

- <span data-ttu-id="b284a-114">使用 `.` 來形成「限定名稱」以存取命名空間內的類型，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="b284a-114">Use `.` to form a *qualified name* to access a type within a namespace, as the following code shows:</span></span>

  [!code-csharp[qualified name](snippets/shared/MemberAccessOperators.cs#QualifiedName)]

  <span data-ttu-id="b284a-115">使用指示[ `using` 詞，讓](../keywords/using-directive.md)限定名稱的使用為選擇性。</span><span class="sxs-lookup"><span data-stu-id="b284a-115">Use a [`using` directive](../keywords/using-directive.md) to make the use of qualified names optional.</span></span>

- <span data-ttu-id="b284a-116">使用 `.` 來存取[類型成員](../../programming-guide/classes-and-structs/index.md#members) (靜態及非靜態)，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="b284a-116">Use `.` to access [type members](../../programming-guide/classes-and-structs/index.md#members), static and non-static, as the following code shows:</span></span>

  [!code-csharp-interactive[type members](snippets/shared/MemberAccessOperators.cs#TypeMemberAccess)]

<span data-ttu-id="b284a-117">您也可以使用 `.` 來存取[擴充方法](../../programming-guide/classes-and-structs/extension-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="b284a-117">You can also use `.` to access an [extension method](../../programming-guide/classes-and-structs/extension-methods.md).</span></span>

## <a name="indexer-operator-"></a><span data-ttu-id="b284a-118">索引子運算子 []</span><span class="sxs-lookup"><span data-stu-id="b284a-118">Indexer operator []</span></span>

<span data-ttu-id="b284a-119">中括弧 (`[]`) 通常用於陣列、索引子或指標元素存取。</span><span class="sxs-lookup"><span data-stu-id="b284a-119">Square brackets, `[]`, are typically used for array, indexer, or pointer element access.</span></span>

### <a name="array-access"></a><span data-ttu-id="b284a-120">陣列存取</span><span class="sxs-lookup"><span data-stu-id="b284a-120">Array access</span></span>

<span data-ttu-id="b284a-121">以下範例將示範如何存取陣列元素：</span><span class="sxs-lookup"><span data-stu-id="b284a-121">The following example demonstrates how to access array elements:</span></span>

[!code-csharp-interactive[array access](snippets/shared/MemberAccessOperators.cs#Arrays)]

<span data-ttu-id="b284a-122">如果陣列索引超出陣列的對應維度界限，就會擲回 <xref:System.IndexOutOfRangeException>。</span><span class="sxs-lookup"><span data-stu-id="b284a-122">If an array index is outside the bounds of the corresponding dimension of an array, an <xref:System.IndexOutOfRangeException> is thrown.</span></span>

<span data-ttu-id="b284a-123">如上述範例所示，您也會在宣告陣列類型或將陣列執行個體具現化時使用方括弧。</span><span class="sxs-lookup"><span data-stu-id="b284a-123">As the preceding example shows, you also use square brackets when you declare an array type or instantiate an array instance.</span></span>

<span data-ttu-id="b284a-124">如需陣列的詳細資訊，請參閱[陣列](../../programming-guide/arrays/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b284a-124">For more information about arrays, see [Arrays](../../programming-guide/arrays/index.md).</span></span>

### <a name="indexer-access"></a><span data-ttu-id="b284a-125">索引子存取</span><span class="sxs-lookup"><span data-stu-id="b284a-125">Indexer access</span></span>

<span data-ttu-id="b284a-126">下列範例會使用 .NET <xref:System.Collections.Generic.Dictionary%602> 型別來示範索引子存取：</span><span class="sxs-lookup"><span data-stu-id="b284a-126">The following example uses the .NET <xref:System.Collections.Generic.Dictionary%602> type to demonstrate indexer access:</span></span>

[!code-csharp-interactive[indexer access](snippets/shared/MemberAccessOperators.cs#Indexers)]

<span data-ttu-id="b284a-127">索引子可讓您透過與陣列編製索引類似的方式，為使用者定義型別的執行個體編製索引。</span><span class="sxs-lookup"><span data-stu-id="b284a-127">Indexers allow you to index instances of a user-defined type in the similar way as array indexing.</span></span> <span data-ttu-id="b284a-128">不同于陣列索引（必須為整數），索引子參數可以宣告為任何類型。</span><span class="sxs-lookup"><span data-stu-id="b284a-128">Unlike array indices, which must be integer, the indexer parameters can be declared to be of any type.</span></span>

<span data-ttu-id="b284a-129">如需索引子的詳細資訊，請參閱[索引子](../../programming-guide/indexers/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b284a-129">For more information about indexers, see [Indexers](../../programming-guide/indexers/index.md).</span></span>

### <a name="other-usages-of-"></a><span data-ttu-id="b284a-130">[] 的其他用法</span><span class="sxs-lookup"><span data-stu-id="b284a-130">Other usages of []</span></span>

<span data-ttu-id="b284a-131">如需有關指標元素存取的相關資訊，請參閱[指標相關運算子](pointer-related-operators.md)一文的[指標元素存取運算子 []](pointer-related-operators.md#pointer-element-access-operator-) 一節。</span><span class="sxs-lookup"><span data-stu-id="b284a-131">For information about pointer element access, see the [Pointer element access operator []](pointer-related-operators.md#pointer-element-access-operator-) section of the [Pointer related operators](pointer-related-operators.md) article.</span></span>

<span data-ttu-id="b284a-132">您也可以使用中括弧來指定[屬性](../../programming-guide/concepts/attributes/index.md)：</span><span class="sxs-lookup"><span data-stu-id="b284a-132">You also use square brackets to specify [attributes](../../programming-guide/concepts/attributes/index.md):</span></span>

```csharp
[System.Diagnostics.Conditional("DEBUG")]
void TraceMethod() {}
```

## <a name="null-conditional-operators--and-"></a><span data-ttu-id="b284a-133">Null 條件運算子 ?.</span><span class="sxs-lookup"><span data-stu-id="b284a-133">Null-conditional operators ?.</span></span> <span data-ttu-id="b284a-134">和 ?[]</span><span class="sxs-lookup"><span data-stu-id="b284a-134">and ?[]</span></span>

<span data-ttu-id="b284a-135">在 c # 6 和更新版本中提供，null 條件運算子[member access](#member-access-expression-) `?.` 只會在運算元評估為非 null 的情況下，將成員存取、或專案[存取權](#indexer-operator-)套用 `?[]` 至其運算元，否則會傳回 `null` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-135">Available in C# 6 and later, a null-conditional operator applies a [member access](#member-access-expression-), `?.`, or [element access](#indexer-operator-), `?[]`, operation to its operand only if that operand evaluates to non-null; otherwise, it returns `null`.</span></span> <span data-ttu-id="b284a-136">那是</span><span class="sxs-lookup"><span data-stu-id="b284a-136">That is,</span></span>

- <span data-ttu-id="b284a-137">如果 `a` 評估為 `null` ，則或的 `a?.x` 結果 `a?[x]` 為 `null` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-137">If `a` evaluates to `null`, the result of `a?.x` or `a?[x]` is `null`.</span></span>
- <span data-ttu-id="b284a-138">如果 `a` 評估為非 null，或的結果 `a?.x` `a?[x]` 會分別與或的結果相同 `a.x` `a[x]` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-138">If `a` evaluates to non-null, the result of `a?.x` or `a?[x]` is the same as the result of `a.x` or `a[x]`, respectively.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b284a-139">如果 `a.x` 或 `a[x]` 擲回例外狀況， `a?.x` 或 `a?[x]` 針對非 null 擲回相同的例外狀況 `a` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-139">If `a.x` or `a[x]` throws an exception, `a?.x` or `a?[x]` would throw the same exception for non-null `a`.</span></span> <span data-ttu-id="b284a-140">例如，如果 `a` 是非 null 的陣列實例，且超出 `x` 的範圍 `a` ，則 `a?[x]` 會擲回 <xref:System.IndexOutOfRangeException> 。</span><span class="sxs-lookup"><span data-stu-id="b284a-140">For example, if `a` is a non-null array instance and `x` is outside the bounds of `a`, `a?[x]` would throw an <xref:System.IndexOutOfRangeException>.</span></span>

<span data-ttu-id="b284a-141">Null 條件運算子會執行最少運算。</span><span class="sxs-lookup"><span data-stu-id="b284a-141">The null-conditional operators are short-circuiting.</span></span> <span data-ttu-id="b284a-142">換句話說，如果條件式成員或項目存取作業鏈結中的一個作業傳回 `null`，則鏈結的其餘部分不會執行。</span><span class="sxs-lookup"><span data-stu-id="b284a-142">That is, if one operation in a chain of conditional member or element access operations returns `null`, the rest of the chain doesn't execute.</span></span> <span data-ttu-id="b284a-143">在下列範例中，如果 `A` 評估為 `null`，則不會評估 `B`；如果 `A` 或 `B` 評估為 `null`，則不會評估 `C`：</span><span class="sxs-lookup"><span data-stu-id="b284a-143">In the following example, `B` is not evaluated if `A` evaluates to `null` and `C` is not evaluated if `A` or `B` evaluates to `null`:</span></span>

```csharp
A?.B?.Do(C);
A?.B?[C];
```

<span data-ttu-id="b284a-144">下列範例示範 `?.` 和 `?[]` 運算子的用法：</span><span class="sxs-lookup"><span data-stu-id="b284a-144">The following example demonstrates the usage of the `?.` and `?[]` operators:</span></span>

[!code-csharp-interactive[null-conditional operators](snippets/shared/MemberAccessOperators.cs#NullConditional)]

<span data-ttu-id="b284a-145">上述範例也會使用[null 聯合運算子 `??` ](null-coalescing-operator.md)來指定替代運算式，以在 null 條件運算的結果為時進行評估 `null` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-145">The preceding example also uses the [null-coalescing operator `??`](null-coalescing-operator.md) to specify an alternative expression to evaluate in case the result of a null-conditional operation is `null`.</span></span>

<span data-ttu-id="b284a-146">如果 `a.x` 或 `a[x]` 為不可為 null 的實值型別 `T` ， `a?.x` 或 `a?[x]` 為對應的 [可為 null 實值型](../builtin-types/nullable-value-types.md)別 `T?` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-146">If `a.x` or `a[x]` is of a non-nullable value type `T`, `a?.x` or `a?[x]` is of the corresponding [nullable value type](../builtin-types/nullable-value-types.md) `T?`.</span></span> <span data-ttu-id="b284a-147">如果您需要類型的運算式 `T` ，請將 null 聯合運算子套用 `??` 至 null 條件運算式，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b284a-147">If you need an expression of type `T`, apply the null-coalescing operator `??` to a null-conditional expression, as the following example shows:</span></span>

[!code-csharp-interactive[null-conditional with null-coalescing](snippets/shared/MemberAccessOperators.cs#NullConditionalWithNullCoalescing)]

<span data-ttu-id="b284a-148">在上述範例中，如果您未使用 `??` 運算子，則 `numbers?.Length < 2` 會在 `false` 是時評估為 `numbers` `null` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-148">In the preceding example, if you don't use the `??` operator, `numbers?.Length < 2` evaluates to `false` when `numbers` is `null`.</span></span>

<span data-ttu-id="b284a-149">Null 條件成員存取運算子 `?.` 也被稱為 Elvis 運算子。</span><span class="sxs-lookup"><span data-stu-id="b284a-149">The null-conditional member access operator `?.` is also known as the Elvis operator.</span></span>

### <a name="thread-safe-delegate-invocation"></a><span data-ttu-id="b284a-150">安全執行緒委派引動流程</span><span class="sxs-lookup"><span data-stu-id="b284a-150">Thread-safe delegate invocation</span></span>

<span data-ttu-id="b284a-151">使用 `?.` 運算子來檢查委派是否為非 Null，然後以安全執行緒方式叫用它 (例如當您[引發事件](../../../standard/events/how-to-raise-and-consume-events.md)時)，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="b284a-151">Use the `?.` operator to check if a delegate is non-null and invoke it in a thread-safe way (for example, when you [raise an event](../../../standard/events/how-to-raise-and-consume-events.md)), as the following code shows:</span></span>

```csharp
PropertyChanged?.Invoke(…)
```

<span data-ttu-id="b284a-152">該程式碼等同於您用於 C# 5 或舊版的下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="b284a-152">That code is equivalent to the following code that you would use in C# 5 or earlier:</span></span>

```csharp
var handler = this.PropertyChanged;
if (handler != null)
{
    handler(…);
}
```

<span data-ttu-id="b284a-153">這是一種安全線程的方法，可確保只叫用非 null `handler` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-153">That is a thread-safe way to ensure that only a non-null `handler` is invoked.</span></span> <span data-ttu-id="b284a-154">因為委派實例是不可變的，所以沒有任何執行緒可以變更本機變數參考的物件 `handler` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-154">Because delegate instances are immutable, no thread can change the object referenced by the `handler` local variable.</span></span> <span data-ttu-id="b284a-155">尤其是，如果另一個執行緒執行的程式碼從事件取消訂閱，並在叫用 `PropertyChanged` `PropertyChanged` `null` 之前變成 `handler` ，則參考的物件會 `handler` 保持不受影響。</span><span class="sxs-lookup"><span data-stu-id="b284a-155">In particular, if the code executed by another thread unsubscribes from the `PropertyChanged` event and `PropertyChanged` becomes `null` before `handler` is invoked, the object referenced by `handler` remains unaffected.</span></span> <span data-ttu-id="b284a-156">`?.`運算子會評估其左邊運算元不超過一次，以保證在 `null` 驗證為非 null 之後，無法將其變更為。</span><span class="sxs-lookup"><span data-stu-id="b284a-156">The `?.` operator evaluates its left-hand operand no more than once, guaranteeing that it cannot be changed to `null` after being verified as non-null.</span></span>

## <a name="invocation-expression-"></a><span data-ttu-id="b284a-157">調用運算式 ( # A1</span><span class="sxs-lookup"><span data-stu-id="b284a-157">Invocation expression ()</span></span>

<span data-ttu-id="b284a-158">使用括弧 `()` 來呼叫[方法](../../programming-guide/classes-and-structs/methods.md)或叫用[委派](../../programming-guide/delegates/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b284a-158">Use parentheses, `()`, to call a [method](../../programming-guide/classes-and-structs/methods.md) or invoke a [delegate](../../programming-guide/delegates/index.md).</span></span>

<span data-ttu-id="b284a-159">下列範例示範如何呼叫方法 (使用或不使用引數)，以及叫用委派：</span><span class="sxs-lookup"><span data-stu-id="b284a-159">The following example demonstrates how to call a method, with or without arguments, and invoke a delegate:</span></span>

[!code-csharp-interactive[invocation with ()](snippets/shared/MemberAccessOperators.cs#Invocation)]

<span data-ttu-id="b284a-160">當您使用 [`new`](new-operator.md) 運算子叫用[建構函式](../../programming-guide/classes-and-structs/constructors.md)時，您也會使用括號。</span><span class="sxs-lookup"><span data-stu-id="b284a-160">You also use parentheses when you invoke a [constructor](../../programming-guide/classes-and-structs/constructors.md) with the [`new`](new-operator.md) operator.</span></span>

### <a name="other-usages-of-"></a><span data-ttu-id="b284a-161">() 的其他用法</span><span class="sxs-lookup"><span data-stu-id="b284a-161">Other usages of ()</span></span>

<span data-ttu-id="b284a-162">您也可以使用括弧來調整評估運算式中作業的順序。</span><span class="sxs-lookup"><span data-stu-id="b284a-162">You also use parentheses to adjust the order in which to evaluate operations in an expression.</span></span> <span data-ttu-id="b284a-163">如需詳細資訊，請參閱 [C# 運算子](index.md)。</span><span class="sxs-lookup"><span data-stu-id="b284a-163">For more information, see [C# operators](index.md).</span></span>

<span data-ttu-id="b284a-164">[Cast 運算式](type-testing-and-cast.md#cast-expression) \(其能執行明確類型轉換\) 也會使用括號。</span><span class="sxs-lookup"><span data-stu-id="b284a-164">[Cast expressions](type-testing-and-cast.md#cast-expression), which perform explicit type conversions, also use parentheses.</span></span>

## <a name="index-from-end-operator-"></a><span data-ttu-id="b284a-165">End 運算子 ^ 的索引</span><span class="sxs-lookup"><span data-stu-id="b284a-165">Index from end operator ^</span></span>

<span data-ttu-id="b284a-166">在 c # 8.0 和更新版本中提供， `^` 運算子表示從序列結尾開始的元素位置。</span><span class="sxs-lookup"><span data-stu-id="b284a-166">Available in C# 8.0 and later, the `^` operator indicates the element position from the end of a sequence.</span></span> <span data-ttu-id="b284a-167">針對長度的序列 `length` ， `^n` 指向具有 `length - n` 從序列開頭位移的元素。</span><span class="sxs-lookup"><span data-stu-id="b284a-167">For a sequence of length `length`, `^n` points to the element with offset `length - n` from the start of a sequence.</span></span> <span data-ttu-id="b284a-168">例如， `^1` 指向序列的最後一個元素，並 `^length` 指向序列的第一個專案。</span><span class="sxs-lookup"><span data-stu-id="b284a-168">For example, `^1` points to the last element of a sequence and `^length` points to the first element of a sequence.</span></span>

[!code-csharp[index from end](snippets/shared/MemberAccessOperators.cs#IndexFromEnd)]

<span data-ttu-id="b284a-169">如上一個範例所示，expression 的型別為 `^e` <xref:System.Index?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="b284a-169">As the preceding example shows, expression `^e` is of the <xref:System.Index?displayProperty=nameWithType> type.</span></span> <span data-ttu-id="b284a-170">在運算式中 `^e` ，的結果 `e` 必須可以隱含地轉換成 `int` 。</span><span class="sxs-lookup"><span data-stu-id="b284a-170">In expression `^e`, the result of `e` must be implicitly convertible to `int`.</span></span>

<span data-ttu-id="b284a-171">您也可以搭配使用 `^` 運算子與 [範圍運算子](#range-operator-) 來建立索引的範圍。</span><span class="sxs-lookup"><span data-stu-id="b284a-171">You can also use the `^` operator with the [range operator](#range-operator-) to create a range of indices.</span></span> <span data-ttu-id="b284a-172">如需詳細資訊，請參閱 [索引和範圍](../../tutorials/ranges-indexes.md)。</span><span class="sxs-lookup"><span data-stu-id="b284a-172">For more information, see [Indices and ranges](../../tutorials/ranges-indexes.md).</span></span>

## <a name="range-operator-"></a><span data-ttu-id="b284a-173">範圍運算子。</span><span class="sxs-lookup"><span data-stu-id="b284a-173">Range operator ..</span></span>

<span data-ttu-id="b284a-174">在 c # 8.0 和更新版本中提供， `..` 運算子會指定索引範圍的開頭和結尾作為其運算元。</span><span class="sxs-lookup"><span data-stu-id="b284a-174">Available in C# 8.0 and later, the `..` operator specifies the start and end of a range of indices as its operands.</span></span> <span data-ttu-id="b284a-175">左邊 *運算元是範圍的開頭。*</span><span class="sxs-lookup"><span data-stu-id="b284a-175">The left-hand operand is an *inclusive* start of a range.</span></span> <span data-ttu-id="b284a-176">右邊運算元是範圍的 *專屬* 結尾。</span><span class="sxs-lookup"><span data-stu-id="b284a-176">The right-hand operand is an *exclusive* end of a range.</span></span> <span data-ttu-id="b284a-177">其中一個運算元可以是從序列開頭或結尾的索引，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b284a-177">Either of operands can be an index from the start or from the end of a sequence, as the following example shows:</span></span>

[!code-csharp[range examples](snippets/shared/MemberAccessOperators.cs#Ranges)]

<span data-ttu-id="b284a-178">如上一個範例所示，expression 的型別為 `a..b` <xref:System.Range?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="b284a-178">As the preceding example shows, expression `a..b` is of the <xref:System.Range?displayProperty=nameWithType> type.</span></span> <span data-ttu-id="b284a-179">在 [運算式] 中 `a..b` ， `a` 和的結果 `b` 必須可以隱含地轉換成 `int` 或 <xref:System.Index> 。</span><span class="sxs-lookup"><span data-stu-id="b284a-179">In expression `a..b`, the results of `a` and `b` must be implicitly convertible to `int` or <xref:System.Index>.</span></span>

<span data-ttu-id="b284a-180">您可以省略運算子的任何運算元 `..` 來取得開放式範圍：</span><span class="sxs-lookup"><span data-stu-id="b284a-180">You can omit any of the operands of the `..` operator to obtain an open-ended range:</span></span>

- <span data-ttu-id="b284a-181">`a..` 相當於 `a..^0`</span><span class="sxs-lookup"><span data-stu-id="b284a-181">`a..` is equivalent to `a..^0`</span></span>
- <span data-ttu-id="b284a-182">`..b` 相當於 `0..b`</span><span class="sxs-lookup"><span data-stu-id="b284a-182">`..b` is equivalent to `0..b`</span></span>
- <span data-ttu-id="b284a-183">`..` 相當於 `0..^0`</span><span class="sxs-lookup"><span data-stu-id="b284a-183">`..` is equivalent to `0..^0`</span></span>

[!code-csharp[ranges with omitted operands](snippets/shared/MemberAccessOperators.cs#RangesOptional)]

<span data-ttu-id="b284a-184">如需詳細資訊，請參閱 [索引和範圍](../../tutorials/ranges-indexes.md)。</span><span class="sxs-lookup"><span data-stu-id="b284a-184">For more information, see [Indices and ranges](../../tutorials/ranges-indexes.md).</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="b284a-185">運算子是否可多載</span><span class="sxs-lookup"><span data-stu-id="b284a-185">Operator overloadability</span></span>

<span data-ttu-id="b284a-186">`.`、、 `()` `^` 和 `..` 運算子無法多載。</span><span class="sxs-lookup"><span data-stu-id="b284a-186">The `.`, `()`, `^`, and `..` operators cannot be overloaded.</span></span> <span data-ttu-id="b284a-187">`[]` 運算子也會視為不可多載的運算子。</span><span class="sxs-lookup"><span data-stu-id="b284a-187">The `[]` operator is also considered a non-overloadable operator.</span></span> <span data-ttu-id="b284a-188">請使用[索引子](../../programming-guide/indexers/index.md)以支援使用使用者定義型別編製索引。</span><span class="sxs-lookup"><span data-stu-id="b284a-188">Use [indexers](../../programming-guide/indexers/index.md) to support indexing with user-defined types.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="b284a-189">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="b284a-189">C# language specification</span></span>

<span data-ttu-id="b284a-190">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的下列幾節：</span><span class="sxs-lookup"><span data-stu-id="b284a-190">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="b284a-191">成員存取</span><span class="sxs-lookup"><span data-stu-id="b284a-191">Member access</span></span>](~/_csharplang/spec/expressions.md#member-access)
- [<span data-ttu-id="b284a-192">項目存取</span><span class="sxs-lookup"><span data-stu-id="b284a-192">Element access</span></span>](~/_csharplang/spec/expressions.md#element-access)
- [<span data-ttu-id="b284a-193">Null 條件運算子</span><span class="sxs-lookup"><span data-stu-id="b284a-193">Null-conditional operator</span></span>](~/_csharplang/spec/expressions.md#null-conditional-operator)
- [<span data-ttu-id="b284a-194">引動流程運算式</span><span class="sxs-lookup"><span data-stu-id="b284a-194">Invocation expressions</span></span>](~/_csharplang/spec/expressions.md#invocation-expressions)

<span data-ttu-id="b284a-195">如需有關索引和範圍的詳細資訊，請參閱 [功能提案注意事項](~/_csharplang/proposals/csharp-8.0/ranges.md)。</span><span class="sxs-lookup"><span data-stu-id="b284a-195">For more information about indices and ranges, see the [feature proposal note](~/_csharplang/proposals/csharp-8.0/ranges.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b284a-196">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b284a-196">See also</span></span>

- [<span data-ttu-id="b284a-197">C# 參考資料</span><span class="sxs-lookup"><span data-stu-id="b284a-197">C# reference</span></span>](../index.md)
- [<span data-ttu-id="b284a-198">C# 運算子與運算式</span><span class="sxs-lookup"><span data-stu-id="b284a-198">C# operators and expressions</span></span>](index.md)
- [<span data-ttu-id="b284a-199">?? (Null 聯合運算子)</span><span class="sxs-lookup"><span data-stu-id="b284a-199">?? (null-coalescing operator)</span></span>](null-coalescing-operator.md)
- [<span data-ttu-id="b284a-200">:: 運算子</span><span class="sxs-lookup"><span data-stu-id="b284a-200">:: operator</span></span>](namespace-alias-qualifier.md)
