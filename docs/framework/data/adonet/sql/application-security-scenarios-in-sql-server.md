---
title: SQL Server 中的應用程式安全性案例
ms.date: 03/30/2017
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.openlocfilehash: 2d0e65f61939312bf29111e87c49366cd9e389be
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197647"
---
# <a name="application-security-scenarios-in-sql-server"></a><span data-ttu-id="f8475-102">SQL Server 中的應用程式安全性案例</span><span class="sxs-lookup"><span data-stu-id="f8475-102">Application Security Scenarios in SQL Server</span></span>

<span data-ttu-id="f8475-103">並沒有單一的正確方式可建立安全的 SQL Server 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8475-103">There is no single correct way to create a secure SQL Server client application.</span></span> <span data-ttu-id="f8475-104">每個應用程式的需求、部署環境與使用者母體都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f8475-104">Every application is unique in its requirements, deployment environment, and user population.</span></span> <span data-ttu-id="f8475-105">一開始部署時相當安全的應用程式，其安全性可能會隨著時間過去而降低。</span><span class="sxs-lookup"><span data-stu-id="f8475-105">An application that is reasonably secure when it is initially deployed can become less secure over time.</span></span> <span data-ttu-id="f8475-106">沒有任何方式能夠準確預測未來可能會出現什麼樣的威脅。</span><span class="sxs-lookup"><span data-stu-id="f8475-106">It is impossible to predict with any accuracy what threats may emerge in the future.</span></span>  
  
 <span data-ttu-id="f8475-107">SQL Server 這個產品已經演變許多版本以納入最新的安全性功能，讓開發人員能建立安全的資料庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8475-107">SQL Server, as a product, has evolved over many versions to incorporate the latest security features that enable developers to create secure database applications.</span></span> <span data-ttu-id="f8475-108">不過，安全性並不會無中生有，需要透過持續地監視及更新才能獲得。</span><span class="sxs-lookup"><span data-stu-id="f8475-108">However, security doesn't come in the box; it requires continual monitoring and updating.</span></span>  
  
## <a name="common-threats"></a><span data-ttu-id="f8475-109">常見威脅</span><span class="sxs-lookup"><span data-stu-id="f8475-109">Common Threats</span></span>  

 <span data-ttu-id="f8475-110">開發人員必須了解安全性威脅、用來計算威脅的工具，以及如何避免自我造成的安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="f8475-110">Developers need to understand security threats, the tools provided to counter them, and how to avoid self-inflicted security holes.</span></span> <span data-ttu-id="f8475-111">我們可以將安全性視為一個鏈結，其中任何一個連結中斷都會危害整體的強度。</span><span class="sxs-lookup"><span data-stu-id="f8475-111">Security can best be thought of as a chain, where a break in any one link compromises the strength of the whole.</span></span> <span data-ttu-id="f8475-112">下列清單包含一些常見的安全性威脅，我們會在此節的主題中深入討論。</span><span class="sxs-lookup"><span data-stu-id="f8475-112">The following list includes some common security threats that are discussed in more detail in the topics in this section.</span></span>  
  
### <a name="sql-injection"></a><span data-ttu-id="f8475-113">SQL 插入</span><span class="sxs-lookup"><span data-stu-id="f8475-113">SQL Injection</span></span>  

 <span data-ttu-id="f8475-114">SQL 插入式攻擊是指惡意使用者輸入 Transact-SQL 陳述式，而非提供有效輸入的程序。</span><span class="sxs-lookup"><span data-stu-id="f8475-114">SQL Injection is the process by which a malicious user enters Transact-SQL statements instead of valid input.</span></span> <span data-ttu-id="f8475-115">如果在未驗證的情況下將輸入直接傳遞至伺服器，而且應用程式不慎執行了以資料隱碼方式撰寫的程式碼，攻擊就可能會破壞或損毀資料。</span><span class="sxs-lookup"><span data-stu-id="f8475-115">If the input is passed directly to the server without being validated and if the application inadvertently executes the injected code, then the attack has the potential to damage or destroy data.</span></span> <span data-ttu-id="f8475-116">您可以透過預存程序和參數化命令、避免動態 SQL 以及限制所有使用者的權限來防堵 SQL Server 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="f8475-116">You can thwart SQL Server injection attacks by using stored procedures and parameterized commands, avoiding dynamic SQL, and restricting permissions on all users.</span></span>  
  
