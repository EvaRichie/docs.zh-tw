---
title: 在 SQL Server 中簽署預存程序
ms.date: 01/05/2018
ms.assetid: eeed752c-0084-48e5-9dca-381353007a0d
ms.openlocfilehash: 3f33af0238781407dd845a823ff28d87af48feb2
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558546"
---
# <a name="signing-stored-procedures-in-sql-server"></a><span data-ttu-id="004da-102">在 SQL Server 中簽署預存程序</span><span class="sxs-lookup"><span data-stu-id="004da-102">Signing Stored Procedures in SQL Server</span></span>

<span data-ttu-id="004da-103">數位簽章是指使用簽署者之私密金鑰 (Private Key) 加密的資料摘要。</span><span class="sxs-lookup"><span data-stu-id="004da-103">A digital signature is a data digest encrypted with the private key of the signer.</span></span> <span data-ttu-id="004da-104">私密金鑰可確保數位簽章對於其 Bearer 或擁有者而言是唯一的。</span><span class="sxs-lookup"><span data-stu-id="004da-104">The private key ensures that the digital signature is unique to its bearer or owner.</span></span> <span data-ttu-id="004da-105">您可以簽署預存程式、函式 (，但內嵌資料表值函式) 、觸發程式和元件除外。</span><span class="sxs-lookup"><span data-stu-id="004da-105">You can sign stored procedures, functions (except for inline table-valued functions), triggers, and assemblies.</span></span>

<span data-ttu-id="004da-106">您可以使用憑證或非對稱金鑰來簽署預存程序。</span><span class="sxs-lookup"><span data-stu-id="004da-106">You can sign a stored procedure with a certificate or an asymmetric key.</span></span> <span data-ttu-id="004da-107">這是針對無法透過擁有權鏈結繼承權限或擁有權鏈結中斷 (例如動態 SQL) 的案例所設計。</span><span class="sxs-lookup"><span data-stu-id="004da-107">This is designed for scenarios when permissions cannot be inherited through ownership chaining or when the ownership chain is broken, such as dynamic SQL.</span></span> <span data-ttu-id="004da-108">然後，您可以建立對應至憑證的使用者，將預存程式需要存取之物件的許可權授與憑證使用者。</span><span class="sxs-lookup"><span data-stu-id="004da-108">You can then create a user mapped to the certificate, granting the certificate user permissions on the objects the stored procedure needs to access.</span></span>

<span data-ttu-id="004da-109">您也可以建立對應至相同憑證的登入，然後將所需的伺服器層級許可權授與該登入，或將登入加入至一或多個固定伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="004da-109">You can also create a login mapped to the same certificate, and then grant any necessary server-level permissions to that login, or add the login to one or more of the fixed server roles.</span></span> <span data-ttu-id="004da-110">這是為了避免在 `TRUSTWORTHY` 需要較高層級許可權的情況下啟用資料庫設定的目的。</span><span class="sxs-lookup"><span data-stu-id="004da-110">This is designed to avoid enabling the `TRUSTWORTHY` database setting for scenarios in which higher level permissions are needed.</span></span>

<span data-ttu-id="004da-111">當執行預存程式時，SQL Server 會將憑證使用者和/或登入的許可權與呼叫端的許可權結合在一起。</span><span class="sxs-lookup"><span data-stu-id="004da-111">When the stored procedure is executed, SQL Server combines the permissions of the certificate user and/or login with those of the caller.</span></span> <span data-ttu-id="004da-112">和子句不同的是 `EXECUTE AS` ，它不會變更程式的執行內容。</span><span class="sxs-lookup"><span data-stu-id="004da-112">Unlike the `EXECUTE AS` clause, it does not change the execution context of the procedure.</span></span> <span data-ttu-id="004da-113">傳回登入和使用者名稱的內建函式會傳回呼叫端的名稱，而非憑證使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="004da-113">Built-in functions that return login and user names return the name of the caller, not the certificate user name.</span></span>

## <a name="creating-certificates"></a><span data-ttu-id="004da-114">建立憑證</span><span class="sxs-lookup"><span data-stu-id="004da-114">Creating Certificates</span></span>

