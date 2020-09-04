---
title: 使用 XML 註解記錄您的程式碼
description: 了解如何使用 XML 文件註解記錄您的程式碼，並在編譯時期產生 XML 文件檔案。
ms.date: 01/21/2020
ms.technology: csharp-fundamentals
ms.assetid: 8e75e317-4a55-45f2-a866-e76124171838
ms.openlocfilehash: 91de11c610ea17999dabff6d0552de9440f532e6
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465295"
---
# <a name="document-your-code-with-xml-comments"></a>使用 XML 批註記錄您的程式碼

XML 文件註解是一種特殊類型的註解，新增於任何使用者定義型別或成員的定義上方。
XML 文件註解具特殊性，因為編譯器可以處理它們以在編譯時期產生 XML 文件檔案。
編譯器產生的 XML 檔案可以與您的 .NET 元件一起散發，讓 Visual Studio 和其他 Ide 可以使用 IntelliSense 來顯示類型或成員的快速資訊。 此外，可以透過 [DocFX](https://dotnet.github.io/docfx/) 和 [Sandcastle](https://github.com/EWSoftware/SHFB) 這類工具執行 XML 檔案來產生 API 參考網站。

編譯器會忽略 XML 文件註解 (例如所有其他註解)。

您可以執行下列其中一項動作，以在編譯時期產生 XML 檔案︰

- 如果您要從命令列使用 .NET Core 開發應用程式，您可以將專案加入 `GenerateDocumentationFile` 至 `<PropertyGroup>` .csproj 專案檔的區段。 您也可以直接使用[ `DocumentationFile` 元素](/visualstudio/msbuild/common-msbuild-project-properties)來指定檔檔的路徑。 下列範例會在根檔案名稱與組件相同的專案目錄中產生 XML 檔案：

   ```xml
   <GenerateDocumentationFile>true</GenerateDocumentationFile>
   ```

   這個運算式就相當於下列運算式：

   ```xml
   <DocumentationFile>bin\$(Configuration)\$(TargetFramework)\$(AssemblyName).xml</DocumentationFile>
   ```

- 如果您正在使用 Visual Studio 開發應用程式，請以滑鼠右鍵按一下專案，然後選取 [屬性]****。 在屬性對話方塊中，選取 [建置]**** 索引標籤，然後檢查 [XML 文件檔案]****。 您也可以變更編譯器寫入檔案的位置。

- 如果您是從命令列編譯 .NET 應用程式，請在編譯時加入 [-doc 編譯器選項](language-reference/compiler-options/doc-compiler-option.md) 。  

XML 文件註解使用三個正斜線 (`///`) 和 XML 格式化註解主體。 例如：

[!code-csharp[XML Documentation Comment](../../samples/snippets/csharp/concepts/codedoc/xml-comment.cs)]

## <a name="walkthrough"></a>逐步介紹

讓我們逐步解說一個非常基本的數學程式庫，讓新的開發人員可以輕鬆地瞭解/參與，並讓協力廠商開發人員使用。

以下是簡單數學程式庫的程式碼︰

[!code-csharp[Sample Library](../../samples/snippets/csharp/concepts/codedoc/sample-library.cs)]

範例程式庫支援四個主要算數運算 (`add` 、 `subtract` 、 `multiply` 和 `divide`) `int` 和 `double` 資料類型。

現在您想要能夠從您的程式碼建立 API 參考檔，以供使用程式庫但無法存取原始程式碼的協力廠商開發人員使用。
如先前所述，XML 文件標籤可以用來達到此目的。 現在將向您介紹 C# 編譯器支援的標準 XML 標籤。

## \<summary>

`<summary>` 標記會新增類型或成員的簡短資訊。
我會將它新增至 `Math` 類別定義和第一個 `Add` 方法來示範其使用方式。 請自由套用至您程式碼的其餘部分。

[!code-csharp[Summary Tag](~/samples/snippets/csharp/concepts/codedoc/summary-tag.cs)]

`<summary>`標記很重要，我們建議您將其納入，因為它的內容是 IntelliSense 或 API 參考檔中類型或成員資訊的主要來源。

## \<remarks>

`<remarks>` 標記會補充 `<summary>` 標記所提供的類型或成員的相關資訊。 在此範例中，您只會將它新增至類別。

[!code-csharp[Remarks Tag](~/samples/snippets/csharp/concepts/codedoc/remarks-tag.cs)]

## \<returns>

`<returns>` 標記描述方法宣告的傳回值。
如前所示，下列範例說明第一個 `Add` 方法的 `<returns>` 標記。 您可以對其他方法執行相同作業。

[!code-csharp[Returns Tag](~/samples/snippets/csharp/concepts/codedoc/returns-tag.cs)]

## \<value>

`<value>` 標記類似於 `<returns>` 標記，但將它用作屬性除外。
假設 `Math` 程式庫的靜態屬性稱為 `PI`，以下是使用這個標記的方式：

[!code-csharp[Value Tag](~/samples/snippets/csharp/concepts/codedoc/value-tag.cs)]

## \<example>

您可以使用 `<example>` 標記，以在 XML 文件中包括範例。
這包含如何使用子 `<code>` 標記。

[!code-csharp[Example Tag](~/samples/snippets/csharp/concepts/codedoc/example-tag.cs)]

`code` 標記會保留分行符號以及較長範例的縮排。

## \<para>

您可以使用 `<para>` 標記來格式化其父標記內的內容。 `<para>` 通常用於標記內 (例如 `<remarks>` 或 `<returns>`)，以將文字分成數個段落。
您可以格式化類別定義的 `<remarks>` 標記內容。

[!code-csharp[Para Tag](~/samples/snippets/csharp/concepts/codedoc/para-tag.cs)]

## \<c>

仍然，在有關格式化的主題，您可以使用 `<c>` 標記將一部分文字標記為程式碼。
它就像 `<code>` 標記，只是會內嵌。 這適用於您想要將快速程式碼範例顯示為標記內容的一部分時。
請更新 `Math` 類別的文件。

[!code-csharp[C Tag](~/samples/snippets/csharp/concepts/codedoc/c-tag.cs)]

## \<exception>

使用 `<exception>` 標記，讓您的開發人員知道方法可以擲回特定例外狀況。
查看 `Math` 程式庫，即可看到兩個 `Add` 方法在符合特定條件時擲回例外狀況。 雖然不明顯，但如果 `b` 參數為零，則也會擲回整數 `Divide` 方法。 現在將例外狀況文件新增至這個方法。

[!code-csharp[Exception Tag](~/samples/snippets/csharp/concepts/codedoc/exception-tag.cs)]

`cref` 屬性代表可從目前編譯環境取得之例外狀況的參考。
這可以是專案或已參考組件中所定義的任何類型。 如果無法解析其值，編譯器會發出警告。

## \<see>

`<see>` 標記可讓您建立另一個程式碼項目之文件頁面的可按式連結。 在下一個範例中，我們將在兩個 `Add` 方法之間建立可按式連結。

[!code-csharp[See Tag](~/samples/snippets/csharp/concepts/codedoc/see-tag.cs)]

`cref` 為**必要**屬性，代表可從目前編譯環境取得的類型或其成員的參考。
這可以是專案或已參考組件中所定義的任何類型。

## \<seealso>

`<seealso>` 標記的使用方式與 `<see>` 標記的使用方式相同。 唯一的差異在於它的內容一般會放在＜另請參閱＞一節中。 在這裡，我們將在整數 `Add` 方法上新增 `seealso` 標記，以參考類別中接受整數參數的其他方法：

[!code-csharp[Seealso Tag](~/samples/snippets/csharp/concepts/codedoc/seealso-tag.cs)]

`cref` 屬性代表可從目前編譯環境取得的類型或其成員的參考。
這可以是專案或已參考組件中所定義的任何類型。

## \<param>

您可以使用 `<param>` 標記來描述方法的參數。 以下是雙 `Add` 方法的範例：標記所描述的屬性指定於**必要的** `name` 屬性中。

[!code-csharp[Param Tag](~/samples/snippets/csharp/concepts/codedoc/param-tag.cs)]

## \<typeparam>

您可以就像使用 `<param>` 標記一樣地使用 `<typeparam>` 標記，但針對泛型型別或方法宣告來描述泛型參數。
請將快速泛型方法新增至 `Math` 類別，以檢查其中一個數量是否大於另一個數量。

[!code-csharp[Typeparam Tag](~/samples/snippets/csharp/concepts/codedoc/typeparam-tag.cs)]

## \<paramref>

您有時可能正在描述方法在 `<summary>` 標記中所執行的作業，而且您可能會想要參考參數。 則 `<paramref>` 標記最適合這麼做。 讓我們更新雙 `Add` 方法的摘要。 就像 `<param>` 標記一樣，參數名稱是在 **必要** `name` 屬性中指定。

[!code-csharp[Paramref Tag](~/samples/snippets/csharp/concepts/codedoc/paramref-tag.cs)]

## \<typeparamref>

您可以就像使用 `<paramref>` 標記一樣地使用 `<typeparamref>` 標記，但針對泛型型別或方法宣告來描述泛型參數。
您可以使用先前建立的相同泛型方法。

[!code-csharp[Typeparamref Tag](~/samples/snippets/csharp/concepts/codedoc/typeparamref-tag.cs)]

## \<list>

您可以使用 `<list>` 標記，將檔資訊格式化為排序的清單、未排序的清單或資料表。 建立 `Math` 程式庫所支援的未排序數學運算清單。

[!code-csharp[List Tag](~/samples/snippets/csharp/concepts/codedoc/list-tag.cs)]

您可以分別將 `type` 屬性變更為 `number` 或 `table`，以建立排序過的清單或表格。

## \<inheritdoc>

您可以使用 `<inheritdoc>` 標記，從基類、介面和類似的方法繼承 XML 批註。 這可避免不必要的複製和貼上重複的 XML 批註，並自動保持 XML 批註的同步。

[!code-csharp-interactive[InheritDoc Tag](~/samples/snippets/csharp/concepts/codedoc/inheritdoc-tag.cs)]

### <a name="put-it-all-together"></a>組合在一起

如已遵循本教學課程，並已在必要時將標記套用至程式碼，則程式碼現在看起來應該如下︰

[!code-csharp[Tagged Library](~/samples/snippets/csharp/concepts/codedoc/tagged-library.cs)]

從程式碼中，您可以產生使用可按式交互參照完成的詳細文件網站。 但您會面臨另一個問題︰您的程式碼變得難以閱讀。
因為有太多資訊需要仔細檢查，這會是想要參與這個程式碼之開發人員的夢魘。
還好有 XML 標記可協助您處理這個問題︰

## \<include>

`<include>` 標記可讓您參考個別 XML 檔案中描述原始程式碼中類型和成員的註解，這與直接在原始程式碼檔中放置文件註解相反。

您現在要將所有 XML 標記移至名為 `docs.xml` 的個別 XML 檔案。 請放心以您想要的名稱來命名檔案。

[!code-xml[Sample XML](~/samples/snippets/csharp/concepts/codedoc/include.xml)]

在上述 XML 中，每個成員的文件註解都會直接顯示在執行動作之後所命名的標記內。 您可以選擇自己的策略。
現在，您的 XML 註解位於在不同的檔案中，請查看如何使用 `<include>` 標記讓您的程式碼更容易閱讀：

[!code-csharp[Include Tag](~/samples/snippets/csharp/concepts/codedoc/include-tag.cs)]

目前您已經準備好了：我們的程式碼又再次為可讀，而且未遺失文件資訊。

`file` 屬性代表包含文件的 XML 檔案名稱。

`path` 屬性代表存在於所指定 `file` 中之 `tag name` 的 [XPath](../standard/data/xml/xpath-queries-and-namespaces.md) 查詢。

`name` 屬性代表標記中位在註解前面的名稱規範。

`id`可以用來取代的屬性， `name` 代表在批註前面的標記識別項。

### <a name="user-defined-tags"></a>使用者定義標記

以上所述的所有標記都代表 C# 編譯器所辨識的標記。 不過，使用者可以定義自己的標記。
>sandcastle 之類的工具可支援和等額外 [\<event>](https://ewsoftware.github.io/XMLCommentsGuide/html/81bf7ad3-45dc-452f-90d5-87ce2494a182.htm) 標記 [\<note>](https://ewsoftware.github.io/XMLCommentsGuide/html/4302a60f-e4f4-4b8d-a451-5f453c4ebd46.htm) ，甚至支援 [記錄命名空間](https://ewsoftware.github.io/XMLCommentsGuide/html/BD91FAD4-188D-4697-A654-7C07FD47EF31.htm)。
自訂或內部文件產生工具也可以與標準標記搭配使用，而且可以支援從 HTML 到 PDF 的多個輸出格式。

## <a name="recommendations"></a>建議

有許多原因，建議您記錄程式碼。 接下來是一些最佳做法、一般使用案例，以及在 C# 程式碼中使用 XML 文件標記時應該知道的事項。

- 為保持一致性，應該記錄所有公開可見的類型和其成員。 如果您必須執行它，則請執行。
- 也可以使用 XML 註解記錄私用成員。 不過，這樣會公開您程式庫的內部 (可能是機密) 運作。
- 類型和其成員最少應該具有 `<summary>` 標記，因為 IntelliSense 需要其內容。
- 應該使用結尾為句號的完整句子來撰寫文件文字。
- 完全支援部分類別，而且文件資訊將會串連為該類型的單一項目。
- 編譯器會驗證、、、、 `<exception>` `<include>` `<param>` `<see>` `<seealso>` 和 `<typeparam>` 標記的語法。
- 編譯器會驗證包含程式碼其他部分的檔案路徑和參考的參數。

## <a name="see-also"></a>另請參閱

- [XML 檔批註 (c # 程式設計手冊) ](programming-guide/xmldoc/index.md)
- [建議使用的文件註解標籤 (C# 程式設計手冊)](programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
