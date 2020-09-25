---
title: 執行階段中的泛型 - C# 程式設計指南
description: 瞭解執行時間中的泛型型別。 請參閱程式碼範例，並檢視其他可用的資源。
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], at run time
ms.assetid: 119df7e6-9ceb-49df-af36-24f8f8c0747f
ms.openlocfilehash: 1d2afd34d1a80841ba711897492cd4cd6412fa53
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91184114"
---
# <a name="generics-in-the-run-time-c-programming-guide"></a><span data-ttu-id="5ae19-104">執行階段中的泛型 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="5ae19-104">Generics in the Run Time (C# Programming Guide)</span></span>

<span data-ttu-id="5ae19-105">當泛型型別或方法編譯到 Microsoft intermediate language (MSIL) 時，會包含可將其識別為具有型別參數的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="5ae19-105">When a generic type or method is compiled into Microsoft intermediate language (MSIL), it contains metadata that identifies it as having type parameters.</span></span> <span data-ttu-id="5ae19-106">泛型型別 MSIL 的使用方法，因提供的型別參數為實值型別或參考型別而異。</span><span class="sxs-lookup"><span data-stu-id="5ae19-106">How the MSIL for a generic type is used differs based on whether the supplied type parameter is a value type or reference type.</span></span>  
  
 <span data-ttu-id="5ae19-107">第一次以實值型別將泛型型別建構為參數時，執行階段會使用提供的參數或在 MSIL 適當位置中取代的參數，建立特定的泛型型別。</span><span class="sxs-lookup"><span data-stu-id="5ae19-107">When a generic type is first constructed with a value type as a parameter, the runtime creates a specialized generic type with the supplied parameter or parameters substituted in the appropriate locations in the MSIL.</span></span> <span data-ttu-id="5ae19-108">用為參數的每個唯一實值型別只建立一次特定的泛型型別。</span><span class="sxs-lookup"><span data-stu-id="5ae19-108">Specialized generic types are created one time for each unique value type that is used as a parameter.</span></span>  
  
 <span data-ttu-id="5ae19-109">例如，假設程式碼宣告以整數建構的堆疊：</span><span class="sxs-lookup"><span data-stu-id="5ae19-109">For example, suppose your program code declared a stack that is constructed of integers:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#42)]  
  
 <span data-ttu-id="5ae19-110">此時，執行階段會產生 <xref:System.Collections.Generic.Stack%601> 類別的特定版本，以整數適當取代其參數。</span><span class="sxs-lookup"><span data-stu-id="5ae19-110">At this point, the runtime generates a specialized version of the <xref:System.Collections.Generic.Stack%601> class that has the integer substituted appropriately for its parameter.</span></span> <span data-ttu-id="5ae19-111">現在，每當程式碼使用整數堆疊時，執行階段都會重複使用所產生的特定 <xref:System.Collections.Generic.Stack%601> 類別。</span><span class="sxs-lookup"><span data-stu-id="5ae19-111">Now, whenever your program code uses a stack of integers, the runtime reuses the generated specialized <xref:System.Collections.Generic.Stack%601> class.</span></span> <span data-ttu-id="5ae19-112">在下例中，會建立兩個整數堆疊的執行個體，它們共用一個 `Stack<int>` 程式碼的單一執行個體：</span><span class="sxs-lookup"><span data-stu-id="5ae19-112">In the following example, two instances of a stack of integers are created, and they share a single instance of the `Stack<int>` code:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#43](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#43)]  
  
 <span data-ttu-id="5ae19-113">不過，假設在程式碼的另一個點建立了另一個 <xref:System.Collections.Generic.Stack%601> 類別，以不同的實值型別 (如 `long`) 或使用者定義的結構做為其參數。</span><span class="sxs-lookup"><span data-stu-id="5ae19-113">However, suppose that another <xref:System.Collections.Generic.Stack%601> class with a different value type such as a `long` or a user-defined structure as its parameter is created at another point in your code.</span></span> <span data-ttu-id="5ae19-114">結果，執行階段會產生另一個版本的泛型型別，替代 MSIL 適當位置的 `long`。</span><span class="sxs-lookup"><span data-stu-id="5ae19-114">As a result, the runtime generates another version of the generic type and substitutes a `long` in the appropriate locations in MSIL.</span></span> <span data-ttu-id="5ae19-115">因為每個特定的泛型類別原本就包含實值型別，所以不再需要轉換。</span><span class="sxs-lookup"><span data-stu-id="5ae19-115">Conversions are no longer necessary because each specialized generic class natively contains the value type.</span></span>  
  
 <span data-ttu-id="5ae19-116">泛型在參考型別的運作方式稍有不同。</span><span class="sxs-lookup"><span data-stu-id="5ae19-116">Generics work somewhat differently for reference types.</span></span> <span data-ttu-id="5ae19-117">第一次搭配任何參考型別建構泛型型別時，執行階段會建立特定的泛型型別，以物件參考取代 MSIL 中的參數。</span><span class="sxs-lookup"><span data-stu-id="5ae19-117">The first time a generic type is constructed with any reference type, the runtime creates a specialized generic type with object references substituted for the parameters in the MSIL.</span></span> <span data-ttu-id="5ae19-118">然後，建構類型每次搭配參考型別具現化為其參數時，不論類型為何，執行階段都會重複使用先前建立的特定版本泛型型別。</span><span class="sxs-lookup"><span data-stu-id="5ae19-118">Then, every time that a constructed type is instantiated with a reference type as its parameter, regardless of what type it is, the runtime reuses the previously created specialized version of the generic type.</span></span> <span data-ttu-id="5ae19-119">這之所以可能，是因為所有的參考大小都相同。</span><span class="sxs-lookup"><span data-stu-id="5ae19-119">This is possible because all references are the same size.</span></span>  
  
 <span data-ttu-id="5ae19-120">例如，假設您有兩個參考型別，`Customer` 類別和 `Order` 類別，也假設您建立了 `Customer` 類型的堆疊：</span><span class="sxs-lookup"><span data-stu-id="5ae19-120">For example, suppose you had two reference types, a `Customer` class and an `Order` class, and also suppose that you created a stack of `Customer` types:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#47](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#47)]  
  
 [!code-csharp[csProgGuideGenerics#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#44)]  
  
 <span data-ttu-id="5ae19-121">此時，執行階段會產生特定版本的 <xref:System.Collections.Generic.Stack%601> 類別，儲存稍後要填入的物件參考，而不是儲存資料。</span><span class="sxs-lookup"><span data-stu-id="5ae19-121">At this point, the runtime generates a specialized version of the <xref:System.Collections.Generic.Stack%601> class that stores object references that will be filled in later instead of storing data.</span></span> <span data-ttu-id="5ae19-122">假設下一行程式碼建立另一個參考型別的堆疊，名為 `Order`：</span><span class="sxs-lookup"><span data-stu-id="5ae19-122">Suppose the next line of code creates a stack of another reference type, which is named `Order`:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#45)]  
  
 <span data-ttu-id="5ae19-123">與實值型別不同，另一個特定版本的 <xref:System.Collections.Generic.Stack%601> 類別並非針對 `Order` 類型而建立。</span><span class="sxs-lookup"><span data-stu-id="5ae19-123">Unlike with value types, another specialized version of the <xref:System.Collections.Generic.Stack%601> class is not created for the `Order` type.</span></span> <span data-ttu-id="5ae19-124">改建立特定版本的 <xref:System.Collections.Generic.Stack%601> 類別執行個體，設定 `orders` 變數參考它。</span><span class="sxs-lookup"><span data-stu-id="5ae19-124">Instead, an instance of the specialized version of the <xref:System.Collections.Generic.Stack%601> class is created and the `orders` variable is set to reference it.</span></span> <span data-ttu-id="5ae19-125">假設您接下來遇到一行程式碼，建立 `Customer` 類型的堆疊：</span><span class="sxs-lookup"><span data-stu-id="5ae19-125">Suppose that you then encountered a line of code to create a stack of a `Customer` type:</span></span>  
  
 [!code-csharp[csProgGuideGenerics#46](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#46)]  
  
 <span data-ttu-id="5ae19-126">如同先前使用以 `Order` 類型建立的 <xref:System.Collections.Generic.Stack%601> 類別一樣，建立另一個特定 <xref:System.Collections.Generic.Stack%601> 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="5ae19-126">As with the previous use of the <xref:System.Collections.Generic.Stack%601> class created by using the `Order` type, another instance of the specialized <xref:System.Collections.Generic.Stack%601> class is created.</span></span> <span data-ttu-id="5ae19-127">其中包含的指標會設定為參考大小為 `Customer` 類型的記憶體區域。</span><span class="sxs-lookup"><span data-stu-id="5ae19-127">The pointers that are contained therein are set to reference an area of memory the size of a `Customer` type.</span></span> <span data-ttu-id="5ae19-128">因為程式與程式之間的參考型別數目大不相同，所以泛型的 C# 實作會將編譯器所建立的參考型別泛型類別的特定類別數目降低到一，大幅減少程式碼數量。</span><span class="sxs-lookup"><span data-stu-id="5ae19-128">Because the number of reference types can vary wildly from program to program, the C# implementation of generics greatly reduces the amount of code by reducing to one the number of specialized classes created by the compiler for generic classes of reference types.</span></span>  
  
 <span data-ttu-id="5ae19-129">甚而，當泛型的 C# 類別使用實值型別或參考型別參數具現化時，反映會在執行階段查詢它，並確定其實際的類型及其型別參數。</span><span class="sxs-lookup"><span data-stu-id="5ae19-129">Moreover, when a generic C# class is instantiated by using a value type or reference type parameter, reflection can query it at runtime and both its actual type and its type parameter can be ascertained.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="5ae19-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5ae19-130">See also</span></span>

- <xref:System.Collections.Generic>
- [<span data-ttu-id="5ae19-131">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="5ae19-131">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="5ae19-132">泛型簡介</span><span class="sxs-lookup"><span data-stu-id="5ae19-132">Introduction to Generics</span></span>](./index.md)
- [<span data-ttu-id="5ae19-133">泛型</span><span class="sxs-lookup"><span data-stu-id="5ae19-133">Generics</span></span>](../../../standard/generics/index.md)
