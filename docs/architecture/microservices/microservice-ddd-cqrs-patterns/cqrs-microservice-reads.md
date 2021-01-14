---
title: 在 CQRS 微服務中實作讀取/查詢
description: .NET 微服務：容器化 .NET 應用程式的架構 | 了解 CQRS 查詢端使用 Dapper 在 eShopOnContainers 訂購微服務上的實作。
ms.date: 01/13/2021
ms.openlocfilehash: 047fc3893dcaf72a17d29f5560c928879757d024
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188916"
---
# <a name="implement-readsqueries-in-a-cqrs-microservice"></a><span data-ttu-id="46bd7-103">在 CQRS 微服務中實作讀取/查詢</span><span class="sxs-lookup"><span data-stu-id="46bd7-103">Implement reads/queries in a CQRS microservice</span></span>

<span data-ttu-id="46bd7-104">如需讀取/查詢，eShopOnContainers 參考應用程式的訂購微服務，會在 DDD 模型和交易區域之外實作查詢。</span><span class="sxs-lookup"><span data-stu-id="46bd7-104">For reads/queries, the ordering microservice from the eShopOnContainers reference application implements the queries independently from the DDD model and transactional area.</span></span> <span data-ttu-id="46bd7-105">這種執行主要是因為查詢和交易的要求明顯不同。</span><span class="sxs-lookup"><span data-stu-id="46bd7-105">This implementation was done primarily because the demands for queries and for transactions are drastically different.</span></span> <span data-ttu-id="46bd7-106">寫入的執行交易必須與網域邏輯相容。</span><span class="sxs-lookup"><span data-stu-id="46bd7-106">Writes execute transactions that must be compliant with the domain logic.</span></span> <span data-ttu-id="46bd7-107">另一方面，查詢具有等冪性，可從網域規則中隔離。</span><span class="sxs-lookup"><span data-stu-id="46bd7-107">Queries, on the other hand, are idempotent and can be segregated from the domain rules.</span></span>

<span data-ttu-id="46bd7-108">方法很簡單，如圖 7-3 所示。</span><span class="sxs-lookup"><span data-stu-id="46bd7-108">The approach is simple, as shown in Figure 7-3.</span></span> <span data-ttu-id="46bd7-109">API 介面是由 Web API 控制器實作，這些控制器會使用任何基礎結構，例如 Dapper 等微物件關聯式對應 (ORM)，並根據 UI 應用程式的需求傳回動態 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="46bd7-109">The API interface is implemented by the Web API controllers using any infrastructure, such as a micro Object Relational Mapper (ORM) like Dapper, and returning dynamic ViewModels depending on the needs of the UI applications.</span></span>

![顯示簡化的 CQRS 中高階查詢的圖表。](./media/cqrs-microservice-reads/simple-approach-cqrs-queries.png)

<span data-ttu-id="46bd7-111">**圖 7-3**.</span><span class="sxs-lookup"><span data-stu-id="46bd7-111">**Figure 7-3**.</span></span> <span data-ttu-id="46bd7-112">CQRS 微服務中最簡單的查詢方法</span><span class="sxs-lookup"><span data-stu-id="46bd7-112">The simplest approach for queries in a CQRS microservice</span></span>

<span data-ttu-id="46bd7-113">以簡化的 CQRS 方法查詢端最簡單的方法，就是使用類似 Dapper 的微 ORM 查詢資料庫，傳回動態 Viewmodel。</span><span class="sxs-lookup"><span data-stu-id="46bd7-113">The simplest approach for the queries-side in a simplified CQRS approach can be implemented by querying the database with a Micro-ORM like Dapper, returning dynamic ViewModels.</span></span> <span data-ttu-id="46bd7-114">查詢定義會查詢資料庫，並傳回每個查詢立即建立的動態 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="46bd7-114">The query definitions query the database and return a dynamic ViewModel built on the fly for each query.</span></span> <span data-ttu-id="46bd7-115">因為查詢都具有等冪性，所以無論您執行查詢多少次，它們都不會變更資料。</span><span class="sxs-lookup"><span data-stu-id="46bd7-115">Since the queries are idempotent, they won't change the data no matter how many times you run a query.</span></span> <span data-ttu-id="46bd7-116">因此，您不必受限於交易端使用的任何 DDD 模式，例如彙總及其他模式，這就是查詢與交易區域分開的原因。</span><span class="sxs-lookup"><span data-stu-id="46bd7-116">Therefore, you don't need to be restricted by any DDD pattern used in the transactional side, like aggregates and other patterns, and that is why queries are separated from the transactional area.</span></span> <span data-ttu-id="46bd7-117">您可以查詢資料庫，以找出 UI 所需的資料，並傳回不需要在任何地方以靜態方式定義的動態 ViewModel， (沒有) Viewmodel 的類別，除了 SQL 語句本身之外。</span><span class="sxs-lookup"><span data-stu-id="46bd7-117">You query the database for the data that the UI needs and return a dynamic ViewModel that does not need to be statically defined anywhere (no classes for the ViewModels) except in the SQL statements themselves.</span></span>

