---
title: 泛型類別 - C# 程式設計指南
description: 瞭解集合（例如連結清單、雜湊表、堆疊、佇列和樹狀結構）中使用的泛型類別。
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, generic classes
- generics [C#], classes
ms.assetid: 27d6f256-cd61-41e3-bc6e-b990a53b0224
ms.openlocfilehash: a885ae042eef939021d3a9b75616505c289bd43c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558083"
---
# <a name="generic-classes-c-programming-guide"></a><span data-ttu-id="e75c4-103">泛型類別 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="e75c4-103">Generic Classes (C# Programming Guide)</span></span>
<span data-ttu-id="e75c4-104">泛型類別會封裝不專屬於特定資料類型的作業。</span><span class="sxs-lookup"><span data-stu-id="e75c4-104">Generic classes encapsulate operations that are not specific to a particular data type.</span></span> <span data-ttu-id="e75c4-105">泛型類別最常搭配類似連結清單、雜湊表、堆疊、佇列、樹狀結構等的集合。</span><span class="sxs-lookup"><span data-stu-id="e75c4-105">The most common use for generic classes is with collections like linked lists, hash tables, stacks, queues, trees, and so on.</span></span> <span data-ttu-id="e75c4-106">無論儲存的資料類型為何，基本上是以相同的方式執行新增和移除集合項目等作業。</span><span class="sxs-lookup"><span data-stu-id="e75c4-106">Operations such as adding and removing items from the collection are performed in basically the same way regardless of the type of data being stored.</span></span>  
  
 <span data-ttu-id="e75c4-107">對需要集合類別的大多數案例而言，建議的方法是使用 .NET 類別庫中提供的那些類別。</span><span class="sxs-lookup"><span data-stu-id="e75c4-107">For most scenarios that require collection classes, the recommended approach is to use the ones provided in the .NET class library.</span></span> <span data-ttu-id="e75c4-108">如需使用這些類別的詳細資訊，請參閱 [.NET 中的泛型集合](../../../standard/generics/collections.md)。</span><span class="sxs-lookup"><span data-stu-id="e75c4-108">For more information about using these classes, see [Generic Collections in .NET](../../../standard/generics/collections.md).</span></span>  
  
 <span data-ttu-id="e75c4-109">建立泛型類別一般是從現有的實體類別開始，一次將一個類型變更成型別參數，直到達成一般化和可用性的最佳平衡。</span><span class="sxs-lookup"><span data-stu-id="e75c4-109">Typically, you create generic classes by starting with an existing concrete class, and changing types into type parameters one at a time until you reach the optimal balance of generalization and usability.</span></span> <span data-ttu-id="e75c4-110">在建立您自己的泛型類別時，重要考量包括：</span><span class="sxs-lookup"><span data-stu-id="e75c4-110">When creating your own generic classes, important considerations include the following:</span></span>  
  
- <span data-ttu-id="e75c4-111">要將哪些類型一般化為型別參數。</span><span class="sxs-lookup"><span data-stu-id="e75c4-111">Which types to generalize into type parameters.</span></span>  
  
     <span data-ttu-id="e75c4-112">依照規則，能夠參數化的類型愈多，程式碼就愈有彈性和可重複使用。</span><span class="sxs-lookup"><span data-stu-id="e75c4-112">As a rule, the more types you can parameterize, the more flexible and reusable your code becomes.</span></span> <span data-ttu-id="e75c4-113">但是，過多的一般化，會建立讓其他開發人員不易閱讀或了解的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e75c4-113">However, too much generalization can create code that is difficult for other developers to read or understand.</span></span>  
  
- <span data-ttu-id="e75c4-114">如果有的話，要將何種條件約束套用至型別參數 (請參閱[型別參數的條件約束](./constraints-on-type-parameters.md))。</span><span class="sxs-lookup"><span data-stu-id="e75c4-114">What constraints, if any, to apply to the type parameters (See [Constraints on Type Parameters](./constraints-on-type-parameters.md)).</span></span>  
  
     <span data-ttu-id="e75c4-115">理想的規則是盡可能套用最多的條件約束，卻仍能讓您處理必須處理的類型。</span><span class="sxs-lookup"><span data-stu-id="e75c4-115">A good rule is to apply the maximum constraints possible that will still let you handle the types you must handle.</span></span> <span data-ttu-id="e75c4-116">例如，如果您知道您的泛型類別，僅打算搭配參考型別，請套用類別條件約束。</span><span class="sxs-lookup"><span data-stu-id="e75c4-116">For example, if you know that your generic class is intended for use only with reference types, apply the class constraint.</span></span> <span data-ttu-id="e75c4-117">這可防止類別非預期搭配實值型別，而且可讓您使用 `T` 的 `as` 運算子，並檢查 null 值。</span><span class="sxs-lookup"><span data-stu-id="e75c4-117">That will prevent unintended use of your class with value types, and will enable you to use the `as` operator on `T`, and check for null values.</span></span>  
  
- <span data-ttu-id="e75c4-118">是否要將泛型行為分解成基底類別和子類別。</span><span class="sxs-lookup"><span data-stu-id="e75c4-118">Whether to factor generic behavior into base classes and subclasses.</span></span>  
  
     <span data-ttu-id="e75c4-119">因為泛型類別可做為基底類別，所以這裡適用和非泛型類別相同的設計考量。</span><span class="sxs-lookup"><span data-stu-id="e75c4-119">Because generic classes can serve as base classes, the same design considerations apply here as with non-generic classes.</span></span> <span data-ttu-id="e75c4-120">請參閱本主題稍後有關繼承自泛型基底類別的規則。</span><span class="sxs-lookup"><span data-stu-id="e75c4-120">See the rules about inheriting from generic base classes later in this topic.</span></span>  
  
- <span data-ttu-id="e75c4-121">是否要實作一或多個泛型介面。</span><span class="sxs-lookup"><span data-stu-id="e75c4-121">Whether to implement one or more generic interfaces.</span></span>  
  
     <span data-ttu-id="e75c4-122">例如，如果您要設計一個類別，用於建立泛型式集合的項目，您可能必須實作 `T` 是您類別類型的介面，例如 <xref:System.IComparable%601>。</span><span class="sxs-lookup"><span data-stu-id="e75c4-122">For example, if you are designing a class that will be used to create items in a generics-based collection, you may have to implement an interface such as <xref:System.IComparable%601> where `T` is the type of your class.</span></span>  
  
 <span data-ttu-id="e75c4-123">如需簡單泛型類別的範例，請參閱[泛型簡介](./index.md)。</span><span class="sxs-lookup"><span data-stu-id="e75c4-123">For an example of a simple generic class, see [Introduction to Generics](./index.md).</span></span>  
  
 <span data-ttu-id="e75c4-124">型別參數和條件約束的規則有數個泛型類別行為的含義，特別是有關繼承和成員存取範圍。</span><span class="sxs-lookup"><span data-stu-id="e75c4-124">The rules for type parameters and constraints have several implications for generic class behavior, especially regarding inheritance and member accessibility.</span></span> <span data-ttu-id="e75c4-125">請先了解一些辭彙再繼續。</span><span class="sxs-lookup"><span data-stu-id="e75c4-125">Before proceeding, you should understand some terms.</span></span> <span data-ttu-id="e75c4-126">泛型類別 `Node<T>,` 用戶端程式碼可藉由指定型別引數來參考類別，建立封閉式的建構類型 (`Node<int>`)。</span><span class="sxs-lookup"><span data-stu-id="e75c4-126">For a generic class `Node<T>,` client code can reference the class either by specifying a type argument, to create a closed constructed type (`Node<int>`).</span></span> <span data-ttu-id="e75c4-127">或者，它也可以保持不指定型別參數，例如，當您指定泛型基底類別時，建立開放式建構類型 (`Node<T>`)。</span><span class="sxs-lookup"><span data-stu-id="e75c4-127">Alternatively, it can leave the type parameter unspecified, for example when you specify a generic base class, to create an open constructed type (`Node<T>`).</span></span> <span data-ttu-id="e75c4-128">泛型類別可以繼承自實體、封閉式或開放式建構基底類別：</span><span class="sxs-lookup"><span data-stu-id="e75c4-128">Generic classes can inherit from concrete, closed constructed, or open constructed base classes:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#16)]  
  
 <span data-ttu-id="e75c4-129">換言之，非泛型的實體類別可以繼承自封閉式建構基底類別，但不是繼承自開放式建構類別或型別參數，因為用戶端程式碼在執行階段沒有任何方法，提供必要的型別引數來具現化基底類別。</span><span class="sxs-lookup"><span data-stu-id="e75c4-129">Non-generic, in other words, concrete, classes can inherit from closed constructed base classes, but not from open constructed classes or from type parameters because there is no way at run time for client code to supply the type argument required to instantiate the base class.</span></span>  
  
 [!code-csharp[csProgGuideGenerics#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#17)]  
  
 <span data-ttu-id="e75c4-130">繼承自開放式建構類型的泛型類別必須為所有任何基底類別類型參數提供型別引數，而繼承類別不共用這些參數，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="e75c4-130">Generic classes that inherit from open constructed types must supply type arguments for any base class type parameters that are not shared by the inheriting class, as demonstrated in the following code:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#18)]  
  
 <span data-ttu-id="e75c4-131">繼承自開放式建構類型的泛型類別必須指定條件約束，這些條件約束是基底類型上的條件約束超集，或暗示基底類型上的條件約束：</span><span class="sxs-lookup"><span data-stu-id="e75c4-131">Generic classes that inherit from open constructed types must specify constraints that are a superset of, or imply, the constraints on the base type:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#19)]  
  
 <span data-ttu-id="e75c4-132">泛型型別可以使用多個型別參數和條件約束，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e75c4-132">Generic types can use multiple type parameters and constraints, as follows:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#20)]  
  
 <span data-ttu-id="e75c4-133">開放式建構和封閉式建構類型可用為方法參數：</span><span class="sxs-lookup"><span data-stu-id="e75c4-133">Open constructed and closed constructed types can be used as method parameters:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#21)]  
  
 <span data-ttu-id="e75c4-134">如果泛型類別實作某個介面，則該類別的所有執行個體都可以轉換成該介面。</span><span class="sxs-lookup"><span data-stu-id="e75c4-134">If a generic class implements an interface, all instances of that class can be cast to that interface.</span></span>  
  
 <span data-ttu-id="e75c4-135">泛型類別都是非變異值。</span><span class="sxs-lookup"><span data-stu-id="e75c4-135">Generic classes are invariant.</span></span> <span data-ttu-id="e75c4-136">換句話說，如果輸入參數指定 `List<BaseClass>`，您會在嘗試提供 `List<DerivedClass>` 時收到編譯時期錯誤。</span><span class="sxs-lookup"><span data-stu-id="e75c4-136">In other words, if an input parameter specifies a `List<BaseClass>`, you will get a compile-time error if you try to provide a `List<DerivedClass>`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e75c4-137">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e75c4-137">See also</span></span>

- <xref:System.Collections.Generic>
- [<span data-ttu-id="e75c4-138">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="e75c4-138">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="e75c4-139">泛型</span><span class="sxs-lookup"><span data-stu-id="e75c4-139">Generics</span></span>](./index.md)
- <span data-ttu-id="e75c4-140">[Saving the State of Enumerators](/archive/blogs/wesdyer/saving-the-state-of-enumerators) (儲存列舉程式狀態)</span><span class="sxs-lookup"><span data-stu-id="e75c4-140">[Saving the State of Enumerators](/archive/blogs/wesdyer/saving-the-state-of-enumerators)</span></span>
- [<span data-ttu-id="e75c4-141">繼承謎題，第一部</span><span class="sxs-lookup"><span data-stu-id="e75c4-141">An Inheritance Puzzle, Part One</span></span>](/archive/blogs/ericlippert/an-inheritance-puzzle-part-one)
