---
title: 利用 DDD 和 CQRS 模式解決微服務中的商務複雜度
description: 容器化 .NET 應用程式的 .NET 微服務架構 | 了解如何利用 DDD 與 CQRS 模式解決複雜的商業案例
ms.date: 10/08/2018
ms.openlocfilehash: 852073548a66fbe568fc5c2531342db944d5a8b0
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144639"
---
# <a name="tackle-business-complexity-in-a-microservice-with-ddd-and-cqrs-patterns"></a><span data-ttu-id="67332-103">使用 DDD 與 CQRS 模式解決微服務中的商務複雜度</span><span class="sxs-lookup"><span data-stu-id="67332-103">Tackle Business Complexity in a Microservice with DDD and CQRS Patterns</span></span>

<span data-ttu-id="67332-104">設計每個微服務的領域模型，或反映對業務領域了解程度的繫結內容。\*\*</span><span class="sxs-lookup"><span data-stu-id="67332-104">*Design a domain model for each microservice or Bounded Context that reflects understanding of the business domain.*</span></span>

<span data-ttu-id="67332-105">本節著重於當您需要解決複雜的子系統時所實作的更進階微服務，或是衍生自領域專家對不斷改變之商務規則知識的微服務。</span><span class="sxs-lookup"><span data-stu-id="67332-105">This section focuses on more advanced microservices that you implement when you need to tackle complex subsystems, or microservices derived from the knowledge of domain experts with ever-changing business rules.</span></span> <span data-ttu-id="67332-106">此節中所使用的架構模式是以領域驅動設計 (Domain-Driven Design，DDD) 以及命令和查詢職責分離 (Command and Query Responsibility Segregation，CQRS) 方法為基礎，如圖 7-1 所示。</span><span class="sxs-lookup"><span data-stu-id="67332-106">The architecture patterns used in this section are based on domain-driven design (DDD) and Command and Query Responsibility Segregation (CQRS) approaches, as illustrated in Figure 7-1.</span></span>

:::image type="complex" source="./media/index/internal-versus-external-architecture.png" alt-text="比較外部和內部架構模式的圖表。":::
<span data-ttu-id="67332-108">外部架構的差異：微服務模式、API 閘道、彈性通訊、pub/sub 等：內部架構：資料 動/CRUD、DDD 模式、相依性插入、多程式庫等。</span><span class="sxs-lookup"><span data-stu-id="67332-108">Difference between external architecture: microservice patterns, API gateways, resilient communications, pub/sub, etc., and internal architecture: data driven/CRUD, DDD patterns, dependency injection, multiple libraries, etc.</span></span>
:::image-end:::

<span data-ttu-id="67332-109">**圖 7-1**.</span><span class="sxs-lookup"><span data-stu-id="67332-109">**Figure 7-1**.</span></span> <span data-ttu-id="67332-110">外部微服務架構與每個微服務的內部架構模式</span><span class="sxs-lookup"><span data-stu-id="67332-110">External microservice architecture versus internal architecture patterns for each microservice</span></span>

<span data-ttu-id="67332-111">不過，資料驅動微服務的大多數技術，像是如何實作 ASP.NET Core Web API 服務，或如何使用 Swashbuckle 或 NSwag 公開 Swagger 中繼資料，也適用於以 DDD 模式在內部實作之更進階的微服務。</span><span class="sxs-lookup"><span data-stu-id="67332-111">However, most of the techniques for data driven microservices, such as how to implement an ASP.NET Core Web API service or how to expose Swagger metadata with Swashbuckle or NSwag, are also applicable to the more advanced microservices implemented internally with DDD patterns.</span></span> <span data-ttu-id="67332-112">本節是前面幾節的延伸，因為稍早所述的大部分實務也適用於這裡或任何類型的微服務。</span><span class="sxs-lookup"><span data-stu-id="67332-112">This section is an extension of the previous sections, because most of the practices explained earlier also apply here or for any kind of microservice.</span></span>

<span data-ttu-id="67332-113">本節會先提供 eShopOnContainers 參考應用程式中所使用之簡化 CQRS 模式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="67332-113">This section first provides details on the simplified CQRS patterns used in the eShopOnContainers reference application.</span></span> <span data-ttu-id="67332-114">稍後會對您概要說明 DDD 技術，這些技術可讓您尋找常見的模式，以便在應用程式中重複使用。</span><span class="sxs-lookup"><span data-stu-id="67332-114">Later, you will get an overview of the DDD techniques that enable you to find common patterns that you can reuse in your applications.</span></span>

