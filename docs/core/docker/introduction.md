---
title: Docker 簡介
description: 本文在 .NET Core 應用程式內容中提供了 Docker 的簡介及概觀。
ms.date: 03/20/2019
ms.custom: mvc
ms.openlocfilehash: 16ad49c39d588aac8f8a7a918eb4d799f37823ac
ms.sourcegitcommit: 4d45bda8cd9558ea8af4be591e3d5a29360c1ece
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2020
ms.locfileid: "91654818"
---
# <a name="introduction-to-net-and-docker"></a><span data-ttu-id="2b1a7-103">.NET 和 Docker 簡介</span><span class="sxs-lookup"><span data-stu-id="2b1a7-103">Introduction to .NET and Docker</span></span>

<span data-ttu-id="2b1a7-104">.NET Core 能夠很容易地在 Docker 容器中執行。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-104">.NET Core can easily run in a Docker container.</span></span> <span data-ttu-id="2b1a7-105">容器提供精簡的方式將您的應用程式與主機系統的其餘部分隔離、只共用核心，以及使用提供給應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-105">Containers provide a lightweight way to isolate your application from the rest of the host system, sharing just the kernel, and using resources given to your application.</span></span> <span data-ttu-id="2b1a7-106">如果不熟悉 Docker，強烈建議閱讀 Docker 的[概觀文件](https://docs.docker.com/engine/docker-overview/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-106">If you're unfamiliar with Docker, it's highly recommended that you read through Docker's [overview documentation](https://docs.docker.com/engine/docker-overview/).</span></span>

<span data-ttu-id="2b1a7-107">如需有關如何安裝 Docker 的詳細資訊，請參閱 Docker Desktop 的下載頁面 [：社區版](https://www.docker.com/products/docker-desktop)。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-107">For more information about how to install Docker, see the download page for [Docker Desktop: Community Edition](https://www.docker.com/products/docker-desktop).</span></span>

## <a name="docker-basics"></a><span data-ttu-id="2b1a7-108">Docker 基本知識</span><span class="sxs-lookup"><span data-stu-id="2b1a7-108">Docker basics</span></span>

<span data-ttu-id="2b1a7-109">有幾個概念您應該很熟悉。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-109">There are a few concepts you should be familiar with.</span></span> <span data-ttu-id="2b1a7-110">Docker 用戶端具有可用來管理映射和容器的 CLI。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-110">The Docker client has a CLI that you can use to manage images and containers.</span></span> <span data-ttu-id="2b1a7-111">如先前所述，您應該仔細閱讀 [Docker 概觀](https://docs.docker.com/engine/docker-overview/) \(英文\) 文件。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-111">As previously stated, you should take the time to read through the [Docker overview](https://docs.docker.com/engine/docker-overview/) documentation.</span></span>

### <a name="images"></a><span data-ttu-id="2b1a7-112">影像</span><span class="sxs-lookup"><span data-stu-id="2b1a7-112">Images</span></span>

<span data-ttu-id="2b1a7-113">映像是構成容器基礎且已排序的檔案系統變更集合。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-113">An image is an ordered collection of filesystem changes that form the basis of a container.</span></span> <span data-ttu-id="2b1a7-114">映像沒有狀態，而且是唯讀的。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-114">The image doesn't have a state and is read-only.</span></span> <span data-ttu-id="2b1a7-115">映像很多時候會以另一個映像作為基礎，但包含一些自訂項目。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-115">Much the time an image is based on another image, but with some customization.</span></span> <span data-ttu-id="2b1a7-116">例如，在建立新的應用程式映像時，可以利用已包含 .NET Core 執行階段的現有映像作為基礎。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-116">For example, when you create an new image for your application, you would base it on an existing image that already contains the .NET Core runtime.</span></span>

<span data-ttu-id="2b1a7-117">因為容器是從映像建立的，所以映像會有一組在容器啟動時執行的執行參數 (例如啟動可執行檔)。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-117">Because containers are created from images, images have a set of run parameters (such as a starting executable) that run when the container starts.</span></span>

### <a name="containers"></a><span data-ttu-id="2b1a7-118">容器</span><span class="sxs-lookup"><span data-stu-id="2b1a7-118">Containers</span></span>

<span data-ttu-id="2b1a7-119">容器是可執行的映像執行個體。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-119">A container is a runnable instance of an image.</span></span> <span data-ttu-id="2b1a7-120">建置映像時，可以部署您的應用程式和相依項目。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-120">As you build your image, you deploy your application and dependencies.</span></span> <span data-ttu-id="2b1a7-121">然後，可以具現化多個容器，每個都會彼此隔離。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-121">Then, multiple containers can be instantiated, each isolated from one another.</span></span> <span data-ttu-id="2b1a7-122">每個容器執行個體都有自己的檔案系統、記憶體和網路介面。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-122">Each container instance has its own filesystem, memory, and network interface.</span></span>

### <a name="registries"></a><span data-ttu-id="2b1a7-123">登錄</span><span class="sxs-lookup"><span data-stu-id="2b1a7-123">Registries</span></span>

<span data-ttu-id="2b1a7-124">容器登錄是映像存放庫的集合。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-124">Container registries are a collection of image repositories.</span></span> <span data-ttu-id="2b1a7-125">您可以使用登錄映像作為映像的基礎。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-125">You can base your images on a registry image.</span></span> <span data-ttu-id="2b1a7-126">您可以在登錄中直接從映像建立容器。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-126">You can create containers directly from an image in a registry.</span></span> <span data-ttu-id="2b1a7-127">在[進行容器化應用程式或微服務的架構設計及建置](../../architecture/microservices/architect-microservice-container-applications/index.md)時，[Docker 容器、映像和登錄之間的關係](../../architecture/microservices/container-docker-introduction/docker-containers-images-registries.md)是相當重要的概念。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-127">The [relationship between Docker containers, images, and registries](../../architecture/microservices/container-docker-introduction/docker-containers-images-registries.md) is an important concept when [architecting and building containerized applications or microservices](../../architecture/microservices/architect-microservice-container-applications/index.md).</span></span> <span data-ttu-id="2b1a7-128">此作法能大幅縮短開發和部署之間的時間。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-128">This approach greatly shortens the time between development and deployment.</span></span>

<span data-ttu-id="2b1a7-129">Docker 擁有公用登錄，已裝載於 [Docker Hub](https://hub.docker.com/) \(英文\) 供您使用。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-129">Docker has a public registry hosted at the [Docker Hub](https://hub.docker.com/) that you can use.</span></span> <span data-ttu-id="2b1a7-130">Docker Hub 會列出 [.NET core 相關映像](https://hub.docker.com/_/microsoft-dotnet-core/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-130">[.NET Core related images](https://hub.docker.com/_/microsoft-dotnet-core/) are listed at the Docker Hub.</span></span>

<span data-ttu-id="2b1a7-131">[Microsoft Container Registry (MCR) ](/azure/container-registry)是 microsoft 所提供容器映射的官方來源。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-131">The [Microsoft Container Registry (MCR)](/azure/container-registry) is the official source of Microsoft-provided container images.</span></span> <span data-ttu-id="2b1a7-132">MCR 建置在 Azure CDN 上，用來提供全域複寫的映像。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-132">The MCR is built on Azure CDN to provide globally-replicated images.</span></span> <span data-ttu-id="2b1a7-133">不過，MCR 並沒有公開網站，因此了解 Microsoft 所提供容器映像的主要方式是透過 [Microsoft Docker Hub 頁面](https://hub.docker.com/_/microsoft-dotnet-core/) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-133">However, the MCR does not have a public-facing website and the primary way to learn about Microsoft-provided container images is through the [Microsoft Docker Hub pages](https://hub.docker.com/_/microsoft-dotnet-core/).</span></span>

### <a name="dockerfile"></a><span data-ttu-id="2b1a7-134">Dockerfile</span><span class="sxs-lookup"><span data-stu-id="2b1a7-134">Dockerfile</span></span>

<span data-ttu-id="2b1a7-135">**Dockerfile** 是一個檔案，定義了一組建立映像的指示。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-135">A **Dockerfile** is a file that defines a set of instructions that creates an image.</span></span> <span data-ttu-id="2b1a7-136">**Dockerfile** 中的每個指示都會在映像中建立一個圖層。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-136">Each instruction in the **Dockerfile** creates a layer in the image.</span></span> <span data-ttu-id="2b1a7-137">大部分的情況下，當您重建映射時，只會重建已變更的圖層。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-137">For the most part, when you rebuild the image, only the layers that have changed are rebuilt.</span></span> <span data-ttu-id="2b1a7-138">**Dockerfile**可散發給其他人，並可讓他們以您建立的相同方式重新建立新的映射。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-138">The **Dockerfile** can be distributed to others and allows them to recreate a new image in the same manner you created it.</span></span> <span data-ttu-id="2b1a7-139">雖然這可讓您散發映像建立方式的*指示*，但散發映像的主要方式是將它發行至登錄。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-139">While this allows you to distribute the *instructions* on how to create the image, the main way to distribute your image is to publish it to a registry.</span></span>

## <a name="net-core-images"></a><span data-ttu-id="2b1a7-140">.NET Core 映像</span><span class="sxs-lookup"><span data-stu-id="2b1a7-140">.NET Core images</span></span>

<span data-ttu-id="2b1a7-141">官方 .NET Core Docker 映像會發佈至 Microsoft 容器登錄 (MCR)，並且可在 [Microsoft.NET Core Docker Hub 存放庫](https://hub.docker.com/_/microsoft-dotnet-core/) \(英文\) 中找到。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-141">Official .NET Core Docker images are published to the Microsoft Container Registry (MCR) and are discoverable at the [Microsoft .NET Core Docker Hub repository](https://hub.docker.com/_/microsoft-dotnet-core/).</span></span> <span data-ttu-id="2b1a7-142">每個存放庫都包含您可以使用的 .NET (SDK 或執行階段) 與作業系統不同組合的映像。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-142">Each repository contains images for different combinations of the .NET (SDK or Runtime) and OS that you can use.</span></span>

<span data-ttu-id="2b1a7-143">Microsoft 會提供針對特定案例量身訂做的映像。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-143">Microsoft provides images that are tailored for specific scenarios.</span></span> <span data-ttu-id="2b1a7-144">例如，[ASP.NET Core 存放庫](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) \(英文\) 可提供為了在生產環境中執行 ASP.NET Core 應用程式而建置的映像。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-144">For example, the [ASP.NET Core repository](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) provides images that are built for running ASP.NET Core apps in production.</span></span>

## <a name="azure-services"></a><span data-ttu-id="2b1a7-145">Azure 服務</span><span class="sxs-lookup"><span data-stu-id="2b1a7-145">Azure services</span></span>

<span data-ttu-id="2b1a7-146">各種 Azure 服務支援容器。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-146">Various Azure services support containers.</span></span> <span data-ttu-id="2b1a7-147">您可以為應用程式建立 Docker 映像，並將它部署到下列其中一個服務：</span><span class="sxs-lookup"><span data-stu-id="2b1a7-147">You create a Docker image for your application and deploy it to one of the following services:</span></span>

- <span data-ttu-id="2b1a7-148">[Azure Kubernetes Service (AKS) ](https://azure.microsoft.com/services/kubernetes-service/)</span><span class="sxs-lookup"><span data-stu-id="2b1a7-148">[Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service/)</span></span>\
<span data-ttu-id="2b1a7-149">調整規模及協調使用 Kubernetes 的 Linux 容器。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-149">Scale and orchestrate Linux containers using Kubernetes.</span></span>

- <span data-ttu-id="2b1a7-150">[Azure App Service](https://azure.microsoft.com/services/app-service/containers/)</span><span class="sxs-lookup"><span data-stu-id="2b1a7-150">[Azure App Service](https://azure.microsoft.com/services/app-service/containers/)</span></span>\
<span data-ttu-id="2b1a7-151">在 PaaS 環境中使用 Linux 容器部署 Web 應用程式或 API。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-151">Deploy web apps or APIs using Linux containers in a PaaS environment.</span></span>

- <span data-ttu-id="2b1a7-152">[Azure 容器實例](https://azure.microsoft.com/services/container-instances/)</span><span class="sxs-lookup"><span data-stu-id="2b1a7-152">[Azure Container Instances](https://azure.microsoft.com/services/container-instances/)</span></span>\
<span data-ttu-id="2b1a7-153">在沒有任何較高層級管理服務的情況下，將容器裝載於雲端。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-153">Host your container in the cloud without any higher-level management services.</span></span>

- <span data-ttu-id="2b1a7-154">[Azure Batch](https://azure.microsoft.com/services/batch/)</span><span class="sxs-lookup"><span data-stu-id="2b1a7-154">[Azure Batch](https://azure.microsoft.com/services/batch/)</span></span>\
<span data-ttu-id="2b1a7-155">使用容器執行重複的計算工作。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-155">Run repetitive compute jobs using containers.</span></span>

- <span data-ttu-id="2b1a7-156">[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)</span><span class="sxs-lookup"><span data-stu-id="2b1a7-156">[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)</span></span>\
<span data-ttu-id="2b1a7-157">使用 Windows Server 容器將 .NET 應用程式隨即轉移和現代化，以微服務。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-157">Lift, shift, and modernize .NET applications to microservices using Windows Server containers.</span></span>

- <span data-ttu-id="2b1a7-158">[Azure Container Registry](https://azure.microsoft.com/services/container-registry/)</span><span class="sxs-lookup"><span data-stu-id="2b1a7-158">[Azure Container Registry](https://azure.microsoft.com/services/container-registry/)</span></span>\
<span data-ttu-id="2b1a7-159">儲存及管理所有 Azure 部署類型的容器映像。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-159">Store and manage container images across all types of Azure deployments.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b1a7-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b1a7-160">Next steps</span></span>

- [<span data-ttu-id="2b1a7-161">了解如何將 .NET Core 應用程式容器化。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-161">Learn how to containerize a .NET Core application.</span></span>](build-container.md)
- [<span data-ttu-id="2b1a7-162">了解如何將 ASP.NET Core 應用程式容器化。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-162">Learn how to containerize an ASP.NET Core application.</span></span>](/aspnet/core/host-and-deploy/docker/building-net-docker-images)
- [<span data-ttu-id="2b1a7-163">嘗試「了解 ASP.NET Core 微服務」教學課程。</span><span class="sxs-lookup"><span data-stu-id="2b1a7-163">Try the Learn ASP.NET Core Microservice tutorial.</span></span>](https://dotnet.microsoft.com/learn/web/aspnet-microservice-tutorial/intro)
- [<span data-ttu-id="2b1a7-164">了解 Visual Studio 中的容器工具</span><span class="sxs-lookup"><span data-stu-id="2b1a7-164">Learn about Container Tools in Visual Studio</span></span>](/visualstudio/containers/overview)
