---
title: 建立 DataView 物件 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 76057508-e12d-4779-a707-06a4c2568acf
ms.openlocfilehash: f76574a912128918ed575cbf0eca892041dc354c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91148317"
---
# <a name="creating-a-dataview-object-linq-to-dataset"></a><span data-ttu-id="3d5bf-102">建立 DataView 物件 (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="3d5bf-102">Creating a DataView Object (LINQ to DataSet)</span></span>

<span data-ttu-id="3d5bf-103">有兩種方式可以 <xref:System.Data.DataView> 在 LINQ to DataSet 內容中建立。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-103">There are two ways to create a <xref:System.Data.DataView> in the LINQ to DataSet context.</span></span> <span data-ttu-id="3d5bf-104">您可以 <xref:System.Data.DataView> 從 LINQ to DataSet 查詢建立，也可以從具型別或不具類型的查詢 <xref:System.Data.DataTable> 建立 <xref:System.Data.DataTable> 。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-104">You can create a <xref:System.Data.DataView> from a LINQ to DataSet query over a <xref:System.Data.DataTable>, or you can create it from a typed or un-typed <xref:System.Data.DataTable>.</span></span> <span data-ttu-id="3d5bf-105">在這兩種情況下，您可以 <xref:System.Data.DataView> 使用其中一個擴充方法來建立，而 <xref:System.Data.DataTableExtensions.AsDataView%2A> <xref:System.Data.DataView> 不會在 LINQ to DataSet 內容中直接可建構。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-105">In both cases, you create the <xref:System.Data.DataView> by using one of the <xref:System.Data.DataTableExtensions.AsDataView%2A> extension methods; <xref:System.Data.DataView> is not directly constructible in the LINQ to DataSet context.</span></span>  
  
 <span data-ttu-id="3d5bf-106">在您已經建立 <xref:System.Data.DataView> 之後，就可以將它繫結程序至 Windows Forms 應用程式或 ASP.NET 應用程式中的 UI 控制項，也可以變更篩選和排序設定。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-106">After the <xref:System.Data.DataView> has been created, you can bind it to a UI control in a Windows forms application or an ASP.NET application, or change the filtering and sorting settings.</span></span>  
  
 <span data-ttu-id="3d5bf-107"><xref:System.Data.DataView> 會建構索引，以便大幅增加可使用索引之作業的效能，例如篩選和排序。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-107"><xref:System.Data.DataView> constructs an index, which significantly increases the performance of operations that can use the index, such as filtering and sorting.</span></span> <span data-ttu-id="3d5bf-108">在您建立 <xref:System.Data.DataView> 以及修改任何排序或篩選資訊時，系統就會建立 <xref:System.Data.DataView> 的索引。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-108">The index for a <xref:System.Data.DataView> is built both when the <xref:System.Data.DataView> is created and when any of the sorting or filtering information is modified.</span></span> <span data-ttu-id="3d5bf-109">如果您建立 <xref:System.Data.DataView>，然後設定排序或篩選資訊，將會導致系統至少建立索引兩次：一次是建立 <xref:System.Data.DataView> 時，另一次是修改任何排序或篩選屬性時。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-109">Creating a <xref:System.Data.DataView> and then setting the sorting or filtering information later causes the index to be built at least twice: once when the <xref:System.Data.DataView> is created, and again when any of the sort or filter properties are modified.</span></span>  
  
 <span data-ttu-id="3d5bf-110">如需有關篩選和排序的詳細資訊 <xref:System.Data.DataView> ，請參閱使用 dataview 進行 [篩選](filtering-with-dataview-linq-to-dataset.md) 和 [排序](sorting-with-dataview-linq-to-dataset.md)。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-110">For more information about filtering and sorting with <xref:System.Data.DataView>, see [Filtering with DataView](filtering-with-dataview-linq-to-dataset.md) and [Sorting with DataView](sorting-with-dataview-linq-to-dataset.md).</span></span>  
  