### <a name="elevation-of-privilege"></a><span data-ttu-id="f8475-117">提高權限</span><span class="sxs-lookup"><span data-stu-id="f8475-117">Elevation of Privilege</span></span>  

 <span data-ttu-id="f8475-118">當使用者能夠取得像是擁有者或系統管理員等受信任帳戶的權限時，就會發生權限提高攻擊。</span><span class="sxs-lookup"><span data-stu-id="f8475-118">Elevation of privilege attacks occur when a user is able to assume the privileges of a trusted account, such as an owner or administrator.</span></span> <span data-ttu-id="f8475-119">因此請一律使用具備最低權限的使用者帳戶來執行，並只指派需要的權限。</span><span class="sxs-lookup"><span data-stu-id="f8475-119">Always run under least-privileged user accounts and assign only needed permissions.</span></span> <span data-ttu-id="f8475-120">避免使用系統管理或擁有者帳戶來執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="f8475-120">Avoid using administrative or owner accounts for executing code.</span></span> <span data-ttu-id="f8475-121">這可以限制攻擊成功時可能產生的破壞力。</span><span class="sxs-lookup"><span data-stu-id="f8475-121">This limits the amount of damage that can occur if an attack succeeds.</span></span> <span data-ttu-id="f8475-122">執行需要額外權限的工作時，請只在工作期間使用程序簽署或模擬。</span><span class="sxs-lookup"><span data-stu-id="f8475-122">When performing tasks that require additional permissions, use procedure signing or impersonation only for the duration of the task.</span></span> <span data-ttu-id="f8475-123">您可以用憑證來簽署預存程序，或使用模擬來暫時指派權限。</span><span class="sxs-lookup"><span data-stu-id="f8475-123">You can sign stored procedures with certificates or use impersonation to temporarily assign permissions.</span></span>  
  
### <a name="probing-and-intelligent-observation"></a><span data-ttu-id="f8475-124">探查和智慧型觀測</span><span class="sxs-lookup"><span data-stu-id="f8475-124">Probing and Intelligent Observation</span></span>  

 <span data-ttu-id="f8475-125">探查攻擊可能會使用應用程式所產生的錯誤訊息來搜尋安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="f8475-125">A probing attack can use error messages generated by an application to search for security vulnerabilities.</span></span> <span data-ttu-id="f8475-126">請在所有程序性程式碼中實作錯誤處理功能，以防止系統將 SQL Server 錯誤資訊傳回給終端使用者。</span><span class="sxs-lookup"><span data-stu-id="f8475-126">Implement error handling in all procedural code to prevent SQL Server error information from being returned to the end user.</span></span>  
  
### <a name="authentication"></a><span data-ttu-id="f8475-127">驗證</span><span class="sxs-lookup"><span data-stu-id="f8475-127">Authentication</span></span>  

 <span data-ttu-id="f8475-128">如果以使用者輸入為基礎的連接字串是在執行階段所建構的，使用 SQL Server 登入時就可能會發生連接字串插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="f8475-128">A connection string injection attack can occur when using SQL Server logins if a connection string based on user input is constructed at run time.</span></span> <span data-ttu-id="f8475-129">如果未檢查連接字串是否包含有效的關鍵字組，攻擊者就可能會透過插入額外的字元，來存取伺服器上的機密資料或其他資源。</span><span class="sxs-lookup"><span data-stu-id="f8475-129">If the connection string is not checked for valid keyword pairs, an attacker can insert extra characters, potentially accessing sensitive data or other resources on the server.</span></span> <span data-ttu-id="f8475-130">可能的話，請盡量使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="f8475-130">Use Windows authentication wherever possible.</span></span> <span data-ttu-id="f8475-131">如果您必須使用 SQL Server 登入，請使用 <xref:System.Data.SqlClient.SqlConnectionStringBuilder>，以在執行階段建立及驗證連接字串。</span><span class="sxs-lookup"><span data-stu-id="f8475-131">If you must use SQL Server logins, use the <xref:System.Data.SqlClient.SqlConnectionStringBuilder> to create and validate connection strings at run time.</span></span>  
  
