---
title: 設計 Docker 應用程式
description: 您可以在這裡找到微服務架構深入指南的參考資料，因為本指南並未詳細說明該主題。
ms.date: 08/06/2020
ms.openlocfilehash: b63d4344abb358a393587bdacf91f6091b531af0
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87915983"
---
# <a name="design-docker-applications"></a><span data-ttu-id="bfb12-103">設計 Docker 應用程式</span><span class="sxs-lookup"><span data-stu-id="bfb12-103">Design Docker applications</span></span>

<span data-ttu-id="bfb12-104">第 1 章介紹有關容器和 Docker 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="bfb12-104">Chapter 1 introduced the fundamental concepts regarding containers and Docker.</span></span> <span data-ttu-id="bfb12-105">該資訊是您開始所需的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="bfb12-105">That information is the basic level of information you need to get started.</span></span> <span data-ttu-id="bfb12-106">但企業應用程式可能很複雜，且是由多個服務而不是單一服務或容器所組成。</span><span class="sxs-lookup"><span data-stu-id="bfb12-106">But, enterprise applications can be complex and composed of multiple services instead of a single service or container.</span></span> <span data-ttu-id="bfb12-107">針對這些選擇性使用案例，您必須了解其他設計方法，例如服務導向架構 (SOA)，以及更進階的微服務概念和容器協調流程概念。</span><span class="sxs-lookup"><span data-stu-id="bfb12-107">For those optional use cases, you need to know additional approaches to design, such as Service-Oriented Architecture (SOA) and the more advanced microservices concepts and container orchestration concepts.</span></span> <span data-ttu-id="bfb12-108">本檔的範圍不限於微服務，而是任何 Docker 應用程式生命週期，因此不會深入探索微服務架構，因為您也可以使用容器和 Docker 搭配一般 SOA、背景工作或作業，甚至是整合型應用程式部署方法。</span><span class="sxs-lookup"><span data-stu-id="bfb12-108">The scope of this document is not limited to microservices but to any Docker application life cycle, therefore, it does not explore microservices architecture in depth because you can also use containers and Docker with regular SOA, background tasks or jobs, or even with monolithic application deployment approaches.</span></span>

<span data-ttu-id="bfb12-109">**詳細資訊**若要深入瞭解企業應用程式和微服務架構，請閱讀指南[NET 微服務：容器化 .Net 應用程式的架構](../../microservices/index.md)，您也可以從這裡下載 <https://aka.ms/MicroservicesEbook> 。</span><span class="sxs-lookup"><span data-stu-id="bfb12-109">**More info** To learn more about enterprise applications and microservices architecture in depth, read the guide [NET Microservices: Architecture for Containerized .NET Applications](../../microservices/index.md) that you can also download from <https://aka.ms/MicroservicesEbook>.</span></span>

<span data-ttu-id="bfb12-110">不過，在進入應用程式生命週期和 DevOps 之前，請務必瞭解您要如何設計和建立應用程式，以及您的設計選擇。</span><span class="sxs-lookup"><span data-stu-id="bfb12-110">However, before you get into the application life cycle and DevOps, it's important to know how you're going to design and construct your application and what are your design choices.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="bfb12-111">[上一個](index.md) 
>[下一步](common-container-design-principles.md)</span><span class="sxs-lookup"><span data-stu-id="bfb12-111">[Previous](index.md)
[Next](common-container-design-principles.md)</span></span>
