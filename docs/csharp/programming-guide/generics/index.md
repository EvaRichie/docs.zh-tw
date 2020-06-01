---
title: 泛型 - C# 程式設計手冊
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, generics
- generics [C#]
ms.assetid: 75ea8509-a4ea-4e7a-a2b3-cf72482e9282
ms.openlocfilehash: a3ed3aa412c7d9c9d6b705dba80b527057c647fa
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241665"
---
# <a name="generics-c-programming-guide"></a><span data-ttu-id="3a47d-102">泛型 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="3a47d-102">Generics (C# Programming Guide)</span></span>

<span data-ttu-id="3a47d-103">泛型引進 .NET 類型參數的概念，讓您可以設計類別和方法，以延遲一或多個類型的規格，直到用戶端程式代碼宣告並具現化類別或方法為止。</span><span class="sxs-lookup"><span data-stu-id="3a47d-103">Generics introduce the concept of type parameters to .NET, which make it possible to design classes and methods that defer the specification of one or more types until the class or method is declared and instantiated by client code.</span></span> <span data-ttu-id="3a47d-104">例如，藉由使用泛型型別參數 `T` ，您可以撰寫其他用戶端程式代碼可以使用的單一類別，而不會產生執行時間轉換或裝箱作業的成本或風險，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3a47d-104">For example, by using a generic type parameter `T`, you can write a single class that other client code can use without incurring the cost or risk of runtime casts or boxing operations, as shown here:</span></span>

[!code-csharp[csProgGuideGenerics#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#1)]

<span data-ttu-id="3a47d-105">泛型類別和方法結合重複使用性、型別安全和效率，使其非泛型對應項無法使用。</span><span class="sxs-lookup"><span data-stu-id="3a47d-105">Generic classes and methods combine reusability, type safety, and efficiency in a way that their non-generic counterparts cannot.</span></span> <span data-ttu-id="3a47d-106">泛型最常搭配在其上操作的集合和方法使用。</span><span class="sxs-lookup"><span data-stu-id="3a47d-106">Generics are most frequently used with collections and the methods that operate on them.</span></span> <span data-ttu-id="3a47d-107"><xref:System.Collections.Generic>命名空間包含數個以泛型為基礎的集合類別。</span><span class="sxs-lookup"><span data-stu-id="3a47d-107">The <xref:System.Collections.Generic> namespace contains several generic-based collection classes.</span></span> <span data-ttu-id="3a47d-108">不建議使用非泛型集合，例如，基於 <xref:System.Collections.ArrayList> 相容性目的而維護。</span><span class="sxs-lookup"><span data-stu-id="3a47d-108">The non-generic collections, such as <xref:System.Collections.ArrayList> are not recommended and are maintained for compatibility purposes.</span></span> <span data-ttu-id="3a47d-109">如需詳細資訊，請參閱 [.NET 的泛型](../../../standard/generics/index.md)。</span><span class="sxs-lookup"><span data-stu-id="3a47d-109">For more information, see [Generics in .NET](../../../standard/generics/index.md).</span></span>

<span data-ttu-id="3a47d-110">當然，您也可以建立自訂的泛型型別和方法，自行處理泛型化的問題，並設計型別安全且有效率的模式。</span><span class="sxs-lookup"><span data-stu-id="3a47d-110">Of course, you can also create custom generic types and methods to provide your own generalized solutions and design patterns that are type-safe and efficient.</span></span> <span data-ttu-id="3a47d-111">下列程式碼範例顯示一個簡單的泛型連結清單類別，以供示範之用</span><span class="sxs-lookup"><span data-stu-id="3a47d-111">The following code example shows a simple generic linked-list class for demonstration purposes.</span></span> <span data-ttu-id="3a47d-112">（在大部分的情況下，您應該使用 <xref:System.Collections.Generic.List%601> .net 所提供的類別，而不是自行建立）。類型參數 `T` 用於數個位置，而具體類型通常會用來表示清單中儲存的專案類型。</span><span class="sxs-lookup"><span data-stu-id="3a47d-112">(In most cases, you should use the <xref:System.Collections.Generic.List%601> class provided by .NET instead of creating your own.) The type parameter `T` is used in several locations where a concrete type would ordinarily be used to indicate the type of the item stored in the list.</span></span> <span data-ttu-id="3a47d-113">這個參數可以用於下列方面：</span><span class="sxs-lookup"><span data-stu-id="3a47d-113">It is used in the following ways:</span></span>

- <span data-ttu-id="3a47d-114">作為 `AddHead` 方法中的方法參數類型。</span><span class="sxs-lookup"><span data-stu-id="3a47d-114">As the type of a method parameter in the `AddHead` method.</span></span>
- <span data-ttu-id="3a47d-115">作為巢狀 `Node` 類別中 `Data` 屬性的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="3a47d-115">As the return type of the `Data` property in the nested `Node` class.</span></span>
- <span data-ttu-id="3a47d-116">作為巢狀類別中私用成員 `data` 的類型。</span><span class="sxs-lookup"><span data-stu-id="3a47d-116">As the type of the private member `data` in the nested class.</span></span>

 <span data-ttu-id="3a47d-117">請注意， `T` 可供 nested `Node` 類別使用。</span><span class="sxs-lookup"><span data-stu-id="3a47d-117">Note that `T` is available to the nested `Node` class.</span></span> <span data-ttu-id="3a47d-118">當 `GenericList<T>` 以具象類型具現化時 (例如具現化為 `GenericList<int>`)，所出現的每個 `T` 都會以 `int` 取代。</span><span class="sxs-lookup"><span data-stu-id="3a47d-118">When `GenericList<T>` is instantiated with a concrete type, for example as a `GenericList<int>`, each occurrence of `T` will be replaced with `int`.</span></span>

[!code-csharp[csProgGuideGenerics#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#2)]

<span data-ttu-id="3a47d-119">下列程式碼範例示範用戶端程式碼如何使用泛型 `GenericList<T>` 類別建立整數清單。</span><span class="sxs-lookup"><span data-stu-id="3a47d-119">The following code example shows how client code uses the generic `GenericList<T>` class to create a list of integers.</span></span> <span data-ttu-id="3a47d-120">您只要變更型別引數，就能輕鬆修改下列的程式碼來建立字串清單或任何其他自訂類型的清單：</span><span class="sxs-lookup"><span data-stu-id="3a47d-120">Simply by changing the type argument, the following code could easily be modified to create lists of strings or any other custom type:</span></span>

[!code-csharp[csProgGuideGenerics#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#3)]

## <a name="generics-overview"></a><span data-ttu-id="3a47d-121">泛型總覽</span><span class="sxs-lookup"><span data-stu-id="3a47d-121">Generics overview</span></span>

- <span data-ttu-id="3a47d-122">使用泛型型別以最佳化程式碼重複使用、型別安全和效能。</span><span class="sxs-lookup"><span data-stu-id="3a47d-122">Use generic types to maximize code reuse, type safety, and performance.</span></span>
- <span data-ttu-id="3a47d-123">泛型的最常見用法是建立集合類別。</span><span class="sxs-lookup"><span data-stu-id="3a47d-123">The most common use of generics is to create collection classes.</span></span>
- <span data-ttu-id="3a47d-124">.NET 類別庫包含命名空間中的數個泛型集合類別 <xref:System.Collections.Generic> 。</span><span class="sxs-lookup"><span data-stu-id="3a47d-124">The .NET class library contains several generic collection classes in the <xref:System.Collections.Generic> namespace.</span></span> <span data-ttu-id="3a47d-125">您應該盡可能使用這些類別，而不是使用類似在 <xref:System.Collections> 命名空間中的 <xref:System.Collections.ArrayList> 類別。</span><span class="sxs-lookup"><span data-stu-id="3a47d-125">These should be used whenever possible instead of classes such as <xref:System.Collections.ArrayList> in the <xref:System.Collections> namespace.</span></span>
- <span data-ttu-id="3a47d-126">您可以建立自己的泛型介面、類別、方法、事件和委派。</span><span class="sxs-lookup"><span data-stu-id="3a47d-126">You can create your own generic interfaces, classes, methods, events, and delegates.</span></span>
- <span data-ttu-id="3a47d-127">泛型類別可限制為允許存取特定資料類型上的方法。</span><span class="sxs-lookup"><span data-stu-id="3a47d-127">Generic classes may be constrained to enable access to methods on particular data types.</span></span>
- <span data-ttu-id="3a47d-128">泛型資料類型中所使用的類型相關資訊，可在執行階段透過反映取得。</span><span class="sxs-lookup"><span data-stu-id="3a47d-128">Information on the types that are used in a generic data type may be obtained at run-time by using reflection.</span></span>

## <a name="related-sections"></a><span data-ttu-id="3a47d-129">相關章節</span><span class="sxs-lookup"><span data-stu-id="3a47d-129">Related sections</span></span>

- [<span data-ttu-id="3a47d-130">泛型類型參數</span><span class="sxs-lookup"><span data-stu-id="3a47d-130">Generic Type Parameters</span></span>](generic-type-parameters.md)
- [<span data-ttu-id="3a47d-131">型別參數的條件約束</span><span class="sxs-lookup"><span data-stu-id="3a47d-131">Constraints on Type Parameters</span></span>](constraints-on-type-parameters.md)
- [<span data-ttu-id="3a47d-132">泛型類別</span><span class="sxs-lookup"><span data-stu-id="3a47d-132">Generic Classes</span></span>](generic-classes.md)
- [<span data-ttu-id="3a47d-133">泛型介面</span><span class="sxs-lookup"><span data-stu-id="3a47d-133">Generic Interfaces</span></span>](generic-interfaces.md)
- [<span data-ttu-id="3a47d-134">泛型方法</span><span class="sxs-lookup"><span data-stu-id="3a47d-134">Generic Methods</span></span>](generic-methods.md)
- [<span data-ttu-id="3a47d-135">泛型委派</span><span class="sxs-lookup"><span data-stu-id="3a47d-135">Generic Delegates</span></span>](generic-delegates.md)
- [<span data-ttu-id="3a47d-136">C++ 範本和 C# 泛型之間的差異</span><span class="sxs-lookup"><span data-stu-id="3a47d-136">Differences Between C++ Templates and C# Generics</span></span>](differences-between-cpp-templates-and-csharp-generics.md)
- [<span data-ttu-id="3a47d-137">泛型和反映</span><span class="sxs-lookup"><span data-stu-id="3a47d-137">Generics and Reflection</span></span>](generics-and-reflection.md)
- [<span data-ttu-id="3a47d-138">執行階段中的泛型</span><span class="sxs-lookup"><span data-stu-id="3a47d-138">Generics in the Run Time</span></span>](generics-in-the-run-time.md)

## <a name="c-language-specification"></a><span data-ttu-id="3a47d-139">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="3a47d-139">C# language specification</span></span>

<span data-ttu-id="3a47d-140">如需詳細資訊，請參閱[c # 語言規格](~/_csharplang/spec/types.md#constructed-types)。</span><span class="sxs-lookup"><span data-stu-id="3a47d-140">For more information, see the [C# Language Specification](~/_csharplang/spec/types.md#constructed-types).</span></span>

## <a name="see-also"></a><span data-ttu-id="3a47d-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3a47d-141">See also</span></span>

- <xref:System.Collections.Generic>
- [<span data-ttu-id="3a47d-142">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="3a47d-142">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="3a47d-143">類型</span><span class="sxs-lookup"><span data-stu-id="3a47d-143">Types</span></span>](../types/index.md)
- [\<typeparam>](../xmldoc/typeparam.md)
- [\<typeparamref>](../xmldoc/typeparamref.md)
- [<span data-ttu-id="3a47d-144">.NET 的泛型</span><span class="sxs-lookup"><span data-stu-id="3a47d-144">Generics in .NET</span></span>](../../../standard/generics/index.md)