<span data-ttu-id="004da-115">當您使用憑證或非對稱金鑰簽署預存程式時，系統會使用私密金鑰來建立包含預存程式程式碼的加密雜湊以及執行為使用者的資料摘要。</span><span class="sxs-lookup"><span data-stu-id="004da-115">When you sign a stored procedure with a certificate or asymmetric key, a data digest consisting of the encrypted hash of the stored procedure code, along with the execute-as user, is created using the private key.</span></span> <span data-ttu-id="004da-116">在執行階段中，系統會使用公開金鑰 (Public Key) 來解密資料摘要，並與預存程序的雜湊值 (Hash Value) 進行比較。</span><span class="sxs-lookup"><span data-stu-id="004da-116">At run time, the data digest is decrypted with the public key and compared with the hash value of the stored procedure.</span></span> <span data-ttu-id="004da-117">變更 execute as 使用者會讓雜湊值失效，使數位簽章不再相符。</span><span class="sxs-lookup"><span data-stu-id="004da-117">Changing the execute-as user invalidates the hash value so that the digital signature no longer matches.</span></span> <span data-ttu-id="004da-118">修改預存程式會完全卸載簽章，這可防止沒有私密金鑰存取權的人員變更預存程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="004da-118">Modifying the stored procedure drops the signature entirely, which prevents someone who does not have access to the private key from changing the stored procedure code.</span></span> <span data-ttu-id="004da-119">無論是哪一種情況，您都必須在每次變更程式碼或執行為使用者時重新簽署程式。</span><span class="sxs-lookup"><span data-stu-id="004da-119">In either case, you must re-sign the procedure each time you change the code or the execute-as user.</span></span>

<span data-ttu-id="004da-120">簽署模組有兩個必要步驟：</span><span class="sxs-lookup"><span data-stu-id="004da-120">There are two required steps involved in signing a module:</span></span>

1. <span data-ttu-id="004da-121">使用 Transact-SQL `CREATE CERTIFICATE [certificateName]` 陳述式來建立憑證。</span><span class="sxs-lookup"><span data-stu-id="004da-121">Create a certificate using the Transact-SQL `CREATE CERTIFICATE [certificateName]` statement.</span></span> <span data-ttu-id="004da-122">這個陳述式具有許多設定開始和結束日期與密碼的選項。</span><span class="sxs-lookup"><span data-stu-id="004da-122">This statement has several options for setting a start and end date and a password.</span></span> <span data-ttu-id="004da-123">預設的到期日是一年。</span><span class="sxs-lookup"><span data-stu-id="004da-123">The default expiration date is one year.</span></span>

1. <span data-ttu-id="004da-124">使用 Transact-SQL `ADD SIGNATURE TO [procedureName] BY CERTIFICATE [certificateName]` 陳述式並搭配憑證來簽署程序。</span><span class="sxs-lookup"><span data-stu-id="004da-124">Sign the procedure with the certificate using the Transact-SQL `ADD SIGNATURE TO [procedureName] BY CERTIFICATE [certificateName]` statement.</span></span>

<span data-ttu-id="004da-125">一旦將模組簽署之後，必須建立一或多個主體，才能保存應該與憑證相關聯的其他許可權。</span><span class="sxs-lookup"><span data-stu-id="004da-125">Once the module has been signed, one or more principals needs to be created in order to hold the additional permissions that should be associated with the certificate.</span></span>

<span data-ttu-id="004da-126">如果模組需要額外的資料庫層級許可權：</span><span class="sxs-lookup"><span data-stu-id="004da-126">If the module needs additional database-level permissions:</span></span>

1. <span data-ttu-id="004da-127">使用 Transact-SQL `CREATE USER [userName] FROM CERTIFICATE [certificateName]` 陳述式來建立與憑證相關聯的資料庫使用者。</span><span class="sxs-lookup"><span data-stu-id="004da-127">Create a database user associated with that certificate using the Transact-SQL `CREATE USER [userName] FROM CERTIFICATE [certificateName]` statement.</span></span> <span data-ttu-id="004da-128">此使用者僅存在於資料庫中，除非也已經從相同的憑證建立登入，否則不會與登入相關聯。</span><span class="sxs-lookup"><span data-stu-id="004da-128">This user exists in the database only and is not associated with a login unless a login has also been created from that same certificate.</span></span>

1. <span data-ttu-id="004da-129">授與憑證使用者所需的資料庫層級許可權。</span><span class="sxs-lookup"><span data-stu-id="004da-129">Grant the certificate user the required database-level permissions.</span></span>

<span data-ttu-id="004da-130">如果模組需要額外的伺服器層級許可權：</span><span class="sxs-lookup"><span data-stu-id="004da-130">If the module needs additional server-level permissions:</span></span>

1. <span data-ttu-id="004da-131">將憑證複製到 `master` 資料庫。</span><span class="sxs-lookup"><span data-stu-id="004da-131">Copy the certificate to the `master` database.</span></span>

