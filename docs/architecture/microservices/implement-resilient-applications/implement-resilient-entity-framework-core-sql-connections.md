---
title: 實作具復原功能的 Entity Framework Core SQL 連接
description: 了解如何實作具復原功能的 Entity Framework Core SQL 連線。 在雲端中使用 Azure SQL Database 時，此技術特別重要。
ms.date: 10/16/2018
ms.openlocfilehash: cae3550ce301750949b042957d5d10f0167e614c
ms.sourcegitcommit: 88fbb019b84c2d044d11fb4f6004aec07f2b25b1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2021
ms.locfileid: "97899557"
---
# <a name="implement-resilient-entity-framework-core-sql-connections"></a><span data-ttu-id="dc5d4-104">實作具復原功能的 Entity Framework Core SQL 連接</span><span class="sxs-lookup"><span data-stu-id="dc5d4-104">Implement resilient Entity Framework Core SQL connections</span></span>

<span data-ttu-id="dc5d4-105">針對 Azure SQL DB，Entity Framework (EF) Core 已提供內部資料庫連線恢復功能和重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-105">For Azure SQL DB, Entity Framework (EF) Core already provides internal database connection resiliency and retry logic.</span></span> <span data-ttu-id="dc5d4-106">如果您想要使用[具復原功能的 EF Core 連線](/ef/core/miscellaneous/connection-resiliency)，則必須為每個 <xref:Microsoft.EntityFrameworkCore.DbContext> 連線啟用 Entity Framework 執行策略。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-106">But you need to enable the Entity Framework execution strategy for each <xref:Microsoft.EntityFrameworkCore.DbContext> connection if you want to have [resilient EF Core connections](/ef/core/miscellaneous/connection-resiliency).</span></span>

<span data-ttu-id="dc5d4-107">例如，EF Core 連接層級的下列程式碼可在連接失敗時重試具有恢復功能的 SQL 連接。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-107">For instance, the following code at the EF Core connection level enables resilient SQL connections that are retried if the connection fails.</span></span>

```csharp
// Startup.cs from any ASP.NET Core Web API
public class Startup
{
    // Other code ...
    public IServiceProvider ConfigureServices(IServiceCollection services)
    {
        // ...
        services.AddDbContext<CatalogContext>(options =>
        {
            options.UseSqlServer(Configuration["ConnectionString"],
            sqlServerOptionsAction: sqlOptions =>
            {
                sqlOptions.EnableRetryOnFailure(
                maxRetryCount: 10,
                maxRetryDelay: TimeSpan.FromSeconds(30),
                errorNumbersToAdd: null);
            });
        });
    }
//...
}
```

## <a name="execution-strategies-and-explicit-transactions-using-begintransaction-and-multiple-dbcontexts"></a><span data-ttu-id="dc5d4-108">使用 BeginTransaction 和多個 DbContext 的執行策略和明確異動</span><span class="sxs-lookup"><span data-stu-id="dc5d4-108">Execution strategies and explicit transactions using BeginTransaction and multiple DbContexts</span></span>

<span data-ttu-id="dc5d4-109">在 EF Core 連接中啟用重試時，您使用 EF Core 執行的每項作業都會變成其本身可重試的作業。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-109">When retries are enabled in EF Core connections, each operation you perform using EF Core becomes its own retryable operation.</span></span> <span data-ttu-id="dc5d4-110">如果發生暫時性失敗，`SaveChanges` 的每個查詢和每個呼叫都會當做一個單位來重試。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-110">Each query and each call to `SaveChanges` will be retried as a unit if a transient failure occurs.</span></span>

<span data-ttu-id="dc5d4-111">不過，如果您的程式碼使用 `BeginTransaction` 起始異動，您將定義需視為一個單位的專屬作業群組。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-111">However, if your code initiates a transaction using `BeginTransaction`, you're defining your own group of operations that need to be treated as a unit.</span></span> <span data-ttu-id="dc5d4-112">如果發生失敗，必須復原異動內的所有項目。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-112">Everything inside the transaction has to be rolled back if a failure occurs.</span></span>

