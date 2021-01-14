---
title: 協調微服務和多容器應用程式的高延展性和可用性
description: 探索協調微服務和多容器應用程式之高延展性和可用性的各種選項，以及開發 Kubernetes 應用程式生命週期時使用 Azure Dev Spaces 的可能性。
ms.date: 01/13/2021
ms.openlocfilehash: 7ba0367bca98edbab1be2059ee37e863359edad3
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189409"
---
# <a name="orchestrate-microservices-and-multi-container-applications-for-high-scalability-and-availability"></a>協調微服務和多容器應用程式的高延展性和可用性

如果您的應用程式是以微服務為基礎或分散於多個容器，您就必須為適用於生產環境的應用程式使用協調器。 如之前所介紹，以微服務為基礎的方法中，每個微服務都擁有自己的模型和資料，因此從開發和部署的角度來看，它是非常自主的。 但是，即使您擁有的是由多個服務組成的傳統應用程式 (例如 SOA)，您也會使用多個容器或服務來組成單一商務應用程式，而這些項目都必須部署為分散式系統。 向外延展和管理這類系統非常的複雜；因此，如果您想要擁有一個適用於生產環境且可延展的多容器應用程式，就一定要使用協調器。

圖 4-23 說明由多個微服務 (容器) 所組成之應用程式叢集中的部署。

![顯示叢集中所組成之 Docker 應用程式的圖表。](./media/scalable-available-multi-container-microservice-applications/composed-docker-applications-cluster.png)

**圖 4-23**： 容器叢集

您可以為每個服務執行個體各使用一個容器。 Docker 容器是「部署的單位」，而容器是 Docker 的實例。 主機會處理許多容器。 看起來像邏輯方法。 不過，您該如何處理這些組成應用程式的負載平衡、路由及協調作業？

如果是一部主機上單一映像執行個體的管理需求，可靠單一 Docker 主機中的單純 Docker 引擎來滿足，但若是更複雜的分散式應用程式，它就無法滿足部署於多個主機上多個容器的管理需求。 在大多數情況下，您需要一個管理平臺，以自動啟動容器、向外延展容器（每個映射具有多個實例）、暫停它們或在需要時關閉它們，而且在理想情況下也會控制其存取資源的方式，例如網路和資料儲存體。

如果您不只要管理個別容器或組成簡單的應用程式，而是要進展到具有微服務的大型企業應用程式，就必須採用協調流程和叢集平台。

從架構和開發角度來看，如果您要建置由微服務應用程式所組成的大型企業應用程式，請務必了解下列可支援進階案例的平台和產品：

**叢集和協調器**： 當您要跨許多 Docker 主機向外延展應用程式時 (亦即大型微服務應用程式)，您必須簡化基礎平台的複雜性，並以單一叢集的形式來管理其中的所有主機。 而這正是容器叢集和協調器所提供的功能。 Kubernetes 是協調器的一個範例，可以透過 Azure Kubernetes Service 在 Azure 中取得。

**排程器**： 「排程」可讓系統管理員啟動叢集中的容器，因此這些排程器也會提供 UI。 叢集排程器有下列職責：有效率地使用叢集的資源、設定使用者所提供的條件約束、跨節點或主機有效進行容器負載平衡，以及維持容錯性並保障高可用性。

叢集與排程器的概念密切相關，因此不同廠商所提供的產品通常會兩組功能都提供。 下列清單顯示您可以針對叢集和排程器選擇的最重要平台和軟體。 一般來說，Azure 這類公用雲端都會提供這些協調器。

## <a name="software-platforms-for-container-clustering-orchestration-and-scheduling"></a>用於容器叢集、協調流程和排程的軟體平台

