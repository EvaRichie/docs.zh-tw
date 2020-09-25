---
title: 使用 ASP.NET Core 應用程式中的資料
description: 使用 ASP.NET Core 和 Azure 架構現代化 Web 應用程式 | 使用 ASP.NET Core 應用程式中的資料
author: ardalis
ms.author: wiwagn
ms.date: 08/12/2020
no-loc:
- Blazor
- WebAssembly
ms.openlocfilehash: 4668922de8f0efc775acf6e505d56143b7ead8e7
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169059"
---
# <a name="working-with-data-in-aspnet-core-apps"></a><span data-ttu-id="f8011-103">使用 ASP.NET Core 應用程式中的資料</span><span class="sxs-lookup"><span data-stu-id="f8011-103">Working with Data in ASP.NET Core Apps</span></span>

> <span data-ttu-id="f8011-104">「資料是非常寶貴的資產，而且比系統本身擁有更長久的價值。」</span><span class="sxs-lookup"><span data-stu-id="f8011-104">"Data is a precious thing and will last longer than the systems themselves."</span></span>
>
> <span data-ttu-id="f8011-105">Tim Berners-Lee</span><span class="sxs-lookup"><span data-stu-id="f8011-105">Tim Berners-Lee</span></span>

<span data-ttu-id="f8011-106">對所有軟體應用程式來說，資料存取都是非常重要的一部分。</span><span class="sxs-lookup"><span data-stu-id="f8011-106">Data access is an important part of almost any software application.</span></span> <span data-ttu-id="f8011-107">ASP.NET Core 支援各種不同的資料存取選項，包括 Entity Framework Core (和 Entity Framework 6)，並可使用任何 .NET 資料存取架構。</span><span class="sxs-lookup"><span data-stu-id="f8011-107">ASP.NET Core supports a variety of data access options, including Entity Framework Core (and Entity Framework 6 as well), and can work with any .NET data access framework.</span></span> <span data-ttu-id="f8011-108">至於要選擇使用哪種資料存取架構，則取決於應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="f8011-108">The choice of which data access framework to use depends on the application's needs.</span></span> <span data-ttu-id="f8011-109">您可以將這些選項從 ApplicationCore 和 UI 專案中抽離出來，並將實作詳細資料封裝到基礎結構中，以協助產生相依性低的可測試軟體。</span><span class="sxs-lookup"><span data-stu-id="f8011-109">Abstracting these choices from the ApplicationCore and UI projects, and encapsulating implementation details in Infrastructure, helps to produce loosely coupled, testable software.</span></span>

## <a name="entity-framework-core-for-relational-databases"></a><span data-ttu-id="f8011-110">Entity Framework Core (適用於關聯式資料庫)</span><span class="sxs-lookup"><span data-stu-id="f8011-110">Entity Framework Core (for relational databases)</span></span>

<span data-ttu-id="f8011-111">如果您要撰寫的新 ASP.NET Core 應用程式需要使用關聯式資料，建議您讓應用程式使用 Entity Framework Core (EF Core) 來存取資料。</span><span class="sxs-lookup"><span data-stu-id="f8011-111">If you're writing a new ASP.NET Core application that needs to work with relational data, then Entity Framework Core (EF Core) is the recommended way for your application to access its data.</span></span> <span data-ttu-id="f8011-112">EF Core 是一種物件關聯式對應程式 (O/RM)，可讓 .NET 開發人員保存要進出資料來源的物件。</span><span class="sxs-lookup"><span data-stu-id="f8011-112">EF Core is an object-relational mapper (O/RM) that enables .NET developers to persist objects to and from a data source.</span></span> <span data-ttu-id="f8011-113">它可以讓開發人員免除一般需要撰寫的大多數資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="f8011-113">It eliminates the need for most of the data access code developers would typically need to write.</span></span> <span data-ttu-id="f8011-114">EF Core 和 ASP.NET Core 一樣，已經過從頭改寫以支援模組化跨平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8011-114">Like ASP.NET Core, EF Core has been rewritten from the ground up to support modular cross-platform applications.</span></span> <span data-ttu-id="f8011-115">您可以將它以 NuGet 套件形式新增至應用程式，並於 啟動時進行設定，再視需要透過相依性插入對其提出要求。</span><span class="sxs-lookup"><span data-stu-id="f8011-115">You add it to your application as a NuGet package, configure it in Startup, and request it through dependency injection wherever you need it.</span></span>

<span data-ttu-id="f8011-116">若要搭配使用 EF Core 與 SQL Server 資料庫，請執行下列 dotnet CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="f8011-116">To use EF Core with a SQL Server database, run the following dotnet CLI command:</span></span>

```dotnetcli
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

<span data-ttu-id="f8011-117">若要新增對 InMemory 資料來源的支援以進行測試：</span><span class="sxs-lookup"><span data-stu-id="f8011-117">To add support for an InMemory data source, for testing:</span></span>

```dotnetcli
dotnet add package Microsoft.EntityFrameworkCore.InMemory
```

### <a name="the-dbcontext"></a><span data-ttu-id="f8011-118">DbContext</span><span class="sxs-lookup"><span data-stu-id="f8011-118">The DbContext</span></span>

<span data-ttu-id="f8011-119">若要使用 EF Core，您需要 <xref:Microsoft.EntityFrameworkCore.DbContext> 的子類別。</span><span class="sxs-lookup"><span data-stu-id="f8011-119">To work with EF Core, you need a subclass of <xref:Microsoft.EntityFrameworkCore.DbContext>.</span></span> <span data-ttu-id="f8011-120">這個類別包含的屬性代表應用程式會用到的實體集合。</span><span class="sxs-lookup"><span data-stu-id="f8011-120">This class holds properties representing collections of the entities your application will work with.</span></span> <span data-ttu-id="f8011-121">eShopOnWeb 範例包括 CatalogContext 以及項目、品牌和類型的集合：</span><span class="sxs-lookup"><span data-stu-id="f8011-121">The eShopOnWeb sample includes a CatalogContext with collections for items, brands, and types:</span></span>

```csharp
public class CatalogContext : DbContext
{
    public CatalogContext(DbContextOptions<CatalogContext> options) : base(options)
    {

    }

    public DbSet<CatalogItem> CatalogItems { get; set; }

    public DbSet<CatalogBrand> CatalogBrands { get; set; }

    public DbSet<CatalogType> CatalogTypes { get; set; }
}
```

<span data-ttu-id="f8011-122">您的 DbContext 必須具備可接受 DbContextOptions 的建構函式，並將此引數傳遞給基底 DbContext 建構函式。</span><span class="sxs-lookup"><span data-stu-id="f8011-122">Your DbContext must have a constructor that accepts DbContextOptions and pass this argument to the base DbContext constructor.</span></span> <span data-ttu-id="f8011-123">如果您的應用程式中只有一個 DbCoNtext，您可以傳遞 DbCoNtextOptions 的實例，但如果您有一個以上的實例，就必須使用泛型 DbCoNtextOptions \<T> 類型，並傳入 DbCoNtext 型別做為泛型參數。</span><span class="sxs-lookup"><span data-stu-id="f8011-123">If you have only one DbContext in your application, you can pass an instance of DbContextOptions, but if you have more than one you must use the generic DbContextOptions\<T> type, passing in your DbContext type as the generic parameter.</span></span>

### <a name="configuring-ef-core"></a><span data-ttu-id="f8011-124">設定 EF Core</span><span class="sxs-lookup"><span data-stu-id="f8011-124">Configuring EF Core</span></span>

<span data-ttu-id="f8011-125">一般來說，您需要在 ASP.NET Core 應用程式的 ConfigureServices 方法中設定 EF Core。</span><span class="sxs-lookup"><span data-stu-id="f8011-125">In your ASP.NET Core application, you'll typically configure EF Core in your ConfigureServices method.</span></span> <span data-ttu-id="f8011-126">EF Core 使用的 DbContextOptionsBuilder 可支援幾項實用的擴充方法，以簡化其組態。</span><span class="sxs-lookup"><span data-stu-id="f8011-126">EF Core uses a DbContextOptionsBuilder, which supports several helpful extension methods to streamline its configuration.</span></span> <span data-ttu-id="f8011-127">若要將 CatalogContext 設定為搭配使用 SQL Server 資料庫與 [組態] 中定義的連接字串，您可以將下列程式碼新增至 ConfigureServices：</span><span class="sxs-lookup"><span data-stu-id="f8011-127">To configure CatalogContext to use a SQL Server database with a connection string defined in Configuration, you would add the following code to ConfigureServices:</span></span>

```csharp
services.AddDbContext<CatalogContext>(options => options.UseSqlServer (Configuration.GetConnectionString("DefaultConnection")));
```

<span data-ttu-id="f8011-128">若要使用記憶體內部資料庫：</span><span class="sxs-lookup"><span data-stu-id="f8011-128">To use the in-memory database:</span></span>

```csharp
services.AddDbContext<CatalogContext>(options =>
    options.UseInMemoryDatabase());
```

<span data-ttu-id="f8011-129">一旦您安裝好 EF Core、建立 DbContext 子類型，並在 ConfigureServices 中進行設定，即可使用 EF Core。</span><span class="sxs-lookup"><span data-stu-id="f8011-129">Once you have installed EF Core, created a DbContext child type, and configured it in ConfigureServices, you are ready to use EF Core.</span></span> <span data-ttu-id="f8011-130">您可以在任何需要 DbContext 類型執行個體的服務中，對其提出要求，並透過 LINQ 來使用您保存的實體，如同它們就在集合中一般。</span><span class="sxs-lookup"><span data-stu-id="f8011-130">You can request an instance of your DbContext type in any service that needs it, and start working with your persisted entities using LINQ as if they were simply in a collection.</span></span> <span data-ttu-id="f8011-131">EF Core 會將您的 LINQ 運算式轉譯為 SQL 查詢以儲存和擷取資料。</span><span class="sxs-lookup"><span data-stu-id="f8011-131">EF Core does the work of translating your LINQ expressions into SQL queries to store and retrieve your data.</span></span>

<span data-ttu-id="f8011-132">EF Core 會設定記錄器，並確保其層級至少設定為「資訊」以執行查詢，如圖 8-1 所示。</span><span class="sxs-lookup"><span data-stu-id="f8011-132">You can see the queries EF Core is executing by configuring a logger and ensuring its level is set to at least Information, as shown in Figure 8-1.</span></span>

![記錄 EF Core 對主控台的查詢](./media/image8-1.png)

<span data-ttu-id="f8011-134">**圖 8-1**：</span><span class="sxs-lookup"><span data-stu-id="f8011-134">**Figure 8-1**.</span></span> <span data-ttu-id="f8011-135">記錄 EF Core 對主控台的查詢</span><span class="sxs-lookup"><span data-stu-id="f8011-135">Logging EF Core queries to the console</span></span>

### <a name="fetching-and-storing-data"></a><span data-ttu-id="f8011-136">擷取與儲存資料</span><span class="sxs-lookup"><span data-stu-id="f8011-136">Fetching and storing Data</span></span>

<span data-ttu-id="f8011-137">若要從 EF Core 擷取資料，您可以存取適當的屬性，並使用 LINQ 篩選結果。</span><span class="sxs-lookup"><span data-stu-id="f8011-137">To retrieve data from EF Core, you access the appropriate property and use LINQ to filter the result.</span></span> <span data-ttu-id="f8011-138">您也可以使用 LINQ 來執行投影，將某種類的結果轉換到另一種類型。</span><span class="sxs-lookup"><span data-stu-id="f8011-138">You can also use LINQ to perform projection, transforming the result from one type to another.</span></span> <span data-ttu-id="f8011-139">下列範例會擷取 CatalogBrands，並依名稱排序、依 Enabled 屬性篩選，然後投射到 SelectListItem 類型：</span><span class="sxs-lookup"><span data-stu-id="f8011-139">The following example would retrieve CatalogBrands, ordered by name, filtered by their Enabled property, and projected onto a SelectListItem type:</span></span>

```csharp
var brandItems = await _context.CatalogBrands
    .Where(b => b.Enabled)
    .OrderBy(b => b.Name)
    .Select(b => new SelectListItem {
        Value = b.Id, Text = b.Name })
    .ToListAsync();
