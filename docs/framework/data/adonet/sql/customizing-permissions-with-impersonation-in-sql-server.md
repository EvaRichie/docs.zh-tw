---
title: 在 SQL Server 中使用模擬來自訂權限
ms.date: 03/30/2017
ms.assetid: dc733d09-1d6d-4af0-9c4b-8d24504860f1
ms.openlocfilehash: 84c5585912ba259fdcefaae186138c4466b16206
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91180851"
---
# <a name="customizing-permissions-with-impersonation-in-sql-server"></a>在 SQL Server 中使用模擬來自訂權限

許多應用程式會使用預存程序 (Stored Procedure) 來存取資料，並仰賴擁有權鏈結來限制基底資料表的存取。 您可以授與預存程序的 EXECUTE 權限，並撤銷或拒絕基底資料表的權限。 如果預存程序和資料表具有相同的擁有者，SQL Server 就不會檢查呼叫端的權限。 不過，如果物件具有不同的擁有者或在動態 SQL 的情況中，擁有權鏈結便沒有作用。  
  
 當呼叫端沒有所參考資料庫物件的權限時，您就可以在預存程序中使用 EXECUTE AS 子句。 EXECUTE AS 子句的作用是將執行內容切換至 Proxy 使用者。 所有程式碼以及巢狀預存程序或觸發程序 (Trigger) 的任何呼叫都會在 Proxy 使用者的安全性內容底下執行。 只有在執行程序之後或發出 REVERT 陳述式時，執行內容才會還原為原始呼叫者。  
  
## <a name="context-switching-with-the-execute-as-statement"></a>使用 EXECUTE AS 陳述式來切換內容  

 Transact-SQL EXECUTE AS 陳述式可讓您透過模擬另一個登入或資料庫使用者，切換陳述式的執行內容。 以另一個使用者的身分測試查詢和程序時，這是很有用的技巧。  
  
```sql  
EXECUTE AS LOGIN = 'loginName';  
EXECUTE AS USER = 'userName';  
```  
  
 您必須擁有要模擬之登入或使用的 IMPERSONATE 權限。 對於所有資料庫的 `sysadmin` 以及擁有資料庫的 `db_owner` 角色成員而言，這個權限是隱含的。  
  
## <a name="granting-permissions-with-the-execute-as-clause"></a>使用 EXECUTE AS 子句來授與權限  

 您可以在預存程序、觸發程序或使用者定義函式 (內嵌 (Inline) 資料表值函式除外) 的定義標頭中使用 EXECUTE AS 子句。 這樣做會導致此程序在 EXECUTE AS 子句中指定之使用者名稱或關鍵字的內容中執行。 您可以在資料庫中建立沒有對應至登入的 Proxy 使用者，並僅授與此程序所存取之物件的必要權限給該位使用者。 只有 EXECUTE AS 子句中指定的 Proxy 使用者必須擁有此模組所存取之所有物件的權限。  
  
> [!NOTE]
> 某些動作 (例如 TRUNCATE TABLE) 沒有可授與的權限。 您可以在程序中併入陳述式並指定擁有 ALTER TABLE 權限的 Proxy 使用者，藉以針對僅擁有程序之 EXECUTE 權限的呼叫端擴充截斷資料表的權限。  
  
 EXECUTE AS 子句中指定的內容在此程序的持續期間內有效，包括巢狀程序和觸發程序。 當執行完成或發出 REVERT 陳述式時，內容就會還原成呼叫端。  
  
 在程序中使用 EXECUTE AS 子句包含三個步驟。  
  
1. 在資料庫中建立沒有對應至登入的 Proxy 使用者。 雖然這並非必要條件，但是在管理權限時很有用。  
  
```sql
CREATE USER proxyUser WITHOUT LOGIN  
```  
  
1. 將必要權限授與 Proxy 使用者。  
  
2. 將 EXECUTE AS 子句加入至預存程序或使用者定義函式。  
  
```sql
CREATE PROCEDURE [procName] WITH EXECUTE AS 'proxyUser' AS ...  
```  
  
> [!NOTE]
> 需要稽核的應用程式可能會中斷，因為系統沒有保留呼叫端的原始安全性內容。 傳回目前使用者之識別 (例如 SESSION_USER、USER 或 USER_NAME) 的內建函式會傳回與 EXECUTE AS 子句相關聯的使用者，而非原始呼叫端。  
  
### <a name="using-execute-as-with-revert"></a>使用 EXECUTE AS 搭配 REVERT  

 您可以使用 Transact-SQL REVERT 陳述式來還原成原始執行內容。  
  
 選擇性子句（沒有還原 COOKIE = @variableName ）可讓您在 @variableName 變數包含正確的值時，將執行內容切換回呼叫端。 這樣可讓您在使用連接共用 (Connection Pooling) 的環境中，將執行內容切換回呼叫端。 由於的值 @variableName 只有 EXECUTE AS 語句的呼叫者知道，呼叫者可以保證叫用應用程式的終端使用者無法變更執行內容。 關閉連接時，它就會傳回集區。 如需 ADO.NET 中連接共用的詳細資訊，請參閱 [ (ADO.NET) SQL Server 連接 ](../sql-server-connection-pooling.md)共用。  
  
### <a name="specifying-the-execution-context"></a>指定執行內容  

 除了指定使用者以外，您也可以使用 EXECUTE AS 搭配下列任何關鍵字。  
  
- CALLER： 以 CALLER 的身分執行是預設值。如果沒有指定任何其他選項，此程序就會在呼叫端的安全性內容中執行。  
  
- OWNER： 以 OWNER 的身分執行會在程序擁有者的內容中執行此程序。 如果此程序建立於 `dbo` 或資料庫擁有者所擁有的結構描述中，此程序將以不受限制的權限執行。  
  
- SELF： 以 SELF 的身分執行會在預存程序之建立者的安全性內容中執行。 這相當於以指定之使用者的身分執行，而該指定的使用者是建立或更改程序的人員。  
  
## <a name="see-also"></a>另請參閱

- [設定 ADO.NET 應用程式的安全性](../securing-ado-net-applications.md)
- [SQL Server 安全性概觀](overview-of-sql-server-security.md)
- [SQL Server 中的應用程式安全性案例](application-security-scenarios-in-sql-server.md)
- [使用預存程序管理 SQL Server 中的權限](managing-permissions-with-stored-procedures-in-sql-server.md)
- [在 SQL Server 撰寫安全動態 SQL](writing-secure-dynamic-sql-in-sql-server.md)
- [在 SQL Server 中簽署預存程序](signing-stored-procedures-in-sql-server.md)
- [使用預存程序修改資料](../modifying-data-with-stored-procedures.md)
- [ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)
