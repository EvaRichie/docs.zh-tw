---
title: 使用 DataView 進行篩選 (LINQ to DataSet)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5632d74a-ff53-4ea7-9fe7-4a148eeb1c68
ms.openlocfilehash: 9b4c8e9730dde7d19df9e6a11052ae4591465ea7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177458"
---
# <a name="filtering-with-dataview-linq-to-dataset"></a><span data-ttu-id="b8f25-102">使用 DataView 進行篩選 (LINQ to DataSet)</span><span class="sxs-lookup"><span data-stu-id="b8f25-102">Filtering with DataView (LINQ to DataSet)</span></span>

<span data-ttu-id="b8f25-103">使用特定準則來篩選資料，然後透過 UI 控制項呈現資料給用戶端的功能是資料繫結的重要層面。</span><span class="sxs-lookup"><span data-stu-id="b8f25-103">The ability to filter data using specific criteria and then present the data to a client through a UI control is an important aspect of data binding.</span></span> <span data-ttu-id="b8f25-104"><xref:System.Data.DataView> 提供了許多方式來篩選資料並傳回符合特定篩選準則的資料列子集。</span><span class="sxs-lookup"><span data-stu-id="b8f25-104"><xref:System.Data.DataView> provides several ways to filter data and return subsets of data rows meeting specific filter criteria.</span></span> <span data-ttu-id="b8f25-105">除了以字串為基礎的篩選功能之外， <xref:System.Data.DataView> 也提供將 LINQ 運算式用於篩選準則的功能。</span><span class="sxs-lookup"><span data-stu-id="b8f25-105">In addition to the string-based filtering capabilities, <xref:System.Data.DataView> also provides the ability to use LINQ expressions for the filtering criteria.</span></span> <span data-ttu-id="b8f25-106">LINQ 運算式允許比以字串為基礎的篩選更為複雜且功能強大的篩選作業。</span><span class="sxs-lookup"><span data-stu-id="b8f25-106">LINQ expressions allow for much more complex and powerful filtering operations than the string-based filtering.</span></span>  
  
 <span data-ttu-id="b8f25-107">目前有兩種方式可以使用 <xref:System.Data.DataView> 來篩選資料：</span><span class="sxs-lookup"><span data-stu-id="b8f25-107">There are two ways to filter data using a <xref:System.Data.DataView>:</span></span>  
  
- <span data-ttu-id="b8f25-108"><xref:System.Data.DataView>使用 Where 子句從 LINQ to DataSet 查詢建立。</span><span class="sxs-lookup"><span data-stu-id="b8f25-108">Create a <xref:System.Data.DataView> from a LINQ to DataSet query with a Where clause.</span></span>  
  
- <span data-ttu-id="b8f25-109">使用 <xref:System.Data.DataView> 現有的以字串為基礎的篩選功能。</span><span class="sxs-lookup"><span data-stu-id="b8f25-109">Use the existing, string-based filtering capabilities of <xref:System.Data.DataView>.</span></span>  
  
