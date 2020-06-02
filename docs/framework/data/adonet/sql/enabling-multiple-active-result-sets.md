---
title: 啟用 Multiple Active Result Set
description: 瞭解如何在連接字串中啟用/停用 MARS，這會與 SQL Server 搭配使用，讓您可以在 ADO.NET 的單一連接上執行多個批次。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
ms.openlocfilehash: 43bdfebce291c3c1d6c90104c5fef440b295934b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286477"
---
# <a name="enabling-multiple-active-result-sets"></a><span data-ttu-id="9311a-103">啟用 Multiple Active Result Set</span><span class="sxs-lookup"><span data-stu-id="9311a-103">Enabling Multiple Active Result Sets</span></span>
<span data-ttu-id="9311a-104">Multiple Active Result Set (MARS) 是與 SQL Server 搭配使用的功能，允許在單一連線中執行多個批次作業。</span><span class="sxs-lookup"><span data-stu-id="9311a-104">Multiple Active Result Sets (MARS) is a feature that works with SQL Server to allow the execution of multiple batches on a single connection.</span></span> <span data-ttu-id="9311a-105">在啟用 MARS 以與 SQL Server 搭配使用時，使用的每個命令物件都會在連線中新增工作階段。</span><span class="sxs-lookup"><span data-stu-id="9311a-105">When MARS is enabled for use with SQL Server, each command object used adds a session to the connection.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="9311a-106">單一 MARS 工作階段會開啟一個邏輯連線以供 MARS 使用，然後針對每個使用中的命令建立一個邏輯連線。</span><span class="sxs-lookup"><span data-stu-id="9311a-106">A single MARS session opens one logical connection for MARS to use and then one logical connection for each active command.</span></span>  
  
## <a name="enabling-and-disabling-mars-in-the-connection-string"></a><span data-ttu-id="9311a-107">在連接字串中啟用及停用 MARS</span><span class="sxs-lookup"><span data-stu-id="9311a-107">Enabling and Disabling MARS in the Connection String</span></span>  
  
> [!NOTE]
> <span data-ttu-id="9311a-108">下列連接字串使用包含於 SQL Server 的 **AdventureWorks** 範例資料庫。</span><span class="sxs-lookup"><span data-stu-id="9311a-108">The following connection strings use the sample **AdventureWorks** database included with SQL Server.</span></span> <span data-ttu-id="9311a-109">提供的連接字串假設資料庫已安裝於名為 MSSQL1 的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="9311a-109">The connection strings provided assume that the database is installed on a server named MSSQL1.</span></span> <span data-ttu-id="9311a-110">請依據環境需求修改連接字串。</span><span class="sxs-lookup"><span data-stu-id="9311a-110">Modify the connection string as necessary for your environment.</span></span>  
  
 <span data-ttu-id="9311a-111">此 MARS 功能預設為停用。</span><span class="sxs-lookup"><span data-stu-id="9311a-111">The MARS feature is disabled by default.</span></span> <span data-ttu-id="9311a-112">將 "MultipleActiveResultSets=True" 關鍵字組新增至連接字串，即可加以啟用。</span><span class="sxs-lookup"><span data-stu-id="9311a-112">It can be enabled by adding the "MultipleActiveResultSets=True" keyword pair to your connection string.</span></span> <span data-ttu-id="9311a-113">"True" 是啟用 MARS 的唯一有效值。</span><span class="sxs-lookup"><span data-stu-id="9311a-113">"True" is the only valid value for enabling MARS.</span></span> <span data-ttu-id="9311a-114">下列範例示範如何連線到 SQL Server 的執行個體，以及如何指定應該啟用 MARS。</span><span class="sxs-lookup"><span data-stu-id="9311a-114">The following example demonstrates how to connect to an instance of SQL Server and how to specify that MARS should be enabled.</span></span>  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=True"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
 <span data-ttu-id="9311a-115">您可以藉由將 "MultipleActiveResultSets=False" 關鍵字組新增至連接字串來停用 MARS。</span><span class="sxs-lookup"><span data-stu-id="9311a-115">You can disable MARS by adding the "MultipleActiveResultSets=False" keyword pair to your connection string.</span></span> <span data-ttu-id="9311a-116">"False" 是停用 MARS 的唯一有效值。</span><span class="sxs-lookup"><span data-stu-id="9311a-116">"False" is the only valid value for disabling MARS.</span></span> <span data-ttu-id="9311a-117">下列連接字串示範如何停用 MARS。</span><span class="sxs-lookup"><span data-stu-id="9311a-117">The following connection string demonstrates how to disable MARS.</span></span>  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=False"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## <a name="special-considerations-when-using-mars"></a><span data-ttu-id="9311a-118">使用 MARS 時的特殊考量</span><span class="sxs-lookup"><span data-stu-id="9311a-118">Special Considerations When Using MARS</span></span>  
 <span data-ttu-id="9311a-119">一般來說，現有的應用程式應該不需要修改，就能使用已啟用 MARS 的連線。</span><span class="sxs-lookup"><span data-stu-id="9311a-119">In general, existing applications should not need modification to use a MARS-enabled connection.</span></span> <span data-ttu-id="9311a-120">不過，如果您想要在應用程式中使用 MARS 功能，就應該了解下列特殊考量。</span><span class="sxs-lookup"><span data-stu-id="9311a-120">However, if you wish to use MARS features in your applications, you should understand the following special considerations.</span></span>  
  
