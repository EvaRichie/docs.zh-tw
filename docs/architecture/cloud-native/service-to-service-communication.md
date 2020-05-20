---
title: 服務對服務通訊
description: 瞭解後端雲端原生微服務如何與其他後端微服務通訊。
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: dec06cc28ac177381b882f9e441e19e5c51bd5ad
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83613703"
---
# <a name="service-to-service-communication"></a>服務對服務通訊

從前端用戶端移動之後，我們現在會解決後端微服務彼此通訊的情形。

在建立雲端原生應用程式時，您會想要區分後端服務彼此通訊的方式。 在理想的情況下，服務間的通訊越少越好。 不過，不一定可以避免使用，因為後端服務通常會依賴另一個來完成操作。

有數個廣為接受的方法可執行跨服務通訊。 *通訊互動的類型*通常會決定最佳的方法。

請考慮下列互動類型：

- *查詢*–呼叫微服務需要來自所呼叫微服務的回應，例如「嘿，為我提供指定客戶識別碼的買方資訊」。

- *命令*–呼叫微服務需要另一個微服務來執行動作，但不需要回應，例如「嘿，只要寄出此訂單」。

- *事件*–微服務（稱為「發行者」）會引發狀態已變更或已發生動作的事件。 其他有興趣的微服務稱為「訂閱者」，可以適當地回應事件。 「發行者」和「訂閱者」彼此不知道。

微服務系統通常會在執行需要跨服務互動的作業時，使用這些互動類型的組合。 讓我們仔細看一下每一種方法，以及您可以如何執行它們。

## <a name="queries"></a>查詢

許多時候，一個微服務可能需要*查詢*另一個，而需要立即回應才能完成作業。 購物籃微服務可能需要產品資訊和價格，才能將專案新增至購物籃。 有數種方法可以執行查詢作業。

### <a name="requestresponse-messaging"></a>要求/回應傳訊

執行此案例的其中一個選項是呼叫後端微服務，對它需要查詢的微服務提出直接的 HTTP 要求，如圖4-8 所示。

![直接 HTTP 通訊](./media/direct-http-communication.png)

**圖 4-8**。 直接 HTTP 通訊

雖然微服務之間的直接 HTTP 呼叫相對較簡單，但還是應採取措施來將這種作法降到最低。 首先，這些呼叫一律是*同步*的，而且會封鎖作業，直到傳回結果或要求超時為止。 獨立、獨立的服務、能夠獨立開發和經常部署的功能，現在會彼此結合。 隨著微服務增加，其架構優勢也會降低。

針對某些系統，執行對另一個微服務進行單一直接 HTTP 呼叫的不常要求可能是可接受的。 不過，不建議對多個微服務叫用直接 HTTP 呼叫的高容量呼叫。 它們可以增加延遲，並對系統的效能、擴充性和可用性造成負面影響。 更糟的是，一長串的直接 HTTP 通訊可能會導致同步微服務呼叫的深度和複雜鏈，如圖4-9 所示：

![連結 HTTP 查詢](./media/chaining-http-queries.png)

**圖 4-9**。 連結 HTTP 查詢

您當然可以想像上圖所示的設計風險。 如果步驟3失敗，會發生什麼事 \# ？ 或步驟 \# 8 失敗？ 如何復原？ 如果步驟 \# 6 因為基礎服務忙碌而變慢，該怎麼辦？ 您要如何繼續？ 即使所有作業都正常運作，您也可以考慮此呼叫會產生的延遲，這是每個步驟的延遲總和。

上圖中的大量結合性建議服務無法以最佳模式進行模型化。 它會 behoove 小組來重新審視其設計。

### <a name="materialized-view-pattern"></a>具體化檢視模式

