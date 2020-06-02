---
title: DataAdapter 和 DataReader
description: 瞭解 ADO.NET DataReader，這會從資料庫抓取資料，而 DataAdapter 則會從資料來源抓取資料並填入資料集。
ms.date: 03/30/2017
ms.assetid: cc952ca2-ec19-46ab-9189-15174b52cb74
ms.openlocfilehash: 17463d65266baa53521bed9603c8abd96923277b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286969"
---
# <a name="dataadapters-and-datareaders"></a><span data-ttu-id="27c37-103">DataAdapter 和 DataReader</span><span class="sxs-lookup"><span data-stu-id="27c37-103">DataAdapters and DataReaders</span></span>
<span data-ttu-id="27c37-104">您可以使用 ADO.NET **DataReader** ，從資料庫中取出唯讀、順向資料流程的資料。</span><span class="sxs-lookup"><span data-stu-id="27c37-104">You can use the ADO.NET **DataReader** to retrieve a read-only, forward-only stream of data from a database.</span></span> <span data-ttu-id="27c37-105">執行查詢時會傳回結果，並將其儲存在用戶端上的網路緩衝區中，直到您使用**DataReader**的**Read**方法要求它們為止。</span><span class="sxs-lookup"><span data-stu-id="27c37-105">Results are returned as the query executes, and are stored in the network buffer on the client until you request them using the **Read** method of the **DataReader**.</span></span> <span data-ttu-id="27c37-106">使用**DataReader**可提高應用程式效能，方法是在資料可用時立即抓取它，而且（預設）在記憶體中一次只儲存一個資料列，以降低系統負荷。</span><span class="sxs-lookup"><span data-stu-id="27c37-106">Using the **DataReader** can increase application performance both by retrieving data as soon as it is available, and (by default) storing only one row at a time in memory, reducing system overhead.</span></span>  
  
 <span data-ttu-id="27c37-107"><xref:System.Data.Common.DataAdapter> 可用於從資料來源擷取資料，並填入 <xref:System.Data.DataSet> 內的資料表。</span><span class="sxs-lookup"><span data-stu-id="27c37-107">A <xref:System.Data.Common.DataAdapter> is used to retrieve data from a data source and populate tables within a <xref:System.Data.DataSet>.</span></span> <span data-ttu-id="27c37-108">`DataAdapter` 亦可將對 `DataSet` 所做的變更解析回資料來源。</span><span class="sxs-lookup"><span data-stu-id="27c37-108">The `DataAdapter` also resolves changes made to the `DataSet` back to the data source.</span></span> <span data-ttu-id="27c37-109">`DataAdapter` 會使用 .NET Framework 資料提供者的 `Connection` 物件連接到資料來源，並使用 `Command` 物件從資料來源擷取資料，以及將變更解析回資料來源。</span><span class="sxs-lookup"><span data-stu-id="27c37-109">The `DataAdapter` uses the `Connection` object of the .NET Framework data provider to connect to a data source, and it uses `Command` objects to retrieve data from and resolve changes to the data source.</span></span>  
  
 <span data-ttu-id="27c37-110">內含在 .NET Framework 中的每個 .NET Framework 資料提供者都有 <xref:System.Data.Common.DbDataReader> 和 <xref:System.Data.Common.DbDataAdapter> 物件：.NET Framework Data Provider for OLE DB 包含 <xref:System.Data.OleDb.OleDbDataReader> 和 <xref:System.Data.OleDb.OleDbDataAdapter> 物件、.NET Framework Data Provider for SQL Server 包含 <xref:System.Data.SqlClient.SqlDataReader> 和 <xref:System.Data.SqlClient.SqlDataAdapter> 物件、.NET Framework Data Provider for ODBC 包含 <xref:System.Data.Odbc.OdbcDataReader> 和 <xref:System.Data.Odbc.OdbcDataAdapter> 物件，而且 .NET Framework Data Provider for Oracle 包含 <xref:System.Data.OracleClient.OracleDataReader> 和 <xref:System.Data.OracleClient.OracleDataAdapter> 物件。</span><span class="sxs-lookup"><span data-stu-id="27c37-110">Each .NET Framework data provider included with the .NET Framework has a <xref:System.Data.Common.DbDataReader> and a <xref:System.Data.Common.DbDataAdapter> object: the .NET Framework Data Provider for OLE DB includes an <xref:System.Data.OleDb.OleDbDataReader> and an <xref:System.Data.OleDb.OleDbDataAdapter> object, the .NET Framework Data Provider for SQL Server includes a <xref:System.Data.SqlClient.SqlDataReader> and a <xref:System.Data.SqlClient.SqlDataAdapter> object, the .NET Framework Data Provider for ODBC includes an <xref:System.Data.Odbc.OdbcDataReader> and an <xref:System.Data.Odbc.OdbcDataAdapter> object, and the .NET Framework Data Provider for Oracle includes an <xref:System.Data.OracleClient.OracleDataReader> and an <xref:System.Data.OracleClient.OracleDataAdapter> object.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="27c37-111">本節內容</span><span class="sxs-lookup"><span data-stu-id="27c37-111">In This Section</span></span>  
 [<span data-ttu-id="27c37-112">使用 DataReader 擷取資料</span><span class="sxs-lookup"><span data-stu-id="27c37-112">Retrieving Data Using a DataReader</span></span>](retrieving-data-using-a-datareader.md)  
 <span data-ttu-id="27c37-113">描述 ADO.NET **DataReader**物件，以及如何使用它從資料來源傳回結果的資料流程。</span><span class="sxs-lookup"><span data-stu-id="27c37-113">Describes the ADO.NET **DataReader** object and how to use it to return a stream of results from a data source.</span></span>  
  
 [<span data-ttu-id="27c37-114">從 DataAdapter 填入資料集</span><span class="sxs-lookup"><span data-stu-id="27c37-114">Populating a DataSet from a DataAdapter</span></span>](populating-a-dataset-from-a-dataadapter.md)  
 <span data-ttu-id="27c37-115">說明如何使用 `DataSet` 來以資料表、資料行及資料列填入 `DataAdapter`。</span><span class="sxs-lookup"><span data-stu-id="27c37-115">Describes how to fill a `DataSet` with tables, columns, and rows by using a `DataAdapter`.</span></span>  
  
 [<span data-ttu-id="27c37-116">DataAdapter 的參數</span><span class="sxs-lookup"><span data-stu-id="27c37-116">DataAdapter Parameters</span></span>](dataadapter-parameters.md)  
 <span data-ttu-id="27c37-117">說明如何搭配使用參數與 `DataAdapter` 的命令屬性，包括如何將 `DataSet` 中資料行的內容對應至命令參數。</span><span class="sxs-lookup"><span data-stu-id="27c37-117">Describes how to use parameters with the command properties of a `DataAdapter` including how to map the contents of a column in a `DataSet` to a command parameter.</span></span>  
  
 [<span data-ttu-id="27c37-118">將現有條件約束加入至資料集</span><span class="sxs-lookup"><span data-stu-id="27c37-118">Adding Existing Constraints to a DataSet</span></span>](adding-existing-constraints-to-a-dataset.md)  
 <span data-ttu-id="27c37-119">說明如何將現有條件約束加入 `DataSet`。</span><span class="sxs-lookup"><span data-stu-id="27c37-119">Describes how to add existing constraints to a `DataSet`.</span></span>  
  
 [<span data-ttu-id="27c37-120">DataAdapter DataTable 和 DataColumn 對應</span><span class="sxs-lookup"><span data-stu-id="27c37-120">DataAdapter DataTable and DataColumn Mappings</span></span>](dataadapter-datatable-and-datacolumn-mappings.md)  
 <span data-ttu-id="27c37-121">說明如何設定 `DataTableMappings` 的 `ColumnMappings` 和 `DataAdapter`。</span><span class="sxs-lookup"><span data-stu-id="27c37-121">Describes how to set up `DataTableMappings` and `ColumnMappings` for a `DataAdapter`.</span></span>  
  
 [<span data-ttu-id="27c37-122">逐頁查看查詢結果</span><span class="sxs-lookup"><span data-stu-id="27c37-122">Paging Through a Query Result</span></span>](paging-through-a-query-result.md)  
 <span data-ttu-id="27c37-123">提供以資料分頁形式檢視查詢結果的範例。</span><span class="sxs-lookup"><span data-stu-id="27c37-123">Provides an example of viewing the results of a query as pages of data.</span></span>  
  
 [<span data-ttu-id="27c37-124">使用 DataAdapter 更新資料來源</span><span class="sxs-lookup"><span data-stu-id="27c37-124">Updating Data Sources with DataAdapters</span></span>](updating-data-sources-with-dataadapters.md)  
 <span data-ttu-id="27c37-125">說明如何使用 `DataAdapter`，將 `DataSet` 中的變更解析回資料庫。</span><span class="sxs-lookup"><span data-stu-id="27c37-125">Describes how to use a `DataAdapter` to resolve changes in a `DataSet` back to the database.</span></span>  
  
 [<span data-ttu-id="27c37-126">處理 DataAdapter 的事件</span><span class="sxs-lookup"><span data-stu-id="27c37-126">Handling DataAdapter Events</span></span>](handling-dataadapter-events.md)  
 <span data-ttu-id="27c37-127">說明 `DataAdapter` 事件以及如何使用它們。</span><span class="sxs-lookup"><span data-stu-id="27c37-127">Describes `DataAdapter` events and how to use them.</span></span>  
  
 [<span data-ttu-id="27c37-128">使用 DataAdapter 執行批次作業</span><span class="sxs-lookup"><span data-stu-id="27c37-128">Performing Batch Operations Using DataAdapters</span></span>](performing-batch-operations-using-dataadapters.md)  
 <span data-ttu-id="27c37-129">說明在套用來自 `DataSet` 的更新時，如何藉由減少與 SQL Server 之間的往返次數，提高應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="27c37-129">Describes enhancing application performance by reducing the number of round trips to SQL Server when applying updates from the `DataSet`.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="27c37-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="27c37-130">See also</span></span>

- [<span data-ttu-id="27c37-131">連接到資料來源</span><span class="sxs-lookup"><span data-stu-id="27c37-131">Connecting to a Data Source</span></span>](connecting-to-a-data-source.md)
- [<span data-ttu-id="27c37-132">命令和參數</span><span class="sxs-lookup"><span data-stu-id="27c37-132">Commands and Parameters</span></span>](commands-and-parameters.md)
- [<span data-ttu-id="27c37-133">異動和並行存取</span><span class="sxs-lookup"><span data-stu-id="27c37-133">Transactions and Concurrency</span></span>](transactions-and-concurrency.md)
- [<span data-ttu-id="27c37-134">DataSet、DataTable 和 DataView</span><span class="sxs-lookup"><span data-stu-id="27c37-134">DataSets, DataTables, and DataViews</span></span>](./dataset-datatable-dataview/index.md)
- <span data-ttu-id="27c37-135">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="27c37-135">[ADO.NET Overview](ado-net-overview.md)</span></span>
