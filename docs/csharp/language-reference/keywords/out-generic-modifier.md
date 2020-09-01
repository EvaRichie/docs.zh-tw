---
description: out 關鍵字 (泛型修飾詞) - C# 參考
title: out 關鍵字 (泛型修飾詞) - C# 參考
ms.date: 07/20/2015
helpviewer_keywords:
- covariance, out keyword [C#]
- out keyword [C#]
ms.assetid: f8c20dec-a8bc-426a-9882-4076b1db1e00
ms.openlocfilehash: 84f3647309c0772f6ae61d3614f8649fe277f153
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89142332"
---
# <a name="out-generic-modifier-c-reference"></a><span data-ttu-id="461d5-103">out (泛型修飾詞) (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="461d5-103">out (generic modifier) (C# Reference)</span></span>

<span data-ttu-id="461d5-104">若為泛型型別參數，`out` 關鍵字會指定型別參數是 Covariant。</span><span class="sxs-lookup"><span data-stu-id="461d5-104">For generic type parameters, the `out` keyword specifies that the type parameter is covariant.</span></span> <span data-ttu-id="461d5-105">您可以在泛型介面及委派中使用 `out` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="461d5-105">You can use the `out` keyword in generic interfaces and delegates.</span></span>

<span data-ttu-id="461d5-106">共變數可讓您使用比泛型參數指定的衍生程度更高的衍生型別。</span><span class="sxs-lookup"><span data-stu-id="461d5-106">Covariance enables you to use a more derived type than that specified by the generic parameter.</span></span> <span data-ttu-id="461d5-107">這可隱含轉換實作 covariant 介面的類別和隱含轉換委派型別。</span><span class="sxs-lookup"><span data-stu-id="461d5-107">This allows for implicit conversion of classes that implement covariant interfaces and implicit conversion of delegate types.</span></span> <span data-ttu-id="461d5-108">參考型別支援共變數和反變數，但實值型別不支援它們。</span><span class="sxs-lookup"><span data-stu-id="461d5-108">Covariance and contravariance are supported for reference types, but they are not supported for value types.</span></span>

<span data-ttu-id="461d5-109">具有 Covariant 型別參數的介面可讓其方法傳回的衍生型別，衍生程度高過型別參數指定的衍生型別。</span><span class="sxs-lookup"><span data-stu-id="461d5-109">An interface that has a covariant type parameter enables its methods to return more derived types than those specified by the type parameter.</span></span> <span data-ttu-id="461d5-110">例如，因為在 .NET Framework 4 的 <xref:System.Collections.Generic.IEnumerable%601> 中，T 類型是 Covariant，所以您可以不使用任何特殊的轉換方法，將 `IEnumerable(Of String)` 類型的物件指派給 `IEnumerable(Of Object)` 類型的物件。</span><span class="sxs-lookup"><span data-stu-id="461d5-110">For example, because in .NET Framework 4, in <xref:System.Collections.Generic.IEnumerable%601>, type T is covariant, you can assign an object of the `IEnumerable(Of String)` type to an object of the `IEnumerable(Of Object)` type without using any special conversion methods.</span></span>

<span data-ttu-id="461d5-111">Covariant 委派可以指派給同型別的另一個委派，但具有衍生程度較大的泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="461d5-111">A covariant delegate can be assigned another delegate of the same type, but with a more derived generic type parameter.</span></span>

<span data-ttu-id="461d5-112">如需詳細資訊，請參閱 [Covariance and Contravariance](../../programming-guide/concepts/covariance-contravariance/index.md) (共變數和反變數 (C# 和 Visual Basic))。</span><span class="sxs-lookup"><span data-stu-id="461d5-112">For more information, see [Covariance and Contravariance](../../programming-guide/concepts/covariance-contravariance/index.md).</span></span>

## <a name="example---covariant-generic-interface"></a><span data-ttu-id="461d5-113">範例 - Covariant 泛型介面</span><span class="sxs-lookup"><span data-stu-id="461d5-113">Example - covariant generic interface</span></span>

<span data-ttu-id="461d5-114">下例會示範如何宣告、擴充及實作 Covariant 泛型介面。</span><span class="sxs-lookup"><span data-stu-id="461d5-114">The following example shows how to declare, extend, and implement a covariant generic interface.</span></span> <span data-ttu-id="461d5-115">它也會示範如何針對實作 Covariant 介面的類別使用隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="461d5-115">It also shows how to use implicit conversion for classes that implement a covariant interface.</span></span>

[!code-csharp[csVarianceKeywords#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csvariancekeywords/cs/program.cs#3)]

<span data-ttu-id="461d5-116">在泛型介面中，型別參數如果滿足下列條件即可宣告為 Covariant︰</span><span class="sxs-lookup"><span data-stu-id="461d5-116">In a generic interface, a type parameter can be declared covariant if it satisfies the following conditions:</span></span>

- <span data-ttu-id="461d5-117">型別參數僅用為介面方法的傳回型別，不用為方法引數的型別。</span><span class="sxs-lookup"><span data-stu-id="461d5-117">The type parameter is used only as a return type of interface methods and not used as a type of method arguments.</span></span>

    > [!NOTE]
    > <span data-ttu-id="461d5-118">這個規則只有一個例外。</span><span class="sxs-lookup"><span data-stu-id="461d5-118">There is one exception to this rule.</span></span> <span data-ttu-id="461d5-119">如果您在 Covariant 介面中以 Contravariant 泛型委派作為方法參數，則可將 Covariant 型別用為此委派的泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="461d5-119">If in a covariant interface you have a contravariant generic delegate as a method parameter, you can use the covariant type as a generic type parameter for this delegate.</span></span> <span data-ttu-id="461d5-120">如需 Covariant 和 Contravariant 泛型委派的詳細資訊，請參閱 [Variance in Delegates](../../programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) (委派中的變異數) 和 [Using Variance for Func and Action Generic Delegates](../../programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md) (針對 Func 與 Action 委派使用變異數)。</span><span class="sxs-lookup"><span data-stu-id="461d5-120">For more information about covariant and contravariant generic delegates, see [Variance in Delegates](../../programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) and [Using Variance for Func and Action Generic Delegates](../../programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md).</span></span>

- <span data-ttu-id="461d5-121">型別參數不是用為介面方法的泛型條件約束。</span><span class="sxs-lookup"><span data-stu-id="461d5-121">The type parameter is not used as a generic constraint for the interface methods.</span></span>

## <a name="example---covariant-generic-delegate"></a><span data-ttu-id="461d5-122">範例 - Covariant 泛型委派</span><span class="sxs-lookup"><span data-stu-id="461d5-122">Example - covariant generic delegate</span></span>

<span data-ttu-id="461d5-123">下例會示範如何宣告、具現化及叫用 Covariant 泛型委派。</span><span class="sxs-lookup"><span data-stu-id="461d5-123">The following example shows how to declare, instantiate, and invoke a covariant generic delegate.</span></span> <span data-ttu-id="461d5-124">它也會顯示如何以隱含方式轉換委派型別。</span><span class="sxs-lookup"><span data-stu-id="461d5-124">It also shows how to implicitly convert delegate types.</span></span>

[!code-csharp[csVarianceKeywords#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csvariancekeywords/cs/program.cs#4)]

<span data-ttu-id="461d5-125">在泛型委派中，如果型別只用為方法傳回型別，不用於方法引數，則可以宣告為 Covariant。</span><span class="sxs-lookup"><span data-stu-id="461d5-125">In a generic delegate, a type can be declared covariant if it is used only as a method return type and not used for method arguments.</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="461d5-126">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="461d5-126">C# language specification</span></span>

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="461d5-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="461d5-127">See also</span></span>

- [<span data-ttu-id="461d5-128">泛型介面中的變異數</span><span class="sxs-lookup"><span data-stu-id="461d5-128">Variance in Generic Interfaces</span></span>](../../programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
- [<span data-ttu-id="461d5-129">in</span><span class="sxs-lookup"><span data-stu-id="461d5-129">in</span></span>](in-generic-modifier.md)
- [<span data-ttu-id="461d5-130">修飾詞</span><span class="sxs-lookup"><span data-stu-id="461d5-130">Modifiers</span></span>](index.md)
