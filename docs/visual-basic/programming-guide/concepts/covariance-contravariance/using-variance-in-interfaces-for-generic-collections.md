---
title: 針對泛型集合使用介面中的變異數
ms.date: 07/20/2015
ms.assetid: c867fcea-7462-4995-b9c5-542feec74036
ms.openlocfilehash: b762ce42215f9b24371313446637e95962677bfb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84375637"
---
# <a name="using-variance-in-interfaces-for-generic-collections-visual-basic"></a><span data-ttu-id="cd3ee-102">使用泛型集合介面中的變異數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="cd3ee-102">Using Variance in Interfaces for Generic Collections (Visual Basic)</span></span>

<span data-ttu-id="cd3ee-103">Covariant 介面允許其方法傳回與介面中指定的類型相比，其衍生程度較大的類型。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-103">A covariant interface allows its methods to return more derived types than those specified in the interface.</span></span> <span data-ttu-id="cd3ee-104">Contravariant 介面允許其方法接受與介面中指定的參數相比，其類型衍生程度較小的參數。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-104">A contravariant interface allows its methods to accept parameters of less derived types than those specified in the interface.</span></span>

<span data-ttu-id="cd3ee-105">在 .NET Framework 4 中，有數個現有介面已變成 Covariant 和 Contravariant。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-105">In .NET Framework 4, several existing interfaces became covariant and contravariant.</span></span> <span data-ttu-id="cd3ee-106">這些結構包括 <xref:System.Collections.Generic.IEnumerable%601> 及 <xref:System.IComparable%601>。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-106">These include <xref:System.Collections.Generic.IEnumerable%601> and <xref:System.IComparable%601>.</span></span> <span data-ttu-id="cd3ee-107">因此，您可以針對衍生類型的集合，重複使用搭配基底類型之泛型集合運作的方法。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-107">This enables you to reuse methods that operate with generic collections of base types for collections of derived types.</span></span>

<span data-ttu-id="cd3ee-108">如需 .NET Framework 中的 variant 介面清單，請參閱[泛型介面中的變異數（Visual Basic）](variance-in-generic-interfaces.md)。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-108">For a list of variant interfaces in the .NET Framework, see [Variance in Generic Interfaces (Visual Basic)](variance-in-generic-interfaces.md).</span></span>

## <a name="converting-generic-collections"></a><span data-ttu-id="cd3ee-109">轉換泛型集合</span><span class="sxs-lookup"><span data-stu-id="cd3ee-109">Converting Generic Collections</span></span>

<span data-ttu-id="cd3ee-110">下列範例說明在 <xref:System.Collections.Generic.IEnumerable%601> 介面中支援共變數的好處。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-110">The following example illustrates the benefits of covariance support in the <xref:System.Collections.Generic.IEnumerable%601> interface.</span></span> <span data-ttu-id="cd3ee-111">`PrintFullName` 方法接受 `IEnumerable(Of Person)` 類型的集合作為參數。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-111">The `PrintFullName` method accepts a collection of the `IEnumerable(Of Person)` type as a parameter.</span></span> <span data-ttu-id="cd3ee-112">不過，您可以重複用於 `IEnumerable(Of Person)` 類型的集合，因為 `Employee` 會繼承 `Person`。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-112">However, you can reuse it for a collection of the `IEnumerable(Of Person)` type because `Employee` inherits `Person`.</span></span>

```vb
' Simple hierarchy of classes.
Public Class Person
    Public Property FirstName As String
    Public Property LastName As String
End Class

Public Class Employee
    Inherits Person
End Class

' The method has a parameter of the IEnumerable(Of Person) type.
Public Sub PrintFullName(ByVal persons As IEnumerable(Of Person))
    For Each person As Person In persons
        Console.WriteLine(
            "Name: " & person.FirstName & " " & person.LastName)
    Next
End Sub

Sub Main()
    Dim employees As IEnumerable(Of Employee) = New List(Of Employee)

    ' You can pass IEnumerable(Of Employee),
    ' although the method expects IEnumerable(Of Person).

    PrintFullName(employees)

End Sub
```

## <a name="comparing-generic-collections"></a><span data-ttu-id="cd3ee-113">比較泛型集合</span><span class="sxs-lookup"><span data-stu-id="cd3ee-113">Comparing Generic Collections</span></span>

<span data-ttu-id="cd3ee-114">下列範例說明在 <xref:System.Collections.Generic.IComparer%601> 介面中支援反變數的好處。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-114">The following example illustrates the benefits of contravariance support in the <xref:System.Collections.Generic.IComparer%601> interface.</span></span> <span data-ttu-id="cd3ee-115">`PersonComparer` 類別會實作 `IComparer(Of Person)` 介面。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-115">The `PersonComparer` class implements the `IComparer(Of Person)` interface.</span></span> <span data-ttu-id="cd3ee-116">不過，您可以重複使用此類別來比較一連串類型為 `Employee` 的物件，因為 `Employee` 會繼承 `Person`。</span><span class="sxs-lookup"><span data-stu-id="cd3ee-116">However, you can reuse this class to compare a sequence of objects of the `Employee` type because `Employee` inherits `Person`.</span></span>

```vb
' Simple hierarchy of classes.
Public Class Person
    Public Property FirstName As String
    Public Property LastName As String
End Class

Public Class Employee
    Inherits Person
End Class
' The custom comparer for the Person type
' with standard implementations of Equals()
' and GetHashCode() methods.
Class PersonComparer
    Implements IEqualityComparer(Of Person)

    Public Function Equals1(
        ByVal x As Person,
        ByVal y As Person) As Boolean _
        Implements IEqualityComparer(Of Person).Equals

        If x Is y Then Return True
        If x Is Nothing OrElse y Is Nothing Then Return False
        Return (x.FirstName = y.FirstName) AndAlso
            (x.LastName = y.LastName)
    End Function
    Public Function GetHashCode1(
        ByVal person As Person) As Integer _
        Implements IEqualityComparer(Of Person).GetHashCode

        If person Is Nothing Then Return 0
        Dim hashFirstName =
            If(person.FirstName Is Nothing,
            0, person.FirstName.GetHashCode())
        Dim hashLastName = person.LastName.GetHashCode()
        Return hashFirstName Xor hashLastName
    End Function
End Class

Sub Main()
    Dim employees = New List(Of Employee) From {
        New Employee With {.FirstName = "Michael", .LastName = "Alexander"},
        New Employee With {.FirstName = "Jeff", .LastName = "Price"}
    }

    ' You can pass PersonComparer,
    ' which implements IEqualityComparer(Of Person),
    ' although the method expects IEqualityComparer(Of Employee)

    Dim noduplicates As IEnumerable(Of Employee) = employees.Distinct(New PersonComparer())

    For Each employee In noduplicates
        Console.WriteLine(employee.FirstName & " " & employee.LastName)
    Next
End Sub
```

## <a name="see-also"></a><span data-ttu-id="cd3ee-117">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cd3ee-117">See also</span></span>

- [<span data-ttu-id="cd3ee-118">泛型介面中的變異數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="cd3ee-118">Variance in Generic Interfaces (Visual Basic)</span></span>](variance-in-generic-interfaces.md)