### <a name="statement-interleaving"></a><span data-ttu-id="9311a-121">陳述式交錯</span><span class="sxs-lookup"><span data-stu-id="9311a-121">Statement Interleaving</span></span>  
 <span data-ttu-id="9311a-122">MARS 作業會在伺服器上同步執行。</span><span class="sxs-lookup"><span data-stu-id="9311a-122">MARS operations execute synchronously on the server.</span></span> <span data-ttu-id="9311a-123">允許 SELECT 和 BULK INSERT 陳述式的陳述式交錯。</span><span class="sxs-lookup"><span data-stu-id="9311a-123">Statement interleaving of SELECT and BULK INSERT statements is allowed.</span></span> <span data-ttu-id="9311a-124">但是，資料操作語言 (DML) 和資料定義語言 (DDL) 陳述式會以不可部分完成的方式執行。</span><span class="sxs-lookup"><span data-stu-id="9311a-124">However, data manipulation language (DML) and data definition language (DDL) statements execute atomically.</span></span> <span data-ttu-id="9311a-125">在執行不可部分完成的批次時，任何嘗試執行的陳述式都會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="9311a-125">Any statements attempting to execute while an atomic batch is executing are blocked.</span></span> <span data-ttu-id="9311a-126">在伺服器上平行執行不是 MARS 功能。</span><span class="sxs-lookup"><span data-stu-id="9311a-126">Parallel execution at the server is not a MARS feature.</span></span>  
  
 <span data-ttu-id="9311a-127">如果在 MARS 連線下提交兩個批次，其中一個包含 SELECT 陳述式，另一個包含 DML 陳述式，則 DML 可以在 SELECT 陳述式執行期間開始執行。</span><span class="sxs-lookup"><span data-stu-id="9311a-127">If two batches are submitted under a MARS connection, one of them containing a SELECT statement, the other containing a DML statement, the DML can begin execution within execution of the SELECT statement.</span></span> <span data-ttu-id="9311a-128">不過，DML 陳述式必須先執行完成，SELECT 陳述式才可取得進展。</span><span class="sxs-lookup"><span data-stu-id="9311a-128">However, the DML statement must run to completion before the SELECT statement can make progress.</span></span> <span data-ttu-id="9311a-129">如果這兩個陳述式都是在相同交易下執行，則讀取作業看不到 DML 陳述式在 SELECT 陳述式開始執行之後所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="9311a-129">If both statements are running under the same transaction, any changes made by a DML statement after the SELECT statement has started execution are not visible to the read operation.</span></span>  
  
 <span data-ttu-id="9311a-130">SELECT 陳述式內的 WAITFOR 陳述式不會在等候時 (也就是在產生第一個資料列之前) 產生交易。</span><span class="sxs-lookup"><span data-stu-id="9311a-130">A WAITFOR statement inside a SELECT statement does not yield the transaction while it is waiting, that is, until the first row is produced.</span></span> <span data-ttu-id="9311a-131">這表示在 WAITFOR 陳述式等候時，無法在相同連線內執行任何其他批次。</span><span class="sxs-lookup"><span data-stu-id="9311a-131">This implies that no other batches can execute within the same connection while a WAITFOR statement is waiting.</span></span>  
  
