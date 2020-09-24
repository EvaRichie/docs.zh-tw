---
title: Entity SQL 概觀
ms.date: 03/30/2017
ms.assetid: f0bb8120-e709-40a3-ac1e-5520dc47477d
ms.openlocfilehash: e9a5117984380938e48e0cd1113107c74389480f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91148123"
---
# <a name="entity-sql-overview"></a>Entity SQL 概觀

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 是一種類似 SQL 的語言，可讓您查詢 Entity Framework 中的概念模型。 概念模型將資料表示為實體和關聯性，並可 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 讓您以熟悉 SQL 的格式來查詢這些實體和關聯性。  

 Entity Framework 適用于儲存體專屬的資料提供者，可將泛型轉譯為 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 儲存體專屬的查詢。 EntityClient 提供者會提供一個方式來針對實體模型執行 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 命令，並傳回豐富的資料型別，包括純量結果、結果集和物件圖形。 當您建構 <xref:System.Data.EntityClient.EntityCommand> 物件時，您可以指定預存程序名稱或查詢的文字，其方式是將 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢字串指派給它的 <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> 屬性。 <xref:System.Data.EntityClient.EntityDataReader> 會公開針對 EDM 執行 <xref:System.Data.EntityClient.EntityCommand> 的結果。 若要執行可傳回 <xref:System.Data.EntityClient.EntityDataReader> 的命令，請呼叫 <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>。  
  
 除了 EntityClient 提供者之外，Entity Framework 還可讓您用 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 來針對概念模型執行查詢，並將資料以強型別 CLR 物件（實體類型的實例）傳回。 如需詳細資訊，請參閱 [使用物件](../working-with-objects.md)。  
  
 本章節提供有關 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 的概念資訊。  
  
## <a name="in-this-section"></a>本節內容  

 [Entity SQL 與 Transact-SQL 的相異之處](how-entity-sql-differs-from-transact-sql.md)  
  
 [Entity SQL 快速參考](entity-sql-quick-reference.md)  
  
 [型別系統](type-system-entity-sql.md)  
  
 [類型定義](type-definitions-entity-sql.md)  
  
 [建構類型](constructing-types-entity-sql.md)  
  
 [查詢計劃快取](query-plan-caching-entity-sql.md)  
  
 [命名空間](namespaces-entity-sql.md)  
  
 [識別碼](identifiers-entity-sql.md)  
  
 [參數](parameters-entity-sql.md)  
  
 [變數](variables-entity-sql.md)  
  
 [不支援的運算式](unsupported-expressions-entity-sql.md)  
  
 [文字](literals-entity-sql.md)  
  
 [Null 常值和型別推斷](null-literals-and-type-inference-entity-sql.md)  
  
 [輸入字元集](input-character-set-entity-sql.md)  
  
 [查詢運算式](query-expressions-entity-sql.md)  
  
 [函式](functions-entity-sql.md)  
  
 [運算子優先順序](operator-precedence-entity-sql.md)  
  
 [Paging](paging-entity-sql.md)  
  
 [比較語意](comparison-semantics-entity-sql.md)  
  
 [撰寫巢狀 Entity SQL 查詢](composing-nested-entity-sql-queries.md)  
  
 [可為 Null 的結構類型](nullable-structured-types-entity-sql.md)  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 參考](entity-sql-reference.md)
- [Entity SQL 語言](entity-sql-language.md)
- [CSDL、SSDL 和 MSL 規格](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)
