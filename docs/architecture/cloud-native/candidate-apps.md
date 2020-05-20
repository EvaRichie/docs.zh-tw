---
title: 適用于雲端原生的候選應用程式
description: 瞭解哪些類型的應用程式可從雲端原生方法獲益
author: robvet
ms.date: 05/14/2020
ms.openlocfilehash: b907a17b2351bc4ffe49fd6eb6f5963b209d00db
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83614236"
---
# <a name="candidate-apps-for-cloud-native"></a><span data-ttu-id="02bba-103">適用于雲端原生的候選應用程式</span><span class="sxs-lookup"><span data-stu-id="02bba-103">Candidate apps for cloud native</span></span>

<span data-ttu-id="02bba-104">查看您的組合中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="02bba-104">Look at the apps in your portfolio.</span></span> <span data-ttu-id="02bba-105">有多少人符合雲端原生架構的資格？</span><span class="sxs-lookup"><span data-stu-id="02bba-105">How many of them qualify for a cloud-native architecture?</span></span> <span data-ttu-id="02bba-106">全部？</span><span class="sxs-lookup"><span data-stu-id="02bba-106">All of them?</span></span> <span data-ttu-id="02bba-107">也許有些嗎？</span><span class="sxs-lookup"><span data-stu-id="02bba-107">Perhaps some?</span></span>

<span data-ttu-id="02bba-108">套用成本/權益分析，很有可能不會支援雲端原生所需的等於沉重 price 標記。</span><span class="sxs-lookup"><span data-stu-id="02bba-108">Applying a cost/benefit analysis, there's a good chance that most wouldn't support the hefty price tag required to be cloud native.</span></span> <span data-ttu-id="02bba-109">雲端原生的成本遠遠超過應用程式的商業價值。</span><span class="sxs-lookup"><span data-stu-id="02bba-109">The cost of being cloud native would far exceed the business value of the application.</span></span>

<span data-ttu-id="02bba-110">何種類型的應用程式可能是雲端原生的候選項目？</span><span class="sxs-lookup"><span data-stu-id="02bba-110">What type of application might be a candidate for cloud native?</span></span>

- <span data-ttu-id="02bba-111">需要不斷演進商務功能/功能的策略性企業系統</span><span class="sxs-lookup"><span data-stu-id="02bba-111">Strategic enterprise system that need to constantly evolve business capabilities/features</span></span>

- <span data-ttu-id="02bba-112">需要高發行速度的應用程式，具有高度信賴度</span><span class="sxs-lookup"><span data-stu-id="02bba-112">An application that requires a high release velocity - with high confidence</span></span>

- <span data-ttu-id="02bba-113">一種系統，其中個別功能必須在不完整重新部署整個系統的情況*下*發行</span><span class="sxs-lookup"><span data-stu-id="02bba-113">A system with where individual features must release *without* a full redeployment of the entire system</span></span>

- <span data-ttu-id="02bba-114">由小組開發的應用程式，具有不同技術堆疊的專業知識</span><span class="sxs-lookup"><span data-stu-id="02bba-114">An application developed by teams with expertise in different technology stacks</span></span>

- <span data-ttu-id="02bba-115">具有必須獨立調整之元件的應用程式</span><span class="sxs-lookup"><span data-stu-id="02bba-115">An application with components that must scale independently</span></span>

<span data-ttu-id="02bba-116">那就是舊版系統。</span><span class="sxs-lookup"><span data-stu-id="02bba-116">Then there are legacy systems.</span></span> <span data-ttu-id="02bba-117">雖然我們想要建立新的應用程式，但我們通常會負責現代化對企業而言非常重要的舊版工作負載。</span><span class="sxs-lookup"><span data-stu-id="02bba-117">While we'd all like to build new applications, we're often responsible for modernizing legacy workloads that are critical to the business.</span></span> <span data-ttu-id="02bba-118">一段時間後，繼承應用程式可能會分解成微服務、容器化，最後是「replatformed」到雲端原生架構中。</span><span class="sxs-lookup"><span data-stu-id="02bba-118">Over time, a legacy application could be decomposed into microservices, containerized, and ultimately "replatformed" into a cloud-native architecture.</span></span>

### <a name="modernizing-legacy-apps"></a><span data-ttu-id="02bba-119">現代化繼承應用程式</span><span class="sxs-lookup"><span data-stu-id="02bba-119">Modernizing legacy apps</span></span>