```

<span data-ttu-id="f8011-140">請務必在上述範例中新增 ToListAsync 呼叫，以立即執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f8011-140">It's important in the above example to add the call to ToListAsync in order to execute the query immediately.</span></span> <span data-ttu-id="f8011-141">否則，陳述式會指派 IQueryable\<SelectListItem> 給 brandItem，直到系統列舉它時才執行。</span><span class="sxs-lookup"><span data-stu-id="f8011-141">Otherwise, the statement will assign an IQueryable\<SelectListItem> to brandItems, which will not be executed until it is enumerated.</span></span> <span data-ttu-id="f8011-142">從方法傳回 IQueryable 結果時，也有其優缺點。</span><span class="sxs-lookup"><span data-stu-id="f8011-142">There are pros and cons to returning IQueryable results from methods.</span></span> <span data-ttu-id="f8011-143">它可讓您進一步修改 EF Core 建構的查詢，但如果您將作業新增至 EF Core 不能轉譯的查詢時，也可能會出現只在執行階段發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8011-143">It allows the query EF Core will construct to be further modified, but can also result in errors that only occur at runtime, if operations are added to the query that EF Core cannot translate.</span></span> <span data-ttu-id="f8011-144">一般來說，比較安全的做法是將任何篩選條件傳遞給執行資料存取的方法，並傳回記憶體內部的集合 (例如，List\<T>) 作為結果。</span><span class="sxs-lookup"><span data-stu-id="f8011-144">It's generally safer to pass any filters into the method performing the data access, and return back an in-memory collection (for example, List\<T>) as the result.</span></span>

<span data-ttu-id="f8011-145">EF Core 會追蹤其從持續性儲存區擷取的實體變更。</span><span class="sxs-lookup"><span data-stu-id="f8011-145">EF Core tracks changes on entities it fetches from persistence.</span></span> <span data-ttu-id="f8011-146">若要儲存追蹤實體的變更，您只需要在 DbContext 上呼叫 SaveChanges 方法，並確定它是用來擷取實體的相同 DbContext 執行個體。</span><span class="sxs-lookup"><span data-stu-id="f8011-146">To save changes to a tracked entity, you just call the SaveChanges method on the DbContext, making sure it's the same DbContext instance that was used to fetch the entity.</span></span> <span data-ttu-id="f8011-147">新增和移除實體是直接在適當的 DbSet 屬性上完成，並再次地使用 SaveChanges 呼叫來執行資料庫命令。</span><span class="sxs-lookup"><span data-stu-id="f8011-147">Adding and removing entities is directly done on the appropriate DbSet property, again with a call to SaveChanges to execute the database commands.</span></span> <span data-ttu-id="f8011-148">下列範例示範如何新增、更新和移除持續性儲存區的實體。</span><span class="sxs-lookup"><span data-stu-id="f8011-148">The following example demonstrates adding, updating, and removing entities from persistence.</span></span>

```csharp
// create
var newBrand = new CatalogBrand() { Brand = "Acme" };
_context.Add(newBrand);
await _context.SaveChangesAsync();

// read and update
var existingBrand = _context.CatalogBrands.Find(1);
existingBrand.Brand = "Updated Brand";
await _context.SaveChangesAsync();

// read and delete (alternate Find syntax)
var brandToDelete = _context.Find<CatalogBrand>(2);
_context.CatalogBrands.Remove(brandToDelete);
await _context.SaveChangesAsync();
```

<span data-ttu-id="f8011-149">EF Core 支援擷取和儲存的同步與非同步的方法。</span><span class="sxs-lookup"><span data-stu-id="f8011-149">EF Core supports both synchronous and async methods for fetching and saving.</span></span> <span data-ttu-id="f8011-150">若是 Web 應用程式，建議搭配使用非同步方法與非同步/等候模式，Web 伺服器執行緒才不會在等候資料存取作業完成期間受到封鎖。</span><span class="sxs-lookup"><span data-stu-id="f8011-150">In web applications, it's recommended to use the async/await pattern with the async methods, so that web server threads are not blocked while waiting for data access operations to complete.</span></span>

### <a name="fetching-related-data"></a><span data-ttu-id="f8011-151">擷取相關資料</span><span class="sxs-lookup"><span data-stu-id="f8011-151">Fetching related data</span></span>

<span data-ttu-id="f8011-152">當 EF Core 擷取實體時，它會填入與資料庫中的這個實體一起儲存的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="f8011-152">When EF Core retrieves entities, it populates all of the properties that are stored directly with that entity in the database.</span></span> <span data-ttu-id="f8011-153">EF Core 不會填入相關實體清單這類導覽屬性，且可能會將其值設為 Null。</span><span class="sxs-lookup"><span data-stu-id="f8011-153">Navigation properties, such as lists of related entities, are not populated and may have their value set to null.</span></span> <span data-ttu-id="f8011-154">這可確保 EF Core 不會擷取超過實際所需的資料，這對 Web 應用程式來說尤其重要，因為這類應用程式必須快速處理要求，並以有效率的方式傳回回應。</span><span class="sxs-lookup"><span data-stu-id="f8011-154">This ensures EF Core is not fetching more data than is needed, which is especially important for web applications, which must quickly process requests and return responses in an efficient manner.</span></span> <span data-ttu-id="f8011-155">若要使用「積極式載入」__ 來包含實體的關聯性，您可以在查詢中使用 Include 擴充方法以指定屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f8011-155">To include relationships with an entity using _eager loading_, you specify the property using the Include extension method on the query, as shown:</span></span>

```csharp
// .Include requires using Microsoft.EntityFrameworkCore
var brandsWithItems = await _context.CatalogBrands
    .Include(b => b.Items)
    .ToListAsync();
```

<span data-ttu-id="f8011-156">您可以包含多個關聯性，也可以使用 >theninclude 包含 subrelationships。</span><span class="sxs-lookup"><span data-stu-id="f8011-156">You can include multiple relationships, and you can also include subrelationships using ThenInclude.</span></span> <span data-ttu-id="f8011-157">EF Core 會執行單一查詢來擷取產生的實體集。</span><span class="sxs-lookup"><span data-stu-id="f8011-157">EF Core will execute a single query to retrieve the resulting set of entities.</span></span> <span data-ttu-id="f8011-158">或者您可以藉由將以 '.' 分隔的字串傳遞至 `.Include()` 擴充方法，來包含導覽屬性的導覽屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f8011-158">Alternately you can include navigation properties of navigation properties by passing a '.'-separated string to the `.Include()` extension method, like so:</span></span>

```csharp
    .Include("Items.Products")
```

<span data-ttu-id="f8011-159">除了封裝篩選邏輯，規格還可以指定要傳回的資料形式，包括要填入的屬性。</span><span class="sxs-lookup"><span data-stu-id="f8011-159">In addition to encapsulating filtering logic, a specification can specify the shape of the data to be returned, including which properties to populate.</span></span> <span data-ttu-id="f8011-160">eShopOnWeb 範例包括數個示範在規格中封裝積極式載入資訊的規格。</span><span class="sxs-lookup"><span data-stu-id="f8011-160">The eShopOnWeb sample includes several specifications that demonstrate encapsulating eager loading information within the specification.</span></span> <span data-ttu-id="f8011-161">您可以在這裡了解規格如何作為查詢的一部份使用：</span><span class="sxs-lookup"><span data-stu-id="f8011-161">You can see how the specification is used as part of a query here:</span></span>

```csharp
// Includes all expression-based includes
query = specification.Includes.Aggregate(query,
            (current, include) => current.Include(include));

// Include any string-based include statements
query = specification.IncludeStrings.Aggregate(query,
            (current, include) => current.Include(include));
```

<span data-ttu-id="f8011-162">另一個用來載入相關資料的選項是使用「明確式載入」__。</span><span class="sxs-lookup"><span data-stu-id="f8011-162">Another option for loading related data is to use _explicit loading_.</span></span> <span data-ttu-id="f8011-163">明確式載入可讓您將其他資料載入已擷取的實體中。</span><span class="sxs-lookup"><span data-stu-id="f8011-163">Explicit loading allows you to load additional data into an entity that has already been retrieved.</span></span> <span data-ttu-id="f8011-164">由於這牽涉到資料庫的個別要求，因此不建議用於 Web 應用程式，而應該將每項要求的資料庫往返次數降至最低。</span><span class="sxs-lookup"><span data-stu-id="f8011-164">Since this involves a separate request to the database, it's not recommended for web applications, which should minimize the number of database round trips made per request.</span></span>

<span data-ttu-id="f8011-165">「消極式載入」__ 功能會自動載入應用程式參考的相關資料。</span><span class="sxs-lookup"><span data-stu-id="f8011-165">_Lazy loading_ is a feature that automatically loads related data as it is referenced by the application.</span></span> <span data-ttu-id="f8011-166">EF Core 已在 2.1 版中新增對消極式載入的支援。</span><span class="sxs-lookup"><span data-stu-id="f8011-166">EF Core has added support for lazy loading in version 2.1.</span></span> <span data-ttu-id="f8011-167">消極式載入預設不會啟用，而且需要安裝 `Microsoft.EntityFrameworkCore.Proxies`。</span><span class="sxs-lookup"><span data-stu-id="f8011-167">Lazy loading is not enabled by default and requires installing the `Microsoft.EntityFrameworkCore.Proxies`.</span></span> <span data-ttu-id="f8011-168">如同明確式載入，通常應該為 Web 應用程式停用消極式載入，因為其使用會導致在每個 Web 要求中發出額外的資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="f8011-168">As with explicit loading, lazy loading should typically be disabled for web applications, since its use will result in additional database queries being made within each web request.</span></span> <span data-ttu-id="f8011-169">不幸的是，當延遲很小且用於測試的資料集通常很小時，消極式載入所產生的額外負荷往往在開發期間不易察覺。</span><span class="sxs-lookup"><span data-stu-id="f8011-169">Unfortunately, the overhead incurred by lazy loading often goes unnoticed at development time, when latency is small and often the data sets used for testing are small.</span></span> <span data-ttu-id="f8011-170">不過，在生產環境中，由於使用者、資料和延遲更多，額外的資料庫要求通常會導致 Web 應用程式大量使用消極式載入而效能不佳。</span><span class="sxs-lookup"><span data-stu-id="f8011-170">However, in production, with more users, more data, and more latency, the additional database requests can often result in poor performance for web applications that make heavy use of lazy loading.</span></span>

[<span data-ttu-id="f8011-171">避免在 Web 應用程式中消極載入實體</span><span class="sxs-lookup"><span data-stu-id="f8011-171">Avoid Lazy Loading Entities in Web Applications</span></span>](https://ardalis.com/avoid-lazy-loading-entities-in-asp-net-applications)

### <a name="encapsulating-data"></a><span data-ttu-id="f8011-172">封裝資料</span><span class="sxs-lookup"><span data-stu-id="f8011-172">Encapsulating data</span></span>

<span data-ttu-id="f8011-173">EF Core 支援多種功能，可讓您的模型正確封裝其狀態。</span><span class="sxs-lookup"><span data-stu-id="f8011-173">EF Core supports several features that allow your model to properly encapsulate its state.</span></span> <span data-ttu-id="f8011-174">領域模型中的常見問題之一便是他們會將集合導覽屬性作為可公開存取的清單類型公開。</span><span class="sxs-lookup"><span data-stu-id="f8011-174">A common problem in domain models is that they expose collection navigation properties as publicly accessible list types.</span></span> <span data-ttu-id="f8011-175">這可讓任何共同作業者操縱這些集合類型的內容，使其略過與集合相關的重要商務規則，並可能讓物件處於無效狀態。</span><span class="sxs-lookup"><span data-stu-id="f8011-175">This allows any collaborator to manipulate the contents of these collection types, which may bypass important business rules related to the collection, possibly leaving the object in an invalid state.</span></span> <span data-ttu-id="f8011-176">其解決方案便是公開相關集合的唯讀存取，並明確提供定義用戶端可操縱他們之方式的方法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="f8011-176">The solution to this is to expose read-only access to related collections, and explicitly provide methods defining ways in which clients can manipulate them, as in this example:</span></span>

```csharp
public class Basket : BaseEntity
{
    public string BuyerId { get; set; }
    private readonly List<BasketItem> _items = new List<BasketItem>();
    public IReadOnlyCollection<BasketItem> Items => _items.AsReadOnly();

