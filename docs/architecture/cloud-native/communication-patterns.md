---
title: 雲端原生通訊模式
description: 瞭解雲端原生應用程式中的重要服務通訊考慮
author: robvet
ms.date: 08/31/2019
ms.openlocfilehash: b3edc0817fb76ad99a1344b17d600eb747187f86
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895622"
---
# <a name="cloud-native-communication-patterns"></a><span data-ttu-id="b0885-103">雲端原生通訊模式</span><span class="sxs-lookup"><span data-stu-id="b0885-103">Cloud-native communication patterns</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="b0885-104">在建立雲端原生系統時，通訊會成為重要的設計決策。</span><span class="sxs-lookup"><span data-stu-id="b0885-104">When constructing a cloud-native system, communication becomes a significant design decision.</span></span> <span data-ttu-id="b0885-105">前端用戶端應用程式如何與後端微服務通訊？</span><span class="sxs-lookup"><span data-stu-id="b0885-105">How does a front-end client application communicate with a back-end microservice?</span></span> <span data-ttu-id="b0885-106">後端微服務如何彼此通訊？</span><span class="sxs-lookup"><span data-stu-id="b0885-106">How do back-end microservices communicate with each other?</span></span> <span data-ttu-id="b0885-107">在雲端原生應用程式中執行通訊時，需要考慮哪些原則、模式和最佳作法？</span><span class="sxs-lookup"><span data-stu-id="b0885-107">What are the principles, patterns, and best practices to consider when implementing communication in cloud-native applications?</span></span>

## <a name="communication-considerations"></a><span data-ttu-id="b0885-108">通訊考慮</span><span class="sxs-lookup"><span data-stu-id="b0885-108">Communication considerations</span></span>

<span data-ttu-id="b0885-109">在整合型應用程式中，通訊非常簡單。</span><span class="sxs-lookup"><span data-stu-id="b0885-109">In a monolithic application, communication is straightforward.</span></span> <span data-ttu-id="b0885-110">程式碼模組會在伺服器上的同一個可執行空間（進程）中一起執行。</span><span class="sxs-lookup"><span data-stu-id="b0885-110">The code modules execute together in the same executable space (process) on a server.</span></span> <span data-ttu-id="b0885-111">當所有專案都在共用記憶體中一起執行時，這個方法可能會有效能上的優勢，但會產生緊密結合的程式碼，而變得很容易維護、演進和調整。</span><span class="sxs-lookup"><span data-stu-id="b0885-111">This approach can have performance advantages as everything runs together in shared memory, but results in tightly coupled code that becomes difficult to maintain, evolve, and scale.</span></span>

<span data-ttu-id="b0885-112">雲端原生系統會實微服務架構，其中包含許多小型、獨立的微服務。</span><span class="sxs-lookup"><span data-stu-id="b0885-112">Cloud-native systems implement a microservice-based architecture with many small, independent microservices.</span></span> <span data-ttu-id="b0885-113">每個微服務會在個別的進程中執行，且通常會在部署至叢集*的容器內執行。*</span><span class="sxs-lookup"><span data-stu-id="b0885-113">Each microservice executes in a separate process and typically runs inside a container that is deployed to a *cluster*.</span></span>

<span data-ttu-id="b0885-114">叢集會將虛擬機器的集區群組在一起，以形成高可用性的環境。</span><span class="sxs-lookup"><span data-stu-id="b0885-114">A cluster groups a pool of virtual machines together to form a highly available environment.</span></span> <span data-ttu-id="b0885-115">它們是使用協調流程工具來管理，負責部署和管理容器化微服務。</span><span class="sxs-lookup"><span data-stu-id="b0885-115">They're managed with an orchestration tool, which is responsible for deploying and managing the containerized microservices.</span></span> <span data-ttu-id="b0885-116">圖4-1 顯示使用完全受控[Azure Kubernetes 服務](https://docs.microsoft.com/azure/aks/intro-kubernetes)部署到 azure 雲端的[Kubernetes](https://kubernetes.io)叢集。</span><span class="sxs-lookup"><span data-stu-id="b0885-116">Figure 4-1 shows a [Kubernetes](https://kubernetes.io) cluster deployed into the Azure cloud with the fully managed [Azure Kubernetes Services](https://docs.microsoft.com/azure/aks/intro-kubernetes).</span></span>

![Azure 中的 Kubernetes 叢集](./media/kubernetes-cluster-in-azure.png)

<span data-ttu-id="b0885-118">**圖 4-1**。</span><span class="sxs-lookup"><span data-stu-id="b0885-118">**Figure 4-1**.</span></span> <span data-ttu-id="b0885-119">Azure 中的 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="b0885-119">A Kubernetes cluster in Azure</span></span>

