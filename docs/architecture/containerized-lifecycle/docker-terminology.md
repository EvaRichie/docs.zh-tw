---
title: Docker 術語
description: 了解使用 Docker 時每天會用到的一些基本術語。
ms.date: 08/06/2020
ms.openlocfilehash: b47639a2995c3a0a30ea7111c16bbea21f1048ba
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87915192"
---
# <a name="docker-terminology"></a>Docker 術語

本節列出您應該熟悉才能深入探索 Docker 的術語和定義。 如需進一步定義，請參閱 Docker 所提供的詳盡[字彙表](https://docs.docker.com/glossary/)。

**容器映像**：包含建立容器所需之所有相依性和資訊的封裝。 映像會包含所有相依性 (例如架構)，以及容器執行階段所要使用的部署和執行組態。 通常，一個映像會衍生自多個基底映像，這些基底映像是彼此交互堆疊以構成容器檔案系統的圖層。 映像一旦建立，就不可改變。

**Dockerfile**：文字檔，其中包含建立 Docker 映射的指示。 如同批次指令碼，第一行說明開始的基底映像，然後遵循指示安裝必要的程式、複製檔案等，直到取得您需要的工作環境。

**建立**：建立容器映像的動作，該映像會以其 Dockerfile 及建立映像之資料夾中其他檔案所提供的資訊和內容為依據。 您可以使用下列 Docker 命令來建立映射：

```bash
docker build
```

**容器**：Docker 映像的執行個體。 容器代表單一應用程式、處理序或服務的執行。 其中包含 Docker 映像的內容、執行環境和一組標準的指示。 擴充服務時，您會從同一個映像建立容器的多個執行個體。 或者，一個批次工作可以從同一個映像建立多個容器，並將不同的參數傳遞至每個執行個體。

**磁碟區**：提供容器可使用的可寫入檔案系統。 因為映像是唯讀的，但是大部分程式需要寫入到檔案系統 (磁碟區會在容器映像上方新增可寫入的層)，因此程式能夠存取可寫入的檔案系統。 程式並不知道其正在存取分層的檔案系統，其僅為一般的檔案系統。 磁碟區位於主機系統，而且由 Docker 管理。

**標記**：您可以套用至映像的標記或標籤，以便識別相同映像的不同映像版本 (視版本號碼或目標環境而定)。

**多階段建置**：這是 Docker 17.05 或更高版本中的功能，可協助減少最終映像的大小。 例如，包含 SDK 的大型基底映射可以用來編譯和發行，然後使用小型的僅限執行時間基底映射來裝載應用程式。

**存放庫 (Repository 或 Repo)**：相關的 Docker 映像集合，已加上標記指出映像版本。 某些存放庫包含特定映射的多種變體，例如包含 Sdk 的映射 (較大的) 、僅包含執行時間的映射 (較淺的) 等等。這些變體可以標記標記。 一個存放庫可以包含多種平台變化，例如 Linux 映像和 Windows 映像。

**登錄**：提供存放庫存取權的服務。 大多數公用映像的預設登錄是 [Docker Hub](https://hub.docker.com/) (以組織形式為 Docker 所擁有）。 登錄通常會包含來自多個小組的存放庫。 公司通常會有私人登錄來儲存及管理其所建立的映像。 Azure Container Registry 是另一個範例。

**多架構映射**：針對多結構，這項功能可根據 Docker 執行所在的平臺，簡化適當映射的選取。 例如，當 Dockerfile 從登錄要求**mcr.microsoft.com/dotnet/core/sdk:3.1**的基底映射時，它實際上會取得**3.1-sdk-nanoserver-1909**、 **3.1-sdk-nanoserver-1809**或**3.1-sdk-buster-超薄**，視執行 Docker 的作業系統和版本而定。

**Docker Hub**：上傳並使用映像的公開登錄。 Docker Hub 提供 Docker 映像裝載、公開或私人登錄、組建觸發程序和 Webhook，以及與 GitHub 和 Bitbucket 的整合。

**Azure Container Registry**：Azure 中使用 Docker 映像及其元件的公用資源。 這會提供接近 Azure 部署的登錄，並可讓您控制存取權，以便使用您的 Azure Active Directory 群組和權限。

**Docker Trusted Registry (DTR)**：可在內部部署安裝的 Docker 登錄服務 (來自 Docker)，以便存在於組織的資料中心和網路內。 這會方便在企業內管理私人映像。 Docker Trusted Registry 隨附於 Docker Datacenter 產品中。 如需詳細資訊，請參閱 [Docker Trusted Registry (DTR)](https://www.docker.com/sites/default/files/Docker%20Trusted%20Registry.pdf)。

**Docker Community Edition (CE)**：適用於 Windows 和 macOS 的開發工具，可在本機建置、執行及測試容器。 Docker CE for Windows 提供適用於 Linux 和 Windows 容器的開發環境。 Windows 上的 Linux Docker 主機是以 [Hyper-V](https://www.microsoft.com/cloud-platform/server-virtualization) 虛擬機器為基礎。 Windows 容器的主機則是直接以 Windows 為基礎。 Docker CE for Mac 是以 Apple Hypervisor 架構和 [xhyve hypervisor](https://github.com/mist64/xhyve) 為基礎，其提供 Mac OS X 版的 Linux Docker 主機虛擬機器。Docker CE for Windows 和 Docker CE for Mac 取代以 Oracle VirtualBox 為基礎的 Docker Toolbox。

**Docker Enterprise Edition (EE)**：適用於 Linux 和 Windows 開發之企業級版本的 Docker 工具。

**撰寫**：命令列工具和 YAML 檔案格式，其中繼資料可定義及執行多容器應用程式。 您可以使用一或多個 .yml 檔案，來定義以多個映像為基礎的單一應用程式，這些檔案可能會覆寫相依於環境的值。 建立定義之後，您可以使用單一命令 (docker-compose up) 來部署整個多容器應用程式，以在 Docker 主機上針對每個映像建立一個容器。

**叢集**：以單一虛擬 Docker 主機形式公開的 Docker 主機集合，讓應用程式可以擴充為分散到叢集內多部主機的多個服務執行個體。 您可以使用 Kubernetes、Azure Service Fabric、Docker Swarm 和 Mesosphere DC/OS 來建立 Docker 叢集。

**Orchestrator**：可簡化叢集和 Docker 主機管理的工具。 協調器可讓您透過命令列介面 (CLI) 或圖形化 UI 來管理其映像、容器和主機。 您可以管理容器網路功能、組態、負載平衡、服務探索、高可用性、Docker 主機組態等等。 協調器會負責跨節點集合執行、散發、擴充及修復工作負載。 一般而言，協調器產品與提供叢集基礎結構的產品相同，例如在市場中其他供應項目之間的 Kubernetes 和 Azure Service Fabric。

>[!div class="step-by-step"]
>[上一個](what-is-docker.md) 
>[下一步](docker-containers-images-and-registries.md)