    public void AddItem(int catalogItemId, decimal unitPrice, int quantity = 1)
    {
        if (!Items.Any(i => i.CatalogItemId == catalogItemId))
        {
            _items.Add(new BasketItem()
            {
                CatalogItemId = catalogItemId,
                Quantity = quantity,
                UnitPrice = unitPrice
            });
            return;
        }
        var existingItem = Items.FirstOrDefault(i => i.CatalogItemId == catalogItemId);
        existingItem.Quantity += quantity;
    }
}
```

<span data-ttu-id="f8011-177">此實體類型不會公開公用 `List` 或 `ICollection` 屬性，而是會公開 `IReadOnlyCollection` 包裝基礎清單類型的類型。</span><span class="sxs-lookup"><span data-stu-id="f8011-177">This entity type doesn't expose a public `List` or `ICollection` property, but instead exposes an `IReadOnlyCollection` type that wraps the underlying List type.</span></span> <span data-ttu-id="f8011-178">在使用這個模式時，您可以透過 Entity Framework Core 來使用支援欄位，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f8011-178">When using this pattern, you can indicate to Entity Framework Core to use the backing field like so:</span></span>

```csharp
private void ConfigureBasket(EntityTypeBuilder<Basket> builder)
{
    var navigation = builder.Metadata.FindNavigation(nameof(Basket.Items));

    navigation.SetPropertyAccessMode(PropertyAccessMode.Field);
}
```

<span data-ttu-id="f8011-179">另一種可供您改進領域模型的方式是使用缺少身分識別並只能由其屬性來辨別之類型的值物件。</span><span class="sxs-lookup"><span data-stu-id="f8011-179">Another way in which you can improve your domain model is through the use of value objects for types that lack identity and are only distinguished by their properties.</span></span> <span data-ttu-id="f8011-180">使用這種類型作為您實體的屬性，可協助保持邏輯專屬於其所屬值物件，並可避免使用相同概念的多個實體間出現重複的邏輯。</span><span class="sxs-lookup"><span data-stu-id="f8011-180">Using such types as properties of your entities can help keep logic specific to the value object where it belongs, and can avoid duplicate logic between multiple entities that use the same concept.</span></span> <span data-ttu-id="f8011-181">在 Entity Framework Core 中，您可以藉由將類型設定為自有實體，來使值物件保留在與其專屬實體相同的資料表中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f8011-181">In Entity Framework Core, you can persist value objects in the same table as their owning entity by configuring the type as an owned entity, like so:</span></span>

```csharp
private void ConfigureOrder(EntityTypeBuilder<Order> builder)
{
    builder.OwnsOne(o => o.ShipToAddress);
}
```

<span data-ttu-id="f8011-182">在此範例中，`ShipToAddress` 屬性的類型為 `Address`。</span><span class="sxs-lookup"><span data-stu-id="f8011-182">In this example, the `ShipToAddress` property is of type `Address`.</span></span> <span data-ttu-id="f8011-183">`Address` 是擁有多個屬性 (例如 `Street` 及 `City`) 的值物件。</span><span class="sxs-lookup"><span data-stu-id="f8011-183">`Address` is a value object with several properties such as `Street` and `City`.</span></span> <span data-ttu-id="f8011-184">EF Core 以每個 `Order` 屬性一個資料行來將 `Address` 物件對應到其資料表，並以屬性名稱作為每個資料行名稱的開頭。</span><span class="sxs-lookup"><span data-stu-id="f8011-184">EF Core maps the `Order` object to its table with one column per `Address` property, prefixing each column name with the name of the property.</span></span> <span data-ttu-id="f8011-185">在這個範例中，`Order` 資料表會包含像是 `ShipToAddress_Street` 及 `ShipToAddress_City` 的資料行。</span><span class="sxs-lookup"><span data-stu-id="f8011-185">In this example, the `Order` table would include columns such as `ShipToAddress_Street` and `ShipToAddress_City`.</span></span> <span data-ttu-id="f8011-186">您也可以視需要將擁有的類型儲存在個別的資料表中。</span><span class="sxs-lookup"><span data-stu-id="f8011-186">It's also possible to store owned types in separate tables, if desired.</span></span>

<span data-ttu-id="f8011-187">[在 EF Core 中深入瞭解擁有的實體支援](/ef/core/modeling/owned-entities)。</span><span class="sxs-lookup"><span data-stu-id="f8011-187">Learn more about owned [entity support in EF Core](/ef/core/modeling/owned-entities).</span></span>

### <a name="resilient-connections"></a><span data-ttu-id="f8011-188">具復原功能的連接</span><span class="sxs-lookup"><span data-stu-id="f8011-188">Resilient connections</span></span>

<span data-ttu-id="f8011-189">有時您可能會無法使用 SQL 資料庫等外部資源。</span><span class="sxs-lookup"><span data-stu-id="f8011-189">External resources like SQL databases may occasionally be unavailable.</span></span> <span data-ttu-id="f8011-190">在暫時無法使用的情況下，應用程式可以使用重試邏輯，以避免引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f8011-190">In cases of temporary unavailability, applications can use retry logic to avoid raising an exception.</span></span> <span data-ttu-id="f8011-191">這項技術通常稱為「連線復原能力」__。</span><span class="sxs-lookup"><span data-stu-id="f8011-191">This technique is commonly referred to as _connection resiliency_.</span></span> <span data-ttu-id="f8011-192">您可以重試某項作業，並以指數方式增加等候時間，直到已達重試計數上限為止，藉此實作[使用指數輪詢重試](/azure/architecture/patterns/retry)技術。</span><span class="sxs-lookup"><span data-stu-id="f8011-192">You can implement your [own retry with exponential backoff](/azure/architecture/patterns/retry) technique by attempting to retry with an exponentially increasing wait time, until a maximum retry count has been reached.</span></span> <span data-ttu-id="f8011-193">這項技術是為了因應雲端資源可能會在短時間內斷斷續續無法使用，而導致某些要求失敗的問題。</span><span class="sxs-lookup"><span data-stu-id="f8011-193">This technique embraces the fact that cloud resources might intermittently be unavailable for short periods of time, resulting in failure of some requests.</span></span>

<span data-ttu-id="f8011-194">在 Azure SQL DB 中，Entity Framework Core 已提供內部資料庫恢復連接功能和重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="f8011-194">For Azure SQL DB, Entity Framework Core already provides internal database connection resiliency and retry logic.</span></span> <span data-ttu-id="f8011-195">如果您想要使用具復原功能的 EF Core 連線，則必須為每個 DbContext 連線啟用 Entity Framework 執行策略。</span><span class="sxs-lookup"><span data-stu-id="f8011-195">But you need to enable the Entity Framework execution strategy for each DbContext connection if you want to have resilient EF Core connections.</span></span>

<span data-ttu-id="f8011-196">例如，EF Core 連接層級的下列程式碼可在連接失敗時重試具有恢復功能的 SQL 連接。</span><span class="sxs-lookup"><span data-stu-id="f8011-196">For instance, the following code at the EF Core connection level enables resilient SQL connections that are retried if the connection fails.</span></span>

```csharp
// Startup.cs from any ASP.NET Core Web API
public class Startup
{
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        //...
        services.AddDbContext<OrderingContext>(options =>
        {
            options.UseSqlServer(Configuration["ConnectionString"],
            sqlServerOptionsAction: sqlOptions =>
        {
            sqlOptions.EnableRetryOnFailure(
            maxRetryCount: 5,
            maxRetryDelay: TimeSpan.FromSeconds(30),
            errorNumbersToAdd: null);
        });
    });
}
//...
```

#### <a name="execution-strategies-and-explicit-transactions-using-begintransaction-and-multiple-dbcontexts"></a><span data-ttu-id="f8011-197">使用 BeginTransaction 和多個 DbContext 的執行策略和明確異動</span><span class="sxs-lookup"><span data-stu-id="f8011-197">Execution strategies and explicit transactions using BeginTransaction and multiple DbContexts</span></span>

<span data-ttu-id="f8011-198">在 EF Core 連接中啟用重試時，您使用 EF Core 執行的每項作業都會變成其本身可重試的作業。</span><span class="sxs-lookup"><span data-stu-id="f8011-198">When retries are enabled in EF Core connections, each operation you perform using EF Core becomes its own retryable operation.</span></span> <span data-ttu-id="f8011-199">如果發生暫時性失敗，SaveChanges 的每個查詢和每個呼叫會當做一個單位來重試。</span><span class="sxs-lookup"><span data-stu-id="f8011-199">Each query and each call to SaveChanges will be retried as a unit if a transient failure occurs.</span></span>

<span data-ttu-id="f8011-200">不過，如果您的程式碼使用 BeginTransaction 來起始異動，您將定義需視為一個單位的專屬作業群組；如果失敗，則必須復原異動內的所有項目。</span><span class="sxs-lookup"><span data-stu-id="f8011-200">However, if your code initiates a transaction using BeginTransaction, you are defining your own group of operations that need to be treated as a unit; everything inside the transaction has to be rolled back if a failure occurs.</span></span> <span data-ttu-id="f8011-201">如果您在使用 EF 執行策略 (重試原則) 時嘗試執行該交易，並在交易中包含來自多個 DbContext 的數個 SaveChanges，則會看到類似如下的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f8011-201">You will see an exception like the following if you attempt to execute that transaction when using an EF execution strategy (retry policy) and you include several SaveChanges from multiple DbContexts in it.</span></span>

<span data-ttu-id="f8011-202">System.InvalidOperationException：已設定的執行策略 'SqlServerRetryingExecutionStrategy' 不支援使用者起始的異動。</span><span class="sxs-lookup"><span data-stu-id="f8011-202">System.InvalidOperationException: The configured execution strategy 'SqlServerRetryingExecutionStrategy' does not support user initiated transactions.</span></span> <span data-ttu-id="f8011-203">使用 ' DbCoNtext. CreateExecutionStrategy ( # A1 ' 所傳回的執行策略，將交易中的所有作業以可重試的單位來執行。</span><span class="sxs-lookup"><span data-stu-id="f8011-203">Use the execution strategy returned by 'DbContext.Database.CreateExecutionStrategy()' to execute all the operations in the transaction as a retryable unit.</span></span>

<span data-ttu-id="f8011-204">解決方法是使用代表必須執行之所有項目的委派，來手動叫用 EF 執行策略。</span><span class="sxs-lookup"><span data-stu-id="f8011-204">The solution is to manually invoke the EF execution strategy with a delegate representing everything that needs to be executed.</span></span> <span data-ttu-id="f8011-205">如果發生暫時性失敗，執行策略會再次叫用委派。</span><span class="sxs-lookup"><span data-stu-id="f8011-205">If a transient failure occurs, the execution strategy will invoke the delegate again.</span></span> <span data-ttu-id="f8011-206">下列程式碼會示範如何實作這個方法：</span><span class="sxs-lookup"><span data-stu-id="f8011-206">The following code shows how to implement this approach:</span></span>

```csharp
// Use of an EF Core resiliency strategy when using multiple DbContexts
// within an explicit transaction
// See:
// https://docs.microsoft.com/ef/core/miscellaneous/connection-resiliency
var strategy = _catalogContext.Database.CreateExecutionStrategy();
await strategy.ExecuteAsync(async () =>
{
    // Achieving atomicity between original Catalog database operation and the
    // IntegrationEventLog thanks to a local transaction
    using (var transaction = _catalogContext.Database.BeginTransaction())
    {
        _catalogContext.CatalogItems.Update(catalogItem);
        await _catalogContext.SaveChangesAsync();

        // Save to EventLog only if product price changed
        if (raiseProductPriceChangedEvent)
            await _integrationEventLogService.SaveEventAsync(priceChangedEvent);
        transaction.Commit();
    }
});
```

<span data-ttu-id="f8011-207">第一個 DbContext 是 \_catalogContext，第二個 DbContext 則位於 \_integrationEventLogService 物件內。</span><span class="sxs-lookup"><span data-stu-id="f8011-207">The first DbContext is the \_catalogContext and the second DbContext is within the \_integrationEventLogService object.</span></span> <span data-ttu-id="f8011-208">最後，系統會使用 EF 執行策略執行多個 DbContext 的認可動作。</span><span class="sxs-lookup"><span data-stu-id="f8011-208">Finally, the Commit action would be performed multiple DbContexts and using an EF Execution Strategy.</span></span>

> ### <a name="references--entity-framework-core"></a><span data-ttu-id="f8011-209">參考資料 – Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="f8011-209">References – Entity Framework Core</span></span>
>
> - <span data-ttu-id="f8011-210">**EF Core 檔**
>   <https://docs.microsoft.com/ef/></span><span class="sxs-lookup"><span data-stu-id="f8011-210">**EF Core Docs**
<https://docs.microsoft.com/ef/></span></span>
> - <span data-ttu-id="f8011-211">**EF Core：相關資料**
>   <https://docs.microsoft.com/ef/core/querying/related-data></span><span class="sxs-lookup"><span data-stu-id="f8011-211">**EF Core: Related Data**
<https://docs.microsoft.com/ef/core/querying/related-data></span></span>
> - <span data-ttu-id="f8011-212">**避免在 ASPNET 應用程式中延遲載入實體**
>   <https://ardalis.com/avoid-lazy-loading-entities-in-asp-net-applications></span><span class="sxs-lookup"><span data-stu-id="f8011-212">**Avoid Lazy Loading Entities in ASPNET Applications**
<https://ardalis.com/avoid-lazy-loading-entities-in-asp-net-applications></span></span>

## <a name="ef-core-or-micro-orm"></a><span data-ttu-id="f8011-213">該使用 EF Core 或微型 ORM？</span><span class="sxs-lookup"><span data-stu-id="f8011-213">EF Core or micro-ORM?</span></span>

<span data-ttu-id="f8011-214">雖然 EF Core 是管理持續性的絕佳選擇，但在大部分的情況下，封裝應用程式開發人員的資料庫詳細資料並不是唯一的選擇。</span><span class="sxs-lookup"><span data-stu-id="f8011-214">While EF Core is a great choice for managing persistence, and for the most part encapsulates database details from application developers, it isn't the only choice.</span></span> <span data-ttu-id="f8011-215">另一個常用的開放原始碼替代方案是 [Dapper](https://github.com/StackExchange/Dapper)，也就是所謂的微型 ORM。</span><span class="sxs-lookup"><span data-stu-id="f8011-215">Another popular open-source alternative is [Dapper](https://github.com/StackExchange/Dapper), a so-called micro-ORM.</span></span> <span data-ttu-id="f8011-216">微型 ORM 是一種功能較簡單的輕量型工具，可將物件對應至資料結構。</span><span class="sxs-lookup"><span data-stu-id="f8011-216">A micro-ORM is a lightweight, less full-featured tool for mapping objects to data structures.</span></span> <span data-ttu-id="f8011-217">舉 Dapper 為例，其設計目標著重在效能，而非完整封裝用來擷取和更新資料的基礎查詢。</span><span class="sxs-lookup"><span data-stu-id="f8011-217">In the case of Dapper, its design goals focus on performance, rather than fully encapsulating the underlying queries it uses to retrieve and update data.</span></span> <span data-ttu-id="f8011-218">因為 Dapper 不需要開發人員完全抽離 SQL，所以是比較單純的「試用版」，可讓開發人員撰寫想用於指定資料存取作業的確切查詢。</span><span class="sxs-lookup"><span data-stu-id="f8011-218">Because it doesn't abstract SQL from the developer, Dapper is "closer to the metal" and lets developers write the exact queries they want to use for a given data access operation.</span></span>

<span data-ttu-id="f8011-219">EF Core 與 Dapper 的主要差異是前者提供下列兩個重要的功能，但這也會對效能產生額外負荷。</span><span class="sxs-lookup"><span data-stu-id="f8011-219">EF Core has two significant features it provides which separate it from Dapper but also add to its performance overhead.</span></span> <span data-ttu-id="f8011-220">第一個是它會將 LINQ 運算式轉譯為 SQL。</span><span class="sxs-lookup"><span data-stu-id="f8011-220">The first is translation from LINQ expressions into SQL.</span></span> <span data-ttu-id="f8011-221">雖然系統會快取這些轉譯，第一次執行時仍會產生額外負荷。</span><span class="sxs-lookup"><span data-stu-id="f8011-221">These translations are cached, but even so there is overhead in performing them the first time.</span></span> <span data-ttu-id="f8011-222">第二個是追蹤實體的變更 (以便產生有效的 UPDATE 陳述式)。</span><span class="sxs-lookup"><span data-stu-id="f8011-222">The second is change tracking on entities (so that efficient update statements can be generated).</span></span> <span data-ttu-id="f8011-223">您可以使用 AsNotTracking 延伸模組，將特定查詢的這項行為關閉。</span><span class="sxs-lookup"><span data-stu-id="f8011-223">This behavior can be turned off for specific queries by using the AsNotTracking extension.</span></span> <span data-ttu-id="f8011-224">EF Core 也會產生非常有效率的 SQL 查詢，而且在任何情況下，效能都是完全可以接受的等級；但如果您需要妥善控制要執行的精確查詢，您也可以使用 EF Core 傳入自訂的 SQL (或執行預存程序)。</span><span class="sxs-lookup"><span data-stu-id="f8011-224">EF Core also generates SQL queries that usually are very efficient and in any case perfectly acceptable from a performance standpoint, but if you need fine control over the precise query to be executed, you can pass in custom SQL (or execute a stored procedure) using EF Core, too.</span></span> <span data-ttu-id="f8011-225">在這種情況下，Dapper 就略勝於 EF Core。</span><span class="sxs-lookup"><span data-stu-id="f8011-225">In this case, Dapper still outperforms EF Core, but only slightly.</span></span> <span data-ttu-id="f8011-226">Julie Lerman 在 2016 年 5 月的 [Dapper, Entity Framework, and Hybrid Apps](/archive/msdn-magazine/2016/may/data-points-dapper-entity-framework-and-hybrid-apps) (Dapper、Entity Framework 和混合式應用程式) MSDN 文章中提供了一些效能資料。</span><span class="sxs-lookup"><span data-stu-id="f8011-226">Julie Lerman presents some performance data in her May 2016 MSDN article [Dapper, Entity Framework, and Hybrid Apps](/archive/msdn-magazine/2016/may/data-points-dapper-entity-framework-and-hybrid-apps).</span></span> <span data-ttu-id="f8011-227">如需各種不同資料存取方法的其他效能基準測試資料，請參閱 [Dapper 網站](https://github.com/StackExchange/Dapper)。</span><span class="sxs-lookup"><span data-stu-id="f8011-227">Additional performance benchmark data for a variety of data access methods can be found on [the Dapper site](https://github.com/StackExchange/Dapper).</span></span>

<span data-ttu-id="f8011-228">若要查看 Dapper 和 EF Core 的語法差異，請參考下列用來擷取項目清單之相同方法的兩個版本：</span><span class="sxs-lookup"><span data-stu-id="f8011-228">To see how the syntax for Dapper varies from EF Core, consider these two versions of the same method for retrieving a list of items:</span></span>

```csharp
// EF Core
private readonly CatalogContext _context;
public async Task<IEnumerable<CatalogType>> GetCatalogTypes()
{
    return await _context.CatalogTypes.ToListAsync();
}

