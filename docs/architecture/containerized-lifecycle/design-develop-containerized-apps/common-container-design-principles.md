---
title: 一般容器設計準則
description: 了解良好容器設計的基本原則就是「容器應只裝載一個處理序」。
ms.date: 08/06/2020
ms.openlocfilehash: 7dcf4b4af3385a2a500c5bc16a889b56fa2c25d5
ms.sourcegitcommit: ef50c99928183a0bba75e07b9f22895cd4c480f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87916003"
---
# <a name="common-container-design-principles"></a>一般容器設計準則

在進展到開發程序之前，還有一些值得一提的容器使用方式基本概念。

## <a name="container-equals-a-process"></a>容器等於處理序

在容器模型中，容器代表單一處理序。 藉由將容器定義為處理序界限，您即可開始建立用來調整或批次關閉處理序的基本項目。 當您執行 Docker 容器時，您會看到 [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) 定義。 這會定義容器的處理序以及存留期。 當處理序完成時，容器生命週期即告結束。 有長時間執行的處理序 (例如網頁伺服器) 和存留較短的程序 (例如批次作業)，其可能會實作為 Microsoft Azure [WebJobs](https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/)。 如果處理序失敗，容器會結束並由 Orchestrator 接管。 如果您已指示協調器保留五個執行中的執行個體，但其中一個失敗，則協調器會建立另一個容器來取代失敗的處理序。 在批次工作中，處理序是透過參數來啟動。 當處理序完成時，工作即告完成。

有時候，您可能需要在單一容器中執行多個處理序。 在任何架構文件中，並沒有「絕不可能」或「一律如此」的情況。 在需要多個處理序的情況下，常見的模式是使用 [Supervisor](http://supervisord.org/)。

>[!div class="step-by-step"]
>[上一個](design-docker-applications.md) 
>[下一步](monolithic-applications.md)