### <a name="mars-session-cache"></a><span data-ttu-id="9311a-132">MARS 工作階段快取</span><span class="sxs-lookup"><span data-stu-id="9311a-132">MARS Session Cache</span></span>  
 <span data-ttu-id="9311a-133">開啟已啟用 MARS 的連線時，即會建立邏輯工作階段，而這會增加額外負荷。</span><span class="sxs-lookup"><span data-stu-id="9311a-133">When a connection is opened with MARS enabled, a logical session is created, which adds additional overhead.</span></span> <span data-ttu-id="9311a-134">為了將負荷最小化並提高效能，**SqlClient** 會快取連線內的 MARS 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9311a-134">To minimize overhead and enhance performance, **SqlClient** caches the MARS session within a connection.</span></span> <span data-ttu-id="9311a-135">快取最多包含 10 個 MARS 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9311a-135">The cache contains at most 10 MARS sessions.</span></span> <span data-ttu-id="9311a-136">使用者無法調整此值。</span><span class="sxs-lookup"><span data-stu-id="9311a-136">This value is not user adjustable.</span></span> <span data-ttu-id="9311a-137">如果達到工作階段限制，即會建立新的工作階段，而不會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="9311a-137">If the session limit is reached, a new session is created—an error is not generated.</span></span> <span data-ttu-id="9311a-138">其中所含的快取和工作階段都會以每個連線為基礎；它們不會在連線之間共用。</span><span class="sxs-lookup"><span data-stu-id="9311a-138">The cache and sessions contained in it are per-connection; they are not shared across connections.</span></span> <span data-ttu-id="9311a-139">釋放工作階段時，除非已達集區上限，否則會將它傳回給該集區。</span><span class="sxs-lookup"><span data-stu-id="9311a-139">When a session is released, it is returned to the pool unless the pool's upper limit has been reached.</span></span> <span data-ttu-id="9311a-140">如果快取集區已滿，就會關閉工作階段。</span><span class="sxs-lookup"><span data-stu-id="9311a-140">If the cache pool is full, the session is closed.</span></span> <span data-ttu-id="9311a-141">MARS 工作階段不會過期。</span><span class="sxs-lookup"><span data-stu-id="9311a-141">MARS sessions do not expire.</span></span> <span data-ttu-id="9311a-142">只有在處置連線物件時，才會清除它們。</span><span class="sxs-lookup"><span data-stu-id="9311a-142">They are only cleaned up when the connection object is disposed.</span></span> <span data-ttu-id="9311a-143">MARS 工作階段快取並未預先載入。</span><span class="sxs-lookup"><span data-stu-id="9311a-143">The MARS session cache is not preloaded.</span></span> <span data-ttu-id="9311a-144">它會因為應用程式需要更多工作階段而載入。</span><span class="sxs-lookup"><span data-stu-id="9311a-144">It is loaded as the application requires more sessions.</span></span>  
  
### <a name="thread-safety"></a><span data-ttu-id="9311a-145">執行緒安全性</span><span class="sxs-lookup"><span data-stu-id="9311a-145">Thread Safety</span></span>  
 <span data-ttu-id="9311a-146">MARS 作業不是安全執行緒。</span><span class="sxs-lookup"><span data-stu-id="9311a-146">MARS operations are not thread-safe.</span></span>  
  
### <a name="connection-pooling"></a><span data-ttu-id="9311a-147">連接共用</span><span class="sxs-lookup"><span data-stu-id="9311a-147">Connection Pooling</span></span>  
 <span data-ttu-id="9311a-148">已啟用 MARS 的連線就像任何其他連線一樣都是集區式的。</span><span class="sxs-lookup"><span data-stu-id="9311a-148">MARS-enabled connections are pooled like any other connection.</span></span> <span data-ttu-id="9311a-149">如果應用程式開啟兩個連線，一個已啟用 MARS，另一個已停用 MARS，則這兩個連線會位於不同的集區。</span><span class="sxs-lookup"><span data-stu-id="9311a-149">If an application opens two connections, one with MARS enabled and one with MARS disabled, the two connections are in separate pools.</span></span> <span data-ttu-id="9311a-150">如需詳細資訊，請參閱 [SQL Server 連線共用 (ADO.NET)](../sql-server-connection-pooling.md) \(機器翻譯\)。</span><span class="sxs-lookup"><span data-stu-id="9311a-150">For more information, see [SQL Server Connection Pooling (ADO.NET)](../sql-server-connection-pooling.md).</span></span>  
  
