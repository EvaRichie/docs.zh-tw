---
title: 'bool 類型-c # 參考'
ms.date: 11/26/2019
f1_keywords:
- bool
- bool_CSharpKeyword
- "true"
- "false"
- true_CSharpKeyword
- false_CSharpKeyword
helpviewer_keywords:
- bool data type [C#]
- Boolean [C#]
ms.assetid: 551cfe35-2632-4343-af49-33ad12da08e2
ms.openlocfilehash: 4623dc7d6c8c6c437c78aee45f0eeee8a92e3200
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87854876"
---
# <a name="bool-c-reference"></a><span data-ttu-id="debe6-102">bool (c # 參考) </span><span class="sxs-lookup"><span data-stu-id="debe6-102">bool (C# reference)</span></span>

<span data-ttu-id="debe6-103">`bool`類型關鍵字是 .net 結構類型的別名， <xref:System.Boolean?displayProperty=nameWithType> 代表布林值，可以是 `true` 或 `false` 。</span><span class="sxs-lookup"><span data-stu-id="debe6-103">The `bool` type keyword is an alias for the .NET <xref:System.Boolean?displayProperty=nameWithType> structure type that represents a Boolean value, which can be either `true` or `false`.</span></span>

<span data-ttu-id="debe6-104">若要執行具有類型值的邏輯運算 `bool` ，請使用[布林邏輯](../operators/boolean-logical-operators.md)運算子。</span><span class="sxs-lookup"><span data-stu-id="debe6-104">To perform logical operations with values of the `bool` type, use [Boolean logical](../operators/boolean-logical-operators.md) operators.</span></span> <span data-ttu-id="debe6-105">`bool`類型是比較和[等號](../operators/equality-operators.md)[比較](../operators/comparison-operators.md)運算子的結果類型。</span><span class="sxs-lookup"><span data-stu-id="debe6-105">The `bool` type is the result type of [comparison](../operators/comparison-operators.md) and [equality](../operators/equality-operators.md) operators.</span></span> <span data-ttu-id="debe6-106">`bool`運算式可以是[if](../keywords/if-else.md)、 [do](../keywords/do.md)、 [while](../keywords/while.md)和[for](../keywords/for.md)語句中的控制條件運算式，以及[條件運算子 `?:` ](../operators/conditional-operator.md)中的。</span><span class="sxs-lookup"><span data-stu-id="debe6-106">A `bool` expression can be a controlling conditional expression in the [if](../keywords/if-else.md), [do](../keywords/do.md), [while](../keywords/while.md), and [for](../keywords/for.md) statements and in the [conditional operator `?:`](../operators/conditional-operator.md).</span></span>

<span data-ttu-id="debe6-107">此類型的預設值 `bool` 為 `false` 。</span><span class="sxs-lookup"><span data-stu-id="debe6-107">The default value of the `bool` type is `false`.</span></span>

## <a name="literals"></a><span data-ttu-id="debe6-108">常值</span><span class="sxs-lookup"><span data-stu-id="debe6-108">Literals</span></span>

<span data-ttu-id="debe6-109">您可以使用 `true` 和 `false` 常值來初始化 `bool` 變數或傳遞 `bool` 值：</span><span class="sxs-lookup"><span data-stu-id="debe6-109">You can use the `true` and `false` literals to initialize a `bool` variable or to pass a `bool` value:</span></span>

[!code-csharp-interactive[bool literals](snippets/BoolType.cs#Literals)]

## <a name="three-valued-boolean-logic"></a><span data-ttu-id="debe6-110">三值布林邏輯</span><span class="sxs-lookup"><span data-stu-id="debe6-110">Three-valued Boolean logic</span></span>

<span data-ttu-id="debe6-111">`bool?`如果您需要支援三值邏輯（例如，當您使用支援三值布林值類型的資料庫時），請使用可為 null 的類型。</span><span class="sxs-lookup"><span data-stu-id="debe6-111">Use the nullable `bool?` type, if you need to support the three-valued logic, for example, when you work with databases that support a three-valued Boolean type.</span></span> <span data-ttu-id="debe6-112">針對 `bool?` 運算元，預先定義的 `&` 和 `|` 運算子支援三值邏輯。</span><span class="sxs-lookup"><span data-stu-id="debe6-112">For the `bool?` operands, the predefined `&` and `|` operators support the three-valued logic.</span></span> <span data-ttu-id="debe6-113">如需詳細資訊，請參閱[布林邏輯運算子](../operators/boolean-logical-operators.md)一文的[可為 Null 的布林邏輯運算子](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators)一節。</span><span class="sxs-lookup"><span data-stu-id="debe6-113">For more information, see the [Nullable Boolean logical operators](../operators/boolean-logical-operators.md#nullable-boolean-logical-operators) section of the [Boolean logical operators](../operators/boolean-logical-operators.md) article.</span></span>

<span data-ttu-id="debe6-114">如需可為 null 的實數值型別的詳細資訊，請參閱[nullable 實數值型別](nullable-value-types.md)。</span><span class="sxs-lookup"><span data-stu-id="debe6-114">For more information about nullable value types, see [Nullable value types](nullable-value-types.md).</span></span>

## <a name="conversions"></a><span data-ttu-id="debe6-115">轉換</span><span class="sxs-lookup"><span data-stu-id="debe6-115">Conversions</span></span>

<span data-ttu-id="debe6-116">C # 只提供兩個牽涉到 `bool` 類型的轉換。</span><span class="sxs-lookup"><span data-stu-id="debe6-116">C# provides only two conversions that involve the `bool` type.</span></span> <span data-ttu-id="debe6-117">這些是對應的可為 null 型別 `bool?` 和從型別明確轉換的隱含轉換 `bool?` 。</span><span class="sxs-lookup"><span data-stu-id="debe6-117">Those are an implicit conversion to the corresponding nullable `bool?` type and an explicit conversion from the `bool?` type.</span></span> <span data-ttu-id="debe6-118">不過，.NET 提供了其他方法，可讓您用來轉換成或從 `bool` 類型轉換。</span><span class="sxs-lookup"><span data-stu-id="debe6-118">However, .NET provides additional methods that you can use to convert to or from the `bool` type.</span></span> <span data-ttu-id="debe6-119">如需詳細資訊，請參閱 API 參考頁面的[轉換成和引數的布林值](/dotnet/api/system.boolean#converting-to-and-from-boolean-values)一節 <xref:System.Boolean?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="debe6-119">For more information, see the [Converting to and from Boolean values](/dotnet/api/system.boolean#converting-to-and-from-boolean-values) section of the <xref:System.Boolean?displayProperty=nameWithType> API reference page.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="debe6-120">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="debe6-120">C# language specification</span></span>

<span data-ttu-id="debe6-121">如需詳細資訊，請參閱[c # 語言規格](~/_csharplang/spec/introduction.md)的[bool 類型](~/_csharplang/spec/types.md#the-bool-type)一節。</span><span class="sxs-lookup"><span data-stu-id="debe6-121">For more information, see [The bool type](~/_csharplang/spec/types.md#the-bool-type) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="debe6-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="debe6-122">See also</span></span>

- [<span data-ttu-id="debe6-123">C# 參考資料</span><span class="sxs-lookup"><span data-stu-id="debe6-123">C# reference</span></span>](../index.md)
- [<span data-ttu-id="debe6-124">值類型</span><span class="sxs-lookup"><span data-stu-id="debe6-124">Value types</span></span>](value-types.md)
- [<span data-ttu-id="debe6-125">true 和 false 運算子</span><span class="sxs-lookup"><span data-stu-id="debe6-125">true and false operators</span></span>](../operators/true-false-operators.md)
