---
title: 在 SQL Server 中建立應用程式角色
ms.date: 03/30/2017
ms.assetid: 27442435-dfb2-4062-8c59-e2960833a638
ms.openlocfilehash: 764ae61cba4bf01681d658cc4aacc2aeaecedd3f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173545"
---
# <a name="creating-application-roles-in-sql-server"></a><span data-ttu-id="a779a-102">在 SQL Server 中建立應用程式角色</span><span class="sxs-lookup"><span data-stu-id="a779a-102">Creating Application Roles in SQL Server</span></span>

<span data-ttu-id="a779a-103">應用程式角色可以用於將權限指派給應用程式，而不是資料庫角色或使用者。</span><span class="sxs-lookup"><span data-stu-id="a779a-103">Application roles provide a way to assign permissions to an application instead of a database role or user.</span></span> <span data-ttu-id="a779a-104">使用者可以連接到資料庫、啟動應用程式角色，並採用授與應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="a779a-104">Users can connect to the database, activate the application role, and assume the permissions granted to the application.</span></span> <span data-ttu-id="a779a-105">授與應用程式角色的權限在連接期間內都會維持有效。</span><span class="sxs-lookup"><span data-stu-id="a779a-105">The permissions granted to the application role are in force for the duration of the connection.</span></span>  
  
> [!IMPORTANT]
> <span data-ttu-id="a779a-106">當用戶端應用程式在連接字串中提供應用程式角色名稱和密碼時，就會啟動應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="a779a-106">Application roles are activated when a client application supplies an application role name and a password in the connection string.</span></span> <span data-ttu-id="a779a-107">這些角色在雙層 (Two-Tier) 應用程式中會造成安全性弱點，因為密碼必須儲存在用戶端電腦上。</span><span class="sxs-lookup"><span data-stu-id="a779a-107">They present a security vulnerability in a two-tier application because the password must be stored on the client computer.</span></span> <span data-ttu-id="a779a-108">在三層 (Three-Tier) 應用程式中，則可以用應用程式使用者無法存取的方式來儲存密碼。</span><span class="sxs-lookup"><span data-stu-id="a779a-108">In a three-tier application, you can store the password so that it cannot be accessed by users of the application.</span></span>  
  
## <a name="application-role-features"></a><span data-ttu-id="a779a-109">應用程式角色功能</span><span class="sxs-lookup"><span data-stu-id="a779a-109">Application Role Features</span></span>  

 <span data-ttu-id="a779a-110">應用程式角色有下列功能：</span><span class="sxs-lookup"><span data-stu-id="a779a-110">Application roles have the following features:</span></span>  
  
- <span data-ttu-id="a779a-111">不同於資料庫角色，應用程式角色不包含任何成員。</span><span class="sxs-lookup"><span data-stu-id="a779a-111">Unlike database roles, application roles contain no members.</span></span>  
  
- <span data-ttu-id="a779a-112">當用戶端應用程式為 `sp_setapprole` 系統預存程序 (Stored Procedure) 提供應用程式角色名稱和密碼時，就會啟動應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="a779a-112">Application roles are activated when an application supplies the application role name and a password to the `sp_setapprole` system stored procedure.</span></span>  
  
- <span data-ttu-id="a779a-113">密碼必須儲存在用戶端電腦上，並在執行階段提供；您無法從 SQL Server 內部啟動應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="a779a-113">The password must be stored on the client computer and supplied at run time; an application role cannot be activated from inside of SQL Server.</span></span>  
  
- <span data-ttu-id="a779a-114">密碼不會加密。</span><span class="sxs-lookup"><span data-stu-id="a779a-114">The password is not encrypted.</span></span> <span data-ttu-id="a779a-115">參數密碼會儲存為單向雜湊。</span><span class="sxs-lookup"><span data-stu-id="a779a-115">The parameter password is stored as a one-way hash.</span></span>  
  
- <span data-ttu-id="a779a-116">透過應用程式角色所取得的權限一旦啟動，在連接期間內都會維持有效。</span><span class="sxs-lookup"><span data-stu-id="a779a-116">Once activated, permissions acquired through the application role remain in effect for the duration of the connection.</span></span>  
  
- <span data-ttu-id="a779a-117">應用程式會繼承授與 `public` 角色的權限。</span><span class="sxs-lookup"><span data-stu-id="a779a-117">The application role inherits permissions granted to the `public` role.</span></span>  
  
