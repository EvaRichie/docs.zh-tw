---
title: 泛型介面中的變異數
ms.date: 07/20/2015
ms.assetid: cf4096d0-4bb3-45a9-9a6b-f01e29a60333
ms.openlocfilehash: df28a9f24518f24d1be89acba726da7dfbbf9570
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84375586"
---
# <a name="variance-in-generic-interfaces-visual-basic"></a><span data-ttu-id="6d7cb-102">泛型介面中的變異數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-102">Variance in Generic Interfaces (Visual Basic)</span></span>

<span data-ttu-id="6d7cb-103">.NET Framework 4 針對數個現有泛型介面推出了差異支援。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-103">.NET Framework 4 introduced variance support for several existing generic interfaces.</span></span> <span data-ttu-id="6d7cb-104">差異支援可讓實作這些介面的類別以隱含方式轉換。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-104">Variance support enables implicit conversion of classes that implement these interfaces.</span></span> <span data-ttu-id="6d7cb-105">下列介面現在都是 Variant︰</span><span class="sxs-lookup"><span data-stu-id="6d7cb-105">The following interfaces are now variant:</span></span>

- <span data-ttu-id="6d7cb-106"><xref:System.Collections.Generic.IEnumerable%601> (T 是 Covariant)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-106"><xref:System.Collections.Generic.IEnumerable%601> (T is covariant)</span></span>

- <span data-ttu-id="6d7cb-107"><xref:System.Collections.Generic.IEnumerator%601> (T 是 Covariant)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-107"><xref:System.Collections.Generic.IEnumerator%601> (T is covariant)</span></span>

- <span data-ttu-id="6d7cb-108"><xref:System.Linq.IQueryable%601> (T 是 Covariant)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-108"><xref:System.Linq.IQueryable%601> (T is covariant)</span></span>

- <span data-ttu-id="6d7cb-109"><xref:System.Linq.IGrouping%602> (`TKey` 和 `TElement` 都是 Covariant)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-109"><xref:System.Linq.IGrouping%602> (`TKey` and `TElement` are covariant)</span></span>

- <span data-ttu-id="6d7cb-110"><xref:System.Collections.Generic.IComparer%601> (T 是 Contravariant)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-110"><xref:System.Collections.Generic.IComparer%601> (T is contravariant)</span></span>

- <span data-ttu-id="6d7cb-111"><xref:System.Collections.Generic.IEqualityComparer%601> (T 是 Contravariant)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-111"><xref:System.Collections.Generic.IEqualityComparer%601> (T is contravariant)</span></span>

- <span data-ttu-id="6d7cb-112"><xref:System.IComparable%601> (T 是 Contravariant)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-112"><xref:System.IComparable%601> (T is contravariant)</span></span>

<span data-ttu-id="6d7cb-113">共變數允許方法具有比介面泛型型別參數所定義之衍生程度更大的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-113">Covariance permits a method to have a more derived return type than that defined by the generic type parameter of the interface.</span></span> <span data-ttu-id="6d7cb-114">若要示範共變數功能，請考慮這些泛型介面︰`IEnumerable(Of Object)` 和 `IEnumerable(Of String)`。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-114">To illustrate the covariance feature, consider these generic interfaces: `IEnumerable(Of Object)` and `IEnumerable(Of String)`.</span></span> <span data-ttu-id="6d7cb-115">`IEnumerable(Of String)` 介面不會繼承 `IEnumerable(Of Object)` 介面。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-115">The `IEnumerable(Of String)` interface does not inherit the `IEnumerable(Of Object)` interface.</span></span> <span data-ttu-id="6d7cb-116">不過，`String` 型別確實會繼承`Object` 型別，而且在某些情況下，您可能希望將這些介面的物件指派給彼此。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-116">However, the `String` type does inherit the `Object` type, and in some cases you may want to assign objects of these interfaces to each other.</span></span> <span data-ttu-id="6d7cb-117">這顯示在下列程式碼範例中。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-117">This is shown in the following code example.</span></span>

```vb
Dim strings As IEnumerable(Of String) = New List(Of String)
Dim objects As IEnumerable(Of Object) = strings
```

<span data-ttu-id="6d7cb-118">在舊版的 .NET Framework 中，此程式碼會導致 Visual Basic 中發生編譯錯誤 `Option Strict On` 。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-118">In earlier versions of the .NET Framework, this code causes a compilation error in Visual Basic with `Option Strict On`.</span></span> <span data-ttu-id="6d7cb-119">但現在您可以使用 `strings`，而不使用 `objects`，如上例所示，因為 <xref:System.Collections.Generic.IEnumerable%601> 介面是 Covariant。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-119">But now you can use `strings` instead of `objects`, as shown in the previous example, because the <xref:System.Collections.Generic.IEnumerable%601> interface is covariant.</span></span>

