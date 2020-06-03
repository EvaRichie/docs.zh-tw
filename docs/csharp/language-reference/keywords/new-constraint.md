---
title: new 條件約束 - C# 參考
ms.date: 07/20/2015
helpviewer_keywords:
- new constraint keyword [C#]
ms.assetid: 58850b64-cb97-4136-be50-1f3bc7fc1da9
ms.openlocfilehash: 6f6d1b663d03dc9b3adf0e7055dcffacc79d83dc
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795335"
---
# <a name="new-constraint-c-reference"></a><span data-ttu-id="1693d-102">new 條件約束 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="1693d-102">new constraint (C# Reference)</span></span>

<span data-ttu-id="1693d-103">`new` 條件約束指定泛型類別宣告中的型別引數都必須有公用無參數建構函式。</span><span class="sxs-lookup"><span data-stu-id="1693d-103">The `new` constraint specifies that a type argument in a generic class declaration must have a public parameterless constructor.</span></span> <span data-ttu-id="1693d-104">若要使用 `new` 條件約束，型別不能為抽象。</span><span class="sxs-lookup"><span data-stu-id="1693d-104">To use the `new` constraint, the type cannot be abstract.</span></span>

<span data-ttu-id="1693d-105">當泛型類別建立新的型別執行個體時，將 `new` 條件約束套用至型別參數，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="1693d-105">Apply the `new` constraint to a type parameter when a generic class creates new instances of the type, as shown in the following example:</span></span>

[!code-csharp[csrefKeywordsOperator#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#5)]

<span data-ttu-id="1693d-106">當您使用 `new()` 條件約束與其他條件約束時，它必須是最後一個指定的︰</span><span class="sxs-lookup"><span data-stu-id="1693d-106">When you use the `new()` constraint with other constraints, it must be specified last:</span></span>

[!code-csharp[csrefKeywordsOperator#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#6)]

<span data-ttu-id="1693d-107">如需詳細資訊，請參閱[型別參數的條件約束](../../programming-guide/generics/constraints-on-type-parameters.md)。</span><span class="sxs-lookup"><span data-stu-id="1693d-107">For more information, see [Constraints on Type Parameters](../../programming-guide/generics/constraints-on-type-parameters.md).</span></span>

<span data-ttu-id="1693d-108">您也可以使用 `new` 關鍵字來[建立型別的執行個體](../operators/new-operator.md)或作為[成員宣告修飾詞](new-modifier.md)。</span><span class="sxs-lookup"><span data-stu-id="1693d-108">You can also use the `new` keyword to [create an instance of a type](../operators/new-operator.md) or as a [member declaration modifier](new-modifier.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="1693d-109">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="1693d-109">C# language specification</span></span>

<span data-ttu-id="1693d-110">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)中的[型別參數條件約束](~/_csharplang/spec/classes.md#type-parameter-constraints)一節。</span><span class="sxs-lookup"><span data-stu-id="1693d-110">For more information, see the [Type parameter constraints](~/_csharplang/spec/classes.md#type-parameter-constraints) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1693d-111">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1693d-111">See also</span></span>

- [<span data-ttu-id="1693d-112">C # 參考</span><span class="sxs-lookup"><span data-stu-id="1693d-112">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="1693d-113">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="1693d-113">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="1693d-114">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="1693d-114">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="1693d-115">泛型</span><span class="sxs-lookup"><span data-stu-id="1693d-115">Generics</span></span>](../../programming-guide/generics/index.md)
