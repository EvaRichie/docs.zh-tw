---
title: 使用 XslTransform 類別進行 XSLT 轉換
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 500335af-f9b5-413b-968a-e6d9a824478c
ms.openlocfilehash: ccdee1bbb94581d842cfc6fabe0f98dd6ec1d252
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818228"
---
# <a name="xslt-transformations-with-the-xsltransform-class"></a><span data-ttu-id="30aa5-102">使用 XslTransform 類別進行 XSLT 轉換</span><span class="sxs-lookup"><span data-stu-id="30aa5-102">XSLT Transformations with the XslTransform Class</span></span>

> [!NOTE]
> <span data-ttu-id="30aa5-103">在 .NET Framework 2.0 中，<xref:System.Xml.Xsl.XslTransform> 類別已過時。</span><span class="sxs-lookup"><span data-stu-id="30aa5-103">The <xref:System.Xml.Xsl.XslTransform> class is obsolete in the .NET Framework 2.0.</span></span> <span data-ttu-id="30aa5-104">您可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 類別來執行可延伸樣式表語言轉換 (XSLT)。</span><span class="sxs-lookup"><span data-stu-id="30aa5-104">You can perform Extensible Stylesheet Language for Transformations (XSLT) transformations using the <xref:System.Xml.Xsl.XslCompiledTransform> class.</span></span> <span data-ttu-id="30aa5-105">如需詳細資訊，請參閱[使用 XslCompiledTransform 類別](using-the-xslcompiledtransform-class.md)和[從 XslTransform 類別移轉](migrating-from-the-xsltransform-class.md)。</span><span class="sxs-lookup"><span data-stu-id="30aa5-105">See [Using the XslCompiledTransform Class](using-the-xslcompiledtransform-class.md) and [Migrating From the XslTransform Class](migrating-from-the-xsltransform-class.md) for more information.</span></span>

