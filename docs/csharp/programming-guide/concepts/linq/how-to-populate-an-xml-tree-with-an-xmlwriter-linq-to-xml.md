---
title: '如何使用 XmlWriter 填入 XML 樹狀結構（LINQ to XML）（c #）'
description: '瞭解如何使用 System.xml.linq.xcontainer.createwriter 來填入 XML 樹狀結構，以建立 XmlWriter，然後寫入 c # 中 LINQ to XML 的 XmlWriter。'
ms.date: 07/20/2015
ms.assetid: cd5674d1-5c54-4efc-ba68-e23b2875295f
ms.openlocfilehash: 9639c5947583bccf4f8ba427fc8611e181ef1536
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87104794"
---
# <a name="how-to-populate-an-xml-tree-with-an-xmlwriter-linq-to-xml-c"></a>如何使用 XmlWriter 填入 XML 樹狀結構（LINQ to XML）（c #）
填入 XML 樹狀的其中一種方式是使用 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 來建立 <xref:System.Xml.XmlWriter>，然後寫入到 <xref:System.Xml.XmlWriter> 中。 XML 樹狀會以寫入到 <xref:System.Xml.XmlWriter> 的所有節點填入。  
  
 當您使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 搭配預期寫入 <xref:System.Xml.XmlWriter> 的其他類別 (例如，<xref:System.Xml.Xsl.XslCompiledTransform>) 時，您通常會使用這個方法。  
  
## <a name="example"></a>範例  
 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 的其中一個可能的使用時機為叫用 XSLT 轉換時。 這個範例會建立 XML 樹狀結構、從 XML 樹狀結構建立 <xref:System.Xml.XmlReader>、建立新文件，然後建立 <xref:System.Xml.XmlWriter> 來寫入新文件。 接著，它會叫用 XSLT 轉換，以傳入至 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter>。 轉換成功完成後，系統會使用轉換的結果填入新的 XML 樹狀結構。  
  
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
using (XmlWriter writer = newTree.CreateWriter())  
{  
    // Load the style sheet.  
    XslCompiledTransform xslt = new XslCompiledTransform();  
    xslt.Load(XmlReader.Create(new StringReader(xslMarkup)));  
  
    // Execute the transformation and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer);  
}  
  
Console.WriteLine(newTree);  
```  
  
 這個範例會產生下列輸出：  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>請參閱

- <xref:System.Xml.Linq.XContainer.CreateWriter%2A>
- <xref:System.Xml.XmlWriter>
- <xref:System.Xml.Xsl.XslCompiledTransform>
- [建立 XML 樹狀結構 (C#)](./linq-to-xml-overview.md)
