---
title: 針對 .NET 容器要設為目標的作業系統
description: 容器化 .NET 應用程式的 .NET 微服務架構 | 針對 .NET 容器要設為目標的作業系統
ms.date: 01/30/2020
ms.openlocfilehash: 1f52dcb4da6509be7e771af353daea9cfc97306c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95688454"
---
# <a name="what-os-to-target-with-net-containers"></a><span data-ttu-id="2e0c0-103">針對 .NET 容器要設為目標的作業系統</span><span class="sxs-lookup"><span data-stu-id="2e0c0-103">What OS to target with .NET containers</span></span>

<span data-ttu-id="2e0c0-104">考量到 Docker 支援的作業系統多樣性及 .NET Framework 和 .NET Core 之間的不同，建議您根據您使用的架構來瞄準特定 OS 和特定的版本。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-104">Given the diversity of operating systems supported by Docker and the differences between .NET Framework and .NET Core, you should target a specific OS and specific versions depending on the framework you are using.</span></span>

<span data-ttu-id="2e0c0-105">針對 Windows，您可以使用 Windows Server Core 或 Windows Nano Server。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-105">For Windows, you can use Windows Server Core or Windows Nano Server.</span></span> <span data-ttu-id="2e0c0-106">這些 Windows 版本提供了 .NET Framework 或 .NET Core 各自所需的不同特性 (Windows Server 中的 IIS 與 Nano Server 中的自我裝載網頁伺服器，例如 Kestrel)。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-106">These Windows versions provide different characteristics (IIS in Windows Server Core versus a self-hosted web server like Kestrel in Nano Server) that might be needed by .NET Framework or .NET Core, respectively.</span></span>

<span data-ttu-id="2e0c0-107">針對 Linux，有多個發佈可供使用，且受到正式 .NET Docker 映像的支援 (例如 Debian)。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-107">For Linux, multiple distros are available and supported in official .NET Docker images (like Debian).</span></span>

<span data-ttu-id="2e0c0-108">在圖 3-1 中，您可以看到根據使用的 .NET Framework，可能使用的 OS 版本。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-108">In Figure 3-1 you can see the possible OS version depending on the .NET framework used.</span></span>

![顯示哪些作業系統與 .NET 容器搭配使用的圖表。](./media/net-container-os-targets/targeting-operating-systems.png)

<span data-ttu-id="2e0c0-110">**圖3-1。**</span><span class="sxs-lookup"><span data-stu-id="2e0c0-110">**Figure 3-1.**</span></span> <span data-ttu-id="2e0c0-111">根據 .NET Framework 版本決定要設為目標的作業系統</span><span class="sxs-lookup"><span data-stu-id="2e0c0-111">Operating systems to target depending on versions of the .NET framework</span></span>

<span data-ttu-id="2e0c0-112">當您部署舊版 .NET Framework 應用程式時，您必須以 Windows Server Core 為目標，與繼承應用程式和 IIS 相容，但它有較大的影像。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-112">When deploying legacy .NET Framework applications you have to target Windows Server Core, compatible with legacy apps and IIS, but it has a larger image.</span></span> <span data-ttu-id="2e0c0-113">在部署 .NET Core 應用程式時，您能夠以 Windows Nano Server 為目標，因為它已經過雲端最佳化、使用 Kestrel，且較為輕巧而啟動速度較快。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-113">When deploying .NET Core applications, you can target Windows Nano Server, which is cloud optimized, uses Kestrel and is smaller and starts faster.</span></span> <span data-ttu-id="2e0c0-114">此外，支援 Debian、Alpine 和其他項目的 Linux 也可作為目標。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-114">You can also target Linux, supporting Debian, Alpine and others.</span></span> <span data-ttu-id="2e0c0-115">也會使用 Kestrel、較小且更快速地啟動。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-115">Also uses Kestrel, is smaller, and starts faster.</span></span>

