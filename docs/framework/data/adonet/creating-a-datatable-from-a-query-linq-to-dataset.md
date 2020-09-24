---
title: 從查詢建立 DataTable (LINQ to DataSet)
description: 瞭解如何使用 CopyToDataTable 方法來取得查詢的結果，並將資料複製到 DataTable 中，以便用於資料系結。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1b97afeb-03f8-41e2-8eb3-58aff65f7d18
ms.openlocfilehash: 064688f173e375481373e9a33d66c64666e1583f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91148357"
---
# <a name="creating-a-datatable-from-a-query-linq-to-dataset"></a><span data-ttu-id="256e5-103">從查詢建立 DataTable (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="256e5-103">Creating a DataTable From a Query (LINQ to DataSet)</span></span>

<span data-ttu-id="256e5-104">資料繫結 (Data Binding) 是 <xref:System.Data.DataTable> 物件的常見用法。</span><span class="sxs-lookup"><span data-stu-id="256e5-104">Data binding is a common use of <xref:System.Data.DataTable> object.</span></span> <span data-ttu-id="256e5-105"><xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法會採用查詢的結果並將資料複製到 <xref:System.Data.DataTable> 中，然後此物件便可用於資料繫結。</span><span class="sxs-lookup"><span data-stu-id="256e5-105">The <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> method takes the results of a query and copies the data into a <xref:System.Data.DataTable>, which can then be used for data binding.</span></span> <span data-ttu-id="256e5-106">執行了資料作業之後，新的 <xref:System.Data.DataTable> 就會合併回來源 <xref:System.Data.DataTable> 中。</span><span class="sxs-lookup"><span data-stu-id="256e5-106">When the data operations have been performed, the new <xref:System.Data.DataTable> is merged back into the source <xref:System.Data.DataTable>.</span></span>  
  
 <span data-ttu-id="256e5-107"><xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法會使用下列程序，從查詢中建立 <xref:System.Data.DataTable>：</span><span class="sxs-lookup"><span data-stu-id="256e5-107">The <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> method uses the following process to create a <xref:System.Data.DataTable> from a query:</span></span>  
  
1. <span data-ttu-id="256e5-108"><xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法會從來源資料表 (實作 <xref:System.Data.DataTable> 介面的 <xref:System.Data.DataTable> 物件) 中複製 (Clone) <xref:System.Linq.IQueryable%601>。</span><span class="sxs-lookup"><span data-stu-id="256e5-108">The <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> method clones a <xref:System.Data.DataTable> from the source table (a <xref:System.Data.DataTable> object that implements the <xref:System.Linq.IQueryable%601> interface).</span></span> <span data-ttu-id="256e5-109"><xref:System.Collections.IEnumerable>來源通常是源自 LINQ to DataSet 運算式或方法查詢。</span><span class="sxs-lookup"><span data-stu-id="256e5-109">The <xref:System.Collections.IEnumerable> source has generally originated from a LINQ to DataSet expression or method query.</span></span>  
  
2. <span data-ttu-id="256e5-110">複製的 <xref:System.Data.DataTable> 結構描述是根據來源資料表中第一個列舉 <xref:System.Data.DataRow> 物件的資料行所建立，而且複製之資料表的名稱就是來源資料表的名稱並附加上 "query" 一字。</span><span class="sxs-lookup"><span data-stu-id="256e5-110">The schema of the cloned <xref:System.Data.DataTable> is built from the columns of the first enumerated <xref:System.Data.DataRow> object in the source table and the name of the cloned table is the name of the source table with the word "query" appended to it.</span></span>  
  
