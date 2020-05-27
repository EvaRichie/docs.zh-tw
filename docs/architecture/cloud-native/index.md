---
title: 架構適用于 Azure 的雲端原生 .NET 應用程式
description: 建立雲端原生應用程式的指南，利用 Azure 的容器、微服務和無伺服器功能。
author: ardalis
ms.date: 05/13/2020
ms.openlocfilehash: 196671468e56147f714078d1671f44af21bcf327
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/26/2020
ms.locfileid: "83840880"
---
# <a name="architecting-cloud-native-net-applications-for-azure"></a><span data-ttu-id="d1d2d-103">架構適用于 Azure 的雲端原生 .NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="d1d2d-103">Architecting Cloud Native .NET Applications for Azure</span></span>

![封面影像](./media/cover.png)

<span data-ttu-id="d1d2d-105">**版本 v1。0**</span><span class="sxs-lookup"><span data-stu-id="d1d2d-105">**EDITION v.1.0**</span></span>

<span data-ttu-id="d1d2d-106">發行者</span><span class="sxs-lookup"><span data-stu-id="d1d2d-106">PUBLISHED BY</span></span>

<span data-ttu-id="d1d2d-107">Microsoft 開發人員部門 .NET 和 Visual Studio 產品小組</span><span class="sxs-lookup"><span data-stu-id="d1d2d-107">Microsoft Developer Division, .NET, and Visual Studio product teams</span></span>

<span data-ttu-id="d1d2d-108">Microsoft Corporation 部門</span><span class="sxs-lookup"><span data-stu-id="d1d2d-108">A division of Microsoft Corporation</span></span>

<span data-ttu-id="d1d2d-109">One Microsoft Way</span><span class="sxs-lookup"><span data-stu-id="d1d2d-109">One Microsoft Way</span></span>

<span data-ttu-id="d1d2d-110">Redmond, Washington 98052-6399</span><span class="sxs-lookup"><span data-stu-id="d1d2d-110">Redmond, Washington 98052-6399</span></span>

<span data-ttu-id="d1d2d-111">&copy;Microsoft Corporation 的著作權2020</span><span class="sxs-lookup"><span data-stu-id="d1d2d-111">Copyright &copy; 2020 by Microsoft Corporation</span></span>

<span data-ttu-id="d1d2d-112">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-112">All rights reserved.</span></span> <span data-ttu-id="d1d2d-113">本書內容的任何部分在未經過發行者書面許可下，不得以任何形式或透過任何方式進行重製或傳送。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-113">No part of the contents of this book may be reproduced or transmitted in any form or by any means without the written permission of the publisher.</span></span>

<span data-ttu-id="d1d2d-114">本書依照「現況」提供，代表作者的觀點和意見。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-114">This book is provided "as-is" and expresses the author's views and opinions.</span></span> <span data-ttu-id="d1d2d-115">本書中所述之觀點、意見與資訊 (包括 URL 及其他網際網路的網站參考) 如有變更，恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-115">The views, opinions, and information expressed in this book, including URL and other Internet website references, may change without notice.</span></span>

<span data-ttu-id="d1d2d-116">此處描述的一些範例僅供說明之用，純屬虛構。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-116">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="d1d2d-117">並未影射或關聯任何真實的人、事、物。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-117">No real association or connection is intended or should be inferred.</span></span>

