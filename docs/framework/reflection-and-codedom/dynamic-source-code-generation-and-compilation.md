---
title: 動態原始程式碼的產生和編譯
description: 使用程式碼檔物件模型（CodeDOM）在 .NET 中編譯和產生動態原始程式碼。 CodeDOM 元素會連結以形成 CodeDOM 圖表。
ms.date: 03/30/2017
helpviewer_keywords:
- Code Document Object Model
- System.CodeDom namespace
- language-independent source code modeling
- CodeDOM
- multiple languages supported by CodeDOM
- source code in multiple languages
- languages, multiple language support by CodeDOM
ms.assetid: d077a3e8-bd81-4bdf-b6a3-323857ea30fb
ms.openlocfilehash: 3cdd89ac9745f6af133ca683afff64283f2727d1
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/20/2020
ms.locfileid: "86475095"
---
# <a name="compile-and-generate-dynamic-source-code"></a><span data-ttu-id="22a71-104">編譯並產生動態原始程式碼</span><span class="sxs-lookup"><span data-stu-id="22a71-104">Compile and generate dynamic source code</span></span>

<span data-ttu-id="22a71-105">.NET Framework 包含稱為程式碼文件物件模型 (CodeDOM) 的機制，它可讓發出原始程式碼的程式開發人員在執行階段，根據代表要呈現之程式碼的單一模型，產生多種程式語言的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="22a71-105">The .NET Framework includes a mechanism called the Code Document Object Model (CodeDOM) that enables developers of programs that emit source code to generate source code in multiple programming languages at run time, based on a single model that represents the code to render.</span></span>  
  
<span data-ttu-id="22a71-106">為了代表原始程式碼，CodeDOM 項目會彼此連結，形成稱為 CodeDOM 圖形的資料結構，它會建立一些原始程式碼結構的模型。</span><span class="sxs-lookup"><span data-stu-id="22a71-106">To represent source code, CodeDOM elements are linked to each other to form a data structure known as a CodeDOM graph, which models the structure of some source code.</span></span>  
  
<span data-ttu-id="22a71-107"><xref:System.CodeDom?displayProperty=fullName> 命名空間會定義類型，可代表獨立於特定程式設計語言的原始碼邏輯結構。</span><span class="sxs-lookup"><span data-stu-id="22a71-107">The <xref:System.CodeDom?displayProperty=fullName> namespace defines types that can represent the logical structure of source code, independent of a specific programming language.</span></span> <span data-ttu-id="22a71-108"><xref:System.CodeDom.Compiler?displayProperty=fullName> 命名空間會定義類型，以從 CodeDOM 圖表產生原始程式碼，以及管理使用支援語言的原始程式碼編譯。</span><span class="sxs-lookup"><span data-stu-id="22a71-108">The <xref:System.CodeDom.Compiler?displayProperty=fullName> namespace defines types for generating source code from CodeDOM graphs and managing the compilation of source code in supported languages.</span></span> <span data-ttu-id="22a71-109">編譯器廠商或開發人員可以擴充支援的語言集。</span><span class="sxs-lookup"><span data-stu-id="22a71-109">Compiler vendors or developers can extend the set of supported languages.</span></span>  
  
<span data-ttu-id="22a71-110">程式需要產生適用於多種語言的程式模型原始程式碼，或是不確定目標語言的原始程式碼時，很適合使用與語言無關的原始程式碼模型。</span><span class="sxs-lookup"><span data-stu-id="22a71-110">Language-independent source code modeling can be valuable when a program needs to generate source code for a program model in multiple languages or for an uncertain target language.</span></span> <span data-ttu-id="22a71-111">比方說，某些設計工具使用 CodeDOM 作為語言抽象介面，以正確的程式設計語言產生程式碼，如果該語言支援 CodeDOM 的話。</span><span class="sxs-lookup"><span data-stu-id="22a71-111">For example, some designers use the CodeDOM as a language abstraction interface to produce source code in the correct programming language, if CodeDOM support for the language is available.</span></span>  
  
