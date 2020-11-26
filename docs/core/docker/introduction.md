---
title: Docker 簡介
description: 本文在 .NET Core 應用程式內容中提供了 Docker 的簡介及概觀。
ms.date: 03/20/2019
ms.custom: mvc
ms.openlocfilehash: 6303c16e914c86f3a431a9e5367e6feb8ff88c9e
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "95724738"
---
# <a name="introduction-to-net-and-docker"></a>.NET 和 Docker 簡介

.NET Core 能夠很容易地在 Docker 容器中執行。 容器提供精簡的方式將您的應用程式與主機系統的其餘部分隔離、只共用核心，以及使用提供給應用程式的資源。 如果不熟悉 Docker，強烈建議閱讀 Docker 的[概觀文件](https://docs.docker.com/engine/docker-overview/) \(英文\)。

如需有關如何安裝 Docker 的詳細資訊，請參閱 Docker Desktop 的下載頁面 [：社區版](https://www.docker.com/products/docker-desktop)。

## <a name="docker-basics"></a>Docker 基本知識

有幾個概念您應該很熟悉。 Docker 用戶端具有可用來管理映射和容器的 CLI。 如先前所述，您應該仔細閱讀 [Docker 概觀](https://docs.docker.com/engine/docker-overview/) \(英文\) 文件。

### <a name="images"></a>影像

映像是構成容器基礎且已排序的檔案系統變更集合。 映像沒有狀態，而且是唯讀的。 映像很多時候會以另一個映像作為基礎，但包含一些自訂項目。 例如，在建立新的應用程式映像時，可以利用已包含 .NET Core 執行階段的現有映像作為基礎。

因為容器是從映像建立的，所以映像會有一組在容器啟動時執行的執行參數 (例如啟動可執行檔)。

### <a name="containers"></a>容器

容器是可執行的映像執行個體。 建置映像時，可以部署您的應用程式和相依項目。 然後，可以具現化多個容器，每個都會彼此隔離。 每個容器執行個體都有自己的檔案系統、記憶體和網路介面。

### <a name="registries"></a>登錄

容器登錄是映像存放庫的集合。 您可以使用登錄映像作為映像的基礎。 您可以在登錄中直接從映像建立容器。 在[進行容器化應用程式或微服務的架構設計及建置](../../architecture/microservices/architect-microservice-container-applications/index.md)時，[Docker 容器、映像和登錄之間的關係](../../architecture/microservices/container-docker-introduction/docker-containers-images-registries.md)是相當重要的概念。 此作法能大幅縮短開發和部署之間的時間。

Docker 擁有公用登錄，已裝載於 [Docker Hub](https://hub.docker.com/) \(英文\) 供您使用。 Docker Hub 會列出 [.NET core 相關映像](https://hub.docker.com/_/microsoft-dotnet/) \(英文\)。

[Microsoft Container Registry (MCR) ](/azure/container-registry)是 microsoft 所提供容器映射的官方來源。 MCR 建置在 Azure CDN 上，用來提供全域複寫的映像。 不過，MCR 並沒有公開網站，因此了解 Microsoft 所提供容器映像的主要方式是透過 [Microsoft Docker Hub 頁面](https://hub.docker.com/_/microsoft-dotnet/) \(英文\)。

### <a name="dockerfile"></a>Dockerfile

**Dockerfile** 是一個檔案，定義了一組建立映像的指示。 **Dockerfile** 中的每個指示都會在映像中建立一個圖層。 大部分的情況下，當您重建映射時，只會重建已變更的圖層。 **Dockerfile** 可散發給其他人，並可讓他們以您建立的相同方式重新建立新的映射。 雖然這可讓您散發映像建立方式的 *指示*，但散發映像的主要方式是將它發行至登錄。

## <a name="net-core-images"></a>.NET Core 映像

官方 .NET Core Docker 映像會發佈至 Microsoft 容器登錄 (MCR)，並且可在 [Microsoft.NET Core Docker Hub 存放庫](https://hub.docker.com/_/microsoft-dotnet/) \(英文\) 中找到。 每個存放庫都包含您可以使用的 .NET (SDK 或執行階段) 與作業系統不同組合的映像。

Microsoft 會提供針對特定案例量身訂做的映像。 例如，[ASP.NET Core 存放庫](https://hub.docker.com/_/microsoft-dotnet-aspnet/) \(英文\) 可提供為了在生產環境中執行 ASP.NET Core 應用程式而建置的映像。

## <a name="azure-services"></a>Azure 服務

各種 Azure 服務支援容器。 您可以為應用程式建立 Docker 映像，並將它部署到下列其中一個服務：

- [Azure Kubernetes Service (AKS) ](https://azure.microsoft.com/services/kubernetes-service/)\
調整規模及協調使用 Kubernetes 的 Linux 容器。

- [Azure App Service](https://azure.microsoft.com/services/app-service/containers/)\
在 PaaS 環境中使用 Linux 容器部署 Web 應用程式或 API。

- [Azure 容器實例](https://azure.microsoft.com/services/container-instances/)\
在沒有任何較高層級管理服務的情況下，將容器裝載於雲端。

- [Azure Batch](https://azure.microsoft.com/services/batch/)\
使用容器執行重複的計算工作。

- [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)\
使用 Windows Server 容器將 .NET 應用程式隨即轉移和現代化，以微服務。

- [Azure Container Registry](https://azure.microsoft.com/services/container-registry/)\
儲存及管理所有 Azure 部署類型的容器映像。

## <a name="next-steps"></a>後續步驟

- [了解如何將 .NET Core 應用程式容器化。](build-container.md)
- [了解如何將 ASP.NET Core 應用程式容器化。](/aspnet/core/host-and-deploy/docker/building-net-docker-images)
- [嘗試「了解 ASP.NET Core 微服務」教學課程。](https://dotnet.microsoft.com/learn/web/aspnet-microservice-tutorial/intro)
- [了解 Visual Studio 中的容器工具](/visualstudio/containers/overview)
