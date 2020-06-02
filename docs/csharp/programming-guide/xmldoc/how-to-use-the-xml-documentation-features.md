---
title: '如何使用 XML 檔功能-c # 程式設計手冊'
ms.date: 06/01/2018
helpviewer_keywords:
- XML documentation [C#]
- C# language, XML documentation features
ms.assetid: 8f33917b-9577-4c9a-818a-640dbbb0b399
ms.openlocfilehash: b7c5a8a895271f067505496c0d13f98b66a393d9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287359"
---
# <a name="how-to-use-the-xml-documentation-features"></a><span data-ttu-id="6b33f-102">如何使用 XML 文件功能</span><span class="sxs-lookup"><span data-stu-id="6b33f-102">How to use the XML documentation features</span></span>

<span data-ttu-id="6b33f-103">下列範例提供已記載之類型的基本概觀。</span><span class="sxs-lookup"><span data-stu-id="6b33f-103">The following sample provides a basic overview of a type that has been documented.</span></span>

## <a name="example"></a><span data-ttu-id="6b33f-104">範例</span><span class="sxs-lookup"><span data-stu-id="6b33f-104">Example</span></span>

[!code-csharp[csProgGuideDocComments#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#15)]

<span data-ttu-id="6b33f-105">此範例會產生包含下列內容的 *.xml*檔案。</span><span class="sxs-lookup"><span data-stu-id="6b33f-105">The example generates an *.xml* file with the following contents.</span></span>

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>xmlsample</name>
    </assembly>
    <members>
        <member name="T:TestClass">
            <summary>
            Class level summary documentation goes here.
            </summary>
            <remarks>
            Longer comments can be associated with a type or member through
            the remarks tag.
            </remarks>
        </member>
        <member name="F:TestClass._name">
            <summary>
            Store for the Name property.
            </summary>
        </member>
        <member name="M:TestClass.#ctor">
            <summary>
            The class constructor.
            </summary>
        </member>
        <member name="P:TestClass.Name">
            <summary>
            Name property.
            </summary>
            <value>
            A value tag is used to describe the property value.
            </value>
        </member>
        <member name="M:TestClass.SomeMethod(System.String)">
            <summary>
            Description for SomeMethod.
            </summary>
            <param name="s"> Parameter description for s goes here.</param>
            <seealso cref="T:System.String">
            You can use the cref attribute on any tag to reference a type or member
            and the compiler will check that the reference exists.
            </seealso>
        </member>
        <member name="M:TestClass.SomeOtherMethod">
            <summary>
            Some other method.
            </summary>
            <returns>
            Return values are described through the returns tag.
            </returns>
            <seealso cref="M:TestClass.SomeMethod(System.String)">
            Notice the use of the cref attribute to reference a specific method.
            </seealso>
        </member>
        <member name="M:TestClass.Main(System.String[])">
            <summary>
            The entry point for the application.
            </summary>
            <param name="args"> A list of command line arguments.</param>
        </member>
        <member name="T:TestInterface">
            <summary>
            Documentation that describes the interface goes here.
            </summary>
            <remarks>
            Details about the interface go here.
            </remarks>
        </member>
        <member name="M:TestInterface.InterfaceMethod(System.Int32)">
            <summary>
            Documentation that describes the method goes here.
            </summary>
            <param name="n">
            Parameter n requires an integer argument.
            </param>
            <returns>
            The method returns an integer.
            </returns>
        </member>
    </members>
</doc>
```

## <a name="compiling-the-code"></a><span data-ttu-id="6b33f-106">編譯程式碼</span><span class="sxs-lookup"><span data-stu-id="6b33f-106">Compiling the code</span></span>

<span data-ttu-id="6b33f-107">若要編譯範例，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6b33f-107">To compile the example, enter the following command:</span></span>

`csc XMLsample.cs /doc:XMLsample.xml`

<span data-ttu-id="6b33f-108">此命令會建立 XML 檔案*xmlsample.xml*，您可以在瀏覽器中或使用命令來查看該檔案。 `TYPE`</span><span class="sxs-lookup"><span data-stu-id="6b33f-108">This command creates the XML file *XMLsample.xml*, which you can view in your browser or by using the `TYPE` command.</span></span>

## <a name="robust-programming"></a><span data-ttu-id="6b33f-109">穩固程式設計</span><span class="sxs-lookup"><span data-stu-id="6b33f-109">Robust programming</span></span>

<span data-ttu-id="6b33f-110">XML 檔的開頭為 `///` 。</span><span class="sxs-lookup"><span data-stu-id="6b33f-110">XML documentation starts with `///`.</span></span> <span data-ttu-id="6b33f-111">當您建立新的專案時，系統 `///` 會為您將一些入門行放在中。</span><span class="sxs-lookup"><span data-stu-id="6b33f-111">When you create a new project, the wizards put some starter `///` lines in for you.</span></span> <span data-ttu-id="6b33f-112">這些註解在處理時有一些限制：</span><span class="sxs-lookup"><span data-stu-id="6b33f-112">The processing of these comments has some restrictions:</span></span>

- <span data-ttu-id="6b33f-113">文件必須是語式正確的 XML。</span><span class="sxs-lookup"><span data-stu-id="6b33f-113">The documentation must be well-formed XML.</span></span> <span data-ttu-id="6b33f-114">如果 XML 的語式不正確，則會產生警告，而且文件檔案會包含註解，指出發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6b33f-114">If the XML is not well-formed, a warning is generated and the documentation file will contain a comment that says that an error was encountered.</span></span>

- <span data-ttu-id="6b33f-115">開發人員可以自由建立自己的標記集合。</span><span class="sxs-lookup"><span data-stu-id="6b33f-115">Developers are free to create their own set of tags.</span></span> <span data-ttu-id="6b33f-116">有一[組建議的標記](recommended-tags-for-documentation-comments.md)。</span><span class="sxs-lookup"><span data-stu-id="6b33f-116">There is a [recommended set of tags](recommended-tags-for-documentation-comments.md).</span></span> <span data-ttu-id="6b33f-117">其中一些建議的標記具有特殊意義：</span><span class="sxs-lookup"><span data-stu-id="6b33f-117">Some of the recommended tags have special meanings:</span></span>

  - <span data-ttu-id="6b33f-118">`<param>`標記是用來描述參數。</span><span class="sxs-lookup"><span data-stu-id="6b33f-118">The `<param>` tag is used to describe parameters.</span></span> <span data-ttu-id="6b33f-119">如果使用，編譯器會驗證參數存在，而且所有參數在文件中都有描述。</span><span class="sxs-lookup"><span data-stu-id="6b33f-119">If used, the compiler verifies that the parameter exists and that all parameters are described in the documentation.</span></span> <span data-ttu-id="6b33f-120">如果驗證失敗，編譯器會發出警告。</span><span class="sxs-lookup"><span data-stu-id="6b33f-120">If the verification fails, the compiler issues a warning.</span></span>

  - <span data-ttu-id="6b33f-121">`cref`屬性可以附加至任何標記，以參考程式碼元素。</span><span class="sxs-lookup"><span data-stu-id="6b33f-121">The `cref` attribute can be attached to any tag to reference a code element.</span></span> <span data-ttu-id="6b33f-122">編譯器會驗證此程式碼項目存在。</span><span class="sxs-lookup"><span data-stu-id="6b33f-122">The compiler verifies that this code element exists.</span></span> <span data-ttu-id="6b33f-123">如果驗證失敗，編譯器會發出警告。</span><span class="sxs-lookup"><span data-stu-id="6b33f-123">If the verification fails, the compiler issues a warning.</span></span> <span data-ttu-id="6b33f-124">編譯器在尋找 `cref` 屬性中所述的類型時，會遵守任何 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6b33f-124">The compiler respects any `using` statements when it looks for a type described in the `cref` attribute.</span></span>

  - <span data-ttu-id="6b33f-125">`<summary>`Visual Studio 內的 IntelliSense 會使用此標記來顯示類型或成員的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="6b33f-125">The `<summary>` tag is used by IntelliSense inside Visual Studio to display additional information about a type or member.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6b33f-126">XML 檔案不會提供類型和成員的完整資訊 (例如，它不會包含任何類型資訊)。</span><span class="sxs-lookup"><span data-stu-id="6b33f-126">The XML file does not provide full information about the type and members (for example, it does not contain any type information).</span></span> <span data-ttu-id="6b33f-127">若要取得有關類型或成員的完整資訊，請搭配實際類型或成員的反映使用檔檔。</span><span class="sxs-lookup"><span data-stu-id="6b33f-127">To get full information about a type or member, use the documentation file together with reflection on the actual type or member.</span></span>

## <a name="see-also"></a><span data-ttu-id="6b33f-128">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6b33f-128">See also</span></span>

- [<span data-ttu-id="6b33f-129">C# 程式設計手冊</span><span class="sxs-lookup"><span data-stu-id="6b33f-129">C# programming guide</span></span>](../index.md)
- [<span data-ttu-id="6b33f-130">-doc （c # 編譯器選項）</span><span class="sxs-lookup"><span data-stu-id="6b33f-130">-doc (C# compiler options)</span></span>](../../language-reference/compiler-options/doc-compiler-option.md)
- [<span data-ttu-id="6b33f-131">XML 文件註解</span><span class="sxs-lookup"><span data-stu-id="6b33f-131">XML documentation comments</span></span>](./index.md)
- [<span data-ttu-id="6b33f-132">DocFX 檔處理器</span><span class="sxs-lookup"><span data-stu-id="6b33f-132">DocFX documentation processor</span></span>](https://dotnet.github.io/docfx/)
- [<span data-ttu-id="6b33f-133">Sandcastle 這類檔處理器</span><span class="sxs-lookup"><span data-stu-id="6b33f-133">Sandcastle documentation processor</span></span>](https://github.com/EWSoftware/SHFB)
