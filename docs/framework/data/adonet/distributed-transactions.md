---
title: 分散式交易
ms.date: 03/30/2017
ms.assetid: 718b257c-bcb2-408e-b004-a7b0adb1c176
ms.openlocfilehash: b6553d50039ca0f4888f0610b187c6b419a462b5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91153193"
---
# <a name="distributed-transactions"></a>分散式交易

異動是一組相關工作，尤其是它會做為一個單位的成功 (認可) 或失敗 (中止)。 *分散式交易*是影響數個資源的交易。 對於要認可的分散式異動，所有參與者都必須保證資料的任何變更都是永久的。 不管系統是否當機，還是發生其他不可預見的事件，變更必須持續。 如果單一參與者無法做出此保證，則整個異動會失敗，異動範圍內的任何資料變更都將復原。  
  
> [!NOTE]
> 如果在異動作用期間啟動了 `DataReader`，而您嘗試認可或復原該異動，就會擲回例外狀況 (Exception)。  
  
## <a name="working-with-systemtransactions"></a>使用 System.Transactions  

 在 .NET Framework 中，會透過 <xref:System.Transactions> 命名空間中的 API 來管理分散式異動。 當涉及多個持續性資源管理員時，<xref:System.Transactions> API 會將分散式異動處理委派給異動監視器，如 Microsoft 分散式異動協調器 (MS DTC)。 如需詳細資訊，請參閱 [交易基礎](../transactions/transaction-fundamentals.md)概念。  
  
 ADO.NET 2.0 支援使用 `EnlistTransaction` 方法在分散式交易中登記，該方法會在 <xref:System.Transactions.Transaction> 執行個體中登記連接。 在舊版 ADO.NET 中，會使用連接的 `EnlistDistributedTransaction` 方法在分散式異動中進行明確登記，以在支援回溯相容性的 <xref:System.EnterpriseServices.ITransaction> 執行個體 (Instance) 中登記連接。 如需企業服務交易的詳細資訊，請參閱 [與 Enterprise services 和 COM + 交易的互通性](../transactions/interoperability-with-enterprise-services-and-com-transactions.md)。  
  
 當針對 SQL Server 資料庫，使用具有 SQL Server 的 .NET Framework 提供者之 <xref:System.Transactions> 異動時，會自動使用輕量型 <xref:System.Transactions.Transaction>。 然後，交易可視需要提升為完全分散式交易。 如需詳細資訊，請參閱 [System. 交易與 SQL Server 整合](system-transactions-integration-with-sql-server.md)。  
  
> [!NOTE]
> Oracle 資料庫一次可參與的分散式交易數目上限預設為 10。 與 Oracle 資料庫連接時，在第 10 次交易後會擲回例外狀況。 Oracle 不支援分散式異動內的 `DDL`。  
  
## <a name="automatically-enlisting-in-a-distributed-transaction"></a>自動登記分散式異動  

 自動登記是整合 ADO.NET 連接與 `System.Transactions` 的預設 (及慣用) 方式。 如果連接物件確定交易處於作用中 (在 `System.Transaction` 詞彙中，表示 `Transaction.Current` 不為 Null)，則會自動在現有分散式交易中登記。 當開啟連接時，即會發生自動異動登記。 之後即使在異動範圍內執行命令，該事件也不會發生。 您可藉由指定 `Enlist=false` 做為 <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> 的連接字串參數，或指定 `OLE DB Services=-7` 做為 <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A?displayProperty=nameWithType> 的連接字串參數，停用現有交易中的自動登記。 如需 Oracle 及 ODBC 連接字串參數的詳細資訊，請參閱 <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A?displayProperty=nameWithType> 及 <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A?displayProperty=nameWithType>。  
  
## <a name="manually-enlisting-in-a-distributed-transaction"></a>在分散式異動中手動登記  

 如果停用了自動登記，或需要登記在開啟連接之後啟動的交易，您可以針對所使用的提供者，使用 `EnlistTransaction` 物件的 <xref:System.Data.Common.DbConnection> 方法，在現有的分散式交易中登記。 在現有的分散式異動中登記可確保，如果認可或復原異動，則也會認可或復原資料來源的程式碼所做的修改。  
  
 當共用商務物件時，在分散式異動中登記會特別適用。 如果與開啟的連接共用商務物件，則僅當該連接開啟時，才會發生自動交易登記。 如果使用共用的商務物件來執行多個異動，則該物件的開啟連接將不會自動在新起始的異動中登記。 在此情況下，您可以停用連接的自動異動登記，並使用 `EnlistTransaction` 在異動中登記連接。  
  
 `EnlistTransaction` 採用型別的單一引數 <xref:System.Transactions.Transaction> ，這是現有交易的參考。 呼叫連接的 `EnlistTransaction` 方法之後，對使用連接之資料來源所做的所有修改都會包含在異動中。 傳遞 Null 值可將連接從目前的分散式異動登記中取消登記。 請注意，在呼叫 `EnlistTransaction` 之前，必須先開啟連接。  
  
> [!NOTE]
> 在交易上明確地登記連接之後，直到第一個交易完成之前，無法取消登記或在其他交易中登記它。  
  
> [!CAUTION]
> 如果連接已使用連接的 `EnlistTransaction` 方法啟動異動，則 <xref:System.Data.Common.DbConnection.BeginTransaction%2A> 會擲回例外狀況。 不過，如果異動是在資料來源上啟動的本機異動 (例如，使用 <xref:System.Data.SqlClient.SqlCommand>，明確執行 BEGIN TRANSACTION 陳述式)，則 `EnlistTransaction` 將復原本機異動，並按要求在現有的分散式異動中登記。 您不會收到復原本機異動的通知，而且必須管理所有非使用 <xref:System.Data.Common.DbConnection.BeginTransaction%2A> 啟動的本機異動。 如果您是將 .NET Framework Data Provider for SQL Server (`SqlClient`) 用於 SQL Server，則嘗試登記會擲回例外狀況。 將不會偵測到所有其他情況。  
  
## <a name="promotable-transactions-in-sql-server"></a>SQL Server 中的可提升異動  

 SQL Server 支援可提升異動，在該異動中，本機輕量型異動可在必要時自動提升為分散式異動。 除非需要已加入的負荷，否則可提升交易不會叫用分散式交易的已加入負荷。 如需詳細資訊和程式碼範例，請參閱 [System. 交易與 SQL Server 整合](system-transactions-integration-with-sql-server.md)。  
  
## <a name="configuring-distributed-transactions"></a>設定分散式異動  

 您可能需要透過網路啟用 MS DTC，才能使用分散式異動。 如果已啟用 Windows 防火牆，則必須允許 MS DTC 服務使用網路或開啟 MS DTC 連接埠。  
  
## <a name="see-also"></a>另請參閱

- [異動和並行存取](transactions-and-concurrency.md)
- [System.Transactions 與 SQL Server 整合](system-transactions-integration-with-sql-server.md)
- [ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)
