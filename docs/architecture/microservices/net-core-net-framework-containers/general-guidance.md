---
title: 一般方針
description: 容器化 .NET 應用程式的 .NET 微服務架構 | 一般指引
ms.date: 09/11/2018
ms.openlocfilehash: 6e63d7804abc1703f17378584d58d66a933022c7
ms.sourcegitcommit: 5280b2aef60a1ed99002dba44e4b9e7f6c830604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/03/2020
ms.locfileid: "84306873"
---
# <a name="general-guidance"></a><span data-ttu-id="595b5-103">一般方針</span><span class="sxs-lookup"><span data-stu-id="595b5-103">General guidance</span></span>

<span data-ttu-id="595b5-104">本節提供了何時應選擇 .NET Core 或 .NET Framework 的摘要。</span><span class="sxs-lookup"><span data-stu-id="595b5-104">This section provides a summary of when to choose .NET Core or .NET Framework.</span></span> <span data-ttu-id="595b5-105">我們在後續的章節中提供了更多關於這些選擇的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="595b5-105">We provide more details about these choices in the sections that follow.</span></span>

<span data-ttu-id="595b5-106">在下列情況下，針對您的容器化 Docker 伺服器應用程式使用 .NET Core （含 Linux 或 Windows 容器）：</span><span class="sxs-lookup"><span data-stu-id="595b5-106">Use .NET Core, with Linux or Windows Containers, for your containerized Docker server application when:</span></span>

- <span data-ttu-id="595b5-107">您有跨平台需求。</span><span class="sxs-lookup"><span data-stu-id="595b5-107">You have cross-platform needs.</span></span> <span data-ttu-id="595b5-108">例如，當您想要同時使用 Linux 和 Windows 容器時。</span><span class="sxs-lookup"><span data-stu-id="595b5-108">For example, you want to use both Linux and Windows Containers.</span></span>

- <span data-ttu-id="595b5-109">您的應用程式架構是以微服務作為基礎的。</span><span class="sxs-lookup"><span data-stu-id="595b5-109">Your application architecture is based on microservices.</span></span>

- <span data-ttu-id="595b5-110">您需要快速啟動容器，並且想要每個容器僅具有極小的使用量，以達到更佳的密度，或在每個硬體單位上擁有更多容器，以降低您的成本。</span><span class="sxs-lookup"><span data-stu-id="595b5-110">You need to start containers fast and want a small footprint per container to achieve better density or more containers per hardware unit in order to lower your costs.</span></span>

<span data-ttu-id="595b5-111">簡而言之，當您建立新的容器化 .NET 應用程式時，您便應考慮使用 .NET Core 作為預設選擇。</span><span class="sxs-lookup"><span data-stu-id="595b5-111">In short, when you create new containerized .NET applications, you should consider .NET Core as the default choice.</span></span> <span data-ttu-id="595b5-112">它具有許多優點，並且最符合容器原理和工作樣式。</span><span class="sxs-lookup"><span data-stu-id="595b5-112">It has many benefits and fits best with the containers philosophy and style of working.</span></span>

<span data-ttu-id="595b5-113">使用 .NET Core 的另一個優點便是您可以在相同的電腦上針對應用程式執行並存的 .NET 版本。</span><span class="sxs-lookup"><span data-stu-id="595b5-113">An additional benefit of using .NET Core is that you can run side by side .NET versions for applications within the same machine.</span></span> <span data-ttu-id="595b5-114">這項優點對不使用容器的伺服器或 VM 來說更為重要，因為容器會隔離應用程式需要的 .NET 版本。</span><span class="sxs-lookup"><span data-stu-id="595b5-114">This benefit is more important for servers or VMs that do not use containers, because containers isolate the versions of .NET that the app needs.</span></span> <span data-ttu-id="595b5-115">(只要他們與基礎 OS 相容。)</span><span class="sxs-lookup"><span data-stu-id="595b5-115">(As long as they are compatible with the underlying OS.)</span></span>

<span data-ttu-id="595b5-116">在下列情況中，使用容器化 Docker 伺服器應用程式的 .NET Framework：</span><span class="sxs-lookup"><span data-stu-id="595b5-116">Use .NET Framework for your containerized Docker server application when:</span></span>

- <span data-ttu-id="595b5-117">您的應用程式目前使用的是 .NET Framework，並且對 Windows 具有強烈的相依性。</span><span class="sxs-lookup"><span data-stu-id="595b5-117">Your application currently uses .NET Framework and has strong dependencies on Windows.</span></span>

- <span data-ttu-id="595b5-118">您需要使用 .NET Core 不支援的 Windows API。</span><span class="sxs-lookup"><span data-stu-id="595b5-118">You need to use Windows APIs that are not supported by .NET Core.</span></span>

- <span data-ttu-id="595b5-119">您需要使用的協力廠商 .NET 程式庫或 NuGet 套件不適用 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="595b5-119">You need to use third-party .NET libraries or NuGet packages that are not available for .NET Core.</span></span>

<span data-ttu-id="595b5-120">在 Docker 上使用 .NET Framework 可藉由將部署問題降至最低來改善您的部署體驗。</span><span class="sxs-lookup"><span data-stu-id="595b5-120">Using .NET Framework on Docker can improve your deployment experiences by minimizing deployment issues.</span></span> <span data-ttu-id="595b5-121">這項[「隨即轉移」案例](https://aka.ms/liftandshiftwithcontainersebook)對容器化原本使用傳統 .NET Framework (例如 ASP.NET WebForm、MVC Web 應用程式或 WCF (Windows Communication Foundation) 服務) 開發的舊版應用程式來說非常重要。</span><span class="sxs-lookup"><span data-stu-id="595b5-121">This ["lift and shift" scenario](https://aka.ms/liftandshiftwithcontainersebook) is important for containerizing legacy applications that were originally developed with the traditional .NET Framework, like ASP.NET WebForms, MVC web apps or WCF (Windows Communication Foundation) services.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="595b5-122">其他資源</span><span class="sxs-lookup"><span data-stu-id="595b5-122">Additional resources</span></span>

- <span data-ttu-id="595b5-123">**電子書：使用 Azure 和 Windows 容器將現有的 .NET Framework 應用程式現代化**</span><span class="sxs-lookup"><span data-stu-id="595b5-123">**E-book: Modernize existing .NET Framework applications with Azure and Windows Containers**</span></span>  
    <https://aka.ms/liftandshiftwithcontainersebook>

- <span data-ttu-id="595b5-124">**應用程式範例：使用 Windows 容器現代化舊版 ASP.NET Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="595b5-124">**Sample apps: Modernization of legacy ASP.NET web apps by using Windows Containers**</span></span>  
    <https://aka.ms/eshopmodernizing>

>[!div class="step-by-step"]
><span data-ttu-id="595b5-125">[上一個](index.md) 
>[下一步](net-core-container-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="595b5-125">[Previous](index.md)
[Next](net-core-container-scenarios.md)</span></span>
