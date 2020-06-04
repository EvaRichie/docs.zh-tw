---
title: 建立 Variant 泛型介面
ms.date: 07/20/2015
ms.assetid: d4037dd2-dfe9-4811-9150-93d4e8b20113
ms.openlocfilehash: 884349159d2738d8481b217f9dab383483616f2b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400638"
---
# <a name="creating-variant-generic-interfaces-visual-basic"></a><span data-ttu-id="d34c9-102">建立 Variant 泛型介面 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d34c9-102">Creating Variant Generic Interfaces (Visual Basic)</span></span>

<span data-ttu-id="d34c9-103">您可以在介面中將泛型型別參數宣告為 Covariant 或 Contravariant。</span><span class="sxs-lookup"><span data-stu-id="d34c9-103">You can declare generic type parameters in interfaces as covariant or contravariant.</span></span> <span data-ttu-id="d34c9-104">「共變數」\*\* 允許介面方法具有比泛型型別參數衍生程度更大的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="d34c9-104">*Covariance* allows interface methods to have more derived return types than that defined by the generic type parameters.</span></span> <span data-ttu-id="d34c9-105">「反變數」\*\* 允許介面具有比泛型參數所指定引數型別衍生程度更小的引數類型。</span><span class="sxs-lookup"><span data-stu-id="d34c9-105">*Contravariance* allows interface methods to have argument types that are less derived than that specified by the generic parameters.</span></span> <span data-ttu-id="d34c9-106">具有 Covariant 或 Contravariant 泛型型別參數的泛型介面稱為「變異」\*\*。</span><span class="sxs-lookup"><span data-stu-id="d34c9-106">A generic interface that has covariant or contravariant generic type parameters is called *variant*.</span></span>

> [!NOTE]
> <span data-ttu-id="d34c9-107">.NET Framework 4 針對數個現有泛型介面推出了差異支援。</span><span class="sxs-lookup"><span data-stu-id="d34c9-107">.NET Framework 4 introduced variance support for several existing generic interfaces.</span></span> <span data-ttu-id="d34c9-108">如需 .NET Framework 中的 variant 介面清單，請參閱[泛型介面中的變異數（Visual Basic）](variance-in-generic-interfaces.md)。</span><span class="sxs-lookup"><span data-stu-id="d34c9-108">For the list of the variant interfaces in the .NET Framework, see [Variance in Generic Interfaces (Visual Basic)](variance-in-generic-interfaces.md).</span></span>

## <a name="declaring-variant-generic-interfaces"></a><span data-ttu-id="d34c9-109">宣告 Variant 泛型介面</span><span class="sxs-lookup"><span data-stu-id="d34c9-109">Declaring Variant Generic Interfaces</span></span>

<span data-ttu-id="d34c9-110">您可以使用泛型型別參數的 `in` 和 `out` 關鍵字宣告 Variant 泛型介面。</span><span class="sxs-lookup"><span data-stu-id="d34c9-110">You can declare variant generic interfaces by using the `in` and `out` keywords for generic type parameters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d34c9-111">`ByRef`Visual Basic 中的參數不可以是 variant。</span><span class="sxs-lookup"><span data-stu-id="d34c9-111">`ByRef` parameters in Visual Basic cannot be variant.</span></span> <span data-ttu-id="d34c9-112">實值型別也不支援變異數。</span><span class="sxs-lookup"><span data-stu-id="d34c9-112">Value types also do not support variance.</span></span>

<span data-ttu-id="d34c9-113">您可以使用 `out` 關鍵字將泛型型別參數宣告為 Covariant 。</span><span class="sxs-lookup"><span data-stu-id="d34c9-113">You can declare a generic type parameter covariant by using the `out` keyword.</span></span> <span data-ttu-id="d34c9-114">Covariant 類型必須滿足下列條件︰</span><span class="sxs-lookup"><span data-stu-id="d34c9-114">The covariant type must satisfy the following conditions:</span></span>

