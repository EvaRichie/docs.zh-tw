---
title: Docker 應用程式的開發工作流程
description: 了解開發 Docker 應用程式的工作流程詳細資料。 一開始會逐步了解一些用以最佳化 Dockerfile 的詳細資料，最後將取得使用 Visual Studio 時可用的簡化工作流程。
ms.date: 01/30/2020
ms.openlocfilehash: d32134a10fb9b56e874bbc6218ca2c4d822adb90
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2020
ms.locfileid: "90678845"
---
# <a name="development-workflow-for-docker-apps"></a>Docker 應用程式的開發工作流程

應用程式開發生命週期開始於您以開發人員身分使用的電腦，您會在電腦上使用慣用語言來撰寫應用程式的程式碼，並於本機上測試。 使用此工作流程，不論您選擇哪一種語言、架構和平台，一定能開發和測試 Docker 容器，但只能在本機作業。

每個容器 (Docker 映像的執行個體) 包含下列元件：

- 作業系統選取項目，例如 Linux 發行版本、Windows Nano Server 或 Windows Server Core。

- 開發期間新增的檔案，例如原始程式碼和應用程式二進位檔。

- 組態資訊，例如環境設定和相依性。

## <a name="workflow-for-developing-docker-container-based-applications"></a>開發 Docker 容器型應用程式的工作流程

本節描述 Docker 容器型應用程式的「內部迴圈」** 開發工作流程。 內部迴圈工作流程表示不考慮更廣泛的 DevOps 工作流程，其最多可包含生產環境部署，而只著重于在開發人員電腦上完成的開發工作。 設定環境的初始步驟不包含在內，因為這些步驟只執行一次。

應用程式是由您自己的服務加上額外的程式庫 (相依性) 所組成。 以下是組建 Docker 應用程式時通常會採用的基本步驟，如圖 5-1 所示。

:::image type="complex" source="./media/docker-app-development-workflow/life-cycle-containerized-apps-docker-cli.png" alt-text="此圖顯示建立容器化應用程式所需的7個步驟。":::
Docker 應用程式的開發程式： 1-撰寫應用程式的程式碼、2寫入 Dockerfile/秒、3-建立在 Dockerfile/s 定義的映射、4- (選擇性) 在 >docker-compose.yml yml 檔案中撰寫服務、5-執行容器或 Docker 撰寫應用程式、6-測試您的應用程式或微服務、7-推送至存放庫並重複執行。
:::image-end:::

**圖5-1。** 開發 Docker 容器化應用程式的逐步工作流程

本節會詳細說明這整個程序，並針對 Visual Studio 環境說明每個主要步驟。