// Dapper
private readonly SqlConnection _conn;
public async Task<IEnumerable<CatalogType>> GetCatalogTypesWithDapper()
{
    return await _conn.QueryAsync<CatalogType>("SELECT * FROM CatalogType");
}
```

<span data-ttu-id="f8011-229">如果您需要使用 Dapper 建立更複雜的物件圖形，則必須自行撰寫相關的查詢 (反之，在 EF Core 中是要新增 Include)。</span><span class="sxs-lookup"><span data-stu-id="f8011-229">If you need to build more complex object graphs with Dapper, you need to write the associated queries yourself (as opposed to adding an Include as you would in EF Core).</span></span> <span data-ttu-id="f8011-230">上述作業是透過各種語法來支援，包括「多重對應」這項功能，可讓您將個別資料列對應到多個對應物件。</span><span class="sxs-lookup"><span data-stu-id="f8011-230">This is supported through a variety of syntaxes, including a feature called Multi Mapping that lets you map individual rows to multiple mapped objects.</span></span> <span data-ttu-id="f8011-231">例如，假設 Post 類別具有 User 類型的 Owner 屬性 ，下列 SQL 就會傳回所有必要的資料：</span><span class="sxs-lookup"><span data-stu-id="f8011-231">For example, given a class Post with a property Owner of type User, the following SQL would return all of the necessary data:</span></span>

```sql
select * from #Posts p
left join #Users u on u.Id = p.OwnerId
Order by p.Id
```

<span data-ttu-id="f8011-232">每個傳回的資料列都包含 User 和 Post 資料。</span><span class="sxs-lookup"><span data-stu-id="f8011-232">Each returned row includes both User and Post data.</span></span> <span data-ttu-id="f8011-233">因為 User 資料應該透過其 Owner 屬性附加至 Post 資料，所以會使用下列函式：</span><span class="sxs-lookup"><span data-stu-id="f8011-233">Since the User data should be attached to the Post data via its Owner property, the following function is used:</span></span>

```csharp
(post, user) => { post.Owner = user; return post; }
```

<span data-ttu-id="f8011-234">下列為完整的程式碼清單，其會傳回文章集合，並以相關聯的使用者資料填入 Owner 屬性：</span><span class="sxs-lookup"><span data-stu-id="f8011-234">The full code listing to return a collection of posts with their Owner property populated with the associated user data would be:</span></span>

```csharp
var sql = @"select * from #Posts p
left join #Users u on u.Id = p.OwnerId
Order by p.Id";
var data = connection.Query<Post, User, Post>(sql,
(post, user) => { post.Owner = user; return post;});
```

<span data-ttu-id="f8011-235">因為 Dapper 提供較少的封裝，所以開發人員必須進一步了解如何儲存資料、如何有效率地查詢資料，並撰寫更多程式碼來擷取資料。</span><span class="sxs-lookup"><span data-stu-id="f8011-235">Because it offers less encapsulation, Dapper requires developers know more about how their data is stored, how to query it efficiently, and write more code to fetch it.</span></span> <span data-ttu-id="f8011-236">當模型變更時，您不只要建立新的移轉 (另一個 EF Core 功能)，及/或逐一更新 DbContext 中每個位置的對應資訊，還要更新會受到影響的每一個查詢。</span><span class="sxs-lookup"><span data-stu-id="f8011-236">When the model changes, instead of simply creating a new migration (another EF Core feature), and/or updating mapping information in one place in a DbContext, every query that is impacted must be updated.</span></span> <span data-ttu-id="f8011-237">這些查詢沒有任何編譯時期的保證，因此它們可能會在執行時間中斷以回應模型或資料庫的變更，讓錯誤更難快速偵測。</span><span class="sxs-lookup"><span data-stu-id="f8011-237">These queries have no compile-time guarantees, so they may break at run time in response to changes to the model or database, making errors more difficult to detect quickly.</span></span> <span data-ttu-id="f8011-238">Dapper 折衷了上述情況，以提供極快速的效能。</span><span class="sxs-lookup"><span data-stu-id="f8011-238">In exchange for these tradeoffs, Dapper offers extremely fast performance.</span></span>

<span data-ttu-id="f8011-239">對於大部分應用程式以及幾乎所有主要的應用程式來說，EF Core 可提供還不錯的效能。</span><span class="sxs-lookup"><span data-stu-id="f8011-239">For most applications, and most parts of almost all applications, EF Core offers acceptable performance.</span></span> <span data-ttu-id="f8011-240">因此，其開發人員的生產力優勢可能遠大於它的效能負擔。</span><span class="sxs-lookup"><span data-stu-id="f8011-240">Thus, its developer productivity benefits are likely to outweigh its performance overhead.</span></span> <span data-ttu-id="f8011-241">如果查詢可受益於快取，實際的查詢可能只會執行很短的時間，這時查詢效能之間的微小差異就無傷大雅了。</span><span class="sxs-lookup"><span data-stu-id="f8011-241">For queries that can benefit from caching, the actual query may only be executed a tiny percentage of the time, making relatively small query performance differences moot.</span></span>

## <a name="sql-or-nosql"></a><span data-ttu-id="f8011-242">SQL 或 NoSQL</span><span class="sxs-lookup"><span data-stu-id="f8011-242">SQL or NoSQL</span></span>

<span data-ttu-id="f8011-243">傳統上來看，SQL Server 這類關聯式資料庫主導了永續性資料儲存的市場，但它們並不是唯一可用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f8011-243">Traditionally, relational databases like SQL Server have dominated the marketplace for persistent data storage, but they are not the only solution available.</span></span> <span data-ttu-id="f8011-244">[MongoDB](https://www.mongodb.com/what-is-mongodb) 這類 NoSQL 資料庫提供儲存物件的不同方式。</span><span class="sxs-lookup"><span data-stu-id="f8011-244">NoSQL databases like [MongoDB](https://www.mongodb.com/what-is-mongodb) offer a different approach to storing objects.</span></span> <span data-ttu-id="f8011-245">這個選項不會將物件對應至資料表和資料列，而是序列化整個物件圖形，並且將結果儲存。</span><span class="sxs-lookup"><span data-stu-id="f8011-245">Rather than mapping objects to tables and rows, another option is to serialize the entire object graph, and store the result.</span></span> <span data-ttu-id="f8011-246">初步來講，這個方法的優點是簡潔和效能。</span><span class="sxs-lookup"><span data-stu-id="f8011-246">The benefits of this approach, at least initially, are simplicity and performance.</span></span> <span data-ttu-id="f8011-247">使用索引鍵來儲存單一序列化物件會比將物件分解為許多資料表更簡單，而這些資料表具有關聯性和更新，以及自從上次從資料庫抓取物件之後可能已經變更的資料列。</span><span class="sxs-lookup"><span data-stu-id="f8011-247">It's simpler to store a single serialized object with a key than to decompose the object into many tables with relationships and update and rows that may have changed since the object was last retrieved from the database.</span></span> <span data-ttu-id="f8011-248">同樣地，相較於從關聯式資料庫完整撰寫相同物件所需的複雜聯結或多個資料庫查詢，從以索引鍵為基礎的存放區中擷取和還原序列化單一物件通常更為快速、簡單。</span><span class="sxs-lookup"><span data-stu-id="f8011-248">Likewise, fetching and deserializing a single object from a key-based store is typically much faster and easier than complex joins or multiple database queries required to fully compose the same object from a relational database.</span></span> <span data-ttu-id="f8011-249">缺少鎖定或交易或固定的架構也會讓 NoSQL 資料庫適合在多部電腦上進行調整，以支援非常大型的資料集。</span><span class="sxs-lookup"><span data-stu-id="f8011-249">The lack of locks or transactions or a fixed schema also makes NoSQL databases amenable to scaling across many machines, supporting very large datasets.</span></span>

<span data-ttu-id="f8011-250">另一方面來看，NoSQL 資料庫 (如字面通稱) 也有其缺點。</span><span class="sxs-lookup"><span data-stu-id="f8011-250">On the other hand, NoSQL databases (as they are typically called) have their drawbacks.</span></span> <span data-ttu-id="f8011-251">關聯式資料庫使用正規化功能，強制執行一致性並避免出現重複的資料。</span><span class="sxs-lookup"><span data-stu-id="f8011-251">Relational databases use normalization to enforce consistency and avoid duplication of data.</span></span> <span data-ttu-id="f8011-252">這可減少資料庫的大小總計，並確保對共用資料所做的更新可在整個資料庫中立即生效。</span><span class="sxs-lookup"><span data-stu-id="f8011-252">This reduces the total size of the database and ensures that updates to shared data are available immediately throughout the database.</span></span> <span data-ttu-id="f8011-253">在關聯式資料庫中，假設「地址」資料表參考「國家/地區」資料表中的識別碼，則當國家/地區的名稱變更時，地址記錄也會隨之更新，因此您不需要另行更新地址記錄。</span><span class="sxs-lookup"><span data-stu-id="f8011-253">In a relational database, an Address table might reference a Country table by ID, such that if the name of a country/region were changed, the address records would benefit from the update without themselves having to be updated.</span></span> <span data-ttu-id="f8011-254">不過，在 NoSQL 資料庫中，「地址」和其相關聯的「國家/地區」可能會序列化為許多預存物件的一部分。</span><span class="sxs-lookup"><span data-stu-id="f8011-254">However, in a NoSQL database, Address and its associated Country might be serialized as part of many stored objects.</span></span> <span data-ttu-id="f8011-255">更新國家/地區名稱時，也必須更新所有相關物件，而不是單一資料列。</span><span class="sxs-lookup"><span data-stu-id="f8011-255">An update to a country/region name would require all such objects to be updated, rather than a single row.</span></span> <span data-ttu-id="f8011-256">關聯式資料庫也可以強制執行規則 (例如外部索引鍵)，以確保關聯的完整性。</span><span class="sxs-lookup"><span data-stu-id="f8011-256">Relational databases can also ensure relational integrity by enforcing rules like foreign keys.</span></span> <span data-ttu-id="f8011-257">NoSQL 資料庫通常不會對其資料提供這類條件約束。</span><span class="sxs-lookup"><span data-stu-id="f8011-257">NoSQL databases typically do not offer such constraints on their data.</span></span>

<span data-ttu-id="f8011-258">NoSQL 資料庫還有一個必須處理的複雜問題是版本設定。</span><span class="sxs-lookup"><span data-stu-id="f8011-258">Another complexity NoSQL databases must deal with is versioning.</span></span> <span data-ttu-id="f8011-259">當物件的屬性變更時，您可能無法從過去已儲存的版本將它還原序列化。</span><span class="sxs-lookup"><span data-stu-id="f8011-259">When an object's properties change, it may not be able to be deserialized from past versions that were stored.</span></span> <span data-ttu-id="f8011-260">因此，所有含序列化版本 (舊版) 物件的現有物件，都必須更新以符合新的結構描述。</span><span class="sxs-lookup"><span data-stu-id="f8011-260">Thus, all existing objects that have a serialized (previous) version of the object must be updated to conform to its new schema.</span></span> <span data-ttu-id="f8011-261">而在關聯式資料庫中，當結構描述變更時，有時需要更新指令碼或對應更新，因此兩者已不只是概念上的差異。</span><span class="sxs-lookup"><span data-stu-id="f8011-261">This is not conceptually different from a relational database, where schema changes sometimes require update scripts or mapping updates.</span></span> <span data-ttu-id="f8011-262">不過，使用 NoSQL 方法時，您必須修改的項目數通常非常多，因為重複的資料比較多。</span><span class="sxs-lookup"><span data-stu-id="f8011-262">However, the number of entries that must be modified is often much greater in the NoSQL approach, because there is more duplication of data.</span></span>

<span data-ttu-id="f8011-263">您可以在 NoSQL 資料庫中儲存物件的多個版本，而固定結構描述的關聯式資料庫通常不支援這項功能。</span><span class="sxs-lookup"><span data-stu-id="f8011-263">It's possible in NoSQL databases to store multiple versions of objects, something fixed schema relational databases typically do not support.</span></span> <span data-ttu-id="f8011-264">不過，在這種情況下，應用程式的程式碼必須找出存在的舊版本物件，這增加了其額外的複雜性。</span><span class="sxs-lookup"><span data-stu-id="f8011-264">However, in this case your application code will need to account for the existence of previous versions of objects, adding additional complexity.</span></span>

<span data-ttu-id="f8011-265">NoSQL 資料庫通常不會強制執行 [ACID](https://en.wikipedia.org/wiki/ACID)，因此在效能和延展性方面比關聯式資料庫更有優勢。</span><span class="sxs-lookup"><span data-stu-id="f8011-265">NoSQL databases typically do not enforce [ACID](https://en.wikipedia.org/wiki/ACID), which means they have both performance and scalability benefits over relational databases.</span></span> <span data-ttu-id="f8011-266">它們非常適合非常大型的資料集和物件，而不適合儲存在正規化資料表結構中。</span><span class="sxs-lookup"><span data-stu-id="f8011-266">They're well suited to extremely large datasets and objects that are not well suited to storage in normalized table structures.</span></span> <span data-ttu-id="f8011-267">單一應用程式也可以同時利用關聯式和 NoSQL 資料庫，只要依據最適合的情況來選擇即可。</span><span class="sxs-lookup"><span data-stu-id="f8011-267">There is no reason why a single application cannot take advantage of both relational and NoSQL databases, using each where it is best suited.</span></span>

## <a name="azure-cosmos-db"></a><span data-ttu-id="f8011-268">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f8011-268">Azure Cosmos DB</span></span>

<span data-ttu-id="f8011-269">Azure Cosmos DB 是完全受控的 NoSQL 資料庫服務，可提供雲端架構的無架構資料儲存。</span><span class="sxs-lookup"><span data-stu-id="f8011-269">Azure Cosmos DB is a fully managed NoSQL database service that offers cloud-based schema-free data storage.</span></span> <span data-ttu-id="f8011-270">Azure Cosmos DB 是專為快速且可預測的效能、高可用性、彈性調整和全球散發所建立。</span><span class="sxs-lookup"><span data-stu-id="f8011-270">Azure Cosmos DB is built for fast and predictable performance, high availability, elastic scaling, and global distribution.</span></span> <span data-ttu-id="f8011-271">即使在 NoSQL 資料庫中，開發人員仍可以對 JSON 資料使用豐富且熟悉的 SQL 查詢功能。</span><span class="sxs-lookup"><span data-stu-id="f8011-271">Despite being a NoSQL database, developers can use rich and familiar SQL query capabilities on JSON data.</span></span> <span data-ttu-id="f8011-272">Azure Cosmos DB 中的所有資源都會儲存為 JSON 檔。</span><span class="sxs-lookup"><span data-stu-id="f8011-272">All resources in Azure Cosmos DB are stored as JSON documents.</span></span> <span data-ttu-id="f8011-273">系統會以「項目」__ 形式來管理資源；也就是說，資源是包含中繼資料和「摘要」__ 的文件，也是項目的集合。</span><span class="sxs-lookup"><span data-stu-id="f8011-273">Resources are managed as _items_, which are documents containing metadata, and _feeds_, which are collections of items.</span></span> <span data-ttu-id="f8011-274">圖8-2 顯示不同 Azure Cosmos DB 資源之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="f8011-274">Figure 8-2 shows the relationship between different Azure Cosmos DB resources.</span></span>

![Azure Cosmos DB 中的資源之間的階層式關聯性，即 NoSQL JSON 資料庫](./media/image8-2.png)

<span data-ttu-id="f8011-276">**圖 8-2**：</span><span class="sxs-lookup"><span data-stu-id="f8011-276">**Figure 8-2.**</span></span> <span data-ttu-id="f8011-277">Azure Cosmos DB 資源組織。</span><span class="sxs-lookup"><span data-stu-id="f8011-277">Azure Cosmos DB resource organization.</span></span>

<span data-ttu-id="f8011-278">Azure Cosmos DB 查詢語言是一種簡單但功能強大的介面，可用於查詢 JSON 檔。</span><span class="sxs-lookup"><span data-stu-id="f8011-278">The Azure Cosmos DB query language is a simple yet powerful interface for querying JSON documents.</span></span> <span data-ttu-id="f8011-279">此語言支援 ANSI SQL 文法的子集，並新增 JavaScript 物件、陣列、物件建構和函式叫用的深入整合。</span><span class="sxs-lookup"><span data-stu-id="f8011-279">The language supports a subset of ANSI SQL grammar and adds deep integration of JavaScript object, arrays, object construction, and function invocation.</span></span>

<span data-ttu-id="f8011-280">**參考– Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="f8011-280">**References – Azure Cosmos DB**</span></span>

- <span data-ttu-id="f8011-281">Azure Cosmos DB 簡介 <https://docs.microsoft.com/azure/cosmos-db/introduction></span><span class="sxs-lookup"><span data-stu-id="f8011-281">Azure Cosmos DB Introduction <https://docs.microsoft.com/azure/cosmos-db/introduction></span></span>

## <a name="other-persistence-options"></a><span data-ttu-id="f8011-282">其他持續性選項</span><span class="sxs-lookup"><span data-stu-id="f8011-282">Other persistence options</span></span>

<span data-ttu-id="f8011-283">除了關聯式和 NoSQL 儲存區選項，ASP.NET Core 應用程式也可以使用 Azure 儲存體，透過以雲端為基礎且可擴充的方式，來儲存各種不同的資料格式和檔案。</span><span class="sxs-lookup"><span data-stu-id="f8011-283">In addition to relational and NoSQL storage options, ASP.NET Core applications can use Azure Storage to store a variety of data formats and files in a cloud-based, scalable fashion.</span></span> <span data-ttu-id="f8011-284">Azure 儲存體可大幅進行調整，因此您可以一開始先儲存少量資料，之後再視應用程式的需要，擴充儲存至數百 GB 或 TB。</span><span class="sxs-lookup"><span data-stu-id="f8011-284">Azure Storage is massively scalable, so you can start out storing small amounts of data and scale up to storing hundreds or terabytes if your application requires it.</span></span> <span data-ttu-id="f8011-285">Azure 儲存體支援下列四種資料類型：</span><span class="sxs-lookup"><span data-stu-id="f8011-285">Azure Storage supports four kinds of data:</span></span>

- <span data-ttu-id="f8011-286">Blob 儲存體，也稱為物件儲存體，適用於非結構化的文字或二進位儲存。</span><span class="sxs-lookup"><span data-stu-id="f8011-286">Blob Storage for unstructured text or binary storage, also referred to as object storage.</span></span>

- <span data-ttu-id="f8011-287">資料表儲存體，可透過資料列索引鍵存取，適用於結構化資料集。</span><span class="sxs-lookup"><span data-stu-id="f8011-287">Table Storage for structured datasets, accessible via row keys.</span></span>

- <span data-ttu-id="f8011-288">佇列儲存體，適合用來進行以佇列為主的通訊。</span><span class="sxs-lookup"><span data-stu-id="f8011-288">Queue Storage for reliable queue-based messaging.</span></span>

- <span data-ttu-id="f8011-289">檔案儲存體，適合用來存取 Azure 虛擬機器和內部部署應用程式之間的共用檔案。</span><span class="sxs-lookup"><span data-stu-id="f8011-289">File Storage for shared file access between Azure virtual machines and on-premises applications.</span></span>

<span data-ttu-id="f8011-290">**參考資料 – Azure 儲存體**</span><span class="sxs-lookup"><span data-stu-id="f8011-290">**References – Azure Storage**</span></span>

- <span data-ttu-id="f8011-291">Azure 儲存體簡介 <https://docs.microsoft.com/azure/storage/common/storage-introduction></span><span class="sxs-lookup"><span data-stu-id="f8011-291">Azure Storage Introduction <https://docs.microsoft.com/azure/storage/common/storage-introduction></span></span>

## <a name="caching"></a><span data-ttu-id="f8011-292">Caching</span><span class="sxs-lookup"><span data-stu-id="f8011-292">Caching</span></span>

<span data-ttu-id="f8011-293">在 Web 應用程式中，每個 Web 要求都應盡量在最短時間內完成。</span><span class="sxs-lookup"><span data-stu-id="f8011-293">In web applications, each web request should be completed in the shortest time possible.</span></span> <span data-ttu-id="f8011-294">為了達成上述目的，其中一個方法是限制伺服器為完成要求必須發出的外部呼叫數目。</span><span class="sxs-lookup"><span data-stu-id="f8011-294">One way to achieve this is to limit the number of external calls the server must make to complete the request.</span></span> <span data-ttu-id="f8011-295">快取功能會將資料的複本儲存到伺服器 (或比資料來源更容易查詢的其他資料存放區)。</span><span class="sxs-lookup"><span data-stu-id="f8011-295">Caching involves storing a copy of data on the server (or another data store that is more easily queried than the source of the data).</span></span> <span data-ttu-id="f8011-296">Web 應用程式 (特別是非 SPA 的傳統 Web 應用程式) 必須使用每個要求來建置完整的使用者介面。</span><span class="sxs-lookup"><span data-stu-id="f8011-296">Web applications, and especially non-SPA traditional web applications, need to build the entire user interface with every request.</span></span> <span data-ttu-id="f8011-297">若要這麼做，通常要從某個使用者要求到下一個使用者要求不斷重複進行許多相同的資料庫查詢。</span><span class="sxs-lookup"><span data-stu-id="f8011-297">This frequently involves making many of the same database queries repeatedly from one user request to the next.</span></span> <span data-ttu-id="f8011-298">在大部分情況下，這些資料很少變更，因此實在沒有必要不斷向資料庫提出要求。</span><span class="sxs-lookup"><span data-stu-id="f8011-298">In most cases, this data changes rarely, so there is little reason to constantly request it from the database.</span></span> <span data-ttu-id="f8011-299">ASP.NET Core 支援可快取整個頁面的回應快取，以及可支援更細微快取行為的資料快取。</span><span class="sxs-lookup"><span data-stu-id="f8011-299">ASP.NET Core supports response caching, for caching entire pages, and data caching, which supports more granular caching behavior.</span></span>

<span data-ttu-id="f8011-300">當實作快取時，應特別注意關注點分離原則。</span><span class="sxs-lookup"><span data-stu-id="f8011-300">When implementing caching, it's important to keep in mind separation of concerns.</span></span> <span data-ttu-id="f8011-301">避免在資料存取邏輯或使用者介面中，實作快取邏輯。</span><span class="sxs-lookup"><span data-stu-id="f8011-301">Avoid implementing caching logic in your data access logic, or in your user interface.</span></span> <span data-ttu-id="f8011-302">相反地，請將快取封裝在其自身的類別中，並使用組態來管理它的行為。</span><span class="sxs-lookup"><span data-stu-id="f8011-302">Instead, encapsulate caching in its own classes, and use configuration to manage its behavior.</span></span> <span data-ttu-id="f8011-303">這會遵循開啟/關閉準則 (Open/Closed Principle) 和單一責任準則 (Single Responsibility Principle)，並可讓您更輕鬆管理應用程式增長時的快取使用方式。</span><span class="sxs-lookup"><span data-stu-id="f8011-303">This follows the Open/Closed and Single Responsibility principles, and will make it easier for you to manage how you use caching in your application as it grows.</span></span>

### <a name="aspnet-core-response-caching"></a><span data-ttu-id="f8011-304">ASP.NET Core 回應快取</span><span class="sxs-lookup"><span data-stu-id="f8011-304">ASP.NET Core response caching</span></span>

<span data-ttu-id="f8011-305">ASP.NET Core 支援兩個層級的快取回應。</span><span class="sxs-lookup"><span data-stu-id="f8011-305">ASP.NET Core supports two levels of response caching.</span></span> <span data-ttu-id="f8011-306">第一個層級不會快取伺服器上的任何項目，但會新增 HTTP 標頭以指示用戶端和 Proxy 伺服器來快取回應。</span><span class="sxs-lookup"><span data-stu-id="f8011-306">The first level does not cache anything on the server, but adds HTTP headers that instruct clients and proxy servers to cache responses.</span></span> <span data-ttu-id="f8011-307">上述作業的實作方式為將 ResponseCache 屬性新增至個別的控制器或動作：</span><span class="sxs-lookup"><span data-stu-id="f8011-307">This is implemented by adding the ResponseCache attribute to individual controllers or actions:</span></span>

```csharp
[ResponseCache(Duration = 60)]
public IActionResult Contact()
{
    ViewData["Message"] = "Your contact page.";
    return View();
}
```

<span data-ttu-id="f8011-308">上述範例會導致將下列標頭新增至回應，並指示用戶端快取結果高達 60 秒。</span><span class="sxs-lookup"><span data-stu-id="f8011-308">The previous example will result in the following header being added to the response, instructing clients to cache the result for up to 60 seconds.</span></span>

<span data-ttu-id="f8011-309">Cache-Control: public,max-age=60</span><span class="sxs-lookup"><span data-stu-id="f8011-309">Cache-Control: public,max-age=60</span></span>

<span data-ttu-id="f8011-310">若要將伺服器端記憶體內部快取新增至應用程式，您必須參考 Microsoft.AspNetCore.ResponseCaching NuGet 套件，然後新增回應快取中介軟體。</span><span class="sxs-lookup"><span data-stu-id="f8011-310">In order to add server-side in-memory caching to the application, you must reference the Microsoft.AspNetCore.ResponseCaching NuGet package, and then add the Response Caching middleware.</span></span> <span data-ttu-id="f8011-311">此中介軟體是在啟動的 ConfigureServices 和 Configure 中設定：</span><span class="sxs-lookup"><span data-stu-id="f8011-311">This middleware is configured in both ConfigureServices and Configure in Startup:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddResponseCaching();
}

public void Configure(IApplicationBuilder app)
{
    app.UseResponseCaching();
}
```

