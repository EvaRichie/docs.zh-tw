---
title: 推斷關聯性
ms.date: 03/30/2017
ms.assetid: 8fa86a9d-6545-4a9d-b1f5-58d9742179c7
ms.openlocfilehash: ee691eee95c34afdb6374cdd7448d4b44ece3055
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177562"
---
# <a name="inferring-relationships"></a>推斷關聯性

若被推斷為資料表的項目具有子項目，且子項目也被推斷為資料表，則兩個資料表間會建立 <xref:System.Data.DataRelation>。 名稱為 **ParentTableName_Id** 的新資料行，將會加入針對父元素建立的資料表，以及針對子專案所建立的資料表。 這個識別欄位的**ColumnMapping**屬性將會設定為**MappingType。** 此資料行將會是父資料表的自動遞增主鍵，而且將用於這兩個數據表之間的 **DataRelation** 。 除了其他所有推斷資料行的資料類型（ **system.string**）之外，已加入之識別欄位的資料類型將為**system.object。** <xref:System.Data.ForeignKeyConstraint>此外， **DeleteRule**  =  也會使用父資料表和子資料工作表中的新資料行，建立具有 DeleteRule**Cascade**的。  
  
 例如，請考量下列 XML：  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1 attr1="value1" attr2="value2"/>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 推斷進程會產生兩個數據表： **Element1** 和 **ChildElement1**。  
  
 **Element1**資料表會有兩個數據行： **Element1_Id**和**ChildElement2**。 **Element1_Id**資料行的**ColumnMapping**屬性將會設定為**MappingType。** **ChildElement2**資料行的**ColumnMapping**屬性將會設定為**MappingType. Element**。 **Element1_Id**資料行將會設定為**Element1**資料表的主鍵。  
  
 **ChildElement1**資料表會有三個數據行： **attr1**、 **attr2**及**Element1_Id**。 **Attr1**和**attr2**資料行的**ColumnMapping**屬性將會設定為**MappingType. Attribute**。 **Element1_Id**資料行的**ColumnMapping**屬性將會設定為**MappingType。**  
  
 將會使用兩個數據表的**Element1_Id**資料行來建立**DataRelation**和**ForeignKeyConstraint** 。  
  
 **資料集：** DocumentElement  
  
 **資料表：** Element1  
  
|Element1_Id|ChildElement2|  
|------------------|-------------------|  
|0|Text2|  
  
 **資料表：** ChildElement1  
  
|attr1|attr2|Element1_Id|  
|-----------|-----------|------------------|  
|value1|value2|0|  
  
 **DataRelation：** Element1_ChildElement1  
  
 **ParentTable：** Element1  
  
 **ParentColumn：** Element1_Id  
  
 **ChildTable：** ChildElement1  
  
 **ChildColumn：** Element1_Id  
  
 **Nested：** 真  
  
 **ForeignKeyConstraint：** Element1_ChildElement1  
  
 資料**行：** Element1_Id  
  
 **ParentTable：** Element1  
  
 **ChildTable：** ChildElement1  
  
 **DeleteRule：** 級 聯  
  
 **AcceptRejectRule：** 沒有  
  
## <a name="see-also"></a>另請參閱

- [從 XML 推斷資料集關聯式結構](inferring-dataset-relational-structure-from-xml.md)
- [從 XML 載入資料集](loading-a-dataset-from-xml.md)
- [從 XML 載入資料集結構描述資訊](loading-dataset-schema-information-from-xml.md)
- [巢狀 DataRelation](nesting-datarelations.md)
- [在資料集中使用 XML](using-xml-in-a-dataset.md)
- [DataSet、DataTable 和 DataView](index.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)
