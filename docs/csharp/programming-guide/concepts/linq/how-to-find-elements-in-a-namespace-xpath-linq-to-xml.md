---
title: '如何尋找命名空間中的元素（XPath-LINQ to XML）（c #）'
description: 瞭解如何使用 XPath 運算式尋找命名空間中的元素。 如需讀取包含兩個命名空間之 XML 樹狀結構的範例，請參閱。
ms.date: 07/20/2015
ms.assetid: cae1c4ac-6cd5-46cf-9b1c-bd85bc9b7ea9
ms.openlocfilehash: 3bf15c4183e3ca339fa7090c21baff83526e37d3
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303227"
---
# <a name="how-to-find-elements-in-a-namespace-xpath-linq-to-xml-c"></a>如何尋找命名空間中的元素（XPath-LINQ to XML）（c #）

XPath 運算式可以在特定的命名空間中尋找節點。 XPath 運算式使用命名空間前置詞來指定命名空間。 若要剖析包含命名空間前置詞的 XPath 運算式，您必須將物件傳遞到實作 <xref:System.Xml.IXmlNamespaceResolver> 的 XPath 方法。 此範例會使用 <xref:System.Xml.XmlNamespaceManager>。

XPath 運算式為：

`./aw:*`

## <a name="example"></a>範例

下列範例會讀取包含兩個命名空間的 XML 樹狀。 該範例會使用 <xref:System.Xml.XmlReader> 來讀取 XML 文件。 接著，它會從 <xref:System.Xml.XmlNameTable> 取得 <xref:System.Xml.XmlReader>，並從 <xref:System.Xml.XmlNamespaceManager> 取得 <xref:System.Xml.XmlNameTable>。 選取項目時，它會使用 <xref:System.Xml.XmlNamespaceManager>。

```csharp
XmlReader reader = XmlReader.Create("ConsolidatedPurchaseOrders.xml");
XElement root = XElement.Load(reader);
XmlNameTable nameTable = reader.NameTable;
XmlNamespaceManager namespaceManager = new XmlNamespaceManager(nameTable);
namespaceManager.AddNamespace("aw", "http://www.adventure-works.com");
IEnumerable<XElement> list1 = root.XPathSelectElements("./aw:*", namespaceManager);
IEnumerable<XElement> list2 =
    from el in root.Elements()
    where el.Name.Namespace == "http://www.adventure-works.com"
    select el;
if (list1.Count() == list2.Count() &&
        list1.Intersect(list2).Count() == list1.Count())
    Console.WriteLine("Results are identical");
else
    Console.WriteLine("Results differ");
foreach (XElement el in list2)
    Console.WriteLine(el);
```

這個範例會產生下列輸出：

```output
Results are identical
<aw:PurchaseOrder PONumber="11223" Date="2000-01-15" xmlns:aw="http://www.adventure-works.com">
    <aw:ShippingAddress>
      <aw:Name>Chris Preston</aw:Name>
      <aw:Street>123 Main St.</aw:Street>
      <aw:City>Seattle</aw:City>
      <aw:State>WA</aw:State>
      <aw:Zip>98113</aw:Zip>
      <aw:Country>USA</aw:Country>
    </aw:ShippingAddress>
    <aw:BillingAddress>
      <aw:Name>Chris Preston</aw:Name>
      <aw:Street>123 Main St.</aw:Street>
      <aw:City>Seattle</aw:City>
      <aw:State>WA</aw:State>
      <aw:Zip>98113</aw:Zip>
      <aw:Country>USA</aw:Country>
    </aw:BillingAddress>
    <aw:DeliveryInstructions>Ship only complete order.</aw:DeliveryInstructions>
    <aw:Item PartNum="LIT-01">
      <aw:ProductID>Litware Networking Card</aw:ProductID>
      <aw:Qty>1</aw:Qty>
      <aw:Price>20.99</aw:Price>
    </aw:Item>
    <aw:Item PartNum="LIT-25">
      <aw:ProductID>Litware 17in LCD Monitor</aw:ProductID>
      <aw:Qty>1</aw:Qty>
      <aw:Price>199.99</aw:Price>
    </aw:Item>
  </aw:PurchaseOrder>
```
