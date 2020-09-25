---
title: 類型系統 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 818a505b-a196-41dd-aaac-2ccd5f7a2f1a
ms.openlocfilehash: d4c8ba7a9d9b58220455b50ff99960fa132c00c7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200988"
---
# <a name="type-system-entity-sql"></a>類型系統 (Entity SQL)

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支援數種類型：  
  
- 基本 (簡單) 型別，例如 `Int32` 和 `String.`。  
  
- 結構描述中定義的名義型別，例如 <xref:System.Data.Metadata.Edm.EntityType>、<xref:System.Data.Metadata.Edm.ComplexType> 和 <xref:System.Data.Metadata.Edm.RelationshipType>。  
  
- 沒有在結構描述中明確定義的匿名型別：<xref:System.Data.Metadata.Edm.CollectionType>、<xref:System.Data.Metadata.Edm.RowType> 和 <xref:System.Data.Metadata.Edm.RefType>。  
  
 本節討論未明確定義在架構中，但 Entity SQL 支援的匿名型別。 如需基本和名義類型的詳細資訊，請參閱 [ (CSDL) 的概念模型類型 ](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#conceptual-model-types-csdl)。  
  
## <a name="rows"></a>資料列  

 資料列的結構取決於此資料列所包含之具型別和具名成員的序列。 資料列型別沒有任何識別 (Identity)，而且無法從中繼承。 如果這些成員分別對等，相同資料列型別的執行個體 (Instance) 就會對等。 除了結構化對等以外，資料列沒有任何行為，而且在 Common Language Runtime 中沒有對等項目。 查詢可能會產生包含資料列或資料列集合的結構。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢與主應用程式 (Host) 語言之間的 API 繫結會定義如何在產生結果的查詢中實現資料列。 如需有關如何建立資料列實例的詳細資訊，請參閱 [建立類型](constructing-types-entity-sql.md)。  
  
## <a name="collections"></a>集合  

 集合型別代表零個或多個其他物件的執行個體。 如需有關如何建立集合的詳細資訊，請參閱 [建立類型](constructing-types-entity-sql.md)。  
  
## <a name="references"></a>參考資料  

 參考是指向特定實體集中特定實體的邏輯指標。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支援下列用來建構、解構及巡覽參考的運算子：  
  
- [裁判](ref-entity-sql.md)  
  
- [CREATEREF](createref-entity-sql.md)  
  
- [KEY](key-entity-sql.md)  
  
- [DEREF](deref-entity-sql.md)  
  
 您可以使用成員存取 (點) 運算子 (`.`) 來巡覽參考。 下列程式碼片段會透過巡覽 r (參考) 屬性，擷取 (訂單的) Id 屬性。  
  
```sql  
select o2.r.Id
from (select ref(o) as r from LOB.Orders as o) as o2
```  
  
 如果此參數值為 null，或者參考的目標不存在，結果就是 null。  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 概觀](entity-sql-overview.md)
- [Entity SQL 參考](entity-sql-reference.md)
- [CAST](cast-entity-sql.md)
- [CSDL、SSDL 和 MSL 規格](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
