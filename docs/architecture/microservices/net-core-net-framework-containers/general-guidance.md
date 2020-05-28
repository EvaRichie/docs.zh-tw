---
title: 一般方針
description: 容器化 .NET 應用程式的 .NET 微服務架構 | 一般指引
ms.date: 09/11/2018
ms.openlocfilehash: e3bb4b8cf3e371c31d783fe4cfafeac282fb72b8
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144561"
---
# <a name="general-guidance"></a>一般方針

本節提供了何時應選擇 .NET Core 或 .NET Framework 的摘要。 我們在後續的章節中提供了更多關於這些選擇的詳細資料。

您應該在下列情況下針對您的容器化 Docker 伺服器應用程式使用 .NET Core，並搭配 Linux 或 Windows 容器：

- 您有跨平台需求。 例如，當您想要同時使用 Linux 和 Windows 容器時。

- 您的應用程式架構是以微服務作為基礎的。

- 您需要快速啟動容器，並且想要每個容器僅具有極小的使用量，以達到更佳的密度，或在每個硬體單位上擁有更多容器，以降低您的成本。

簡而言之，當您建立新的容器化 .NET 應用程式時，您便應考慮使用 .NET Core 作為預設選擇。 它具有許多優點，並且最符合容器原理和工作樣式。

使用 .NET Core 的另一個優點便是您可以在相同的電腦上針對應用程式執行並存的 .NET 版本。 這項優點對不使用容器的伺服器或 VM 來說更為重要，因為容器會隔離應用程式需要的 .NET 版本。 (只要他們與基礎 OS 相容。)

在下列情況下，您應為容器化 Docker 伺服器應用程式使用 .NET Framework：

- 您的應用程式目前使用的是 .NET Framework，並且對 Windows 具有強烈的相依性。

- 您需要使用 .NET Core 不支援的 Windows API。

- 您需要使用的協力廠商 .NET 程式庫或 NuGet 套件不適用 .NET Core。

在 Docker 上使用 .NET Framework 可藉由將部署問題降至最低來改善您的部署體驗。 這項[「隨即轉移」案例](https://aka.ms/liftandshiftwithcontainersebook)對容器化原本使用傳統 .NET Framework (例如 ASP.NET WebForm、MVC Web 應用程式或 WCF (Windows Communication Foundation) 服務) 開發的舊版應用程式來說非常重要。

### <a name="additional-resources"></a>其他資源

- **電子書：使用 Azure 和 Windows 容器將現有的 .NET Framework 應用程式現代化**  
    <https://aka.ms/liftandshiftwithcontainersebook>

- **應用程式範例：使用 Windows 容器現代化舊版 ASP.NET Web 應用程式**  
    <https://aka.ms/eshopmodernizing>

>[!div class="step-by-step"]
>[上一個](index.md) 
>[下一步](net-core-container-scenarios.md)
