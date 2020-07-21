---
title: 抽象和密封類別以及類別成員 - C# 程式設計手冊
description: 'C # 中的 abstract 關鍵字會建立不完整的類別和類別成員。 Sealed 關鍵字會防止繼承先前的虛擬類別或類別成員。'
ms.date: 07/20/2015
helpviewer_keywords:
- abstract classes [C#]
- sealed classes [C#]
- C# language, abstract classes
- C# language, sealed
ms.assetid: 99aa52f7-b435-43f9-936e-2470af734c4e
ms.openlocfilehash: 391a8ccbb1fbe6626d1cd5a4b6fcfd9ace3506e6
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86474484"
---
# <a name="abstract-and-sealed-classes-and-class-members-c-programming-guide"></a><span data-ttu-id="c8389-104">抽象和密封類別以及類別成員 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="c8389-104">Abstract and Sealed Classes and Class Members (C# Programming Guide)</span></span>
<span data-ttu-id="c8389-105">[abstract](../../language-reference/keywords/abstract.md) 關鍵字可讓您建立類別和[類別](../../language-reference/keywords/class.md)成員，這些類別和成員並不完整，因此必須在衍生類別中實作。</span><span class="sxs-lookup"><span data-stu-id="c8389-105">The [abstract](../../language-reference/keywords/abstract.md) keyword enables you to create classes and [class](../../language-reference/keywords/class.md) members that are incomplete and must be implemented in a derived class.</span></span>  
  
 <span data-ttu-id="c8389-106">[sealed](../../language-reference/keywords/sealed.md) 關鍵字可讓您避免繼承類別，或是先前標記為 [virtual](../../language-reference/keywords/virtual.md) 的特定類別成員。</span><span class="sxs-lookup"><span data-stu-id="c8389-106">The [sealed](../../language-reference/keywords/sealed.md) keyword enables you to prevent the inheritance of a class or certain class members that were previously marked [virtual](../../language-reference/keywords/virtual.md).</span></span>  
  
## <a name="abstract-classes-and-class-members"></a><span data-ttu-id="c8389-107">抽象類別和類別成員</span><span class="sxs-lookup"><span data-stu-id="c8389-107">Abstract Classes and Class Members</span></span>  
 <span data-ttu-id="c8389-108">在類別定義前面加入 `abstract` 關鍵字，就可以將類別宣告為抽象。</span><span class="sxs-lookup"><span data-stu-id="c8389-108">Classes can be declared as abstract by putting the keyword `abstract` before the class definition.</span></span> <span data-ttu-id="c8389-109">例如：</span><span class="sxs-lookup"><span data-stu-id="c8389-109">For example:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#13)]  
  
 <span data-ttu-id="c8389-110">抽象類別無法具現化。</span><span class="sxs-lookup"><span data-stu-id="c8389-110">An abstract class cannot be instantiated.</span></span> <span data-ttu-id="c8389-111">抽象類別的用途是提供基底類別的通用定義，可供多個衍生類別共用。</span><span class="sxs-lookup"><span data-stu-id="c8389-111">The purpose of an abstract class is to provide a common definition of a base class that multiple derived classes can share.</span></span> <span data-ttu-id="c8389-112">例如，類別庫會定義做為其多個函式的參數使用的抽象類別，並且要求使用該類別庫的程式設計人員建立衍生類別來提供自己的類別實作。</span><span class="sxs-lookup"><span data-stu-id="c8389-112">For example, a class library may define an abstract class that is used as a parameter to many of its functions, and require programmers using that library to provide their own implementation of the class by creating a derived class.</span></span>  
  
 <span data-ttu-id="c8389-113">抽象類別也可以定義抽象方法。</span><span class="sxs-lookup"><span data-stu-id="c8389-113">Abstract classes may also define abstract methods.</span></span> <span data-ttu-id="c8389-114">只要在方法的傳回型別前面加上關鍵字 `abstract`，就可以達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="c8389-114">This is accomplished by adding the keyword `abstract` before the return type of the method.</span></span> <span data-ttu-id="c8389-115">例如：</span><span class="sxs-lookup"><span data-stu-id="c8389-115">For example:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#14)]  
  
 <span data-ttu-id="c8389-116">抽象方法沒有任何實作，因此方法定義後面會接著一個分號，而不是一般方法區塊。</span><span class="sxs-lookup"><span data-stu-id="c8389-116">Abstract methods have no implementation, so the method definition is followed by a semicolon instead of a normal method block.</span></span> <span data-ttu-id="c8389-117">抽象類別的衍生類別必須實作所有抽象方法。</span><span class="sxs-lookup"><span data-stu-id="c8389-117">Derived classes of the abstract class must implement all abstract methods.</span></span> <span data-ttu-id="c8389-118">當抽象類別從基底類別繼承虛擬方法時，抽象類別可以使用抽象方法覆寫虛擬方法。</span><span class="sxs-lookup"><span data-stu-id="c8389-118">When an abstract class inherits a virtual method from a base class, the abstract class can override the virtual method with an abstract method.</span></span> <span data-ttu-id="c8389-119">例如：</span><span class="sxs-lookup"><span data-stu-id="c8389-119">For example:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#15)]  
  
 <span data-ttu-id="c8389-120">如果 `virtual` 方法宣告為 `abstract`，則該方法對於繼承自抽象類別的任何類別來說仍為虛擬。</span><span class="sxs-lookup"><span data-stu-id="c8389-120">If a `virtual` method is declared `abstract`, it is still virtual to any class inheriting from the abstract class.</span></span> <span data-ttu-id="c8389-121">繼承抽象方法的類別無法存取方法的原始實作：在前一個範例中，F 類別的 `DoWork` 無法呼叫 D 類別的 `DoWork`。如此一來，抽象類別可以強制衍生的類別為虛擬方法提供新的方法實作。</span><span class="sxs-lookup"><span data-stu-id="c8389-121">A class inheriting an abstract method cannot access the original implementation of the method—in the previous example, `DoWork` on class F cannot call `DoWork` on class D. In this way, an abstract class can force derived classes to provide new method implementations for virtual methods.</span></span>  
  
## <a name="sealed-classes-and-class-members"></a><span data-ttu-id="c8389-122">密封類別和類別成員</span><span class="sxs-lookup"><span data-stu-id="c8389-122">Sealed Classes and Class Members</span></span>  
 <span data-ttu-id="c8389-123">在類別定義前面加入 `sealed` 關鍵字，就可以將類別宣告為 [sealed](../../language-reference/keywords/sealed.md)。</span><span class="sxs-lookup"><span data-stu-id="c8389-123">Classes can be declared as [sealed](../../language-reference/keywords/sealed.md) by putting the keyword `sealed` before the class definition.</span></span> <span data-ttu-id="c8389-124">例如：</span><span class="sxs-lookup"><span data-stu-id="c8389-124">For example:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#16)]  
  
 <span data-ttu-id="c8389-125">密封類別不能當做基底類別使用。</span><span class="sxs-lookup"><span data-stu-id="c8389-125">A sealed class cannot be used as a base class.</span></span> <span data-ttu-id="c8389-126">基於這個理由，該類別也不能是抽象類別。</span><span class="sxs-lookup"><span data-stu-id="c8389-126">For this reason, it cannot also be an abstract class.</span></span> <span data-ttu-id="c8389-127">密封類別可以避免衍生。</span><span class="sxs-lookup"><span data-stu-id="c8389-127">Sealed classes prevent derivation.</span></span> <span data-ttu-id="c8389-128">由於密封類別永遠不能當做基底類別使用，因此某些執行階段最佳化呼叫密封類別成員的速度就能夠稍為加快。</span><span class="sxs-lookup"><span data-stu-id="c8389-128">Because they can never be used as a base class, some run-time optimizations can make calling sealed class members slightly faster.</span></span>  
  
 <span data-ttu-id="c8389-129">若方法、索引子、屬性或事件位於覆寫基底類別之虛擬成員的衍生類別上，就可以將該成員宣告為密封。</span><span class="sxs-lookup"><span data-stu-id="c8389-129">A method, indexer, property, or event, on a derived class that is overriding a virtual member of the base class can declare that member as sealed.</span></span> <span data-ttu-id="c8389-130">這樣一來，後續任何衍生類別的成員都不再擁有虛擬部分。</span><span class="sxs-lookup"><span data-stu-id="c8389-130">This negates the virtual aspect of the member for any further derived class.</span></span> <span data-ttu-id="c8389-131">只要在類別成員宣告中的 [override](../../language-reference/keywords/override.md) 關鍵字前面放置 `sealed` 關鍵字，就可以達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="c8389-131">This is accomplished by putting the `sealed` keyword before the [override](../../language-reference/keywords/override.md) keyword in the class member declaration.</span></span> <span data-ttu-id="c8389-132">例如：</span><span class="sxs-lookup"><span data-stu-id="c8389-132">For example:</span></span>  
  
 [!code-csharp[csProgGuideInheritance#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#17)]  
  
## <a name="see-also"></a><span data-ttu-id="c8389-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c8389-133">See also</span></span>

- [<span data-ttu-id="c8389-134">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="c8389-134">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="c8389-135">類別和結構</span><span class="sxs-lookup"><span data-stu-id="c8389-135">Classes and Structs</span></span>](./index.md)
- [<span data-ttu-id="c8389-136">繼承</span><span class="sxs-lookup"><span data-stu-id="c8389-136">Inheritance</span></span>](./inheritance.md)
- [<span data-ttu-id="c8389-137">方法</span><span class="sxs-lookup"><span data-stu-id="c8389-137">Methods</span></span>](./methods.md)
- [<span data-ttu-id="c8389-138">欄位</span><span class="sxs-lookup"><span data-stu-id="c8389-138">Fields</span></span>](./fields.md)
- [<span data-ttu-id="c8389-139">如何定義抽象屬性</span><span class="sxs-lookup"><span data-stu-id="c8389-139">How to define abstract properties</span></span>](./how-to-define-abstract-properties.md)
