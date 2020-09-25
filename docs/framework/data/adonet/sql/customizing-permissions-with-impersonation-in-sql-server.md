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
# <a name="customizing-permissions-with-impersonation-in-sql-server"></a><span data-ttu-id="98308-102">在 SQL Server 中使用模擬來自訂權限</span><span class="sxs-lookup"><span data-stu-id="98308-102">Customizing Permissions with Impersonation in SQL Server</span></span>

<span data-ttu-id="98308-103">許多應用程式會使用預存程序 (Stored Procedure) 來存取資料，並仰賴擁有權鏈結來限制基底資料表的存取。</span><span class="sxs-lookup"><span data-stu-id="98308-103">Many applications use stored procedures to access data, relying on ownership chaining to restrict access to base tables.</span></span> <span data-ttu-id="98308-104">您可以授與預存程序的 EXECUTE 權限，並撤銷或拒絕基底資料表的權限。</span><span class="sxs-lookup"><span data-stu-id="98308-104">You can grant EXECUTE permissions on stored procedures, revoking or denying permissions on the base tables.</span></span> <span data-ttu-id="98308-105">如果預存程序和資料表具有相同的擁有者，SQL Server 就不會檢查呼叫端的權限。</span><span class="sxs-lookup"><span data-stu-id="98308-105">SQL Server does not check the permissions of the caller if the stored procedure and tables have the same owner.</span></span> <span data-ttu-id="98308-106">不過，如果物件具有不同的擁有者或在動態 SQL 的情況中，擁有權鏈結便沒有作用。</span><span class="sxs-lookup"><span data-stu-id="98308-106">However, ownership chaining doesn't work if objects have different owners or in the case of dynamic SQL.</span></span>  
  
 <span data-ttu-id="98308-107">當呼叫端沒有所參考資料庫物件的權限時，您就可以在預存程序中使用 EXECUTE AS 子句。</span><span class="sxs-lookup"><span data-stu-id="98308-107">You can use the EXECUTE AS clause in a stored procedure when the caller doesn't have permissions on the referenced database objects.</span></span> <span data-ttu-id="98308-108">EXECUTE AS 子句的作用是將執行內容切換至 Proxy 使用者。</span><span class="sxs-lookup"><span data-stu-id="98308-108">The effect of the EXECUTE AS clause is that the execution context is switched to the proxy user.</span></span> <span data-ttu-id="98308-109">所有程式碼以及巢狀預存程序或觸發程序 (Trigger) 的任何呼叫都會在 Proxy 使用者的安全性內容底下執行。</span><span class="sxs-lookup"><span data-stu-id="98308-109">All code, as well as any calls to nested stored procedures or triggers, executes under the security context of the proxy user.</span></span> <span data-ttu-id="98308-110">只有在執行程序之後或發出 REVERT 陳述式時，執行內容才會還原為原始呼叫者。</span><span class="sxs-lookup"><span data-stu-id="98308-110">Execution context is reverted to the original caller only after execution of the procedure or when a REVERT statement is issued.</span></span>  
  
## <a name="context-switching-with-the-execute-as-statement"></a><span data-ttu-id="98308-111">使用 EXECUTE AS 陳述式來切換內容</span><span class="sxs-lookup"><span data-stu-id="98308-111">Context Switching with the EXECUTE AS Statement</span></span>  

 <span data-ttu-id="98308-112">Transact-SQL EXECUTE AS 陳述式可讓您透過模擬另一個登入或資料庫使用者，切換陳述式的執行內容。</span><span class="sxs-lookup"><span data-stu-id="98308-112">The Transact-SQL EXECUTE AS statement allows you to switch the execution context of a statement by impersonating another login or database user.</span></span> <span data-ttu-id="98308-113">以另一個使用者的身分測試查詢和程序時，這是很有用的技巧。</span><span class="sxs-lookup"><span data-stu-id="98308-113">This is a useful technique for testing queries and procedures as another user.</span></span>  
  