3. <span data-ttu-id="256e5-111">若為來源資料表中的每個資料列，資料列的內容會複製到新的 <xref:System.Data.DataRow> 物件中，然後該物件便插入複製的資料表中。</span><span class="sxs-lookup"><span data-stu-id="256e5-111">For each row in the source table, the content of the row is copied into a new <xref:System.Data.DataRow> object, which is then inserted into the cloned table.</span></span> <span data-ttu-id="256e5-112">在複製作業中，<xref:System.Data.DataRow.RowState%2A> 和 <xref:System.Data.DataRow.RowError%2A> 屬性會保留下來。</span><span class="sxs-lookup"><span data-stu-id="256e5-112">The <xref:System.Data.DataRow.RowState%2A> and <xref:System.Data.DataRow.RowError%2A> properties are preserved across the copy operation.</span></span> <span data-ttu-id="256e5-113">如果來源中的 <xref:System.ArgumentException> 物件來自於不同的資料表，系統就會擲回 <xref:System.Data.DataRow>。</span><span class="sxs-lookup"><span data-stu-id="256e5-113">An <xref:System.ArgumentException> is thrown if the <xref:System.Data.DataRow> objects in the source are from different tables.</span></span>  
  
4. <span data-ttu-id="256e5-114">在輸入可查詢資料表中的所有 <xref:System.Data.DataTable> 物件都已經複製之後，就會傳回複製的 <xref:System.Data.DataRow>。</span><span class="sxs-lookup"><span data-stu-id="256e5-114">The cloned <xref:System.Data.DataTable> is returned after all <xref:System.Data.DataRow> objects in the input queryable table have been copied.</span></span> <span data-ttu-id="256e5-115">如果來源序列 (Sequence) 沒有包含任何 <xref:System.Data.DataRow> 物件，此方法就會傳回空的 <xref:System.Data.DataTable>。</span><span class="sxs-lookup"><span data-stu-id="256e5-115">If the source sequence does not contain any <xref:System.Data.DataRow> objects, the method returns an empty <xref:System.Data.DataTable>.</span></span>  
  
