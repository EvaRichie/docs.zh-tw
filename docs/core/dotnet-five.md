---
title: .NET 5 的新功能
description: 深入瞭解 .NET 5，這是一個跨平臺和開放原始碼的開發平臺，也就是 .NET Core 的下一次演進。
ms.date: 11/30/2020
ms.topic: overview
ms.author: dapine
author: IEvangelist
ms.openlocfilehash: 7984f235044db5dfc7533343e7d43cd7745fba33
ms.sourcegitcommit: 88fbb019b84c2d044d11fb4f6004aec07f2b25b1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2021
ms.locfileid: "97899451"
---
# <a name="whats-new-in-net-5"></a>.NET 5 的新功能

.NET 5.0 是下一個 .NET Core 的主要版本，之後是3.1。 我們將這個新版本的 .NET 5.0 （而不是 .NET Core 4.0）命名為以下兩個原因：

- 我們略過了版本號碼4.x，以避免與 .NET Framework 4.x 混淆。
- 我們從名稱中捨棄了「核心」，以強調這是未來的 .NET 主要實作為。 .NET 5.0 支援比 .NET Core 或 .NET Framework 更多類型的應用程式和平臺。

ASP.NET Core 5.0 是以 .NET 5.0 為基礎，但會保留 "Core" 的名稱，以避免與 ASP.NET MVC 5 混淆。 同樣地，Entity Framework Core 5.0 會保留 "Core" 的名稱，以避免與 Entity Framework 5 和6混淆。

相較于 .NET Core 3.1，.NET 5.0 包含下列改進功能和新功能：