```sql  
EXECUTE AS LOGIN = 'loginName';  
EXECUTE AS USER = 'userName';  
```  
  
 <span data-ttu-id="98308-114">您必須擁有要模擬之登入或使用的 IMPERSONATE 權限。</span><span class="sxs-lookup"><span data-stu-id="98308-114">You must have IMPERSONATE permissions on the login or user you are impersonating.</span></span> <span data-ttu-id="98308-115">對於所有資料庫的 `sysadmin` 以及擁有資料庫的 `db_owner` 角色成員而言，這個權限是隱含的。</span><span class="sxs-lookup"><span data-stu-id="98308-115">This permission is implied for `sysadmin` for all databases, and `db_owner` role members in databases that they own.</span></span>  
  
## <a name="granting-permissions-with-the-execute-as-clause"></a><span data-ttu-id="98308-116">使用 EXECUTE AS 子句來授與權限</span><span class="sxs-lookup"><span data-stu-id="98308-116">Granting Permissions with the EXECUTE AS Clause</span></span>  

 <span data-ttu-id="98308-117">您可以在預存程序、觸發程序或使用者定義函式 (內嵌 (Inline) 資料表值函式除外) 的定義標頭中使用 EXECUTE AS 子句。</span><span class="sxs-lookup"><span data-stu-id="98308-117">You can use the EXECUTE AS clause in the definition header of a stored procedure, trigger, or user-defined function (except for inline table-valued functions).</span></span> <span data-ttu-id="98308-118">這樣做會導致此程序在 EXECUTE AS 子句中指定之使用者名稱或關鍵字的內容中執行。</span><span class="sxs-lookup"><span data-stu-id="98308-118">This causes the procedure to execute in the context of the user name or keyword specified in the EXECUTE AS clause.</span></span> <span data-ttu-id="98308-119">您可以在資料庫中建立沒有對應至登入的 Proxy 使用者，並僅授與此程序所存取之物件的必要權限給該位使用者。</span><span class="sxs-lookup"><span data-stu-id="98308-119">You can create a proxy user in the database that is not mapped to a login, granting it only the necessary permissions on the objects accessed by the procedure.</span></span> <span data-ttu-id="98308-120">只有 EXECUTE AS 子句中指定的 Proxy 使用者必須擁有此模組所存取之所有物件的權限。</span><span class="sxs-lookup"><span data-stu-id="98308-120">Only the proxy user specified in the EXECUTE AS clause must have permissions on all objects accessed by the module.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="98308-121">某些動作 (例如 TRUNCATE TABLE) 沒有可授與的權限。</span><span class="sxs-lookup"><span data-stu-id="98308-121">Some actions, such as TRUNCATE TABLE, do not have grantable permissions.</span></span> <span data-ttu-id="98308-122">您可以在程序中併入陳述式並指定擁有 ALTER TABLE 權限的 Proxy 使用者，藉以針對僅擁有程序之 EXECUTE 權限的呼叫端擴充截斷資料表的權限。</span><span class="sxs-lookup"><span data-stu-id="98308-122">By incorporating the statement within a procedure and specifying a proxy user who has ALTER TABLE permissions, you can extend the permissions to truncate the table to callers who have only EXECUTE permissions on the procedure.</span></span>  
  
 <span data-ttu-id="98308-123">EXECUTE AS 子句中指定的內容在此程序的持續期間內有效，包括巢狀程序和觸發程序。</span><span class="sxs-lookup"><span data-stu-id="98308-123">The context specified in the EXECUTE AS clause is valid for the duration of the procedure, including nested procedures and triggers.</span></span> <span data-ttu-id="98308-124">當執行完成或發出 REVERT 陳述式時，內容就會還原成呼叫端。</span><span class="sxs-lookup"><span data-stu-id="98308-124">Context reverts to the caller when execution is complete or the REVERT statement is issued.</span></span>  
  
 <span data-ttu-id="98308-125">在程序中使用 EXECUTE AS 子句包含三個步驟。</span><span class="sxs-lookup"><span data-stu-id="98308-125">There are three steps involved in using the EXECUTE AS clause in a procedure.</span></span>  
  
1. <span data-ttu-id="98308-126">在資料庫中建立沒有對應至登入的 Proxy 使用者。</span><span class="sxs-lookup"><span data-stu-id="98308-126">Create a proxy user in the database that is not mapped to a login.</span></span> <span data-ttu-id="98308-127">雖然這並非必要條件，但是在管理權限時很有用。</span><span class="sxs-lookup"><span data-stu-id="98308-127">This is not required, but it helps when managing permissions.</span></span>  
  
