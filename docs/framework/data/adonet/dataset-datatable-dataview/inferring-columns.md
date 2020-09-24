---
title: 推斷資料行
ms.date: 03/30/2017
ms.assetid: 0e022699-c922-454c-93e2-957dd7e7247a
ms.openlocfilehash: 45d27b78b5d83d333c16192e172e7b7e3dd88c10
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91164697"
---
# <a name="inferring-columns"></a>推斷資料行

ADO.NET 從 XML 文件中判斷要將哪些項目推斷成 <xref:System.Data.DataSet> 的資料表後，接著就會推斷這些資料表的資料行。 ADO.NET 2.0 引進了新的架構推斷引擎，可推斷每個 **simpleType** 專案的強型別資料型別。 在先前的版本中，推斷的 **simpleType** 專案的資料類型一律為 **xsd： string**。  
  
## <a name="migration-and-backward-compatibility"></a>移轉和回溯相容性  

 **ReadXml**方法會採用**InferSchema**類型的引數。 這個引數可讓您指定與舊版本相容的推斷行為。 下表顯示 **InferSchema** 列舉的可用值。  
  
 <xref:System.Data.XmlReadMode.InferSchema>  
 將簡單型別永遠推斷為 <xref:System.String>，以提供回溯相容性 (Backward Compatibility)。  
  
 <xref:System.Data.XmlReadMode.InferTypedSchema>  
 推斷強型別資料型別。 若用於 <xref:System.Data.DataTable>，則會擲回例外狀況 (Exception)。  
  
 <xref:System.Data.XmlReadMode.IgnoreSchema>  
 忽略任何內嵌結構描述，並將資料讀入現有的 <xref:System.Data.DataSet> 結構描述中。  
  
## <a name="attributes"></a>屬性  

 如 [推斷資料表](inferring-tables.md)中所定義，具有屬性的元素將會推斷為數據表。 然後，該項目的屬性會推斷為資料表的資料行。 資料行的 **ColumnMapping** 屬性將會設定為 **MappingType**，以確保將架構寫回 XML 時，資料行名稱會寫入為屬性。 屬性的值儲存在資料表的資料列中。 例如，請考量下列 XML：  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 推斷進程會產生名為 **Element1** 的資料表，其中包含兩個數據行： **attr1** 和 **attr2**。 這兩個數據行的 **ColumnMapping** 屬性將會設定為 **MappingType. Attribute**。  
  
 **資料集：** DocumentElement  
  
 **資料表：** Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|value1|value2|  
  
## <a name="elements-without-attributes-or-child-elements"></a>沒有屬性或項目子系的項目  

 如果項目沒有項目子系或屬性，則會推斷為資料行。 資料行的 **ColumnMapping** 屬性將會設定為 **MappingType. Element**。 項目子系的文字儲存在資料表的資料列中。 例如，請考量下列 XML：  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 推斷進程會產生名為 **Element1** 的資料表，其中包含兩個數據行： **ChildElement1** 和 **ChildElement2**。 這兩個數據行的 **ColumnMapping** 屬性將會設定為 **MappingType. Element**。  
  
 **資料集：** DocumentElement  
  
 **資料表：** Element1  
  
|ChildElement1|ChildElement2|  
|-------------------|-------------------|  
|Text1|Text2|  
  
## <a name="see-also"></a>另請參閱

- [從 XML 推斷資料集關聯式結構](inferring-dataset-relational-structure-from-xml.md)
- [從 XML 載入資料集](loading-a-dataset-from-xml.md)
- [從 XML 載入資料集結構描述資訊](loading-dataset-schema-information-from-xml.md)
- [在資料集中使用 XML](using-xml-in-a-dataset.md)
- [DataSet、DataTable 和 DataView](index.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)
