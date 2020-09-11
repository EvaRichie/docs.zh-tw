---
title: 容器化整合型應用程式
description: 容器化整合型應用程式雖然無法從微服務架構獲得所有好處，但可立即提供重要部署優勢。
ms.date: 01/30/2020
ms.openlocfilehash: b26a9b79ec00ba06404a12d62343ea31d67151cb
ms.sourcegitcommit: 6d4ee46871deb9ea1e45bb5f3784474e240bbc26
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/11/2020
ms.locfileid: "90022879"
---
# <a name="containerizing-monolithic-applications"></a>容器化整合型應用程式

您可能想要建置單一完整部署的 Web 應用程式或服務，並將它部署為容器。 應用程式本身從內部來看可能不是單體式，而是結構化為數個程式庫、元件或甚至是階層 (應用程式層、領域層、資料存取層等)。 不過從外部來看，它是單一容器 (單一處理序、單一 Web 應用程式或單一服務)。

為了管理此模型，您會部署單一容器來代表應用程式。 若要增加容量，您需要進行擴充，也就是只在前端新增多個含有負載平衡器的複本。 由於是在單一容器或 VM 中管理單一部署，因此很簡單。

![顯示整合型容器化應用程式元件的圖表。](./media/containerize-monolithic-applications/monolithic-containerized-application.png)

**圖 4-1**。 容器化整合型應用程式的架構範例

您可以在每個容器中包含多個元件、程式庫或內部階層，如圖 4-1 所示。 整合型容器化應用程式在單一容器內具有內部層或程式庫的大部分功能，並藉由將容器複製到多部伺服器/Vm 來相應放大。 不過，此整合型模式可能會與「容器執行一項動作並在一個處理序中執行」的容器原則衝突，但在某些情況下可能沒問題。

如果應用程式成長而需要擴充，此方法的缺點會變得很明顯。 若可調整整個應用程式，則不成問題。 不過，在大部分情況下，應用程式的幾個部分是需要調整的扼點，而其他元件則較少使用。

例如，在典型電子商務應用程式中，您可能需要擴充產品資訊子系統，因為比起購買產品，會有更多客戶瀏覽產品。 比起使用付款管道，會有更多客戶使用其購物籃。 新增留言或檢視其購買歷程記錄的客戶較少。 而且，您可能只有少數幾個員工需要管理內容和行銷活動。 如果您擴充整合型設計，這些不同工作的所有程式碼會部署多次並等比例擴充。

調整應用程式的方式有許多種：水平複製、分割應用程式的不同區域，以及分割類似的商務概念或資料。 但除了擴充所有元件的問題之外，每個元件的變更都需要完整重新測試整個應用程式，並完整重新部署所有執行個體。

不過，整合型方法並不常見，因為應用程式開發一開始會比微服務方法更容易。 因此，許多組織會使用此架構方法進行開發。 雖然某些組織的結果就已夠好，但其他組織會遇到極限。 許多組織使用此模型來設計其應用程式，因為多年前的工具和基礎結構很難建置服務導向架構 (SOA)，而且在應用程式成長之前也沒有需求。

從基礎結構的觀點來看，每部伺服器可以在相同主機內執行許多應用程式，並有可接受的資源使用效率比，如圖 4-2 所示。

![顯示一部主機在容器中執行許多應用程式的圖表。](./media/containerize-monolithic-applications/host-multiple-apps-containers.png)

**圖 4-2**。 整合型方法：執行多個應用程式的主機，每個應用程式會當做容器來執行

