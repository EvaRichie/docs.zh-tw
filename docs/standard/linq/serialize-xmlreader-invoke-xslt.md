---
title: 序列化至 XmlReader (叫用 XSLT) -LINQ to XML
description: 您可以使用 CreateReader 來建立 XmlReader，以提供 XML 樹狀結構的節點給 XSLT 轉換。
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 4cc3ee03-ef4c-429b-a408-fedd10b728cd
ms.openlocfilehash: e079627b5fe114438feabaa1a49f42a65afedf43
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552154"
---
# <a name="serialize-to-an-xmlreader-invoke-xslt-linq-to-xml"></a><span data-ttu-id="00e80-103">序列化至 XmlReader (叫用 XSLT)  (LINQ to XML) </span><span class="sxs-lookup"><span data-stu-id="00e80-103">Serialize to an XmlReader (invoke XSLT) (LINQ to XML)</span></span>

<span data-ttu-id="00e80-104">當您使用 <xref:System.Xml?displayProperty=nameWithType> LINQ to XML 的互通性功能時，您可以使用 <xref:System.Xml.Linq.XNode.CreateReader%2A> 來建立 <xref:System.Xml.XmlReader> 。</span><span class="sxs-lookup"><span data-stu-id="00e80-104">When you use the <xref:System.Xml?displayProperty=nameWithType> interoperability capabilities of LINQ to XML, you can use <xref:System.Xml.Linq.XNode.CreateReader%2A> to create an <xref:System.Xml.XmlReader>.</span></span> <span data-ttu-id="00e80-105">從這個 <xref:System.Xml.XmlReader> 讀取的模組會讀取 XML 樹狀結構中的節點並加以處理。</span><span class="sxs-lookup"><span data-stu-id="00e80-105">The module that reads from this <xref:System.Xml.XmlReader> reads the nodes from the XML tree and processes them accordingly.</span></span>

## <a name="example-invoke-an-xslt-transformation"></a><span data-ttu-id="00e80-106">範例：叫用 XSLT 轉換</span><span class="sxs-lookup"><span data-stu-id="00e80-106">Example: Invoke an XSLT transformation</span></span>

<span data-ttu-id="00e80-107">此方法的其中一個可能的使用時機為叫用 XSLT 轉換時。</span><span class="sxs-lookup"><span data-stu-id="00e80-107">One possible use for this method is when invoking an XSLT transformation.</span></span> <span data-ttu-id="00e80-108">您可以建立 XML 樹狀、從 XML 樹狀建立 <xref:System.Xml.XmlReader>、建立新文件，然後建立 <xref:System.Xml.XmlWriter> 以寫入新文件中。</span><span class="sxs-lookup"><span data-stu-id="00e80-108">You can create an XML tree, create an <xref:System.Xml.XmlReader> from the XML tree, create a new document, and then create an <xref:System.Xml.XmlWriter> to write into the new document.</span></span> <span data-ttu-id="00e80-109">接著，您可以叫用 XSLT 轉換，以傳入 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter>。</span><span class="sxs-lookup"><span data-stu-id="00e80-109">Then, you can invoke the XSLT transformation, passing in <xref:System.Xml.XmlReader> and <xref:System.Xml.XmlWriter>.</span></span> <span data-ttu-id="00e80-110">轉換成功完成後，系統會使用轉換的結果填入新的 XML 樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="00e80-110">After the transformation successfully completes, the new XML tree is populated with the results of the transformation.</span></span>

```csharp
string xslMarkup = @"<?xml version='1.0'?>
<xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>
    <xsl:template match='/Parent'>
        <Root>
            <C1>
            <xsl:value-of select='Child1'/>
            </C1>
            <C2>
            <xsl:value-of select='Child2'/>
            </C2>
        </Root>
    </xsl:template>
</xsl:stylesheet>";

XDocument xmlTree = new XDocument(
    new XElement("Parent",
        new XElement("Child1", "Child1 data"),
        new XElement("Child2", "Child2 data")
    )
);

XDocument newTree = new XDocument();
using (XmlWriter writer = newTree.CreateWriter()) {
    // Load the style sheet.
    XslCompiledTransform xslt = new XslCompiledTransform();
    xslt.Load(XmlReader.Create(new StringReader(xslMarkup)));

    // Execute the transformation and output the results to a writer.
    xslt.Transform(xmlTree.CreateReader(), writer);
}

Console.WriteLine(newTree);
```

```vb
Dim xslMarkup As XDocument = _
    <?xml version='1.0'?>
    <xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>
        <xsl:template match='/Parent'>
            <Root>
                <C1>
                    <xsl:value-of select='Child1'/>
                </C1>
                <C2>
                    <xsl:value-of select='Child2'/>
                </C2>
            </Root>
        </xsl:template>
    </xsl:stylesheet>

Dim xmlTree As XDocument = _
    <?xml version='1.0'?>
    <Parent>
        <Child1>Child1 data</Child1>
        <Child2>Child2 data</Child2>
    </Parent>

Dim newTree As XDocument = New XDocument()
Using writer As XmlWriter = newTree.CreateWriter()
    ' Load the style sheet.
    Dim xslt As XslCompiledTransform = New XslCompiledTransform()
    xslt.Load(xslMarkup.CreateReader())

    ' Execute the transformation and output the results to a writer.
    xslt.Transform(xmlTree.CreateReader(), writer)
End Using

Console.WriteLine(newTree)
```

<span data-ttu-id="00e80-111">這個範例會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="00e80-111">This example produces the following output:</span></span>

```xml
<Root>
  <C1>Child1 data</C1>
  <C2>Child2 data</C2>
</Root>
```
