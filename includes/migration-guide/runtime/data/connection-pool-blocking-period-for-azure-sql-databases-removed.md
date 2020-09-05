---
ms.openlocfilehash: c27c63e5bbd4a144b9482a0b1cb74250ae78d91c
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497129"
---
### <a name="connection-pool-blocking-period-for-azure-sql-databases-is-removed"></a><span data-ttu-id="69684-101">Azure SQL 資料庫的連線集區封鎖期已移除</span><span class="sxs-lookup"><span data-stu-id="69684-101">Connection pool blocking period for Azure SQL databases is removed</span></span>

#### <a name="details"></a><span data-ttu-id="69684-102">詳細資料</span><span class="sxs-lookup"><span data-stu-id="69684-102">Details</span></span>

<span data-ttu-id="69684-103">從 .NET Framework 4.6.2 開始，針對已知 Azure SQL 資料庫的連線開啟要求 (\* . database.windows.net、 \* database.chinacloudapi.cn、 \* database.usgovcloudapi.net、 \* database.cloudapi.de) 、已移除連接集區封鎖期間，且未快取連接開啟的錯誤。</span><span class="sxs-lookup"><span data-stu-id="69684-103">Starting with the .NET Framework 4.6.2, for connection open requests to known Azure SQL databases (\*.database.windows.net, \*.database.chinacloudapi.cn, \*.database.usgovcloudapi.net, \*.database.cloudapi.de), the connection pool blocking period is removed, and connection open errors are not cached.</span></span> <span data-ttu-id="69684-104">發生暫時性連線錯誤之後，幾乎會立即嘗試重試連線開啟要求。</span><span class="sxs-lookup"><span data-stu-id="69684-104">Attempts to retry connection open requests will occur almost immediately after transient connection errors.</span></span> <span data-ttu-id="69684-105">這項變更允許立即重試 Azure SQL Database 的連線開啟嘗試，因而提升啟用雲端功能的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="69684-105">This change allows the connection open attempt to be retried immediately for Azure SQL databases, thereby improving the performance of cloud- enabled apps.</span></span> <span data-ttu-id="69684-106">至於所有其他連線嘗試，則會繼續強制執行連線集區封鎖期。</span><span class="sxs-lookup"><span data-stu-id="69684-106">For all other connection attempts, the connection pool blocking period continues to be enforced.</span></span><p/><span data-ttu-id="69684-107">在 .NET Framework 4.6.1 和舊版中，如果應用程式在連線到資料庫時發生暫時性連線失敗，由於連線集區會快取此錯誤並在 5 秒鐘到 1 分鐘後重新擲回，因此無法很快就重試連線。</span><span class="sxs-lookup"><span data-stu-id="69684-107">In the .NET Framework 4.6.1 and earlier versions, when an app encounters a transient connection failure when connecting to a database, the connection attempt cannot be retried quickly, because the connection pool caches the error and re-throws it for 5 seconds to 1 minute.</span></span> <span data-ttu-id="69684-108">如需詳細資訊，請參閱 [SQL Server 連線共用 (ADO.NET)](~/docs/framework/data/adonet/sql-server-connection-pooling.md) \(機器翻譯\)。</span><span class="sxs-lookup"><span data-stu-id="69684-108">For more information, see [SQL Server Connection Pooling (ADO.NET)](~/docs/framework/data/adonet/sql-server-connection-pooling.md).</span></span> <span data-ttu-id="69684-109">此行為會對 Azure SQL Database 連線造成問題，連線通常會因暫時性錯誤而失敗，而且一般會在幾秒內復原。</span><span class="sxs-lookup"><span data-stu-id="69684-109">This behavior is problematic for connections to Azure SQL databases, which often fail with transient errors that are typically recovered from within a few seconds.</span></span> <span data-ttu-id="69684-110">連線集區封鎖功能表示應用程式有很長的一段時間無法連線到資料庫，即使資料庫可供使用且應用程式需要在幾秒內呈現也一樣。</span><span class="sxs-lookup"><span data-stu-id="69684-110">The connection pool blocking feature means that the app cannot connect to the database for an extensive period, even though the database is available and the app needs to render within a few seconds.</span></span>

#### <a name="suggestion"></a><span data-ttu-id="69684-111">建議</span><span class="sxs-lookup"><span data-stu-id="69684-111">Suggestion</span></span>

<span data-ttu-id="69684-112">如果不需要這種行為，可以藉由設定 .NET Framework 4.6.2 中引進的 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=fullName> 屬性來設定連線集區封鎖期。</span><span class="sxs-lookup"><span data-stu-id="69684-112">If this behavior is undesirable, the connection pool blocking period can be configured by setting the <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=fullName> property introduced in the .NET Framework 4.6.2.</span></span> <span data-ttu-id="69684-113">屬性的值是 <xref:System.Data.SqlClient.PoolBlockingPeriod?displayProperty=fullName> 列舉的成員，可以採用三個值的其中一個值︰</span><span class="sxs-lookup"><span data-stu-id="69684-113">The value of the property is a member of the <xref:System.Data.SqlClient.PoolBlockingPeriod?displayProperty=fullName> enumeration that can take either of three values:</span></span><ul><li><xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock></li><li><xref:System.Data.SqlClient.PoolBlockingPeriod.Auto></li><li><xref:System.Data.SqlClient.PoolBlockingPeriod.NeverBlock></li></ul><span data-ttu-id="69684-114">將 <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=fullName> 屬性設為 <xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock> 可以還原舊有行為。</span><span class="sxs-lookup"><span data-stu-id="69684-114">The previous behavior can be restored by setting the <xref:System.Data.SqlClient.SqlConnectionStringBuilder.PoolBlockingPeriod?displayProperty=fullName> property to <xref:System.Data.SqlClient.PoolBlockingPeriod.AlwaysBlock>.</span></span>

| <span data-ttu-id="69684-115">名稱</span><span class="sxs-lookup"><span data-stu-id="69684-115">Name</span></span>    | <span data-ttu-id="69684-116">值</span><span class="sxs-lookup"><span data-stu-id="69684-116">Value</span></span>       |
|:--------|:------------|
| <span data-ttu-id="69684-117">範圍</span><span class="sxs-lookup"><span data-stu-id="69684-117">Scope</span></span>   |<span data-ttu-id="69684-118">Minor</span><span class="sxs-lookup"><span data-stu-id="69684-118">Minor</span></span>|
|<span data-ttu-id="69684-119">版本</span><span class="sxs-lookup"><span data-stu-id="69684-119">Version</span></span>|<span data-ttu-id="69684-120">4.6.2</span><span class="sxs-lookup"><span data-stu-id="69684-120">4.6.2</span></span>|
|<span data-ttu-id="69684-121">類型</span><span class="sxs-lookup"><span data-stu-id="69684-121">Type</span></span>|<span data-ttu-id="69684-122">執行階段</span><span class="sxs-lookup"><span data-stu-id="69684-122">Runtime</span></span>|

#### <a name="affected-apis"></a><span data-ttu-id="69684-123">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="69684-123">Affected APIs</span></span>

- <xref:System.Data.Common.DbConnection.OpenAsync?displayProperty=nameWithType>
- <xref:System.Data.SqlClient.SqlConnection.Open?displayProperty=nameWithType>
- <xref:System.Data.SqlClient.SqlConnection.OpenAsync(System.Threading.CancellationToken)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Data.Common.DbConnection.OpenAsync`
- `M:System.Data.SqlClient.SqlConnection.Open`
- `M:System.Data.SqlClient.SqlConnection.OpenAsync(System.Threading.CancellationToken)`

-->