## <a name="creating-dataview-from-a-linq-to-dataset-query"></a><span data-ttu-id="3d5bf-111">從 LINQ to DataSet 查詢中建立 DataView</span><span class="sxs-lookup"><span data-stu-id="3d5bf-111">Creating DataView from a LINQ to DataSet Query</span></span>  

 <span data-ttu-id="3d5bf-112">您 <xref:System.Data.DataView> 可以從 LINQ to DataSet 查詢的結果建立物件，其中結果是物件的投射 <xref:System.Data.DataRow> 。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-112">A <xref:System.Data.DataView> object can be created from the results of a LINQ to DataSet query, where the results are a projection of <xref:System.Data.DataRow> objects.</span></span> <span data-ttu-id="3d5bf-113">新建立的 <xref:System.Data.DataView> 會從建立此物件的查詢中繼承篩選和排序資訊。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-113">The newly created <xref:System.Data.DataView> inherits the filtering and sorting information from the query it is created from.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="3d5bf-114">在大部分清況中，用於篩選和排序的運算式不應該具有副作用 (Side Effect) 而且必須具決定性。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-114">In most cases, the expressions used for filtering and sorting should not have side effects and must be deterministic.</span></span> <span data-ttu-id="3d5bf-115">此外，這些運算式不應該包含取決於固定執行次數的任何邏輯，因為排序和篩選作業可能會執行任何次數。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-115">Also, the expressions should not contain any logic that depend on a set number of executions, as the sorting and filtering operations may be executed any number of times.</span></span>  
  
 <span data-ttu-id="3d5bf-116">目前不支援從傳回匿名型別的查詢或執行聯結 (Join) 作業的查詢中建立 <xref:System.Data.DataView>。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-116">Creating a <xref:System.Data.DataView> from a query that returns anonymous types or queries that perform join operations is not supported.</span></span>  
  
 <span data-ttu-id="3d5bf-117">在用來建立 <xref:System.Data.DataView> 的查詢中只支援使用下列查詢運算子：</span><span class="sxs-lookup"><span data-stu-id="3d5bf-117">Only the following query operators are supported in a query used to create <xref:System.Data.DataView>:</span></span>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Cast%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.OrderBy%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.OrderByDescending%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Select%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.ThenBy%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.ThenByDescending%2A>  
  
