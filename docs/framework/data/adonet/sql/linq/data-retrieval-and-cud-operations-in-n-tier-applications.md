---
title: 多層式架構應用程式中的資料擷取和 CUD 作業 (LINQ to SQL)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c3133d53-83ed-4a4d-af8b-82edcf3831db
ms.openlocfilehash: 1bc97504b4dd053ce9ef747460a79865cbe836ee
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197413"
---
# <a name="data-retrieval-and-cud-operations-in-n-tier-applications-linq-to-sql"></a><span data-ttu-id="725c6-102">多層式架構應用程式中的資料擷取和 CUD 作業 (LINQ to SQL)</span><span class="sxs-lookup"><span data-stu-id="725c6-102">Data Retrieval and CUD Operations in N-Tier Applications (LINQ to SQL)</span></span>

<span data-ttu-id="725c6-103">當您將像是 Customers 或 Orders 等實體物件透過網路序列化到用戶端時，這些實體會與其資料內容中斷連結。</span><span class="sxs-lookup"><span data-stu-id="725c6-103">When you serialize entity objects such as Customers or Orders to a client over a network, those entities are detached from their data context.</span></span> <span data-ttu-id="725c6-104">資料內容不會再追蹤它們的變更或它們與其他物件的關聯。</span><span class="sxs-lookup"><span data-stu-id="725c6-104">The data context no longer tracks their changes or their associations with other objects.</span></span> <span data-ttu-id="725c6-105">如果用戶端只讀取資料，這就不成問題。</span><span class="sxs-lookup"><span data-stu-id="725c6-105">This is not an issue as long as the clients are only reading the data.</span></span> <span data-ttu-id="725c6-106">此外，要讓用戶端加入資料列到資料庫，也相對來說簡單。</span><span class="sxs-lookup"><span data-stu-id="725c6-106">It is also relatively simple to enable clients to add new rows to a database.</span></span> <span data-ttu-id="725c6-107">不過，如果您的應用程式要讓用戶端能夠更新或刪除資料，就必須將實體附加到新的資料內容，才能呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="725c6-107">However, if your application requires that clients be able to update or delete data, then you must attach the entities to a new data context before you call <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="725c6-108">此外，如果您使用開放式並行存取 (Optimistic Concurrency) 來檢查原始值，那麼也需要想辦法將原始實體和修改過的實體提供給資料庫。</span><span class="sxs-lookup"><span data-stu-id="725c6-108">In addition, if you are using an optimistic concurrency check with original values, then you will also need a way to provide the database both the original entity and the entity as modified.</span></span> <span data-ttu-id="725c6-109">`Attach` 方法即是提供來讓您將中斷連結的實體放入新的資料內容。</span><span class="sxs-lookup"><span data-stu-id="725c6-109">The `Attach` methods are provided to enable you to put entities into a new data context after they have been detached.</span></span>  
  
 <span data-ttu-id="725c6-110">即使您要序列化 proxy 物件來取代 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 實體，仍然需要在資料存取層 (DAL) 上建立實體，並將它附加至新的 <xref:System.Data.Linq.DataContext?displayProperty=nameWithType> ，以便將資料提交給資料庫。</span><span class="sxs-lookup"><span data-stu-id="725c6-110">Even if you are serializing proxy objects in place of the [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] entities, you still have to construct an entity on the data access layer (DAL), and attach it to a new <xref:System.Data.Linq.DataContext?displayProperty=nameWithType>, in order to submit the data to the database.</span></span>  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="725c6-111">會完整不在乎實體的序列化方式。</span><span class="sxs-lookup"><span data-stu-id="725c6-111">is completely indifferent about how entities are serialized.</span></span> <span data-ttu-id="725c6-112">如需有關如何使用物件關聯式設計工具和 SQLMetal 工具來產生可使用 Windows Communication Foundation (WCF) 序列化之類別的詳細資訊，請參閱 [如何：讓實體成為可](how-to-make-entities-serializable.md)序列化。</span><span class="sxs-lookup"><span data-stu-id="725c6-112">For more information about how to use the Object Relational Designer and SQLMetal tools to generate classes that are serializable by using Windows Communication Foundation (WCF), see [How to: Make Entities Serializable](how-to-make-entities-serializable.md).</span></span>  
  