<span data-ttu-id="02bba-120">免費的 Microsoft 電子書[現代化現有的 .net 應用程式與 Azure 雲端和 Windows 容器](https://dotnet.microsoft.com/download/thank-you/modernizing-existing-net-apps-ebook)，提供將內部部署工作負載遷移至雲端的指引。</span><span class="sxs-lookup"><span data-stu-id="02bba-120">The free Microsoft e-book [Modernize existing .NET applications with Azure cloud and Windows Containers](https://dotnet.microsoft.com/download/thank-you/modernizing-existing-net-apps-ebook) provides guidance for migrating on-premises workloads into cloud.</span></span> <span data-ttu-id="02bba-121">圖1-10 顯示現代化繼承應用程式不會有單一大小適用的策略。</span><span class="sxs-lookup"><span data-stu-id="02bba-121">Figure 1-10 shows that there isn't a single, one-size-fits-all strategy for modernizing legacy applications.</span></span>

![遷移舊版工作負載的策略](./media/strategies-for-migrating-legacy-workloads.png)

<span data-ttu-id="02bba-123">**圖 1-10**。</span><span class="sxs-lookup"><span data-stu-id="02bba-123">**Figure 1-10**.</span></span> <span data-ttu-id="02bba-124">遷移舊版工作負載的策略</span><span class="sxs-lookup"><span data-stu-id="02bba-124">Strategies for migrating legacy workloads</span></span>

<span data-ttu-id="02bba-125">非關鍵的整合型應用程式，主要受益于快速隨即轉移（[雲端基礎結構就緒](../modernize-with-azure-containers/lift-and-shift-existing-apps-azure-iaas.md)）的遷移。</span><span class="sxs-lookup"><span data-stu-id="02bba-125">Monolithic apps that are non-critical largely benefit from a quick lift-and-shift ([Cloud Infrastructure-Ready](../modernize-with-azure-containers/lift-and-shift-existing-apps-azure-iaas.md)) migration.</span></span> <span data-ttu-id="02bba-126">在這裡，內部部署工作負載會重新裝載至雲端式 VM，而不會變更。</span><span class="sxs-lookup"><span data-stu-id="02bba-126">Here, the on-premises workload is rehosted to a cloud-based VM, without changes.</span></span> <span data-ttu-id="02bba-127">此方法使用[IaaS （基礎結構即服務）模型](https://azure.microsoft.com/overview/what-is-iaas/)。</span><span class="sxs-lookup"><span data-stu-id="02bba-127">This approach uses the [IaaS (Infrastructure as a Service) model](https://azure.microsoft.com/overview/what-is-iaas/).</span></span> <span data-ttu-id="02bba-128">Azure 包含數個工具，例如[Azure Migrate](https://azure.microsoft.com/services/azure-migrate/)、 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)和[Azure 資料庫移轉服務](https://azure.microsoft.com/campaigns/database-migration/)，讓這類移動變得更容易。</span><span class="sxs-lookup"><span data-stu-id="02bba-128">Azure includes several tools such as [Azure Migrate](https://azure.microsoft.com/services/azure-migrate/), [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/), and [Azure Database Migration Service](https://azure.microsoft.com/campaigns/database-migration/) to make such a move easier.</span></span> <span data-ttu-id="02bba-129">雖然此策略可以節省一些成本，但這類應用程式通常無法解除鎖定並運用雲端運算的優點。</span><span class="sxs-lookup"><span data-stu-id="02bba-129">While this strategy can yield some cost savings, such applications typically weren't architected to unlock and leverage the benefits of cloud computing.</span></span>

<span data-ttu-id="02bba-130">對企業而言至關重要的整合型應用程式，往往受益于增強的隨即轉移（*雲端優化*）遷移。</span><span class="sxs-lookup"><span data-stu-id="02bba-130">Monolithic apps that are critical to the business oftentimes benefit from an enhanced lift-and-shift (*Cloud Optimized*) migration.</span></span> <span data-ttu-id="02bba-131">此方法包含可啟用重要雲端服務的部署優化，而不需變更應用程式的核心架構。</span><span class="sxs-lookup"><span data-stu-id="02bba-131">This approach includes deployment optimizations that enable key cloud services - without changing the core architecture of the application.</span></span> <span data-ttu-id="02bba-132">例如，您可能會[容器化](https://docs.microsoft.com/virtualization/windowscontainers/about/)應用程式，並將它部署到容器協調器（例如[Azure Kubernetes Services](https://azure.microsoft.com/services/kubernetes-service/)），這本書稍後會討論到。</span><span class="sxs-lookup"><span data-stu-id="02bba-132">For example, you might [containerize](https://docs.microsoft.com/virtualization/windowscontainers/about/) the application and deploy it to a container orchestrator, like [Azure Kubernetes Services](https://azure.microsoft.com/services/kubernetes-service/), discussed later in this book.</span></span> <span data-ttu-id="02bba-133">一旦進入雲端，應用程式可能會耗用其他雲端服務，例如資料庫、訊息佇列、監視和分散式快取。</span><span class="sxs-lookup"><span data-stu-id="02bba-133">Once in the cloud, the application could consume other cloud services such as databases, message queues, monitoring, and distributed caching.</span></span>

<span data-ttu-id="02bba-134">最後，執行策略性企業功能的整合型應用程式，對於*雲端原生*方法（本書的主旨）可能會有最大的好處。</span><span class="sxs-lookup"><span data-stu-id="02bba-134">Finally, monolithic apps that perform strategic enterprise functions might best benefit from a *Cloud-Native* approach, the subject of this book.</span></span> <span data-ttu-id="02bba-135">這種方法提供了靈活性和速度。</span><span class="sxs-lookup"><span data-stu-id="02bba-135">This approach provides agility and velocity.</span></span> <span data-ttu-id="02bba-136">但是，它的代價是遷移、重新架構和重寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="02bba-136">But, it comes at a cost of replatforming, rearchitecting, and rewriting code.</span></span>

<span data-ttu-id="02bba-137">如果您和您的小組相信雲端原生方法是適當的，它對您以合理化組織的決策。</span><span class="sxs-lookup"><span data-stu-id="02bba-137">If you and your team believe a cloud-native approach is appropriate, it behooves you to rationalize the decision with your organization.</span></span> <span data-ttu-id="02bba-138">雲端原生方法所能解決的商務問題到底是什麼？</span><span class="sxs-lookup"><span data-stu-id="02bba-138">What exactly is the business problem that a cloud-native approach will solve?</span></span> <span data-ttu-id="02bba-139">它如何與商務需求一致？</span><span class="sxs-lookup"><span data-stu-id="02bba-139">How would it align with business needs?</span></span>

- <span data-ttu-id="02bba-140">功能的快速發行增加了信心嗎？</span><span class="sxs-lookup"><span data-stu-id="02bba-140">Rapid releases of features with increased confidence?</span></span>

- <span data-ttu-id="02bba-141">更細緻的擴充性-更有效率地使用資源？</span><span class="sxs-lookup"><span data-stu-id="02bba-141">Fine-grained scalability - more efficient usage of resources?</span></span>

- <span data-ttu-id="02bba-142">改良的系統復原功能？</span><span class="sxs-lookup"><span data-stu-id="02bba-142">Improved system resiliency?</span></span>

- <span data-ttu-id="02bba-143">已改善系統效能？</span><span class="sxs-lookup"><span data-stu-id="02bba-143">Improved system performance?</span></span>

- <span data-ttu-id="02bba-144">有更多的作業可見度嗎？</span><span class="sxs-lookup"><span data-stu-id="02bba-144">More visibility into operations?</span></span>

- <span data-ttu-id="02bba-145">Blend 開發平臺和資料存放區，以取得最適合工作的工具嗎？</span><span class="sxs-lookup"><span data-stu-id="02bba-145">Blend development platforms and data stores to arrive at the best tool for the job?</span></span>

- <span data-ttu-id="02bba-146">未來證明應用程式的投資？</span><span class="sxs-lookup"><span data-stu-id="02bba-146">Future-proof application investment?</span></span>

<span data-ttu-id="02bba-147">適當的遷移策略取決於組織優先順序和您的目標系統。</span><span class="sxs-lookup"><span data-stu-id="02bba-147">The right migration strategy depends on organizational priorities and the systems you're targeting.</span></span> <span data-ttu-id="02bba-148">對許多人而言，將整合型應用程式優化，或將粗略服務新增至多層式應用程式，可能會更符合成本效益。</span><span class="sxs-lookup"><span data-stu-id="02bba-148">For many, it may be more cost effective to cloud-optimize a monolithic application or add coarse-grained services to an N-Tier app.</span></span> <span data-ttu-id="02bba-149">在這些情況下，您仍然可以充分利用雲端 PaaS 功能，例如 Azure App Service 所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="02bba-149">In these cases, you can still make full use of cloud PaaS capabilities like the ones offered by Azure App Service.</span></span>

## <a name="summary"></a><span data-ttu-id="02bba-150">摘要</span><span class="sxs-lookup"><span data-stu-id="02bba-150">Summary</span></span>

<span data-ttu-id="02bba-151">在本章中，我們引進了雲端原生運算。</span><span class="sxs-lookup"><span data-stu-id="02bba-151">In this chapter, we introduced cloud-native computing.</span></span> <span data-ttu-id="02bba-152">我們提供了一種定義，以及驅動雲端原生應用程式的主要功能。</span><span class="sxs-lookup"><span data-stu-id="02bba-152">We provided a definition along with the key capabilities that drive a cloud-native application.</span></span> <span data-ttu-id="02bba-153">我們探討了可能會證明這項投資和投入時間的應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="02bba-153">We looked at the types of applications that might justify this investment and effort.</span></span>

<span data-ttu-id="02bba-154">隨著背後的介紹，我們現在深入探討雲端原生的詳細探討。</span><span class="sxs-lookup"><span data-stu-id="02bba-154">With the introduction behind, we now dive into a much more detailed look at cloud native.</span></span>

### <a name="references"></a><span data-ttu-id="02bba-155">參考</span><span class="sxs-lookup"><span data-stu-id="02bba-155">References</span></span>

- [<span data-ttu-id="02bba-156">雲端原生運算基礎</span><span class="sxs-lookup"><span data-stu-id="02bba-156">Cloud Native Computing Foundation</span></span>](https://www.cncf.io/)

- [<span data-ttu-id="02bba-157">.NET 微服務：容器化 .NET 應用程式的架構</span><span class="sxs-lookup"><span data-stu-id="02bba-157">.NET Microservices: Architecture for Containerized .NET applications</span></span>](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook)

- [<span data-ttu-id="02bba-158">使用 Azure 雲端及 Windows 容器將現有 .NET 應用程式現代化</span><span class="sxs-lookup"><span data-stu-id="02bba-158">Modernize existing .NET applications with Azure cloud and Windows Containers</span></span>](https://dotnet.microsoft.com/download/thank-you/modernizing-existing-net-apps-ebook)

- [<span data-ttu-id="02bba-159">雲端原生模式，依 Cornelia Davis</span><span class="sxs-lookup"><span data-stu-id="02bba-159">Cloud Native Patterns by Cornelia Davis</span></span>](https://www.manning.com/books/cloud-native-patterns)

- [<span data-ttu-id="02bba-160">超越12因素應用程式</span><span class="sxs-lookup"><span data-stu-id="02bba-160">Beyond the Twelve-Factor Application</span></span>](https://content.pivotal.io/blog/beyond-the-twelve-factor-app)

- [<span data-ttu-id="02bba-161">什麼是基礎結構即程式碼</span><span class="sxs-lookup"><span data-stu-id="02bba-161">What is Infrastructure as Code</span></span>](https://docs.microsoft.com/azure/devops/learn/what-is-infrastructure-as-code)

- [<span data-ttu-id="02bba-162">Uber 工程的微部署：自信地每天部署</span><span class="sxs-lookup"><span data-stu-id="02bba-162">Uber Engineering's Micro Deploy: Deploying Daily with Confidence</span></span>](https://eng.uber.com/micro-deploy/)

- [<span data-ttu-id="02bba-163">Netflix 如何部署程式碼</span><span class="sxs-lookup"><span data-stu-id="02bba-163">How Netflix Deploys Code</span></span>](https://www.infoq.com/news/2013/06/netflix/)

- [<span data-ttu-id="02bba-164">調整 WeChat 微服務的多載控制</span><span class="sxs-lookup"><span data-stu-id="02bba-164">Overload Control for Scaling WeChat Microservices</span></span>](https://www.cs.columbia.edu/~ruigu/papers/socc18-final100.pdf)

>[!div class="step-by-step"]
><span data-ttu-id="02bba-165">[上一個](definition.md) 
>[下一步](introduce-eshoponcontainers-reference-app.md)</span><span class="sxs-lookup"><span data-stu-id="02bba-165">[Previous](definition.md)
[Next](introduce-eshoponcontainers-reference-app.md)</span></span>
