---
title: 使用 Web API 實作微服務應用程式層
description: 瞭解相依性插入和中繼程式模式，以及其在 Web API 應用層中的實作為詳細資料。
ms.date: 01/13/2021
ms.openlocfilehash: bf37b0bfc7d9438752673d1c617657822b2a48ad
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188968"
---
# <a name="implement-the-microservice-application-layer-using-the-web-api"></a><span data-ttu-id="70c9e-103">使用 Web API 實作微服務應用程式層</span><span class="sxs-lookup"><span data-stu-id="70c9e-103">Implement the microservice application layer using the Web API</span></span>

## <a name="use-dependency-injection-to-inject-infrastructure-objects-into-your-application-layer"></a><span data-ttu-id="70c9e-104">使用相依性插入將基礎結構物件插入至應用程式層</span><span class="sxs-lookup"><span data-stu-id="70c9e-104">Use Dependency Injection to inject infrastructure objects into your application layer</span></span>

<span data-ttu-id="70c9e-105">如前所述，應用程式層可以實作為要建置成品 (組件) 的一部分，例如在 Web API 專案或 MVC Web 應用程式專案內。</span><span class="sxs-lookup"><span data-stu-id="70c9e-105">As mentioned previously, the application layer can be implemented as part of the artifact (assembly) you are building, such as within a Web API project or an MVC web app project.</span></span> <span data-ttu-id="70c9e-106">如果是使用 ASP.NET Core 所建置的微服務，則應用程式層通常會是 Web API 程式庫。</span><span class="sxs-lookup"><span data-stu-id="70c9e-106">In the case of a microservice built with ASP.NET Core, the application layer will usually be your Web API library.</span></span> <span data-ttu-id="70c9e-107">如果您想要區隔來自 ASP.NET Core 的內容 (其基礎結構和您的控制站) 與自訂應用程式層程式碼，則也可以將應用程式層放在個別的類別庫中，但這是選擇性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-107">If you want to separate what is coming from ASP.NET Core (its infrastructure plus your controllers) from your custom application layer code, you could also place your application layer in a separate class library, but that is optional.</span></span>

<span data-ttu-id="70c9e-108">例如，訂購微服務的應用程式層程式碼可直接實作為 **Ordering.API** 專案 (ASP.NET Core Web API 專案) 的一部分，如圖 7-23 所示。</span><span class="sxs-lookup"><span data-stu-id="70c9e-108">For instance, the application layer code of the ordering microservice is directly implemented as part of the **Ordering.API** project (an ASP.NET Core Web API project), as shown in Figure 7-23.</span></span>

:::image type="complex" source="./media/microservice-application-layer-implementation-web-api/ordering-api-microservice.png" alt-text="方案總管中 [排序] 微服務的螢幕擷取畫面。":::
<span data-ttu-id="70c9e-110">微服務的 [排序 API] 方案總管視圖，顯示應用程式資料夾下的子資料夾：行為、命令、DomainEventHandlers、IntegrationEvents、模型、查詢和驗證。</span><span class="sxs-lookup"><span data-stu-id="70c9e-110">The Solution Explorer view of the Ordering.API microservice, showing the subfolders under the Application folder: Behaviors, Commands, DomainEventHandlers, IntegrationEvents, Models, Queries, and Validations.</span></span>
:::image-end:::

<span data-ttu-id="70c9e-111">**圖 7-23**。</span><span class="sxs-lookup"><span data-stu-id="70c9e-111">**Figure 7-23**.</span></span> <span data-ttu-id="70c9e-112">Ordering.API ASP.NET Core Web API 專案中的應用程式層</span><span class="sxs-lookup"><span data-stu-id="70c9e-112">The application layer in the Ordering.API ASP.NET Core Web API project</span></span>

<span data-ttu-id="70c9e-113">ASP.NET Core 包含簡單[內建 IoC 容器](/aspnet/core/fundamentals/dependency-injection) (由 IServiceProvider 介面代表)，它預設會支援建構函式插入，ASP.NET 則是透過 DI 提供特定服務。</span><span class="sxs-lookup"><span data-stu-id="70c9e-113">ASP.NET Core includes a simple [built-in IoC container](/aspnet/core/fundamentals/dependency-injection) (represented by the IServiceProvider interface) that supports constructor injection by default, and ASP.NET makes certain services available through DI.</span></span> <span data-ttu-id="70c9e-114">ASP.NET Core 會將「服務」詞彙用於透過 DI 插入的任何已註冊類型。</span><span class="sxs-lookup"><span data-stu-id="70c9e-114">ASP.NET Core uses the term *service* for any of the types you register that will be injected through DI.</span></span> <span data-ttu-id="70c9e-115">您可以在應用程式 Startup 類別的 ConfigureServices 方法中設定內建容器服務。</span><span class="sxs-lookup"><span data-stu-id="70c9e-115">You configure the built-in container's services in the ConfigureServices method in your application's Startup class.</span></span> <span data-ttu-id="70c9e-116">相依性實作所在之服務為類型所需且以 IoC 容器註冊的服務。</span><span class="sxs-lookup"><span data-stu-id="70c9e-116">Your dependencies are implemented in the services that a type needs and that you register in the IoC container.</span></span>

<span data-ttu-id="70c9e-117">一般而言，您會想要插入可實作基礎結構物件的相依性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-117">Typically, you want to inject dependencies that implement infrastructure objects.</span></span> <span data-ttu-id="70c9e-118">要插入的一般相依性是存放庫。</span><span class="sxs-lookup"><span data-stu-id="70c9e-118">A typical dependency to inject is a repository.</span></span> <span data-ttu-id="70c9e-119">但是，您可以插入可能會有的任何其他基礎結構相依性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-119">But you could inject any other infrastructure dependency that you may have.</span></span> <span data-ttu-id="70c9e-120">為求更簡單的實作，您可以直接插入工作單元模式物件 (EF DbContext 物件)，因為 DBContext 也是您基礎結構持續性物件的實作。</span><span class="sxs-lookup"><span data-stu-id="70c9e-120">For simpler implementations, you could directly inject your Unit of Work pattern object (the EF DbContext object), because the DBContext is also the implementation of your infrastructure persistence objects.</span></span>

<span data-ttu-id="70c9e-121">在下列範例中，您可以看到 .NET 如何透過此函式來插入所需的存放庫物件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-121">In the following example, you can see how .NET is injecting the required repository objects through the constructor.</span></span> <span data-ttu-id="70c9e-122">類別是命令處理常式，將在下一節中討論。</span><span class="sxs-lookup"><span data-stu-id="70c9e-122">The class is a command handler, which will get covered in the next section.</span></span>

```csharp
public class CreateOrderCommandHandler
        : IRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;
    private readonly IOrderingIntegrationEventService _orderingIntegrationEventService;
    private readonly ILogger<CreateOrderCommandHandler> _logger;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
        IOrderingIntegrationEventService orderingIntegrationEventService,
        IOrderRepository orderRepository,
        IIdentityService identityService,
        ILogger<CreateOrderCommandHandler> logger)
    {
        _orderRepository = orderRepository ?? throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ?? throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ?? throw new ArgumentNullException(nameof(mediator));
        _orderingIntegrationEventService = orderingIntegrationEventService ?? throw new ArgumentNullException(nameof(orderingIntegrationEventService));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
    }

    public async Task<bool> Handle(CreateOrderCommand message, CancellationToken cancellationToken)
    {
        // Add Integration event to clean the basket
        var orderStartedIntegrationEvent = new OrderStartedIntegrationEvent(message.UserId);
        await _orderingIntegrationEventService.AddAndSaveEventAsync(orderStartedIntegrationEvent);

        // Add/Update the Buyer AggregateRoot
        // DDD patterns comment: Add child entities and value-objects through the Order Aggregate-Root
        // methods and constructor so validations, invariants and business logic
        // make sure that consistency is preserved across the whole aggregate
        var address = new Address(message.Street, message.City, message.State, message.Country, message.ZipCode);
        var order = new Order(message.UserId, message.UserName, address, message.CardTypeId, message.CardNumber, message.CardSecurityNumber, message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice, item.Discount, item.PictureUrl, item.Units);
        }

        _logger.LogInformation("----- Creating Order - Order: {@Order}", order);

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync(cancellationToken);
    }
}

```

