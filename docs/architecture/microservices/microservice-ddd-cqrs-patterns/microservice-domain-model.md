---
title: 設計微服務領域模型
description: .NET 微服務：容器化 .NET 應用程式的架構 | 了解設計 DDD 導向領域模型時的重要概念。
ms.date: 01/30/2020
ms.openlocfilehash: fe78e719570d5758b71531beab883e5c24a88dca
ms.sourcegitcommit: 5280b2aef60a1ed99002dba44e4b9e7f6c830604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84306902"
---
# <a name="design-a-microservice-domain-model"></a>設計微服務領域模型

為每個商務微服務或限定內容定義一個豐富領域模型。**

您的目標是為每個商務微服務或限定內容 (BC) 建立單一內聚領域模型。 不過請記住，BC 或商務微服務有時候可能是由共用單一領域模型的多個實體服務所組成。 領域模型必須擷取單一限定內容或其代表之商務微服務的規則、行為、商務語言和限定式。

## <a name="the-domain-entity-pattern"></a>領域實體模式

實體代表領域物件，而且主要是由其身分識別、連續性及一段時間的持續性所定義，而不只是由包含這些項目的屬性所定義。 如同 Eric Evans 說，「主要由其身分識別定義的物件稱為「實體」（Entity）。 實體在領域模型中很重要，因為它們是模型的基礎。 因此，您應該仔細識別及設計。

*實體的身分識別可以跨多個微服務或限定內容。*

您可以在多個限定內容或微服務之間，建立相同身分識別 (也就是相同的 `Id` 值) 但可能不同領域實體的模型。 不過，這並不表示會在多個限定內容中實作具有相同屬性和邏輯的相同實體。 相反地，每個系結內容中的實體會將其屬性和行為限制在該限定內容的網域中所需的專案。

例如，購買者實體可能會在設定檔或身分識別微服務的使用者實體中定義大部分的人員屬性，包括身分識別。 但訂購微服務中的購買者實體可能有較少的屬性，因為只有特定購買者資料會與訂購流程相關。 每個微服務或限定內容的內容會影響其領域模型。

除了實作資料屬性，領域實體還必須實作行為。**

DDD 中的領域實體必須實作與實體資料 (從記憶體存取的物件) 相關的領域邏輯或行為。 例如，作為訂單實體類別的一部分，您必須將商務邏輯和作業實作為工作的方法，例如新增訂單項目、資料驗證和總計算。 實體的方法會處理實體的非變異數和規則，而不是將這些規則散佈到應用層。

圖 7-8 所顯示的領域實體不只會實作資料屬性，還會實作具有相關領域邏輯的作業或方法。

![顯示領域實體模式的圖表。](./media/microservice-domain-model/domain-entity-pattern.png)

**圖 7-8**。 實作資料加上行為的領域實體設計範例

領域模型實體會透過方法實作行為，也就是它不是 "Anemic" 模型。 當然，有時候您可以有未實作任何邏輯作為實體類別一部分的實體。 如果子實體沒有任何特殊邏輯，彙總內的子實體就可能會發生這種情況，因為彙總根中已定義大部分邏輯。 如果您有在服務類別中（而不是在領域實體中）實作為邏輯的複雜微服務，您可能會進入 anemic 領域模型，如下一節所述。

### <a name="rich-domain-model-versus-anemic-domain-model"></a>豐富領域模型與 Anemic 領域模型