<span data-ttu-id="6d7cb-120">反變數允許方法具有比介面泛型參數所指定之衍生程度更小的引數型別。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-120">Contravariance permits a method to have argument types that are less derived than that specified by the generic parameter of the interface.</span></span> <span data-ttu-id="6d7cb-121">為示範反變數，我們假設您已建立 `BaseComparer` 類別來比較 `BaseClass` 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-121">To illustrate contravariance, assume that you have created a `BaseComparer` class to compare instances of the `BaseClass` class.</span></span> <span data-ttu-id="6d7cb-122">`BaseComparer` 類別會實作 `IEqualityComparer(Of BaseClass)` 介面。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-122">The `BaseComparer` class implements the `IEqualityComparer(Of BaseClass)` interface.</span></span> <span data-ttu-id="6d7cb-123">因為 <xref:System.Collections.Generic.IEqualityComparer%601> 介面現在是 Contravariant，所以您可以使用 `BaseComparer` 比較繼承了 `BaseClass` 類別的類別執行個體。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-123">Because the <xref:System.Collections.Generic.IEqualityComparer%601> interface is now contravariant, you can use `BaseComparer` to compare instances of classes that inherit the `BaseClass` class.</span></span> <span data-ttu-id="6d7cb-124">這顯示在下列程式碼範例中。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-124">This is shown in the following code example.</span></span>

```vb
' Simple hierarchy of classes.
Class BaseClass
End Class

Class DerivedClass
    Inherits BaseClass
End Class

' Comparer class.
Class BaseComparer
    Implements IEqualityComparer(Of BaseClass)

    Public Function Equals1(ByVal x As BaseClass,
                            ByVal y As BaseClass) As Boolean _
                            Implements IEqualityComparer(Of BaseClass).Equals
        Return (x.Equals(y))
    End Function

    Public Function GetHashCode1(ByVal obj As BaseClass) As Integer _
        Implements IEqualityComparer(Of BaseClass).GetHashCode
        Return obj.GetHashCode
    End Function
End Class
Sub Test()
    Dim baseComparer As IEqualityComparer(Of BaseClass) = New BaseComparer
    ' Implicit conversion of IEqualityComparer(Of BaseClass) to
    ' IEqualityComparer(Of DerivedClass).
    Dim childComparer As IEqualityComparer(Of DerivedClass) = baseComparer
End Sub
```

<span data-ttu-id="6d7cb-125">如需更多範例，請參閱針對[泛型集合使用介面中的變異數（Visual Basic）](using-variance-in-interfaces-for-generic-collections.md)。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-125">For more examples, see [Using Variance in Interfaces for Generic Collections (Visual Basic)](using-variance-in-interfaces-for-generic-collections.md).</span></span>

<span data-ttu-id="6d7cb-126">僅參考型別支援泛型介面的差異。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-126">Variance in generic interfaces is supported for reference types only.</span></span> <span data-ttu-id="6d7cb-127">實值型別不支援差異。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-127">Value types do not support variance.</span></span> <span data-ttu-id="6d7cb-128">例如，`IEnumerable(Of Integer)` 無法以隱含方式轉換成 `IEnumerable(Of Object)`，因為整數是以實值型別表示。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-128">For example, `IEnumerable(Of Integer)` cannot be implicitly converted to `IEnumerable(Of Object)`, because integers are represented by a value type.</span></span>

```vb
Dim integers As IEnumerable(Of Integer) = New List(Of Integer)
' The following statement generates a compiler error
' with Option Strict On, because Integer is a value type.
' Dim objects As IEnumerable(Of Object) = integers
```

<span data-ttu-id="6d7cb-129">請務必牢記，實作 Variant 介面的類別仍然是非變異的。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-129">It is also important to remember that classes that implement variant interfaces are still invariant.</span></span> <span data-ttu-id="6d7cb-130">例如，雖然 <xref:System.Collections.Generic.List%601> 實作了 Covariant 介面 <xref:System.Collections.Generic.IEnumerable%601>，但您不能以隱含方式將 `List(Of Object)` 轉換成 `List(Of String)`。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-130">For example, although <xref:System.Collections.Generic.List%601> implements the covariant interface <xref:System.Collections.Generic.IEnumerable%601>, you cannot implicitly convert `List(Of Object)` to `List(Of String)`.</span></span> <span data-ttu-id="6d7cb-131">下列程式碼範例說明此情形。</span><span class="sxs-lookup"><span data-stu-id="6d7cb-131">This is illustrated in the following code example.</span></span>

```vb
' The following statement generates a compiler error
' because classes are invariant.
' Dim list As List(Of Object) = New List(Of String)

' You can use the interface object instead.
Dim listObjects As IEnumerable(Of Object) = New List(Of String)
```

## <a name="see-also"></a><span data-ttu-id="6d7cb-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6d7cb-132">See also</span></span>

- [<span data-ttu-id="6d7cb-133">使用泛型集合介面中的變異數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-133">Using Variance in Interfaces for Generic Collections (Visual Basic)</span></span>](using-variance-in-interfaces-for-generic-collections.md)
- [<span data-ttu-id="6d7cb-134">建立 Variant 泛型介面 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-134">Creating Variant Generic Interfaces (Visual Basic)</span></span>](creating-variant-generic-interfaces.md)
- [<span data-ttu-id="6d7cb-135">泛型介面</span><span class="sxs-lookup"><span data-stu-id="6d7cb-135">Generic Interfaces</span></span>](../../../../standard/generics/interfaces.md)
- [<span data-ttu-id="6d7cb-136">委派中的變異數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6d7cb-136">Variance in Delegates (Visual Basic)</span></span>](variance-in-delegates.md)
