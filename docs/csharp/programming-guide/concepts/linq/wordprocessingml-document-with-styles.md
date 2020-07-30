---
title: WordprocessingML 文件以及樣式
description: 這個範例 WordprocessingML 檔包含使用樣式格式化的段落。 瞭解樣式的相關檔部分。
ms.date: 07/20/2015
ms.assetid: 40e35de6-ac93-4bba-88ab-a018cbe93873
ms.openlocfilehash: b799c1bee95d7d638e6a3210b4876ff036e088eb
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302200"
---
# <a name="wordprocessingml-document-with-styles"></a><span data-ttu-id="85472-104">WordprocessingML 文件以及樣式</span><span class="sxs-lookup"><span data-stu-id="85472-104">WordprocessingML Document with Styles</span></span>
<span data-ttu-id="85472-105">更複雜的 WordprocessingML 文件擁有使用樣式格式化的段落。</span><span class="sxs-lookup"><span data-stu-id="85472-105">More complicated WordprocessingML documents have paragraphs that are formatted with styles.</span></span>  
  
 <span data-ttu-id="85472-106">關於 WordprocessingML 文件結構的一些注意事項將很有幫助。</span><span class="sxs-lookup"><span data-stu-id="85472-106">A few notes about the makeup of WordprocessingML documents are helpful.</span></span> <span data-ttu-id="85472-107">WordprocessingML 文件會儲存在封裝中。</span><span class="sxs-lookup"><span data-stu-id="85472-107">WordprocessingML documents are stored in packages.</span></span> <span data-ttu-id="85472-108">這些封裝有多個部分 (用於封裝內容時，這些封裝擁有明確的意義、基本上，這些部分是壓縮在一起以組成封裝的檔案)。</span><span class="sxs-lookup"><span data-stu-id="85472-108">Packages have multiple parts (parts have an explicit meaning when used in the context of packages; essentially, parts are files that are zipped together to comprise a package).</span></span> <span data-ttu-id="85472-109">如果文件包含使用樣式格式化的段落，將會有一個文件部分包含已套用樣式的段落。</span><span class="sxs-lookup"><span data-stu-id="85472-109">If a document contains paragraphs that are formatted with styles, there will be a document part that contains paragraphs that have styles applied to them.</span></span> <span data-ttu-id="85472-110">同時，也會有包含文件所參考之樣式的樣式部分。</span><span class="sxs-lookup"><span data-stu-id="85472-110">There will also be a style part that contains the styles that are referred to by the document.</span></span>  
  
 <span data-ttu-id="85472-111">存取封裝時，最好透過這些部分之間的關聯性 (而非使用任意路徑) 進行。</span><span class="sxs-lookup"><span data-stu-id="85472-111">When accessing packages, it is important that you do so through the relationships between parts, rather than using an arbitrary path.</span></span> <span data-ttu-id="85472-112">這個問題超出＜管理 WordprocessingML 文件中的內容＞教學課程的範圍，但隨附在此教學課程中的範例程式會示範正確的方法。</span><span class="sxs-lookup"><span data-stu-id="85472-112">This issue is beyond the scope of the Manipulating Content in a WordprocessingML Document tutorial, but the example programs that are included in this tutorial demonstrate the correct approach.</span></span>  
  
