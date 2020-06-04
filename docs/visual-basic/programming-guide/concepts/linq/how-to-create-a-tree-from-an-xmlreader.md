---
title: 作法：從 XmlReader 建立樹狀結構
ms.date: 07/20/2015
ms.assetid: 6de683d8-177d-402b-b0de-d0539f1ce5d8
ms.openlocfilehash: 25c15ff08563b12b26041a536dfbca1c9cce260a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414604"
---
# <a name="how-to-create-a-tree-from-an-xmlreader-visual-basic"></a>如何：從 XmlReader 建立樹狀結構（Visual Basic）

這個主題顯示如何從 <xref:System.Xml.XmlReader> 直接建立 XML 樹狀結構。 若要從 <xref:System.Xml.Linq.XElement> 建立 <xref:System.Xml.XmlReader>，您必須將 <xref:System.Xml.XmlReader> 定位在項目節點上。 <xref:System.Xml.XmlReader> 將會略過註解與處理指示，但是，如果 <xref:System.Xml.XmlReader> 定位在文字節點上，則會擲出錯誤。 若要避免此類的錯誤，請務必將 <xref:System.Xml.XmlReader> 定位在項目上，然後再從 <xref:System.Xml.XmlReader> 建立 XML 樹狀結構。

## <a name="example"></a>範例

此範例使用下列 XML 文件︰[範例 XML 檔：書籍 (LINQ to XML)](sample-xml-file-books-linq-to-xml.md)。

下列程式碼會建立 `T:System.Xml.XmlReader` 物件，然後讀取節點，直到找到第一個項目節點為止。 接著，它會載入 <xref:System.Xml.Linq.XElement> 物件。

```vb
Dim r As XmlReader = XmlReader.Create("books.xml")
Do While r.NodeType <> XmlNodeType.Element
    r.Read()
Loop
Dim e As XElement = XElement.Load(r)
Console.WriteLine(e)
```

這個範例會產生下列輸出：

```xml
<Catalog>
   <Book id="bk101">
      <Author>Garghentini, Davide</Author>
      <Title>XML Developer's Guide</Title>
      <Genre>Computer</Genre>
      <Price>44.95</Price>
      <PublishDate>2000-10-01</PublishDate>
      <Description>An in-depth look at creating applications
      with XML.</Description>
   </Book>
   <Book id="bk102">
      <Author>Garcia, Debra</Author>
      <Title>Midnight Rain</Title>
      <Genre>Fantasy</Genre>
      <Price>5.95</Price>
      <PublishDate>2000-12-16</PublishDate>
      <Description>A former architect battles corporate zombies,
      an evil sorceress, and her own childhood to become queen
      of the world.</Description>
   </Book>
</Catalog>
```

## <a name="see-also"></a>另請參閱

- [剖析 XML （Visual Basic）](parsing-xml.md)
