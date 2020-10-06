---
title: .NET API 分析器
description: 了解「.NET API 分析器」如何協助偵測已被取代的 API 及平台相容性問題。
author: oliag
ms.date: 02/20/2020
ms.technology: dotnet-standard
ms.openlocfilehash: a689ae347efbc8c2dd933b2f6920ac6cc06cda7d
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756191"
---
# <a name="net-api-analyzer"></a>.NET API 分析器

「.NET API 分析器」是一個 Roslyn 分析器，可探索不同平台上 C# API 的潛在相容性風險，並偵測對已被取代之 API 的呼叫。 對於任何開發階段的所有 C# 開發人員來說，都是相當實用的工具。

「API 分析器」是以 NuGet 套件 [Microsoft.DotNet.Analyzers.Compatibility](https://www.nuget.org/packages/Microsoft.DotNet.Analyzers.Compatibility/) 的形式提供。 在您於專案中參考它之後，它就會自動監視程式碼並指出有問題的 API 使用情況。 您也可以按一下燈泡圖示來取得可能之修正的相關建議。 下拉式功能表中有包含隱藏警告的選項。

> [!NOTE]
> .NET API 分析器目前仍然是發行前版本。

## <a name="prerequisites"></a>必要條件

- Visual Studio 2017 及更新版本，或 Visual Studio for Mac (所有版本)。

## <a name="discover-deprecated-apis"></a>探索已淘汰的 Api

### <a name="what-are-deprecated-apis"></a>什麼是已被取代的 API？

.NET 系列是一組不斷升級來更加滿足客戶需求的大型產品。 很自然地會淘汰一些 API 並以新的 API 取而代之。 當一個 API 有更好的替代方案存在時，即可視為被取代。 其中一個通知使用者某個 API 已被取代而不應使用的方式，就是使用 <xref:System.ObsoleteAttribute> 屬性來標示它。 此方法的缺點是所有已淘汰的 API 只有一個診斷識別碼 (就 C# 而言為 [CS0612](../../csharp/misc/cs0612.md))。 這表示：

- 無法讓每個案例都有專用的文件。
- 無法隱藏特定類別的警告。 您可以隱藏所有警告或全部不隱藏。
- 若要通知使用者有新的取代項目，就必須更新參考的組件或目標套件。

「API 分析器」會使用 API 特定的錯誤碼，其開頭為 DE (代表 Deprecation Error，即「取代錯誤」)，可用來控制個別警示的顯示。 [dotnet/platform-compat](https://github.com/dotnet/platform-compat) \(英文\) 存放庫中定義了分析器所識別的已被取代 API。

### <a name="add-the-api-analyzer-to-your-project"></a>將 API 分析器新增至您的專案

1. 開啟 Visual Studio。
2. 開啟您想要執行分析器的專案。
3. 在 **方案總管**中，以滑鼠右鍵按一下您的專案，然後選擇 [ **管理 NuGet 套件**]。 (這個選項也可以在 [專案]**** 功能表中取得)。
4. 在 [NuGet 封裝管理員] 索引標籤上：
   1. 選取 "nuget.org" 作為套件來源。
   2. 移至 [ **流覽** ] 索引標籤。
   3. 選取 [包括發行前版本]****。
   4. 搜尋 **DotNet 的相容性**。
   5. 在清單中選取該套件。
   6. 選取 [安裝]**** 按鈕。
   7. 在 [預覽變更]**** 對話方塊上，選取 [確定]**** 按鈕，然後在 [授權接受]**** 對話方塊上，如果您同意所列套件的授權條款，請選取 [我接受]****。

### <a name="use-the-api-analyzer"></a>使用 API 分析器

當程式碼中使用已被取代的 API (例如 <xref:System.Net.WebClient>) 時，「API 分析器」會使用綠色曲線來醒目標示它。 當您將滑鼠游標暫留在該 API 呼叫上時，會顯示燈泡圖示及有關該 API 取代的資訊，如以下範例所示：

![以綠色波浪線和左邊燈泡的 WebClient API 螢幕擷取畫面。](media/api-analyzer/green-squiggle.jpg)

[錯誤清單]**** 視窗會包含警告，其中每個已被取代的 API 都會有一個唯一識別碼 ，如以下範例所示 (`DE004`)：

![顯示警告識別碼和描述的 [錯誤清單] 視窗螢幕擷取畫面。](media/api-analyzer/warnings-id-and-descriptions.jpg "包含警告的 [錯誤清單] 視窗。")

藉由按一下識別碼，您便可以前往含有詳細資訊的網頁，當中會說明 API 被取代的原因，並提供有關可使用之替代 API 的建議。

以滑鼠右鍵按一下反白顯示的成員，然後選取 [**隱藏 \<diagnostic ID> **]，即可隱藏任何警告。 有兩種隱藏警告的方式：

- [本機 (在原始程式檔中)](#suppress-warnings-locally)
- [全域 (在隱藏項目檔中)](#suppress-warnings-globally) - 建議使用

### <a name="suppress-warnings-locally"></a>在本機隱藏警告

若要在本機隱藏警告，請在您想要隱藏警告的成員上按一下滑鼠右鍵，然後選取 [**快速動作] 和 [重構**  >  隱藏來源中的***診斷識別碼* \<diagnostic ID> **]  >  ** **。 [#Pragma](../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md)警告預處理器指示詞會新增至您在定義範圍中的原始程式碼：已 ![ 停用 #pragma 警告的程式碼螢幕擷取畫面。](media/api-analyzer/suppress-in-source.jpg)

### <a name="suppress-warnings-globally"></a>全域隱藏警告

若要全域隱藏警告，請在您想要隱藏警告的成員上按一下滑鼠右鍵，然後選取 [**快速動作] 和 [重構**隱藏隱藏專案檔中的  >  ***診斷識別碼* \<diagnostic ID> **]  >  ** **。

![滑鼠右鍵功能表的螢幕擷取畫面，其中顯示在 Visual Studio 中隱藏警告的選項。](media/api-analyzer/suppress-in-sup-file.jpg)

*GlobalSuppressions.cs* 檔案會在第一次隱藏之後新增到您的專案中。 新的全域隱藏會附加到這個檔案。

![方案總管中 GlobalSuppressions.cs 檔案的螢幕擷取畫面。](media/api-analyzer/suppression-file.jpg)

全域隱藏式建議的使用方式，可確保所有專案的 API 使用方式一致。

## <a name="discover-cross-platform-issues"></a>探索跨平臺問題

> [!NOTE]
> .NET 5.0 引進了 [平臺相容性分析器](platform-compat-analyzer.md) 來取代這項功能。 平臺相容性分析器隨附于 .NET SDK (不需要個別安裝) 且預設為開啟。

與已被取代的 API 類似，分析器會識別所有不是跨平台的 API。 例如，<xref:System.Console.WindowWidth?displayProperty=nameWithType>可在 Windows 上運作，但無法在 Linux 和 macOS 上運作。 診斷識別碼會顯示在 [錯誤清單]**** 視窗中。 您可以按一下滑鼠右鍵並選取 [快速動作與重構]**** 來隱藏該警示。 與有兩個選項 (繼續使用已被取代的成員並隱藏警告，或完全不使用它) 的取代案例不同，在這裡，如果您僅針對特定平台來開發程式碼，就可以隱藏您不打算用來執行程式碼之所有其他平台的所有警告。 若要這樣做，您只需編輯專案檔，然後新增 `PlatformCompatIgnore` 屬性來列出所有要忽略的平台即可。 接受的值包括：`Linux`、`macOS` 及 `Windows`。

```xml
<PropertyGroup>
    <PlatformCompatIgnore>Linux;macOS</PlatformCompatIgnore>
</PropertyGroup>
```

如果您的程式碼以多個平台為目標，而您想要利用其中某些平台所不支援的 API，就可以使用 `if` 陳述式來保護該部分的程式碼：

```csharp
if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
{
     var w = Console.WindowWidth;
     // More code
}
```

您也可以有條件地依目標架構/作業系統進行編譯，但目前必須以[手動方式](../frameworks.md#how-to-specify-a-target-framework)執行。

## <a name="supported-diagnostics"></a>支援的診斷

目前，分析器可處理下列情況：

- 使用擲回 <xref:System.PlatformNotSupportedException> 的 .NET Standard API (PC001)。
- 使用 .NET Framework 4.6.1 上未提供的.NET Standard API (PC002)。
- 使用 UWP 中不存在的原生 API (PC003) 。
- Delegate.BeginInvoke 及 EndInvoke API 的使用方式 (PC004)。
- 使用標示為已被取代的 API (DEXXXX)。

## <a name="ci-machine"></a>CI 電腦

所有這些診斷不僅在 IDE 中有提供，在組建專案過程中的命令列上也有提供，其中包括 CI 伺服器。

## <a name="configuration"></a>組態

使用者可決定診斷的處理方式：視為警告、錯誤、建議，或將其關閉。 例如，如果您是架構設計人員，就可以決定應將相容性問題視為錯誤，讓對一些已被取代之 API 的呼叫產生警告，而其他則只產生建議。 您可以依診斷識別碼及依專案分別進行此設定。 若要這樣做，請在 [方案總管]**** 中，瀏覽至您專案底下的 [相依性]**** 節點。 展開 [節點**Dependencies**相依  >  性**分析器**]  >  **DotNet**。 在診斷識別碼上按一下滑鼠右鍵，選取 [ **設定規則集嚴重性**]，然後選取所需的選項。

![方案總管的螢幕擷取畫面，顯示具有規則集嚴重性的診斷和快顯對話方塊。](media/api-analyzer/disable-notifications.jpg)

## <a name="see-also"></a>另請參閱

- [API 分析器簡介](https://devblogs.microsoft.com/dotnet/introducing-api-analyzer/) \(英文\) 部落格文章。
- YouTube 上的 [API 分析器](https://youtu.be/eeBEahYXGd0)示範影片。
- [平臺相容性分析器](platform-compat-analyzer.md)