<span data-ttu-id="67332-115">DDD 是一個龐大的主題，內含一組豐富的學習資源。</span><span class="sxs-lookup"><span data-stu-id="67332-115">DDD is a large topic with a rich set of resources for learning.</span></span> <span data-ttu-id="67332-116">您可以從 Eric Evans 所著 [Domain-Driven Design](https://domainlanguage.com/ddd/) 之類的書籍，以及 Vaughn Vernon、Jimmy Nilsson、Greg Young、Udi Dahan、Jimmy Bogard 和許多其他 DDD/CQRS 專家所提供的其他教材開始著手。</span><span class="sxs-lookup"><span data-stu-id="67332-116">You can start with books like [Domain-Driven Design](https://domainlanguage.com/ddd/) by Eric Evans and additional materials from Vaughn Vernon, Jimmy Nilsson, Greg Young, Udi Dahan, Jimmy Bogard, and many other DDD/CQRS experts.</span></span> <span data-ttu-id="67332-117">但最重要的是，您需要試著了解如何在專家協助下，將來自交談、白板與領域模型課程的 DDD 技術，應用在您的實體業務領域中。</span><span class="sxs-lookup"><span data-stu-id="67332-117">But most of all you need to try to learn how to apply DDD techniques from the conversations, whiteboarding, and domain modeling sessions with the experts in your concrete business domain.</span></span>

#### <a name="additional-resources"></a><span data-ttu-id="67332-118">其他資源</span><span class="sxs-lookup"><span data-stu-id="67332-118">Additional resources</span></span>

##### <a name="ddd-domain-driven-design"></a><span data-ttu-id="67332-119">DDD (領域驅動設計)</span><span class="sxs-lookup"><span data-stu-id="67332-119">DDD (Domain-Driven Design)</span></span>

- <span data-ttu-id="67332-120">**Eric Evans。網域語言** </span><span class="sxs-lookup"><span data-stu-id="67332-120">**Eric Evans. Domain Language** </span></span>\
  <https://domainlanguage.com/>

- <span data-ttu-id="67332-121">**聖馬丁 Fowler。領域驅動設計** </span><span class="sxs-lookup"><span data-stu-id="67332-121">**Martin Fowler. Domain-Driven Design** </span></span>\
  <https://martinfowler.com/tags/domain%20driven%20design.html>

- <span data-ttu-id="67332-122">**Jimmy Bogard。加強您的領域：入門** </span><span class="sxs-lookup"><span data-stu-id="67332-122">**Jimmy Bogard. Strengthening your domain: a primer** </span></span>\
  <https://lostechies.com/jimmybogard/2010/02/04/strengthening-your-domain-a-primer/>

##### <a name="ddd-books"></a><span data-ttu-id="67332-123">DDD 書籍</span><span class="sxs-lookup"><span data-stu-id="67332-123">DDD books</span></span>

- <span data-ttu-id="67332-124">**Eric Evans。領域驅動設計：處理軟體核心的複雜性** </span><span class="sxs-lookup"><span data-stu-id="67332-124">**Eric Evans. Domain-Driven Design: Tackling Complexity in the Heart of Software** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

- <span data-ttu-id="67332-125">**Eric Evans。領域驅動設計參考：定義與模式摘要** </span><span class="sxs-lookup"><span data-stu-id="67332-125">**Eric Evans. Domain-Driven Design Reference: Definitions and Pattern Summaries** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Reference-Definitions-2014-09-22/dp/B01N8YB4ZO/>

- <span data-ttu-id="67332-126">**Vaughn Vernon。執行領域驅動設計** </span><span class="sxs-lookup"><span data-stu-id="67332-126">**Vaughn Vernon. Implementing Domain-Driven Design** </span></span>\
  <https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/>

- <span data-ttu-id="67332-127">**Vaughn Vernon。領域驅動設計已提煉** </span><span class="sxs-lookup"><span data-stu-id="67332-127">**Vaughn Vernon. Domain-Driven Design Distilled** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/>

- <span data-ttu-id="67332-128">**Jimmy Nilsson。套用領域驅動設計和模式** </span><span class="sxs-lookup"><span data-stu-id="67332-128">**Jimmy Nilsson. Applying Domain-Driven Design and Patterns** </span></span>\
  <https://www.amazon.com/Applying-Domain-Driven-Design-Patterns-Examples/dp/0321268202/>

- <span data-ttu-id="67332-129">**Cesar de la Torre。使用 .NET 的 N 層式網域導向架構指南** </span><span class="sxs-lookup"><span data-stu-id="67332-129">**Cesar de la Torre. N-Layered Domain-Oriented Architecture Guide with .NET** </span></span>\
  <https://www.amazon.com/N-Layered-Domain-Oriented-Architecture-Guide-NET/dp/8493903612/>

- <span data-ttu-id="67332-130">**Abel Avram 和 Floyd Marinescu。網域驅動設計快速** </span><span class="sxs-lookup"><span data-stu-id="67332-130">**Abel Avram and Floyd Marinescu. Domain-Driven Design Quickly** </span></span>\
  <https://www.amazon.com/Domain-Driven-Design-Quickly-Abel-Avram/dp/1411609255/>

- <span data-ttu-id="67332-131">**Scott Millett，Nick 領域驅動設計的微調模式、原則和作法** </span><span class="sxs-lookup"><span data-stu-id="67332-131">**Scott Millett, Nick Tune - Patterns, Principles, and Practices of Domain-Driven Design** </span></span>\
  <https://www.wiley.com/Patterns%2C+Principles%2C+and+Practices+of+Domain+Driven+Design-p-9781118714706>

##### <a name="ddd-training"></a><span data-ttu-id="67332-132">DDD 訓練課程</span><span class="sxs-lookup"><span data-stu-id="67332-132">DDD training</span></span>

- <span data-ttu-id="67332-133">**Julie Lerman 和 Steve Smith。領域驅動設計基本概念** </span><span class="sxs-lookup"><span data-stu-id="67332-133">**Julie Lerman and Steve Smith. Domain-Driven Design Fundamentals** </span></span>\
  <https://bit.ly/PS-DDD>

>[!div class="step-by-step"]
><span data-ttu-id="67332-134">[上一個](../multi-container-microservice-net-applications/implement-api-gateways-with-ocelot.md) 
>[下一步](apply-simplified-microservice-cqrs-ddd-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="67332-134">[Previous](../multi-container-microservice-net-applications/implement-api-gateways-with-ocelot.md)
[Next](apply-simplified-microservice-cqrs-ddd-patterns.md)</span></span>
