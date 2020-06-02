---
title: XslTransform 類別實作 XSLT 處理器
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 88373fe2-4a6b-44f9-8a62-8a3e348e3a46
ms.openlocfilehash: eec5d6588d907e2d12b588ab3bfe743d6d1eaff9
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281605"
---
# <a name="xsltransform-class-implements-the-xslt-processor"></a><span data-ttu-id="d0c16-102">XslTransform 類別實作 XSLT 處理器</span><span class="sxs-lookup"><span data-stu-id="d0c16-102">XslTransform Class Implements the XSLT Processor</span></span>

> [!NOTE]
> <span data-ttu-id="d0c16-103">在 .NET Framework 2.0 中，<xref:System.Xml.Xsl.XslTransform> 類別已過時。</span><span class="sxs-lookup"><span data-stu-id="d0c16-103">The <xref:System.Xml.Xsl.XslTransform> class is obsolete in the .NET Framework 2.0.</span></span> <span data-ttu-id="d0c16-104">您可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別來執行可延伸樣式表語言轉換 (XSLT)。</span><span class="sxs-lookup"><span data-stu-id="d0c16-104">You can perform Extensible Stylesheet Language for Transformations (XSLT) transformations using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="d0c16-105">如需詳細資訊，請參閱[使用 XslCompiledTransform 類別](using-the-xslcompiledtransform-class.md)和[從 XslTransform 類別移轉](migrating-from-the-xsltransform-class.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c16-105">See [Using the XslCompiledTransform Class](using-the-xslcompiledtransform-class.md) and [Migrating From the XslTransform Class](migrating-from-the-xsltransform-class.md) for more information.</span></span>

<span data-ttu-id="d0c16-106"><xref:System.Xml.Xsl.XslTransform> 類別是可實作 XSL 轉換 (XSLT) 1.0 版建議事項的 XSLT 處理器。</span><span class="sxs-lookup"><span data-stu-id="d0c16-106">The <xref:System.Xml.Xsl.XslTransform> class is an XSLT processor implementing the XSL Transformations (XSLT) Version 1.0 recommendation.</span></span> <span data-ttu-id="d0c16-107"><xref:System.Xml.Xsl.XslTransform.Load%2A> 方法可尋找及讀取樣式表，而 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法則可轉換指定的來源文件。</span><span class="sxs-lookup"><span data-stu-id="d0c16-107">The <xref:System.Xml.Xsl.XslTransform.Load%2A> method locates and reads style sheets, and the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method transforms the given source document.</span></span> <span data-ttu-id="d0c16-108">任何實作 <xref:System.Xml.XPath.IXPathNavigable> 介面的存放區都可用來做為 <xref:System.Xml.Xsl.XslTransform> 的來源文件。</span><span class="sxs-lookup"><span data-stu-id="d0c16-108">Any store that implements the <xref:System.Xml.XPath.IXPathNavigable> interface can be used as the source document for the <xref:System.Xml.Xsl.XslTransform>.</span></span> <span data-ttu-id="d0c16-109">.NET Framework 目前實作 <xref:System.Xml.XmlDocument> 上的 <xref:System.Xml.XPath.IXPathNavigable> 介面、<xref:System.Xml.XmlDataDocument>，以及 <xref:System.Xml.XPath.XPathDocument>，因此這些項目都可以用來作為轉換的輸入來源文件。</span><span class="sxs-lookup"><span data-stu-id="d0c16-109">The .NET Framework currently implements the <xref:System.Xml.XPath.IXPathNavigable> interface on the <xref:System.Xml.XmlDocument>, the <xref:System.Xml.XmlDataDocument>, and the <xref:System.Xml.XPath.XPathDocument>, so all of these can be used as the input source document to a transformation.</span></span>

<span data-ttu-id="d0c16-110">.NET Framework 中的 <xref:System.Xml.Xsl.XslTransform> 物件僅支援 XSLT 1.0 規格，該規格是使用下列的命名空間定義：</span><span class="sxs-lookup"><span data-stu-id="d0c16-110">The <xref:System.Xml.Xsl.XslTransform> object in the .NET Framework only supports the XSLT 1.0 specification, defined with the following namespace:</span></span>

```xml
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
```

<span data-ttu-id="d0c16-111"><xref:System.Xml.Xsl.XslTransform.Load%2A> 方法可用來將下列其中一個類別載入樣式表：</span><span class="sxs-lookup"><span data-stu-id="d0c16-111">The style sheet can be loaded, using the <xref:System.Xml.Xsl.XslTransform.Load%2A> method, from one of the following classes:</span></span>

- <span data-ttu-id="d0c16-112">XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="d0c16-112">XPathNavigator</span></span>

- <span data-ttu-id="d0c16-113">XmlReader</span><span class="sxs-lookup"><span data-stu-id="d0c16-113">XmlReader</span></span>

- <span data-ttu-id="d0c16-114">表示 URL 的字串 </span><span class="sxs-lookup"><span data-stu-id="d0c16-114">A string representing a URL</span></span>

<span data-ttu-id="d0c16-115">上述每個輸入類別都有不同的 <xref:System.Xml.Xsl.XslTransform.Load%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="d0c16-115">There is a different <xref:System.Xml.Xsl.XslTransform.Load%2A> method for each of the above input classes.</span></span> <span data-ttu-id="d0c16-116">有些方法會採用上述其中一個類別與 <xref:System.Xml.XmlResolver> 類別的組合，來做為引數。</span><span class="sxs-lookup"><span data-stu-id="d0c16-116">Some methods take in a combination of one of these classes and the <xref:System.Xml.XmlResolver> class as arguments.</span></span> <span data-ttu-id="d0c16-117"><xref:System.Xml.XmlResolver> 會尋找樣式表中可發現之 `<xsl:import>` 或 `<xsl:include>` 所參考的資源。</span><span class="sxs-lookup"><span data-stu-id="d0c16-117">The <xref:System.Xml.XmlResolver> locates resources referenced by `<xsl:import>` or `<xsl:include>` found in the style sheet.</span></span> <span data-ttu-id="d0c16-118">下列幾種方法會採用字串 (<xref:System.Xml.XmlReader>) 或 <xref:System.Xml.XPath.XPathNavigator> 做為輸入。</span><span class="sxs-lookup"><span data-stu-id="d0c16-118">The following methods take a string, <xref:System.Xml.XmlReader>, or <xref:System.Xml.XPath.XPathNavigator> as input.</span></span>

```vb
Overloads Public Sub Load(String)
```

```csharp
public void Load(string);
```

```vb
Overloads Public Sub Load(String, XmlResolver)
```

```csharp
public void Load(string, XmlResolver);
```

```vb
Overloads Public Sub Load(XmlReader, XmlResolver, Evidence)
```

```csharp
public void Load(XmlReader, XmlResolver, Evidence);
```

```vb
Overloads Public Sub Load(XPathNavigator, XmlResolver, Evidence)
```

```csharp
public void Load(XPathNavigator, XmlResolver, Evidence);
```

<span data-ttu-id="d0c16-119">上述 <xref:System.Xml.Xsl.XslTransform.Load%2A> 方法大多會以 <xref:System.Xml.XmlResolver> 做為參數。</span><span class="sxs-lookup"><span data-stu-id="d0c16-119">Most of the <xref:System.Xml.Xsl.XslTransform.Load%2A> methods shown above take an <xref:System.Xml.XmlResolver> as a parameter.</span></span> <span data-ttu-id="d0c16-120"><xref:System.Xml.XmlResolver> 可用來載入樣式表，以及 xsl:import 和 xsl:include 項目中所參考的任何樣式表。</span><span class="sxs-lookup"><span data-stu-id="d0c16-120">The <xref:System.Xml.XmlResolver> is used to load the style sheet and any style sheet(s) referenced in xsl:import and xsl:include elements.</span></span>

<span data-ttu-id="d0c16-121">大多數的 <xref:System.Xml.Xsl.XslTransform.Load%2A> 方法也會以辨識項做為參數。</span><span class="sxs-lookup"><span data-stu-id="d0c16-121">Most of the <xref:System.Xml.Xsl.XslTransform.Load%2A> methods also take evidence as a parameter.</span></span> <span data-ttu-id="d0c16-122">辨識項參數是指與樣式表關聯的 <xref:System.Security.Policy.Evidence>。</span><span class="sxs-lookup"><span data-stu-id="d0c16-122">The evidence parameter is the <xref:System.Security.Policy.Evidence> that is associated with the style sheet.</span></span> <span data-ttu-id="d0c16-123">樣式表的安全性層級會影響它所參考之後續資源的安全性層級，例如它所包含的指令碼、所使用的任何 `document()` 函式，以及 <xref:System.Xml.Xsl.XsltArgumentList> 所使用的任何擴充物件。</span><span class="sxs-lookup"><span data-stu-id="d0c16-123">The security level of the style sheet affects the security level of any subsequent resources it references, such as the script it contains, any `document()` functions it uses, and any extension objects used by the <xref:System.Xml.Xsl.XsltArgumentList>.</span></span>

<span data-ttu-id="d0c16-124">如果使用 <xref:System.Xml.Xsl.XslTransform.Load%2A> 方法 (具有 URL 參數但未提供辨識項) 來載入樣式表，則會結合指定的 URL 與其網站和區域來計算樣式表的辨識項。</span><span class="sxs-lookup"><span data-stu-id="d0c16-124">If the style sheet is loaded using a <xref:System.Xml.Xsl.XslTransform.Load%2A> method that contains a URL parameter and no evidence is provided, the evidence of the style sheet is calculated by combining the given URL with its site and zone.</span></span>

<span data-ttu-id="d0c16-125">若未提供 URI 或辨識項，則樣式表的辨識項集合將完全受信任。</span><span class="sxs-lookup"><span data-stu-id="d0c16-125">If no URI or evidence is provided, then the evidence set for the style sheet is fully trusted.</span></span> <span data-ttu-id="d0c16-126">請勿從未受信任的來源載入樣式表，或者將未受信任的擴充物件加入 <xref:System.Xml.Xsl.XsltArgumentList> 中。</span><span class="sxs-lookup"><span data-stu-id="d0c16-126">Do not load style sheets from untrusted sources, or add untrusted extension objects into the <xref:System.Xml.Xsl.XsltArgumentList>.</span></span>

<span data-ttu-id="d0c16-127">如需安全性層級和辨識項的詳細資訊，以及它如何影響腳本，請參閱[使用 \<msxsl:script> 的 XSLT 樣式表單腳本](xslt-stylesheet-scripting-using-msxsl-script.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c16-127">For more information about security levels and evidence and how it affects scripting, see [XSLT Stylesheet Scripting Using \<msxsl:script>](xslt-stylesheet-scripting-using-msxsl-script.md).</span></span> <span data-ttu-id="d0c16-128">如需安全性層級、辨識項，以及辨識項將會如何影響指令碼的詳細資訊，請參閱[樣式表參數和擴充物件的 XsltArgumentList](xsltargumentlist-for-style-sheet-parameters-and-extension-objects.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c16-128">For information about security levels and evidence and how it affects extension objects, see [XsltArgumentList for Style Sheet Parameters and Extension Objects](xsltargumentlist-for-style-sheet-parameters-and-extension-objects.md).</span></span>

<span data-ttu-id="d0c16-129">如需安全性層級、辨識項，以及辨識項將會如何影響 `document()` 函式的詳細資訊，請參閱[解析外部的 XSLT 樣式表和文件](resolving-external-xslt-style-sheets-and-documents.md) 。</span><span class="sxs-lookup"><span data-stu-id="d0c16-129">For information about security levels and evidence and how it affects the `document()` function, see [Resolving External XSLT Style Sheets and Documents](resolving-external-xslt-style-sheets-and-documents.md).</span></span>

<span data-ttu-id="d0c16-130">可提供樣式表數個輸入參數。</span><span class="sxs-lookup"><span data-stu-id="d0c16-130">A style sheet can be supplied with a number of input parameters.</span></span> <span data-ttu-id="d0c16-131">樣式表也可以呼叫擴充物件上的函式。</span><span class="sxs-lookup"><span data-stu-id="d0c16-131">The style sheet can also call functions on extension objects.</span></span> <span data-ttu-id="d0c16-132">參數和擴充物件都可透過 <xref:System.Xml.Xsl.XsltArgumentList> 類別提供給樣式表。</span><span class="sxs-lookup"><span data-stu-id="d0c16-132">Both parameters and extension objects are supplied to the style sheet using the <xref:System.Xml.Xsl.XsltArgumentList> class.</span></span> <span data-ttu-id="d0c16-133">如需 <xref:System.Xml.Xsl.XsltArgumentList> 的詳細資訊，請參閱<xref:System.Xml.Xsl.XsltArgumentList>。</span><span class="sxs-lookup"><span data-stu-id="d0c16-133">For more information about the <xref:System.Xml.Xsl.XsltArgumentList>, see <xref:System.Xml.Xsl.XsltArgumentList>.</span></span>

## <a name="recommended-secure-use-of-xsltransform-class"></a><span data-ttu-id="d0c16-134">建議的 XslTransform 類別安全使用法</span><span class="sxs-lookup"><span data-stu-id="d0c16-134">Recommended Secure Use of XslTransform Class</span></span>

<span data-ttu-id="d0c16-135">樣式表的安全性權限取決於所提供的辨識項。</span><span class="sxs-lookup"><span data-stu-id="d0c16-135">The security privileges of the style sheet depend on the evidence provided.</span></span> <span data-ttu-id="d0c16-136">下表摘錄樣式表的位置，並針對應提供何種辨識項型別加以說明。</span><span class="sxs-lookup"><span data-stu-id="d0c16-136">The following table summarizes the location of the style sheet and gives an explanation of what type of evidence to give.</span></span>

- <span data-ttu-id="d0c16-137">XSLT 樣式表沒有外部參考，或者樣式表是來自您信任的程式碼基底。</span><span class="sxs-lookup"><span data-stu-id="d0c16-137">The XSLT style sheet has no external references, or the style sheet comes from a code base that you trust.</span></span>

  - <span data-ttu-id="d0c16-138">從您的組件提供辨識項：</span><span class="sxs-lookup"><span data-stu-id="d0c16-138">Provide the evidence from your assembly:</span></span>

    ```vb
    Dim xslt = New XslTransform() xslt.Load(stylesheet, resolver, Me.GetType().Assembly.Evidence)

    XsltTransform xslt = new XslTransform();  xslt.Load(stylesheet, resolver, this.GetType().Assembly.Evidence);
    ```

- <span data-ttu-id="d0c16-139">XSLT 樣式表來自外部來源。</span><span class="sxs-lookup"><span data-stu-id="d0c16-139">The XSLT style sheet comes from an outside source.</span></span> <span data-ttu-id="d0c16-140">已知來源的源頭，並且有可驗證的 URI。</span><span class="sxs-lookup"><span data-stu-id="d0c16-140">The origin of the source is known and there is a verifiable URI.</span></span>

  - <span data-ttu-id="d0c16-141">使用 URI 建立辨識項。</span><span class="sxs-lookup"><span data-stu-id="d0c16-141">Create evidence using the URI.</span></span>

    ```vb
    Dim xslt As New XslTransform() Dim ev As Evidence = XmlSecureResolver.CreateEvidenceForUrl(stylesheetUri) xslt.Load(stylesheet, resolver, evidence)

    XslTransform xslt = new XslTransform(); Evidence ev = XmlSecureResolver.CreateEvidenceForUrl(stylesheetUri); xslt.Load(stylesheet, resolver, evidence);
    ```

- <span data-ttu-id="d0c16-142">XSLT 樣式表來自外部來源。</span><span class="sxs-lookup"><span data-stu-id="d0c16-142">The XSLT style sheet comes from an outside source.</span></span> <span data-ttu-id="d0c16-143">來源的源頭未知。</span><span class="sxs-lookup"><span data-stu-id="d0c16-143">The origin of the source is not known.</span></span>

  - <span data-ttu-id="d0c16-144">將辨識項設為 `null`。</span><span class="sxs-lookup"><span data-stu-id="d0c16-144">Set evidence to `null`.</span></span> <span data-ttu-id="d0c16-145">不會處理指令碼區塊、不支援 XSLT `document()` 函式，且不允許已授權的擴充物件。</span><span class="sxs-lookup"><span data-stu-id="d0c16-145">Script blocks are not processed, the XSLT `document()` function is not supported, and privileged extension objects are disallowed.</span></span>

    <span data-ttu-id="d0c16-146">此外，您也可以將 `resolver` 參數設為 `null`，如此可確保不會處理 `xsl:import` 和 `xsl:include` 項目。</span><span class="sxs-lookup"><span data-stu-id="d0c16-146">Additionally, you can also set the `resolver` parameter to `null` This ensures that `xsl:import` and `xsl:include` elements are not processed.</span></span>

- <span data-ttu-id="d0c16-147">XSLT 樣式表來自外部來源。</span><span class="sxs-lookup"><span data-stu-id="d0c16-147">The XSLT style sheet comes from an outside source.</span></span> <span data-ttu-id="d0c16-148">來源的源頭未知，但是您需要指令碼支援。</span><span class="sxs-lookup"><span data-stu-id="d0c16-148">The origin of the source is not known, but you require script support.</span></span>

  - <span data-ttu-id="d0c16-149">自呼叫端要求識別項。</span><span class="sxs-lookup"><span data-stu-id="d0c16-149">Request evidence from the caller.</span></span>

## <a name="transformation-of-xml-data"></a><span data-ttu-id="d0c16-150">XML 資料的轉換</span><span class="sxs-lookup"><span data-stu-id="d0c16-150">Transformation of XML Data</span></span>

<span data-ttu-id="d0c16-151">載入樣式表後，即可呼叫其中一個 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法以及提供輸入來源文件來啟動轉換。</span><span class="sxs-lookup"><span data-stu-id="d0c16-151">Once a style sheet is loaded, the transformation starts by calling one of the <xref:System.Xml.Xsl.XslTransform.Transform%2A> methods and supplying an input source document.</span></span> <span data-ttu-id="d0c16-152">可多載化 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法，以提供不同的轉換輸出。</span><span class="sxs-lookup"><span data-stu-id="d0c16-152">The <xref:System.Xml.Xsl.XslTransform.Transform%2A> method is overloaded to provide different transformation outputs.</span></span> <span data-ttu-id="d0c16-153">轉換可以產生下列輸出格式：</span><span class="sxs-lookup"><span data-stu-id="d0c16-153">The transformation can result in the following output formats:</span></span>

- <xref:System.Xml.XmlReader>

- <xref:System.Xml.XmlWriter>

- <xref:System.IO.TextWriter>

- <xref:System.IO.Stream>

- <span data-ttu-id="d0c16-154">檔案的字串 URL</span><span class="sxs-lookup"><span data-stu-id="d0c16-154">String URL of file</span></span>

<span data-ttu-id="d0c16-155">字串 URL 是最後一個格式，它經用於 URL 中的輸入文件轉換，以及將文件寫入輸出 URL 等作業案例中。</span><span class="sxs-lookup"><span data-stu-id="d0c16-155">This last format, the string URL, provides for a commonly used scenario in transforming an input document located in a URL and writing the document to the output URL.</span></span> <span data-ttu-id="d0c16-156">這項 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 是一項便利的方法，可從檔案載入 XML 文件，然後執行 XSLT 轉換，再將輸出寫入檔案中。</span><span class="sxs-lookup"><span data-stu-id="d0c16-156">This <xref:System.Xml.Xsl.XslTransform.Transform%2A> method is a convenience method to load an XML document from a file, perform the XSLT transformation, and write the output to a file.</span></span> <span data-ttu-id="d0c16-157">如此可以防止您必須建立和載入輸入來源文件，再寫入至檔案資料流。</span><span class="sxs-lookup"><span data-stu-id="d0c16-157">This prevents you from having to create and load the input source document, and then write to a file stream.</span></span> <span data-ttu-id="d0c16-158">下列程式碼範例將以字串 URL 做為輸入和輸出，以示範 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法的使用情形：</span><span class="sxs-lookup"><span data-stu-id="d0c16-158">The following code sample shows this use of the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method using the string URL as input and output:</span></span>

```vb
Dim xsltransform As XslTransform = New XslTransform()
xsltransform.Load("favorite.xsl")
xsltransform.Transform("MyDocument.Xml", "TransformResult.xml", Nothing)
```

```csharp
XslTransform xsltransform = new XslTransform();
xsltransform.Load("favorite.xsl");
xsltransform.Transform("MyDocument.xml", "TransformResult.xml", null);
```

## <a name="transforming-a-section-of-an-xml-document"></a><span data-ttu-id="d0c16-159">轉換 XML 文件的段落</span><span class="sxs-lookup"><span data-stu-id="d0c16-159">Transforming a Section of an XML Document</span></span>

<span data-ttu-id="d0c16-160">轉換是指套用到整個文件。</span><span class="sxs-lookup"><span data-stu-id="d0c16-160">Transformations apply to the document as a whole.</span></span> <span data-ttu-id="d0c16-161">換言之，如果您要傳入的節點不是文件的根節點，則不會阻止轉換程序取得已載入文件中的所有節點。</span><span class="sxs-lookup"><span data-stu-id="d0c16-161">In other words, if you pass in a node other than the document root node, this does not prevent the transformation process from accessing all nodes in the loaded document.</span></span> <span data-ttu-id="d0c16-162">若要轉換結果樹狀結構片段，則必須建立僅包含結果樹狀結構片段的 <xref:System.Xml.XmlDocument>，並將 <xref:System.Xml.XmlDocument> 傳遞至 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法中。</span><span class="sxs-lookup"><span data-stu-id="d0c16-162">To transform a result tree fragment, you must create an <xref:System.Xml.XmlDocument> containing just the result tree fragment and pass that <xref:System.Xml.XmlDocument> to the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method.</span></span> <span data-ttu-id="d0c16-163">以下範例將執行結果樹狀結構片段的轉換。</span><span class="sxs-lookup"><span data-stu-id="d0c16-163">The following example performs a transformation on a result tree fragment.</span></span>

```vb
Dim xslt As New XslTransform()
xslt.Load("print_root.xsl")
Dim doc As New XmlDocument()
doc.Load("library.xml")
' Create a new document containing just the result tree fragment.
Dim testNode As XmlNode = doc.DocumentElement.FirstChild
Dim tmpDoc As New XmlDocument()
tmpDoc.LoadXml(testNode.OuterXml)
' Pass the document containing the result tree fragment
' to the Transform method.
Console.WriteLine(("Passing " + tmpDoc.OuterXml + " to print_root.xsl"))
xslt.Transform(tmpDoc, Nothing, Console.Out, Nothing)
```

```csharp
XslTransform xslt = new XslTransform();
xslt.Load("print_root.xsl");
XmlDocument doc = new XmlDocument();
doc.Load("library.xml");
// Create a new document containing just the result tree fragment.
XmlNode testNode = doc.DocumentElement.FirstChild;
XmlDocument tmpDoc = new XmlDocument();
tmpDoc.LoadXml(testNode.OuterXml);
// Pass the document containing the result tree fragment
// to the Transform method.
Console.WriteLine("Passing " + tmpDoc.OuterXml + " to print_root.xsl");
xslt.Transform(tmpDoc, null, Console.Out, null);
```

<span data-ttu-id="d0c16-164">此範例會使用 library .xml 和 print_root .xsl 檔案做為輸入，並將下列內容輸出到主控台：</span><span class="sxs-lookup"><span data-stu-id="d0c16-164">The example uses the library.xml and print_root.xsl files as input and outputs the following to the console:</span></span>

```console
Passing <book genre="novel" ISBN="1-861001-57-5"><title>Pride And Prejudice</title></book> to print_root.xsl
Root node is book.
```

<span data-ttu-id="d0c16-165">library.xml</span><span class="sxs-lookup"><span data-stu-id="d0c16-165">library.xml</span></span>

```xml
<library>
  <book genre='novel' ISBN='1-861001-57-5'>
     <title>Pride And Prejudice</title>
  </book>
  <book genre='novel' ISBN='1-81920-21-2'>
     <title>Hook</title>
  </book>
</library>
```

<span data-ttu-id="d0c16-166">print_root.xsl</span><span class="sxs-lookup"><span data-stu-id="d0c16-166">print_root.xsl</span></span>

```xml
<stylesheet version="1.0" xmlns="http://www.w3.org/1999/XSL/Transform" >
  <output method="text" />
  <template match="/">
     Root node is  <value-of select="local-name(//*[position() = 1])" />
  </template>
</stylesheet>
```

## <a name="migration-of-xslt-from-net-framework-version-10-to-net-framework-version-11"></a><span data-ttu-id="d0c16-167">XSLT 從 .NET Framework 1.0 版到 .NET Framework 1.1 版的轉換</span><span class="sxs-lookup"><span data-stu-id="d0c16-167">Migration of XSLT from .NET Framework version 1.0 to .NET Framework version 1.1</span></span>

<span data-ttu-id="d0c16-168">下表會顯示 <xref:System.Xml.Xsl.XslTransform.Load%2A> 方法已淘汰的 .NET Framework 版本 1.0 方法，以及新的 .NET Framework 版本 1.1 方法。</span><span class="sxs-lookup"><span data-stu-id="d0c16-168">The following table shows the obsolete .NET Framework version 1.0 methods and new .NET Framework version 1.1 methods for the <xref:System.Xml.Xsl.XslTransform.Load%2A> method.</span></span> <span data-ttu-id="d0c16-169">新方法可讓您藉由指定辨識項來限制樣式表的使用權限。</span><span class="sxs-lookup"><span data-stu-id="d0c16-169">The new methods enable you to limit the permissions of the style sheet by specifying evidence.</span></span>

|<span data-ttu-id="d0c16-170">.NET Framework 1.0 版過時的 Load 方法</span><span class="sxs-lookup"><span data-stu-id="d0c16-170">Obsolete .NET Framework version 1.0 Load Methods</span></span>|<span data-ttu-id="d0c16-171">.NET Framework 1.1 版替代的 Load 方法</span><span class="sxs-lookup"><span data-stu-id="d0c16-171">Replacement .NET Framework version 1.1 Load Methods</span></span>|
|------------------------------------------------------|---------------------------------------------------------|
|<span data-ttu-id="d0c16-172">Load(XPathNavigator input);</span><span class="sxs-lookup"><span data-stu-id="d0c16-172">Load(XPathNavigator input);</span></span><br /><br /> <span data-ttu-id="d0c16-173">Load(XPathNavigator input, XmlResolver resolver);</span><span class="sxs-lookup"><span data-stu-id="d0c16-173">Load(XPathNavigator input, XmlResolver resolver);</span></span>|<span data-ttu-id="d0c16-174">Load(XPathNavigator stylesheet, XmlResolver resolver, Evidence evidence);</span><span class="sxs-lookup"><span data-stu-id="d0c16-174">Load(XPathNavigator stylesheet, XmlResolver resolver, Evidence evidence);</span></span>|
|<span data-ttu-id="d0c16-175">Load(IXPathNavigable stylesheet);</span><span class="sxs-lookup"><span data-stu-id="d0c16-175">Load(IXPathNavigable stylesheet);</span></span><br /><br /> <span data-ttu-id="d0c16-176">Load(IXPathNavigable stylesheet, XmlResolver resolver);</span><span class="sxs-lookup"><span data-stu-id="d0c16-176">Load(IXPathNavigable stylesheet, XmlResolver resolver);</span></span>|<span data-ttu-id="d0c16-177">Load(IXPathNavigable stylesheet, XmlResolver resolver, Evidence evidence);</span><span class="sxs-lookup"><span data-stu-id="d0c16-177">Load(IXPathNavigable stylesheet, XmlResolver resolver, Evidence evidence);</span></span>|
|<span data-ttu-id="d0c16-178">Load(XmlReader stylesheet);</span><span class="sxs-lookup"><span data-stu-id="d0c16-178">Load(XmlReader stylesheet);</span></span><br /><br /> <span data-ttu-id="d0c16-179">Load(XmlReader stylesheet, XmlResolver resolver);</span><span class="sxs-lookup"><span data-stu-id="d0c16-179">Load(XmlReader stylesheet, XmlResolver resolver);</span></span>|<span data-ttu-id="d0c16-180">Load(XmlReader stylesheet, XmlResolver resolver, Evidence evidence);</span><span class="sxs-lookup"><span data-stu-id="d0c16-180">Load(XmlReader stylesheet, XmlResolver resolver, Evidence evidence);</span></span>|

<span data-ttu-id="d0c16-181">下列表格將針對 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法列出已過時的方法和新的方法。</span><span class="sxs-lookup"><span data-stu-id="d0c16-181">The following table shows the obsolete and new methods for the <xref:System.Xml.Xsl.XslTransform.Transform%2A> method.</span></span> <span data-ttu-id="d0c16-182">新方法採用的是 <xref:System.Xml.XmlResolver> 物件。</span><span class="sxs-lookup"><span data-stu-id="d0c16-182">The new methods take an <xref:System.Xml.XmlResolver> object.</span></span>

|<span data-ttu-id="d0c16-183">.NET Framework 1.0 版過時的 Transform 方法 </span><span class="sxs-lookup"><span data-stu-id="d0c16-183">Obsolete .NET Framework version 1.0 Transform Methods</span></span>|<span data-ttu-id="d0c16-184">.NET Framework 1.1 版替代的 Transform 方法</span><span class="sxs-lookup"><span data-stu-id="d0c16-184">Replacement .NET Framework version Transform 1.1 Methods</span></span>|
|-----------------------------------------------------------|--------------------------------------------------------------|
|<span data-ttu-id="d0c16-185">XmlReader Transform(XPathNavigator input, XsltArgumentList args)</span><span class="sxs-lookup"><span data-stu-id="d0c16-185">XmlReader Transform(XPathNavigator input, XsltArgumentList args)</span></span>|<span data-ttu-id="d0c16-186">XmlReader Transform(XPathNavigator  input, XsltArgumentList args, XmlResolver resolver)</span><span class="sxs-lookup"><span data-stu-id="d0c16-186">XmlReader Transform(XPathNavigator  input, XsltArgumentList args, XmlResolver resolver)</span></span>|
|<span data-ttu-id="d0c16-187">XmlReader Transform(IXPathNavigable input, XsltArgumentList args)</span><span class="sxs-lookup"><span data-stu-id="d0c16-187">XmlReader Transform(IXPathNavigable input, XsltArgumentList args)</span></span>|<span data-ttu-id="d0c16-188">XmlReader Transform(IXPathNavigable input, XsltArgumentList args, XmlResolver resolver)</span><span class="sxs-lookup"><span data-stu-id="d0c16-188">XmlReader Transform(IXPathNavigable input, XsltArgumentList args, XmlResolver resolver)</span></span>|
|<span data-ttu-id="d0c16-189">Void Transform(XPathNavigator input, XsltArgumentList args, XmlWriter output)</span><span class="sxs-lookup"><span data-stu-id="d0c16-189">Void Transform(XPathNavigator input, XsltArgumentList args, XmlWriter output)</span></span>|<span data-ttu-id="d0c16-190">Void Transform(XPathNavigator input, XsltArgumentList args, XmlWriter output, XmlResolver resolver)</span><span class="sxs-lookup"><span data-stu-id="d0c16-190">Void Transform(XPathNavigator input, XsltArgumentList args, XmlWriter output, XmlResolver resolver)</span></span>|
|<span data-ttu-id="d0c16-191">Void Transform(IXPathNavigable input, XsltArgumentList args, XmlWriter output)</span><span class="sxs-lookup"><span data-stu-id="d0c16-191">Void Transform(IXPathNavigable input, XsltArgumentList args, XmlWriter output)</span></span>|<span data-ttu-id="d0c16-192">Void Transform(IXpathNavigable input, XsltArgumentList args, XmlWriter output, XmlResolver resolver)</span><span class="sxs-lookup"><span data-stu-id="d0c16-192">Void Transform(IXpathNavigable input, XsltArgumentList args, XmlWriter output, XmlResolver resolver)</span></span>|
|<span data-ttu-id="d0c16-193">Void Transform(XPathNavigator input, XsltArgumentList args, TextWriter output)</span><span class="sxs-lookup"><span data-stu-id="d0c16-193">Void Transform(XPathNavigator input, XsltArgumentList args, TextWriter output)</span></span>|<span data-ttu-id="d0c16-194">Void Transform(XPathNavigator input, XsltArgumentList args, TextWriter output, XmlResolver resolver)</span><span class="sxs-lookup"><span data-stu-id="d0c16-194">Void Transform(XPathNavigator input, XsltArgumentList args, TextWriter output, XmlResolver resolver)</span></span>|
|<span data-ttu-id="d0c16-195">Void Transform(IXPathNavigable input, XsltArgumentList args, TextWriter output)</span><span class="sxs-lookup"><span data-stu-id="d0c16-195">Void Transform(IXPathNavigable input, XsltArgumentList args, TextWriter output)</span></span>|<span data-ttu-id="d0c16-196">Void Transform(IXPathNavigable input, XsltArgumentList args, TextWriter output, XmlResolver resolver)</span><span class="sxs-lookup"><span data-stu-id="d0c16-196">Void Transform(IXPathNavigable input, XsltArgumentList args, TextWriter output, XmlResolver resolver)</span></span>|
|<span data-ttu-id="d0c16-197">Void Transform(XPathNavigator input, XsltArgumentList args, Stream output)</span><span class="sxs-lookup"><span data-stu-id="d0c16-197">Void Transform(XPathNavigator input, XsltArgumentList args, Stream output)</span></span>|<span data-ttu-id="d0c16-198">Void Transform(XPathNavigator input, XsltArgumentList args, Stream output, XmlResolver resolver)</span><span class="sxs-lookup"><span data-stu-id="d0c16-198">Void Transform(XPathNavigator input, XsltArgumentList args, Stream output, XmlResolver resolver)</span></span>|
|<span data-ttu-id="d0c16-199">Void Transform(IXPathNavigable input, XsltArgumentList args, Stream output)</span><span class="sxs-lookup"><span data-stu-id="d0c16-199">Void Transform(IXPathNavigable input, XsltArgumentList args, Stream output)</span></span>|<span data-ttu-id="d0c16-200">Void Transform(IXPathNavigable input, XsltArgumentList args, Stream output, XmlResolver resolver)</span><span class="sxs-lookup"><span data-stu-id="d0c16-200">Void Transform(IXPathNavigable input, XsltArgumentList args, Stream output, XmlResolver resolver)</span></span>|
|<span data-ttu-id="d0c16-201">Void Transform(String input, String output);</span><span class="sxs-lookup"><span data-stu-id="d0c16-201">Void Transform(String input, String output);</span></span>|<span data-ttu-id="d0c16-202">Void Transform(String input, String output, XmlResolver resolver);</span><span class="sxs-lookup"><span data-stu-id="d0c16-202">Void Transform(String input, String output, XmlResolver resolver);</span></span>|

<span data-ttu-id="d0c16-203">在 .NET Framework 版本 1.1 中，<xref:System.Xml.Xsl.XslTransform.XmlResolver%2A?displayProperty=nameWithType> 屬性已遭淘汰。</span><span class="sxs-lookup"><span data-stu-id="d0c16-203">The <xref:System.Xml.Xsl.XslTransform.XmlResolver%2A?displayProperty=nameWithType> property is obsolete in .NET Framework version 1.1.</span></span> <span data-ttu-id="d0c16-204">請改用新的 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 多載，它採用的是 <xref:System.Xml.XmlResolver> 物件。</span><span class="sxs-lookup"><span data-stu-id="d0c16-204">Instead, use the new <xref:System.Xml.Xsl.XslTransform.Transform%2A> overloads which take an <xref:System.Xml.XmlResolver> object.</span></span>

## <a name="see-also"></a><span data-ttu-id="d0c16-205">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d0c16-205">See also</span></span>

- <xref:System.Xml.Xsl.XslTransform>
- [<span data-ttu-id="d0c16-206">使用 XslTransform 類別進行 XSLT 轉換</span><span class="sxs-lookup"><span data-stu-id="d0c16-206">XSLT Transformations with the XslTransform Class</span></span>](xslt-transformations-with-the-xsltransform-class.md)
- [<span data-ttu-id="d0c16-207">轉換中的 XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="d0c16-207">XPathNavigator in Transformations</span></span>](xpathnavigator-in-transformations.md)
- [<span data-ttu-id="d0c16-208">轉換中的 XPathNodeIterator</span><span class="sxs-lookup"><span data-stu-id="d0c16-208">XPathNodeIterator in Transformations</span></span>](xpathnodeiterator-in-transformations.md)
- [<span data-ttu-id="d0c16-209">XslTransform 的 XPathDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="d0c16-209">XPathDocument Input to XslTransform</span></span>](xpathdocument-input-to-xsltransform.md)
- [<span data-ttu-id="d0c16-210">XslTransform 的 XmlDataDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="d0c16-210">XmlDataDocument Input to XslTransform</span></span>](xmldatadocument-input-to-xsltransform.md)
- [<span data-ttu-id="d0c16-211">XslTransform 的 XmlDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="d0c16-211">XmlDocument Input to XslTransform</span></span>](xmldocument-input-to-xsltransform.md)
