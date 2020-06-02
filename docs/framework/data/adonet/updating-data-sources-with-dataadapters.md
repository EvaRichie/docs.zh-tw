---
title: 使用 DataAdapter 更新資料來源
description: 瞭解 DataAdapter 的更新方法如何將資料集的變更解析回 ADO.NET 應用程式中的資料來源。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d1bd9a8c-0e29-40e3-bda8-d89176b72fb1
ms.openlocfilehash: e2348a3a89aa1c28856bfc21aaa25f2c8327aac7
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286180"
---
# <a name="updating-data-sources-with-dataadapters"></a><span data-ttu-id="dd838-103">使用 DataAdapter 更新資料來源</span><span class="sxs-lookup"><span data-stu-id="dd838-103">Updating Data Sources with DataAdapters</span></span>

<span data-ttu-id="dd838-104">呼叫 `Update` 的 <xref:System.Data.Common.DataAdapter> 方法，可將 <xref:System.Data.DataSet> 的變更解析回資料來源。</span><span class="sxs-lookup"><span data-stu-id="dd838-104">The `Update` method of the <xref:System.Data.Common.DataAdapter> is called to resolve changes from a <xref:System.Data.DataSet> back to the data source.</span></span> <span data-ttu-id="dd838-105">`Update` 方法類似 `Fill` 方法，會將 `DataSet` 的執行個體以及選擇性 (Optional) <xref:System.Data.DataTable> 物件或 `DataTable` 名稱做為引數。</span><span class="sxs-lookup"><span data-stu-id="dd838-105">The `Update` method, like the `Fill` method, takes as arguments an instance of a `DataSet`, and an optional <xref:System.Data.DataTable> object or `DataTable` name.</span></span> <span data-ttu-id="dd838-106">`DataSet` 執行個體是包含已進行之變更的 `DataSet`，而 `DataTable` 則識別要從中擷取變更的資料表。</span><span class="sxs-lookup"><span data-stu-id="dd838-106">The `DataSet` instance is the `DataSet` that contains the changes that have been made, and the `DataTable` identifies the table from which to retrieve the changes.</span></span> <span data-ttu-id="dd838-107">如果沒有指定任何 `DataTable`，就會使用 `DataTable` 中的第一個 `DataSet`。</span><span class="sxs-lookup"><span data-stu-id="dd838-107">If no `DataTable` is specified, the first `DataTable` in the `DataSet` is used.</span></span>

<span data-ttu-id="dd838-108">當您呼叫 `Update` 方法時，`DataAdapter` 會分析已進行的變更，並執行適當的命令 (INSERT、UPDATE 或 DELETE)。</span><span class="sxs-lookup"><span data-stu-id="dd838-108">When you call the `Update` method, the `DataAdapter` analyzes the changes that have been made and executes the appropriate command (INSERT, UPDATE, or DELETE).</span></span> <span data-ttu-id="dd838-109">當 `DataAdapter` 發現 <xref:System.Data.DataRow> 的變更時，它會使用 <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>、<xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> 或 <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> 來處理變更。</span><span class="sxs-lookup"><span data-stu-id="dd838-109">When the `DataAdapter` encounters a change to a <xref:System.Data.DataRow>, it uses the <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>, <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A>, or <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> to process the change.</span></span> <span data-ttu-id="dd838-110">如此可讓您於設計階段指定命令語法並盡量利用預存程序 (Stored Procedure)，發揮 ADO.NET 應用程式的最高效能。</span><span class="sxs-lookup"><span data-stu-id="dd838-110">This allows you to maximize the performance of your ADO.NET application by specifying command syntax at design time and, where possible, through the use of stored procedures.</span></span> <span data-ttu-id="dd838-111">您必須在呼叫 `Update` 之前明確地設定命令。</span><span class="sxs-lookup"><span data-stu-id="dd838-111">You must explicitly set the commands before calling `Update`.</span></span> <span data-ttu-id="dd838-112">如果呼叫 `Update` 之後，特定更新沒有適當命令可用 (例如，刪除的資料列沒有 `DeleteCommand`)，便會擲回例外狀況 (Exception)。</span><span class="sxs-lookup"><span data-stu-id="dd838-112">If `Update` is called and the appropriate command does not exist for a particular update (for example, no `DeleteCommand` for deleted rows), an exception is thrown.</span></span>

> [!NOTE]
> <span data-ttu-id="dd838-113">如果您要使用 SQL Server 預存程序搭配 `DataAdapter` 來編輯或刪除資料，請務必不要在預存程序定義中使用 SET NOCOUNT ON。</span><span class="sxs-lookup"><span data-stu-id="dd838-113">If you are using SQL Server stored procedures to edit or delete data using a `DataAdapter`, make sure that you do not use SET NOCOUNT ON in the stored procedure definition.</span></span> <span data-ttu-id="dd838-114">因為這樣會讓傳回的受影響資料列計數成為零，而 `DataAdapter` 會將它解譯為並行衝突。</span><span class="sxs-lookup"><span data-stu-id="dd838-114">This causes the rows affected count returned to be zero, which the `DataAdapter` interprets as a concurrency conflict.</span></span> <span data-ttu-id="dd838-115">在此事件中，系統會擲回 <xref:System.Data.DBConcurrencyException>。</span><span class="sxs-lookup"><span data-stu-id="dd838-115">In this event, a <xref:System.Data.DBConcurrencyException> will be thrown.</span></span>