<span data-ttu-id="46bd7-118">因為這種方法很簡單，所以查詢端所需的程式碼 (例如使用 [Dapper](https://github.com/StackExchange/Dapper)) 等微型 ORM 的程式碼，可以在 [相同的 Web API 專案內](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Queries/OrderQueries.cs)執行。</span><span class="sxs-lookup"><span data-stu-id="46bd7-118">Since this approach is simple, the code required for the queries side (such as code using a micro ORM like [Dapper](https://github.com/StackExchange/Dapper)) can be implemented [within the same Web API project](https://github.com/dotnet-architecture/eShopOnContainers/blob/master/src/Services/Ordering/Ordering.API/Application/Queries/OrderQueries.cs).</span></span> <span data-ttu-id="46bd7-119">圖7-4 顯示此方法。</span><span class="sxs-lookup"><span data-stu-id="46bd7-119">Figure 7-4 shows this approach.</span></span> <span data-ttu-id="46bd7-120">查詢是在 eShopOnContainers 解決方案內的 **Ordering.API** 微服務專案中所定義。</span><span class="sxs-lookup"><span data-stu-id="46bd7-120">The queries are defined in the **Ordering.API** microservice project within the eShopOnContainers solution.</span></span>

![排序. API 專案的 [查詢] 資料夾的螢幕擷取畫面。](./media/cqrs-microservice-reads/ordering-api-queries-folder.png)

<span data-ttu-id="46bd7-122">**圖 7-4**。</span><span class="sxs-lookup"><span data-stu-id="46bd7-122">**Figure 7-4**.</span></span> <span data-ttu-id="46bd7-123">eShopOnContainers 訂購微服務中的查詢</span><span class="sxs-lookup"><span data-stu-id="46bd7-123">Queries in the Ordering microservice in eShopOnContainers</span></span>

## <a name="use-viewmodels-specifically-made-for-client-apps-independent-from-domain-model-constraints"></a><span data-ttu-id="46bd7-124">使用專為用戶端應用程式建立的 ViewModel，獨立於網域模型限制式之外</span><span class="sxs-lookup"><span data-stu-id="46bd7-124">Use ViewModels specifically made for client apps, independent from domain model constraints</span></span>

<span data-ttu-id="46bd7-125">因為執行查詢是為取得用戶端應用程式所需要的資料，所以可以根據查詢傳回的資料，專為用戶端建立傳回型別。</span><span class="sxs-lookup"><span data-stu-id="46bd7-125">Since the queries are performed to obtain the data needed by the client applications, the returned type can be specifically made for the clients, based on the data returned by the queries.</span></span> <span data-ttu-id="46bd7-126">這些模型或資料傳輸物件 (DTO)，稱為 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="46bd7-126">These models, or Data Transfer Objects (DTOs), are called ViewModels.</span></span>

<span data-ttu-id="46bd7-127">傳回的資料 (ViewModel) 可以是多個實體或資料庫多資料表的聯結資料結果，甚至可以是跨多個在交易區域網域模型中定義的彙總結果。</span><span class="sxs-lookup"><span data-stu-id="46bd7-127">The returned data (ViewModel) can be the result of joining data from multiple entities or tables in the database, or even across multiple aggregates defined in the domain model for the transactional area.</span></span> <span data-ttu-id="46bd7-128">在此情況下，因為您要建立與網域模型無關的查詢，所以會忽略匯總界限和條件約束，而且您可以自由地查詢任何您可能需要的資料表和資料行。</span><span class="sxs-lookup"><span data-stu-id="46bd7-128">In this case, because you are creating queries independent of the domain model, the aggregates boundaries and constraints are ignored and you're free to query any table and column you might need.</span></span> <span data-ttu-id="46bd7-129">此方法為開發人員建立或更新查詢提供了極大的彈性和生產力。</span><span class="sxs-lookup"><span data-stu-id="46bd7-129">This approach provides great flexibility and productivity for the developers creating or updating the queries.</span></span>

<span data-ttu-id="46bd7-130">Viewmodel 可以是在類別中定義的靜態類型 (如同在訂購微服務) 中執行一樣。</span><span class="sxs-lookup"><span data-stu-id="46bd7-130">The ViewModels can be static types defined in classes (as is implemented in the ordering microservice).</span></span> <span data-ttu-id="46bd7-131">或者，您也可以根據執行的查詢來動態建立它們，這對開發人員而言是敏捷的。</span><span class="sxs-lookup"><span data-stu-id="46bd7-131">Or they can be created dynamically based on the queries performed, which is agile for developers.</span></span>

## <a name="use-dapper-as-a-micro-orm-to-perform-queries"></a><span data-ttu-id="46bd7-132">將 Dapper 用作微 ORM 以執行查詢</span><span class="sxs-lookup"><span data-stu-id="46bd7-132">Use Dapper as a micro ORM to perform queries</span></span>

<span data-ttu-id="46bd7-133">您可以使用任何微 ORM、Entity Framework Core 或甚至純 ADO.NET 進行查詢。</span><span class="sxs-lookup"><span data-stu-id="46bd7-133">You can use any micro ORM, Entity Framework Core, or even plain ADO.NET for querying.</span></span> <span data-ttu-id="46bd7-134">在範例應用程式中，eShopOnContainers 的訂購微服務選取 Dapper 為熱門的微 ORM 範例。</span><span class="sxs-lookup"><span data-stu-id="46bd7-134">In the sample application, Dapper was selected for the ordering microservice in eShopOnContainers as a good example of a popular micro ORM.</span></span> <span data-ttu-id="46bd7-135">它可以執行具有絕佳效能的純 SQL 查詢，因為它是輕量的架構。</span><span class="sxs-lookup"><span data-stu-id="46bd7-135">It can run plain SQL queries with great performance, because it's a light framework.</span></span> <span data-ttu-id="46bd7-136">您可以使用 Dapper 撰寫能存取並聯結多份資料表的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="46bd7-136">Using Dapper, you can write a SQL query that can access and join multiple tables.</span></span>

<span data-ttu-id="46bd7-137">Dapper 是開放原始碼專案 (原創者為 Sam Saffron)，屬於 [Stack Overflow](https://stackoverflow.com/) (堆疊溢位) 的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="46bd7-137">Dapper is an open-source project (original created by Sam Saffron), and is part of the building blocks used in [Stack Overflow](https://stackoverflow.com/).</span></span> <span data-ttu-id="46bd7-138">若要使用 Dapper，您只需要透過 [Dapper NuGet 套件](https://www.nuget.org/packages/Dapper)安裝它即可，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="46bd7-138">To use Dapper, you just need to install it through the [Dapper NuGet package](https://www.nuget.org/packages/Dapper), as shown in the following figure:</span></span>

![NuGet 套件視圖中 Dapper 套件的螢幕擷取畫面。](./media/cqrs-microservice-reads/drapper-package-nuget.png)

<span data-ttu-id="46bd7-140">您也需要加入指示詞 `using` ，讓您的程式碼可以存取 Dapper 擴充方法。</span><span class="sxs-lookup"><span data-stu-id="46bd7-140">You also need to add a `using` directive so your code has access to the Dapper extension methods.</span></span>

<span data-ttu-id="46bd7-141">當您在程式碼中使用 Dapper 時，您可直接使用 <xref:System.Data.SqlClient> 命名空間提供的 <xref:System.Data.SqlClient.SqlConnection> 類別。</span><span class="sxs-lookup"><span data-stu-id="46bd7-141">When you use Dapper in your code, you directly use the <xref:System.Data.SqlClient.SqlConnection> class available in the <xref:System.Data.SqlClient> namespace.</span></span> <span data-ttu-id="46bd7-142">透過 QueryAsync 方法和其他擴充類別的擴充方法 <xref:System.Data.SqlClient.SqlConnection> ，您可以直接且高效能的方式執行查詢。</span><span class="sxs-lookup"><span data-stu-id="46bd7-142">Through the QueryAsync method and other extension methods that extend the <xref:System.Data.SqlClient.SqlConnection> class, you can run queries in a straightforward and performant way.</span></span>

## <a name="dynamic-versus-static-viewmodels"></a><span data-ttu-id="46bd7-143">動態 ViewModel 與靜態 ViewModel</span><span class="sxs-lookup"><span data-stu-id="46bd7-143">Dynamic versus static ViewModels</span></span>

<span data-ttu-id="46bd7-144">從伺服器端將 ViewModel 傳回用戶端應用程式時，您可以將這些 ViewModel 視為不同於您實體模型內部網域實體的 DTO (資料傳輸物件)，因為 ViewModel 是依用戶端應用程式需要的方式保留資料。</span><span class="sxs-lookup"><span data-stu-id="46bd7-144">When returning ViewModels from the server-side to client apps, you can think about those ViewModels as DTOs (Data Transfer Objects) that can be different to the internal domain entities of your entity model because the ViewModels hold the data the way the client app needs.</span></span> <span data-ttu-id="46bd7-145">因此，在許多情況下，您可以彙總來自多個網域實體的資料，並根據用戶端應用程式需要該資料的方式精確撰寫 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="46bd7-145">Therefore, in many cases, you can aggregate data coming from multiple domain entities and compose the ViewModels precisely according to how the client app needs that data.</span></span>

<span data-ttu-id="46bd7-146">這些 Viewmodel 或 Dto 可以明確地定義 (為數據持有者類別) ，就像 `OrderSummary` 稍後的程式碼片段中所示的類別一樣。</span><span class="sxs-lookup"><span data-stu-id="46bd7-146">Those ViewModels or DTOs can be defined explicitly (as data holder classes), like the `OrderSummary` class shown in a later code snippet.</span></span> <span data-ttu-id="46bd7-147">或者，您可以只根據查詢傳回的屬性，將動態 Viewmodel 或動態 Dto 傳回為動態類型。</span><span class="sxs-lookup"><span data-stu-id="46bd7-147">Or, you could just return dynamic ViewModels or dynamic DTOs based on the attributes returned by your queries as a dynamic type.</span></span>

### <a name="viewmodel-as-dynamic-type"></a><span data-ttu-id="46bd7-148">ViewModel 作為動態類型</span><span class="sxs-lookup"><span data-stu-id="46bd7-148">ViewModel as dynamic type</span></span>

<span data-ttu-id="46bd7-149">如下列程式碼所示，透過傳回在內部以查詢所傳回屬性為基礎的「動態」類型，查詢可以直接傳回 `ViewModel`。</span><span class="sxs-lookup"><span data-stu-id="46bd7-149">As shown in the following code, a `ViewModel` can be directly returned by the queries by just returning a *dynamic* type that internally is based on the attributes returned by a query.</span></span> <span data-ttu-id="46bd7-150">這表示要傳回的屬性子集是以查詢本身為基礎。</span><span class="sxs-lookup"><span data-stu-id="46bd7-150">That means that the subset of attributes to be returned is based on the query itself.</span></span> <span data-ttu-id="46bd7-151">因此，如果您在查詢或聯結中新增新的資料行，該資料會以動態方式新增至傳回的 `ViewModel`。</span><span class="sxs-lookup"><span data-stu-id="46bd7-151">Therefore, if you add a new column to the query or join, that data is dynamically added to the returned `ViewModel`.</span></span>

```csharp
using Dapper;
using Microsoft.Extensions.Configuration;
using System.Data.SqlClient;
using System.Threading.Tasks;
using System.Dynamic;
using System.Collections.Generic;

public class OrderQueries : IOrderQueries
{
    public async Task<IEnumerable<dynamic>> GetOrdersAsync()
    {
        using (var connection = new SqlConnection(_connectionString))
        {
            connection.Open();
            return await connection.QueryAsync<dynamic>(
                @"SELECT o.[Id] as ordernumber,
                o.[OrderDate] as [date],os.[Name] as [status],
                SUM(oi.units*oi.unitprice) as total
                FROM [ordering].[Orders] o
                LEFT JOIN[ordering].[orderitems] oi ON o.Id = oi.orderid
                LEFT JOIN[ordering].[orderstatus] os on o.OrderStatusId = os.Id
                GROUP BY o.[Id], o.[OrderDate], os.[Name]");
        }
    }
}
```

<span data-ttu-id="46bd7-152">重點是，透過使用動態類型，傳回的資料集合會以動態方式組合成 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="46bd7-152">The important point is that by using a dynamic type, the returned collection of data is dynamically assembled as the ViewModel.</span></span>

<span data-ttu-id="46bd7-153">**專業人員：** 每當您更新查詢的 SQL 句子時，這個方法就能減少修改靜態 ViewModel 類別的需求，讓這種設計方法在撰寫程式碼、直接且快速地在未來的變更中發展時變得敏捷。</span><span class="sxs-lookup"><span data-stu-id="46bd7-153">**Pros:** This approach reduces the need to modify static ViewModel classes whenever you update the SQL sentence of a query, making this design approach agile when coding, straightforward, and quick to evolve in regard to future changes.</span></span>

<span data-ttu-id="46bd7-154">**缺點：** 長期來看，動態類型對清晰度和服務與用戶端應用程式的相容性可能造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="46bd7-154">**Cons:** In the long term, dynamic types can negatively impact the clarity and the compatibility of a service with client apps.</span></span> <span data-ttu-id="46bd7-155">此外，如果使用動態類型，像 Swashbuckle 這類的中介軟體無法提供傳回型別的同級文件。</span><span class="sxs-lookup"><span data-stu-id="46bd7-155">In addition, middleware software like Swashbuckle cannot provide the same level of documentation on returned types if using dynamic types.</span></span>

### <a name="viewmodel-as-predefined-dto-classes"></a><span data-ttu-id="46bd7-156">ViewModel 作為預先定義的 DTO 類別</span><span class="sxs-lookup"><span data-stu-id="46bd7-156">ViewModel as predefined DTO classes</span></span>

<span data-ttu-id="46bd7-157">**專業人員**：擁有靜態、預先定義的 ViewModel 類別，例如以明確 DTO 類別為基礎的「合約」，對於公用 api （也適用于長期微服務）來說，也是較好的方法，即使它們只由相同的應用程式使用也是如此。</span><span class="sxs-lookup"><span data-stu-id="46bd7-157">**Pros**: Having static, predefined ViewModel classes, like "contracts" based on explicit DTO classes, is definitely better for public APIs but also for long-term microservices, even if they are only used by the same application.</span></span>

<span data-ttu-id="46bd7-158">如要指定 Swagger 的回應類型，您需要使用明確的 DTO 類別作為傳回型別。</span><span class="sxs-lookup"><span data-stu-id="46bd7-158">If you want to specify response types for Swagger, you need to use explicit DTO classes as the return type.</span></span> <span data-ttu-id="46bd7-159">因此，預先定義的 DTO 類別可讓您提供更豐富的 Swagger 資訊。</span><span class="sxs-lookup"><span data-stu-id="46bd7-159">Therefore, predefined DTO classes allow you to offer richer information from Swagger.</span></span> <span data-ttu-id="46bd7-160">這會在使用 API 時改善 API 文件和相容性。</span><span class="sxs-lookup"><span data-stu-id="46bd7-160">That improves the API documentation and compatibility when consuming an API.</span></span>

<span data-ttu-id="46bd7-161">**缺點：** 如前所述，更新程式碼時，它會採用更多步驟來更新 DTO 類別。</span><span class="sxs-lookup"><span data-stu-id="46bd7-161">**Cons**: As mentioned earlier, when updating the code, it takes some more steps to update the DTO classes.</span></span>

<span data-ttu-id="46bd7-162">以 *我們的經驗為基礎的秘訣*：在 EShopOnContainers 的訂購微服務上所執行的查詢中，我們開始使用動態 viewmodel 進行開發，因為它在早期開發階段是直接且敏捷的。</span><span class="sxs-lookup"><span data-stu-id="46bd7-162">*Tip based on our experience*: In the queries implemented at the Ordering microservice in eShopOnContainers, we started developing by using dynamic ViewModels as it was straightforward and agile on the early development stages.</span></span> <span data-ttu-id="46bd7-163">但在穩定開發之後，我們選擇重構 Api，並針對 Viewmodel 使用靜態或預先定義的 Dto，因為更清楚地讓微服務的取用者知道明確的 DTO 型別，用來作為「合約」。</span><span class="sxs-lookup"><span data-stu-id="46bd7-163">But, once the development was stabilized, we chose to refactor the APIs and use static or pre-defined DTOs for the ViewModels, because it is clearer for the microservice's consumers to know explicit DTO types, used as "contracts".</span></span>

<span data-ttu-id="46bd7-164">在下例中，您會看到查詢如何使用明確的 ViewModel DTO 類別：OrderSummary 類別，傳回資料。</span><span class="sxs-lookup"><span data-stu-id="46bd7-164">In the following example, you can see how the query is returning data by using an explicit ViewModel DTO class: the OrderSummary class.</span></span>

```csharp
using Dapper;
using Microsoft.Extensions.Configuration;
using System.Data.SqlClient;
using System.Threading.Tasks;
using System.Dynamic;
using System.Collections.Generic;

public class OrderQueries : IOrderQueries
{
  public async Task<IEnumerable<OrderSummary>> GetOrdersAsync()
    {
        using (var connection = new SqlConnection(_connectionString))
        {
            connection.Open();
            return await connection.QueryAsync<OrderSummary>(
                  @"SELECT o.[Id] as ordernumber,
                  o.[OrderDate] as [date],os.[Name] as [status],
                  SUM(oi.units*oi.unitprice) as total
                  FROM [ordering].[Orders] o
                  LEFT JOIN[ordering].[orderitems] oi ON  o.Id = oi.orderid
                  LEFT JOIN[ordering].[orderstatus] os on o.OrderStatusId = os.Id
                  GROUP BY o.[Id], o.[OrderDate], os.[Name]
                  ORDER BY o.[Id]");
        }
    }
}
```

#### <a name="describe-response-types-of-web-apis"></a><span data-ttu-id="46bd7-165">描述 Web API 的回應類型</span><span class="sxs-lookup"><span data-stu-id="46bd7-165">Describe response types of Web APIs</span></span>

<span data-ttu-id="46bd7-166">取用 web Api 和微服務的開發人員最關心的是傳回的內容，特別是回應類型和錯誤碼（如果不是標準)  (）。</span><span class="sxs-lookup"><span data-stu-id="46bd7-166">Developers consuming web APIs and microservices are most concerned with what is returned—specifically response types and error codes (if not standard).</span></span> <span data-ttu-id="46bd7-167">回應類型會在 XML 批註和資料批註中處理。</span><span class="sxs-lookup"><span data-stu-id="46bd7-167">The response types are handled in the XML comments and data annotations.</span></span>

<span data-ttu-id="46bd7-168">Swagger UI 中沒有正確的文件，取用者就不清楚應該傳回哪些類型或可以傳回哪些 HTTP 代碼。</span><span class="sxs-lookup"><span data-stu-id="46bd7-168">Without proper documentation in the Swagger UI, the consumer lacks knowledge of what types are being returned or what HTTP codes can be returned.</span></span> <span data-ttu-id="46bd7-169">已藉由新增 <xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute?displayProperty=nameWithType> 來修正該問題，因此 Swashbuckle 可以產生 API 傳回模型和值的更多相關資訊，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="46bd7-169">That problem is fixed by adding the <xref:Microsoft.AspNetCore.Mvc.ProducesResponseTypeAttribute?displayProperty=nameWithType>, so Swashbuckle can generate richer information about the API return model and values, as shown in the following code:</span></span>

```csharp
namespace Microsoft.eShopOnContainers.Services.Ordering.API.Controllers
{
    [Route("api/v1/[controller]")]
    [Authorize]
    public class OrdersController : Controller
    {
        //Additional code...
        [Route("")]
        [HttpGet]
        [ProducesResponseType(typeof(IEnumerable<OrderSummary>),
            (int)HttpStatusCode.OK)]
        public async Task<IActionResult> GetOrders()
        {
            var userid = _identityService.GetUserIdentity();
            var orders = await _orderQueries
                .GetOrdersFromUserAsync(Guid.Parse(userid));
            return Ok(orders);
        }
    }
}
```

<span data-ttu-id="46bd7-170">不過，`ProducesResponseType` 屬性不能用作動態類型，卻需要使用像 `OrderSummary` ViewModel DTO 的明確類型，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="46bd7-170">However, the `ProducesResponseType` attribute cannot use dynamic as a type but requires to use explicit types, like the `OrderSummary` ViewModel DTO, shown in the following example:</span></span>

```csharp
public class OrderSummary
{
    public int ordernumber { get; set; }
    public DateTime date { get; set; }
    public string status { get; set; }
    public double total { get; set; }
}
```

<span data-ttu-id="46bd7-171">這是就長期而言，明確的傳回型別優於動態類型的另一個原因。</span><span class="sxs-lookup"><span data-stu-id="46bd7-171">This is another reason why explicit returned types are better than dynamic types, in the long term.</span></span> <span data-ttu-id="46bd7-172">使用屬性時 `ProducesResponseType` ，您也可以指定可能的 HTTP 錯誤/代碼的預期結果，例如200、400等等。</span><span class="sxs-lookup"><span data-stu-id="46bd7-172">When using the `ProducesResponseType` attribute, you can also specify what is the expected outcome regarding possible HTTP errors/codes, like 200, 400, etc.</span></span>

<span data-ttu-id="46bd7-173">在下圖中，您會看到 Swagger UI 如何顯示 ResponseType 資訊。</span><span class="sxs-lookup"><span data-stu-id="46bd7-173">In the following image, you can see how Swagger UI shows the ResponseType information.</span></span>

![訂購 API 的 Swagger UI 頁面螢幕擷取畫面。](./media/cqrs-microservice-reads/swagger-ordering-http-api.png)

<span data-ttu-id="46bd7-175">**圖 7-5**.</span><span class="sxs-lookup"><span data-stu-id="46bd7-175">**Figure 7-5**.</span></span> <span data-ttu-id="46bd7-176">顯示 Web API 回應類型和可能 HTTP 狀態碼的 Swagger UI</span><span class="sxs-lookup"><span data-stu-id="46bd7-176">Swagger UI showing response types and possible HTTP status codes from a Web API</span></span>

<span data-ttu-id="46bd7-177">影像會根據 ViewModel 類型以及可傳回的可能 HTTP 狀態碼，顯示一些範例值。</span><span class="sxs-lookup"><span data-stu-id="46bd7-177">The image shows some example values based on the ViewModel types and the possible HTTP status codes that can be returned.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46bd7-178">其他資源</span><span class="sxs-lookup"><span data-stu-id="46bd7-178">Additional resources</span></span>

- <span data-ttu-id="46bd7-179">**Dapper**</span><span class="sxs-lookup"><span data-stu-id="46bd7-179">**Dapper**</span></span>  
 <https://github.com/StackExchange/dapper-dot-net>

- <span data-ttu-id="46bd7-180">**Julie Lerman。資料點-Dapper、Entity Framework 和混合式應用程式 (MSDN 雜誌文章)**</span><span class="sxs-lookup"><span data-stu-id="46bd7-180">**Julie Lerman. Data Points - Dapper, Entity Framework and Hybrid Apps (MSDN magazine article)**</span></span>  
  <https://docs.microsoft.com/archive/msdn-magazine/2016/may/data-points-dapper-entity-framework-and-hybrid-apps>

- <span data-ttu-id="46bd7-181">**使用 Swagger 來 ASP.NET Core Web API 說明頁面**</span><span class="sxs-lookup"><span data-stu-id="46bd7-181">**ASP.NET Core Web API Help Pages using Swagger**</span></span>  
  <https://docs.microsoft.com/aspnet/core/tutorials/web-api-help-pages-using-swagger?tabs=visual-studio>

>[!div class="step-by-step"]
><span data-ttu-id="46bd7-182">[上一個](eshoponcontainers-cqrs-ddd-microservice.md) 
>[下一步](ddd-oriented-microservice.md)</span><span class="sxs-lookup"><span data-stu-id="46bd7-182">[Previous](eshoponcontainers-cqrs-ddd-microservice.md)
[Next](ddd-oriented-microservice.md)</span></span>
