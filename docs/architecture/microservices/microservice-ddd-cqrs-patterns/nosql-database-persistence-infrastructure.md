---
title: 使用 NoSQL 資料庫作為持續性基礎結構
description: 請先瞭解 NoSql 資料庫的一般使用方式，並 Azure Cosmos DB 特別是執行持續性的選項。
ms.date: 01/13/2021
ms.openlocfilehash: 32f32a3fd247f49ac54deaf33605bcc2ac7b55dc
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188825"
---
# <a name="use-nosql-databases-as-a-persistence-infrastructure"></a>使用 NoSQL 資料庫作為持續性基礎結構

當您將 NoSQL 資料庫用於基礎結構資料層時，通常不會使用 Entity Framework Core 這類 ORM。 相反地，您使用 NoSQL 引擎所提供的 API (例如 Azure Cosmos DB、MongoDB、Cassandra、RavenDB、CouchDB 或 Azure Storage Tables)。

不過，如果您使用 NoSQL 資料庫，特別是 Azure Cosmos DB、CouchDB 或 RavenDB 這類文件導向資料庫，則使用 DDD 彙總來設計模型的方式在識別彙總根、子實體類別和值物件類別方面有部分類似 EF Core 中的執行方式。 但最後資料庫選項會影響您的設計。

當您使用文件導向資料庫時，可以將彙總實作為以 JSON 或另一種格式序列化的單一文件。 不過，從領域模型程式碼觀點，資料庫的使用是透明的。 使用 NoSQL 資料庫時，您仍然會使用實體類別和彙總根類別，但彈性大於使用 EF Core 時，因為持續性不是關聯式。

差異在於如何持續保存該模型。 如果您實作根據 POCO 實體類別且無特定基礎結構持續性的領域模型，則可能可以移至不同的持續性基礎結構，即使是從關聯式到 NoSQL 也是一樣。 不過，這不應該是您的目標。 不同資料庫技術中一律會有條件約束和取捨，因此關聯式或 NoSQL 資料庫不能使用同一模型。 變更持續性模型不簡單，因為交易和持續性作業大不相同。

例如，在文件導向資料庫中，彙總根可以有多個子集合屬性。 在關聯式資料庫中，查詢多個子集合屬性不易最佳化，因為會從 EF 會取回 UNION ALL SQL 陳述式。 關聯式資料庫或 NoSQL 資料庫有相同的領域模型並不簡單，您也不應該嘗試這麼做。 實際上，您必須透過了解要如何使用每個特定資料庫中的資料來設計模型。

使用 NoSQL 資料庫時的好處是實體更正規化，因此您未設定資料表對應。 領域模型可能會比使用關聯式資料庫更有彈性。

當您根據彙總來設計領域模型時，移至 NoSQL 和文件導向資料庫可能會比使用關聯式資料庫更為容易，因為您所設計的彙總與文件導向資料庫中的序列化文件類似。 然後，您可以將該匯總所需的所有資訊包含在這些「包」中。

例如，下列 JSON 程式碼是使用文件導向資料庫時的訂單彙總範例實作。 這類似我們在 eShopOnContainers 範例中實作的訂單彙總，但其下不使用 EF Core。

```json
{
    "id": "2017001",
    "orderDate": "2/25/2017",
    "buyerId": "1234567",
    "address": [
        {
        "street": "100 One Microsoft Way",
        "city": "Redmond",
        "state": "WA",
        "zip": "98052",
        "country": "U.S."
        }
    ],
    "orderItems": [
        {"id": 20170011, "productId": "123456", "productName": ".NET T-Shirt",
        "unitPrice": 25, "units": 2, "discount": 0},
        {"id": 20170012, "productId": "123457", "productName": ".NET Mug",
        "unitPrice": 15, "units": 1, "discount": 0}
    ]
}
```

## <a name="introduction-to-azure-cosmos-db-and-the-native-cosmos-db-api"></a>Azure Cosmos DB 和原生 Cosmos DB API 簡介

