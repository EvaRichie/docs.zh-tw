---
title: XElement 類別概觀
ms.date: 07/20/2015
ms.assetid: 52331fcd-6023-4d19-b423-7b24f2d86ded
ms.openlocfilehash: a0e50c8a5a14150ee09a328f4dcdd5bc88363621
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413215"
---
# <a name="xelement-class-overview-visual-basic"></a>System.xml.linq.xelement> 類別總覽（Visual Basic）
<xref:System.Xml.Linq.XElement> 類別是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中的其中一個基本類別。 它代表 XML 項目。 您可以使用這個類別來建立項目；變更項目的內容；加入、變更或刪除子項目；將屬性加入到項目中；或以文字格式序列化項目的內容。 您也可以與 <xref:System.Xml?displayProperty=nameWithType> 中的其他類別相互溝通，例如，<xref:System.Xml.XmlReader>、<xref:System.Xml.XmlWriter> 和 <xref:System.Xml.Xsl.XslCompiledTransform>。  
  
## <a name="xelement-functionality"></a>XElement 功能  
 本主題描述 <xref:System.Xml.Linq.XElement> 類別提供的功能。  
  
### <a name="constructing-xml-trees"></a>建構 XML 樹狀結構  
 您可以用各種方式建構 XML 樹狀結構，包括：  
  
- 您可以在程式碼中建構 XML 樹狀結構。 如需詳細資訊，請參閱[建立 XML 樹狀結構（Visual Basic）](creating-xml-trees.md)。  
  
- 您可以剖析來自各種來源的 XML，包括 <xref:System.IO.TextReader>、文字檔或網路位址 (URL)。 如需詳細資訊，請參閱[剖析 XML （Visual Basic）](parsing-xml.md)。  
  
- 您可以使用 <xref:System.Xml.XmlReader> 來填入樹狀結構。 如需詳細資訊，請參閱 <xref:System.Xml.Linq.XNode.ReadFrom%2A> 。  
  
- 如果您擁有的模組可以將內容寫入到 <xref:System.Xml.XmlWriter>，您可以使用 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 方法來建立寫入器、將寫入器傳遞到模組，然後使用寫入到 <xref:System.Xml.XmlWriter> 的內容填入 XML 樹狀結構。  
  
 不過，建立 XML 樹狀結構最常見的方式為下：  
  
```vb  
Dim contacts As XElement = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone>206-555-0144</Phone>  
            <Address>  
                <Street1>123 Main St</Street1>  
                <City>Mercer Island</City>  
                <State>WA</State>  
                <Postal>68042</Postal>  
            </Address>  
        </Contact>  
    </Contacts>  
```  
  
 建立 XML 樹狀結構的另一個非常常見的技術，包括使用 LINQ 查詢的結果來填入 XML 樹狀結構，如下列範例所示：  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element>1</Element>  
        <Element>2</Element>  
        <Element>3</Element>  
        <Element>4</Element>  
        <Element>5</Element>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child>1</Child>  
        <Child>2</Child>  
        <%= From el In srcTree.Elements() _  
            Where el.Value > 2 _  
            Select el %>  
    </Root>  
Console.WriteLine(xmlTree)  
```  
  
 這個範例會產生下列輸出：  
  
```xml  
<Root>  
  <Child>1</Child>  
  <Child>2</Child>  
  <Element>3</Element>  
  <Element>4</Element>  
  <Element>5</Element>  
</Root>  
```  
  
### <a name="serializing-xml-trees"></a>序列化 XML 樹狀結構  
 您可以將 XML 樹狀結構序列化至 <xref:System.IO.File>、<xref:System.IO.TextWriter> 或 <xref:System.Xml.XmlWriter>。  
  
 如需詳細資訊，請參閱序列化[XML 樹狀結構（Visual Basic）](serializing-xml-trees.md)。  
  
### <a name="retrieving-xml-data-via-axis-methods"></a>透過座標軸方法擷取 XML 資料  
 您可以使用座標軸方法來擷取屬性、子項目、子系項目以及祖系項目。 LINQ 查詢會在座標軸方法上運作，並提供數個彈性且功能強大的方式來流覽和處理 XML 樹狀結構。  
  
 如需詳細資訊，請參閱[LINQ to XML 軸（Visual Basic）](linq-to-xml-axes.md)。  
  
### <a name="querying-xml-trees"></a>查詢 XML 樹狀  
 您可以撰寫從 XML 樹狀結構中解壓縮資料的 LINQ 查詢。  
  
 如需詳細資訊，請參閱[查詢 XML 樹狀結構（Visual Basic）](querying-xml-trees.md)。  
  
### <a name="modifying-xml-trees"></a>修改 XML 樹狀  
 您可以用各種方式修改項目，包括變更其內容或屬性。 您也可以從其父代移除項目。  
  
 如需詳細資訊，請參閱[修改 XML 樹狀結構（LINQ to XML）（Visual Basic）](modifying-xml-trees-linq-to-xml.md)。  
  
## <a name="see-also"></a>另請參閱

- [LINQ to XML 程式設計總覽（Visual Basic）](linq-to-xml-programming-overview.md)
