---
title: .NET 中的泛型集合
ms.date: 02/15/2018
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generics [.NET], collections
- generic collections [.NET]
- generic types [.NET]
ms.assetid: 5b646751-6ab7-465c-916c-b1a76aefa9f5
ms.openlocfilehash: 256fddd6c35cb78e8e22562960580929e1230c34
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94827343"
---
# <a name="generic-collections-in-net"></a><span data-ttu-id="8edb6-102">.NET 中的泛型集合</span><span class="sxs-lookup"><span data-stu-id="8edb6-102">Generic collections in .NET</span></span>

 <span data-ttu-id="8edb6-103">.NET 類別庫提供 <xref:System.Collections.Generic> 和 <xref:System.Collections.ObjectModel> 命名空間中的數種泛型集合類別。</span><span class="sxs-lookup"><span data-stu-id="8edb6-103">The .NET class library provides a number of generic collection classes in the <xref:System.Collections.Generic> and <xref:System.Collections.ObjectModel> namespaces.</span></span> <span data-ttu-id="8edb6-104">如需這些類別的詳細資訊，請參閱[常用的集合類型](../collections/commonly-used-collection-types.md)。</span><span class="sxs-lookup"><span data-stu-id="8edb6-104">For more detailed information about these classes, see [Commonly Used Collection Types](../collections/commonly-used-collection-types.md).</span></span>  
  
## <a name="systemcollectionsgeneric"></a><span data-ttu-id="8edb6-105">System.Collections.Generic</span><span class="sxs-lookup"><span data-stu-id="8edb6-105">System.Collections.Generic</span></span>

 <span data-ttu-id="8edb6-106">許多泛型集合類型是非泛型類型的直接模擬。</span><span class="sxs-lookup"><span data-stu-id="8edb6-106">Many of the generic collection types are direct analogs of nongeneric types.</span></span> <span data-ttu-id="8edb6-107"><xref:System.Collections.Generic.Dictionary%602> 是 <xref:System.Collections.Hashtable> 的泛型版本，使用泛型結構 <xref:System.Collections.Generic.KeyValuePair%602> (而不是 <xref:System.Collections.DictionaryEntry>) 來進行列舉。</span><span class="sxs-lookup"><span data-stu-id="8edb6-107"><xref:System.Collections.Generic.Dictionary%602> is a generic version of <xref:System.Collections.Hashtable>; it uses the generic structure <xref:System.Collections.Generic.KeyValuePair%602> for enumeration instead of <xref:System.Collections.DictionaryEntry>.</span></span>  
  
 <span data-ttu-id="8edb6-108"><xref:System.Collections.Generic.List%601> 是 <xref:System.Collections.ArrayList> 的泛型版本。</span><span class="sxs-lookup"><span data-stu-id="8edb6-108"><xref:System.Collections.Generic.List%601> is a generic version of <xref:System.Collections.ArrayList>.</span></span> <span data-ttu-id="8edb6-109">泛型 <xref:System.Collections.Generic.Queue%601> 和 <xref:System.Collections.Generic.Stack%601> 類別有對應的非泛型版本。</span><span class="sxs-lookup"><span data-stu-id="8edb6-109">There are generic <xref:System.Collections.Generic.Queue%601> and <xref:System.Collections.Generic.Stack%601> classes that correspond to the nongeneric versions.</span></span>  
  
 <span data-ttu-id="8edb6-110"><xref:System.Collections.Generic.SortedList%602> 有泛型和非泛型版本。</span><span class="sxs-lookup"><span data-stu-id="8edb6-110">There are generic and nongeneric versions of <xref:System.Collections.Generic.SortedList%602>.</span></span> <span data-ttu-id="8edb6-111">這兩種版本是字典和清單的混合。</span><span class="sxs-lookup"><span data-stu-id="8edb6-111">Both versions are hybrids of a dictionary and a list.</span></span> <span data-ttu-id="8edb6-112"><xref:System.Collections.Generic.SortedDictionary%602> 泛型類別是純字典，沒有對應的非泛型版本。</span><span class="sxs-lookup"><span data-stu-id="8edb6-112">The <xref:System.Collections.Generic.SortedDictionary%602> generic class is a pure dictionary and has no nongeneric counterpart.</span></span>  
  
 <span data-ttu-id="8edb6-113"><xref:System.Collections.Generic.LinkedList%601> 泛型類別是純連結清單，</span><span class="sxs-lookup"><span data-stu-id="8edb6-113">The <xref:System.Collections.Generic.LinkedList%601> generic class is a true linked list.</span></span> <span data-ttu-id="8edb6-114">沒有對應的非泛型版本。</span><span class="sxs-lookup"><span data-stu-id="8edb6-114">It has no nongeneric counterpart.</span></span>  
  