<span data-ttu-id="2e0c0-116">若您想要使用不同的 Linux 發佈或 Microsoft 未支援的版本，您也可以建立您自己的 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-116">You can also create your own Docker image in cases where you want to use a different Linux distro or where you want an image with versions not provided by Microsoft.</span></span> <span data-ttu-id="2e0c0-117">例如，您可以建立讓 ASP.NET Core 在傳統式 .NET Framework 及 Windows Server Core 上執行的映像 (並非 Docker 的常見案例)。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-117">For example, you might create an image with ASP.NET Core running on the traditional .NET Framework and Windows Server Core, which is a not-so-common scenario for Docker.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e0c0-118">當您使用 Windows Server Core 映射時，可能會發現某些 Dll 遺失，相較于完整的 Windows 映像。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-118">When using Windows Server Core images, you might find that some DLLs are missing, when compared to full Windows images.</span></span> <span data-ttu-id="2e0c0-119">您可以藉由建立自訂 Server Core 映射，在映射建立時新增遺失的檔案，如此 [GitHub 批註](https://github.com/microsoft/dotnet-framework-docker/issues/299#issuecomment-511537448)中所述，您可以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-119">You might be able to solve this problem by creating a custom Server Core image, adding the missing files at image build time, as mentioned in this [GitHub comment](https://github.com/microsoft/dotnet-framework-docker/issues/299#issuecomment-511537448).</span></span>

<span data-ttu-id="2e0c0-120">當您將映像名稱新增至您的 Dockerfile 檔案時，您可以根據使用的標籤選取作業系統及版本，如下列範例中所示：</span><span class="sxs-lookup"><span data-stu-id="2e0c0-120">When you add the image name to your Dockerfile file, you can select the operating system and version depending on the tag you use, as in the following examples:</span></span>

| <span data-ttu-id="2e0c0-121">映像</span><span class="sxs-lookup"><span data-stu-id="2e0c0-121">Image</span></span> | <span data-ttu-id="2e0c0-122">註解</span><span class="sxs-lookup"><span data-stu-id="2e0c0-122">Comments</span></span> |
|-------|----------|
| <span data-ttu-id="2e0c0-123">mcr.microsoft.com/dotnet/runtime:3.1</span><span class="sxs-lookup"><span data-stu-id="2e0c0-123">mcr.microsoft.com/dotnet/runtime:3.1</span></span> | <span data-ttu-id="2e0c0-124">.NET Core 3.1 多架構：支援 Linux 和 Windows Nano Server，視 Docker 主機而定。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-124">.NET Core 3.1 multi-architecture: Supports Linux and Windows Nano Server depending on the Docker host.</span></span> |
| <span data-ttu-id="2e0c0-125">mcr.microsoft.com/dotnet/aspnet:3.1</span><span class="sxs-lookup"><span data-stu-id="2e0c0-125">mcr.microsoft.com/dotnet/aspnet:3.1</span></span> | <span data-ttu-id="2e0c0-126">ASP.NET Core 3.1 多架構：支援 Linux 和 Windows Nano Server，視 Docker 主機而定。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-126">ASP.NET Core 3.1 multi-architecture: Supports Linux and Windows Nano Server depending on the Docker host.</span></span> <br/> <span data-ttu-id="2e0c0-127">aspnetcore 映像有幾項針對 ASP.NET Core 所做的最佳化。</span><span class="sxs-lookup"><span data-stu-id="2e0c0-127">The aspnetcore image has a few optimizations for ASP.NET Core.</span></span> |
| <span data-ttu-id="2e0c0-128">mcr.microsoft.com/dotnet/aspnet:3.1-buster-slim</span><span class="sxs-lookup"><span data-stu-id="2e0c0-128">mcr.microsoft.com/dotnet/aspnet:3.1-buster-slim</span></span> | <span data-ttu-id="2e0c0-129">僅限 .NET Core 3.1 執行時間-僅限於 Linux Debian 發行版本</span><span class="sxs-lookup"><span data-stu-id="2e0c0-129">.NET Core 3.1 runtime-only on Linux Debian distro</span></span> |
| <span data-ttu-id="2e0c0-130">mcr.microsoft.com/dotnet/aspnet:3.1-nanoserver-1809</span><span class="sxs-lookup"><span data-stu-id="2e0c0-130">mcr.microsoft.com/dotnet/aspnet:3.1-nanoserver-1809</span></span> | <span data-ttu-id="2e0c0-131">僅限 .NET Core 3.1 執行時間-僅限於 Windows Nano Server (Windows Server 1809 版) </span><span class="sxs-lookup"><span data-stu-id="2e0c0-131">.NET Core 3.1 runtime-only on Windows Nano Server (Windows Server version 1809)</span></span> |

## <a name="additional-resources"></a><span data-ttu-id="2e0c0-132">其他資源</span><span class="sxs-lookup"><span data-stu-id="2e0c0-132">Additional resources</span></span>

- <span data-ttu-id="2e0c0-133">**BitmapDecoder 失敗，因為 GitHub 問題缺少 WindowsCodecsExt.dll ()**</span><span class="sxs-lookup"><span data-stu-id="2e0c0-133">**BitmapDecoder fails due to missing WindowsCodecsExt.dll (GitHub issue)**</span></span>  
  <https://github.com/microsoft/dotnet-framework-docker/issues/299>

> [!div class="step-by-step"]
> <span data-ttu-id="2e0c0-134">[上一個](container-framework-choice-factors.md) 
> [下一步](official-net-docker-images.md)</span><span class="sxs-lookup"><span data-stu-id="2e0c0-134">[Previous](container-framework-choice-factors.md)
[Next](official-net-docker-images.md)</span></span>
