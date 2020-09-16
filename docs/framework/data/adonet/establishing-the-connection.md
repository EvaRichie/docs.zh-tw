---
title: 建立連接
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3af512f3-87d9-4005-9e2f-abb1060ff43f
ms.openlocfilehash: 0da74b4896ad5434e46df336183db89054198134
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90540962"
---
# <a name="establishing-the-connection"></a>建立連接
若要連接至 Microsoft SQL Server，請使用 .NET Framework Data Provider for SQL Server 的 <xref:System.Data.SqlClient.SqlConnection> 物件。 若要連接至 OLE DB 資料來源，請使用 .NET Framework Data Provider for OLE DB 的 <xref:System.Data.OleDb.OleDbConnection> 物件。 若要連接至 ODBC 資料來源，請使用 ODBC 的 .NET Framework 資料提供者的 <xref:System.Data.Odbc.OdbcConnection> 物件。 若要連接至 Oracle 資料來源，請使用 Oracle 的 .NET Framework 資料提供者的 <xref:System.Data.OracleClient.OracleConnection> 物件。 若要安全地儲存及抓取連接字串，請參閱 [保護連接資訊](protecting-connection-information.md)。  
  
## <a name="closing-connections"></a>關閉連接  
 建議您在使用完連接後一律關閉該連接，以便將連接傳回集區。 即使有未處理的例外狀況，Visual Basic 或 C# 中的 `Using` 區塊也會在程式碼結束該區塊時自動處理連接。 如需詳細資訊，請參閱 [Using 語句](../../../csharp/language-reference/keywords/using-statement.md) 和 [using 語句](../../../visual-basic/language-reference/statements/using-statement.md) 。  
  
 您也可針對使用的提供者，使用連接物件的 `Close` 或 `Dispose` 方法。 可能不會將未明確關閉的連接加入或傳回集區。 例如，已離開範圍但尚未明確關閉的連接僅會在已達到最大集區大小，且連接仍然有效時，才會回到連接集區。 如需詳細資訊，請參閱 [OLE DB、ODBC 和 Oracle 連接](ole-db-odbc-and-oracle-connection-pooling.md)共用。  
  
> [!NOTE]
> 請勿 `Close` `Dispose` 在您類別之方法中的 **連接**、 **DataReader**或任何其他 managed 物件上呼叫或 `Finalize` 。 在完成項中，只需釋放類別直接擁有的 Unmanaged 資源。 如果類別未擁有任何 Unmanaged 資源，請不要在類別定義中包含 `Finalize` 方法。 如需詳細資訊，請參閱 [垃圾收集](../../../standard/garbage-collection/index.md)。  
  
> [!NOTE]
> 從連接集區中擷取連接或將連接傳回連接集區時，系統不會在伺服器上引發登入和登出事件，因為當連接傳回連接集區時，連接實際上並未關閉。 如需詳細資訊，請參閱 [SQL Server 連線共用 (ADO.NET)](sql-server-connection-pooling.md) \(機器翻譯\)。  
  
