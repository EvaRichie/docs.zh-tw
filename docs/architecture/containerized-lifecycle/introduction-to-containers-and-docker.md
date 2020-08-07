---
title: 容器和 Docker 簡介
description: 取得使用 Docker 主要優點的高階概觀。
ms.date: 04/15/2020
ms.openlocfilehash: 79b4752ef4d2f0aa6199414aea5cf4ef357c86d3
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87915941"
---
# <a name="introduction-to-containers-and-docker"></a>容器和 Docker 簡介

*容器化是一種軟體發展方法，其中的應用程式或服務、其相依性和設定 (抽象化為部署資訊清單檔案，) 會封裝在一起做為容器映射。接著，您可以將容器化應用程式測試為一個單位，並將其部署為主機作業系統 (OS) 的容器映射實例。*

就像是貨櫃允許利用船隻、火車或貨車運輸貨物，而不論內含哪種貨物，軟體容器是軟體部署的標準單位，可包含不同的程式碼和相依性。 以此方式容器化軟體可讓開發人員和 IT 專業人員只需要一點修改或不需要任何修改，就能跨環境進行部署。

容器也可讓不同的應用程式在共用 OS 上彼此隔離。 容器化應用程式會在容器主機上執行，再於 OS (Linux 或 Windows) 上執行。 因此，容器所需磁碟使用量小於虛擬機器 (VM) 映像。

每個容器可以執行整個 Web 應用程式或服務，如圖 1-1 所示。 在此範例中，Docker 主機是容器主機，而 App1、App2、Svc1 及 Svc2 是容器化應用程式或服務。

![此圖顯示在 VM 或伺服器中執行的四個容器。](./media/introduction-to-containers-and-docker/multiple-containers-single-host.png)

**圖 1-1**。 在容器主機上執行的多個容器

您可以從容器化衍生的另一個優點是延展性。 您可以針對短期工作建立新的容器，以更快擴充。 從應用程式的觀點來看，具現化映像 (建立容器) 類似於具現化處理序 (例如服務或 Web 應用程式)。 不過，為了可靠起見，當您在多部主機伺服器之間執行相同映像的多個執行個體時，您通常需要在不同的主機伺服器或 VM 中，或是不同的容錯網域中，執行各個容器 (映像執行個體)。

簡單來說，容器在整個應用程式生命週期工作流程中，提供隔離、可攜性、彈性、延展性和控制能力等優點。 最重要的優點是可為開發與作業提供環境隔離。

>[!div class="step-by-step"]
>[上一個](index.md) 
>[下一步](what-is-docker.md)