<span data-ttu-id="f8011-312">回應快取中介軟體會根據一組可自訂的條件來自動快取回應。</span><span class="sxs-lookup"><span data-stu-id="f8011-312">The Response Caching Middleware will automatically cache responses based on a set of conditions, which you can customize.</span></span> <span data-ttu-id="f8011-313">根據預設，只會快取透過 GET 或 HEAD 方法要求的 200 (沒問題) 回應。</span><span class="sxs-lookup"><span data-stu-id="f8011-313">By default, only 200 (OK) responses requested via GET or HEAD methods are cached.</span></span> <span data-ttu-id="f8011-314">此外，要求的回應必須具備 Cache-Control: public 標頭，而且不能包含 Authorization 或 Set-Cookie 的標頭。</span><span class="sxs-lookup"><span data-stu-id="f8011-314">In addition, requests must have a response with a Cache-Control: public header, and cannot include headers for Authorization or Set-Cookie.</span></span> <span data-ttu-id="f8011-315">請參閱[回應快取中介軟體所使用的快取條件完整清單](/aspnet/core/performance/caching/middleware#conditions-for-caching)。</span><span class="sxs-lookup"><span data-stu-id="f8011-315">See a [complete list of the caching conditions used by the response caching middleware](/aspnet/core/performance/caching/middleware#conditions-for-caching).</span></span>

### <a name="data-caching"></a><span data-ttu-id="f8011-316">資料快取</span><span class="sxs-lookup"><span data-stu-id="f8011-316">Data caching</span></span>

<span data-ttu-id="f8011-317">您可以只快取個別的資料查詢結果，或同時快取完整的 Web 回應。</span><span class="sxs-lookup"><span data-stu-id="f8011-317">Rather than (or in addition to) caching full web responses, you can cache the results of individual data queries.</span></span> <span data-ttu-id="f8011-318">若要這麼做，您可以在 Web 伺服器上使用記憶體內部快取，或使用[分散式快取](/aspnet/core/performance/caching/distributed)。</span><span class="sxs-lookup"><span data-stu-id="f8011-318">For this, you can use in memory caching on the web server, or use [a distributed cache](/aspnet/core/performance/caching/distributed).</span></span> <span data-ttu-id="f8011-319">本節將示範如何實作記憶體內部快取。</span><span class="sxs-lookup"><span data-stu-id="f8011-319">This section will demonstrate how to implement in memory caching.</span></span>

<span data-ttu-id="f8011-320">在 ConfigureServices 中，新增對記憶體 (或分散式) 快取的支援：</span><span class="sxs-lookup"><span data-stu-id="f8011-320">You add support for memory (or distributed) caching in ConfigureServices:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMemoryCache();
    services.AddMvc();
}
```

<span data-ttu-id="f8011-321">請務必一併新增 Microsoft.Extensions.Caching.Memory NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="f8011-321">Be sure to add the Microsoft.Extensions.Caching.Memory NuGet package as well.</span></span>

<span data-ttu-id="f8011-322">新增服務之後，每當您需要存取快取時，即可透過相依性插入要求 IMemoryCache。</span><span class="sxs-lookup"><span data-stu-id="f8011-322">Once you've added the service, you request IMemoryCache via dependency injection wherever you need to access the cache.</span></span> <span data-ttu-id="f8011-323">在此範例中，CachedCatalogService 會提供 ICatalogService 的替代實作來使用 Proxy (或裝飾項目) 設計模式，以控制基礎 CatalogService 實作的存取權 (或新增行為至基礎 CatalogService 實作)。</span><span class="sxs-lookup"><span data-stu-id="f8011-323">In this example, the CachedCatalogService is using the Proxy (or Decorator) design pattern, by providing an alternative implementation of ICatalogService that controls access to (or adds behavior to) the underlying CatalogService implementation.</span></span>

```csharp
public class CachedCatalogService : ICatalogService
{
    private readonly IMemoryCache _cache;
    private readonly CatalogService _catalogService;
    private static readonly string _brandsKey = "brands";
    private static readonly string _typesKey = "types";
    private static readonly TimeSpan _defaultCacheDuration = TimeSpan.FromSeconds(30);
    public CachedCatalogService(IMemoryCache cache,
    CatalogService catalogService)
    {
        _cache = cache;
        _catalogService = catalogService;
    }

