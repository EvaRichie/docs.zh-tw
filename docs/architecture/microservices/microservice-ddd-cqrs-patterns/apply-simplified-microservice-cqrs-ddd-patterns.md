---
title: 在微服務中套用簡化的 CQRS 和 DDD 模式
description: .NET 微服務：容器化 .NET 應用程式的架構 | 了解 CQRS 和 DDD 模式之間的整體關聯。
ms.date: 01/13/2021
ms.openlocfilehash: c1a990689a446e2efba48beafe4b55d614b54427
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188955"
---
# <a name="apply-simplified-cqrs-and-ddd-patterns-in-a-microservice"></a>在微服務中套用簡化 CQRS 和 DDD 模式

CQRS 是將模型分隔為讀取資料和寫入資料的架構模式。 相關的詞彙 [命令查詢分隔 (CQS)](https://martinfowler.com/bliki/CommandQuerySeparation.html) 最初是由本書的面向 *物件軟體結構* 中的 Bertrand Meyer 所定義。 基本概念是，您可以將系統的作業分成兩個簡單的分類：

- 查詢： 這些查詢會傳回結果，而不會變更系統的狀態，而且它們沒有任何副作用。

- 命令。 這些命令會變更系統的狀態。

CQS 是一個簡單的概念：它與相同物件內的方法是查詢或命令。 每個方法可傳回狀態或變動狀態，但不會同時執行。 即使是單一存放庫模式物件也會遵守 CQS。 CQS 可視為 CQRS 的基本原則。

[命令和查詢職責分離 (CQRS)](https://martinfowler.com/bliki/CQRS.html)是由 Greg Young 所引進，並由 Udi Dahan 等人強烈提倡。 它是以 CQS 原則為依據，但內容更詳細。 它可以視為根據命令和事件 (或選擇性地根據非同步訊息) 的模式。 在許多情況下，CQRS 與更進階的案例相關，像是針對讀取 (查詢) 和寫入 (更新) 使用不同的實體資料庫。 此外，更進階的 CQRS 系統可能會針對您的更新資料庫實作[事件溯源 (Event Sourcing，ES)](https://martinfowler.com/eaaDev/EventSourcing.html)，因此您只會在領域模型中儲存事件，而不會儲存目前的狀態資料。 不過，本指南不會使用此方法。 本指南使用最簡單的 CQRS 方法，其中只包含從命令分隔查詢。

您可以將查詢作業分組為一個層級，並將命令分組為另一個層級，來達到 CQRS 的分離狀況。 每個層級都有自己的資料模型 (請注意我們是說模型，但不一定是不同的資料庫)，並使用自己的模式和技術組合來建立。 更重要的是，這兩個層級可以在相同的階層或微服務中，如本指南中所使用的範例 (訂購微服務) 所示。 或者，它們可能會在不同的微服務或處理序上實作，以便可分別最佳化和擴充而不會彼此影響。

CQRS 表示會有兩個物件用於讀取/寫入作業，在其他內容中則有一個。 使用反正規化的讀取資料庫有其原因，您可以在更進階的 CQRS 文獻中了解。 但我們不會在此使用該方法，因為此處的目標在於提高查詢的彈性，而不在於使用 DDD 模式中的條件約束 (例如彙總) 來限制查詢。

eShopOnContainers 參考應用程式中的訂購微服務即為這種服務的範例。 此服務會實作以簡化的 CQRS 方法為基礎的微服務。 它會使用單一資料來源或資料庫，但有兩個邏輯模型加上異動領域的 DDD 模式，如圖 7-2 所示。

![此圖顯示高階簡化的 CQRS 和 DDD 微服務。](./media/apply-simplified-microservice-cqrs-ddd-patterns/simplified-cqrs-ddd-microservice.png)

**圖 7-2**. 簡化的 CQRS 和 DDD 型微服務

邏輯 "順序" 微服務包含其訂購資料庫，但不一定是相同的 Docker 主機。 資料庫在相同的 Docker 主機中對開發有利，但對生產則不然。

應用程式層可以是 Web API 本身。 此處的重要設計觀點是微服務已遵循 CQRS 模式，將查詢、ViewModel (專為用戶端應用程式所建立的資料模型) 與命令、領域模型、異動分開。 此方法可確保查詢不會受限於來自 DDD 模式的限制和條件約束，這些限制和條件約束只對異動和更新才有意義，如稍後章節所述。

## <a name="additional-resources"></a>其他資源

- **Greg 年輕事件來源系統中的版本控制** (免費閱讀線上電子書) \
   <https://leanpub.com/esversioning/read>

>[!div class="step-by-step"]
>[上一個](index.md) 
>[下一步](eshoponcontainers-cqrs-ddd-microservice.md)