> [!NOTE]
> <span data-ttu-id="725c6-113">請只在新的或還原序列化的實體上呼叫 `Attach` 方法。</span><span class="sxs-lookup"><span data-stu-id="725c6-113">Only call the `Attach` methods on new or deserialized entities.</span></span> <span data-ttu-id="725c6-114">要將實體與其原始資料內容中斷連結的唯一方式就是使其序列化。</span><span class="sxs-lookup"><span data-stu-id="725c6-114">The only way for an entity to be detached from its original data context is for it to be serialized.</span></span> <span data-ttu-id="725c6-115">如果您嘗試將未中斷連結的實體附加到新的資料內容，而該實體仍擁有先前資料內容的延遲載入器，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 就會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="725c6-115">If you try to attach an undetached entity to a new data context, and that entity still has deferred loaders from its previous data context, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] will thrown an exception.</span></span> <span data-ttu-id="725c6-116">若實體擁有來自兩個不同資料內容的延遲載入器，當您在該實體上執行插入、更新和刪除作業時，可能會導致不想要的結果。</span><span class="sxs-lookup"><span data-stu-id="725c6-116">An entity with deferred loaders from two different data contexts could cause unwanted results when you perform insert, update, and delete operations on that entity.</span></span> <span data-ttu-id="725c6-117">如需延遲載入器的詳細資訊，請參閱 [延後和立即載入](deferred-versus-immediate-loading.md)。</span><span class="sxs-lookup"><span data-stu-id="725c6-117">For more information about deferred loaders, see [Deferred versus Immediate Loading](deferred-versus-immediate-loading.md).</span></span>  
  
## <a name="retrieving-data"></a><span data-ttu-id="725c6-118">擷取資料</span><span class="sxs-lookup"><span data-stu-id="725c6-118">Retrieving Data</span></span>  
  
### <a name="client-method-call"></a><span data-ttu-id="725c6-119">用戶端方法呼叫</span><span class="sxs-lookup"><span data-stu-id="725c6-119">Client Method Call</span></span>  

 <span data-ttu-id="725c6-120">下列範例示範 Windows Form 用戶端對 DAL 的範例方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="725c6-120">The following examples show a sample method call to the DAL from a Windows Forms client.</span></span> <span data-ttu-id="725c6-121">在這個範例中，DAL 實作為 Windows 服務庫：</span><span class="sxs-lookup"><span data-stu-id="725c6-121">In this example, the DAL is implemented as a Windows Service Library:</span></span>  
  
```vb  
Private Function GetProdsByCat_Click(ByVal sender As Object, ByVal e _  
    As EventArgs)  
  
    ' Create the WCF client proxy.  
    Dim proxy As New NorthwindServiceReference.Service1Client  
  
    ' Call the method on the service.  
    Dim products As NorthwindServiceReference.Product() = _  
        proxy.GetProductsByCategory(1)  
  
    ' If the database uses original values for concurrency checks,  
    ' the client needs to store them and pass them back to the  
    ' middle tier along with the new values when updating data.  
  
    For Each v As NorthwindClient1.NorthwindServiceReference.Product _  
        In products  
        ' Persist to a List(Of Product) declared at class scope.  
        ' Additional change-tracking logic is the responsibility  
        ' of the presentation tier and/or middle tier.  
        originalProducts.Add(v)  
    Next  
  
    ' (Not shown) Bind the products list to a control  
    ' and/or perform whatever processing is necessary.  
End Function  
```  
  
```csharp  
private void GetProdsByCat_Click(object sender, EventArgs e)  
{  
    // Create the WCF client proxy.  
    NorthwindServiceReference.Service1Client proxy =
    new NorthwindClient.NorthwindServiceReference.Service1Client();  
  
    // Call the method on the service.  
    NorthwindServiceReference.Product[] products =
    proxy.GetProductsByCategory(1);  
  
    // If the database uses original values for concurrency checks,
    // the client needs to store them and pass them back to the
    // middle tier along with the new values when updating data.  
    foreach (var v in products)  
    {  
        // Persist to a list<Product> declared at class scope.  
        // Additional change-tracking logic is the responsibility  
        // of the presentation tier and/or middle tier.  
        originalProducts.Add(v);  
    }  
  
    // (Not shown) Bind the products list to a control  
    // and/or perform whatever processing is necessary.  
    }  
```  
  
### <a name="middle-tier-implementation"></a><span data-ttu-id="725c6-122">中介層實作</span><span class="sxs-lookup"><span data-stu-id="725c6-122">Middle Tier Implementation</span></span>  

 <span data-ttu-id="725c6-123">下列範例顯示中介層 (Middle Tier) 上的介面方法實作。</span><span class="sxs-lookup"><span data-stu-id="725c6-123">The following example shows an implementation of the interface method on the middle tier.</span></span> <span data-ttu-id="725c6-124">下列是需要注意的兩個重點：</span><span class="sxs-lookup"><span data-stu-id="725c6-124">The following are the two main points to note:</span></span>  
  
- <span data-ttu-id="725c6-125"><xref:System.Data.Linq.DataContext> 是在方法範圍內宣告。</span><span class="sxs-lookup"><span data-stu-id="725c6-125">The <xref:System.Data.Linq.DataContext> is declared at method scope.</span></span>  
  
