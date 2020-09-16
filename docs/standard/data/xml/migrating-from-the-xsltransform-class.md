---
title: 從 XslTransform 類別移轉
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 9404d758-679f-4ffb-995d-3d07d817659e
ms.openlocfilehash: 32fac1b5ab339dd4c71d761cf07fcde99ce1f2fa
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90550159"
---
# <a name="migrating-from-the-xsltransform-class"></a><span data-ttu-id="a8228-102">從 XslTransform 類別移轉</span><span class="sxs-lookup"><span data-stu-id="a8228-102">Migrating From the XslTransform Class</span></span>

<span data-ttu-id="a8228-103">XSLT 架構已在 Visual Studio 2005 版本中重新設計。</span><span class="sxs-lookup"><span data-stu-id="a8228-103">The XSLT architecture was redesigned in the Visual Studio 2005 release.</span></span> <span data-ttu-id="a8228-104"><xref:System.Xml.Xsl.XslTransform> 類別已由 <xref:System.Xml.Xsl.XslCompiledTransform> 類別取代。</span><span class="sxs-lookup"><span data-stu-id="a8228-104">The <xref:System.Xml.Xsl.XslTransform> class was replaced by the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span>

<span data-ttu-id="a8228-105">下列章節將說明 <xref:System.Xml.Xsl.XslCompiledTransform> 與 <xref:System.Xml.Xsl.XslTransform> 類別之間的一些主要差異。</span><span class="sxs-lookup"><span data-stu-id="a8228-105">The following sections describe some of the main differences between the <xref:System.Xml.Xsl.XslCompiledTransform> and the <xref:System.Xml.Xsl.XslTransform> classes.</span></span>

## <a name="performance"></a><span data-ttu-id="a8228-106">效能</span><span class="sxs-lookup"><span data-stu-id="a8228-106">Performance</span></span>

<span data-ttu-id="a8228-107"><xref:System.Xml.Xsl.XslCompiledTransform> 類別包括許多效能改進。</span><span class="sxs-lookup"><span data-stu-id="a8228-107">The <xref:System.Xml.Xsl.XslCompiledTransform> class includes many performance improvements.</span></span> <span data-ttu-id="a8228-108">類似於 Common Language Runtime (CLR) 處理其他程式設計語言的方式，新版 XSLT 處理器會將 XSLT 樣式表編譯成常見的中繼格式。</span><span class="sxs-lookup"><span data-stu-id="a8228-108">The new XSLT processor compiles the XSLT style sheet down to a common intermediate format, similar to what the common language runtime (CLR) does for other programming languages.</span></span> <span data-ttu-id="a8228-109">樣式表一旦編譯完畢，便可對其進行快取及重複使用。</span><span class="sxs-lookup"><span data-stu-id="a8228-109">Once the style sheet is compiled, it can be cached and reused.</span></span>

<span data-ttu-id="a8228-110"><xref:System.Xml.Xsl.XslCompiledTransform> 類別還包括其他最佳化功能，讓其速度要比 <xref:System.Xml.Xsl.XslTransform> 類別快很多。</span><span class="sxs-lookup"><span data-stu-id="a8228-110">The <xref:System.Xml.Xsl.XslCompiledTransform> class also includes other optimizations that make it much faster than the <xref:System.Xml.Xsl.XslTransform> class.</span></span>

> [!NOTE]
> <span data-ttu-id="a8228-111">雖然 <xref:System.Xml.Xsl.XslCompiledTransform> 類別的整體效能優於 <xref:System.Xml.Xsl.XslTransform> 類別，但是在轉換時第一次呼叫 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 類別的 <xref:System.Xml.Xsl.XslCompiledTransform> 方法之執行速度可能會比 <xref:System.Xml.Xsl.XslTransform.Load%2A> 類別的 <xref:System.Xml.Xsl.XslTransform> 方法慢許多。</span><span class="sxs-lookup"><span data-stu-id="a8228-111">Although the overall performance of the <xref:System.Xml.Xsl.XslCompiledTransform> class is better than the <xref:System.Xml.Xsl.XslTransform> class, the <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> method of the <xref:System.Xml.Xsl.XslCompiledTransform> class might perform more slowly than the <xref:System.Xml.Xsl.XslTransform.Load%2A> method of the <xref:System.Xml.Xsl.XslTransform> class the first time it is called on a transformation.</span></span> <span data-ttu-id="a8228-112">這是因為在載入之前必須先編譯 XSLT 檔案。</span><span class="sxs-lookup"><span data-stu-id="a8228-112">This is because the XSLT file must be compiled before it is loaded.</span></span> <span data-ttu-id="a8228-113">如需詳細資訊，請參閱下列部落格文章：[XslCompiledTransform 比 XslTransform 還慢嗎？](/archive/blogs/antosha/xslcompiledtransform-slower-than-xsltransform) (英文)</span><span class="sxs-lookup"><span data-stu-id="a8228-113">For more information, see the following blog post: [XslCompiledTransform Slower than XslTransform?](/archive/blogs/antosha/xslcompiledtransform-slower-than-xsltransform)</span></span>

