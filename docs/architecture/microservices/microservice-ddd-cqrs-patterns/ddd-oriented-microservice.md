---
title: 設計 DDD 導向微服務
description: .NET 微服務：容器化 .NET 應用程式的架構 | 了解 DDD 導向的訂購微服務及其應用程式層的設計。
ms.date: 01/13/2021
ms.openlocfilehash: 1d17f0842bb371ce65e96f33d25b2d6e94493396
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188331"
---
# <a name="design-a-ddd-oriented-microservice"></a>設計 DDD 導向微服務

網域驅動設計 (DDD) 支援以與您的使用案例相關之商務實際情況建立模型。 在建置應用程式的內容中，DDD 會將問題作為領域討論。 它將獨立問題區域描述為限定內容 (每個限定內容都與一個微服務相互關聯)，並強調討論這些問題的通用語言。 它也會建議許多技術概念和模式，例如具有豐富模型的領域實體 (沒有 [anemic 領域模型](https://martinfowler.com/bliki/AnemicDomainModel.html)) 、值物件、匯總，以及匯總根 (或根實體) 規則來支援內部執行。 本節將介紹這些內部模式的設計及實作。

有時候這些 DDD 技術規則和模式會被認為是實作 DDD 方法時具有陡峭學習曲線的障礙。 但重要的並非模式本身，而是組織程式碼，使其能與商務問題校準，並使用相同的商務字詞 (通用語言)。 此外，只有您在使用大量商務規則實作複雜的微服務時，才應套用 DDD 方法。 較簡單的責任，例如 CRUD 服務，可使用更為簡單的方法來管理。

如何劃定界線便是設計及定義微服務時的關鍵工作。 DDD 模式可協助您了解領域中的複雜度。 針對每一個限定內容的領域模型，您會識別並定義實體、值物件，以及為您的領域建立模型的彙總。 您會建置並精簡化包含於定義您內容之界限內的領域模型。 而且這是微服務形式的明確。 包含在那些界限內的元件最後會變成您的微服務，雖然在一些案例中，BC 或商務微服務可由數種實體服務組成。 DDD 與界限相關，微服務也一樣。

## <a name="keep-the-microservice-context-boundaries-relatively-small"></a>讓微服務內容界限保持相對較小

決定在限定內容之間的何處放置界限，才能平衡兩個競爭的目標。 首先，您會希望在一開始盡可能的建立最小的微服務，即使那並不是最主要的驅策因素。您應在需要內聚的事物周圍建立界限。 接著，您會想要避免任何微服務間多餘的通訊。 這些目標可能會彼此互相矛盾。 您應該藉由盡可能的將系統分解為許多小型的微服務來平衡他們，直到您發現隨著每一次分離新限定內容的額外嘗試，通訊界限正迅速的成長。 內聚是單一限定內容中的關鍵。

這與在實作類別時的 [Inappropriate Intimacy (程式碼不適當的親密性)](https://sourcemaking.com/refactoring/smells/inappropriate-intimacy) 相似。 若兩個微服務需要彼此進行大量的共同作業，他們便應該成為相同的一項微服務。

另一種查看此層面的方法是自我管理。 若微服務必須倚賴另外一個服務才能服務一項要求，它便不是真正的自主。

## <a name="layers-in-ddd-microservices"></a>DDD 微服務中的層

大部分包含大量商務與技術複雜性的企業應用程式都會由多個層定義。 「層」只是邏輯的成品，與服務的部署無關。 他們存在的目的只是為了要協助開發人員管理程式碼中的複雜度。 不同層 (像是領域模型層和展示層等，) 可能會有不同的類型，這會在這些類型之間強制翻譯。

例如，實體可從資料庫載入。 然後該資訊的一部份，或是包含從其他實體取得之額外資料的資訊彙總，便可透過 REST Web API 傳送至用戶端 UI。 重點在於領域實體是包含在領域模型層中，不應散佈到其不屬於的其他區域，例如展示層。

此外，您需要讓彙總根 (根實體) 控制永遠有效的實體 (請參閱[在領域模型層中設計驗證](domain-model-layer-validations.md)一節)。 因此，實體不應繫結於用戶端檢視，因為在 UI 層級中，有些資料可能尚未驗證。 這是 ViewModel 的目的。 ViewModel 是一種僅針對展示層需求的資料模型。 領域實體不直接屬於 ViewModel。 相反地，您需要在 ViewModel 和領域實體之間進行轉換，反之亦然。

當處理複雜性時，擁有由確認所有與該實體群組 (彙總) 相關的不區分及規則都是透過單一進入點或閘道 (彙總根) 執行的彙總根控制的領域模型是非常重要的。

圖 7-5 顯示分層設計在 eShopOnContainer 應用程式中的實作方式。

![顯示領域驅動設計微服務中之圖層的圖表。](./media/ddd-oriented-microservice/domain-driven-design-microservice.png)

**圖 7-5**. eShopOnContainers 訂購微服務中的 DDD 層

訂購等 DDD 微服務中的三層。 每一層都是 VS 專案：應用程式層是 Ordering.API、領域層是 Ordering.Domain，而基礎結構層是 Ordering.Infrastructure。 您會希望將系統設計成每一個層都只會跟特定的其他層通訊。 如果將圖層實作為不同的類別庫，則該方法可能更容易強制執行，因為您可以清楚地識別程式庫間設定的相依性。 例如，領域模型層不應該相依於任何其他的層 (領域模型類別應為簡單的 CLR 物件 ([POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 類別)。 如 [圖 7-6] 所示，「 **網域** 層程式庫」只在 .net 程式庫或 NuGet 套件上具有相依性，而不是在其他任何自訂程式庫上，例如資料連結庫或持續性程式庫。

![排序網域相依性的螢幕擷取畫面。](./media/ddd-oriented-microservice/ordering-domain-dependencies.png)

**圖 7-6**。 作為程式庫實作的層允許對層之間的相依性進行更佳的控制

### <a name="the-domain-model-layer"></a>領域模型層

Eric Evans 的優良書籍 [Domain Driven Design (領域驅動設計)](https://domainlanguage.com/ddd/) 提到了下列關於領域模型層及應用程式層的內容。

**領域模型層** 負責呈現商務概念、商務情況的資訊，以及商務規則。 反映商務情況的狀態會受控並用於此處，即使儲存它的技術細節已委派給基礎結構。 此層是商務軟體的核心。

領域模型層是表達商務的地方。 當您在 .NET 中實作微服務領域模型層時，該層會編碼為帶有擷取資料與行為 (帶有邏輯的方法) 之領域實體的類別庫。

遵循 [Persistence Ignorance (永續性無知)](https://deviq.com/persistence-ignorance/) 與 [Infrastructure Ignorance (基礎結構無知)](https://ayende.com/blog/3137/infrastructure-ignorance) 準則，此層必須完全忽略資料永續性詳細資料。 這些永續性工作應由基礎結構層執行。 因此，此層不應直接相依於基礎結構。這表示讓您的領域模型實體類別為 [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object) 是非常重要的一項規則。

領域實體不應直接相依 (例如衍生自基底類別) 於任何資料存取基礎結構架構，例如 Entity Framework 或 NHibernate。 在理想情況下，您的領域實體不應衍生自或實作在任何基礎結構架構中定義的任何類型。

大多數的現代 ORM 架構 (例如 Entity Framework Core) 允許這種方法，以使您的領域模型類別不會與基礎結構結合。 然而，在使用特定 NoSQL 資料庫及架構，例如 Azure Service Fabric 中的動作項目及可靠集合時，不見得都能擁有 POCO 實體。

即使針對您的領域模型遵循永續性無知準則是非常重要的，您也不應忽略永續性考量。 但請務必瞭解實體資料模型，以及它如何對應至您的實體物件模型。 否則，您便可以建立不可能的設計。

此外，此層面並不表示您可以使用為關係資料庫設計的模型，並將它直接移至 NoSQL 或檔導向的資料庫。 在某些實體模型中，模型可能會適合，但通常並不會。 您的實體模型仍然必須基於儲存技術和 ORM 技術遵守條件約束。

### <a name="the-application-layer"></a>應用程式層

接下來移動到應用程式層，我們可以再次引用 Eric Evan 的書籍 [Domain Driven Design (領域驅動設計)](https://domainlanguage.com/ddd/)：

**應用程式層：** 定義軟體應執行的工作，並指示表達性領域物件解決問題。 此層負責的工作對於商務來說是有意義的，或是對與其他系統應用程式層進行的互動來說是必要的。 此圖層會保持精簡。 它並不會包含商務規則或知識，而只負責協調工作並將工作委派給下一層領域物件的共同作業。 它不具有反映商務情況的狀態，但可以擁有反映使用者或程式工作進度的狀態。

.NET 中的微服務應用層通常會編碼為 ASP.NET Core Web API 專案。 專案會執行微服務的互動、遠端網路存取，以及從 UI 或用戶端應用程式使用的外部 Web Api。 若使用的是 CQRS 方法，它便會包含查詢、微服務接受的命令，甚至是微服務之間的事件驅動通訊 (整合事件)。 代表應用程式層的 ASP.NET Core Web API 不可包含商務規則或領域知識 (尤其是交易或更新的領域規則)。這些內容應該由領域模型類別庫擁有。 應用程式層應僅負責協調工作，而不可保有或定義任何領域狀態 (領域模型)。 它會將商務規則的執行委派給領域模型類別自身 (彙總根及領域實體)，而後者最後便會在那些領域實體中更新資料。

基本上，應用程式邏輯便是您實作所有相依於指定前端之使用案例的地方。 例如，與 Web API 服務相關的實作。

目標是位於領域模型層中的領域邏輯、其不區分、資料模型，以及相關的商務規則都必須完全獨立於展示層及應用程式層。 最重要的是，領域模型層不可直接相依於任何基礎結構架構。

### <a name="the-infrastructure-layer"></a>基礎結構層

基礎結構層是一開始保有在領域實體 (記憶體中) 中的資料永續保存在資料庫或其他永續性存放區的方式。 其中一個範例便是使用 Entity Framework Core 程式碼來實作使用 DBContext 來將資料永續存放在關聯式資料庫中的存放庫模式類別。

根據先前所述的 [持續性無知](https://deviq.com/persistence-ignorance/) 和 [基礎結構無知](https://ayende.com/blog/3137/infrastructure-ignorance) 準則，基礎結構層不能「污染」網域模型層。 您必須透過使其對架構不具有硬式相依性，來讓領域模型實體類別保持無從得知您用來永續保存資料的基礎結構 (EF 或其他任何架構)。 您的領域模型層類別庫應僅具有您的領域程式碼，即只有實作您軟體核心的 [POCO](https://en.wikipedia.org/wiki/Plain_Old_CLR_Object)，並且完全與基礎技術分開。

因此，您的層或類別庫及專案最後應相依於您的領域模型層 (程式庫)，而不是反過來也一樣，如圖 7-7 所示。

![顯示 DDD 服務層級之間存在相依性的圖表。](./media/ddd-oriented-microservice/ddd-service-layer-dependencies.png)

**圖 7-7**。 DDD 中層之間的相依性

DDD 服務中的相依性，應用程式層相依於領域和基礎結構，基礎結構相依於網域，但網域不相依於任一層。 針對每一個微服務，此層應獨立設計。 如前文所述，您可以遵循 DDD 模式來實作最複雜的微服務，同時卻能以更簡單的方式實作更簡單的資料驅動微服務 (於單一層中的簡單 CRUD)。

#### <a name="additional-resources"></a>其他資源

- **DevIQ.持續性無知準則** \
  <https://deviq.com/persistence-ignorance/>

- **Oren Eini。基礎結構無知** \
  <https://ayende.com/blog/3137/infrastructure-ignorance>

- **天使 Lopez。Domain-Driven 設計中的分層架構** \
  <https://ajlopez.wordpress.com/2008/09/12/layered-architecture-in-domain-driven-design/>

>[!div class="step-by-step"]
>[上一個](cqrs-microservice-reads.md) 
>[下一步](microservice-domain-model.md)
