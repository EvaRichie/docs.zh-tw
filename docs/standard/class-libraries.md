---
title: .NET 類別庫
description: 了解 .NET 類別庫如何讓您將有用的功能分組成可供多個應用程式使用的模組。
author: richlander
ms.date: 06/20/2016
ms.assetid: a67484c3-fe92-44d8-8fa3-36fa2071d880
ms.openlocfilehash: bbf8d5fa44af931e39f2bf1344c13f9d9d9bfe05
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94823949"
---
# <a name="net-class-libraries"></a>.NET 類別庫

類別庫是 .NET 的[共用程式庫](https://en.wikipedia.org/wiki/Library_%28computing%29#Shared_libraries)概念。 它們可讓您將有用的功能設為可供多個應用程式使用的模組中的元件。 它們也可以作為一種方法，來載入應用程式啟動時不需要或未知的功能。 類別庫是使用 [.NET 組件檔案格式](assembly/file-format.md)進行描述。

您可以使用三種類型的類別庫：

* **平台特定** 類別庫可以存取指定平台中的所有 API (例如，.NET Framework、Xamarin iOS)，但是只能供將目標設為該平台的應用程式和程式庫使用。
* **可攜式** 類別庫可以存取 API 子集，並且可以供將目標設為多個平台的應用程式和程式庫使用。
* **.NET Standard** 類別庫會將平台特定和可攜式程式庫概念合併到提供兼具兩者的單一模型。

## <a name="platform-specific-class-libraries"></a>平台特定類別庫

平台特定程式庫會繫結至單一 .NET 實作 (例如 Windows 上的 .NET Framework)，因此對已知執行環境具有重大相依性。 這類環境會公開一組已知 API (.NET 和 OS API)，並維護和公開預期狀態 (例如，Windows 登錄)。

建立平臺特定程式庫的開發人員可以充分利用基礎平臺。 程式庫永遠只會在該指定平台上執行，這樣就不需要進行平台檢查或撰寫其他形式的條件式程式碼 (以多平台的單一來源程式碼為模數)。

平台特定程式庫已是 .NET Framework 的主要類別庫類型。 即使隨著其他 .NET 實作的出現，平台特定程式庫仍然會保有主控程式庫類型。

## <a name="portable-class-libraries"></a>可攜式類別庫

多個 .NET 實作支援可攜式程式庫。 它們仍然可以依賴已知的執行環境，不過，環境是一組實體 .NET 實作為交集所產生的綜合專案。 公開的 Api 和平臺假設是平臺特定程式庫可使用之功能的子集。

當您建立可攜式程式庫時，可以選擇平台組態。 平臺設定是一組您需要支援的平臺 (例如 .NET Framework 4.5 +、Windows Phone 8.0 +) 。 您選擇的平台越多，可以進行的 API 和平台假設就越少 (即最小公分母)。 這項特性一開始可能會令人困惑，因為人們通常認為「更好的」，但發現更支援的平臺會產生較少的可用 Api。

許多程式庫開發人員已從透過一個來源產生多個平台特定程式庫 (使用條件式編譯指示詞) 切換到可攜式程式庫。 有[數種方式](https://blog.stephencleary.com/2012/11/portable-class-library-enlightenment.html)，可以使用目前最廣泛接受的 bait-and-switch 技術來存取可攜式程式庫內的平台特定功能。

## <a name="net-standard-class-libraries"></a>.NET Standard 類別庫

.NET Standard 程式庫可以取代平台特定和可攜式程式庫概念。 就它們可以公開基礎平台 (沒有綜合平台或平台交集) 的所有功能這點而言，它們是平台特定的。 就它們可以在所有支援的平台上運作這點而言，它們是可攜式。

.NET Standard 會公開一組程式庫 _合約_。 .NET 實作必須完整支援或根本不支援每個協定。 因此，每個實作都支援一組 .NET Standard 協定。 必然結果是支援協定相依性的平台上支援每個 .NET Standard 類別庫。

.NET Standard 不會公開 .NET Framework 的整個功能 (也不會) 目標，不過它們會公開比便攜類別庫更多的 Api。 一段時間之後，就會新增更多 API。

下列平台支援 .NET Standard 類別庫：

* .NET Core
* .NET Framework
* Mono
* Xamarin.iOS, Xamarin.Mac, Xamarin.Android
* 通用 Windows 平台 (UWP)
* Windows
* Windows Phone
* Windows Phone Silverlight

如需詳細資訊，請參閱 [.NET Standard](net-standard.md)。

## <a name="mono-class-libraries"></a>Mono 類別庫

Mono 支援類別庫，包括上述三種類型的程式庫。 通常會看到 Mono (正確) 為 .NET Framework 的跨平臺執行。 在某種程度上，原因是平台特定 .NET Framework 程式庫可以在 Mono 執行階段上執行，而不需要進行修改或重新編譯。 在建立可攜式類別庫之前就具有這項特性，因此是啟用 .NET Framework 與 Mono 之間的二進位可攜性的明確選擇 (雖然只作用於一個方向)。
