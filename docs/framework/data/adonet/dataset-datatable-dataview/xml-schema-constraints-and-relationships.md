---
title: XML 結構描述條件約束和關聯性
ms.date: 03/30/2017
ms.assetid: 165bc2bc-60a1-40e0-9b89-7c68ef979079
ms.openlocfilehash: 5861386e42defa189aaa50a3af0bd95d7e9257fd
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173701"
---
# <a name="xml-schema-constraints-and-relationships"></a><span data-ttu-id="e00ee-102">XML 結構描述條件約束和關聯性</span><span class="sxs-lookup"><span data-stu-id="e00ee-102">XML Schema Constraints and Relationships</span></span>

<span data-ttu-id="e00ee-103">在 XML 架構定義語言 (XSD) 架構中，您可以使用 **msdata： Relationship** 注釋 (，指定 (unique、key 和 keyref 條件約束的條件約束) 和關聯性) 。</span><span class="sxs-lookup"><span data-stu-id="e00ee-103">In an XML Schema definition language (XSD) schema, you can specify constraints (unique, key, and keyref constraints) and relationships (using the **msdata:Relationship** annotation).</span></span> <span data-ttu-id="e00ee-104">這個主題會說明 XML 結構描述中指定的條件約束和關聯性如何經過解譯以產生 <xref:System.Data.DataSet>。</span><span class="sxs-lookup"><span data-stu-id="e00ee-104">This topic explains how the constraints and relationships specified in an XML Schema are interpreted to generate the <xref:System.Data.DataSet>.</span></span>  
  
 <span data-ttu-id="e00ee-105">一般而言，如果您只想要在**資料集中**產生關聯性，請在 XML 架構中指定**msdata： Relationship**注釋。</span><span class="sxs-lookup"><span data-stu-id="e00ee-105">In general, in an XML Schema, you specify the **msdata:Relationship** annotation if you want to generate only relationships in the **DataSet**.</span></span> <span data-ttu-id="e00ee-106">如需詳細資訊，請參閱 [從 XML 架構產生資料集關聯 (XSD) ](generating-dataset-relations-from-xml-schema-xsd.md)。</span><span class="sxs-lookup"><span data-stu-id="e00ee-106">For more information, see [Generating DataSet Relations from XML Schema (XSD)](generating-dataset-relations-from-xml-schema-xsd.md).</span></span> <span data-ttu-id="e00ee-107">如果您想要在 **資料集中**產生條件約束，您可以指定條件約束 (unique、key 和 keyref) 。</span><span class="sxs-lookup"><span data-stu-id="e00ee-107">You specify constraints (unique, key, and keyref) if you want to generate constraints in the **DataSet**.</span></span> <span data-ttu-id="e00ee-108">請注意，索引鍵條件約束和 keyref 條件約束也用於產生關聯性，詳情請見這個主題的後續說明。</span><span class="sxs-lookup"><span data-stu-id="e00ee-108">Note that the key and keyref constraints are also used to generate relationships, as explained later in this topic.</span></span>  
  
## <a name="generating-a-relationship-from-key-and-keyref-constraints"></a><span data-ttu-id="e00ee-109">從索引鍵條件約束和 keyref 條件約束產生關聯性</span><span class="sxs-lookup"><span data-stu-id="e00ee-109">Generating a Relationship from key and keyref Constraints</span></span>  

 <span data-ttu-id="e00ee-110">您可以指定索引鍵和 keyref 條件約束，而不是指定 **msdata： Relationship** 注釋，而是在 XML 架構對應程式中，用來產生不只產生條件約束，也不會產生 **資料集**內的關聯性。</span><span class="sxs-lookup"><span data-stu-id="e00ee-110">Instead of specifying the **msdata:Relationship** annotation, you can specify key and keyref constraints, which are used during the XML Schema mapping process to generate not only the constraints but also the relationship in the **DataSet**.</span></span> <span data-ttu-id="e00ee-111">但是，如果您 `msdata:ConstraintOnly="true"` 在 **keyref** 專案中指定， **資料集** 只會包含條件約束，且不會包含關聯性。</span><span class="sxs-lookup"><span data-stu-id="e00ee-111">However, if you specify `msdata:ConstraintOnly="true"` in the **keyref** element, the **DataSet** will include only the constraints and will not include the relationship.</span></span>  
  
 <span data-ttu-id="e00ee-112">下列範例顯示的 XML 架構包含 **Order** 和 **OrderDetail** 專案，這些專案未進行嵌套。</span><span class="sxs-lookup"><span data-stu-id="e00ee-112">The following example shows an XML Schema that includes **Order** and **OrderDetail** elements, which are not nested.</span></span> <span data-ttu-id="e00ee-113">結構描述也指定索引鍵條件約束和 keyref 條件約束。</span><span class="sxs-lookup"><span data-stu-id="e00ee-113">The schema also specifies key and keyref constraints.</span></span>  
  
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
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 <span data-ttu-id="e00ee-114">XML 架構對應進程期間所產生的 **資料集會** 包含 **Order** 和 **OrderDetail** 資料表。</span><span class="sxs-lookup"><span data-stu-id="e00ee-114">The **DataSet** that is generated during the XML Schema mapping process includes the **Order** and **OrderDetail** tables.</span></span> <span data-ttu-id="e00ee-115">此外， **資料集** 也包含關聯性和條件約束。</span><span class="sxs-lookup"><span data-stu-id="e00ee-115">In addition, the **DataSet** includes relationships and constraints.</span></span> <span data-ttu-id="e00ee-116">下列範例會顯示這些關聯性和條件約束。</span><span class="sxs-lookup"><span data-stu-id="e00ee-116">The following example shows these relationships and constraints.</span></span> <span data-ttu-id="e00ee-117">請注意，架構不會指定 **msdata： Relationship** 注釋;相反地，索引鍵和 keyref 條件約束會用來產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e00ee-117">Note that the schema does not specify the **msdata:Relationship** annotation; instead, the key and keyref constraints are used to generate the relation.</span></span>  
  