### <a name="sql-server-batch-execution-environment"></a><span data-ttu-id="9311a-151">SQL Server 批次執行環境</span><span class="sxs-lookup"><span data-stu-id="9311a-151">SQL Server Batch Execution Environment</span></span>  
 <span data-ttu-id="9311a-152">開啟連線時，即會定義預設的環境。</span><span class="sxs-lookup"><span data-stu-id="9311a-152">When a connection is opened, a default environment is defined.</span></span> <span data-ttu-id="9311a-153">接著會將此環境複製到邏輯 MARS 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9311a-153">This environment is then copied into a logical MARS session.</span></span>  
  
 <span data-ttu-id="9311a-154">批次執行環境包括下列元件：</span><span class="sxs-lookup"><span data-stu-id="9311a-154">The batch execution environment includes the following components:</span></span>  
  
- <span data-ttu-id="9311a-155">設定選項 (例如，ANSI_NULLS、DATE_FORMAT、LANGUAGE、TEXTSIZE)</span><span class="sxs-lookup"><span data-stu-id="9311a-155">Set options (for example, ANSI_NULLS, DATE_FORMAT, LANGUAGE, TEXTSIZE)</span></span>  
  
- <span data-ttu-id="9311a-156">資訊安全內容 (使用者/應用程式角色)</span><span class="sxs-lookup"><span data-stu-id="9311a-156">Security context (user/application role)</span></span>  
  
- <span data-ttu-id="9311a-157">資料庫內容 (目前的資料庫)</span><span class="sxs-lookup"><span data-stu-id="9311a-157">Database context (current database)</span></span>  
  
- <span data-ttu-id="9311a-158">執行狀態變數 (例如，@@ERROR、@@ROWCOUNT、@@FETCH_STATUS @@IDENTITY)</span><span class="sxs-lookup"><span data-stu-id="9311a-158">Execution state variables (for example, @@ERROR, @@ROWCOUNT, @@FETCH_STATUS @@IDENTITY)</span></span>  
  
- <span data-ttu-id="9311a-159">最上層暫存資料表</span><span class="sxs-lookup"><span data-stu-id="9311a-159">Top-level temporary tables</span></span>  
  
 <span data-ttu-id="9311a-160">使用 MARS，預設執行環境就會與連線產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9311a-160">With MARS, a default execution environment is associated to a connection.</span></span> <span data-ttu-id="9311a-161">針對指定連線而開始執行的每一個新批次，都會收到預設環境的複本。</span><span class="sxs-lookup"><span data-stu-id="9311a-161">Every new batch that starts executing under a given connection receives a copy of the default environment.</span></span> <span data-ttu-id="9311a-162">每當在指定批次中執行程式碼時，對環境所做的所有變更範圍都會侷限於該特定批次。</span><span class="sxs-lookup"><span data-stu-id="9311a-162">Whenever code is executed under a given batch, all changes made to the environment are scoped to the specific batch.</span></span> <span data-ttu-id="9311a-163">執行完成之後，執行設定就會複製到預設環境中。</span><span class="sxs-lookup"><span data-stu-id="9311a-163">Once execution finishes, the execution settings are copied into the default environment.</span></span> <span data-ttu-id="9311a-164">如果是在相同交易下發出數個要循序執行之命令的單一批次，則語意會與涉及早期用戶端或伺服器之連線所公開的語意相同。</span><span class="sxs-lookup"><span data-stu-id="9311a-164">In the case of a single batch issuing several commands to be executed sequentially under the same transaction, semantics are the same as those exposed by connections involving earlier clients or servers.</span></span>  
  