- <span data-ttu-id="d34c9-115">類型僅用為介面方法的傳回型別，不用為方法引數的類型。</span><span class="sxs-lookup"><span data-stu-id="d34c9-115">The type is used only as a return type of interface methods and not used as a type of method arguments.</span></span> <span data-ttu-id="d34c9-116">這說明於下列範例中，其中 `R` 類型已宣告為 Covariant。</span><span class="sxs-lookup"><span data-stu-id="d34c9-116">This is illustrated in the following example, in which the type `R` is declared covariant.</span></span>

    ```vb
    Interface ICovariant(Of Out R)
        Function GetSomething() As R
        ' The following statement generates a compiler error.
        ' Sub SetSomething(ByVal sampleArg As R)
    End Interface
    ```

    <span data-ttu-id="d34c9-117">這個規則只有一個例外。</span><span class="sxs-lookup"><span data-stu-id="d34c9-117">There is one exception to this rule.</span></span> <span data-ttu-id="d34c9-118">如果您以 Contravariant 泛型委派作為方法參數，則可將類型用作委派的泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="d34c9-118">If you have a contravariant generic delegate as a method parameter, you can use the type as a generic type parameter for the delegate.</span></span> <span data-ttu-id="d34c9-119">以下範例的 `R` 類型說明這種情況：</span><span class="sxs-lookup"><span data-stu-id="d34c9-119">This is illustrated by the type `R` in the following example.</span></span> <span data-ttu-id="d34c9-120">如需詳細資訊，請參閱[委派中的變異數（Visual Basic）](variance-in-delegates.md)和[針對 Func 與 Action 泛型委派使用變異數（Visual Basic）](using-variance-for-func-and-action-generic-delegates.md)。</span><span class="sxs-lookup"><span data-stu-id="d34c9-120">For more information, see [Variance in Delegates (Visual Basic)](variance-in-delegates.md) and [Using Variance for Func and Action Generic Delegates (Visual Basic)](using-variance-for-func-and-action-generic-delegates.md).</span></span>

    ```vb
    Interface ICovariant(Of Out R)
        Sub DoSomething(ByVal callback As Action(Of R))
    End Interface
    ```

- <span data-ttu-id="d34c9-121">類型不會用作介面方法的泛型條件約束。</span><span class="sxs-lookup"><span data-stu-id="d34c9-121">The type is not used as a generic constraint for the interface methods.</span></span> <span data-ttu-id="d34c9-122">下列程式碼說明此情形。</span><span class="sxs-lookup"><span data-stu-id="d34c9-122">This is illustrated in the following code.</span></span>

    ```vb
    Interface ICovariant(Of Out R)
        ' The following statement generates a compiler error
        ' because you can use only contravariant or invariant types
        ' in generic constraints.
        ' Sub DoSomething(Of T As R)()
    End Interface
    ```

<span data-ttu-id="d34c9-123">您可以使用 `in` 關鍵字將泛型型別參數宣告為 Contravariant 。</span><span class="sxs-lookup"><span data-stu-id="d34c9-123">You can declare a generic type parameter contravariant by using the `in` keyword.</span></span> <span data-ttu-id="d34c9-124">Contravariant 類型僅可用作方法引數的類型，而不能用作介面方法的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="d34c9-124">The contravariant type can be used only as a type of method arguments and not as a return type of interface methods.</span></span> <span data-ttu-id="d34c9-125">Contravariant 類型也用於泛型條件約束。</span><span class="sxs-lookup"><span data-stu-id="d34c9-125">The contravariant type can also be used for generic constraints.</span></span> <span data-ttu-id="d34c9-126">下列程式碼示範如何宣告 Contravariant 介面，並針對其中一個方法使用泛型條件約束。</span><span class="sxs-lookup"><span data-stu-id="d34c9-126">The following code shows how to declare a contravariant interface and use a generic constraint for one of its methods.</span></span>

```vb
Interface IContravariant(Of In A)
    Sub SetSomething(ByVal sampleArg As A)
    Sub DoSomething(Of T As A)()
    ' The following statement generates a compiler error.
    ' Function GetSomething() As A
End Interface
```