```text
....ConstraintName: OrderNumberKey  
....Type: UniqueConstraint  
....Table: Order  
....Columns: OrderNumber  
....IsPrimaryKey: False  
  
....ConstraintName: OrderNoRef  
....Type: ForeignKeyConstraint  
....Table: OrderDetail  
....Columns: OrderNo  
....RelatedTable: Order  
....RelatedColumns: OrderNumber  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
```  
  
 <span data-ttu-id="e00ee-118">在先前的架構範例中， **Order** 和 **OrderDetail** 元素不會進行嵌套。</span><span class="sxs-lookup"><span data-stu-id="e00ee-118">In the previous schema example, the **Order** and **OrderDetail** elements are not nested.</span></span> <span data-ttu-id="e00ee-119">下列的結構描述範例中，這些項目則為巢狀化。</span><span class="sxs-lookup"><span data-stu-id="e00ee-119">In the following schema example, these elements are nested.</span></span> <span data-ttu-id="e00ee-120">但是，不會指定 **msdata： Relationship** 注釋;因此，會假設隱含關聯性。</span><span class="sxs-lookup"><span data-stu-id="e00ee-120">However, no **msdata:Relationship** annotation is specified; therefore, an implicit relation is assumed.</span></span> <span data-ttu-id="e00ee-121">如需詳細資訊，請參閱 [對應嵌套架構元素之間的隱含](map-implicit-relations-between-nested-schema-elements.md)關聯。</span><span class="sxs-lookup"><span data-stu-id="e00ee-121">For more information, see [Map Implicit Relations Between Nested Schema Elements](map-implicit-relations-between-nested-schema-elements.md).</span></span> <span data-ttu-id="e00ee-122">結構描述也指定索引鍵條件約束和 keyref 條件約束。</span><span class="sxs-lookup"><span data-stu-id="e00ee-122">The schema also specifies key and keyref constraints.</span></span>  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""
            xmlns:xs="http://www.w3.org/2001/XMLSchema"
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:integer" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 <span data-ttu-id="e00ee-123">XML 架構對應進程所產生的 **資料集會** 包含兩個數據表：</span><span class="sxs-lookup"><span data-stu-id="e00ee-123">The **DataSet** resulting from the XML Schema mapping process includes two tables:</span></span>  
  
```text  
Order(OrderNumber, EmpNumber, Order_Id)  
OrderDetail(OrderNumber, ItemNumber, Order_Id)  
```  
  
 <span data-ttu-id="e00ee-124">**資料集**也包含兩個關聯性 (一個以**msdata： relationship**注釋為基礎，而另一個是根據索引鍵和 keyref 條件約束) 和各種條件約束。</span><span class="sxs-lookup"><span data-stu-id="e00ee-124">The **DataSet** also includes the two relationships (one based on the **msdata:relationship** annotation and the other based on the key and keyref constraints) and various constraints.</span></span> <span data-ttu-id="e00ee-125">下列範例顯示關聯和條件約束。</span><span class="sxs-lookup"><span data-stu-id="e00ee-125">The following example shows the relations and constraints.</span></span>  
  
```text
..RelationName: Order_OrderDetail  
..ParentTable: Order  
..ParentColumns: Order_Id  
..ChildTable: OrderDetail  
..ChildColumns: Order_Id  
..ParentKeyConstraint: Constraint1  
..ChildKeyConstraint: Order_OrderDetail  
..Nested: True  
  
..RelationName: OrderNoRef  
..ParentTable: Order  
..ParentColumns: OrderNumber  
..ChildTable: OrderDetail  
..ChildColumns: OrderNo  
..ParentKeyConstraint: OrderNumberKey  
..ChildKeyConstraint: OrderNoRef  
..Nested: False  
  
..ConstraintName: OrderNumberKey  
..Type: UniqueConstraint  
..Table: Order  
..Columns: OrderNumber  
..IsPrimaryKey: False  
  
..ConstraintName: Constraint1  
..Type: UniqueConstraint  
..Table: Order  
..Columns: Order_Id  
..IsPrimaryKey: True  
  
..ConstraintName: Order_OrderDetail  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: Order_Id  
..RelatedTable: Order  
..RelatedColumns: Order_Id  
  
..ConstraintName: OrderNoRef  
..Type: ForeignKeyConstraint  
..Table: OrderDetail  
..Columns: OrderNo  
..RelatedTable: Order  
..RelatedColumns: OrderNumber  
```  
  
 <span data-ttu-id="e00ee-126">如果參考嵌套資料表的 keyref 條件約束包含 **msdata： IsNested = "true"** 注釋， **資料集** 將會建立以 keyref 條件約束和相關 unique/key 條件約束為基礎的單一嵌套關聯性。</span><span class="sxs-lookup"><span data-stu-id="e00ee-126">If a keyref constraint referring to a nested table contains the **msdata:IsNested="true"** annotation, the **DataSet** will create a single nested relationship that is based on the keyref constraint and the related unique/key constraint.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e00ee-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e00ee-127">See also</span></span>

- [<span data-ttu-id="e00ee-128">從 XML 結構描述 (XSD) 衍生資料集關聯式結構</span><span class="sxs-lookup"><span data-stu-id="e00ee-128">Deriving DataSet Relational Structure from XML Schema (XSD)</span></span>](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- <span data-ttu-id="e00ee-129">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="e00ee-129">[ADO.NET Overview](../ado-net-overview.md)</span></span>
