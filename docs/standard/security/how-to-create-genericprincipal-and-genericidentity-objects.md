---
title: 如何：建立 GenericPrincipal 和 GenericIdentity 物件
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Creating Generic Identity Objects
- GenericPrincipal Objects
- Creating GenericPrincipal Objects
- GenericIdentity Objects
ms.assetid: 465694cf-258b-4747-9dae-35b01a5bcdbb
ms.openlocfilehash: 10a71185db3359cda1c3bf7a12f5698929c98296
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290859"
---
# <a name="how-to-create-genericprincipal-and-genericidentity-objects"></a>如何：建立 GenericPrincipal 和 GenericIdentity 物件

您可以 <xref:System.Security.Principal.GenericIdentity> 搭配類別使用類別 <xref:System.Security.Principal.GenericPrincipal> ，以建立獨立于 Windows 網域的授權配置。

### <a name="to-create-a-genericprincipal-object"></a>建立 GenericPrincipal 物件

1. 建立身分識別類別的新執行個體，並以您想要它保留的名稱進行初始化。 下列程式碼會建立新的 **GenericIdentity** 物件並以名稱 `MyUser` 進行初始化。

    ```vb
    Dim myIdentity As New GenericIdentity("MyUser")
    ```

    ```csharp
    GenericIdentity myIdentity = new GenericIdentity("MyUser");
    ```

2. 建立 **GenericPrincipal** 類別的新執行個體，並以先前建立的 **GenericIdentity** 物件和代表您要與此主體建立關聯之角色的字串陣列進行初始化。 下列程式碼範例會指定代表系統管理員角色和使用者角色的字串陣列。 然後會使用先前的 **GenericIdentity** 和字串陣列初始化 **GenericPrincipal**。

    ```vb
    Dim myStringArray As String() = {"Manager", "Teller"}
    DIm myPrincipal As New GenericPrincipal(myIdentity, myStringArray)
    ```

    ```csharp
    String[] myStringArray = {"Manager", "Teller"};
    GenericPrincipal myPrincipal = new GenericPrincipal(myIdentity, myStringArray);
    ```

3. 使用下列程式碼將主體附加至目前的執行緒。 這在主體必須經過多次驗證的情況下很有用，必須由應用程式中執行的其他程式碼進行驗證，或者必須由 <xref:System.Security.Permissions.PrincipalPermission> 物件驗證。 您仍然可以在主體物件上執行角色型驗證，而不需將它附加至執行緒。 如需詳細資訊，請參閱[取代 Principal 物件](replacing-a-principal-object.md)。

    ```vb
    Thread.CurrentPrincipal = myPrincipal
    ```

    ```csharp
    Thread.CurrentPrincipal = myPrincipal;
    ```

## <a name="example"></a>範例

下列程式碼範例示範如何建立 **GenericPrincipal** 和 **GenericIdentity** 的執行個體。 此程式碼會在主控台中顯示這些物件的值。

```vb
Imports System.Security.Principal
Imports System.Threading

Public Class Class1

    Public Shared Sub Main()
        ' Create generic identity.
        Dim myIdentity As New GenericIdentity("MyIdentity")

        ' Create generic principal.
        Dim myStringArray As String() =  {"Manager", "Teller"}
        Dim myPrincipal As New GenericPrincipal(myIdentity, myStringArray)

        ' Attach the principal to the current thread.
        ' This is not required unless repeated validation must occur,
        ' other code in your application must validate, or the
        ' PrincipalPermission object is used.
        Thread.CurrentPrincipal = myPrincipal

        ' Print values to the console.
        Dim name As String = myPrincipal.Identity.Name
        Dim auth As Boolean = myPrincipal.Identity.IsAuthenticated
        Dim isInRole As Boolean = myPrincipal.IsInRole("Manager")

        Console.WriteLine("The name is: {0}", name)
        Console.WriteLine("The isAuthenticated is: {0}", auth)
        Console.WriteLine("Is this a Manager? {0}", isInRole)

    End Sub

End Class
```

```csharp
using System;
using System.Security.Principal;
using System.Threading;

public class Class1
{
    public static int Main(string[] args)
    {
    // Create generic identity.
    GenericIdentity myIdentity = new GenericIdentity("MyIdentity");

    // Create generic principal.
    String[] myStringArray = {"Manager", "Teller"};
    GenericPrincipal myPrincipal =
        new GenericPrincipal(myIdentity, myStringArray);

    // Attach the principal to the current thread.
    // This is not required unless repeated validation must occur,
    // other code in your application must validate, or the
    // PrincipalPermission object is used.
    Thread.CurrentPrincipal = myPrincipal;

    // Print values to the console.
    String name =  myPrincipal.Identity.Name;
    bool auth =  myPrincipal.Identity.IsAuthenticated;
    bool isInRole =  myPrincipal.IsInRole("Manager");

    Console.WriteLine("The name is: {0}", name);
    Console.WriteLine("The isAuthenticated is: {0}", auth);
    Console.WriteLine("Is this a Manager? {0}", isInRole);

    return 0;
    }
}
```

執行後，應用程式會顯示與下列類似的輸出。

```console
The Name is: MyIdentity
The IsAuthenticated is: True
Is this a Manager? True
```

## <a name="see-also"></a>另請參閱

- <xref:System.Security.Principal.GenericIdentity>
- <xref:System.Security.Principal.GenericPrincipal>
- <xref:System.Security.Permissions.PrincipalPermission>
- [取代 Principal 物件](replacing-a-principal-object.md)
- [Principal 和 Identity 物件](principal-and-identity-objects.md)
