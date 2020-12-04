---
description: using 指示詞 - C# 參考
title: using 指示詞 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- using_CSharpKeyword
helpviewer_keywords:
- using directive [C#]
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
ms.openlocfilehash: 77d9c894dae9adc24343ce3a639a4afb904fb0a1
ms.sourcegitcommit: 9d525bb8109216ca1dc9e39c149d4902f4b43da5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/04/2020
ms.locfileid: "96599405"
---
# <a name="using-directive-c-reference"></a>using 指示詞 (C# 參考)

`using` 指示詞有三個用途：

- 若要允許在命名空間中使用類型，使得您不需限定在該命名空間中使用的類型：

    ```csharp
    using System.Text;
    ```

- 允許您存取類型的靜態成員和巢狀類型，但不必以類型名稱限定存取。

    ```csharp
    using static System.Math;
    ```

    如需詳細資訊，請參閱 [using static 指示詞](using-static.md)。

- 若要建立命名空間或類型的別名。 這稱為 *using alias 指示詞*。

    ```csharp
    using Project = PC.MyCompany.Project;
    ```

`using` 關鍵字也用來建立 *using 陳述式*，協助確保能夠正確處理 <xref:System.IDisposable> 物件 (例如檔案和字型)。 如需詳細資訊，請參閱 [using 陳述式](using-statement.md)。

## <a name="using-static-type"></a>Using static 類型

您可以存取類型的靜態成員，而不需以類型名稱限定存取：

```csharp
using static System.Console;
using static System.Math;
class Program
{
    static void Main()
    {
        WriteLine(Sqrt(3*3 + 4*4));
    }
}
```

## <a name="remarks"></a>備註

`using` 指示詞的範圍僅限於其出現的檔案。

`using` 指示詞會出現：

- 位於原始程式碼檔的開頭，在任何命名空間或類型定義之前。
- 在任何命名空間中，但在任何命名空間或類型於此命名空間宣告之前。

否則，就會發生編譯器錯誤 [CS1529](../../misc/cs1529.md)。

建立 `using` 別名指示詞，讓您更輕鬆地將識別碼限定在命名空間或類型。 在任何 `using` 指示詞中，必須使用完整的命名空間或類型，不論 `using` 指示詞是否在它前面。 `using` 指示詞的宣告中不可使用任何 `using` 別名。 例如，下列內容會產生編譯器錯誤：

```csharp
using s = System.Text;
using s.RegularExpressions; // Generates a compiler error.
```

建立 `using` 指示詞，以在命名空間中使用類型，而無需指定命名空間。 `using` 指示詞不會授予巢狀於您指定的命名空間中的任何命名空間的存取權。

命名空間有兩種類型：使用者定義和系統定義。 使用者定義的命名空間是在程式碼中定義的命名空間。 如需系統定義的命名空間清單，請參閱 [.NET API 瀏覽器](../../../../api/index.md)。

## <a name="example-1"></a>範例 1

下列範例示範如何定義和使用命名空間的 `using` 別名：

[!code-csharp[csrefKeywordsNamespace#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace2.cs#8)]

using alias 指示詞的右邊不能有開放式的泛型類型。 例如，您無法為 `List<T>` 建立 using 別名，但是可以為 `List<int>` 建立。

## <a name="example-2"></a>範例 2

下列範例示範如何定義類別的 `using` 指示詞和 `using` 別名：

[!code-csharp[csrefKeywordsNamespace#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsNamespace/CS/csrefKeywordsNamespace2.cs#9)]

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)的 [Using 指示詞](~/_csharplang/spec/namespaces.md#using-directives)。 語言規格是 C# 語法及用法的限定來源。

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [使用命名空間](../../programming-guide/namespaces/using-namespaces.md)
- [C # 關鍵字](index.md)
- [命名空間](../../programming-guide/namespaces/index.md)
- [using 陳述式](using-statement.md)
