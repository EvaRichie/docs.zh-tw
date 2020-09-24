---
title: 從 DataAdapter 填入資料集
description: 瞭解如何從 ADO.NET 中的 DataAdapter 填入資料集，以提供與資料來源無關的一致性關聯式程式設計模型。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3fa0ac7d-e266-4954-bfac-3fbe2f913153
ms.openlocfilehash: ac84af884238b166266d4206802878c1e21169fd
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177406"
---
# <a name="populating-a-dataset-from-a-dataadapter"></a><span data-ttu-id="351cc-103">從 DataAdapter 填入資料集</span><span class="sxs-lookup"><span data-stu-id="351cc-103">Populating a DataSet from a DataAdapter</span></span>

<span data-ttu-id="351cc-104">ADO.NET <xref:System.Data.DataSet> 是記憶體常駐的資料表示，可提供與資料來源無關的一致性關聯式程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="351cc-104">The ADO.NET <xref:System.Data.DataSet> is a memory-resident representation of data that provides a consistent relational programming model independent of the data source.</span></span> <span data-ttu-id="351cc-105">`DataSet` 表示一組完整的資料，包括資料表、條件約束和資料表間的關係。</span><span class="sxs-lookup"><span data-stu-id="351cc-105">The `DataSet` represents a complete set of data that includes tables, constraints, and relationships among the tables.</span></span> <span data-ttu-id="351cc-106">因為 `DataSet` 與資料來源無關，所以 `DataSet` 可包含應用程式的本機資料，以及來自多個資料來源的資料。</span><span class="sxs-lookup"><span data-stu-id="351cc-106">Because the `DataSet` is independent of the data source, a `DataSet` can include data local to the application, and data from multiple data sources.</span></span> <span data-ttu-id="351cc-107">而您與現有資料來源的互動則是透過 `DataAdapter`。</span><span class="sxs-lookup"><span data-stu-id="351cc-107">Interaction with existing data sources is controlled through the `DataAdapter`.</span></span>  
  
 <span data-ttu-id="351cc-108">`SelectCommand` 的 `DataAdapter` 屬性為 `Command` 物件，可用於從資料來源擷取資料。</span><span class="sxs-lookup"><span data-stu-id="351cc-108">The `SelectCommand` property of the `DataAdapter` is a `Command` object that retrieves data from the data source.</span></span> <span data-ttu-id="351cc-109">`InsertCommand`的 `UpdateCommand`、 `DeleteCommand` 和 `DataAdapter` 屬性為 `Command` 物件，可根據對 `DataSet`內資料的修改，管理對資料來源內資料的更新作業。</span><span class="sxs-lookup"><span data-stu-id="351cc-109">The `InsertCommand`, `UpdateCommand`, and `DeleteCommand` properties of the `DataAdapter` are `Command` objects that manage updates to the data in the data source according to modifications made to the data in the `DataSet`.</span></span> <span data-ttu-id="351cc-110">這些屬性在 [使用 Dataadapter 更新資料來源](updating-data-sources-with-dataadapters.md)中有更詳細的討論。</span><span class="sxs-lookup"><span data-stu-id="351cc-110">These properties are covered in more detail in [Updating Data Sources with DataAdapters](updating-data-sources-with-dataadapters.md).</span></span>  
  
 <span data-ttu-id="351cc-111">`Fill` 的 `DataAdapter` 方法用於以 `DataSet` 之 `SelectCommand` 的結果填入 `DataAdapter`。</span><span class="sxs-lookup"><span data-stu-id="351cc-111">The `Fill` method of the `DataAdapter` is used to populate a `DataSet` with the results of the `SelectCommand` of the `DataAdapter`.</span></span> <span data-ttu-id="351cc-112">`Fill` 把下列各項當成引數：要填入的 `DataSet` 、 `DataTable` 物件，或是以 `DataTable` 傳回資料列填入的 `SelectCommand`名稱。</span><span class="sxs-lookup"><span data-stu-id="351cc-112">`Fill` takes as its arguments a `DataSet` to be populated, and a `DataTable` object, or the name of the `DataTable` to be filled with the rows returned from the `SelectCommand`.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="351cc-113">使用 `DataAdapter` 擷取所有的資料表要花很多時間，特別是資料表包含許多資料列時。</span><span class="sxs-lookup"><span data-stu-id="351cc-113">Using the `DataAdapter` to retrieve all of a table takes time, especially if there are many rows in the table.</span></span> <span data-ttu-id="351cc-114">這是因為存取資料庫，尋找和處理資料，然後再將資料傳輸至用戶端的過程非常耗時。</span><span class="sxs-lookup"><span data-stu-id="351cc-114">This is because accessing the database, locating and processing the data, and then transferring the data to the client is time-consuming.</span></span> <span data-ttu-id="351cc-115">在將所有資料表提取到用戶端時，所有在伺服器上的資料列都會鎖定。</span><span class="sxs-lookup"><span data-stu-id="351cc-115">Pulling all of the table to the client also locks all of the rows on the server.</span></span> <span data-ttu-id="351cc-116">若要提升效能，您可以使用 `WHERE` 子句大幅減少傳回用戶端的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="351cc-116">To improve performance, you can use the `WHERE` clause to greatly reduce the number of rows returned to the client.</span></span> <span data-ttu-id="351cc-117">您也可以藉由在 `SELECT` 陳述式中明確列出所需的資料行，以減少傳回用戶端的資料數量。</span><span class="sxs-lookup"><span data-stu-id="351cc-117">You can also reduce the amount of data returned to the client by only explicitly listing required columns in the `SELECT` statement.</span></span> <span data-ttu-id="351cc-118">另一個不錯的解決方法就是以批次方式擷取資料列 (例如一次擷取數百個資料列)，同時僅在用戶端完成目前的批次作業後，才擷取下一批次。</span><span class="sxs-lookup"><span data-stu-id="351cc-118">Another good workaround is to retrieve the rows in batches (such as several hundred rows at a time) and only retrieve the next batch when the client is finished with the current batch.</span></span>  
  
 <span data-ttu-id="351cc-119">`Fill` 方法會隱含地使用 `DataReader` 物件傳回用於在 `DataSet`內建立資料表的資料行名稱和型別，以及用於填入 `DataSet`內資料表資料列的資料。</span><span class="sxs-lookup"><span data-stu-id="351cc-119">The `Fill` method uses the `DataReader` object implicitly to return the column names and types that are used to create the tables in the `DataSet`, and the data to populate the rows of the tables in the `DataSet`.</span></span> <span data-ttu-id="351cc-120">資料表和資料行只有在不存在時才會建立；否則 `Fill` 會使用現有的 `DataSet` 結構描述。</span><span class="sxs-lookup"><span data-stu-id="351cc-120">Tables and columns are only created if they do not already exist; otherwise `Fill` uses the existing `DataSet` schema.</span></span> <span data-ttu-id="351cc-121">資料行類型會根據 [ADO.NET 中資料類型](data-type-mappings-in-ado-net.md)對應的資料表，建立成 .NET Framework 類型。</span><span class="sxs-lookup"><span data-stu-id="351cc-121">Column types are created as .NET Framework types according to the tables in [Data Type Mappings in ADO.NET](data-type-mappings-in-ado-net.md).</span></span> <span data-ttu-id="351cc-122">除非主要索引鍵存在於資料來源和中，否則不會建立主鍵 `DataAdapter` **。**`MissingSchemaAction`</span><span class="sxs-lookup"><span data-stu-id="351cc-122">Primary keys are not created unless they exist in the data source and `DataAdapter`**.**`MissingSchemaAction`</span></span> <span data-ttu-id="351cc-123">設定為 `MissingSchemaAction` **。** `AddWithKey`</span><span class="sxs-lookup"><span data-stu-id="351cc-123">is set to `MissingSchemaAction`**.**`AddWithKey`.</span></span> <span data-ttu-id="351cc-124">如果 `Fill` 發現主索引鍵已在資料表中，它就會以資料列 (其主索引鍵的資料行值，符合從資料來源傳回的資料列對應值) 的資料來源資料，覆寫 `DataSet` 中的資料。</span><span class="sxs-lookup"><span data-stu-id="351cc-124">If `Fill` finds that a primary key exists for a table, it will overwrite data in the `DataSet` with data from the data source for rows where the primary key column values match those of the row returned from the data source.</span></span> <span data-ttu-id="351cc-125">如果沒發現主索引鍵，則資料會附加在 `DataSet`的資料表內。</span><span class="sxs-lookup"><span data-stu-id="351cc-125">If no primary key is found, the data is appended to the tables in the `DataSet`.</span></span> <span data-ttu-id="351cc-126">`Fill` 當您填入 `DataSet` (請參閱 [DataAdapter DataTable 和 DataColumn](dataadapter-datatable-and-datacolumn-mappings.md) 對應) 時，會使用可能存在的任何對應。</span><span class="sxs-lookup"><span data-stu-id="351cc-126">`Fill` uses any mappings that may exist when you populate the `DataSet` (see [DataAdapter DataTable and DataColumn Mappings](dataadapter-datatable-and-datacolumn-mappings.md)).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="351cc-127">如果 `SelectCommand` 傳回 OUTER JOIN 的結果，則 `DataAdapter` 便不會為產生的 `PrimaryKey` 設定 `DataTable`值。</span><span class="sxs-lookup"><span data-stu-id="351cc-127">If the `SelectCommand` returns the results of an OUTER JOIN, the `DataAdapter` does not set a `PrimaryKey` value for the resulting `DataTable`.</span></span> <span data-ttu-id="351cc-128">您必須自己定義 `PrimaryKey` ，確保正確解析重複的資料列。</span><span class="sxs-lookup"><span data-stu-id="351cc-128">You must define the `PrimaryKey` yourself to make sure that duplicate rows are resolved correctly.</span></span> <span data-ttu-id="351cc-129">如需詳細資訊，請參閱 [定義主鍵](./dataset-datatable-dataview/defining-primary-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="351cc-129">For more information, see [Defining Primary Keys](./dataset-datatable-dataview/defining-primary-keys.md).</span></span>  
  
 <span data-ttu-id="351cc-130">下列程式碼範例會建立 <xref:System.Data.SqlClient.SqlDataAdapter> 的執行個體，它使用 <xref:System.Data.SqlClient.SqlConnection> 連接至 Microsoft SQL Server `Northwind` 資料庫，並以客戶清單填入 <xref:System.Data.DataTable> 中的 `DataSet` 。</span><span class="sxs-lookup"><span data-stu-id="351cc-130">The following code example creates an instance of a <xref:System.Data.SqlClient.SqlDataAdapter> that uses a <xref:System.Data.SqlClient.SqlConnection> to the Microsoft SQL Server `Northwind` database and populates a <xref:System.Data.DataTable> in a `DataSet` with the list of customers.</span></span> <span data-ttu-id="351cc-131">SQL 陳述式和傳遞給 <xref:System.Data.SqlClient.SqlConnection> 建構函式的 <xref:System.Data.SqlClient.SqlDataAdapter> 引數，可用於建立 <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> 的 <xref:System.Data.SqlClient.SqlDataAdapter>屬性。</span><span class="sxs-lookup"><span data-stu-id="351cc-131">The SQL statement and <xref:System.Data.SqlClient.SqlConnection> arguments passed to the <xref:System.Data.SqlClient.SqlDataAdapter> constructor are used to create the <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> property of the <xref:System.Data.SqlClient.SqlDataAdapter>.</span></span>  
  
## <a name="example"></a><span data-ttu-id="351cc-132">範例</span><span class="sxs-lookup"><span data-stu-id="351cc-132">Example</span></span>  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim queryString As String = _  
  "SELECT CustomerID, CompanyName FROM dbo.Customers"  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  queryString, connection)  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
