---
title: 將 unique XML 結構描述 (XSD) 條件約束對應至資料集條件約束
ms.date: 03/30/2017
ms.assetid: 56da90bf-21d3-4d1a-8bb8-de908866b78d
ms.openlocfilehash: 3b2dad44176e52adcf32e2e3ccff3d82ba23f6ed
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153231"
---
# <a name="map-unique-xml-schema-xsd-constraints-to-dataset-constraints"></a>將 unique XML 結構描述 (XSD) 條件約束對應至資料集條件約束

在 XML 架構定義語言 (XSD) 架構中， **unique** 元素會指定元素或屬性的唯一性條件約束。 在將 XML 結構描述轉譯到關聯式結構描述的處理序中，會將 XML 結構描述內項目或屬性上指定的唯一的條件約束 (Constraint)，對應到所產生的對應 <xref:System.Data.DataTable> 內 <xref:System.Data.DataSet> 的唯一的條件約束。  
  
 下表列出您可以在**unique**元素中指定的**msdata**屬性。  
  
|屬性名稱|描述|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|如果指定這個屬性，則它的值會被當成條件約束名稱使用。 否則， **name** 屬性會提供條件約束名稱的值。|  
|**msdata:PrimaryKey**|如果 `PrimaryKey="true"` **unique** 專案中有，則會建立唯一的條件約束，並將 **IsPrimaryKey** 屬性設定為 **true**。|  
  
 下列範例顯示使用 **unique** 專案指定唯一性條件約束的 XML 架構。  
  
```xml  
<xs:schema id="SampleDataSet"
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:integer"
           minOccurs="0"/>  
        <xs:element name="CompanyName" type="xs:string"
           minOccurs="0"/>  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
  
 <xs:element name="SampleDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:unique     msdata:ConstraintName="UCustID"     name="UniqueCustIDConstr" >       <xs:selector xpath=".//Customers" />       <xs:field xpath="CustomerID" />     </xs:unique>  
</xs:element>  
</xs:schema>  
```  
  
 架構中的 **unique** 元素會指定檔實例中所有 **Customers** 專案的， **CustomerID** 子專案的值必須是唯一的。 在建立 **資料集**時，對應進程會讀取此架構並產生下表：  
  
```text  
Customers (CustomerID, CompanyName, Phone)  
```  
  
 對應進程也會在 **CustomerID** 資料行上建立 unique 條件約束，如下列 **資料集**所示。 (為了便於了解，此處僅顯示相關屬性)。  
  
```text  
      DataSetName: MyDataSet  
TableName: Customers  
  ColumnName: CustomerID  
      AllowDBNull: True  
      Unique: True  
  ConstraintName: UcustID       Type: UniqueConstraint  
      Table: Customers  
      Columns: CustomerID
      IsPrimaryKey: False  
```  
  
 在產生的 **資料集中** ，unique 條件約束的 **IsPrimaryKey** 屬性會設為 **False** 。 資料行上的 **unique** 屬性工作表示 **CustomerID** 資料行值必須是唯一的 (但可以是 null 參考，如資料行) 的 **AllowDBNull** 屬性所指定。  
  
 如果您修改架構，並將選擇性的 **msdata： PrimaryKey** 屬性值設定為 **True**，就會在資料表上建立 unique 條件約束。 **AllowDBNull**資料行屬性設定為**False**，而且條件約束的**IsPrimaryKey**屬性設定為**True**，因此**CustomerID**資料行是主鍵資料行。  
  
 您可以在 XML 結構描述中，將唯一的條件約束指定給合併的項目或屬性。 下列範例示範如何藉由在架構中加入另一個**xs： field**專案，指定在任何實例中，所有**客戶**的**CustomerID**與**公司**值的組合必須是唯一的。  
  
```xml  
      <xs:unique
         msdata:ConstraintName="SomeName"
         name="UniqueCustIDConstr" >
  <xs:selector xpath=".//Customers" />
  <xs:field xpath="CustomerID" />
  <xs:field xpath="CompanyName" />
</xs:unique>  
```  
  
 這是在產生的 **資料集中**建立的條件約束。  
  
```text  
ConstraintName: SomeName  
  Table: Customers  
  Columns: CustomerID CompanyName
  IsPrimaryKey: False  
```  
  
## <a name="see-also"></a>另請參閱

- [將 XML 結構描述 (XSD) 條件約束對應至資料集條件約束](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [從 XML 結構描述 (XSD) 產生資料集關聯](generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)