- <span data-ttu-id="a779a-118">如果 `sysadmin` 固定伺服器角色的成員啟動了應用程式角色，則安全性內容會在連接期間切換至應用程式角色的安全性內容。</span><span class="sxs-lookup"><span data-stu-id="a779a-118">If a member of the `sysadmin` fixed server role activates an application role, the security context switches to that of the application role for the duration of the connection.</span></span>  
  
- <span data-ttu-id="a779a-119">如果在具有應用程式角色的資料庫中建立 `guest` 帳戶，則不需要針對該應用程式角色或叫用 (Invoke) 該角色的登入而建立資料庫使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a779a-119">If you create a `guest` account in a database that has an application role, you do not need to create a database user account for the application role or for any of the logins that invoke it.</span></span> <span data-ttu-id="a779a-120">只有當 `guest` 帳戶存在於第二個資料庫中的時候，應用程式角色才可以直接存取其他資料庫。</span><span class="sxs-lookup"><span data-stu-id="a779a-120">Application roles can directly access another database only if a `guest` account exists in the second database</span></span>  
  
- <span data-ttu-id="a779a-121">傳回登入名稱 (例如 SYSTEM_USER) 的內建功能會傳回叫用應用程式角色的登入名稱；</span><span class="sxs-lookup"><span data-stu-id="a779a-121">Built-in functions that return login names, such as SYSTEM_USER, return the name of the login that invoked the application role.</span></span> <span data-ttu-id="a779a-122">傳回資料庫使用者名稱的內建功能則會傳回應用程式角色的名稱。</span><span class="sxs-lookup"><span data-stu-id="a779a-122">Built-in functions that return database user names return the name of the application role.</span></span>  
  
### <a name="the-principle-of-least-privilege"></a><span data-ttu-id="a779a-123">最小權限的原則</span><span class="sxs-lookup"><span data-stu-id="a779a-123">The Principle of Least Privilege</span></span>  

 <span data-ttu-id="a779a-124">應用程式角色僅能被授與必要的權限，以免密碼遭到破解。</span><span class="sxs-lookup"><span data-stu-id="a779a-124">Application roles should be granted only required permissions in case the password is compromised.</span></span> <span data-ttu-id="a779a-125">在所有使用應用程式角色的資料庫中，則應該額銷 `public` 角色的權限。</span><span class="sxs-lookup"><span data-stu-id="a779a-125">Permissions to the `public` role should be revoked in any database using an application role.</span></span> <span data-ttu-id="a779a-126">請在不想讓應用程式角色的呼叫端存取的資料庫中，停用 `guest` 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a779a-126">Disable the `guest` account in any database you do not want callers of the application role to have access to.</span></span>  
  
### <a name="application-role-enhancements"></a><span data-ttu-id="a779a-127">應用程式角色加強功能</span><span class="sxs-lookup"><span data-stu-id="a779a-127">Application Role Enhancements</span></span>  

 <span data-ttu-id="a779a-128">啟用應用程式角色之後，可以將執行內容切換回原始呼叫端，免除了停用連線集區的需要。</span><span class="sxs-lookup"><span data-stu-id="a779a-128">The execution context can be switched back to the original caller after activating an application role, removing the need to disable connection pooling.</span></span> <span data-ttu-id="a779a-129">`sp_setapprole` 程序具有建立 Cookie 的新選項，Cookie 中可包含有關呼叫端的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="a779a-129">The `sp_setapprole` procedure has a new option that creates a cookie, which contains context information about the caller.</span></span> <span data-ttu-id="a779a-130">您可以呼叫 `sp_unsetapprole` 程序並將 Cookie 傳送給它，藉此還原工作階段 (Session)。</span><span class="sxs-lookup"><span data-stu-id="a779a-130">You can revert the session by calling the `sp_unsetapprole` procedure, passing it the cookie.</span></span>  
  
## <a name="application-role-alternatives"></a><span data-ttu-id="a779a-131">應用程式角色替代方案</span><span class="sxs-lookup"><span data-stu-id="a779a-131">Application Role Alternatives</span></span>  

 <span data-ttu-id="a779a-132">應用程式角色仰賴密碼的安全性，而這點可能會造成安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="a779a-132">Application roles depend on the security of a password, which presents a potential security vulnerability.</span></span> <span data-ttu-id="a779a-133">密碼可能會因內嵌在應用程式程式碼或儲存在磁碟中而外洩。</span><span class="sxs-lookup"><span data-stu-id="a779a-133">Passwords may be exposed by being embedded in application code or saved on disk.</span></span>  
  
 <span data-ttu-id="a779a-134">您可能要考慮以下的替代方案。</span><span class="sxs-lookup"><span data-stu-id="a779a-134">You may want to consider the following alternatives.</span></span>  
  