### <a name="parallel-execution"></a><span data-ttu-id="9311a-165">平行執行</span><span class="sxs-lookup"><span data-stu-id="9311a-165">Parallel Execution</span></span>  
 <span data-ttu-id="9311a-166">MARS 並非設計來移除應用程式中有多個連線的所有需求。</span><span class="sxs-lookup"><span data-stu-id="9311a-166">MARS is not designed to remove all requirements for multiple connections in an application.</span></span> <span data-ttu-id="9311a-167">如果應用程式需要對伺服器進行真正的命令平行執行，就應該使用多個連線。</span><span class="sxs-lookup"><span data-stu-id="9311a-167">If an application needs true parallel execution of commands against a server, multiple connections should be used.</span></span>  
  
 <span data-ttu-id="9311a-168">例如，請設想下列情況。</span><span class="sxs-lookup"><span data-stu-id="9311a-168">For example, consider the following scenario.</span></span> <span data-ttu-id="9311a-169">已建立兩個命令物件，一個用於處理結果集，另一個則用於更新資料；它們會透過 MARS 共用一般連線。</span><span class="sxs-lookup"><span data-stu-id="9311a-169">Two command objects are created, one for processing a result set and another for updating data; they share a common connection via MARS.</span></span> <span data-ttu-id="9311a-170">在此案例中，`Transaction`.`Commit`</span><span class="sxs-lookup"><span data-stu-id="9311a-170">In this scenario, the `Transaction`.`Commit`</span></span> <span data-ttu-id="9311a-171">會無法更新，直到第一個命令物件上的全部結果均讀取完畢，並產生下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="9311a-171">fails on the update until all the results have been read on the first command object, yielding the following exception:</span></span>  
  
 <span data-ttu-id="9311a-172">訊息：交易內容正由另一個工作階段所使用。</span><span class="sxs-lookup"><span data-stu-id="9311a-172">Message: Transaction context in use by another session.</span></span>  
  
 <span data-ttu-id="9311a-173">來源： .NET SqlClient Data Provider</span><span class="sxs-lookup"><span data-stu-id="9311a-173">Source: .NET SqlClient Data Provider</span></span>  
  
 <span data-ttu-id="9311a-174">預期：(Null)</span><span class="sxs-lookup"><span data-stu-id="9311a-174">Expected: (null)</span></span>  
  
 <span data-ttu-id="9311a-175">已接收：System.Data.SqlClient.SqlException</span><span class="sxs-lookup"><span data-stu-id="9311a-175">Received: System.Data.SqlClient.SqlException</span></span>  
  
 <span data-ttu-id="9311a-176">有三個選項可用來處理此案例：</span><span class="sxs-lookup"><span data-stu-id="9311a-176">There are three options for handling this scenario:</span></span>  
  
1. <span data-ttu-id="9311a-177">建立讀取器之後啟動交易，因此它不屬於交易的一部分。</span><span class="sxs-lookup"><span data-stu-id="9311a-177">Start the transaction after the reader is created, so that it is not part of the transaction.</span></span> <span data-ttu-id="9311a-178">接著，每個更新都會變成它自己的交易。</span><span class="sxs-lookup"><span data-stu-id="9311a-178">Every update then becomes its own transaction.</span></span>  
  
2. <span data-ttu-id="9311a-179">在讀取器關閉後認可所有工作。</span><span class="sxs-lookup"><span data-stu-id="9311a-179">Commit all work after the reader is closed.</span></span> <span data-ttu-id="9311a-180">這可能會有大量的更新批次。</span><span class="sxs-lookup"><span data-stu-id="9311a-180">This has the potential for a substantial batch of updates.</span></span>  
  
3. <span data-ttu-id="9311a-181">不要使用 MARS，而是針對每個命令物件改為使用個別連線，就像您在 MARS 之前所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="9311a-181">Don't use MARS; instead use a separate connection for each command object as you would have before MARS.</span></span>  
  
### <a name="detecting-mars-support"></a><span data-ttu-id="9311a-182">偵測 MARS 支援</span><span class="sxs-lookup"><span data-stu-id="9311a-182">Detecting MARS Support</span></span>  
 <span data-ttu-id="9311a-183">應用程式可以藉由讀取 `SqlConnection.ServerVersion` 值來檢查 MARS 支援。</span><span class="sxs-lookup"><span data-stu-id="9311a-183">An application can check for MARS support by reading the `SqlConnection.ServerVersion` value.</span></span> <span data-ttu-id="9311a-184">SQL Server 2005 的主要版本號碼應為 9，而 SQL Server 2008 的則為 10。</span><span class="sxs-lookup"><span data-stu-id="9311a-184">The major number should be 9 for SQL Server 2005 and 10 for SQL Server 2008.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="9311a-185">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9311a-185">See also</span></span>

- [<span data-ttu-id="9311a-186">Multiple Active Result Set (MARS)</span><span class="sxs-lookup"><span data-stu-id="9311a-186">Multiple Active Result Sets (MARS)</span></span>](multiple-active-result-sets-mars.md)
- <span data-ttu-id="9311a-187">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="9311a-187">[ADO.NET Overview](../ado-net-overview.md)</span></span>