<span data-ttu-id="d34c9-127">也可以在相同介面中同時支援共變數和反變數，但是對於不同的型別參數，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="d34c9-127">It is also possible to support both covariance and contravariance in the same interface, but for different type parameters, as shown in the following code example.</span></span>

```vb
Interface IVariant(Of Out R, In A)
    Function GetSomething() As R
    Sub SetSomething(ByVal sampleArg As A)
    Function GetSetSomething(ByVal sampleArg As A) As R
End Interface
```

<span data-ttu-id="d34c9-128">在 Visual Basic 中，您不能在 variant 介面中宣告事件，而不需要指定委派類型。</span><span class="sxs-lookup"><span data-stu-id="d34c9-128">In Visual Basic, you can't declare events in variant interfaces without specifying the delegate type.</span></span> <span data-ttu-id="d34c9-129">此外，變體介面不能有嵌套的類別、列舉或結構，但它可以有嵌套介面。</span><span class="sxs-lookup"><span data-stu-id="d34c9-129">Also, a variant interface can't have nested classes, enums, or structures, but it can have nested interfaces.</span></span> <span data-ttu-id="d34c9-130">下列程式碼說明此情形。</span><span class="sxs-lookup"><span data-stu-id="d34c9-130">This is illustrated in the following code.</span></span>

```vb
Interface ICovariant(Of Out R)
    ' The following statement generates a compiler error.
    ' Event SampleEvent()
    ' The following statement specifies the delegate type and
    ' does not generate an error.
    Event AnotherEvent As EventHandler

    ' The following statements generate compiler errors,
    ' because a variant interface cannot have
    ' nested enums, classes, or structures.

    'Enum SampleEnum : test : End Enum
    'Class SampleClass : End Class
    'Structure SampleStructure : Dim value As Integer : End Structure

    ' Variant interfaces can have nested interfaces.
    Interface INested : End Interface
End Interface
```

## <a name="implementing-variant-generic-interfaces"></a><span data-ttu-id="d34c9-131">實作 Variant 泛型介面</span><span class="sxs-lookup"><span data-stu-id="d34c9-131">Implementing Variant Generic Interfaces</span></span>

<span data-ttu-id="d34c9-132">您可以使用用於非變異介面的相同語法，在類別中實作 Variant 泛型介面。</span><span class="sxs-lookup"><span data-stu-id="d34c9-132">You implement variant generic interfaces in classes by using the same syntax that is used for invariant interfaces.</span></span> <span data-ttu-id="d34c9-133">下列程式碼範例示範如何在泛型類別中實作 Covariant 介面。</span><span class="sxs-lookup"><span data-stu-id="d34c9-133">The following code example shows how to implement a covariant interface in a generic class.</span></span>

```vb
Interface ICovariant(Of Out R)
    Function GetSomething() As R
End Interface

Class SampleImplementation(Of R)
    Implements ICovariant(Of R)
    Public Function GetSomething() As R _
    Implements ICovariant(Of R).GetSomething
        ' Some code.
    End Function
End Class
```

<span data-ttu-id="d34c9-134">實作 Variant 介面的類別為非變異。</span><span class="sxs-lookup"><span data-stu-id="d34c9-134">Classes that implement variant interfaces are invariant.</span></span> <span data-ttu-id="d34c9-135">例如，試想下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d34c9-135">For example, consider the following code.</span></span>

```vb
 The interface is covariant.
Dim ibutton As ICovariant(Of Button) =
    New SampleImplementation(Of Button)
Dim iobj As ICovariant(Of Object) = ibutton

' The class is invariant.
Dim button As SampleImplementation(Of Button) =
    New SampleImplementation(Of Button)
' The following statement generates a compiler error
' because classes are invariant.
' Dim obj As SampleImplementation(Of Object) = button
```

## <a name="extending-variant-generic-interfaces"></a><span data-ttu-id="d34c9-136">擴充 Variant 泛型介面</span><span class="sxs-lookup"><span data-stu-id="d34c9-136">Extending Variant Generic Interfaces</span></span>