<span data-ttu-id="d1d2d-118">Microsoft 和列于「商標」網頁的商標 [https://www.microsoft.com](https://www.microsoft.com) 是 microsoft 公司集團的商標。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-118">Microsoft and the trademarks listed at [https://www.microsoft.com](https://www.microsoft.com) on the "Trademarks" webpage are trademarks of the Microsoft group of companies.</span></span>

<span data-ttu-id="d1d2d-119">Mac 與 macOS 是 Apple Inc. 的商標。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-119">Mac and macOS are trademarks of Apple Inc.</span></span>

<span data-ttu-id="d1d2d-120">Docker whale 標誌是 Docker，Inc. 的注冊商標，由許可權使用。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-120">The Docker whale logo is a registered trademark of Docker, Inc. Used by permission.</span></span>

<span data-ttu-id="d1d2d-121">所有其他商標和標誌屬於其各自擁有者的財產。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-121">All other marks and logos are property of their respective owners.</span></span>

<span data-ttu-id="d1d2d-122">作者：</span><span class="sxs-lookup"><span data-stu-id="d1d2d-122">Authors:</span></span>

> <span data-ttu-id="d1d2d-123">**Vettor**，首席雲端系統架構師/IP 架構師- [thinkingincloudnative.com](http://thinkingincloudnative.com/about/)，Microsoft</span><span class="sxs-lookup"><span data-stu-id="d1d2d-123">**Rob Vettor**, Principal Cloud System Architect/IP Architect - [thinkingincloudnative.com](http://thinkingincloudnative.com/about/), Microsoft</span></span>
>
> <span data-ttu-id="d1d2d-124">**Steve "ardalis" Smith**，軟體架構師和訓練人員- [Ardalis.com](https://ardalis.com)</span><span class="sxs-lookup"><span data-stu-id="d1d2d-124">**Steve "ardalis" Smith**, Software Architect and Trainer - [Ardalis.com](https://ardalis.com)</span></span>

<span data-ttu-id="d1d2d-125">參與者和審核者：</span><span class="sxs-lookup"><span data-stu-id="d1d2d-125">Participants and Reviewers:</span></span>

> <span data-ttu-id="d1d2d-126">**Cesar De La Torre**，首席計畫經理，.net 小組，Microsoft</span><span class="sxs-lookup"><span data-stu-id="d1d2d-126">**Cesar De la Torre**, Principal Program Manager, .NET team, Microsoft</span></span>
>
> <span data-ttu-id="d1d2d-127">**Nish Anil**，Microsoft 的資深計畫經理，.net 團隊</span><span class="sxs-lookup"><span data-stu-id="d1d2d-127">**Nish Anil**, Senior Program Manager, .NET team, Microsoft</span></span>
>
> <span data-ttu-id="d1d2d-128">**Jeremy Likness**，Microsoft 的資深計畫經理，.net 團隊</span><span class="sxs-lookup"><span data-stu-id="d1d2d-128">**Jeremy Likness**, Senior Program Manager, .NET team, Microsoft</span></span>
>
> <span data-ttu-id="d1d2d-129">Microsoft 資深雲端提倡者**Cecil Phillip**</span><span class="sxs-lookup"><span data-stu-id="d1d2d-129">**Cecil Phillip**, Senior Cloud Advocate, Microsoft</span></span>

<span data-ttu-id="d1d2d-130">編輯者：</span><span class="sxs-lookup"><span data-stu-id="d1d2d-130">Editors:</span></span>

> <span data-ttu-id="d1d2d-131">**Maira Wenzel**，Microsoft 的計畫經理，.net 團隊</span><span class="sxs-lookup"><span data-stu-id="d1d2d-131">**Maira Wenzel**, Program Manager, .NET team, Microsoft</span></span>

## <a name="version"></a><span data-ttu-id="d1d2d-132">版本</span><span class="sxs-lookup"><span data-stu-id="d1d2d-132">Version</span></span>

<span data-ttu-id="d1d2d-133">本指南的撰寫旨在涵蓋 **.Net core 3.1**版本，以及許多與 .net core 3.1 版本的相同「wave」技術（也就是 Azure 和其他協力廠商技術） coinciding 的其他相關更新。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-133">This guide has been written to cover **.NET Core 3.1** version along with many additional updates related to the same “wave” of technologies (that is, Azure and additional third-party technologies) coinciding in time with the .NET Core 3.1 release.</span></span>

## <a name="who-should-use-this-guide"></a><span data-ttu-id="d1d2d-134">誰應該使用本指南</span><span class="sxs-lookup"><span data-stu-id="d1d2d-134">Who should use this guide</span></span>

<span data-ttu-id="d1d2d-135">本指南的物件主要是開發人員、開發組長和架構設計人員，有興趣學習如何建立專為雲端設計的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-135">The audience for this guide is mainly developers, development leads, and architects who are interested in learning how to build applications designed for the cloud.</span></span>

<span data-ttu-id="d1d2d-136">次要物件是技術決策者，他們打算選擇是否要使用雲端原生方法來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-136">A secondary audience is technical decision-makers who plan to choose whether to build their applications using a cloud-native approach.</span></span>

## <a name="how-you-can-use-this-guide"></a><span data-ttu-id="d1d2d-137">此指南的使用方式</span><span class="sxs-lookup"><span data-stu-id="d1d2d-137">How you can use this guide</span></span>

<span data-ttu-id="d1d2d-138">本指南一開始會定義雲端原生，並介紹使用雲端原生原則和技術建立的參考應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-138">This guide begins by defining cloud native and introducing a reference application built using cloud-native principles and technologies.</span></span> <span data-ttu-id="d1d2d-139">除了這前兩個章節以外，本書的其餘部分會細分為著重于大部分雲端原生應用程式常見主題的特定章節。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-139">Beyond these first two chapters, the rest of the book is broken up into specific chapters focused on topics common to most cloud-native applications.</span></span> <span data-ttu-id="d1d2d-140">您可以跳至下列任一章節，以瞭解雲端原生方法：</span><span class="sxs-lookup"><span data-stu-id="d1d2d-140">You can jump to any of these chapters to learn about cloud-native approaches to:</span></span>

- <span data-ttu-id="d1d2d-141">資料和資料存取</span><span class="sxs-lookup"><span data-stu-id="d1d2d-141">Data and data access</span></span>
- <span data-ttu-id="d1d2d-142">通訊模式</span><span class="sxs-lookup"><span data-stu-id="d1d2d-142">Communication patterns</span></span>
- <span data-ttu-id="d1d2d-143">調整和擴充性</span><span class="sxs-lookup"><span data-stu-id="d1d2d-143">Scaling and scalability</span></span>
- <span data-ttu-id="d1d2d-144">應用程式復原</span><span class="sxs-lookup"><span data-stu-id="d1d2d-144">Application resiliency</span></span>
- <span data-ttu-id="d1d2d-145">監視與健康狀態</span><span class="sxs-lookup"><span data-stu-id="d1d2d-145">Monitoring and health</span></span>
- <span data-ttu-id="d1d2d-146">身分識別與安全性</span><span class="sxs-lookup"><span data-stu-id="d1d2d-146">Identity and security</span></span>
- <span data-ttu-id="d1d2d-147">DevOps</span><span class="sxs-lookup"><span data-stu-id="d1d2d-147">DevOps</span></span>

<span data-ttu-id="d1d2d-148">本指南以 PDF 形式和線上版本提供。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-148">This guide is available both in PDF form and online.</span></span> <span data-ttu-id="d1d2d-149">請隨意將本檔或其線上版本的連結轉寄給您的小組，以協助確保這些主題的一般瞭解。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-149">Feel free to forward this document or links to its online version to your team to help ensure common understanding of these topics.</span></span> <span data-ttu-id="d1d2d-150">大部分的主題都是以一致的方式瞭解基礎原則和模式，以及與這些主題相關的決策所牽涉到的取捨。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-150">Most of these topics benefit from a consistent understanding of the underlying principles and patterns, as well as the trade-offs involved in decisions related to these topics.</span></span> <span data-ttu-id="d1d2d-151">本檔的目標是要為小組及其領導者提供針對其應用程式架構、開發和裝載做出明智決策所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-151">Our goal with this document is to equip teams and their leaders with the information they need to make well-informed decisions for their applications' architecture, development, and hosting.</span></span>

## <a name="send-your-feedback"></a><span data-ttu-id="d1d2d-152">傳送您的意見反應</span><span class="sxs-lookup"><span data-stu-id="d1d2d-152">Send your feedback</span></span>

<span data-ttu-id="d1d2d-153">這本書與相關範例不斷演進，所以您的意見反應歡迎！</span><span class="sxs-lookup"><span data-stu-id="d1d2d-153">This book and related samples are constantly evolving, so your feedback is welcomed!</span></span> <span data-ttu-id="d1d2d-154">如果您有關于如何改進這本書的意見，請使用[GitHub 問題](https://github.com/dotnet/docs/issues)上任何網頁底部的 [意見反應] 區段。</span><span class="sxs-lookup"><span data-stu-id="d1d2d-154">If you have comments about how this book can be improved, use the feedback section at the bottom of any page built on [GitHub issues](https://github.com/dotnet/docs/issues).</span></span>

>[!div class="step-by-step"]
>[<span data-ttu-id="d1d2d-155">下一步</span><span class="sxs-lookup"><span data-stu-id="d1d2d-155">Next</span></span>](introduction.md)
