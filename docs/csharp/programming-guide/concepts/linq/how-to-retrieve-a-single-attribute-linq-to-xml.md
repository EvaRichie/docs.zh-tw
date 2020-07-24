---
title: '如何取出單一屬性（LINQ to XML）（c #）'
description: '瞭解如何在給定屬性名稱的情況下，使用 LINQ to XML 抓取 c # 中元素的單一屬性。'
ms.date: 07/20/2015
ms.assetid: 1b6b07b9-933f-47e9-874e-e790cab49dc5
ms.openlocfilehash: 4efcae5324ad5a2e4664e68e35e15ec2053daece
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87103435"
---
# <a name="how-to-retrieve-a-single-attribute-linq-to-xml-c"></a>如何取出單一屬性（LINQ to XML）（c #）
這個主題會說明如何擷取項目的單一屬性 (如果有屬性名稱)。 這在撰寫您要尋找具有特定屬性之項目的查詢運算式時，相當實用。  
  
 <xref:System.Xml.Linq.XElement.Attribute%2A> 類別的 <xref:System.Xml.Linq.XElement> 方法會傳回具有指定之名稱的 <xref:System.Xml.Linq.XAttribute>。  
  
## <a name="example"></a>範例  
 下列範例使用 <xref:System.Xml.Linq.XElement.Attribute%2A> 方法。  
  
```csharp  
XElement cust = new XElement("PhoneNumbers",  
    new XElement("Phone",  
        new XAttribute("type", "home"),  
        "555-555-5555"),  
    new XElement("Phone",  
        new XAttribute("type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =  
    from el in cust.Descendants("Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute("type"));  
```  
  
 此範例將尋找名為 `Phone` 樹狀結構中所有的子代，然後尋找名為 `type` 的屬性。  
  
 此程式碼會產生下列輸出：  
  
```output  
home  
work  
```  
  
## <a name="example"></a>範例  
 如果您要擷取屬性的值，您可以進行轉型，如同將 <xref:System.Xml.Linq.XElement> 物件轉型。 下列範例示範此作業。  
  
```csharp  
XElement cust = new XElement("PhoneNumbers",  
    new XElement("Phone",  
        new XAttribute("type", "home"),  
        "555-555-5555"),  
    new XElement("Phone",  
        new XAttribute("type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =
    from el in cust.Descendants("Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute("type"));  
```  
  
 此程式碼會產生下列輸出：  
  
```output  
home  
work  
```  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 提供了 <xref:System.Xml.Linq.XAttribute> 類別至 `string`、`bool`、`bool?`、`int`、`int?`、`uint`、`uint?`、`long`、`long?`、`ulong`、`ulong?`、`float`、`float?`、`double`、`double?`、`decimal`、`decimal?`、`DateTime`、`DateTime?`、`TimeSpan`、`TimeSpan?`、`GUID` 及 `GUID?` 的明確轉換運算子。  
  
## <a name="example"></a>範例  
 下列範例顯示命名空間中之屬性的相同程式碼。 如需詳細資訊，請參閱[命名空間概觀 (LINQ to XML) (C#)](namespaces-overview-linq-to-xml.md)。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement cust = new XElement(aw + "PhoneNumbers",  
    new XElement(aw + "Phone",  
        new XAttribute(aw + "type", "home"),  
        "555-555-5555"),  
    new XElement(aw + "Phone",  
        new XAttribute(aw + "type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =  
    from el in cust.Descendants(aw + "Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute(aw + "type"));  
```  
  
 此程式碼會產生下列輸出：  
  
```output  
home  
work  
```  
  
## <a name="see-also"></a>請參閱

- [LINQ to XML 座標軸 (C#)](./linq-to-xml-axes-overview.md)