<span data-ttu-id="d34c9-137">當您擴充 Variant 泛型介面時，必須使用 `in` 和 `out` 關鍵字明確指定衍生的介面是否支援變異數。</span><span class="sxs-lookup"><span data-stu-id="d34c9-137">When you extend a variant generic interface, you have to use the `in` and `out` keywords to explicitly specify whether the derived interface supports variance.</span></span> <span data-ttu-id="d34c9-138">編譯器不會從要擴充的介面推斷變異數。</span><span class="sxs-lookup"><span data-stu-id="d34c9-138">The compiler does not infer the variance from the interface that is being extended.</span></span> <span data-ttu-id="d34c9-139">例如，請參考下列介面。</span><span class="sxs-lookup"><span data-stu-id="d34c9-139">For example, consider the following interfaces.</span></span>

```vb
Interface ICovariant(Of Out T)
End Interface

Interface IInvariant(Of T)
    Inherits ICovariant(Of T)
End Interface

Interface IExtCovariant(Of Out T)
    Inherits ICovariant(Of T)
End Interface
```

<span data-ttu-id="d34c9-140">在 `Invariant(Of T)` 介面中，泛型型別參數 `T` 是不變的，而在 `IExtCovariant (Of Out T)` 型別參數中則是協變數，雖然這兩個介面都會擴充相同的介面。</span><span class="sxs-lookup"><span data-stu-id="d34c9-140">In the `Invariant(Of T)` interface, the generic type parameter `T` is invariant, whereas in `IExtCovariant (Of Out T)`the type parameter is covariant, although both interfaces extend the same interface.</span></span> <span data-ttu-id="d34c9-141">相同的規則也套用至 Contravariant 泛型型別參數。</span><span class="sxs-lookup"><span data-stu-id="d34c9-141">The same rule is applied to contravariant generic type parameters.</span></span>

<span data-ttu-id="d34c9-142">您可以建立介面，以便擴充 `T` 泛型型別參數為 Covariant 的介面，以及如果在擴充介面中， `T` 泛型型別參數為非變異的情況下，擴充其為 Contravariant 的介面。</span><span class="sxs-lookup"><span data-stu-id="d34c9-142">You can create an interface that extends both the interface where the generic type parameter `T` is covariant and the interface where it is contravariant if in the extending interface the generic type parameter `T` is invariant.</span></span> <span data-ttu-id="d34c9-143">下列程式碼範例說明此情形。</span><span class="sxs-lookup"><span data-stu-id="d34c9-143">This is illustrated in the following code example.</span></span>

```vb
Interface ICovariant(Of Out T)
End Interface

Interface IContravariant(Of In T)
End Interface

Interface IInvariant(Of T)
    Inherits ICovariant(Of T), IContravariant(Of T)
End Interface
```

<span data-ttu-id="d34c9-144">不過，如果 `T` 泛型型別參數在一個介面中宣告為 Covariant，則無法在擴充的介面中將它宣告為 Contravariant，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="d34c9-144">However, if a generic type parameter `T` is declared covariant in one interface, you cannot declare it contravariant in the extending interface, or vice versa.</span></span> <span data-ttu-id="d34c9-145">下列程式碼範例說明此情形。</span><span class="sxs-lookup"><span data-stu-id="d34c9-145">This is illustrated in the following code example.</span></span>

```vb
Interface ICovariant(Of Out T)
End Interface

' The following statements generate a compiler error.
' Interface ICoContraVariant(Of In T)
'     Inherits ICovariant(Of T)
' End Interface
```

### <a name="avoiding-ambiguity"></a><span data-ttu-id="d34c9-146">避免語意模糊</span><span class="sxs-lookup"><span data-stu-id="d34c9-146">Avoiding Ambiguity</span></span>