- <span data-ttu-id="725c6-126">此方法會傳回實際結果的 <xref:System.Collections.IEnumerable> 集合。</span><span class="sxs-lookup"><span data-stu-id="725c6-126">The method returns an <xref:System.Collections.IEnumerable> collection of the actual results.</span></span> <span data-ttu-id="725c6-127">序列化程式將會執行查詢，將結果送回用戶端/展示層。</span><span class="sxs-lookup"><span data-stu-id="725c6-127">The serializer will execute the query to send the results back to the client/presentation tier.</span></span> <span data-ttu-id="725c6-128">若要在中介層本機上存取查詢結果，您可以在查詢變數上呼叫 `ToList` 或 `ToArray` 來強制執行。</span><span class="sxs-lookup"><span data-stu-id="725c6-128">To access the query results locally on the middle tier, you can force execution by calling `ToList` or `ToArray` on the query variable.</span></span> <span data-ttu-id="725c6-129">然後就可以將該清單或陣列以 `IEnumerable` 傳回。</span><span class="sxs-lookup"><span data-stu-id="725c6-129">You can then return that list or array as an `IEnumerable`.</span></span>  
  
```vb  
Public Function GetProductsByCategory(ByVal categoryID As Integer) _  
    As IEnumerable(Of Product)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    Dim productQuery = _  
    From prod In db.Products _  
    Where prod.CategoryID = categoryID _  
    Select prod  
  
    Return productQuery.AsEnumerable()  
  
End Function  
```  
  
```csharp  
public IEnumerable<Product> GetProductsByCategory(int categoryID)  
{  
    NorthwindClasses1DataContext db =
    new NorthwindClasses1DataContext(connectionString);  
  
    IEnumerable<Product> productQuery =  
    from prod in db.Products  
    where prod.CategoryID == categoryID  
    select prod;  
  
    return productQuery.AsEnumerable();
}  
```  
  
 <span data-ttu-id="725c6-130">資料內容的執行個體應具有「工作單元」的存留期 (Lifetime)。</span><span class="sxs-lookup"><span data-stu-id="725c6-130">An instance of a data context should have a lifetime of one "unit of work."</span></span> <span data-ttu-id="725c6-131">在鬆散結合的環境中，工作單元通常很小，可能是一個開放式異動，其中包含對 `SubmitChanges` 的單一呼叫。</span><span class="sxs-lookup"><span data-stu-id="725c6-131">In a loosely-coupled environment, a unit of work is typically small, perhaps one optimistic transaction, including a single call to `SubmitChanges`.</span></span> <span data-ttu-id="725c6-132">因此，資料內容會在方法範圍內建立和處置 (Dispose)。</span><span class="sxs-lookup"><span data-stu-id="725c6-132">Therefore, the data context is created and disposed at method scope.</span></span> <span data-ttu-id="725c6-133">如果工作單元包含對商務規則邏輯的呼叫，那麼通常會需要在整個作業期間保留 `DataContext` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="725c6-133">If the unit of work includes calls to business rules logic, then generally you will want to keep the `DataContext` instance for that whole operation.</span></span> <span data-ttu-id="725c6-134">無論在哪種情況下，`DataContext` 執行個體都不適合跨任意數目的交易而長期保持作用中。</span><span class="sxs-lookup"><span data-stu-id="725c6-134">In any case, `DataContext` instances are not intended to be kept alive for long periods of time across arbitrary numbers of transactions.</span></span>  
  
 <span data-ttu-id="725c6-135">這個方法將傳回 Product 物件，而不是與每個 Project 相關聯之 Order_Detail 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="725c6-135">This method will return Product objects but not the collection of Order_Detail objects that are associated with each Product.</span></span> <span data-ttu-id="725c6-136">請使用 <xref:System.Data.Linq.DataLoadOptions> 物件來變更此預設行為。</span><span class="sxs-lookup"><span data-stu-id="725c6-136">Use the <xref:System.Data.Linq.DataLoadOptions> object to change this default behavior.</span></span> <span data-ttu-id="725c6-137">如需詳細資訊，請參閱 [如何：控制要抓取的相關資料量](how-to-control-how-much-related-data-is-retrieved.md)。</span><span class="sxs-lookup"><span data-stu-id="725c6-137">For more information, see [How to: Control How Much Related Data Is Retrieved](how-to-control-how-much-related-data-is-retrieved.md).</span></span>  
  
## <a name="inserting-data"></a><span data-ttu-id="725c6-138">插入資料</span><span class="sxs-lookup"><span data-stu-id="725c6-138">Inserting Data</span></span>  

 <span data-ttu-id="725c6-139">若要插入新物件，展示層會在中介層介面上呼叫相關方法，並傳入要插入的新物件即可。</span><span class="sxs-lookup"><span data-stu-id="725c6-139">To insert a new object, the presentation tier just calls the relevant method on the middle tier interface, and passes in the new object to insert.</span></span> <span data-ttu-id="725c6-140">在某些情況下，為提高效率，用戶端可能只會傳入部分值，再由中介層建構完整物件。</span><span class="sxs-lookup"><span data-stu-id="725c6-140">In some cases, it may be more efficient for the client to pass in only some values and have the middle tier construct the full object.</span></span>  
  
