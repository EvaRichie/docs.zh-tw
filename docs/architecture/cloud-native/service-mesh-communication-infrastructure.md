---
title: 服務網格通訊基礎結構
description: 瞭解服務網格技術如何簡化雲端原生微服務通訊
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: 1b11024cd029433c756812850e2665b7836a13d3
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83613679"
---
# <a name="service-mesh-communication-infrastructure"></a><span data-ttu-id="20edb-103">服務網格通訊基礎結構</span><span class="sxs-lookup"><span data-stu-id="20edb-103">Service Mesh communication infrastructure</span></span>

<span data-ttu-id="20edb-104">在本章中，我們探討了微服務通訊的挑戰。</span><span class="sxs-lookup"><span data-stu-id="20edb-104">Throughout this chapter, we've explored the challenges of microservice communication.</span></span> <span data-ttu-id="20edb-105">我們說過，開發小組必須區分後端服務彼此通訊的方式。</span><span class="sxs-lookup"><span data-stu-id="20edb-105">We said that development teams need to be sensitive to how back-end services communicate with each other.</span></span> <span data-ttu-id="20edb-106">在理想的情況下，服務間的通訊越少越好。</span><span class="sxs-lookup"><span data-stu-id="20edb-106">Ideally, the less inter-service communication, the better.</span></span> <span data-ttu-id="20edb-107">不過，不一定可以避免這種情況，因為後端服務通常會依賴另一個來完成作業。</span><span class="sxs-lookup"><span data-stu-id="20edb-107">However, avoidance isn't always possible as back-end services often rely on one another to complete operations.</span></span>

<span data-ttu-id="20edb-108">我們探索了不同的方法來執行同步 HTTP 通訊和非同步訊息。</span><span class="sxs-lookup"><span data-stu-id="20edb-108">We explored different approaches for implementing synchronous HTTP communication and asynchronous messaging.</span></span> <span data-ttu-id="20edb-109">在每個案例中，開發人員都有執行通訊程式碼的負擔。</span><span class="sxs-lookup"><span data-stu-id="20edb-109">In each of the cases, the developer is burdened with implementing communication code.</span></span> <span data-ttu-id="20edb-110">通訊程式碼既複雜又耗費時間。</span><span class="sxs-lookup"><span data-stu-id="20edb-110">Communication code is complex and time intensive.</span></span> <span data-ttu-id="20edb-111">不正確的決策可能會導致嚴重的效能問題。</span><span class="sxs-lookup"><span data-stu-id="20edb-111">Incorrect decisions can lead to significant performance issues.</span></span>