<span data-ttu-id="256e5-116">呼叫 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法會導致系結至來源資料表的查詢執行。</span><span class="sxs-lookup"><span data-stu-id="256e5-116">Calling the <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> method causes the query bound to the source table to execute.</span></span>  
  
 <span data-ttu-id="256e5-117">當 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法在來源資料表的資料列中遇到 Null 參考或可為 Null 的實值型別 (Value Type) 時，它會將此值取代成 <xref:System.DBNull.Value>。</span><span class="sxs-lookup"><span data-stu-id="256e5-117">When the <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> method encounters either a null reference or nullable value type in a row in the source table, it replaces the value with <xref:System.DBNull.Value>.</span></span> <span data-ttu-id="256e5-118">如此一來，傳回之 <xref:System.Data.DataTable> 中的 Null 值都會經過正確處理。</span><span class="sxs-lookup"><span data-stu-id="256e5-118">This way, null values are handled correctly in the returned <xref:System.Data.DataTable>.</span></span>  
  
 <span data-ttu-id="256e5-119">注意：<xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法會接受可從多個 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 物件傳回資料列的查詢當做輸入。</span><span class="sxs-lookup"><span data-stu-id="256e5-119">Note: The <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> method accepts as input a query that can return rows from multiple <xref:System.Data.DataTable> or <xref:System.Data.DataSet> objects.</span></span> <span data-ttu-id="256e5-120"><xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法會將資料 (但不包含屬性) 從來源 <xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 物件複製到傳回的 <xref:System.Data.DataTable>。</span><span class="sxs-lookup"><span data-stu-id="256e5-120">The <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> method will copy the data but not the properties from the source <xref:System.Data.DataTable> or <xref:System.Data.DataSet> objects to the returned <xref:System.Data.DataTable>.</span></span> <span data-ttu-id="256e5-121">您必須針對傳回的 <xref:System.Data.DataTable> 明確設定屬性，例如 <xref:System.Data.DataTable.Locale%2A> 和 <xref:System.Data.DataTable.TableName%2A>。</span><span class="sxs-lookup"><span data-stu-id="256e5-121">You will need to explicitly set the properties on the returned <xref:System.Data.DataTable>, such as <xref:System.Data.DataTable.Locale%2A> and <xref:System.Data.DataTable.TableName%2A>.</span></span>  
  
 <span data-ttu-id="256e5-122">下列範例將在 SalesOrderHeader 資料表中查詢是否有 2001 年 8 月 8 日之後的訂單，然後使用 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法，從該查詢中建立 <xref:System.Data.DataTable>。</span><span class="sxs-lookup"><span data-stu-id="256e5-122">The following example queries the SalesOrderHeader table for orders after August 8, 2001 and uses the <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> method to create a <xref:System.Data.DataTable> from that query.</span></span> <span data-ttu-id="256e5-123">接著，<xref:System.Data.DataTable> 便繫結至 <xref:System.Windows.Forms.BindingSource>，而它會當做 <xref:System.Windows.Forms.DataGridView> 的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="256e5-123">The <xref:System.Data.DataTable> is then bound to a <xref:System.Windows.Forms.BindingSource>, which acts as proxy for a <xref:System.Windows.Forms.DataGridView>.</span></span>  
  
 [!code-csharp[DP LINQ to DataSet Examples#CopyToDataTable1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#copytodatatable1)]
 [!code-vb[DP LINQ to DataSet Examples#CopyToDataTable1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#copytodatatable1)]  
  
## <a name="creating-a-custom-copytodatatablet-method"></a><span data-ttu-id="256e5-124">建立自訂 CopyToDataTable \<T> 方法</span><span class="sxs-lookup"><span data-stu-id="256e5-124">Creating a Custom CopyToDataTable\<T> Method</span></span>  

 <span data-ttu-id="256e5-125">現有的 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法只能在通用參數 <xref:System.Collections.Generic.IEnumerable%601> 為 `T` 型別的<xref:System.Data.DataRow> 來源上運作。</span><span class="sxs-lookup"><span data-stu-id="256e5-125">The existing <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> methods only operate on an <xref:System.Collections.Generic.IEnumerable%601> source where the generic parameter `T` is of type <xref:System.Data.DataRow>.</span></span> <span data-ttu-id="256e5-126">雖然這樣非常有用，但是資料表卻無法從一序列的純量型別、傳回匿名型別的查詢或執行資料表聯結的查詢建立。</span><span class="sxs-lookup"><span data-stu-id="256e5-126">Although this is useful, it does not allow tables to be created from a sequence of scalar types, from queries that return anonymous types, or from queries that perform table joins.</span></span> <span data-ttu-id="256e5-127">如需如何實作為從純量或匿名型別順序載入資料表的兩個自訂方法的範例 `CopyToDataTable` ，請參閱 [如何：實 CopyToDataTable， \<T> 其中泛型型別 T 不是 DataRow](implement-copytodatatable-where-type-not-a-datarow.md)s。</span><span class="sxs-lookup"><span data-stu-id="256e5-127">For an example of how to implement two custom `CopyToDataTable` methods that load a table from a sequence of scalar or anonymous types, see [How to: Implement CopyToDataTable\<T> Where the Generic Type T Is Not a DataRow](implement-copytodatatable-where-type-not-a-datarow.md)s.</span></span>  
  
 <span data-ttu-id="256e5-128">本節的範例都使用以下自訂型別：</span><span class="sxs-lookup"><span data-stu-id="256e5-128">The examples in this section use the following custom types:</span></span>  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#ItemClass](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#itemclass)]
 [!code-vb[DP Custom CopyToDataTable Examples#ItemClass](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#itemclass)]  
  
### <a name="example"></a><span data-ttu-id="256e5-129">範例</span><span class="sxs-lookup"><span data-stu-id="256e5-129">Example</span></span>  

 <span data-ttu-id="256e5-130">此範例會執行 `SalesOrderHeader` 和 `SalesOrderDetail` 資料表的聯結，以取得八月的線上訂單資訊並根據此查詢建立資料表。</span><span class="sxs-lookup"><span data-stu-id="256e5-130">This example performs a join over the `SalesOrderHeader` and `SalesOrderDetail` tables to get online orders from the month of August and creates a table from the query.</span></span>  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#Join](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#join)]
 [!code-vb[DP Custom CopyToDataTable Examples#Join](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#join)]  
  
### <a name="example"></a><span data-ttu-id="256e5-131">範例</span><span class="sxs-lookup"><span data-stu-id="256e5-131">Example</span></span>  

 <span data-ttu-id="256e5-132">下列範例會查詢集合中價格大於 $9.99 的項目，並根據查詢結果建立資料表。</span><span class="sxs-lookup"><span data-stu-id="256e5-132">The following example queries a collection for items of price greater than $9.99 and creates a table from the query results.</span></span>  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsIntoTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsintotable)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsIntoTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsintotable)]  
  
### <a name="example"></a><span data-ttu-id="256e5-133">範例</span><span class="sxs-lookup"><span data-stu-id="256e5-133">Example</span></span>  

 <span data-ttu-id="256e5-134">下列範例會查詢集合中價格大於 $9.99 的項目並擲回結果。</span><span class="sxs-lookup"><span data-stu-id="256e5-134">The following example queries a collection for items of price greater than 9.99 and projects the results.</span></span> <span data-ttu-id="256e5-135">所傳回的匿名型別序列就會載入到現有的資料表中。</span><span class="sxs-lookup"><span data-stu-id="256e5-135">The returned sequence of anonymous types is loaded into an existing table.</span></span>  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsIntoExistingTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsintoexistingtable)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsIntoExistingTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsintoexistingtable)]  
  
### <a name="example"></a><span data-ttu-id="256e5-136">範例</span><span class="sxs-lookup"><span data-stu-id="256e5-136">Example</span></span>  

 <span data-ttu-id="256e5-137">下列範例會查詢集合中價格大於 $9.99 的項目並擲回結果。</span><span class="sxs-lookup"><span data-stu-id="256e5-137">The following example queries a collection for items of price greater than $9.99 and projects the results.</span></span> <span data-ttu-id="256e5-138">所傳回的匿名型別序列就會載入到現有的資料表中。</span><span class="sxs-lookup"><span data-stu-id="256e5-138">The returned sequence of anonymous types is loaded into an existing table.</span></span> <span data-ttu-id="256e5-139">因為 `Book` 和 `Movies` 型別是衍生自 `Item` 型別，所以資料表結構描述會自動展開。</span><span class="sxs-lookup"><span data-stu-id="256e5-139">The table schema is automatically expanded because the `Book` and `Movies` types are derived from the `Item` type.</span></span>  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadItemsExpandSchema](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loaditemsexpandschema)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadItemsExpandSchema](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loaditemsexpandschema)]  
  