<span data-ttu-id="30aa5-106">XSLT 的目的在於，將來源 XML 文件的內容轉換為使用不同格式或結構的其他文件 (例如，將 XML 轉換為 HTML 以供網站使用，或將 XML 轉換為僅含某個應用程式所需之欄位的文件)。</span><span class="sxs-lookup"><span data-stu-id="30aa5-106">The goal of the XSLT is to transform the content of a source XML document into another document that is different in format or structure (for example, to transform XML into HTML for use on a Web site or to transform it into a document that contains only the fields required by an application).</span></span> <span data-ttu-id="30aa5-107">這項轉換程序是由全球資訊網協會 (W3C) [XSLT 1.0 版建議事項](https://www.w3.org/TR/1999/REC-xslt-19991116)所指定。</span><span class="sxs-lookup"><span data-stu-id="30aa5-107">This transformation process is specified by the World Wide Web Consortium (W3C)[XSLT version 1.0 recommendation](https://www.w3.org/TR/1999/REC-xslt-19991116).</span></span> <span data-ttu-id="30aa5-108">在 .NET Framework 之 <xref:System.Xml.Xsl> 命名空間中的 <xref:System.Xml.Xsl.XslTransform> 類別為 XSLT 處理器，其實作此規格功能。</span><span class="sxs-lookup"><span data-stu-id="30aa5-108">In the .NET Framework, the <xref:System.Xml.Xsl.XslTransform> class, found in the <xref:System.Xml.Xsl> namespace, is the XSLT processor that implements the functionality of this specification.</span></span> <span data-ttu-id="30aa5-109">W3C XSLT 1.0 版建議事項中有少數功能未被實作，列示於 [XslTransform 的輸出](outputs-from-an-xsltransform.md)中。</span><span class="sxs-lookup"><span data-stu-id="30aa5-109">There are a small number of features that have not been implemented from the W3C XSLT 1.0 recommendation, listed in [Outputs from an XslTransform](outputs-from-an-xsltransform.md).</span></span> <span data-ttu-id="30aa5-110">下圖說明 .NET Framework 的轉換架構。</span><span class="sxs-lookup"><span data-stu-id="30aa5-110">The following figure shows the transformation architecture of the .NET Framework.</span></span>

## <a name="overview"></a><span data-ttu-id="30aa5-111">概觀</span><span class="sxs-lookup"><span data-stu-id="30aa5-111">Overview</span></span>

![顯示 XSLT 轉換架構的圖表。](./media/xslt-transformations-with-the-xsltransform-class/xslt-transformation-architecture.gif)

<span data-ttu-id="30aa5-113">XSLT 建議事項使用 XML 路徑語言 (XPath) 來選擇 XML 文件的一部分，其中 XPath 是用來巡覽文件樹狀結構節點的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="30aa5-113">The XSLT recommendation uses XML Path Language (XPath) to select parts of an XML document, where XPath is a query language used to navigate nodes of a document tree.</span></span> <span data-ttu-id="30aa5-114">如圖所示，XPath 之 .NET Framework 實作會用來選取儲存在數個類別中的 XML 部分，例如 <xref:System.Xml.XmlDocument>、<xref:System.Xml.XmlDataDocument> 及 <xref:System.Xml.XPath.XPathDocument>。</span><span class="sxs-lookup"><span data-stu-id="30aa5-114">As shown in the diagram, the .NET Framework implementation of XPath is used to select parts of XML stored in several classes, such as an <xref:System.Xml.XmlDocument>, an <xref:System.Xml.XmlDataDocument>, and an <xref:System.Xml.XPath.XPathDocument>.</span></span> <span data-ttu-id="30aa5-115"><xref:System.Xml.XPath.XPathDocument> 是最佳化的 XSLT 資料存放區，當它與 <xref:System.Xml.Xsl.XslTransform> 搭配使用時，可在 XSLT 轉換期間提供最佳效能。</span><span class="sxs-lookup"><span data-stu-id="30aa5-115">An <xref:System.Xml.XPath.XPathDocument> is an optimized XSLT data store, and when used with <xref:System.Xml.Xsl.XslTransform>, it provides XSLT transformations with good performance.</span></span>

<span data-ttu-id="30aa5-116">下列表格列出與 <xref:System.Xml.Xsl.XslTransform> 和 XPath 搭配使用時最常用的類別及其函式。</span><span class="sxs-lookup"><span data-stu-id="30aa5-116">The following table list commonly uses classes when working with <xref:System.Xml.Xsl.XslTransform> and XPath and their function.</span></span>

|<span data-ttu-id="30aa5-117">類別或介面</span><span class="sxs-lookup"><span data-stu-id="30aa5-117">Class or Interface</span></span>|<span data-ttu-id="30aa5-118">函式</span><span class="sxs-lookup"><span data-stu-id="30aa5-118">Function</span></span>|
|------------------------|--------------|
|<xref:System.Xml.XPath.XPathNavigator>|<span data-ttu-id="30aa5-119">它是 API，為巡覽存放區提供了游標樣式模式以及 XPath 查詢支援。</span><span class="sxs-lookup"><span data-stu-id="30aa5-119">It is an API that provides a cursor style model for navigating over a store, along with XPath query support.</span></span> <span data-ttu-id="30aa5-120">它並未提供基礎存放區的編輯。</span><span class="sxs-lookup"><span data-stu-id="30aa5-120">It does not provide editing of the underlying store.</span></span> <span data-ttu-id="30aa5-121">若要進行編輯，請使用 <xref:System.Xml.XmlDocument> 類別。</span><span class="sxs-lookup"><span data-stu-id="30aa5-121">For editing, use the <xref:System.Xml.XmlDocument> class.</span></span>|
|<xref:System.Xml.XPath.IXPathNavigable>|<span data-ttu-id="30aa5-122">此介面可將 `CreateNavigator` 方法提供給 <xref:System.Xml.XPath.XPathNavigator>，以進行儲存。</span><span class="sxs-lookup"><span data-stu-id="30aa5-122">It is an interface that provides a `CreateNavigator` method to an <xref:System.Xml.XPath.XPathNavigator> for the store.</span></span>|
|<xref:System.Xml.XmlDocument>|<span data-ttu-id="30aa5-123">它使得能夠編輯文件。</span><span class="sxs-lookup"><span data-stu-id="30aa5-123">It enables editing of this document.</span></span> <span data-ttu-id="30aa5-124">它可實作 <xref:System.Xml.XPath.IXPathNavigable>，以達成後續需進行 XSLT 轉換的文件編輯案例。</span><span class="sxs-lookup"><span data-stu-id="30aa5-124">It implements <xref:System.Xml.XPath.IXPathNavigable>, allowing document-editing scenarios where XSLT transformations are subsequently required.</span></span> <span data-ttu-id="30aa5-125">如需詳細資訊，請參閱 [XslTransform 的 XmlDocument 輸入](xmldocument-input-to-xsltransform.md)。</span><span class="sxs-lookup"><span data-stu-id="30aa5-125">For more information, see [XmlDocument Input to XslTransform](xmldocument-input-to-xsltransform.md).</span></span>|
|<xref:System.Xml.XmlDataDocument>|<span data-ttu-id="30aa5-126">它衍生自 <xref:System.Xml.XmlDocument>。</span><span class="sxs-lookup"><span data-stu-id="30aa5-126">It is derived from the <xref:System.Xml.XmlDocument>.</span></span> <span data-ttu-id="30aa5-127">它使用 <xref:System.Data.DataSet>，並根據 <xref:System.Data.DataSet> 上的指定對應，對 XML 文件內的結構化資料儲存進行最佳化，藉以連絡關聯式領域與 XML 領域。</span><span class="sxs-lookup"><span data-stu-id="30aa5-127">It bridges the relational and XML worlds by using a <xref:System.Data.DataSet> to optimize storage of structured data within the XML document according to specified mappings on the <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="30aa5-128">它會實作 <xref:System.Xml.XPath.IXPathNavigable>，以達成 XSLT 轉換可在擷取自資料庫之關聯式資料上執行的案例。</span><span class="sxs-lookup"><span data-stu-id="30aa5-128">It implements <xref:System.Xml.XPath.IXPathNavigable>, allowing scenarios where XSLT transformations can be performed over relational data retrieved from a database.</span></span> <span data-ttu-id="30aa5-129">如需詳細資訊，請參閱 [XML 與關聯式資料和 ADO.NET 互相整合](xml-integration-with-relational-data-and-adonet.md)。</span><span class="sxs-lookup"><span data-stu-id="30aa5-129">For more information, see [XML Integration with Relational Data and ADO.NET](xml-integration-with-relational-data-and-adonet.md).</span></span>|
|<xref:System.Xml.XPath.XPathDocument>|<span data-ttu-id="30aa5-130">此類別已針對 <xref:System.Xml.Xsl.XslTransform> 處理與 XPath 查詢進行最佳化，並可提供高效能的唯讀快取。</span><span class="sxs-lookup"><span data-stu-id="30aa5-130">This class is optimized for <xref:System.Xml.Xsl.XslTransform> processing and XPath queries, and it provides a read-only high performance cache.</span></span> <span data-ttu-id="30aa5-131">它會實作 <xref:System.Xml.XPath.IXPathNavigable>，是進行 XSLT 轉換時適用的存放區。</span><span class="sxs-lookup"><span data-stu-id="30aa5-131">It implements <xref:System.Xml.XPath.IXPathNavigable> and is the preferred store to use for XSLT transformations.</span></span>|
|<xref:System.Xml.XPath.XPathNodeIterator>|<span data-ttu-id="30aa5-132">它提供跨 XPath 節點集的巡覽。</span><span class="sxs-lookup"><span data-stu-id="30aa5-132">It provides navigation over XPath node sets.</span></span> <span data-ttu-id="30aa5-133"><xref:System.Xml.XPath.XPathNavigator> 上的所有 XPath 選取方法都會傳回 <xref:System.Xml.XPath.XPathNodeIterator>。</span><span class="sxs-lookup"><span data-stu-id="30aa5-133">All XPath selection methods on the <xref:System.Xml.XPath.XPathNavigator> return an <xref:System.Xml.XPath.XPathNodeIterator>.</span></span> <span data-ttu-id="30aa5-134">相同的存放區上可建立多個 <xref:System.Xml.XPath.XPathNodeIterator> 物件，而每個物件各代表一個選取的節點集。</span><span class="sxs-lookup"><span data-stu-id="30aa5-134">Multiple <xref:System.Xml.XPath.XPathNodeIterator> objects can be created over the same store, each representing a selected set of nodes.</span></span>|

## <a name="msxml-xslt-extensions"></a><span data-ttu-id="30aa5-135">MSXML XSLT 擴充</span><span class="sxs-lookup"><span data-stu-id="30aa5-135">MSXML XSLT Extensions</span></span>

<span data-ttu-id="30aa5-136">`msxsl:script` 類別所支援的 Microsoft XML Core Services (MSXML) XSLT 擴充只有 `msxsl:node-set` 和 <xref:System.Xml.Xsl.XslTransform> 這兩個函式。</span><span class="sxs-lookup"><span data-stu-id="30aa5-136">The `msxsl:script` and `msxsl:node-set` functions are the only Microsoft XML Core Services (MSXML) XSLT extensions supported by the <xref:System.Xml.Xsl.XslTransform> class.</span></span>

## <a name="example"></a><span data-ttu-id="30aa5-137">範例</span><span class="sxs-lookup"><span data-stu-id="30aa5-137">Example</span></span>

<span data-ttu-id="30aa5-138">下列程式碼範例會載入 XSL 樣式表、將名為 mydata.xml 的檔案讀取至 <xref:System.Xml.XPath.XPathDocument>，並且在名為 myStyleSheet.xsl 之虛擬檔案的資料上執行轉換，然後將格式化的輸出傳送給主控台。</span><span class="sxs-lookup"><span data-stu-id="30aa5-138">The following code example loads an XSLT style sheet, reads a file called mydata.xml into an <xref:System.Xml.XPath.XPathDocument>, and performs a transformation on the data on a fictitious file called myStyleSheet.xsl, sending the formatted output to the console.</span></span>

```vb
Imports System.IO
Imports System.Xml
Imports System.Xml.XPath
Imports System.Xml.Xsl

Public Class Sample
    Private filename As [String] = "mydata.xml"
    Private stylesheet As [String] = "myStyleSheet.xsl"

    Public Shared Sub Main()
        Dim xslt As New XslTransform()
        xslt.Load(stylesheet)
        Dim xpathdocument As New XPathDocument(filename)
        Dim writer As New XmlTextWriter(Console.Out)
        writer.Formatting = Formatting.Indented

        xslt.Transform(xpathdocument, Nothing, writer, Nothing)
    End Sub 'Main
End Class 'Sample
```

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.XPath;
using System.Xml.Xsl;

public class Sample
{
    private const String filename = "mydata.xml";
    private const String stylesheet = "myStyleSheet.xsl";

    public static void Main()
    {
        XslTransform xslt = new XslTransform();
        xslt.Load(stylesheet);
        XPathDocument xpathdocument = new XPathDocument(filename);
        XmlTextWriter writer = new XmlTextWriter(Console.Out);
        writer.Formatting = Formatting.Indented;

        xslt.Transform(xpathdocument, null, writer, null);
    }
}
```

## <a name="see-also"></a><span data-ttu-id="30aa5-139">請參閱</span><span class="sxs-lookup"><span data-stu-id="30aa5-139">See also</span></span>

- <xref:System.Xml.Xsl.XslTransform>
- [<span data-ttu-id="30aa5-140">XslTransform 類別實作 XSLT 處理器</span><span class="sxs-lookup"><span data-stu-id="30aa5-140">XslTransform Class Implements the XSLT Processor</span></span>](xsltransform-class-implements-the-xslt-processor.md)
- [<span data-ttu-id="30aa5-141">XslTransform 類別中的 Discretionary 行為實作</span><span class="sxs-lookup"><span data-stu-id="30aa5-141">Implementation of Discretionary Behaviors in the XslTransform Class</span></span>](implementation-of-discretionary-behaviors-in-the-xsltransform-class.md)
- [<span data-ttu-id="30aa5-142">轉換中的 XPathNavigator</span><span class="sxs-lookup"><span data-stu-id="30aa5-142">XPathNavigator in Transformations</span></span>](xpathnavigator-in-transformations.md)
- [<span data-ttu-id="30aa5-143">轉換中的 XPathNodeIterator</span><span class="sxs-lookup"><span data-stu-id="30aa5-143">XPathNodeIterator in Transformations</span></span>](xpathnodeiterator-in-transformations.md)
- [<span data-ttu-id="30aa5-144">XslTransform 的 XPathDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="30aa5-144">XPathDocument Input to XslTransform</span></span>](xpathdocument-input-to-xsltransform.md)
- [<span data-ttu-id="30aa5-145">XslTransform 的 XmlDataDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="30aa5-145">XmlDataDocument Input to XslTransform</span></span>](xmldatadocument-input-to-xsltransform.md)
- [<span data-ttu-id="30aa5-146">XslTransform 的 XmlDocument 輸入</span><span class="sxs-lookup"><span data-stu-id="30aa5-146">XmlDocument Input to XslTransform</span></span>](xmldocument-input-to-xsltransform.md)
