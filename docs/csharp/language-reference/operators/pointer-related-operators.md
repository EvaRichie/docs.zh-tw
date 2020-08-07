---
title: 指標相關運算子 - C# 參考
description: 了解使用指標時您可以使用的 C# 運算子。
ms.date: 05/20/2019
author: pkulikov
f1_keywords:
- ->_CSharpKeyword
helpviewer_keywords:
- pointer related operators [C#]
- address-of operator [C#]
- '& operator [C#]'
- pointer indirection operator [C#]
- dereference operator [C#]
- '* operator [C#]'
- pointer member access operator [C#]
- -> operator [C#]
- pointer element access [C#]
- '[] operator [C#]'
- pointer arithmetic [C#]
- pointer increment [C#]
- pointer decrement [C#]
- pointer comparison [C#]
ms.openlocfilehash: 3728778b31a4b4adc51933e8fdc6287f28e03d83
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87916709"
---
# <a name="pointer-related-operators-c-reference"></a><span data-ttu-id="9f5b4-103">指標相關運算子 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="9f5b4-103">Pointer related operators (C# reference)</span></span>

<span data-ttu-id="9f5b4-104">您可以搭配下列運算子來使用指標：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-104">You can use the following operators to work with pointers:</span></span>

- <span data-ttu-id="9f5b4-105">一元[ `&` () 運算子的位址](#address-of-operator-)：取得變數的位址</span><span class="sxs-lookup"><span data-stu-id="9f5b4-105">Unary [`&` (address-of)](#address-of-operator-) operator: to get the address of a variable</span></span>
- <span data-ttu-id="9f5b4-106">一元[ `*` (指標間接取值) ](#pointer-indirection-operator-)運算子：取得指標所指向的變數</span><span class="sxs-lookup"><span data-stu-id="9f5b4-106">Unary [`*` (pointer indirection)](#pointer-indirection-operator-) operator: to obtain the variable pointed by a pointer</span></span>
- <span data-ttu-id="9f5b4-107">[ `->` (成員存取) ](#pointer-member-access-operator--)和[ `[]` (元素存取) ](#pointer-element-access-operator-)運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-107">The [`->` (member access)](#pointer-member-access-operator--) and [`[]` (element access)](#pointer-element-access-operator-) operators</span></span>
- <span data-ttu-id="9f5b4-108">算術運算子[ `+` 、 `-` 、 `++` 和 `--` ](#pointer-arithmetic-operators)</span><span class="sxs-lookup"><span data-stu-id="9f5b4-108">Arithmetic operators [`+`, `-`, `++`, and `--`](#pointer-arithmetic-operators)</span></span>
- <span data-ttu-id="9f5b4-109">比較運算子[ `==` 、 `!=` 、 `<` 、 `>` 、 `<=` 和 `>=` ](#pointer-comparison-operators)</span><span class="sxs-lookup"><span data-stu-id="9f5b4-109">Comparison operators [`==`, `!=`, `<`, `>`, `<=`, and `>=`](#pointer-comparison-operators)</span></span>

<span data-ttu-id="9f5b4-110">如需指標型別的資訊，請參閱[指標型別](../../programming-guide/unsafe-code-pointers/pointer-types.md)。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-110">For information about pointer types, see [Pointer types](../../programming-guide/unsafe-code-pointers/pointer-types.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9f5b4-111">任何具有指標的作業都需要 [unsafe](../keywords/unsafe.md) 內容。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-111">Any operation with pointers requires an [unsafe](../keywords/unsafe.md) context.</span></span> <span data-ttu-id="9f5b4-112">包含 unsafe 區塊的程式碼必須使用編譯器選項來編譯 [`-unsafe`](../compiler-options/unsafe-compiler-option.md) 。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-112">The code that contains unsafe blocks must be compiled with the [`-unsafe`](../compiler-options/unsafe-compiler-option.md) compiler option.</span></span>

## <a name="address-of-operator-amp"></a><a name="address-of-operator-"></a><span data-ttu-id="9f5b4-113">Address 運算子&amp;</span><span class="sxs-lookup"><span data-stu-id="9f5b4-113">Address-of operator &amp;</span></span>

<span data-ttu-id="9f5b4-114">一元 `&` 運算子會傳回其運算元的位址：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-114">The unary `&` operator returns the address of its operand:</span></span>

[!code-csharp[address of local](snippets/shared/PointerOperators.cs#AddressOf)]

<span data-ttu-id="9f5b4-115">`&` 運算子的運算元必須是固定的變數。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-115">The operand of the `&` operator must be a fixed variable.</span></span> <span data-ttu-id="9f5b4-116">「固定」\*\* 變數是位在不受[記憶體回收行程](../../../standard/garbage-collection/index.md)作業影響之儲存位置的變數。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-116">*Fixed* variables are variables that reside in storage locations that are unaffected by operation of the [garbage collector](../../../standard/garbage-collection/index.md).</span></span> <span data-ttu-id="9f5b4-117">在前述範例中，區域變數 `number` 是固定的變數，因為它位於堆疊上。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-117">In the preceding example, the local variable `number` is a fixed variable, because it resides on the stack.</span></span> <span data-ttu-id="9f5b4-118">會受到記憶體回收行程影響且位在儲存位置的變數 (例如重新配置)，稱為「可移動」\*\* 變數。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-118">Variables that reside in storage locations that can be affected by the garbage collector (for example, relocated) are called *movable* variables.</span></span> <span data-ttu-id="9f5b4-119">物件欄位和陣列元素是可移動變數的範例。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-119">Object fields and array elements are examples of movable variables.</span></span> <span data-ttu-id="9f5b4-120">如果您使用[ `fixed` 語句](../keywords/fixed-statement.md)來 [修正] 或 [釘選]，可以取得可移動變數的位址。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-120">You can get the address of a movable variable if you "fix", or "pin", it with a [`fixed` statement](../keywords/fixed-statement.md).</span></span> <span data-ttu-id="9f5b4-121">取得的位址只在語句區塊內有效 `fixed` 。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-121">The obtained address is valid only inside the block of a `fixed` statement.</span></span> <span data-ttu-id="9f5b4-122">下列範例顯示如何使用 `fixed` 語句和 `&` 運算子：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-122">The following example shows how to use a `fixed` statement and the `&` operator:</span></span>

[!code-csharp[address of fixed](snippets/shared/PointerOperators.cs#AddressOfFixed)]

<span data-ttu-id="9f5b4-123">您無法取得常數或值的位址。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-123">You can't get the address of a constant or a value.</span></span>

<span data-ttu-id="9f5b4-124">如需固定和可移動變數的詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[固定和可移動變數](~/_csharplang/spec/unsafe-code.md#fixed-and-moveable-variables)一節。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-124">For more information about fixed and movable variables, see the [Fixed and moveable variables](~/_csharplang/spec/unsafe-code.md#fixed-and-moveable-variables) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

<span data-ttu-id="9f5b4-125">二元 `&` 運算子會計算其布林運算元的[邏輯 AND](boolean-logical-operators.md#logical-and-operator-)或其整數運算元的[位元邏輯 AND](bitwise-and-shift-operators.md#logical-and-operator-)。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-125">The binary `&` operator computes the [logical AND](boolean-logical-operators.md#logical-and-operator-) of its Boolean operands or the [bitwise logical AND](bitwise-and-shift-operators.md#logical-and-operator-) of its integral operands.</span></span>

## <a name="pointer-indirection-operator-"></a><span data-ttu-id="9f5b4-126">指標間接運算子 \*</span><span class="sxs-lookup"><span data-stu-id="9f5b4-126">Pointer indirection operator \*</span></span>

<span data-ttu-id="9f5b4-127">一元指標間接運算子 `*` 取得其運算元指向的變數。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-127">The unary pointer indirection operator `*` obtains the variable to which its operand points.</span></span> <span data-ttu-id="9f5b4-128">它也稱之為取值運算子。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-128">It's also known as the dereference operator.</span></span> <span data-ttu-id="9f5b4-129">`*` 運算子的運算元必須是指標型別。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-129">The operand of the `*` operator must be of a pointer type.</span></span>

[!code-csharp[pointer indirection](snippets/shared/PointerOperators.cs#PointerIndirection)]

<span data-ttu-id="9f5b4-130">您不能將 `*` 運算子套用至 `void*` 型別的運算式。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-130">You cannot apply the `*` operator to an expression of type `void*`.</span></span>

<span data-ttu-id="9f5b4-131">二元 `*` 運算子會計算其數值運算元的[乘積](arithmetic-operators.md#multiplication-operator-)。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-131">The binary `*` operator computes the [product](arithmetic-operators.md#multiplication-operator-) of its numeric operands.</span></span>

## <a name="pointer-member-access-operator--"></a><span data-ttu-id="9f5b4-132">指標成員存取運算子 -></span><span class="sxs-lookup"><span data-stu-id="9f5b4-132">Pointer member access operator -></span></span>

<span data-ttu-id="9f5b4-133">`->` 運算子結合[指標間接](#pointer-indirection-operator-)和[成員存取](member-access-operators.md#member-access-expression-)。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-133">The `->` operator combines [pointer indirection](#pointer-indirection-operator-) and [member access](member-access-operators.md#member-access-expression-).</span></span> <span data-ttu-id="9f5b4-134">也就是說，如果 `x` 是類型的指標， `T*` 而且 `y` 是類型的可存取成員 `T` ，則為格式的運算式</span><span class="sxs-lookup"><span data-stu-id="9f5b4-134">That is, if `x` is a pointer of type `T*` and `y` is an accessible member of type `T`, an expression of the form</span></span>

```csharp
x->y
```

<span data-ttu-id="9f5b4-135">相當於</span><span class="sxs-lookup"><span data-stu-id="9f5b4-135">is equivalent to</span></span>

```csharp
(*x).y
```

<span data-ttu-id="9f5b4-136">下列範例示範 `->` 運算子的用法：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-136">The following example demonstrates the usage of the `->` operator:</span></span>

[!code-csharp[pointer member access](snippets/shared/PointerOperators.cs#MemberAccess)]

<span data-ttu-id="9f5b4-137">您不能將 `->` 運算子套用至 `void*` 型別的運算式。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-137">You cannot apply the `->` operator to an expression of type `void*`.</span></span>

## <a name="pointer-element-access-operator-"></a><span data-ttu-id="9f5b4-138">指標元素存取運算子 []</span><span class="sxs-lookup"><span data-stu-id="9f5b4-138">Pointer element access operator []</span></span>

<span data-ttu-id="9f5b4-139">針對指標型別的運算式 `p`，`p[n]` 格式的指標元素存取會評估為 `*(p + n)`，其中 `n` 必須是可隱含轉換成 `int`、`uint`、`long` 或 `ulong` 的型別。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-139">For an expression `p` of a pointer type, a pointer element access of the form `p[n]` is evaluated as `*(p + n)`, where `n` must be of a type implicitly convertible to `int`, `uint`, `long`, or `ulong`.</span></span> <span data-ttu-id="9f5b4-140">如需 `+` 運算子搭配指標的行為資訊，請參閱[在指標中加減整數值](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer)一節。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-140">For information about the behavior of the `+` operator with pointers, see the [Addition or subtraction of an integral value to or from a pointer](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) section.</span></span>

<span data-ttu-id="9f5b4-141">下例示範如何使用指標和 `[]` 運算子存取陣列元素：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-141">The following example demonstrates how to access array elements with a pointer and the `[]` operator:</span></span>

[!code-csharp[pointer element access](snippets/shared/PointerOperators.cs#ElementAccess)]

<span data-ttu-id="9f5b4-142">在上述範例中， [ `stackalloc` 運算式](stackalloc.md)會配置堆疊上的記憶體區塊。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-142">In the preceding example, a [`stackalloc` expression](stackalloc.md) allocates a block of memory on the stack.</span></span>

> [!NOTE]
> <span data-ttu-id="9f5b4-143">指標元素存取運算子不會檢查超出範圍的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-143">The pointer element access operator doesn't check for out-of-bounds errors.</span></span>

<span data-ttu-id="9f5b4-144">型別為 `void*` 的運算式，指標元素存取無法使用 `[]`。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-144">You cannot use `[]` for pointer element access with an expression of type `void*`.</span></span>

<span data-ttu-id="9f5b4-145">您也可以使用 `[]` 運算子來進行[陣列元素或索引子存取](member-access-operators.md#indexer-operator-)。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-145">You can also use the `[]` operator for [array element or indexer access](member-access-operators.md#indexer-operator-).</span></span>

## <a name="pointer-arithmetic-operators"></a><span data-ttu-id="9f5b4-146">指標算術運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-146">Pointer arithmetic operators</span></span>

<span data-ttu-id="9f5b4-147">您可以使用指標執行下列算術運算：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-147">You can perform the following arithmetic operations with pointers:</span></span>

- <span data-ttu-id="9f5b4-148">在指標中加減整數值</span><span class="sxs-lookup"><span data-stu-id="9f5b4-148">Add or subtract an integral value to or from a pointer</span></span>
- <span data-ttu-id="9f5b4-149">減去兩個指標</span><span class="sxs-lookup"><span data-stu-id="9f5b4-149">Subtract two pointers</span></span>
- <span data-ttu-id="9f5b4-150">遞增或遞減指標</span><span class="sxs-lookup"><span data-stu-id="9f5b4-150">Increment or decrement a pointer</span></span>

<span data-ttu-id="9f5b4-151">您無法使用 `void*` 型別的指標執行這些運算。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-151">You cannot perform those operations with pointers of type `void*`.</span></span>

<span data-ttu-id="9f5b4-152">如需支援的數值型別算術運算資訊，請參閱[算術運算子](arithmetic-operators.md)。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-152">For information about supported arithmetic operations with numeric types, see [Arithmetic operators](arithmetic-operators.md).</span></span>

### <a name="addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer"></a><span data-ttu-id="9f5b4-153">在指標中加減整數值</span><span class="sxs-lookup"><span data-stu-id="9f5b4-153">Addition or subtraction of an integral value to or from a pointer</span></span>

<span data-ttu-id="9f5b4-154">針對 `T*` 型別的 `p` 指標和可隱含轉換成 `int`、`uint`、`long` 或 `ulong` 的運算式 `n`，加減定義如下：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-154">For a pointer `p` of type `T*` and an expression `n` of a type implicitly convertible to `int`, `uint`, `long`, or `ulong`, addition and subtraction are defined as follows:</span></span>

- <span data-ttu-id="9f5b4-155">`p + n` 和 `n + p` 運算式都會產生因為將 `n * sizeof(T)` 新增到 `p` 指定位址而得到的 `T*` 型別指標。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-155">Both `p + n` and `n + p` expressions produce a pointer of type `T*` that results from adding `n * sizeof(T)` to the address given by `p`.</span></span>
- <span data-ttu-id="9f5b4-156">`p - n` 運算式會產生因為從 `p` 指定的位址減去 `n * sizeof(T)` 而得到的 `T*` 型別指標。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-156">The `p - n` expression produces a pointer of type `T*` that results from subtracting `n * sizeof(T)` from the address given by `p`.</span></span>

<span data-ttu-id="9f5b4-157">[ `sizeof` 運算子](sizeof.md)會取得類型的大小（以位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-157">The [`sizeof` operator](sizeof.md) obtains the size of a type in bytes.</span></span>

<span data-ttu-id="9f5b4-158">下例示範 `+` 運算子加指標的用法：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-158">The following example demonstrates the usage of the `+` operator with a pointer:</span></span>

[!code-csharp[pointer addition](snippets/shared/PointerOperators.cs#AddNumber)]

### <a name="pointer-subtraction"></a><span data-ttu-id="9f5b4-159">指標減法</span><span class="sxs-lookup"><span data-stu-id="9f5b4-159">Pointer subtraction</span></span>

<span data-ttu-id="9f5b4-160">針對 `T*` 型別的兩個指標 `p1` 和 `p2`，運算式 `p1 - p2` 會產生 `p1` 和 `p2` 除以 `sizeof(T)` 所指定的位址間差異。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-160">For two pointers `p1` and `p2` of type `T*`, the expression `p1 - p2` produces the difference between the addresses given by `p1` and `p2` divided by `sizeof(T)`.</span></span> <span data-ttu-id="9f5b4-161">結果的類型是 `long`。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-161">The type of the result is `long`.</span></span> <span data-ttu-id="9f5b4-162">亦即，`p1 - p2` 會計算為 `((long)(p1) - (long)(p2)) / sizeof(T)`。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-162">That is, `p1 - p2` is computed as `((long)(p1) - (long)(p2)) / sizeof(T)`.</span></span>

<span data-ttu-id="9f5b4-163">下例示範指標減法：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-163">The following example demonstrates the pointer subtraction:</span></span>

[!code-csharp[pointer subtraction](snippets/shared/PointerOperators.cs#SubtractPointers)]

### <a name="pointer-increment-and-decrement"></a><span data-ttu-id="9f5b4-164">指標遞增和遞減</span><span class="sxs-lookup"><span data-stu-id="9f5b4-164">Pointer increment and decrement</span></span>

<span data-ttu-id="9f5b4-165">`++` 遞增運算子在其指標運算元中[加](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) 1。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-165">The `++` increment operator [adds](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) 1 to its pointer operand.</span></span> <span data-ttu-id="9f5b4-166">`--` 遞減運算子從其指標運算元中[減](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) 1。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-166">The `--` decrement operator [subtracts](#addition-or-subtraction-of-an-integral-value-to-or-from-a-pointer) 1 from its pointer operand.</span></span>

<span data-ttu-id="9f5b4-167">這兩個運算子都支援兩種形式：後置 (`p++` 和 `p--`) 及前置 (`++p` 和 `--p`)。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-167">Both operators are supported in two forms: postfix (`p++` and `p--`) and prefix (`++p` and `--p`).</span></span> <span data-ttu-id="9f5b4-168">`p++` 和 `p--` 的結果是運算「前」 \*\* 的 `p` 值。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-168">The result of `p++` and `p--` is the value of `p` *before* the operation.</span></span> <span data-ttu-id="9f5b4-169">`++p` 和 `--p` 的結果是運算「後」 \*\* 的 `p` 值。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-169">The result of `++p` and `--p` is the value of `p` *after* the operation.</span></span>

<span data-ttu-id="9f5b4-170">下例示範前置和後置遞增運算子的行為：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-170">The following example demonstrates the behavior of both postfix and prefix increment operators:</span></span>

[!code-csharp[pointer increment](snippets/shared/PointerOperators.cs#Increment)]

## <a name="pointer-comparison-operators"></a><span data-ttu-id="9f5b4-171">指標比較運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-171">Pointer comparison operators</span></span>

<span data-ttu-id="9f5b4-172">您可以使用 `==`、`!=`、`<`、`>`、`<=` 和 `>=` 運算子來比較包括 `void*` 在內之任何指標型別的運算元。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-172">You can use the `==`, `!=`, `<`, `>`, `<=`, and `>=` operators to compare operands of any pointer type, including `void*`.</span></span> <span data-ttu-id="9f5b4-173">這些運算子會比較兩個運算元指定的位址，如同它們是不帶正負號的整數一樣。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-173">Those operators compare the addresses given by the two operands as if they were unsigned integers.</span></span>

<span data-ttu-id="9f5b4-174">如需這些其他型別運算元的運算子行為資訊，請參閱[等號運算子](equality-operators.md)和[比較運算子](comparison-operators.md)文章。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-174">For information about the behavior of those operators for operands of other types, see the [Equality operators](equality-operators.md) and [Comparison operators](comparison-operators.md) articles.</span></span>

## <a name="operator-precedence"></a><span data-ttu-id="9f5b4-175">運算子優先順序</span><span class="sxs-lookup"><span data-stu-id="9f5b4-175">Operator precedence</span></span>

<span data-ttu-id="9f5b4-176">下列清單排列指標相關的運算子，從最高優先順序到最低：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-176">The following list orders pointer related operators starting from the highest precedence to the lowest:</span></span>

- <span data-ttu-id="9f5b4-177">後置遞增 `x++` 和遞減 `x--` 運算子以及 `->` 和 `[]` 運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-177">Postfix increment `x++` and decrement `x--` operators and the `->` and `[]` operators</span></span>
- <span data-ttu-id="9f5b4-178">前置遞增 `++x` 和遞減 `--x` 運算子以及 `&` 和 `*` 運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-178">Prefix increment `++x` and decrement `--x` operators and the `&` and `*` operators</span></span>
- <span data-ttu-id="9f5b4-179">加法類 `+` 和 `-` 運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-179">Additive `+` and `-` operators</span></span>
- <span data-ttu-id="9f5b4-180">比較 `<`、`>`、`<=` 和 `>=` 運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-180">Comparison `<`, `>`, `<=`, and `>=` operators</span></span>
- <span data-ttu-id="9f5b4-181">等號 `==` 和 `!=` 運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-181">Equality `==` and `!=` operators</span></span>

<span data-ttu-id="9f5b4-182">使用括弧 `()` 變更由運算子優先順序強制執行的評估順序。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-182">Use parentheses, `()`, to change the order of evaluation imposed by operator precedence.</span></span>

<span data-ttu-id="9f5b4-183">如需依優先順序層級排序之 c # 運算子的完整清單，請參閱[c # 運算子](index.md)一文的[運算子優先順序](index.md#operator-precedence)一節。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-183">For the complete list of C# operators ordered by precedence level, see the [Operator precedence](index.md#operator-precedence) section of the [C# operators](index.md) article.</span></span>

## <a name="operator-overloadability"></a><span data-ttu-id="9f5b4-184">運算子是否可多載</span><span class="sxs-lookup"><span data-stu-id="9f5b4-184">Operator overloadability</span></span>

<span data-ttu-id="9f5b4-185">使用者定義的型別無法多載指標相關運算子 `&`、`*`、`->` 和 `[]`。</span><span class="sxs-lookup"><span data-stu-id="9f5b4-185">A user-defined type cannot overload the pointer related operators `&`, `*`, `->`, and `[]`.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="9f5b4-186">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="9f5b4-186">C# language specification</span></span>

<span data-ttu-id="9f5b4-187">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的下列幾節：</span><span class="sxs-lookup"><span data-stu-id="9f5b4-187">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="9f5b4-188">固定和可移動變數</span><span class="sxs-lookup"><span data-stu-id="9f5b4-188">Fixed and moveable variables</span></span>](~/_csharplang/spec/unsafe-code.md#fixed-and-moveable-variables)
- [<span data-ttu-id="9f5b4-189">傳址運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-189">The address-of operator</span></span>](~/_csharplang/spec/unsafe-code.md#the-address-of-operator)
- [<span data-ttu-id="9f5b4-190">指標間接</span><span class="sxs-lookup"><span data-stu-id="9f5b4-190">Pointer indirection</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-indirection)
- [<span data-ttu-id="9f5b4-191">指標成員存取</span><span class="sxs-lookup"><span data-stu-id="9f5b4-191">Pointer member access</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-member-access)
- [<span data-ttu-id="9f5b4-192">指標元素存取</span><span class="sxs-lookup"><span data-stu-id="9f5b4-192">Pointer element access</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-element-access)
- [<span data-ttu-id="9f5b4-193">指標算術</span><span class="sxs-lookup"><span data-stu-id="9f5b4-193">Pointer arithmetic</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-arithmetic)
- [<span data-ttu-id="9f5b4-194">指標遞增和遞減</span><span class="sxs-lookup"><span data-stu-id="9f5b4-194">Pointer increment and decrement</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-increment-and-decrement)
- [<span data-ttu-id="9f5b4-195">指標比較</span><span class="sxs-lookup"><span data-stu-id="9f5b4-195">Pointer comparison</span></span>](~/_csharplang/spec/unsafe-code.md#pointer-comparison)

## <a name="see-also"></a><span data-ttu-id="9f5b4-196">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9f5b4-196">See also</span></span>

- [<span data-ttu-id="9f5b4-197">C# 參考資料</span><span class="sxs-lookup"><span data-stu-id="9f5b4-197">C# reference</span></span>](../index.md)
- [<span data-ttu-id="9f5b4-198">C# 運算子與運算式</span><span class="sxs-lookup"><span data-stu-id="9f5b4-198">C# operators and expressions</span></span>](index.md)
- [<span data-ttu-id="9f5b4-199">指標類型</span><span class="sxs-lookup"><span data-stu-id="9f5b4-199">Pointer types</span></span>](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [<span data-ttu-id="9f5b4-200">unsafe 關鍵字</span><span class="sxs-lookup"><span data-stu-id="9f5b4-200">unsafe keyword</span></span>](../keywords/unsafe.md)
- [<span data-ttu-id="9f5b4-201">fixed 關鍵字</span><span class="sxs-lookup"><span data-stu-id="9f5b4-201">fixed keyword</span></span>](../keywords/fixed-statement.md)
- [<span data-ttu-id="9f5b4-202">stackalloc</span><span class="sxs-lookup"><span data-stu-id="9f5b4-202">stackalloc</span></span>](stackalloc.md)
- [<span data-ttu-id="9f5b4-203">sizeof 運算子</span><span class="sxs-lookup"><span data-stu-id="9f5b4-203">sizeof operator</span></span>](sizeof.md)