### <a name="example"></a><span data-ttu-id="256e5-140">範例</span><span class="sxs-lookup"><span data-stu-id="256e5-140">Example</span></span>  

 <span data-ttu-id="256e5-141">下列範例會查詢集合中價格大於 $9.99 的項目並傳回結果 <xref:System.Double> 序列，這序列會在入到新資料表中。</span><span class="sxs-lookup"><span data-stu-id="256e5-141">The following example queries a collection for items of price greater than $9.99 and returns a sequence of <xref:System.Double>, which is loaded into a new table.</span></span>  
  
 [!code-csharp[DP Custom CopyToDataTable Examples#LoadScalarSequence](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#loadscalarsequence)]
 [!code-vb[DP Custom CopyToDataTable Examples#LoadScalarSequence](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#loadscalarsequence)]  
  
## <a name="see-also"></a><span data-ttu-id="256e5-142">另請參閱</span><span class="sxs-lookup"><span data-stu-id="256e5-142">See also</span></span>

- [<span data-ttu-id="256e5-143">程式設計指南</span><span class="sxs-lookup"><span data-stu-id="256e5-143">Programming Guide</span></span>](programming-guide-linq-to-dataset.md)
- [<span data-ttu-id="256e5-144">泛型 Field 和 SetField 方法</span><span class="sxs-lookup"><span data-stu-id="256e5-144">Generic Field and SetField Methods</span></span>](generic-field-and-setfield-methods-linq-to-dataset.md)
- [<span data-ttu-id="256e5-145">LINQ to DataSet 範例</span><span class="sxs-lookup"><span data-stu-id="256e5-145">LINQ to DataSet Examples</span></span>](linq-to-dataset-examples.md)