## <a name="connecting-to-sql-server"></a>連線到 SQL Server  
 SQL Server 的 .NET Framework 資料提供者支援與 OLE DB (ADO) 連接字串格式類似的連接字串格式。 如需有效的字串格式名稱及值，請參閱 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> 物件的 <xref:System.Data.SqlClient.SqlConnection> 屬性。 您也可以使用 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 類別在執行階段建立語法有效的連接字串。 如需詳細資訊，請參閱[連接字串建置器](connection-string-builders.md)。  
  
 下列程式碼範例示範如何建立及開啟與 SQL Server 資料庫的連接。  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New SqlConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (SqlConnection connection = new SqlConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
### <a name="integrated-security-and-aspnet"></a>整合安全性與 ASP.NET  
 SQL Server 整合安全性 (也稱為信任連接) 可在連接至 SQL Server 時，協助提供保護，因為它不會在連接字串中公開使用者 ID 及密碼，因此建議在驗證連接時使用。 整合安全性會使用執行中處理序的目前安全性識別或語彙基元。 對於桌面應用程式，這通常是目前已登入使用者的識別。  
  
 ASP.NET 應用程式的安全性識別可設為數個不同的選項之一。 若要深入瞭解 ASP.NET 應用程式連接到 SQL Server 時所使用的安全性識別，請參閱 [ASP.NET](/previous-versions/aspnet/xh507fc5(v=vs.100))模擬、 [ASP.NET 驗證](/previous-versions/aspnet/eeyk640h(v=vs.100))和 How [to：使用 Windows 整合式安全性存取 SQL Server](/previous-versions/aspnet/bsz5788z(v=vs.100))。  
  
## <a name="connecting-to-an-ole-db-data-source"></a>連接至 OLE DB 資料來源  
 OLE DB 的 .NET Framework Data Provider 會使用 **OleDbConnection** 物件，為 (OLE DB 的 SQL Server 提供者提供使用 OLE DB) （）所公開的資料來源連接。  
  
 對於 OLE DB 的 .NET Framework 資料提供者，連接字串格式與 ADO 中使用的連接字串格式相同，但下列情況例外：  
  
- 必須 **提供 Provider** 關鍵字。  
  
- 不支援 **URL**、 **遠端提供者**和 **遠端伺服器** 關鍵字。  
  
 如需 OLE DB 連接字串的詳細資訊，請參閱 <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A> 主題。 您也可以使用 <xref:System.Data.OleDb.OleDbConnectionStringBuilder> 在執行階段建立連接字串。  
  
> [!NOTE]
> **OleDbConnection**物件不支援設定或抓取 OLE DB 提供者特定的動態屬性。 僅支援 OLE DB 提供者之連接字串中可傳遞的屬性。  
  
 下列程式碼範例說明如何建立及開啟與 OLE DB 資料來源的連接。  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OleDbConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OleDbConnection connection =
  new OleDbConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## <a name="do-not-use-universal-data-link-files"></a>不使用通用資料連結檔  
 您可以在通用資料連結 (UDL) 檔中提供 **OleDbConnection** 的連接資訊;不過，您應該避免這樣做。 UDL 檔並未加密，並且會以純文字的格式公開連接字串資訊。 因為對您的應用程式而言，UDL 檔是外部的檔案型資源，所以您無法使用 .NET Framework 來保護該檔案。  
  
## <a name="connecting-to-an-odbc-data-source"></a>連接至 ODBC 資料來源  
 ODBC 的 .NET Framework Data Provider 會使用 **OdbcConnection** 物件，提供與使用 ODBC 公開之資料來源的連接。  
  
 對於 ODBC 的 .NET Framework 資料提供者，會將連接字串格式設計為儘可能與 ODBC 連接字串格式相符。 您也可以提供 ODBC 資料來源名稱 (DSN)。 如需 **OdbcConnection** 的詳細資訊，請參閱 <xref:System.Data.Odbc.OdbcConnection> 。  
  
 下列程式碼範例說明如何建立及開啟與 ODBC 資料來源的連接。  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OdbcConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OdbcConnection connection =
  new OdbcConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## <a name="connecting-to-an-oracle-data-source"></a>連接至 Oracle 資料來源  
 Oracle 的 .NET Framework Data Provider 會使用 **OracleConnection** 物件提供與 oracle 資料來源的連接。  
  
 對於 Oracle 的 .NET Framework 資料提供者，會將連接字串格式設計為儘可能與 Oracle OLE DB 提供者 (MSDAORA) 連接字串格式相符。 如需 **OracleConnection**的詳細資訊，請參閱 <xref:System.Data.OracleClient.OracleConnection> 。  
  
 下列程式碼範例說明如何建立及開啟與 Oracle 資料來源的連接。  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OracleConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OracleConnection connection =
  new OracleConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
OracleConnection nwindConn = new OracleConnection("Data Source=MyOracleServer;Integrated Security=yes;");  
nwindConn.Open();  
```  
  
## <a name="see-also"></a>另請參閱

- [連接到資料來源](connecting-to-a-data-source.md)
- [連接字串](connection-strings.md)
- [OLE DB、ODBC 和 Oracle 連接共用](ole-db-odbc-and-oracle-connection-pooling.md)
- [ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)