    public async Task<IEnumerable<SelectListItem>> GetBrands()
    {
        return await _cache.GetOrCreateAsync(_brandsKey, async entry =>
        {
            entry.SlidingExpiration = _defaultCacheDuration;
            return await _catalogService.GetBrands();
        });
    }

    public async Task<Catalog> GetCatalogItems(int pageIndex, int itemsPage, int? brandID, int? typeId)
    {
        string cacheKey = $"items-{pageIndex}-{itemsPage}-{brandID}-{typeId}";
        return await _cache.GetOrCreateAsync(cacheKey, async entry =>
        {
            entry.SlidingExpiration = _defaultCacheDuration;
            return await _catalogService.GetCatalogItems(pageIndex, itemsPage, brandID, typeId);
        });
    }

    public async Task<IEnumerable<SelectListItem>> GetTypes()
    {
        return await _cache.GetOrCreateAsync(_typesKey, async entry =>
        {
            entry.SlidingExpiration = _defaultCacheDuration;
            return await _catalogService.GetTypes();
        });
    }
}
```

<span data-ttu-id="f8011-324">若要將應用程式設定為使用服務的快取版本，但仍然允許服務取得其建構函式中所需的 CatalogService 執行個體，您可以在 ConfigureServices 中新增下列項目：</span><span class="sxs-lookup"><span data-stu-id="f8011-324">To configure the application to use the cached version of the service, but still allow the service to get the instance of CatalogService it needs in its constructor, you would add the following in ConfigureServices:</span></span>

```csharp
services.AddMemoryCache();
services.AddScoped<ICatalogService, CachedCatalogService>();
services.AddScoped<CatalogService>();
```

<span data-ttu-id="f8011-325">完成上述作業時，系統只會每分鐘呼叫一次資料庫以擷取目錄資料，而不會在每次要求時都呼叫。</span><span class="sxs-lookup"><span data-stu-id="f8011-325">With this in place, the database calls to fetch the catalog data will only be made once per minute, rather than on every request.</span></span> <span data-ttu-id="f8011-326">視網站的流量而定，這可能會對資料庫的查詢數目產生顯著的影響，而首頁的平均頁面載入時間則取決於此服務所公開的三個查詢。</span><span class="sxs-lookup"><span data-stu-id="f8011-326">Depending on the traffic to the site, this can have a significant impact on the number of queries made to the database, and the average page load time for the home page that currently depends on all three of the queries exposed by this service.</span></span>

<span data-ttu-id="f8011-327">執行快取時所發生的問題是 _過時的資料_ ，也就是在來源變更但過期版本仍在快取中的資料。</span><span class="sxs-lookup"><span data-stu-id="f8011-327">An issue that arises when caching is implemented is _stale data_ – that is, data that has changed at the source but an out-of-date version remains in the cache.</span></span> <span data-ttu-id="f8011-328">若要緩和這個問題，一個簡單的方式是將快取持續時間縮短，因為對忙碌的應用程式來說，延長快取資料的時間長度意義不大。</span><span class="sxs-lookup"><span data-stu-id="f8011-328">A simple way to mitigate this issue is to use small cache durations, since for a busy application there is limited additional benefit to extending the length data is cached.</span></span> <span data-ttu-id="f8011-329">例如，假設某個頁面會進行單一資料庫查詢，且每秒要求 10 次。</span><span class="sxs-lookup"><span data-stu-id="f8011-329">For example, consider a page that makes a single database query, and is requested 10 times per second.</span></span> <span data-ttu-id="f8011-330">如果將這個頁面快取一分鐘，則資料庫每分鐘查詢的數目可從 600 降到 1，減少了 99.8%。</span><span class="sxs-lookup"><span data-stu-id="f8011-330">If this page is cached for one minute, it will result in the number of database queries made per minute to drop from 600 to 1, a reduction of 99.8%.</span></span> <span data-ttu-id="f8011-331">如果快取持續時間設為一小時，整體可以減少 99.997%；不過，這樣一來，過時資料的可能性和存在時間都會大幅增加。</span><span class="sxs-lookup"><span data-stu-id="f8011-331">If instead the cache duration were made one hour, the overall reduction would be 99.997%, but now the likelihood and potential age of stale data are both increased dramatically.</span></span>

<span data-ttu-id="f8011-332">另一個方法是當快取項目包含的資料有所更新時，就主動移除快取項目。</span><span class="sxs-lookup"><span data-stu-id="f8011-332">Another approach is to proactively remove cache entries when the data they contain is updated.</span></span> <span data-ttu-id="f8011-333">只要知道索引鍵，就可以移除任何個別的項目：</span><span class="sxs-lookup"><span data-stu-id="f8011-333">Any individual entry can be removed if its key is known:</span></span>

```csharp
_cache.Remove(cacheKey);
```

<span data-ttu-id="f8011-334">如果應用程式會公開功能以更新它的快取項目，您可以在執行更新的程式碼中移除對應的快取項目。</span><span class="sxs-lookup"><span data-stu-id="f8011-334">If your application exposes functionality for updating entries that it caches, you can remove the corresponding cache entries in your code that performs the updates.</span></span> <span data-ttu-id="f8011-335">有時候，可能會有許多不同的項目相依於特定的資料集。</span><span class="sxs-lookup"><span data-stu-id="f8011-335">Sometimes there may be many different entries that depend on a particular set of data.</span></span> <span data-ttu-id="f8011-336">在此情況下，您可以使用 CancellationChangeToken 來建立快取項目之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="f8011-336">In that case, it can be useful to create dependencies between cache entries, by using a CancellationChangeToken.</span></span> <span data-ttu-id="f8011-337">透過 CancellationChangeToken，您可以藉由取消權杖，一次將多個快取專案過期。</span><span class="sxs-lookup"><span data-stu-id="f8011-337">With a CancellationChangeToken, you can expire multiple cache entries at once by canceling the token.</span></span>

```csharp
// configure CancellationToken and add entry to cache
var cts = new CancellationTokenSource();
_cache.Set("cts", cts);
_cache.Set(cacheKey,
itemToCache,
new CancellationChangeToken(cts.Token));