<span data-ttu-id="dc5d4-113">如果您在使用 EF 執行策略 (重試原則) 時嘗試執行該交易，並呼叫來自多個 DbContext 的 `SaveChanges`，則會看到如下所示的例外狀況：</span><span class="sxs-lookup"><span data-stu-id="dc5d4-113">If you try to execute that transaction when using an EF execution strategy (retry policy) and you call `SaveChanges` from multiple DbContexts, you'll get an exception like this one:</span></span>

> <span data-ttu-id="dc5d4-114">System.InvalidOperationException：已設定的執行策略 'SqlServerRetryingExecutionStrategy' 不支援使用者起始的異動。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-114">System.InvalidOperationException: The configured execution strategy 'SqlServerRetryingExecutionStrategy' does not support user initiated transactions.</span></span> <span data-ttu-id="dc5d4-115">使用 'DbContext.Database.CreateExecutionStrategy()' 所傳回的執行策略，將異動中的所有作業當做一個可重試的單位來執行。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-115">Use the execution strategy returned by 'DbContext.Database.CreateExecutionStrategy()' to execute all the operations in the transaction as a retriable unit.</span></span>

<span data-ttu-id="dc5d4-116">解決方法是使用代表必須執行之所有項目的委派，來手動叫用 EF 執行策略。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-116">The solution is to manually invoke the EF execution strategy with a delegate representing everything that needs to be executed.</span></span> <span data-ttu-id="dc5d4-117">如果發生暫時性失敗，執行策略會再次叫用委派。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-117">If a transient failure occurs, the execution strategy will invoke the delegate again.</span></span> <span data-ttu-id="dc5d4-118">例如，下列程式碼示範在更新產品並接著儲存 ProductPriceChangedIntegrationEvent 物件時 (此時必須使用不同的 DbContext)，如何在具有兩組多個 DbContext (\_catalogContext 和 IntegrationEventLogContext) 的 eShopOnContainers 中實作。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-118">For example, the following code show how it's implemented in eShopOnContainers with two multiple DbContexts (\_catalogContext and the IntegrationEventLogContext) when updating a product and then saving the ProductPriceChangedIntegrationEvent object, which needs to use a different DbContext.</span></span>

```csharp
public async Task<IActionResult> UpdateProduct(
    [FromBody]CatalogItem productToUpdate)
{
    // Other code ...

    var oldPrice = catalogItem.Price;
    var raiseProductPriceChangedEvent = oldPrice != productToUpdate.Price;

    // Update current product
    catalogItem = productToUpdate;

    // Save product's data and publish integration event through the Event Bus
    // if price has changed
    if (raiseProductPriceChangedEvent)
    {
        //Create Integration Event to be published through the Event Bus
        var priceChangedEvent = new ProductPriceChangedIntegrationEvent(
          catalogItem.Id, productToUpdate.Price, oldPrice);

       // Achieving atomicity between original Catalog database operation and the
       // IntegrationEventLog thanks to a local transaction
       await _catalogIntegrationEventService.SaveEventAndCatalogContextChangesAsync(
           priceChangedEvent);

       // Publish through the Event Bus and mark the saved event as published
       await _catalogIntegrationEventService.PublishThroughEventBusAsync(
           priceChangedEvent);
    }
    // Just save the updated product because the Product's Price hasn't changed.
    else
    {
        await _catalogContext.SaveChangesAsync();
    }
}
```

<span data-ttu-id="dc5d4-119">第一個 <xref:Microsoft.EntityFrameworkCore.DbContext> 為 `_catalogContext`，第二個 `DbContext` 則是在 `_catalogIntegrationEventService` 物件內。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-119">The first <xref:Microsoft.EntityFrameworkCore.DbContext> is `_catalogContext` and the second `DbContext` is within the `_catalogIntegrationEventService` object.</span></span> <span data-ttu-id="dc5d4-120">系統會使用 EF 執行策略跨所有 `DbContext` 物件執行認可動作。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-120">The Commit action is performed across all `DbContext` objects using an EF execution strategy.</span></span>

