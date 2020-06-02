---
title: HOW TO：指定 XML 資料流的替代元素名稱
description: 瞭解如何使用替代元素名稱建立 XML 資料流程，例如，針對需要相同資訊但稍微不同的 XML Web Service。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XML serialization, overriding
- serialization, overriding
- XML stream, specifying alternate element name for
- overriding XML serialization
- classes, overriding
- overriding classes
ms.assetid: 5cc1c0b0-f94b-4525-9a41-88a582cd6668
ms.openlocfilehash: d7e482ee6e1e1a7318ab05766508537d4b87789e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289586"
---
# <a name="how-to-specify-an-alternate-element-name-for-an-xml-stream"></a>HOW TO：指定 XML 資料流的替代元素名稱
  
使用 <xref:System.Xml.Serialization.XmlSerializer>，以相同類別集，可產生一個以上的 XML 資料流。 當兩個不同的 XML Web 服務要求相同的基本資訊以及些微差異時，您也許會想這麼做。 例如，試想有兩家處理書本訂單的 XML Web 服務，而且都需要 ISBN 號碼。 其中一個服務會使用標記， \<ISBN> 而第二個則使用標籤 \<BookID> 。 您有名為  的類別，其中包含名為 的欄位。 當 `Book` 類別的執行個體序列化時，它會根據預設使用成員名稱 (ISBN) 做為標記項目名稱。 對於第一個 XML Web 服務，這正如預期。 不過要想要傳送 XML 資料流至第二個 XML Web 服務，您必須覆寫序列化，讓標記的項目名稱為 `BookID`。  
  
## <a name="to-create-an-xml-stream-with-an-alternate-element-name"></a>以其他項目名稱建立 XML 資料流  
  
1. 建立 <xref:System.Xml.Serialization.XmlElementAttribute> 類別的執行個體。  
  
2. 將 <xref:System.Xml.Serialization.XmlElementAttribute.ElementName%2A> 的 <xref:System.Xml.Serialization.XmlElementAttribute> 設為 "BookID"。  
  
3. 建立 <xref:System.Xml.Serialization.XmlAttributes> 類別的執行個體。  
  
4. 將 `XmlElementAttribute` 物件加入至透過 <xref:System.Xml.Serialization.XmlAttributes.XmlElements%2A> 之 <xref:System.Xml.Serialization.XmlAttributes> 屬性存取的集合。  
  
5. 建立 <xref:System.Xml.Serialization.XmlAttributeOverrides> 類別的執行個體。  
  
6. 將 `XmlAttributes` 加入至 <xref:System.Xml.Serialization.XmlAttributeOverrides>，傳遞要覆寫的物件型別及遭覆寫的成員名稱。  
  
7. 使用 建立  類別的執行個體。  
  
8. 建立 `Book` 類別的執行個體，將它序列化或還原序列化。  
  
## <a name="example"></a>範例  
  
```vb  
Public Function SerializeOverride()  
    ' Creates an XmlElementAttribute with the alternate name.  
    Dim myElementAttribute As XmlElementAttribute = _  
    New XmlElementAttribute()  
    myElementAttribute.ElementName = "BookID"  
    Dim myAttributes As XmlAttributes = New XmlAttributes()  
    myAttributes.XmlElements.Add(myElementAttribute)  
    Dim myOverrides As XmlAttributeOverrides = New XmlAttributeOverrides()  
    myOverrides.Add(typeof(Book), "ISBN", myAttributes)  
    Dim mySerializer As XmlSerializer = _  
    New XmlSerializer(GetType(Book), myOverrides)  
    Dim b As Book = New Book()  
    b.ISBN = "123456789"  
    ' Creates a StreamWriter to write the XML stream to.  
    Dim writer As StreamWriter = New StreamWriter("Book.xml")  
    mySerializer.Serialize(writer, b);  
End Class  
```  
  
```csharp  
public void SerializeOverride()  
{  
    // Creates an XmlElementAttribute with the alternate name.  
    XmlElementAttribute myElementAttribute = new XmlElementAttribute();  
    myElementAttribute.ElementName = "BookID";  
    XmlAttributes myAttributes = new XmlAttributes();  
    myAttributes.XmlElements.Add(myElementAttribute);  
    XmlAttributeOverrides myOverrides = new XmlAttributeOverrides();  
    myOverrides.Add(typeof(Book), "ISBN", myAttributes);  
    XmlSerializer mySerializer =
    new XmlSerializer(typeof(Book), myOverrides)  
    Book b = new Book();  
    b.ISBN = "123456789"  
    // Creates a StreamWriter to write the XML stream to.  
    StreamWriter writer = new StreamWriter("Book.xml");  
    mySerializer.Serialize(writer, b);  
}  
```  
  
 XML 資料流可能類似下列所示。  
  
```xml  
<Book>  
    <BookID>123456789</BookID>  
</Book>  
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Xml.Serialization.XmlElementAttribute>
- <xref:System.Xml.Serialization.XmlAttributes>
- <xref:System.Xml.Serialization.XmlAttributeOverrides>
- [XML 和 SOAP 序列化](xml-and-soap-serialization.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [HOW TO：序列化物件](how-to-serialize-an-object.md)
- [如何：還原序列化物件](how-to-deserialize-an-object.md)
