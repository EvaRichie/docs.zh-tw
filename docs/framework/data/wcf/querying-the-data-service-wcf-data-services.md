---
title: 查詢資料服務 (WCF 資料服務)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, client library
- WCF Data Services, querying
- WCF Data Services, accessing data
ms.assetid: 823e9444-27aa-4f1f-be8e-0486d67f54c0
ms.openlocfilehash: 8ae4b4b9938f72f4f4fc011e180cd69440ec3dd9
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84201763"
---
# <a name="querying-the-data-service-wcf-data-services"></a><span data-ttu-id="1d220-102">查詢資料服務 (WCF 資料服務)</span><span class="sxs-lookup"><span data-stu-id="1d220-102">Querying the Data Service (WCF Data Services)</span></span>

<span data-ttu-id="1d220-103">WCF Data Services 用戶端程式庫可讓您使用熟悉的 .NET Framework 程式設計模式（包括使用語言整合式查詢（LINQ））對資料服務執行查詢。</span><span class="sxs-lookup"><span data-stu-id="1d220-103">The WCF Data Services client library enables you to execute queries against a data service by using familiar .NET Framework programming patterns, including using language integrated query (LINQ).</span></span> <span data-ttu-id="1d220-104">用戶端程式庫會將查詢轉譯為 HTTP GET 要求訊息，該查詢在用戶端上已定義為 <xref:System.Data.Services.Client.DataServiceQuery%601> 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="1d220-104">The client library translates a query, which is defined on the client as an instance of the <xref:System.Data.Services.Client.DataServiceQuery%601> class, into an HTTP GET request message.</span></span> <span data-ttu-id="1d220-105">程式庫會接收回應訊息，並將它轉譯為用戶端資料服務類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="1d220-105">The library receives the response message and translates it into instances of client data service classes.</span></span> <span data-ttu-id="1d220-106">這些類別會由 <xref:System.Data.Services.Client.DataServiceContext> 所屬的 <xref:System.Data.Services.Client.DataServiceQuery%601> 追蹤。</span><span class="sxs-lookup"><span data-stu-id="1d220-106">These classes are tracked by the <xref:System.Data.Services.Client.DataServiceContext> to which the <xref:System.Data.Services.Client.DataServiceQuery%601> belongs.</span></span>

## <a name="data-service-queries"></a><span data-ttu-id="1d220-107">資料服務查詢</span><span class="sxs-lookup"><span data-stu-id="1d220-107">Data Service Queries</span></span>

<span data-ttu-id="1d220-108"><xref:System.Data.Services.Client.DataServiceQuery%601> 泛型類別表示傳回零個或多個實體型別執行個體之集合的查詢。</span><span class="sxs-lookup"><span data-stu-id="1d220-108">The <xref:System.Data.Services.Client.DataServiceQuery%601> generic class represents a query that returns a collection of zero or more entity type instances.</span></span> <span data-ttu-id="1d220-109">資料服務查詢永遠屬於現有的資料服務內容。</span><span class="sxs-lookup"><span data-stu-id="1d220-109">A data service query always belongs to an existing data service context.</span></span> <span data-ttu-id="1d220-110">此內容會維持撰寫及執行查詢所需的服務 URI 和中繼資料 (Metadata) 資訊。</span><span class="sxs-lookup"><span data-stu-id="1d220-110">This context maintains the service URI and metadata information that is required to compose and execute the query.</span></span>