string queryString =
  "SELECT CustomerID, CompanyName FROM dbo.Customers";  
SqlDataAdapter adapter = new SqlDataAdapter(queryString, connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
> <span data-ttu-id="351cc-133">這個範例所顯示的程式碼並未明確開啟和關閉 `Connection`。</span><span class="sxs-lookup"><span data-stu-id="351cc-133">The code shown in this example does not explicitly open and close the `Connection`.</span></span> <span data-ttu-id="351cc-134">`Fill` 方法若發現連接尚未開啟，會隱含開啟 `Connection` 正在使用的 `DataAdapter` 。</span><span class="sxs-lookup"><span data-stu-id="351cc-134">The `Fill` method implicitly opens the `Connection` that the `DataAdapter` is using if it finds that the connection is not already open.</span></span> <span data-ttu-id="351cc-135">如果 `Fill` 開啟了連接，則當 `Fill` 結束時也會一併關閉連接。</span><span class="sxs-lookup"><span data-stu-id="351cc-135">If `Fill` opened the connection, it also closes the connection when `Fill` is finished.</span></span> <span data-ttu-id="351cc-136">如此便可在處理單一作業時 (例如 `Fill` 或 `Update`)，簡化您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="351cc-136">This can simplify your code when you deal with a single operation such as a `Fill` or an `Update`.</span></span> <span data-ttu-id="351cc-137">但是，如果您要執行需要開啟連接的多項作業，您可明確呼叫 `Open` 的 `Connection`方法，針對資料來源執行作業，然後呼叫 `Close` 的 `Connection`方法，如此即可改善應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="351cc-137">However, if you are performing multiple operations that require an open connection, you can improve the performance of your application by explicitly calling the `Open` method of the `Connection`, performing the operations against the data source, and then calling the `Close` method of the `Connection`.</span></span> <span data-ttu-id="351cc-138">您應該儘量減少與資料來源之間的連接，以釋放資源給其他用戶端應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="351cc-138">You should try to keep connections to the data source open as briefly as possible to free resources for use by other client applications.</span></span>  
  
## <a name="multiple-result-sets"></a><span data-ttu-id="351cc-139">多個結果集</span><span class="sxs-lookup"><span data-stu-id="351cc-139">Multiple Result Sets</span></span>  

 <span data-ttu-id="351cc-140">如果 `DataAdapter` 發現多個結果集，它便會在 `DataSet`內建立多個資料表。</span><span class="sxs-lookup"><span data-stu-id="351cc-140">If the `DataAdapter` encounters multiple result sets, it creates multiple tables in the `DataSet`.</span></span> <span data-ttu-id="351cc-141">資料表會指定 Table*N*的遞增預設名稱，從 "Table" 開始 (Table0)。</span><span class="sxs-lookup"><span data-stu-id="351cc-141">The tables are given an incremental default name of Table*N*, starting with "Table" for Table0.</span></span> <span data-ttu-id="351cc-142">如果資料表名稱做為引數傳遞至 `Fill` 方法，則資料表會獲得開頭為 "TableName"，格式為 TableName*N*的遞增預設名稱，例如 TableName0。</span><span class="sxs-lookup"><span data-stu-id="351cc-142">If a table name is passed as an argument to the `Fill` method, the tables are given an incremental default name of TableName*N*, starting with "TableName" for TableName0.</span></span>  
  
## <a name="populating-a-dataset-from-multiple-dataadapters"></a><span data-ttu-id="351cc-143">從多重 DataAdapters 填入 DataSet</span><span class="sxs-lookup"><span data-stu-id="351cc-143">Populating a DataSet from Multiple DataAdapters</span></span>  

 <span data-ttu-id="351cc-144">任何數目的 `DataAdapter` 物件都可以搭配使用 `DataSet` 。</span><span class="sxs-lookup"><span data-stu-id="351cc-144">Any number of `DataAdapter` objects can be used with a `DataSet`.</span></span> <span data-ttu-id="351cc-145">每個 `DataAdapter` 都可以用以填滿一個或多個 `DataTable` 物件，並將更新解析回相關的資料來源。</span><span class="sxs-lookup"><span data-stu-id="351cc-145">Each `DataAdapter` can be used to fill one or more `DataTable` objects and resolve updates back to the relevant data source.</span></span> <span data-ttu-id="351cc-146">`DataRelation` 與 `Constraint` 物件可以新增至本機的 `DataSet` ，這可讓您將來自不同資料來源的資料關聯。</span><span class="sxs-lookup"><span data-stu-id="351cc-146">`DataRelation` and `Constraint` objects can be added to the `DataSet` locally, which enables you to relate data from dissimilar data sources.</span></span> <span data-ttu-id="351cc-147">例如， `DataSet` 包含的資料可來自 Microsoft SQL Server 資料庫、透過 OLE DB 公開的 IBM DB2 資料庫和產生 XML 資料流的資料來源。</span><span class="sxs-lookup"><span data-stu-id="351cc-147">For example, a `DataSet` can contain data from a Microsoft SQL Server database, an IBM DB2 database exposed through OLE DB, and a data source that streams XML.</span></span> <span data-ttu-id="351cc-148">與每個資料來源的通訊可以由一個或多個 `DataAdapter` 物件處理。</span><span class="sxs-lookup"><span data-stu-id="351cc-148">One or more `DataAdapter` objects can handle communication to each data source.</span></span>  
  
### <a name="example"></a><span data-ttu-id="351cc-149">範例</span><span class="sxs-lookup"><span data-stu-id="351cc-149">Example</span></span>  

 <span data-ttu-id="351cc-150">下列程式碼範例從 Microsoft SQL Server 上的 `Northwind` 資料庫填入客戶清單，並從存放在 Microsoft Access 2000 的 `Northwind` 資料庫填入訂貨清單。</span><span class="sxs-lookup"><span data-stu-id="351cc-150">The following code example populates a list of customers from the `Northwind` database on Microsoft SQL Server, and a list of orders from the `Northwind` database stored in Microsoft Access 2000.</span></span> <span data-ttu-id="351cc-151">填入的資料表和 `DataRelation`有關，之後客戶清單便會顯示該客戶的訂貨。</span><span class="sxs-lookup"><span data-stu-id="351cc-151">The filled tables are related with a `DataRelation`, and the list of customers is then displayed with the orders for that customer.</span></span> <span data-ttu-id="351cc-152">如需物件的詳細資訊 `DataRelation` ，請參閱 [加入 Datarelation](./dataset-datatable-dataview/adding-datarelations.md) 和 [流覽 datarelation](./dataset-datatable-dataview/navigating-datarelations.md)。</span><span class="sxs-lookup"><span data-stu-id="351cc-152">For more information about `DataRelation` objects, see [Adding DataRelations](./dataset-datatable-dataview/adding-datarelations.md) and [Navigating DataRelations](./dataset-datatable-dataview/navigating-datarelations.md).</span></span>  
  
```vb  
' Assumes that customerConnection is a valid SqlConnection object.  
' Assumes that orderConnection is a valid OleDbConnection object.  
Dim custAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers", customerConnection)  
  
Dim ordAdapter As OleDbDataAdapter = New OleDbDataAdapter( _  
  "SELECT * FROM Orders", orderConnection)  
  
Dim customerOrders As DataSet = New DataSet()  
custAdapter.Fill(customerOrders, "Customers")  
ordAdapter.Fill(customerOrders, "Orders")  
  
Dim relation As DataRelation = _  
  customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustomerID"), _
  customerOrders.Tables("Orders").Columns("CustomerID"))  
  
Dim pRow, cRow As DataRow  
For Each pRow In customerOrders.Tables("Customers").Rows  
  Console.WriteLine(pRow("CustomerID").ToString())  
  
  For Each cRow In pRow.GetChildRows(relation)  
    Console.WriteLine(vbTab & cRow("OrderID").ToString())  
  Next  
Next  
```  
  
```csharp  
// Assumes that customerConnection is a valid SqlConnection object.  
// Assumes that orderConnection is a valid OleDbConnection object.  
SqlDataAdapter custAdapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers", customerConnection);  
OleDbDataAdapter ordAdapter = new OleDbDataAdapter(  
  "SELECT * FROM Orders", orderConnection);  
  
DataSet customerOrders = new DataSet();  
  
custAdapter.Fill(customerOrders, "Customers");  
ordAdapter.Fill(customerOrders, "Orders");  
  
DataRelation relation = customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustomerID"],  
  customerOrders.Tables["Orders"].Columns["CustomerID"]);  
  
foreach (DataRow pRow in customerOrders.Tables["Customers"].Rows)  
{  
  Console.WriteLine(pRow["CustomerID"]);  
   foreach (DataRow cRow in pRow.GetChildRows(relation))  
    Console.WriteLine("\t" + cRow["OrderID"]);  
}  
```  
  
## <a name="sql-server-decimal-type"></a><span data-ttu-id="351cc-153">SQL Server Decimal 型別</span><span class="sxs-lookup"><span data-stu-id="351cc-153">SQL Server Decimal Type</span></span>  

 <span data-ttu-id="351cc-154">根據預設，會 `DataSet` 使用 .NET Framework 資料類型來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="351cc-154">By default, the `DataSet` stores data by using .NET Framework data types.</span></span> <span data-ttu-id="351cc-155">對大部分的應用程式而言，這些型別可便於表示資料來源資訊，</span><span class="sxs-lookup"><span data-stu-id="351cc-155">For most applications, these provide a convenient representation of data source information.</span></span> <span data-ttu-id="351cc-156">但是當資料來源中的資料型別為 SQL Server decimal 或 numeric 資料型別時，這種表示可能會造成問題。</span><span class="sxs-lookup"><span data-stu-id="351cc-156">However, this representation may cause a problem when the data type in the data source is a SQL Server decimal or numeric data type.</span></span> <span data-ttu-id="351cc-157">.NET Framework `decimal` 資料類型最多允許28個有效位數，而 SQL Server `decimal` 資料類型允許38個有效位數。</span><span class="sxs-lookup"><span data-stu-id="351cc-157">The .NET Framework `decimal` data type allows a maximum of 28 significant digits, whereas the SQL Server `decimal` data type allows 38 significant digits.</span></span> <span data-ttu-id="351cc-158">在 `SqlDataAdapter` 作業期間，如果 `Fill` 判斷 SQL Server `decimal` 欄位的精確度超過 28 個字元，則目前的資料列便不會加入 `DataTable`。</span><span class="sxs-lookup"><span data-stu-id="351cc-158">If the `SqlDataAdapter` determines during a `Fill` operation that the precision of a SQL Server `decimal` field is larger than 28 characters, the current row is not added to the `DataTable`.</span></span> <span data-ttu-id="351cc-159">反而會發生 `FillError` 事件，讓您判斷是否會失去精確度，並做出適當回應。</span><span class="sxs-lookup"><span data-stu-id="351cc-159">Instead the `FillError` event occurs, which enables you to determine whether a loss of precision will occur, and respond appropriately.</span></span> <span data-ttu-id="351cc-160">如需事件的詳細資訊 `FillError` ，請參閱 [處理 DataAdapter 事件](handling-dataadapter-events.md)。</span><span class="sxs-lookup"><span data-stu-id="351cc-160">For more information about the `FillError` event, see [Handling DataAdapter Events](handling-dataadapter-events.md).</span></span> <span data-ttu-id="351cc-161">若要取得 SQL Server `decimal` 值，您也可以使用 <xref:System.Data.SqlClient.SqlDataReader> 物件並呼叫 <xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="351cc-161">To get the SQL Server `decimal` value, you can also use a <xref:System.Data.SqlClient.SqlDataReader> object and call the <xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A> method.</span></span>  
  
 <span data-ttu-id="351cc-162">ADO.NET 2.0 在中引進了的增強支援 <xref:System.Data.SqlTypes> `DataSet` 。</span><span class="sxs-lookup"><span data-stu-id="351cc-162">ADO.NET 2.0 introduced enhanced support for <xref:System.Data.SqlTypes> in the `DataSet`.</span></span> <span data-ttu-id="351cc-163">如需詳細資訊，請參閱 [SqlTypes and the DataSet](./sql/sqltypes-and-the-dataset.md)。</span><span class="sxs-lookup"><span data-stu-id="351cc-163">For more information, see [SqlTypes and the DataSet](./sql/sqltypes-and-the-dataset.md).</span></span>  
  
## <a name="ole-db-chapters"></a><span data-ttu-id="351cc-164">OLE DB 章節</span><span class="sxs-lookup"><span data-stu-id="351cc-164">OLE DB Chapters</span></span>  

 <span data-ttu-id="351cc-165">您可以使用階層式資料列集 (Rowset)，或稱章節 (OLE DB 型別 `DBTYPE_HCHAPTER`、ADO 型別 `adChapter`) 來填入 `DataSet`的內容。</span><span class="sxs-lookup"><span data-stu-id="351cc-165">Hierarchical rowsets, or chapters (OLE DB type `DBTYPE_HCHAPTER`, ADO type `adChapter`) can be used to fill the contents of a `DataSet`.</span></span> <span data-ttu-id="351cc-166">若在 <xref:System.Data.OleDb.OleDbDataAdapter> 作業期間， `Fill` 遇到已章節化的資料行，則會針對該章節化的資料行建立 `DataTable` ，且該資料表會填入來自章節的資料行和資料列。</span><span class="sxs-lookup"><span data-stu-id="351cc-166">When the <xref:System.Data.OleDb.OleDbDataAdapter> encounters a chaptered column during a `Fill` operation, a `DataTable` is created for the chaptered column, and that table is filled with the columns and rows from the chapter.</span></span> <span data-ttu-id="351cc-167">為章節化資料行所建立的資料表會以 "*ParentTableNameChapteredColumnName*" 的形式，取用父資料表名稱和章節化資料行名稱來命名。</span><span class="sxs-lookup"><span data-stu-id="351cc-167">The table created for the chaptered column is named by using both the parent table name and the chaptered column name in the form "*ParentTableNameChapteredColumnName*".</span></span> <span data-ttu-id="351cc-168">如果 `DataSet` 中已有資料表，且與章節化資料行的名稱相符，則目前的資料表內會填入章節資料。</span><span class="sxs-lookup"><span data-stu-id="351cc-168">If a table already exists in the `DataSet` that matches the name of the chaptered column, the current table is filled with the chapter data.</span></span> <span data-ttu-id="351cc-169">如果現有資料表內沒有資料行符合章節內找到的資料行，則會加入新資料行。</span><span class="sxs-lookup"><span data-stu-id="351cc-169">If there is no column in an existing table that matches a column found in the chapter, a new column is added.</span></span>  
  
 <span data-ttu-id="351cc-170">在 `DataSet` 內的資料表中填入章節化資料行的資料前，會在階層式資料列集的父子資料表間建立關聯，方法是在父子資料表兩方均加入整數資料行，將父資料行設為自動遞增，然後使用加入自兩個資料表的資料行建立 `DataRelation` 。</span><span class="sxs-lookup"><span data-stu-id="351cc-170">Before the tables in the `DataSet` are filled with the data in the chaptered columns, a relation is created between the parent and child tables of the hierarchical rowset by adding an integer column to both the parent and child table, setting the parent column to auto-increment, and creating a `DataRelation` using the added columns from both tables.</span></span> <span data-ttu-id="351cc-171">加入的關聯以 "*ParentTableNameChapterColumnName*" 形式，使用父資料表和章節化資料行的名稱來命名。</span><span class="sxs-lookup"><span data-stu-id="351cc-171">The added relation is named by using the parent table and chapter column names in the form "*ParentTableNameChapterColumnName*".</span></span>  
  
 <span data-ttu-id="351cc-172">請注意，關聯資料行僅存在於 `DataSet`。</span><span class="sxs-lookup"><span data-stu-id="351cc-172">Note that the related column only exists in the `DataSet`.</span></span> <span data-ttu-id="351cc-173">來自資料來源的後續填入會造成資料表中加入新資料列，而非將變更合併至現有資料列。</span><span class="sxs-lookup"><span data-stu-id="351cc-173">Subsequent fills from the data source can cause new rows to be added to the tables instead of changes being merged into existing rows.</span></span>  
  
 <span data-ttu-id="351cc-174">另外要注意的是，如果您使用的 `DataAdapter.Fill` 多載採用 `DataTable`，則只有該資料表會填入。</span><span class="sxs-lookup"><span data-stu-id="351cc-174">Note also that, if you use the `DataAdapter.Fill` overload that takes a `DataTable`, only that table will be filled.</span></span> <span data-ttu-id="351cc-175">自動遞增的整數資料行仍會加入資料表，但不會建立或填入子資料表，也不會建立關聯。</span><span class="sxs-lookup"><span data-stu-id="351cc-175">An auto-incrementing integer column will still be added to the table, but no child table will be created or filled, and no relation will be created.</span></span>  
  
 <span data-ttu-id="351cc-176">下列範例使用 MSDataShape 提供者產生客戶清單中，每位客戶訂單的章節資料行。</span><span class="sxs-lookup"><span data-stu-id="351cc-176">The following example uses the MSDataShape Provider to generate a chapter column of orders for each customer in a list of customers.</span></span> <span data-ttu-id="351cc-177">接著便在 `DataSet` 內填入資料。</span><span class="sxs-lookup"><span data-stu-id="351cc-177">A `DataSet` is then filled with the data.</span></span>  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection( _  
  "Provider=MSDataShape;Data Provider=SQLOLEDB;" & _  
  "Data Source=(local);Integrated " & _  
  "Security=SSPI;Initial Catalog=northwind")  
  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter( _  
  "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " & _  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS Orders " & _  
  "RELATE CustomerID TO CustomerID)", connection)  
  
Dim customers As DataSet = New DataSet()  
  
adapter.Fill(customers, "Customers")  
End Using  
```  
  
```csharp  
using (OleDbConnection connection = new OleDbConnection("Provider=MSDataShape;Data Provider=SQLOLEDB;" +  
  "Data Source=(local);Integrated Security=SSPI;Initial Catalog=northwind"))  
{  
OleDbDataAdapter adapter = new OleDbDataAdapter("SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS Orders " +  
  "RELATE CustomerID TO CustomerID)", connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
}  
```  
  
 <span data-ttu-id="351cc-178">`Fill` 作業完畢後， `DataSet` 會包含兩個資料表： `Customers` 和 `CustomersOrders`，其中 `CustomersOrders` 表示章節化的資料行。</span><span class="sxs-lookup"><span data-stu-id="351cc-178">When the `Fill` operation is complete, the `DataSet` contains two tables: `Customers` and `CustomersOrders`, where `CustomersOrders` represents the chaptered column.</span></span> <span data-ttu-id="351cc-179">接下來，另一個名為 `Orders` 的資料行會加入 `Customers` 資料表，而另一個名為 `CustomersOrders` 的資料行會加入 `CustomersOrders` 資料表。</span><span class="sxs-lookup"><span data-stu-id="351cc-179">An additional column named `Orders` is added to the `Customers` table, and an additional column named `CustomersOrders` is added to the `CustomersOrders` table.</span></span> <span data-ttu-id="351cc-180">`Orders` 資料表內的 `Customers` 資料行設為自動遞增。</span><span class="sxs-lookup"><span data-stu-id="351cc-180">The `Orders` column in the `Customers` table is set to auto-increment.</span></span> <span data-ttu-id="351cc-181">接著會使用加入資料表的資料行 (將 `DataRelation`當做父資料表)，建立 `CustomersOrders`( `Customers` )。</span><span class="sxs-lookup"><span data-stu-id="351cc-181">A `DataRelation`, `CustomersOrders`, is created by using the columns that were added to the tables with `Customers` as the parent table.</span></span> <span data-ttu-id="351cc-182">下表顯示一些範例結果。</span><span class="sxs-lookup"><span data-stu-id="351cc-182">The following tables show some sample results.</span></span>  
  
### <a name="tablename-customers"></a><span data-ttu-id="351cc-183">TableName：Customers</span><span class="sxs-lookup"><span data-stu-id="351cc-183">TableName: Customers</span></span>  
  
|<span data-ttu-id="351cc-184">CustomerID</span><span class="sxs-lookup"><span data-stu-id="351cc-184">CustomerID</span></span>|<span data-ttu-id="351cc-185">公司名稱</span><span class="sxs-lookup"><span data-stu-id="351cc-185">CompanyName</span></span>|<span data-ttu-id="351cc-186">訂單</span><span class="sxs-lookup"><span data-stu-id="351cc-186">Orders</span></span>|  
|----------------|-----------------|------------|  
|<span data-ttu-id="351cc-187">ALFKI</span><span class="sxs-lookup"><span data-stu-id="351cc-187">ALFKI</span></span>|<span data-ttu-id="351cc-188">Alfreds Futterkiste</span><span class="sxs-lookup"><span data-stu-id="351cc-188">Alfreds Futterkiste</span></span>|<span data-ttu-id="351cc-189">0</span><span class="sxs-lookup"><span data-stu-id="351cc-189">0</span></span>|  
|<span data-ttu-id="351cc-190">ANATR</span><span class="sxs-lookup"><span data-stu-id="351cc-190">ANATR</span></span>|<span data-ttu-id="351cc-191">Ana Trujillo Emparedados y helados</span><span class="sxs-lookup"><span data-stu-id="351cc-191">Ana Trujillo Emparedados y helados</span></span>|<span data-ttu-id="351cc-192">1</span><span class="sxs-lookup"><span data-stu-id="351cc-192">1</span></span>|  
  
### <a name="tablename-customersorders"></a><span data-ttu-id="351cc-193">TableName：CustomersOrders</span><span class="sxs-lookup"><span data-stu-id="351cc-193">TableName: CustomersOrders</span></span>  
  
|<span data-ttu-id="351cc-194">CustomerID</span><span class="sxs-lookup"><span data-stu-id="351cc-194">CustomerID</span></span>|<span data-ttu-id="351cc-195">OrderID</span><span class="sxs-lookup"><span data-stu-id="351cc-195">OrderID</span></span>|<span data-ttu-id="351cc-196">CustomersOrders</span><span class="sxs-lookup"><span data-stu-id="351cc-196">CustomersOrders</span></span>|  
|----------------|-------------|---------------------|  
|<span data-ttu-id="351cc-197">ALFKI</span><span class="sxs-lookup"><span data-stu-id="351cc-197">ALFKI</span></span>|<span data-ttu-id="351cc-198">10643</span><span class="sxs-lookup"><span data-stu-id="351cc-198">10643</span></span>|<span data-ttu-id="351cc-199">0</span><span class="sxs-lookup"><span data-stu-id="351cc-199">0</span></span>|  
|<span data-ttu-id="351cc-200">ALFKI</span><span class="sxs-lookup"><span data-stu-id="351cc-200">ALFKI</span></span>|<span data-ttu-id="351cc-201">10692</span><span class="sxs-lookup"><span data-stu-id="351cc-201">10692</span></span>|<span data-ttu-id="351cc-202">0</span><span class="sxs-lookup"><span data-stu-id="351cc-202">0</span></span>|  
|<span data-ttu-id="351cc-203">ANATR</span><span class="sxs-lookup"><span data-stu-id="351cc-203">ANATR</span></span>|<span data-ttu-id="351cc-204">10308</span><span class="sxs-lookup"><span data-stu-id="351cc-204">10308</span></span>|<span data-ttu-id="351cc-205">1</span><span class="sxs-lookup"><span data-stu-id="351cc-205">1</span></span>|  
|<span data-ttu-id="351cc-206">ANATR</span><span class="sxs-lookup"><span data-stu-id="351cc-206">ANATR</span></span>|<span data-ttu-id="351cc-207">10625</span><span class="sxs-lookup"><span data-stu-id="351cc-207">10625</span></span>|<span data-ttu-id="351cc-208">1</span><span class="sxs-lookup"><span data-stu-id="351cc-208">1</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="351cc-209">另請參閱</span><span class="sxs-lookup"><span data-stu-id="351cc-209">See also</span></span>

- [<span data-ttu-id="351cc-210">DataAdapter 和 DataReader</span><span class="sxs-lookup"><span data-stu-id="351cc-210">DataAdapters and DataReaders</span></span>](dataadapters-and-datareaders.md)
- [<span data-ttu-id="351cc-211">ADO.NET 中的資料類型對應</span><span class="sxs-lookup"><span data-stu-id="351cc-211">Data Type Mappings in ADO.NET</span></span>](data-type-mappings-in-ado-net.md)
- [<span data-ttu-id="351cc-212">使用 DbDataAdapter 修改資料</span><span class="sxs-lookup"><span data-stu-id="351cc-212">Modifying Data with a DbDataAdapter</span></span>](modifying-data-with-a-dbdataadapter.md)
- [<span data-ttu-id="351cc-213">Multiple Active Result Set (MARS)</span><span class="sxs-lookup"><span data-stu-id="351cc-213">Multiple Active Result Sets (MARS)</span></span>](./sql/multiple-active-result-sets-mars.md)
- <span data-ttu-id="351cc-214">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="351cc-214">[ADO.NET Overview](ado-net-overview.md)</span></span>
