---
title: 雲端原生通訊模式
description: 瞭解雲端原生應用程式中的重要服務通訊考慮
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: 5ce789924e828865f7bdf717b081b9112203293a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91160914"
---
# <a name="cloud-native-communication-patterns"></a><span data-ttu-id="ea38a-103">雲端原生通訊模式</span><span class="sxs-lookup"><span data-stu-id="ea38a-103">Cloud-native communication patterns</span></span>

<span data-ttu-id="ea38a-104">當您建立雲端原生系統時，通訊會成為很重要的設計決策。</span><span class="sxs-lookup"><span data-stu-id="ea38a-104">When constructing a cloud-native system, communication becomes a significant design decision.</span></span> <span data-ttu-id="ea38a-105">前端用戶端應用程式如何與後端微服務通訊？</span><span class="sxs-lookup"><span data-stu-id="ea38a-105">How does a front-end client application communicate with a back-end microservice?</span></span> <span data-ttu-id="ea38a-106">後端微服務如何彼此通訊？</span><span class="sxs-lookup"><span data-stu-id="ea38a-106">How do back-end microservices communicate with each other?</span></span> <span data-ttu-id="ea38a-107">在雲端原生應用程式中進行通訊時，要考慮的原則、模式和最佳作法為何？</span><span class="sxs-lookup"><span data-stu-id="ea38a-107">What are the principles, patterns, and best practices to consider when implementing communication in cloud-native applications?</span></span>

## <a name="communication-considerations"></a><span data-ttu-id="ea38a-108">通訊考慮</span><span class="sxs-lookup"><span data-stu-id="ea38a-108">Communication considerations</span></span>

<span data-ttu-id="ea38a-109">在整合型應用程式中，通訊很簡單。</span><span class="sxs-lookup"><span data-stu-id="ea38a-109">In a monolithic application, communication is straightforward.</span></span> <span data-ttu-id="ea38a-110">程式碼模組會在相同的可執行空間中一起執行 (處理伺服器上的) 。</span><span class="sxs-lookup"><span data-stu-id="ea38a-110">The code modules execute together in the same executable space (process) on a server.</span></span> <span data-ttu-id="ea38a-111">當所有專案都在共用記憶體中一起執行時，此方法會有效能優勢，但會產生緊密結合的程式碼，使其變得難以維護、演進和調整。</span><span class="sxs-lookup"><span data-stu-id="ea38a-111">This approach can have performance advantages as everything runs together in shared memory, but results in tightly coupled code that becomes difficult to maintain, evolve, and scale.</span></span>

<span data-ttu-id="ea38a-112">雲端原生系統採用以微服務為基礎的架構，其具有許多小型且獨立的微服務。</span><span class="sxs-lookup"><span data-stu-id="ea38a-112">Cloud-native systems implement a microservice-based architecture with many small, independent microservices.</span></span> <span data-ttu-id="ea38a-113">每個微服務都會在個別的進程中執行，而且通常會在部署至叢集*的容器內執行。*</span><span class="sxs-lookup"><span data-stu-id="ea38a-113">Each microservice executes in a separate process and typically runs inside a container that is deployed to a *cluster*.</span></span>

<span data-ttu-id="ea38a-114">叢集會將虛擬機器的集區群組在一起，以形成高可用性環境。</span><span class="sxs-lookup"><span data-stu-id="ea38a-114">A cluster groups a pool of virtual machines together to form a highly available environment.</span></span> <span data-ttu-id="ea38a-115">它們是使用協調流程工具管理的，負責部署和管理容器化微服務。</span><span class="sxs-lookup"><span data-stu-id="ea38a-115">They're managed with an orchestration tool, which is responsible for deploying and managing the containerized microservices.</span></span> <span data-ttu-id="ea38a-116">圖4-1 顯示使用完全受控的[Azure Kubernetes 服務](/azure/aks/intro-kubernetes)，將[Kubernetes](https://kubernetes.io)叢集部署到 azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="ea38a-116">Figure 4-1 shows a [Kubernetes](https://kubernetes.io) cluster deployed into the Azure cloud with the fully managed [Azure Kubernetes Services](/azure/aks/intro-kubernetes).</span></span>

![Azure 中的 Kubernetes 叢集](./media/kubernetes-cluster-in-azure.png)

<span data-ttu-id="ea38a-118">**圖 4-1**。</span><span class="sxs-lookup"><span data-stu-id="ea38a-118">**Figure 4-1**.</span></span> <span data-ttu-id="ea38a-119">Azure 中的 Kubernetes 叢集</span><span class="sxs-lookup"><span data-stu-id="ea38a-119">A Kubernetes cluster in Azure</span></span>

