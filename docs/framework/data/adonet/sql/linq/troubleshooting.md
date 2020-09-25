---
title: 疑難排解
ms.date: 03/30/2017
ms.assetid: 8cd4401c-b12c-4116-a421-f3dcffa65670
ms.openlocfilehash: 0ac71d9a55e92161f24deb490b8df6148bfc840c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202184"
---
# <a name="troubleshooting"></a><span data-ttu-id="76686-102">疑難排解</span><span class="sxs-lookup"><span data-stu-id="76686-102">Troubleshooting</span></span>

<span data-ttu-id="76686-103">下列資訊將說明一些您在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 應用程式中可能會遇到的問題，並提供建議來避免或降低這些問題的影響。</span><span class="sxs-lookup"><span data-stu-id="76686-103">The following information exposes some issues you might encounter in your [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] applications, and provides suggestions to avoid or otherwise reduce the effect of these issues.</span></span>  
  
 <span data-ttu-id="76686-104">[常見問題](frequently-asked-questions.md)中有其他問題的解決方式。</span><span class="sxs-lookup"><span data-stu-id="76686-104">Additional issues are addressed in [Frequently Asked Questions](frequently-asked-questions.md).</span></span>  
  
## <a name="unsupported-standard-query-operators"></a><span data-ttu-id="76686-105">不支援的標準查詢運算子</span><span class="sxs-lookup"><span data-stu-id="76686-105">Unsupported Standard Query Operators</span></span>  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="76686-106">並非支援所有標準查詢運算子方法 (例如 <xref:System.Linq.Enumerable.ElementAt%2A>)。</span><span class="sxs-lookup"><span data-stu-id="76686-106">does not support all standard query operator methods (for example, <xref:System.Linq.Enumerable.ElementAt%2A>).</span></span> <span data-ttu-id="76686-107">因此，專案即使可以編譯，仍可能產生執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="76686-107">As a result, projects that compile can still produce run-time errors.</span></span> <span data-ttu-id="76686-108">如需詳細資訊，請參閱 [標準查詢運算子轉譯](standard-query-operator-translation.md)。</span><span class="sxs-lookup"><span data-stu-id="76686-108">For more information, see [Standard Query Operator Translation](standard-query-operator-translation.md).</span></span>  
  