Martin Fowler 在 [AnemicDomainModel](https://martinfowler.com/bliki/AnemicDomainModel.html) (Anemic 領域模型) 一文中對 Anemic 領域模型有以下描述：

Anemic 領域模型的基本特徵是，乍看之下很像實物。 其中包含物件，許多物件會以領域空間中的名詞來命名，而且這些物件會透過真實領域模型所具有的豐富關聯性和結構來連接。 從行為上會看出端倪，並了解這些物件上幾乎沒有任何行為，比較像是一組 getter 和 setter。

當然，使用 Anemic 領域模型時，會從一組擷取所有領域或商務邏輯的服務物件 (傳統上稱為「商務層」**) 來使用這些資料模型。 商務層位於資料模型最上層，其使用資料模型的方式就像是資料一樣。

Anemic 領域模型只是程序樣式設計。 Anemic 實體物件不是真正的物件，因為它們缺少行為 (方法)。 它們只會保存資料屬性，因此不是物件導向設計。 藉由將所有的行為放入服務物件（商務層）中，您基本上會得到[spaghetti 程式碼](https://en.wikipedia.org/wiki/Spaghetti_code)或[交易腳本](https://martinfowler.com/eaaCatalog/transactionScript.html)，因此您會失去領域模型所提供的優點。

即便如此，如果您的微服務或限定內容很簡單 (CRUD 服務)，只有資料屬性之實體物件形式的 Anemic 領域模型便已足夠，而且可能不值得實作更複雜的 DDD 模式。 在此情況下，它只是持續性模型，因為您刻意建立只有 CRUD 用途資料的實體。

這就是為什麼微服務架構對於根據每個限定內容之多架構方法很理想的原因。 例如，在 eShopOnContainers 中，訂購微服務會實作 DDD 模式，但目錄微服務是簡易 CRUD 服務，因此不會實作此模式。

有些人認為 Anemic 領域模型是反模式。 它其實取決於您實作的內容。 如果您要建立的微服務夠簡單 (例如 CRUD 服務)，遵循 Anemic 領域模型就不是反模式。 不過，如果您需要處理微服務網域的複雜性，而此領域有許多不斷改變的商務規則，則 anemic 領域模型可能是該微服務或限定內容的反模式。 在此情況下，將它設計為具有實體的豐富模型可能會相當有利於這類微服務的長期成功，因為這些實體包含資料加上行為，並實作額外的 DDD 模式 (彙總、值物件等)。

#### <a name="additional-resources"></a>其他資源

- **DevIQ.網域實體** \
  <https://deviq.com/entity/>

- **聖馬丁 Fowler。網域模型** \
  <https://martinfowler.com/eaaCatalog/domainModel.html>

- **聖馬丁 Fowler。Anemic 領域模型** \
  <https://martinfowler.com/bliki/AnemicDomainModel.html>

### <a name="the-value-object-pattern"></a>值物件模式

如同 Eric Evans 所述，「許多物件沒有概念識別。 這些物件會描述某個事物的某些特性。」

實體需要身分識別，但系統中有許多物件則不需要，例如值物件模式。 值物件是描述領域層面之不具概念性身分識別的物件。 這些是您具現化來表示只與您暫時有關之設計元素的物件。 您關心這些物件的「本質」**，而不是它們的「身分」**。 範例包含數字和字串，但也可能是更高階的概念，例如屬性群組。

微服務中的實體不一定會是另一個微服務中的實體，因為在後者中，限定內容可能代表不同的意思。 例如，電子商務應用程式中的位址可能完全沒有身分識別，因為它可能只代表個人或公司客戶設定檔的一組屬性。 在此情況下，該地址應該會分類為值物件。 不過，在電力公用事業公司的應用程式中，客戶地址對公司領域可能很重要。 因此，地址必須含有身分識別，帳務系統才能直接連結至該地址。 在此情況下，地址應該會分類為領域實體。

具有名稱和姓氏的人員通常是實體，因為某個人具有身分識別，即使名稱和姓氏與另一組值一致（例如，這些名稱也會參考不同的人）。

值物件在關係資料庫和 Orm （例如 Entity Framework （EF））中很難管理，而在檔導向資料庫中，它們比較容易執行和使用。

EF Core 2.0 和更新版本包含[擁有的實體](https://devblogs.microsoft.com/dotnet/announcing-entity-framework-core-2-0/#owned-entities-and-table-splitting)功能，可讓您更輕鬆地處理值物件，如我們稍後會詳細說明。

#### <a name="additional-resources"></a>其他資源

- **聖馬丁 Fowler。值物件模式** \
  <https://martinfowler.com/bliki/ValueObject.html>

- **Value 物件** \
  <https://deviq.com/value-object/>

- **測試導向開發中的值物件** \
  [https://leanpub.com/tdd-ebook/read\#leanpub-auto-value-objects](https://leanpub.com/tdd-ebook/read#leanpub-auto-value-objects)

- **Eric Evans。領域驅動設計：處理軟體核心的複雜性。** (書籍；包含值物件的探討) \
  <https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/>

### <a name="the-aggregate-pattern"></a>彙總模式

領域模型包含不同資料實體和處理序的叢集，可控制重要功能區域，例如訂單完成或庫存。 更精細的 DDD 單位是彙總，其描述可視為內聚單位之實體和行為的叢集或群組。

您通常會根據所需的交易來定義彙總。 典型的範例是同時包含訂單項目清單的訂單。 訂單項目通常會是實體。 但它會是訂單彙總內的子實體，這也會包含訂單實體作為其根實體，通常稱為彙總根。

識別彙總可能很難。 彙總是一組必須同時一致的物件群組，但您不可以只挑選一組物件並將它們加上彙總標籤。 您必須從領域概念開始，並考慮在與該概念相關的最常見交易中使用的實體。 這些需要交易一致的實體會形成彙總。 考慮交易作業可能是識別彙總的最佳方式。

### <a name="the-aggregate-root-or-root-entity-pattern"></a>彙總根或根實體模式

彙總至少是由一個實體所組成，那就是彙總根，也稱為根實體或主要實體。 此外，它可以有多個子實體和值物件，所有實體和物件會共同實作必要的行為和交易。

彙總根的目的是確保彙總的一致性，它應該是透過彙總根類別中的方法或作業對彙總進行更新的唯一進入點。 您只能透過彙總根變更彙總內的實體。 它是匯總的一致性守護者，會考慮您可能需要在匯總中遵守的所有不變數和一致性規則。 如果您獨立變更子實體或值物件，彙總根無法確保彙總處於有效狀態。 就像是桌子鬆了桌腳一樣。 維護一致性是彙總根的主要目的。

在圖 7-9 中，您會看到購買者彙總之類的範例彙總，其中包含單一實體 (彙總根購買者)。 訂單彙總包含多個實體和值物件。

![比較買方匯總和訂單匯總的圖表。](./media/microservice-domain-model/buyer-order-aggregate-pattern.png)

**圖 7-9**。 具有多個或單一實體的彙總範例

DDD 領域模型由彙總組成，彙總可以只有一個實體或多個實體，而且也可以包含值物件。 請注意，視您的領域而定，購買者彙總可能會有其他子實體，就像是在 eShopOnContainers 參考應用程式中的訂購微服務一樣。 圖 7-9 只會描述購買者具有單一實體的情況，例如只包含彙總根的彙總。

若要維持彙總分離並保持彙總之間的清楚界限，建議在 DDD 領域模型中，不要允許在彙總之間直接瀏覽，而只具有外部索引鍵 (FK) 欄位，如 eShopOnContainers 的[訂購微服務領域模型](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.Domain/AggregatesModel/OrderAggregate/Order.cs)中所實作。 Order 實體只有買方的外鍵欄位，而不是 EF Core 導覽屬性，如下列程式碼所示：

```csharp
public class Order : Entity, IAggregateRoot
{
    private DateTime _orderDate;
    public Address Address { get; private set; }
    private int? _buyerId; // FK pointing to a different aggregate root
    public OrderStatus OrderStatus { get; private set; }
    private readonly List<OrderItem> _orderItems;
    public IReadOnlyCollection<OrderItem> OrderItems => _orderItems;
    // ... Additional code
}
```

識別及使用彙總需要研究和經驗。 如需詳細資訊，請參閱下列＜其他資源＞清單。

#### <a name="additional-resources"></a>其他資源

- **Vaughn Vernon。有效的匯總設計-第一部分：模型化單一匯總**（來自 <https://dddcommunity.org/> ） \
  <https://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_1.pdf>

- **Vaughn Vernon。有效的匯總設計-第二部分：使匯總能夠共同作業**（from <https://dddcommunity.org/> ） \
  <https://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf>

- **Vaughn Vernon。有效的匯總設計-第 III 部分：透過探索取得見解**（from <https://dddcommunity.org/> ） \
  <https://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_3.pdf>

- **Sergey Grybniak。DDD 戰術設計模式** \
  <https://www.codeproject.com/Articles/1164363/Domain-Driven-Design-Tactical-Design-Patterns-Part>

- **Chris Richardson。使用匯總開發交易式微服務** \
  <https://www.infoq.com/articles/microservices-aggregates-events-cqrs-part-1-richardson>

- **DevIQ.匯總模式** \
  <https://deviq.com/aggregate-pattern/>

>[!div class="step-by-step"]
>[上一個](ddd-oriented-microservice.md) 
>[下一步](net-core-microservice-domain-model.md)