移除微服務的結合常用的選項是 [[具體化視圖模式](https://docs.microsoft.com/azure/architecture/patterns/materialized-view)]。 使用此模式時，微服務會儲存其本身的本機、反正規化的資料複本（由其他服務所擁有）。 除了購物籃微服務查詢產品目錄和定價微服務，它還會維護自己的本機資料複本。 此模式可排除不必要的結合性並改善可靠性和回應時間。 整個作業會在單一進程中執行。 我們將在第5章探討此模式和其他資料顧慮。

### <a name="service-aggregator-pattern"></a>服務匯總工具模式

排除微服務對微服務結合的另一個選項是匯總程式[微服務](https://devblogs.microsoft.com/cesardelatorre/designing-and-implementing-api-gateways-with-ocelot-in-a-microservices-and-container-based-architecture/)，如圖4-10 中的紫色所示。

![匯總工具服務](./media/aggregator-service.png)

**圖 4-10**： 匯總工具微服務

此模式會隔離呼叫多個後端微服務的作業，並將其邏輯集中到專門的微服務。  上圖中的紫色結帳匯總工具微服務會協調結帳作業的工作流程。 其中包括以排序次序呼叫數個後端微服務。 工作流程中的資料會匯總並傳回給呼叫者。 雖然它仍然會執行直接的 HTTP 呼叫，但匯總工具微服務會減少後端微服務間的直接相依性。

### <a name="requestreply-pattern"></a>要求/回復模式

將同步 HTTP 訊息分離的另一種方法是[要求-回復模式](https://www.enterpriseintegrationpatterns.com/patterns/messaging/RequestReply.html)，它會使用佇列通訊。 使用佇列的通訊一律是單向通道，其中產生者會傳送訊息和接收它。 使用此模式時，會同時執行要求佇列和回應佇列，如圖4-11 所示。

![要求-回復模式](./media/request-reply-pattern.png)

**圖 4-11**： 要求-回復模式

在這裡，訊息產生者會建立包含唯一相互關聯識別碼的查詢訊息，並將其放入要求佇列中。 取用服務會清除訊息、加以處理，並將回應放入具有相同相互關聯識別碼的回應佇列中。 生產者服務會清除訊息，並與相互關聯識別碼相符並繼續處理。 我們將在下一節詳細討論佇列。

## <a name="commands"></a>命令

另一種通訊互動類型是*命令*。 微服務可能需要另一個微服務來執行動作。 訂購微服務可能需要出貨微服務，才能建立已核准訂單的出貨。 在圖4-12 中，一個稱為生產者的微服務會將訊息傳送給另一個微服務，也就是取用者，將它命令來執行某個動作。

![與佇列的命令互動](./media/command-interaction-with-queue.png)

**圖 4-12**. 與佇列的命令互動

最常見的情況是，產生者不需要回應，而且可能會*引發並忘記*訊息。 如果需要回復，取用者會將個別的訊息傳回給另一個通道上的生產者。 命令訊息最適合透過訊息佇列以非同步方式傳送。 輕量訊息代理程式所支援。 在上圖中，請注意佇列如何分隔和分離這兩項服務。

「訊息佇列」是一種中繼結構，生產者和取用者會透過它來傳遞訊息。 佇列會執行非同步點對點訊息模式。 產生者知道需要傳送命令和適當路由的位置。 佇列保證訊息只由其中一個從通道讀取的取用者實例處理。 在此案例中，生產者或取用者服務可以相應放大，而不會影響另一個。 同樣地，各端的技術可能會不同，這表示我們可能會有 JAVA 微服務呼叫[Golang](https://golang.org)微服務。

在第1章中，我們討論了*支援服務*。 支援服務是雲端原生系統所依賴的輔助資源。 訊息佇列是支援服務。 Azure 雲端支援兩種類型的訊息佇列，可供您的雲端原生系統用來執行命令訊息： Azure 儲存體佇列和 Azure 服務匯流排佇列。

### <a name="azure-storage-queues"></a>Azure 儲存體佇列

Azure 儲存體佇列提供簡單的佇列基礎結構，以快速、實惠且受到 Azure 儲存體帳戶的支援。

[Azure 儲存體佇列](https://docs.microsoft.com/azure/storage/queues/storage-queues-introduction)的功能是以 REST 為基礎的佇列機制，具備可靠且持續性的訊息。 它們提供最基本的功能集，但成本低廉，並儲存數百萬則訊息。 其容量範圍上限為 500 TB。 單一訊息的大小最高可達 64 KB。

您可以透過使用 HTTP 或 HTTPS 的已驗證呼叫，從世界各地存取訊息。 儲存體佇列可相應放大為大量的並行用戶端，以處理流量尖峰。

話雖如此，服務的限制如下：

- 不保證訊息順序。

- 訊息只能保存七天，才會自動移除。

- 無法支援狀態管理、重複偵測或交易。

圖4-13 顯示 Azure 儲存體佇列的階層。

![儲存體佇列階層](./media/storage-queue-hierarchy.png)

**圖 4-13**. 儲存體佇列階層

在上圖中，請注意儲存體佇列如何將其訊息儲存在基礎 Azure 儲存體帳戶中。

對於開發人員，Microsoft 提供數個用戶端和伺服器端程式庫來處理儲存體佇列。 支援大部分的主要平臺，包括 .NET、JAVA、JavaScript、Ruby、Python 和 Go。 開發人員絕對不應直接與這些程式庫通訊。 這麼做會將您的微服務程式代碼緊密地帶到 Azure 儲存體佇列服務。 更好的作法是將 API 的執行細節隔離。 引進會公開一般作業並封裝具體程式庫的 intermediation 層或中繼 API。 這種鬆散結合可讓您交換另一個佇列服務，而不需要對主線服務程式代碼進行變更。

Azure 儲存體佇列是在您的雲端原生應用程式中執行命令訊息的經濟實惠選項。 特別是當佇列大小超過 80 GB 時，或簡單的功能集是可接受的。 您只需支付訊息的儲存空間，沒有固定的每小時費用。

### <a name="azure-service-bus-queues"></a>Azure 服務匯流排佇列

如需更複雜的訊息處理需求，請考慮 Azure 服務匯流排的佇列。

坐在強大的訊息基礎結構上， [Azure 服務匯流排](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)支援代理*訊息模型*。 訊息會可靠地儲存在 broker （佇列）中，直到取用者收到為止。 佇列保證先進先出（FIFO）訊息傳遞，遵循訊息新增至佇列的順序。

訊息的大小可能會大很多，最高可達 256 KB。 訊息會保存在佇列中一段無限期的時間。 服務匯流排不只支援以 HTTP 為基礎的呼叫，也會提供[AMQP 通訊協定](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-amqp-overview)的完整支援。 AMQP 是跨廠商的開放式標準，可支援二進位通訊協定和較高程度的可靠性。

服務匯流排提供一組豐富的功能，包括[交易支援](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-transactions)和[重複的偵測功能](https://docs.microsoft.com/azure/service-bus-messaging/duplicate-detection)。 佇列保證每個訊息「最多一次傳遞」。 它會自動捨棄已經傳送的訊息。 如果產生者不確定，它可以重新傳送相同的訊息，服務匯流排保證只會處理一個複本。 重複偵測可讓您不必建立額外的基礎結構配管。

另外兩個企業功能是分割和會話。 傳統服務匯流排佇列是由單一訊息代理程式處理，並儲存在單一訊息存放區中。 但是，[服務匯流排資料分割](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-partitioning)會將佇列散佈到多個訊息代理程式和訊息存放區。 整體輸送量不再受限於單一訊息代理程式或訊息存放區的效能。 訊息存放區暫時中斷不會導致分割的佇列無法使用。

[服務匯流排會話](https://codingcanvas.com/azure-service-bus-sessions/)提供一種方式來分組相關的訊息。 假設有一個工作流程案例，也就是必須一起處理訊息，並在結尾完成作業。 若要利用，必須為佇列明確啟用會話，而且每個相關的 messaged 都必須包含相同的會話識別碼。

不過，有一些重要的警告：服務匯流排佇列大小限制為 80 GB，這比儲存佇列中可用的數目小很多。 此外，服務匯流排佇列會產生每個作業的基本成本和費用。

圖4-14 概述服務匯流排佇列的高階架構。

![服務匯流排佇列](./media/service-bus-queue.png)

**圖 4-14**. 服務匯流排佇列

在上圖中，請注意點對點關聯性。 相同提供者的兩個實例會佇列訊息至單一服務匯流排佇列。 每個訊息只會由右邊的三個取用者實例的其中一個使用。 接下來，我們會討論如何執行訊息，其中不同的取用者可能會對相同的訊息感興趣。

## <a name="events"></a>事件

「訊息佇列」是一種有效的方法，可讓產生者以非同步方式傳送訊息給取用者的通訊。 不過，當有*許多不同*的取用者對相同訊息感興趣時，會發生什麼事？ 每個取用者的專用訊息佇列不會適當地進行調整，因而變得難以管理。

為了解決這種情況，我們會移至第三種類型的訊息互動，也就是*事件*。 一個微服務宣佈已發生動作。 其他微服務（如果有興趣）回應動作或事件。

事件處理是兩個步驟的程式。 針對指定的狀態變更，微服務會將事件發佈到訊息代理程式，使其可供任何其他感興趣的微服務使用。 有興趣的微服務會在訊息代理程式中訂閱事件時收到通知。 您可以使用[發佈/訂閱](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber)模式來執行以[事件為基礎的通訊](https://docs.microsoft.com/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/integration-event-based-microservice-communications)。

圖4-15 顯示的購物籃微服務發佈了兩個其他微服務訂閱的事件。

![事件驅動的訊息](./media/event-driven-messaging.png)

**圖 4-15**： 事件驅動的訊息

請注意位於通道中央的*事件匯流排*元件。 這是一個自訂類別，它會封裝訊息代理程式，並將它與基礎應用程式分離。 訂購和清查微服務會獨立操作事件，而不知道彼此或購物籃微服務。 當註冊的事件發佈至事件匯流排時，它們會對它採取動作。

有了事件，我們會從佇列技術移至*主題*。 [主題](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)與佇列類似，但支援一對多訊息模式。 一個微服務會發佈訊息。 多個訂閱微服務可以選擇接收該訊息並採取行動。 圖4-16 顯示主題架構。

![主題架構](./media/topic-architecture.png)

**圖 4-16**： 主題架構

在上圖中，發行者會將訊息傳送至主題。 最後，訂閱者會從訂用帳戶接收訊息。 在中間，主題會根據一組*規則*（以暗藍色方塊顯示），將訊息轉送至訂閱。 規則會作為將特定訊息轉寄至訂用帳戶的篩選準則。 在這裡，"CreateOrder" 事件會傳送到訂用帳戶 \# 1 和訂用帳戶 \# 3，但不會傳送到訂用帳戶 \# 2。 「OrderCompleted」事件會傳送到訂用帳戶 \# 2 和訂用帳戶 \# 3。

Azure 雲端支援兩種不同的主題服務： Azure 服務匯流排主題和 Azure EventGrid。

### <a name="azure-service-bus-topics"></a>Azure 服務匯流排主題

在 Azure 服務匯流排佇列的相同健全代理訊息模型上， [Azure 服務匯流排主題](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)。 主題可以接收來自多個獨立發行者的訊息，並將訊息傳送到最多2000的訂閱者。 您可以在執行時間動態加入或移除訂閱，而不需要停止系統或重新建立主題。

許多來自 Azure 服務匯流排佇列的先進功能也適用于主題，包括[重複的偵測](https://docs.microsoft.com/azure/service-bus-messaging/duplicate-detection)和[交易支援](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-transactions)。 根據預設，服務匯流排主題是由單一訊息代理程式處理，並儲存在單一訊息存放區中。 但是，[服務匯流排資料分割](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-partitioning)會將主題分散到許多訊息代理程式和訊息存放區來調整其規模。

[排定的訊息傳遞](https://docs.microsoft.com/azure/service-bus-messaging/message-sequencing)會標記特定時間進行處理的訊息。 訊息將不會出現在該時間之前的主題中。 [訊息延遲](https://docs.microsoft.com/azure/service-bus-messaging/message-deferral)可讓您將訊息的抓取延後一段時間。 這兩者通常用於工作流程處理案例，其中的作業會以特定連續處理。 您可以延後處理已接收的訊息，直到先前的工作完成為止。

服務匯流排主題是強大且經過證實的技術，可在您的雲端原生系統中啟用發佈/訂閱通訊。

### <a name="azure-event-grid"></a>Azure Event Grid

雖然 Azure 服務匯流排是具有一組完整企業功能的經過測試的訊息代理程式，但[Azure 事件方格](https://docs.microsoft.com/azure/event-grid/overview)是此新的孩子。

乍看之下，事件方格看起來就像是另一個以主題為基礎的訊息系統。 不過，它在許多方面都不同。 它著重于事件導向的工作負載，可啟用即時事件處理、深度 Azure 整合和開放平臺-全部都在無伺服器基礎結構上。 它是專為現代雲端原生和無伺服器應用程式所設計

作為*集中式事件後*擋板或管道，事件方格會回應 Azure 資源內和您自己的服務中的事件。

事件通知會發佈至事件方格主題，接著會將每個事件路由至訂用帳戶。 訂閱者對應至訂閱並取用事件。 如同服務匯流排，事件方格支援已*篩選的訂閱者模型*，其中的訂用帳戶會針對它想要接收的事件設定規則。 事件方格可提供快速的輸送量，並保證每秒10000000個事件的傳送速率遠超過 Azure 服務匯流排可以產生的時間。

事件方格的最佳位置是其深入整合到 Azure 基礎結構的網狀架構。 Azure 資源（例如 Cosmos DB）可以將內建事件直接發行到其他感興趣的 Azure 資源，而不需要自訂程式碼。 事件方格可以發佈來自 Azure 訂用帳戶、資源群組或服務的事件，讓開發人員更精細地控制雲端資源的生命週期。 不過，事件方格並不限於 Azure。 它是一個開放式平臺，可使用從應用程式或協力廠商服務發佈的自訂 HTTP 事件，並將事件路由至外部訂閱者。

發佈和訂閱 Azure 資源的原生事件時，不需要撰寫任何程式碼。 透過簡單的設定，您可以將事件從一個 Azure 資源整合到另一個使用主題和訂用帳戶內建的管道。 圖4-17 顯示事件方格的剖析。

![事件方格剖析](./media/event-grid-anatomy.png)

**圖 4-17**： 事件方格剖析

EventGrid 和服務匯流排之間的主要差異在於基礎*訊息交換模式*。

服務匯流排會執行較舊的樣式*提取模型*，下游訂閱者會在其中主動輪詢主題訂用帳戶中的新訊息。 這種方法的優點是，訂閱者可以完全掌控其處理訊息的步調。 它會控制在任何指定時間要處理的訊息和數目。 未讀取的訊息會保留在訂用帳戶中，直到處理為止。 重大缺點是產生事件的時間與將該訊息提取至訂閱者以進行處理的輪詢作業之間的延遲。 此外，持續輪詢下一個事件的額外負荷會耗用資源和金錢。

不過，EventGrid 是不同的。 它會執行*推送模型*，其中事件會以接收的方式傳送至 EventHandlers，提供近乎即時的事件傳遞。 它也會降低成本，因為只有在需要取用事件時才會觸發服務，而不是隨著輪詢而持續使用。 話雖如此，事件處理常式必須處理傳入的負載，並提供節流機制來保護自己免于被淹沒。 許多使用這些事件的 Azure 服務，例如 Azure Functions 和 Logic Apps 會提供自動調整功能，以處理增加的負載。  

事件方格是完全受控的無伺服器雲端服務。 它會根據您的流量動態調整，並只針對實際使用量收費，而不是預先購買的容量。 每月前100000作業是免費的–作業會定義為事件輸入（傳入事件通知）、訂用帳戶傳遞嘗試、管理呼叫，以及依主旨篩選。 使用99.99% 的可用性，EventGrid 可保證在24小時期間內傳遞事件，並提供不成功傳遞的內建重試功能。 未傳遞的訊息可以移至「寄不出的信件」佇列進行解析。  不同于 Azure 服務匯流排，事件方格已針對快速效能進行微調，且不支援已排序訊息、交易和會話等功能。

### <a name="streaming-messages-in-the-azure-cloud"></a>在 Azure 雲端中串流處理訊息

Azure 服務匯流排和事件方格針對公開單一獨立事件的應用程式提供絕佳的支援，例如新檔已插入 Cosmos DB。 但是，如果您的雲端原生系統需要處理*相關事件的資料流程*，該怎麼辦？ [事件資料流程](https://docs.microsoft.com/archive/msdn-magazine/2015/february/microsoft-azure-the-rise-of-event-stream-oriented-systems)較複雜。 它們通常是依時間排序、相互關聯，而且必須以群組的方式處理。

[Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)是一種資料串流平臺和事件內嵌服務，可收集、轉換及儲存事件。 它會微調以捕捉串流資料，例如從遙測內容發出的連續事件通知。 此服務具有高度擴充性，而且每秒可儲存和[處理數百萬個事件](https://docs.microsoft.com/azure/event-hubs/event-hubs-about)。 如圖4-18 所示，這通常是事件管線的前端，可將內嵌資料流程從事件耗用量分離出來。

![Azure 事件中樞](./media/azure-event-hub.png)

**圖 4-18**. Azure 事件中樞

事件中樞支援低延遲和可設定的保留時間。 不同于佇列和主題，事件中樞會在取用者讀取事件資料之後加以保留。 這項功能可讓其他資料分析服務（內部和外部）重新執行資料，以進行進一步的分析。 儲存在事件中樞中的事件只會在保留期限到期時刪除（預設為一天，但可設定）。

事件中樞支援常見的事件發佈通訊協定，包括 HTTPS 和 AMQP。 它也支援 Kafka 1.0。 [現有的 Kafka 應用程式可以使用 Kafka 通訊協定與事件中樞通訊](https://docs.microsoft.com/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)，以提供管理大型 Kafka 叢集的替代方法。 許多開放原始碼雲端原生系統採用 Kafka。

事件中樞透過[分割取用者模型](https://docs.microsoft.com/azure/event-hubs/event-hubs-features)來執行訊息串流，而每個取用者只會讀取訊息資料流程的特定子集或資料分割。 此模式支援大幅的水平擴充來處理事件，並提供佇列和主題所沒有的其他串流功能。 資料分割是經過排序且保存在事件中樞內的事件序列。 當較新的事件抵達時，它們會新增至此順序的結尾。圖4-19 顯示事件中樞內的資料分割。

![事件中樞資料分割](./media/event-hub-partitioning.png)

**圖 4-19**. 事件中樞資料分割

每個取用者群組會讀取訊息資料流程的子集或分割區，而不是從相同的資源讀取。

對於必須串流大量事件的雲端原生應用程式，Azure 事件中樞可以是健全且實惠的解決方案。

>[!div class="step-by-step"]
>[上一個](front-end-communication.md) 
>[下一步](grpc.md)
