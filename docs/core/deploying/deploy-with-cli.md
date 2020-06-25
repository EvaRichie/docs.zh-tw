---
title: 使用 .NET Core CLI 發佈應用程式
description: 瞭解如何使用 .NET Core CLI 命令發佈 .NET Core 應用程式。
author: adegeo
ms.author: adegeo
ms.date: 12/12/2019
dev_langs:
- csharp
- vb
ms.openlocfilehash: a592b397d1ffee5b224638a8d17ce6fa9e44eea2
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325019"
---
# <a name="publish-net-core-apps-with-the-net-core-cli"></a>使用 .NET Core CLI 發佈 .NET Core 應用程式

本文示範如何從命令列發佈 .NET Core 應用程式。 .NET Core 提供三種發佈應用程式的方式。 Framework 相依部署會產生跨平台的 .dll 檔案，以使用本機安裝的 .NET Core 執行階段。 Framework 相依可執行檔會產生平台特定的可執行檔，來使用本機安裝的 .NET Core 執行階段。 獨立式可執行檔則會產生平台特定的可執行檔，並包含 .NET Core 執行階段的本機複本。

如需這些發佈模式的概觀，請參閱 [.NET Core 應用程式部署](index.md)。

需要一些使用 CLI 的快速說明嗎？ 下表顯示一些如何發佈應用程式的範例。 您可以使用 `-f <TFM>` 參數或藉由編輯專案檔來指定目標 Framework。 如需詳細資訊，請參閱[發佈基本概念](#publishing-basics)。

| 發佈模式 | SDK 版本 | 命令 |
| ------------ | ----------- | ------- |
| 與 Framework 相依的部署 | 2.x | `dotnet publish -c Release` |
| Framework 相依可執行檔 | 2.2 | `dotnet publish -c Release -r <RID> --self-contained false` |
|                                | 3.0 | `dotnet publish -c Release -r <RID> --self-contained false` |
|                                | 3.0* | `dotnet publish -c Release` |
| 自封式部署      | 2.1 | `dotnet publish -c Release -r <RID> --self-contained true` |
|                                | 2.2 | `dotnet publish -c Release -r <RID> --self-contained true` |
|                                | 3.0 | `dotnet publish -c Release -r <RID> --self-contained true` |

\* 使用 SDK 3.0 版時，相依於架構的可執行檔是執行基本 `dotnet publish` 命令時的預設發佈模式。 這只適用於以 **.NET Core 2.1** 或 **.NET Core 3.0** 為目標的專案。

## <a name="publishing-basics"></a>發佈基本概念

專案檔的 `<TargetFramework>` 設定會指定發佈應用程式時的預設目標 Framework。 您可以將目標 Framework 變更為任何有效的[目標 Framework Moniker (TFM)](../../standard/frameworks.md)。 例如，如果您的專案使用 `<TargetFramework>netcoreapp2.2</TargetFramework>`，就會建立以 .NET Core 2.2 為目標的二進位檔。 此設定中指定的 TFM 是命令使用的預設目標 [`dotnet publish`](../tools/dotnet-publish.md) 。

如果您想要以多個 Framework 為目標，則可以將 `<TargetFrameworks>` 設定設為以分號隔開的多個 TFM 值。 您可以使用 `dotnet publish -f <TFM>` 命令來發佈其中一個 Framework。 例如，如果您的專案具有 `<TargetFrameworks>netcoreapp2.1;netcoreapp2.2</TargetFrameworks>` 並執行 `dotnet publish -f netcoreapp2.1`，就會建立以 .NET Core 2.1 為目標的二進位檔。

除非另有設定，否則命令的輸出目錄 [`dotnet publish`](../tools/dotnet-publish.md) 為 `./bin/<BUILD-CONFIGURATION>/<TFM>/publish/` 。 除非使用 `-c` 參數加以變更，否則預設的**組建組態**模式為 [偵錯]****。 例如，`dotnet publish -c Release -f netcoreapp2.1` 會發佈至 `myfolder/bin/Release/netcoreapp2.1/publish/`。

如果您使用 .NET Core SDK 3.0 或更新版本，則以 .NET Core 版本2.1、2.2、3.0 或更新版本為目標之應用程式的預設發行模式是與 framework 相依的可執行檔。

如果您使用 .NET Core SDK 2.1，則以 .NET Core 2.1 和2.2 版為目標之應用程式的預設發行模式就是與 framework 相依的部署。

### <a name="native-dependencies"></a>原生相依性

如果您的應用程式具有原生相依性，它可能無法在不同的作業系統上執行。 例如，如果您的應用程式使用原生 Windows API，它就不會在 macOS 或 Linux 上執行。 您必須提供平台特定程式碼，並為每個平台編譯可執行檔。

另外，請考慮如果您參考的程式庫具有原生相依性，您的應用程式可能無法在每個平台上執行。 不過，您參考的 NuGet 套件可能包含了平台特定版本，以便為您處理必要的原生相依性。

散發具有原生相依性的應用程式時，您可能需要使用 `dotnet publish -r <RID>` 參數來指定想要為其發佈的目標平台。 如需執行階段識別碼清單，請參閱[執行階段識別碼 (RID) 目錄](../rid-catalog.md)。

平台特定二進位檔的詳細資訊涵蓋在 [Framework 相依可執行檔](#framework-dependent-executable)和[獨立式部署](#self-contained-deployment)章節中。

## <a name="sample-app"></a>範例應用程式

您可以使用下列應用程式來流覽發佈命令。 在終端機中執行下列命令即可建立此應用程式：

```dotnetcli
mkdir apptest1
cd apptest1
dotnet new console
dotnet add package Figgle
```

主控台範本所產生的 `Program.cs` 或 `Program.vb` 檔案必須變更如下：

```csharp
using System;

namespace apptest1
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(Figgle.FiggleFonts.Standard.Render("Hello, World!"));
        }
    }
}
```

```vb
Module Program
    Sub Main(args As String())
        Console.WriteLine(Figgle.FiggleFonts.Standard.Render("Hello, World!"))
    End Sub
End Module
```

當您執行應用程式（ [`dotnet run`](../tools/dotnet-run.md) ）時，會顯示下列輸出：

```terminal
  _   _      _ _         __        __         _     _ _
 | | | | ___| | | ___    \ \      / /__  _ __| | __| | |
 | |_| |/ _ \ | |/ _ \    \ \ /\ / / _ \| '__| |/ _` | |
 |  _  |  __/ | | (_) |    \ V  V / (_) | |  | | (_| |_|
 |_| |_|\___|_|_|\___( )    \_/\_/ \___/|_|  |_|\__,_(_)
                     |/
```

## <a name="framework-dependent-deployment"></a>與 Framework 相依的部署

若為 .NET Core SDK 2.x CLI，Framework 相依部署 (FDD) 是基本 `dotnet publish` 命令的預設模式。

當您將應用程式發佈為 FDD 時，就會在 `./bin/<BUILD-CONFIGURATION>/<TFM>/publish/` 資料夾中建立 `<PROJECT-NAME>.dll` 檔案。 若要執行您的應用程式，請巡覽至輸出資料夾，並使用 `dotnet <PROJECT-NAME>.dll` 命令。

您的應用程式會設定為以 .NET Core 特定版本為目標。 該目標 .NET Core 執行時間必須位於您的應用程式執行所在的任何電腦上。 例如，如果您的應用程式以 .NET Core 2.2 為目標，則應用程式執行所在的任何電腦都必須已安裝 .NET Core 2.2 執行階段。 依照[發佈基本概念](#publishing-basics)一節中所述，您可以編輯專案檔來變更預設的目標 Framework，或以多個 Framework 為目標。

發佈 FDD 會建立一個應用程式，以自動向前復原到應用程式執行所在系統上可用的最新 .NET Core 安全性修補程式。 如需編譯時期版本繫結的詳細資訊，請參閱[選取要使用的 .NET Core 版本](../versions/selection.md#framework-dependent-apps-roll-forward)。

## <a name="framework-dependent-executable"></a>Framework 相依可執行檔

針對 .NET Core SDK 3.x CLI，與 framework 相依的可執行檔（FDE）是基本命令的預設模式 `dotnet publish` 。 您不需要指定任何其他參數，只要您想要以目前的作業系統為目標。

在此模式中，將會建立平台特定可執行檔主機來裝載您的跨平台應用程式。 此模式類似于 FDD，因為 FDD 需要命令形式的主機 `dotnet` 。 主機可執行檔檔案名會因平臺而異，並命名為類似的內容 `<PROJECT-FILE>.exe` 。 您可以直接執行此可執行檔，而不是呼叫 `dotnet <PROJECT-FILE>.dll` ，這仍然是執行應用程式的可接受方式。

您的應用程式會設定為以 .NET Core 特定版本為目標。 該目標 .NET Core 執行時間必須位於您的應用程式執行所在的任何電腦上。 例如，如果您的應用程式以 .NET Core 2.2 為目標，則應用程式執行所在的任何電腦都必須已安裝 .NET Core 2.2 執行階段。 依照[發佈基本概念](#publishing-basics)一節中所述，您可以編輯專案檔來變更預設的目標 Framework，或以多個 Framework 為目標。

發佈 FDE 會建立一個應用程式，以自動向前復原到應用程式執行所在系統上可用的最新 .NET Core 安全性修補程式。 如需編譯時期版本繫結的詳細資訊，請參閱[選取要使用的 .NET Core 版本](../versions/selection.md#framework-dependent-apps-roll-forward)。

針對 .NET Core 2.2 和更早版本，您必須使用下列參數搭配 `dotnet publish` 命令來發佈 FDE：

- `-r <RID>` 此參數會使用識別碼 (RID) 來指定目標平台。 如需執行階段識別碼清單，請參閱[執行階段識別碼 (RID) 目錄](../rid-catalog.md)。

- `--self-contained false` 此參數會指示 .NET Core SDK 將可執行檔建立為 FDE。

只要您使用 `-r` 參數，輸出資料夾路徑就會變更為： `./bin/<BUILD-CONFIGURATION>/<TFM>/<RID>/publish/`

如果您使用[範例應用程式](#sample-app)，請執行 `dotnet publish -f netcoreapp2.2 -r win10-x64 --self-contained false`。 此命令會建立下列可執行檔： `./bin/Debug/netcoreapp2.2/win10-x64/publish/apptest1.exe`

> [!NOTE]
> 您可以啟用**全域無差異模式**來減少您部署的大小總計。 此模式適用於非全域應用程式，其能使用格式化慣例、大小寫慣例及字串比較，還有[不因文化特性而異](xref:System.Globalization.CultureInfo.InvariantCulture)的排序次序。 如需**全球化不變模式**和如何啟用的詳細資訊，請參閱[.Net Core 全球化不變模式](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md)。

## <a name="self-contained-deployment"></a>自封式部署

當您發佈獨立式部署 (SCD) 時，.NET Core SDK 會建立平台特定的可執行檔。 發佈 SCD 包含執行應用程式所需的所有 .NET Core 檔案，但不包含[.Net Core 的原生](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)相依性。 在執行應用程式之前，系統上必須具有這些相依性。

發佈 SCD 會建立不會向前復原到最新可用 .NET Core 安全性修補程式的應用程式。 如需編譯時期版本繫結的詳細資訊，請參閱[選取要使用的 .NET Core 版本](../versions/selection.md#self-contained-deployments-include-the-selected-runtime)。

您必須使用下列參數搭配 `dotnet publish` 命令來發佈 SCD：

- `-r <RID>` 此參數會使用識別碼 (RID) 來指定目標平台。 如需執行階段識別碼清單，請參閱[執行階段識別碼 (RID) 目錄](../rid-catalog.md)。

- `--self-contained true` 此參數會指示 .NET Core SDK 將可執行檔建立為 SCD。

> [!NOTE]
> 您可以啟用**全域無差異模式**來減少您部署的大小總計。 此模式適用於非全域應用程式，其能使用格式化慣例、大小寫慣例及字串比較，還有[不因文化特性而異](xref:System.Globalization.CultureInfo.InvariantCulture)的排序次序。 如需**全球化不變模式**和如何啟用的詳細資訊，請參閱[.Net Core 全球化不變模式](https://github.com/dotnet/runtime/blob/master/docs/design/features/globalization-invariant-mode.md)。

## <a name="see-also"></a>另請參閱

- [.NET Core 應用程式部署概觀](index.md)
- [.NET Core 執行階段識別項 (RID) 目錄](../rid-catalog.md)