## <a name="creating-dataview-from-a-query-with-filtering-information"></a><span data-ttu-id="b8f25-110">從含有篩選資訊的查詢中建立 DataView</span><span class="sxs-lookup"><span data-stu-id="b8f25-110">Creating DataView from a Query with Filtering Information</span></span>  

 <span data-ttu-id="b8f25-111">您 <xref:System.Data.DataView> 可以從 LINQ to DataSet 查詢建立物件。</span><span class="sxs-lookup"><span data-stu-id="b8f25-111">A <xref:System.Data.DataView> object can be created from a LINQ to DataSet query.</span></span> <span data-ttu-id="b8f25-112">如果該查詢包含 `Where` 子句，<xref:System.Data.DataView> 就是使用查詢的篩選資訊建立的。</span><span class="sxs-lookup"><span data-stu-id="b8f25-112">If that query contains a `Where` clause, the <xref:System.Data.DataView> is created with the filtering information from the query.</span></span> <span data-ttu-id="b8f25-113">`Where` 子句中的運算式可用來決定哪些資料列將包含在 <xref:System.Data.DataView> 中，而且它是篩選的基礎。</span><span class="sxs-lookup"><span data-stu-id="b8f25-113">The expression in the `Where` clause is used to determine which data rows will be included in the <xref:System.Data.DataView>, and is the basis for the filter.</span></span>  
  
 <span data-ttu-id="b8f25-114">以運算式為基礎的篩選會比較簡單的以字串為基礎的篩選提供功能更強大且更複雜的篩選。</span><span class="sxs-lookup"><span data-stu-id="b8f25-114">Expression-based filters offer more powerful and complex filtering than the simpler string-based filters.</span></span> <span data-ttu-id="b8f25-115">以字串為基礎的篩選和以運算式為基礎的篩選會互斥。</span><span class="sxs-lookup"><span data-stu-id="b8f25-115">The string-based and expression-based filters are mutually exclusive.</span></span> <span data-ttu-id="b8f25-116">如果您從查詢中建立 <xref:System.Data.DataView.RowFilter%2A> 之後才設定以字串為基礎的 <xref:System.Data.DataView>，就會清除從查詢中推斷的以運算式為基礎的篩選。</span><span class="sxs-lookup"><span data-stu-id="b8f25-116">When the string-based <xref:System.Data.DataView.RowFilter%2A> is set after a <xref:System.Data.DataView> is created from a query, the expression based filter inferred from the query is cleared.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="b8f25-117">在大部分清況中，用於篩選的運算式不應該具有副作用 (Side Effect) 而且必須具決定性。</span><span class="sxs-lookup"><span data-stu-id="b8f25-117">In most cases, the expressions used for filtering should not have side effects and must be deterministic.</span></span> <span data-ttu-id="b8f25-118">此外，這些運算式不應該包含取決於固定執行次數的任何邏輯，因為篩選作業可能會執行任何次數。</span><span class="sxs-lookup"><span data-stu-id="b8f25-118">Also, the expressions should not contain any logic that depends on a set number of executions, because the filtering operations might be executed any number of times.</span></span>  
  
### <a name="example"></a><span data-ttu-id="b8f25-119">範例</span><span class="sxs-lookup"><span data-stu-id="b8f25-119">Example</span></span>  

 <span data-ttu-id="b8f25-120">下列範例會在 SalesOrderDetail 資料表中查詢是否有數量大於 2 而小於 6 的訂單、從該查詢中建立 <xref:System.Data.DataView>，然後將 <xref:System.Data.DataView> 繫結至 <xref:System.Windows.Forms.BindingSource>：</span><span class="sxs-lookup"><span data-stu-id="b8f25-120">The following example queries the SalesOrderDetail table for orders with a quantity greater than 2 and less than 6; creates a <xref:System.Data.DataView> from that query; and binds the <xref:System.Data.DataView> to a <xref:System.Windows.Forms.BindingSource>:</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere)]  
  
### <a name="example"></a><span data-ttu-id="b8f25-121">範例</span><span class="sxs-lookup"><span data-stu-id="b8f25-121">Example</span></span>  

 <span data-ttu-id="b8f25-122">下列範例會從 2001 年 6 月 6 日之後下單的訂單查詢中建立 <xref:System.Data.DataView>：</span><span class="sxs-lookup"><span data-stu-id="b8f25-122">The following example creates a <xref:System.Data.DataView> from a query for orders placed after June 6, 2001:</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhere3)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhere3](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhere3)]  
  
### <a name="example"></a><span data-ttu-id="b8f25-123">範例</span><span class="sxs-lookup"><span data-stu-id="b8f25-123">Example</span></span>  

 <span data-ttu-id="b8f25-124">篩選也可以與排序結合。</span><span class="sxs-lookup"><span data-stu-id="b8f25-124">Filtering can also be combined with sorting.</span></span> <span data-ttu-id="b8f25-125">下列範例會從姓氏以 "S" 為開頭並先依據姓氏，然後再依據名字排序的連絡人查詢中建立 <xref:System.Data.DataView>。</span><span class="sxs-lookup"><span data-stu-id="b8f25-125">The following example creates a <xref:System.Data.DataView> from a query for contacts whose last name start with "S" and sorted by last name, then first name:</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywhereorderbythenby)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereOrderByThenBy](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywhereorderbythenby)]  
  
