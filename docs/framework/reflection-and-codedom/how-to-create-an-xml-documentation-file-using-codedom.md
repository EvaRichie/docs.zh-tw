---
title: 如何：使用 CodeDOM 建立 XML 文件檔案
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CodeDOM, generating XML documentation
- XML documentation, creating using CodeDOM
- Code Document Object Model, generating XML documentation
ms.assetid: e3b80484-36b9-41dd-9d21-a2f9a36381dc
ms.openlocfilehash: b9e11a51048733dbfc42ff9f575e18effc80db07
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596242"
---
# <a name="how-to-create-an-xml-documentation-file-using-codedom"></a><span data-ttu-id="78c39-102">如何：使用 CodeDOM 建立 XML 檔檔案</span><span class="sxs-lookup"><span data-stu-id="78c39-102">How to: Create an XML documentation file using CodeDOM</span></span>

<span data-ttu-id="78c39-103">CodeDOM 可以用來建立會產生 XML 文件的程式碼。</span><span class="sxs-lookup"><span data-stu-id="78c39-103">CodeDOM can be used to create code that generates XML documentation.</span></span> <span data-ttu-id="78c39-104">此程序涉及建立包含 XML 文件註解的 CodeDOM 圖表、產生程式碼，以及編譯可建立 XML 文件輸出的以編譯器選項產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="78c39-104">The process involves creating the CodeDOM graph that contains the XML documentation comments, generating the code, and compiling the generated code with the compiler option that creates the XML documentation output.</span></span>  
  
## <a name="create-a-codedom-graph"></a><span data-ttu-id="78c39-105">建立 CodeDOM 圖形</span><span class="sxs-lookup"><span data-stu-id="78c39-105">Create a CodeDOM graph</span></span>
  
1. <span data-ttu-id="78c39-106">為範例應用程式建立包含 CodeDOM 圖形的 <xref:System.CodeDom.CodeCompileUnit>。</span><span class="sxs-lookup"><span data-stu-id="78c39-106">Create a <xref:System.CodeDom.CodeCompileUnit> containing the CodeDOM graph for the sample application.</span></span>  
  
2. <span data-ttu-id="78c39-107">使用 `docComment` 參數設定為 `true` 的 <xref:System.CodeDom.CodeCommentStatement.%23ctor%2A> 建構函式來建立 XML 文件註解項目和文字。</span><span class="sxs-lookup"><span data-stu-id="78c39-107">Use the <xref:System.CodeDom.CodeCommentStatement.%23ctor%2A> constructor with the `docComment` parameter set to `true` to create the XML documentation comment elements and text.</span></span>  
  
     [!code-csharp[CodeDomHelloWorldSample#4](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#4)]
     [!code-vb[CodeDomHelloWorldSample#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#4)]  
  
### <a name="generate-the-code-from-the-codecompileunit"></a><span data-ttu-id="78c39-108">從 CodeCompileUnit 產生程式碼</span><span class="sxs-lookup"><span data-stu-id="78c39-108">Generate the code from the CodeCompileUnit</span></span>
  
1. <span data-ttu-id="78c39-109">使用 <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> 方法來產生程式碼，並建立要編譯的來源檔案。</span><span class="sxs-lookup"><span data-stu-id="78c39-109">Use the <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> method to generate the code and create a source file to be compiled.</span></span>  
  
     [!code-csharp[CodeDomHelloWorldSample#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#5)]
     [!code-vb[CodeDomHelloWorldSample#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#5)]  
  
### <a name="compile-the-code-and-generate-the-documentation-file"></a><span data-ttu-id="78c39-110">編譯器代碼並產生檔檔</span><span class="sxs-lookup"><span data-stu-id="78c39-110">Compile the code and generate the documentation file</span></span>
  
1. <span data-ttu-id="78c39-111">將 **/doc** 編譯器選項新增至 <xref:System.CodeDom.Compiler.CompilerParameters> 物件的 <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> 屬性，並在編譯程式碼時將物件傳送至 <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> 方法建立 XML 文件檔。</span><span class="sxs-lookup"><span data-stu-id="78c39-111">Add the **/doc** compiler option to the <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> property of a <xref:System.CodeDom.Compiler.CompilerParameters> object and pass the object to the <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> method to create the XML documentation file when the code is compiled.</span></span>  
  
     [!code-csharp[CodeDomHelloWorldSample#6](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#6)]
     [!code-vb[CodeDomHelloWorldSample#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#6)]  
  
## <a name="example"></a><span data-ttu-id="78c39-112">範例</span><span class="sxs-lookup"><span data-stu-id="78c39-112">Example</span></span>

<span data-ttu-id="78c39-113">下列程式碼範例會建立有文件註解的 CodeDOM 圖表、從圖表產生程式碼檔案，以及編譯檔案並建立相關聯的 XML 文件檔案。</span><span class="sxs-lookup"><span data-stu-id="78c39-113">The following code example creates a CodeDOM graph with documentation comments, generates a code file from the graph, and compiles the file and creates an associated XML documentation file.</span></span>  
  
 [!code-csharp[CodeDomHelloWorldSample#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#1)]
 [!code-vb[CodeDomHelloWorldSample#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#1)]  
  
 <span data-ttu-id="78c39-114">程式碼範例會在*HelloWorldDoc*檔案中建立下列 xml 檔。</span><span class="sxs-lookup"><span data-stu-id="78c39-114">The code example creates the following XML documentation in the *HelloWorldDoc.xml* file.</span></span>  
  
```xml  
<?xml version="1.0" ?>
<doc>  
  <assembly>  
    <name>HelloWorld</name>
  </assembly>  
  <members>  
    <member name="T:Samples.Class1">  
      <summary>  
        Create a Hello World application.
      </summary>
      <seealso cref="M:Samples.Class1.Main" />
    </member>  
    <member name="M:Samples.Class1.Main">  
      <summary>  
        Main method for HelloWorld application.
        <para>Add a new paragraph to the description.</para>
      </summary>  
    </member>  
  </members>  
</doc>  
```  
  
## <a name="compile-permissions"></a><span data-ttu-id="78c39-115">編譯許可權</span><span class="sxs-lookup"><span data-stu-id="78c39-115">Compile permissions</span></span>
  
<span data-ttu-id="78c39-116">此程式碼範例需要設定 `FullTrust` 權限，才能順利執行。</span><span class="sxs-lookup"><span data-stu-id="78c39-116">This code example requires the `FullTrust` permission set to execute successfully.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="78c39-117">請參閱</span><span class="sxs-lookup"><span data-stu-id="78c39-117">See also</span></span>

- [<span data-ttu-id="78c39-118">使用 XML 記錄您的程式碼（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="78c39-118">Document your code with XML (Visual Basic)</span></span>](../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
- [<span data-ttu-id="78c39-119">XML 文件註解</span><span class="sxs-lookup"><span data-stu-id="78c39-119">XML documentation comments</span></span>](../../csharp/programming-guide/xmldoc/index.md)
- [<span data-ttu-id="78c39-120">XML 檔（c + +）</span><span class="sxs-lookup"><span data-stu-id="78c39-120">XML documentation (C++)</span></span>](/cpp/ide/xml-documentation-visual-cpp)