### <a name="passwords"></a><span data-ttu-id="f8475-132">密碼</span><span class="sxs-lookup"><span data-stu-id="f8475-132">Passwords</span></span>  

 <span data-ttu-id="f8475-133">許多攻擊能夠成功的原因在於入侵者能夠取得或猜出有特殊權限的使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="f8475-133">Many attacks succeed because an intruder was able to obtain or guess a password for a privileged user.</span></span> <span data-ttu-id="f8475-134">密碼是對抗入侵者的第一道防線，因此，設定強式密碼對於系統的安全性很重要。</span><span class="sxs-lookup"><span data-stu-id="f8475-134">Passwords are your first line of defense against intruders, so setting strong passwords is essential to the security of your system.</span></span> <span data-ttu-id="f8475-135">針對混合模式驗證建立並強制執行密碼原則。</span><span class="sxs-lookup"><span data-stu-id="f8475-135">Create and enforce password policies for mixed mode authentication.</span></span>  
  
 <span data-ttu-id="f8475-136">即使使用「Windows 驗證」，也請一律指派強式密碼給 `sa` 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f8475-136">Always assign a strong password to the `sa` account, even when using Windows Authentication.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="f8475-137">本節內容</span><span class="sxs-lookup"><span data-stu-id="f8475-137">In This Section</span></span>  

 [<span data-ttu-id="f8475-138">使用預存程序管理 SQL Server 中的權限</span><span class="sxs-lookup"><span data-stu-id="f8475-138">Managing Permissions with Stored Procedures in SQL Server</span></span>](managing-permissions-with-stored-procedures-in-sql-server.md)  
 <span data-ttu-id="f8475-139">說明如何使用預存程序 (Stored Procedure) 管理權限並控制資料存取。</span><span class="sxs-lookup"><span data-stu-id="f8475-139">Describes how to use stored procedures to manage permissions and control data access.</span></span> <span data-ttu-id="f8475-140">使用預存程序是許多安全性威脅的有效回應方式。</span><span class="sxs-lookup"><span data-stu-id="f8475-140">Using stored procedures is an effective way to respond to many security threats.</span></span>  
  
 [<span data-ttu-id="f8475-141">在 SQL Server 撰寫安全動態 SQL</span><span class="sxs-lookup"><span data-stu-id="f8475-141">Writing Secure Dynamic SQL in SQL Server</span></span>](writing-secure-dynamic-sql-in-sql-server.md)  
 <span data-ttu-id="f8475-142">說明使用預存程序撰寫安全動態 SQL 的技術。</span><span class="sxs-lookup"><span data-stu-id="f8475-142">Describes techniques for writing secure dynamic SQL using stored procedures.</span></span>  
  
 [<span data-ttu-id="f8475-143">在 SQL Server 中簽署預存程序</span><span class="sxs-lookup"><span data-stu-id="f8475-143">Signing Stored Procedures in SQL Server</span></span>](signing-stored-procedures-in-sql-server.md)  
 <span data-ttu-id="f8475-144">說明如何使用憑證簽署預存程序，讓使用者可以使用不能直接存取的資料。</span><span class="sxs-lookup"><span data-stu-id="f8475-144">Describes how to sign a stored procedure with a certificate to enable users to work with data they do not have direct access to.</span></span> <span data-ttu-id="f8475-145">如此預存程序就可以執行呼叫端並無直接執行權限的作業。</span><span class="sxs-lookup"><span data-stu-id="f8475-145">This enables stored procedures to perform operations that the caller does not have permissions to perform directly.</span></span>  
  
 [<span data-ttu-id="f8475-146">在 SQL Server 中使用模擬來自訂權限</span><span class="sxs-lookup"><span data-stu-id="f8475-146">Customizing Permissions with Impersonation in SQL Server</span></span>](customizing-permissions-with-impersonation-in-sql-server.md)  
 <span data-ttu-id="f8475-147">說明如何使用 EXECUTE AS 子句模擬其他使用者。</span><span class="sxs-lookup"><span data-stu-id="f8475-147">Describes how to use the EXECUTE AS clause to impersonate another user.</span></span> <span data-ttu-id="f8475-148">模擬會將執行內容從呼叫端切換到指定的使用者。</span><span class="sxs-lookup"><span data-stu-id="f8475-148">Impersonation switches the execution context from the caller to the specified user.</span></span>  
  
 [<span data-ttu-id="f8475-149">在 SQL Server 中授與資料列層級權限</span><span class="sxs-lookup"><span data-stu-id="f8475-149">Granting Row-Level Permissions in SQL Server</span></span>](granting-row-level-permissions-in-sql-server.md)  
 <span data-ttu-id="f8475-150">說明如何實作資料列層級權限以限制資料存取。</span><span class="sxs-lookup"><span data-stu-id="f8475-150">Describes how to implement row-level permissions to restrict data access.</span></span>  
  
 [<span data-ttu-id="f8475-151">在 SQL Server 中建立應用程式角色</span><span class="sxs-lookup"><span data-stu-id="f8475-151">Creating Application Roles in SQL Server</span></span>](creating-application-roles-in-sql-server.md)  
 <span data-ttu-id="f8475-152">說明應用程式角色的功能。</span><span class="sxs-lookup"><span data-stu-id="f8475-152">Describes features and functionality of application roles.</span></span>  
  
 [<span data-ttu-id="f8475-153">在 SQL Server 中啟用跨資料庫存取</span><span class="sxs-lookup"><span data-stu-id="f8475-153">Enabling Cross-Database Access in SQL Server</span></span>](enabling-cross-database-access-in-sql-server.md)  
 <span data-ttu-id="f8475-154">說明如何在不危及安全性的前提下啟用跨資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="f8475-154">Describes how to enable cross-database access without jeopardizing security.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f8475-155">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f8475-155">See also</span></span>

- [<span data-ttu-id="f8475-156">SQL Server 安全性</span><span class="sxs-lookup"><span data-stu-id="f8475-156">SQL Server Security</span></span>](sql-server-security.md)
- [<span data-ttu-id="f8475-157">SQL Server 安全性概觀</span><span class="sxs-lookup"><span data-stu-id="f8475-157">Overview of SQL Server Security</span></span>](overview-of-sql-server-security.md)
- [<span data-ttu-id="f8475-158">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="f8475-158">Securing ADO.NET Applications</span></span>](../securing-ado-net-applications.md)
- <span data-ttu-id="f8475-159">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="f8475-159">[ADO.NET Overview](../ado-net-overview.md)</span></span>
