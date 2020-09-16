---
title: 實作微服務之間的事件通訊 (整合事件)
description: .NET 微服務：容器化 .NET 應用程式的架構 | 了解整合事件以實作微服務之間的事件通訊。
ms.date: 10/02/2018
ms.openlocfilehash: cbc9d28f9fbcaea528eabc4930476545cb919bb4
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90539342"
---
# <a name="implementing-event-based-communication-between-microservices-integration-events"></a>實作微服務之間的事件通訊 (整合事件)

如前所述，當您使用事件通訊時，微服務會在發生值得注意的事件時發行事件，例如當它更新商務實體時。 其他微服務會訂閱這些事件。 當微服務收到事件時，它可以更新自己的商務實體，這可能會導致發行更多的事件。 這是最終一致性概念的本質。 此發行/訂閱系統通常藉由使用事件匯流排實作來執行。 事件匯流排可設計為介面，並具備訂閱及取消訂閱事件以及發行事件所需的 API。 它也可以有一或多個實作以任何處理序間或傳訊通訊為基礎，例如支援非同步通訊和發行/訂閱模型的傳訊佇列或服務匯流排。

您可以使用事件來實作橫跨多個服務的商務交易，這樣將提供這些服務之間的最終一致性。 最終一致的交易是由一系列的分散式動作所組成。 在每個動作中，微服務會更新商務實體，並發行觸發下一個動作的事件。 圖6-18 顯示透過事件匯流排發佈的 PriceUpdated 事件，因此價格更新會傳播到購物籃和其他微服務。

![與事件匯流排進行非同步事件驅動通訊的圖表。](./media/integration-event-based-microservice-communications/event-driven-communication.png)

**圖 6-18**。 以事件匯流排為基礎的事件驅動通訊

本節描述如何使用一般事件匯流排介面來實作這種類型的 .NET 通訊，如圖 6-18 所示。 有多種可能的實作，每一種都使用不同的技術或基礎結構，例如 RabbitMQ、Azure 服務匯流排，或任何其他協力廠商開放原始碼或商業服務匯流排。

## <a name="using-message-brokers-and-services-buses-for-production-systems"></a>對於生產環境使用訊息代理程式和服務匯流

如架構一節所述，您可以從多種傳訊技術選擇，以便實作抽象事件匯流排。 但是，這些技術都是在不同層級。 例如，RabbitMQ 是傳訊代理程式傳輸，它的層級比例如 Azure 服務匯流排、NServiceBus、MassTransit 或 Brighter 等商業產品低。 大部分的這些產品可以在 RabbitMQ 或 Azure 服務匯流排上工作。 您所選擇的產品取決於您的應用程式需要多少功能和多少現成的延展性。

針對只為您的開發環境實作事件匯流排的概念證明，如同 eShopOnContainers 範例，在執行作為容器的 RabbitMQ 上進行簡單實作可能就足夠了。 但對於需要高延展性的關鍵任務和生產系統，您可能想要評估，並使用 Azure 服務匯流排。

