---
title: 領域事件： 設計和實作
description: .NET 微服務：容器化 .NET 應用程式的架構 | 深入了解領域事件，這是用來在彙總之間建立通訊的重要概念。
ms.date: 10/08/2018
ms.openlocfilehash: 651d9cb98444c0729b97f523cc3d688f0f8d51d5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173363"
---
# <a name="domain-events-design-and-implementation"></a><span data-ttu-id="fdd56-104">領域事件：設計和實作</span><span class="sxs-lookup"><span data-stu-id="fdd56-104">Domain events: design and implementation</span></span>

<span data-ttu-id="fdd56-105">使用領域事件可明確實作您領域中變更的副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-105">Use domain events to explicitly implement side effects of changes within your domain.</span></span> <span data-ttu-id="fdd56-106">換句話說 (以 DDD 術語來說)，使用領域事件可在多個彙總之間明確實作副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-106">In other words, and using DDD terminology, use domain events to explicitly implement side effects across multiple aggregates.</span></span> <span data-ttu-id="fdd56-107">為了提高延展性並降低資料庫鎖定的影響，您可以選擇在相同領域中的多個彙總之間使用最終一致性。</span><span class="sxs-lookup"><span data-stu-id="fdd56-107">Optionally, for better scalability and less impact in database locks, use eventual consistency between aggregates within the same domain.</span></span>

## <a name="what-is-a-domain-event"></a><span data-ttu-id="fdd56-108">什麼是領域事件？</span><span class="sxs-lookup"><span data-stu-id="fdd56-108">What is a domain event?</span></span>

<span data-ttu-id="fdd56-109">事件是指過去發生的某件事。</span><span class="sxs-lookup"><span data-stu-id="fdd56-109">An event is something that has happened in the past.</span></span> <span data-ttu-id="fdd56-110">領域事件是領域中發生的某件事，您想要相同領域 (同處理序) 的其他組件獲知該事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-110">A domain event is, something that happened in the domain that you want other parts of the same domain (in-process) to be aware of.</span></span> <span data-ttu-id="fdd56-111">獲通知的組件通常會以某種方式對事件做出回應。</span><span class="sxs-lookup"><span data-stu-id="fdd56-111">The notified parts usually react somehow to the events.</span></span>

<span data-ttu-id="fdd56-112">領域事件的重要優點是可以明確表示副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-112">An important benefit of domain events is that side effects can be expressed explicitly.</span></span>

<span data-ttu-id="fdd56-113">例如，如果您只使用 Entity Framework，而且必須對某些事件做出反應，則您可能會撰寫需要與觸發事件內容接近的任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="fdd56-113">For example, if you're just using Entity Framework and there has to be a reaction to some event, you would probably code whatever you need close to what triggers the event.</span></span> <span data-ttu-id="fdd56-114">因此，規則會以隱含方式與程式碼結合，您必須查看程式碼，以便了解在該處實作的規則。</span><span class="sxs-lookup"><span data-stu-id="fdd56-114">So the rule gets coupled, implicitly, to the code, and you have to look into the code to, hopefully, realize the rule is implemented there.</span></span>

<span data-ttu-id="fdd56-115">另一方面，使用領域事件明確呈現概念，因為其中涉及到 `DomainEvent` 以及至少一個 `DomainEventHandler`。</span><span class="sxs-lookup"><span data-stu-id="fdd56-115">On the other hand, using domain events makes the concept explicit, because there is a `DomainEvent` and at least one `DomainEventHandler` involved.</span></span>

<span data-ttu-id="fdd56-116">例如，在 eShopOnContainers 應用程式中建立訂單時，使用者會變成購買者，因此會引發 `OrderStartedDomainEvent` 並在 `ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler` 中進行處理，如此基礎概念就顯而易見。</span><span class="sxs-lookup"><span data-stu-id="fdd56-116">For example, in the eShopOnContainers application, when an order is created, the user becomes a buyer, so an `OrderStartedDomainEvent` is raised and handled in the `ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler`, so the underlying concept is evident.</span></span>

<span data-ttu-id="fdd56-117">簡單地說，領域事件可協助您明確表示由領域專家所提供並以通用語言為基礎的領域規則。</span><span class="sxs-lookup"><span data-stu-id="fdd56-117">In short, domain events help you to express, explicitly, the domain rules, based in the ubiquitous language provided by the domain experts.</span></span> <span data-ttu-id="fdd56-118">領域事件也可以改善相同領域中類別之間的關注點分離。</span><span class="sxs-lookup"><span data-stu-id="fdd56-118">Domain events also enable a better separation of concerns among classes within the same domain.</span></span>

<span data-ttu-id="fdd56-119">就像資料庫交易一樣，請務必確保與領域事件相關的所有作業都成功完成或全都未完成。</span><span class="sxs-lookup"><span data-stu-id="fdd56-119">It's important to ensure that, just like a database transaction, either all the operations related to a domain event finish successfully or none of them do.</span></span>

<span data-ttu-id="fdd56-120">領域事件類似傳訊樣式事件，但有一個重要的差異。</span><span class="sxs-lookup"><span data-stu-id="fdd56-120">Domain events are similar to messaging-style events, with one important difference.</span></span> <span data-ttu-id="fdd56-121">透過即時傳訊、訊息佇列、訊息代理程式或使用 AMQP 的服務匯流排，訊息一律會以非同步方式傳送，並跨處理序與電腦通訊。</span><span class="sxs-lookup"><span data-stu-id="fdd56-121">With real messaging, message queuing, message brokers, or a service bus using AMQP, a message is always sent asynchronously and communicated across processes and machines.</span></span> <span data-ttu-id="fdd56-122">這有助於整合多個限定內容、微服務或甚至是不同的應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-122">This is useful for integrating multiple Bounded Contexts, microservices, or even different applications.</span></span> <span data-ttu-id="fdd56-123">不過，使用領域事件時，您不只希望從目前正在執行的領域作業引發事件，也希望所有副作用都會出現在相同的領域中。</span><span class="sxs-lookup"><span data-stu-id="fdd56-123">However, with domain events, you want to raise an event from the domain operation you are currently running, but you want any side effects to occur within the same domain.</span></span>

<span data-ttu-id="fdd56-124">領域事件及其副作用 (之後會觸發並由事件處理常式管理的動作) 應該幾乎會在相同領域 (通常是同處理序) 中立即發生。</span><span class="sxs-lookup"><span data-stu-id="fdd56-124">The domain events and their side effects (the actions triggered afterwards that are managed by event handlers) should occur almost immediately, usually in-process, and within the same domain.</span></span> <span data-ttu-id="fdd56-125">因此，領域事件可以為同步或非同步。</span><span class="sxs-lookup"><span data-stu-id="fdd56-125">Thus, domain events could be synchronous or asynchronous.</span></span> <span data-ttu-id="fdd56-126">不過，整合事件應該一律為非同步。</span><span class="sxs-lookup"><span data-stu-id="fdd56-126">Integration events, however, should always be asynchronous.</span></span>

## <a name="domain-events-versus-integration-events"></a><span data-ttu-id="fdd56-127">領域事件與整合事件的比較</span><span class="sxs-lookup"><span data-stu-id="fdd56-127">Domain events versus integration events</span></span>

<span data-ttu-id="fdd56-128">語意上來說，領域事件與整合事件同義，兩者都會通知剛發生的某件事。</span><span class="sxs-lookup"><span data-stu-id="fdd56-128">Semantically, domain and integration events are the same thing: notifications about something that just happened.</span></span> <span data-ttu-id="fdd56-129">不過，其實作必須不同。</span><span class="sxs-lookup"><span data-stu-id="fdd56-129">However, their implementation must be different.</span></span> <span data-ttu-id="fdd56-130">領域事件是推送至領域事件發送器的訊息，可實作為以 IoC 容器或任何其他方法為基礎的記憶體內部中繼程序。</span><span class="sxs-lookup"><span data-stu-id="fdd56-130">Domain events are just messages pushed to a domain event dispatcher, which could be implemented as an in-memory mediator based on an IoC container or any other method.</span></span>