<span data-ttu-id="1d220-111">當您使用 [**加入服務參考**] 對話方塊將資料服務加入至以 .NET Framework 為基礎的用戶端應用程式時，會建立繼承自類別的實體容器類別 <xref:System.Data.Services.Client.DataServiceContext> 。</span><span class="sxs-lookup"><span data-stu-id="1d220-111">When you use the **Add Service Reference** dialog to add a data service to a .NET Framework-based client application, an entity container class is created that inherits from the <xref:System.Data.Services.Client.DataServiceContext> class.</span></span> <span data-ttu-id="1d220-112">這個類別包含會傳回具型別之 <xref:System.Data.Services.Client.DataServiceQuery%601> 執行個體的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d220-112">This class includes properties that return typed <xref:System.Data.Services.Client.DataServiceQuery%601> instances.</span></span> <span data-ttu-id="1d220-113">每一個實體集都有一個屬性，並由資料服務公開。</span><span class="sxs-lookup"><span data-stu-id="1d220-113">There is one property for each entity set that the data service exposes.</span></span> <span data-ttu-id="1d220-114">這些屬性可以讓具型別 <xref:System.Data.Services.Client.DataServiceQuery%601> 執行個體的建立作業更為容易。</span><span class="sxs-lookup"><span data-stu-id="1d220-114">These properties make it easier to create an instance of a typed <xref:System.Data.Services.Client.DataServiceQuery%601>.</span></span>

<span data-ttu-id="1d220-115">以下情況下會執行查詢：</span><span class="sxs-lookup"><span data-stu-id="1d220-115">A query is executed in the following scenarios:</span></span>

