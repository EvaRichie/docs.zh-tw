---
title: 作法：擷取單一屬性 (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: 11b938d7-c011-4048-900e-8b9183c41c94
ms.openlocfilehash: 34c390fbffc1aea68a2fd8ae64b17d2637a1f4f1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397852"
---
# <a name="how-to-retrieve-a-single-attribute-linq-to-xml-visual-basic"></a>如何：取出單一屬性（LINQ to XML）（Visual Basic）
這個主題會說明如何擷取項目的單一屬性 (如果有屬性名稱)。 這在撰寫您要尋找具有特定屬性之項目的查詢運算式時，相當實用。  
  
 <xref:System.Xml.Linq.XElement.Attribute%2A> 類別的 <xref:System.Xml.Linq.XElement> 方法會傳回具有指定之名稱的 <xref:System.Xml.Linq.XAttribute>。  
  
## <a name="example"></a>範例  
 下列範例使用 <xref:System.Xml.Linq.XElement.Attribute%2A> 方法。  
  
```vb  
Dim cust As XElement = <PhoneNumbers>  
                           <Phone type="home">555-555-5555</Phone>  
                           <Phone type="work">555-555-6666</Phone>  
                       </PhoneNumbers>  
Dim elList = From el In cust...<Phone>  
For Each e As XElement In elList  
    Console.WriteLine(e.@type)  
Next  
```  
  
 此範例將尋找名為 `Phone` 樹狀結構中所有的子代，然後尋找名為 `type` 的屬性。  
  
 此程式碼會產生下列輸出：  
  
```console  
home  
work  
```  
  
## <a name="example"></a>範例  
 如果您要擷取屬性的值，您可以進行轉型，如同將 <xref:System.Xml.Linq.XElement> 物件轉型。 下列範例示範此作業。  
  
```vb  
Dim cust As XElement = <PhoneNumbers>  
                           <Phone type="home">555-555-5555</Phone>  
                           <Phone type="work">555-555-6666</Phone>  
                       </PhoneNumbers>  
Dim elList As IEnumerable(Of XElement) = _  
    From el In cust...<Phone> _  
    Select el  
For Each el As XElement In elList  
    Console.WriteLine(el.@type)  
Next  
```  
  
 此程式碼會產生下列輸出：  
  
```console  
home  
work  
```  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 提供了 <xref:System.Xml.Linq.XAttribute> 類別至 `string`、`bool`、`bool?`、`int`、`int?`、`uint`、`uint?`、`long`、`long?`、`ulong`、`ulong?`、`float`、`float?`、`double`、`double?`、`decimal`、`decimal?`、`DateTime`、`DateTime?`、`TimeSpan`、`TimeSpan?`、`GUID` 及 `GUID?` 的明確轉換運算子。  
  
## <a name="example"></a>範例  
 下列範例顯示命名空間中之屬性的相同程式碼。 如需詳細資訊，請參閱[命名空間總覽（LINQ to XML）（Visual Basic）](namespaces-overview-linq-to-xml.md)。  
  
```vb  
Imports <xmlns:aw="http://www.adventure-works.com">  
  
Module Module1  
    Sub Main()  
        Dim cust As XElement = _  
            <aw:PhoneNumbers>  
                <aw:Phone aw:type="home">555-555-5555</aw:Phone>  
                <aw:Phone aw:type="work">555-555-6666</aw:Phone>  
            </aw:PhoneNumbers>  
        Dim elList As IEnumerable(Of XElement) = _  
            From el In cust...<aw:Phone> _  
            Select el  
        For Each el As XElement In elList  
            Console.WriteLine(el.@aw:type)  
        Next  
    End Sub  
End Module  
```  
  
 此程式碼會產生下列輸出：  
  
```console  
home  
work  
```  
  
## <a name="see-also"></a>另請參閱

- [LINQ to XML 軸 (Visual Basic)](linq-to-xml-axes.md)
