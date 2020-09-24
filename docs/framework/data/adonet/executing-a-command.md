---
title: 執行命令
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
ms.openlocfilehash: d7d290c1c149f9eab2449c25e8d32f2568eb0277
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156455"
---
# <a name="executing-a-command"></a>執行命令

內含在 .NET Framework 中的每個 .NET Framework 資料提供者本身都有命令物件，此物件是繼承自 <xref:System.Data.Common.DbCommand>。 .NET Framework Data Provider for OLE DB 包含 <xref:System.Data.OleDb.OleDbCommand> 物件、.NET Framework Data Provider for SQL Server 包含 <xref:System.Data.SqlClient.SqlCommand> 物件、.NET Framework Data Provider for ODBC 包含 <xref:System.Data.Odbc.OdbcCommand> 物件，而 .NET Framework Data Provider for Oracle 包含 <xref:System.Data.OracleClient.OracleCommand> 物件。 上述每種物件都會根據命令類型和想要的傳回值而公開 (Expose) 執行命令的方法，如下表所述。  
  
|Command|傳回值|  
|-------------|------------------|  
|`ExecuteReader`|傳回 `DataReader` 物件。|  
|`ExecuteScalar`|傳回單一純量值。|  
|`ExecuteNonQuery`|執行不會傳回任何資料列的命令。|  
|`ExecuteXMLReader`|傳回 <xref:System.Xml.XmlReader>。 僅適用於 `SqlCommand` 物件。|  
  
 每個強型別 (Strongly Typed) 的命令物件也會支援 <xref:System.Data.CommandType> 列舉型別 (Enumeration)，此型別可指定解譯命令字串的方式。  
  
|CommandType|描述|  
|-----------------|-----------------|  
|`Text`|SQL 命令，可定義在資料來源執行的陳述式。|  
|`StoredProcedure`|預存程序的名稱。 您可以使用命令的 `Parameters` 屬性來存取輸入和輸出參數及傳回值，不論呼叫的是哪一個 `Execute` 方法。 在使用 `ExecuteReader` 時，無法在 `DataReader` 關閉之前存取傳回值和輸出參數。|  
|`TableDirect`|資料表的名稱。|  
  
## <a name="example"></a>範例  

 下列程式碼範例示範如何建立 <xref:System.Data.SqlClient.SqlCommand> 物件，以藉由設定其屬性來執行預存程序。 用來指定預存程序輸出參數的 <xref:System.Data.SqlClient.SqlParameter> 物件。 此命令是藉由使用 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 方法來執行，而 <xref:System.Data.SqlClient.SqlDataReader> 的輸出則會顯示在主控台視窗中。  
  
 [!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]  
  
### <a name="troubleshooting-commands"></a>疑難排解命令  

 .NET Framework Data Provider for SQL Server 加入一個效能計數器，可讓您偵測與失敗命令執行相關的週期性問題。 如需詳細資訊，請參閱 [效能計數器](performance-counters.md)。  
  
## <a name="see-also"></a>另請參閱

- [命令和參數](commands-and-parameters.md)
- [DataAdapter 和 DataReader](dataadapters-and-datareaders.md)
- [ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)