### <a name="example"></a><span data-ttu-id="b8f25-126">範例</span><span class="sxs-lookup"><span data-stu-id="b8f25-126">Example</span></span>  

 <span data-ttu-id="b8f25-127">下列範例會使用 SoundEx 演算法來尋找姓氏類似於 "Zhu" 的連絡人。</span><span class="sxs-lookup"><span data-stu-id="b8f25-127">The following example uses the SoundEx algorithm to find contacts whose last name is similar to "Zhu".</span></span> <span data-ttu-id="b8f25-128">SoundEx 演算法是在 SoundEx 方法中實作的。</span><span class="sxs-lookup"><span data-stu-id="b8f25-128">The SoundEx algorithm is implemented in the SoundEx method.</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvsoundexfilter)]
 [!code-vb[DP DataView Samples#LDVSoundExFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvsoundexfilter)]  
  
 <span data-ttu-id="b8f25-129">SoundEx 是用於依據聲音索引名稱的語音演算法，而這些名稱都是以英文發音 (原本由美國人口普查局 (U.S. Census Bureau) 所開發)。</span><span class="sxs-lookup"><span data-stu-id="b8f25-129">SoundEx is a phonetic algorithm used for indexing names by sound, as they are pronounced in English, originally developed by the U.S. Census Bureau.</span></span> <span data-ttu-id="b8f25-130">SoundEx 方法會針對名稱傳回四個字元碼，其中包含一個英文字母，後面接著三個數字。</span><span class="sxs-lookup"><span data-stu-id="b8f25-130">The SoundEx method returns a four character code for a name consisting of an English letter followed by three numbers.</span></span> <span data-ttu-id="b8f25-131">該字母是名稱的第一個字母，而這些數字則編碼名稱中的其餘子音字母。</span><span class="sxs-lookup"><span data-stu-id="b8f25-131">The letter is the first letter of the name and the numbers encode the remaining consonants in the name.</span></span> <span data-ttu-id="b8f25-132">類似發音的名稱會共用相同的 SoundEx 代碼。</span><span class="sxs-lookup"><span data-stu-id="b8f25-132">Similar sounding names share the same SoundEx code.</span></span> <span data-ttu-id="b8f25-133">在先前範例之 SoundEx 方法中使用的 SoundEx 實作如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8f25-133">The SoundEx implementation used in the SoundEx method of the previous example is shown here:</span></span>  
  
 [!code-csharp[DP DataView Samples#SoundEx](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#soundex)]
 [!code-vb[DP DataView Samples#SoundEx](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#soundex)]  
  
## <a name="using-the-rowfilter-property"></a><span data-ttu-id="b8f25-134">使用 RowFilter 屬性</span><span class="sxs-lookup"><span data-stu-id="b8f25-134">Using the RowFilter Property</span></span>  

 <span data-ttu-id="b8f25-135">的現有字串型篩選功能仍可 <xref:System.Data.DataView> 在 LINQ to DataSet 內容中運作。</span><span class="sxs-lookup"><span data-stu-id="b8f25-135">The existing string-based filtering functionality of <xref:System.Data.DataView> still works in the LINQ to DataSet context.</span></span> <span data-ttu-id="b8f25-136">如需以字串為基礎之篩選的詳細資訊 <xref:System.Data.DataView.RowFilter%2A> ，請參閱 [排序和篩選資料](./dataset-datatable-dataview/sorting-and-filtering-data.md)。</span><span class="sxs-lookup"><span data-stu-id="b8f25-136">For more information about string-based <xref:System.Data.DataView.RowFilter%2A> filtering, see [Sorting and Filtering Data](./dataset-datatable-dataview/sorting-and-filtering-data.md).</span></span>  
  
 <span data-ttu-id="b8f25-137">下列範例會從 Contact 資料表中建立 <xref:System.Data.DataView>，然後設定 <xref:System.Data.DataView.RowFilter%2A> 屬性，以便傳回連絡人姓氏為 "Zhu" 的資料列：</span><span class="sxs-lookup"><span data-stu-id="b8f25-137">The following example creates a <xref:System.Data.DataView> from the Contact table and then sets the <xref:System.Data.DataView.RowFilter%2A> property to return rows where the contact's last name is "Zhu":</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvrowfilter)]
 [!code-vb[DP DataView Samples#LDVRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvrowfilter)]  
  
 <span data-ttu-id="b8f25-138"><xref:System.Data.DataView>從 <xref:System.Data.DataTable> 或 LINQ to DataSet 查詢建立之後，您可以使用 <xref:System.Data.DataView.RowFilter%2A> 屬性，根據資料行的資料行值來指定資料列的子集。</span><span class="sxs-lookup"><span data-stu-id="b8f25-138">After a <xref:System.Data.DataView> has been created from a <xref:System.Data.DataTable> or LINQ to DataSet query, you can use the <xref:System.Data.DataView.RowFilter%2A> property to specify subsets of rows based on their column values.</span></span> <span data-ttu-id="b8f25-139">以字串為基礎的篩選和以運算式為基礎的篩選會互斥。</span><span class="sxs-lookup"><span data-stu-id="b8f25-139">The string-based and expression-based filters are mutually exclusive.</span></span> <span data-ttu-id="b8f25-140">設定 <xref:System.Data.DataView.RowFilter%2A> 屬性將會清除從 LINQ to DataSet 查詢推斷的篩選運算式，而無法重設篩選運算式。</span><span class="sxs-lookup"><span data-stu-id="b8f25-140">Setting the <xref:System.Data.DataView.RowFilter%2A> property will clear the filter expression inferred from the LINQ to DataSet query, and the filter expression cannot be reset.</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromquerywheresetrowfilter)]
 [!code-vb[DP DataView Samples#LDVFromQueryWhereSetRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromquerywheresetrowfilter)]  
  
 <span data-ttu-id="b8f25-141">如果您想要傳回特定資料查詢的結果，但不要提供資料子集的動態檢視，就可以使用 <xref:System.Data.DataView.Find%2A> 的 <xref:System.Data.DataView.FindRows%2A> 或 <xref:System.Data.DataView> 方法，而非設定 <xref:System.Data.DataView.RowFilter%2A> 屬性。</span><span class="sxs-lookup"><span data-stu-id="b8f25-141">If you want to return the results of a particular query on the data, as opposed to providing a dynamic view of a subset of the data, you can use the <xref:System.Data.DataView.Find%2A> or <xref:System.Data.DataView.FindRows%2A> methods of the <xref:System.Data.DataView>, rather than setting the <xref:System.Data.DataView.RowFilter%2A> property.</span></span> <span data-ttu-id="b8f25-142"><xref:System.Data.DataView.RowFilter%2A> 屬性最適於資料繫結應用程式，因為這種應用程式會用繫結控制項顯示篩選結果。</span><span class="sxs-lookup"><span data-stu-id="b8f25-142">The <xref:System.Data.DataView.RowFilter%2A> property is best used in a data-bound application where a bound control displays filtered results.</span></span> <span data-ttu-id="b8f25-143">設定 <xref:System.Data.DataView.RowFilter%2A> 屬性會重建資料索引，因而增加應用程式的負荷並降低效能。</span><span class="sxs-lookup"><span data-stu-id="b8f25-143">Setting the <xref:System.Data.DataView.RowFilter%2A> property rebuilds the index for the data, adding overhead to your application and decreasing performance.</span></span> <span data-ttu-id="b8f25-144"><xref:System.Data.DataView.Find%2A> 和 <xref:System.Data.DataView.FindRows%2A> 方法會使用目前的索引，而不需要重建索引。</span><span class="sxs-lookup"><span data-stu-id="b8f25-144">The <xref:System.Data.DataView.Find%2A> and <xref:System.Data.DataView.FindRows%2A> methods use the current index without requiring the index to be rebuilt.</span></span> <span data-ttu-id="b8f25-145">如果您只要呼叫 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 一次，就應該使用現有的 <xref:System.Data.DataView>。</span><span class="sxs-lookup"><span data-stu-id="b8f25-145">If you are going to call <xref:System.Data.DataView.Find%2A> or <xref:System.Data.DataView.FindRows%2A> only once, then you should use the existing <xref:System.Data.DataView>.</span></span> <span data-ttu-id="b8f25-146">如果您要呼叫 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 多次，就應該建立新的 <xref:System.Data.DataView> 來重建您想要搜尋之資料行的索引，然後呼叫 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="b8f25-146">If you are going to call <xref:System.Data.DataView.Find%2A> or <xref:System.Data.DataView.FindRows%2A> multiple times, you should create a new <xref:System.Data.DataView> to rebuild the index on the column you want to search on, and then call the <xref:System.Data.DataView.Find%2A> or <xref:System.Data.DataView.FindRows%2A> methods.</span></span> <span data-ttu-id="b8f25-147">如需和方法的詳細資訊 <xref:System.Data.DataView.Find%2A> ， <xref:System.Data.DataView.FindRows%2A> 請參閱 [尋找資料列](./dataset-datatable-dataview/finding-rows.md) 和 [DataView 效能](dataview-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="b8f25-147">For more information about the <xref:System.Data.DataView.Find%2A> and <xref:System.Data.DataView.FindRows%2A> methods see [Finding Rows](./dataset-datatable-dataview/finding-rows.md) and [DataView Performance](dataview-performance.md).</span></span>  
  
## <a name="clearing-the-filter"></a><span data-ttu-id="b8f25-148">清除篩選</span><span class="sxs-lookup"><span data-stu-id="b8f25-148">Clearing the Filter</span></span>  

 <span data-ttu-id="b8f25-149">在您已經使用 <xref:System.Data.DataView> 屬性來設定篩選之後，就可以清除 <xref:System.Data.DataView.RowFilter%2A> 上的篩選。</span><span class="sxs-lookup"><span data-stu-id="b8f25-149">The filter on a <xref:System.Data.DataView> can be cleared after filtering has been set using the <xref:System.Data.DataView.RowFilter%2A> property.</span></span> <span data-ttu-id="b8f25-150">您可以使用兩種不同的方式來清除 <xref:System.Data.DataView> 上的篩選：</span><span class="sxs-lookup"><span data-stu-id="b8f25-150">The filter on a <xref:System.Data.DataView> can be cleared in two different ways:</span></span>  
  
- <span data-ttu-id="b8f25-151">將 <xref:System.Data.DataView.RowFilter%2A> 屬性設定為 `null`。</span><span class="sxs-lookup"><span data-stu-id="b8f25-151">Set the <xref:System.Data.DataView.RowFilter%2A> property to `null`.</span></span>  
  
- <span data-ttu-id="b8f25-152">將 <xref:System.Data.DataView.RowFilter%2A> 屬性設定為空字串。</span><span class="sxs-lookup"><span data-stu-id="b8f25-152">Set the <xref:System.Data.DataView.RowFilter%2A> property to an empty string.</span></span>  
  
### <a name="example"></a><span data-ttu-id="b8f25-153">範例</span><span class="sxs-lookup"><span data-stu-id="b8f25-153">Example</span></span>  

 <span data-ttu-id="b8f25-154">下列範例會從查詢中建立 <xref:System.Data.DataView>，然後將 <xref:System.Data.DataView.RowFilter%2A> 屬性設定為 `null`，藉以清除篩選：</span><span class="sxs-lookup"><span data-stu-id="b8f25-154">The following example creates a <xref:System.Data.DataView> from a query and then clears the filter by setting <xref:System.Data.DataView.RowFilter%2A> property to `null`:</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter2)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter2)]  
  
### <a name="example"></a><span data-ttu-id="b8f25-155">範例</span><span class="sxs-lookup"><span data-stu-id="b8f25-155">Example</span></span>  

 <span data-ttu-id="b8f25-156">下列範例會從資料表中建立 <xref:System.Data.DataView>、設定 <xref:System.Data.DataView.RowFilter%2A> 屬性，然後將 <xref:System.Data.DataView.RowFilter%2A> 屬性設定為空字串，藉以清除篩選：</span><span class="sxs-lookup"><span data-stu-id="b8f25-156">The following example creates a <xref:System.Data.DataView> from a table sets the <xref:System.Data.DataView.RowFilter%2A> property, and then clears the filter by setting the <xref:System.Data.DataView.RowFilter%2A> property to an empty string:</span></span>  
  
 [!code-csharp[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvclearrowfilter)]
 [!code-vb[DP DataView Samples#LDVClearRowFilter](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvclearrowfilter)]  
  
## <a name="see-also"></a><span data-ttu-id="b8f25-157">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b8f25-157">See also</span></span>

- [<span data-ttu-id="b8f25-158">資料繫結和 LINQ to DataSet</span><span class="sxs-lookup"><span data-stu-id="b8f25-158">Data Binding and LINQ to DataSet</span></span>](data-binding-and-linq-to-dataset.md)
- [<span data-ttu-id="b8f25-159">使用 DataView 進行排序</span><span class="sxs-lookup"><span data-stu-id="b8f25-159">Sorting with DataView</span></span>](sorting-with-dataview-linq-to-dataset.md)
