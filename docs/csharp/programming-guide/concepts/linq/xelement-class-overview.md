---
title: XElement 類別概觀 (C#)
description: 'System.xml.linq.xelement> 類別代表 c # 中的 XML 元素。 這是 LINQ to XML 中的其中一個基礎類別。 瞭解 System.xml.linq.xelement> 所提供的功能。'
ms.date: 07/20/2015
ms.assetid: 2b9f0cd8-a1d1-4037-accf-0f38a410fa11
ms.openlocfilehash: f76f51703de054443f47531294777b43a9c0b004
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302174"
---
# <a name="xelement-class-overview-c"></a>XElement 類別概觀 (C#)
<xref:System.Xml.Linq.XElement> 類別是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 中的其中一個基本類別。 它代表 XML 項目。 您可以使用這個類別來建立項目；變更項目的內容；加入、變更或刪除子項目；將屬性加入到項目中；或以文字格式序列化項目的內容。 您也可以與 <xref:System.Xml?displayProperty=nameWithType> 中的其他類別相互溝通，例如，<xref:System.Xml.XmlReader>、<xref:System.Xml.XmlWriter> 和 <xref:System.Xml.Xsl.XslCompiledTransform>。  
  
本主題描述 <xref:System.Xml.Linq.XElement> 類別提供的功能。  
  
## <a name="constructing-xml-trees"></a>建構 XML 樹狀結構  
 您可以用各種方式建構 XML 樹狀結構，包括：  
  
- 您可以在程式碼中建構 XML 樹狀結構。 如需詳細資訊，請參閱[建立 XML 樹狀結構 (C#)](./linq-to-xml-overview.md)。  
  
- 您可以剖析來自各種來源的 XML，包括 <xref:System.IO.TextReader>、文字檔或網路位址 (URL)。 如需詳細資訊，請參閱[剖析 XML (C#)](./how-to-parse-a-string.md)。  
  
- 您可以使用 <xref:System.Xml.XmlReader> 來填入樹狀結構。 如需詳細資訊，請參閱 <xref:System.Xml.Linq.XNode.ReadFrom%2A>。  
  
- 如果您擁有的模組可以將內容寫入到 <xref:System.Xml.XmlWriter>，您可以使用 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 方法來建立寫入器、將寫入器傳遞到模組，然後使用寫入到 <xref:System.Xml.XmlWriter> 的內容填入 XML 樹狀結構。  
  
 不過，建立 XML 樹狀結構最常見的方式為下：  
  
```csharp  
XElement contacts =  
    new XElement("Contacts",  
        new XElement("Contact",  
            new XElement("Name", "Patrick Hines"),
            new XElement("Phone", "206-555-0144"),  
            new XElement("Address",  
                new XElement("Street1", "123 Main St"),  
                new XElement("City", "Mercer Island"),  
                new XElement("State", "WA"),  
                new XElement("Postal", "68042")  
            )  
        )  
    );  
```  
  
 建立 XML 樹狀結構的另一個非常常見的技術，包括使用 LINQ 查詢的結果來填入 XML 樹狀結構，如下列範例所示：  
  
```csharp  
XElement srcTree = new XElement("Root",  
    new XElement("Element", 1),  
    new XElement("Element", 2),  
    new XElement("Element", 3),  
    new XElement("Element", 4),  
    new XElement("Element", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child", 1),  
    new XElement("Child", 2),  
    from el in srcTree.Elements()  
    where (int)el > 2  
    select el  
);  
Console.WriteLine(xmlTree);  
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
  
## <a name="serializing-xml-trees"></a>序列化 XML 樹狀結構  
 您可以將 XML 樹狀結構序列化至 <xref:System.IO.File>、<xref:System.IO.TextWriter> 或 <xref:System.Xml.XmlWriter>。  
  
 如需詳細資訊，請參閱[序列化 XML 樹狀結構 (C#)](./preserving-white-space-while-serializing.md)。  
  
## <a name="retrieving-xml-data-via-axis-methods"></a>透過座標軸方法擷取 XML 資料  
 您可以使用座標軸方法來擷取屬性、子項目、子系項目以及祖系項目。 LINQ 查詢會在座標軸方法上運作，並提供數個彈性且功能強大的方式來流覽和處理 XML 樹狀結構。  
  
 如需詳細資訊，請參閱 [LINQ to XML 座標軸 (C#)](./linq-to-xml-axes-overview.md)。  
  
## <a name="querying-xml-trees"></a>查詢 XML 樹狀  
 您可以撰寫從 XML 樹狀結構中解壓縮資料的 LINQ 查詢。  
  
 如需詳細資訊，請參閱[查詢 XML 樹狀結構 (C#)](./how-to-find-an-element-with-a-specific-attribute.md)。  
  
## <a name="modifying-xml-trees"></a>修改 XML 樹狀  
 您可以用各種方式修改項目，包括變更其內容或屬性。 您也可以從其父代移除項目。  
  
 如需詳細資訊，請參閱[修改 XML 樹狀結構 (LINQ to XML) (C#)](./in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml.md)。  
  
## <a name="see-also"></a>另請參閱

- [LINQ to XML 程式設計概觀 (C#)](serializing-to-files-textwriters-and-xmlwriters.md)