## <a name="a-document-that-uses-styles"></a><span data-ttu-id="85472-113">使用樣式的文件</span><span class="sxs-lookup"><span data-stu-id="85472-113">A Document that Uses Styles</span></span>  
 <span data-ttu-id="85472-114">顯示在 [WordprocessingML 文件的組織結構 (C#)](./shape-of-wordprocessingml-documents.md) 主題中的 WordML 範例相當簡單。</span><span class="sxs-lookup"><span data-stu-id="85472-114">The WordML example presented in the [Shape of WordprocessingML Documents (C#)](./shape-of-wordprocessingml-documents.md) topic is a very simple one.</span></span> <span data-ttu-id="85472-115">下列文件較為複雜：該文件擁有使用樣式格式化的段落。</span><span class="sxs-lookup"><span data-stu-id="85472-115">The following document is more complicated: It has paragraphs that are formatted with styles.</span></span> <span data-ttu-id="85472-116">查看組成 Office Open XML 文件之 XML 的最簡單方式是執行[輸出 Office Open XML 文件部分內容的範例 (C#)](./example-that-outputs-office-open-xml-document-parts.md)。</span><span class="sxs-lookup"><span data-stu-id="85472-116">The easiest way to see the XML that makes up an Office Open XML document is to run the [Example that Outputs Office Open XML Document Parts (C#)](./example-that-outputs-office-open-xml-document-parts.md).</span></span>  
  
 <span data-ttu-id="85472-117">在下列文件中，第一個段落的樣式為 `Heading1`。</span><span class="sxs-lookup"><span data-stu-id="85472-117">In the following document, the first paragraph has the style `Heading1`.</span></span> <span data-ttu-id="85472-118">具有預設樣式的段落有好幾個。</span><span class="sxs-lookup"><span data-stu-id="85472-118">There are a number of paragraphs that have the default style.</span></span> <span data-ttu-id="85472-119">同時，具有樣式 `Code` 的段落也有好幾個。</span><span class="sxs-lookup"><span data-stu-id="85472-119">There are also a number of paragraphs that have the style `Code`.</span></span> <span data-ttu-id="85472-120">由於這個相對複雜度，這是利用 LINQ to XML 進行剖析更有趣的文件。</span><span class="sxs-lookup"><span data-stu-id="85472-120">Because of this relative complexity, this is a more interesting document to parse with LINQ to XML.</span></span>  
  
 <span data-ttu-id="85472-121">在具有非預設樣式的段落中，段落項目擁有一個名稱為 `w:pPr` 的子項目，而該子項目的子項目為 `w:pStyle`。</span><span class="sxs-lookup"><span data-stu-id="85472-121">In those paragraphs with non-default styles, the paragraph elements have a child element named `w:pPr`, which in turn has a child element `w:pStyle`.</span></span> <span data-ttu-id="85472-122">該項目所擁有的屬性 `w:val` 包含樣式名稱。</span><span class="sxs-lookup"><span data-stu-id="85472-122">That element has an attribute, `w:val`, which contains the style name.</span></span> <span data-ttu-id="85472-123">如果段落具有預設樣式，表示該段落項目沒有 `w:p.Pr` 子項目。</span><span class="sxs-lookup"><span data-stu-id="85472-123">If the paragraph has the default style, it means that the paragraph element does not have a `w:p.Pr` child element.</span></span>  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<w:document  
    xmlns:ve="http://schemas.openxmlformats.org/markup-compatibility/2006"  
    xmlns:o="urn:schemas-microsoft-com:office:office"  
    xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"  
    xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math"  
    xmlns:v="urn:schemas-microsoft-com:vml"  
    xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing"  
    xmlns:w10="urn:schemas-microsoft-com:office:word"  
    xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
    xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml">  
  <w:body>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Heading1" />  
      </w:pPr>  
      <w:r>  
        <w:t>Parsing WordprocessingML with LINQ to XML</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" />  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0">  
      <w:r>  
        <w:t>The following example prints to the console.</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" />  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r>  
        <w:t>using System;</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t>class Program {</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t xml:space="preserve">    public static void </w:t>  
      </w:r>  
      <w:smartTag w:uri="urn:schemas-microsoft-com:office:smarttags" w:element="place">  
        <w:r w:rsidRPr="00876F34">  
          <w:t>Main</w:t>  
        </w:r>  
      </w:smartTag>  
      <w:r w:rsidRPr="00876F34">  
        <w:t>(string[] args) {</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t xml:space="preserve">        Console.WriteLine("Hello World");</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t xml:space="preserve">    }</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t>}</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" />  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0">  
      <w:r>  
        <w:t>This example produces the following output:</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" />  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r>  
        <w:t>Hello World</w:t>  
      </w:r>  
    </w:p>  
    <w:sectPr w:rsidR="00A75AE0" w:rsidSect="00A75AE0">  
      <w:pgSz w:w="12240" w:h="15840" />  
      <w:pgMar w:top="1440" w:right="1800" w:bottom="1440" w:left="1800" w:header="720" w:footer="720" w:gutter="0" />  
      <w:cols w:space="720" />  
      <w:docGrid w:linePitch="360" />  
    </w:sectPr>  
  </w:body>  
</w:document>  
```  
