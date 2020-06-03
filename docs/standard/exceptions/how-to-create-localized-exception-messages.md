---
title: 如何使用當地語系化的例外狀況訊息來建立使用者定義的例外狀況
description: 瞭解如何使用當地語系化的例外狀況訊息來建立使用者定義的例外狀況
author: Youssef1313
dev_langs:
- csharp
- vb
ms.date: 09/13/2019
ms.openlocfilehash: fa0bbfdbfc9408302eec2edd4e4ee4503d2612c7
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/13/2020
ms.locfileid: "81243345"
---
# <a name="how-to-create-user-defined-exceptions-with-localized-exception-messages"></a>如何使用當地語系化的例外狀況訊息來建立使用者定義的例外狀況

在本文中，您將瞭解如何使用附屬元件，建立繼承自基類的使用者自訂例外狀況 <xref:System.Exception> 以及當地語系化的例外狀況訊息。

## <a name="create-custom-exceptions"></a>建立自訂例外狀況

.NET 包含許多您可以使用的不同例外狀況。 不過，在某些情況下，如果它們都不符合您的需求，您可以建立自己的自訂例外狀況。

假設您想要建立 `StudentNotFoundException` 包含 `StudentName` 屬性的。
若要建立自訂例外狀況，請遵循下列步驟：

1. 建立繼承自的可序列化類別 <xref:System.Exception> 。 類別名稱的結尾應該是 "Exception"：

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception { }
    ```

    ```vb
    <Serializable>
    Public Class StudentNotFoundException
        Inherits Exception
    End Class
    ```

1. 新增預設的構造函式：

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception
    {
        public StudentNotFoundException() { }

        public StudentNotFoundException(string message)
            : base(message) { }

        public StudentNotFoundException(string message, Exception inner)
            : base(message, inner) { }
    }
    ```

    ```vb
    <Serializable>
    Public Class StudentNotFoundException
        Inherits Exception

        Public Sub New()
        End Sub

        Public Sub New(message As String)
            MyBase.New(message)
        End Sub

        Public Sub New(message As String, inner As Exception)
            MyBase.New(message, inner)
        End Sub
    End Class
    ```

1. 定義任何其他屬性和構造函式：

    ```csharp
    [Serializable]
    public class StudentNotFoundException : Exception
    {
        public string StudentName { get; }

        public StudentNotFoundException() { }

        public StudentNotFoundException(string message)
            : base(message) { }

        public StudentNotFoundException(string message, Exception inner)
            : base(message, inner) { }

        public StudentNotFoundException(string message, string studentName)
            : this(message)
        {
            StudentName = studentName;
        }
    }
    ```

    ```vb
    <Serializable>
    Public Class StudentNotFoundException
        Inherits Exception

        Public ReadOnly Property StudentName As String

        Public Sub New()
        End Sub

        Public Sub New(message As String)
            MyBase.New(message)
        End Sub

        Public Sub New(message As String, inner As Exception)
            MyBase.New(message, inner)
        End Sub

        Public Sub New(message As String, studentName As String)
            Me.New(message)
            StudentName = studentName
        End Sub
    End Class
    ```

## <a name="create-localized-exception-messages"></a>建立當地語系化的例外狀況訊息

您已建立自訂例外狀況，您可以使用類似下列的程式碼在任何地方擲回它：

```csharp
throw new StudentNotFoundException("The student cannot be found.", "John");
```

```vb
Throw New StudentNotFoundException("The student cannot be found.", "John")
```

前一行的問題在於，它 `"The student cannot be found."` 只是一個常數位串。 在當地語系化的應用程式中，您想要根據使用者文化特性來擁有不同的訊息。
[附屬元件](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md)是執行這項操作的好方法。 附屬元件是包含特定語言之資源的 .dll。 當您在執行時間要求特定資源時，CLR 會根據使用者文化特性來尋找該資源。 如果找不到該文化特性的附屬元件，則會使用預設文化特性的資源。

若要建立當地語系化的例外狀況訊息：

1. 建立名為*Resources*的新資料夾來存放資源檔。
1. 在其中加入新的資源檔。 若要在 Visual Studio 中執行此動作，請以滑鼠右鍵按一下**方案總管**中的資料夾，**然後選取 [**  >  **新增專案**] [  >  **資源**] [檔案]。 將檔案命名為*ExceptionMessages .resx*。 這是預設的資源檔。
1. 新增例外狀況訊息的名稱/值組，如下圖所示：

   ![將資源新增至預設文化特性](media/add-resources-to-default-culture.jpg)

1. 新增法文的新資源檔。 將它命名*為 ExceptionMessages.fr-fr .resx*。
1. 再次新增例外狀況訊息的名稱/值組，但使用法文值：

   ![將資源新增至 fr-fr 文化特性](media/add-resources-to-fr-culture.jpg)

1. 在您建立專案之後，組建輸出檔案夾應該包含*fr-fr*資料夾，其為 *.dll*檔案，也就是附屬元件。
1. 您會擲回例外狀況，其程式碼如下所示：

    ```csharp
    var resourceManager = new ResourceManager("FULLY_QUALIFIED_NAME_OF_RESOURCE_FILE", Assembly.GetExecutingAssembly());
    throw new StudentNotFoundException(resourceManager.GetString("StudentNotFound"), "John");
    ```

    ```vb
    Dim resourceManager As New ResourceManager("FULLY_QUALIFIED_NAME_OF_RESOURCE_FILE", Assembly.GetExecutingAssembly())
    Throw New StudentNotFoundException(resourceManager.GetString("StudentNotFound"), "John")
    ```

    > [!NOTE]
    > 如果專案名稱是 `TestProject` ，而資源檔*ExceptionMessages*位於專案的*Resources*資料夾中，則資源檔的完整名稱是 `TestProject.Resources.ExceptionMessages` 。

## <a name="see-also"></a>另請參閱

- [如何建立使用者定義的例外狀況](how-to-create-user-defined-exceptions.md)
- [建立桌面應用程式的附屬組件](../../framework/resources/creating-satellite-assemblies-for-desktop-apps.md)
- [base (C# 參考)](../../csharp/language-reference/keywords/base.md)
- [this (C# 參考)](../../csharp/language-reference/keywords/this.md)
