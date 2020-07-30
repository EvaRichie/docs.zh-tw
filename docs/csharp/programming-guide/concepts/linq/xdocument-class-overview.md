---
title: XDocument 類別概觀 (C#)
description: 'C # 中的 XDocument 類別包含有效 XML 檔所需的資訊，包括 XML 宣告、處理指示和批註。'
ms.date: 07/20/2015
ms.assetid: 63305603-ab54-49fc-84e4-f76eecc59549
ms.openlocfilehash: 6d522cef25e99e4a5ea54e644855c8dfa7a05f4a
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87302187"
---
# <a name="xdocument-class-overview-c"></a>XDocument 類別概觀 (C#)
本主題說明 <xref:System.Xml.Linq.XDocument> 類別。  
  
## <a name="overview-of-the-xdocument-class"></a>XDocument 類別的概觀  
 <xref:System.Xml.Linq.XDocument> 類別包含有效 XML 文件所需的資訊。 這包括 XML 宣告、處理指示與註解。  
  
 請注意，如果您需要 <xref:System.Xml.Linq.XDocument> 類別所提供的特定功能，您僅需要建立 <xref:System.Xml.Linq.XDocument> 物件。 在許多情況下，您可以直接使用 <xref:System.Xml.Linq.XElement>。 直接使用 <xref:System.Xml.Linq.XElement> 是較簡單的程式設計模型。  
  
 <xref:System.Xml.Linq.XDocument> 衍生自 <xref:System.Xml.Linq.XContainer>。 因此，它可以包含子節點。 不過，<xref:System.Xml.Linq.XDocument> 物件可以有只有一個 <xref:System.Xml.Linq.XElement> 子節點。 這會反映 XML 標準，也就是說 XML 文件中只能有一個根項目 (Root Element)。  
  
## <a name="components-of-xdocument"></a>XDocument 的元件  
 <xref:System.Xml.Linq.XDocument> 可以包含下列項目：  
  
- 一個 <xref:System.Xml.Linq.XDeclaration> 物件。 <xref:System.Xml.Linq.XDeclaration> 可讓您指定 XML 宣告的關聯部分：XML 版本、文件的編碼，以及 XML 文件是否是獨立的。  
  
- 一個 <xref:System.Xml.Linq.XElement> 物件。 這是 XML 文件的根節點。  
  
- 任何數目的 <xref:System.Xml.Linq.XProcessingInstruction> 物件。 處理指示會將資訊傳達到處理 XML 的應用程式。  
  
- 任何數目的 <xref:System.Xml.Linq.XComment> 物件。 這些註解將是根項目的同層級。 <xref:System.Xml.Linq.XComment> 物件不得為清單中的第一個引數，因為對於 XML 文件而言，它不適用於開始註解。  
  
- 一個適用於 DTD 的 <xref:System.Xml.Linq.XDocumentType>。  
  
 當您序列化 <xref:System.Xml.Linq.XDocument> 時，即使 `XDocument.Declaration` 為 `null`，如果寫入器已將 `Writer.Settings.OmitXmlDeclaration` 設定為 `false` (預設值)，則輸出將會有 XML 宣告。  
  
 根據預設，[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 會將版本設定為 "1.0"，並將編碼設定為 "utf-8"。  
  
## <a name="using-xelement-without-xdocument"></a>在沒有 XDocument 的情況下使用 XElement  
 如先前所述，<xref:System.Xml.Linq.XElement> 類別是 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 程式發展介面中的主要類別。 在許多情況下，您的應用程式將不需要您建立文件。 您可以使用 <xref:System.Xml.Linq.XElement> 類別來建立 XML 樹狀結構、在其中加入其他 XML 樹狀結構、修改 XML 樹狀結構，然後加以儲存。  
  
## <a name="using-xdocument"></a>使用 XDocument  
 若要建構 <xref:System.Xml.Linq.XDocument>，請使用功能結構，如同您建構 <xref:System.Xml.Linq.XElement> 物件時所執行的操作。  
  
 下列程式碼會建立 <xref:System.Xml.Linq.XDocument> 物件及其所包含的相關聯物件。  
  
```csharp  
XDocument d = new XDocument(  
    new XComment("This is a comment."),  
    new XProcessingInstruction("xml-stylesheet",  
        "href='mystyle.css' title='Compact' type='text/css'"),  
    new XElement("Pubs",  
        new XElement("Book",  
            new XElement("Title", "Artifacts of Roman Civilization"),  
            new XElement("Author", "Moreno, Jordao")  
        ),  
        new XElement("Book",  
            new XElement("Title", "Midieval Tools and Implements"),  
            new XElement("Author", "Gazit, Inbar")  
        )  
    ),  
    new XComment("This is another comment.")  
);  
d.Declaration = new XDeclaration("1.0", "utf-8", "true");  
Console.WriteLine(d);  
  
d.Save("test.xml");  
```  
  
 當您檢查 test.xml 檔案時，您會得到下列輸出：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!--This is a comment.-->  
<?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>  
<Pubs>  
  <Book>  
    <Title>Artifacts of Roman Civilization</Title>  
    <Author>Moreno, Jordao</Author>  
  </Book>  
  <Book>  
    <Title>Midieval Tools and Implements</Title>  
    <Author>Gazit, Inbar</Author>  
  </Book>  
</Pubs>  
<!--This is another comment.-->  
```  
  
## <a name="see-also"></a>另請參閱

- [LINQ to XML 程式設計概觀 (C#)](./linq-to-xml-overview.md)
