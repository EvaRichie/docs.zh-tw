---
title: 在 SQL Server 中撰寫安全的動態 SQL
ms.date: 03/30/2017
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.openlocfilehash: c598427a17ceb289f75fab481a55016f0efe5624
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91147446"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>在 SQL Server 中撰寫安全的動態 SQL

SQL 插入式攻擊是指惡意使用者輸入 Transact-SQL 陳述式，而非提供有效輸入的程序。 如果在未驗證的情況下將輸入直接傳遞至伺服器，而且應用程式不慎執行了以資料隱碼方式撰寫的程式碼，攻擊就可能會破壞或損毀資料。  
  
 建構 SQL 陳述式的任何程序都應該經過檢閱，以確認有無插入弱點，因為 SQL Server 會執行收到的所有語法有效查詢。 即使是參數化資料也可能被技術純熟又執意操作的攻擊者操縱。 如果您使用動態 SQL，請務必將命令參數化，且一律不要將參數值直接包含在查詢字串中。  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>SQL 插入式攻擊的分析  

 資料隱碼處理的運作方式是不當地終止文字字串並附加新命令。 因為插入的命令在執行之前可能附加有其他字串，所以不懷好意的人會使用註解標記 "--" 終止插入的字串。 在執行時，後續文字便會被忽略。 可以使用分號 (;) 分隔符號插入多個命令。  
  
 只要插入的 SQL 程式碼語法正確，就無法以程式設計方式偵測竄改。 因此，您必須驗證所有使用者輸入，並且仔細檢視在您使用的伺服器中執行建構之 SQL 命令的程式碼。 絕不串連未經驗證的使用者輸入。 字串串連是指令碼資料隱碼的主要進入點。  
  
 以下提供一些實用的指導方針：  
  
- 一律不要直接從使用者輸入建立 Transact-SQL 陳述式，並使用預存程序驗證使用者輸入。  
  
- 透過測試類型、長度、格式和範圍，驗證使用者輸入。 使用 Transact-SQL QUOTENAME () 函式來逸出系統名稱或 REPLACE () 函式，以逸出字串中的任何字元。  
  
- 在應用程式的每一層實作多層驗證。  
  
- 測試輸入的大小和資料類型，並強制執行適當的限制。 這有助於防止蓄意的緩衝區滿溢。  
  
- 測試字串變數的內容，僅接受預期的值。 拒絕包含二進位資料、逸出序列和註解字元的項目。  
  
- 使用 XML 文件時，在輸入資料時即驗證所有資料的結構描述。  
  
- 在多層環境中，所有資料應在進入受信任區域之前進行驗證。  
  
- 在可用以建構檔案名稱的欄位中，不接受下列字串：AUX、CLOCK$、COM1 到 COM8、CON、CONFIG$、LPT1 到 LPT8、NUL 和 PRN。  
  
- 搭配預存程序和命令使用 <xref:System.Data.SqlClient.SqlParameter> 物件，以提供類型檢查及長度驗證功能。  
  
- 在用戶端程式碼中使用 <xref:System.Text.RegularExpressions.Regex> 運算式來篩選無效字元。  
  
## <a name="dynamic-sql-strategies"></a>動態 SQL 策略  

 在您的程序式程式碼中執行動態建立的 SQL 陳述式會中斷擁有權鏈結，使 SQL Server 針對動態 SQL 所存取的物件檢查呼叫者的權限。  
  
 SQL Server 具有一些方法，可使用執行動態 SQL 的預存程序和使用者定義函式來授與資料存取權給使用者。  
  
- 使用模擬搭配 Transact-SQL EXECUTE AS 子句，如[在 SQL Server 中使用模擬來自訂權限](customizing-permissions-with-impersonation-in-sql-server.md)中所述。  
  
- 使用憑證簽署預存程序，如[在 SQL Server 中簽署預存程序](signing-stored-procedures-in-sql-server.md)中所述。  
  
### <a name="execute-as"></a>EXECUTE AS  

 EXECUTE AS 子句會將呼叫者的權限取代為 EXECUTE AS 子句中所指定使用者的權限。 巢狀預存程序或觸發程序會以 Proxy 使用者的資訊安全內容執行。 這可能會中斷依賴資料列層級安全性或需要稽核的應用程式。 某些會傳回使用者身分識別的函式會傳回 EXECUTE AS 子句中指定的使用者，而非原始呼叫者。 只有在執行程序之後或發出 REVERT 陳述式時，執行內容才會還原為原始呼叫者。  
  
### <a name="certificate-signing"></a>憑證簽署  

 當使用憑證簽署的預存程序執行時，授與憑證使用者的權限會與呼叫者的權限合併。 執行內容會維持不變；憑證使用者並不會模擬呼叫者。 簽署預存程序需要實作數個步驟。 每次修改程序之後，都必須重新簽署。  
  
### <a name="cross-database-access"></a>跨資料庫存取  

 執行以動態方式建立的 SQL 陳述式時，跨資料庫擁有權鏈結無法運作。 您可以在 SQL Server 中建立存取其他資料庫資料的預存程序，並使用存在於兩個資料庫中的憑證來簽署程序，藉此解決上述問題。 這可讓使用者存取由程序所使用的資料庫資源，不需要授與他們資料庫存取權或權限。  
  
## <a name="external-resources"></a>外部資源  

 如需詳細資訊，請參閱下列資源。  
  
|資源|描述|  
|--------------|-----------------|  
|《SQL Server 線上叢書》中的[預存程序](/sql/relational-databases/stored-procedures/stored-procedures-database-engine)和 [SQL 資料隱碼](/sql/relational-databases/security/sql-injection)|各主題會描述如何建立預存程序，以及 SQL 插入式攻擊的運作方式。|  
  
## <a name="see-also"></a>另請參閱

- [設定 ADO.NET 應用程式的安全性](../securing-ado-net-applications.md)
- [SQL Server 安全性概觀](overview-of-sql-server-security.md)
- [SQL Server 中的應用程式安全性案例](application-security-scenarios-in-sql-server.md)
- [使用預存程序管理 SQL Server 中的權限](managing-permissions-with-stored-procedures-in-sql-server.md)
- [在 SQL Server 中簽署預存程序](signing-stored-procedures-in-sql-server.md)
- [在 SQL Server 中使用模擬來自訂權限](customizing-permissions-with-impersonation-in-sql-server.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)
