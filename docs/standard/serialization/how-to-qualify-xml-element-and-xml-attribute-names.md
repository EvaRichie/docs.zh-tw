---
title: 如何限定 XML 元素和 XML 屬性名稱
description: 本文說明如何在 XML 檔中限定 XML 元素和 XML 屬性的名稱。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- qualifying XML names
- qualifying XML elements
- XML namespaces, qualifying elements and names in
ms.assetid: 44719f90-7e15-42e8-a9e2-282287e2b5bf
ms.openlocfilehash: 6c29e03d9ce28e5b0abc68a5d7e8d82f4485ac93
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "83378405"
---
# <a name="how-to-qualify-xml-element-and-xml-attribute-names"></a>如何限定 XML 元素和 XML 屬性名稱

類別實例所包含的 XML 命名空間 <xref:System.Xml.Serialization.XmlSerializerNamespaces> 必須符合[在 XML 中稱為命名空間](https://www.w3.org/TR/REC-xml-names/)的全球資訊網協會（W3C）規格。

XML 命名空間提供限定 XML 文件中 XML 項目和 XML 屬性名稱的方法。 限定名稱 (Qualified Name) 是由前置詞和本機名稱所組成，並以半形冒號 (:) 隔開。 前置詞的作用只是個替代符號 (Placeholder)，它會對應到指定命名空間的 URI。 通用管理的 URI 命名空間和本機名稱的組合會產生保證是通用唯一的名稱。

藉由建立 `XmlSerializerNamespaces` 執行個體以及將命名空間配對加入物件中，您可指定 XML 文件使用的前置詞。

## <a name="to-create-qualified-names-in-an-xml-document"></a>若要在 XML 文件中建立限定名稱

1. 建立 `XmlSerializerNamespaces` 類別的執行個體。

2. 加入所有前置詞與命名空間配對至 `XmlSerializerNamespaces`。

3. 套用適當的 `System.Xml.Serialization` 屬性至 <xref:System.Xml.Serialization.XmlSerializer> 將要序列化至 XML 文件的每個成員或類別。

    可用的屬性為：<xref:System.Xml.Serialization.XmlAnyElementAttribute>、<xref:System.Xml.Serialization.XmlArrayAttribute>、<xref:System.Xml.Serialization.XmlArrayItemAttribute>、<xref:System.Xml.Serialization.XmlAttributeAttribute>、<xref:System.Xml.Serialization.XmlElementAttribute>、<xref:System.Xml.Serialization.XmlRootAttribute> 與 <xref:System.Xml.Serialization.XmlTypeAttribute>。

4. 將每個屬性 (Attribute) 的 `Namespace` 屬性 (Property) 設定為 `XmlSerializerNamespaces` 的其中一個命名空間值。

5. 傳遞 `XmlSerializerNamespaces` 至 `Serialize` 的 `XmlSerializer` 方法。

## <a name="example"></a>範例

下列範例建立 `XmlSerializerNamespaces`，並在物件加入兩個前置詞和命名空間配對。 程式碼建立用來系列化 `XmlSerializer` 類別執行個體的 `Books`。 程式碼以 呼叫  方法，讓 XML 能包含有前置詞的命名空間。

```vb
Imports System.IO
Imports System.Xml
Imports System.Xml.Serialization

Public Module Program

    Public Sub Main()
        SerializeObject("XmlNamespaces.xml")
    End Sub

    Public Sub SerializeObject(filename As String)
        Dim mySerializer As New XmlSerializer(GetType(Books))
        ' Writing a file requires a TextWriter.
        Dim myWriter As New StreamWriter(filename)

        ' Creates an XmlSerializerNamespaces and adds two
        ' prefix-namespace pairs.
        Dim myNamespaces As New XmlSerializerNamespaces()
        myNamespaces.Add("books", "http://www.cpandl.com")
        myNamespaces.Add("money", "http://www.cohowinery.com")

        ' Creates a Book.
        Dim myBook As New Book()
        myBook.TITLE = "A Book Title"
        Dim myPrice As New Price()
        myPrice.price = CDec(9.95)
        myPrice.currency = "US Dollar"
        myBook.PRICE = myPrice
        Dim myBooks As New Books()
        myBooks.Book = myBook
        mySerializer.Serialize(myWriter, myBooks, myNamespaces)
        myWriter.Close()
    End Sub
End Module

Public Class Books
    <XmlElement([Namespace] := "http://www.cohowinery.com")> _
    Public Book As Book
End Class

<XmlType([Namespace] := "http://www.cpandl.com")> _
Public Class Book
    <XmlElement([Namespace] := "http://www.cpandl.com")> _
    Public TITLE As String
    <XmlElement([Namespace] := "http://www.cohowinery.com")> _
    Public PRICE As Price
End Class

Public Class Price
    <XmlAttribute([Namespace] := "http://www.cpandl.com")> _
    Public currency As String
    <XmlElement([Namespace] := "http://www.cohowinery.com")> _
    Public price As Decimal
End Class
```

```csharp
using System;
using System.IO;
using System.Xml;
using System.Xml.Serialization;

public class Program
{
    public static void Main()
    {
        SerializeObject("XmlNamespaces.xml");
    }

    public static void SerializeObject(string filename)
    {
        var mySerializer = new XmlSerializer(typeof(Books));
        // Writing a file requires a TextWriter.
        TextWriter myWriter = new StreamWriter(filename);

        // Creates an XmlSerializerNamespaces and adds two
        // prefix-namespace pairs.
        var myNamespaces = new XmlSerializerNamespaces();
        myNamespaces.Add("books", "http://www.cpandl.com");
        myNamespaces.Add("money", "http://www.cohowinery.com");

        // Creates a Book.
        var myBook = new Book();
        myBook.TITLE = "A Book Title";
        var myPrice = new Price();
        myPrice.price = (decimal) 9.95;
        myPrice.currency = "US Dollar";
        myBook.PRICE = myPrice;
        var myBooks = new Books();
        myBooks.Book = myBook;
        mySerializer.Serialize(myWriter, myBooks, myNamespaces);
        myWriter.Close();
    }
}

public class Books
{
    [XmlElement(Namespace = "http://www.cohowinery.com")]
    public Book Book;
}

[XmlType(Namespace ="http://www.cpandl.com")]
public class Book
{
    [XmlElement(Namespace = "http://www.cpandl.com")]
    public string TITLE;
    [XmlElement(Namespace ="http://www.cohowinery.com")]
    public Price PRICE;
}

public class Price
{
    [XmlAttribute(Namespace = "http://www.cpandl.com")]
    public string currency;
    [XmlElement(Namespace = "http://www.cohowinery.com")]
    public decimal price;
}
```

## <a name="see-also"></a>另請參閱

- <xref:System.Xml.Serialization.XmlSerializer>
- [XML 結構描述定義工具和 XML 序列化](the-xml-schema-definition-tool-and-xml-serialization.md)
- [XML 序列化簡介](introducing-xml-serialization.md)
- [XmlSerializer 類別](xref:System.Xml.Serialization.XmlSerializer)
- [控制 XML 序列化的屬性](attributes-that-control-xml-serialization.md)
- [如何：指定 XML 資料流的替代元素名稱](how-to-specify-an-alternate-element-name-for-an-xml-stream.md)
- [HOW TO：序列化物件](how-to-serialize-an-object.md)
- [如何：還原序列化物件](how-to-deserialize-an-object.md)
