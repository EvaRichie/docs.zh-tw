---
title: 使用 .NET Native 編譯應用程式
ms.date: 03/30/2017
helpviewer_keywords:
- native compilation
- .NET and native code
- compilation with .NET Native
- .NET Native
- C# and native compilation
ms.assetid: 47cd5648-9469-4b1d-804c-43cc04384045
ms.openlocfilehash: 1f176e81905fe68c6d740a13240fe814659a7a59
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73128381"
---
# <a name="compiling-apps-with-net-native"></a>使用 .NET Native 編譯應用程式

.NET Native 是用來建立和部署 Windows 應用程式的先行編譯技術，隨附于 Visual Studio 2015 和更新版本中。 此工具可將以 Managed 程式碼 (C# 或 Visual Basic) 撰寫且目標為 .NET Framework 和 Windows 10 的應用程式發行版本自動編譯為機器碼。

一般而言，以 .NET Framework 為目標的應用程式會編譯成中繼語言 (IL)。 在執行階段，just-in-time (JIT) 編譯器會將 IL 轉譯成機器碼。 相反地，.NET Native 會將 Windows 應用程式直接編譯成機器碼。 對開發人員而言，這表示：

- 您的應用程式會功能機器碼的效能。 通常，效能會比第一次編譯到 IL，然後由 JIT 編譯程式編譯成機器碼的程式碼更上層。

- 您可以繼續以 C# 或 Visual Basic 進行程式設計。

- 您可以繼續利用 .NET Framework 所提供的資源，包括其類別庫、自動記憶體管理和記憶體回收，以及例外狀況處理。

對於您應用程式的使用者，.NET Native 提供下列優點：

- 針對大部分的應用程式和案例，更快速地執行執行時間。

- 針對大部分的應用程式和案例，啟動時間更快。

- 低部署和更新成本。

- 優化的應用程式記憶體使用量。

> [!IMPORTANT]
> 在大部分的應用程式和案例中，相較于編譯為 IL 或 NGEN 影像的應用程式，.NET Native 提供明顯更快的啟動時間和更佳的效能。 不過，您的結果可能會有所不同。 為確保您的應用程式已受益于 .NET Native 的效能增強功能，您應該比較其效能與應用程式的 non-.NET 原生版本。 如需詳細資訊，請參閱[效能會話總覽](https://docs.microsoft.com/visualstudio/profiling/performance-session-overview)。

但是 .NET Native 牽涉到一個以上的程式碼編譯。 它會將轉換 .NET Framework 應用程式建置和執行的方式。 尤其是：

- 在預先編譯期間，.NET Framework 的必要部分會以靜態方式連結到您的應用程式。 這樣可以讓應用程式以 .NET Framework 的 app-local 程式庫來執行，並且讓編譯器執行全域分析，以提供優異的效能。 如此一來，即使 .NET Framework 更新之後，應用程式還是一貫地會以更快的速度啟動。

- .NET Native 執行時間已針對靜態先行編譯進行優化，而在大部分的情況下，可提供優異的效能。 同時，它還保留了開發人員會覺得生產力極佳的核心反映功能。

- .NET Native 使用與 c + + 編譯器相同的後端，其已針對靜態先行編譯案例進行優化。

.NET Native 能夠將 c + + 的效能優勢帶給 managed 程式碼開發人員，因為它會在幕後使用與 c + + 相同或類似的工具，如下表所示。

||.NET Native|C++|
|-|----------------------------------------------------------------|-----------|
|程式庫|.NET Framework + Windows 執行階段|Win32 + Windows 執行階段|
|編譯器|UTC 最佳化編譯器|UTC 最佳化編譯器|
|已部署|可立即執行的二進位檔案|可立即執行的二進位檔案 (ASM)|
|執行階段|MRT.dll (最小 CLR 執行階段)|CRT.dll (C 執行階段)|

針對適用於 Windows 10 的 Windows 應用程式，您要將應用程式封裝 (.appx 檔) 中的 .NET 機器碼編譯二進位檔上傳至 Windows 市集。

## <a name="in-this-section"></a>本節內容

如需有關使用 .NET 機器碼編譯來開發應用程式的詳細資訊，請參閱下列主題：

- [開始使用 .NET 機器碼編譯：開發人員經驗逐步解說](getting-started-with-net-native.md)

- [.NET 原生和編譯：](net-native-and-compilation.md) .NET 原生如何將您的專案編譯成原生程式碼。

- [反映和 .NET Native](reflection-and-net-native.md)

  - [依賴反映的 API](apis-that-rely-on-reflection.md)

  - [反映 API 參考](net-native-reflection-api-reference.md)

  - [執行階段指示詞 (rd.xml) 組態檔參考](runtime-directives-rd-xml-configuration-file-reference.md)

- [序列化和中繼資料](serialization-and-metadata.md)

- [將您的 Windows 市集應用程式移轉至 .NET Native](migrating-your-windows-store-app-to-net-native.md)

- [.NET Native 一般疑難排解](net-native-general-troubleshooting.md)