<span data-ttu-id="fdd56-131">另一方面，整合事件的目的是將已認可的交易和更新傳播至其他子系統，不論是其他微服務、限定內容或甚至是外部應用程式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-131">On the other hand, the purpose of integration events is to propagate committed transactions and updates to additional subsystems, whether they are other microservices, Bounded Contexts or even external applications.</span></span> <span data-ttu-id="fdd56-132">因此，它們應該只有在成功保存實體時才會出現，否則就像整個作業從未發生過一樣。</span><span class="sxs-lookup"><span data-stu-id="fdd56-132">Hence, they should occur only if the entity is successfully persisted, otherwise it's as if the entire operation never happened.</span></span>

<span data-ttu-id="fdd56-133">如前所述，整合事件必須以多個微服務 (其他限定內容) 或甚至是外部系統/應用程式之間的非同步通訊為基礎。</span><span class="sxs-lookup"><span data-stu-id="fdd56-133">As mentioned before, integration events must be based on asynchronous communication between multiple microservices (other Bounded Contexts) or even external systems/applications.</span></span>

<span data-ttu-id="fdd56-134">因此，事件匯流排介面需要可在潛在遠端服務之間進行處理序間和分散式通訊的一些基礎結構。</span><span class="sxs-lookup"><span data-stu-id="fdd56-134">Thus, the event bus interface needs some infrastructure that allows inter-process and distributed communication between potentially remote services.</span></span> <span data-ttu-id="fdd56-135">它可以依據商業服務匯流排、佇列、用作信箱的共用資料庫，或任何其他分散式且最好為發送型傳訊系統。</span><span class="sxs-lookup"><span data-stu-id="fdd56-135">It can be based on a commercial service bus, queues, a shared database used as a mailbox, or any other distributed and ideally push based messaging system.</span></span>

## <a name="domain-events-as-a-preferred-way-to-trigger-side-effects-across-multiple-aggregates-within-the-same-domain"></a><span data-ttu-id="fdd56-136">領域事件是在相同領域中的多個彙總之間觸發副作用的慣用方法</span><span class="sxs-lookup"><span data-stu-id="fdd56-136">Domain events as a preferred way to trigger side effects across multiple aggregates within the same domain</span></span>

<span data-ttu-id="fdd56-137">如果執行與一個彙總執行個體相關的命令需要在一或多個額外的彙總上執行其他領域規則，您應該設計並實作領域事件所要觸發的這些副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-137">If executing a command related to one aggregate instance requires additional domain rules to be run on one or more additional aggregates, you should design and implement those side effects to be triggered by domain events.</span></span> <span data-ttu-id="fdd56-138">如圖 7-14 所示 (這是其中一個最重要的使用案例)，您應該使用領域事件，在相同領域模型中的多個彙總之間傳播狀態變更。</span><span class="sxs-lookup"><span data-stu-id="fdd56-138">As shown in Figure 7-14, and as one of the most important use cases, a domain event should be used to propagate state changes across multiple aggregates within the same domain model.</span></span>

![此圖顯示控制買方匯總資料的領域事件。](./media/domain-events-design-implementation/domain-model-ordering-microservice.png)

<span data-ttu-id="fdd56-140">**圖 7-14**。</span><span class="sxs-lookup"><span data-stu-id="fdd56-140">**Figure 7-14**.</span></span> <span data-ttu-id="fdd56-141">要在相同領域中的多個彙總之間強制執行一致性的領域事件</span><span class="sxs-lookup"><span data-stu-id="fdd56-141">Domain events to enforce consistency between multiple aggregates within the same domain</span></span>

<span data-ttu-id="fdd56-142">圖7-14 顯示領域事件如何達到匯總之間的一致性。</span><span class="sxs-lookup"><span data-stu-id="fdd56-142">Figure 7-14 shows how consistency between aggregates is achieved by domain events.</span></span> <span data-ttu-id="fdd56-143">當使用者起始訂單時，訂單匯總會傳送 `OrderStarted` 領域事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-143">When the user initiates an order, the Order Aggregate sends an `OrderStarted` domain event.</span></span> <span data-ttu-id="fdd56-144">買方匯總會處理 OrderStarted 領域事件，以根據身分識別微服務 (中的原始使用者資訊與 CreateOrder 命令) 中提供的資訊，在訂購微服務中建立買方物件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-144">The OrderStarted domain event is handled by the Buyer Aggregate to create a Buyer object in the ordering microservice, based on the original user info from the identity microservice (with information provided in the CreateOrder command).</span></span>

<span data-ttu-id="fdd56-145">或者，您可以讓彙總根訂閱其彙總成員 (子實體) 所引發的事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-145">Alternately, you can have the aggregate root subscribed for events raised by members of its aggregates (child entities).</span></span> <span data-ttu-id="fdd56-146">例如，當項目價格高於特定金額或產品項目金額太高時，每個 OrderItem 子實體都會引發一個事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-146">For instance, each OrderItem child entity can raise an event when the item price is higher than a specific amount, or when the product item amount is too high.</span></span> <span data-ttu-id="fdd56-147">然後，彙總根可接收這些事件，並執行全域計算或彙總。</span><span class="sxs-lookup"><span data-stu-id="fdd56-147">The aggregate root can then receive those events and perform a global calculation or aggregation.</span></span>

<span data-ttu-id="fdd56-148">請務必了解，此事件架構通訊不會直接在彙總內實作；您必須實作領域事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-148">It is important to understand that this event-based communication is not implemented directly within the aggregates; you need to implement domain event handlers.</span></span>

<span data-ttu-id="fdd56-149">處理領域事件是應用程式考量。</span><span class="sxs-lookup"><span data-stu-id="fdd56-149">Handling the domain events is an application concern.</span></span> <span data-ttu-id="fdd56-150">領域模型層應該只著重於領域邏輯 (也就是領域專家了解的內容)，而不是應用程式基礎結構 (例如處理常式及使用儲存機制的副作用持續性動作)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-150">The domain model layer should only focus on the domain logic—things that a domain expert would understand, not application infrastructure like handlers and side-effect persistence actions using repositories.</span></span> <span data-ttu-id="fdd56-151">因此，應用程式層是引發領域事件時，您應該讓領域事件處理常式觸發動作的位置。</span><span class="sxs-lookup"><span data-stu-id="fdd56-151">Therefore, the application layer level is where you should have domain event handlers triggering actions when a domain event is raised.</span></span>

<span data-ttu-id="fdd56-152">領域事件也可用來觸發任何數目的應用程式動作，而且更重要的是，必須沒有限制才能在未來以低耦合方式增加數目。</span><span class="sxs-lookup"><span data-stu-id="fdd56-152">Domain events can also be used to trigger any number of application actions, and what is more important, must be open to increase that number in the future in a decoupled way.</span></span> <span data-ttu-id="fdd56-153">例如，啟動訂單時，您可能想要發行領域事件，將該資訊傳播至其他彙總，或甚至是引發通知等應用程式動作。</span><span class="sxs-lookup"><span data-stu-id="fdd56-153">For instance, when the order is started, you might want to publish a domain event to propagate that info to other aggregates or even to raise application actions like notifications.</span></span>

<span data-ttu-id="fdd56-154">重點是不要限制領域事件出現時所要執行的動作數目。</span><span class="sxs-lookup"><span data-stu-id="fdd56-154">The key point is the open number of actions to be executed when a domain event occurs.</span></span> <span data-ttu-id="fdd56-155">領域和應用程式中的動作和規則最終都會成長。</span><span class="sxs-lookup"><span data-stu-id="fdd56-155">Eventually, the actions and rules in the domain and application will grow.</span></span> <span data-ttu-id="fdd56-156">當發生問題時，副作用動作的複雜度或數目會成長，但如果您的程式碼與「粘連」 (，也就是使用) 建立特定物件 `new` ，則每次您需要新增動作時，您也必須變更工作和測試程式碼。</span><span class="sxs-lookup"><span data-stu-id="fdd56-156">The complexity or number of side-effect actions when something happens will grow, but if your code were coupled with "glue" (that is, creating specific objects with `new`), then every time you needed to add a new action you would also need to change working and tested code.</span></span>