## <a name="memory-issues"></a><span data-ttu-id="76686-109">記憶體問題</span><span class="sxs-lookup"><span data-stu-id="76686-109">Memory Issues</span></span>  

 <span data-ttu-id="76686-110">如果查詢牽涉到記憶體中的集合和 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Table%601> ，則查詢可能會在記憶體中執行，視指定這兩個集合的順序而定。</span><span class="sxs-lookup"><span data-stu-id="76686-110">If a query involves an in-memory collection and [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.Table%601>, the query might be executed in memory, depending on the order in which the two collections are specified.</span></span> <span data-ttu-id="76686-111">如果查詢必須在記憶體中執行，則必須擷取資料庫資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="76686-111">If the query must be executed in memory, then the data from the database table will need to be retrieved.</span></span>  
  
 <span data-ttu-id="76686-112">這種方式沒有效率，而且可能會耗用大量的記憶體和處理器資源。</span><span class="sxs-lookup"><span data-stu-id="76686-112">This approach is inefficient and could result in significant memory and processor usage.</span></span> <span data-ttu-id="76686-113">請盡量避免這種多重定義域查詢。</span><span class="sxs-lookup"><span data-stu-id="76686-113">Try to avoid such multi-domain queries.</span></span>  
  
## <a name="file-names-and-sqlmetal"></a><span data-ttu-id="76686-114">檔案名稱和 SQLMetal</span><span class="sxs-lookup"><span data-stu-id="76686-114">File Names and SQLMetal</span></span>  

 <span data-ttu-id="76686-115">若要指定輸入檔案名稱，請將名稱以輸入檔案加入命令列。</span><span class="sxs-lookup"><span data-stu-id="76686-115">To specify an input file name, add the name to the command line as the input file.</span></span> <span data-ttu-id="76686-116">不支援將檔案名稱包含在連接字串中 (使用 **/conn** 選項)。</span><span class="sxs-lookup"><span data-stu-id="76686-116">Including the file name in the connection string (using the **/conn** option) is not supported.</span></span> <span data-ttu-id="76686-117">如需詳細資訊，請參閱 [SqlMetal.exe (程式碼產生工具)](../../../../tools/sqlmetal-exe-code-generation-tool.md)。</span><span class="sxs-lookup"><span data-stu-id="76686-117">For more information, see [SqlMetal.exe (Code Generation Tool)](../../../../tools/sqlmetal-exe-code-generation-tool.md).</span></span>  
  
## <a name="class-library-projects"></a><span data-ttu-id="76686-118">類別庫專案</span><span class="sxs-lookup"><span data-stu-id="76686-118">Class Library Projects</span></span>  

 <span data-ttu-id="76686-119">物件關聯式設計工具會在專案的檔案中建立連接字串 `app.config` 。</span><span class="sxs-lookup"><span data-stu-id="76686-119">The Object Relational Designer creates a connection string in the `app.config` file of the project.</span></span> <span data-ttu-id="76686-120">類別庫專案不使用 `app.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="76686-120">In class library projects, the `app.config` file is not used.</span></span> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="76686-121">會使用設計階段檔案中提供的連接字串。</span><span class="sxs-lookup"><span data-stu-id="76686-121">uses the Connection String provided in the design-time files.</span></span> <span data-ttu-id="76686-122">變更 `app.config` 中的值不會變更應用程式所連接的資料庫。</span><span class="sxs-lookup"><span data-stu-id="76686-122">Changing the value in `app.config` does not change the database to which your application connects.</span></span>  
  
## <a name="cascade-delete"></a><span data-ttu-id="76686-123">串聯刪除</span><span class="sxs-lookup"><span data-stu-id="76686-123">Cascade Delete</span></span>  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="76686-124">不支援或辨識串聯 (Cascade) 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="76686-124">does not support or recognize cascade-delete operations.</span></span> <span data-ttu-id="76686-125">如果您要刪除有條件約束之資料表中的資料列，必須執行下列其中一項工作：</span><span class="sxs-lookup"><span data-stu-id="76686-125">If you want to delete a row in a table that has constraints against it, you must do either of the following:</span></span>  
  
- <span data-ttu-id="76686-126">在資料庫的外部索引鍵條件約束中設定 `ON DELETE CASCADE` 規則。</span><span class="sxs-lookup"><span data-stu-id="76686-126">Set the `ON DELETE CASCADE` rule in the foreign-key constraint in the database.</span></span>  
  
- <span data-ttu-id="76686-127">使用您自己的程式碼，先刪除使父物件無法刪除的子物件。</span><span class="sxs-lookup"><span data-stu-id="76686-127">Use your own code to first delete the child objects that prevent the parent object from being deleted.</span></span>  
  
 <span data-ttu-id="76686-128">否則會擲回 <xref:System.Data.SqlClient.SqlException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="76686-128">Otherwise, a <xref:System.Data.SqlClient.SqlException> exception is thrown.</span></span>  
  
 <span data-ttu-id="76686-129">如需詳細資訊，請參閱 [如何：從資料庫刪除資料列](how-to-delete-rows-from-the-database.md)。</span><span class="sxs-lookup"><span data-stu-id="76686-129">For more information, see [How to: Delete Rows From the Database](how-to-delete-rows-from-the-database.md).</span></span>  
  
## <a name="expression-not-queryable"></a><span data-ttu-id="76686-130">無法查詢運算式</span><span class="sxs-lookup"><span data-stu-id="76686-130">Expression Not Queryable</span></span>  

 <span data-ttu-id="76686-131">如果您看到「運算式 [expression] 無法查詢；是否遺漏組件參考？」</span><span class="sxs-lookup"><span data-stu-id="76686-131">If you get the "Expression [expression] is not queryable; are you missing an assembly reference?"</span></span> <span data-ttu-id="76686-132">錯誤，請確定下列各項：</span><span class="sxs-lookup"><span data-stu-id="76686-132">error, make sure of the following:</span></span>  
  
- <span data-ttu-id="76686-133">您的應用程式的目標為 .NET Compact Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="76686-133">Your application is targeting .NET Compact Framework 3.5.</span></span>  
  
- <span data-ttu-id="76686-134">您有 `System.Core.dll` 和 `System.Data.Linq.dll` 的參考。</span><span class="sxs-lookup"><span data-stu-id="76686-134">You have a reference to `System.Core.dll` and `System.Data.Linq.dll`.</span></span>  
  
- <span data-ttu-id="76686-135">您有 `Imports` 適用于和的 (Visual Basic) 或 `using` (c # ) 指示詞 <xref:System.Linq> <xref:System.Data.Linq> 。</span><span class="sxs-lookup"><span data-stu-id="76686-135">You have an `Imports` (Visual Basic) or `using` (C#) directive for <xref:System.Linq> and <xref:System.Data.Linq>.</span></span>  
  
## <a name="duplicatekeyexception"></a><span data-ttu-id="76686-136">DuplicateKeyException</span><span class="sxs-lookup"><span data-stu-id="76686-136">DuplicateKeyException</span></span>  

 <span data-ttu-id="76686-137">在對專案進行程式化的過程中 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ，您可能會跨越實體的關係。</span><span class="sxs-lookup"><span data-stu-id="76686-137">In the course of debugging a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] project, you might traverse an entity's relations.</span></span> <span data-ttu-id="76686-138">這樣做會將這些專案帶入快取中，並 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 察覺它們的存在。</span><span class="sxs-lookup"><span data-stu-id="76686-138">Doing so brings these items into the cache, and [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] becomes aware of their presence.</span></span> <span data-ttu-id="76686-139">如果您接著嘗試執行 <xref:System.Data.Linq.Table%601.Attach%2A> 或 <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>，或是類似方法來產生有相同索引鍵的多個資料列，就會擲回 <xref:System.Data.Linq.DuplicateKeyException>。</span><span class="sxs-lookup"><span data-stu-id="76686-139">If you then try to execute <xref:System.Data.Linq.Table%601.Attach%2A> or <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> or a similar method that produces multiple rows that have the same key, a <xref:System.Data.Linq.DuplicateKeyException> is thrown.</span></span>  
  
## <a name="string-concatenation-exceptions"></a><span data-ttu-id="76686-140">字串串連例外狀況</span><span class="sxs-lookup"><span data-stu-id="76686-140">String Concatenation Exceptions</span></span>  

 <span data-ttu-id="76686-141">串連對應到 `[n]text` 和其他 `[n][var]char` 的運算元是不支援的做法。</span><span class="sxs-lookup"><span data-stu-id="76686-141">Concatenation on operands mapped to `[n]text` and other `[n][var]char` is not supported.</span></span> <span data-ttu-id="76686-142">串連對應到兩組不同型別的字串時，會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="76686-142">An exception is thrown for concatenation of strings mapped to the two different sets of types.</span></span> <span data-ttu-id="76686-143">如需詳細資訊，請參閱 [System.string 方法](system-string-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="76686-143">For more information, see [System.String Methods](system-string-methods.md).</span></span>  
  
## <a name="skip-and-take-exceptions-in-sql-server-2000"></a><span data-ttu-id="76686-144">SQL Server 2000 中的 Skip 和 Take 例外狀況</span><span class="sxs-lookup"><span data-stu-id="76686-144">Skip and Take Exceptions in SQL Server 2000</span></span>  

 <span data-ttu-id="76686-145">當您對 SQL Server 2000 資料庫使用 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A> 或 <xref:System.Linq.Queryable.Take%2A> 時，必須使用識別成員 (<xref:System.Linq.Queryable.Skip%2A>)。</span><span class="sxs-lookup"><span data-stu-id="76686-145">You must use identity members (<xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A>) when you use <xref:System.Linq.Queryable.Take%2A> or <xref:System.Linq.Queryable.Skip%2A> against a SQL Server 2000 database.</span></span> <span data-ttu-id="76686-146">此查詢必須針對單一資資料表 (即非聯結資料表) 執行，或為 <xref:System.Linq.Queryable.Distinct%2A>、<xref:System.Linq.Queryable.Except%2A>、<xref:System.Linq.Queryable.Intersect%2A> 或 <xref:System.Linq.Queryable.Union%2A> 作業，而且不能包含 <xref:System.Linq.Queryable.Concat%2A> 作業。</span><span class="sxs-lookup"><span data-stu-id="76686-146">The query must be against a single table (that is, not a join), or be a <xref:System.Linq.Queryable.Distinct%2A>, <xref:System.Linq.Queryable.Except%2A>, <xref:System.Linq.Queryable.Intersect%2A>, or <xref:System.Linq.Queryable.Union%2A> operation, and must not include a <xref:System.Linq.Queryable.Concat%2A> operation.</span></span> <span data-ttu-id="76686-147">如需詳細資訊，請參閱 [標準查詢運算子轉譯](standard-query-operator-translation.md)中的「SQL Server 2000 支援」一節。</span><span class="sxs-lookup"><span data-stu-id="76686-147">For more information, see the "SQL Server 2000 Support" section in [Standard Query Operator Translation](standard-query-operator-translation.md).</span></span>  
  
 <span data-ttu-id="76686-148">這項需求不適用於 SQL Server 2005。</span><span class="sxs-lookup"><span data-stu-id="76686-148">This requirement does not apply to SQL Server 2005.</span></span>  
  
## <a name="groupby-invalidoperationexception"></a><span data-ttu-id="76686-149">GroupBy InvalidOperationException</span><span class="sxs-lookup"><span data-stu-id="76686-149">GroupBy InvalidOperationException</span></span>  

 <span data-ttu-id="76686-150">當以 <xref:System.Linq.Enumerable.GroupBy%2A> 運算式做為群組依據 (例如 `boolean`) 的 `group x by (Phone==@phone)` 查詢有資料行的值為 null 時，會擲回此例外狀況。</span><span class="sxs-lookup"><span data-stu-id="76686-150">This exception is thrown when a column value is null in a <xref:System.Linq.Enumerable.GroupBy%2A> query that groups by a `boolean` expression, such as `group x by (Phone==@phone)`.</span></span> <span data-ttu-id="76686-151">由於運算式是，因此會將索引 `boolean` 鍵推斷為 `boolean` ，而不是 `nullable` `boolean` 。</span><span class="sxs-lookup"><span data-stu-id="76686-151">Because the expression is a `boolean`, the key is inferred to be `boolean`, not `nullable` `boolean`.</span></span> <span data-ttu-id="76686-152">當轉譯的比較產生 null 時，會嘗試將指派給 `nullable` `boolean` ，並擲回 `boolean` 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="76686-152">When the translated comparison produces a null, an attempt is made to assign a `nullable` `boolean` to a `boolean`, and the exception is thrown.</span></span>  
  
 <span data-ttu-id="76686-153">為避免這個情況 (假設您要將 null 視為 false)，請使用類似下列的方式：</span><span class="sxs-lookup"><span data-stu-id="76686-153">To avoid this situation (assuming you want to treat nulls as false), use an approach such as the following:</span></span>  
  
 `GroupBy="(Phone != null) && (Phone=@Phone)"`  
  
## <a name="oncreated-partial-method"></a><span data-ttu-id="76686-154">OnCreated() 部分方法</span><span class="sxs-lookup"><span data-stu-id="76686-154">OnCreated() Partial Method</span></span>  

 <span data-ttu-id="76686-155">每次呼叫物件建構函式時，都會呼叫產生的方法 `OnCreated()`，包括 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 呼叫建構函式來複製原始值的情況。</span><span class="sxs-lookup"><span data-stu-id="76686-155">The generated method `OnCreated()` is called each time the object constructor is called, including the scenario in which [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] calls the constructor to make a copy for original values.</span></span> <span data-ttu-id="76686-156">如果您要在自己的部分類別中實作 `OnCreated()` 方法，請將此行為列入考量。</span><span class="sxs-lookup"><span data-stu-id="76686-156">Take this behavior into account if you implement the `OnCreated()` method in your own partial class.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="76686-157">另請參閱</span><span class="sxs-lookup"><span data-stu-id="76686-157">See also</span></span>

- [<span data-ttu-id="76686-158">偵錯支援</span><span class="sxs-lookup"><span data-stu-id="76686-158">Debugging Support</span></span>](debugging-support.md)
- [<span data-ttu-id="76686-159">常見問題集</span><span class="sxs-lookup"><span data-stu-id="76686-159">Frequently Asked Questions</span></span>](frequently-asked-questions.md)