### <a name="middle-tier-implementation"></a><span data-ttu-id="725c6-141">中介層實作</span><span class="sxs-lookup"><span data-stu-id="725c6-141">Middle Tier Implementation</span></span>  

 <span data-ttu-id="725c6-142">在中介層上，新的 <xref:System.Data.Linq.DataContext> 會建立，物件會使用 <xref:System.Data.Linq.DataContext> 方法附加到 <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>，當呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 時，物件即會插入。</span><span class="sxs-lookup"><span data-stu-id="725c6-142">On the middle tier, a new <xref:System.Data.Linq.DataContext> is created, the object is attached to the <xref:System.Data.Linq.DataContext> by using the <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> method, and the object is inserted when <xref:System.Data.Linq.DataContext.SubmitChanges%2A> is called.</span></span> <span data-ttu-id="725c6-143">例外狀況、回呼 (Callback) 和錯誤狀況的處理方式就如同在任何其他 Web 服務案例中處理一樣。</span><span class="sxs-lookup"><span data-stu-id="725c6-143">Exceptions, callbacks, and error conditions can be handled just as in any other Web service scenario.</span></span>  
  
```vb  
' No call to Attach is necessary for inserts.  
Public Sub InsertOrder(ByVal o As Order)  
  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
    db.Orders.InsertOnSubmit(o)  
  
    ' Exception handling not shown.  
    db.SubmitChanges()  
  
End Sub  
```  
  
```csharp  
// No call to Attach is necessary for inserts.  
    public void InsertOrder(Order o)  
    {  
        NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
        db.Orders.InsertOnSubmit(o);  
  
        // Exception handling not shown.  
        db.SubmitChanges();  
    }  
```  
  