## <a name="security"></a><span data-ttu-id="a8228-114">安全性</span><span class="sxs-lookup"><span data-stu-id="a8228-114">Security</span></span>

<span data-ttu-id="a8228-115">根據預設，<xref:System.Xml.Xsl.XslCompiledTransform> 類別會停用 XSLT `document()` 函式與內嵌指令碼的支援。</span><span class="sxs-lookup"><span data-stu-id="a8228-115">By default, the <xref:System.Xml.Xsl.XslCompiledTransform> class disables support for the XSLT `document()` function and embedded scripting.</span></span> <span data-ttu-id="a8228-116">您可藉由建立啟用這些功能的 <xref:System.Xml.Xsl.XsltSettings> 物件，並將其傳遞至 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 方法來啟用功能。</span><span class="sxs-lookup"><span data-stu-id="a8228-116">These features can be enabled by creating an <xref:System.Xml.Xsl.XsltSettings> object that has the features enabled and passing it to the <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> method.</span></span> <span data-ttu-id="a8228-117">下列範例將示範如何啟用指令碼及執行 XSLT 轉換。</span><span class="sxs-lookup"><span data-stu-id="a8228-117">The following example shows how to enable scripting and perform an XSLT transformation.</span></span>

[!code-csharp[XML_Migration#16](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#16)]
[!code-vb[XML_Migration#16](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#16)]

<span data-ttu-id="a8228-118">如需詳細資訊，請參閱 [XSLT 安全性考量](xslt-security-considerations.md)。</span><span class="sxs-lookup"><span data-stu-id="a8228-118">For more information, see [XSLT Security Considerations](xslt-security-considerations.md).</span></span>

## <a name="new-features"></a><span data-ttu-id="a8228-119">新功能</span><span class="sxs-lookup"><span data-stu-id="a8228-119">New Features</span></span>

### <a name="temporary-files"></a><span data-ttu-id="a8228-120">暫存檔案</span><span class="sxs-lookup"><span data-stu-id="a8228-120">Temporary Files</span></span>

<span data-ttu-id="a8228-121">暫存檔案有時會在 XSLT 處理期間產生。</span><span class="sxs-lookup"><span data-stu-id="a8228-121">Temporary files are sometimes generated during XSLT processing.</span></span> <span data-ttu-id="a8228-122">如果樣式表包含指令碼區塊，或是在編譯時將偵錯設定為 true，則可能會在 %TEMP% 資料夾中建立暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="a8228-122">If a style sheet contains script blocks, or if it is compiled with the debug setting set to true, temporary files may be created in the %TEMP% folder.</span></span> <span data-ttu-id="a8228-123">可能會有一些案例是因為時間問題而刪除某些暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="a8228-123">There may be instances when some temporary files are not deleted due to timing issues.</span></span> <span data-ttu-id="a8228-124">例如，如果目前的 AppDomain 或偵錯工具正在使用檔案，則 <xref:System.CodeDom.Compiler.TempFileCollection> 物件的完成項無法將其移除。</span><span class="sxs-lookup"><span data-stu-id="a8228-124">For example, if the files are in use by the current AppDomain or by the debugger, the finalizer of the <xref:System.CodeDom.Compiler.TempFileCollection> object will not be able to remove them.</span></span>

<span data-ttu-id="a8228-125"><xref:System.Xml.Xsl.XslCompiledTransform.TemporaryFiles%2A> 屬性可用於其他清除工作，以確定所有的暫存檔案都已從用戶端中移除。</span><span class="sxs-lookup"><span data-stu-id="a8228-125">The <xref:System.Xml.Xsl.XslCompiledTransform.TemporaryFiles%2A> property can be used for additional cleanup to make sure that all temporary files are removed from the client.</span></span>

### <a name="support-for-the-xsloutput-element-and-xmlwriter"></a><span data-ttu-id="a8228-126">xsl:output 項目和 XmlWriter 的支援</span><span class="sxs-lookup"><span data-stu-id="a8228-126">Support for the xsl:output Element and XmlWriter</span></span>

<span data-ttu-id="a8228-127">當轉換輸出傳送到 <xref:System.Xml.Xsl.XslTransform> 物件時，`xsl:output` 類別會忽略 <xref:System.Xml.XmlWriter> 設定。</span><span class="sxs-lookup"><span data-stu-id="a8228-127">The <xref:System.Xml.Xsl.XslTransform> class ignored `xsl:output` settings when the transform output was sent to an <xref:System.Xml.XmlWriter> object.</span></span> <span data-ttu-id="a8228-128"><xref:System.Xml.Xsl.XslCompiledTransform> 類別具有 <xref:System.Xml.Xsl.XslCompiledTransform.OutputSettings%2A> 屬性，此屬性會傳回包含衍生自樣式表 <xref:System.Xml.XmlWriterSettings> 項目之輸出資訊的 `xsl:output` 物件。</span><span class="sxs-lookup"><span data-stu-id="a8228-128">The <xref:System.Xml.Xsl.XslCompiledTransform> class has an <xref:System.Xml.Xsl.XslCompiledTransform.OutputSettings%2A> property that returns an <xref:System.Xml.XmlWriterSettings> object containing the output information derived from the `xsl:output` element of the style sheet.</span></span> <span data-ttu-id="a8228-129"><xref:System.Xml.XmlWriterSettings> 物件是用來建立 <xref:System.Xml.XmlWriter> 物件，其正確的設定可以傳遞給 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="a8228-129">The <xref:System.Xml.XmlWriterSettings> object is used to create an <xref:System.Xml.XmlWriter> object with the correct settings that can be passed to the <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> method.</span></span> <span data-ttu-id="a8228-130">下列 C# 程式碼說明這個行為：</span><span class="sxs-lookup"><span data-stu-id="a8228-130">The following C# code illustrates this behavior:</span></span>

```csharp
// Create the XslTransform object and load the style sheet.
XslCompiledTransform xslt = new XslCompiledTransform();
xslt.Load(stylesheet);

// Load the file to transform.
XPathDocument doc = new XPathDocument(filename);

// Create the writer.
XmlWriter writer = XmlWriter.Create(Console.Out, xslt.OutputSettings);

// Transform the file and send the output to the console.
xslt.Transform(doc, writer);
writer.Close();
```

### <a name="debug-option"></a><span data-ttu-id="a8228-131">偵錯選項</span><span class="sxs-lookup"><span data-stu-id="a8228-131">Debug Option</span></span>

<span data-ttu-id="a8228-132"><xref:System.Xml.Xsl.XslCompiledTransform> 類別可以產生偵錯資訊，此資訊可讓您使用 Microsoft Visual Studio 偵錯工具來偵錯樣式表。</span><span class="sxs-lookup"><span data-stu-id="a8228-132">The <xref:System.Xml.Xsl.XslCompiledTransform> class can generate debug information, which enables you to debug the style sheet with the Microsoft Visual Studio Debugger.</span></span> <span data-ttu-id="a8228-133">如需相關資訊，請參閱 <xref:System.Xml.Xsl.XslCompiledTransform.%23ctor%28System.Boolean%29> 。</span><span class="sxs-lookup"><span data-stu-id="a8228-133">See <xref:System.Xml.Xsl.XslCompiledTransform.%23ctor%28System.Boolean%29> for more information.</span></span>

## <a name="behavioral-differences"></a><span data-ttu-id="a8228-134">行為的差異</span><span class="sxs-lookup"><span data-stu-id="a8228-134">Behavioral Differences</span></span>

### <a name="transforming-to-an-xmlreader"></a><span data-ttu-id="a8228-135">轉換成 XmlReader</span><span class="sxs-lookup"><span data-stu-id="a8228-135">Transforming to an XmlReader</span></span>

<span data-ttu-id="a8228-136"><xref:System.Xml.Xsl.XslTransform> 類別有數個 Transform 多載，可將轉換結果當做 <xref:System.Xml.XmlReader> 物件傳回。</span><span class="sxs-lookup"><span data-stu-id="a8228-136">The <xref:System.Xml.Xsl.XslTransform> class has several Transform overloads that return transformation results as an <xref:System.Xml.XmlReader> object.</span></span> <span data-ttu-id="a8228-137">這些多載可用來將轉換結果載入記憶體中的表示法 (例如 <xref:System.Xml.XmlDocument> 或 <xref:System.Xml.XPath.XPathDocument>)，而不會產生序列化和還原序列化結果 XML 樹狀結構的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="a8228-137">These overloads can be used to load the transformation results into an in-memory representation (such as <xref:System.Xml.XmlDocument> or <xref:System.Xml.XPath.XPathDocument>) without incurring the overhead of serialization and deserialization of the resulting XML tree.</span></span> <span data-ttu-id="a8228-138">下列 C# 程式碼示範如何將轉換結果載入 <xref:System.Xml.XmlDocument> 物件。</span><span class="sxs-lookup"><span data-stu-id="a8228-138">The following C# code shows how to load the transformation results into an <xref:System.Xml.XmlDocument> object.</span></span>

```csharp
// Load the style sheet
XslTransform xslt = new XslTransform();
xslt.Load("MyStylesheet.xsl");

// Transform input document to XmlDocument for additional processing
XmlDocument doc = new XmlDocument();
doc.Load(xslt.Transform(input, (XsltArgumentList)null));
```

<span data-ttu-id="a8228-139"><xref:System.Xml.Xsl.XslCompiledTransform> 類別不支援轉換成 <xref:System.Xml.XmlReader> 物件。</span><span class="sxs-lookup"><span data-stu-id="a8228-139">The <xref:System.Xml.Xsl.XslCompiledTransform> class does not support transforming to an <xref:System.Xml.XmlReader> object.</span></span> <span data-ttu-id="a8228-140">但是，您可以採取類似的處理方式，透過 <xref:System.Xml.XPath.XPathNavigator.CreateNavigator%2A> 方法從 <xref:System.Xml.XmlWriter> 直接載入產生的 XML 樹狀。</span><span class="sxs-lookup"><span data-stu-id="a8228-140">However, you can do something similar by using the <xref:System.Xml.XPath.XPathNavigator.CreateNavigator%2A> method to load the resulting XML tree directly from an <xref:System.Xml.XmlWriter>.</span></span> <span data-ttu-id="a8228-141">下列 C# 程式碼將示範如何使用 <xref:System.Xml.Xsl.XslCompiledTransform> 完成相同的工作。</span><span class="sxs-lookup"><span data-stu-id="a8228-141">The following C# code shows how to accomplish the same task using <xref:System.Xml.Xsl.XslCompiledTransform>.</span></span>

```csharp
// Transform input document to XmlDocument for additional processing
XmlDocument doc = new XmlDocument();
using (XmlWriter writer = doc.CreateNavigator().AppendChild()) {
    xslt.Transform(input, (XsltArgumentList)null, writer);
}
```

### <a name="discretionary-behavior"></a><span data-ttu-id="a8228-142">Discretionary 行為</span><span class="sxs-lookup"><span data-stu-id="a8228-142">Discretionary Behavior</span></span>

<span data-ttu-id="a8228-143">＜W3C XSL 轉換 (XSLT) 1.0 版建議事項＞中所包含的領域，可告訴實作提供者該採取哪些決策來處理哪種狀況。</span><span class="sxs-lookup"><span data-stu-id="a8228-143">The W3C XSL Transformations (XSLT) Version 1.0 Recommendation includes areas in which the implementation provider may decide how to handle a situation.</span></span> <span data-ttu-id="a8228-144">這些領域視為 Discretionary 行為。</span><span class="sxs-lookup"><span data-stu-id="a8228-144">These areas are considered to be discretionary behavior.</span></span> <span data-ttu-id="a8228-145">在幾個領域中，<xref:System.Xml.Xsl.XslCompiledTransform> 的行為與 <xref:System.Xml.Xsl.XslTransform> 類別有一些差異。</span><span class="sxs-lookup"><span data-stu-id="a8228-145">There are several areas where the <xref:System.Xml.Xsl.XslCompiledTransform> behaves differently than the <xref:System.Xml.Xsl.XslTransform> class.</span></span> <span data-ttu-id="a8228-146">如需詳細資訊，請參閱[可復原的 XSLT 錯誤](recoverable-xslt-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="a8228-146">For more information, see [Recoverable XSLT Errors](recoverable-xslt-errors.md).</span></span>

### <a name="extension-objects-and-script-functions"></a><span data-ttu-id="a8228-147">擴充物件和指令碼函式</span><span class="sxs-lookup"><span data-stu-id="a8228-147">Extension Objects and Script Functions</span></span>

<span data-ttu-id="a8228-148"><xref:System.Xml.Xsl.XslCompiledTransform> 對於指令碼函式的使用引入兩項新的限制：</span><span class="sxs-lookup"><span data-stu-id="a8228-148"><xref:System.Xml.Xsl.XslCompiledTransform> introduces two new restrictions on the use of script functions:</span></span>

- <span data-ttu-id="a8228-149">只有公用方法才可以從 XPath 運算式呼叫。</span><span class="sxs-lookup"><span data-stu-id="a8228-149">Only public methods may be called from XPath expressions.</span></span>

- <span data-ttu-id="a8228-150">多載可根據引數的數目彼此區分。</span><span class="sxs-lookup"><span data-stu-id="a8228-150">Overloads are distinguishable from each other based on the number of arguments.</span></span> <span data-ttu-id="a8228-151">如果有一個以上的多載具有相同的引數數目，將會引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8228-151">If more than one overload has the same number of arguments, an exception will be raised.</span></span>

<span data-ttu-id="a8228-152">在 <xref:System.Xml.Xsl.XslCompiledTransform> 中，繫結 (方法名稱查閱) 至指令碼函式會在編譯時期發生，當使用 XslTranform 的樣式表是以 <xref:System.Xml.Xsl.XslCompiledTransform> 載入時，可能會導致例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a8228-152">In <xref:System.Xml.Xsl.XslCompiledTransform>, a binding (method name lookup) to script functions occurs at compile time, and style sheets that worked with XslTransform may cause an exception when they are loaded with <xref:System.Xml.Xsl.XslCompiledTransform>.</span></span>

<span data-ttu-id="a8228-153"><xref:System.Xml.Xsl.XslCompiledTransform> 支援在 `msxsl:using` 項目內有 `msxsl:assembly` 和 `msxsl:script` 子項目。</span><span class="sxs-lookup"><span data-stu-id="a8228-153"><xref:System.Xml.Xsl.XslCompiledTransform> supports having `msxsl:using` and `msxsl:assembly` child elements within the `msxsl:script` element.</span></span> <span data-ttu-id="a8228-154">`msxsl:using` 和 `msxsl:assembly` 項目是用來宣告要在指令碼區塊內使用的其他命名空間和組件。</span><span class="sxs-lookup"><span data-stu-id="a8228-154">The `msxsl:using` and `msxsl:assembly` elements are used to declare additional namespaces and assemblies for use in the script block.</span></span> <span data-ttu-id="a8228-155">如需詳細資訊，請參閱[使用 msxsl:script 的指令碼區塊](script-blocks-using-msxsl-script.md)。</span><span class="sxs-lookup"><span data-stu-id="a8228-155">See [Script Blocks Using msxsl:script](script-blocks-using-msxsl-script.md) for more information.</span></span>

<span data-ttu-id="a8228-156"><xref:System.Xml.Xsl.XslCompiledTransform> 禁止具有多個多載的擴充物件有相同的引數數目。</span><span class="sxs-lookup"><span data-stu-id="a8228-156"><xref:System.Xml.Xsl.XslCompiledTransform> prohibits extension objects that have multiple overloads with the same number of arguments.</span></span>

### <a name="msxml-functions"></a><span data-ttu-id="a8228-157">MSXML 函式</span><span class="sxs-lookup"><span data-stu-id="a8228-157">MSXML Functions</span></span>

<span data-ttu-id="a8228-158">其他 MSXML 函式的支援已加入到 <xref:System.Xml.Xsl.XslCompiledTransform> 類別中。</span><span class="sxs-lookup"><span data-stu-id="a8228-158">Support for additional MSXML functions have been added to the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="a8228-159">下列清單說明新的或改良的功能：</span><span class="sxs-lookup"><span data-stu-id="a8228-159">The following list describes new or improved functionality:</span></span>

- <span data-ttu-id="a8228-160">msxsl:node-set：<xref:System.Xml.Xsl.XslTransform> 要求 [node-set Function](/previous-versions/dotnet/netframework-4.0/ms256197(v=vs.100)) 函式的引數為 result tree fragment。</span><span class="sxs-lookup"><span data-stu-id="a8228-160">msxsl:node-set: <xref:System.Xml.Xsl.XslTransform> required the argument of the [node-set Function](/previous-versions/dotnet/netframework-4.0/ms256197(v=vs.100)) function to be a result tree fragment.</span></span> <span data-ttu-id="a8228-161"><xref:System.Xml.Xsl.XslCompiledTransform> 類別並沒有這項需求。</span><span class="sxs-lookup"><span data-stu-id="a8228-161">The <xref:System.Xml.Xsl.XslCompiledTransform> class does not have this requirement.</span></span>

- <span data-ttu-id="a8228-162">msxsl:version：在 <xref:System.Xml.Xsl.XslCompiledTransform> 中支援此函式。</span><span class="sxs-lookup"><span data-stu-id="a8228-162">msxsl:version: This function is supported in <xref:System.Xml.Xsl.XslCompiledTransform>.</span></span>

- <span data-ttu-id="a8228-163">XPath 擴充函式：現在支援 [ms:string-compare Function](/previous-versions/dotnet/netframework-4.0/ms256114(v=vs.100))、[ms:utc Function](/previous-versions/dotnet/netframework-4.0/ms256474(v=vs.100)), [ms:namespace-uri Function](/previous-versions/dotnet/netframework-4.0/ms256231(v=vs.100))、[ms:local-name Function](/previous-versions/dotnet/netframework-4.0/ms256055(v=vs.100))、[ms:number Function](/previous-versions/dotnet/netframework-4.0/ms256155(v=vs.100))、[ms:format-date Function](/previous-versions/dotnet/netframework-4.0/ms256099(v=vs.100)) 和 [ms:format-time Function](/previous-versions/dotnet/netframework-4.0/ms256467(v=vs.100)) 函式。</span><span class="sxs-lookup"><span data-stu-id="a8228-163">XPath extension functions: The [ms:string-compare Function](/previous-versions/dotnet/netframework-4.0/ms256114(v=vs.100)), [ms:utc Function](/previous-versions/dotnet/netframework-4.0/ms256474(v=vs.100)), [ms:namespace-uri Function](/previous-versions/dotnet/netframework-4.0/ms256231(v=vs.100)), [ms:local-name Function](/previous-versions/dotnet/netframework-4.0/ms256055(v=vs.100)), [ms:number Function](/previous-versions/dotnet/netframework-4.0/ms256155(v=vs.100)), [ms:format-date Function](/previous-versions/dotnet/netframework-4.0/ms256099(v=vs.100)), and [ms:format-time Function](/previous-versions/dotnet/netframework-4.0/ms256467(v=vs.100)) functions are now supported.</span></span>

- <span data-ttu-id="a8228-164">與結構描述相關的 XPath 擴充函式：<xref:System.Xml.Xsl.XslCompiledTransform> 原本就不支援這些函式。</span><span class="sxs-lookup"><span data-stu-id="a8228-164">Schema-related XPath extension functions: These functions are not supported natively by <xref:System.Xml.Xsl.XslCompiledTransform>.</span></span> <span data-ttu-id="a8228-165">不過，它們可以實作為擴充函式。</span><span class="sxs-lookup"><span data-stu-id="a8228-165">However, they can be implemented as extension functions.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8228-166">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a8228-166">See also</span></span>

- [<span data-ttu-id="a8228-167">XSLT 轉換</span><span class="sxs-lookup"><span data-stu-id="a8228-167">XSLT Transformations</span></span>](xslt-transformations.md)
- [<span data-ttu-id="a8228-168">使用 XslCompiledTransform 類別</span><span class="sxs-lookup"><span data-stu-id="a8228-168">Using the XslCompiledTransform Class</span></span>](using-the-xslcompiledtransform-class.md)
