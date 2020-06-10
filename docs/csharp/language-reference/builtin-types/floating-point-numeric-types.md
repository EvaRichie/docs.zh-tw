---
title: 浮點數值型別 - C# 參考
description: '瞭解內建的 c # 浮點類型： float、double 和 decimal'
ms.date: 02/10/2020
f1_keywords:
- float
- float_CSharpKeyword
- double
- double_CSharpKeyword
- decimal_CSharpKeyword
- decimal
helpviewer_keywords:
- floating-point numbers [C#]
- ranges of floating-point types [C#]
- size of floating-point types [C#]
- types [C#], floating-point types
- float keyword [C#]
- floating-point numbers [C#], float keyword
- double data type [C#]
- decimal keyword [C#]
ms.openlocfilehash: a1142d1aa04003ae1942902672cfc7a05edc99c0
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662663"
---
# <a name="floating-point-numeric-types-c-reference"></a><span data-ttu-id="e807b-103">浮點數值型別 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="e807b-103">Floating-point numeric types (C# reference)</span></span>

<span data-ttu-id="e807b-104">*浮點數數值型別*代表實數。</span><span class="sxs-lookup"><span data-stu-id="e807b-104">The *floating-point numeric types* represent real numbers.</span></span> <span data-ttu-id="e807b-105">所有浮點數數值型別都是實[數值型別](value-types.md)。</span><span class="sxs-lookup"><span data-stu-id="e807b-105">All floating-point numeric types are [value types](value-types.md).</span></span> <span data-ttu-id="e807b-106">它們也是[簡單類型](value-types.md#built-in-value-types)，而且可以使用[常](#real-literals)值進行初始化。</span><span class="sxs-lookup"><span data-stu-id="e807b-106">They are also [simple types](value-types.md#built-in-value-types) and can be initialized with [literals](#real-literals).</span></span> <span data-ttu-id="e807b-107">所有浮點數數值型別都支援[算術](../operators/arithmetic-operators.md)、比較和[等號](../operators/equality-operators.md)[比較](../operators/comparison-operators.md)運算子。</span><span class="sxs-lookup"><span data-stu-id="e807b-107">All floating-point numeric types support [arithmetic](../operators/arithmetic-operators.md), [comparison](../operators/comparison-operators.md), and [equality](../operators/equality-operators.md) operators.</span></span>

## <a name="characteristics-of-the-floating-point-types"></a><span data-ttu-id="e807b-108">浮點數型別的特性</span><span class="sxs-lookup"><span data-stu-id="e807b-108">Characteristics of the floating-point types</span></span>

<span data-ttu-id="e807b-109">C# 支援下列預先定義的浮點數型別：</span><span class="sxs-lookup"><span data-stu-id="e807b-109">C# supports the following predefined floating-point types:</span></span>
  
|<span data-ttu-id="e807b-110">C# 型別/關鍵字</span><span class="sxs-lookup"><span data-stu-id="e807b-110">C# type/keyword</span></span>|<span data-ttu-id="e807b-111">大概範圍</span><span class="sxs-lookup"><span data-stu-id="e807b-111">Approximate range</span></span>|<span data-ttu-id="e807b-112">準確率</span><span class="sxs-lookup"><span data-stu-id="e807b-112">Precision</span></span>|<span data-ttu-id="e807b-113">大小</span><span class="sxs-lookup"><span data-stu-id="e807b-113">Size</span></span>|<span data-ttu-id="e807b-114">.NET 類型</span><span class="sxs-lookup"><span data-stu-id="e807b-114">.NET type</span></span>|
|----------|-----------------------|---------------|--------------|--------------|
|`float`|<span data-ttu-id="e807b-115">±1.5 x 10<sup>−45</sup> 到 ±3.4 x 10<sup>38</sup></span><span class="sxs-lookup"><span data-stu-id="e807b-115">±1.5 x 10<sup>−45</sup> to ±3.4 x 10<sup>38</sup></span></span>|<span data-ttu-id="e807b-116">~6-9 位數</span><span class="sxs-lookup"><span data-stu-id="e807b-116">~6-9 digits</span></span>|<span data-ttu-id="e807b-117">4 個位元組</span><span class="sxs-lookup"><span data-stu-id="e807b-117">4 bytes</span></span>|<xref:System.Single?displayProperty=nameWithType>|
|`double`|<span data-ttu-id="e807b-118">±5.0 × 10<sup>−324</sup> 至 ±1.7 × 10<sup>308</sup></span><span class="sxs-lookup"><span data-stu-id="e807b-118">±5.0 × 10<sup>−324</sup> to ±1.7 × 10<sup>308</sup></span></span>|<span data-ttu-id="e807b-119">~15-17 位數</span><span class="sxs-lookup"><span data-stu-id="e807b-119">~15-17 digits</span></span>|<span data-ttu-id="e807b-120">8 個位元組</span><span class="sxs-lookup"><span data-stu-id="e807b-120">8 bytes</span></span>|<xref:System.Double?displayProperty=nameWithType>|
|`decimal`|<span data-ttu-id="e807b-121">±1.0 x 10<sup>-28</sup> 到 ±7.9228 x 10<sup>28</sup></span><span class="sxs-lookup"><span data-stu-id="e807b-121">±1.0 x 10<sup>-28</sup> to ±7.9228 x 10<sup>28</sup></span></span>|<span data-ttu-id="e807b-122">28-29 位數</span><span class="sxs-lookup"><span data-stu-id="e807b-122">28-29 digits</span></span>|<span data-ttu-id="e807b-123">16 個位元組</span><span class="sxs-lookup"><span data-stu-id="e807b-123">16 bytes</span></span>|<xref:System.Decimal?displayProperty=nameWithType>|

<span data-ttu-id="e807b-124">在上表中，最左邊欄中的每個 C# 型別關鍵字，都是相對應 .NET 型別的別名。</span><span class="sxs-lookup"><span data-stu-id="e807b-124">In the preceding table, each C# type keyword from the leftmost column is an alias for the corresponding .NET type.</span></span> <span data-ttu-id="e807b-125">它們是可互換的。</span><span class="sxs-lookup"><span data-stu-id="e807b-125">They are interchangeable.</span></span> <span data-ttu-id="e807b-126">例如，下列宣告會宣告相同型別的變數：</span><span class="sxs-lookup"><span data-stu-id="e807b-126">For example, the following declarations declare variables of the same type:</span></span>

```csharp
double a = 12.3;
System.Double b = 12.3;
```

<span data-ttu-id="e807b-127">每個浮點數型別的預設值都是零 (`0`)。</span><span class="sxs-lookup"><span data-stu-id="e807b-127">The default value of each floating-point type is zero, `0`.</span></span> <span data-ttu-id="e807b-128">每個浮點數型別都有 `MinValue` 與 `MaxValue` 常數，提供該型別的最小與最大有限值。</span><span class="sxs-lookup"><span data-stu-id="e807b-128">Each of the floating-point types has the `MinValue` and `MaxValue` constants that provide the minimum and maximum finite value of that type.</span></span> <span data-ttu-id="e807b-129">`float` 與 `double` 型別也提供表示不是數字和無限值的常數。</span><span class="sxs-lookup"><span data-stu-id="e807b-129">The `float` and `double` types also provide constants that represent not-a-number and infinity values.</span></span> <span data-ttu-id="e807b-130">例如，`double` 型別提供下列常數：<xref:System.Double.NaN?displayProperty=nameWithType>、<xref:System.Double.NegativeInfinity?displayProperty=nameWithType> 與 <xref:System.Double.PositiveInfinity?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="e807b-130">For example, the `double` type provides the following constants: <xref:System.Double.NaN?displayProperty=nameWithType>, <xref:System.Double.NegativeInfinity?displayProperty=nameWithType>, and <xref:System.Double.PositiveInfinity?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="e807b-131">相較於 `float` 與 `double`，因為 `decimal` 型別的精確度較高且範圍較小，所以非常適合財務與金融計算。</span><span class="sxs-lookup"><span data-stu-id="e807b-131">Because the `decimal` type has more precision and a smaller range than both `float` and `double`, it's appropriate for financial and monetary calculations.</span></span>

<span data-ttu-id="e807b-132">您可以在運算式中混合[整數](integral-numeric-types.md)類資料類型和 `float` 和 `double` 類型。</span><span class="sxs-lookup"><span data-stu-id="e807b-132">You can mix [integral](integral-numeric-types.md) types and the `float` and `double` types in an expression.</span></span> <span data-ttu-id="e807b-133">在此情況下，整數類資料類型會隱含地轉換成其中一個浮點類型，並在必要時，將 `float` 類型隱含地轉換成 `double` 。</span><span class="sxs-lookup"><span data-stu-id="e807b-133">In this case, integral types are implicitly converted to one of the floating-point types and, if necessary, the `float` type is implicitly converted to `double`.</span></span> <span data-ttu-id="e807b-134">運算式評估如下：</span><span class="sxs-lookup"><span data-stu-id="e807b-134">The expression is evaluated as follows:</span></span>

- <span data-ttu-id="e807b-135">如果運算式中有 `double` 類型，則運算式會評估為 `double` ，或 [`bool`](bool.md) 在關聯式和相等比較中為。</span><span class="sxs-lookup"><span data-stu-id="e807b-135">If there is `double` type in the expression, the expression evaluates to `double`, or to [`bool`](bool.md) in relational and equality comparisons.</span></span>
- <span data-ttu-id="e807b-136">如果運算式中沒有 `double` 類型，則運算式會評估為 `float` ，或 `bool` 在關聯式和相等比較中為。</span><span class="sxs-lookup"><span data-stu-id="e807b-136">If there is no `double` type in the expression, the expression evaluates to `float`, or to `bool` in relational and equality comparisons.</span></span>

<span data-ttu-id="e807b-137">您也可以在運算式中混合整數類資料類型和 `decimal` 類型。</span><span class="sxs-lookup"><span data-stu-id="e807b-137">You can also mix integral types and the `decimal` type in an expression.</span></span> <span data-ttu-id="e807b-138">在此情況下，整數類資料類型會隱含地轉換成 `decimal` 類型，而運算式會 `decimal` `bool` 在關聯式和相等比較中，評估為，或為。</span><span class="sxs-lookup"><span data-stu-id="e807b-138">In this case, integral types are implicitly converted to the `decimal` type and the expression evaluates to `decimal`, or to `bool` in relational and equality comparisons.</span></span>

<span data-ttu-id="e807b-139">您不能 `decimal` 在運算式中混用類型與 `float` 和 `double` 類型。</span><span class="sxs-lookup"><span data-stu-id="e807b-139">You cannot mix the `decimal` type with the `float` and `double` types in an expression.</span></span> <span data-ttu-id="e807b-140">在此情況下，如果您想要執行算術、比較或相等運算，您必須明確地將運算元從或轉換成 `decimal` 類型，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e807b-140">In this case, if you want to perform arithmetic, comparison, or equality operations, you must explicitly convert the operands either from or to the `decimal` type, as the following example shows:</span></span>

```csharp-interactive
double a = 1.0;
decimal b = 2.1m;
Console.WriteLine(a + (double)b);
Console.WriteLine((decimal)a + b);
```

<span data-ttu-id="e807b-141">您可以使用[標準數值格式字串](../../../standard/base-types/standard-numeric-format-strings.md)或[自訂數值格式字串](../../../standard/base-types/custom-numeric-format-strings.md)，設定浮點數值格式。</span><span class="sxs-lookup"><span data-stu-id="e807b-141">You can use either [standard numeric format strings](../../../standard/base-types/standard-numeric-format-strings.md) or [custom numeric format strings](../../../standard/base-types/custom-numeric-format-strings.md) to format a floating-point value.</span></span>

## <a name="real-literals"></a><span data-ttu-id="e807b-142">實際常值</span><span class="sxs-lookup"><span data-stu-id="e807b-142">Real literals</span></span>

<span data-ttu-id="e807b-143">實際常值的類型取決於其後置詞，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e807b-143">The type of a real literal is determined by its suffix as follows:</span></span>

- <span data-ttu-id="e807b-144">不含尾碼或具有 `d` 或尾碼的常 `D` 值屬於類型`double`</span><span class="sxs-lookup"><span data-stu-id="e807b-144">The literal without suffix or with the `d` or `D` suffix is of type `double`</span></span>
- <span data-ttu-id="e807b-145">具有 `f` 或尾碼的常 `F` 值屬於類型`float`</span><span class="sxs-lookup"><span data-stu-id="e807b-145">The literal with the `f` or `F` suffix is of type `float`</span></span>
- <span data-ttu-id="e807b-146">具有 `m` 或尾碼的常 `M` 值屬於類型`decimal`</span><span class="sxs-lookup"><span data-stu-id="e807b-146">The literal with the `m` or `M` suffix is of type `decimal`</span></span>

<span data-ttu-id="e807b-147">下列程式碼示範每個的範例：</span><span class="sxs-lookup"><span data-stu-id="e807b-147">The following code demonstrates an example of each:</span></span>

```csharp
double d = 3D;
d = 4d;
d = 3.934_001;

float f = 3_000.5F;
f = 5.4f;

decimal myMoney = 3_000.5m;
myMoney = 400.75M;
```

<span data-ttu-id="e807b-148">上述範例也會示範如何使用 `_` 做為*數位分隔符號*，從 c # 7.0 開始支援。</span><span class="sxs-lookup"><span data-stu-id="e807b-148">The preceding example also shows the use of `_` as a *digit separator*, which is supported starting with C# 7.0.</span></span> <span data-ttu-id="e807b-149">您可以使用數位分隔符號搭配所有類型的數值常值。</span><span class="sxs-lookup"><span data-stu-id="e807b-149">You can use the digit separator with all kinds of numeric literals.</span></span>

<span data-ttu-id="e807b-150">您也可以使用科學記號標記法，也就是指定實際常值的指數部分，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="e807b-150">You can also use scientific notation, that is, specify an exponent part of a real literal, as the following example shows:</span></span>

```csharp-interactive
double d = 0.42e2;
Console.WriteLine(d);  // output 42

float f = 134.45E-2f;
Console.WriteLine(f);  // output: 1.3445

decimal m = 1.5E6m;
Console.WriteLine(m);  // output: 1500000
```

## <a name="conversions"></a><span data-ttu-id="e807b-151">轉換</span><span class="sxs-lookup"><span data-stu-id="e807b-151">Conversions</span></span>

<span data-ttu-id="e807b-152">浮點數數值型別之間只有一個隱含轉換：從 `float` 到 `double` 。</span><span class="sxs-lookup"><span data-stu-id="e807b-152">There is only one implicit conversion between floating-point numeric types: from `float` to `double`.</span></span> <span data-ttu-id="e807b-153">不過，您可以使用[明確轉換](../operators/type-testing-and-cast.md#cast-expression)，將任何浮點類型轉換成任何其他浮點類型。</span><span class="sxs-lookup"><span data-stu-id="e807b-153">However, you can convert any floating-point type to any other floating-point type with the [explicit cast](../operators/type-testing-and-cast.md#cast-expression).</span></span> <span data-ttu-id="e807b-154">如需詳細資訊，請參閱[內建數值轉換](numeric-conversions.md)。</span><span class="sxs-lookup"><span data-stu-id="e807b-154">For more information, see [Built-in numeric conversions](numeric-conversions.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="e807b-155">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="e807b-155">C# language specification</span></span>

<span data-ttu-id="e807b-156">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的下列幾節：</span><span class="sxs-lookup"><span data-stu-id="e807b-156">For more information, see the following sections of the [C# language specification](~/_csharplang/spec/introduction.md):</span></span>

- [<span data-ttu-id="e807b-157">浮點類型</span><span class="sxs-lookup"><span data-stu-id="e807b-157">Floating-point types</span></span>](~/_csharplang/spec/types.md#floating-point-types)
- [<span data-ttu-id="e807b-158">Decimal 類型</span><span class="sxs-lookup"><span data-stu-id="e807b-158">The decimal type</span></span>](~/_csharplang/spec/types.md#the-decimal-type)
- [<span data-ttu-id="e807b-159">實際常值</span><span class="sxs-lookup"><span data-stu-id="e807b-159">Real literals</span></span>](~/_csharplang/spec/lexical-structure.md#real-literals)

## <a name="see-also"></a><span data-ttu-id="e807b-160">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e807b-160">See also</span></span>

- [<span data-ttu-id="e807b-161">C# 參考資料</span><span class="sxs-lookup"><span data-stu-id="e807b-161">C# reference</span></span>](../index.md)
- [<span data-ttu-id="e807b-162">實值型別</span><span class="sxs-lookup"><span data-stu-id="e807b-162">Value types</span></span>](value-types.md)
- [<span data-ttu-id="e807b-163">整數型別</span><span class="sxs-lookup"><span data-stu-id="e807b-163">Integral types</span></span>](integral-numeric-types.md)
- [<span data-ttu-id="e807b-164">標準數值格式字串</span><span class="sxs-lookup"><span data-stu-id="e807b-164">Standard numeric format strings</span></span>](../../../standard/base-types/standard-numeric-format-strings.md)
- [<span data-ttu-id="e807b-165">.NET 中的數值</span><span class="sxs-lookup"><span data-stu-id="e807b-165">Numerics in .NET</span></span>](../../../standard/numerics.md)
- <xref:System.Numerics.Complex?displayProperty=nameWithType>
