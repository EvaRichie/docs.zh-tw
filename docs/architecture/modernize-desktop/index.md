---
title: 使用 .NET 5 在 Windows 10 上現代化桌面應用程式
description: 瞭解如何使用 .NET 5 將現有的桌面應用程式現代化
ms.date: 01/06/2021
ms.openlocfilehash: de8a451b0598b5eabd99028d377c161dace61623
ms.sourcegitcommit: 632818f4b527e5bf3c48fc04e0c7f3b4bdb8a248
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/20/2021
ms.locfileid: "98615696"
---
# <a name="modernizing-desktop-apps-on-windows-10-with-net-5"></a>使用 .NET 5 在 Windows 10 上現代化桌面應用程式

![顯示「現代化桌面應用程式」電子書封面的螢幕擷取畫面。](./media/modernizing-existing-desktop-apps-ebook-cover.png)

**版本 1.0.1** -更新至 .net 5

請參閱 [變更記錄](https://aka.ms/desktop-ebook-changelog) ，以取得書籍更新和社區貢獻。

發行者

Microsoft 開發人員部門 .NET 和 Visual Studio 產品小組

Microsoft Corporation 部門

One Microsoft Way

Redmond, Washington 98052-6399

Microsoft Corporation 的著作權©2021

著作權所有，並保留一切權利。 本書內容的任何部分在未經過發行者書面許可下，不得以任何形式或透過任何方式進行重製或傳送。

本書依照「現況」提供，代表作者的觀點和意見。 本書中所述之觀點、意見與資訊 (包括 URL 及其他網際網路的網站參考) 如有變更，恕不另行通知。

此處描述的一些範例僅供說明之用，純屬虛構。 並未影射或關聯任何真實的人、事、物。

Microsoft 與列於 <https://www.microsoft.com>「商標」網頁的商標是 Microsoft 集團的商標。

Mac 與 macOS 是 Apple Inc. 的商標。

所有其他商標和標誌屬於其各自擁有者的財產。

共同作者：

> **Olia Gavrysh**，Microsoft 的專案經理，.net 團隊

> **Miguel 天使 Castejón Dominguez**，創新架構設計師，Kabel

參與者和檢閱者：

> **Maira Wenzel**，Microsoft 資深專案經理，.net 團隊

> **Gorge**，資深內容開發人員，.net 檔團隊，Microsoft

> **Miguel Ramos**，Windows Developer Platform 團隊，Microsoft 的資深專案經理

> **Adam Braden**，首席程式經理，Windows Developer Platform 小組，Microsoft

> **Ricardo Minguez Pablos**，Microsoft Azure IoT 團隊資深專案經理

> **Nish Anil**，Microsoft 資深專案經理，.net 團隊

> Microsoft 資深產品行銷經理 **Beth Massi**

> **Scott Hunter**，合作夥伴總監計畫經理，.net 團隊，Microsoft

> **Marta Fuentes Lara**、Kabel

> **Raúl Fernández De Córdoba**、Kabel

> **Antonio Manuel Fernández Cantos**，Kabel

## <a name="introduction"></a>簡介

這本書是關於您可以採用的策略，以透過現代化的途徑來移動現有的桌面應用程式，並納入最新的執行時間、語言和平臺功能。 您會發現每個應用程式都不會有獨特的配方，因此您的需求和喜好設定。 好消息是，您可以套用一些常見的方法，將新的功能新增至您的應用程式。 其中有些甚至不需要修改程式碼。 在本書中，我們將說明這些功能在幕後的運作方式，並說明其執行的機制。 此外，您會發現一些常見的現代化桌面應用程式案例，讓您可以找到發展專案的靈感。

Microsoft 的現代化現有應用程式的方法，是讓您彈性地建立自己的自訂路徑。 本書中所述的所有現代化策略大多都是獨立的。 您可以選擇與您的應用程式相關的應用程式，並略過不重要的其他專案。 換句話說，您可以混搭策略，以最符合您應用程式需求的方式。

## <a name="who-should-use-the-book"></a>誰應該使用書

這本書適用于想要將現有的 Windows Forms 和 WPF 桌面應用程式現代化，以充分利用 .NET 和 Windows 10 的開發人員和解決方案架構設計人員。

如果您是技術決策者，例如企業架構設計人員或想要概述更新現有傳統型應用程式之優點的開發組長或主管，您可能也會覺得這本書很有用。

## <a name="how-to-use-the-book"></a>如何使用書

本書解決了「原因」，也就是您可能想要將現有應用程式現代化的原因，以及利用 NET 和 MSIX 讓桌面應用程式現代化的特定好處。 本書的內容是專為想要瞭解的架構設計人員和技術決策者所設計，但不需要專注于執行和技術的逐步詳細資料。

在不同的章節中，會提供範例程式碼程式碼片段和螢幕擷取畫面，其中第5章專門用來展示範例應用程式的完整遷移程式。

## <a name="what-this-book-doesnt-cover"></a>本書未涵蓋的內容

本書涵蓋了一組特定的案例，這些案例著重于隨即轉移案例，並概述在不需要重寫程式碼的情況下，獲得現代化優勢的方法。

這本書不是從頭開始使用 .NET 開發新式應用程式，或是開始使用 Windows Forms 和 WPF。 它著重于如何以最新的桌上型電腦開發技術來更新現有的桌面應用程式。

## <a name="samples-used-in-this-book"></a>本書中使用的範例

為了強調執行現代化的必要步驟，我們將使用名為的範例應用程式 `eShopModernizing` 。 此應用程式有兩種類別，Windows Forms 和 WPF，而我們將示範如何在這兩個 .NET 上執行現代化的逐步流程。

此外，您也可以在本書的 GitHub 存放庫中找到此程式的結果，如果您決定要遵循逐步教學課程，就可以參考此程式。

## <a name="send-your-feedback"></a>傳送您的意見反應

本書和相關的範例不斷演進，所以您的意見反應歡迎！ 如果您有關于如何改進本書的意見，請使用內建于 [GitHub 問題](https://github.com/dotnet/docs/issues)之任何頁面底部的意見反應區段。

>[!div class="step-by-step"]
>[下一步](why-modern-applications.md)