- [C # 更新](#c-updates)
- [F # 更新](#f-updates)
- [Visual Basic 更新](#visual-basic-updates)
- [ 新功能的System.Text.Js](#systemtextjson-new-features)
- [單一檔案應用程式](deploying/single-file.md)
- [應用程式修剪](https://devblogs.microsoft.com/dotnet/app-trimming-in-net-5)
- Windows ARM64 和 ARM64 內建函式
- 傾印偵錯工具的工具支援
- 執行時間程式庫已針對可為[null 的參考型別](../csharp/nullable-references.md)標注80%
- 效能改進：
  - [垃圾收集 (GC) ](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5/#gc)
  - [System.Text.Json](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5/#json)
  - [System.Text.RegularExpressions](https://devblogs.microsoft.com/dotnet/regex-performance-improvements-in-net-5)
  - [非同步 ValueTask 共用](https://devblogs.microsoft.com/dotnet/async-valuetask-pooling-in-net-5)
  - [容器大小優化](https://github.com/dotnet/dotnet-docker/issues/1814#issuecomment-625294750)
  - [更多區域](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5)

## <a name="net-50-doesnt-replace-net-framework"></a>.NET 5.0 不會取代 .NET Framework

.NET 5.0 是未來的 .NET 的主要執行，而且仍支援 .NET Framework 4.x。

沒有將下列技術從 .NET Framework 移植到 .NET 5.0 的計畫，但 .NET 5.0 中有替代方案：

| 技術            | 建議的替代方案                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------|
| Web Form             | ASP.NET Core [Blazor](/aspnet/core/blazor) 或 [Razor Pages](/aspnet/core/tutorials/razor-pages) |
| Windows Workflow (WF)  | [開放原始碼 CoreWF](https://github.com/UiPath-Open/corewf) 或 [Elsa-工作流程](https://github.com/elsa-workflows/elsa-core) |

### <a name="windows-communication-foundation"></a>Windows Communication Foundation

只有在 Windows 上才支援 [Windows Communication Foundation (WCF) ](../framework/wcf/index.md) 的原始執行。 不過，.NET Foundation 有提供用戶端埠。 它是完全 [開放的原始](https://github.com/dotnet/wcf)碼、跨平臺，並受到 Microsoft 的支援。 核心 NuGet 套件如下所示：

- [System.ServiceModel.Duplex](https://www.nuget.org/packages/System.ServiceModel.Duplex)
- [System.servicemodel. 同盟](https://www.nuget.org/packages/System.ServiceModel.Federation)
- [System.ServiceModel.Http](https://www.nuget.org/packages/System.ServiceModel.Http)
- [System.ServiceModel.NetTcp](https://www.nuget.org/packages/System.ServiceModel.NetTcp)
- [System.ServiceModel.Primitives](https://www.nuget.org/packages/System.ServiceModel.Primitives)
- [System.servicemodel. 安全性](https://www.nuget.org/packages/System.ServiceModel.Security)

此社區會維護伺服器元件，以補充上述的用戶端程式庫。 您可以在 [CoreWCF](https://github.com/CoreWCF/CoreWCF)找到 GitHub 存放庫。 Microsoft _未_ 正式支援伺服器元件。 如需 WCF 的替代方案，請考慮 [gRPC](/aspnet/core/grpc)。

## <a name="net-50-doesnt-replace-net-standard"></a>.NET 5.0 不會取代 .NET Standard

新的應用程式開發可以 `net5.0` 針對所有專案類型（包括類別庫）指定目標 framework 標記 (TFM) 。 在 .NET 5 工作負載之間共用程式碼已經過簡化，您只需要 `net5.0` TFM。

針對 .NET 5.0 應用程式和程式庫， `net5.0` 目標 Framework 標記 (TFM) 結合和取代 `netcoreapp` 和 `netstandard` tfm。 但是，如果您打算在 .NET Framework、.NET Core 和 .NET 5 工作負載之間共用程式碼，您可以指定 `netstandard2.0` 為 TFM。 如需詳細資訊，請參閱 [.NET Standard](../standard/net-standard.md)。

## <a name="c-updates"></a>C # 更新

撰寫 .NET 5 應用程式的開發人員可以存取最新的 c # 版本和功能。 .NET 5 與 c # 9 配對，這對語言有許多新功能。 以下是一些重點：

- 記錄：具有以值為基礎之相等語義的參考型別，以及新運算式支援的非破壞性變化 `with` 。
- 關聯式模式比對：將模式比對功能延伸至關聯評估和運算式的關係運算子，包括邏輯模式-新的關鍵字 `and` 、 `or` 和 `not` 。
- 最上層語句：作為加速採用和學習 c # 的方法，您 `Main` 可以省略方法，並將應用程式視為有效，如下所示：

   ```csharp
   System.Console.Write("Hello world!");
   ```

- 函式指標：語言結構會公開下列中繼語言 (IL) 碼碼： `ldftn` 和 `calli` 。

如需可用 c # 9 功能的詳細資訊，請參閱 [c # 9 的新](../csharp/whats-new/csharp-9.md)功能。

### <a name="source-generators"></a>來源產生器

除了一些醒目提示的新 c # 功能之外，來源產生器也會將其轉換成開發人員專案。 來源產生器可讓在編譯期間執行的程式碼檢查您的程式，並產生與其余程式碼一起編譯的其他檔案。

如需來源產生器的詳細資訊，請參閱 [c # 來源](https://devblogs.microsoft.com/dotnet/introducing-c-source-generators) 產生器和 [c # 來源](https://devblogs.microsoft.com/dotnet/new-c-source-generator-samples)產生器範例簡介。

## <a name="f-updates"></a>F # 更新

F # 是 .NET 功能性程式設計語言，而在 .NET 5 中，開發人員可以存取 F # 5。 以下是 F # 5 的幾項新功能：

### <a name="interpolated-strings"></a>插入字串

類似于 c # 中的字串插值，甚至 JavaScript，F # 都支援基本的字串插補。

```fsharp
let name = "David"
let age = 36
let message = $"{name} is {age} years old."
```

除了基底字元串插補，還有具類型的插補。 使用具類型的插補時，指定的類型必須符合格式規範。

```fsharp
let name = "David"
let age = 36
let message = $"%s{name} is %d{age} years old."
```

這類似于 [`sprintf`](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-printfmodule.html#sprintf) 根據型別安全輸入來格式化字串的函式。 <!-- For more information, see [What's new in F# 5](fsharp/whats-new/fsharp-50.md). -->

## <a name="visual-basic-updates"></a>Visual Basic 更新

.NET 5 中沒有適用于 Visual Basic 的新語言功能。 不過，在 .NET 5 中，Visual Basic 支援延伸至：

| 描述                            | `dotnet new` 參數 |
|----------------------------------------|------------------------|
| 主控台應用程式                    | `console`              |
| 類別庫                          | `classlib`             |
| WPF 應用程式                        | `wpf`                  |
| WPF 類別庫                      | `wpflib`               |
| WPF 自訂控制項程式庫             | `wpfcustomcontrollib`  |
| WPF 使用者控制項程式庫               | `wpfusercontrollib`    |
| Windows Forms (WinForms) 應用程式   | `winforms`             |
| Windows Forms (WinForms) 類別庫 | `winformslib`          |
| 單元測試專案                      | `mstest`               |
| NUnit 3 測試專案                   | `nunit`                |
| NUnit 3 測試項目                      | `nunit-test`           |
| xUnit 測試專案                     | `xunit`                |

如需 .NET CLI 專案範本的詳細資訊，請參閱 [`dotnet new`](tools/dotnet-new.md) 。

## <a name="systemtextjson-new-features"></a>新功能的 System.Text.Json

和中有 [System.Text.Json](../standard/serialization/system-text-json-overview.md)的新功能：

- [保留參考並處理迴圈參考](../standard/serialization/system-text-json-preserve-references.md)
- [HttpClient 和 HttpContent 擴充方法](../standard/serialization/system-text-json-how-to.md#httpclient-and-httpcontent-extension-methods)
- [以引號允許或寫入數位](../standard/serialization/system-text-json-invalid-json.md#allow-or-write-numbers-in-quotes)
- [支援不可變的類型和 c # 9 記錄](../standard/serialization/system-text-json-immutability.md)
- [支援非公用屬性存取子](../standard/serialization/system-text-json-immutability.md)
- [支援欄位](../standard/serialization/system-text-json-how-to.md#include-fields)
- [有條件地忽略屬性](../standard/serialization/system-text-json-ignore-properties.md)
- [支援非字串索引鍵字典](../standard/serialization/system-text-json-migrate-from-newtonsoft-how-to.md#dictionary-with-non-string-key)
- [允許自訂轉換器處理 null](../standard/serialization/system-text-json-converters-how-to.md#handle-null-values)
- [複製 JsonSerializerOptions](../standard/serialization/system-text-json-configure-options.md#copy-jsonserializeroptions)
- [使用 web 預設值建立 JsonSerializerOptions](../standard/serialization/system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions)

## <a name="see-also"></a>請參閱

- [一個 .NET 的旅程](https://channel9.msdn.com/Events/Build/2020/BOD106)
- [.NET 5 的效能改進](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-5)
- [下載 .NET SDK](https://dotnet.microsoft.com/download)
