---
title: 'cref 屬性-c # 程式設計指南'
description: 瞭解 cref 屬性。 Cref 屬性工作表示「程式碼參考」，而且會指定標記的內部文字是 code 元素。
ms.date: 07/20/2015
helpviewer_keywords:
- cref [C#]
ms.assetid: 66a6b0e5-b961-4504-a461-3a4cf481fc8b
ms.openlocfilehash: 31fa1a3f182d7b72a1dfbe1ce47386f87fbbff75
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87381992"
---
# <a name="cref-attribute-c-programming-guide"></a>cref 屬性（c # 程式設計手冊）

`cref` 屬性在 XML 文件標記中表示「程式碼參考」。 它會指定標記的內部文字是程式碼項目，例如類型、方法或屬性。 [DocFX](https://dotnet.github.io/docfx/) 和 [Sandcastle](https://github.com/EWSoftware/SHFB) 這類文件工具使用 `cref` 屬性自動產生記錄類型或成員的頁面超連結。

## <a name="example"></a>範例

下列範例顯示 `cref` 標記中使用的 [\<see>](./see.md) 屬性。

[!code-csharp[csProgGuideDocComments#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#3)]

編譯時，此程式會產生下列 XML 檔案。 請注意，以 `GetZero` 方法的 `cref` 屬性為例，已被編譯器轉換成 `"M:TestNamespace.TestClass.GetZero"`。 "M:" 前置詞表示「方法」，而且是能為 DocFX 和 Sandcastle 這類文件工具識別的慣例。 如需前置詞的完整清單，請參閱[處理 XML 檔案](./processing-the-xml-file.md)。

```xml  
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>CRefTest</name>
    </assembly>
    <members>
        <member name="T:TestNamespace.TestClass">
            <summary>
            TestClass contains several cref examples.
            </summary>
        </member>
        <member name="M:TestNamespace.TestClass.#ctor">
            <summary>
            This sample shows how to specify the <see cref="T:TestNamespace.TestClass"/> constructor as a cref attribute.
            </summary>
        </member>
        <member name="M:TestNamespace.TestClass.#ctor(System.Int32)">
            <summary>
            This sample shows how to specify the <see cref="M:TestNamespace.TestClass.#ctor(System.Int32)"/> constructor as a cref attribute.
            </summary>
        </member>
        <member name="M:TestNamespace.TestClass.GetZero">
            <summary>
            The GetZero method.
            </summary>
            <example>
            This sample shows how to call the <see cref="M:TestNamespace.TestClass.GetZero"/> method.
            <code>
            class TestClass
            {
                static int Main()
                {
                    return GetZero();
                }
            }
            </code>
            </example>
        </member>
        <member name="M:TestNamespace.TestClass.GetGenericValue``1(``0)">
            <summary>
            The GetGenericValue method.
            </summary>
            <remarks>
            This sample shows how to specify the <see cref="M:TestNamespace.TestClass.GetGenericValue``1(``0)"/> method as a cref attribute.
            </remarks>
        </member>
        <member name="T:TestNamespace.GenericClass`1">
            <summary>
            GenericClass.
            </summary>
            <remarks>
            This example shows how to specify the <see cref="T:TestNamespace.GenericClass`1"/> type as a cref attribute.
            </remarks>
        </member>
    </members>
</doc>
```

## <a name="see-also"></a>另請參閱

- [XML 文件註解](./index.md)
- [建議使用的文件註解標籤](./recommended-tags-for-documentation-comments.md)
