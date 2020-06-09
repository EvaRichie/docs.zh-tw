---
title: 探索尋找與尋找準則
ms.date: 03/30/2017
ms.assetid: 99016fa4-1778-495b-b4cc-0e22fbec42c6
ms.openlocfilehash: 1d6a0e3fcca45c3fe57aab84b0f2b6b86fabb404
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599174"
---
# <a name="discovery-find-and-findcriteria"></a><span data-ttu-id="1c531-102">探索尋找與尋找準則</span><span class="sxs-lookup"><span data-stu-id="1c531-102">Discovery Find and FindCriteria</span></span>

<span data-ttu-id="1c531-103">探索尋找作業是由用戶端初始化，用於探索一項或多項服務，並且為探索中的其中一個主要動作。</span><span class="sxs-lookup"><span data-stu-id="1c531-103">A discovery find operation is initiated by a client to discover one or more services and is one of the main actions in discovery.</span></span> <span data-ttu-id="1c531-104">執行尋找會透過網路傳送 WS-Discovery Probe 訊息。</span><span class="sxs-lookup"><span data-stu-id="1c531-104">Performing a find sends a WS-Discovery Probe message over the network.</span></span> <span data-ttu-id="1c531-105">符合指定準則的服務會以 WS-Discovery ProbeMatch 訊息回覆。</span><span class="sxs-lookup"><span data-stu-id="1c531-105">Services that match the criteria specified reply with WS-Discovery ProbeMatch messages.</span></span> <span data-ttu-id="1c531-106">如需探索訊息的詳細資訊，請參閱[WS-discovery 規格](http://schemas.xmlsoap.org/ws/2004/10/discovery/ws-discovery.pdf)。</span><span class="sxs-lookup"><span data-stu-id="1c531-106">For more information about discovery messages, see the [WS-Discovery specification](http://schemas.xmlsoap.org/ws/2004/10/discovery/ws-discovery.pdf).</span></span>

## <a name="discoveryclient"></a><span data-ttu-id="1c531-107">DiscoveryClient</span><span class="sxs-lookup"><span data-stu-id="1c531-107">DiscoveryClient</span></span>

<span data-ttu-id="1c531-108"><xref:System.ServiceModel.Discovery.DiscoveryClient> 類別會提供執行尋找作業的機制，並且讓執行探索用戶端的作業更為簡單。</span><span class="sxs-lookup"><span data-stu-id="1c531-108">The <xref:System.ServiceModel.Discovery.DiscoveryClient> class provides the mechanism to perform find operations and makes performing discovery client operations easy.</span></span> <span data-ttu-id="1c531-109">它包含 <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 方法，用於執行 (封鎖) 同步尋找，以及 <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> 方法，用於初始化非封鎖非同步尋找。</span><span class="sxs-lookup"><span data-stu-id="1c531-109">It contains a <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> method, which performs a (blocking) synchronous find, and a <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> method, which initiates a non-blocking asynchronous find.</span></span> <span data-ttu-id="1c531-110">這兩種方法都採用 <xref:System.ServiceModel.Discovery.FindCriteria> 參數，並且透過 <xref:System.ServiceModel.Discovery.FindResponse> 物件將結果提供給使用者。</span><span class="sxs-lookup"><span data-stu-id="1c531-110">Both methods take a <xref:System.ServiceModel.Discovery.FindCriteria> parameter, and provide results to the user through a <xref:System.ServiceModel.Discovery.FindResponse> object.</span></span>

## <a name="findcriteria"></a><span data-ttu-id="1c531-111">FindCriteria</span><span class="sxs-lookup"><span data-stu-id="1c531-111">FindCriteria</span></span>

<span data-ttu-id="1c531-112"><xref:System.ServiceModel.Discovery.FindCriteria> 擁有數個屬性，可分組為搜尋準則，用於指定您要尋找的服務，以及尋找終止準則 (搜尋應持續的時間長度)。</span><span class="sxs-lookup"><span data-stu-id="1c531-112"><xref:System.ServiceModel.Discovery.FindCriteria> has several properties, which can be grouped into search criteria, which specify what services you are looking for, and find termination criteria (how long the search should last).</span></span> <span data-ttu-id="1c531-113"><xref:System.ServiceModel.Discovery.FindCriteria> 可以包含多個搜尋準則。</span><span class="sxs-lookup"><span data-stu-id="1c531-113">A <xref:System.ServiceModel.Discovery.FindCriteria> can contain multiple search criteria.</span></span> <span data-ttu-id="1c531-114">根據預設，服務必須符合所有元件，否則不會將本身視為相符的服務。</span><span class="sxs-lookup"><span data-stu-id="1c531-114">By default, the service has to match all of the components otherwise it does not consider itself a matching service.</span></span> <span data-ttu-id="1c531-115">如果您要尋找僅符合部分準則的服務，可以在服務上實作自訂尋找邏輯，或是使用多個查詢。</span><span class="sxs-lookup"><span data-stu-id="1c531-115">If you want to find services that only match some of the criteria, you can implement custom find logic on the service or you can use multiple queries.</span></span>

<span data-ttu-id="1c531-116">搜尋準則包括：</span><span class="sxs-lookup"><span data-stu-id="1c531-116">Search criteria include:</span></span>

- <span data-ttu-id="1c531-117"><xref:System.ServiceModel.Discovery.Configuration.ContractTypeNameElement>：選擇項。</span><span class="sxs-lookup"><span data-stu-id="1c531-117"><xref:System.ServiceModel.Discovery.Configuration.ContractTypeNameElement> - Optional.</span></span> <span data-ttu-id="1c531-118">要搜尋的服務合約名稱，以及搜尋服務時常用的準則。</span><span class="sxs-lookup"><span data-stu-id="1c531-118">The contract name of the service being searched for and the criteria typically used when searching for a service.</span></span> <span data-ttu-id="1c531-119">如果指定多個合約名稱，則只會回覆符合「所有」合約的服務端點。</span><span class="sxs-lookup"><span data-stu-id="1c531-119">If more than one contract name is specified, only service endpoints matching ALL contracts reply.</span></span> <span data-ttu-id="1c531-120">請注意，在 WCF 中，端點只能支援一個合約。</span><span class="sxs-lookup"><span data-stu-id="1c531-120">Note that in WCF an endpoint can only support one contract.</span></span>

- <span data-ttu-id="1c531-121"><xref:System.ServiceModel.Discovery.Configuration.ScopeElement>：選擇項。</span><span class="sxs-lookup"><span data-stu-id="1c531-121"><xref:System.ServiceModel.Discovery.Configuration.ScopeElement> - Optional.</span></span> <span data-ttu-id="1c531-122">範圍是絕對 URI，可用來分類個別服務端點。</span><span class="sxs-lookup"><span data-stu-id="1c531-122">Scopes are absolute URIs that are used to categorize individual service endpoints.</span></span> <span data-ttu-id="1c531-123">在多個端點公開相同合約，而您希望能夠搜尋端點子集的情況下，可能會想要使用這種方式。</span><span class="sxs-lookup"><span data-stu-id="1c531-123">You may want to use this in scenarios where multiple endpoints expose the same contract and you want a way to search for a subset of the endpoints.</span></span> <span data-ttu-id="1c531-124">如果指定多個範圍，則只會回覆符合「所有」範圍的服務端點。</span><span class="sxs-lookup"><span data-stu-id="1c531-124">If more than one scope is specified, only service endpoints matching ALL scopes reply.</span></span>

- <span data-ttu-id="1c531-125"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchBy%2A>：指定比對 Probe 訊息中的範圍與端點的範圍時，要使用的比對演算法。</span><span class="sxs-lookup"><span data-stu-id="1c531-125"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchBy%2A> - Specifies the matching algorithm to use while matching the scopes in the Probe message with that of the endpoint.</span></span> <span data-ttu-id="1c531-126">支援的範圍比對規則有五種：</span><span class="sxs-lookup"><span data-stu-id="1c531-126">There are five supported scope-matching rules:</span></span>

  - <span data-ttu-id="1c531-127"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByExact?displayProperty=nameWithType> 會執行基本的區分大小寫字串比較。</span><span class="sxs-lookup"><span data-stu-id="1c531-127"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByExact?displayProperty=nameWithType> does a basic case-sensitive string comparison.</span></span>

  - <span data-ttu-id="1c531-128"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByPrefix?displayProperty=nameWithType>依據以 "/" 分隔的區段比對。</span><span class="sxs-lookup"><span data-stu-id="1c531-128"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByPrefix?displayProperty=nameWithType> matches by segments separated by "/".</span></span> <span data-ttu-id="1c531-129">搜尋 `http://contoso/building1` 符合具有範圍的服務 `http://contoso/building/floor1` 。</span><span class="sxs-lookup"><span data-stu-id="1c531-129">A search for `http://contoso/building1` matches a service with scope `http://contoso/building/floor1`.</span></span> <span data-ttu-id="1c531-130">請注意，它不相符， `http://contoso/building100` 因為最後兩個區段不相符。</span><span class="sxs-lookup"><span data-stu-id="1c531-130">Note that it does not match `http://contoso/building100` because the last two segments do not match.</span></span>

  - <span data-ttu-id="1c531-131"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByLdap?displayProperty=nameWithType> 會使用 LDAP URL 依照區段比對範圍。</span><span class="sxs-lookup"><span data-stu-id="1c531-131"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByLdap?displayProperty=nameWithType> matches scopes by segments using an LDAP URL.</span></span>

  - <span data-ttu-id="1c531-132"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByUuid?displayProperty=nameWithType> 會使用 UUID 字串精確比對範圍。</span><span class="sxs-lookup"><span data-stu-id="1c531-132"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByUuid?displayProperty=nameWithType> matches scopes exactly using a UUID string.</span></span>

  - <span data-ttu-id="1c531-133"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByNone?displayProperty=nameWithType> 僅比對未定範圍的服務。</span><span class="sxs-lookup"><span data-stu-id="1c531-133"><xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByNone?displayProperty=nameWithType> matches only those services that do not specify a scope.</span></span>

  <span data-ttu-id="1c531-134">如果未指定範圍比對規則，則會使用 <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByPrefix>。</span><span class="sxs-lookup"><span data-stu-id="1c531-134">If a scope-matching rule is not specified, <xref:System.ServiceModel.Discovery.FindCriteria.ScopeMatchByPrefix> is used.</span></span>

<span data-ttu-id="1c531-135">終止準則包括：</span><span class="sxs-lookup"><span data-stu-id="1c531-135">Termination criteria include:</span></span>

1. <span data-ttu-id="1c531-136"><xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> - 在網路上等待服務回覆的時間上限。</span><span class="sxs-lookup"><span data-stu-id="1c531-136"><xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> - The maximum time to wait for replies from services on the network.</span></span> <span data-ttu-id="1c531-137">預設持續時間為 20 秒。</span><span class="sxs-lookup"><span data-stu-id="1c531-137">The default duration is 20 seconds.</span></span>

2. <span data-ttu-id="1c531-138"><xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> - 要等待的回覆數目上限。</span><span class="sxs-lookup"><span data-stu-id="1c531-138"><xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> - The maximum number of replies to wait for.</span></span> <span data-ttu-id="1c531-139">如果在 <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 經過之前，先收到 <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> 回覆，尋找作業就會結束。</span><span class="sxs-lookup"><span data-stu-id="1c531-139">If <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> replies are received before <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> has elapsed, the find operation ends.</span></span>

## <a name="findresponse"></a><span data-ttu-id="1c531-140">FindResponse</span><span class="sxs-lookup"><span data-stu-id="1c531-140">FindResponse</span></span>

<span data-ttu-id="1c531-141"><xref:System.ServiceModel.Discovery.FindResponse> 擁有 <xref:System.ServiceModel.Discovery.FindResponse.Endpoints%2A> 集合屬性，其中包含網路上相符的服務傳送的任何回覆。</span><span class="sxs-lookup"><span data-stu-id="1c531-141"><xref:System.ServiceModel.Discovery.FindResponse> has an <xref:System.ServiceModel.Discovery.FindResponse.Endpoints%2A> collection property that contains any replies sent by matching services on the network.</span></span> <span data-ttu-id="1c531-142">如果沒有任何服務回覆，則集合會是空的。</span><span class="sxs-lookup"><span data-stu-id="1c531-142">If no services replied, the collection is empty.</span></span> <span data-ttu-id="1c531-143">如果有一項或多項服務回覆，則每個回覆都會儲存在 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> 物件中，其中包含與服務相關的位址、合約和一些額外資訊。</span><span class="sxs-lookup"><span data-stu-id="1c531-143">If one or more services replied, each reply is stored in an <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> object, which contains the address, contract, and some additional information about the service.</span></span>

<span data-ttu-id="1c531-144">下列範例示範如何在程式碼中執行尋找作業。</span><span class="sxs-lookup"><span data-stu-id="1c531-144">The following example shows how to perform a find operation in code.</span></span>

```csharp
// Create DiscoveryClient
DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());

// Create FindCriteria
FindCriteria findCriteria = new FindCriteria(typeof(IPrinterService));
findCriteria.Scopes.Add(new Uri("http://www.contoso.com/building1/floor1"));
findCriteria.Duration = TimeSpan.FromSeconds(10);

// Find ICalculatorService endpoints
FindResponse findResponse = discoveryClient.Find(findCriteria);

Console.WriteLine("Found {0} ICalculatorService endpoint(s).", findResponse.Endpoints.Count)
```

## <a name="see-also"></a><span data-ttu-id="1c531-145">請參閱</span><span class="sxs-lookup"><span data-stu-id="1c531-145">See also</span></span>

- [<span data-ttu-id="1c531-146">WCF 探索概觀</span><span class="sxs-lookup"><span data-stu-id="1c531-146">WCF Discovery Overview</span></span>](wcf-discovery-overview.md)
- [<span data-ttu-id="1c531-147">使用探索用戶端通道</span><span class="sxs-lookup"><span data-stu-id="1c531-147">Using the Discovery Client Channel</span></span>](using-the-discovery-client-channel.md)
- [<span data-ttu-id="1c531-148">探索範圍</span><span class="sxs-lookup"><span data-stu-id="1c531-148">Discovery with Scopes</span></span>](../samples/discovery-with-scopes-sample.md)
- [<span data-ttu-id="1c531-149">Basic</span><span class="sxs-lookup"><span data-stu-id="1c531-149">Basic</span></span>](../samples/basic-sample.md)