<span data-ttu-id="dd838-116">命令參數可用來針對 `DataSet` 內每個經過修改的資料列指定 SQL 陳述式或預存程序的輸入和輸出值。</span><span class="sxs-lookup"><span data-stu-id="dd838-116">Command parameters can be used to specify input and output values for an SQL statement or stored procedure for each modified row in a `DataSet`.</span></span> <span data-ttu-id="dd838-117">如需詳細資訊，請參閱[DataAdapter 參數](dataadapter-parameters.md)。</span><span class="sxs-lookup"><span data-stu-id="dd838-117">For more information, see [DataAdapter Parameters](dataadapter-parameters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dd838-118">請務必瞭解刪除 <xref:System.Data.DataTable> 中的資料列與移除資料列之間的差異。</span><span class="sxs-lookup"><span data-stu-id="dd838-118">It is important to understand the difference between deleting a row in a <xref:System.Data.DataTable> and removing the row.</span></span> <span data-ttu-id="dd838-119">當您呼叫 `Remove` 或 `RemoveAt` 方法時，系統會立即移除資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-119">When you call the `Remove` or `RemoveAt` method, the row is removed immediately.</span></span> <span data-ttu-id="dd838-120">如果您之後傳遞 `DataTable` 或 `DataSet` 給 `DataAdapter` 並呼叫 `Update`，則後端 (Back End) 資料來源中的任何對應資料列將不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="dd838-120">Any corresponding rows in the back end data source will not be affected if you then pass the `DataTable` or `DataSet` to a `DataAdapter` and call `Update`.</span></span> <span data-ttu-id="dd838-121">當您使用 `Delete` 方法時，資料列會保留在 `DataTable` 中並標示為待刪除。</span><span class="sxs-lookup"><span data-stu-id="dd838-121">When you use the `Delete` method, the row remains in the `DataTable` and is marked for deletion.</span></span> <span data-ttu-id="dd838-122">如果您之後傳遞 `DataTable` 或 `DataSet` 給 `DataAdapter` 並呼叫 `Update`，系統就會刪除後端資料來源中的對應資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-122">If you then pass the `DataTable` or `DataSet` to a `DataAdapter` and call `Update`, the corresponding row in the back end data source is deleted.</span></span>

<span data-ttu-id="dd838-123">如果您的 `DataTable` 對應至或產生自單一資料庫資料表，則可以利用 <xref:System.Data.Common.DbCommandBuilder> 物件來自動產生 `DeleteCommand`、`InsertCommand` 以及 `UpdateCommand` 的 `DataAdapter` 物件。</span><span class="sxs-lookup"><span data-stu-id="dd838-123">If your `DataTable` maps to or is generated from a single database table, you can take advantage of the <xref:System.Data.Common.DbCommandBuilder> object to automatically generate the `DeleteCommand`, `InsertCommand`, and `UpdateCommand` objects for the `DataAdapter`.</span></span> <span data-ttu-id="dd838-124">如需詳細資訊，請參閱[使用 Commandbuilder 產生命令](generating-commands-with-commandbuilders.md)。</span><span class="sxs-lookup"><span data-stu-id="dd838-124">For more information, see [Generating Commands with CommandBuilders](generating-commands-with-commandbuilders.md).</span></span>

## <a name="using-updatedrowsource-to-map-values-to-a-dataset"></a><span data-ttu-id="dd838-125">使用 UpdatedRowSource 將值對應至 DataSet</span><span class="sxs-lookup"><span data-stu-id="dd838-125">Using UpdatedRowSource to Map Values to a DataSet</span></span>

<span data-ttu-id="dd838-126">在呼叫 `DataTable` 的 Update 方法之後，您可以使用 `DataAdapter` 物件的 <xref:System.Data.Common.DbCommand.UpdatedRowSource%2A> 屬性來控制從資料來源傳回的值要如何對應回 <xref:System.Data.Common.DbCommand>。</span><span class="sxs-lookup"><span data-stu-id="dd838-126">You can control how the values returned from the data source are mapped back to the `DataTable` following a call to the Update method of a `DataAdapter`, by using the <xref:System.Data.Common.DbCommand.UpdatedRowSource%2A> property of a <xref:System.Data.Common.DbCommand> object.</span></span> <span data-ttu-id="dd838-127">您可以透過將 `UpdatedRowSource` 屬性設為其中一個 <xref:System.Data.UpdateRowSource> 列舉值，控制要忽略 `DataAdapter` 命令所傳回的輸出參數，還是要將這些參數套用至 `DataSet` 中已變更的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-127">By setting the `UpdatedRowSource` property to one of the <xref:System.Data.UpdateRowSource> enumeration values, you can control whether output parameters returned by the `DataAdapter` commands are ignored or applied to the changed row in the `DataSet`.</span></span> <span data-ttu-id="dd838-128">您還能夠指定是否要將第一個傳回的資料列 (如果存在) 套用至 `DataTable` 中已變更的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-128">You can also specify whether the first returned row (if it exists) is applied to the changed row in the `DataTable`.</span></span>

<span data-ttu-id="dd838-129">下列表格說明 `UpdateRowSource` 列舉型別的各種值，以及這些值如何影響與 `DataAdapter` 搭配使用之命令的行為。</span><span class="sxs-lookup"><span data-stu-id="dd838-129">The following table describes the different values of the `UpdateRowSource` enumeration and how they affect the behavior of a command used with a `DataAdapter`.</span></span>

|<span data-ttu-id="dd838-130">UpdatedRowSource 列舉型別</span><span class="sxs-lookup"><span data-stu-id="dd838-130">UpdatedRowSource Enumeration</span></span>|<span data-ttu-id="dd838-131">描述</span><span class="sxs-lookup"><span data-stu-id="dd838-131">Description</span></span>|
|----------------------------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|<span data-ttu-id="dd838-132">輸出參數和傳回結果集的第一個資料列都會對應至 `DataSet` 中已變更的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-132">Both the output parameters and the first row of a returned result set may be mapped to the changed row in the `DataSet`.</span></span>|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|<span data-ttu-id="dd838-133">只有傳回結果集之第一個資料列內的資料會對應至 `DataSet` 中已變更的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-133">Only the data in the first row of a returned result set may be mapped to the changed row in the `DataSet`.</span></span>|
|<xref:System.Data.UpdateRowSource.None>|<span data-ttu-id="dd838-134">將忽略任何輸出參數或傳回結果集的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-134">Any output parameters or rows of a returned result set are ignored.</span></span>|
|<xref:System.Data.UpdateRowSource.OutputParameters>|<span data-ttu-id="dd838-135">只有輸出參數會對應至 `DataSet` 中已變更的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-135">Only output parameters may be mapped to the changed row in the `DataSet`.</span></span>|

<span data-ttu-id="dd838-136">`Update` 方法會將您的變更解析回資料來源，但是自從您上次填入 `DataSet` 之後，其他用戶端可能也已經修改資料來源的資料。</span><span class="sxs-lookup"><span data-stu-id="dd838-136">The `Update` method resolves your changes back to the data source; however other clients may have modified data at the data source since the last time you filled the `DataSet`.</span></span> <span data-ttu-id="dd838-137">若要以目前的資料重新整理 `DataSet`，請使用 `DataAdapter` 和 `Fill` 方法。</span><span class="sxs-lookup"><span data-stu-id="dd838-137">To refresh your `DataSet` with current data, use the `DataAdapter` and `Fill` method.</span></span> <span data-ttu-id="dd838-138">如此新資料列會加入資料表，而更新資訊也會合併入現有資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-138">New rows will be added to the table, and updated information will be incorporated into existing rows.</span></span> <span data-ttu-id="dd838-139">`Fill` 方法會藉由檢查 `DataSet` 中資料列的主索引鍵值以及 `SelectCommand` 所傳回的資料列，決定要加入新資料列或更新現有資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-139">The `Fill` method determines whether a new row will be added or an existing row will be updated by examining the primary key values of the rows in the `DataSet` and the rows returned by the `SelectCommand`.</span></span> <span data-ttu-id="dd838-140">如果 `Fill` 方法發現 `DataSet` 中之資料列的主索引鍵值符合 `SelectCommand` 所傳回結果中之資料列的主索引鍵值，它就會以 `SelectCommand` 所傳回之資料列中的資訊更新現有資料列，並將現有資料列的 <xref:System.Data.DataRow.RowState%2A> 設為 `Unchanged`。</span><span class="sxs-lookup"><span data-stu-id="dd838-140">If the `Fill` method encounters a primary key value for a row in the `DataSet` that matches a primary key value from a row in the results returned by the `SelectCommand`, it updates the existing row with the information from the row returned by the `SelectCommand` and sets the <xref:System.Data.DataRow.RowState%2A> of the existing row to `Unchanged`.</span></span> <span data-ttu-id="dd838-141">如果 `SelectCommand` 傳回之資料列的主索引鍵值與 `DataSet` 中資料列的任何主索引鍵值都不相符，`Fill` 方法就加入 `RowState` 設定為 `Unchanged` 的新資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-141">If a row returned by the `SelectCommand` has a primary key value that does not match any of the primary key values of the rows in the `DataSet`, the `Fill` method adds a new row with a `RowState` of `Unchanged`.</span></span>

> [!NOTE]
> <span data-ttu-id="dd838-142">如果 `SelectCommand` 傳回 OUTER JOIN 的結果，`DataAdapter` 將不會為產生的 `PrimaryKey` 設定 `DataTable` 值。</span><span class="sxs-lookup"><span data-stu-id="dd838-142">If the `SelectCommand` returns the results of an OUTER JOIN, the `DataAdapter` will not set a `PrimaryKey` value for the resulting `DataTable`.</span></span> <span data-ttu-id="dd838-143">您必須自己定義 `PrimaryKey`，確保正確解析重複的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-143">You must define the `PrimaryKey` yourself to ensure that duplicate rows are resolved correctly.</span></span> <span data-ttu-id="dd838-144">如需詳細資訊，請參閱[定義主要索引鍵](./dataset-datatable-dataview/defining-primary-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="dd838-144">For more information, see [Defining Primary Keys](./dataset-datatable-dataview/defining-primary-keys.md).</span></span>

<span data-ttu-id="dd838-145">若要處理呼叫方法時可能會發生的例外狀況 `Update` ，您可以使用 `RowUpdated` 事件來回應發生的資料列更新錯誤（請參閱[處理 DataAdapter 事件](handling-dataadapter-events.md)），或者您可以在 `DataAdapter.ContinueUpdateOnError` 呼叫之前將設定為 `true` `Update` ，然後在更新完成時回應儲存于特定資料列之屬性中的錯誤資訊 `RowError` （請參閱資料[列錯誤資訊](./dataset-datatable-dataview/row-error-information.md)）。</span><span class="sxs-lookup"><span data-stu-id="dd838-145">To handle exceptions that may occur when calling the `Update` method, you can use the `RowUpdated` event to respond to row update errors as they occur (see [Handling DataAdapter Events](handling-dataadapter-events.md)), or you can set `DataAdapter.ContinueUpdateOnError` to `true` before calling `Update`, and respond to the error information stored in the `RowError` property of a particular row when the update is complete (see [Row Error Information](./dataset-datatable-dataview/row-error-information.md)).</span></span>

> [!NOTE]
> <span data-ttu-id="dd838-146">`AcceptChanges`在 `DataSet` 、或上呼叫將會使用的 `DataTable` `DataRow` `Original` `DataRow` 值來覆寫的所有值 `Current` `DataRow` 。</span><span class="sxs-lookup"><span data-stu-id="dd838-146">Calling `AcceptChanges` on the `DataSet`, `DataTable`, or `DataRow` will cause all `Original` values for a `DataRow` to be overwritten with the `Current` values for the `DataRow`.</span></span> <span data-ttu-id="dd838-147">如果識別資料列為唯一的欄位值已經被修改，則在呼叫 `AcceptChanges` 之後，`Original` 值就不會再與資料來源內的值相符。</span><span class="sxs-lookup"><span data-stu-id="dd838-147">If the field values that identify the row as unique have been modified, after calling `AcceptChanges` the `Original` values will no longer match the values in the data source.</span></span> <span data-ttu-id="dd838-148">此時，系統會在呼叫 `AcceptChanges` 的 Update 方法期間，自動針對每個資料列呼叫 `DataAdapter`。</span><span class="sxs-lookup"><span data-stu-id="dd838-148">`AcceptChanges` is called automatically for each row during a call to the Update method of a `DataAdapter`.</span></span> <span data-ttu-id="dd838-149">您可以先將 `AcceptChangesDuringUpdate` 的 `DataAdapter` 屬性設定為 false，或針對 `RowUpdated` 事件建立事件處理常式並將 <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> 設定為 <xref:System.Data.UpdateStatus.SkipCurrentRow>，藉以在呼叫 Update 方法期間保留原始值。</span><span class="sxs-lookup"><span data-stu-id="dd838-149">You can preserve the original values during a call to the Update method by first setting the `AcceptChangesDuringUpdate` property of the `DataAdapter` to false, or by creating an event handler for the `RowUpdated` event and setting the <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> to <xref:System.Data.UpdateStatus.SkipCurrentRow>.</span></span> <span data-ttu-id="dd838-150">如需詳細資訊，請參閱[合併資料集內容](./dataset-datatable-dataview/merging-dataset-contents.md)和[處理 DataAdapter 事件](handling-dataadapter-events.md)。</span><span class="sxs-lookup"><span data-stu-id="dd838-150">For more information, see [Merging DataSet Contents](./dataset-datatable-dataview/merging-dataset-contents.md) and [Handling DataAdapter Events](handling-dataadapter-events.md).</span></span>

## <a name="example"></a><span data-ttu-id="dd838-151">範例</span><span class="sxs-lookup"><span data-stu-id="dd838-151">Example</span></span>

<span data-ttu-id="dd838-152">下列範例示範如何藉由明確地設定的 `UpdateCommand` `DataAdapter` 並呼叫其方法，來執行修改過的資料列更新 `Update` 。</span><span class="sxs-lookup"><span data-stu-id="dd838-152">The following examples demonstrate how to perform updates to modified rows by explicitly setting the `UpdateCommand` of a `DataAdapter` and calling its `Update` method.</span></span> <span data-ttu-id="dd838-153">請注意，在 UPDATE 陳述式之 WHERE 子句中指定的參數是設定為使用 `Original` 的 `SourceColumn` 值。</span><span class="sxs-lookup"><span data-stu-id="dd838-153">Notice that the parameter specified in the WHERE clause of the UPDATE statement is set to use the `Original` value of the `SourceColumn`.</span></span> <span data-ttu-id="dd838-154">這一點相當重要，因為 `Current` 值可能已經修改，而不符合資料來源中的值。</span><span class="sxs-lookup"><span data-stu-id="dd838-154">This is important, because the `Current` value may have been modified and may not match the value in the data source.</span></span> <span data-ttu-id="dd838-155">`Original` 值是用來填入資料來源之 `DataTable` 的值。</span><span class="sxs-lookup"><span data-stu-id="dd838-155">The `Original` value is the value that was used to populate the `DataTable` from the data source.</span></span>

[!code-csharp[DataWorks SqlClient.DataAdapterUpdate#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.DataAdapterUpdate/CS/source.cs#1)]
[!code-vb[DataWorks SqlClient.DataAdapterUpdate#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.DataAdapterUpdate/VB/source.vb#1)]

## <a name="autoincrement-columns"></a><span data-ttu-id="dd838-156">AutoIncrement 資料行</span><span class="sxs-lookup"><span data-stu-id="dd838-156">AutoIncrement Columns</span></span>

<span data-ttu-id="dd838-157">如果來自資料來源的資料表具有自動遞增的資料行，您就可以將這些資料行填入 `DataSet` 中，方法包括：將自動遞增值當成預存程序的輸出參數傳回並將它對應至資料表的資料行、傳回結果集 (由預存程序或 SQL 陳述式所傳回) 之第一個資料列中的自動遞增值，或使用 `RowUpdated` 的 `DataAdapter` 事件來執行其他 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="dd838-157">If the tables from your data source have auto-incrementing columns, you can fill the columns in your `DataSet` either by returning the auto-increment value as an output parameter of a stored procedure and mapping that to a column in a table, by returning the auto-increment value in the first row of a result set returned by a stored procedure or SQL statement, or by using the `RowUpdated` event of the `DataAdapter` to execute an additional SELECT statement.</span></span> <span data-ttu-id="dd838-158">如需詳細資訊和範例，請參閱抓取[識別或自動編號值](retrieving-identity-or-autonumber-values.md)。</span><span class="sxs-lookup"><span data-stu-id="dd838-158">For more information and an example, see [Retrieving Identity or Autonumber Values](retrieving-identity-or-autonumber-values.md).</span></span>

## <a name="ordering-of-inserts-updates-and-deletes"></a><span data-ttu-id="dd838-159">插入、更新和刪除的順序</span><span class="sxs-lookup"><span data-stu-id="dd838-159">Ordering of Inserts, Updates, and Deletes</span></span>

<span data-ttu-id="dd838-160">在許多情況下，以何種順序將透過 `DataSet` 所進行的變更傳送給資料來源是很重要的。</span><span class="sxs-lookup"><span data-stu-id="dd838-160">In many circumstances, the order in which changes made through the `DataSet` are sent to the data source is important.</span></span> <span data-ttu-id="dd838-161">例如，如果更新了現有資料列的主索引鍵值，也加入了以新主索引鍵值當做外部索引鍵的資料列，則先進行更新再執行插入是很重要的。</span><span class="sxs-lookup"><span data-stu-id="dd838-161">For example, if a primary key value for an existing row is updated, and a new row has been added with the new primary key value as a foreign key, it is important to process the update before the insert.</span></span>

<span data-ttu-id="dd838-162">您可以使用 `Select` 的 `DataTable` 方法來傳回僅參考具有特定 `DataRow` 之資料列的 `RowState` 陣列。</span><span class="sxs-lookup"><span data-stu-id="dd838-162">You can use the `Select` method of the `DataTable` to return a `DataRow` array that only references rows with a particular `RowState`.</span></span> <span data-ttu-id="dd838-163">接著，您可以將傳回的 `DataRow` 陣列傳遞給 `Update` 的 `DataAdapter` 方法來處理已修改的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-163">You can then pass the returned `DataRow` array to the `Update` method of the `DataAdapter` to process the modified rows.</span></span> <span data-ttu-id="dd838-164">您可指定要更新的資料列子集，藉以控制插入、更新和刪除的處理順序。</span><span class="sxs-lookup"><span data-stu-id="dd838-164">By specifying a subset of rows to be updated, you can control the order in which inserts, updates, and deletes are processed.</span></span>

## <a name="example"></a><span data-ttu-id="dd838-165">範例</span><span class="sxs-lookup"><span data-stu-id="dd838-165">Example</span></span>

<span data-ttu-id="dd838-166">例如，下列程式碼確保先處理資料表的已刪除資料列，接著處理已更新資料列，然後再處理已插入資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-166">For example, the following code ensures that the deleted rows of the table are processed first, then the updated rows, and then the inserted rows.</span></span>

```vb
Dim table As DataTable = dataSet.Tables("Customers")

' First process deletes.
dataSet.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.Deleted))

' Next process updates.
adapter.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.ModifiedCurrent))

' Finally, process inserts.
adapter.Update(table.Select(Nothing, Nothing, _
  DataViewRowState.Added))
```

```csharp
DataTable table = dataSet.Tables["Customers"];

// First process deletes.
adapter.Update(table.Select(null, null, DataViewRowState.Deleted));

// Next process updates.
adapter.Update(table.Select(null, null,
  DataViewRowState.ModifiedCurrent));

// Finally, process inserts.
adapter.Update(table.Select(null, null, DataViewRowState.Added));
```

## <a name="use-a-dataadapter-to-retrieve-and-update-data"></a><span data-ttu-id="dd838-167">使用 DataAdapter 擷取和更新資料</span><span class="sxs-lookup"><span data-stu-id="dd838-167">Use a DataAdapter to Retrieve and Update Data</span></span>

<span data-ttu-id="dd838-168">您可以使用 DataAdapter 擷取和更新資料。</span><span class="sxs-lookup"><span data-stu-id="dd838-168">You can use a DataAdapter to retrieve and update the data.</span></span>

- <span data-ttu-id="dd838-169">範例會使用 DataAdapter.AcceptChangesDuringFill 複製資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="dd838-169">The sample uses DataAdapter.AcceptChangesDuringFill to clone the data in the database.</span></span> <span data-ttu-id="dd838-170">如果屬性設為 false，填入資料表時就不會呼叫 AcceptChanges，並會將新加入的資料列視為插入的資料列。</span><span class="sxs-lookup"><span data-stu-id="dd838-170">If the property is set as false, AcceptChanges is not called when filling the table, and the newly added rows are treated as inserted rows.</span></span> <span data-ttu-id="dd838-171">因此，範例會使用這些資料列，將新資料列插入資料庫。</span><span class="sxs-lookup"><span data-stu-id="dd838-171">So, the sample uses these rows to insert the new rows into the database.</span></span>

- <span data-ttu-id="dd838-172">範例會使用 DataAdapter.TableMappings 定義來源資料表和 DataTable 之間的對應。</span><span class="sxs-lookup"><span data-stu-id="dd838-172">The samples uses DataAdapter.TableMappings to define the mapping between the source table and DataTable.</span></span>

- <span data-ttu-id="dd838-173">範例會使用 DataAdapter.FillLoadOption 決定配接器如何從 DbDataReader 填入 DataTable。</span><span class="sxs-lookup"><span data-stu-id="dd838-173">The sample uses DataAdapter.FillLoadOption to determine how the adapter fills the DataTable from the DbDataReader.</span></span> <span data-ttu-id="dd838-174">建立 DataTable 時，您可以將屬性設定為 LoadOption.Upsert 或 LoadOption.PreserveChanges，只將資料庫的資料寫入目前版本或原始版本。</span><span class="sxs-lookup"><span data-stu-id="dd838-174">When you create a DataTable, you can only write the data from database to the current version or the original version by setting the property as the LoadOption.Upsert or the LoadOption.PreserveChanges.</span></span>

- <span data-ttu-id="dd838-175">範例也會使用 DbDataAdapter.UpdateBatchSize，更新資料表以執行批次作業。</span><span class="sxs-lookup"><span data-stu-id="dd838-175">The sample will also update the table by using DbDataAdapter.UpdateBatchSize to perform batch operations.</span></span>

<span data-ttu-id="dd838-176">在編譯和執行範例之前，您必須建立範例資料庫：</span><span class="sxs-lookup"><span data-stu-id="dd838-176">Before you compile and run the sample, you need to create the sample database:</span></span>

```sql
USE [master]
GO

CREATE DATABASE [MySchool]

GO

USE [MySchool]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Course]([CourseID] [nvarchar](10) NOT NULL,
[Year] [smallint] NOT NULL,
[Title] [nvarchar](100) NOT NULL,
[Credits] [int] NOT NULL,
[DepartmentID] [int] NOT NULL,
 CONSTRAINT [PK_Course] PRIMARY KEY CLUSTERED
(
[CourseID] ASC,
[Year] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Department]([DepartmentID] [int] IDENTITY(1,1) NOT NULL,
[Name] [nvarchar](50) NOT NULL,
[Budget] [money] NOT NULL,
[StartDate] [datetime] NOT NULL,
[Administrator] [int] NULL,
 CONSTRAINT [PK_Department] PRIMARY KEY CLUSTERED
(
[DepartmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1045', 2012, N'Calculus', 4, 7)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1061', 2012, N'Physics', 4, 1)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2021', 2012, N'Composition', 3, 2)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2042', 2012, N'Literature', 4, 2)

SET IDENTITY_INSERT [dbo].[Department] ON

INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (1, N'Engineering', 350000.0000, CAST(0x0000999C00000000 AS DateTime), 2)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (2, N'English', 120000.0000, CAST(0x0000999C00000000 AS DateTime), 6)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (4, N'Economics', 200000.0000, CAST(0x0000999C00000000 AS DateTime), 4)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (7, N'Mathematics', 250024.0000, CAST(0x0000999C00000000 AS DateTime), 3)
SET IDENTITY_INSERT [dbo].[Department] OFF

ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
```

<span data-ttu-id="dd838-177">使用此程式碼範例的 c # 和 Visual Basic 專案，可以在[開發人員程式碼範例](https://code.msdn.microsoft.com/site/search?f%5B0%5D.Type=SearchText&f%5B0%5D.Value=How%20to%20use%20DataAdapter%20to%20retrieve%20and%20update%20data&f%5B1%5D)中找到。</span><span class="sxs-lookup"><span data-stu-id="dd838-177">C# and Visual Basic projects with this code sample can be found on [Developer Code Samples](https://code.msdn.microsoft.com/site/search?f%5B0%5D.Type=SearchText&f%5B0%5D.Value=How%20to%20use%20DataAdapter%20to%20retrieve%20and%20update%20data&f%5B1%5D).</span></span>

```csharp
using System;
using System.Data;
using System.Data.Common;
using System.Data.SqlClient;
using System.Linq;
using CSDataAdapterOperations.Properties;

namespace CSDataAdapterOperations.Properties {
   internal sealed partial class Settings : global::System.Configuration.ApplicationSettingsBase {

      private static Settings defaultInstance = ((Settings)(global::System.Configuration.ApplicationSettingsBase.Synchronized(new Settings())));

      public static Settings Default {
         get {
            return defaultInstance;
         }
      }

      [global::System.Configuration.ApplicationScopedSettingAttribute()]
      [global::System.Configuration.DefaultSettingValueAttribute("Data Source=(local);Initial Catalog=MySchool;Integrated Security=True")]
      public string MySchoolConnectionString {
         get {
            return ((string)(this["MySchoolConnectionString"]));
         }
      }
   }
}

class Program {
   static void Main(string[] args) {
      Settings settings = new Settings();

      // Copy the data from the database.  Get the table Department and Course from the database.
      String selectString = @"SELECT [DepartmentID],[Name],[Budget],[StartDate],[Administrator]
                                     FROM [MySchool].[dbo].[Department];

                                   SELECT [CourseID],@Year as [Year],Max([Title]) as [Title],
                                   Max([Credits]) as [Credits],Max([DepartmentID]) as [DepartmentID]
                                   FROM [MySchool].[dbo].[Course]
                                   Group by [CourseID]";

      DataSet mySchool = new DataSet();

      SqlCommand selectCommand = new SqlCommand(selectString);
      SqlParameter parameter = selectCommand.Parameters.Add("@Year", SqlDbType.SmallInt, 2);
      parameter.Value = new Random(DateTime.Now.Millisecond).Next(9999);

      // Use DataTableMapping to map the source tables and the destination tables.
      DataTableMapping[] tableMappings = {new DataTableMapping("Table", "Department"), new DataTableMapping("Table1", "Course")};
      CopyData(mySchool, settings.MySchoolConnectionString, selectCommand, tableMappings);

      Console.WriteLine("The following tables are from the database.");
      foreach (DataTable table in mySchool.Tables) {
         Console.WriteLine(table.TableName);
         ShowDataTable(table);
      }

      // Roll back the changes
      DataTable department = mySchool.Tables["Department"];
      DataTable course = mySchool.Tables["Course"];

      department.Rows[0]["Name"] = "New" + department.Rows[0][1];
      course.Rows[0]["Title"] = "New" + course.Rows[0]["Title"];
      course.Rows[0]["Credits"] = 10;

      Console.WriteLine("After we changed the tables:");
      foreach (DataTable table in mySchool.Tables) {
         Console.WriteLine(table.TableName);
         ShowDataTable(table);
      }

      department.RejectChanges();
      Console.WriteLine("After use the RejectChanges method in Department table to roll back the changes:");
      ShowDataTable(department);

      DataColumn[] primaryColumns = { course.Columns["CourseID"] };
      DataColumn[] resetColumns = { course.Columns["Title"] };
      ResetCourse(course, settings.MySchoolConnectionString, primaryColumns, resetColumns);
      Console.WriteLine("After use the ResetCourse method in Course table to roll back the changes:");
      ShowDataTable(course);

      // Batch update the table.
      String insertString = @"Insert into [MySchool].[dbo].[Course]([CourseID],[Year],[Title],
                                   [Credits],[DepartmentID])
             values (@CourseID,@Year,@Title,@Credits,@DepartmentID)";
      SqlCommand insertCommand = new SqlCommand(insertString);
      insertCommand.Parameters.Add("@CourseID", SqlDbType.NVarChar, 10, "CourseID");
      insertCommand.Parameters.Add("@Year", SqlDbType.SmallInt, 2, "Year");
      insertCommand.Parameters.Add("@Title", SqlDbType.NVarChar, 100, "Title");
      insertCommand.Parameters.Add("@Credits", SqlDbType.Int, 4, "Credits");
      insertCommand.Parameters.Add("@DepartmentID", SqlDbType.Int, 4, "DepartmentID");

      const Int32 batchSize = 10;
      BatchInsertUpdate(course, settings.MySchoolConnectionString, insertCommand, batchSize);
   }

   private static void CopyData(DataSet dataSet, String connectionString, SqlCommand selectCommand, DataTableMapping[] tableMappings) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         selectCommand.Connection = connection;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter(selectCommand)) {adapter.TableMappings.AddRange(tableMappings);
            // If set the AcceptChangesDuringFill as the false, AcceptChanges will not be called on a
            // DataRow after it is added to the DataTable during any of the Fill operations.
            adapter.AcceptChangesDuringFill = false;

            adapter.Fill(dataSet);
         }
      }
   }

   // Roll back only one column or several columns data of the Course table by call ResetDataTable method.
   private static void ResetCourse(DataTable table, String connectionString,
       DataColumn[] primaryColumns, DataColumn[] resetColumns) {
      table.PrimaryKey = primaryColumns;

      // Build the query string
      String primaryCols = String.Join(",", primaryColumns.Select(col => col.ColumnName));
      String resetCols = String.Join(",", resetColumns.Select(col => $"Max({col.ColumnName}) as {col.ColumnName}"));

      String selectString = $"Select {primaryCols},{resetCols} from Course Group by {primaryCols}");

      SqlCommand selectCommand = new SqlCommand(selectString);

      ResetDataTable(table, connectionString, selectCommand);
   }

   // RejectChanges will roll back all changes made to the table since it was loaded, or the last time AcceptChanges
   // was called. When you copy from the database, you can lose all the data after calling RejectChanges
   // The ResetDataTable method rolls back one or more columns of data.
   private static void ResetDataTable(DataTable table, String connectionString,
       SqlCommand selectCommand) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         selectCommand.Connection = connection;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter(selectCommand)) {
            // The incoming values for this row will be written to the current version of each
            // column. The original version of each column's data will not be changed.
            adapter.FillLoadOption = LoadOption.Upsert;

            adapter.Fill(table);
         }
      }
   }

   private static void BatchInsertUpdate(DataTable table, String connectionString,
       SqlCommand insertCommand, Int32 batchSize) {
      using (SqlConnection connection = new SqlConnection(connectionString)) {
         insertCommand.Connection = connection;
         // When setting UpdateBatchSize to a value other than 1, all the commands
         // associated with the SqlDataAdapter have to have their UpdatedRowSource
         // property set to None or OutputParameters. An exception is thrown otherwise.
         insertCommand.UpdatedRowSource = UpdateRowSource.None;

         connection.Open();

         using (SqlDataAdapter adapter = new SqlDataAdapter()) {
            adapter.InsertCommand = insertCommand;
            // Gets or sets the number of rows that are processed in each round-trip to the server.
            // Setting it to 1 disables batch updates, as rows are sent one at a time.
            adapter.UpdateBatchSize = batchSize;

            adapter.Update(table);

            Console.WriteLine("Successfully to update the table.");
         }
      }
   }

   private static void ShowDataTable(DataTable table) {
      foreach (DataColumn col in table.Columns) {
         Console.Write("{0,-14}", col.ColumnName);
      }
      Console.WriteLine("{0,-14}", "RowState");

      foreach (DataRow row in table.Rows) {
         foreach (DataColumn col in table.Columns) {
            if (col.DataType.Equals(typeof(DateTime)))
               Console.Write("{0,-14:d}", row[col]);
            else if (col.DataType.Equals(typeof(Decimal)))
               Console.Write("{0,-14:C}", row[col]);
            else
               Console.Write("{0,-14}", row[col]);
         }
         Console.WriteLine("{0,-14}", row.RowState);
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="dd838-178">另請參閱</span><span class="sxs-lookup"><span data-stu-id="dd838-178">See also</span></span>

- [<span data-ttu-id="dd838-179">DataAdapter 和 DataReader</span><span class="sxs-lookup"><span data-stu-id="dd838-179">DataAdapters and DataReaders</span></span>](dataadapters-and-datareaders.md)
- [<span data-ttu-id="dd838-180">資料列狀態和資料列版本</span><span class="sxs-lookup"><span data-stu-id="dd838-180">Row States and Row Versions</span></span>](./dataset-datatable-dataview/row-states-and-row-versions.md)
- [<span data-ttu-id="dd838-181">AcceptChanges 和 RejectChanges</span><span class="sxs-lookup"><span data-stu-id="dd838-181">AcceptChanges and RejectChanges</span></span>](./dataset-datatable-dataview/acceptchanges-and-rejectchanges.md)
- [<span data-ttu-id="dd838-182">合併 DataSet 內容</span><span class="sxs-lookup"><span data-stu-id="dd838-182">Merging DataSet Contents</span></span>](./dataset-datatable-dataview/merging-dataset-contents.md)
- [<span data-ttu-id="dd838-183">擷取身分識別或自動編號值</span><span class="sxs-lookup"><span data-stu-id="dd838-183">Retrieving Identity or Autonumber Values</span></span>](retrieving-identity-or-autonumber-values.md)
- <span data-ttu-id="dd838-184">[ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)</span><span class="sxs-lookup"><span data-stu-id="dd838-184">[ADO.NET Overview](ado-net-overview.md)</span></span>
