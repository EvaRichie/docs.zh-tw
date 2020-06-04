---
title: 針對 Func 與 Action 泛型委派使用變異數
ms.date: 07/20/2015
ms.assetid: 36c3012f-b39c-493b-b90f-079b5912ac1b
ms.openlocfilehash: f824d2422d67f1395d21a0863ca8c95d9f108989
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84375754"
---
# <a name="using-variance-for-func-and-action-generic-delegates-visual-basic"></a><span data-ttu-id="f54f7-102">針對 Func 與 Action 泛型委派使用變異數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f54f7-102">Using Variance for Func and Action Generic Delegates (Visual Basic)</span></span>

<span data-ttu-id="f54f7-103">下列範例示範如何在 `Func` 和 `Action` 泛型委派中使用共變數和反變數，以便在您的程式碼中重複使用方法並提供更多彈性。</span><span class="sxs-lookup"><span data-stu-id="f54f7-103">These examples demonstrate how to use covariance and contravariance in the `Func` and `Action` generic delegates to enable reuse of methods and provide more flexibility in your code.</span></span>

<span data-ttu-id="f54f7-104">如需共變數和逆變性的詳細資訊，請參閱[委派中的變異數（Visual Basic）](variance-in-delegates.md)。</span><span class="sxs-lookup"><span data-stu-id="f54f7-104">For more information about covariance and contravariance, see [Variance in Delegates (Visual Basic)](variance-in-delegates.md).</span></span>

## <a name="using-delegates-with-covariant-type-parameters"></a><span data-ttu-id="f54f7-105">使用具有 Covariant 型別參數的委派</span><span class="sxs-lookup"><span data-stu-id="f54f7-105">Using Delegates with Covariant Type Parameters</span></span>

<span data-ttu-id="f54f7-106">下列範例說明在泛型 `Func` 委派中支援共變數的好處。</span><span class="sxs-lookup"><span data-stu-id="f54f7-106">The following example illustrates the benefits of covariance support in the generic `Func` delegates.</span></span> <span data-ttu-id="f54f7-107">`FindByTitle` 方法使用 `String` 類型的參數，並傳回 `Employee` 類型的物件。</span><span class="sxs-lookup"><span data-stu-id="f54f7-107">The `FindByTitle` method takes a parameter of the `String` type and returns an object of the `Employee` type.</span></span> <span data-ttu-id="f54f7-108">不過，您可以將此方法指派給 `Func(Of String, Person)` 委派，因為 `Employee` 會繼承 `Person`。</span><span class="sxs-lookup"><span data-stu-id="f54f7-108">However, you can assign this method to the `Func(Of String, Person)` delegate because `Employee` inherits `Person`.</span></span>

```vb
' Simple hierarchy of classes.
Public Class Person
End Class

Public Class Employee
    Inherits Person
End Class

Class Finder
    Public Shared Function FindByTitle(
        ByVal title As String) As Employee
        ' This is a stub for a method that returns
        ' an employee that has the specified title.
        Return New Employee
    End Function

    Sub Test()
        ' Create an instance of the delegate without using variance.
        Dim findEmployee As Func(Of String, Employee) =
            AddressOf FindByTitle

        ' The delegate expects a method to return Person,
        ' but you can assign it a method that returns Employee.
        Dim findPerson As Func(Of String, Person) =
            AddressOf FindByTitle

        ' You can also assign a delegate
        ' that returns a more derived type to a delegate
        ' that returns a less derived type.
        findPerson = findEmployee
    End Sub
End Class
```

## <a name="using-delegates-with-contravariant-type-parameters"></a><span data-ttu-id="f54f7-109">使用具有 Contravariant 型別參數的委派</span><span class="sxs-lookup"><span data-stu-id="f54f7-109">Using Delegates with Contravariant Type Parameters</span></span>

<span data-ttu-id="f54f7-110">下列範例說明在泛型 `Action` 委派中支援反變數的好處。</span><span class="sxs-lookup"><span data-stu-id="f54f7-110">The following example illustrates the benefits of contravariance support in the generic `Action` delegates.</span></span> <span data-ttu-id="f54f7-111">`AddToContacts` 方法使用 `Person` 類型的參數。</span><span class="sxs-lookup"><span data-stu-id="f54f7-111">The `AddToContacts` method takes a parameter of the `Person` type.</span></span> <span data-ttu-id="f54f7-112">不過，您可以將此方法指派給 `Action(Of Employee)` 委派，因為 `Employee` 會繼承 `Person`。</span><span class="sxs-lookup"><span data-stu-id="f54f7-112">However, you can assign this method to the `Action(Of Employee)` delegate because `Employee` inherits `Person`.</span></span>

```vb
Public Class Person
End Class

Public Class Employee
    Inherits Person
End Class

Class AddressBook
    Shared Sub AddToContacts(ByVal person As Person)
        ' This method adds a Person object
        ' to a contact list.
    End Sub

    Sub Test()
        ' Create an instance of the delegate without using variance.
        Dim addPersonToContacts As Action(Of Person) =
            AddressOf AddToContacts

        ' The Action delegate expects
        ' a method that has an Employee parameter,
        ' but you can assign it a method that has a Person parameter
        ' because Employee derives from Person.
        Dim addEmployeeToContacts As Action(Of Employee) =
            AddressOf AddToContacts

        ' You can also assign a delegate
        ' that accepts a less derived parameter
        ' to a delegate that accepts a more derived parameter.
        addEmployeeToContacts = addPersonToContacts
    End Sub
End Class
```

## <a name="see-also"></a><span data-ttu-id="f54f7-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f54f7-113">See also</span></span>

- [<span data-ttu-id="f54f7-114">共變數和反變數 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="f54f7-114">Covariance and Contravariance (Visual Basic)</span></span>](index.md)
- [<span data-ttu-id="f54f7-115">泛型</span><span class="sxs-lookup"><span data-stu-id="f54f7-115">Generics</span></span>](../../../../standard/generics/index.md)
