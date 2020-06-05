---
title: In (泛型修飾詞)
ms.date: 07/20/2015
f1_keywords:
- vb.VarianceOut
helpviewer_keywords:
- Out keyword [Visual Basic]
- covariance, Out keyword [Visual Basic]
ms.assetid: c4418369-1518-4a46-9a1e-054c61038eca
ms.openlocfilehash: 28ae7d6fd51170aa822072fc2f5357443f51a353
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392089"
---
# <a name="out-generic-modifier-visual-basic"></a><span data-ttu-id="663ac-102">Out (泛型修飾詞) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="663ac-102">Out (Generic Modifier) (Visual Basic)</span></span>

<span data-ttu-id="663ac-103">若為泛型型別參數， `Out` 關鍵字會指定型別為「協變數」。</span><span class="sxs-lookup"><span data-stu-id="663ac-103">For generic type parameters, the `Out` keyword specifies that the type is covariant.</span></span>

## <a name="remarks"></a><span data-ttu-id="663ac-104">備註</span><span class="sxs-lookup"><span data-stu-id="663ac-104">Remarks</span></span>

<span data-ttu-id="663ac-105">共變數可讓您使用比泛型參數指定的衍生程度更高的衍生型別。</span><span class="sxs-lookup"><span data-stu-id="663ac-105">Covariance enables you to use a more derived type than that specified by the generic parameter.</span></span> <span data-ttu-id="663ac-106">這可隱含轉換實作 variant 介面的類別和隱含轉換委派類型。</span><span class="sxs-lookup"><span data-stu-id="663ac-106">This allows for implicit conversion of classes that implement variant interfaces and implicit conversion of delegate types.</span></span>

