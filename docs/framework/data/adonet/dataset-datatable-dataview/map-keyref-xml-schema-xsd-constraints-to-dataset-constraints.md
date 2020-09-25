---
title: 將 keyref XML 結構描述 (XSD) 條件約束對應至資料集條件約束
ms.date: 03/30/2017
ms.assetid: 5b634fea-cc1e-4f6b-9454-10858105b1c8
ms.openlocfilehash: fe53232b6818b5bb28b433c4a473b6381b8e9083
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198557"
---
# <a name="map-keyref-xml-schema-xsd-constraints-to-dataset-constraints"></a><span data-ttu-id="1378e-102">將 keyref XML 結構描述 (XSD) 條件約束對應至資料集條件約束</span><span class="sxs-lookup"><span data-stu-id="1378e-102">Map keyref XML Schema (XSD) Constraints to DataSet Constraints</span></span>

<span data-ttu-id="1378e-103">**Keyref**元素可讓您在檔內的元素之間建立連結。</span><span class="sxs-lookup"><span data-stu-id="1378e-103">The **keyref** element allows you to establish links between elements within a document.</span></span> <span data-ttu-id="1378e-104">這與關聯式資料庫中的外部索引鍵關聯性很類似。</span><span class="sxs-lookup"><span data-stu-id="1378e-104">This is similar to a foreign key relationship in a relational database.</span></span> <span data-ttu-id="1378e-105">如果架構指定 **keyref** 專案，則在架構對應進程期間，會將專案轉換成資料表中的資料行上對應的外鍵條件約束 <xref:System.Data.DataSet> 。</span><span class="sxs-lookup"><span data-stu-id="1378e-105">If a schema specifies the **keyref** element, the element is converted during the schema mapping process to a corresponding foreign key constraint on the columns in the tables of the <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="1378e-106">根據預設， **keyref** 元素也會產生關聯性，並在關聯上指定 **ParentTable**、 **ChildTable**、 **ParentColumn**和 **ChildColumn** 屬性。</span><span class="sxs-lookup"><span data-stu-id="1378e-106">By default, the **keyref** element also generates a relation, with the **ParentTable**, **ChildTable**, **ParentColumn**, and **ChildColumn** properties specified on the relation.</span></span>  
  
 <span data-ttu-id="1378e-107">下表概述可在**keyref**元素中指定的**msdata**屬性。</span><span class="sxs-lookup"><span data-stu-id="1378e-107">The following table outlines the **msdata** attributes you can specify in the **keyref** element.</span></span>  
  
|<span data-ttu-id="1378e-108">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="1378e-108">Attribute name</span></span>|<span data-ttu-id="1378e-109">描述</span><span class="sxs-lookup"><span data-stu-id="1378e-109">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="1378e-110">**msdata:ConstraintOnly**</span><span class="sxs-lookup"><span data-stu-id="1378e-110">**msdata:ConstraintOnly**</span></span>|<span data-ttu-id="1378e-111">如果在架構中的**keyref**元素上指定**ConstraintOnly = "true"** ，則會建立條件約束，但不會建立關聯。</span><span class="sxs-lookup"><span data-stu-id="1378e-111">If **ConstraintOnly="true"** is specified on the **keyref** element in the schema, a constraint is created, but no relation is created.</span></span> <span data-ttu-id="1378e-112">如果未指定這個屬性 (或設定為 **False**) ，則會在 **資料集中**建立條件約束和關聯。</span><span class="sxs-lookup"><span data-stu-id="1378e-112">If this attribute is not specified (or is set to **False**), both the constraint and the relation are created in the **DataSet**.</span></span>|  
|<span data-ttu-id="1378e-113">**msdata:ConstraintName**</span><span class="sxs-lookup"><span data-stu-id="1378e-113">**msdata:ConstraintName**</span></span>|<span data-ttu-id="1378e-114">如果指定了 **ConstraintName** 屬性，則會使用其值做為條件約束的名稱。</span><span class="sxs-lookup"><span data-stu-id="1378e-114">If the **ConstraintName** attribute is specified, its value is used as the name of the constraint.</span></span> <span data-ttu-id="1378e-115">否則，架構中的**keyref**專案的**name**屬性會提供**資料集中**的條件約束名稱。</span><span class="sxs-lookup"><span data-stu-id="1378e-115">Otherwise, the **name** attribute of the **keyref** element in the schema provides the constraint name in the **DataSet**.</span></span>|  
|<span data-ttu-id="1378e-116">**msdata:UpdateRule**</span><span class="sxs-lookup"><span data-stu-id="1378e-116">**msdata:UpdateRule**</span></span>|<span data-ttu-id="1378e-117">如果在架構的**keyref**專案中指定了**UpdateRule**屬性，則會將其值指派給**資料集**內的**UpdateRule**條件約束屬性。</span><span class="sxs-lookup"><span data-stu-id="1378e-117">If the **UpdateRule** attribute is specified in the **keyref** element in the schema, its value is assigned to the **UpdateRule** constraint property in the **DataSet**.</span></span> <span data-ttu-id="1378e-118">否則， **UpdateRule** 屬性會設定為 **Cascade**。</span><span class="sxs-lookup"><span data-stu-id="1378e-118">Otherwise the **UpdateRule** property is set to **Cascade**.</span></span>|  
|<span data-ttu-id="1378e-119">**msdata:DeleteRule**</span><span class="sxs-lookup"><span data-stu-id="1378e-119">**msdata:DeleteRule**</span></span>|<span data-ttu-id="1378e-120">如果在架構的**keyref**專案中指定了**DeleteRule**屬性，則會將其值指派給**資料集**內的**DeleteRule**條件約束屬性。</span><span class="sxs-lookup"><span data-stu-id="1378e-120">If the **DeleteRule** attribute is specified in the **keyref** element in the schema, its value is assigned to the **DeleteRule** constraint property in the **DataSet**.</span></span> <span data-ttu-id="1378e-121">否則， **DeleteRule** 屬性會設定為 **Cascade**。</span><span class="sxs-lookup"><span data-stu-id="1378e-121">Otherwise the **DeleteRule** property is set to **Cascade**.</span></span>|  
|<span data-ttu-id="1378e-122">**msdata:AcceptRejectRule**</span><span class="sxs-lookup"><span data-stu-id="1378e-122">**msdata:AcceptRejectRule**</span></span>|<span data-ttu-id="1378e-123">如果在架構的**keyref**專案中指定了**AcceptRejectRule**屬性，則會將其值指派給**資料集**內的**AcceptRejectRule**條件約束屬性。</span><span class="sxs-lookup"><span data-stu-id="1378e-123">If the **AcceptRejectRule** attribute is specified in the **keyref** element in the schema, its value is assigned to the **AcceptRejectRule** constraint property in the **DataSet**.</span></span> <span data-ttu-id="1378e-124">否則， **AcceptRejectRule** 屬性會設定為 **None**。</span><span class="sxs-lookup"><span data-stu-id="1378e-124">Otherwise the **AcceptRejectRule** property is set to **None**.</span></span>|  
  
 <span data-ttu-id="1378e-125">下列範例所包含的架構，會在**Order**專案的**OrderNumber**子專案和**OrderDetail**專案的**OrderNo**子項目之間，指定索引**鍵**和**keyref**關聯性。</span><span class="sxs-lookup"><span data-stu-id="1378e-125">The following example contains a schema that specifies the **key** and **keyref** relationships between the **OrderNumber** child element of the **Order** element and the **OrderNo** child element of the **OrderDetail** element.</span></span>  
  
 <span data-ttu-id="1378e-126">在此範例中， **OrderDetail**專案的**OrderNumber**子專案會參考**Order**元素的**OrderNo** key 子項目。</span><span class="sxs-lookup"><span data-stu-id="1378e-126">In the example, the **OrderNumber** child element of the **OrderDetail** element refers to the **OrderNo** key child element of the **Order** element.</span></span>  
  
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
  
 <span data-ttu-id="1378e-127">XML 架構定義語言 (XSD) 架構對應進程會產生具有兩個數據表的下列 **資料集** ：</span><span class="sxs-lookup"><span data-stu-id="1378e-127">The XML Schema definition language (XSD) schema mapping process produces the following **DataSet** with two tables:</span></span>  
  