<span data-ttu-id="22a71-112">.NET Framework 包含 <xref:Microsoft.CSharp.CSharpCodeProvider>、<xref:Microsoft.JScript.JScriptCodeProvider> 和 <xref:Microsoft.VisualBasic.VBCodeProvider> 的程式碼產生器和程式碼編譯器。</span><span class="sxs-lookup"><span data-stu-id="22a71-112">The .NET Framework includes code generators and code compilers for <xref:Microsoft.CSharp.CSharpCodeProvider>, <xref:Microsoft.JScript.JScriptCodeProvider>, and <xref:Microsoft.VisualBasic.VBCodeProvider>.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="22a71-113">本節內容</span><span class="sxs-lookup"><span data-stu-id="22a71-113">In this section</span></span>

- [<span data-ttu-id="22a71-114">使用 CodeDOM</span><span class="sxs-lookup"><span data-stu-id="22a71-114">Using the CodeDOM</span></span>](using-the-codedom.md)

  <span data-ttu-id="22a71-115">說明常見的用法，並示範使用 CodeDOM 建置簡單的物件圖形。</span><span class="sxs-lookup"><span data-stu-id="22a71-115">Describes common uses, and demonstrates building a simple object graph using the CodeDOM.</span></span>  
  
- [<span data-ttu-id="22a71-116">從 CodeDOM 圖表產生原始程式碼並編譯器</span><span class="sxs-lookup"><span data-stu-id="22a71-116">Generate Source Code and Compile a Program from a CodeDOM Graph</span></span>](generating-and-compiling-source-code-from-a-codedom-graph.md)  

  <span data-ttu-id="22a71-117">描述如何產生原始程式碼，和使用外部編譯器以及 `System.CodeDom.Compiler` 命名空間中定義的類別編譯產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="22a71-117">Describes how to generate source code and compile the generated code with an external compiler using classes defined in the `System.CodeDom.Compiler` namespace.</span></span>  
  
- [<span data-ttu-id="22a71-118">如何：使用 CodeDOM 建立 XML 文件檔案</span><span class="sxs-lookup"><span data-stu-id="22a71-118">How to: Create an XML Documentation File Using CodeDOM</span></span>](how-to-create-an-xml-documentation-file-using-codedom.md)  

  <span data-ttu-id="22a71-119">描述如何使用 CodeDOM 產生程式碼和 XML 文件註解，並編譯產生的程式碼，以建立 XML 文件輸出。</span><span class="sxs-lookup"><span data-stu-id="22a71-119">Describes how to use CodeDOM to generate code with XML documentation comments, and compile the generated code so that it creates the XML documentation output.</span></span>  
  
- [<span data-ttu-id="22a71-120">如何：使用 CodeDOM 建立類別</span><span class="sxs-lookup"><span data-stu-id="22a71-120">How to: Create a Class Using CodeDOM</span></span>](how-to-create-a-class-using-codedom.md)  

  <span data-ttu-id="22a71-121">描述如何使用 CodeDOM 產生包含欄位、屬性、方法、建構函式和進入點的類別。</span><span class="sxs-lookup"><span data-stu-id="22a71-121">Describes how to use CodeDOM to generate a class containing fields, properties, a method, a constructor, and an entry point.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="22a71-122">參考</span><span class="sxs-lookup"><span data-stu-id="22a71-122">Reference</span></span>  

- <xref:System.CodeDom>  

  <span data-ttu-id="22a71-123">定義元素，代表以 Common Language Runtime 為目標之程式設計語言中的程式碼元素。</span><span class="sxs-lookup"><span data-stu-id="22a71-123">Defines elements that represent code elements in programming languages that target the common language runtime.</span></span>  
  
- <xref:System.CodeDom.Compiler>  

  <span data-ttu-id="22a71-124">定義介面以便在執行階段產生和編譯程式碼。</span><span class="sxs-lookup"><span data-stu-id="22a71-124">Defines interfaces for generating and compiling code at run time.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="22a71-125">相關章節</span><span class="sxs-lookup"><span data-stu-id="22a71-125">Related sections</span></span>  

- <span data-ttu-id="22a71-126">[Codedom 快速參考](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100))提供了一種快速的方法，讓開發人員尋找代表原始程式碼元素的 CodeDOM 元素。</span><span class="sxs-lookup"><span data-stu-id="22a71-126">[CodeDOM Quick Reference](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100)) provides a quick way for developers to find the CodeDOM elements that represent source code elements.</span></span>
