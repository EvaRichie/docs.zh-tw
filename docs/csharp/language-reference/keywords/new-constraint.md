---
description: new 條件約束 - C# 參考
title: new 條件約束 - C# 參考
ms.date: 07/20/2015
helpviewer_keywords:
- new constraint keyword [C#]
ms.assetid: 58850b64-cb97-4136-be50-1f3bc7fc1da9
ms.openlocfilehash: f7b097729fe973aba7b85c48e1b1033aade83080
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89139446"
---
# <a name="new-constraint-c-reference"></a><span data-ttu-id="2c4c3-103">new 條件約束 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="2c4c3-103">new constraint (C# Reference)</span></span>

<span data-ttu-id="2c4c3-104">`new` 條件約束指定泛型類別宣告中的型別引數都必須有公用無參數建構函式。</span><span class="sxs-lookup"><span data-stu-id="2c4c3-104">The `new` constraint specifies that a type argument in a generic class declaration must have a public parameterless constructor.</span></span> <span data-ttu-id="2c4c3-105">若要使用 `new` 條件約束，型別不能為抽象。</span><span class="sxs-lookup"><span data-stu-id="2c4c3-105">To use the `new` constraint, the type cannot be abstract.</span></span>

<span data-ttu-id="2c4c3-106">當泛型類別建立新的型別執行個體時，將 `new` 條件約束套用至型別參數，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="2c4c3-106">Apply the `new` constraint to a type parameter when a generic class creates new instances of the type, as shown in the following example:</span></span>

[!code-csharp[csrefKeywordsOperator#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#5)]

<span data-ttu-id="2c4c3-107">當您使用 `new()` 條件約束與其他條件約束時，它必須是最後一個指定的︰</span><span class="sxs-lookup"><span data-stu-id="2c4c3-107">When you use the `new()` constraint with other constraints, it must be specified last:</span></span>

[!code-csharp[csrefKeywordsOperator#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#6)]

<span data-ttu-id="2c4c3-108">如需詳細資訊，請參閱[型別參數的條件約束](../../programming-guide/generics/constraints-on-type-parameters.md)。</span><span class="sxs-lookup"><span data-stu-id="2c4c3-108">For more information, see [Constraints on Type Parameters](../../programming-guide/generics/constraints-on-type-parameters.md).</span></span>

<span data-ttu-id="2c4c3-109">您也可以使用 `new` 關鍵字來[建立型別的執行個體](../operators/new-operator.md)或作為[成員宣告修飾詞](new-modifier.md)。</span><span class="sxs-lookup"><span data-stu-id="2c4c3-109">You can also use the `new` keyword to [create an instance of a type](../operators/new-operator.md) or as a [member declaration modifier](new-modifier.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="2c4c3-110">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="2c4c3-110">C# language specification</span></span>

<span data-ttu-id="2c4c3-111">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)中的[型別參數條件約束](~/_csharplang/spec/classes.md#type-parameter-constraints)一節。</span><span class="sxs-lookup"><span data-stu-id="2c4c3-111">For more information, see the [Type parameter constraints](~/_csharplang/spec/classes.md#type-parameter-constraints) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2c4c3-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2c4c3-112">See also</span></span>

- [<span data-ttu-id="2c4c3-113">C # 參考</span><span class="sxs-lookup"><span data-stu-id="2c4c3-113">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="2c4c3-114">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="2c4c3-114">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="2c4c3-115">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="2c4c3-115">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="2c4c3-116">泛型</span><span class="sxs-lookup"><span data-stu-id="2c4c3-116">Generics</span></span>](../../programming-guide/generics/index.md)
