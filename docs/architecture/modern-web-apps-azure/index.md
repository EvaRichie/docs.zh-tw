---
title: 使用 ASP.NET Core 和 Azure 架構現代化 Web 應用程式
description: 本指南會提供使用 ASP.NET Core 和 Azure 建置整合型 Web 應用程式的端對端指引。
author: ardalis
ms.author: wiwagn
ms.date: 12/4/2019
ms.openlocfilehash: 8eebe9a8e530b244f4596adef1b5e6dd23e305bd
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144535"
---
# <a name="architect-modern-web-applications-with-aspnet-core-and-azure"></a>使用 ASP.NET Core 和 Azure 架構現代化 Web 應用程式

![架構現代化 Web 應用程式指南的書籍封面影像。](./media/index/web-application-guide-cover-image.png)

**版本 3.1** -更新為 ASP.NET Core 3。1

發行者

Microsoft 開發人員部門 .NET 和 Visual Studio 產品小組

Microsoft Corporation 部門

One Microsoft Way

Redmond, Washington 98052-6399

Microsoft Corporation 的著作權©2020

著作權所有，並保留一切權利。 本書內容的任何部分在未經過發行者書面許可下，不得以任何形式或透過任何方式進行重製或傳送。

本書依照「現況」提供，代表作者的觀點和意見。 本書中所述之觀點、意見與資訊 (包括 URL 及其他網際網路的網站參考) 如有變更，恕不另行通知。

此處描述的一些範例僅供說明之用，純屬虛構。 並未影射或關聯任何真實的人、事、物。

Microsoft 與列於 <https://www.microsoft.com>「商標」網頁的商標是 Microsoft 集團的商標。

Mac 與 macOS 是 Apple Inc. 的商標。

Docker whale 標誌是 Docker，Inc. 的注冊商標，由許可權使用。

所有其他商標和標誌屬於其各自擁有者的財產。

作者︰

> **Steve "ardalis" Smith** - 軟體架構設計人員和講師 - [Ardalis.com](https://ardalis.com)

編輯者：

> **Maira Wenzel**

## <a name="action-links"></a>動作連結

- 本電子書也提供 PDF 格式（僅限英文版）[下載](https://aka.ms/webappebook)

- 複製/派生[GitHub 上](https://github.com/dotnet-architecture/eShopOnWeb)的參考應用程式 eShopOnWeb

## <a name="introduction"></a>簡介

.NET Core 和 ASP.NET Core 提供許多優於傳統.NET 開發的優點。 如果下列部分或所有項目對應用程式成功而言十分重要，則您應該將 .NET Core 用於伺服器應用程式：

- 跨平台支援。

- 使用微服務。

- 使用 Docker 容器。

- 高效能和延展性需求。

- 相同伺服器上應用程式之 .NET 版本的並存版本控制。

傳統 .NET 應用程式可以並確實支援這些需求，但 ASP.NET Core 和 .NET Core 已最佳化可提供針對上述案例的改善支援。

越來越多的組織會選擇使用 Microsoft Azure 這類服務，以在雲端中裝載其 Web 應用程式。 如果下列對您的應用程式或組織十分重要，則您應該考慮將應用程式裝載在雲端中：

- 降低對資料中心成本的投資 (硬體、軟體、空間、公用程式、伺服器管理等等)

- 彈性定價 (根據使用量付費，而閒置容量不需付費)。

- 可靠性極高。

- 改善的應用程式行動性；輕鬆地變更您應用程式的部署位置和方式。

- 彈性容量；根據實際需求相應增加或減少。

使用 ASP.NET Core 建置 Web 應用程式 (且其裝載於 Azure) 提供許多比傳統替代項目更具競爭性的優點。 ASP.NET Core 已針對現代化 Web 應用程式開發做法和雲端裝載案例最佳化。 在本指南中，您將學習如何架構 ASP.NET Core 應用程式，以善加利用這些功能。

## <a name="purpose"></a>目的

本指南提供使用 ASP.NET Core 和*Azure 建立整合*型 web 應用程式的端對端指引。 此處的「整合型」是指這些應用程式會部署為單一單位，而不是互動服務和應用程式的集合。

本指南是[".Net 微服務" 的補充 _。容器化 .NET 應用程式的架構_](../microservices/index.md)」，著重在 Docker、微服務及部署容器以裝載企業應用程式。

### <a name="net-microservices-architecture-for-containerized-net-applications"></a>.NET 微服務。 容器化 .NET 應用程式的架構

- **電子書**  
  <https://aka.ms/MicroservicesEbook>
- **範例應用程式**  
  <https://aka.ms/microservicesarchitecture>

## <a name="who-should-use-this-guide"></a>誰應該使用本指南

本指南的對象主要是開發人員、開發負責人和架構設計人員，而他們對使用 Microsoft 技術和服務在雲端中建置現代化 Web 應用程式感興趣。

次要對象是技術決策者，其已熟悉 ASP.NET 或 Azure，並尋找是否可以升級為新專案或現有專案之 ASP.NET Core 的相關資訊。

## <a name="how-you-can-use-this-guide"></a>此指南的使用方式

本指南已壓縮成一個相對較小的檔，著重于使用現代化 .NET 技術和 Azure 來建立 web 應用程式。 因此，可以完整讀取它，以提供對這類應用程式和其技術考量的基礎了解。 本指南與其範例應用程式也可以作為起點或參考。 使用相關聯的範例應用程式作為您專屬應用程式的範本，或查看如何組織應用程式的元件組件。 當您要為專屬應用程式權衡這些選擇時，請回頭參考指南內架構和技術選項的原則與說明還有決策考量。

請隨意將本指南轉寄給您的小組，協助確保對這些考量和機會有共同的了解。 讓所有人都使用一組共用術語和基礎原則，有助確保套用一致的架構模式和做法。

## <a name="references"></a>參考資料

- **針對伺服器應用程式在 .NET Core 和 .NET Framework 之間進行選擇**  
  [https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server](../../standard/choosing-core-framework-server.md)

>[!div class="step-by-step"]
>[下一步](modern-web-applications-characteristics.md)
