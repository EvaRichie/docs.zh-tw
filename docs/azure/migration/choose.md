---
title: 選擇正確的 Azure 裝載選項
description: 了解哪些 Azure 移轉路徑適合您的 ASP.NET Web 應用程式。
author: CESARDELATORRE
ms.author: cesardl
ms.date: 03/01/2020
ms.openlocfilehash: a8ad946b03f97272cb8685620858af6b21a372dc
ms.sourcegitcommit: e3cbf26d67f7e9286c7108a2752804050762d02d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2020
ms.locfileid: "82072106"
---
# <a name="choose-the-right-azure-hosting-option"></a><span data-ttu-id="46437-103">選擇正確的 Azure 裝載選項</span><span class="sxs-lookup"><span data-stu-id="46437-103">Choose the right Azure hosting option</span></span>

<span data-ttu-id="46437-104">本文提供您在將現有的 .NET Framework 應用程式從內部部署遷移至 Azure 時，Azure 中多個選擇之間的考慮和比較。</span><span class="sxs-lookup"><span data-stu-id="46437-104">This article provides considerations and comparisons between the multiple choices you have in Azure when migrating your existing .NET Framework applications from on-premises to Azure.</span></span>

<span data-ttu-id="46437-105">將現有 .NET 應用程式移轉至 Azure 時要考慮的基本領域如下︰</span><span class="sxs-lookup"><span data-stu-id="46437-105">The fundamental areas to consider when migrating existing .NET applications to Azure are:</span></span>

1. <span data-ttu-id="46437-106">計算服務選項</span><span class="sxs-lookup"><span data-stu-id="46437-106">Compute choices</span></span>
1. <span data-ttu-id="46437-107">資料庫選項</span><span class="sxs-lookup"><span data-stu-id="46437-107">Database choices</span></span>
1. <span data-ttu-id="46437-108">網路和安全性考量</span><span class="sxs-lookup"><span data-stu-id="46437-108">Networking and security considerations</span></span>
1. <span data-ttu-id="46437-109">驗證和授權考量</span><span class="sxs-lookup"><span data-stu-id="46437-109">Authentication and authorization considerations</span></span>

## <a name="compute-choices"></a><span data-ttu-id="46437-110">計算服務選項</span><span class="sxs-lookup"><span data-stu-id="46437-110">Compute choices</span></span>

<span data-ttu-id="46437-111">將現有的 .NET Framework 應用程式移轉至 Azure 時則會有多個選項。</span><span class="sxs-lookup"><span data-stu-id="46437-111">When migrating existing .NET Framework applications to Azure you have multiple choices.</span></span> <span data-ttu-id="46437-112">不過，因為 .NET Framework 相依於 Windows，下列選項僅限於以 Windows 為基礎的計算服務。</span><span class="sxs-lookup"><span data-stu-id="46437-112">However, since .NET Framework depends on Windows, the following choices are limited to Windows-based compute services.</span></span>

<span data-ttu-id="46437-113">下表列出數個比較和建議，可協助您為現有的 .NET 應用程式選擇適合的計算移轉路徑。</span><span class="sxs-lookup"><span data-stu-id="46437-113">The following table shows several comparisons and recommendations to help you choose the right compute migration path for your existing .NET application.</span></span>

