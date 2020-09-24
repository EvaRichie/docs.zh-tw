---
title: 啟用查詢通知
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a5333e19-8e55-4aa9-82dc-ca8745e516ed
ms.openlocfilehash: 4e9b3a2e1f176a9d01e983bc469cc4032fa5d730
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156169"
---
# <a name="enabling-query-notifications"></a><span data-ttu-id="37786-102">啟用查詢通知</span><span class="sxs-lookup"><span data-stu-id="37786-102">Enabling Query Notifications</span></span>

<span data-ttu-id="37786-103">取用查詢通知的應用程式有一組常見需求。</span><span class="sxs-lookup"><span data-stu-id="37786-103">Applications that consume query notifications have a common set of requirements.</span></span> <span data-ttu-id="37786-104">您必須正確設定資料來源才能支援 SQL 查詢通知，而且使用者必須具有正確的用戶端及伺服器端權限。</span><span class="sxs-lookup"><span data-stu-id="37786-104">Your data source must be correctly configured to support SQL query notifications, and the user must have the correct client-side and server-side permissions.</span></span>  
  
 <span data-ttu-id="37786-105">若要使用查詢通知，您必須：</span><span class="sxs-lookup"><span data-stu-id="37786-105">To use query notifications you must:</span></span>  
  
- <span data-ttu-id="37786-106">啟用資料庫的查詢通知。</span><span class="sxs-lookup"><span data-stu-id="37786-106">Enable query notifications for your database.</span></span>  
  
- <span data-ttu-id="37786-107">確定用來連線到資料庫的使用者識別碼具備必要權限。</span><span class="sxs-lookup"><span data-stu-id="37786-107">Ensure that the user ID used to connect to the database has the necessary permissions.</span></span>  
  
- <span data-ttu-id="37786-108">使用 <xref:System.Data.SqlClient.SqlCommand> 物件搭配關聯的通知物件 (<xref:System.Data.SqlClient.SqlDependency> 或 <xref:System.Data.Sql.SqlNotificationRequest>) 執行有效 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="37786-108">Use a <xref:System.Data.SqlClient.SqlCommand> object to execute a valid SELECT statement with an associated notification object—either <xref:System.Data.SqlClient.SqlDependency> or <xref:System.Data.Sql.SqlNotificationRequest>.</span></span>  
  
- <span data-ttu-id="37786-109">提供程式碼來處理受監視的資料發生變更時要發出的通知。</span><span class="sxs-lookup"><span data-stu-id="37786-109">Provide code to process the notification if the data being monitored changes.</span></span>  
  
## <a name="query-notifications-requirements"></a><span data-ttu-id="37786-110">查詢通知需求</span><span class="sxs-lookup"><span data-stu-id="37786-110">Query Notifications Requirements</span></span>  

 <span data-ttu-id="37786-111">只有符合一組特定需求的 SELECT 陳述式才支援查詢通知。</span><span class="sxs-lookup"><span data-stu-id="37786-111">Query notifications are supported only for SELECT statements that meet a list of specific requirements.</span></span> <span data-ttu-id="37786-112">下表提供 SQL Server 線上叢書中 Service Broker 與查詢通知文件的連結。</span><span class="sxs-lookup"><span data-stu-id="37786-112">The following table provides links to the Service Broker and Query Notifications documentation in SQL Server Books Online.</span></span>  
  
 <span data-ttu-id="37786-113">**SQL Server 文件**</span><span class="sxs-lookup"><span data-stu-id="37786-113">**SQL Server documentation**</span></span>  
  
- <span data-ttu-id="37786-114">[為通知建立查詢](/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="37786-114">[Creating a Query for Notification](/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))</span></span>  
  
- <span data-ttu-id="37786-115">[Service Broker 的安全性考量](/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))</span><span class="sxs-lookup"><span data-stu-id="37786-115">[Security Considerations for Service Broker](/previous-versions/sql/sql-server-2005/ms166059(v=sql.90))</span></span>  
  