- <xref:System.Data.EnumerableRowCollectionExtensions.Where%2A>  
  
 <span data-ttu-id="3d5bf-118">請注意，當 <xref:System.Data.DataView> 從 LINQ to DataSet 查詢建立時， <xref:System.Data.EnumerableRowCollectionExtensions.Select%2A> 方法必須是查詢中所呼叫的最後一個方法。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-118">Note that when a <xref:System.Data.DataView> is created from a LINQ to DataSet query the <xref:System.Data.EnumerableRowCollectionExtensions.Select%2A> method must be the final method called in the query.</span></span> <span data-ttu-id="3d5bf-119">這會顯示在下列範例中，它會建立 <xref:System.Data.DataView> 依 total total 排序的線上訂單：</span><span class="sxs-lookup"><span data-stu-id="3d5bf-119">This is shown in the following example, which creates a <xref:System.Data.DataView> of online orders sorted by total due:</span></span>  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQuery1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquery1)]
 [!code-vb[DP DataView Samples#CreateLDVFromQuery1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquery1)]  
  
 <span data-ttu-id="3d5bf-120">從查詢建立之後，您也可以使用 <xref:System.Data.DataView.RowFilter%2A> 以字串為基礎和 <xref:System.Data.DataView.Sort%2A> 屬性來篩選和排序 <xref:System.Data.DataView> 。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-120">You can also use the string-based <xref:System.Data.DataView.RowFilter%2A> and <xref:System.Data.DataView.Sort%2A> properties to filter and sort a <xref:System.Data.DataView> after it has been created from a query.</span></span> <span data-ttu-id="3d5bf-121">請注意，這樣做會清除繼承自查詢的排序和篩選資訊。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-121">Note that this will clear the sorting and filtering information inherited from the query.</span></span> <span data-ttu-id="3d5bf-122">下列範例 <xref:System.Data.DataView> 會從 LINQ to DataSet 查詢建立，此查詢會依姓氏開頭為 ' ' 的名稱進行篩選。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-122">The following example creates a <xref:System.Data.DataView> from a LINQ to DataSet query that filters by last names that start with 'S'.</span></span> <span data-ttu-id="3d5bf-123">以字串為基礎的 <xref:System.Data.DataView.Sort%2A> 屬性會設定為按照遞增順序排序姓氏，然後再按照遞減順序排序名字：</span><span class="sxs-lookup"><span data-stu-id="3d5bf-123">The string-based <xref:System.Data.DataView.Sort%2A> property is set to sort on last names in ascending order and then first names in descending order:</span></span>  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromquerystringsort)]
 [!code-vb[DP DataView Samples#CreateLDVFromQueryStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromquerystringsort)]  
  
## <a name="creating-a-dataview-from-a-datatable"></a><span data-ttu-id="3d5bf-124">從 DataTable 中建立 DataView</span><span class="sxs-lookup"><span data-stu-id="3d5bf-124">Creating a DataView from a DataTable</span></span>  

 <span data-ttu-id="3d5bf-125">除了從 LINQ to DataSet 查詢建立之外，您 <xref:System.Data.DataView> 也可以使用方法，從建立物件 <xref:System.Data.DataTable> <xref:System.Data.DataTableExtensions.AsDataView%2A> 。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-125">In addition to being created from a LINQ to DataSet query, a <xref:System.Data.DataView> object can be created from a <xref:System.Data.DataTable> by using the <xref:System.Data.DataTableExtensions.AsDataView%2A> method.</span></span>  
  
 <span data-ttu-id="3d5bf-126">下列範例會從 SalesOrderDetail 資料表中建立 <xref:System.Data.DataView>，然後將它設定為 <xref:System.Windows.Forms.BindingSource> 物件的資料來源。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-126">The following example creates a <xref:System.Data.DataView> from the SalesOrderDetail table and sets it as the data source of a <xref:System.Windows.Forms.BindingSource> object.</span></span> <span data-ttu-id="3d5bf-127">這個物件會當做 <xref:System.Windows.Forms.DataGridView> 控制項的 Proxy。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-127">This object acts as a proxy for a <xref:System.Windows.Forms.DataGridView> control.</span></span>  
  
 [!code-csharp[DP DataView Samples#CreateLDVFromTable](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#createldvfromtable)]
 [!code-vb[DP DataView Samples#CreateLDVFromTable](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#createldvfromtable)]  
  
 <span data-ttu-id="3d5bf-128">在您已經從 <xref:System.Data.DataView> 中建立 <xref:System.Data.DataTable> 之後，就可以針對它設定篩選和排序。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-128">Filtering and sorting can be set on the <xref:System.Data.DataView> after it has been created from a <xref:System.Data.DataTable>.</span></span> <span data-ttu-id="3d5bf-129">下列範例會從 Contact 資料表中建立 <xref:System.Data.DataView> 並將 <xref:System.Data.DataView.Sort%2A> 屬性設定為按照遞增順序排序姓氏，然後再按照遞減順序排序名字：</span><span class="sxs-lookup"><span data-stu-id="3d5bf-129">The following example creates a <xref:System.Data.DataView> from the Contact table and sets the <xref:System.Data.DataView.Sort%2A> property to sort on last names in ascending order and then first names in descending order:</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVStringSort](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvstringsort)]
 [!code-vb[DP DataView Samples#LDVStringSort](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvstringsort)]  
  
 <span data-ttu-id="3d5bf-130">不過，在您已經從查詢中建立 <xref:System.Data.DataView.RowFilter%2A> 之後設定 <xref:System.Data.DataView.Sort%2A> 或 <xref:System.Data.DataView> 屬性會發生效能降低的情況，因為 <xref:System.Data.DataView> 會建構索引來支援篩選和排序作業。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-130">However, there is a performance loss that comes with setting the <xref:System.Data.DataView.RowFilter%2A> or <xref:System.Data.DataView.Sort%2A> property after the <xref:System.Data.DataView> has been created from a query, because <xref:System.Data.DataView> constructs an index to support filtering and sorting operations.</span></span> <span data-ttu-id="3d5bf-131">設定 <xref:System.Data.DataView.RowFilter%2A> 或 <xref:System.Data.DataView.Sort%2A> 屬性會重建資料索引，因而增加應用程式的負荷並降低效能。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-131">Setting the <xref:System.Data.DataView.RowFilter%2A> or <xref:System.Data.DataView.Sort%2A> property rebuilds the index for the data, adding overhead to your application and decreasing performance.</span></span> <span data-ttu-id="3d5bf-132">如果可能的話，最好是在您首次建立 <xref:System.Data.DataView> 時指定篩選和排序資訊，並且避免之後修改這項資訊。</span><span class="sxs-lookup"><span data-stu-id="3d5bf-132">When possible, it is better to specify the filtering and sorting information when you first create the <xref:System.Data.DataView> and avoid modifying it afterwards.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3d5bf-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3d5bf-133">See also</span></span>

- [<span data-ttu-id="3d5bf-134">資料繫結和 LINQ to DataSet</span><span class="sxs-lookup"><span data-stu-id="3d5bf-134">Data Binding and LINQ to DataSet</span></span>](data-binding-and-linq-to-dataset.md)
- [<span data-ttu-id="3d5bf-135">使用 DataView 進行篩選</span><span class="sxs-lookup"><span data-stu-id="3d5bf-135">Filtering with DataView</span></span>](filtering-with-dataview-linq-to-dataset.md)
- [<span data-ttu-id="3d5bf-136">使用 DataView 進行排序</span><span class="sxs-lookup"><span data-stu-id="3d5bf-136">Sorting with DataView</span></span>](sorting-with-dataview-linq-to-dataset.md)