// elsewhere, expire the cache by cancelling the token\
_cache.Get<CancellationTokenSource>("cts").Cancel();
```

<span data-ttu-id="f8011-338">快取可大幅提升從資料庫反覆要求相同值的網頁效能。</span><span class="sxs-lookup"><span data-stu-id="f8011-338">Caching can dramatically improve the performance of web pages that repeatedly request the same values from the database.</span></span> <span data-ttu-id="f8011-339">請務必測量資料存取和頁面效能，再套用快取，並僅在看到有改進的需求時才套用快取。</span><span class="sxs-lookup"><span data-stu-id="f8011-339">Be sure to measure data access and page performance before applying caching, and only apply caching where you see a need for improvement.</span></span> <span data-ttu-id="f8011-340">快取會取用 web 伺服器記憶體資源並增加應用程式的複雜度，因此請務必不要使用這項技術來更早地優化。</span><span class="sxs-lookup"><span data-stu-id="f8011-340">Caching consumes web server memory resources and increases the complexity of the application, so it's important you don't prematurely optimize using this technique.</span></span>

## <a name="getting-data-to-no-locblazor-no-locwebassembly-apps"></a><span data-ttu-id="f8011-341">將資料取得 Blazor WebAssembly 應用程式</span><span class="sxs-lookup"><span data-stu-id="f8011-341">Getting data to Blazor WebAssembly apps</span></span>

<span data-ttu-id="f8011-342">如果您要建立使用伺服器的應用程式 Blazor ，您可以使用 Entity Framework 和其他直接資料存取技術，就像在本章中討論到目前為止所討論的一樣。</span><span class="sxs-lookup"><span data-stu-id="f8011-342">If you're building apps that use Blazor Server, you can use Entity Framework and other direct data access technologies as they've been discussed thus far in this chapter.</span></span> <span data-ttu-id="f8011-343">但是，當您建立應用程式時，就 Blazor WebAssembly 像其他 SPA 架構一樣，您需要不同的資料存取策略。</span><span class="sxs-lookup"><span data-stu-id="f8011-343">However, when building Blazor WebAssembly apps, like other SPA frameworks, you will need a different strategy for data access.</span></span> <span data-ttu-id="f8011-344">這些應用程式通常會透過 web API 端點來存取資料，並與伺服器互動。</span><span class="sxs-lookup"><span data-stu-id="f8011-344">Typically, these applications access data and interact with the server through web API endpoints.</span></span>

<span data-ttu-id="f8011-345">如果要執行的資料或作業是機密的，請務必參閱上 [一章](develop-asp-net-core-mvc-apps.md) 中的安全性章節，並保護您的 api 不會遭到未經授權的存取。</span><span class="sxs-lookup"><span data-stu-id="f8011-345">If the data or operations being performed are sensitive, be sure to review the section on security in the [previous chapter](develop-asp-net-core-mvc-apps.md) and protect your APIs against unauthorized access.</span></span>

<span data-ttu-id="f8011-346">您可以在 Blazor WebAssembly 管理專案的 [eShopOnWeb 參考應用程式](https://github.com/dotnet-architecture/eShopOnWeb)中找到應用程式的範例 Blazor 。</span><span class="sxs-lookup"><span data-stu-id="f8011-346">You'll find an example of a Blazor WebAssembly app in the [eShopOnWeb reference application](https://github.com/dotnet-architecture/eShopOnWeb), in the BlazorAdmin project.</span></span> <span data-ttu-id="f8011-347">此專案裝載于 eShopOnWeb Web 專案內，可讓 Administrators 群組中的使用者管理存放區中的專案。</span><span class="sxs-lookup"><span data-stu-id="f8011-347">This project is hosted within the eShopOnWeb Web project, and allows users in the Administrators group to manage the items in the store.</span></span> <span data-ttu-id="f8011-348">您可以在圖8-3 中看到應用程式的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="f8011-348">You can see a screenshot of the application in Figure 8-3.</span></span>

![eShopOnWeb 目錄系統管理員螢幕擷取畫面](./media/image8-3.jpg)

<span data-ttu-id="f8011-350">**圖8-3。**</span><span class="sxs-lookup"><span data-stu-id="f8011-350">**Figure 8-3.**</span></span> <span data-ttu-id="f8011-351">eShopOnWeb 目錄系統管理員螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="f8011-351">eShopOnWeb Catalog Admin Screenshot.</span></span>

<span data-ttu-id="f8011-352">從應用程式中的 web Api 提取資料時 Blazor WebAssembly ，您只要使用的實例就 `HttpClient` 如同在任何 .net 應用程式中一樣。</span><span class="sxs-lookup"><span data-stu-id="f8011-352">When fetching data from web APIs within a Blazor WebAssembly app, you just use an instance of `HttpClient` as you would in any .NET application.</span></span> <span data-ttu-id="f8011-353">相關的基本步驟是建立要求，以便在必要時傳送 (，通常是針對 POST 或 PUT 要求) 、等待要求本身、確認狀態碼，以及將回應還原序列化。</span><span class="sxs-lookup"><span data-stu-id="f8011-353">The basic steps involved are to create the request to send (if required, usually for POST or PUT requests), await the request itself, verify the status code, and deserialize the response.</span></span> <span data-ttu-id="f8011-354">如果您要對一組指定的 Api 提出許多要求，最好是封裝您的 Api 並 `HttpClient` 集中設定基底位址。</span><span class="sxs-lookup"><span data-stu-id="f8011-354">If you're going to make many requests to a given set of APIs, it's a good idea to encapsulate your APIs and configure the `HttpClient` base address centrally.</span></span> <span data-ttu-id="f8011-355">如此一來，如果您需要在環境之間調整任何這些設定，您可以只在一個位置進行變更。</span><span class="sxs-lookup"><span data-stu-id="f8011-355">This way, if you need to adjust any of these settings between environments, you can make the changes in just one place.</span></span> <span data-ttu-id="f8011-356">您應該在中新增此服務的支援 `Program.Main` ：</span><span class="sxs-lookup"><span data-stu-id="f8011-356">You should add support for this service in your `Program.Main`:</span></span>

```csharp
builder.Services.AddScoped(sp =>
    new HttpClient
    {
        BaseAddress = new Uri(builder.HostEnvironment.BaseAddress)
    });