<span data-ttu-id="20edb-112">一種更現代化的方法，可微服務通訊中心，這是一項新的快速發展技術，以*服務網格*為依據。</span><span class="sxs-lookup"><span data-stu-id="20edb-112">A more modern approach to microservice communication centers around a new and rapidly evolving technology entitled *Service Mesh*.</span></span> <span data-ttu-id="20edb-113">[服務網格](https://www.nginx.com/blog/what-is-a-service-mesh/)是可設定的基礎結構層，具有內建功能，可處理服務對服務的通訊、復原，以及許多跨領域考慮。</span><span class="sxs-lookup"><span data-stu-id="20edb-113">A [service mesh](https://www.nginx.com/blog/what-is-a-service-mesh/) is a configurable infrastructure layer with built-in capabilities to handle service-to-service communication, resiliency, and many cross-cutting concerns.</span></span> <span data-ttu-id="20edb-114">它會將這些顧慮的責任移出微服務和服務網格層。</span><span class="sxs-lookup"><span data-stu-id="20edb-114">It moves the responsibility for these concerns out of the microservices and into service mesh layer.</span></span> <span data-ttu-id="20edb-115">通訊會從您的微服務中抽象化出來。</span><span class="sxs-lookup"><span data-stu-id="20edb-115">Communication is abstracted away from your microservices.</span></span>

<span data-ttu-id="20edb-116">服務網格的主要元件是 proxy。</span><span class="sxs-lookup"><span data-stu-id="20edb-116">A key component of a service mesh is a proxy.</span></span> <span data-ttu-id="20edb-117">在雲端原生應用程式中，proxy 的實例通常會與每個微服務共存。</span><span class="sxs-lookup"><span data-stu-id="20edb-117">In a cloud-native application, an instance of a proxy is typically colocated with each microservice.</span></span> <span data-ttu-id="20edb-118">當它們在不同的進程中執行時，這兩個會緊密連結，並共用相同的生命週期。</span><span class="sxs-lookup"><span data-stu-id="20edb-118">While they execute in separate processes, the two are closely linked and share the same lifecycle.</span></span> <span data-ttu-id="20edb-119">此模式稱為[側車模式](https://docs.microsoft.com/azure/architecture/patterns/sidecar)，如圖4-24 所示。</span><span class="sxs-lookup"><span data-stu-id="20edb-119">This pattern, known as the [Sidecar pattern](https://docs.microsoft.com/azure/architecture/patterns/sidecar), and is shown in Figure 4-24.</span></span>

![具有側車的服務網格](./media/service-mesh-with-side-car.png)

<span data-ttu-id="20edb-121">**圖 4-24**：</span><span class="sxs-lookup"><span data-stu-id="20edb-121">**Figure 4-24**.</span></span> <span data-ttu-id="20edb-122">具有側車的服務網格</span><span class="sxs-lookup"><span data-stu-id="20edb-122">Service mesh with a side car</span></span>

<span data-ttu-id="20edb-123">請注意，在上圖中，每個微服務一起執行的 proxy 會攔截訊息。</span><span class="sxs-lookup"><span data-stu-id="20edb-123">Note in the previous figure how messages are intercepted by a proxy that runs alongside each microservice.</span></span> <span data-ttu-id="20edb-124">每個 proxy 都可以使用微服務特定的流量規則來設定。</span><span class="sxs-lookup"><span data-stu-id="20edb-124">Each proxy can be configured with traffic rules specific to the microservice.</span></span> <span data-ttu-id="20edb-125">它瞭解訊息，並可在您的服務和外部世界之間路由傳送。</span><span class="sxs-lookup"><span data-stu-id="20edb-125">It understands messages and can route them across your services and the outside world.</span></span>

<span data-ttu-id="20edb-126">除了管理服務對服務的通訊，服務網格也提供服務探索和負載平衡的支援。</span><span class="sxs-lookup"><span data-stu-id="20edb-126">Along with managing service-to-service communication, the Service Mesh provides support for service discovery and load balancing.</span></span>

<span data-ttu-id="20edb-127">設定好之後，服務網格就能發揮高功能。</span><span class="sxs-lookup"><span data-stu-id="20edb-127">Once configured, a service mesh is highly functional.</span></span> <span data-ttu-id="20edb-128">網格會從服務探索端點抓取對應的實例集區。</span><span class="sxs-lookup"><span data-stu-id="20edb-128">The mesh retrieves a corresponding pool of instances from a service discovery endpoint.</span></span> <span data-ttu-id="20edb-129">它會將要求傳送至特定的服務實例，並記錄結果的延遲和回應類型。</span><span class="sxs-lookup"><span data-stu-id="20edb-129">It sends a request to a specific service instance, recording the latency and response type of the result.</span></span> <span data-ttu-id="20edb-130">它會根據不同的因素（包括最近要求的觀察延遲），選擇最有可能傳回快速回應的實例。</span><span class="sxs-lookup"><span data-stu-id="20edb-130">It chooses the instance most likely to return a fast response based on different factors, including the observed latency for recent requests.</span></span>

<span data-ttu-id="20edb-131">服務網格會管理應用層級的流量、通訊和網路問題。</span><span class="sxs-lookup"><span data-stu-id="20edb-131">A service mesh manages traffic, communication, and networking concerns at the application level.</span></span> <span data-ttu-id="20edb-132">它瞭解訊息和要求。</span><span class="sxs-lookup"><span data-stu-id="20edb-132">It understands messages and requests.</span></span> <span data-ttu-id="20edb-133">服務網格通常會與容器協調器整合。</span><span class="sxs-lookup"><span data-stu-id="20edb-133">A service mesh typically integrates with a container orchestrator.</span></span> <span data-ttu-id="20edb-134">Kubernetes 支援可在其中加入服務網格的可擴充架構。</span><span class="sxs-lookup"><span data-stu-id="20edb-134">Kubernetes supports an extensible architecture in which a service mesh can be added.</span></span>

<span data-ttu-id="20edb-135">在第6章中，我們深入探討服務網格技術，包括對其架構和可用開放原始碼的整合進行討論。</span><span class="sxs-lookup"><span data-stu-id="20edb-135">In chapter 6, we deep-dive into Service Mesh technologies including a discussion on its architecture and available open-source implementations.</span></span>

## <a name="summary"></a><span data-ttu-id="20edb-136">摘要</span><span class="sxs-lookup"><span data-stu-id="20edb-136">Summary</span></span>

<span data-ttu-id="20edb-137">在本章中，我們討論了雲端原生通訊模式。</span><span class="sxs-lookup"><span data-stu-id="20edb-137">In this chapter, we discussed cloud-native communication patterns.</span></span> <span data-ttu-id="20edb-138">我們一開始先檢查前端用戶端如何與後端微服務通訊。</span><span class="sxs-lookup"><span data-stu-id="20edb-138">We started by examining how front-end clients communicate with back-end microservices.</span></span> <span data-ttu-id="20edb-139">在過程中，我們討論了 API 閘道平臺和即時通訊。</span><span class="sxs-lookup"><span data-stu-id="20edb-139">Along the way, we talked about API Gateway platforms and real-time communication.</span></span> <span data-ttu-id="20edb-140">接著，我們探討了微服務如何與其他後端服務通訊。</span><span class="sxs-lookup"><span data-stu-id="20edb-140">We then looked at how microservices communicate with other back-end services.</span></span> <span data-ttu-id="20edb-141">我們探討了同步 HTTP 通訊，以及跨服務的非同步訊息。</span><span class="sxs-lookup"><span data-stu-id="20edb-141">We looked at both synchronous HTTP communication and asynchronous messaging across services.</span></span> <span data-ttu-id="20edb-142">我們涵蓋了 gRPC，這是雲端原生世界中即將推出的技術。</span><span class="sxs-lookup"><span data-stu-id="20edb-142">We covered gRPC, an upcoming technology in the cloud-native world.</span></span> <span data-ttu-id="20edb-143">最後，我們引進了一項新的、快速發展的技術，其服務網格可簡化微服務通訊。</span><span class="sxs-lookup"><span data-stu-id="20edb-143">Finally, we introduced a new and rapidly evolving technology entitled Service Mesh that can streamline microservice communication.</span></span>

<span data-ttu-id="20edb-144">特別著重于受控 Azure 服務，可協助您在雲端原生系統中執行通訊：</span><span class="sxs-lookup"><span data-stu-id="20edb-144">Special emphasis was on managed Azure services that can help implement communication in cloud-native systems:</span></span>

- [<span data-ttu-id="20edb-145">Azure 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="20edb-145">Azure Application Gateway</span></span>](https://docs.microsoft.com/azure/application-gateway/overview)
- [<span data-ttu-id="20edb-146">Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="20edb-146">Azure API Management</span></span>](https://azure.microsoft.com/services/api-management/)
- [<span data-ttu-id="20edb-147">Azure SignalR 服務</span><span class="sxs-lookup"><span data-stu-id="20edb-147">Azure SignalR Service</span></span>](https://azure.microsoft.com/services/signalr-service/)
- [<span data-ttu-id="20edb-148">Azure 儲存體佇列</span><span class="sxs-lookup"><span data-stu-id="20edb-148">Azure Storage Queues</span></span>](https://docs.microsoft.com/azure/storage/queues/storage-queues-introduction)
- [<span data-ttu-id="20edb-149">Azure 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="20edb-149">Azure Service Bus</span></span>](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)
- [<span data-ttu-id="20edb-150">事件格線</span><span class="sxs-lookup"><span data-stu-id="20edb-150">Azure Event Grid</span></span>](https://docs.microsoft.com/azure/event-grid/overview)
- [<span data-ttu-id="20edb-151">Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="20edb-151">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

<span data-ttu-id="20edb-152">接下來，移至雲端原生系統中的分散式資料，以及它所呈現的優點和挑戰。</span><span class="sxs-lookup"><span data-stu-id="20edb-152">We next move to distributed data in cloud-native systems and the benefits and challenges that it presents.</span></span>

### <a name="references"></a><span data-ttu-id="20edb-153">參考</span><span class="sxs-lookup"><span data-stu-id="20edb-153">References</span></span>

- [<span data-ttu-id="20edb-154">.NET 微服務：容器化 .NET 應用程式的架構</span><span class="sxs-lookup"><span data-stu-id="20edb-154">.NET Microservices: Architecture for Containerized .NET applications</span></span>](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook)

- [<span data-ttu-id="20edb-155">設計微服務的服務間通訊</span><span class="sxs-lookup"><span data-stu-id="20edb-155">Designing Interservice Communication for Microservices</span></span>](https://docs.microsoft.com/azure/architecture/microservices/design/interservice-communication)

- [<span data-ttu-id="20edb-156">Azure SignalR Service，這是一種完全受控的服務，可新增即時功能</span><span class="sxs-lookup"><span data-stu-id="20edb-156">Azure SignalR Service, a fully managed service to add real-time functionality</span></span>](https://azure.microsoft.com/blog/azure-signalr-service-a-fully-managed-service-to-add-real-time-functionality/)

- [<span data-ttu-id="20edb-157">Azure API 閘道輸入控制器</span><span class="sxs-lookup"><span data-stu-id="20edb-157">Azure API Gateway Ingress Controller</span></span>](https://azure.github.io/application-gateway-kubernetes-ingress/)

- [<span data-ttu-id="20edb-158">關於 Azure Kubernetes Service 中的輸入（AKS）</span><span class="sxs-lookup"><span data-stu-id="20edb-158">About Ingress in Azure Kubernetes Service (AKS)</span></span>](https://vincentlauzon.com/2018/10/10/about-ingress-in-azure-kubernetes-service-aks/)

- [<span data-ttu-id="20edb-159">gRPC 檔</span><span class="sxs-lookup"><span data-stu-id="20edb-159">gRPC Documentation</span></span>](https://grpc.io/docs/guides/)

- [<span data-ttu-id="20edb-160">適用於 WCF 開發人員的 gRPC</span><span class="sxs-lookup"><span data-stu-id="20edb-160">gRPC for WCF Developers</span></span>](https://docs.microsoft.com/dotnet/architecture/grpc-for-wcf-developers/)

- [<span data-ttu-id="20edb-161">比較 gRPC 服務與 HTTP Api</span><span class="sxs-lookup"><span data-stu-id="20edb-161">Comparing gRPC Services with HTTP APIs</span></span>](https://docs.microsoft.com/aspnet/core/grpc/comparison?view=aspnetcore-3.0)

- [<span data-ttu-id="20edb-162">使用 .NET 建立 gRPC 服務影片</span><span class="sxs-lookup"><span data-stu-id="20edb-162">Building gRPC Services with .NET video</span></span>](https://channel9.msdn.com/Shows/The-Cloud-Native-Show/Building-Microservices-with-gRPC-and-NET)

>[!div class="step-by-step"]
><span data-ttu-id="20edb-163">[上一個](grpc.md) 
>[下一步](distributed-data.md)</span><span class="sxs-lookup"><span data-stu-id="20edb-163">[Previous](grpc.md)
[Next](distributed-data.md)</span></span>
