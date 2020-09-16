---
title: Entity Framework 的 EntityClient 提供者
ms.date: 03/30/2017
ms.assetid: 8c5db787-78e6-4a34-8dc1-188bca0aca5e
ms.openlocfilehash: cd02f2ede37ef3518071b5d4c79cdffe2e2f1b5d
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90542590"
---
# <a name="entityclient-provider-for-the-entity-framework"></a>Entity Framework 的 EntityClient 提供者
EntityClient 提供者是 Entity Framework 應用程式用來存取概念模型中所描述之資料的資料提供者。 如需概念模型的相關資訊，請參閱 [模型和對應](modeling-and-mapping.md)。 EntityClient 會使用其他 .NET Framework 資料提供者來存取資料來源。 例如，EntityClient 會在存取 SQL Server 資料庫時使用 .NET Framework Data Provider for SQL Server (SqlClient)。 如需 SqlClient 提供者的相關資訊，請參閱 [Entity Framework 的 SqlClient](sqlclient-for-the-entity-framework.md)。 EntityClient 提供者是在 <xref:System.Data.EntityClient> 命名空間 (Namespace) 中實作的。  
  
## <a name="managing-connections"></a>管理連接  
 Entity Framework 藉由提供 <xref:System.Data.EntityClient.EntityConnection> 給基礎資料提供者和關係資料庫，建立在儲存體專屬 ADO.NET 資料提供者之上。 若要建立 <xref:System.Data.EntityClient.EntityConnection> 物件，您必須參考一組包含必要模型和對應的中繼資料，以及儲存體專屬的資料提供者名稱和連接字串。 <xref:System.Data.EntityClient.EntityConnection>準備就緒之後，即可透過概念模型所產生的類別來存取實體。  
  
 您可以在 app.config 檔案中指定連接字串。  
  
 <xref:System.Data.EntityClient> 也包含 <xref:System.Data.EntityClient.EntityConnectionStringBuilder> 類別。 這個類別可讓開發人員使用此類別的屬性和方法，以程式設計方式建立語法正確的連接字串，以及剖析和重建現有的連接字串。 如需詳細資訊，請參閱 [如何：建立 EntityConnection 連接字串](how-to-build-an-entityconnection-connection-string.md)。  
  
## <a name="creating-queries"></a>建立查詢  
 此 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 語言是與儲存體無關的 SQL 方言，可直接與概念實體架構一起運作並支援實體資料模型的概念，例如繼承和關聯性。 <xref:System.Data.EntityClient.EntityCommand>類別是用來 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 針對實體模型執行命令。 建構 <xref:System.Data.EntityClient.EntityCommand> 物件時，您可以指定預存程序名稱或查詢文字。 Entity Framework 適用于儲存體專屬的資料提供者，可將泛型轉譯為 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 儲存體專屬的查詢。 如需有關撰寫查詢的詳細資訊 [!INCLUDE[esql](../../../../../includes/esql-md.md)] ，請參閱 [Entity SQL 語言](./language-reference/entity-sql-language.md)。  
  
 下列範例會建立 <xref:System.Data.EntityClient.EntityCommand> 物件，並 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 將查詢文字指派給它的 <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> 屬性。 此 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 查詢會要求從概念模型依標價排序的產品。 下列程式碼完全不了解儲存模型的相關資訊。  
  
 ```csharp
EntityCommand cmd = conn.CreateCommand();
cmd.CommandText = @"SELECT VALUE p
  FROM AdventureWorksEntities.Product AS p
  ORDER BY p.ListPrice";
```
  
## <a name="executing-queries"></a>執行查詢  
 執行查詢時，會先剖析查詢然後將它轉換成標準命令樹。 所有後續的查詢處理都是在此命令樹上執行。 命令樹是 <xref:System.Data.EntityClient> 和基礎 .NET Framework 資料提供者（例如）之間的通訊方式 <xref:System.Data.SqlClient> 。  
  
 <xref:System.Data.EntityClient.EntityDataReader> 會公開針對概念模型執行 <xref:System.Data.EntityClient.EntityCommand> 的結果。 若要執行可傳回 <xref:System.Data.EntityClient.EntityDataReader> 的命令，請呼叫 <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>。 <xref:System.Data.EntityClient.EntityDataReader> 會實作 <xref:System.Data.IExtendedDataRecord> 來描述豐富的結構化結果。  
  
## <a name="managing-transactions"></a>管理交易  
 Entity Framework 中有兩種使用異動的方式：自動與明確。 自動交易會使用 <xref:System.Transactions> 命名空間，而明確交易會使用 <xref:System.Data.EntityClient.EntityTransaction> 類別。  
  
 若要更新透過概念模型公開的資料，請參閱 [如何：管理 Entity Framework 中的交易](/previous-versions/dotnet/netframework-4.0/bb738523(v=vs.100))。  
  
## <a name="in-this-section"></a>本節內容  
 [作法：建置 EntityCollection 連接字串](how-to-build-an-entityconnection-connection-string.md)  
  
 [作法：執行可傳回 PrimitiveType 結果的查詢](how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [作法：執行可傳回 StructuralType 結果的查詢](how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [作法：執行可傳回 RefType 結果的查詢](how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [作法：執行可傳回複雜類型的查詢](how-to-execute-a-query-that-returns-complex-types.md)  
  
 [作法：執行可傳回巢狀集合的查詢](how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [作法：使用 EntityCommand 執行參數化 Entity SQL 查詢](how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [作法：使用 EntityCommand 執行參數化預存程序](how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [作法：執行多型查詢](how-to-execute-a-polymorphic-query.md)  
  
 [作法：使用 Navigate 運算子巡覽關聯性](how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## <a name="see-also"></a>另請參閱

- [管理連接和異動](/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))
- [ADO.NET Entity Framework](index.md)
- [語言參考](./language-reference/index.md)