<span data-ttu-id="d34c9-147">當您實作 Variant 泛型介面時，變異數有時會導致語意模糊。</span><span class="sxs-lookup"><span data-stu-id="d34c9-147">When you implement variant generic interfaces, variance can sometimes lead to ambiguity.</span></span> <span data-ttu-id="d34c9-148">對此應該要設法避免。</span><span class="sxs-lookup"><span data-stu-id="d34c9-148">This should be avoided.</span></span>

<span data-ttu-id="d34c9-149">例如，如果您在一個類別中，明確地實作相同 Variant 泛型介面與不同泛型型別參數，它可能會造成語意模糊。</span><span class="sxs-lookup"><span data-stu-id="d34c9-149">For example, if you explicitly implement the same variant generic interface with different generic type parameters in one class, it can create ambiguity.</span></span> <span data-ttu-id="d34c9-150">在此情況下，編譯器不會產生錯誤，但未指定在執行階段將選擇哪個介面實作。</span><span class="sxs-lookup"><span data-stu-id="d34c9-150">The compiler does not produce an error in this case, but it is not specified which interface implementation will be chosen at runtime.</span></span> <span data-ttu-id="d34c9-151">這可能會導致您的程式碼中有細微錯誤。</span><span class="sxs-lookup"><span data-stu-id="d34c9-151">This could lead to subtle bugs in your code.</span></span> <span data-ttu-id="d34c9-152">請參考下列程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="d34c9-152">Consider the following code example.</span></span>

> [!NOTE]
> <span data-ttu-id="d34c9-153">使用 `Option Strict Off` 時，Visual Basic 會在有不明確的介面執行時產生編譯器警告。</span><span class="sxs-lookup"><span data-stu-id="d34c9-153">With `Option Strict Off`, Visual Basic generates a compiler warning when there is an ambiguous interface implementation.</span></span> <span data-ttu-id="d34c9-154">若為 `Option Strict On` ，Visual Basic 會產生編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="d34c9-154">With `Option Strict On`, Visual Basic generates a compiler error.</span></span>

```vb
' Simple class hierarchy.
Class Animal
End Class

Class Cat
    Inherits Animal
End Class

Class Dog
    Inherits Animal
End Class

' This class introduces ambiguity
' because IEnumerable(Of Out T) is covariant.
Class Pets
    Implements IEnumerable(Of Cat), IEnumerable(Of Dog)

    Public Function GetEnumerator() As IEnumerator(Of Cat) _
        Implements IEnumerable(Of Cat).GetEnumerator
        Console.WriteLine("Cat")
        ' Some code.
    End Function

    Public Function GetEnumerator1() As IEnumerator(Of Dog) _
        Implements IEnumerable(Of Dog).GetEnumerator
        Console.WriteLine("Dog")
        ' Some code.
    End Function

    Public Function GetEnumerator2() As IEnumerator _
        Implements IEnumerable.GetEnumerator
        ' Some code.
    End Function
End Class

Sub Main()
    Dim pets As IEnumerable(Of Animal) = New Pets()
    pets.GetEnumerator()
End Sub
```

<span data-ttu-id="d34c9-155">在此範例中，並未指定 `pets.GetEnumerator` 方法如何在 `Cat` 和 `Dog` 之間選擇。</span><span class="sxs-lookup"><span data-stu-id="d34c9-155">In this example, it is unspecified how the `pets.GetEnumerator` method chooses between `Cat` and `Dog`.</span></span> <span data-ttu-id="d34c9-156">這可能會在程式碼中造成問題。</span><span class="sxs-lookup"><span data-stu-id="d34c9-156">This could cause problems in your code.</span></span>

## <a name="see-also"></a><span data-ttu-id="d34c9-157">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d34c9-157">See also</span></span>

- [<span data-ttu-id="d34c9-158">泛型介面中的變異數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d34c9-158">Variance in Generic Interfaces (Visual Basic)</span></span>](variance-in-generic-interfaces.md)
- [<span data-ttu-id="d34c9-159">針對 Func 與 Action 泛型委派使用變異數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d34c9-159">Using Variance for Func and Action Generic Delegates (Visual Basic)</span></span>](using-variance-for-func-and-action-generic-delegates.md)
