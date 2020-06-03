---
title: 針對開發或測試環境使用 RabbitMQ 實作事件匯流排
description: 容器化 .NET 應用程式的 .NET 微服務架構 | 針對開發或測試環境使用 RabbitMQ 實作整合事件的事件匯流排傳訊。
ms.date: 10/02/2018
ms.openlocfilehash: 1af72d18825eb610d6900178205450e2c2e34c25
ms.sourcegitcommit: 5280b2aef60a1ed99002dba44e4b9e7f6c830604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84306886"
---
# <a name="implementing-an-event-bus-with-rabbitmq-for-the-development-or-test-environment"></a>針對開發或測試環境使用 RabbitMQ 實作事件匯流排

首先您應該知道，如果您根據容器中所執行的 RabbitMQ 來建立自訂事件匯流排 (如同 eShopOnContainers 應用程式的做法)，則只能用於開發和測試環境。 請勿將它用於生產環境，除非您將它建立為生產就緒服務匯流排的一部分。 簡單的自訂事件匯流排可能會遺失許多商業服務匯流排所具備並可供生產環境使用的重要功能。

EShopOnContainers 中的其中一個事件匯流排自訂建立，基本上是使用 RabbitMQ API 的程式庫。 （有另一個以 Azure 服務匯流排為基礎的執行）。

使用 RabbitMQ 實作事件匯流排可讓微服務訂閱事件、發行事件和接收事件，如圖 6-21 所示。

![顯示訊息寄件者和訊息接收者之間 RabbitMQ 的圖表。](./media/rabbitmq-event-bus-development-test-environment/rabbitmq-implementation.png)

**圖 6-12。** 事件匯流排的 RabbitMQ 實作

RabbitMQ 的功能是訊息發行者與訂閱者之間的媒介，用來處理散發。 在程式碼中，EventBusRabbitMQ 類別會實作泛型 IEventBus 介面。 這是以相依性插入為基礎，因此您可以從此開發/測試版本切換至生產版本。

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Implementation using RabbitMQ API
    //...
}
```

範例開發/測試事件匯流排的 RabbitMQ 實作是未定案程式碼。 它必須處理 RabbitMQ 伺服器的連接，並提供程式碼將訊息事件發行到佇列。 它也必須實作每個事件類型之整合事件處理常式集合的字典，這些事件類型對每個接收者微服務的具現化和訂閱可能都不同，如圖 6-21 所示。

## <a name="implementing-a-simple-publish-method-with-rabbitmq"></a>使用 RabbitMQ 實作簡單的發行方法

下列程式碼是簡化****** 版本的 RabbitMQ 事件匯流排實作，目的是展示整個情節。 您並不會真的這樣處理連線。 若要查看完整的實作，請參閱 [dotnet-architecture/eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.cs) 存放庫中的實際程式碼。

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Member objects and other methods ...
    // ...

    public void Publish(IntegrationEvent @event)
    {
        var eventName = @event.GetType().Name;
        var factory = new ConnectionFactory() { HostName = _connectionString };
        using (var connection = factory.CreateConnection())
        using (var channel = connection.CreateModel())
        {
            channel.ExchangeDeclare(exchange: _brokerName,
                type: "direct");
            string message = JsonConvert.SerializeObject(@event);
            var body = Encoding.UTF8.GetBytes(message);
            channel.BasicPublish(exchange: _brokerName,
                routingKey: eventName,
                basicProperties: null,
                body: body);
       }
    }
}
```

eShopOnContainers 應用程式中發行方法的[實際程式碼](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.cs)可透過使用 [Polly](https://github.com/App-vNext/Polly) 重試原則來改進，該原則會在 RabbitMQ 容器未就緒時，重試工作特定次數。 當 docker-compose 正在啟動容器時，就會發生此情況；例如，RabbitMQ 容器可能會比其他容器更慢啟動。

如前所述，RabbitMQ 中有許多可能的組態，因此這段程式碼只應該用於開發/測試環境。

## <a name="implementing-the-subscription-code-with-the-rabbitmq-api"></a>使用 RabbitMQ API 實作訂閱程式碼

如同發行程式碼，下列程式碼是 RabbitMQ 之事件匯流排實作的一部分簡化。 同樣地，除非您想要改進，否則您通常不需要將它變更。

```csharp
public class EventBusRabbitMQ : IEventBus, IDisposable
{
    // Member objects and other methods ...
    // ...

    public void Subscribe<T, TH>()
        where T : IntegrationEvent
        where TH : IIntegrationEventHandler<T>
    {
        var eventName = _subsManager.GetEventKey<T>();

        var containsKey = _subsManager.HasSubscriptionsForEvent(eventName);
        if (!containsKey)
        {
            if (!_persistentConnection.IsConnected)
            {
                _persistentConnection.TryConnect();
            }

            using (var channel = _persistentConnection.CreateModel())
            {
                channel.QueueBind(queue: _queueName,
                                    exchange: BROKER_NAME,
                                    routingKey: eventName);
            }
        }

        _subsManager.AddSubscription<T, TH>();
    }
}
```

每個事件類型會有相關的通道以從 RabbitMQ 取得事件。 之後，您可以視需要針對每個通道和事件類型，擁有許多事件處理常式。

Subscribe 方法接受 IIntegrationEventHandler 物件，就像是目前微服務及其相關 IntegrationEvent 物件中的回呼方法。 此程式碼接著會將該事件處理常式新增至事件處理常式清單，每個整合事件類型可根據每個用戶端微服務擁有這些事件處理常式。 如果用戶端程式碼尚未訂閱事件，程式碼會建立事件類型的通道，以便在從任何其他服務發行該事件時，可從 RabbitMQ 接收推送樣式的事件。

如先前所述，在 eShopOnContainers 中實作用的事件匯流排只會處理主要案例，而不會準備好用於生產環境。

針對生產案例，請檢查下列其他資源（特定于 RabbitMQ）和[微服務區段之間的執行事件型通訊](./integration-event-based-microservice-communications.md#additional-resources)。

## <a name="additional-resources"></a>其他資源

支援 RabbitMQ 的生產環境就緒解決方案。

- **EasyNetQ** -開放原始碼 .net API Client for RabbitMQ \
  <https://easynetq.com/>

- **MassTransit** \
  <https://masstransit-project.com/>
  
> [!div class="step-by-step"]
> [上一個](integration-event-based-microservice-communications.md) 
> [下一步](subscribe-events.md)