```text  
OrderDetail(OrderNo, ItemNo) and  
Order(OrderNumber, EmpNumber)  
```  
  
 <span data-ttu-id="1378e-128">此外， **資料集會** 定義下列條件約束：</span><span class="sxs-lookup"><span data-stu-id="1378e-128">In addition, the **DataSet** defines the following constraints:</span></span>  
  
- <span data-ttu-id="1378e-129">**Order**資料表的 unique 條件約束。</span><span class="sxs-lookup"><span data-stu-id="1378e-129">A unique constraint on the **Order** table.</span></span>  
  
    ```text
              Table: Order  
    Columns: OrderNumber
    ConstraintName: OrderNumberKey  
    Type: UniqueConstraint  
    IsPrimaryKey: False  
    ```  
  
- <span data-ttu-id="1378e-130">**Order**和**OrderDetail**資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="1378e-130">A relationship between the **Order** and **OrderDetail** tables.</span></span> <span data-ttu-id="1378e-131">**Nested**屬性會設定為**False** ，因為這兩個元素不會嵌套在架構中。</span><span class="sxs-lookup"><span data-stu-id="1378e-131">The **Nested** property is set to **False** because the two elements are not nested in the schema.</span></span>  
  
    ```text
              ParentTable: Order  
    ParentColumns: OrderNumber
    ChildTable: OrderDetail  
    ChildColumns: OrderNo
    ParentKeyConstraint: OrderNumberKey  
    ChildKeyConstraint: OrderNoRef  
    RelationName: OrderNoRef  
    Nested: False  
    ```  
  
- <span data-ttu-id="1378e-132">**OrderDetail**資料表上的 foreign key 條件約束。</span><span class="sxs-lookup"><span data-stu-id="1378e-132">A foreign key constraint on the **OrderDetail** table.</span></span>  
  
    ```text  
              ConstraintName: OrderNoRef  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: OrderNo
    RelatedTable: Order  
    RelatedColumns: OrderNumber
    ```  
  
## <a name="see-also"></a><span data-ttu-id="1378e-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1378e-133">See also</span></span>

- [<span data-ttu-id="1378e-134">將 XML 結構描述 (XSD) 條件約束對應至資料集條件約束</span><span class="sxs-lookup"><span data-stu-id="1378e-134">Mapping XML Schema (XSD) Constraints to DataSet Constraints</span></span>](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [<span data-ttu-id="1378e-135">從 XML 結構描述 (XSD) 產生資料集關聯</span><span class="sxs-lookup"><span data-stu-id="1378e-135">Generating DataSet Relations from XML Schema (XSD)</span></span>](generating-dataset-relations-from-xml-schema-xsd.md)
- <span data-ttu-id="1378e-136">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="1378e-136">[ADO.NET Overview](../ado-net-overview.md)</span></span>
