---
title: 微服務可定址性和服務登錄
description: 了解容器映像登錄在微服務架構中的角色。
ms.date: 01/13/2021
ms.openlocfilehash: 363a307d44d30125563863bbe3ebeb5f5b9ad2bc
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188409"
---
# <a name="microservices-addressability-and-the-service-registry"></a><span data-ttu-id="99456-103">微服務可定址性和服務登錄</span><span class="sxs-lookup"><span data-stu-id="99456-103">Microservices addressability and the service registry</span></span>

<span data-ttu-id="99456-104">每個微服務都有用來解析其位置的唯一名稱 (URL)。</span><span class="sxs-lookup"><span data-stu-id="99456-104">Each microservice has a unique name (URL) that's used to resolve its location.</span></span> <span data-ttu-id="99456-105">只要您的微服務正在執行，就必須是可定址的。</span><span class="sxs-lookup"><span data-stu-id="99456-105">Your microservice needs to be addressable wherever it's running.</span></span> <span data-ttu-id="99456-106">如果您必須想一下正在執行特定微服務的電腦為何，問題可能會急遽惡化。</span><span class="sxs-lookup"><span data-stu-id="99456-106">If you have to think about which computer is running a particular microservice, things can go bad quickly.</span></span> <span data-ttu-id="99456-107">就像是 DNS 將 URL 解析為特定電腦，您的微服務也必須具有唯一名稱，才能探索其目前位置。</span><span class="sxs-lookup"><span data-stu-id="99456-107">In the same way that DNS resolves a URL to a particular computer, your microservice needs to have a unique name so that its current location is discoverable.</span></span> <span data-ttu-id="99456-108">微服務需要可定址的名稱，以獨立於其執行所在的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="99456-108">Microservices need addressable names that make them independent from the infrastructure that they're running on.</span></span> <span data-ttu-id="99456-109">這種方法表示服務的部署方式與探索方式之間會有互動，因為需要有 [服務](https://microservices.io/patterns/service-registry.html)登錄。</span><span class="sxs-lookup"><span data-stu-id="99456-109">This approach implies that there's an interaction between how your service is deployed and how it's discovered, because there needs to be a [service registry](https://microservices.io/patterns/service-registry.html).</span></span> <span data-ttu-id="99456-110">同樣地，當電腦失敗時，登錄服務必須能夠指出服務現在正在執行的位置。</span><span class="sxs-lookup"><span data-stu-id="99456-110">In the same vein, when a computer fails, the registry service must be able to indicate where the service is now running.</span></span>

<span data-ttu-id="99456-111">[服務登錄模式](https://microservices.io/patterns/service-registry.html)是服務探索的主要部分。</span><span class="sxs-lookup"><span data-stu-id="99456-111">The [service registry pattern](https://microservices.io/patterns/service-registry.html) is a key part of service discovery.</span></span> <span data-ttu-id="99456-112">登錄是包含服務執行個體之網路位置的資料庫。</span><span class="sxs-lookup"><span data-stu-id="99456-112">The registry is a database containing the network locations of service instances.</span></span> <span data-ttu-id="99456-113">服務登錄必須高度可用且處於最新狀態。</span><span class="sxs-lookup"><span data-stu-id="99456-113">A service registry needs to be highly available and up-to-date.</span></span> <span data-ttu-id="99456-114">用戶端可以快取從服務登錄取得的網路位置。</span><span class="sxs-lookup"><span data-stu-id="99456-114">Clients could cache network locations obtained from the service registry.</span></span> <span data-ttu-id="99456-115">不過，該資訊最終會過期，此時用戶端將無法再探索服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="99456-115">However, that information eventually goes out of date and clients can no longer discover service instances.</span></span> <span data-ttu-id="99456-116">因此，服務登錄是由使用複寫通訊協定來維持一致性的伺服器叢集所組成。</span><span class="sxs-lookup"><span data-stu-id="99456-116">So, a service registry consists of a cluster of servers that use a replication protocol to maintain consistency.</span></span>

<span data-ttu-id="99456-117">在某些微服務部署環境 (稱為「叢集」（) 稍後的章節中所述），服務探索是內建的。</span><span class="sxs-lookup"><span data-stu-id="99456-117">In some microservice deployment environments (called clusters, to be covered in a later section), service discovery is built in.</span></span> <span data-ttu-id="99456-118">例如，Azure Container Service with Kubernetes (AKS) 環境可以處理服務執行個體註冊和取消註冊。</span><span class="sxs-lookup"><span data-stu-id="99456-118">For example, an Azure Container Service with Kubernetes (AKS) environment can handle service instance registration and deregistration.</span></span> <span data-ttu-id="99456-119">它也會在扮演伺服器端探索路由器角色的每部叢集主機上執行 Proxy。</span><span class="sxs-lookup"><span data-stu-id="99456-119">It also runs a proxy on each cluster host that plays the role of server-side discovery router.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99456-120">其他資源</span><span class="sxs-lookup"><span data-stu-id="99456-120">Additional resources</span></span>

- <span data-ttu-id="99456-121">**Chris Richardson。模式：服務登錄** </span><span class="sxs-lookup"><span data-stu-id="99456-121">**Chris Richardson. Pattern: Service registry** </span></span>\
  <https://microservices.io/patterns/service-registry.html>

- <span data-ttu-id="99456-122">**Auth0.服務登錄** </span><span class="sxs-lookup"><span data-stu-id="99456-122">**Auth0. The Service Registry** </span></span>\
  <https://auth0.com/blog/an-introduction-to-microservices-part-3-the-service-registry/>

- <span data-ttu-id="99456-123">**Gabriel Schenker。服務探索** </span><span class="sxs-lookup"><span data-stu-id="99456-123">**Gabriel Schenker. Service discovery** </span></span>\
  <https://lostechies.com/gabrielschenker/2016/01/27/service-discovery/>

>[!div class="step-by-step"]
><span data-ttu-id="99456-124">[上一個](maintain-microservice-apis.md) 
>[下一步](microservice-based-composite-ui-shape-layout.md)</span><span class="sxs-lookup"><span data-stu-id="99456-124">[Previous](maintain-microservice-apis.md)
[Next](microservice-based-composite-ui-shape-layout.md)</span></span>