## <a name="deleting-data"></a><span data-ttu-id="725c6-144">刪除資料</span><span class="sxs-lookup"><span data-stu-id="725c6-144">Deleting Data</span></span>  

 <span data-ttu-id="725c6-145">若要刪除資料庫中的現有物件，展示層會在中介層介面上呼叫相關方法，然後針對要刪除的物件，傳入包含其原始值的複本。</span><span class="sxs-lookup"><span data-stu-id="725c6-145">To delete an existing object from the database, the presentation tier calls the relevant method on the middle tier interface, and passes in its copy that includes original values of the object to be deleted.</span></span>  
  
 <span data-ttu-id="725c6-146">刪除作業包含開放式並行存取檢查，而要刪除的物件必須先附加到新的資料內容。</span><span class="sxs-lookup"><span data-stu-id="725c6-146">Delete operations involve optimistic concurrency checks, and the object to be deleted must first be attached to the new data context.</span></span> <span data-ttu-id="725c6-147">在這個範例中，`Boolean` 參數會設定為 `false`，表示物件沒有時間戳記 (RowVersion)。</span><span class="sxs-lookup"><span data-stu-id="725c6-147">In this example, the `Boolean` parameter is set to `false` to indicate that the object does not have a timestamp (RowVersion).</span></span> <span data-ttu-id="725c6-148">如果資料庫資料表會為每個資料錄產生時間戳記，那麼開放式並行存取檢查會簡單許多，對用戶端來說尤然。</span><span class="sxs-lookup"><span data-stu-id="725c6-148">If your database table does generate timestamps for each record, then concurrency checks are much simpler, especially for the client.</span></span> <span data-ttu-id="725c6-149">這只要傳入原始或修改過的物件，再將 `Boolean` 參數設定為 `true` 即可。</span><span class="sxs-lookup"><span data-stu-id="725c6-149">Just pass in either the original or modified object and set the `Boolean` parameter to `true`.</span></span> <span data-ttu-id="725c6-150">無論在哪種情況下，在中介層上通常需要攔截 <xref:System.Data.Linq.ChangeConflictException>。</span><span class="sxs-lookup"><span data-stu-id="725c6-150">In any case, on the middle tier it is typically necessary to catch the <xref:System.Data.Linq.ChangeConflictException>.</span></span> <span data-ttu-id="725c6-151">如需如何處理開放式平行存取衝突的詳細資訊，請參閱 [開放式平行存取：總覽](optimistic-concurrency-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="725c6-151">For more information about how to handle optimistic concurrency conflicts, see [Optimistic Concurrency: Overview](optimistic-concurrency-overview.md).</span></span>  
  
 <span data-ttu-id="725c6-152">刪除在關聯資料表上具有外部索引鍵條件約束的實體時，您必須先刪除其 <xref:System.Data.Linq.EntitySet%601> 集合中的所有物件。</span><span class="sxs-lookup"><span data-stu-id="725c6-152">When deleting entities that have foreign key constraints on associated tables, you must first delete all the objects in its <xref:System.Data.Linq.EntitySet%601> collections.</span></span>  
  
```vb  
' Attach is necessary for deletes.  
Public Sub DeleteOrder(ByVal order As Order)  
    Dim db As New NorthwindClasses1DataContext(connectionString)  
  
    db.Orders.Attach(order, False)  
    ' This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order)  
  
    Try  
        ' ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict)  
  
    Catch ex As ChangeConflictException  
        ' Get conflict information, and take actions  
        ' that are appropriate for your application.  
        ' See MSDN Article "How to: Manage Change  
        ' Conflicts (LINQ to SQL).  
  
    End Try  
End Sub  
```  
  
```csharp  
// Attach is necessary for deletes.  
public void DeleteOrder(Order order)  
{  
    NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString);  
  
    db.Orders.Attach(order, false);  
    // This will throw an exception if the order has order details.  
    db.Orders.DeleteOnSubmit(order);  
    try  
    {  
        // ConflictMode is an optional parameter.  
        db.SubmitChanges(ConflictMode.ContinueOnConflict);  
    }  
    catch (ChangeConflictException e)  
    {  
       // Get conflict information, and take actions  
       // that are appropriate for your application.  
       // See MSDN Article How to: Manage Change Conflicts (LINQ to SQL).  
    }  
}  
```  
  
## <a name="updating-data"></a><span data-ttu-id="725c6-153">更新資料</span><span class="sxs-lookup"><span data-stu-id="725c6-153">Updating Data</span></span>  

 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <span data-ttu-id="725c6-154">支援在下列牽涉到開放式並行存取的案例中更新：</span><span class="sxs-lookup"><span data-stu-id="725c6-154">supports updates in these scenarios involving optimistic concurrency:</span></span>  
  
- <span data-ttu-id="725c6-155">以時間戳記或 RowVersion 號碼為基礎的開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="725c6-155">Optimistic concurrency based on timestamps or RowVersion numbers.</span></span>  
  
- <span data-ttu-id="725c6-156">以實體屬性子集的原始值為基礎的開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="725c6-156">Optimistic concurrency based on original values of a subset of entity properties.</span></span>  
  
- <span data-ttu-id="725c6-157">以完整原始和修改過的實體為基礎的開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="725c6-157">Optimistic concurrency based on the complete original and modified entities.</span></span>  
  
 <span data-ttu-id="725c6-158">您也可以對實體連同其關聯一起執行更新或刪除，例如 Customer 及其關聯 Order 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="725c6-158">You can also perform updates or deletes on an entity together with its relations, for example a Customer and a collection of its associated Order objects.</span></span> <span data-ttu-id="725c6-159">當您在用戶端上修改實體物件及子 (`EntitySet`) 集合的圖形，而開放式並行存取需要原始值時，用戶端必須提供每個實體和 <xref:System.Data.Linq.EntitySet%601> 物件的原始值。</span><span class="sxs-lookup"><span data-stu-id="725c6-159">When you make modifications on the client to a graph of entity objects and their child (`EntitySet`) collections, and the optimistic concurrency checks require original values, the client must provide those original values for each entity and <xref:System.Data.Linq.EntitySet%601> object.</span></span> <span data-ttu-id="725c6-160">如果要讓用戶端能夠在單一方法呼叫中執行一組相關的更新、刪除和插入，您必須提供用戶端方式來指出要對每個實體執行何種作業。</span><span class="sxs-lookup"><span data-stu-id="725c6-160">If you want to enable clients to make a set of related updates, deletes, and insertions in a single method call, you must provide the client a way to indicate what type of operation to perform on each entity.</span></span> <span data-ttu-id="725c6-161">接著在中介層上，您必須為每個實體呼叫適當的 <xref:System.Data.Linq.ITable.Attach%2A> 方法，再呼叫 <xref:System.Data.Linq.ITable.InsertOnSubmit%2A>、<xref:System.Data.Linq.ITable.DeleteAllOnSubmit%2A> 或 <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> (插入不需要 `Attach`)，才能呼叫 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>。</span><span class="sxs-lookup"><span data-stu-id="725c6-161">On the middle tier, you then must call the appropriate <xref:System.Data.Linq.ITable.Attach%2A> method and then <xref:System.Data.Linq.ITable.InsertOnSubmit%2A>, <xref:System.Data.Linq.ITable.DeleteAllOnSubmit%2A>, or <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> (without `Attach`, for insertions) for each entity before you call <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.</span></span> <span data-ttu-id="725c6-162">請不要擷取資料庫的值來當做更新之前取得原始值的方式。</span><span class="sxs-lookup"><span data-stu-id="725c6-162">Do not retrieve data from the database as a way to obtain original values before you try updates.</span></span>  
  
 <span data-ttu-id="725c6-163">如需開放式平行存取的詳細資訊，請參閱 [開放式平行存取：總覽](optimistic-concurrency-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="725c6-163">For more information about optimistic concurrency, see [Optimistic Concurrency: Overview](optimistic-concurrency-overview.md).</span></span> <span data-ttu-id="725c6-164">如需解決開放式平行存取變更衝突的詳細資訊，請參閱 [如何：管理變更衝突](how-to-manage-change-conflicts.md)。</span><span class="sxs-lookup"><span data-stu-id="725c6-164">For detailed information about resolving optimistic concurrency change conflicts, see [How to: Manage Change Conflicts](how-to-manage-change-conflicts.md).</span></span>  
  
 <span data-ttu-id="725c6-165">下列範例將示範每個案例：</span><span class="sxs-lookup"><span data-stu-id="725c6-165">The following examples demonstrate each scenario:</span></span>  
  
### <a name="optimistic-concurrency-with-timestamps"></a><span data-ttu-id="725c6-166">使用時間戳記的開放式並行存取</span><span class="sxs-lookup"><span data-stu-id="725c6-166">Optimistic concurrency with timestamps</span></span>  
  
```vb  
' Assume that "customer" has been sent by client.  
' Attach with "true" to say this is a modified entity  
' and it can be checked for optimistic concurrency  
' because it has a column that is marked with the  
' "RowVersion" attribute.  
  
db.Customers.Attach(customer, True)  
  
Try  
    ' Optional: Specify a ConflictMode value  
    ' in call to SubmitChanges.  
    db.SubmitChanges()  
Catch ex As ChangeConflictException  
    ' Handle conflict based on options provided.  
    ' See MSDN article "How to: Manage Change  
    ' Conflicts (LINQ to SQL)".  
End Try  
```  
  
```csharp  
// Assume that "customer" has been sent by client.  
// Attach with "true" to say this is a modified entity  
// and it can be checked for optimistic concurrency because  
//  it has a column that is marked with "RowVersion" attribute  
db.Customers.Attach(customer, true)  
try  
{  
    // Optional: Specify a ConflictMode value  
    // in call to SubmitChanges.  
    db.SubmitChanges();  
}  
catch(ChangeConflictException e)  
{  
    // Handle conflict based on options provided  
    // See MSDN article How to: Manage Change Conflicts (LINQ to SQL).  
}  
```  
  
### <a name="with-subset-of-original-values"></a><span data-ttu-id="725c6-167">使用原始值子集</span><span class="sxs-lookup"><span data-stu-id="725c6-167">With Subset of Original Values</span></span>  

 <span data-ttu-id="725c6-168">在這種方式中，用戶端會傳回已序列化的完整物件以及要修改的值。</span><span class="sxs-lookup"><span data-stu-id="725c6-168">In this approach, the client returns the complete serialized object, together with the values to be modified.</span></span>  
  
```vb  
Public Sub UpdateProductInventory(ByVal p As Product, ByVal _  
    unitsInStock As Short?, ByVal unitsOnOrder As Short?)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        ' p is the original unmodified product  
        ' that was obtained from the database.  
        ' The client kept a copy and returns it now.  
        db.Products.Attach(p, False)  
  
        ' Now that the original values are in the data context,  
        ' apply the changes.  
        p.UnitsInStock = unitsInStock  
        p.UnitsOnOrder = unitsOnOrder  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle conflict based on options provided.  
            ' See MSDN article "How to: Manage Change Conflicts  
            ' (LINQ to SQL)".  
        End Try  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInventory(Product p, short? unitsInStock, short? unitsOnOrder)  
{  
    using (NorthwindClasses1DataContext db = new NorthwindClasses1DataContext(connectionString))  
    {  
        // p is the original unmodified product  
        // that was obtained from the database.  
        // The client kept a copy and returns it now.  
        db.Products.Attach(p, false);  
  
        // Now that the original values are in the data context, apply the changes.  
        p.UnitsInStock = unitsInStock;  
        p.UnitsOnOrder = unitsOnOrder;  
        try  
        {  
             // Optional: Specify a ConflictMode value  
             // in call to SubmitChanges.  
             db.SubmitChanges();  
        }  
        catch (ChangeConflictException e)  
        {  
            // Handle conflict based on provided options.  
            // See MSDN article How to: Manage Change Conflicts  
            // (LINQ to SQL).  
        }  
    }  
}  
```  
  
### <a name="with-complete-entities"></a><span data-ttu-id="725c6-169">使用完整實體</span><span class="sxs-lookup"><span data-stu-id="725c6-169">With Complete Entities</span></span>  
  
```vb  
Public Sub UpdateProductInfo(ByVal newProd As Product, ByVal _  
    originalProd As Product)  
  
    Using db As New NorthwindClasses1DataContext(connectionString)  
        db.Products.Attach(newProd, originalProd)  
  
        Try  
            ' Optional: Specify a ConflictMode value  
            ' in call to SubmitChanges.  
            db.SubmitChanges()  
  
        Catch ex As Exception  
            ' Handle potential change conflicgt in whatever way  
            ' is appropriate for your application.  
            ' For more information, see the MSDN article  
            ' "How to: Manage Change Conflicts (LINQ to  
            ' SQL)".  
        End Try  
  
    End Using  
End Sub  
```  
  
```csharp  
public void UpdateProductInfo(Product newProd, Product originalProd)  
{  
     using (NorthwindClasses1DataContext db = new  
        NorthwindClasses1DataContext(connectionString))  
     {  
         db.Products.Attach(newProd, originalProd);  
         try  
         {  
               // Optional: Specify a ConflictMode value  
               // in call to SubmitChanges.  
               db.SubmitChanges();  
         }  
        catch (ChangeConflictException e)  
        {  
            // Handle potential change conflict in whatever way  
            // is appropriate for your application.  
            // For more information, see the MSDN article  
            // How to: Manage Change Conflicts (LINQ to SQL)/  
        }
    }  
}  
```  
  
 <span data-ttu-id="725c6-170">若要更新集合，請呼叫 <xref:System.Data.Linq.ITable.AttachAll%2A>，而非 `Attach`。</span><span class="sxs-lookup"><span data-stu-id="725c6-170">To update a collection, call <xref:System.Data.Linq.ITable.AttachAll%2A> instead of `Attach`.</span></span>  
  
### <a name="expected-entity-members"></a><span data-ttu-id="725c6-171">必要的實體成員</span><span class="sxs-lookup"><span data-stu-id="725c6-171">Expected Entity Members</span></span>  

 <span data-ttu-id="725c6-172">如前所述，在呼叫 `Attach` 方法之前，只需要設定實體物件的某些成員。</span><span class="sxs-lookup"><span data-stu-id="725c6-172">As stated previously, only certain members of the entity object are required to be set before you call the `Attach` methods.</span></span> <span data-ttu-id="725c6-173">需要設定的實體成員必須符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="725c6-173">Entity members that are required to be set must fulfill the following criteria:</span></span>  
  
- <span data-ttu-id="725c6-174">屬於實體識別的一部分。</span><span class="sxs-lookup"><span data-stu-id="725c6-174">Be part of the entity’s identity.</span></span>  
  
- <span data-ttu-id="725c6-175">必須修改。</span><span class="sxs-lookup"><span data-stu-id="725c6-175">Be expected to be modified.</span></span>  
  
- <span data-ttu-id="725c6-176">本身是時間戳記或將其 <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> 屬性 (Attribute) 設為 `Never` 以外的值。</span><span class="sxs-lookup"><span data-stu-id="725c6-176">Be a timestamp or have its <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> attribute set to something besides `Never`.</span></span>  
  
 <span data-ttu-id="725c6-177">如果資料表使用時間戳記或版本號碼進行開放式並行存取檢查，則您必須設定這些成員，才能呼叫 <xref:System.Data.Linq.ITable.Attach%2A>。</span><span class="sxs-lookup"><span data-stu-id="725c6-177">If a table uses a timestamp or version number for an optimistic concurrency check, you must set those members before you call <xref:System.Data.Linq.ITable.Attach%2A>.</span></span> <span data-ttu-id="725c6-178">當 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> 屬性 (Property) 在該 Column 屬性 (Attribute) 上設定為 true 時，成員就會專供開放式並行存取檢查使用。</span><span class="sxs-lookup"><span data-stu-id="725c6-178">A member is dedicated for optimistic concurrency checking when the <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A> property is set to true on that Column attribute.</span></span> <span data-ttu-id="725c6-179">只有在版本號碼或時間戳記值在資料庫上相同時，才會提交任何要求的變更。</span><span class="sxs-lookup"><span data-stu-id="725c6-179">Any requested updates will be submitted only if the version number or timestamp values are the same on the database.</span></span>  
  
 <span data-ttu-id="725c6-180">只要成員沒有將 <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> 設定為 `Never`，該成員也會用於開放式並行存取檢查。</span><span class="sxs-lookup"><span data-stu-id="725c6-180">A member is also used in the optimistic concurrency check as long as the member does not have <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A> set to `Never`.</span></span> <span data-ttu-id="725c6-181">如果沒有指定其他值，預設值會是 `Always`。</span><span class="sxs-lookup"><span data-stu-id="725c6-181">The default value is `Always` if no other value is specified.</span></span>  
  
 <span data-ttu-id="725c6-182">如果遺漏任何一個必要成員，在 <xref:System.Data.Linq.ChangeConflictException> 期間會擲回 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> (「資料列找不到，或者已變更」)。</span><span class="sxs-lookup"><span data-stu-id="725c6-182">If any one of these required members is missing, a <xref:System.Data.Linq.ChangeConflictException> is thrown during <xref:System.Data.Linq.DataContext.SubmitChanges%2A> ("Row not found or changed").</span></span>  
  
### <a name="state"></a><span data-ttu-id="725c6-183">State</span><span class="sxs-lookup"><span data-stu-id="725c6-183">State</span></span>  

 <span data-ttu-id="725c6-184">實體物件在附加到 <xref:System.Data.Linq.DataContext> 執行個體之後，會視為處於 `PossiblyModified` 狀態。</span><span class="sxs-lookup"><span data-stu-id="725c6-184">After an entity object is attached to the <xref:System.Data.Linq.DataContext> instance, the object is considered to be in the `PossiblyModified` state.</span></span> <span data-ttu-id="725c6-185">有三種方式可將附加物件強制視為 `Modified`。</span><span class="sxs-lookup"><span data-stu-id="725c6-185">There are three ways to force an attached object to be considered `Modified`.</span></span>  
  
1. <span data-ttu-id="725c6-186">以未修改的形式附加，再執行修改欄位。</span><span class="sxs-lookup"><span data-stu-id="725c6-186">Attach it as unmodified, and then directly modify the fields.</span></span>  
  
2. <span data-ttu-id="725c6-187">使用接受目前和原始物件執行個體的 <xref:System.Data.Linq.Table%601.Attach%2A> 多載附加。</span><span class="sxs-lookup"><span data-stu-id="725c6-187">Attach it with the <xref:System.Data.Linq.Table%601.Attach%2A> overload that takes current and original object instances.</span></span> <span data-ttu-id="725c6-188">這會將新舊值一起提供給變更 Tracker，這樣它就會自動得知哪些欄位已變更。</span><span class="sxs-lookup"><span data-stu-id="725c6-188">This supplies the change tracker with old and new values so that it will automatically know which fields have changed.</span></span>  
  
3. <span data-ttu-id="725c6-189">使用接受第二個布林值參數 (設為 true) 的 <xref:System.Data.Linq.Table%601.Attach%2A> 多載附加。</span><span class="sxs-lookup"><span data-stu-id="725c6-189">Attach it with the <xref:System.Data.Linq.Table%601.Attach%2A> overload that takes a second Boolean parameter (set to true).</span></span> <span data-ttu-id="725c6-190">這會指示變更 Tracker 將物件視為已修改，而無須提供任何原始值。</span><span class="sxs-lookup"><span data-stu-id="725c6-190">This will tell the change tracker to consider the object modified without having to supply any original values.</span></span> <span data-ttu-id="725c6-191">在此方式中，物件必須有版本/時間戳記欄位。</span><span class="sxs-lookup"><span data-stu-id="725c6-191">In this approach, the object must have a version/timestamp field.</span></span>  
  
 <span data-ttu-id="725c6-192">如需詳細資訊，請參閱 [物件狀態和變更追蹤](object-states-and-change-tracking.md)。</span><span class="sxs-lookup"><span data-stu-id="725c6-192">For more information, see [Object States and Change-Tracking](object-states-and-change-tracking.md).</span></span>  
  
 <span data-ttu-id="725c6-193">如果實體物件已出現在 ID 快取，而其識別與要附加的物件相同，就會擲回 <xref:System.Data.Linq.DuplicateKeyException>。</span><span class="sxs-lookup"><span data-stu-id="725c6-193">If an entity object already occurs in the ID Cache with the same identity as the object being attached, a <xref:System.Data.Linq.DuplicateKeyException> is thrown.</span></span>  
  
 <span data-ttu-id="725c6-194">當您使用一組 `IEnumerable` 物件附加時，若有已經存在的索引鍵出現時，會擲回 <xref:System.Data.Linq.DuplicateKeyException>。</span><span class="sxs-lookup"><span data-stu-id="725c6-194">When you attach with an `IEnumerable` set of objects, a <xref:System.Data.Linq.DuplicateKeyException> is thrown when an already existing key is present.</span></span> <span data-ttu-id="725c6-195">其餘的物件將不會附加。</span><span class="sxs-lookup"><span data-stu-id="725c6-195">Remaining objects are not attached.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="725c6-196">另請參閱</span><span class="sxs-lookup"><span data-stu-id="725c6-196">See also</span></span>

- [<span data-ttu-id="725c6-197">多層式架構和遠端應用程式以及 LINQ to SQL</span><span class="sxs-lookup"><span data-stu-id="725c6-197">N-Tier and Remote Applications with LINQ to SQL</span></span>](n-tier-and-remote-applications-with-linq-to-sql.md)
- [<span data-ttu-id="725c6-198">背景資訊</span><span class="sxs-lookup"><span data-stu-id="725c6-198">Background Information</span></span>](background-information.md)