<span data-ttu-id="70c9e-123">此類別會使用已插入的存放庫來執行交易，並持續保存狀態變更。</span><span class="sxs-lookup"><span data-stu-id="70c9e-123">The class uses the injected repositories to execute the transaction and persist the state changes.</span></span> <span data-ttu-id="70c9e-124">不論該類別是命令處理常式、ASP.NET Core Web API 控制器方法還是 [DDD 應用程式服務](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-124">It does not matter whether that class is a command handler, an ASP.NET Core Web API controller method, or a [DDD Application Service](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/).</span></span> <span data-ttu-id="70c9e-125">它最終會是使用存放庫、領域實體和其他應用程式協調的簡單類別，其形式與命令處理常式類似。</span><span class="sxs-lookup"><span data-stu-id="70c9e-125">It is ultimately a simple class that uses repositories, domain entities, and other application coordination in a fashion similar to a command handler.</span></span> <span data-ttu-id="70c9e-126">所有提及類別的相依性插入運作方式都相同，如根據建構函式使用 DI 的範例所示。</span><span class="sxs-lookup"><span data-stu-id="70c9e-126">Dependency Injection works the same way for all the mentioned classes, as in the example using DI based on the constructor.</span></span>

### <a name="register-the-dependency-implementation-types-and-interfaces-or-abstractions"></a><span data-ttu-id="70c9e-127">註冊相依性實作類型和介面或抽象物件</span><span class="sxs-lookup"><span data-stu-id="70c9e-127">Register the dependency implementation types and interfaces or abstractions</span></span>

<span data-ttu-id="70c9e-128">您需要先知道在哪裡註冊介面和類別，以產生透過 DI 插入至 應用程式類別的物件，才能使用透過建構函式所插入的物件 </span><span class="sxs-lookup"><span data-stu-id="70c9e-128">Before you use the objects injected through constructors, you need to know where to register the interfaces and classes that produce the objects injected into your application classes through DI.</span></span> <span data-ttu-id="70c9e-129">(例如根據建構函式的 DI，如前所述)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-129">(Like DI based on the constructor, as shown previously.)</span></span>

#### <a name="use-the-built-in-ioc-container-provided-by-aspnet-core"></a><span data-ttu-id="70c9e-130">使用 ASP.NET Core 所提供的內建 IoC 容器</span><span class="sxs-lookup"><span data-stu-id="70c9e-130">Use the built-in IoC container provided by ASP.NET Core</span></span>

<span data-ttu-id="70c9e-131">當您使用 ASP.NET Core 所提供的內建 IoC 容器時，會註冊您想要在 Startup.cs 檔案的 ConfigureServices 方法中插入的類型，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="70c9e-131">When you use the built-in IoC container provided by ASP.NET Core, you register the types you want to inject in the ConfigureServices method in the Startup.cs file, as in the following code:</span></span>

```csharp
// Registration of types into ASP.NET Core built-in container
public void ConfigureServices(IServiceCollection services)
{
    // Register out-of-the-box framework services.
    services.AddDbContext<CatalogContext>(c =>
        c.UseSqlServer(Configuration["ConnectionString"]),
        ServiceLifetime.Scoped);

    services.AddMvc();
    // Register custom application dependencies.
    services.AddScoped<IMyCustomRepository, MyCustomSQLRepository>();
}
```

<span data-ttu-id="70c9e-132">在 IoC 容器中註冊類型時的最常見模式是註冊一組類型：介面和其相關實作類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-132">The most common pattern when registering types in an IoC container is to register a pair of types—an interface and its related implementation class.</span></span> <span data-ttu-id="70c9e-133">然後，當您透過任何建構函式從 IoC 容器要求物件時，會要求特定類型之介面的物件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-133">Then when you request an object from the IoC container through any constructor, you request an object of a certain type of interface.</span></span> <span data-ttu-id="70c9e-134">例如，在上述範例中，最後一行指出有任何建構函式與 IMyCustomRepository (介面或抽象) 相依時，IoC 容器將會插入 MyCustomSQLServerRepository 實作類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="70c9e-134">For instance, in the previous example, the last line states that when any of your constructors have a dependency on IMyCustomRepository (interface or abstraction), the IoC container will inject an instance of the MyCustomSQLServerRepository implementation class.</span></span>

#### <a name="use-the-scrutor-library-for-automatic-types-registration"></a><span data-ttu-id="70c9e-135">使用 Scrutor 程式庫進行自動類型註冊</span><span class="sxs-lookup"><span data-stu-id="70c9e-135">Use the Scrutor library for automatic types registration</span></span>

<span data-ttu-id="70c9e-136">在 .NET 中使用 DI 時，您可能會想要能夠掃描元件，並依慣例自動註冊其類型。</span><span class="sxs-lookup"><span data-stu-id="70c9e-136">When using DI in .NET, you might want to be able to scan an assembly and automatically register its types by convention.</span></span> <span data-ttu-id="70c9e-137">ASP.NET Core 目前未提供此功能。</span><span class="sxs-lookup"><span data-stu-id="70c9e-137">This feature is not currently available in ASP.NET Core.</span></span> <span data-ttu-id="70c9e-138">不過，您可以使用 [Scrutor](https://github.com/khellang/Scrutor) 程式庫來進行這項作業。</span><span class="sxs-lookup"><span data-stu-id="70c9e-138">However, you can use the [Scrutor](https://github.com/khellang/Scrutor) library for that.</span></span> <span data-ttu-id="70c9e-139">當您有數個需要在 IoC 容器中註冊的類型時，這種方法十分方便。</span><span class="sxs-lookup"><span data-stu-id="70c9e-139">This approach is convenient when you have dozens of types that need to be registered in your IoC container.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="70c9e-140">其他資源</span><span class="sxs-lookup"><span data-stu-id="70c9e-140">Additional resources</span></span>

- <span data-ttu-id="70c9e-141">**Matthew 王。使用 Scrutor 註冊服務** </span><span class="sxs-lookup"><span data-stu-id="70c9e-141">**Matthew King. Registering services with Scrutor** </span></span>\
  <https://www.mking.net/blog/registering-services-with-scrutor>

- <span data-ttu-id="70c9e-142">**Kristian Hellang。Scrutor.**</span><span class="sxs-lookup"><span data-stu-id="70c9e-142">**Kristian Hellang. Scrutor.**</span></span> <span data-ttu-id="70c9e-143">GitHub 存放庫。</span><span class="sxs-lookup"><span data-stu-id="70c9e-143">GitHub repo.</span></span> \
  <https://github.com/khellang/Scrutor>

#### <a name="use-autofac-as-an-ioc-container"></a><span data-ttu-id="70c9e-144">使用 Autofac 作為 IoC 容器</span><span class="sxs-lookup"><span data-stu-id="70c9e-144">Use Autofac as an IoC container</span></span>

<span data-ttu-id="70c9e-145">您也可以使用其他 IoC 容器，並將它們插入至 ASP.NET Core 管道，就像 eShopOnContainers 中的訂購微服務一樣，而訂購微服務使用 [Autofac](https://autofac.org/)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-145">You can also use additional IoC containers and plug them into the ASP.NET Core pipeline, as in the ordering microservice in eShopOnContainers, which uses [Autofac](https://autofac.org/).</span></span> <span data-ttu-id="70c9e-146">使用 Autofac 時，通常會透過模組來註冊類型，以讓您根據類型位置來分割多個檔案之間的註冊類型，就像您將應用程式類型分散到多個類別程式庫一樣。</span><span class="sxs-lookup"><span data-stu-id="70c9e-146">When using Autofac you typically register the types via modules, which allow you to split the registration types between multiple files depending on where your types are, just as you could have the application types distributed across multiple class libraries.</span></span>

<span data-ttu-id="70c9e-147">例如，下列 [Autofac 應用程式模組](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/ApplicationModule.cs)適用於具有您想要插入之類型的 [Ordering.API Web API](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Services/Ordering/Ordering.API) 專案。</span><span class="sxs-lookup"><span data-stu-id="70c9e-147">For example, the following is the [Autofac application module](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/ApplicationModule.cs) for the [Ordering.API Web API](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/Services/Ordering/Ordering.API) project with the types you will want to inject.</span></span>

```csharp
public class ApplicationModule : Autofac.Module
{
    public string QueriesConnectionString { get; }
    public ApplicationModule(string qconstr)
    {
        QueriesConnectionString = qconstr;
    }

    protected override void Load(ContainerBuilder builder)
    {
        builder.Register(c => new OrderQueries(QueriesConnectionString))
            .As<IOrderQueries>()
            .InstancePerLifetimeScope();
        builder.RegisterType<BuyerRepository>()
            .As<IBuyerRepository>()
            .InstancePerLifetimeScope();
        builder.RegisterType<OrderRepository>()
            .As<IOrderRepository>()
            .InstancePerLifetimeScope();
        builder.RegisterType<RequestManager>()
            .As<IRequestManager>()
            .InstancePerLifetimeScope();
   }
}
```

<span data-ttu-id="70c9e-148">Autofac 也有功能可[掃描組件以及按命名慣例註冊類型](https://autofac.readthedocs.io/en/latest/register/scanning.html)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-148">Autofac also has a feature to [scan assemblies and register types by name conventions](https://autofac.readthedocs.io/en/latest/register/scanning.html).</span></span>

<span data-ttu-id="70c9e-149">註冊程序和概念與您可向內建 ASP.NET Core IoC 容器註冊類型的方式極為類似，但使用 Autofac 時的語法略為不同。</span><span class="sxs-lookup"><span data-stu-id="70c9e-149">The registration process and concepts are very similar to the way you can register types with the built-in ASP.NET Core IoC container, but the syntax when using Autofac is a bit different.</span></span>

<span data-ttu-id="70c9e-150">在範例程式碼中，會一起註冊抽象 IOrderRepository 與實作類別 OrderRepository。</span><span class="sxs-lookup"><span data-stu-id="70c9e-150">In the example code, the abstraction IOrderRepository is registered along with the implementation class OrderRepository.</span></span> <span data-ttu-id="70c9e-151">這表示只要建構函式透過 IOrderRepository 抽象或介面來宣告相依性，IoC 容器就會插入 OrderRepository 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="70c9e-151">This means that whenever a constructor is declaring a dependency through the IOrderRepository abstraction or interface, the IoC container will inject an instance of the OrderRepository class.</span></span>

<span data-ttu-id="70c9e-152">執行個體範圍類型決定如何在相同服務或相依性的要求之間共用執行個體。</span><span class="sxs-lookup"><span data-stu-id="70c9e-152">The instance scope type determines how an instance is shared between requests for the same service or dependency.</span></span> <span data-ttu-id="70c9e-153">提出相依性要求時，IoC 容器可以傳回下列結果：</span><span class="sxs-lookup"><span data-stu-id="70c9e-153">When a request is made for a dependency, the IoC container can return the following:</span></span>

- <span data-ttu-id="70c9e-154">一個存留期範圍有單一執行個體 (在 ASP.NET Core IoC 容器中稱為「範圍」)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-154">A single instance per lifetime scope (referred to in the ASP.NET Core IoC container as *scoped*).</span></span>

- <span data-ttu-id="70c9e-155">一個相依性有新的執行個體 (在 ASP.NET Core IoC 容器中稱為「暫時性」)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-155">A new instance per dependency (referred to in the ASP.NET Core IoC container as *transient*).</span></span>

- <span data-ttu-id="70c9e-156">跨所有使用 IoC 容器的物件所共用的單一執行個體 (在 ASP.NET Core IoC 容器中稱為「單一」).</span><span class="sxs-lookup"><span data-stu-id="70c9e-156">A single instance shared across all objects using the IoC container (referred to in the ASP.NET Core IoC container as *singleton*).</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="70c9e-157">其他資源</span><span class="sxs-lookup"><span data-stu-id="70c9e-157">Additional resources</span></span>

- <span data-ttu-id="70c9e-158">**ASP.NET Core 中的相依性插入簡介** </span><span class="sxs-lookup"><span data-stu-id="70c9e-158">**Introduction to Dependency Injection in ASP.NET Core** </span></span>\
  [https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection](/aspnet/core/fundamentals/dependency-injection)

- <span data-ttu-id="70c9e-159">**Autofac.**</span><span class="sxs-lookup"><span data-stu-id="70c9e-159">**Autofac.**</span></span> <span data-ttu-id="70c9e-160">正式文件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-160">Official documentation.</span></span> \
  <https://docs.autofac.org/en/latest/>

- <span data-ttu-id="70c9e-161">**比較 ASP.NET Core IoC 容器服務存留期與 Autofac IoC 容器執行個體範圍 - Cesar de la Torre。**</span><span class="sxs-lookup"><span data-stu-id="70c9e-161">**Comparing ASP.NET Core IoC container service lifetimes with Autofac IoC container instance scopes - Cesar de la Torre.**</span></span> \
  <https://devblogs.microsoft.com/cesardelatorre/comparing-asp-net-core-ioc-service-life-times-and-autofac-ioc-instance-scopes/>

## <a name="implement-the-command-and-command-handler-patterns"></a><span data-ttu-id="70c9e-162">實作命令和命令處理常式模式</span><span class="sxs-lookup"><span data-stu-id="70c9e-162">Implement the Command and Command Handler patterns</span></span>

<span data-ttu-id="70c9e-163">在上節所顯示的透過建構函式的 DI 範例中，IoC 容器將會透過類別中的建構函式來插入存放庫。</span><span class="sxs-lookup"><span data-stu-id="70c9e-163">In the DI-through-constructor example shown in the previous section, the IoC container was injecting repositories through a constructor in a class.</span></span> <span data-ttu-id="70c9e-164">但，其確切插入位置為何？</span><span class="sxs-lookup"><span data-stu-id="70c9e-164">But exactly where were they injected?</span></span> <span data-ttu-id="70c9e-165">例如，在簡單的 Web API (例如，在 eShopOnContainers) 中的目錄微服務，您會將它們插入至控制器的中的 MVC 控制器層級，作為 ASP.NET Core 要求管線的一部分。</span><span class="sxs-lookup"><span data-stu-id="70c9e-165">In a simple Web API (for example, the catalog microservice in eShopOnContainers), you inject them at the MVC controllers' level, in a controller constructor, as part of the request pipeline of ASP.NET Core.</span></span> <span data-ttu-id="70c9e-166">不過，在此區段的初始程式碼中 (eShopOnContainers 的 Ordering.API 服務中的 [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) 類別)，是透過特定命令處理常式的建構函式來插入相依性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-166">However, in the initial code of this section (the [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) class from the Ordering.API service in eShopOnContainers), the injection of dependencies is done through the constructor of a particular command handler.</span></span> <span data-ttu-id="70c9e-167">讓我們說明什麼是命令處理常式以及您想要使用它的原因。</span><span class="sxs-lookup"><span data-stu-id="70c9e-167">Let us explain what a command handler is and why you would want to use it.</span></span>

<span data-ttu-id="70c9e-168">命令模式本質上與本指南稍早介紹的 CQRS 模式有關。</span><span class="sxs-lookup"><span data-stu-id="70c9e-168">The Command pattern is intrinsically related to the CQRS pattern that was introduced earlier in this guide.</span></span> <span data-ttu-id="70c9e-169">CQRS 有兩端。</span><span class="sxs-lookup"><span data-stu-id="70c9e-169">CQRS has two sides.</span></span> <span data-ttu-id="70c9e-170">第一個區域是搭配使用簡化查詢與 [Dapper](https://github.com/StackExchange/dapper-dot-net) 微 ORM (先前已說明過) 的查詢。</span><span class="sxs-lookup"><span data-stu-id="70c9e-170">The first area is queries, using simplified queries with the [Dapper](https://github.com/StackExchange/dapper-dot-net) micro ORM, which was explained previously.</span></span> <span data-ttu-id="70c9e-171">第二個區域是命令，這是交易的起點以及服務外部的輸入通道。</span><span class="sxs-lookup"><span data-stu-id="70c9e-171">The second area is commands, which are the starting point for transactions, and the input channel from outside the service.</span></span>

<span data-ttu-id="70c9e-172">如圖7-24 所示，模式是以從用戶端接受命令為基礎，根據領域模型規則處理它們，最後保存交易的狀態。</span><span class="sxs-lookup"><span data-stu-id="70c9e-172">As shown in Figure 7-24, the pattern is based on accepting commands from the client-side, processing them based on the domain model rules, and finally persisting the states with transactions.</span></span>

![顯示從用戶端到資料庫之高階資料流程的圖表。](./media/microservice-application-layer-implementation-web-api/high-level-writes-side.png)

<span data-ttu-id="70c9e-174">**圖 7-24**.</span><span class="sxs-lookup"><span data-stu-id="70c9e-174">**Figure 7-24**.</span></span> <span data-ttu-id="70c9e-175">CQRS 模式中命令或「交易式端」的高階觀點</span><span class="sxs-lookup"><span data-stu-id="70c9e-175">High-level view of the commands or "transactional side" in a CQRS pattern</span></span>

<span data-ttu-id="70c9e-176">圖7-24 顯示 UI 應用程式透過 API 傳送命令，該 API 會 `CommandHandler` 根據領域模型和基礎結構來更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="70c9e-176">Figure 7-24 shows that the UI app sends a command through the API that gets to a `CommandHandler`, that depends on the Domain model and the Infrastructure, to update the database.</span></span>

### <a name="the-command-class"></a><span data-ttu-id="70c9e-177">命令類別</span><span class="sxs-lookup"><span data-stu-id="70c9e-177">The command class</span></span>

<span data-ttu-id="70c9e-178">命令是一種要求，讓系統執行可變更系統狀態的動作。</span><span class="sxs-lookup"><span data-stu-id="70c9e-178">A command is a request for the system to perform an action that changes the state of the system.</span></span> <span data-ttu-id="70c9e-179">命令是命令式的，而且只應該處理一次。</span><span class="sxs-lookup"><span data-stu-id="70c9e-179">Commands are imperative, and should be processed just once.</span></span>

<span data-ttu-id="70c9e-180">因為命令是命令式的，所以通常是透過命令式方式使用動詞進行命名 (例如，"create" 或 "update")，而且可能包含彙總類型 (例如 CreateOrderCommand)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-180">Since commands are imperatives, they are typically named with a verb in the imperative mood (for example, "create" or "update"), and they might include the aggregate type, such as CreateOrderCommand.</span></span> <span data-ttu-id="70c9e-181">與事件不同，命令不是過去的事實；它只是要求，因此可能會遭拒絕。</span><span class="sxs-lookup"><span data-stu-id="70c9e-181">Unlike an event, a command is not a fact from the past; it is only a request, and thus may be refused.</span></span>

<span data-ttu-id="70c9e-182">程序管理員指示彙總來執行動作時，命令可能因起始要求的使用者而源自 UI，或源自程序管理員。</span><span class="sxs-lookup"><span data-stu-id="70c9e-182">Commands can originate from the UI as a result of a user initiating a request, or from a process manager when the process manager is directing an aggregate to perform an action.</span></span>

<span data-ttu-id="70c9e-183">命令的重要特性是單一接收者只應該處理它一次。</span><span class="sxs-lookup"><span data-stu-id="70c9e-183">An important characteristic of a command is that it should be processed just once by a single receiver.</span></span> <span data-ttu-id="70c9e-184">原因是命令是您想要在應用程式中執行的單一動作或交易。</span><span class="sxs-lookup"><span data-stu-id="70c9e-184">This is because a command is a single action or transaction you want to perform in the application.</span></span> <span data-ttu-id="70c9e-185">例如，相同的訂單建立命令只應該處理一次。</span><span class="sxs-lookup"><span data-stu-id="70c9e-185">For example, the same order creation command should not be processed more than once.</span></span> <span data-ttu-id="70c9e-186">這是命令與事件之間的重要差異。</span><span class="sxs-lookup"><span data-stu-id="70c9e-186">This is an important difference between commands and events.</span></span> <span data-ttu-id="70c9e-187">可能會多次處理事件，因為許多系統或微服務可能都會對事件感興趣。</span><span class="sxs-lookup"><span data-stu-id="70c9e-187">Events may be processed multiple times, because many systems or microservices might be interested in the event.</span></span>

<span data-ttu-id="70c9e-188">此外，如果命令不是等冪，則命令務必只處理一次。</span><span class="sxs-lookup"><span data-stu-id="70c9e-188">In addition, it is important that a command be processed only once in case the command is not idempotent.</span></span> <span data-ttu-id="70c9e-189">如果基於命令本質或系統處理命令的方式，命令可以執行多次，而不變更結果，則命令為等冪。</span><span class="sxs-lookup"><span data-stu-id="70c9e-189">A command is idempotent if it can be executed multiple times without changing the result, either because of the nature of the command, or because of the way the system handles the command.</span></span>

<span data-ttu-id="70c9e-190">最好的作法是在您的網域商務規則和非變異下，讓命令和更新等冪成為有利的。</span><span class="sxs-lookup"><span data-stu-id="70c9e-190">It is a good practice to make your commands and updates idempotent when it makes sense under your domain's business rules and invariants.</span></span> <span data-ttu-id="70c9e-191">例如，若要使用相同的範例，如果基於任何原因 (重試邏輯、駭客等等) 相同的 CreateOrder 命令到達您的系統多次，則您應該可以識別它，並確保未建立多個訂單。</span><span class="sxs-lookup"><span data-stu-id="70c9e-191">For instance, to use the same example, if for any reason (retry logic, hacking, etc.) the same CreateOrder command reaches your system multiple times, you should be able to identify it and ensure that you do not create multiple orders.</span></span> <span data-ttu-id="70c9e-192">若要這樣做，您需要在作業中附加某種類型的身分識別，並識別是否已處理命令或更新。</span><span class="sxs-lookup"><span data-stu-id="70c9e-192">To do so, you need to attach some kind of identity in the operations and identify whether the command or update was already processed.</span></span>

<span data-ttu-id="70c9e-193">您將命令傳送給單一接收者；請不要發行命令。</span><span class="sxs-lookup"><span data-stu-id="70c9e-193">You send a command to a single receiver; you do not publish a command.</span></span> <span data-ttu-id="70c9e-194">發佈適用於指出事實的事件：發生了某事，而事件接收者可能對此感興趣。</span><span class="sxs-lookup"><span data-stu-id="70c9e-194">Publishing is for events that state a fact—that something has happened and might be interesting for event receivers.</span></span> <span data-ttu-id="70c9e-195">如果是事件，則發行者不會關心哪些接收器收到事件或其處理方式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-195">In the case of events, the publisher has no concerns about which receivers get the event or what they do it.</span></span> <span data-ttu-id="70c9e-196">但是先前各節中已介紹過的網域或整合事件則不同。</span><span class="sxs-lookup"><span data-stu-id="70c9e-196">But domain or integration events are a different story already introduced in previous sections.</span></span>

<span data-ttu-id="70c9e-197">命令是使用類別進行實作，而類別包含資料欄位或具有執行該命令所需之所有資訊的集合。</span><span class="sxs-lookup"><span data-stu-id="70c9e-197">A command is implemented with a class that contains data fields or collections with all the information that is needed in order to execute that command.</span></span> <span data-ttu-id="70c9e-198">命令是一種特殊的資料轉送物件 (DTO)，專門用來要求變更或交易。</span><span class="sxs-lookup"><span data-stu-id="70c9e-198">A command is a special kind of Data Transfer Object (DTO), one that is specifically used to request changes or transactions.</span></span> <span data-ttu-id="70c9e-199">命令本身只根據處理命令所需的資訊，而不需要其他資訊。</span><span class="sxs-lookup"><span data-stu-id="70c9e-199">The command itself is based on exactly the information that is needed for processing the command, and nothing more.</span></span>

<span data-ttu-id="70c9e-200">下列範例顯示簡化的 `CreateOrderCommand` 類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-200">The following example shows the simplified `CreateOrderCommand` class.</span></span> <span data-ttu-id="70c9e-201">這是 eShopOnContainers 訂購微服務中所使用的不可變命令。</span><span class="sxs-lookup"><span data-stu-id="70c9e-201">This is an immutable command that is used in the ordering microservice in eShopOnContainers.</span></span>

```csharp
// DDD and CQRS patterns comment: Note that it is recommended to implement immutable Commands
// In this case, its immutability is achieved by having all the setters as private
// plus only being able to update the data just once, when creating the object through its constructor.
// References on Immutable Commands:
// http://cqrs.nu/Faq
// https://docs.spine3.org/motivation/immutability.html
// http://blog.gauffin.org/2012/06/griffin-container-introducing-command-support/
// https://docs.microsoft.com/dotnet/csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties

[DataContract]
public class CreateOrderCommand
    : IRequest<bool>
{
    [DataMember]
    private readonly List<OrderItemDTO> _orderItems;

    [DataMember]
    public string UserId { get; private set; }

    [DataMember]
    public string UserName { get; private set; }

    [DataMember]
    public string City { get; private set; }

    [DataMember]
    public string Street { get; private set; }

    [DataMember]
    public string State { get; private set; }

    [DataMember]
    public string Country { get; private set; }

    [DataMember]
    public string ZipCode { get; private set; }

    [DataMember]
    public string CardNumber { get; private set; }

    [DataMember]
    public string CardHolderName { get; private set; }

    [DataMember]
    public DateTime CardExpiration { get; private set; }

    [DataMember]
    public string CardSecurityNumber { get; private set; }

    [DataMember]
    public int CardTypeId { get; private set; }

    [DataMember]
    public IEnumerable<OrderItemDTO> OrderItems => _orderItems;

    public CreateOrderCommand()
    {
        _orderItems = new List<OrderItemDTO>();
    }

    public CreateOrderCommand(List<BasketItem> basketItems, string userId, string userName, string city, string street, string state, string country, string zipcode,
        string cardNumber, string cardHolderName, DateTime cardExpiration,
        string cardSecurityNumber, int cardTypeId) : this()
    {
        _orderItems = basketItems.ToOrderItemsDTO().ToList();
        UserId = userId;
        UserName = userName;
        City = city;
        Street = street;
        State = state;
        Country = country;
        ZipCode = zipcode;
        CardNumber = cardNumber;
        CardHolderName = cardHolderName;
        CardExpiration = cardExpiration;
        CardSecurityNumber = cardSecurityNumber;
        CardTypeId = cardTypeId;
        CardExpiration = cardExpiration;
    }


    public class OrderItemDTO
    {
        public int ProductId { get; set; }

        public string ProductName { get; set; }

        public decimal UnitPrice { get; set; }

        public decimal Discount { get; set; }

        public int Units { get; set; }

        public string PictureUrl { get; set; }
    }
}
```

<span data-ttu-id="70c9e-202">基本上，此命令類別包含您使用領域模型物件來執行商務交易所需的所有資料。</span><span class="sxs-lookup"><span data-stu-id="70c9e-202">Basically, the command class contains all the data you need for performing a business transaction by using the domain model objects.</span></span> <span data-ttu-id="70c9e-203">因此，命令只是包含唯讀資料而沒有行為的資料結構。</span><span class="sxs-lookup"><span data-stu-id="70c9e-203">Thus, commands are simply data structures that contain read-only data, and no behavior.</span></span> <span data-ttu-id="70c9e-204">命令的名稱表示其用途。</span><span class="sxs-lookup"><span data-stu-id="70c9e-204">The command's name indicates its purpose.</span></span> <span data-ttu-id="70c9e-205">在許多 C# 這類語言中，命令會呈現為類別，但就實際物件導向意義而言，它們不是真正的類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-205">In many languages like C#, commands are represented as classes, but they are not true classes in the real object-oriented sense.</span></span>

<span data-ttu-id="70c9e-206">作為其他特性，命令是不可變的，因為預期的用法是領域模型會直接處理它們。</span><span class="sxs-lookup"><span data-stu-id="70c9e-206">As an additional characteristic, commands are immutable, because the expected usage is that they are processed directly by the domain model.</span></span> <span data-ttu-id="70c9e-207">它們在其預測存留期間不需要變更。</span><span class="sxs-lookup"><span data-stu-id="70c9e-207">They do not need to change during their projected lifetime.</span></span> <span data-ttu-id="70c9e-208">在 c # 類別中，沒有任何 setter 或變更內部狀態的其他方法，可以達到永久性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-208">In a C# class, immutability can be achieved by not having any setters or other methods that change the internal state.</span></span>

<span data-ttu-id="70c9e-209">請記住，如果您想要或預期命令會通過序列化/還原序列化程式，則屬性必須有私用 setter，以及 `[DataMember]` (或 `[JsonProperty]`) 屬性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-209">Keep in mind that if you intend or expect commands to go through a serializing/deserializing process, the properties must have a private setter, and the `[DataMember]` (or `[JsonProperty]`) attribute.</span></span> <span data-ttu-id="70c9e-210">否則，還原序列化無法在目的地使用必要的值來重建物件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-210">Otherwise, the deserializer won't be able to reconstruct the object at the destination with the required values.</span></span> <span data-ttu-id="70c9e-211">如果類別有一個具有所有屬性參數的函式，且具有一般 camelCase 命名慣例，並將其標注為，則您也可以使用真正的唯讀屬性 `[JsonConstructor]` 。</span><span class="sxs-lookup"><span data-stu-id="70c9e-211">You can also use truly read-only properties if the class has a constructor with parameters for all properties, with the usual camelCase naming convention, and annotate the constructor as `[JsonConstructor]`.</span></span> <span data-ttu-id="70c9e-212">不過，此選項需要更多程式碼。</span><span class="sxs-lookup"><span data-stu-id="70c9e-212">However, this option requires more code.</span></span>

<span data-ttu-id="70c9e-213">例如，建立訂單的命令類別可能類似您想要建立之訂單的資料，但您可能不需要相同的屬性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-213">For example, the command class for creating an order is probably similar in terms of data to the order you want to create, but you probably do not need the same attributes.</span></span> <span data-ttu-id="70c9e-214">例如，沒有 `CreateOrderCommand` 訂單識別碼，因為尚未建立訂單。</span><span class="sxs-lookup"><span data-stu-id="70c9e-214">For instance, `CreateOrderCommand` does not have an order ID, because the order has not been created yet.</span></span>

<span data-ttu-id="70c9e-215">許多命令類別都可以簡單，只需要某個需要變更之狀態的幾個欄位。</span><span class="sxs-lookup"><span data-stu-id="70c9e-215">Many command classes can be simple, requiring only a few fields about some state that needs to be changed.</span></span> <span data-ttu-id="70c9e-216">如果您只是使用類似下列的命令，將訂單的狀態從「處理中」變更為「已付款」或「已出貨」，就會發生這種情況：</span><span class="sxs-lookup"><span data-stu-id="70c9e-216">That would be the case if you are just changing the status of an order from "in process" to "paid" or "shipped" by using a command similar to the following:</span></span>

```csharp
[DataContract]
public class UpdateOrderStatusCommand
    :IRequest<bool>
{
    [DataMember]
    public string Status { get; private set; }

    [DataMember]
    public string OrderId { get; private set; }

    [DataMember]
    public string BuyerIdentityGuid { get; private set; }
}
```

<span data-ttu-id="70c9e-217">有些開發人員會區隔其 UI 要求物件與其命令 DTO，但這只是喜好設定。</span><span class="sxs-lookup"><span data-stu-id="70c9e-217">Some developers make their UI request objects separate from their command DTOs, but that is just a matter of preference.</span></span> <span data-ttu-id="70c9e-218">它是一種繁瑣的區隔，而且沒有額外的價值，而物件幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="70c9e-218">It is a tedious separation with not much additional value, and the objects are almost exactly the same shape.</span></span> <span data-ttu-id="70c9e-219">例如，在 eShopOnContainers 中，有些命令會直接來自用戶端。</span><span class="sxs-lookup"><span data-stu-id="70c9e-219">For instance, in eShopOnContainers, some commands come directly from the client-side.</span></span>

### <a name="the-command-handler-class"></a><span data-ttu-id="70c9e-220">命令處理常式類別</span><span class="sxs-lookup"><span data-stu-id="70c9e-220">The Command handler class</span></span>

<span data-ttu-id="70c9e-221">您應該為每個命令實作特定命令處理常式類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-221">You should implement a specific command handler class for each command.</span></span> <span data-ttu-id="70c9e-222">這就是模式的運作方式，而您將使用命令物件、網域物件和基礎結構存放庫物件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-222">That is how the pattern works, and it's where you'll use the command object, the domain objects, and the infrastructure repository objects.</span></span> <span data-ttu-id="70c9e-223">命令處理常式實際上是 CQRS 和 DDD 的應用程式層中心。</span><span class="sxs-lookup"><span data-stu-id="70c9e-223">The command handler is in fact the heart of the application layer in terms of CQRS and DDD.</span></span> <span data-ttu-id="70c9e-224">不過，所有領域邏輯都應該包含在網域類別中， (根實體) 、子實體或 [網域服務](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/)，但不在命令處理常式中，這是應用層的類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-224">However, all the domain logic should be contained in the domain classes—within the aggregate roots (root entities), child entities, or [domain services](https://lostechies.com/jimmybogard/2008/08/21/services-in-domain-driven-design/), but not within the command handler, which is a class from the application layer.</span></span>

<span data-ttu-id="70c9e-225">命令處理常式類別提供強式的墊腳石來達成前節中所述的單一職責原則 (SRP)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-225">The command handler class offers a strong stepping stone in the way to achieve the Single Responsibility Principle (SRP) mentioned in a previous section.</span></span>

<span data-ttu-id="70c9e-226">命令處理常式會收到命令，並取得所使用彙總的結果。</span><span class="sxs-lookup"><span data-stu-id="70c9e-226">A command handler receives a command and obtains a result from the aggregate that is used.</span></span> <span data-ttu-id="70c9e-227">結果應該是命令執行成功或是發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="70c9e-227">The result should be either successful execution of the command, or an exception.</span></span> <span data-ttu-id="70c9e-228">如果是例外狀況，則系統狀態應該會維持不變。</span><span class="sxs-lookup"><span data-stu-id="70c9e-228">In the case of an exception, the system state should be unchanged.</span></span>

<span data-ttu-id="70c9e-229">命令處理常式通常會採取下列步驟：</span><span class="sxs-lookup"><span data-stu-id="70c9e-229">The command handler usually takes the following steps:</span></span>

- <span data-ttu-id="70c9e-230">接收命令物件，例如 DTO (從[中繼程序](https://en.wikipedia.org/wiki/Mediator_pattern)或其他基礎結構物件)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-230">It receives the command object, like a DTO (from the [mediator](https://en.wikipedia.org/wiki/Mediator_pattern) or other infrastructure object).</span></span>

- <span data-ttu-id="70c9e-231">驗證命令有效 (如果未經中繼程序驗證)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-231">It validates that the command is valid (if not validated by the mediator).</span></span>

- <span data-ttu-id="70c9e-232">具現化為目前命令目標的彙總根執行個體。</span><span class="sxs-lookup"><span data-stu-id="70c9e-232">It instantiates the aggregate root instance that is the target of the current command.</span></span>

- <span data-ttu-id="70c9e-233">對彙總根執行個體執行方法，以透過命令取得必要資料。</span><span class="sxs-lookup"><span data-stu-id="70c9e-233">It executes the method on the aggregate root instance, getting the required data from the command.</span></span>

- <span data-ttu-id="70c9e-234">它會將彙總的新狀態持續保存至其相關資料庫。</span><span class="sxs-lookup"><span data-stu-id="70c9e-234">It persists the new state of the aggregate to its related database.</span></span> <span data-ttu-id="70c9e-235">這個最後一項作業是實際交易。</span><span class="sxs-lookup"><span data-stu-id="70c9e-235">This last operation is the actual transaction.</span></span>

<span data-ttu-id="70c9e-236">一般而言，命令處理常式會處理其彙總根 (根實體) 所驅動的單一彙總。</span><span class="sxs-lookup"><span data-stu-id="70c9e-236">Typically, a command handler deals with a single aggregate driven by its aggregate root (root entity).</span></span> <span data-ttu-id="70c9e-237">如果接收單一命令會影響多個彙總，則您可以使用領域事件將狀態或動作散佈到多個彙總。</span><span class="sxs-lookup"><span data-stu-id="70c9e-237">If multiple aggregates should be impacted by the reception of a single command, you could use domain events to propagate states or actions across multiple aggregates.</span></span>

<span data-ttu-id="70c9e-238">這裡的重點是處理命令時，所有領域邏輯都應該位在領域模型 (彙總) 內、全部進行封裝，而且可進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="70c9e-238">The important point here is that when a command is being processed, all the domain logic should be inside the domain model (the aggregates), fully encapsulated and ready for unit testing.</span></span> <span data-ttu-id="70c9e-239">命令處理常式只是作為從資料庫取得領域模型的方法以及最後一個步驟，以告知基礎結構層級 (存放庫) 在模型變更時持續保存變更。</span><span class="sxs-lookup"><span data-stu-id="70c9e-239">The command handler just acts as a way to get the domain model from the database, and as the final step, to tell the infrastructure layer (repositories) to persist the changes when the model is changed.</span></span> <span data-ttu-id="70c9e-240">這種方法的優點是您不需要變更應用程式或基礎結構層中的程式碼，即可在隔離、完整封裝且豐富的行為領域模型中重構領域邏輯，而這些層級是連接層級 (命令處理常式、Web API、存放庫等等)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-240">The advantage of this approach is that you can refactor the domain logic in an isolated, fully encapsulated, rich, behavioral domain model without changing code in the application or infrastructure layers, which are the plumbing level (command handlers, Web API, repositories, etc.).</span></span>

<span data-ttu-id="70c9e-241">命令處理常式因太多邏輯而變得複雜時，就會像程式碼。</span><span class="sxs-lookup"><span data-stu-id="70c9e-241">When command handlers get complex, with too much logic, that can be a code smell.</span></span> <span data-ttu-id="70c9e-242">檢閱其內容，而且，如果您發現領域邏輯，請重構程式碼，以將該領域行為移至領域物件 (彙總根和子實體) 的方法。</span><span class="sxs-lookup"><span data-stu-id="70c9e-242">Review them, and if you find domain logic, refactor the code to move that domain behavior to the methods of the domain objects (the aggregate root and child entity).</span></span>

<span data-ttu-id="70c9e-243">下列程式碼是命令處理常式類別的範例，會顯示 `CreateOrderCommandHandler` 您在本章節開頭看到的相同類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-243">As an example of a command handler class, the following code shows the same `CreateOrderCommandHandler` class that you saw at the beginning of this chapter.</span></span> <span data-ttu-id="70c9e-244">在這種情況下，它也會反白顯示使用領域模型物件/匯總的控制碼方法和作業。</span><span class="sxs-lookup"><span data-stu-id="70c9e-244">In this case, it also highlights the Handle method and the operations with the domain model objects/aggregates.</span></span>

```csharp
public class CreateOrderCommandHandler
        : IRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;
    private readonly IOrderingIntegrationEventService _orderingIntegrationEventService;
    private readonly ILogger<CreateOrderCommandHandler> _logger;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
        IOrderingIntegrationEventService orderingIntegrationEventService,
        IOrderRepository orderRepository,
        IIdentityService identityService,
        ILogger<CreateOrderCommandHandler> logger)
    {
        _orderRepository = orderRepository ?? throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ?? throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ?? throw new ArgumentNullException(nameof(mediator));
        _orderingIntegrationEventService = orderingIntegrationEventService ?? throw new ArgumentNullException(nameof(orderingIntegrationEventService));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
    }

    public async Task<bool> Handle(CreateOrderCommand message, CancellationToken cancellationToken)
    {
        // Add Integration event to clean the basket
        var orderStartedIntegrationEvent = new OrderStartedIntegrationEvent(message.UserId);
        await _orderingIntegrationEventService.AddAndSaveEventAsync(orderStartedIntegrationEvent);

        // Add/Update the Buyer AggregateRoot
        // DDD patterns comment: Add child entities and value-objects through the Order Aggregate-Root
        // methods and constructor so validations, invariants and business logic
        // make sure that consistency is preserved across the whole aggregate
        var address = new Address(message.Street, message.City, message.State, message.Country, message.ZipCode);
        var order = new Order(message.UserId, message.UserName, address, message.CardTypeId, message.CardNumber, message.CardSecurityNumber, message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice, item.Discount, item.PictureUrl, item.Units);
        }

        _logger.LogInformation("----- Creating Order - Order: {@Order}", order);

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync(cancellationToken);
    }
}
```

<span data-ttu-id="70c9e-245">下列是命令處理常式應該採取的額外步驟：</span><span class="sxs-lookup"><span data-stu-id="70c9e-245">These are additional steps a command handler should take:</span></span>

- <span data-ttu-id="70c9e-246">使用命令的資料來操作匯總根的方法和行為。</span><span class="sxs-lookup"><span data-stu-id="70c9e-246">Use the command's data to operate with the aggregate root's methods and behavior.</span></span>

- <span data-ttu-id="70c9e-247">在領域物件內部，於執行交易時引發領域事件，但這從命令處理常式觀點是透明的。</span><span class="sxs-lookup"><span data-stu-id="70c9e-247">Internally within the domain objects, raise domain events while the transaction is executed, but that is transparent from a command handler point of view.</span></span>

- <span data-ttu-id="70c9e-248">如果匯總的作業結果成功，而且在交易完成之後，請引發整合事件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-248">If the aggregate's operation result is successful and after the transaction is finished, raise integration events.</span></span> <span data-ttu-id="70c9e-249">(這些可能也是由存放庫這類基礎結構類別所引發)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-249">(These might also be raised by infrastructure classes like repositories.)</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="70c9e-250">其他資源</span><span class="sxs-lookup"><span data-stu-id="70c9e-250">Additional resources</span></span>

- <span data-ttu-id="70c9e-251">**Mark Seemann。在界限中，應用程式不是物件導向** </span><span class="sxs-lookup"><span data-stu-id="70c9e-251">**Mark Seemann. At the Boundaries, Applications are Not Object-Oriented** </span></span>\
  <https://blog.ploeh.dk/2011/05/31/AttheBoundaries,ApplicationsareNotObject-Oriented/>

- <span data-ttu-id="70c9e-252">**命令和事件** </span><span class="sxs-lookup"><span data-stu-id="70c9e-252">**Commands and events** </span></span>\
  <https://cqrs.nu/Faq/commands-and-events>

- <span data-ttu-id="70c9e-253">**命令處理常式有何作用？**</span><span class="sxs-lookup"><span data-stu-id="70c9e-253">**What does a command handler do?**</span></span> \
  <https://cqrs.nu/Faq/command-handlers>

- <span data-ttu-id="70c9e-254">**Jimmy Bogard。網域命令模式–處理常式** </span><span class="sxs-lookup"><span data-stu-id="70c9e-254">**Jimmy Bogard. Domain Command Patterns – Handlers** </span></span>\
  <https://jimmybogard.com/domain-command-patterns-handlers/>

- <span data-ttu-id="70c9e-255">**Jimmy Bogard。網域命令模式–驗證** </span><span class="sxs-lookup"><span data-stu-id="70c9e-255">**Jimmy Bogard. Domain Command Patterns – Validation** </span></span>\
  <https://jimmybogard.com/domain-command-patterns-validation/>

## <a name="the-command-process-pipeline-how-to-trigger-a-command-handler"></a><span data-ttu-id="70c9e-256">命令處理序管道：如何觸發命令處理常式</span><span class="sxs-lookup"><span data-stu-id="70c9e-256">The Command process pipeline: how to trigger a command handler</span></span>

<span data-ttu-id="70c9e-257">下一個問題是如何叫用命令處理常式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-257">The next question is how to invoke a command handler.</span></span> <span data-ttu-id="70c9e-258">您可以從每個相關 ASP.NET Core 控制器中手動呼叫它。</span><span class="sxs-lookup"><span data-stu-id="70c9e-258">You could manually call it from each related ASP.NET Core controller.</span></span> <span data-ttu-id="70c9e-259">不過，該方法結合太多，並不理想。</span><span class="sxs-lookup"><span data-stu-id="70c9e-259">However, that approach would be too coupled and is not ideal.</span></span>

<span data-ttu-id="70c9e-260">另兩個主要選項是建議的選項，包括：</span><span class="sxs-lookup"><span data-stu-id="70c9e-260">The other two main options, which are the recommended options, are:</span></span>

- <span data-ttu-id="70c9e-261">透過記憶體內部中繼程序模式成品。</span><span class="sxs-lookup"><span data-stu-id="70c9e-261">Through an in-memory Mediator pattern artifact.</span></span>

- <span data-ttu-id="70c9e-262">在控制器與處理常式之間使用非同步訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="70c9e-262">With an asynchronous message queue, in between controllers and handlers.</span></span>

### <a name="use-the-mediator-pattern-in-memory-in-the-command-pipeline"></a><span data-ttu-id="70c9e-263">在命令管線中使用中繼程序模式 (記憶體內部)</span><span class="sxs-lookup"><span data-stu-id="70c9e-263">Use the Mediator pattern (in-memory) in the command pipeline</span></span>

<span data-ttu-id="70c9e-264">如圖 7-25 所示，在 CQRS 方法中，您使用與記憶體內部匯流排類似的智慧型中繼程序，而它聰明到可以根據所收到的命令或 DTO 類型，重新導向至正確的命令處理常式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-264">As shown in Figure 7-25, in a CQRS approach you use an intelligent mediator, similar to an in-memory bus, which is smart enough to redirect to the right command handler based on the type of the command or DTO being received.</span></span> <span data-ttu-id="70c9e-265">元件之間的單一黑色箭號代表物件 (在許多情況下，是透過 DI 插入) 與其相關互動之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-265">The single black arrows between components represent the dependencies between objects (in many cases, injected through DI) with their related interactions.</span></span>

![顯示從用戶端到資料庫之更詳細資料流程的圖表。](./media/microservice-application-layer-implementation-web-api/mediator-cqrs-microservice.png)

<span data-ttu-id="70c9e-267">**圖 7-25**。</span><span class="sxs-lookup"><span data-stu-id="70c9e-267">**Figure 7-25**.</span></span> <span data-ttu-id="70c9e-268">在單一 CQRS 微服務過程中使用中繼程序模式</span><span class="sxs-lookup"><span data-stu-id="70c9e-268">Using the Mediator pattern in process in a single CQRS microservice</span></span>

<span data-ttu-id="70c9e-269">上圖顯示影像7-24 的放大： ASP.NET Core 控制器會將命令傳送至 MediatR 的命令管線，使其到達適當的處理常式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-269">The above diagram shows a zoom-in from image 7-24: the ASP.NET Core controller sends the command to MediatR's command pipeline, so they get to the appropriate handler.</span></span>

<span data-ttu-id="70c9e-270">使用中繼程序模式的合理原因是，在企業應用程式中，處理要求會變得複雜。</span><span class="sxs-lookup"><span data-stu-id="70c9e-270">The reason that using the Mediator pattern makes sense is that in enterprise applications, the processing requests can get complicated.</span></span> <span data-ttu-id="70c9e-271">您想要可以新增已開啟數目的跨領域關注，例如記錄、驗證、稽核和安全性。</span><span class="sxs-lookup"><span data-stu-id="70c9e-271">You want to be able to add an open number of cross-cutting concerns like logging, validations, audit, and security.</span></span> <span data-ttu-id="70c9e-272">在這些情況下，您可以依賴中繼程序管道 (請參閱[中繼程序模式](https://en.wikipedia.org/wiki/Mediator_pattern)) 提供這些額外行為或跨領域關注的方法。</span><span class="sxs-lookup"><span data-stu-id="70c9e-272">In these cases, you can rely on a mediator pipeline (see [Mediator pattern](https://en.wikipedia.org/wiki/Mediator_pattern)) to provide a means for these extra behaviors or cross-cutting concerns.</span></span>

<span data-ttu-id="70c9e-273">中繼程式是封裝此進程「如何」的物件：它會根據狀態、叫用命令處理常式的方式，或您提供給處理常式的承載來協調執行。</span><span class="sxs-lookup"><span data-stu-id="70c9e-273">A mediator is an object that encapsulates the "how" of this process: it coordinates execution based on state, the way a command handler is invoked, or the payload you provide to the handler.</span></span> <span data-ttu-id="70c9e-274">有了中繼程式元件，您就可以在[MediatR 3](https://www.nuget.org/packages/MediatR/3.0.0)) 之後套用裝飾專案 (或[管線行為](https://github.com/jbogard/MediatR/wiki/Behaviors)，以集中且透明的方式套用跨領域考慮。</span><span class="sxs-lookup"><span data-stu-id="70c9e-274">With a mediator component, you can apply cross-cutting concerns in a centralized and transparent way by applying decorators (or [pipeline behaviors](https://github.com/jbogard/MediatR/wiki/Behaviors) since [MediatR 3](https://www.nuget.org/packages/MediatR/3.0.0)).</span></span> <span data-ttu-id="70c9e-275">如需詳細資訊，請參閱[裝飾項目模式](https://en.wikipedia.org/wiki/Decorator_pattern)。</span><span class="sxs-lookup"><span data-stu-id="70c9e-275">For more information, see the [Decorator pattern](https://en.wikipedia.org/wiki/Decorator_pattern).</span></span>

<span data-ttu-id="70c9e-276">裝飾項目和行為類似[層面導向程式設計 (AOP)](https://en.wikipedia.org/wiki/Aspect-oriented_programming)，僅套用至中繼程序元件所管理的特定處理序管線。</span><span class="sxs-lookup"><span data-stu-id="70c9e-276">Decorators and behaviors are similar to [Aspect Oriented Programming (AOP)](https://en.wikipedia.org/wiki/Aspect-oriented_programming), only applied to a specific process pipeline managed by the mediator component.</span></span> <span data-ttu-id="70c9e-277">根據在編譯期間插入的「層面編織程序」或根據物件呼叫攔截，套用 AOP 中實作跨領域關注的層面。</span><span class="sxs-lookup"><span data-stu-id="70c9e-277">Aspects in AOP that implement cross-cutting concerns are applied based on *aspect weavers* injected at compilation time or based on object call interception.</span></span> <span data-ttu-id="70c9e-278">這兩種典型 AOP 方法的運作有時稱為「就像變魔術一樣」，因為不容易看到 AOP 的運作工作。</span><span class="sxs-lookup"><span data-stu-id="70c9e-278">Both typical AOP approaches are sometimes said to work "like magic," because it is not easy to see how AOP does its work.</span></span> <span data-ttu-id="70c9e-279">處理嚴重問題或 Bug 時，AOP 很難進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="70c9e-279">When dealing with serious issues or bugs, AOP can be difficult to debug.</span></span> <span data-ttu-id="70c9e-280">另一方面，這些裝飾項目/行為十分明確，而且只會套用至中繼程序內容，因此，偵錯更容易預測且更為輕鬆。</span><span class="sxs-lookup"><span data-stu-id="70c9e-280">On the other hand, these decorators/behaviors are explicit and applied only in the context of the mediator, so debugging is much more predictable and easy.</span></span>

<span data-ttu-id="70c9e-281">例如，在 eShopOnContainers 順序微服務中，有兩個範例行為的實作為 [LogBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) 類別和 [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) 類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-281">For example, in the eShopOnContainers ordering microservice, has an implementation of two sample behaviors, a [LogBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) class and a [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) class.</span></span> <span data-ttu-id="70c9e-282">下一節會說明 eShopOnContainers 如何使用 [MediatR](https://www.nuget.org/packages/MediatR) [行為](https://github.com/jbogard/MediatR/wiki/Behaviors)，來說明行為的實。</span><span class="sxs-lookup"><span data-stu-id="70c9e-282">The implementation of the behaviors is explained in the next section by showing how eShopOnContainers uses [MediatR](https://www.nuget.org/packages/MediatR) [behaviors](https://github.com/jbogard/MediatR/wiki/Behaviors).</span></span>

### <a name="use-message-queues-out-of-proc-in-the-commands-pipeline"></a><span data-ttu-id="70c9e-283">在命令的管線中使用訊息佇列 (跨進程) </span><span class="sxs-lookup"><span data-stu-id="70c9e-283">Use message queues (out-of-proc) in the command's pipeline</span></span>

<span data-ttu-id="70c9e-284">另一個選擇是根據訊息代理程式或訊息佇列來使用非同步訊息，如圖 7-26 所示。</span><span class="sxs-lookup"><span data-stu-id="70c9e-284">Another choice is to use asynchronous messages based on brokers or message queues, as shown in Figure 7-26.</span></span> <span data-ttu-id="70c9e-285">該選項也可以與命令處理常式正前方的中繼程序一起使用。</span><span class="sxs-lookup"><span data-stu-id="70c9e-285">That option could also be combined with the mediator component right before the command handler.</span></span>

![顯示使用 HA 訊息佇列之資料流程的圖表。](./media/microservice-application-layer-implementation-web-api/add-ha-message-queue.png)

<span data-ttu-id="70c9e-287">**圖 7-26**。</span><span class="sxs-lookup"><span data-stu-id="70c9e-287">**Figure 7-26**.</span></span> <span data-ttu-id="70c9e-288">使用訊息佇列 (進程外的程式，以及使用 CQRS 命令的處理序間通訊) </span><span class="sxs-lookup"><span data-stu-id="70c9e-288">Using message queues (out of the process and inter-process communication) with CQRS commands</span></span>

<span data-ttu-id="70c9e-289">命令的管線也可以由高可用性訊息佇列處理，將命令傳遞給適當的處理常式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-289">Command's pipeline can also be handled by a high availability message queue to deliver the commands to the appropriate handler.</span></span> <span data-ttu-id="70c9e-290">使用訊息佇列來接受命令可能會讓命令的管線變得更複雜，因為您可能需要將管線分割成透過外部訊息佇列連接的兩個處理常式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-290">Using message queues to accept the commands can further complicate your command's pipeline, because you will probably need to split the pipeline into two processes connected through the external message queue.</span></span> <span data-ttu-id="70c9e-291">儘管如此，如果您需要擁有根據非同步訊息的已改善延展性和效能，則應該使用它。</span><span class="sxs-lookup"><span data-stu-id="70c9e-291">Still, it should be used if you need to have improved scalability and performance based on asynchronous messaging.</span></span> <span data-ttu-id="70c9e-292">請考慮在圖 7-26 的情況下，控制器只會將命令訊息公佈至佇列並傳回。</span><span class="sxs-lookup"><span data-stu-id="70c9e-292">Consider that in the case of Figure 7-26, the controller just posts the command message into the queue and returns.</span></span> <span data-ttu-id="70c9e-293">命令處理常式接著會依自己的步調來處理訊息。</span><span class="sxs-lookup"><span data-stu-id="70c9e-293">Then the command handlers process the messages at their own pace.</span></span> <span data-ttu-id="70c9e-294">這是佇列的最大好處：訊息佇列可以作為需要超級延展性時的緩衝區，例如針對股票或任何其他具有大量輸入資料的案例。</span><span class="sxs-lookup"><span data-stu-id="70c9e-294">That is a great benefit of queues: the message queue can act as a buffer in cases when hyper scalability is needed, such as for stocks or any other scenario with a high volume of ingress data.</span></span>

<span data-ttu-id="70c9e-295">不過，由於訊息佇列的非同步本質，您必須瞭解如何與用戶端應用程式通訊，以瞭解命令程式的成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="70c9e-295">However, because of the asynchronous nature of message queues, you need to figure out how to communicate with the client application about the success or failure of the command's process.</span></span> <span data-ttu-id="70c9e-296">作為規則，您永遠都不應該使用「引發並忘記」命令。</span><span class="sxs-lookup"><span data-stu-id="70c9e-296">As a rule, you should never use "fire and forget" commands.</span></span> <span data-ttu-id="70c9e-297">每個商務應用程式都需要知道是否已成功處理命令，或至少已驗證和接受命令。</span><span class="sxs-lookup"><span data-stu-id="70c9e-297">Every business application needs to know if a command was processed successfully, or at least validated and accepted.</span></span>

<span data-ttu-id="70c9e-298">因此，在驗證提交至非同步佇列的命令訊息之後，能夠回應用戶端會增加系統的複雜度，相較于在執行交易之後傳回作業結果的同進程命令進程。</span><span class="sxs-lookup"><span data-stu-id="70c9e-298">Thus, being able to respond to the client after validating a command message that was submitted to an asynchronous queue adds complexity to your system, as compared to an in-process command process that returns the operation's result after running the transaction.</span></span> <span data-ttu-id="70c9e-299">使用佇列，您可能需要透過其他作業結果訊息來傳回命令處理序結果，而這需要系統中的額外元件和自訂通訊。</span><span class="sxs-lookup"><span data-stu-id="70c9e-299">Using queues, you might need to return the result of the command process through other operation result messages, which will require additional components and custom communication in your system.</span></span>

<span data-ttu-id="70c9e-300">此外，非同步命令是單向命令，而這在許多情況下可能不需要，如 Burtsev Alexey 與 Greg Young 在[線上對話](https://groups.google.com/forum/#!msg/dddcqrs/xhJHVxDx2pM/WP9qP8ifYCwJ)中的下列有趣交流所述：</span><span class="sxs-lookup"><span data-stu-id="70c9e-300">Additionally, async commands are one-way commands, which in many cases might not be needed, as is explained in the following interesting exchange between Burtsev Alexey and Greg Young in an [online conversation](https://groups.google.com/forum/#!msg/dddcqrs/xhJHVxDx2pM/WP9qP8ifYCwJ):</span></span>

> <span data-ttu-id="70c9e-301">\[Burtsev Alexey \] 我發現很多程式碼，讓人們使用非同步命令處理或單向命令訊息，而不需要這麼做， (它們不會執行一些長時間的作業，它們並不會執行外部非同步程式碼，甚至不會跨應用程式界限使用訊息匯流排) 。</span><span class="sxs-lookup"><span data-stu-id="70c9e-301">\[Burtsev Alexey\] I find lots of code where people use async command handling or one-way command messaging without any reason to do so (they are not doing some long operation, they are not executing external async code, they do not even cross-application boundary to be using message bus).</span></span> <span data-ttu-id="70c9e-302">為什麼它們會造成這種不必要的複雜性？</span><span class="sxs-lookup"><span data-stu-id="70c9e-302">Why do they introduce this unnecessary complexity?</span></span> <span data-ttu-id="70c9e-303">實際上，我到目前為止還沒有看過具有封鎖命令處理常式的 CQRS 程式碼範例，雖然它只會在大部分情況下正常運作。</span><span class="sxs-lookup"><span data-stu-id="70c9e-303">And actually, I haven't seen a CQRS code example with blocking command handlers so far, though it will work just fine in most cases.</span></span>
>
> <span data-ttu-id="70c9e-304">\[Greg 年輕 \] \[ ... \] 非同步命令不存在，其實是另一個事件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-304">\[Greg Young\] \[...\] an asynchronous command doesn't exist; it's actually another event.</span></span> <span data-ttu-id="70c9e-305">如果我必須接受您傳送給我的內容，並在我不同意時引發事件，則您不會再告訴我要做的事 \[ ，而不是命令 \] 。</span><span class="sxs-lookup"><span data-stu-id="70c9e-305">If I must accept what you send me and raise an event if I disagree, it's no longer you telling me to do something \[that is, it's not a command\].</span></span> <span data-ttu-id="70c9e-306">而是告訴我已完成哪項作業。</span><span class="sxs-lookup"><span data-stu-id="70c9e-306">It's you telling me something has been done.</span></span> <span data-ttu-id="70c9e-307">這在一開始略為不同，但有許多影響。</span><span class="sxs-lookup"><span data-stu-id="70c9e-307">This seems like a slight difference at first, but it has many implications.</span></span>

<span data-ttu-id="70c9e-308">非同步命令可大幅增加系統複雜性，因為沒有任何簡單的方式可以指出失敗。</span><span class="sxs-lookup"><span data-stu-id="70c9e-308">Asynchronous commands greatly increase the complexity of a system, because there is no simple way to indicate failures.</span></span> <span data-ttu-id="70c9e-309">因此，不建議使用非同步命令，除非需要調整需求時，或在特殊情況下，透過訊息溝通內部微服務時。</span><span class="sxs-lookup"><span data-stu-id="70c9e-309">Therefore, asynchronous commands are not recommended other than when scaling requirements are needed or in special cases when communicating the internal microservices through messaging.</span></span> <span data-ttu-id="70c9e-310">在這些情況下，您必須針對失敗設計不同的報告和復原系統。</span><span class="sxs-lookup"><span data-stu-id="70c9e-310">In those cases, you must design a separate reporting and recovery system for failures.</span></span>

<span data-ttu-id="70c9e-311">在 eShopOnContainers 的初始版本中，已決定使用同步命令處理、從 HTTP 要求啟動，並由中繼程式模式驅動。</span><span class="sxs-lookup"><span data-stu-id="70c9e-311">In the initial version of eShopOnContainers, it was decided to use synchronous command processing, started from HTTP requests and driven by the Mediator pattern.</span></span> <span data-ttu-id="70c9e-312">這可輕鬆地讓您傳回處理序的成功或失敗，如同 [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/netcore1.1/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) 實作一樣。</span><span class="sxs-lookup"><span data-stu-id="70c9e-312">That easily allows you to return the success or failure of the process, as in the [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/netcore1.1/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs) implementation.</span></span>

<span data-ttu-id="70c9e-313">在任何情況下，這應該是根據您的應用程式或微服務的商務需求進行決策。</span><span class="sxs-lookup"><span data-stu-id="70c9e-313">In any case, this should be a decision based on your application's or microservice's business requirements.</span></span>

## <a name="implement-the-command-process-pipeline-with-a-mediator-pattern-mediatr"></a><span data-ttu-id="70c9e-314">使用中繼程序模式 (MediatR) 實作命令處理序管線</span><span class="sxs-lookup"><span data-stu-id="70c9e-314">Implement the command process pipeline with a mediator pattern (MediatR)</span></span>

<span data-ttu-id="70c9e-315">作為範例實作，本指南建議根據中繼程序模式來使用同處理序管道，在記憶體內部將命令擷取和路由命令驅動到正確命令處理常式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-315">As a sample implementation, this guide proposes using the in-process pipeline based on the Mediator pattern to drive command ingestion and route commands, in memory, to the right command handlers.</span></span> <span data-ttu-id="70c9e-316">本指南也會建議套用[行為](https://github.com/jbogard/MediatR/wiki/Behaviors)以區隔跨領域關注。</span><span class="sxs-lookup"><span data-stu-id="70c9e-316">The guide also proposes applying [behaviors](https://github.com/jbogard/MediatR/wiki/Behaviors) in order to separate cross-cutting concerns.</span></span>

<span data-ttu-id="70c9e-317">在 .NET 中執行時，有多個開放原始碼程式庫可執行中繼程式模式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-317">For implementation in .NET, there are multiple open-source libraries available that implement the Mediator pattern.</span></span> <span data-ttu-id="70c9e-318">本指南中所使用的程式庫是 [MediatR](https://github.com/jbogard/MediatR) 開放原始碼程式庫 (由 Jimmy Bogard 所建立)，但您可以使用另一種方法。</span><span class="sxs-lookup"><span data-stu-id="70c9e-318">The library used in this guide is the [MediatR](https://github.com/jbogard/MediatR) open-source library (created by Jimmy Bogard), but you could use another approach.</span></span> <span data-ttu-id="70c9e-319">MediatR 是小型且簡單的程式庫，可讓您處理命令這類記憶體內部訊息，同時套用裝飾項目或行為。</span><span class="sxs-lookup"><span data-stu-id="70c9e-319">MediatR is a small and simple library that allows you to process in-memory messages like a command, while applying decorators or behaviors.</span></span>

<span data-ttu-id="70c9e-320">使用中繼程序模式可協助您減少結合，並找出所要求工作的關注，同時自動連接至執行該工作的處理常式，在此情況下，是連接至命令處理常式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-320">Using the Mediator pattern helps you to reduce coupling and to isolate the concerns of the requested work, while automatically connecting to the handler that performs that work—in this case, to command handlers.</span></span>

<span data-ttu-id="70c9e-321">檢閱本指南時，Jimmy Bogard 會說明另一個使用中繼程序模式的好理由：</span><span class="sxs-lookup"><span data-stu-id="70c9e-321">Another good reason to use the Mediator pattern was explained by Jimmy Bogard when reviewing this guide:</span></span>

> <span data-ttu-id="70c9e-322">我認為您可能需要注意這裡的測試 - 它提供不錯的一致窗口，讓您查看系統的行為。</span><span class="sxs-lookup"><span data-stu-id="70c9e-322">I think it might be worth mentioning testing here – it provides a nice consistent window into the behavior of your system.</span></span> <span data-ttu-id="70c9e-323">要求-傳入，回應。我們發現這一點非常適合用來建立一致的行為測試。</span><span class="sxs-lookup"><span data-stu-id="70c9e-323">Request-in, response-out. We've found that aspect quite valuable in building consistently behaving tests.</span></span>

<span data-ttu-id="70c9e-324">首先，讓我們看看一個範例 WebAPI 控制器，您實際上會使用中繼程式物件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-324">First, let's look at a sample WebAPI controller where you actually would use the mediator object.</span></span> <span data-ttu-id="70c9e-325">如果您未使用中繼程式物件，則必須插入該控制器的所有相依性，例如記錄器物件和其他專案。</span><span class="sxs-lookup"><span data-stu-id="70c9e-325">If you weren't using the mediator object, you'd need to inject all the dependencies for that controller, things like a logger object and others.</span></span> <span data-ttu-id="70c9e-326">因此，此函式會很複雜。</span><span class="sxs-lookup"><span data-stu-id="70c9e-326">Therefore, the constructor would be complicated.</span></span> <span data-ttu-id="70c9e-327">另一方面，如果您使用中繼程序物件，則控制器的建構函式可能會較為簡單，即只有一些相依性而不是許多相依性 (如果一個跨領域作業有一個相依性)，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="70c9e-327">On the other hand, if you use the mediator object, the constructor of your controller can be a lot simpler, with just a few dependencies instead of many dependencies if you had one per cross-cutting operation, as in the following example:</span></span>

```csharp
public class MyMicroserviceController : Controller
{
    public MyMicroserviceController(IMediator mediator,
                                    IMyMicroserviceQueries microserviceQueries)
    {
        // ...
    }
}
```

<span data-ttu-id="70c9e-328">您可以看到中繼程序提供全新和簡式 Web API 控制器建構函式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-328">You can see that the mediator provides a clean and lean Web API controller constructor.</span></span> <span data-ttu-id="70c9e-329">此外，在控制器方法內，將命令傳送至中繼程序物件的程式碼幾乎就是一行：</span><span class="sxs-lookup"><span data-stu-id="70c9e-329">In addition, within the controller methods, the code to send a command to the mediator object is almost one line:</span></span>

```csharp
[Route("new")]
[HttpPost]
public async Task<IActionResult> ExecuteBusinessOperation([FromBody]RunOpCommand
                                                               runOperationCommand)
{
    var commandResult = await _mediator.SendAsync(runOperationCommand);

    return commandResult ? (IActionResult)Ok() : (IActionResult)BadRequest();
}
```

### <a name="implement-idempotent-commands"></a><span data-ttu-id="70c9e-330">實作等冪命令</span><span class="sxs-lookup"><span data-stu-id="70c9e-330">Implement idempotent Commands</span></span>

<span data-ttu-id="70c9e-331">在 **eShopOnContainers** 中，比上述更進階的範例是從訂購微服務提交 CreateOrderCommand 物件。</span><span class="sxs-lookup"><span data-stu-id="70c9e-331">In **eShopOnContainers**, a more advanced example than the above is submitting a CreateOrderCommand object from the Ordering microservice.</span></span> <span data-ttu-id="70c9e-332">但由於訂購商務程式有點複雜，而且在我們的案例中，實際上是從購物籃微服務中開始，所以提交 CreateOrderCommand 物件的動作是從名為 [UserCheckoutAcceptedIntegrationEventHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/IntegrationEvents/EventHandling/UserCheckoutAcceptedIntegrationEventHandler.cs) 的整合事件處理常式，而不是從用戶端應用程式呼叫的簡單 WebAPI 控制器來執行，如同先前的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="70c9e-332">But since the Ordering business process is a bit more complex and, in our case, it actually starts in the Basket microservice, this action of submitting the CreateOrderCommand object is performed from an integration-event handler named [UserCheckoutAcceptedIntegrationEventHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/IntegrationEvents/EventHandling/UserCheckoutAcceptedIntegrationEventHandler.cs) instead of a simple WebAPI controller called from the client App as in the previous simpler example.</span></span>

<span data-ttu-id="70c9e-333">不過，將命令提交給 MediatR 的動作相當類似，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="70c9e-333">Nevertheless, the action of submitting the Command to MediatR is pretty similar, as shown in the following code.</span></span>

```csharp
var createOrderCommand = new CreateOrderCommand(eventMsg.Basket.Items,
                                                eventMsg.UserId, eventMsg.City,
                                                eventMsg.Street, eventMsg.State,
                                                eventMsg.Country, eventMsg.ZipCode,
                                                eventMsg.CardNumber,
                                                eventMsg.CardHolderName,
                                                eventMsg.CardExpiration,
                                                eventMsg.CardSecurityNumber,
                                                eventMsg.CardTypeId);

var requestCreateOrder = new IdentifiedCommand<CreateOrderCommand,bool>(createOrderCommand,
                                                                        eventMsg.RequestId);
result = await _mediator.Send(requestCreateOrder);
```

<span data-ttu-id="70c9e-334">不過，這種情況也稍微先進一點，因為我們也會執行等冪命令。</span><span class="sxs-lookup"><span data-stu-id="70c9e-334">However, this case is also slightly more advanced because we're also implementing idempotent commands.</span></span> <span data-ttu-id="70c9e-335">CreateOrderCommand 處理序應該是等冪，因此，如果相同的訊息因任何原因 (例如重試) 而透過網路進行複製，則相同的商務訂單只會處理一次。</span><span class="sxs-lookup"><span data-stu-id="70c9e-335">The CreateOrderCommand process should be idempotent, so if the same message comes duplicated through the network, because of any reason, like retries, the same business order will be processed just once.</span></span>

<span data-ttu-id="70c9e-336">這是藉由包裝商務命令 (來執行，在此案例中，CreateOrderCommand) 並將其內嵌至一般 Identifiedcommand 而中，而每個訊息的識別碼都會透過具有等冪性的網路進行追蹤。</span><span class="sxs-lookup"><span data-stu-id="70c9e-336">This is implemented by wrapping the business command (in this case CreateOrderCommand) and embedding it into a generic IdentifiedCommand, which is tracked by an ID of every message coming through the network that has to be idempotent.</span></span>

<span data-ttu-id="70c9e-337">在下列程式碼中，您可以看到 IdentifiedCommand 就只是具有識別碼和已包裝商務命令物件的 DTO。</span><span class="sxs-lookup"><span data-stu-id="70c9e-337">In the code below, you can see that the IdentifiedCommand is nothing more than a DTO with and ID plus the wrapped business command object.</span></span>

```csharp
public class IdentifiedCommand<T, R> : IRequest<R>
    where T : IRequest<R>
{
    public T Command { get; }
    public Guid Id { get; }
    public IdentifiedCommand(T command, Guid id)
    {
        Command = command;
        Id = id;
    }
}
```

<span data-ttu-id="70c9e-338">然後，IdentifiedCommand 的 CommandHandler (名為 [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs)) 基本上會檢查資料表中是否已有為訊息一部分的識別碼。</span><span class="sxs-lookup"><span data-stu-id="70c9e-338">Then the CommandHandler for the IdentifiedCommand named [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs) will basically check if the ID coming as part of the message already exists in a table.</span></span> <span data-ttu-id="70c9e-339">如果已經存在，則不會再次處理該命令，因此它的行為會是等冪的命令。</span><span class="sxs-lookup"><span data-stu-id="70c9e-339">If it already exists, that command won't be processed again, so it behaves as an idempotent command.</span></span> <span data-ttu-id="70c9e-340">該基礎結構程式碼是透過下面所呼叫的 `_requestManager.ExistAsync` 方法來執行。</span><span class="sxs-lookup"><span data-stu-id="70c9e-340">That infrastructure code is performed by the `_requestManager.ExistAsync` method call below.</span></span>

```csharp
// IdentifiedCommandHandler.cs
public class IdentifiedCommandHandler<T, R> : IRequestHandler<IdentifiedCommand<T, R>, R>
        where T : IRequest<R>
{
    private readonly IMediator _mediator;
    private readonly IRequestManager _requestManager;
    private readonly ILogger<IdentifiedCommandHandler<T, R>> _logger;

    public IdentifiedCommandHandler(
        IMediator mediator,
        IRequestManager requestManager,
        ILogger<IdentifiedCommandHandler<T, R>> logger)
    {
        _mediator = mediator;
        _requestManager = requestManager;
        _logger = logger ?? throw new System.ArgumentNullException(nameof(logger));
    }

    /// <summary>
    /// Creates the result value to return if a previous request was found
    /// </summary>
    /// <returns></returns>
    protected virtual R CreateResultForDuplicateRequest()
    {
        return default(R);
    }

    /// <summary>
    /// This method handles the command. It just ensures that no other request exists with the same ID, and if this is the case
    /// just enqueues the original inner command.
    /// </summary>
    /// <param name="message">IdentifiedCommand which contains both original command & request ID</param>
    /// <returns>Return value of inner command or default value if request same ID was found</returns>
    public async Task<R> Handle(IdentifiedCommand<T, R> message, CancellationToken cancellationToken)
    {
        var alreadyExists = await _requestManager.ExistAsync(message.Id);
        if (alreadyExists)
        {
            return CreateResultForDuplicateRequest();
        }
        else
        {
            await _requestManager.CreateRequestForCommandAsync<T>(message.Id);
            try
            {
                var command = message.Command;
                var commandName = command.GetGenericTypeName();
                var idProperty = string.Empty;
                var commandId = string.Empty;

                switch (command)
                {
                    case CreateOrderCommand createOrderCommand:
                        idProperty = nameof(createOrderCommand.UserId);
                        commandId = createOrderCommand.UserId;
                        break;

                    case CancelOrderCommand cancelOrderCommand:
                        idProperty = nameof(cancelOrderCommand.OrderNumber);
                        commandId = $"{cancelOrderCommand.OrderNumber}";
                        break;

                    case ShipOrderCommand shipOrderCommand:
                        idProperty = nameof(shipOrderCommand.OrderNumber);
                        commandId = $"{shipOrderCommand.OrderNumber}";
                        break;

                    default:
                        idProperty = "Id?";
                        commandId = "n/a";
                        break;
                }

                _logger.LogInformation(
                    "----- Sending command: {CommandName} - {IdProperty}: {CommandId} ({@Command})",
                    commandName,
                    idProperty,
                    commandId,
                    command);

                // Send the embedded business command to mediator so it runs its related CommandHandler
                var result = await _mediator.Send(command, cancellationToken);

                _logger.LogInformation(
                    "----- Command result: {@Result} - {CommandName} - {IdProperty}: {CommandId} ({@Command})",
                    result,
                    commandName,
                    idProperty,
                    commandId,
                    command);

                return result;
            }
            catch
            {
                return default(R);
            }
        }
    }
}
```

<span data-ttu-id="70c9e-341">由於 Identifiedcommand 而的作用就像是商務命令的信封，因此當商務命令不是重複的識別碼時，需要處理商務命令，然後它會採用該內部商務命令，並將其重新提交至中繼程式，如同執行時從上方顯示的程式碼最後一個部分（ `_mediator.Send(message.Command)` 從 [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs)）。</span><span class="sxs-lookup"><span data-stu-id="70c9e-341">Since the IdentifiedCommand acts like a business command's envelope, when the business command needs to be processed because it is not a repeated ID, then it takes that inner business command and resubmits it to Mediator, as in the last part of the code shown above when running `_mediator.Send(message.Command)`, from the [IdentifiedCommandHandler.cs](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/IdentifiedCommandHandler.cs).</span></span>

<span data-ttu-id="70c9e-342">這麼做時，它會連結並執行商務命令處理常式，在此案例中， [會對排序](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs)資料庫執行交易，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="70c9e-342">When doing that, it will link and run the business command handler, in this case, the [CreateOrderCommandHandler](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Commands/CreateOrderCommandHandler.cs), which is running transactions against the Ordering database, as shown in the following code.</span></span>

```csharp
// CreateOrderCommandHandler.cs
public class CreateOrderCommandHandler
        : IRequestHandler<CreateOrderCommand, bool>
{
    private readonly IOrderRepository _orderRepository;
    private readonly IIdentityService _identityService;
    private readonly IMediator _mediator;
    private readonly IOrderingIntegrationEventService _orderingIntegrationEventService;
    private readonly ILogger<CreateOrderCommandHandler> _logger;

    // Using DI to inject infrastructure persistence Repositories
    public CreateOrderCommandHandler(IMediator mediator,
        IOrderingIntegrationEventService orderingIntegrationEventService,
        IOrderRepository orderRepository,
        IIdentityService identityService,
        ILogger<CreateOrderCommandHandler> logger)
    {
        _orderRepository = orderRepository ?? throw new ArgumentNullException(nameof(orderRepository));
        _identityService = identityService ?? throw new ArgumentNullException(nameof(identityService));
        _mediator = mediator ?? throw new ArgumentNullException(nameof(mediator));
        _orderingIntegrationEventService = orderingIntegrationEventService ?? throw new ArgumentNullException(nameof(orderingIntegrationEventService));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
    }

    public async Task<bool> Handle(CreateOrderCommand message, CancellationToken cancellationToken)
    {
        // Add Integration event to clean the basket
        var orderStartedIntegrationEvent = new OrderStartedIntegrationEvent(message.UserId);
        await _orderingIntegrationEventService.AddAndSaveEventAsync(orderStartedIntegrationEvent);

        // Add/Update the Buyer AggregateRoot
        // DDD patterns comment: Add child entities and value-objects through the Order Aggregate-Root
        // methods and constructor so validations, invariants and business logic
        // make sure that consistency is preserved across the whole aggregate
        var address = new Address(message.Street, message.City, message.State, message.Country, message.ZipCode);
        var order = new Order(message.UserId, message.UserName, address, message.CardTypeId, message.CardNumber, message.CardSecurityNumber, message.CardHolderName, message.CardExpiration);

        foreach (var item in message.OrderItems)
        {
            order.AddOrderItem(item.ProductId, item.ProductName, item.UnitPrice, item.Discount, item.PictureUrl, item.Units);
        }

        _logger.LogInformation("----- Creating Order - Order: {@Order}", order);

        _orderRepository.Add(order);

        return await _orderRepository.UnitOfWork
            .SaveEntitiesAsync(cancellationToken);
    }
}
```

### <a name="register-the-types-used-by-mediatr"></a><span data-ttu-id="70c9e-343">註冊 MediatR 所使用的類型</span><span class="sxs-lookup"><span data-stu-id="70c9e-343">Register the types used by MediatR</span></span>

<span data-ttu-id="70c9e-344">為了讓 MediatR 知道您的命令處理常式類別，您需要在 IoC 容器中註冊中繼程序類別和命令處理常式類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-344">In order for MediatR to be aware of your command handler classes, you need to register the mediator classes and the command handler classes in your IoC container.</span></span> <span data-ttu-id="70c9e-345">MediatR 預設會使用 Autofac 作為 IoC 容器，但您也可以使用內建 ASP.NET Core IoC 容器或 MediatR 所支援的任何其他容器。</span><span class="sxs-lookup"><span data-stu-id="70c9e-345">By default, MediatR uses Autofac as the IoC container, but you can also use the built-in ASP.NET Core IoC container or any other container supported by MediatR.</span></span>

<span data-ttu-id="70c9e-346">下列程式碼示範如何在使用 Autofac 模組時，註冊中繼程式的類型和命令。</span><span class="sxs-lookup"><span data-stu-id="70c9e-346">The following code shows how to register Mediator's types and commands when using Autofac modules.</span></span>

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterAssemblyTypes(typeof(IMediator).GetTypeInfo().Assembly)
            .AsImplementedInterfaces();

        // Register all the Command classes (they implement IRequestHandler)
        // in assembly holding the Commands
        builder.RegisterAssemblyTypes(typeof(CreateOrderCommand).GetTypeInfo().Assembly)
                .AsClosedTypesOf(typeof(IRequestHandler<,>));
        // Other types registration
        //...
    }
}
```

<span data-ttu-id="70c9e-347">這就是 MediatR 的「魔術」。</span><span class="sxs-lookup"><span data-stu-id="70c9e-347">This is where "the magic happens" with MediatR.</span></span>

<span data-ttu-id="70c9e-348">當每個命令處理常式都實作為泛型 `IRequestHandler<T>` 介面時，當您使用方法註冊元件時， `RegisteredAssemblyTypes` 所有標記為的 `IRequestHandler` 型別也會向其註冊 `Commands` 。</span><span class="sxs-lookup"><span data-stu-id="70c9e-348">As each command handler implements the generic `IRequestHandler<T>` interface, when you register the assemblies using `RegisteredAssemblyTypes` method all the types marked as `IRequestHandler` also gets registered with their `Commands`.</span></span> <span data-ttu-id="70c9e-349">例如：</span><span class="sxs-lookup"><span data-stu-id="70c9e-349">For   example:</span></span>

```csharp
public class CreateOrderCommandHandler
  : IRequestHandler<CreateOrderCommand, bool>
{
```

<span data-ttu-id="70c9e-350">這是建立命令與命令處理常式之關聯的程式碼。</span><span class="sxs-lookup"><span data-stu-id="70c9e-350">That is the code that correlates commands with command handlers.</span></span> <span data-ttu-id="70c9e-351">處理常式只是簡單類別，但它繼承自 `RequestHandler<T>`，其中 T 為命令類型，而且 MediatR 確定它是使用正確承載 (命令) 所叫用。</span><span class="sxs-lookup"><span data-stu-id="70c9e-351">The handler is just a simple class, but it inherits from `RequestHandler<T>`, where T is the command type, and MediatR makes sure it is invoked with the correct payload (the command).</span></span>

## <a name="apply-cross-cutting-concerns-when-processing-commands-with-the-behaviors-in-mediatr"></a><span data-ttu-id="70c9e-352">使用 MediatR 中的行為處理命令時會套用跨領域關注</span><span class="sxs-lookup"><span data-stu-id="70c9e-352">Apply cross-cutting concerns when processing commands with the Behaviors in MediatR</span></span>

<span data-ttu-id="70c9e-353">還有一件事：可以將跨領域關注套用至中繼程序管道。</span><span class="sxs-lookup"><span data-stu-id="70c9e-353">There is one more thing: being able to apply cross-cutting concerns to the mediator pipeline.</span></span> <span data-ttu-id="70c9e-354">您也可以查看 Autofac 註冊模組程式碼結尾，了解如何註冊行為類型，特別是自訂 LoggingBehavior 類別和 ValidatorBehavior 類別。</span><span class="sxs-lookup"><span data-stu-id="70c9e-354">You can also see at the end of the Autofac registration module code how it registers a behavior type, specifically, a custom LoggingBehavior class and a ValidatorBehavior class.</span></span> <span data-ttu-id="70c9e-355">但是，您也可以新增其他自訂行為。</span><span class="sxs-lookup"><span data-stu-id="70c9e-355">But you could add other custom behaviors, too.</span></span>

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        builder.RegisterAssemblyTypes(typeof(IMediator).GetTypeInfo().Assembly)
            .AsImplementedInterfaces();

        // Register all the Command classes (they implement IRequestHandler)
        // in assembly holding the Commands
        builder.RegisterAssemblyTypes(
                              typeof(CreateOrderCommand).GetTypeInfo().Assembly).
                                   AsClosedTypesOf(typeof(IRequestHandler<,>));
        // Other types registration
        //...
        builder.RegisterGeneric(typeof(LoggingBehavior<,>)).
                                                   As(typeof(IPipelineBehavior<,>));
        builder.RegisterGeneric(typeof(ValidatorBehavior<,>)).
                                                   As(typeof(IPipelineBehavior<,>));
    }
}
```

<span data-ttu-id="70c9e-356">該 [LoggingBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) 類別可以實作為下列程式碼，以記錄所執行命令處理常式的相關資訊以及是否成功。</span><span class="sxs-lookup"><span data-stu-id="70c9e-356">That [LoggingBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/LoggingBehavior.cs) class can be implemented as the following code, which logs information about the command handler being executed and whether it was successful or not.</span></span>

```csharp
public class LoggingBehavior<TRequest, TResponse>
         : IPipelineBehavior<TRequest, TResponse>
{
    private readonly ILogger<LoggingBehavior<TRequest, TResponse>> _logger;
    public LoggingBehavior(ILogger<LoggingBehavior<TRequest, TResponse>> logger) =>
                                                                  _logger = logger;

    public async Task<TResponse> Handle(TRequest request,
                                        RequestHandlerDelegate<TResponse> next)
    {
        _logger.LogInformation($"Handling {typeof(TRequest).Name}");
        var response = await next();
        _logger.LogInformation($"Handled {typeof(TResponse).Name}");
        return response;
    }
}
```

<span data-ttu-id="70c9e-357">只要實作此行為類別，以及在管線 (上文的 MediatorModule) 中登錄它，透過 MediatR 處理的所有命令都會記錄執行相關資訊。</span><span class="sxs-lookup"><span data-stu-id="70c9e-357">Just by implementing this behavior class and by registering it in the pipeline (in the MediatorModule above), all the commands processed through MediatR will be logging information about the execution.</span></span>

<span data-ttu-id="70c9e-358">eShopOnContainers 訂購微服務也會套用第二個行為來進行基本驗證，即依賴 [FluentValidation](https://github.com/JeremySkinner/FluentValidation) 程式庫的 [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) 類別，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="70c9e-358">The eShopOnContainers ordering microservice also applies a second behavior for basic validations, the [ValidatorBehavior](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/Behaviors/ValidatorBehavior.cs) class that relies on the [FluentValidation](https://github.com/JeremySkinner/FluentValidation) library, as shown in the following code:</span></span>

```csharp
public class ValidatorBehavior<TRequest, TResponse>
         : IPipelineBehavior<TRequest, TResponse>
{
    private readonly IValidator<TRequest>[] _validators;
    public ValidatorBehavior(IValidator<TRequest>[] validators) =>
                                                         _validators = validators;

    public async Task<TResponse> Handle(TRequest request,
                                        RequestHandlerDelegate<TResponse> next)
    {
        var failures = _validators
            .Select(v => v.Validate(request))
            .SelectMany(result => result.Errors)
            .Where(error => error != null)
            .ToList();

        if (failures.Any())
        {
            throw new OrderingDomainException(
                $"Command Validation Errors for type {typeof(TRequest).Name}",
                        new ValidationException("Validation exception", failures));
        }

        var response = await next();
        return response;
    }
}
```

<span data-ttu-id="70c9e-359">在此行為會在驗證失敗時引發例外狀況，但您也可以傳回結果物件，其中包含命令結果（如果成功的話）或驗證訊息（如果沒有的話）。</span><span class="sxs-lookup"><span data-stu-id="70c9e-359">Here the behavior is raising an exception if validation fails, but you could also return a result object, containing the command result if it succeeded or the validation messages in case it didn't.</span></span> <span data-ttu-id="70c9e-360">這樣可能更容易向使用者顯示驗證結果。</span><span class="sxs-lookup"><span data-stu-id="70c9e-360">This would probably make it easier to display validation results to the user.</span></span>

<span data-ttu-id="70c9e-361">然後，根據 [FluentValidation](https://github.com/JeremySkinner/FluentValidation) 程式庫，您會針對以 CreateOrderCommand 傳遞的資料建立驗證，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="70c9e-361">Then, based on the [FluentValidation](https://github.com/JeremySkinner/FluentValidation) library, you would create validation for the data passed with CreateOrderCommand, as in the following code:</span></span>

```csharp
public class CreateOrderCommandValidator : AbstractValidator<CreateOrderCommand>
{
    public CreateOrderCommandValidator()
    {
        RuleFor(command => command.City).NotEmpty();
        RuleFor(command => command.Street).NotEmpty();
        RuleFor(command => command.State).NotEmpty();
        RuleFor(command => command.Country).NotEmpty();
        RuleFor(command => command.ZipCode).NotEmpty();
        RuleFor(command => command.CardNumber).NotEmpty().Length(12, 19);
        RuleFor(command => command.CardHolderName).NotEmpty();
        RuleFor(command => command.CardExpiration).NotEmpty().Must(BeValidExpirationDate).WithMessage("Please specify a valid card expiration date");
        RuleFor(command => command.CardSecurityNumber).NotEmpty().Length(3);
        RuleFor(command => command.CardTypeId).NotEmpty();
        RuleFor(command => command.OrderItems).Must(ContainOrderItems).WithMessage("No order items found");
    }

    private bool BeValidExpirationDate(DateTime dateTime)
    {
        return dateTime >= DateTime.UtcNow;
    }

    private bool ContainOrderItems(IEnumerable<OrderItemDTO> orderItems)
    {
        return orderItems.Any();
    }
}

```

<span data-ttu-id="70c9e-362">您可以建立額外驗證。</span><span class="sxs-lookup"><span data-stu-id="70c9e-362">You could create additional validations.</span></span> <span data-ttu-id="70c9e-363">這是實作命令驗證的全新且更簡潔的方式。</span><span class="sxs-lookup"><span data-stu-id="70c9e-363">This is a very clean and elegant way to implement your command validations.</span></span>

<span data-ttu-id="70c9e-364">使用類似的方式，您可以實作想要在處理命令時套用至命令之其他層面或跨領域關注的其他行為。</span><span class="sxs-lookup"><span data-stu-id="70c9e-364">In a similar way, you could implement other behaviors for additional aspects or cross-cutting concerns that you want to apply to commands when handling them.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="70c9e-365">其他資源</span><span class="sxs-lookup"><span data-stu-id="70c9e-365">Additional resources</span></span>

##### <a name="the-mediator-pattern"></a><span data-ttu-id="70c9e-366">中繼程序模式</span><span class="sxs-lookup"><span data-stu-id="70c9e-366">The mediator pattern</span></span>

- <span data-ttu-id="70c9e-367">**中繼程式模式** </span><span class="sxs-lookup"><span data-stu-id="70c9e-367">**Mediator pattern** </span></span>\
  [https://en.wikipedia.org/wiki/Mediator\_pattern](https://en.wikipedia.org/wiki/Mediator_pattern)

##### <a name="the-decorator-pattern"></a><span data-ttu-id="70c9e-368">裝飾項目模式</span><span class="sxs-lookup"><span data-stu-id="70c9e-368">The decorator pattern</span></span>

- <span data-ttu-id="70c9e-369">**裝飾專案模式** </span><span class="sxs-lookup"><span data-stu-id="70c9e-369">**Decorator pattern** </span></span>\
  [https://en.wikipedia.org/wiki/Decorator\_pattern](https://en.wikipedia.org/wiki/Decorator_pattern)

##### <a name="mediatr-jimmy-bogard"></a><span data-ttu-id="70c9e-370">MediatR (Jimmy Bogard)</span><span class="sxs-lookup"><span data-stu-id="70c9e-370">MediatR (Jimmy Bogard)</span></span>

- <span data-ttu-id="70c9e-371">**MediatR.**</span><span class="sxs-lookup"><span data-stu-id="70c9e-371">**MediatR.**</span></span> <span data-ttu-id="70c9e-372">GitHub 存放庫。</span><span class="sxs-lookup"><span data-stu-id="70c9e-372">GitHub repo.</span></span> \
  <https://github.com/jbogard/MediatR>

- <span data-ttu-id="70c9e-373">**CQRS 搭配 MediatR 和 AutoMapper** </span><span class="sxs-lookup"><span data-stu-id="70c9e-373">**CQRS with MediatR and AutoMapper** </span></span>\
  <https://lostechies.com/jimmybogard/2015/05/05/cqrs-with-mediatr-and-automapper/>

- <span data-ttu-id="70c9e-374">**讓您的控制項瘦身：POST 和命令。**</span><span class="sxs-lookup"><span data-stu-id="70c9e-374">**Put your controllers on a diet: POSTs and commands.**</span></span> \
  <https://lostechies.com/jimmybogard/2013/12/19/put-your-controllers-on-a-diet-posts-and-commands/>

- <span data-ttu-id="70c9e-375">**使用中繼程式管線處理跨領域關注** </span><span class="sxs-lookup"><span data-stu-id="70c9e-375">**Tackling cross-cutting concerns with a mediator pipeline** </span></span>\
  <https://lostechies.com/jimmybogard/2014/09/09/tackling-cross-cutting-concerns-with-a-mediator-pipeline/>

- <span data-ttu-id="70c9e-376">**CQRS 和 REST：完美相符** </span><span class="sxs-lookup"><span data-stu-id="70c9e-376">**CQRS and REST: the perfect match** </span></span>\
  <https://lostechies.com/jimmybogard/2016/06/01/cqrs-and-rest-the-perfect-match/>

- <span data-ttu-id="70c9e-377">**MediatR 管線範例** </span><span class="sxs-lookup"><span data-stu-id="70c9e-377">**MediatR Pipeline Examples** </span></span>\
  <https://lostechies.com/jimmybogard/2016/10/13/mediatr-pipeline-examples/>

- <span data-ttu-id="70c9e-378">**MediatR 和 ASP.NET Core 的垂直配量測試裝置** </span><span class="sxs-lookup"><span data-stu-id="70c9e-378">**Vertical Slice Test Fixtures for MediatR and ASP.NET Core** </span></span>\
  <https://lostechies.com/jimmybogard/2016/10/24/vertical-slice-test-fixtures-for-mediatr-and-asp-net-core/>

- <span data-ttu-id="70c9e-379">**已發行適用于 Microsoft 相依性插入的 MediatR 延伸模組** </span><span class="sxs-lookup"><span data-stu-id="70c9e-379">**MediatR Extensions for Microsoft Dependency Injection Released** </span></span>\
  <https://lostechies.com/jimmybogard/2016/07/19/mediatr-extensions-for-microsoft-dependency-injection-released/>

##### <a name="fluent-validation"></a><span data-ttu-id="70c9e-380">Fluent 驗證</span><span class="sxs-lookup"><span data-stu-id="70c9e-380">Fluent validation</span></span>

- <span data-ttu-id="70c9e-381">**Jeremy Skinner。FluentValidation.**</span><span class="sxs-lookup"><span data-stu-id="70c9e-381">**Jeremy Skinner. FluentValidation.**</span></span> <span data-ttu-id="70c9e-382">GitHub 存放庫。</span><span class="sxs-lookup"><span data-stu-id="70c9e-382">GitHub repo.</span></span> \
  <https://github.com/JeremySkinner/FluentValidation>

> [!div class="step-by-step"]
> <span data-ttu-id="70c9e-383">[上一個](microservice-application-layer-web-api-design.md) 
> [下一步](../implement-resilient-applications/index.md)</span><span class="sxs-lookup"><span data-stu-id="70c9e-383">[Previous](microservice-application-layer-web-api-design.md)
[Next](../implement-resilient-applications/index.md)</span></span>