- <span data-ttu-id="1d220-116">結果以隱含方式列舉時，例如：</span><span class="sxs-lookup"><span data-stu-id="1d220-116">When results are enumerated implicitly, such as:</span></span>

  - <span data-ttu-id="1d220-117">列舉代表 <xref:System.Data.Services.Client.DataServiceContext> 上的屬性及實體集時，例如 `foreach` (C#) 或 `For Each` (Visual Basic) 迴圈期間。</span><span class="sxs-lookup"><span data-stu-id="1d220-117">When a property on the <xref:System.Data.Services.Client.DataServiceContext> that represents and entity set is enumerated, such as during a `foreach` (C#) or `For Each` (Visual Basic) loop.</span></span>

  - <span data-ttu-id="1d220-118">查詢已指派至 `List` 集合時。</span><span class="sxs-lookup"><span data-stu-id="1d220-118">When the query is assigned to a `List` collection.</span></span>

- <span data-ttu-id="1d220-119">明確呼叫 <xref:System.Data.Services.Client.DataServiceQuery%601.Execute%2A> 或 <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> 方法時。</span><span class="sxs-lookup"><span data-stu-id="1d220-119">When the <xref:System.Data.Services.Client.DataServiceQuery%601.Execute%2A> or <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> method is explicitly called.</span></span>

- <span data-ttu-id="1d220-120">當呼叫 LINQ 查詢執行運算子 (如 <xref:System.Linq.Enumerable.First%2A> 或 <xref:System.Linq.Enumerable.Single%2A>) 時。</span><span class="sxs-lookup"><span data-stu-id="1d220-120">When a LINQ query execution operator, such as <xref:System.Linq.Enumerable.First%2A> or <xref:System.Linq.Enumerable.Single%2A> is called.</span></span>

<span data-ttu-id="1d220-121">下列查詢在執行時會傳回 Northwind 資料服務中的所有 `Customers` 實體：</span><span class="sxs-lookup"><span data-stu-id="1d220-121">The following query, when it is executed, returns all `Customers` entities in the Northwind data service:</span></span>

[!code-csharp[Astoria Northwind Client#GetAllCustomersSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getallcustomersspecific)]
[!code-vb[Astoria Northwind Client#GetAllCustomersSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getallcustomersspecific)]

<span data-ttu-id="1d220-122">如需詳細資訊，請參閱[如何：執行資料服務查詢](how-to-execute-data-service-queries-wcf-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="1d220-122">For more information, see [How to: Execute Data Service Queries](how-to-execute-data-service-queries-wcf-data-services.md).</span></span>

<span data-ttu-id="1d220-123">WCF Data Services 用戶端支援晚期繫結物件的查詢，例如當您在 c # 中使用*動態*類型時。</span><span class="sxs-lookup"><span data-stu-id="1d220-123">The WCF Data Services client supports queries for late-bound objects, such as when you use the *dynamic* type in C#.</span></span> <span data-ttu-id="1d220-124">不過，基於效能的考慮，您應該一律針對資料服務撰寫強型別查詢。</span><span class="sxs-lookup"><span data-stu-id="1d220-124">However, for performance reasons you should always compose strongly typed queries against the data service.</span></span> <span data-ttu-id="1d220-125">用戶端不支援 <xref:System.Tuple> 型別和動態物件。</span><span class="sxs-lookup"><span data-stu-id="1d220-125">The <xref:System.Tuple> type and dynamic objects are not supported by the client.</span></span>

## <a name="linq-queries"></a><span data-ttu-id="1d220-126">LINQ 查詢</span><span class="sxs-lookup"><span data-stu-id="1d220-126">LINQ Queries</span></span>

<span data-ttu-id="1d220-127">由於 <xref:System.Data.Services.Client.DataServiceQuery%601> 類別 <xref:System.Linq.IQueryable%601> 會執行 LINQ 所定義的介面，因此 WCF Data Services 用戶端程式庫可以將實體集資料的 LINQ 查詢轉換為 URI，以代表針對資料服務資源評估的查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="1d220-127">Because the <xref:System.Data.Services.Client.DataServiceQuery%601> class implements the <xref:System.Linq.IQueryable%601> interface defined by LINQ, the WCF Data Services client library is able to transform LINQ queries against entity set data into a URI that represents a query expression evaluated against a data service resource.</span></span> <span data-ttu-id="1d220-128">下列範例是 LINQ 查詢，其相當於以前的 <xref:System.Data.Services.Client.DataServiceQuery%601>，它會傳回運費成本超過 $30 的 `Orders`，並依運費成本排序結果：</span><span class="sxs-lookup"><span data-stu-id="1d220-128">The following example is a LINQ query that is equivalent to the previous <xref:System.Data.Services.Client.DataServiceQuery%601> that returns `Orders` that have a freight cost of more than $30 and orders the results by the freight cost:</span></span>

[!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addqueryoptionslinqspecific)]
[!code-vb[Astoria Northwind Client#AddQueryOptionsLinqSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addqueryoptionslinqspecific)]

<span data-ttu-id="1d220-129">此 LINQ 查詢會轉譯成下列查詢 URI，並針對以 Northwind 為基礎的[快速入門](quickstart-wcf-data-services.md)資料服務來執行：</span><span class="sxs-lookup"><span data-stu-id="1d220-129">This LINQ query is translated into the following query URI that is executed against the Northwind-based [quickstart](quickstart-wcf-data-services.md) data service:</span></span>

```http
http://localhost:12345/Northwind.svc/Orders?Orderby=ShippedDate&?filter=Freight gt 30
```

> [!NOTE]
> <span data-ttu-id="1d220-130">可以用 LINQ 語法表示的查詢集合會比在資料服務所使用之具像狀態傳輸 (REST) 架構 URI 語法中啟用的查詢集合更廣泛。</span><span class="sxs-lookup"><span data-stu-id="1d220-130">The set of queries expressible in the LINQ syntax is broader than those enabled in the representational state transfer (REST)-based URI syntax that is used by data services.</span></span> <span data-ttu-id="1d220-131">當查詢無法對應至目標資料服務中的 URI 時，就會引發 <xref:System.NotSupportedException>。</span><span class="sxs-lookup"><span data-stu-id="1d220-131">A <xref:System.NotSupportedException> is raised when the query cannot be mapped to a URI in the target data service.</span></span>

<span data-ttu-id="1d220-132">如需詳細資訊，請參閱[LINQ 考慮](linq-considerations-wcf-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="1d220-132">For more information, see [LINQ Considerations](linq-considerations-wcf-data-services.md).</span></span>

## <a name="adding-query-options"></a><span data-ttu-id="1d220-133">加入查詢選項</span><span class="sxs-lookup"><span data-stu-id="1d220-133">Adding Query Options</span></span>

<span data-ttu-id="1d220-134">資料服務查詢支援 WCF 資料服務提供的所有查詢選項。</span><span class="sxs-lookup"><span data-stu-id="1d220-134">Data service queries support all the query options that WCF Data Servicess provides.</span></span> <span data-ttu-id="1d220-135">您可以呼叫 <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 方法，將查詢選項附加至 <xref:System.Data.Services.Client.DataServiceQuery%601> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1d220-135">You call the <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> method to append query options to a <xref:System.Data.Services.Client.DataServiceQuery%601> instance.</span></span> <span data-ttu-id="1d220-136"><xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 會傳回新的 <xref:System.Data.Services.Client.DataServiceQuery%601> 執行個體，其相當於原始的查詢，但使用新的查詢選項集。</span><span class="sxs-lookup"><span data-stu-id="1d220-136"><xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> returns a new <xref:System.Data.Services.Client.DataServiceQuery%601> instance that is equivalent to the original query but with the new query option set.</span></span> <span data-ttu-id="1d220-137">下列查詢在執行時會傳回 `Orders`，其係經由 `Freight` 值進行篩選並依 `OrderID` 遞減順序排序：</span><span class="sxs-lookup"><span data-stu-id="1d220-137">The following query, when executed, returns `Orders` that are filtered by the `Freight` value and ordered by the `OrderID`, descending:</span></span>

[!code-csharp[Astoria Northwind Client#AddQueryOptionsSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#addqueryoptionsspecific)]
[!code-vb[Astoria Northwind Client#AddQueryOptionsSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#addqueryoptionsspecific)]

<span data-ttu-id="1d220-138">您可以使用 `$orderby` 查詢選項根據單一屬性來排序及篩選查詢，如下列範例根據 `Orders` 屬性的值篩選及排序傳回的 `Freight` 物件：</span><span class="sxs-lookup"><span data-stu-id="1d220-138">You can use the `$orderby` query option to both order and filter a query based on a single property, as in the following example that filters and orders the returned `Orders` objects based on the value of the `Freight` property:</span></span>

[!code-csharp[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#orderwithfilter)]
[!code-vb[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#orderwithfilter)]

<span data-ttu-id="1d220-139">您可以連續呼叫 <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 方法來建構複雜的查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="1d220-139">You can call the <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> method consecutively to construct complex query expressions.</span></span> <span data-ttu-id="1d220-140">如需詳細資訊，請參閱[如何：將查詢選項加入至資料服務查詢](how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="1d220-140">For more information, see [How to: Add Query Options to a Data Service Query](how-to-add-query-options-to-a-data-service-query-wcf-data-services.md).</span></span>

<span data-ttu-id="1d220-141">查詢選項提供您另一種表示 LINQ 查詢語法元件的方式。</span><span class="sxs-lookup"><span data-stu-id="1d220-141">Query options give you another way to express the syntactic components of a LINQ query.</span></span> <span data-ttu-id="1d220-142">如需詳細資訊，請參閱[LINQ 考慮](linq-considerations-wcf-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="1d220-142">For more information, see [LINQ Considerations](linq-considerations-wcf-data-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1d220-143">您無法使用 `$select` 方法，將 <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> 查詢選項加入至查詢 URI。</span><span class="sxs-lookup"><span data-stu-id="1d220-143">The `$select` query option cannot be added to a query URI by using the <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> method.</span></span> <span data-ttu-id="1d220-144">建議您使用 LINQ <xref:System.Linq.Enumerable.Select%2A> 方法，讓用戶端在要求 URI 中產生 `$select` 查詢選項。</span><span class="sxs-lookup"><span data-stu-id="1d220-144">We recommend that you use the LINQ <xref:System.Linq.Enumerable.Select%2A> method to have the client generate the `$select` query option in the request URI.</span></span>

<a name="executingQueries"></a>

## <a name="client-versus-server-execution"></a><span data-ttu-id="1d220-145">用戶端與伺服器執行的比較</span><span class="sxs-lookup"><span data-stu-id="1d220-145">Client versus Server Execution</span></span>

<span data-ttu-id="1d220-146">用戶端會以兩個部分執行查詢。</span><span class="sxs-lookup"><span data-stu-id="1d220-146">The client executes a query in two parts.</span></span> <span data-ttu-id="1d220-147">如果可能，查詢中的運算式會先在用戶端上進行評估，然後產生 URI 架構的查詢，並將其傳送至資料服務，以便針對服務中的資料進行評估。</span><span class="sxs-lookup"><span data-stu-id="1d220-147">Whenever possible, expressions in a query are first evaluated on the client, and then a URI-based query is generated and sent to the data service for evaluation against data in the service.</span></span> <span data-ttu-id="1d220-148">請考慮下列 LINQ 查詢：</span><span class="sxs-lookup"><span data-stu-id="1d220-148">Consider the following LINQ query:</span></span>

[!code-csharp[Astoria Northwind Client#LinqQueryClientEvalSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#linqqueryclientevalspecific)]
[!code-vb[Astoria Northwind Client#LinqQueryClientEvalSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#linqqueryclientevalspecific)]

<span data-ttu-id="1d220-149">在此範例中，運算式 `(basePrice – (basePrice * discount))` 會在用戶端上進行評估。</span><span class="sxs-lookup"><span data-stu-id="1d220-149">In this example, the expression `(basePrice – (basePrice * discount))` is evaluated on the client.</span></span> <span data-ttu-id="1d220-150">因此，傳送至資料服務的實際查詢 URI `http://localhost:12345/northwind.svc/Products()?$filter=(UnitPrice gt 90.00M) and substringof('bike',ProductName)` 在 filter 子句中，包含已經計算的十進位值 `90`。</span><span class="sxs-lookup"><span data-stu-id="1d220-150">Because of this, the actual query URI `http://localhost:12345/northwind.svc/Products()?$filter=(UnitPrice gt 90.00M) and substringof('bike',ProductName)` that is sent to the data service contains the already calculated decimal value of `90` in the filter clause.</span></span> <span data-ttu-id="1d220-151">篩選運算式的另一個部分 (包括子字串運算式)，則由資料服務評估。</span><span class="sxs-lookup"><span data-stu-id="1d220-151">The other parts of the filtering expression, including the substring expression, are evaluated by the data service.</span></span> <span data-ttu-id="1d220-152">在用戶端上評估的運算式會遵循 common language runtime （CLR）的語義，而傳送至資料服務的運算式會依賴 OData 通訊協定的資料服務執行。</span><span class="sxs-lookup"><span data-stu-id="1d220-152">Expressions that are evaluated on the client follow common language runtime (CLR) semantics, while expressions sent to the data service rely on the data service implementation of the OData Protocol.</span></span> <span data-ttu-id="1d220-153">您也應該知道這個個別評估的案例可能會造成非預期的結果，例如，當用戶端和服務同時在不同的時區中執行以時間為基礎的評估時。</span><span class="sxs-lookup"><span data-stu-id="1d220-153">You should also be aware of scenarios where this separate evaluation may cause unexpected results, such as when both the client and service perform time-based evaluations in different time zones.</span></span>

## <a name="query-responses"></a><span data-ttu-id="1d220-154">查詢回應</span><span class="sxs-lookup"><span data-stu-id="1d220-154">Query Responses</span></span>

<span data-ttu-id="1d220-155">執行時，<xref:System.Data.Services.Client.DataServiceQuery%601> 會傳回要求之實體類型的 <xref:System.Collections.Generic.IEnumerable%601>。</span><span class="sxs-lookup"><span data-stu-id="1d220-155">When executed, the <xref:System.Data.Services.Client.DataServiceQuery%601> returns an <xref:System.Collections.Generic.IEnumerable%601> of the requested entity type.</span></span> <span data-ttu-id="1d220-156">此查詢結果可以轉型為 <xref:System.Data.Services.Client.QueryOperationResponse%601> 物件，如下列範例：</span><span class="sxs-lookup"><span data-stu-id="1d220-156">This query result can be cast to a <xref:System.Data.Services.Client.QueryOperationResponse%601> object, as in the following example:</span></span>

[!code-csharp[Astoria Northwind Client#GetResponseSpecific](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getresponsespecific)]
[!code-vb[Astoria Northwind Client#GetResponseSpecific](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getresponsespecific)]

<span data-ttu-id="1d220-157">資料服務中代表實體的實體類型執行個體是透過稱為物件具體化的程序，在用戶端上建立的。</span><span class="sxs-lookup"><span data-stu-id="1d220-157">The entity type instances that represent entities in the data service are created on the client by a process called object materialization.</span></span> <span data-ttu-id="1d220-158">如需詳細資訊，請參閱[物件具體化](object-materialization-wcf-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="1d220-158">For more information, see [Object Materialization](object-materialization-wcf-data-services.md).</span></span> <span data-ttu-id="1d220-159"><xref:System.Data.Services.Client.QueryOperationResponse%601> 物件會實作 <xref:System.Collections.Generic.IEnumerable%601> 以提供查詢結果的存取權。</span><span class="sxs-lookup"><span data-stu-id="1d220-159">The <xref:System.Data.Services.Client.QueryOperationResponse%601> object implements <xref:System.Collections.Generic.IEnumerable%601> to provide access to the results of the query.</span></span>

<span data-ttu-id="1d220-160"><xref:System.Data.Services.Client.QueryOperationResponse%601> 還有下列成員，可讓您存取有關查詢結果的其他資訊：</span><span class="sxs-lookup"><span data-stu-id="1d220-160">The <xref:System.Data.Services.Client.QueryOperationResponse%601> also has the following members that enable you to access additional information about a query result:</span></span>

- <span data-ttu-id="1d220-161"><xref:System.Data.Services.Client.OperationResponse.Error%2A> - 取得作業擲回的錯誤 (若有發生錯誤的話)。</span><span class="sxs-lookup"><span data-stu-id="1d220-161"><xref:System.Data.Services.Client.OperationResponse.Error%2A> - gets an error thrown by the operation, if any has occurred.</span></span>

- <span data-ttu-id="1d220-162"><xref:System.Data.Services.Client.OperationResponse.Headers%2A> - 包含與查詢回應相關聯之 HTTP 回應標頭的集合。</span><span class="sxs-lookup"><span data-stu-id="1d220-162"><xref:System.Data.Services.Client.OperationResponse.Headers%2A> - contains the collection of HTTP response headers associated with the query response.</span></span>

- <span data-ttu-id="1d220-163"><xref:System.Data.Services.Client.QueryOperationResponse.Query%2A> - 取得產生 <xref:System.Data.Services.Client.DataServiceQuery%601> 的原始 <xref:System.Data.Services.Client.QueryOperationResponse%601>。</span><span class="sxs-lookup"><span data-stu-id="1d220-163"><xref:System.Data.Services.Client.QueryOperationResponse.Query%2A> - gets the original <xref:System.Data.Services.Client.DataServiceQuery%601> that generated the <xref:System.Data.Services.Client.QueryOperationResponse%601>.</span></span>

- <span data-ttu-id="1d220-164"><xref:System.Data.Services.Client.OperationResponse.StatusCode%2A> - 取得查詢回應的 HTTP 回應碼。</span><span class="sxs-lookup"><span data-stu-id="1d220-164"><xref:System.Data.Services.Client.OperationResponse.StatusCode%2A> - gets the HTTP response code for the query response.</span></span>

- <span data-ttu-id="1d220-165"><xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> - 在 <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> 上呼叫 <xref:System.Data.Services.Client.DataServiceQuery%601> 方法時，取得實體集中的實體總數。</span><span class="sxs-lookup"><span data-stu-id="1d220-165"><xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> - gets the total number of entities in the entity set when the <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> method was called on the <xref:System.Data.Services.Client.DataServiceQuery%601>.</span></span>

- <span data-ttu-id="1d220-166"><xref:System.Data.Services.Client.QueryOperationResponse.GetContinuation%2A> - 傳回包含下一頁結果之 URI 的 <xref:System.Data.Services.Client.DataServiceQueryContinuation> 物件。</span><span class="sxs-lookup"><span data-stu-id="1d220-166"><xref:System.Data.Services.Client.QueryOperationResponse.GetContinuation%2A> - returns a <xref:System.Data.Services.Client.DataServiceQueryContinuation> object that contains the URI of the next page of results.</span></span>

<span data-ttu-id="1d220-167">根據預設，WCF Data Services 只會傳回查詢 URI 所明確選取的資料。</span><span class="sxs-lookup"><span data-stu-id="1d220-167">By default, WCF Data Services only returns data that is explicitly selected by the query URI.</span></span> <span data-ttu-id="1d220-168">它還提供選項可讓您於必要時，從資料服務明確載入其他資料。</span><span class="sxs-lookup"><span data-stu-id="1d220-168">This gives you the option to explicitly load additional data from the data service when it is needed.</span></span> <span data-ttu-id="1d220-169">每次您從資料服務明確載入資料時，就會傳送一個要求至資料服務。</span><span class="sxs-lookup"><span data-stu-id="1d220-169">A request is sent to the data service each time you explicitly load data from the data service.</span></span> <span data-ttu-id="1d220-170">可以明確載入的資料包括相關實體、分頁的回應資料，以及二進位資料流。</span><span class="sxs-lookup"><span data-stu-id="1d220-170">Data that can be explicitly loaded includes related entities, paged response data, and binary data streams.</span></span>

> [!NOTE]
> <span data-ttu-id="1d220-171">因為資料服務可能傳回分頁的回應，我們建議您的應用程式使用程式設計模式來處理分頁的資料服務回應。</span><span class="sxs-lookup"><span data-stu-id="1d220-171">Because a data service may return a paged response, we recommend that your application use the programming pattern to handle a paged data service response.</span></span> <span data-ttu-id="1d220-172">如需詳細資訊，請參閱[載入延](loading-deferred-content-wcf-data-services.md)後的內容。</span><span class="sxs-lookup"><span data-stu-id="1d220-172">For more information, see [Loading Deferred Content](loading-deferred-content-wcf-data-services.md).</span></span>

<span data-ttu-id="1d220-173">指定回應中僅傳回特定實體屬性，也可以降低查詢傳回的資料量。</span><span class="sxs-lookup"><span data-stu-id="1d220-173">The amount of data returned by a query can also be reduced by specifying that only certain properties of an entity are returned in the response.</span></span> <span data-ttu-id="1d220-174">如需詳細資訊，請參閱[查詢投影](query-projections-wcf-data-services.md)。</span><span class="sxs-lookup"><span data-stu-id="1d220-174">For more information, see [Query Projections](query-projections-wcf-data-services.md).</span></span>

## <a name="getting-a-count-of-the-total-number-of-entities-in-the-set"></a><span data-ttu-id="1d220-175">取得集合中實體總數的計數</span><span class="sxs-lookup"><span data-stu-id="1d220-175">Getting a Count of the Total Number of Entities in the Set</span></span>

<span data-ttu-id="1d220-176">在部分情況下，這麼做有助於得知實體集中的實體總數，且不僅是查詢傳回的數目。</span><span class="sxs-lookup"><span data-stu-id="1d220-176">In some scenarios, it is helpful to know the total number of entities in an entity set and not merely the number returned by the query.</span></span> <span data-ttu-id="1d220-177">在 <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> 上呼叫 <xref:System.Data.Services.Client.DataServiceQuery%601> 方法，以要求集合中的這項實體總計數包含在查詢結果中。</span><span class="sxs-lookup"><span data-stu-id="1d220-177">Call the <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> method on the <xref:System.Data.Services.Client.DataServiceQuery%601> to request that this total count of entities in the set be included with the query result.</span></span> <span data-ttu-id="1d220-178">在此案例中，傳回之 <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> 的 <xref:System.Data.Services.Client.QueryOperationResponse%601> 屬性會傳回集合中的實體總數。</span><span class="sxs-lookup"><span data-stu-id="1d220-178">In this case, the <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> property of the returned <xref:System.Data.Services.Client.QueryOperationResponse%601> returns the total number of entities in the set.</span></span>

<span data-ttu-id="1d220-179">您也可以分別呼叫 <xref:System.Int32> 或 <xref:System.Int64> 方法，藉此只取得集合中的實體總計數，以做為 <xref:System.Linq.Enumerable.Count%2A> 或做為 <xref:System.Linq.Enumerable.LongCount%2A> 值。</span><span class="sxs-lookup"><span data-stu-id="1d220-179">You can also get only the total count of entities in the set either as an <xref:System.Int32> or as a <xref:System.Int64> value by calling the <xref:System.Linq.Enumerable.Count%2A> or <xref:System.Linq.Enumerable.LongCount%2A> methods respectively.</span></span> <span data-ttu-id="1d220-180">呼叫這些方法時，並未傳回 <xref:System.Data.Services.Client.QueryOperationResponse%601>；只會傳回計數值。</span><span class="sxs-lookup"><span data-stu-id="1d220-180">When these methods are called, a <xref:System.Data.Services.Client.QueryOperationResponse%601> is not returned; only the count value is returned.</span></span> <span data-ttu-id="1d220-181">如需詳細資訊，請參閱[如何：判斷查詢傳回的實體數目](number-of-entities-returned-by-a-query-wcf.md)。</span><span class="sxs-lookup"><span data-stu-id="1d220-181">For more information, see [How to: Determine the Number of Entities Returned by a Query](number-of-entities-returned-by-a-query-wcf.md).</span></span>

## <a name="in-this-section"></a><span data-ttu-id="1d220-182">本節內容</span><span class="sxs-lookup"><span data-stu-id="1d220-182">In This Section</span></span>

- [<span data-ttu-id="1d220-183">查詢投影</span><span class="sxs-lookup"><span data-stu-id="1d220-183">Query Projections</span></span>](query-projections-wcf-data-services.md)

- [<span data-ttu-id="1d220-184">物件具體化</span><span class="sxs-lookup"><span data-stu-id="1d220-184">Object Materialization</span></span>](object-materialization-wcf-data-services.md)

- [<span data-ttu-id="1d220-185">LINQ 考量</span><span class="sxs-lookup"><span data-stu-id="1d220-185">LINQ Considerations</span></span>](linq-considerations-wcf-data-services.md)

- [<span data-ttu-id="1d220-186">如何：執行資料服務查詢</span><span class="sxs-lookup"><span data-stu-id="1d220-186">How to: Execute Data Service Queries</span></span>](how-to-execute-data-service-queries-wcf-data-services.md)

- [<span data-ttu-id="1d220-187">如何：將查詢選項加入至資料服務查詢</span><span class="sxs-lookup"><span data-stu-id="1d220-187">How to: Add Query Options to a Data Service Query</span></span>](how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)

- [<span data-ttu-id="1d220-188">如何：判斷查詢傳回的實體數目</span><span class="sxs-lookup"><span data-stu-id="1d220-188">How to: Determine the Number of Entities Returned by a Query</span></span>](number-of-entities-returned-by-a-query-wcf.md)

- [<span data-ttu-id="1d220-189">HOW TO：指定資料服務要求的用戶端認證</span><span class="sxs-lookup"><span data-stu-id="1d220-189">How to: Specify Client Credentials for a Data Service Request</span></span>](specify-client-creds-for-a-data-service-request-wcf.md)

- [<span data-ttu-id="1d220-190">HOW TO：設定用戶端要求中的標頭</span><span class="sxs-lookup"><span data-stu-id="1d220-190">How to: Set Headers in the Client Request</span></span>](how-to-set-headers-in-the-client-request-wcf-data-services.md)

- [<span data-ttu-id="1d220-191">如何：投影查詢結果</span><span class="sxs-lookup"><span data-stu-id="1d220-191">How to: Project Query Results</span></span>](how-to-project-query-results-wcf-data-services.md)

## <a name="see-also"></a><span data-ttu-id="1d220-192">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1d220-192">See also</span></span>

- [<span data-ttu-id="1d220-193">WCF 資料服務用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="1d220-193">WCF Data Services Client Library</span></span>](wcf-data-services-client-library.md)
