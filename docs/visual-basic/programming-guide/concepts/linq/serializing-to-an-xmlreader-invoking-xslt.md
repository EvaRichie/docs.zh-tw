---
title: 序列化至 XmlReader (叫用 XSLT)
ms.date: 07/20/2015
ms.assetid: 8b64f95a-e8f6-40f7-99f9-a8002c63af96
ms.openlocfilehash: e51bfc031ad6d5d0eb98718f5d547fb18eb45295
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357370"
---
# <a name="serializing-to-an-xmlreader-invoking-xslt-visual-basic"></a>序列化至 XmlReader （叫用 XSLT）（Visual Basic）
當您使用 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 的 <xref:System.Xml?displayProperty=nameWithType> 互通性能力時，可以使用 <xref:System.Xml.Linq.XNode.CreateReader%2A> 來建立 <xref:System.Xml.XmlReader>。 從這個 <xref:System.Xml.XmlReader> 讀取的模組會讀取 XML 樹狀結構中的節點並加以處理。  
  
## <a name="invoking-an-xslt-transformation"></a>叫用 XSLT 轉換  
 此方法的其中一個可能的使用時機為叫用 XSLT 轉換時。 您可以建立 XML 樹狀、從 XML 樹狀建立 <xref:System.Xml.XmlReader>、建立新文件，然後建立 <xref:System.Xml.XmlWriter> 以寫入新文件中。 接著，您可以叫用 XSLT 轉換，以傳入 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter>。 轉換成功完成後，系統會使用轉換的結果填入新的 XML 樹狀結構。  
  
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
  
 這個範例會產生下列輸出：  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>另請參閱

- [序列化 XML 樹狀結構（Visual Basic）](serializing-xml-trees.md)