```

<span data-ttu-id="f8011-357">如果您需要安全地存取服務，您應該存取安全權杖，並設定， `HttpClient` 以便在每個要求時將此權杖作為驗證標頭傳遞：</span><span class="sxs-lookup"><span data-stu-id="f8011-357">If you need to access services securely, you should access a secure token and configure the `HttpClient` to pass this token as an Authentication header with every request:</span></span>

```csharp
_httpClient.DefaultRequestHeaders.Authorization =
    new AuthenticationHeaderValue("Bearer", token);
```

<span data-ttu-id="f8011-358">這可以從任何已插入它的元件來完成 `HttpClient` ，但前提是未 `HttpClient` 新增至存留期為應用程式的服務 `Transient` 。</span><span class="sxs-lookup"><span data-stu-id="f8011-358">This can be done from any component that has the `HttpClient` injected into it, provided that `HttpClient` wasn't added to the application's services with a `Transient` lifetime.</span></span> <span data-ttu-id="f8011-359">應用程式中的每個參考都會 `HttpClient` 參考相同的實例，因此在一個元件中對它進行的變更會流經整個應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8011-359">Every reference to `HttpClient` in the application references the same instance, so changes to it in one component flow through the entire application.</span></span> <span data-ttu-id="f8011-360">執行這項驗證檢查的好地方 (接著指定權杖) 在共用元件中，例如網站的主要導覽。</span><span class="sxs-lookup"><span data-stu-id="f8011-360">A good place to perform this authentication check (followed by specifying the token) is in a shared component like the main navigation for the site.</span></span> <span data-ttu-id="f8011-361">若要深入瞭解這種方法，請參閱 `BlazorAdmin` [eShopOnWeb 參考應用程式](https://github.com/dotnet-architecture/eShopOnWeb)的專案。</span><span class="sxs-lookup"><span data-stu-id="f8011-361">Learn more about this approach in the `BlazorAdmin` project in the [eShopOnWeb reference application](https://github.com/dotnet-architecture/eShopOnWeb).</span></span>

<span data-ttu-id="f8011-362">Blazor WebAssembly 超越傳統 JavaScript spa 的其中一個優點是，您不需要保留資料傳輸物件的複本 (dto) 同步處理。</span><span class="sxs-lookup"><span data-stu-id="f8011-362">One benefit of Blazor WebAssembly over traditional JavaScript SPAs is that you don't need to keep to copies of your data transfer objects(DTOs) synchronized.</span></span> <span data-ttu-id="f8011-363">您的 Blazor WebAssembly 專案和您的 web API 專案都可以共用相同的 dto 在共同的共用專案中。</span><span class="sxs-lookup"><span data-stu-id="f8011-363">Your Blazor WebAssembly project and your web API project can both share the same DTOs in a common shared project.</span></span> <span data-ttu-id="f8011-364">這消除了開發 Spa 所牽涉到的一些取捨。</span><span class="sxs-lookup"><span data-stu-id="f8011-364">This eliminates some of the friction involved in developing SPAs.</span></span>

<span data-ttu-id="f8011-365">若要快速從 API 端點取得資料，您可以使用內建的 helper 方法 `GetFromJsonAsync` 。</span><span class="sxs-lookup"><span data-stu-id="f8011-365">To quickly get data from an API endpoint, you can use the built-in helper method, `GetFromJsonAsync`.</span></span> <span data-ttu-id="f8011-366">POST、PUT 等有類似的方法。以下顯示如何使用 `HttpClient` 在應用程式中設定的 API 端點來取得 CatalogItem Blazor WebAssembly ：</span><span class="sxs-lookup"><span data-stu-id="f8011-366">There are similar methods for POST, PUT, etc. The following shows how to get a CatalogItem from an API endpoint using a configured `HttpClient` in a Blazor WebAssembly app:</span></span>

```csharp
var item = await _httpClient.GetFromJsonAsync<CatalogItem>($"catalog-items/{id}");
```

<span data-ttu-id="f8011-367">當您擁有所需的資料之後，您通常會在本機追蹤變更。</span><span class="sxs-lookup"><span data-stu-id="f8011-367">Once you have the data you need, you'll typically track changes locally.</span></span> <span data-ttu-id="f8011-368">當您想要對後端資料存放區進行更新時，您將會針對此目的呼叫其他 web Api。</span><span class="sxs-lookup"><span data-stu-id="f8011-368">When you want to make updates to the backend data store, you'll call additional web APIs for this purpose.</span></span>

<span data-ttu-id="f8011-369">**參考 Blazor 資料-資料**</span><span class="sxs-lookup"><span data-stu-id="f8011-369">**References – Blazor Data**</span></span>

- <span data-ttu-id="f8011-370">從 ASP.NET Core 呼叫 web API Blazor</span><span class="sxs-lookup"><span data-stu-id="f8011-370">Call a web API from ASP.NET Core Blazor</span></span>
  <https://docs.microsoft.com/aspnet/core/blazor/call-web-api>

>[!div class="step-by-step"]
><span data-ttu-id="f8011-371">[上一個](develop-asp-net-core-mvc-apps.md) 
>[下一步](test-asp-net-core-mvc-apps.md)</span><span class="sxs-lookup"><span data-stu-id="f8011-371">[Previous](develop-asp-net-core-mvc-apps.md)
[Next](test-asp-net-core-mvc-apps.md)</span></span>