<span data-ttu-id="663ac-107">如需詳細資訊，請參閱 [Covariance and Contravariance](../../programming-guide/concepts/covariance-contravariance/index.md) (共變數和反變數 (C# 和 Visual Basic))。</span><span class="sxs-lookup"><span data-stu-id="663ac-107">For more information, see [Covariance and Contravariance](../../programming-guide/concepts/covariance-contravariance/index.md).</span></span>

## <a name="rules"></a><span data-ttu-id="663ac-108">規則</span><span class="sxs-lookup"><span data-stu-id="663ac-108">Rules</span></span>

<span data-ttu-id="663ac-109">您可以在泛型介面及委派中使用 `Out` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="663ac-109">You can use the `Out` keyword in generic interfaces and delegates.</span></span>

<span data-ttu-id="663ac-110">在泛型介面中，型別參數如果滿足下列條件即可宣告為 Covariant︰</span><span class="sxs-lookup"><span data-stu-id="663ac-110">In a generic interface, a type parameter can be declared covariant if it satisfies the following conditions:</span></span>

- <span data-ttu-id="663ac-111">型別參數僅用為介面方法的傳回型別，不用為方法引數的型別。</span><span class="sxs-lookup"><span data-stu-id="663ac-111">The type parameter is used only as a return type of interface methods and not used as a type of method arguments.</span></span>

    > [!NOTE]
    > <span data-ttu-id="663ac-112">這個規則只有一個例外。</span><span class="sxs-lookup"><span data-stu-id="663ac-112">There is one exception to this rule.</span></span> <span data-ttu-id="663ac-113">如果您在 Covariant 介面中以 Contravariant 泛型委派作為方法參數，則可將 Covariant 型別用為此委派的泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="663ac-113">If in a covariant interface you have a contravariant generic delegate as a method parameter, you can use the covariant type as a generic type parameter for this delegate.</span></span> <span data-ttu-id="663ac-114">如需 Covariant 和 Contravariant 泛型委派的詳細資訊，請參閱 [Variance in Delegates](../../programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) (委派中的變異數) 和 [Using Variance for Func and Action Generic Delegates](../../programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md) (針對 Func 與 Action 委派使用變異數)。</span><span class="sxs-lookup"><span data-stu-id="663ac-114">For more information about covariant and contravariant generic delegates, see [Variance in Delegates](../../programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) and [Using Variance for Func and Action Generic Delegates](../../programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md).</span></span>

- <span data-ttu-id="663ac-115">型別參數不是用為介面方法的泛型條件約束。</span><span class="sxs-lookup"><span data-stu-id="663ac-115">The type parameter is not used as a generic constraint for the interface methods.</span></span>

<span data-ttu-id="663ac-116">在泛型委派中，如果型別參數僅做為方法傳回型別使用，而不是用於方法引數，則可以宣告為「不可變」。</span><span class="sxs-lookup"><span data-stu-id="663ac-116">In a generic delegate, a type parameter can be declared covariant if it is used only as a method return type and not used for method arguments.</span></span>

<span data-ttu-id="663ac-117">參考型別支援共變數和反變數，但實值型別不支援它們。</span><span class="sxs-lookup"><span data-stu-id="663ac-117">Covariance and contravariance are supported for reference types, but they are not supported for value types.</span></span>

<span data-ttu-id="663ac-118">在 Visual Basic 中，您不能在不指定委派類型的情況下，于協變數介面中宣告事件。</span><span class="sxs-lookup"><span data-stu-id="663ac-118">In Visual Basic, you cannot declare events in covariant interfaces without specifying the delegate type.</span></span> <span data-ttu-id="663ac-119">此外，協變數介面不能有嵌套的類別、列舉或結構，但它們可以有嵌套介面。</span><span class="sxs-lookup"><span data-stu-id="663ac-119">Also, covariant interfaces cannot have nested classes, enums, or structures, but they can have nested interfaces.</span></span>

## <a name="behavior"></a><span data-ttu-id="663ac-120">行為</span><span class="sxs-lookup"><span data-stu-id="663ac-120">Behavior</span></span>

<span data-ttu-id="663ac-121">具有 Covariant 型別參數的介面可讓其方法傳回的衍生型別，衍生程度高過型別參數指定的衍生型別。</span><span class="sxs-lookup"><span data-stu-id="663ac-121">An interface that has a covariant type parameter enables its methods to return more derived types than those specified by the type parameter.</span></span> <span data-ttu-id="663ac-122">例如，因為在 .NET Framework 4 的 <xref:System.Collections.Generic.IEnumerable%601> 中，T 類型是 Covariant，所以您可以不使用任何特殊的轉換方法，將 `IEnumerable(Of String)` 類型的物件指派給 `IEnumerable(Of Object)` 類型的物件。</span><span class="sxs-lookup"><span data-stu-id="663ac-122">For example, because in .NET Framework 4, in <xref:System.Collections.Generic.IEnumerable%601>, type T is covariant, you can assign an object of the `IEnumerable(Of String)` type to an object of the `IEnumerable(Of Object)` type without using any special conversion methods.</span></span>

<span data-ttu-id="663ac-123">Covariant 委派可以指派給同型別的另一個委派，但具有衍生程度較大的泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="663ac-123">A covariant delegate can be assigned another delegate of the same type, but with a more derived generic type parameter.</span></span>

## <a name="example"></a><span data-ttu-id="663ac-124">範例</span><span class="sxs-lookup"><span data-stu-id="663ac-124">Example</span></span>

<span data-ttu-id="663ac-125">下例會示範如何宣告、擴充及實作 Covariant 泛型介面。</span><span class="sxs-lookup"><span data-stu-id="663ac-125">The following example shows how to declare, extend, and implement a covariant generic interface.</span></span> <span data-ttu-id="663ac-126">它也會示範如何針對實作 Covariant 介面的類別使用隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="663ac-126">It also shows how to use implicit conversion for classes that implement a covariant interface.</span></span>

[!code-vb[vbVarianceKeywords#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvariancekeywords/vb/module1.vb#3)]

## <a name="example"></a><span data-ttu-id="663ac-127">範例</span><span class="sxs-lookup"><span data-stu-id="663ac-127">Example</span></span>

<span data-ttu-id="663ac-128">下例會示範如何宣告、具現化及叫用 Covariant 泛型委派。</span><span class="sxs-lookup"><span data-stu-id="663ac-128">The following example shows how to declare, instantiate, and invoke a covariant generic delegate.</span></span> <span data-ttu-id="663ac-129">它也會說明如何使用委派類型的隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="663ac-129">It also shows how you can use implicit conversion for delegate types.</span></span>

[!code-vb[vbVarianceKeywords#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvariancekeywords/vb/module1.vb#4)]

## <a name="see-also"></a><span data-ttu-id="663ac-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="663ac-130">See also</span></span>

- [<span data-ttu-id="663ac-131">泛型介面中的變異數</span><span class="sxs-lookup"><span data-stu-id="663ac-131">Variance in Generic Interfaces</span></span>](../../programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md)
- [<span data-ttu-id="663ac-132">位於</span><span class="sxs-lookup"><span data-stu-id="663ac-132">In</span></span>](in-generic-modifier.md)