您可以針對每個執行個體使用專用 VM，在 Microsoft Azure 中部署整合型應用程式。 此外，您還可以使用 [Azure 虛擬機器擴展集](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)輕鬆地調整 VM。 [Azure App Service](https://azure.microsoft.com/services/app-service/) 也可以執行整合型應用程式並輕鬆地擴充執行個體，而不需要您管理 VM。 從 2016 年開始，Azure App Service 也可以執行 Docker 容器的單一執行個體，以簡化部署。

在 QA 環境或有限的生產環境中，您可以部署多部 Docker 主機 VM 並使用 Azure 平衡器進行平衡，如圖 4-3 所示。 這可讓您以粗略的方法來管理擴充，因為整個應用程式都位於單一容器內。

![此圖顯示數個執行整合型應用程式容器的主機。](./media/containerize-monolithic-applications/docker-infrastructure-monolithic-application.png)

**圖 4-3**。 向上擴充單一容器應用程式的多部主機範例

您可以透過傳統部署技術來管理不同主機的部署， 並可以手動執行 `docker run` 或 `docker-compose` 等命令，或是透過持續傳遞 (CD) 管線等自動化方法來管理 Docker 主機。

## <a name="deploying-a-monolithic-application-as-a-container"></a>將整合型應用程式部署為容器

使用容器來管理整合型應用程式部署有許多優點。 擴充容器執行個體遠比部署額外的 VM 更輕鬆快速。 即使您使用虛擬機器擴展集，VM 還是需要時間才能啟動。 部署為傳統應用程式執行個體而不是容器時，應用程式的組態會當作 VM 的一部分來管理，這並不理想。

以 Docker 映像來部署更新會更快且網路效率更高。 Docker 映像通常只要幾秒鐘就能啟動，因此可加速推出。 卸除 Docker 映像執行個體很容易，只要發出 `docker stop` 命令即可，而且通常不到一秒就會完成。

由於容器根據設計是不可變的，因此您永遠不必擔心已損毀的 VM。 相反地，VM 的更新指令碼可能會忘記說明某些特定組態，或忘記有檔案還留在磁碟上。

雖然整合型應用程式可以從 Docker 獲益，但這只是一小部分優點。 管理容器的其他優點來自於使用容器協調器進行部署，這會管理各種執行個體和每個容器執行個體的生命週期。 將整合型應用程式分成可個別擴充、開發及部署的多個子系統，是您開始使用微服務的不錯起點。

## <a name="publishing-a-single-container-based-application-to-azure-app-service"></a>將單一容器應用程式發行至 Azure App Service

不論您想要取得部署至 Azure 的容器驗證，還是在應用程式只是單一容器應用程式的情況下，Azure App Service 都有絕佳的方法來提供可擴充的單一容器服務。 使用 Azure App Service 很簡單。 它提供與 Git 的絕佳整合，讓您可以輕鬆地取得程式碼、在 Visual Studio 中建置，並將它直接部署至 Azure。

![顯示容器登錄的 [建立 App Service] 對話方塊的螢幕擷取畫面。](./media/containerize-monolithic-applications/publish-azure-app-service-container.png)

**圖 4-4**。 從 Visual Studio 2019 將單一容器應用程式發佈至 Azure App Service

之前沒有 Docker 時，如果您需要 Azure App Service 不支援的其他功能、架構或相依性，您必須等到 Azure 小組更新 App Service 中的這些相依性。 或者，您必須切換至其他服務 (例如 Azure 雲端服務或 VM)，才能進一步控制並可安裝應用程式的必要元件或架構。

Visual Studio 2017 和更新版本中的容器支援可讓您在應用程式環境中包含您要的任何項目，如圖 4-4 所示。 由於您在容器中執行，因此如果您將相依性新增至應用程式，您可以在 Dockerfile 或 Docker 映像中包含此相依性。

此外，如圖 4-4 所示，發行流程會透過容器登錄推送映像。 這可以是 Azure Container Registry (接近您的 Azure 部署並受到 Azure Active Directory 群組和帳戶保護的登錄)，或任何其他 Docker 登錄，例如 Docker Hub 或內部部署登錄。

>[!div class="step-by-step"]
>[上一個](index.md) 
>[下一步](docker-application-state-data.md)
