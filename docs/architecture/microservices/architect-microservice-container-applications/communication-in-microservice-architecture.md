---
title: 微服務架構中的通訊
description: 探索微服務之間的不同通訊方式，並了解同步和非同步方式的影響。
ms.date: 01/30/2020
ms.openlocfilehash: f1a240609b898fe8f365c39ba0c95f486377c445
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169254"
---
# <a name="communication-in-a-microservice-architecture"></a>微服務架構中的通訊

在單一處理序上執行的整合型應用程式中，元件會使用語言層級方法或函式呼叫來彼此叫用。 如果您是使用程式碼 (例如 `new ClassName()`) 來建立物件，這些元件就可以強固結合；或者，如果您是透過參考抽象概念 (而不是具象的物件執行個體) 來使用相依性插入，即可以獨立方式呼叫這些元件。 無論何種情況，物件都會在相同的處理序內執行。 從整合型應用程式變更為微服務應用程式時，最大的挑戰在於變更通訊機制。 從服務的內含式方法呼叫直接轉換成 RPC 呼叫時，會導致過度對話，且在分散式環境中的通訊效率不佳。 除了眾所周知的分散式系統設計挑戰之外，還要考慮 [Fallacies of distributed computing](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing) (分散式計算的謬論)，其中列出開發人員從整合型設計進展至分散式設計時通常會有的假設。

對此，您可以採用好幾種解決方案。 其中一個解決方法包括盡量隔離商務微服務。 接著，您可以使用內部微服務之間的非同步通訊，並以廣泛通訊取代細部通訊 (其為物件之間的常見處理序間通訊)。 若要進行這項作業，您可以將呼叫分組，並將多個內部呼叫的彙總結果資料傳回給用戶端。

微服務應用程式是一種分散式系統，其執行於多個處理序或服務上，通常甚至跨多部伺服器或主機。 每個服務執行個體通常就是一個處理序。 因此，服務必須使用處理序間的通訊協定來互動，例如 HTTP、AMQP 或 TCP 這類二進位通訊協定 (根據每個服務的本質而定)。

