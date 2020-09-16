---
title: Entity SQL 語言
ms.date: 03/30/2017
ms.assetid: 9e7d8837-28c5-429d-a824-7bafb59724cf
ms.openlocfilehash: 2600b7626ebc5196c702f2d1e3159fd9549227f7
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90553378"
---
# <a name="entity-sql-language"></a>Entity SQL 語言
Entity SQL 是與儲存體無關的查詢語言，與 SQL 類似。 Entity SQL 可讓您查詢實體資料 (無論以物件形式或在表格式資料表中)。 在下列情況下，您可以考慮使用 Entity SQL：  
  
- 必須在執行階段動態建構查詢時。 在此情況下，您也可以考慮使用 <xref:System.Data.Objects.ObjectQuery%601> 的查詢產生器方法，而不在執行階段建構 Entity SQL 查詢字串。  
  
- 當您想要將查詢定義為模型定義的一部分時。 資料模型僅支援 Entity SQL。 如需詳細資訊，請參閱 [QueryView 元素 (MSL) ](/ef/ef6/modeling/designer/advanced/edmx/msl-spec#queryview-element-msl)  
  
- 使用 EntityClient 傳回唯讀實體資料，做為使用 <xref:System.Data.EntityClient.EntityDataReader> 的資料列集時。 如需詳細資訊，請參閱 [適用於 Entity Framework 的 EntityClient 提供者](../entityclient-provider-for-the-entity-framework.md)。  
  
- 如果您非常熟悉 SQL 查詢語言，對您來說，Entity SQL 可能最易於使用。  
  
## <a name="using-entity-sql-with-the-entityclient-provider"></a>搭配 EntityClient 提供者使用 Entity SQL  
 如果您想要搭配 EntityClient 提供者使用 Entity SQL，請參閱下列主題取得詳細資訊：  
  
 [Entity Framework 的 EntityClient 提供者](../entityclient-provider-for-the-entity-framework.md)  
  
 [作法：建置 EntityCollection 連接字串](../how-to-build-an-entityconnection-connection-string.md)  
  
 [作法：執行可傳回 PrimitiveType 結果的查詢](../how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [作法：執行可傳回 StructuralType 結果的查詢](../how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [作法：執行可傳回 RefType 結果的查詢](../how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [作法：執行可傳回複雜類型的查詢](../how-to-execute-a-query-that-returns-complex-types.md)  
  
 [作法：執行可傳回巢狀集合的查詢](../how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [作法：使用 EntityCommand 執行參數化 Entity SQL 查詢](../how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [作法：使用 EntityCommand 執行參數化預存程序](../how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [作法：執行多型查詢](../how-to-execute-a-polymorphic-query.md)  
  
 [作法：使用 Navigate 運算子巡覽關聯性](../how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## <a name="using-entity-sql-with-object-queries"></a>搭配物件查詢使用 Entity SQL  
 如果您想要搭配物件查詢使用 Entity SQL，請參閱下列主題取得詳細資訊：  
  
 [如何：執行可傳回實體類型集合的查詢](/previous-versions/dotnet/netframework-4.0/bb738694(v=vs.100))  
  
 [如何：執行參數化查詢](/previous-versions/dotnet/netframework-4.0/bb738521(v=vs.100))  
  
 [如何：使用導覽屬性來導覽關聯性](/previous-versions/dotnet/netframework-4.0/bb896321(v=vs.100))  
  
 [如何：呼叫使用者定義函式](/previous-versions/dotnet/netframework-4.0/dd490951(v=vs.100))  
  
 [如何：篩選資料](/previous-versions/dotnet/netframework-4.0/cc716755(v=vs.100))  
  
 [如何：排序資料](/previous-versions/dotnet/netframework-4.0/cc716784(v=vs.100))  
  
 [如何：群組資料](/previous-versions/dotnet/netframework-4.0/bb896341(v=vs.100))  
  
 [如何：彙總資料](/previous-versions/dotnet/netframework-4.0/cc716738(v=vs.100))  
  
 [如何：執行可傳回匿名類型集合的查詢](/previous-versions/dotnet/netframework-4.0/bb738512(v=vs.100))  
  
 [如何：執行可傳回基本類型集合的查詢](/previous-versions/dotnet/netframework-4.0/bb738451(v=vs.100))  
  
 [如何：在 EntityCollection 中查詢相關物件](/previous-versions/dotnet/netframework-4.0/cc716708(v=vs.100))  
  
 [如何：排序兩個查詢的聯集](/previous-versions/dotnet/netframework-4.0/bb896299(v=vs.100))  
  
 [如何：逐頁檢視查詢結果](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))  
  
## <a name="in-this-section"></a>本節內容  
 [Entity SQL 概觀](entity-sql-overview.md)  
  
 [Entity SQL 參考](entity-sql-reference.md)  
  
## <a name="see-also"></a>另請參閱

- [ADO.NET Entity Framework](../index.md)
- [語言參考](index.md)
