---
description: ':::no-loc text=interface::: (c # 參考) '
title: interface - C# 參考
ms.date: 01/17/2020
f1_keywords:
- interface_CSharpKeyword
helpviewer_keywords:
- interface keyword [C#]
ms.assetid: 7da38e81-4f99-4bc5-b07d-c986b687eeba
ms.openlocfilehash: 24f95e828522f467c519c0c8a7ba9410aa97af4e
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "89134584"
---
# <a name="no-loc-textinterface-c-reference"></a><span data-ttu-id="305eb-103">:::no-loc text="interface"::: (c # 參考) </span><span class="sxs-lookup"><span data-stu-id="305eb-103">:::no-loc text="interface"::: (C# Reference)</span></span>

<span data-ttu-id="305eb-104">介面會定義合約。</span><span class="sxs-lookup"><span data-stu-id="305eb-104">An interface defines a contract.</span></span> <span data-ttu-id="305eb-105">任何 [`class`](class.md) [`struct`](../builtin-types/struct.md) 執行該合約的或，都必須提供介面中所定義之成員的實作為。</span><span class="sxs-lookup"><span data-stu-id="305eb-105">Any [`class`](class.md) or [`struct`](../builtin-types/struct.md) that implements that contract must provide an implementation of the members defined in the interface.</span></span> <span data-ttu-id="305eb-106">從 c # 8.0 開始，介面可能會定義成員的預設執行。</span><span class="sxs-lookup"><span data-stu-id="305eb-106">Beginning with C# 8.0, an interface may define a default implementation for members.</span></span> <span data-ttu-id="305eb-107">它也可以定義 [`static`](static.md) 成員，以便為一般功能提供單一的實作為。</span><span class="sxs-lookup"><span data-stu-id="305eb-107">It may also define [`static`](static.md) members in order to provide a single implementation for common functionality.</span></span>

<span data-ttu-id="305eb-108">在下列範例中，類別 `ImplementationClass` 必須實作名為 `SampleMethod` 的方法，該方法沒有參數並會傳回 `void`。</span><span class="sxs-lookup"><span data-stu-id="305eb-108">In the following example, class `ImplementationClass` must implement a method named `SampleMethod` that has no parameters and returns `void`.</span></span>

<span data-ttu-id="305eb-109">如需詳細資訊與範例，請參閱[介面](../../programming-guide/interfaces/index.md)。</span><span class="sxs-lookup"><span data-stu-id="305eb-109">For more information and examples, see [Interfaces](../../programming-guide/interfaces/index.md).</span></span>

## <a name="example"></a><span data-ttu-id="305eb-110">範例</span><span class="sxs-lookup"><span data-stu-id="305eb-110">Example</span></span>

[!code-csharp[csrefKeywordsTypes#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#14)]

<span data-ttu-id="305eb-111">介面可以是命名空間或類別的成員。</span><span class="sxs-lookup"><span data-stu-id="305eb-111">An interface can be a member of a namespace or a class.</span></span> <span data-ttu-id="305eb-112">介面宣告可以包含宣告 (簽章，而不需要下列成員的任何實) ：</span><span class="sxs-lookup"><span data-stu-id="305eb-112">An interface declaration can contain declarations (signatures without any implementation) of the following members:</span></span>

- [<span data-ttu-id="305eb-113">方法</span><span class="sxs-lookup"><span data-stu-id="305eb-113">Methods</span></span>](../../programming-guide/classes-and-structs/methods.md)
- [<span data-ttu-id="305eb-114">屬性</span><span class="sxs-lookup"><span data-stu-id="305eb-114">Properties</span></span>](../../programming-guide/classes-and-structs/using-properties.md)
- [<span data-ttu-id="305eb-115">索引子</span><span class="sxs-lookup"><span data-stu-id="305eb-115">Indexers</span></span>](../../programming-guide/indexers/using-indexers.md)
- [<span data-ttu-id="305eb-116">事件</span><span class="sxs-lookup"><span data-stu-id="305eb-116">Events</span></span>](event.md)

<span data-ttu-id="305eb-117">上述的成員宣告通常不包含主體。</span><span class="sxs-lookup"><span data-stu-id="305eb-117">These preceding member declarations typically do not contain a body.</span></span> <span data-ttu-id="305eb-118">從 c # 8.0 開始，介面成員可以宣告主體。</span><span class="sxs-lookup"><span data-stu-id="305eb-118">Beginning with C# 8.0, an interface member may declare a body.</span></span> <span data-ttu-id="305eb-119">這稱為 *預設實值*。</span><span class="sxs-lookup"><span data-stu-id="305eb-119">This is called a *default implementation*.</span></span> <span data-ttu-id="305eb-120">具有主體的成員允許介面針對未提供覆寫執行的類別和結構提供「預設」實值。</span><span class="sxs-lookup"><span data-stu-id="305eb-120">Members with bodies permit the interface to provide a "default" implementation for classes and structs that don't provide an overriding implementation.</span></span> <span data-ttu-id="305eb-121">此外，從 c # 8.0 開始，介面可能包含：</span><span class="sxs-lookup"><span data-stu-id="305eb-121">In addition, beginning with C# 8.0, an interface may include:</span></span>

- [<span data-ttu-id="305eb-122">常數</span><span class="sxs-lookup"><span data-stu-id="305eb-122">Constants</span></span>](const.md)
- [<span data-ttu-id="305eb-123">運算子</span><span class="sxs-lookup"><span data-stu-id="305eb-123">Operators</span></span>](../operators/operator-overloading.md)
- <span data-ttu-id="305eb-124">[靜態](../../programming-guide/classes-and-structs/constructors.md#static-constructors)的函式。</span><span class="sxs-lookup"><span data-stu-id="305eb-124">[Static constructor](../../programming-guide/classes-and-structs/constructors.md#static-constructors).</span></span>
- [<span data-ttu-id="305eb-125">巢狀型別</span><span class="sxs-lookup"><span data-stu-id="305eb-125">Nested types</span></span>](../../programming-guide/classes-and-structs/nested-types.md)
- [<span data-ttu-id="305eb-126">靜態欄位、方法、屬性、索引子和事件</span><span class="sxs-lookup"><span data-stu-id="305eb-126">Static fields, methods, properties, indexers, and events</span></span>](static.md)
- <span data-ttu-id="305eb-127">使用明確介面執行語法的成員宣告。</span><span class="sxs-lookup"><span data-stu-id="305eb-127">Member declarations using the explicit interface implementation syntax.</span></span>
- <span data-ttu-id="305eb-128">明確的存取修飾詞 (預設存取是 [`public`](access-modifiers.md)) 。</span><span class="sxs-lookup"><span data-stu-id="305eb-128">Explicit access modifiers (the default access is [`public`](access-modifiers.md)).</span></span>

<span data-ttu-id="305eb-129">介面不能包含實例狀態。</span><span class="sxs-lookup"><span data-stu-id="305eb-129">Interfaces may not contain instance state.</span></span> <span data-ttu-id="305eb-130">雖然現在允許靜態欄位，但介面中不允許有實例欄位。</span><span class="sxs-lookup"><span data-stu-id="305eb-130">While static fields are now permitted, instance fields are not permitted in interfaces.</span></span> <span data-ttu-id="305eb-131">[實例 auto 屬性](../../programming-guide/classes-and-structs/auto-implemented-properties.md) 在介面中不受支援，因為它們會以隱含方式宣告隱藏的欄位。</span><span class="sxs-lookup"><span data-stu-id="305eb-131">[Instance auto-properties](../../programming-guide/classes-and-structs/auto-implemented-properties.md) are not supported in interfaces, as they would implicitly declare a hidden field.</span></span> <span data-ttu-id="305eb-132">此規則對屬性宣告具有微妙的影響。</span><span class="sxs-lookup"><span data-stu-id="305eb-132">This rule has a subtle effect on property declarations.</span></span> <span data-ttu-id="305eb-133">在介面宣告中，下列程式碼不會宣告自動執行的屬性，就像在或中 `class` 一樣 `struct` 。</span><span class="sxs-lookup"><span data-stu-id="305eb-133">In an interface declaration, the following code does not declare an auto-implemented property as it does in a `class` or `struct`.</span></span> <span data-ttu-id="305eb-134">相反地，它會宣告沒有預設執行的屬性，但必須在任何實介面的型別中執行：</span><span class="sxs-lookup"><span data-stu-id="305eb-134">Instead, it declares a property that doesn't have a default implementation but must be implemented in any type that implements the interface:</span></span>

```csharp
public interface INamed
{
  public string Name {get; set;}
}
```

<span data-ttu-id="305eb-135">介面可以繼承一或多個基底介面。</span><span class="sxs-lookup"><span data-stu-id="305eb-135">An interface can inherit from one or more base interfaces.</span></span> <span data-ttu-id="305eb-136">當介面 [覆寫](override.md) 基底介面中所執行的方法時，它必須使用 [明確的介面實](../../programming-guide/interfaces/explicit-interface-implementation.md) 語法。</span><span class="sxs-lookup"><span data-stu-id="305eb-136">When an interface [overrides a method](override.md) implemented in a base interface, it must use the [explicit interface implementation](../../programming-guide/interfaces/explicit-interface-implementation.md) syntax.</span></span>

<span data-ttu-id="305eb-137">當基底類型清單包含基底類別和介面時，基底類別一定會排在清單的第一個。</span><span class="sxs-lookup"><span data-stu-id="305eb-137">When a base type list contains a base class and interfaces, the base class must come first in the list.</span></span>

<span data-ttu-id="305eb-138">實作介面的類別能夠明確實作該介面的成員。</span><span class="sxs-lookup"><span data-stu-id="305eb-138">A class that implements an interface can explicitly implement members of that interface.</span></span> <span data-ttu-id="305eb-139">明確實作的成員不能經由類別執行個體存取，只能經由介面的執行個體來存取。</span><span class="sxs-lookup"><span data-stu-id="305eb-139">An explicitly implemented member cannot be accessed through a class instance, but only through an instance of the interface.</span></span> <span data-ttu-id="305eb-140">此外，只能透過介面的實例存取預設介面成員。</span><span class="sxs-lookup"><span data-stu-id="305eb-140">In addition, default interface members can only be accessed through an instance of the interface.</span></span>

<span data-ttu-id="305eb-141">如需明確介面執行的詳細資訊，請參閱 [明確介面執行](../../programming-guide/interfaces/explicit-interface-implementation.md)。</span><span class="sxs-lookup"><span data-stu-id="305eb-141">For more information about explicit interface implementation, see [Explicit Interface Implementation](../../programming-guide/interfaces/explicit-interface-implementation.md).</span></span>

## <a name="example"></a><span data-ttu-id="305eb-142">範例</span><span class="sxs-lookup"><span data-stu-id="305eb-142">Example</span></span>

<span data-ttu-id="305eb-143">下列範例示範介面實作。</span><span class="sxs-lookup"><span data-stu-id="305eb-143">The following example demonstrates interface implementation.</span></span> <span data-ttu-id="305eb-144">在此範例中，介面包含屬性宣告，而類別包含實作。</span><span class="sxs-lookup"><span data-stu-id="305eb-144">In this example, the interface contains the property declaration and the class contains the implementation.</span></span> <span data-ttu-id="305eb-145">實作 `IPoint` 的任何類別執行個體都有整數屬性 `x` 和 `y`。</span><span class="sxs-lookup"><span data-stu-id="305eb-145">Any instance of a class that implements `IPoint` has integer properties `x` and `y`.</span></span>

[!code-csharp[csrefKeywordsTypes#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#15)]

## <a name="c-language-specification"></a><span data-ttu-id="305eb-146">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="305eb-146">C# language specification</span></span>

<span data-ttu-id="305eb-147">如需詳細資訊，請參閱[c # 語言規格](~/_csharplang/spec/introduction.md)的[介面](~/_csharplang/spec/interfaces.md)區段和[預設介面成員的功能規格-c # 8.0](~/_csharplang/proposals/csharp-8.0/default-interface-methods.md)</span><span class="sxs-lookup"><span data-stu-id="305eb-147">For more information, see the [Interfaces](~/_csharplang/spec/interfaces.md) section of the [C# language specification](~/_csharplang/spec/introduction.md) and the feature specification for [Default interface members - C# 8.0](~/_csharplang/proposals/csharp-8.0/default-interface-methods.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="305eb-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="305eb-148">See also</span></span>

- [<span data-ttu-id="305eb-149">C # 參考</span><span class="sxs-lookup"><span data-stu-id="305eb-149">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="305eb-150">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="305eb-150">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="305eb-151">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="305eb-151">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="305eb-152">參考型別</span><span class="sxs-lookup"><span data-stu-id="305eb-152">Reference Types</span></span>](reference-types.md)
- [<span data-ttu-id="305eb-153">介面</span><span class="sxs-lookup"><span data-stu-id="305eb-153">Interfaces</span></span>](../../programming-guide/interfaces/index.md)
- [<span data-ttu-id="305eb-154">使用屬性</span><span class="sxs-lookup"><span data-stu-id="305eb-154">Using Properties</span></span>](../../programming-guide/classes-and-structs/using-properties.md)
- [<span data-ttu-id="305eb-155">使用索引子</span><span class="sxs-lookup"><span data-stu-id="305eb-155">Using Indexers</span></span>](../../programming-guide/indexers/using-indexers.md)