<span data-ttu-id="ea38a-120">在整個叢集中，微服務會透過 Api 和訊息技術彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="ea38a-120">Across the cluster, microservices communicate with each other through APIs and messaging technologies.</span></span>

<span data-ttu-id="ea38a-121">雖然它們提供許多優點，但微服務並沒有任何免費的午餐。</span><span class="sxs-lookup"><span data-stu-id="ea38a-121">While they provide many benefits, microservices are no free lunch.</span></span> <span data-ttu-id="ea38a-122">元件之間的本機同進程方法呼叫現在會取代為網路呼叫。</span><span class="sxs-lookup"><span data-stu-id="ea38a-122">Local in-process method calls between components are now replaced with network calls.</span></span> <span data-ttu-id="ea38a-123">每個微服務都必須透過網路通訊協定進行通訊，這會增加系統的複雜度：</span><span class="sxs-lookup"><span data-stu-id="ea38a-123">Each microservice must communicate over a network protocol, which adds complexity to your system:</span></span>

- <span data-ttu-id="ea38a-124">網路擁塞、延遲和暫時性錯誤都是固定的問題。</span><span class="sxs-lookup"><span data-stu-id="ea38a-124">Network congestion, latency, and transient faults are a constant concern.</span></span>

- <span data-ttu-id="ea38a-125">復原 (也就是，重試失敗的要求) 是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="ea38a-125">Resiliency (that is, retrying failed requests) is essential.</span></span>

- <span data-ttu-id="ea38a-126">某些呼叫必須具有 [等冪](https://www.restapitutorial.com/lessons/idempotency.html) 性，才能維持一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="ea38a-126">Some calls must be [idempotent](https://www.restapitutorial.com/lessons/idempotency.html) as to keep consistent state.</span></span>

- <span data-ttu-id="ea38a-127">每個微服務都必須驗證並授權呼叫。</span><span class="sxs-lookup"><span data-stu-id="ea38a-127">Each microservice must authenticate and authorize calls.</span></span>

- <span data-ttu-id="ea38a-128">每個訊息都必須序列化然後還原序列化，這可能會很耗費資源。</span><span class="sxs-lookup"><span data-stu-id="ea38a-128">Each message must be serialized and then deserialized - which can be expensive.</span></span>

- <span data-ttu-id="ea38a-129">訊息加密/解密變得很重要。</span><span class="sxs-lookup"><span data-stu-id="ea38a-129">Message encryption/decryption becomes important.</span></span>

<span data-ttu-id="ea38a-130">[.Net 微服務：容器化 .Net 應用程式的架構](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook)（可從 Microsoft 免費取得）可為微服務應用程式提供深入的通訊模式涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="ea38a-130">The book [.NET Microservices: Architecture for Containerized .NET Applications](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook), available for free from Microsoft, provides an in-depth coverage of communication patterns for microservice applications.</span></span> <span data-ttu-id="ea38a-131">在本章中，我們會提供這些模式的概要說明，以及 Azure 雲端中可用的執行選項。</span><span class="sxs-lookup"><span data-stu-id="ea38a-131">In this chapter, we provide a high-level overview of these patterns along with implementation options available in the Azure cloud.</span></span>

<span data-ttu-id="ea38a-132">在本章中，我們會先解決前端應用程式與後端微服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="ea38a-132">In this chapter, we'll first address communication between front-end applications and back-end microservices.</span></span> <span data-ttu-id="ea38a-133">接著，我們會查看後端微服務彼此通訊的方式。</span><span class="sxs-lookup"><span data-stu-id="ea38a-133">We'll then look at back-end microservices communicate with each other.</span></span> <span data-ttu-id="ea38a-134">我們將探索 up 和 gRPC 通訊技術。</span><span class="sxs-lookup"><span data-stu-id="ea38a-134">We'll explore the up and gRPC communication technology.</span></span> <span data-ttu-id="ea38a-135">最後，我們將使用服務網格技術來尋找新的創新通訊模式。</span><span class="sxs-lookup"><span data-stu-id="ea38a-135">Finally, we'll look new innovative communication patterns using service mesh technology.</span></span> <span data-ttu-id="ea38a-136">我們也會看到 Azure 雲端如何提供不同類型的支援 *服務* ，以支援雲端原生通訊。</span><span class="sxs-lookup"><span data-stu-id="ea38a-136">We'll also see how the Azure cloud provides different kinds of *backing services* to support cloud-native communication.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="ea38a-137">[上一個](other-deployment-options.md) 
>[下一步](front-end-communication.md)</span><span class="sxs-lookup"><span data-stu-id="ea38a-137">[Previous](other-deployment-options.md)
[Next](front-end-communication.md)</span></span>