|     |   |
|:---:|---|
| **Kubernetes** <br> ![Kubernetes 標誌的影像。](./media/scalable-available-multi-container-microservice-applications/kubernetes-container-orchestration-system-logo.png) | [*Kubernetes*](https://kubernetes.io/) 是開放原始碼產品，可提供叢集基礎結構、容器排程到容器協調等功能。 它可讓您跨主機叢集自動化部署、規模調整及應用程式容器的作業。 <br><br> *Kubernetes* 提供以容器為中心的基礎結構，讓您將應用程式容器分組為邏輯單元，以便於管理及探索。 <br><br> 比起 Windows，*Kubernetes* 在 Linux 中相對成熟穩定。 |
| **Azure Kubernetes Service (AKS)** <br> ![Azure Kubernetes Service 標誌的影像。](./media/scalable-available-multi-container-microservice-applications/azure-kubernetes-service-logo.png) | [AKS](https://azure.microsoft.com/services/kubernetes-service/) 是 Azure 中的受控 Kubernetes 容器協調流程服務，可簡化 Kubernetes 叢集的管理、部署和作業。 |

## <a name="using-container-based-orchestrators-in-microsoft-azure"></a>在 Microsoft Azure 中使用容器協調器

許多雲端廠商都支援 Docker 容器以及 Docker 叢集和協調流程，包括 Microsoft Azure、Amazon EC2 Container Service 和 Google Container Engine。 Microsoft Azure 透過 Azure Kubernetes Service (AKS)，提供 Docker 叢集和協調器支援。

## <a name="using-azure-kubernetes-service"></a>使用 Azure Kubernetes Service

Kubernetes 叢集裝載了多部 Docker 主機，並將其公開為單一虛擬 Docker 主機，因此您可以部署多個容器到該叢集中，並以任意容器執行個體數目向外延展。 叢集會處理所有複雜的管理配置作業，例如延展性、健康狀態等等。

AKS 可讓您以簡化的方式，在 Azure 中建立、組態及管理預先設定為執行容器化應用程式的虛擬機器叢集。 AKS 使用熱門開放原始碼排程和協調流程工具的最佳化組態，可讓您使用現有技能，或運用大量且不斷成長的社群專業知識，在 Microsoft Azure 上部署及管理容器化應用程式。

Azure Kubernetes Service 特別針對 Azure，提供熱門 Docker 叢集開放原始碼工具和技術的最佳化組態。 這樣的開放解決方案，可賦予您容器和應用程式組態的可攜性。 您只要選取主機大小和數目，其餘工作全都由協調器工具和 AKS 處理。

![顯示 Kubernetes 叢集結構的圖表。](./media/scalable-available-multi-container-microservice-applications/kubernetes-cluster-simplified-structure.png)

**圖 4-24**： Kubernetes 叢集的簡化結構和拓撲

在圖4-24 中，您可以看到 Kubernetes 叢集的結構，其中的主要節點 (VM) 控制叢集的大部分協調，而您可以將容器部署到其他節點，這些節點會從應用程式的觀點來當作單一集區來管理，並可讓您擴充至數千個或甚至數千個容器。

## <a name="development-environment-for-kubernetes"></a>Kubernetes 的開發環境

在開發環境中， [docker 于2018年7月宣佈](https://blog.docker.com/2018/07/kubernetes-is-now-available-in-docker-desktop-stable-channel/) ，Kubernetes 也可以在單一開發電腦上執行， (Windows 10 或 macOS) 安裝 [Docker Desktop](https://docs.docker.com/install/)。 您稍後可以部署到雲端 (AKS) 來進一步執行整合測試，如圖 4-25 所示。

![此圖顯示開發電腦上的 Kubernetes，然後部署至 AKS](./media/scalable-available-multi-container-microservice-applications/kubernetes-development-environment.png)

**圖 4-25**： 在開發電腦和雲端中執行 Kubernetes

## <a name="getting-started-with-azure-kubernetes-service-aks"></a>開始使用 Azure Kubernetes Service (AKS)

若要開始使用 AKS，請從 Azure 入口網站或使用 CLI 部署 AKS 叢集。 如需在 Azure 中部署 Kubernetes 叢集的詳細資訊，請參閱[部署 Azure Kubernetes Service (AKS) 叢集](/azure/aks/kubernetes-walkthrough-portal)。

隨附於 AKS 預設安裝的軟體均不會收取任何費用。 所有預設選項都是使用開放原始碼軟體來實作。 AKS 可供 Azure 中的多部虛擬機器使用。 您只需支付所選計算實例的費用，以及所耗用的其他基礎結構資源，例如儲存體和網路功能。 AKS 本身沒有任何累加的費用。

Kubernetes 的預設生產部署選項是使用下一節所引進的 Helm 圖表。

## <a name="deploy-with-helm-charts-into-kubernetes-clusters"></a>使用 Helm 圖表部署到 Kubernetes 叢集中

將應用程式部署到 Kubernetes 叢集時，您可以搭配採用原生格式的部署檔案 (.yaml 檔案) 使用原始 kubectl.exe CLI 工具，如上一節中所述。 不過，對於更複雜的 Kubernetes 應用程式 (例如部署複雜的微服務應用程式時)，則建議使用 [Helm](https://helm.sh/)。

即便是最複雜的 Kubernetes 應用程式，Helm 圖表也能協助您定義、設定版本、安裝、共用、升級或復原。

此外，也建議使用 Helm，因為 Azure 中的其他 Kubernetes 環境（例如 [Azure Dev Spaces](/azure/dev-spaces/azure-dev-spaces) ）也是以 Helm 圖表為基礎。

Helm 是由 [雲端原生運算基礎來維護， () CNCF ](https://www.cncf.io/) 與 Microsoft、Google、Bitnami 和 Helm 參與者社區共同合作。

如需有關 Helm 圖表和 Kubernetes 的詳細資訊，請參閱 [使用 Helm 圖表部署 eShopOnContainers 至 AKS](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Deploy-to-Azure-Kubernetes-Service-(AKS)) 文章。

## <a name="use-azure-dev-spaces-for-your-kubernetes-application-lifecycle"></a>在您的 Kubernetes 應用程式生命週期中使用 Azure Dev Spaces

[Azure Dev Spaces](/azure/dev-spaces/azure-dev-spaces) 為小組提供快速、反復的 Kubernetes 開發體驗。 只需最基本的開發人員機器設定，您即可直接在 Azure Kubernetes Service (AKS) 中反覆執行和偵錯容器。 在 Windows、Mac 或 Linux 上使用熟悉的工具 (例如 Visual Studio、Visual Studio Code 或命令列) 進行開發。

如前所述，Azure Dev Spaces 在部署容器型應用程式時使用 Helm 圖表。

Azure Dev Spaces 可協助開發小組在 Kubernetes 上更具生產力，因為它可讓您使用 Visual Studio 2019 或 Visual Studio Code，直接在 Azure 的全域 Kubernetes 叢集中快速逐一查看和偵測程式碼。 Azure 中的 Kubernetes 叢集是共用的受控 Kubernetes 叢集，讓您的小組可以共同合作。 您可以在隔離的狀況下開發程式碼，然後部署到全域叢集並使用其他元件進行端對端測試，不需要複寫或模擬相依性。

如圖 4-26 所示，Azure Dev Spaces 中最與眾不同的功能，就是能夠建立與叢集中全域部署其餘部分整合的執行「空間」。

![顯示在 Azure Dev Spaces 中使用多個空格的圖表。](./media/scalable-available-multi-container-microservice-applications/use-multiple-spaces-azure-dev.png)

**圖 4-26**。 在 Azure Dev Spaces 中使用多個空間

基本上，您可以在 Azure 中設定共用的開發空間。 每位開發人員可以只專注於他們的應用程式部分，並可以在已包含其案例所依存之所有其他服務和雲端資源的開發空間中，反覆開發預先認可程式碼。 相依性會永遠保持最新狀態，且開發人員會以能反映生產環境的方式工作。

Azure Dev Spaces 提供空間概念，讓您能夠在相對隔離的狀況下工作，不用擔心中斷您小組的工作。 每個開發空間都是階層式結構的一部分，可讓您從最上層的主開發空間，使用您自己的微服務半成品覆寫一個 (或多個) 微服務。

這項功能是以 URL 前置詞作為基礎，因此在 URL 中使用任何開發空間前置詞時，如果該前置詞存在於開發空間中，目標微服務就會提供要求，否則便會往上轉送到階層中所能找到的第一個目標微服務執行個體，最終則會送到最上層的主開發空間。

若要取得具體範例的實際觀點，請參閱 [Azure Dev Spaces 上的 eShopOnContainers wiki 頁面](https://github.com/dotnet-architecture/eShopOnContainers/wiki/Azure-Dev-Spaces)。

如需詳細資訊，請參閱 [使用 Azure Dev Spaces 的小組開發](/azure/dev-spaces/team-development-netcore)文章。

## <a name="additional-resources"></a>其他資源

- **開始使用 Azure Kubernetes Service (AKS)** \
  <https://docs.microsoft.com/azure/aks/kubernetes-walkthrough-portal>

- **Azure Dev Spaces** \
  <https://docs.microsoft.com/azure/dev-spaces/azure-dev-spaces>

- **Kubernetes**：官方網站。 \
  <https://kubernetes.io/>

>[!div class="step-by-step"]
>[上一個](resilient-high-availability-microservices.md) 
>[下一步](../docker-application-development-process/index.md)
