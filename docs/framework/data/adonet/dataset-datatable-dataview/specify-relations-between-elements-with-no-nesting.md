---
title: 指定未巢狀放置之項目間的關聯
ms.date: 03/30/2017
ms.assetid: e31325da-7691-4d33-acf4-99fccca67006
ms.openlocfilehash: 6684e992242d5c695f3c237f70de61b4dae1c48f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183399"
---
# <a name="specify-relations-between-elements-with-no-nesting"></a>指定未巢狀放置之項目間的關聯

項目未巢狀化時，不會建立任何隱含關聯， 不過，您可以使用 **msdata： Relationship** 注釋，明確地指定未以嵌套的元素之間的關聯性。  
  
 下列範例顯示 XML 架構，其中 **msdata： Relationship** 注釋是在 **Order** 和 **OrderDetail** 元素（不是嵌套）之間指定的。 **Msdata： Relationship**注釋指定為**Schema**元素的子項目。  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""
             xmlns:xs="http://www.w3.org/2001/XMLSchema"
             xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:string" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNumber" type="xs:string" />  
           <xs:element name="EmpNumber" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  </xs:element>  
   <xs:annotation>  
     <xs:appinfo>  
       <msdata:Relationship name="OrdOrderDetailRelation"  
                            msdata:parent="Order"
                            msdata:child="OrderDetail"
                            msdata:parentkey="OrderNumber"
                            msdata:childkey="OrderNo"/>  
     </xs:appinfo>  
  </xs:annotation>  
</xs:schema>  
```  
  
 XML 架構定義語言 (XSD) 架構對應進程會建立 <xref:System.Data.DataSet> 具有 **Order** 和 **OrderDetail** 資料表的，以及這兩個數據表之間指定的關聯性，如下所示。  
  
```text  
RelationName: OrdOrderDetailRelation  
ParentTable: Order  
ParentColumns: OrderNumber
ChildTable: OrderDetail  
ChildColumns: OrderNo
Nested: False  
```  
  
## <a name="see-also"></a>另請參閱

- [從 XML 結構描述 (XSD) 產生資料集關聯](generating-dataset-relations-from-xml-schema-xsd.md)
- [將 XML 結構描述 (XSD) 條件約束對應至資料集條件約束](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)