1. <span data-ttu-id="004da-132">使用 Transact-sql 語句建立與該憑證相關聯的登入 `CREATE LOGIN [userName] FROM CERTIFICATE [certificateName]` 。</span><span class="sxs-lookup"><span data-stu-id="004da-132">Create a login associated with that certificate using the Transact-SQL `CREATE LOGIN [userName] FROM CERTIFICATE [certificateName]` statement.</span></span>

1. <span data-ttu-id="004da-133">授與憑證登入所需的伺服器層級許可權。</span><span class="sxs-lookup"><span data-stu-id="004da-133">Grant the certificate login the required server-level permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="004da-134">憑證無法授與權限給擁有使用 DENY 陳述式撤銷之權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="004da-134">A certificate cannot grant permissions to a user that has had permissions revoked using the DENY statement.</span></span> <span data-ttu-id="004da-135">DENY 的優先順序永遠高於 GRANT，可防止呼叫端繼承授與憑證使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="004da-135">DENY always takes precedence over GRANT, preventing the caller from inheriting permissions granted to the certificate user.</span></span>

## <a name="external-resources"></a><span data-ttu-id="004da-136">外部資源</span><span class="sxs-lookup"><span data-stu-id="004da-136">External Resources</span></span>

<span data-ttu-id="004da-137">如需詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="004da-137">For more information, see the following resources.</span></span>

|<span data-ttu-id="004da-138">資源</span><span class="sxs-lookup"><span data-stu-id="004da-138">Resource</span></span>|<span data-ttu-id="004da-139">描述</span><span class="sxs-lookup"><span data-stu-id="004da-139">Description</span></span>|
|--------------|-----------------|
|<span data-ttu-id="004da-140">[模組簽署](/previous-versions/sql/sql-server-2008/ms345102(v=sql.100))</span><span class="sxs-lookup"><span data-stu-id="004da-140">[Module Signing](/previous-versions/sql/sql-server-2008/ms345102(v=sql.100))</span></span>|<span data-ttu-id="004da-141">描述模組簽署，提供範例案例和相關 Transact-sql 文章的連結。</span><span class="sxs-lookup"><span data-stu-id="004da-141">Describes module signing, providing a sample scenario and links to the relevant Transact-SQL articles.</span></span>|
|[<span data-ttu-id="004da-142">使用憑證簽署預存程序</span><span class="sxs-lookup"><span data-stu-id="004da-142">Signing Stored Procedures with a Certificate</span></span>](/sql/relational-databases/tutorial-signing-stored-procedures-with-a-certificate)|<span data-ttu-id="004da-143">提供使用憑證來簽署預存程序的教學課程。</span><span class="sxs-lookup"><span data-stu-id="004da-143">Provides a tutorial for signing a stored procedure with a certificate.</span></span>|

## <a name="see-also"></a><span data-ttu-id="004da-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="004da-144">See also</span></span>

- [<span data-ttu-id="004da-145">設定 ADO.NET 應用程式的安全性</span><span class="sxs-lookup"><span data-stu-id="004da-145">Securing ADO.NET Applications</span></span>](../securing-ado-net-applications.md)
- [<span data-ttu-id="004da-146">SQL Server 安全性概觀</span><span class="sxs-lookup"><span data-stu-id="004da-146">Overview of SQL Server Security</span></span>](overview-of-sql-server-security.md)
- [<span data-ttu-id="004da-147">SQL Server 中的應用程式安全性案例</span><span class="sxs-lookup"><span data-stu-id="004da-147">Application Security Scenarios in SQL Server</span></span>](application-security-scenarios-in-sql-server.md)
- [<span data-ttu-id="004da-148">使用預存程序管理 SQL Server 中的權限</span><span class="sxs-lookup"><span data-stu-id="004da-148">Managing Permissions with Stored Procedures in SQL Server</span></span>](managing-permissions-with-stored-procedures-in-sql-server.md)
- [<span data-ttu-id="004da-149">在 SQL Server 撰寫安全動態 SQL</span><span class="sxs-lookup"><span data-stu-id="004da-149">Writing Secure Dynamic SQL in SQL Server</span></span>](writing-secure-dynamic-sql-in-sql-server.md)
- [<span data-ttu-id="004da-150">在 SQL Server 中使用模擬來自訂權限</span><span class="sxs-lookup"><span data-stu-id="004da-150">Customizing Permissions with Impersonation in SQL Server</span></span>](customizing-permissions-with-impersonation-in-sql-server.md)
- [<span data-ttu-id="004da-151">使用預存程序修改資料</span><span class="sxs-lookup"><span data-stu-id="004da-151">Modifying Data with Stored Procedures</span></span>](../modifying-data-with-stored-procedures.md)
- <span data-ttu-id="004da-152">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="004da-152">[ADO.NET Overview](../ado-net-overview.md)</span></span>