<span data-ttu-id="dc5d4-121">為達成此多個 `DbContext` 認可，`SaveEventAndCatalogContextChangesAsync` 會使用 `ResilientTransaction` 類別，如以下程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="dc5d4-121">To achieve this multiple `DbContext` commit, the `SaveEventAndCatalogContextChangesAsync` uses a `ResilientTransaction` class, as shown in the following code:</span></span>

```csharp
public class CatalogIntegrationEventService : ICatalogIntegrationEventService
{
    //…
    public async Task SaveEventAndCatalogContextChangesAsync(
        IntegrationEvent evt)
    {
        // Use of an EF Core resiliency strategy when using multiple DbContexts
        // within an explicit BeginTransaction():
        // https://docs.microsoft.com/ef/core/miscellaneous/connection-resiliency
        await ResilientTransaction.New(_catalogContext).ExecuteAsync(async () =>
        {
            // Achieving atomicity between original catalog database
            // operation and the IntegrationEventLog thanks to a local transaction
            await _catalogContext.SaveChangesAsync();
            await _eventLogService.SaveEventAsync(evt,
                _catalogContext.Database.CurrentTransaction.GetDbTransaction());
        });
    }
}
```

<span data-ttu-id="dc5d4-122">`ResilientTransaction.ExecuteAsync` 方法基本上會從傳遞的 `DbContext` (`_catalogContext`) 開始交易，然後使 `EventLogService` 使用該交易以儲存 `IntegrationEventLogContext` 的變更，然後認可整個交易。</span><span class="sxs-lookup"><span data-stu-id="dc5d4-122">The `ResilientTransaction.ExecuteAsync` method basically begins a transaction from the passed `DbContext` (`_catalogContext`) and then makes the `EventLogService` use that transaction to save changes from the `IntegrationEventLogContext` and then commits the whole transaction.</span></span>

```csharp
public class ResilientTransaction
{
    private DbContext _context;
    private ResilientTransaction(DbContext context) =>
        _context = context ?? throw new ArgumentNullException(nameof(context));

    public static ResilientTransaction New (DbContext context) =>
        new ResilientTransaction(context);

    public async Task ExecuteAsync(Func<Task> action)
    {
        // Use of an EF Core resiliency strategy when using multiple DbContexts
        // within an explicit BeginTransaction():
        // https://docs.microsoft.com/ef/core/miscellaneous/connection-resiliency
        var strategy = _context.Database.CreateExecutionStrategy();
        await strategy.ExecuteAsync(async () =>
        {
            await using var transaction = await _context.Database.BeginTransactionAsync();
            await action();
            await transaction.CommitAsync();
        });
    }
}
```

## <a name="additional-resources"></a><span data-ttu-id="dc5d4-123">其他資源</span><span class="sxs-lookup"><span data-stu-id="dc5d4-123">Additional resources</span></span>

- <span data-ttu-id="dc5d4-124">**在 ASP.NET MVC 應用程式中使用 EF 的連接恢復功能和命令攔截** </span><span class="sxs-lookup"><span data-stu-id="dc5d4-124">**Connection Resiliency and Command Interception with EF in an ASP.NET MVC Application** </span></span>\
  [https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)

- <span data-ttu-id="dc5d4-125">**Cesar de la Torre。使用彈性的 Entity Framework Core SQL 連接和交易** </span><span class="sxs-lookup"><span data-stu-id="dc5d4-125">**Cesar de la Torre. Using Resilient Entity Framework Core SQL Connections and Transactions** </span></span>\
  <https://devblogs.microsoft.com/cesardelatorre/using-resilient-entity-framework-core-sql-connections-and-transactions-retries-with-exponential-backoff/>

>[!div class="step-by-step"]
><span data-ttu-id="dc5d4-126">[上一個](implement-retries-exponential-backoff.md) 
>[下一步](use-httpclientfactory-to-implement-resilient-http-requests.md)</span><span class="sxs-lookup"><span data-stu-id="dc5d4-126">[Previous](implement-retries-exponential-backoff.md)
[Next](use-httpclientfactory-to-implement-resilient-http-requests.md)</span></span>