[Azure Cosmos DB](/azure/cosmos-db/introduction) 是 Microsoft 的關鍵任務應用程式的全域分散式資料庫服務。 Azure Cosmos DB 提供[一站式全域散發](/azure/cosmos-db/distribute-data-globally)、全球[彈性調整的輸送量和儲存體](/azure/cosmos-db/partition-data)、達到第 99 個百分位數的個位數毫秒延遲、[五個定義完善的一致性層級](/azure/cosmos-db/consistency-levels)，以及保證的高可用性，全部都由[領先業界的 SLA (英文)](https://azure.microsoft.com/support/legal/sla/cosmos-db/) 所支援。 Azure Cosmos DB 會[自動編製資料的索引](https://www.vldb.org/pvldb/vol8/p1668-shukla.pdf)，您不需要處理結構描述和索引管理。 它是多重模型，支援文件、索引鍵/值、圖表和單欄式資料模型。

![顯示 Azure Cosmos DB 全域散發的圖表。](./media/nosql-database-persistence-infrastructure/azure-cosmos-db-global-distribution.png)

**圖 7-19**。 Azure Cosmos DB 全域散發

當您使用 C\# 模型來實作要供 Azure Cosmos DB API 使用的彙總時，彙總可能類似與 EF Core 搭配使用的 C\# POCO 類別。 差異在於從應用程式和基礎結構層級使用它們的方式，如下列程式碼所示：

```csharp
// C# EXAMPLE OF AN ORDER AGGREGATE BEING PERSISTED WITH AZURE COSMOS DB API
// **_ Domain Model Code _*_
// Aggregate: Create an Order object with its child entities and/or value objects.
// Then, use AggregateRoot's methods to add the nested objects so invariants and
// logic is consistent across the nested properties (value objects and entities).

Order orderAggregate = new Order
{
    Id = "2017001",
    OrderDate = new DateTime(2005, 7, 1),
    BuyerId = "1234567",
    PurchaseOrderNumber = "PO18009186470"
}

Address address = new Address
{
    Street = "100 One Microsoft Way",
    City = "Redmond",
    State = "WA",
    Zip = "98052",
    Country = "U.S."
}

orderAggregate.UpdateAddress(address);

OrderItem orderItem1 = new OrderItem
{
    Id = 20170011,
    ProductId = "123456",
    ProductName = ".NET T-Shirt",
    UnitPrice = 25,
    Units = 2,
    Discount = 0;
};

//Using methods with domain logic within the entity. No anemic-domain model
orderAggregate.AddOrderItem(orderItem1);
// _*_ End of Domain Model Code _*_

// _*_ Infrastructure Code using Cosmos DB Client API _*_
Uri collectionUri = UriFactory.CreateDocumentCollectionUri(databaseName,
    collectionName);

await client.CreateDocumentAsync(collectionUri, orderAggregate);

// As your app evolves, let's say your object has a new schema. You can insert
// OrderV2 objects without any changes to the database tier.
Order2 newOrder = GetOrderV2Sample("IdForSalesOrder2");
await client.CreateDocumentAsync(collectionUri, newOrder);
```

您可以看到領域模型使用方式可能類似其在基礎結構是 EF 時於領域模型中的使用方式。 您仍然可以使用相同的彙總根方法來確保彙總內的一致性、非變異值和驗證。

不過，相較於 EF Core 程式碼或任何其他與關聯式資料庫有關的程式碼，當您將模型持續保存至 NoSQL 資料庫時，程式碼和 API 會大幅變更。

## <a name="implement-net-code-targeting-mongodb-and-azure-cosmos-db"></a>實作以 MongoDB 和 Azure Cosmos DB 為目標的 .NET 程式碼

### <a name="use-azure-cosmos-db-from-net-containers"></a>使用 .NET 容器中的 Azure Cosmos DB

您可以透過容器中所執行的 .NET 程式碼來存取 Azure Cosmos DB 資料庫，例如來自任何其他 .NET 應用程式。 例如，實作 eShopOnContainers 中的 Locations.API 和 Marketing.API 微服務，讓它們可以利用 Azure Cosmos DB 資料庫。

不過，從 Docker 開發環境觀點，Azure Cosmos DB 有一些限制。 即使內部部署 [Azure Cosmos DB 模擬器](/azure/cosmos-db/local-emulator) 可在本機開發電腦中執行，它還是只支援 Windows。 不支援 Linux 和 macOS。

此外，也有可能在 Docker 上執行此模擬器，但只是在 Windows 容器上執行，而不是使用 Linux 容器。 如果您的應用程式部署為 Linux 容器，則這是開發環境的初始障礙，因為您目前無法同時在適用於 Windows 的 Docker 上部署 Linux 和 Windows 容器。 所有要部署的容器都必須適用於 Linux 或 Windows。

開發/測試解決方案的理想且更直接部署是要可以部署作為容器的資料庫系統以及自訂容器，讓您的開發/測試環境一律保持一致。

### <a name="use-mongodb-api-for-local-devtest-linuxwindows-containers-plus-azure-cosmos-db"></a>將 MongoDB API 用於本機開發/測試 Linux/Windows 容器和 Azure Cosmos DB

Cosmos DB 資料庫支援 MongoDB API for .NET 以及原生 MongoDB 有線通訊協定。 這表示使用現有的驅動程式，針對 MongoDB 所撰寫的應用程式現在可以與 Cosmos DB 通訊，且使用 Cosmos DB 資料庫，而不是使用 MongoDB 資料庫，如圖 7-20 所示。

![此圖顯示 Cosmos DB 支援 .NET 和 MongoDB 有線通訊協定。](./media/nosql-database-persistence-infrastructure/mongodb-api-wire-protocol.png)

_ * 圖 7-20 * *。 使用 MongoDB API 和通訊協定存取 Azure Cosmos DB

這是含 Linux 容器之 Docker 環境中概念證明的極方便使用方法，因為 [MongoDB Docker 映像](https://hub.docker.com/r/_/mongo/)是支援 Docker Linux 容器和 Docker Windows 容器的多架構映像。

如下圖所示，使用 MongoDB API，eShopOnContainers 可支援 MongoDB Linux 和 Windows 容器開發本機環境，但您接著只要[變更 MongoDB 連接字串以指向 Azure Cosmos DB](/azure/cosmos-db/connect-mongodb-account)，就可以移至可擴充的 PaaS 雲端解決方案作為 Azure Cosmos DB。

![圖表顯示 eShopOnContainers 中的位置微服務可以使用 Cosmos DB 或 Mongo DB。](./media/nosql-database-persistence-infrastructure/eshoponcontainers-mongodb-containers.png)

**圖 7-21**。 將 MongoDB 容器用於開發環境或將 Azure Cosmos DB 用於生產環境的 eShopOnContainers

生產環境 Azure Cosmos DB 會在 Azure 的雲端中以 PaaS 和可擴充服務的形式執行。

您的自訂 .NET 容器可以在本機開發 Docker 主機上執行，該主機 (使用 Windows 10 機器中的適用於 Windows 的 Docker) 或部署到生產環境，例如 Azure AKS 或 Azure Service Fabric 中的 Kubernetes。 在第二個環境中，您只會部署 .NET 自訂容器，而不是 MongoDB 容器，因為您會在雲端中使用 Azure Cosmos DB 在生產環境中處理資料。

使用 MongoDB API 的清楚優點在於您的解決方案可以透過資料庫引擎 (MongoDB 或 Azure Cosmos DB) 執行，因此，移轉至不同環境應該相當簡單。 不過，有時值得使用原生 API (即原生 Cosmos DB API) 來充分利用特定資料庫引擎的功能。

如需進一步比較只在雲端中使用 MongoDB 與 Cosmos DB，請參閱[在此頁面中使用 Azure Cosmos DB 的優點](/azure/cosmos-db/mongodb-introduction)。

### <a name="analyze-your-approach-for-production-applications-mongodb-api-vs-cosmos-db-api"></a>分析實際執行應用程式的方法： MongoDB API 與 Cosmos DB API

在 eShopOnContainers 中，我們將使用 MongoDB API，因為我們的優先順序基本上是要有一個一致的開發/測試環境，也就是使用 NoSQL 資料庫，也可以使用 Azure Cosmos DB。

不過，如果您打算使用 MongoDB API 來存取 Azure 中用於生產應用程式的 Azure Cosmos DB，則在使用 MongoDB API 來存取 Azure Cosmos DB 資料庫時，您應該分析功能和效能的差異，相較于使用原生 Azure Cosmos DB API。 如果類似，則您可以使用 MongoDB API，且獲得同時支援兩個 NoSQL 資料庫引擎的優點。

您也可以使用 MongoDB 叢集做為 Azure 雲端中的生產資料庫，也可以搭配 [Mongodb Azure 服務](https://www.mongodb.com/scale/mongodb-azure-service)使用。 但是，它不是 Microsoft 提供的 PaaS 服務。 在此情況下，Azure 只會託管來自 MongoDB 的那個解決方案。

基本上，這只是一項免責聲明，表示您不應該一律使用 MongoDB API 來進行 Azure Cosmos DB，如同我們在 eShopOnContainers 中所做的一樣，因為它是 Linux 容器的方便選擇。 這項決策應該根據您需要為生產應用程式所執行的特定需求和測試。

### <a name="the-code-use-mongodb-api-in-net-applications"></a>程式碼：在 .NET 應用程式中使用 MongoDB API

MongoDB API for .NET 是以您需要新增至專案的 NuGet 套件為基礎，如同下圖所示的 Locations.API 專案中一樣。

![MongoDB NuGet 套件中相依性的螢幕擷取畫面。](./media/nosql-database-persistence-infrastructure/mongodb-api-nuget-packages.png)

**圖 7-22**。 .NET 專案中的 MongoDB API NuGet 套件參考

讓我們先調查下列各節中的程式碼。

#### <a name="a-model-used-by-mongodb-api"></a>MongoDB API 所使用的模型

首先，您必須在應用程式的記憶體空間中，定義將保留來自資料庫之資料的模型。 以下是用於 eShopOnContainers 位置的模型範例。

```csharp
using MongoDB.Bson;
using MongoDB.Bson.Serialization.Attributes;
using MongoDB.Driver.GeoJsonObjectModel;
using System.Collections.Generic;

public class Locations
{
    [BsonId]
    [BsonRepresentation(BsonType.ObjectId)]
    public string Id { get; set; }
    public int LocationId { get; set; }
    public string Code { get; set; }
    [BsonRepresentation(BsonType.ObjectId)]
    public string Parent_Id { get; set; }
    public string Description { get; set; }
    public double Latitude { get; set; }
    public double Longitude { get; set; }
    public GeoJsonPoint<GeoJson2DGeographicCoordinates> Location
                                                             { get; private set; }
    public GeoJsonPolygon<GeoJson2DGeographicCoordinates> Polygon
                                                             { get; private set; }
    public void SetLocation(double lon, double lat) => SetPosition(lon, lat);
    public void SetArea(List<GeoJson2DGeographicCoordinates> coordinatesList)
                                                    => SetPolygon(coordinatesList);

    private void SetPosition(double lon, double lat)
    {
        Latitude = lat;
        Longitude = lon;
        Location = new GeoJsonPoint<GeoJson2DGeographicCoordinates>(
            new GeoJson2DGeographicCoordinates(lon, lat));
    }

    private void SetPolygon(List<GeoJson2DGeographicCoordinates> coordinatesList)
    {
        Polygon = new GeoJsonPolygon<GeoJson2DGeographicCoordinates>(
                  new GeoJsonPolygonCoordinates<GeoJson2DGeographicCoordinates>(
                  new GeoJsonLinearRingCoordinates<GeoJson2DGeographicCoordinates>(
                                                                 coordinatesList)));
    }
}
```

您可以看到有幾個屬性和型別來自 MongoDB NuGet 套件。

NoSQL 資料庫通常非常適合用於處理非關聯式階層式資料。 在此範例中，我們會使用特別針對地理位置所建立的 MongoDB 類型，例如 `GeoJson2DGeographicCoordinates`。

#### <a name="retrieve-the-database-and-the-collection"></a>擷取資料庫和集合

在 eShopOnContainers 中，我們已經建立自訂資料庫內容，在其中，我們會實作可擷取資料庫和 MongoCollections 的程式碼，如下列程式碼所示。

```csharp
public class LocationsContext
{
    private readonly IMongoDatabase _database = null;

    public LocationsContext(IOptions<LocationSettings> settings)
    {
        var client = new MongoClient(settings.Value.ConnectionString);
        if (client != null)
            _database = client.GetDatabase(settings.Value.Database);
    }

    public IMongoCollection<Locations> Locations
    {
        get
        {
            return _database.GetCollection<Locations>("Locations");
        }
    }
}
```

#### <a name="retrieve-the-data"></a>擷取資料

透過 C# 程式碼 (例如 Web API 控制器或自訂存放庫實作)，您可以在透過 MongoDB API 查詢時撰寫與下列類似的程式碼。 請注意，`_context` 物件是前一個 `LocationsContext` 類別的執行個體。

```csharp
public async Task<Locations> GetAsync(int locationId)
{
    var filter = Builders<Locations>.Filter.Eq("LocationId", locationId);
    return await _context.Locations
                            .Find(filter)
                            .FirstOrDefaultAsync();
}
```

#### <a name="use-an-env-var-in-the-docker-composeoverrideyml-file-for-the-mongodb-connection-string"></a>在 docker-compose.override.yml 檔案中針對 MongoDB 連接字串使用 env-var

建立 MongoClient 物件時，需要有基礎參數，明確地說就是指向正確資料庫的 `ConnectionString` 參數。 在 eShopOnContainers 的情況下，連接字串可以指向本機 MongoDB Docker 容器或「生產」 Azure Cosmos DB 資料庫。  該連接字串來自 `docker-compose.override.yml` 檔案中所定義的環境變數，而此檔案是在使用 docker-compose 或 Visual Studio 部署時使用，如下列 yml 程式碼所示。

```yml
# docker-compose.override.yml
version: '3.4'
services:
  # Other services
  locations-api:
    environment:
      # Other settings
      - ConnectionString=${ESHOP_AZURE_COSMOSDB:-mongodb://nosqldata}

```

`ConnectionString` 環境變數是使用這種方式解決：如果 `ESHOP_AZURE_COSMOSDB` 全域變數定義於 Azure Cosmos DB 連接字串的 `.env` 檔案，則會使用它來存取雲端中的 Azure Cosmos DB 資料庫。 如果未定義，則會採用此 `mongodb://nosqldata` 值並使用開發 MongoDB 容器。

下列程式碼示範含 Azure Cosmos DB 連接字串全域環境變數的 `.env` 檔案，如 eShopOnContainers 中所實作：

```yml
# .env file, in eShopOnContainers root folder
# Other Docker environment variables

ESHOP_EXTERNAL_DNS_NAME_OR_IP=localhost
ESHOP_PROD_EXTERNAL_DNS_NAME_OR_IP=<YourDockerHostIP>

#ESHOP_AZURE_COSMOSDB=<YourAzureCosmosDBConnData>

#Other environment variables for additional Azure infrastructure assets
#ESHOP_AZURE_REDIS_BASKET_DB=<YourAzureRedisBasketInfo>
#ESHOP_AZURE_STORAGE_CATALOG_URL=<YourAzureStorage_Catalog_BLOB_URL>
#ESHOP_AZURE_SERVICE_BUS=<YourAzureServiceBusInfo>
```

將 ESHOP_AZURE_COSMOSDB 行取消批註，並將其更新為從 Azure 入口網站取得的 Azure Cosmos DB 連接字串，如 [將 MongoDB 應用程式連線至 Azure Cosmos DB](/azure/cosmos-db/connect-mongodb-account)中所述。

如果 `ESHOP_AZURE_COSMOSDB` 全域變數是空的，表示它在檔案中是批註 `.env` ，則容器會使用預設的 MongoDB 連接字串。 此連接字串會指向部署在 eShopOnContainers 中的本機 MongoDB 容器，此容器名為 `nosqldata` 且已在 docker 撰寫檔案中定義，如下列 yml 程式碼所示：

``` yml
# docker-compose.yml
version: '3.4'
services:
  # ...Other services...
  nosqldata:
    image: mongo
```

#### <a name="additional-resources"></a>其他資源

- **將 NoSQL 資料庫的檔資料模型化** \
  <https://docs.microsoft.com/azure/cosmos-db/modeling-data>

- **Vaughn Vernon。理想的 Domain-Driven 設計匯總存放區？** \
  <https://kalele.io/blog-posts/the-ideal-domain-driven-design-aggregate-store/>

- **Azure Cosmos DB 的簡介：適用于 MongoDB 的 API**  \
  <https://docs.microsoft.com/azure/cosmos-db/mongodb-introduction>

- **Azure Cosmos DB：使用 .NET 和 Azure 入口網站建立 MongoDB API web 應用程式**  \
  <https://docs.microsoft.com/azure/cosmos-db/create-mongodb-dotnet>

- **使用 Azure Cosmos DB 模擬器進行本機開發和測試**  \
  <https://docs.microsoft.com/azure/cosmos-db/local-emulator>

- **將 MongoDB 應用程式連線至 Azure Cosmos DB**  \
  <https://docs.microsoft.com/azure/cosmos-db/connect-mongodb-account>

- **Cosmos DB 模擬器 Docker 映射 (Windows 容器)**  \
  <https://hub.docker.com/r/microsoft/azure-cosmosdb-emulator/>

- **MongoDB Docker 映射 (Linux 和 Windows 容器)**  \
  <https://hub.docker.com/_/mongo/>

- **搭配使用 MongoChef (Studio 3T) 與 Azure Cosmos DB：適用于 MongoDB 的 API 帳戶**  \
  <https://docs.microsoft.com/azure/cosmos-db/mongodb-mongochef>

>[!div class="step-by-step"]
>[上一個](infrastructure-persistence-layer-implementation-entity-framework-core.md) 
>[下一步](microservice-application-layer-web-api-design.md)