當您使用編輯器/CLI 開發方法 (例如 Visual Studio Code 加上 macOS 或 Windows 上的 Docker CLI) 時，您需要知道每一個步驟，通常要比使用 Visual Studio 更詳細。 如需在 CLI 環境中操作的詳細資訊，請參閱電子書 [Containerized Docker Application lifecycle with Microsoft Platforms and Tools](https://aka.ms/dockerlifecycleebook/)。

當您使用 Visual Studio 2019 時，系統會為您處理其中許多步驟，進而大幅提升您的生產力。 當您使用 Visual Studio 2019 並以多容器應用程式為目標時，更是如此。 例如，只需要按一下滑鼠，Visual Studio 就會將和檔案新增 `Dockerfile` `docker-compose.yml` 至您的專案，並包含應用程式的設定。 當您在 Visual Studio 中執行應用程式時，它會組建 Docker 映像並直接在 Docker 中執行多容器應用程式，甚至可讓您立即偵錯數個容器。 這些功能可大幅提高開發速度。

不過，Visual Studio 自動化這些步驟並不表示您不需要知道 Docker 在做什麼。 因此，下列指引將詳細說明每一個步驟。

![步驟1的影像。](./media/docker-app-development-workflow/step-1-code-your-app.png)

## <a name="step-1-start-coding-and-create-your-initial-application-or-service-baseline"></a>步驟 1： 開始撰寫程式碼，並建立您的初始應用程式或服務比較基準

開發 Docker 應用程式類似於不使用 Docker 開發應用程式的方式。 差別在於，開發 Docker 時，您要在本機環境中部署並測試 Docker 容器內執行的應用程式或服務 (可能是 Docker 的 Linux VM 安裝程式，若使用 Windows 容器則直接使用 Windows)。

### <a name="set-up-your-local-environment-with-visual-studio"></a>設定使用 Visual Studio 的本機環境

開始前，請確定您已安裝 [Docker Community Edition (CE)](https://docs.docker.com/docker-for-windows/) for Windows，如下列指示所述：

[Get started with Docker CE for Windows (開始使用適用於 Windows 的 Docker CE)](https://docs.docker.com/docker-for-windows/)

此外，您需要已安裝 **.Net Core 跨平臺開發** 工作負載的 Visual Studio 2019 16.4 版或更新版本，如圖5-2 所示。

![.NET Core 跨平臺開發選取範圍的螢幕擷取畫面。](./media/docker-app-development-workflow/dotnet-core-cross-platform-development.png)

**圖 5-2**。 在 Visual Studio 2019 安裝期間選取 **.Net Core 跨平臺開發** 工作負載

您甚至可以在於您的應用程式中啟用 Docker，並在 Docker 中部署與測試之前，只使用 .NET 開始撰寫應用程式的程式碼 (如果您打算使用容器通常會使用 .NET Core)。 不過，建議您盡快開始使用 Docker，因為它會成為實際環境，可以盡快發現任何問題。 我們鼓勵您這麼做，是因為 Visual Studio 和 Docker 合作很容易，您幾乎感覺不到它，最佳範例是從 Visual Studio 偵錯多容器應用程式時。

### <a name="additional-resources"></a>其他資源

- **開始使用適用於 Windows 的 Docker CE** \
  <https://docs.docker.com/docker-for-windows/>

- **Visual Studio 2019** \
  [https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)

![步驟2的影像。](./media/docker-app-development-workflow/step-2-write-dockerfile.png)

## <a name="step-2-create-a-dockerfile-related-to-an-existing-net-base-image"></a>步驟 2： 建立與現有 .NET 基底映像有關的 Dockerfile

每個您想要組建的自訂映像都需要 Dockerfile，每個要部署的容器也需要 Dockerfile，無論您是從 Visual Studio 自動部署或使用 Docker CLI (docker run 和 docker-compose 命令) 手動部署。 如果您的應用程式包含單一的自訂服務，您需要單一的 Dockerfile。 如果您的應用程式包含多項服務 (如微服務架構)，每項服務都需要一個 Dockerfile。

Dockerfile 放在您應用程式或服務的根資料夾中。 它包含告訴 Docker 如何設定及執行容器中應用程式或服務的命令。 您可以使用程式碼手動建立 Dockerfile，將它與您的 .NET 相依性一起新增至您的專案。

使用 Visual Studio 及其適用於 Docker 的工具，這項工作只需要按幾下滑鼠即可。 當您在 Visual Studio 2019 中建立新專案時，有一個名為 [ **啟用 Docker 支援**] 的選項，如 [圖 5-3] 所示。

![顯示 [啟用 Docker 支援] 核取方塊的螢幕擷取畫面。](./media/docker-app-development-workflow/enable-docker-support-check-box.png)

**圖 5-3**。 在 Visual Studio 2019 中建立新的 ASP.NET Core 專案時啟用 Docker 支援

您也可以在**方案總管**的專案上按一下滑鼠右鍵，然後選取 [**新增**Docker 支援]，在現有的 ASP.NET Core web 應用程式專案上啟用 Docker 支援  >  ** **，如圖5-4 所示。

![顯示 [新增] 功能表中 [Docker 支援] 選項的螢幕擷取畫面。](./media/docker-app-development-workflow/add-docker-support-option.png)

**圖 5-4**。 在現有的 Visual Studio 2019 專案中啟用 Docker 支援

這個動作會將具有所需組態的 *Dockerfile* 新增至專案，且只能在 ASP.NET Core 專案上使用。

同樣地，Visual Studio 也可以 `docker-compose.yml` 使用 [ **新增 > 容器協調器支援 ...**] 選項新增整個方案的檔案。在步驟4中，我們將更詳細地探索這個選項。

### <a name="using-an-existing-official-net-docker-image"></a>使用現有的官方 .NET Docker 映像

您通常會在基底映像的基礎上，為您的容器建置自訂映像，此基底映像可從 [Docker Hub](https://hub.docker.com/) 登錄等官方存放庫取得。 這就是當您在 Visual Studio 中啟用 Docker 支援時，實際發生的狀況。 您的 Dockerfile 會使用現有 `dotnet/core/aspnet` 映像。

前文曾說明您可以使用的 Docker 映像和存放庫，視您選擇的架構和作業系統而定。 例如，如果您想要使用 ASP.NET Core (Linux 或 Windows)，則要使用的映像就是 `mcr.microsoft.com/dotnet/core/aspnet:3.1`。 因此，您只需要指定要為容器使用的基底 Docker 映像。 將 `FROM mcr.microsoft.com/dotnet/core/aspnet:3.1` 新增至您的 Dockerfile 即可完成此作業。 Visual Studio 會自動執行此作業，但如打算更新版本，則要更新此值。

使用 Docker Hub 中有版本號碼的官方 .NET 映像存放庫，可確保所有電腦上都能使用相同的語言功能 (包括開發、測試和生產環境)。

下例示範 ASP.NET Core 容器的範例 Dockerfile。

```dockerfile
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
ARG source
WORKDIR /app
EXPOSE 80
COPY ${source:-obj/Docker/publish} .
ENTRYPOINT ["dotnet", " MySingleContainerWebApp.dll "]
```

在此情況下，映射是以正式 ASP.NET Core Docker 映射的3.1 版為基礎， (多架構的 Linux 和 Windows) 。 這是 `FROM mcr.microsoft.com/dotnet/core/aspnet:3.1` 設定。  (如需此基底映射的詳細資訊，請參閱 [.Net Core Docker 映射](https://hub.docker.com/_/microsoft-dotnet-core/) 頁面。在 Dockerfile 中 ) ，您也必須指示 Docker 接聽您將在執行時間使用的 TCP 埠 (在此案例中為埠80，如同使用公開設定) 所設定的埠。

您可在 Dockerfile 中指定其他的組態設定，視您使用的語言和架構而定。 例如，ENTRYPOINT 行中有 `["dotnet", "MySingleContainerWebApp.dll"]` 會指示 Docker 執行 .NET Core 應用程式。 如果您使用 SDK 和 .NET Core CLI (dotnet CLI) 建置及執行 .NET 應用程式，此設定會有所不同。 重點是 ENTRYPOINT 行與其他設定會不一樣，視您選擇的應用程式語言和平台而定。

### <a name="additional-resources"></a>其他資源

- **建立適用于 .NET Core 應用程式的 Docker 映射** \
  [https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](/aspnet/core/host-and-deploy/docker/building-net-docker-images)

- **組建您自己的映像**. 在官方 Docker 文件中。\
  <https://docs.docker.com/engine/tutorials/dockerimages/>

- **使用 .NET 容器映射保持最新狀態** \
  <https://devblogs.microsoft.com/dotnet/staying-up-to-date-with-net-container-images/>

- **使用 .NET 和 Docker 搭配使用-DockerCon 2018 更新** \
  <https://devblogs.microsoft.com/dotnet/using-net-and-docker-together-dockercon-2018-update/>

### <a name="using-multi-arch-image-repositories"></a>使用多架構映像存放庫

一個存放庫可以包含多種平台變化，例如 Linux 映像和 Windows 映像。 這項功能可讓像 Microsoft (基底映像建立者) 這樣的廠商建立單一存放庫以涵蓋多個平台 (即 Linux 和 Windows)。 例如，Docker Hub 登錄提供的 [dotnet/core](https://hub.docker.com/_/microsoft-dotnet-core/)存放庫，會使用相同的存放庫名稱提供 Linux 和 Windows Nano Server 支援。

如果您指定標籤，如下列案例一樣明確鎖定平台：

- `mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim` \
  目標：僅適用于 Linux 上的 .NET Core 3.1 執行時間

- `mcr.microsoft.com/dotnet/core/aspnet:3.1-nanoserver-1909` \
  目標： Windows Nano Server 上的僅限 .NET Core 3.1 執行時間

但如果您指定相同的映像名稱，甚至是使用相同的標籤，多架構映像 (例如 `aspnet` 映像) 將會根據您目前部署的 Docker 主機 OS 使用 Linux 或 Windows 版本，如下列範例所示：

- `mcr.microsoft.com/dotnet/core/aspnet:3.1` \
  多架構：僅適用于 Linux 或 Windows Nano Server 上的 .NET Core 3.1 執行時間，視 Docker 主機 OS 而定

如此一來，當您從 Windows 主機提取映像時，它會提取 Windows variant，而從 Linux 主機提取相同的映像名稱則會提取 Linux variant。

### <a name="multi-stage-builds-in-dockerfile"></a>Dockerfile 中的多階段建置

Dockerfile 類似於批次指令碼。 類似於必須從命令列設定電腦時所要執行的作業。

它會從設定初始內容的基底映像開始，就像是啟動檔案系統，都是位於主機 OS 之上。 這並不是作業系統，但您可以將它視為容器內的「作業系統」。

執行每個命令列都會在檔案系統上建立新的圖層，其中包含對上一個圖層所做的變更，這些圖層合併之後即會產生檔案系統。

由於每個新圖層都會「置於」上一個圖層之上，且產生的映像大小會隨著每個命令而增加，因此如果必須包含建置和發佈應用程式所需的 SDK 時，映像可能會變得非常大。

此時請考慮多階段建置 (從 Docker 17.05 和更高版本)，以發揮其功效。

其核心概念是，您可以將 Dockerfile 執行程序分成不同階段，其中一個階段是一個初始映像後面接著一或多個命令，而最後一個階段會決定最終映像大小。

簡單來說，多階段建置允許將建立作業分割成不同的「階段」，再組合最終映像，只從中間階段擷取相關目錄。 這項功能的一般使用方式如下：

1. 使用基底 SDK 映像 (大小並不重要)，其中包含建置和發佈應用程式至資料夾所需的所有項目，然後

2. 使用僅限執行階段的小型基底映像，並複製上一個階段中的發佈資料夾，以產生一個小型最終映像。

透過逐行詳細檢閱 Dockerfile 或許是了解多階段的最佳方式，就讓我們將從新增專案的 Docker 支援時由 Visual Studio 建立的初始 Dockerfile 開始，稍後再探討一些最佳化。

初始 Dockerfile 看起來可能像這樣：

```dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
 6  WORKDIR /src
 7  COPY src/Services/Catalog/Catalog.API/Catalog.API.csproj …
 8  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.AspNetCore.HealthChecks …
 9  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions.HealthChecks …
10  COPY src/BuildingBlocks/EventBus/IntegrationEventLogEF/ …
11  COPY src/BuildingBlocks/EventBus/EventBus/EventBus.csproj …
12  COPY src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.csproj …
13  COPY src/BuildingBlocks/EventBus/EventBusServiceBus/EventBusServiceBus.csproj …
14  COPY src/BuildingBlocks/WebHostCustomization/WebHost.Customization …
15  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
16  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
17  RUN dotnet restore src/Services/Catalog/Catalog.API/Catalog.API.csproj
18  COPY . .
19  WORKDIR /src/src/Services/Catalog/Catalog.API
20  RUN dotnet build Catalog.API.csproj -c Release -o /app
21
22  FROM build AS publish
23  RUN dotnet publish Catalog.API.csproj -c Release -o /app
24
25  FROM base AS final
26  WORKDIR /app
27  COPY --from=publish /app .
28  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

以下逐行詳細說明：

- **行 #1：** 使用「小型」僅限執行時間的基底映射來開始階段，並以參考的方式呼叫它的 **基底** 。

- **行 #2：** 在映射中建立 **/app** 目錄。

- **行 #3：** 公開端口 **80**。

- **行 #5：** 開始具有「大型」映射的新階段來建立/發佈。 呼叫它的 **組建** 以供參考。

- **行 #6：** 在映射中建立目錄 **/src** 。

- **行 #7：** 最多行16，複製參考 **的 .csproj** 專案檔，以便稍後可以還原封裝。

- **行 #17：** 還原 **類別目錄的套件。 API** 專案和參考的專案。

- **行 #18：** 將 **解決方案的所有目錄樹狀結構** (除了 **>.dockerignore** 檔案中包含的檔案/目錄) 至映射中的 **/src** 目錄。

- **行 #19：** 將目前的資料夾變更為 **Catalog. API** 專案。

- **行 #20：** 建立專案 (和其他專案相依性) 並輸出至影像中的 **/app** 目錄。

- **行 #22：** 開始新的階段，從組建繼續進行。 請呼叫它來 **發行** 以供參考。

- **行 #23：** 將專案 (和相依性) 和輸出發行至映射中的 **/app** 目錄。

- **行 #25：** 從 **基底** 開始新的階段，並將它稱為 **最終**。

- **行 #26：** 將目前目錄變更為 **/app**。

- **行 #27：** 從階段**發佈**將 **/app**目錄複寫到目前的目錄。

- **行 #28：** 定義要在容器啟動時執行的命令。

現在讓我們來探索一些可改善整體程序效能的最佳化，以 eShopOnContainers 為例，則表示在 Linux 容器中建置完整方案需要約 22 分鐘或更多的時間。

您將利用 Docker 的圖層快取功能，這項功能相當簡單：如果基底映像和命令與先前執行的某些項目相同，則可以直接使用產生的圖層，而不需要執行命令，因此節省一些時間。

讓我們將重點放在**建置**階段，第 5-6 行大致相同，但第 7-17 行會因 eShopOnContainers 中的每個服務而異，因此每次都必須執行，不過如果您將第 7-16 行變更為：

```dockerfile
COPY . .
```

則每個服務都會相同，它會複製整個方案並建立較大的圖層，但：

1. 複製程序只會在第一次執行 (以及因檔案變更而重建時執行)，並針對所有其他服務使用快取

2. 由於較大的影像會在中繼階段中發生，因此不會影響最終的影像大小。

下一個重要的最佳化涉及第 17 行所執行的 `restore` 命令，這也會因 eShopOnContainers 的每個服務而異。 如果您將該行變更為：

```dockerfile
RUN dotnet restore
```

它會還原整個方案的套件，但同樣地，它只會執行一次，而不是目前策略的 15 次。

不過，資料夾中必須只有單一專案或方案檔，`dotnet restore` 才會執行，因此達成此目的會比較複雜，而解決的方式 (不細究) 如下：

1. 將下列各行新增至 **.dockerignore**：

   - `*.sln`，以忽略主要資料夾樹狀目錄中的所有方案檔

   - `!eShopOnContainers-ServicesAndWebApps.sln`，只包含此方案檔。

2. 將 `/ignoreprojectextensions:.dcproj` 引數加入 `dotnet restore`，讓它也可忽略 docker-compose 專案，並只還原 eShopOnContainers-ServicesAndWebApps 方案的套件。

在最後一個最佳化中，第 20 行剛好是多餘的，因為第 23 行也會建置應用程式且基本上緊接在第 20 行後面，所以是另一個耗時的命令。

產生的檔案如下：

```dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS publish
 6  WORKDIR /src
 7  COPY . .
 8  RUN dotnet restore /ignoreprojectextensions:.dcproj
 9  WORKDIR /src/src/Services/Catalog/Catalog.API
10  RUN dotnet publish Catalog.API.csproj -c Release -o /app
11
12  FROM base AS final
13  WORKDIR /app
14  COPY --from=publish /app
15  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

### <a name="creating-your-base-image-from-scratch"></a>建立全新的基底映像

您可以從頭開始建立您自己的 Docker 基底映像。 Docker 新手不建議此方案，但如果您想要設定專屬基底映像的特點，您可以這樣做。

### <a name="additional-resources"></a>其他資源

- **多架構 .Net Core 映射**。
  <https://github.com/dotnet/announcements/issues/14>

- **建立基底映像**。 官方 Docker 文件。\
  <https://docs.docker.com/develop/develop-images/baseimages/>

![步驟3的影像。](./media/docker-app-development-workflow/step-3-create-dockerfile-defined-images.png)

## <a name="step-3-create-your-custom-docker-images-and-embed-your-application-or-service-in-them"></a>步驟 3： 建立您的自訂 Docker 映像並在其中內嵌您的應用程式或服務

您需要為應用程式中的每項服務建立相關的映像。 如果您的應用程式組成為單一的服務或 Web 應用程式，您只需要單一映像。

請注意，Visual Studio 會自動為您建立 Docker 映像。 只有編輯器/CLI 工作流程需要下列步驟，我們會清楚說明發生的狀況。

您身為開發人員，需要在本機上開發和測試，直到完成原始檔控制系統 (例如 GitHub) 的完整功能或變更。 這表示，您需要建立 Docker 映像，將容器部署到本機的 Docker 主機 (Windows 或 Linux VM) 並執行、測試及偵錯這些本機容器。

若要使用 Docker CLI 和您的 Dockerfile 在本機環境中建立自訂映像，您可以使用 docker build 命令，如圖 5-5 所示。

![顯示 docker build 命令之主控台輸出的螢幕擷取畫面。](./media/docker-app-development-workflow/run-docker-build-command.png)

**圖 5-5**。 建立自訂的 Docker 映像

除了直接從專案資料夾執行 docker build 以外，您可以選擇執行 `dotnet publish`，這樣就能使用所需的 .NET 程式庫及二進位先產生可部署的資料夾，再使用 `docker build` 命令。

這會建立一個名為 `cesardl/netcore-webapi-microservice-docker:first` 的 Docker 映像。 本例中的 :first 是代表特定版本的標籤。 您可以為組成 Docker 應用程式所需建立的每個自訂映像重複此步驟。

當應用程式是由多個容器組成時 (即多容器應用程式)，您也可以使用 `docker-compose up --build` 命令，使用相關 docker-compose.yml 檔案公開的中繼資料，以單一命令建置所有相關映像。

您可以使用 docker images 命令在本機存放庫中尋找現有的映像，如圖 5-6 所示。

![docker images 命令的主控台輸出，顯示現有的映像。](./media/docker-app-development-workflow/view-existing-images-with-docker-images.png)

**圖5-6。** 使用 docker images 命令檢視現有的映像

### <a name="creating-docker-images-with-visual-studio"></a>使用 Visual Studio 建立 Docker 映像

當您使用 Visual Studio 建立具有 Docker 支援的專案時，不用明確地建立映像。 反之，當您按 **F5** (或 **Ctrl-F5**) 執行 Docker 化的應用程式或服務時，就會為您建立映像。 雖然這個步驟會在 Visual Studio 中自動執行，而不會在您眼前發生，但知道背後情況也相當重要。

![選用步驟4的影像。](./media/docker-app-development-workflow/step-4-define-services-docker-compose-yml.png)

## <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application"></a>步驟 4： 組建多容器 Docker 應用程式時，在 docker-compose.yml 中定義您的服務

[Docker compose.yml](https://docs.docker.com/compose/compose-file/) 檔案可讓您定義一組相關服務，部署為具有部署命令的組成應用程式。 它也會設定其相依性關聯和執行階段組態。

若要使用 docker-compose.yml 檔案，您需要使用與下列範例類似的內容，在您的 Main 或根解決方案資料夾中建立檔案：

```yml
version: '3.4'

services:

  webmvc:
    image: eshop/web
    environment:
      - CatalogUrl=http://catalog-api
      - OrderingUrl=http://ordering-api
    ports:
      - "80:80"
    depends_on:
      - catalog-api
      - ordering-api

  catalog-api:
    image: eshop/catalog-api
    environment:
      - ConnectionString=Server=sqldata;Port=1433;Database=CatalogDB;…
    ports:
      - "81:80"
    depends_on:
      - sqldata

  ordering-api:
    image: eshop/ordering-api
    environment:
      - ConnectionString=Server=sqldata;Database=OrderingDb;…
    ports:
      - "82:80"
    extra_hosts:
      - "CESARDLBOOKVHD:10.0.75.1"
    depends_on:
      - sqldata

  sqldata:
    image: mcr.microsoft.com/mssql/server:latest
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
```

此 docker-compose.yml 檔案為簡化的合併版本。 它包含每個容器的靜態組態資料 (例如自訂映像的名稱)，這一律是必要的，可能相依於部署環境的組態資訊，例如連接字串。 在稍後各節中，您會了解如何根據環境和執行類型 (偵錯或發行)，將 docker-compose.yml 組態分割成多個 docker-compose 檔案和覆寫值。

docker-compose.yml 檔案範例會定義四項服務：`webmvc` 服務 (Web 應用程式)、兩項微服務 (`ordering-api` 和 `basket-api`)，以及 `sqldata`，一個以 SQL Server for Linux 為基礎執行為容器的資料來源容器。 每項服務都會部署為容器，因此每個都需要 Docker 映像。

docker-compose.yml 檔案指定的不只是使用何種容器，還會指定它們個別設定的方式。 例如，.yml 檔案中的 `webmvc` 容器定義：

- 使用預先建置的 `eshop/web:latest` 映像。 不過，您也可以設定映像，讓它組建為 docker-compose 的一部分，附帶以 docker-compose 檔案 build: 區段為基礎的額外組態。

- 初始化兩個環境變數 (CatalogUrl 和 OrderingUrl)。

- 將容器上公開的通訊埠 80 轉送至主機的外部通訊埠 80。

- 使用 depends_on 設定連結 Web 應用程式與目錄和訂購服務。 這會導致服務一直等候到這些服務啟動。

當我們討論到如何實作微服務和多容器應用程式時，會在後節重新審視 docker-compose.yml 檔案。

### <a name="working-with-docker-composeyml-in-visual-studio-2019"></a>使用 Visual Studio 2019 中的 >docker-compose.yml. yml

除了將 Dockerfile 新增至專案（如先前所述），) 上的15.8 版 Visual Studio 2017 (可將 Docker Compose 的協調器支援新增至解決方案。

當您第一次新增容器協調器支援時 (如圖 5-7 所示)，Visual Studio 會為專案建立 Dockerfile，並在包含數個全域 `docker-compose*.yml` 檔案的方案中建立新的 (服務區段) 專案，然後將專案新增至這些檔案。 然後您可以開啟 docker-compose.yml 檔案，更新它們增加其他功能。

您必須從要包含在 docker-compose.yml 檔案中的每個專案重複此作業。

在撰寫本文時，Visual Studio 支援 **Docker Compose** 和 **Kubernetes/Helm** 協調器。

![顯示專案操作功能表中 [容器協調器支援] 選項的螢幕擷取畫面。](./media/docker-app-development-workflow/add-container-orchestrator-support-option.png)

**圖 5-7**。 以滑鼠右鍵按一下 ASP.NET Core 專案以在 Visual Studio 2019 中新增 Docker 支援

在您將協調器支援新增至您的 Visual Studio 方案之後，您也會在 [方案總管] 中看到包含已新增 docker-compose.yml 檔案的新節點 (在 `docker-compose.dcproj` 專案檔中)，如圖 5-8 所示。

![方案總管中的 docker 撰寫節點的螢幕擷取畫面。](./media/docker-app-development-workflow/docker-compose-tree-node.png)

**圖 5-8**。 在 Visual Studio 2019 中新增的 **docker 組成** 樹狀結構節點方案總管

您可以透過 `docker-compose up` 命令來使用單一 docker-compose.yml 檔案部署多容器應用程式。 不過，Visual Studio 會新增它們的群組，方便您根據環境 (開發或生產) 和執行類型 (發行或偵錯) 來覆寫值。 這項功能會在後列各節中說明。

![步驟5的影像。](./media/docker-app-development-workflow/step-5-run-containers-compose-app.png)

## <a name="step-5-build-and-run-your-docker-application"></a>步驟 5。 組建並執行您的 Docker 應用程式

如果您的應用程式只有單一容器，您可以將它部署至您的 Docker 主機 (VM 或實體伺服器) 來執行。 但是，如果您的應用程式包含多項服務，您可以使用單一 CLI 命令 (`docker-compose up)` 或 Visual Studio （將在幕後使用該命令），將其部署為組成的應用程式。 讓我們看看不同的選項。

### <a name="option-a-running-a-single-container-application"></a>選項 A：執行單一容器應用程式

#### <a name="using-docker-cli"></a>使用 Docker CLI

您可以使用 `docker run` 命令來執行 Docker 容器，如圖 5-9 所示：

```console
docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

上述命令會在每次執行時，從指定的映像建立新的容器執行個體。 您可以使用 `--name` 參數來提供容器的名稱，然後使用 `docker start {name}` (或使用容器識別碼或自動名稱) 來執行現有的容器實例。

![使用 docker run 命令執行 Docker 容器的螢幕擷取畫面。](./media/docker-app-development-workflow/use-docker-run-command.png)

**圖 5-9**。 使用 docker run 命令執行 Docker 容器

在本列中，命令會將容器的內部通訊埠 5000 繫結到主機電腦的通訊埠 80。 這表示主機會接聽通訊埠 80 並轉送至容器的通訊埠 5000。

顯示的雜湊是容器識別碼，如果未使用此選項，也會將它指派為隨機可讀取的名稱 `--name` 。

#### <a name="using-visual-studio"></a>使用 Visual Studio

如果您尚未新增容器協調器支援，您也可以按 **Ctrl-F5** 在 Visual Studio 中執行單一容器應用程式；此外，您也可以使用 **F5** 對容器內的應用程式偵錯。 容器使用 docker run 於本機上執行。

### <a name="option-b-running-a-multi-container-application"></a>選項 B：執行多容器應用程式

在大部分的企業案例中，Docker 應用程式會由多項服務組成，這表示您需要執行多容器應用程式，如圖 5-10 所示。

![具有數個 Docker 容器的 VM](./media/docker-app-development-workflow/vm-with-docker-containers-deployed.png)

**圖 5-10**。 部署了 Docker 容器的 VM

#### <a name="using-docker-cli"></a>使用 Docker CLI

若要使用 Docker CLI 執行多容器應用程式，請使用 `docker-compose up` 命令。 此命令會使用您在解決方案層級的 **>docker-compose.yml yml** 檔案來部署多容器應用程式。 圖 5-11 顯示從您主要方案目錄執行命令的結果，這會包含 docker-compose.yml 檔案。

![執行 docker-compose up 命令時的畫面檢視](./media/docker-app-development-workflow/results-docker-compose-up.png)

**圖 5-11**。 執行的 docker-compose up 命令的範例結果

在執行 docker-compose up 命令後，應用程式及其相關容器便已部署至您的 Docker 主機，如圖 5-10 所示。

#### <a name="using-visual-studio"></a>使用 Visual Studio

使用 Visual Studio 2019 執行多容器應用程式時，將無法取得任何更簡單的程式。 您可以像往常一樣按 **Ctrl-F5** 執行，或按 **F5** 偵錯，並將 **docker-compose** 專案設定為啟始專案。  Visual Studio 會處理所有必要的設定，因此您可以像平常一樣建立中斷點，並在偵錯工具已附加的情況下，以已附加偵錯工具的方式來處理最後成為獨立進程的程式，就像這樣。

如前所述，每次您將 Docker 解決方案支援新增至解決方案內的專案，就會在全域 (解決方案層級) docker-compose.yml 檔案中設定該專案，這可讓您立即執行或偵錯整個解決方案。 Visual Studio 會為每個啟用 Docker 解決方案支援的專案啟動一個容器，並為您執行所有內部步驟 (dotnet publish、docker build 等等)。

如果想要查看所有繁瑣的工作，請參閱下列檔案：

`{root solution folder}\obj\Docker\docker-compose.vs.debug.g.yml`

這裡的重點是，如圖5-12 所示，在 Visual Studio 2019 中，有一個適用于 F5 按鍵動作的額外 **Docker** 命令。 此選項藉由執行在解決方案層級之 docker-compose.yml 檔案中定義的所有容器，讓您執行或偵錯多容器應用程式。 偵錯多容器解決方案的能力，表示您可以設定多個中斷點，不同的專案 (容器) 各一個中斷點；而從 Visual Studio 偵錯時，您會停在不同專案中定義的中斷點，然後在不同的容器上執行。

![執行 docker 撰寫專案的 debug 工具列螢幕擷取畫面。](./media/docker-app-development-workflow/debug-toolbar-docker-compose-project.png)

**圖 5-12**。 在 Visual Studio 2019 中執行多容器應用程式

### <a name="additional-resources"></a>其他資源

- **將 ASP.NET 容器部署到遠端 Docker 主機** \
  <https://docs.microsoft.com/visualstudio/containers/hosting-web-apps-in-docker>

### <a name="a-note-about-testing-and-deploying-with-orchestrators"></a>測試與部署協調器的注意事項

docker-compose up 和 docker run 命令 (在 Visual Studio 中執行和偵錯容器) 適合在開發環境中測試容器。 但您不應該針對生產環境部署使用這種方法，在此部署中，您應該以 [Kubernetes](https://kubernetes.io/) 或 [Service Fabric](https://azure.microsoft.com/services/service-fabric/) 等協調器為目標。 如果您使用的是 Kubernetes，則必須使用 pod 來組織容器和[服務](https://kubernetes.io/docs/concepts/services-networking/service/) [，以進行](https://kubernetes.io/docs/concepts/workloads/pods/pod/)網路。 您也必須使用[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)來組織 Pod 建立和修改作業。

![步驟6的影像。](./media/docker-app-development-workflow/step-6-test-app-microservices.png)

## <a name="step-6-test-your-docker-application-using-your-local-docker-host"></a>步驟 6. 使用本機的 Docker 主機測試您的 Docker 應用程式

此步驟會隨應用程式執行的作業而異。 在部署為單一容器或服務的簡單 .NET Core Web 應用程式中，您可以藉由在 Docker 主機上開啟瀏覽器並瀏覽至該網站來存取服務，如圖 5-13 所示。 (如果 Dockerfile 中的組態對應至主機通訊埠 80 以外的容器，包括 URL 中的主機連接埠。)

![Localhost/API/值回應的螢幕擷取畫面。](./media/docker-app-development-workflow/test-docker-app-locally-localhost.png)

**圖 5-13**。 使用 localhost 在本機測試 Docker 應用程式的範例

如果 localhost 未指向 Docker 主機 IP (根據預設，當使用 Docker CE 時應該會指向 Docker 主機 IP)，請使用您電腦網路卡的 IP 位址來巡覽至您的服務。

請注意，瀏覽器中這個 URL 為討論中的特定容器範例使用的是通訊埠 80。 不過，要求在內部會重新導向至通訊埠 5000，因為它是以 docker run 命令如此部署的，如上一個步驟中所述。

您也可以從終端機使用 curl 測試應用程式，如圖 5-14 所示。 在 Windows 的 Docker 安裝中，在您電腦的實際 IP 位址以外，預設的 Docker 主機 IP 一律為 10.0.75.1。

![從取得捲曲的主控台輸出 http://10.0.75.1/API/values 。](./media/docker-app-development-workflow/test-docker-app-locally-curl.png)

**圖 5-14**。 使用 curl 在本機測試 Docker 應用程式的範例

### <a name="testing-and-debugging-containers-with-visual-studio-2019"></a>使用 Visual Studio 2019 測試和偵測容器

使用 Visual Studio 2019 來執行和偵錯工具時，您可以像在不使用容器執行時一樣，以相同的方式來進行 .NET 應用程式的偵錯工具。

### <a name="testing-and-debugging-without-visual-studio"></a>不使用 Visual Studio 偵錯和測試

如果您是使用編輯器/CLI 方法進行開發，則偵錯工具會比較困難，而且您可能會想要藉由產生追蹤來進行 debug。

### <a name="additional-resources"></a>其他資源

- **在本機 Docker 容器中對應用程式進行偵錯工具** \
  [https://docs.microsoft.com/visualstudio/containers/edit-and-refresh](/visualstudio/containers/edit-and-refresh)

- **Steve Lasker。使用 Docker 建立、偵測、部署 ASP.NET Core 應用程式。** 影片。 \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T115>

## <a name="simplified-workflow-when-developing-containers-with-visual-studio"></a>使用 Visual Studio 開發容器時的簡化工作流程

實際上，使用 Visual Studio 時的工作流程時遠比您使用編輯器/CLI 方法更簡單。 Visual Studio 會隱藏或簡化與 Dockerfile 和 docker-compose.yml 檔案有關，為 Docker 所需的大部分步驟，如圖 5-15 所示。

:::image type="complex" source="./media/docker-app-development-workflow/simplified-life-cycle-containerized-apps-docker-cli.png" alt-text="顯示建立應用程式所需的五個簡化步驟的圖表。":::
Docker 應用程式的開發程式： 1-撰寫應用程式的程式碼、2寫入 Dockerfile/秒、3-建立在 Dockerfile/s 定義的映射、4- (選擇性) 在 >docker-compose.yml yml 檔案中撰寫服務、5-執行容器或 Docker 撰寫應用程式、6-測試您的應用程式或微服務、7-推送至存放庫並重複執行。
:::image-end:::

**圖 5-15**。 使用 Visual Studio 開發時的簡化工作流程

此外，您只需要執行一次步驟 2 (將 Docker 支援新增至您的專案)。 因此，工作流程類似於您使用 .NET 處理任何其他開發時的一般開發工作。 您需要知道實際狀況 (映像建置程序、使用哪些基底映像、容器部署等等)，有時也需要編輯 Dockerfile 或 docker-compose.yml 檔案以自訂行為。 但使用 Visual Studio 已大幅簡化工作，提高您的產能。

### <a name="additional-resources"></a>其他資源

- **Steve Lasker。使用 Visual Studio (2017) 進行 .NET Docker 開發 ** \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T111>

## <a name="using-powershell-commands-in-a-dockerfile-to-set-up-windows-containers"></a>在 DockerFile 中使用 PowerShell 命令來設定 Windows 容器

[Windows 容器](https://docs.microsoft.com/virtualization/windowscontainers/about/index)可讓您將現有的 Windows 應用程式轉換成 Docker 映像，並使用相同的工具將它們部署為 Docker 生態系統的其他部分。 您要在 Dockerfile 中執行 PowerShell 命令才能使用 Windows 容器，如下列範例所示：

```dockerfile
FROM mcr.microsoft.com/windows/servercore
LABEL Description="IIS" Vendor="Microsoft" Version="10"
RUN powershell -Command Add-WindowsFeature Web-Server
CMD [ "ping", "localhost", "-t" ]
```

在本例中，我們使用 Windows Server Core 基底映像 (FROM 設定)，並使用 PowerShell 命令 (RUN 設定) 安裝 IIS。 使用類似的方式，您也可以使用 PowerShell 命令安裝其他元件，例如 ASP.NET 4.x、.NET 4.6 或任何其他 Windows 軟體。 例如，Dockerfile 中的下列命令會安裝 ASP.NET 4.5：

```dockerfile
RUN powershell add-windowsfeature web-asp-net45
```

### <a name="additional-resources"></a>其他資源

- **aspnet-docker/Dockerfile.** 要從 Dockerfile 執行以包含 Windows 功能的範例 PowerShell 命令。\
  <https://github.com/Microsoft/aspnet-docker/blob/master/4.7.1-windowsservercore-ltsc2016/runtime/Dockerfile>

>[!div class="step-by-step"]
>[上一個](index.md) 
>[下一步](../multi-container-microservice-net-applications/index.md)