<span data-ttu-id="fdd56-157">這項變更可能會導致新的 Bug，而此方法也會違反 [SOLID](https://en.wikipedia.org/wiki/SOLID) 的 [Open–closed principl](https://en.wikipedia.org/wiki/Open/closed_principle) (開啟/關閉準則)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-157">This change could result in new bugs and this approach also goes against the [Open/Closed principle](https://en.wikipedia.org/wiki/Open/closed_principle) from [SOLID](https://en.wikipedia.org/wiki/SOLID).</span></span> <span data-ttu-id="fdd56-158">不僅如此，協調作業的原始類別會不斷成長，這違背[單一功能原則 (SRP)](https://en.wikipedia.org/wiki/Single_responsibility_principle)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-158">Not only that, the original class that was orchestrating the operations would grow and grow, which goes against the [Single Responsibility Principle (SRP)](https://en.wikipedia.org/wiki/Single_responsibility_principle).</span></span>

<span data-ttu-id="fdd56-159">相反地，如果您使用領域事件，就可以透過此方法分離職責，來建立更細緻且低耦合的實作：</span><span class="sxs-lookup"><span data-stu-id="fdd56-159">On the other hand, if you use domain events, you can create a fine-grained and decoupled implementation by segregating responsibilities using this approach:</span></span>

1. <span data-ttu-id="fdd56-160">傳送命令 (例如 CreateOrder)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-160">Send a command (for example, CreateOrder).</span></span>
2. <span data-ttu-id="fdd56-161">接收命令處理常式中的命令。</span><span class="sxs-lookup"><span data-stu-id="fdd56-161">Receive the command in a command handler.</span></span>
   - <span data-ttu-id="fdd56-162">執行單一匯總的交易。</span><span class="sxs-lookup"><span data-stu-id="fdd56-162">Execute a single aggregate's transaction.</span></span>
   - <span data-ttu-id="fdd56-163">(選擇性) 引發副作用的領域事件 (例如 OrderStartedDomainEvent)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-163">(Optional) Raise domain events for side effects (for example, OrderStartedDomainEvent).</span></span>
3. <span data-ttu-id="fdd56-164">處理領域事件 (在目前的處理序中)，這些事件會在多個彙總或應用程式動作中執行不限數目的副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-164">Handle domain events (within the current process) that will execute an open number of side effects in multiple aggregates or application actions.</span></span> <span data-ttu-id="fdd56-165">例如：</span><span class="sxs-lookup"><span data-stu-id="fdd56-165">For example:</span></span>
   - <span data-ttu-id="fdd56-166">確認或建立購買者和付款方式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-166">Verify or create buyer and payment method.</span></span>
   - <span data-ttu-id="fdd56-167">建立相關的整合事件並傳送至事件匯流排，以在微服務之間傳播狀態，或觸發外部動作，例如將電子郵件傳送給購買者。</span><span class="sxs-lookup"><span data-stu-id="fdd56-167">Create and send a related integration event to the event bus to propagate states across microservices or trigger external actions like sending an email to the buyer.</span></span>
   - <span data-ttu-id="fdd56-168">處理其他副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-168">Handle other side effects.</span></span>

<span data-ttu-id="fdd56-169">如圖 7-15 所示，從同一個領域事件開始，您可以處理與領域中其他彙總相關的多個動作，或您需要在微服務 (與整合事件和事件匯流排連線) 之間執行的其他應用程式動作。</span><span class="sxs-lookup"><span data-stu-id="fdd56-169">As shown in Figure 7-15, starting from the same domain event, you can handle multiple actions related to other aggregates in the domain or additional application actions you need to perform across microservices connecting with integration events and the event bus.</span></span>

![顯示將資料傳遞給數個事件處理常式之網域事件的圖表。](./media/domain-events-design-implementation/aggregate-domain-event-handlers.png)

<span data-ttu-id="fdd56-171">**圖 7-15**。</span><span class="sxs-lookup"><span data-stu-id="fdd56-171">**Figure 7-15**.</span></span> <span data-ttu-id="fdd56-172">處理每個領域的多個動作</span><span class="sxs-lookup"><span data-stu-id="fdd56-172">Handling multiple actions per domain</span></span>

<span data-ttu-id="fdd56-173">應用程式層中可以有數個用於相同領域事件的處理常式，一個處理常式可以解決彙總之間的一致性問題，另一個處理常式可以發佈整合事件，讓其他微服務可以對其執行某個動作。</span><span class="sxs-lookup"><span data-stu-id="fdd56-173">There can be several handlers for the same domain event in the Application Layer, one handler can solve consistency between aggregates and another handler can publish an integration event, so other microservices can do something with it.</span></span> <span data-ttu-id="fdd56-174">事件處理常式通常會在應用層中，因為您將會使用基礎結構物件（例如存放庫或應用程式 API）來微服務行為。</span><span class="sxs-lookup"><span data-stu-id="fdd56-174">The event handlers are typically in the application layer, because you will use infrastructure objects like repositories or an application API for the microservice's behavior.</span></span> <span data-ttu-id="fdd56-175">就這點而言，事件處理常式類似命令處理常式，因此兩者都屬於應用程式層。</span><span class="sxs-lookup"><span data-stu-id="fdd56-175">In that sense, event handlers are similar to command handlers, so both are part of the application layer.</span></span> <span data-ttu-id="fdd56-176">重要的差異在於命令只能處理一次。</span><span class="sxs-lookup"><span data-stu-id="fdd56-176">The important difference is that a command should be processed only once.</span></span> <span data-ttu-id="fdd56-177">因為可能有多個接收者或事件處理常式 (每個處理常式的目的不同) 接收領域事件，所以領域事件可能處理零至 *n* 次。</span><span class="sxs-lookup"><span data-stu-id="fdd56-177">A domain event could be processed zero or *n* times, because it can be received by multiple receivers or event handlers with a different purpose for each handler.</span></span>

<span data-ttu-id="fdd56-178">擁有 [每個網域的處理常式數目] 事件，可讓您視需要新增任意數量的定義域規則，而不會影響目前的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fdd56-178">Having an open number of handlers per domain event allows you to add as many domain rules as needed, without affecting  current code.</span></span> <span data-ttu-id="fdd56-179">例如，實作下列商務規則，可能與新增幾個事件處理常式 (或甚至只有一個) 一樣容易：</span><span class="sxs-lookup"><span data-stu-id="fdd56-179">For instance, implementing the following business rule might be as easy as adding a few event handlers (or even just one):</span></span>

> <span data-ttu-id="fdd56-180">當顧客在商店購買任意數目的訂單總金額超過 6000 USD 時，會對每個新的訂單套用 10% 的折扣，並以電子郵件通知顧客未來訂單的折扣。</span><span class="sxs-lookup"><span data-stu-id="fdd56-180">When the total amount purchased by a customer in the store, across any number of orders, exceeds $6,000, apply a 10% off discount to every new order and notify the customer with an email about that discount for future orders.</span></span>

## <a name="implement-domain-events"></a><span data-ttu-id="fdd56-181">實作領域事件</span><span class="sxs-lookup"><span data-stu-id="fdd56-181">Implement domain events</span></span>

<span data-ttu-id="fdd56-182">在 C# 中，領域事件單純是資料保留結構或類別 (例如 DTO)，其中包含與領域中剛發生的事件相關的所有資訊，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="fdd56-182">In C#, a domain event is simply a data-holding structure or class, like a DTO, with all the information related to what just happened in the domain, as shown in the following example:</span></span>

```csharp
public class OrderStartedDomainEvent : INotification
{
    public string UserId { get; }
    public int CardTypeId { get; }
    public string CardNumber { get; }
    public string CardSecurityNumber { get; }
    public string CardHolderName { get; }
    public DateTime CardExpiration { get; }
    public Order Order { get; }

    public OrderStartedDomainEvent(Order order,
                                   int cardTypeId, string cardNumber,
                                   string cardSecurityNumber, string cardHolderName,
                                   DateTime cardExpiration)
    {
        Order = order;
        CardTypeId = cardTypeId;
        CardNumber = cardNumber;
        CardSecurityNumber = cardSecurityNumber;
        CardHolderName = cardHolderName;
        CardExpiration = cardExpiration;
    }
}
```

<span data-ttu-id="fdd56-183">這基本上是保留與 OrderStarted 事件相關之所有資料的類別。</span><span class="sxs-lookup"><span data-stu-id="fdd56-183">This is essentially a class that holds all the data related to the OrderStarted event.</span></span>

<span data-ttu-id="fdd56-184">根據領域的通用語言，由於事件是過去發生的某件事，因此事件的類別名稱應該以過去式動詞來表示，例如 OrderStartedDomainEvent 或 OrderShippedDomainEvent。</span><span class="sxs-lookup"><span data-stu-id="fdd56-184">In terms of the ubiquitous language of the domain, since an event is something that happened in the past, the class name of the event should be represented as a past-tense verb, like OrderStartedDomainEvent or OrderShippedDomainEvent.</span></span> <span data-ttu-id="fdd56-185">這是在 eShopOnContainers 的訂購微服務中實作領域事件的方式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-185">That's how the domain event is implemented in the ordering microservice in eShopOnContainers.</span></span>

<span data-ttu-id="fdd56-186">如稍早所述，事件的一個重要特性是，由於事件是過去發生的某件事，不應該變更。</span><span class="sxs-lookup"><span data-stu-id="fdd56-186">As noted earlier, an important characteristic of events is that since an event is something that happened in the past, it should not change.</span></span> <span data-ttu-id="fdd56-187">因此，它必須是不可變的類別。</span><span class="sxs-lookup"><span data-stu-id="fdd56-187">Therefore, it must be an immutable class.</span></span> <span data-ttu-id="fdd56-188">您可以在上一個程式碼中看到屬性是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="fdd56-188">You can see in the previous code that the properties are read-only.</span></span> <span data-ttu-id="fdd56-189">沒有任何方式可更新物件，您只能在建立時設定值。</span><span class="sxs-lookup"><span data-stu-id="fdd56-189">There's no way to update the object, you can only set values when you create it.</span></span>

<span data-ttu-id="fdd56-190">請務必注意，如果要以非同步方式處理領域事件，使用需要序列化和還原序列化事件物件的佇列，則屬性必須是「私用集合」而非唯讀，如此還原序列化程式才能在清除佇列時指派值。</span><span class="sxs-lookup"><span data-stu-id="fdd56-190">It's important to highlight here that if domain events were to be handled asynchronously, using a queue that required serializing and deserializing the event objects, the properties would have to be "private set" instead of read-only, so the deserializer would be able to assign the values upon dequeuing.</span></span> <span data-ttu-id="fdd56-191">因為網域事件發佈/訂閱是使用 MediatR 以同步方式實作，所以這在訂購微服務中不成問題。</span><span class="sxs-lookup"><span data-stu-id="fdd56-191">This is not an issue in the Ordering microservice, as the domain event pub/sub is implemented synchronously using MediatR.</span></span>

### <a name="raise-domain-events"></a><span data-ttu-id="fdd56-192">引發領域事件</span><span class="sxs-lookup"><span data-stu-id="fdd56-192">Raise domain events</span></span>

<span data-ttu-id="fdd56-193">下一個問題是如何引發領域事件，使它抵達其相關的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-193">The next question is how to raise a domain event so it reaches its related event handlers.</span></span> <span data-ttu-id="fdd56-194">您可以使用多個方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-194">You can use multiple approaches.</span></span>

<span data-ttu-id="fdd56-195">Udi Dahan 原本建議使用靜態類別來管理及引發事件 (如數篇相關的文章所示，例如 [Domain Events - Take 2](https://udidahan.com/2008/08/25/domain-events-take-2/) (領域事件 - 續篇))。</span><span class="sxs-lookup"><span data-stu-id="fdd56-195">Udi Dahan originally proposed (for example, in several related posts, such as [Domain Events – Take 2](https://udidahan.com/2008/08/25/domain-events-take-2/)) using a static class for managing and raising the events.</span></span> <span data-ttu-id="fdd56-196">這可能包含名為 DomainEvents 的靜態類別，該類別會在呼叫時，使用 `DomainEvents.Raise(Event myEvent)` 等語法立即引發領域事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-196">This might include a static class named DomainEvents that would raise domain events immediately when it is called, using syntax like `DomainEvents.Raise(Event myEvent)`.</span></span> <span data-ttu-id="fdd56-197">Jimmy Bogard 所撰寫的部落格文章 ([Strengthening your domain: Domain Events](https://lostechies.com/jimmybogard/2010/04/08/strengthening-your-domain-domain-events/) (增強您的領域：領域事件)) 建議類似的方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-197">Jimmy Bogard wrote a blog post ([Strengthening your domain: Domain Events](https://lostechies.com/jimmybogard/2010/04/08/strengthening-your-domain-domain-events/)) that recommends a similar approach.</span></span>

<span data-ttu-id="fdd56-198">不過，當領域事件類別為靜態時，它也會立即分派至處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-198">However, when the domain events class is static, it also dispatches to handlers immediately.</span></span> <span data-ttu-id="fdd56-199">這會使得測試和偵錯更加困難，因為在引發事件之後會立即執行具有副作用邏輯的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-199">This makes testing and debugging more difficult, because the event handlers with side-effects logic are executed immediately after the event is raised.</span></span> <span data-ttu-id="fdd56-200">當您進行測試和偵錯工具時，您只想要專注于目前的匯總類別中發生的情況;您不希望突然被重新導向至其他事件處理常式，以瞭解與其他匯總或應用程式邏輯相關的副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-200">When you are testing and debugging, you just want to focus on what is happening in the current aggregate classes; you do not want to suddenly be redirected to other event handlers for side effects related to other aggregates or application logic.</span></span> <span data-ttu-id="fdd56-201">這就是其他方法進化的原因，如下一節中所述。</span><span class="sxs-lookup"><span data-stu-id="fdd56-201">This is why other approaches have evolved, as explained in the next section.</span></span>

#### <a name="the-deferred-approach-to-raise-and-dispatch-events"></a><span data-ttu-id="fdd56-202">引發和分派事件的延後方法</span><span class="sxs-lookup"><span data-stu-id="fdd56-202">The deferred approach to raise and dispatch events</span></span>

<span data-ttu-id="fdd56-203">您最好將領域事件新增至集合，然後在認可交易 (如同 EF 中的 SaveChanges)「之前」\*\* 或「之後」\*\* \*\* 分派這些領域事件，而不是直接分派至領域事件處理常式</span><span class="sxs-lookup"><span data-stu-id="fdd56-203">Instead of dispatching to a domain event handler immediately, a better approach is to add the domain events to a collection and then to dispatch those domain events *right before* or *right* *after* committing the transaction (as with SaveChanges in EF).</span></span> <span data-ttu-id="fdd56-204">(Jimmy Bogard 在 [A better domain events pattern](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/) (更佳的領域事件模式) 的這篇文章中說明此方法)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-204">(This approach was described by Jimmy Bogard in this post [A better domain events pattern](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/).)</span></span>

<span data-ttu-id="fdd56-205">請務必決定在認可交易之前或之後傳送領域事件，因為這會決定您將副作用加入作為相同交易的一部分，還是加入不同的交易。</span><span class="sxs-lookup"><span data-stu-id="fdd56-205">Deciding if you send the domain events right before or right after committing the transaction is important, since it determines whether you will include the side effects as part of the same transaction or in different transactions.</span></span> <span data-ttu-id="fdd56-206">在後者的情況下，您需要處理多個彙總之間的最終一致性。</span><span class="sxs-lookup"><span data-stu-id="fdd56-206">In the latter case, you need to deal with eventual consistency across multiple aggregates.</span></span> <span data-ttu-id="fdd56-207">下一節將討論這個主題。</span><span class="sxs-lookup"><span data-stu-id="fdd56-207">This topic is discussed in the next section.</span></span>

<span data-ttu-id="fdd56-208">eShopOnContainers 使用延後方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-208">The deferred approach is what eShopOnContainers uses.</span></span> <span data-ttu-id="fdd56-209">首先，您會將實體中正在發生的事件新增至每個實體的事件集合或清單。</span><span class="sxs-lookup"><span data-stu-id="fdd56-209">First, you add the events happening in your entities into a collection or list of events per entity.</span></span> <span data-ttu-id="fdd56-210">該清單應該是實體物件的一部分，最好是基底實體類別的一部分，如實體基底類別的下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="fdd56-210">That list should be part of the entity object, or even better, part of your base entity class, as shown in the following example of the Entity base class:</span></span>

```csharp
public abstract class Entity
{
     //...
     private List<INotification> _domainEvents;
     public List<INotification> DomainEvents => _domainEvents;

     public void AddDomainEvent(INotification eventItem)
     {
         _domainEvents = _domainEvents ?? new List<INotification>();
         _domainEvents.Add(eventItem);
     }

     public void RemoveDomainEvent(INotification eventItem)
     {
         _domainEvents?.Remove(eventItem);
     }
     //... Additional code
}
```

<span data-ttu-id="fdd56-211">當您想要引發事件時，您只要從彙總根實體之任何方法的程式碼將它新增至事件集合。</span><span class="sxs-lookup"><span data-stu-id="fdd56-211">When you want to raise an event, you just add it to the event collection from code at any method of the aggregate-root entity.</span></span>

<span data-ttu-id="fdd56-212">下列程式碼 (屬於 [eShopOnContainers 的 Order aggregate-root](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Order.cs)) 顯示一個範例：</span><span class="sxs-lookup"><span data-stu-id="fdd56-212">The following code, part of the [Order aggregate-root at eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Order.cs), shows an example:</span></span>

```csharp
var orderStartedDomainEvent = new OrderStartedDomainEvent(this, //Order object
                                                          cardTypeId, cardNumber,
                                                          cardSecurityNumber,
                                                          cardHolderName,
                                                          cardExpiration);
this.AddDomainEvent(orderStartedDomainEvent);
```

<span data-ttu-id="fdd56-213">請注意，AddDomainEvent 方法只會將事件新增至清單。</span><span class="sxs-lookup"><span data-stu-id="fdd56-213">Notice that the only thing that the AddDomainEvent method is doing is adding an event to the list.</span></span> <span data-ttu-id="fdd56-214">尚未分派任何事件，而且尚未叫用任何事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-214">No event is dispatched yet, and no event handler is invoked yet.</span></span>

<span data-ttu-id="fdd56-215">您實際上想要稍後在將交易認可至資料庫時分派事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-215">You actually want to dispatch the events later on, when you commit the transaction to the database.</span></span> <span data-ttu-id="fdd56-216">如果您使用 Entity Framework Core，也就是在 EF DbContext 的 SaveChanges 方法中 (如下列程式碼所示)：</span><span class="sxs-lookup"><span data-stu-id="fdd56-216">If you are using Entity Framework Core, that means in the SaveChanges method of your EF DbContext, as in the following code:</span></span>

```csharp
// EF Core DbContext
public class OrderingContext : DbContext, IUnitOfWork
{
    // ...
    public async Task<bool> SaveEntitiesAsync(CancellationToken cancellationToken = default(CancellationToken))
    {
        // Dispatch Domain Events collection.
        // Choices:
        // A) Right BEFORE committing data (EF SaveChanges) into the DB. This makes
        // a single transaction including side effects from the domain event
        // handlers that are using the same DbContext with Scope lifetime
        // B) Right AFTER committing data (EF SaveChanges) into the DB. This makes
        // multiple transactions. You will need to handle eventual consistency and
        // compensatory actions in case of failures.
        await _mediator.DispatchDomainEventsAsync(this);

        // After this line runs, all the changes (from the Command Handler and Domain
        // event handlers) performed through the DbContext will be committed
        var result = await base.SaveChangesAsync();
    }
}
```

<span data-ttu-id="fdd56-217">在此程式碼中，您會將實體事件分派至其各自的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-217">With this code, you dispatch the entity events to their respective event handlers.</span></span>

<span data-ttu-id="fdd56-218">整體結果是您將引發領域事件 (記憶體內部清單中的一個簡單新增)，與將它分派至事件處理常式的職責分離。</span><span class="sxs-lookup"><span data-stu-id="fdd56-218">The overall result is that you have decoupled the raising of a domain event (a simple add into a list in memory) from dispatching it to an event handler.</span></span> <span data-ttu-id="fdd56-219">此外，根據您使用的發送器類型，您可以利用同步或非同步方式來分派事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-219">In addition, depending on what kind of dispatcher you are using, you could dispatch the events synchronously or asynchronously.</span></span>

<span data-ttu-id="fdd56-220">請注意，交易界限在此扮演重要的角色。</span><span class="sxs-lookup"><span data-stu-id="fdd56-220">Be aware that transactional boundaries come into significant play here.</span></span> <span data-ttu-id="fdd56-221">如果您的工作單位和交易可跨多個彙總 (如同使用 EF Core 和關聯式資料庫時)，則會正常運作。</span><span class="sxs-lookup"><span data-stu-id="fdd56-221">If your unit of work and transaction can span more than one aggregate (as when using EF Core and a relational database), this can work well.</span></span> <span data-ttu-id="fdd56-222">但如果交易不可跨多個彙總 (例如當您使用 Azure CosmosDB 等 NoSQL 資料庫時)，您必須實作額外的步驟，才能達到一致性。</span><span class="sxs-lookup"><span data-stu-id="fdd56-222">But if the transaction cannot span aggregates, such as when you are using a NoSQL database like Azure CosmosDB, you have to implement additional steps to achieve consistency.</span></span> <span data-ttu-id="fdd56-223">這是永續性無知不通用的另一個原因，它需要您使用的儲存體系統。</span><span class="sxs-lookup"><span data-stu-id="fdd56-223">This is another reason why persistence ignorance is not universal; it depends on the storage system you use.</span></span>

### <a name="single-transaction-across-aggregates-versus-eventual-consistency-across-aggregates"></a><span data-ttu-id="fdd56-224">跨彙總的單一交易與跨彙總的最終一致性之比較</span><span class="sxs-lookup"><span data-stu-id="fdd56-224">Single transaction across aggregates versus eventual consistency across aggregates</span></span>

<span data-ttu-id="fdd56-225">要在多個彙總之間執行單一交易，還是要依賴這些彙總之間的最終一致性，是具爭議性的問題。</span><span class="sxs-lookup"><span data-stu-id="fdd56-225">The question of whether to perform a single transaction across aggregates versus relying on eventual consistency across those aggregates is a controversial one.</span></span> <span data-ttu-id="fdd56-226">許多 DDD 作者 (像是 Eric Evans 和 Vaughn Vernon) 提倡一個交易等於一個彙總的規則，因此支持在多個彙總之間取得最終一致性。</span><span class="sxs-lookup"><span data-stu-id="fdd56-226">Many DDD authors like Eric Evans and Vaughn Vernon advocate the rule that one transaction = one aggregate and therefore argue for eventual consistency across aggregates.</span></span> <span data-ttu-id="fdd56-227">例如，Eric Evans 在 *Domain-Driven Design* 一書中表示：</span><span class="sxs-lookup"><span data-stu-id="fdd56-227">For example, in his book *Domain-Driven Design*, Eric Evans says this:</span></span>

> <span data-ttu-id="fdd56-228">任何跨彙總的規則不必總是處於最新狀態。</span><span class="sxs-lookup"><span data-stu-id="fdd56-228">Any rule that spans Aggregates will not be expected to be up-to-date at all times.</span></span> <span data-ttu-id="fdd56-229">透過事件處理、批次處理或其他更新機制，即可解析一段特定時間內的其他相依性</span><span class="sxs-lookup"><span data-stu-id="fdd56-229">Through event processing, batch processing, or other update mechanisms, other dependencies can be resolved within some specific time.</span></span> <span data-ttu-id="fdd56-230">(第 128 頁)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-230">(page 128)</span></span>

<span data-ttu-id="fdd56-231">Vaughn Vernon 在有效的匯總設計中指出下列各項 [。第二部分：讓匯總搭配運作](https://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf)：</span><span class="sxs-lookup"><span data-stu-id="fdd56-231">Vaughn Vernon says the following in [Effective Aggregate Design. Part II: Making Aggregates Work Together](https://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf):</span></span>

> <span data-ttu-id="fdd56-232">因此，如果在一個匯總實例上執行命令，需要在一或多個匯總上執行其他商務規則，請使用最終一致性 \[ ... \] 有一個實用的方法可支援 DDD 模型中的最終一致性。</span><span class="sxs-lookup"><span data-stu-id="fdd56-232">Thus, if executing a command on one aggregate instance requires that additional business rules execute on one or more aggregates, use eventual consistency \[...\] There is a practical way to support eventual consistency in a DDD model.</span></span> <span data-ttu-id="fdd56-233">彙總方法會發行領域事件，及時傳遞至一或多個非同步訂閱者。</span><span class="sxs-lookup"><span data-stu-id="fdd56-233">An aggregate method publishes a domain event that is in time delivered to one or more asynchronous subscribers.</span></span>

<span data-ttu-id="fdd56-234">此原理是以更細緻的交易為基礎，而不是以跨許多彙總或實體的交易為基礎。</span><span class="sxs-lookup"><span data-stu-id="fdd56-234">This rationale is based on embracing fine-grained transactions instead of transactions spanning many aggregates or entities.</span></span> <span data-ttu-id="fdd56-235">其概念是在第二個案例中，資料庫鎖定數目在具有高延展性需求的大型應用程式中會很大。</span><span class="sxs-lookup"><span data-stu-id="fdd56-235">The idea is that in the second case, the number of database locks will be substantial in large-scale applications with high scalability needs.</span></span> <span data-ttu-id="fdd56-236">可高度擴充的應用程式不需要在多個彙總之間有立即交易一致性，認清這點事實有助於接受最終一致性概念。</span><span class="sxs-lookup"><span data-stu-id="fdd56-236">Embracing the fact that highly scalable applications need not have instant transactional consistency between multiple aggregates helps with accepting the concept of eventual consistency.</span></span> <span data-ttu-id="fdd56-237">企業通常不需要不可部分完成變更，而且在任何情況下，領域專家都有責任指出特定作業是否需要不可部分完成交易。</span><span class="sxs-lookup"><span data-stu-id="fdd56-237">Atomic changes are often not needed by the business, and it is in any case the responsibility of the domain experts to say whether particular operations need atomic transactions or not.</span></span> <span data-ttu-id="fdd56-238">如果作業一律需要在多個彙總之間有不可部分完成交易，您可能會詢問彙總是否應該更大或設計是否不正確。</span><span class="sxs-lookup"><span data-stu-id="fdd56-238">If an operation always needs an atomic transaction between multiple aggregates, you might ask whether your aggregate should be larger or was not correctly designed.</span></span>

<span data-ttu-id="fdd56-239">不過，其他開發人員以及像是 Jimmy Bogard 的架構設計人員接受單一交易橫跨數個彙總，但僅限於這些額外的彙總與相同原始命令的副作用相關時。</span><span class="sxs-lookup"><span data-stu-id="fdd56-239">However, other developers and architects like Jimmy Bogard are okay with spanning a single transaction across several aggregates—but only when those additional aggregates are related to side effects for the same original command.</span></span> <span data-ttu-id="fdd56-240">例如，Bogard 在 [A better domain events pattern](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/) (更佳的領域事件模式) 中表示：</span><span class="sxs-lookup"><span data-stu-id="fdd56-240">For instance, in [A better domain events pattern](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/), Bogard says this:</span></span>

> <span data-ttu-id="fdd56-241">一般來說，我想要讓領域事件的副作用發生在相同的邏輯交易中，但不一定是在引發 \[ 領域事件 \] 的相同範圍內 .。。在認可交易之前，我們會將事件分派至其各自的處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-241">Typically, I want the side effects of a domain event to occur within the same logical transaction, but not necessarily in the same scope of raising the domain event \[...\] Just before we commit our transaction, we dispatch our events to their respective handlers.</span></span>

<span data-ttu-id="fdd56-242">如果您在認可原始交易「之前」\*\* 分派領域事件，這是因為您想要將這些事件的副作用包含在相同的交易中。</span><span class="sxs-lookup"><span data-stu-id="fdd56-242">If you dispatch the domain events right *before* committing the original transaction, it is because you want the side effects of those events to be included in the same transaction.</span></span> <span data-ttu-id="fdd56-243">例如，如果 EF DbContext SaveChanges 方法失敗，交易將會復原所有變更，包括相關領域事件處理常式所實作之任何副作用作業的結果。</span><span class="sxs-lookup"><span data-stu-id="fdd56-243">For example, if the EF DbContext SaveChanges method fails, the transaction will roll back all changes, including the result of any side effect operations implemented by the related domain event handlers.</span></span> <span data-ttu-id="fdd56-244">這是因為 DbContext 存留期範圍預設會定義為 "scoped"。</span><span class="sxs-lookup"><span data-stu-id="fdd56-244">This is because the DbContext life scope is by default defined as "scoped."</span></span> <span data-ttu-id="fdd56-245">因此，DbContext 物件會在相同範圍或物件圖形內要具現化的多個儲存機制物件之間共用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-245">Therefore, the DbContext object is shared across multiple repository objects being instantiated within the same scope or object graph.</span></span> <span data-ttu-id="fdd56-246">開發 Web API 或 MVC 應用程式時，這會與 HttpRequest 範圍一致。</span><span class="sxs-lookup"><span data-stu-id="fdd56-246">This coincides with the HttpRequest scope when developing Web API or MVC apps.</span></span>

<span data-ttu-id="fdd56-247">實際上，這兩種方法 (單一不可部分完成交易和最終一致性) 都正確。</span><span class="sxs-lookup"><span data-stu-id="fdd56-247">Actually, both approaches (single atomic transaction and eventual consistency) can be right.</span></span> <span data-ttu-id="fdd56-248">它其實取決於您的領域或商務需求，以及領域專家給您的建議。</span><span class="sxs-lookup"><span data-stu-id="fdd56-248">It really depends on your domain or business requirements and what the domain experts tell you.</span></span> <span data-ttu-id="fdd56-249">它也取決於您需要的服務延展性 (交易越細緻，對資料庫鎖定的影響越低)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-249">It also depends on how scalable you need the service to be (more granular transactions have less impact with regard to database locks).</span></span> <span data-ttu-id="fdd56-250">此外，它取決您願意對程式碼的投資，因為最終一致性需要更複雜的程式碼，才能偵測彙總之間可能不一致性的情況，並需要實作補償動作。</span><span class="sxs-lookup"><span data-stu-id="fdd56-250">And it depends on how much investment you are willing to make in your code, since eventual consistency requires more complex code in order to detect possible inconsistencies across aggregates and the need to implement compensatory actions.</span></span> <span data-ttu-id="fdd56-251">請考慮下列情況，如果您將變更認可至原始彙總，之後當分派事件時發生問題，而且事件處理常式無法認可其副作用，則彙總之間會有不一致的情況。</span><span class="sxs-lookup"><span data-stu-id="fdd56-251">Consider that if you commit changes to the original aggregate and afterwards, when the events are being dispatched, if there is an issue and the event handlers cannot commit their side effects, you will have inconsistencies between aggregates.</span></span>

<span data-ttu-id="fdd56-252">一個允許補償動作的方法是將領域事件儲存在其他資料庫資料表中，讓它們可以成為原始交易的一部分。</span><span class="sxs-lookup"><span data-stu-id="fdd56-252">A way to allow compensatory actions would be to store the domain events in additional database tables so they can be part of the original transaction.</span></span> <span data-ttu-id="fdd56-253">之後，您可以有一個批次程序，藉由比較事件清單與彙總的目前狀態，來偵測不一致性的情況並執行補償動作。</span><span class="sxs-lookup"><span data-stu-id="fdd56-253">Afterwards, you could have a batch process that detects inconsistencies and runs compensatory actions by comparing the list of events with the current state of the aggregates.</span></span> <span data-ttu-id="fdd56-254">補償動作屬於複雜主題，需要您深入分析，包括與企業用戶以及領域專家進行討論。</span><span class="sxs-lookup"><span data-stu-id="fdd56-254">The compensatory actions are part of a complex topic that will require deep analysis from your side, which includes discussing it with the business user and domain experts.</span></span>

<span data-ttu-id="fdd56-255">在任何情況下，您都可以選擇所需的方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-255">In any case, you can choose the approach you need.</span></span> <span data-ttu-id="fdd56-256">但初始延後方法 (在認可前引發事件以便您使用單一交易) 是使用 EF Core 和關聯式資料庫時的最簡單方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-256">But the initial deferred approach—raising the events before committing, so you use a single transaction—is the simplest approach when using EF Core and a relational database.</span></span> <span data-ttu-id="fdd56-257">實作起來更容易，而且在許多商務案例中很有效。</span><span class="sxs-lookup"><span data-stu-id="fdd56-257">It is easier to implement and valid in many business cases.</span></span> <span data-ttu-id="fdd56-258">這也是 eShopOnContainers 中的訂購微服務所使用的方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-258">It is also the approach used in the ordering microservice in eShopOnContainers.</span></span>

<span data-ttu-id="fdd56-259">但您實際上如何將這些事件分派至其各自的事件處理常式？</span><span class="sxs-lookup"><span data-stu-id="fdd56-259">But how do you actually dispatch those events to their respective event handlers?</span></span> <span data-ttu-id="fdd56-260">您在上一個範例中看到的 `_mediator` 物件為何？</span><span class="sxs-lookup"><span data-stu-id="fdd56-260">What's the `_mediator` object you see in the previous example?</span></span> <span data-ttu-id="fdd56-261">這與您用來對應事件與其事件處理常式的技術和成品有關。</span><span class="sxs-lookup"><span data-stu-id="fdd56-261">It has to do with the techniques and artifacts you use to map between events and their event handlers.</span></span>

### <a name="the-domain-event-dispatcher-mapping-from-events-to-event-handlers"></a><span data-ttu-id="fdd56-262">領域事件發送器：事件與事件處理常式的對應</span><span class="sxs-lookup"><span data-stu-id="fdd56-262">The domain event dispatcher: mapping from events to event handlers</span></span>

<span data-ttu-id="fdd56-263">一旦您可以分派或發行事件，您需要某種會發行事件的成品，讓每個相關的處理常式可以取得它，並根據該事件來處理副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-263">Once you're able to dispatch or publish the events, you need some kind of artifact that will publish the event, so that every related handler can get it and process side effects based on that event.</span></span>

<span data-ttu-id="fdd56-264">一個方法是即時傳訊系統或甚至事件匯流排，可能會根據服務匯流排，而不是記憶體內部事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-264">One approach is a real messaging system or even an event bus, possibly based on a service bus as opposed to in-memory events.</span></span> <span data-ttu-id="fdd56-265">不過，在第一個案例中，即時傳訊對處理領域事件會過當，因為您只需要處理相同處理序 (也就是相同領域和應用程式層) 中的這些事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-265">However, for the first case, real messaging would be overkill for processing domain events, since you just need to process those events within the same process (that is, within the same domain and application layer).</span></span>

<span data-ttu-id="fdd56-266">另一個方法是藉由在 IoC 容器中使用類型註冊，將事件對應至多個事件處理常式，因此您可以動態推斷分派事件的位置。</span><span class="sxs-lookup"><span data-stu-id="fdd56-266">Another way to map events to multiple event handlers is by using types registration in an IoC container so you can dynamically infer where to dispatch the events.</span></span> <span data-ttu-id="fdd56-267">換句話說，您需要知道需要取得特定事件的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-267">In other words, you need to know what event handlers need to get a specific event.</span></span> <span data-ttu-id="fdd56-268">圖 7-16 顯示此方法的簡化方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-268">Figure 7-16 shows a simplified approach for this approach.</span></span>

![顯示網域事件發送器將事件傳送到適當處理常式的圖表。](./media/domain-events-design-implementation/domain-event-dispatcher.png)

<span data-ttu-id="fdd56-270">**圖 7-16**。</span><span class="sxs-lookup"><span data-stu-id="fdd56-270">**Figure 7-16**.</span></span> <span data-ttu-id="fdd56-271">使用 IoC 的領域事件發送器</span><span class="sxs-lookup"><span data-stu-id="fdd56-271">Domain event dispatcher using IoC</span></span>

<span data-ttu-id="fdd56-272">您可以建立所有連接和成品，自行實作該方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-272">You can build all the plumbing and artifacts to implement that approach by yourself.</span></span> <span data-ttu-id="fdd56-273">不過，您也可以使用 [MediatR](https://github.com/jbogard/MediatR) 等可用的程式庫，這些程式庫基本上會使用您的 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="fdd56-273">However, you can also use available libraries like [MediatR](https://github.com/jbogard/MediatR) that uses your IoC container under the covers.</span></span> <span data-ttu-id="fdd56-274">因此，您可以直接使用預先定義的介面和中繼程式物件的發佈/分派方法。</span><span class="sxs-lookup"><span data-stu-id="fdd56-274">You can therefore directly use the predefined interfaces and the mediator object's publish/dispatch methods.</span></span>

<span data-ttu-id="fdd56-275">在程式碼中，您必須先在 IoC 容器中登錄事件處理常式類型，如 [eShopOnContainers 訂購微服務](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/MediatorModule.cs)的下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="fdd56-275">In code, you first need to register the event handler types in your IoC container, as shown in the following example at [eShopOnContainers Ordering microservice](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Infrastructure/AutofacModules/MediatorModule.cs):</span></span>

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        // Other registrations ...
        // Register the DomainEventHandler classes (they implement IAsyncNotificationHandler<>)
        // in assembly holding the Domain Events
        builder.RegisterAssemblyTypes(typeof(ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler)
                                       .GetTypeInfo().Assembly)
                                         .AsClosedTypesOf(typeof(IAsyncNotificationHandler<>));
        // Other registrations ...
    }
}
```

<span data-ttu-id="fdd56-276">此程式碼會先尋找保留任何處理常式的組件，以識別包含領域事件處理常式的組件 (使用 typeof(ValidateOrAddBuyerAggregateWhenXxxx)，但您可以選擇任何其他事件處理常式來尋找組件)。</span><span class="sxs-lookup"><span data-stu-id="fdd56-276">The code first identifies the assembly that contains the domain event handlers by locating the assembly that holds any of the handlers (using typeof(ValidateOrAddBuyerAggregateWhenXxxx), but you could have chosen any other event handler to locate the assembly).</span></span> <span data-ttu-id="fdd56-277">由於所有事件處理常式都會實作 IAsyncNotificationHandler 介面，因此程式碼會接著直接搜尋這些類型並登錄所有事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-277">Since all the event handlers implement the IAsyncNotificationHandler interface, the code then just searches for those types and registers all the event handlers.</span></span>

### <a name="how-to-subscribe-to-domain-events"></a><span data-ttu-id="fdd56-278">如何訂閱領域事件</span><span class="sxs-lookup"><span data-stu-id="fdd56-278">How to subscribe to domain events</span></span>

<span data-ttu-id="fdd56-279">當您使用 MediatR 時，每個事件處理常式必須使用 INotificationHandler 介面的泛型參數所提供的事件類型，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="fdd56-279">When you use MediatR, each event handler must use an event type that is provided on the generic parameter of the INotificationHandler interface, as you can see in the following code:</span></span>

```csharp
public class ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler
  : IAsyncNotificationHandler<OrderStartedDomainEvent>
```

<span data-ttu-id="fdd56-280">根據事件與事件處理常式之間的關聯性 (可視為訂閱)，MediatR 成品可探索每個事件的所有事件處理常式，並觸發每一個事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="fdd56-280">Based on the relationship between event and event handler, which can be considered the subscription, the MediatR artifact can discover all the event handlers for each event and trigger each one of those event handlers.</span></span>

### <a name="how-to-handle-domain-events"></a><span data-ttu-id="fdd56-281">如何處理領域事件</span><span class="sxs-lookup"><span data-stu-id="fdd56-281">How to handle domain events</span></span>

<span data-ttu-id="fdd56-282">最後，事件處理常式通常會實作應用程式層程式碼，該程式碼使用基礎結構儲存機制來取得所需的額外彙總，並執行副作用領域邏輯。</span><span class="sxs-lookup"><span data-stu-id="fdd56-282">Finally, the event handler usually implements application layer code that uses infrastructure repositories to obtain the required additional aggregates and to execute side-effect domain logic.</span></span> <span data-ttu-id="fdd56-283">下列 [eShopOnContainers 領域事件處理常式程式碼](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/DomainEventHandlers/OrderStartedEvent/ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler.cs)顯示一個實作範例。</span><span class="sxs-lookup"><span data-stu-id="fdd56-283">The following [domain event handler code at eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/Services/Ordering/Ordering.API/Application/DomainEventHandlers/OrderStartedEvent/ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler.cs), shows an implementation example.</span></span>

```csharp
public class ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler
                   : INotificationHandler<OrderStartedDomainEvent>
{
    private readonly ILoggerFactory _logger;
    private readonly IBuyerRepository<Buyer> _buyerRepository;
    private readonly IIdentityService _identityService;

    public ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler(
        ILoggerFactory logger,
        IBuyerRepository<Buyer> buyerRepository,
        IIdentityService identityService)
    {
        // ...Parameter validations...
    }

    public async Task Handle(OrderStartedDomainEvent orderStartedEvent)
    {
        var cardTypeId = (orderStartedEvent.CardTypeId != 0) ? orderStartedEvent.CardTypeId : 1;
        var userGuid = _identityService.GetUserIdentity();
        var buyer = await _buyerRepository.FindAsync(userGuid);
        bool buyerOriginallyExisted = (buyer == null) ? false : true;

        if (!buyerOriginallyExisted)
        {
            buyer = new Buyer(userGuid);
        }

        buyer.VerifyOrAddPaymentMethod(cardTypeId,
                                       $"Payment Method on {DateTime.UtcNow}",
                                       orderStartedEvent.CardNumber,
                                       orderStartedEvent.CardSecurityNumber,
                                       orderStartedEvent.CardHolderName,
                                       orderStartedEvent.CardExpiration,
                                       orderStartedEvent.Order.Id);

        var buyerUpdated = buyerOriginallyExisted ? _buyerRepository.Update(buyer)
                                                                      : _buyerRepository.Add(buyer);

        await _buyerRepository.UnitOfWork
                .SaveEntitiesAsync();

        // Logging code using buyerUpdated info, etc.
    }
}
```

<span data-ttu-id="fdd56-284">上述領域事件處理常式程式碼會視為應用程式層程式碼，因此它使用基礎結構儲存機制，如下一節的基礎結構持續性層中所述。</span><span class="sxs-lookup"><span data-stu-id="fdd56-284">The previous domain event handler code is considered application layer code because it uses infrastructure repositories, as explained in the next section on the infrastructure-persistence layer.</span></span> <span data-ttu-id="fdd56-285">事件處理常式也可以使用其他基礎結構元件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-285">Event handlers could also use other infrastructure components.</span></span>

#### <a name="domain-events-can-generate-integration-events-to-be-published-outside-of-the-microservice-boundaries"></a><span data-ttu-id="fdd56-286">領域事件可以產生要在微服務界限以外發行的整合事件</span><span class="sxs-lookup"><span data-stu-id="fdd56-286">Domain events can generate integration events to be published outside of the microservice boundaries</span></span>

<span data-ttu-id="fdd56-287">最後值得一提的是，您有時可能會想要在多個微服務之間傳播事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-287">Finally, it's important to mention that you might sometimes want to propagate events across multiple microservices.</span></span> <span data-ttu-id="fdd56-288">這項傳播是整合事件，而且可透過事件匯流排從特定領域事件處理常式發佈。</span><span class="sxs-lookup"><span data-stu-id="fdd56-288">That propagation is an integration event, and it could be published through an event bus from any specific domain event handler.</span></span>

## <a name="conclusions-on-domain-events"></a><span data-ttu-id="fdd56-289">領域事件結論</span><span class="sxs-lookup"><span data-stu-id="fdd56-289">Conclusions on domain events</span></span>

<span data-ttu-id="fdd56-290">如前所述，使用領域事件可明確實作您領域中變更的副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-290">As stated, use domain events to explicitly implement side effects of changes within your domain.</span></span> <span data-ttu-id="fdd56-291">以 DDD 術語來說，使用領域事件可在一或多個彙總之間明確實作副作用。</span><span class="sxs-lookup"><span data-stu-id="fdd56-291">To use DDD terminology, use domain events to explicitly implement side effects across one or multiple aggregates.</span></span> <span data-ttu-id="fdd56-292">此外，為了提高延展性並降低資料庫鎖定的影響，請在相同領域中的多個彙總之間使用最終一致性。</span><span class="sxs-lookup"><span data-stu-id="fdd56-292">Additionally, and for better scalability and less impact on database locks, use eventual consistency between aggregates within the same domain.</span></span>

<span data-ttu-id="fdd56-293">參考應用程式會使用 [MediatR](https://github.com/jbogard/MediatR) ，在單一交易內以同步方式跨匯總傳播領域事件。</span><span class="sxs-lookup"><span data-stu-id="fdd56-293">The reference app uses [MediatR](https://github.com/jbogard/MediatR) to propagate domain events synchronously across aggregates, within a single transaction.</span></span> <span data-ttu-id="fdd56-294">不過，您也可以使用一些 AMQP 的執行，例如 [RabbitMQ](https://www.rabbitmq.com/) 或 [Azure 服務匯流排](/azure/service-bus-messaging/service-bus-messaging-overview) ，以非同步方式使用最終一致性傳播領域事件，但如上所述，您必須考慮在發生失敗時需要補償的動作。</span><span class="sxs-lookup"><span data-stu-id="fdd56-294">However, you could also use some AMQP implementation like [RabbitMQ](https://www.rabbitmq.com/) or [Azure Service Bus](/azure/service-bus-messaging/service-bus-messaging-overview) to propagate domain events asynchronously, using eventual consistency but, as mentioned above, you have to consider the need for compensatory actions in case of failures.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fdd56-295">其他資源</span><span class="sxs-lookup"><span data-stu-id="fdd56-295">Additional resources</span></span>

- <span data-ttu-id="fdd56-296">**Greg 年輕什麼是領域事件？**</span><span class="sxs-lookup"><span data-stu-id="fdd56-296">**Greg Young. What is a Domain Event?**</span></span> \
  <https://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf#page=25>

- <span data-ttu-id="fdd56-297">**Jan Stenberg。領域事件和最終一致性** </span><span class="sxs-lookup"><span data-stu-id="fdd56-297">**Jan Stenberg. Domain Events and Eventual Consistency** </span></span>\
  <https://www.infoq.com/news/2015/09/domain-events-consistency>

- <span data-ttu-id="fdd56-298">**Jimmy Bogard。更好的領域事件模式** </span><span class="sxs-lookup"><span data-stu-id="fdd56-298">**Jimmy Bogard. A better domain events pattern** </span></span>\
  <https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/>

- <span data-ttu-id="fdd56-299">**Vaughn Vernon。有效匯總設計第二部分：讓匯總一起運作** </span><span class="sxs-lookup"><span data-stu-id="fdd56-299">**Vaughn Vernon. Effective Aggregate Design Part II: Making Aggregates Work Together** </span></span>\
  [https://dddcommunity.org/wp-content/uploads/files/pdf\_articles/Vernon\_2011\_2.pdf](https://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf)

- <span data-ttu-id="fdd56-300">**Jimmy Bogard。強化您的領域：領域事件** </span><span class="sxs-lookup"><span data-stu-id="fdd56-300">**Jimmy Bogard. Strengthening your domain: Domain Events** </span></span>\
  <https://lostechies.com/jimmybogard/2010/04/08/strengthening-your-domain-domain-events/>

- <span data-ttu-id="fdd56-301">**Tony Truong。領域事件模式範例** </span><span class="sxs-lookup"><span data-stu-id="fdd56-301">**Tony Truong. Domain Events Pattern Example** </span></span>\
  <https://www.tonytruong.net/domain-events-pattern-example/>

- <span data-ttu-id="fdd56-302">**Udi Dahan。如何建立完整封裝的網域模型** </span><span class="sxs-lookup"><span data-stu-id="fdd56-302">**Udi Dahan. How to create fully encapsulated Domain Models** </span></span>\
  <https://udidahan.com/2008/02/29/how-to-create-fully-encapsulated-domain-models/>

- <span data-ttu-id="fdd56-303">**Udi Dahan。領域事件-Take 2** </span><span class="sxs-lookup"><span data-stu-id="fdd56-303">**Udi Dahan. Domain Events – Take 2** </span></span>\
  <https://udidahan.com/2008/08/25/domain-events-take-2/>

- <span data-ttu-id="fdd56-304">**Udi Dahan。領域事件–解答** </span><span class="sxs-lookup"><span data-stu-id="fdd56-304">**Udi Dahan. Domain Events – Salvation** </span></span>\
  <https://udidahan.com/2009/06/14/domain-events-salvation/>

- <span data-ttu-id="fdd56-305">**Jan Kronquist。不要發佈領域事件，傳回它們！**</span><span class="sxs-lookup"><span data-stu-id="fdd56-305">**Jan Kronquist. Don't publish Domain Events, return them!**</span></span> \
  <https://blog.jayway.com/2013/06/20/dont-publish-domain-events-return-them/>

- <span data-ttu-id="fdd56-306">**Cesar de la Torre。網域事件與 DDD 和微服務架構中的整合事件** </span><span class="sxs-lookup"><span data-stu-id="fdd56-306">**Cesar de la Torre. Domain Events vs. Integration Events in DDD and microservices architectures** </span></span>\
  <https://devblogs.microsoft.com/cesardelatorre/domain-events-vs-integration-events-in-domain-driven-design-and-microservices-architectures/>

>[!div class="step-by-step"]
><span data-ttu-id="fdd56-307">[上一個](client-side-validation.md) 
>[下一步](infrastructure-persistence-layer-design.md)</span><span class="sxs-lookup"><span data-stu-id="fdd56-307">[Previous](client-side-validation.md)
[Next](infrastructure-persistence-layer-design.md)</span></span>