```sql
CREATE USER proxyUser WITHOUT LOGIN  
```  
  
1. <span data-ttu-id="98308-128">將必要權限授與 Proxy 使用者。</span><span class="sxs-lookup"><span data-stu-id="98308-128">Grant the proxy user the necessary permissions.</span></span>  
  
2. <span data-ttu-id="98308-129">將 EXECUTE AS 子句加入至預存程序或使用者定義函式。</span><span class="sxs-lookup"><span data-stu-id="98308-129">Add the EXECUTE AS clause to the stored procedure or user-defined function.</span></span>  
  
```sql
CREATE PROCEDURE [procName] WITH EXECUTE AS 'proxyUser' AS ...  
```  
  
> [!NOTE]
> <span data-ttu-id="98308-130">需要稽核的應用程式可能會中斷，因為系統沒有保留呼叫端的原始安全性內容。</span><span class="sxs-lookup"><span data-stu-id="98308-130">Applications that require auditing can break because the original security context of the caller is not retained.</span></span> <span data-ttu-id="98308-131">傳回目前使用者之識別 (例如 SESSION_USER、USER 或 USER_NAME) 的內建函式會傳回與 EXECUTE AS 子句相關聯的使用者，而非原始呼叫端。</span><span class="sxs-lookup"><span data-stu-id="98308-131">Built-in functions that return the identity of the current user, such as SESSION_USER, USER, or USER_NAME, return the user associated with the EXECUTE AS clause, not the original caller.</span></span>  
  
### <a name="using-execute-as-with-revert"></a><span data-ttu-id="98308-132">使用 EXECUTE AS 搭配 REVERT</span><span class="sxs-lookup"><span data-stu-id="98308-132">Using EXECUTE AS with REVERT</span></span>  

 <span data-ttu-id="98308-133">您可以使用 Transact-SQL REVERT 陳述式來還原成原始執行內容。</span><span class="sxs-lookup"><span data-stu-id="98308-133">You can use the Transact-SQL REVERT statement to revert to the original execution context.</span></span>  
  
 <span data-ttu-id="98308-134">選擇性子句（沒有還原 COOKIE = @variableName ）可讓您在 @variableName 變數包含正確的值時，將執行內容切換回呼叫端。</span><span class="sxs-lookup"><span data-stu-id="98308-134">The optional clause, WITH NO REVERT COOKIE = @variableName, allows you switch the execution context back to the caller if the @variableName variable contains the correct value.</span></span> <span data-ttu-id="98308-135">這樣可讓您在使用連接共用 (Connection Pooling) 的環境中，將執行內容切換回呼叫端。</span><span class="sxs-lookup"><span data-stu-id="98308-135">This allows you to switch the execution context back to the caller in environments where connection pooling is used.</span></span> <span data-ttu-id="98308-136">由於的值 @variableName 只有 EXECUTE AS 語句的呼叫者知道，呼叫者可以保證叫用應用程式的終端使用者無法變更執行內容。</span><span class="sxs-lookup"><span data-stu-id="98308-136">Because the value of @variableName is known only to the caller of the EXECUTE AS statement, the caller can guarantee that the execution context cannot be changed by the end user that invokes the application.</span></span> <span data-ttu-id="98308-137">關閉連接時，它就會傳回集區。</span><span class="sxs-lookup"><span data-stu-id="98308-137">When the connection is closed, it is returned to the pool.</span></span> <span data-ttu-id="98308-138">如需 ADO.NET 中連接共用的詳細資訊，請參閱 [ (ADO.NET) SQL Server 連接 ](../sql-server-connection-pooling.md)共用。</span><span class="sxs-lookup"><span data-stu-id="98308-138">For more information on connection pooling in ADO.NET, see [SQL Server Connection Pooling (ADO.NET)](../sql-server-connection-pooling.md).</span></span>  
  
