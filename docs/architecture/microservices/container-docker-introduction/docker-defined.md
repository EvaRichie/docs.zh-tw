---
title: 什麼是 Docker？
description: 容器化 .NET 應用程式的 .NET 微服務架構 | 什麼是 Docker？
ms.date: 08/31/2018
ms.openlocfilehash: 7d4b419f46f32fa4acdeb1ac7d5e0c2b2c199fc5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91172400"
---
# <a name="what-is-docker"></a><span data-ttu-id="a6b31-103">什麼是 Docker？</span><span class="sxs-lookup"><span data-stu-id="a6b31-103">What is Docker?</span></span>

<span data-ttu-id="a6b31-104">[Docker](https://www.docker.com/) 是[開放原始碼專案](https://github.com/docker/docker)，將應用程式自動化部署為可攜式且可自足的容器，在雲端或內部部署上執行。</span><span class="sxs-lookup"><span data-stu-id="a6b31-104">[Docker](https://www.docker.com/) is an [open-source project](https://github.com/docker/docker) for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises.</span></span> <span data-ttu-id="a6b31-105">Docker 也是一家升級及發展這項技術的[公司](https://www.docker.com/)，並且與雲端、Linux 和 Windows 廠商 (包括 Microsoft) 合作。</span><span class="sxs-lookup"><span data-stu-id="a6b31-105">Docker is also a [company](https://www.docker.com/) that promotes and evolves this technology, working in collaboration with cloud, Linux, and Windows vendors, including Microsoft.</span></span>

![此圖顯示 Docker 容器可執行檔位置。](./media/docker-defined/docker-containers-run-anywhere.png)

<span data-ttu-id="a6b31-107">**圖 2-2**。</span><span class="sxs-lookup"><span data-stu-id="a6b31-107">**Figure 2-2**.</span></span> <span data-ttu-id="a6b31-108">Docker 會在混合式雲端的所有層級部署容器。</span><span class="sxs-lookup"><span data-stu-id="a6b31-108">Docker deploys containers at all layers of the hybrid cloud.</span></span>

<span data-ttu-id="a6b31-109">Docker 容器可以在任何位置執行，例如客戶資料中心的內部部署、外部服務提供者或雲端 (在 Azure 上)。</span><span class="sxs-lookup"><span data-stu-id="a6b31-109">Docker containers can run anywhere, on-premises in the customer datacenter, in an external service provider or in the cloud, on Azure.</span></span> <span data-ttu-id="a6b31-110">Docker 映像容器可以原生方式在 Linux 及 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="a6b31-110">Docker image containers can run natively on Linux and Windows.</span></span> <span data-ttu-id="a6b31-111">不過，Windows 映像只能在 Windows 主機上執行，而 Linux 映像可以在 Linux 主機和 Windows 主機上執行 (目前是使用 Hyper-V Linux VM)，其中主機是指伺服器或 VM。</span><span class="sxs-lookup"><span data-stu-id="a6b31-111">However, Windows images can run only on Windows hosts and Linux images can run on Linux hosts and Windows hosts (using a Hyper-V Linux VM, so far), where host means a server or a VM.</span></span>

<span data-ttu-id="a6b31-112">開發人員可以使用 Windows、Linux 或 macOS 上的開發環境。</span><span class="sxs-lookup"><span data-stu-id="a6b31-112">Developers can use development environments on Windows, Linux, or macOS.</span></span> <span data-ttu-id="a6b31-113">在開發電腦上，開發人員執行的 Docker 主機是 Docker 映像部署所在，包括應用程式及其相依性。</span><span class="sxs-lookup"><span data-stu-id="a6b31-113">On the development computer, the developer runs a Docker host where Docker images are deployed, including the app and its dependencies.</span></span> <span data-ttu-id="a6b31-114">在 Linux 或 macOS 上工作的開發人員會使用以 Linux 為基礎的 Docker 主機，而且只能建立適用于 Linux 容器的映射。</span><span class="sxs-lookup"><span data-stu-id="a6b31-114">Developers who work on Linux or on macOS use a Docker host that is Linux based, and they can create images only for Linux containers.</span></span> <span data-ttu-id="a6b31-115"> (使用 macOS 的開發人員可以從 macOS 編輯程式碼或執行 Docker CLI，但在撰寫本文時，容器不會直接在 macOS 上執行。 ) 在 Windows 上工作的開發人員可以建立 Linux 或 Windows 容器的映射。</span><span class="sxs-lookup"><span data-stu-id="a6b31-115">(Developers working on macOS can edit code or run the Docker CLI from macOS, but as of the time of this writing, containers don't run directly on macOS.) Developers who work on Windows can create images for either Linux or Windows Containers.</span></span>

<span data-ttu-id="a6b31-116">為了在開發環境中裝載容器並且提供其他開發人員工具，Docker 提供適用於 Windows 或 macOS 的 [Docker Community Edition (CE)](https://www.docker.com/community-edition)。</span><span class="sxs-lookup"><span data-stu-id="a6b31-116">To host containers in development environments and provide additional developer tools, Docker ships [Docker Community Edition (CE)](https://www.docker.com/community-edition) for Windows or for macOS.</span></span> <span data-ttu-id="a6b31-117">這些產品都會安裝必要的 VM (Docker 主機) 以裝載容器。</span><span class="sxs-lookup"><span data-stu-id="a6b31-117">These products install the necessary VM (the Docker host) to host the containers.</span></span> <span data-ttu-id="a6b31-118">Docker 也提供 [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition)，這是專為企業開發所設計的，由在生產環境中建置、交付及執行大型商務關鍵性應用程式的 IT 小組來使用。</span><span class="sxs-lookup"><span data-stu-id="a6b31-118">Docker also makes available [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition), which is designed for enterprise development and is used by IT teams who build, ship, and run large business-critical applications in production.</span></span>

<span data-ttu-id="a6b31-119">若要執行 [Windows 容器](/virtualization/windowscontainers/about/)，有兩種執行階段：</span><span class="sxs-lookup"><span data-stu-id="a6b31-119">To run [Windows Containers](/virtualization/windowscontainers/about/), there are two types of runtimes:</span></span>

- <span data-ttu-id="a6b31-120">Windows Server 容器透過程序和命名空間隔離技術，提供應用程式隔離。</span><span class="sxs-lookup"><span data-stu-id="a6b31-120">Windows Server Containers provide application isolation through process and namespace isolation technology.</span></span> <span data-ttu-id="a6b31-121">與 Windows Server 容器共用核心的對象為容器主機以及在此主機上執行的所有容器。</span><span class="sxs-lookup"><span data-stu-id="a6b31-121">A Windows Server Container shares a kernel with the container host and with all containers running on the host.</span></span>

- <span data-ttu-id="a6b31-122">Hyper-V 容器可在 Windows Server 容器提供的隔離上展開，方法是在高度最佳化的虛擬機器中執行每個容器。</span><span class="sxs-lookup"><span data-stu-id="a6b31-122">Hyper-V Containers expand on the isolation provided by Windows Server Containers by running each container in a highly optimized virtual machine.</span></span> <span data-ttu-id="a6b31-123">在此組態中，容器主機的核心不會與 Hyper-V 容器共用，以提供更好的隔離。</span><span class="sxs-lookup"><span data-stu-id="a6b31-123">In this configuration, the kernel of the container host isn't shared with the Hyper-V Containers, providing better isolation.</span></span>

<span data-ttu-id="a6b31-124">這些容器映像的建立及運作方式都相同。</span><span class="sxs-lookup"><span data-stu-id="a6b31-124">The images for these containers are created the same way and function the same.</span></span> <span data-ttu-id="a6b31-125">不同之處在於從執行 Hyper-V 容器的映像建立容器需要額外參數。</span><span class="sxs-lookup"><span data-stu-id="a6b31-125">The difference is in how the container is created from the image running a Hyper-V Container requires an extra parameter.</span></span> <span data-ttu-id="a6b31-126">如需詳細資料，請參閱 [Hyper-V 容器](/virtualization/windowscontainers/manage-containers/hyperv-container)。</span><span class="sxs-lookup"><span data-stu-id="a6b31-126">For details, see [Hyper-V Containers](/virtualization/windowscontainers/manage-containers/hyperv-container).</span></span>

## <a name="comparing-docker-containers-with-virtual-machines"></a><span data-ttu-id="a6b31-127">比較 Docker 容器與虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a6b31-127">Comparing Docker containers with virtual machines</span></span>

<span data-ttu-id="a6b31-128">圖 2-3 比較 VM 和 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="a6b31-128">Figure 2-3 shows a comparison between VMs and Docker containers.</span></span>

| <span data-ttu-id="a6b31-129">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a6b31-129">Virtual Machines</span></span> | <span data-ttu-id="a6b31-130">Docker 容器</span><span class="sxs-lookup"><span data-stu-id="a6b31-130">Docker Containers</span></span> |
| -----------------| ------------------|
|![此圖顯示傳統 VM 的硬體/軟體堆疊。](./media/docker-defined/virtual-machine-hardware-software.png)|![此圖顯示 Docker 容器的硬體/軟體堆疊。](./media/docker-defined/docker-container-hardware-software.png)|
|<span data-ttu-id="a6b31-133">虛擬機器包含應用程式、必要的程式庫或二進位檔，以及完整的客體作業系統。</span><span class="sxs-lookup"><span data-stu-id="a6b31-133">Virtual machines include the application, the required libraries or binaries, and a full guest operating system.</span></span> <span data-ttu-id="a6b31-134">完整的虛擬化比容器化需要更多資源。</span><span class="sxs-lookup"><span data-stu-id="a6b31-134">Full virtualization requires more resources than containerization.</span></span> | <span data-ttu-id="a6b31-135">容器包括應用程式及其所有相依性。</span><span class="sxs-lookup"><span data-stu-id="a6b31-135">Containers include the application and all its dependencies.</span></span> <span data-ttu-id="a6b31-136">不過，它們會與其他容器共用作業系統核心，並在主機作業系統的使用者空間中，以獨立程序的形式執行。</span><span class="sxs-lookup"><span data-stu-id="a6b31-136">However, they share the OS kernel with other containers, running as isolated processes in user space on the host operating system.</span></span> <span data-ttu-id="a6b31-137">(Hyper-V 容器除外，因為每個容器都是在每個容器的特殊虛擬機器內部執行。)</span><span class="sxs-lookup"><span data-stu-id="a6b31-137">(Except in Hyper-V containers, where each container runs inside of a special virtual machine per container.)</span></span> |

<span data-ttu-id="a6b31-138">**圖 2-3**。</span><span class="sxs-lookup"><span data-stu-id="a6b31-138">**Figure 2-3**.</span></span> <span data-ttu-id="a6b31-139">傳統虛擬機器與 Docker 容器的比較</span><span class="sxs-lookup"><span data-stu-id="a6b31-139">Comparison of traditional virtual machines to Docker containers</span></span>

<span data-ttu-id="a6b31-140">針對 VM，在主機伺服器中有三個基礎層，從下到上分別是：基礎結構、主機作業系統和 Hypervisor，每部 VM 在頂端都具有各自的作業系統和所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="a6b31-140">For VMs, there are three base layers in the host server, from the bottom-up: infrastructure, Host Operating System and a Hypervisor and on top of all that each VM has its own OS and all necessary libraries.</span></span> <span data-ttu-id="a6b31-141">針對 Docker，主機伺服器只有基礎結構和作業系統，在上方則是容器引擎，該引擎會讓容器保持隔離，但是共用基礎作業系統服務。</span><span class="sxs-lookup"><span data-stu-id="a6b31-141">For Docker, the host server only has the infrastructure and the OS and on top of that, the container engine, that keeps container isolated but sharing the base OS services.</span></span>

<span data-ttu-id="a6b31-142">因為容器只需要很少的資源 (例如，它們不需要完整的作業系統)，所以容易部署且會快速啟動。</span><span class="sxs-lookup"><span data-stu-id="a6b31-142">Because containers require far fewer resources (for example, they don't need a full OS), they're easy to deploy and they start fast.</span></span> <span data-ttu-id="a6b31-143">這可讓您擁有更高的密度，這表示可讓您在相同硬體單位上執行更多服務，藉此降低成本。</span><span class="sxs-lookup"><span data-stu-id="a6b31-143">This allows you to have higher density, meaning that it allows you to run more services on the same hardware unit, thereby reducing costs.</span></span>

<span data-ttu-id="a6b31-144">在相同核心上執行的副作用是隔離程度比 VM 低。</span><span class="sxs-lookup"><span data-stu-id="a6b31-144">As a side effect of running on the same kernel, you get less isolation than VMs.</span></span>

<span data-ttu-id="a6b31-145">映像的主要目標是跨不同的部署建立相同的環境 (相依性)。</span><span class="sxs-lookup"><span data-stu-id="a6b31-145">The main goal of an image is that it makes the environment (dependencies) the same across different deployments.</span></span> <span data-ttu-id="a6b31-146">這表示您可以在自己的電腦上對它進行偵錯，再將它部署到另一部電腦，保證有相同的環境。</span><span class="sxs-lookup"><span data-stu-id="a6b31-146">This means that you can debug it on your machine and then deploy it to another machine with the same environment guaranteed.</span></span>

<span data-ttu-id="a6b31-147">容器映像是一種封裝應用程式或服務，再以可靠且可重現的方式來部署它的方法。</span><span class="sxs-lookup"><span data-stu-id="a6b31-147">A container image is a way to package an app or service and deploy it in a reliable and reproducible way.</span></span> <span data-ttu-id="a6b31-148">您可以這麼認為：Docker 不只是一項技術，更是哲學與過程。</span><span class="sxs-lookup"><span data-stu-id="a6b31-148">You could say that Docker isn't only a technology but also a philosophy and a process.</span></span>

<span data-ttu-id="a6b31-149">使用 Docker 時，您不會聽到開發人員說：「機器上行得通，為什麼生產環境行不通？」</span><span class="sxs-lookup"><span data-stu-id="a6b31-149">When using Docker, you won't hear developers say, "It works on my machine, why not in production?"</span></span> <span data-ttu-id="a6b31-150">他們只會說：「在 Docker 上可以執行」，因為封裝的 Docker 應用程式可以在任何支援的 Docker 環境中執行，而且它是依照預期的方式在所有部署目標上執行 (例如開發、品管、預備及生產)。</span><span class="sxs-lookup"><span data-stu-id="a6b31-150">They can simply say, "It runs on Docker", because the packaged Docker application can be executed on any supported Docker environment, and it runs the way it was intended to on all deployment targets (such as Dev, QA, staging, and production).</span></span>

## <a name="a-simple-analogy"></a><span data-ttu-id="a6b31-151">簡單的比喻</span><span class="sxs-lookup"><span data-stu-id="a6b31-151">A simple analogy</span></span>

<span data-ttu-id="a6b31-152">也許簡單的比喻可以協助您掌握 Docker 的核心概念。</span><span class="sxs-lookup"><span data-stu-id="a6b31-152">Perhaps a simple analogy can help getting the grasp of the core concept of Docker.</span></span>

<span data-ttu-id="a6b31-153">讓我們暫時回到 1950 年。</span><span class="sxs-lookup"><span data-stu-id="a6b31-153">Let's go back in time to the 1950s for a moment.</span></span> <span data-ttu-id="a6b31-154">當時沒有任何文書處理器，而且到處都在使用影印機 (差不多所有人都在用)。</span><span class="sxs-lookup"><span data-stu-id="a6b31-154">There were no word processors, and the photocopiers were used everywhere (kind of).</span></span>

<span data-ttu-id="a6b31-155">假設您負責根據需求來快速發送大批信件，並使用信紙和信封，將信件實際投遞到每個客戶的地址 (當時並沒有電子郵件)。</span><span class="sxs-lookup"><span data-stu-id="a6b31-155">Imagine you're responsible for quickly issuing batches of letters as required, to mail them to customers, using real paper and envelopes, to be delivered physically to each customer's address (there was no email back then).</span></span>

<span data-ttu-id="a6b31-156">慢慢地，您了解到這些信件的內容是大量段落的組合，只是根據信件目的從中挑選和編排需要的段落，因此您設計一個系統，可以快速地發送信件來提高效率。</span><span class="sxs-lookup"><span data-stu-id="a6b31-156">At some point, you realize the letters are just a composition of a large set of paragraphs, which are picked and arranged as needed, according to the purpose of the letter, so you devise a system to issue letters quickly, expecting to get a hefty raise.</span></span>

<span data-ttu-id="a6b31-157">系統很簡單：</span><span class="sxs-lookup"><span data-stu-id="a6b31-157">The system is simple:</span></span>

1. <span data-ttu-id="a6b31-158">您開始準備一疊透明紙張，每一張紙都包含一個段落。</span><span class="sxs-lookup"><span data-stu-id="a6b31-158">You begin with a deck of transparent sheets containing one paragraph each.</span></span>

2. <span data-ttu-id="a6b31-159">若要發送一批信件，您就挑選具有所需段落的紙張，然後將其堆疊並且排列整齊，讓它們整潔易讀。</span><span class="sxs-lookup"><span data-stu-id="a6b31-159">To issue a set of letters, you pick the sheets with the paragraphs you need, then you stack and align them so they look and read fine.</span></span>

3. <span data-ttu-id="a6b31-160">最後，您將這個組合放入影印機中，然後按下開始以產生所需數量的信件。</span><span class="sxs-lookup"><span data-stu-id="a6b31-160">Finally, you place the set in the photocopier and press start to produce as many letters as required.</span></span>

<span data-ttu-id="a6b31-161">因此，工作精簡了，這就是 Docker 的核心概念。</span><span class="sxs-lookup"><span data-stu-id="a6b31-161">So, simplifying, that's the core idea of Docker.</span></span>

<span data-ttu-id="a6b31-162">Docker 中的每一層都是在執行命令 (例如安裝程式) 之後，檔案系統上所發生的變更結果集。</span><span class="sxs-lookup"><span data-stu-id="a6b31-162">In Docker, each layer is the resulting set of changes that happen to the filesystem after executing a command, such as, installing a program.</span></span>

<span data-ttu-id="a6b31-163">因此，當您在複製層之後「查看」檔案系統時，會看到檔案整體，包含安裝程式的層。</span><span class="sxs-lookup"><span data-stu-id="a6b31-163">So, when you "look" at the filesystem after the layer has been copied, you see all the files, included the layer when the program was installed.</span></span>

<span data-ttu-id="a6b31-164">您可以將映像當作是準備要在「電腦」(已安裝作業系統) 中安裝的輔助唯讀硬碟。</span><span class="sxs-lookup"><span data-stu-id="a6b31-164">You can think of an image as an auxiliary read-only hard disk ready to be installed in a "computer" where the operating system is already installed.</span></span>

<span data-ttu-id="a6b31-165">同樣地，您可以將容器當作是已安裝映像硬碟的「電腦」。</span><span class="sxs-lookup"><span data-stu-id="a6b31-165">Similarly, you can think of a container as the "computer" with the image hard disk installed.</span></span> <span data-ttu-id="a6b31-166">容器，就像電腦一樣，可以開啟或關閉。</span><span class="sxs-lookup"><span data-stu-id="a6b31-166">The container, just like a computer, can be powered on or off.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="a6b31-167">[上一個](index.md) 
>[下一步](docker-terminology.md)</span><span class="sxs-lookup"><span data-stu-id="a6b31-167">[Previous](index.md)
[Next](docker-terminology.md)</span></span>