如果您的長時間執行處理序需要高階抽象，以及更豐富的功能，例如 [Sagas](https://docs.particular.net/nservicebus/sagas/)，以便讓分散式開發更容易，則其他商業和開放原始碼的服務匯流排，例如 NServiceBus、MassTransit 和 Brighter 都值得評估。 在此案例中，要使用的抽象和 API 通常會直接由這些高階服務匯流排提供，而不是您自己的抽象 (例如 [eShopOnContainers 所提供的簡單事件匯流排抽象](https://github.com/dotnet-architecture/eShopOnContainers/blob/dev/src/BuildingBlocks/EventBus/EventBus/Abstractions/IEventBus.cs))。 就這一點而言，您可以 [使用 NServiceBus](https://go.particular.net/eShopOnContainers) (特定軟體所執行的其他衍生範例) 來研究分支 eShopOnContainers。

當然，您永遠可以在較低層級的技術（例如 RabbitMQ 和 Docker）上建立自己的服務匯流排功能，但是「重寫輪子」所需的工作可能太過自訂企業應用程式的成本。

再重申一次：在 eShopOnContainers 範例中所展示的範例事件匯流排抽象概念與實作僅作為概念證明使用。 一旦您決定要進行非同步和事件驅動通訊，如目前這一節中所述，您應該選擇最適合生產環境需求的服務匯流排產品。

## <a name="integration-events"></a>整合事件

整合事件用來讓跨多個微服務或外部系統的領域狀態同步。 這是藉由在微服務以外發行整合事件而達成。 當事件發行到多個接收者微服務時 (微服務的數量為訂閱整合事件的微服務數量)，每個接收者微服務中的適當事件處理常式會處理事件。

整合事件基本上是保存資料的類別，如下列範例所示：

```csharp
public class ProductPriceChangedIntegrationEvent : IntegrationEvent
{
    public int ProductId { get; private set; }
    public decimal NewPrice { get; private set; }
    public decimal OldPrice { get; private set; }

    public ProductPriceChangedIntegrationEvent(int productId, decimal newPrice,
        decimal oldPrice)
    {
        ProductId = productId;
        NewPrice = newPrice;
        OldPrice = oldPrice;
    }
}
```

整合事件可以在每個微服務的應用程式層級定義，讓它們與其他微服務彼此分離，相當於伺服器和用戶端中的 ViewModel 定義方式。 不建議的作法是跨多個微服務共用通用的整合事件程式庫；這麼做會將這些微服務與單一事件定義資料程式庫結合。 您不會想要這樣做，原因就相同於您不會想要在多個微服務之間共用通用的領域模型：微服務必須是完全自主。

只有幾種程式庫是您應該在微服務之間共用的。 其中一種是最終應用程式區塊的程式庫，例如[事件匯流排用戶端 API](https://github.com/dotnet-architecture/eShopOnContainers/tree/master/src/BuildingBlocks/EventBus)，如同在 eShopOnContainers 中。 另一種是構成工具的程式庫，它們也可以共用為 NuGet 元件，例如 JSON 序列化程式。

## <a name="the-event-bus"></a>事件匯流排

事件匯流排允許微服務之間的發佈/訂閱樣式通訊，而不需要元件明確知道彼此，如圖 6-19 所示。

![顯示基本發佈/訂閱模式的圖表。](./media/integration-event-based-microservice-communications/publish-subscribe-basics.png)

**圖 6-19**。 事件匯流排的發行/訂閱基本概念

上圖顯示微服務 A 發佈至事件匯流排，這會散發到訂閱微服務 B 和 C，而不需要發行者知道訂閱者。 事件匯流排與觀察者模式及發行-訂閱模式有關。

### <a name="observer-pattern"></a>觀察者模式

在[觀察者模式](https://en.wikipedia.org/wiki/Observer_pattern)中，您的主要物件 (稱為可預見物件) 會將相關資訊 (事件) 通知其他有興趣的物件 (稱為觀察者)。

### <a name="publishsubscribe-pubsub-pattern"></a>發佈/訂閱 (Pub/Sub) 模式

[發佈/訂閱模式](https://docs.microsoft.com/previous-versions/msp-n-p/ff649664(v=pandp.10))的目的與觀察者模式相同：您想要在特定事件發生時通知其他服務。 但觀察者和 Pub/Sub 模式之間有一項重要的差異。 在觀察者模式中，廣播會直接從可觀察到觀察者執行，因此它們彼此「知道」。 但在使用 Pub/Sub 模式時，有一個稱為代理程式或訊息代理程式或事件匯流排的第三個元件，發行者和訂閱者都知道它。 因此，在使用 Pub/Sub 模式時，發行者和訂閱者會因為提及的事件匯流排或訊息代理程式而精確地分離。

### <a name="the-middleman-or-event-bus"></a>中間人或事件匯流排

您要如何達到發行者和訂閱者之間的匿名？ 簡單的方法是讓中間人負責處理所有通訊。 事件匯流排便是一個這類的中間人。

事件匯流排通常是由兩個部分組成：

- 抽象或介面。

- 一或多個實作。

在圖 6-19 中，您可以看到從應用程式的觀點而言，事件匯流排只不過是發佈/訂閱通道。 實作這個非同步通訊的方式可能有所不同。 它可能有多種實作，因此您可以根據環境需求 (例如，生產與開發環境)，在兩者之間交換。

在圖 6-20 中，您可以看到事件匯流排的抽象概念，其中具有根據基礎結構傳訊技術 (例如 RabbitMQ、Azure 服務匯流排或其他事件/訊息代理程式) 的多個實作。

![顯示新增事件匯流排抽象層的圖表。](./media/integration-event-based-microservice-communications/multiple-implementations-event-bus.png)

**圖 6-20**。 事件匯流排的多個實作

最好是透過介面定義事件匯流排，因此便可使用數種技術 (例如 RabbitMQ Azure 服務匯流排或其他技術) 來實作。 不過，如先前所提及，使用您自己的抽象 (事件匯流排介面) 只適合在您必須抽象所支援的基本事件匯流排功能時。 如果您需要更豐富的服務匯流排功能，可能應該使用您慣用的商業服務匯流排所提供的 API 和抽象，而不是自己的抽象。

### <a name="defining-an-event-bus-interface"></a>定義事件匯流排介面

讓我們從事件匯流排界面的一些程式碼，以及探索用途的可能的實作為著手。 介面應該是泛型且簡單，如同下列介面。

```csharp
public interface IEventBus
{
    void Publish(IntegrationEvent @event);

    void Subscribe<T, TH>()
        where T : IntegrationEvent
        where TH : IIntegrationEventHandler<T>;

    void SubscribeDynamic<TH>(string eventName)
        where TH : IDynamicIntegrationEventHandler;

    void UnsubscribeDynamic<TH>(string eventName)
        where TH : IDynamicIntegrationEventHandler;

    void Unsubscribe<T, TH>()
        where TH : IIntegrationEventHandler<T>
        where T : IntegrationEvent;
}
```

`Publish` 方法很直接明瞭。 事件匯流排會將傳遞給它的整合事件，廣播到任何微服務或甚至是訂閱該事件的外部應用程式。 這個方法由發行事件的微服務所使用。

`Subscribe` 方法 (您可以有根據引數而定的數種實作) 是由想要收到事件的微服務所使用。 這個方法有兩個引數。 第一個是要訂閱的整合事件 (`IntegrationEvent`)。 第二個引數是整合事件處理常式 (或回呼方法)，名為 `IIntegrationEventHandler<T>`，且將在接收者微服務取得該整合事件訊息時執行。

## <a name="additional-resources"></a>其他資源

一些生產環境就緒的訊息解決方案：

- **Azure 服務匯流排** \
  <https://docs.microsoft.com/azure/service-bus-messaging/>
  
- **NServiceBus** \
  <https://particular.net/nservicebus>
  
- **MassTransit** \
  <https://masstransit-project.com/>

> [!div class="step-by-step"]
> [上一個](database-server-container.md) 
> [下一步](rabbitmq-event-bus-development-test-environment.md)