|                 | <span data-ttu-id="46437-114">Azure VM</span><span class="sxs-lookup"><span data-stu-id="46437-114">Azure VMs</span></span> | <span data-ttu-id="46437-115">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="46437-115">Azure App Service</span></span> | <span data-ttu-id="46437-116">Windows 容器</span><span class="sxs-lookup"><span data-stu-id="46437-116">Windows Containers</span></span> |
|-----------------|-----------|-------------------|--------------------|
|<span data-ttu-id="46437-117">使用時機</span><span class="sxs-lookup"><span data-stu-id="46437-117">When to use</span></span>      |<ul><li><span data-ttu-id="46437-118">應用程式在伺服器和本機 .msi 安裝上具有強烈相依性。</span><span class="sxs-lookup"><span data-stu-id="46437-118">Application has strong dependencies on the server and local .msi installations.</span></span></li><li><span data-ttu-id="46437-119">您會希望應用程式移轉路徑越簡單越好</span><span class="sxs-lookup"><span data-stu-id="46437-119">You want the easiest application migration path</span></span></li></ul>|<span data-ttu-id="46437-120">應用程式與伺服器沒有相依性，是個乾淨的 ASP.NET Web 應用程式 (MVC、WebForm) 或存取資料庫伺服器的多層式架構應用程式 (Web API、WCf)。</span><span class="sxs-lookup"><span data-stu-id="46437-120">App has no dependencies on the server, it is just a clean ASP.NET web app (MVC, WebForm) or N-Tier app (Web API, WCf) accessing a database server.</span></span> |<ul><li><span data-ttu-id="46437-121">應用程式在原始伺服器上具有相依性，但這些相依性可以包含在 Docker Windows 映像中。</span><span class="sxs-lookup"><span data-stu-id="46437-121">Application has dependencies on the original server but those dependencies can be included in the Docker Windows image.</span></span></li><li><span data-ttu-id="46437-122">想要將應用程式現代化，使其成為[雲端 DevOps 就緒](../../architecture/modernize-with-azure-containers/modernize-existing-apps-to-cloud-optimized/reasons-to-modernize-existing-net-apps-to-cloud-optimized-applications.md)</span><span class="sxs-lookup"><span data-stu-id="46437-122">Want to modernize the app so it is  [Cloud DevOps-Ready](../../architecture/modernize-with-azure-containers/modernize-existing-apps-to-cloud-optimized/reasons-to-modernize-existing-net-apps-to-cloud-optimized-applications.md)</span></span></li></ul>|
|<span data-ttu-id="46437-123">優點與好處</span><span class="sxs-lookup"><span data-stu-id="46437-123">Pros & benefits</span></span>  |<ul><li><span data-ttu-id="46437-124">最簡單的移轉路徑</span><span class="sxs-lookup"><span data-stu-id="46437-124">Easiest migration path</span></span></li><li><span data-ttu-id="46437-125">熟悉的環境。</span><span class="sxs-lookup"><span data-stu-id="46437-125">Familiar environment.</span></span> <span data-ttu-id="46437-126">部署環境是 VM，因此類似于內部部署伺服器。</span><span class="sxs-lookup"><span data-stu-id="46437-126">Deployment environment is a VM, so it's similar to on-premises servers.</span></span></li></ul> |<span data-ttu-id="46437-127">進行中的 PaaS 維護作業是在 Azure 中管理和調整應用程式最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="46437-127">Ongoing PaaS maintenance, simplest way to manage and scale apps in Azure.</span></span> |<ul><li><span data-ttu-id="46437-128">準備好讓雲端 DevOps 準備就緒，內含應用程式容器中的相依性。</span><span class="sxs-lookup"><span data-stu-id="46437-128">Prepared for the future, Cloud DevOps-Ready with dependencies included in the app's containers.</span></span></li><li><span data-ttu-id="46437-129">幾乎不需要重構 .NET/C # 程式碼。</span><span class="sxs-lookup"><span data-stu-id="46437-129">Almost no need to refactor .NET /C# code.</span></span></li></ul> |
|<span data-ttu-id="46437-130">缺點</span><span class="sxs-lookup"><span data-stu-id="46437-130">Cons</span></span>             |<span data-ttu-id="46437-131">此為 IaaS。</span><span class="sxs-lookup"><span data-stu-id="46437-131">It is IaaS.</span></span> <span data-ttu-id="46437-132">維護成本昂貴。</span><span class="sxs-lookup"><span data-stu-id="46437-132">Maintenance is costly.</span></span> <span data-ttu-id="46437-133">您必須管理 VM 有關網路、負載平衡器、相應放大、IIS 管理等的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="46437-133">You have to manage the VM's infrastructure about networking, load-balancer, scale-out, IIS management, and so on.</span></span> |<ul><li><span data-ttu-id="46437-134">並未[支援](https://appmigration.microsoft.com/assessment)所有的應用程式</span><span class="sxs-lookup"><span data-stu-id="46437-134">Not all apps are [supported](https://appmigration.microsoft.com/assessment)</span></span></li><li><span data-ttu-id="46437-135">有些應用程式可能需要重構，甚至是稍微重新架構，因此支援 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="46437-135">Some apps might need to be refactored and even slightly rearchitected, so they support Azure App Service.</span></span></li></ul> |<ul><li><span data-ttu-id="46437-136">Docker 的技能學習曲線</span><span class="sxs-lookup"><span data-stu-id="46437-136">Docker's skills learning curve</span></span></li><li><span data-ttu-id="46437-137">某些程式碼和應用程式組態設定會變更</span><span class="sxs-lookup"><span data-stu-id="46437-137">Some code and app configuration settings changes</span></span></li></ul>|
|<span data-ttu-id="46437-138">需求</span><span class="sxs-lookup"><span data-stu-id="46437-138">Requirements</span></span> |<span data-ttu-id="46437-139">比起內部部署應用程式，具有相同需求的 Windows Server VM</span><span class="sxs-lookup"><span data-stu-id="46437-139">Windows Server VM with the same requirements than the app for on-premises</span></span> | <span data-ttu-id="46437-140">在[準備檢查](https://github.com/Azure/App-Service-Migration-Assistant/wiki/Readiness-Checks)中指定 Azure App Service 需求。</span><span class="sxs-lookup"><span data-stu-id="46437-140">Azure App Service requirements specified in [Readiness checks](https://github.com/Azure/App-Service-Migration-Assistant/wiki/Readiness-Checks).</span></span> |<ul><li>[<span data-ttu-id="46437-141">Docker Engine-適用于 Windows Server 2019 的 Enterprise</span><span class="sxs-lookup"><span data-stu-id="46437-141">Docker Engine - Enterprise for Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/cloud-infrastructure-services.docker-windows-2019)<br /><span data-ttu-id="46437-142">或</span><span class="sxs-lookup"><span data-stu-id="46437-142">or</span></span></li><li><span data-ttu-id="46437-143">[Azure Container Service (AKS)](https://azure.microsoft.com/services/container-service/) (此為 Kubernetes 協調器)</span><span class="sxs-lookup"><span data-stu-id="46437-143">[Azure Container Service (AKS)](https://azure.microsoft.com/services/container-service/) (That is Kubernetes orchestrator)</span></span><br /><span data-ttu-id="46437-144">或</span><span class="sxs-lookup"><span data-stu-id="46437-144">or</span></span><li><span data-ttu-id="46437-145">[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) 協調器</span><span class="sxs-lookup"><span data-stu-id="46437-145">[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) orchestrator</span></span></li></ul> |
|<span data-ttu-id="46437-146">如何移轉</span><span class="sxs-lookup"><span data-stu-id="46437-146">How to migrate</span></span> |<span data-ttu-id="46437-147">請參閱[移轉至 Azure 虛擬機器](vm.md)</span><span class="sxs-lookup"><span data-stu-id="46437-147">See [Migrate to Azure Virtual Machines](vm.md)</span></span> | <span data-ttu-id="46437-148">請參閱[移轉 Azure App Service](app-service.md)</span><span class="sxs-lookup"><span data-stu-id="46437-148">See [Migrate Azure App Service](app-service.md)</span></span> | <span data-ttu-id="46437-149">遵循[使用 Azure 和 Windows 容器現代化現有 .net 應用程式電子書](https://aka.ms/liftandshiftwithcontainersebook)中所述的考慮、案例和逐步解說</span><span class="sxs-lookup"><span data-stu-id="46437-149">Follow considerations, scenarios, and walkthroughs explained in the [Modernizing existing .NET apps with Azure and Windows Containers eBook](https://aka.ms/liftandshiftwithcontainersebook)</span></span> |

<span data-ttu-id="46437-150">下列流程圖顯示針對現有 .NET Framework 應用程式，規劃遷移至 Azure 時的決策樹。</span><span class="sxs-lookup"><span data-stu-id="46437-150">The following flowchart diagram shows a decision tree when planning a migration to Azure for your existing .NET Framework applications.</span></span> <span data-ttu-id="46437-151">如果可行，請先嘗試 option A，但 option B 是最簡單的執行路徑。</span><span class="sxs-lookup"><span data-stu-id="46437-151">If it's viable, try option A first, but option B is the easiest path to perform.</span></span>

![顯示裝載決策樹的流程圖](../media/migration/choose/decision-tree.png)

## <a name="database-choices"></a><span data-ttu-id="46437-153">資料庫選項</span><span class="sxs-lookup"><span data-stu-id="46437-153">Database choices</span></span>

<span data-ttu-id="46437-154">將關聯式資料庫移轉到 Azure 時您有多個選項。</span><span class="sxs-lookup"><span data-stu-id="46437-154">When migrating relational databases to Azure you have multiple choices.</span></span> <span data-ttu-id="46437-155">請參閱[將 SQL Server 資料庫移轉至 Azure](sql.md)，可協助您為現有的 .NET 應用程式選擇正確的資料庫移轉路徑。</span><span class="sxs-lookup"><span data-stu-id="46437-155">See [Migrate your SQL Server database to Azure](sql.md) to help you choose the right database migration path for your existing .NET application.</span></span>

## <a name="networking-and-security-considerations"></a><span data-ttu-id="46437-156">網路和安全性考量</span><span class="sxs-lookup"><span data-stu-id="46437-156">Networking and security considerations</span></span>

<span data-ttu-id="46437-157">在將應用程式部署至如 Microsoft Azure 等公用雲端時，您可能想要[建立網路 DMZ](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/) 來隔離和保護特定網路，例如 [Azure 與內部部署間的周邊網路](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) 或 [Azure 與網際網路間的 DMZ](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)。</span><span class="sxs-lookup"><span data-stu-id="46437-157">When deploying applications to a public cloud like Microsoft Azure, you might want to isolate and secure certain networks by [creating network DMZs](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/), such as a [DMZ between Azure and on-premises](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) or a [DMZ between Azure and the Internet](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz).</span></span> <span data-ttu-id="46437-158">周邊網路可以透過 [Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)來實作。</span><span class="sxs-lookup"><span data-stu-id="46437-158">DMZs can be implemented with [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).</span></span>

<span data-ttu-id="46437-159">Azure 虛擬網路可讓您：</span><span class="sxs-lookup"><span data-stu-id="46437-159">Azure Virtual networks enable you to:</span></span>

- <span data-ttu-id="46437-160">建置可控制的混合式基礎結構</span><span class="sxs-lookup"><span data-stu-id="46437-160">Build a hybrid infrastructure that you control</span></span>
- <span data-ttu-id="46437-161">使用自己的 IP 位址與 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="46437-161">Bring your own IP addresses and DNS servers</span></span>
- <span data-ttu-id="46437-162">利用 IPsec VPN 或 ExpressRoute 保障連線的安全</span><span class="sxs-lookup"><span data-stu-id="46437-162">Secure your connections with an IPsec VPN or ExpressRoute</span></span>
- <span data-ttu-id="46437-163">對子網路間的流量進行細微的控制</span><span class="sxs-lookup"><span data-stu-id="46437-163">Get granular control over traffic between subnets</span></span>
- <span data-ttu-id="46437-164">使用虛擬應用設備建立精密的網路拓撲</span><span class="sxs-lookup"><span data-stu-id="46437-164">Create sophisticated network topologies using virtual appliances</span></span>
- <span data-ttu-id="46437-165">為您的應用程式取得隔離且高度安全的環境</span><span class="sxs-lookup"><span data-stu-id="46437-165">Get an isolated and highly secure environment for your applications</span></span>

<span data-ttu-id="46437-166">若要開始建置您自己的虛擬網路，請參閱 [Azure 虛擬網路文件](https://docs.microsoft.com/azure/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="46437-166">To get started building your own virtual network, see the [Azure Virtual Network documentation](https://docs.microsoft.com/azure/virtual-network/).</span></span>

## <a name="authentication-and-authorization-considerations-when-migrating-to-azure"></a><span data-ttu-id="46437-167">移轉至 Azure 時的驗證和授權考量</span><span class="sxs-lookup"><span data-stu-id="46437-167">Authentication and authorization considerations when migrating to Azure</span></span>

<span data-ttu-id="46437-168">任何組織要移到雲端時的首要考量皆是安全性。</span><span class="sxs-lookup"><span data-stu-id="46437-168">A top concern of any organization moving to the cloud is security.</span></span> <span data-ttu-id="46437-169">大部分的公司投入了大量的時間、金錢和工程設計和開發安全性模型，因此他們必須能夠運用現有的投資，例如身分識別存放區和單一登入解決方案。</span><span class="sxs-lookup"><span data-stu-id="46437-169">Most companies have invested a substantial amount of time, money, and engineering into designing and developing a security model, and it's important that they're able to leverage existing investments such as identity stores and single sign-on solutions.</span></span>

<span data-ttu-id="46437-170">許多執行於內部部署的現有企業 B2E .NET 應用程式使用 Active Directory 進行驗證和身分識別管理。</span><span class="sxs-lookup"><span data-stu-id="46437-170">Many existing enterprise B2E .NET applications running on-premises use Active Directory for authentication and identity management.</span></span> <span data-ttu-id="46437-171">Azure AD Connect 可讓您整合內部部署目錄與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="46437-171">Azure AD Connect enables you to integrate your on-premises directories with Azure Active Directory.</span></span> <span data-ttu-id="46437-172">若要開始，請參閱[整合您的內部部署目錄與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</span><span class="sxs-lookup"><span data-stu-id="46437-172">To get started, see [Integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>

<span data-ttu-id="46437-173">請參閱[混合式身分識別解決方案的身分識別需求](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-business-needs)以進一步進行 Azure Active Directory 的相關規劃。</span><span class="sxs-lookup"><span data-stu-id="46437-173">See [Identity requirements for your hybrid identity solution](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-business-needs) for further planning related to Azure Active Directory.</span></span>

<span data-ttu-id="46437-174">其他驗證通訊協定的選擇還有 [OAuth](https://en.wikipedia.org/wiki/OAuth) 和 [OpenID](https://en.wikipedia.org/wiki/OpenID)，其在消費者導向應用程式中很常見。</span><span class="sxs-lookup"><span data-stu-id="46437-174">Other authentication protocol choices are [OAuth](https://en.wikipedia.org/wiki/OAuth) and [OpenID](https://en.wikipedia.org/wiki/OpenID), which are common in consumer-facing applications.</span></span> <span data-ttu-id="46437-175">使用自發的身分識別資料庫 (例如由 IdentityServer4 使用 OAuth 包裝的 ASP.NET 身分識別 SQL 資料庫)，通常不需連線到內部部署資料庫或目錄。</span><span class="sxs-lookup"><span data-stu-id="46437-175">When using autonomous identity databases, such as an ASP.NET Identity SQL database wrapped by IdentityServer4 using OAuth, no connectivity to on-premises databases or directories is usually required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46437-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46437-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46437-177">將 ASP.NET web 應用程式遷移至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="46437-177">Migrate an ASP.NET web application to Azure App Service</span></span>](app-service.md)