- <span data-ttu-id="a779a-135">藉由 EXECUTE AS 陳述式 (使用 NO REVERT 和 WITH COOKIE 子句) 使用內容切換。</span><span class="sxs-lookup"><span data-stu-id="a779a-135">Use context switching with the EXECUTE AS statement with its NO REVERT and WITH COOKIE clauses.</span></span> <span data-ttu-id="a779a-136">您可以在資料庫中建立不與登入對應的使用者帳戶，</span><span class="sxs-lookup"><span data-stu-id="a779a-136">You can create a user account in a database that is not mapped to a login.</span></span> <span data-ttu-id="a779a-137">然後再將權限指派給這個帳戶。</span><span class="sxs-lookup"><span data-stu-id="a779a-137">You then assign permissions to this account.</span></span> <span data-ttu-id="a779a-138">以無登入的使用者來使用 EXECUTE AS 比較安全，因為這種方式是以權限為基礎，而不是以密碼為基礎。</span><span class="sxs-lookup"><span data-stu-id="a779a-138">Using EXECUTE AS with a login-less user is more secure because it is permission-based, not password-based.</span></span> <span data-ttu-id="a779a-139">如需詳細資訊，請參閱 [SQL Server 中的模擬自訂許可權](customizing-permissions-with-impersonation-in-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="a779a-139">For more information, see [Customizing Permissions with Impersonation in SQL Server](customizing-permissions-with-impersonation-in-sql-server.md).</span></span>  
  
- <span data-ttu-id="a779a-140">使用憑證來簽署預存程序，且僅授與執行程序的權限。</span><span class="sxs-lookup"><span data-stu-id="a779a-140">Sign stored procedures with certificates, granting only permission to execute the procedures.</span></span> <span data-ttu-id="a779a-141">如需詳細資訊，請參閱 [SQL Server 中的簽署預存程式](signing-stored-procedures-in-sql-server.md)。</span><span class="sxs-lookup"><span data-stu-id="a779a-141">For more information, see [Signing Stored Procedures in SQL Server](signing-stored-procedures-in-sql-server.md).</span></span>  
  
## <a name="external-resources"></a><span data-ttu-id="a779a-142">外部資源</span><span class="sxs-lookup"><span data-stu-id="a779a-142">External Resources</span></span>  

 <span data-ttu-id="a779a-143">如需詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="a779a-143">For more information, see the following resources.</span></span>  
  
|<span data-ttu-id="a779a-144">資源</span><span class="sxs-lookup"><span data-stu-id="a779a-144">Resource</span></span>|<span data-ttu-id="a779a-145">描述</span><span class="sxs-lookup"><span data-stu-id="a779a-145">Description</span></span>|  
|--------------|-----------------|  
|[<span data-ttu-id="a779a-146">應用程式角色</span><span class="sxs-lookup"><span data-stu-id="a779a-146">Application Roles</span></span>](/sql/relational-databases/security/authentication-access/application-roles)|<span data-ttu-id="a779a-147">說明如何在 SQL Server 2008 中建立及使用應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="a779a-147">Describes how to create and use application roles in SQL Server 2008.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="a779a-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a779a-148">See also</span></span>

- [<span data-ttu-id="a779a-149">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="a779a-149">Securing ADO.NET Applications</span></span>](../securing-ado-net-applications.md)
- [<span data-ttu-id="a779a-150">SQL Server 安全性概觀</span><span class="sxs-lookup"><span data-stu-id="a779a-150">Overview of SQL Server Security</span></span>](overview-of-sql-server-security.md)
- [<span data-ttu-id="a779a-151">SQL Server 中的應用程式安全性案例</span><span class="sxs-lookup"><span data-stu-id="a779a-151">Application Security Scenarios in SQL Server</span></span>](application-security-scenarios-in-sql-server.md)
- <span data-ttu-id="a779a-152">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="a779a-152">[ADO.NET Overview](../ado-net-overview.md)</span></span>