### <a name="specifying-the-execution-context"></a><span data-ttu-id="98308-139">指定執行內容</span><span class="sxs-lookup"><span data-stu-id="98308-139">Specifying the Execution Context</span></span>  

 <span data-ttu-id="98308-140">除了指定使用者以外，您也可以使用 EXECUTE AS 搭配下列任何關鍵字。</span><span class="sxs-lookup"><span data-stu-id="98308-140">In addition to specifying a user, you can also use EXECUTE AS with any of the following keywords.</span></span>  
  
- <span data-ttu-id="98308-141">CALLER：</span><span class="sxs-lookup"><span data-stu-id="98308-141">CALLER.</span></span> <span data-ttu-id="98308-142">以 CALLER 的身分執行是預設值。如果沒有指定任何其他選項，此程序就會在呼叫端的安全性內容中執行。</span><span class="sxs-lookup"><span data-stu-id="98308-142">Executing as CALLER is the default; if no other option is specified, then the procedure executes in the security context of the caller.</span></span>  
  
- <span data-ttu-id="98308-143">OWNER：</span><span class="sxs-lookup"><span data-stu-id="98308-143">OWNER.</span></span> <span data-ttu-id="98308-144">以 OWNER 的身分執行會在程序擁有者的內容中執行此程序。</span><span class="sxs-lookup"><span data-stu-id="98308-144">Executing as OWNER executes the procedure in the context of the procedure owner.</span></span> <span data-ttu-id="98308-145">如果此程序建立於 `dbo` 或資料庫擁有者所擁有的結構描述中，此程序將以不受限制的權限執行。</span><span class="sxs-lookup"><span data-stu-id="98308-145">If the procedure is created in a schema owned by `dbo` or the database owner, the procedure will execute with unrestricted permissions.</span></span>  
  
- <span data-ttu-id="98308-146">SELF：</span><span class="sxs-lookup"><span data-stu-id="98308-146">SELF.</span></span> <span data-ttu-id="98308-147">以 SELF 的身分執行會在預存程序之建立者的安全性內容中執行。</span><span class="sxs-lookup"><span data-stu-id="98308-147">Executing as SELF executes in the security context of the creator of the stored procedure.</span></span> <span data-ttu-id="98308-148">這相當於以指定之使用者的身分執行，而該指定的使用者是建立或更改程序的人員。</span><span class="sxs-lookup"><span data-stu-id="98308-148">This is equivalent to executing as a specified user, where the specified user is the person creating or altering the procedure.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="98308-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="98308-149">See also</span></span>

- [<span data-ttu-id="98308-150">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="98308-150">Securing ADO.NET Applications</span></span>](../securing-ado-net-applications.md)
- [<span data-ttu-id="98308-151">SQL Server 安全性概觀</span><span class="sxs-lookup"><span data-stu-id="98308-151">Overview of SQL Server Security</span></span>](overview-of-sql-server-security.md)
- [<span data-ttu-id="98308-152">SQL Server 中的應用程式安全性案例</span><span class="sxs-lookup"><span data-stu-id="98308-152">Application Security Scenarios in SQL Server</span></span>](application-security-scenarios-in-sql-server.md)
- [<span data-ttu-id="98308-153">使用預存程序管理 SQL Server 中的權限</span><span class="sxs-lookup"><span data-stu-id="98308-153">Managing Permissions with Stored Procedures in SQL Server</span></span>](managing-permissions-with-stored-procedures-in-sql-server.md)
- [<span data-ttu-id="98308-154">在 SQL Server 撰寫安全動態 SQL</span><span class="sxs-lookup"><span data-stu-id="98308-154">Writing Secure Dynamic SQL in SQL Server</span></span>](writing-secure-dynamic-sql-in-sql-server.md)
- [<span data-ttu-id="98308-155">在 SQL Server 中簽署預存程序</span><span class="sxs-lookup"><span data-stu-id="98308-155">Signing Stored Procedures in SQL Server</span></span>](signing-stored-procedures-in-sql-server.md)
- [<span data-ttu-id="98308-156">使用預存程序修改資料</span><span class="sxs-lookup"><span data-stu-id="98308-156">Modifying Data with Stored Procedures</span></span>](../modifying-data-with-stored-procedures.md)
- <span data-ttu-id="98308-157">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="98308-157">[ADO.NET Overview](../ado-net-overview.md)</span></span>