微服務社群推廣一種 [Smart Endpoints and Dumb Pipes](https://simplicable.com/new/smart-endpoints-and-dumb-pipes) (智慧端點和傻瓜管道) 的哲學。此標語主要是鼓勵「高內聚、低結合」的設計；亦即盡量分離微服務，並使其在單一的微服務內盡可能地縝密結合。 如前所述，每個微服務擁有它自己的資料和網域邏輯。 但一般來說，由端對端應用程式組成的微服務是單純使用 REST 通訊 (而不是 WS-\* 這類複雜通訊協定) 與彈性的事件驅動通訊 (而不是集中式的商務程序協調器) 來編寫。

兩個最常用的通訊協定是資源 API 的 HTTP 要求/回應 (當查詢是最重要的作業時)，以及跨多個微服務通訊更新時的輕量型非同步傳訊。 下列各節會進行詳細說明。

## <a name="communication-types"></a>通訊類型

用戶端和服務可以透過許多不同通訊類型來進行通訊，每種方式鎖定的案例與目標都不同。 一開始，我們可以將這些通訊類型以兩個軸來分類。

第一個軸定義通訊協定為同步或非同步：

- 同步通訊協定： HTTP 是同步的通訊協定。 用戶端傳送要求，並等候服務的回應。 其獨立於用戶端程式碼的執行，並可能是同步 (會封鎖執行緒) 或非同步 (不封鎖執行緒，且回應最後會抵達回呼)。 此處的重點是通訊協定 (HTTP/HTTPS) 為同步，且用戶端程式碼只能在收到 HTTP 伺服器回應時繼續工作。

- 非同步通訊協定： 其他通訊協定會使用非同步的訊息，例如 AMQP (許多作業系統和雲端環境支援的通訊協定)。 用戶端程式碼或訊息寄件者通常不會等候回應。 而只會在傳送訊息給 RabbitMQ 佇列或任何其他訊息代理程式時傳送訊息。

第二個軸則定義通訊具有單一接收者或多個接收者：

- 單一接收者： 每個要求都必須由一個接收者或服務來處理。 這種通訊的其中一個範例是 [Command pattern](https://en.wikipedia.org/wiki/Command_pattern) (命令模式)。

- 多個接收者： 每個要求可以由零到多個接收者來處理。 這種類型的通訊必須是非同步的。 其中的範例是用於[事件驅動架構](https://microservices.io/patterns/data/event-driven-architecture.html)這類模式的[發佈/訂閱](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern)機制。 這是以透過事件在多個微服務之間散佈資料更新時的事件匯流排介面或訊息代理程式為基礎；通常您可以使用[主題和訂閱](/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)，並透過服務匯流排或類似 [Azure 服務匯流排](https://azure.microsoft.com/services/service-bus/)的構件來實作。

微服務應用程式通常會使用這些通訊樣式的組合。 叫用一般 Web API HTTP 服務時，最常見的類型是使用 HTTP/HTTPS 等同步通訊協定的單一接收者通訊。 微服務通常也會使用傳訊通訊協定，來進行微服務之間的非同步通訊。

這些軸可讓您對可能的通訊機制一目了然，但它們不是建置微服務時的重要考量。 在整合微服務時，用戶端執行緒執行的非同步本質或者所選通訊協定的非同步本質兩者都不是重點。 真正的重點** 在於您要能夠以非同步方式整合微服務，同時保持微服務的獨立性，如下節所述。

## <a name="asynchronous-microservice-integration-enforces-microservices-autonomy"></a>非同步的微服務整合可強化微服務的自主性

如前所述，建置微服務應用程式的重點是整合微服務的方式。 在理想情況下，您應該盡量將內部微服務之間的通訊降到最低。 微服務之間的通訊越少越好。 但在許多情況下，您仍必須整合微服務。 當您要執行上述作業時，重要的規則是微服務之間的通訊應該為非同步。 這不代表您必須使用特定的通訊協定 (例如，非同步傳訊與同步 HTTP)。 而是代表微服務之間的通訊應該僅以非同步資料散佈的方式來進行，但不要試圖仰賴其他屬於初始服務之 HTTP 要求/回應作業的內部微服務。

請盡可能不要仰賴多個微服務之間的同步通訊 (要求/回應)，甚至連查詢也不要仰賴於此。 每個微服務的目標是保持自主並供用戶端取用，即使屬於端對端應用程式一部分的其他服務已關機或狀況不佳時亦同。 如果您設想要從某個微服務呼叫其他微服務 (例如，執行資料查詢的 HTTP 要求)，以便能夠回應用戶端應用程式，這種架構在某些微服務故障時就無法復原。

此外，如圖 4-15 的第一個部分所示，如果微服務之間具有 HTTP 相依性 (例如使用 HTTP 要求鏈結建立長要求/回應循環時)，不只會導致微服務無法自主，一旦該鏈結中的其中一個服務無法順利執行時，也會影響其效能。

如果微服務 (例如查詢要求) 之間的同步相依性越高，用戶端應用程式的整體回應時間就會越糟。

![顯示跨微服務的三種通訊類型的圖表。](./media/communication-in-microservice-architecture/sync-vs-async-patterns-across-microservices.png)

**圖 4-15**： 微服務之間的通訊模式和反向模式

如上圖所示，在同步通訊中，在服務用戶端要求時，微服務之間會建立「鏈」要求。 這是反模式。 在非同步通訊中，微服務會使用非同步訊息或 http 輪詢與其他微服務進行通訊，但用戶端要求會立即處理。

如果您的微服務需要引發另一個微服務的其他動作，請盡量不要同步執行該動作，也不要與原始微服務要求及回覆作業一併執行。 請改為以非同步方式執行 (使用非同步傳訊或整合事件、佇列等)。 但是，請盡量不要與原始的同步要求及回覆作業同步叫用動作。

最後 (這是建置微服務時大部分問題發生的時候)，如果您初始的微服務需要使用原本由其他微服務擁有的資料時，請避免對該資料提出同步要求。 反之，請使用最終一致性 (通常使用整合事件來進行，如接下來的章節中所述)，將該資料 (僅所需的屬性) 複製或散佈到初始服務的資料庫中。

如稍早在 [識別每個微服務區段的領域模型界限](identify-microservice-domain-model-boundaries.md) 中所述，在數個微服務之間複製某些資料不是不正確的設計，相反地，當您這麼做時，您可以將資料轉譯為特定語言或該其他網域或系結內容的詞彙。 例如，在 [eShopOnContainers 應用程式](https://github.com/dotnet-architecture/eShopOnContainers) 中，您有一個名為 `identity-api` 的微服務，它會使用名為的實體來處理大部分的使用者資料 `User` 。 但是，當您需要將使用者的相關資料儲存在微服務中時 `Ordering` ，您會將它儲存為另一個名為的實體 `Buyer` 。 `Buyer`實體與原始實體共用相同的身分識別 `User` ，但它可能只會有網域所需的幾個屬性 `Ordering` ，而非整個使用者設定檔。

您可以使用任何通訊協定來進行通訊，並以非同步方式跨微服務散佈資料，來保持最終一致性。 如前所述，您可以使用事件匯流排或訊息代理程式來運用整合事件；甚至還可以改輪詢其他服務來使用 HTTP。 它並不重要。 重要的規則是不要讓微服務之間建立同步相依性。

下列各節說明您可以考慮在微服務應用程式中使用的多種通訊樣式。

## <a name="communication-styles"></a>通訊樣式

依據所要使用的通訊類型而定，您可以搭配許多通訊協定和選擇來進行通訊。 如果您是使用以同步要求/回應為基礎的通訊機制，則 HTTP 和 REST 這類通訊協定是最常見的方法，尤其是當您要在 Docker 主機或微服務叢集之外發佈服務時。 如果您要在內部服務 (Docker 主機或微服務叢集內) 之間進行通訊，也可以使用二進位格式的通訊機制 (例如使用 TCP 和二進位格式的 WCF)。 或者，您可以使用非同步訊息通訊機制，例如 AMQP。

還有很多種訊息格式可能更有效率，如 JSON 或 XML，甚至二進位格式。 如果您選擇的二進位格式不是標準格式，則不建議您使用該格式來公開發佈服務。 您可以在微服務之間的內部通訊使用非標準格式。 例如，在 Docker 主機或微服務叢集 (如 Docker 協調器) 內的微服務之間進行通訊時，或針對可與微服務通訊的專屬用戶端應用程式，您可以這樣做。

### <a name="requestresponse-communication-with-http-and-rest"></a>使用 HTTP 和 REST 的要求/回應通訊

當用戶端使用要求/回應通訊時，它會將要求傳送給服務，然後由服務處理要求，並傳回回應。 要求/回應通訊非常適合用來查詢用戶端應用程式的即時 UI (即時的使用者介面) 資料。 因此，在微服務架構中，您可能會針對大部分查詢使用這種通訊機制，如圖 4-16 所示。

![顯示即時查詢和更新之要求/回應批註的圖表。](./media/communication-in-microservice-architecture/request-response-comms-live-queries-updates.png)

**圖 4-16**： 使用 HTTP 要求/回應通訊 (同步或非同步)

當用戶端使用要求/回應通訊時，它會假設回應很快抵達，通常少於一秒或最多幾秒鐘的時間。 針對回應延遲，您需要依據[訊息模式](/azure/architecture/patterns/category/messaging)和[技術](https://en.wikipedia.org/wiki/Message-oriented_middleware)來實作非同步通訊；我們將在下節說明此種不同的方法。

要求/回應通訊的熱門架構樣式是 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer)。 這種方法是以 [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) 通訊協定為基礎並與其緊密結合，同時採用 HTTP 動詞命令，例如 GET、POST 和 PUT。 建立服務時，REST 是最常用的架構通訊方法。 開發 ASP.NET Core Web API 服務時，您可以實作 REST 服務。

將 HTTP REST 服務作為您的介面定義語言時，還有其他附加價值。 比方說，如果您使用 [Swagger 中繼資料](https://swagger.io/)來描述服務 API，即可使用工具來產生用戶端 Stub，以直接探索及取用您的服務。

### <a name="additional-resources"></a>其他資源

- **聖馬丁 Fowler。Richardson 成熟度模型** ： REST 模型的描述。 \
  <https://martinfowler.com/articles/richardsonMaturityModel.html>

- **Swagger** 官方網站。 \
  <https://swagger.io/>

### <a name="push-and-real-time-communication-based-on-http"></a>以 HTTP 為基礎的推送和即時通訊

另一個可能性 (通常用途與 REST 不同) 是使用 [ASP.NET SignalR](https://www.asp.net/signalr) 這類更高階 Framework 和 [WebSockets](https://en.wikipedia.org/wiki/WebSocket) 等通訊協定的即時和一對多通訊。

如圖 4-17 所示，即時 HTTP 通訊表示您可以讓伺服器程式碼在資料可用時將內容推送至連線的用戶端，而不需要讓伺服器等候用戶端要求新的資料。

![此圖顯示以 SignalR 為基礎的推播和即時批註。](./media/communication-in-microservice-architecture/one-to-many-communication.png)

**圖 4-17**： 一對一的即時非同步訊息通訊

SignalR 很適合用來完成將內容從後端伺服器推送到用戶端的即時通訊。 由於是即時通訊，因此用戶端應用程式幾乎會立即顯示變更。 一般來說，其會由 WebSockets 這類通訊協定使用許多 Websocket 連線 (每個用戶端一個) 來進行處理。 典型的範例是：某個服務同時向許多用戶端 Web 應用程式傳達運動遊戲之分數變更的情況。

>[!div class="step-by-step"]
>[上一個](direct-client-to-microservice-communication-versus-the-api-gateway-pattern.md) 
>[下一步](asynchronous-message-based-communication.md)