- <span data-ttu-id="37786-116">[安全性與保護 (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="37786-116">[Security and Protection (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522911(v=sql.105))</span></span>  
  
- <span data-ttu-id="37786-117">[Notification Services 的安全性考量](/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))</span><span class="sxs-lookup"><span data-stu-id="37786-117">[Security Considerations for Notifications Services](/previous-versions/sql/sql-server-2005/ms172604(v=sql.90))</span></span>  
  
- <span data-ttu-id="37786-118">[查詢通知權限](/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="37786-118">[Query Notification Permissions](/previous-versions/sql/sql-server-2008-r2/ms188311(v=sql.105))</span></span>  
  
- <span data-ttu-id="37786-119">[Service Broker 的國際性考量](/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))</span><span class="sxs-lookup"><span data-stu-id="37786-119">[International Considerations for Service Broker](/previous-versions/sql/sql-server-2005/ms166028(v=sql.90))</span></span>  
  
- <span data-ttu-id="37786-120">[解決方案設計考量 (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="37786-120">[Solution Design Considerations (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522899(v=sql.105))</span></span>  
  
- <span data-ttu-id="37786-121">[Service Broker 開發人員資訊中心](/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="37786-121">[Service Broker Developer InfoCenter](/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))</span></span>  
  
- <span data-ttu-id="37786-122">[開發人員手冊 (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))</span><span class="sxs-lookup"><span data-stu-id="37786-122">[Developer's Guide (Service Broker)](/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))</span></span>  
  
## <a name="enabling-query-notifications-to-run-sample-code"></a><span data-ttu-id="37786-123">啟用查詢通知來執行範例程式碼</span><span class="sxs-lookup"><span data-stu-id="37786-123">Enabling Query Notifications to Run Sample Code</span></span>  

 <span data-ttu-id="37786-124">若要透過使用 SQL Server Management Studio，在 **AdventureWorks** 資料庫上啟用 Service Broker，請執行下列 Transact-SQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="37786-124">To enable Service Broker on the **AdventureWorks** database by using SQL Server Management Studio, execute the following Transact-SQL statement:</span></span>  
  
 `ALTER DATABASE AdventureWorks SET ENABLE_BROKER;`  
  
 <span data-ttu-id="37786-125">為了讓查詢通知範例正確執行，必須在資料庫伺服器上執行下列 Transact-SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="37786-125">For the query notification samples to run correctly, the following Transact-SQL statements must be executed on the database server.</span></span>  
  
```sql
CREATE QUEUE ContactChangeMessages;  
  
CREATE SERVICE ContactChangeNotifications  
  ON QUEUE ContactChangeMessages  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification]);  
```  
  
## <a name="query-notifications-permissions"></a><span data-ttu-id="37786-126">查詢通知使用權限</span><span class="sxs-lookup"><span data-stu-id="37786-126">Query Notifications Permissions</span></span>  

 <span data-ttu-id="37786-127">若使用者執行的命令會要求通知，則必須有伺服器上的訂閱查詢通知資料庫權限。</span><span class="sxs-lookup"><span data-stu-id="37786-127">Users who execute commands requesting notification must have SUBSCRIBE QUERY NOTIFICATIONS database permission on the server.</span></span>  
  
 <span data-ttu-id="37786-128">在部分信任狀況下執行的用戶端程式碼需要 <xref:System.Data.SqlClient.SqlClientPermission>。</span><span class="sxs-lookup"><span data-stu-id="37786-128">Client-side code that runs in a partial trust situation requires the <xref:System.Data.SqlClient.SqlClientPermission>.</span></span>  
  
 <span data-ttu-id="37786-129">下列程式碼會建立將 <xref:System.Security.Permissions.PermissionState> 設定為 <xref:System.Security.Permissions.PermissionState.Unrestricted> 的 <xref:System.Data.SqlClient.SqlClientPermission> 物件。</span><span class="sxs-lookup"><span data-stu-id="37786-129">The following code creates a <xref:System.Data.SqlClient.SqlClientPermission> object, setting the <xref:System.Security.Permissions.PermissionState> to <xref:System.Security.Permissions.PermissionState.Unrestricted>.</span></span> <span data-ttu-id="37786-130">如果在呼叫堆疊中較高的所有呼叫者都尚未獲授與權限，<xref:System.Security.CodeAccessPermission.Demand%2A> 將會在執行階段強制執行 <xref:System.Security.SecurityException>。</span><span class="sxs-lookup"><span data-stu-id="37786-130">The <xref:System.Security.CodeAccessPermission.Demand%2A> will force a <xref:System.Security.SecurityException> at run time if all callers higher in the call stack have not been granted the permission.</span></span>  
  
 [!code-csharp[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/CS/source.cs#1)]
 [!code-vb[DataWorks SqlNotification.Perms#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlNotification.Perms/VB/source.vb#1)]  
  
## <a name="choosing-a-notification-object"></a><span data-ttu-id="37786-131">選擇通知物件</span><span class="sxs-lookup"><span data-stu-id="37786-131">Choosing a Notification Object</span></span>  

 <span data-ttu-id="37786-132">查詢通知 API 提供兩個物件來處理通知：<xref:System.Data.SqlClient.SqlDependency> 和 <xref:System.Data.Sql.SqlNotificationRequest>。</span><span class="sxs-lookup"><span data-stu-id="37786-132">The query notifications API provides two objects to process notifications: <xref:System.Data.SqlClient.SqlDependency> and <xref:System.Data.Sql.SqlNotificationRequest>.</span></span> <span data-ttu-id="37786-133">一般而言，大多數非 ASP.NET 應用程式應使用 <xref:System.Data.SqlClient.SqlDependency> 物件。</span><span class="sxs-lookup"><span data-stu-id="37786-133">In general, most non-ASP.NET applications should use the <xref:System.Data.SqlClient.SqlDependency> object.</span></span> <span data-ttu-id="37786-134">ASP.NET 應用程式應使用較高層級的 <xref:System.Web.Caching.SqlCacheDependency>，其包裝了 <xref:System.Data.SqlClient.SqlDependency>，並提供用於管理通知及快取物件的架構。</span><span class="sxs-lookup"><span data-stu-id="37786-134">ASP.NET applications should use the higher-level <xref:System.Web.Caching.SqlCacheDependency>, which wraps <xref:System.Data.SqlClient.SqlDependency> and provides a framework for administering the notification and cache objects.</span></span>  
  
### <a name="using-sqldependency"></a><span data-ttu-id="37786-135">使用 SqlDependency</span><span class="sxs-lookup"><span data-stu-id="37786-135">Using SqlDependency</span></span>  

 <span data-ttu-id="37786-136">若要使用 <xref:System.Data.SqlClient.SqlDependency>，所使用的 SQL Server 資料庫必須啟用 Service Broker，且使用者必須具有接收通知的使用權限。</span><span class="sxs-lookup"><span data-stu-id="37786-136">To use <xref:System.Data.SqlClient.SqlDependency>, Service Broker must be enabled for the SQL Server database being used, and users must have permissions to receive notifications.</span></span> <span data-ttu-id="37786-137">系統會預先定義 Service Broker 物件，例如通知佇列。</span><span class="sxs-lookup"><span data-stu-id="37786-137">Service Broker objects, such as the notification queue, are predefined.</span></span>  
  
 <span data-ttu-id="37786-138">此外，<xref:System.Data.SqlClient.SqlDependency> 會自動啟動背景工作執行緒，以便在通知張貼到佇列時進行處理；它也會剖析 Service Broker 訊息，將資訊以事件引數資料形式公開。</span><span class="sxs-lookup"><span data-stu-id="37786-138">In addition, <xref:System.Data.SqlClient.SqlDependency> automatically launches a worker thread to process notifications as they are posted to the queue; it also parses the Service Broker message, exposing the information as event argument data.</span></span> <span data-ttu-id="37786-139"><xref:System.Data.SqlClient.SqlDependency> 必須透過呼叫 `Start` 方法來初始化，以建立對資料庫的相依性。</span><span class="sxs-lookup"><span data-stu-id="37786-139"><xref:System.Data.SqlClient.SqlDependency> must be initialized by calling the `Start` method to establish a dependency to the database.</span></span> <span data-ttu-id="37786-140">這是靜態方法，而且只需要在應用程式初始化期間針對每個必要的資料庫連接呼叫一次。</span><span class="sxs-lookup"><span data-stu-id="37786-140">This is a static method that needs to be called only once during application initialization for each database connection required.</span></span> <span data-ttu-id="37786-141">對於每個進行的相依性連線，`Stop` 方法應該在應用程式終止時呼叫。</span><span class="sxs-lookup"><span data-stu-id="37786-141">The `Stop` method should be called at application termination for each dependency connection that was made.</span></span>  
  
### <a name="using-sqlnotificationrequest"></a><span data-ttu-id="37786-142">使用 SqlNotificationRequest</span><span class="sxs-lookup"><span data-stu-id="37786-142">Using SqlNotificationRequest</span></span>  

 <span data-ttu-id="37786-143">相反地，<xref:System.Data.Sql.SqlNotificationRequest> 需要您自行實作整個接聽基礎結構。</span><span class="sxs-lookup"><span data-stu-id="37786-143">In contrast, <xref:System.Data.Sql.SqlNotificationRequest> requires you to implement the entire listening infrastructure yourself.</span></span> <span data-ttu-id="37786-144">此外，必須定義所有支援的 Service Broker 物件，例如佇列、服務與佇列所支援的訊息類型。</span><span class="sxs-lookup"><span data-stu-id="37786-144">In addition, all the supporting Service Broker objects such as the queue, service, and message types supported by the queue must be defined.</span></span> <span data-ttu-id="37786-145">如果您的應用程式需要特殊的通知訊息或通知行為，或如果您的應用程式是較大型 Service Broker 應用程式的一部分，此手動方法就很有用。</span><span class="sxs-lookup"><span data-stu-id="37786-145">This manual approach is useful if your application requires special notification messages or notification behaviors, or if your application is part of a larger Service Broker application.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="37786-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="37786-146">See also</span></span>

- [<span data-ttu-id="37786-147">SQL Server 中的查詢通知</span><span class="sxs-lookup"><span data-stu-id="37786-147">Query Notifications in SQL Server</span></span>](query-notifications-in-sql-server.md)
- <span data-ttu-id="37786-148">[ADO.NET 概觀](../ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="37786-148">[ADO.NET Overview](../ado-net-overview.md)</span></span>