<span data-ttu-id="b0885-120">在整個叢集中，微服務透過 Api 和訊息技術彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="b0885-120">Across the cluster, microservices communicate with each other through APIs and messaging technologies.</span></span>

<span data-ttu-id="b0885-121">雖然它們提供許多優點，但微服務沒有免費的午餐。</span><span class="sxs-lookup"><span data-stu-id="b0885-121">While they provide many benefits, microservices are no free lunch.</span></span> <span data-ttu-id="b0885-122">元件之間的本機同進程方法呼叫現在已由網路呼叫取代。</span><span class="sxs-lookup"><span data-stu-id="b0885-122">Local in-process method calls between components are now replaced with network calls.</span></span> <span data-ttu-id="b0885-123">每個微服務都必須透過網路通訊協定進行通訊，這會增加系統的複雜度：</span><span class="sxs-lookup"><span data-stu-id="b0885-123">Each microservice must communicate over a network protocol, which adds complexity to your system:</span></span>

- <span data-ttu-id="b0885-124">網路擁塞、延遲和暫時性錯誤是一大考慮。</span><span class="sxs-lookup"><span data-stu-id="b0885-124">Network congestion, latency, and transient faults are a constant concern.</span></span>

- <span data-ttu-id="b0885-125">復原（也就是重試失敗的要求）是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="b0885-125">Resiliency (that is, retrying failed requests) is essential.</span></span>

- <span data-ttu-id="b0885-126">有些呼叫必須具有[等冪](https://www.restapitutorial.com/lessons/idempotency.html)性，才能保持一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="b0885-126">Some calls must be [idempotent](https://www.restapitutorial.com/lessons/idempotency.html) as to keep consistent state.</span></span>

- <span data-ttu-id="b0885-127">每個微服務都必須驗證和授權呼叫。</span><span class="sxs-lookup"><span data-stu-id="b0885-127">Each microservice must authenticate and authorize calls.</span></span>

- <span data-ttu-id="b0885-128">每個訊息都必須經過序列化，然後再還原序列化-這可能很耗費資源。</span><span class="sxs-lookup"><span data-stu-id="b0885-128">Each message must be serialized and then deserialized - which can be expensive.</span></span>

- <span data-ttu-id="b0885-129">訊息加密/解密變得很重要。</span><span class="sxs-lookup"><span data-stu-id="b0885-129">Message encryption/decryption becomes important.</span></span>

<span data-ttu-id="b0885-130">[.Net 微服務：容器化 .Net 應用程式的架構](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook)（可從 Microsoft 免費取得）提供微服務應用程式通訊模式的深入涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="b0885-130">The book [.NET Microservices: Architecture for Containerized .NET Applications](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook), available for free from Microsoft, provides an in-depth coverage of communication patterns for microservice applications.</span></span> <span data-ttu-id="b0885-131">在本章中，我們會提供這些模式的高階概述，以及 Azure 雲端中可用的實作為選項。</span><span class="sxs-lookup"><span data-stu-id="b0885-131">In this chapter, we provide a high-level overview of these patterns along with implementation options available in the Azure cloud.</span></span>

<span data-ttu-id="b0885-132">在本章中，我們會先解決前端應用程式與後端微服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="b0885-132">In this chapter, we'll first address communication between front-end applications and back-end microservices.</span></span> <span data-ttu-id="b0885-133">然後，我們將探討後端微服務彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="b0885-133">We'll then look at back-end microservices communicate with each other.</span></span> <span data-ttu-id="b0885-134">我們將探討 up 和 gRPC 通訊技術。</span><span class="sxs-lookup"><span data-stu-id="b0885-134">We'll explore the up and gRPC communication technology.</span></span> <span data-ttu-id="b0885-135">最後，我們將使用服務網格技術來探討新的創新通訊模式。</span><span class="sxs-lookup"><span data-stu-id="b0885-135">Finally, we'll look new innovative communication patterns using service mesh technology.</span></span> <span data-ttu-id="b0885-136">我們也將瞭解 Azure 雲端如何提供不同種類的支援*服務*，以支援雲端原生通訊。</span><span class="sxs-lookup"><span data-stu-id="b0885-136">We'll also see how the Azure cloud provides different kinds of *backing services* to support cloud-native communication.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="b0885-137">[上一頁](other-deployment-options.md)
>[下一頁](front-end-communication.md)</span><span class="sxs-lookup"><span data-stu-id="b0885-137">[Previous](other-deployment-options.md)
[Next](front-end-communication.md)</span></span>