## <a name="systemcollectionsobjectmodel"></a><span data-ttu-id="8edb6-115">System.Collections.ObjectModel</span><span class="sxs-lookup"><span data-stu-id="8edb6-115">System.Collections.ObjectModel</span></span>

 <span data-ttu-id="8edb6-116"><xref:System.Collections.ObjectModel.Collection%601> 泛型類別提供基底類別，可用於衍生您自己的泛型集合類型。</span><span class="sxs-lookup"><span data-stu-id="8edb6-116">The <xref:System.Collections.ObjectModel.Collection%601> generic class provides a base class for deriving your own generic collection types.</span></span> <span data-ttu-id="8edb6-117"><xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 類別提供一個簡單的方法，從任何實作 <xref:System.Collections.Generic.IList%601> 泛型介面的類型中產生唯讀集合。</span><span class="sxs-lookup"><span data-stu-id="8edb6-117">The <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> class provides an easy way to produce a read-only collection from any type that implements the <xref:System.Collections.Generic.IList%601> generic interface.</span></span> <span data-ttu-id="8edb6-118"><xref:System.Collections.ObjectModel.KeyedCollection%602> 泛型類別提供一個方法來儲存物件 (其中包含物件的索引鍵)。</span><span class="sxs-lookup"><span data-stu-id="8edb6-118">The <xref:System.Collections.ObjectModel.KeyedCollection%602> generic class provides a way to store objects that contain their own keys.</span></span>  
  
## <a name="other-generic-types"></a><span data-ttu-id="8edb6-119">其他泛型型別</span><span class="sxs-lookup"><span data-stu-id="8edb6-119">Other generic types</span></span>

 <span data-ttu-id="8edb6-120"><xref:System.Nullable%601> 泛型結構可讓您使用可指派 `null` 的實值類型。</span><span class="sxs-lookup"><span data-stu-id="8edb6-120">The <xref:System.Nullable%601> generic structure allows you to use value types as if they could be assigned `null`.</span></span> <span data-ttu-id="8edb6-121">這在使用資料庫查詢時會很有用，因為包含實值類型的欄位可能遺漏。</span><span class="sxs-lookup"><span data-stu-id="8edb6-121">This can be useful when working with database queries, where fields that contain value types can be missing.</span></span> <span data-ttu-id="8edb6-122">泛型類型參數可以是任何實值類型。</span><span class="sxs-lookup"><span data-stu-id="8edb6-122">The generic type parameter can be any value type.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="8edb6-123">在 C# 和 Visual Basic 中，不需要明確使用 <xref:System.Nullable%601>，因為語言已具有可為 Null 型別的語法。</span><span class="sxs-lookup"><span data-stu-id="8edb6-123">In C# and Visual Basic, it is not necessary to use <xref:System.Nullable%601> explicitly because the language has syntax for nullable types.</span></span> <span data-ttu-id="8edb6-124">請參閱[可為 null 的實值型別 (c # 參考) ](../../csharp/language-reference/builtin-types/nullable-value-types.md)和[可為 null 的實數值型別 () Visual Basic](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)</span><span class="sxs-lookup"><span data-stu-id="8edb6-124">See [Nullable value types (C# reference)](../../csharp/language-reference/builtin-types/nullable-value-types.md) and [Nullable value types (Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md).</span></span>
  
 <span data-ttu-id="8edb6-125"><xref:System.ArraySegment%601> 泛型結構提供一個方法，將項目範圍限定在任何類型之以零為起始的一維陣列中。</span><span class="sxs-lookup"><span data-stu-id="8edb6-125">The <xref:System.ArraySegment%601> generic structure provides a way to delimit a range of elements within a one-dimensional, zero-based array of any type.</span></span> <span data-ttu-id="8edb6-126">泛型型別參數是陣列的項目類型。</span><span class="sxs-lookup"><span data-stu-id="8edb6-126">The generic type parameter is the type of the array's elements.</span></span>  
  
 <span data-ttu-id="8edb6-127"><xref:System.EventHandler%601>如果您的事件遵循 .net 所使用的事件處理模式，泛型委派就不需要宣告委派類型來處理事件。</span><span class="sxs-lookup"><span data-stu-id="8edb6-127">The <xref:System.EventHandler%601> generic delegate eliminates the need to declare a delegate type to handle events, if your event follows the event-handling pattern used by .NET.</span></span> <span data-ttu-id="8edb6-128">例如，假設您已建立衍生自 <xref:System.EventArgs> 的 `MyEventArgs` 類別來保存事件的資料。</span><span class="sxs-lookup"><span data-stu-id="8edb6-128">For example, suppose you have created a `MyEventArgs` class, derived from <xref:System.EventArgs>, to hold the data for your event.</span></span> <span data-ttu-id="8edb6-129">您可以接著依照下列方式來宣告事件：</span><span class="sxs-lookup"><span data-stu-id="8edb6-129">You can then declare the event as follows:</span></span>  
  
 [!code-cpp[Conceptual.Generics.Overview#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Generics.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source2.cs#7)]
 [!code-vb[Conceptual.Generics.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source2.vb#7)]  
  
## <a name="see-also"></a><span data-ttu-id="8edb6-130">請參閱</span><span class="sxs-lookup"><span data-stu-id="8edb6-130">See also</span></span>

- <xref:System.Collections.Generic?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel?displayProperty=nameWithType>
- [<span data-ttu-id="8edb6-131">泛型</span><span class="sxs-lookup"><span data-stu-id="8edb6-131">Generics</span></span>](index.md)
- [<span data-ttu-id="8edb6-132">用於運算元組和清單的泛型委派</span><span class="sxs-lookup"><span data-stu-id="8edb6-132">Generic Delegates for Manipulating Arrays and Lists</span></span>](delegates-for-manipulating-arrays-and-lists.md)
- [<span data-ttu-id="8edb6-133">泛型介面</span><span class="sxs-lookup"><span data-stu-id="8edb6-133">Generic Interfaces</span></span>](interfaces.md)
