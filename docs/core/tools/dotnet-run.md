---
title: dotnet run 命令
description: dotnet run 命令提供方便的選項，以透過原始程式碼來執行應用程式。
ms.date: 02/19/2020
ms.openlocfilehash: c80f290c75e3bac65ae73fe8edada53db4ce86f8
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634412"
---
# <a name="dotnet-run"></a>dotnet run

本文 **適用于：** ✔️ .net CORE 2.x SDK 和更新版本

## <a name="name"></a>名稱

`dotnet run` - 執行原始程式碼，而不需要有任何明確的編譯或啟動命令。

## <a name="synopsis"></a>概要

```dotnetcli
dotnet run [-c|--configuration <CONFIGURATION>] [-f|--framework <FRAMEWORK>]
    [--force] [--interactive] [--launch-profile <NAME>] [--no-build]
    [--no-dependencies] [--no-launch-profile] [--no-restore]
    [-p|--project <PATH>] [-r|--runtime <RUNTIME_IDENTIFIER>]
    [-v|--verbosity <LEVEL>] [[--] [application arguments]]

dotnet run -h|--help
```

## <a name="description"></a>描述

`dotnet run` 命令提供方便的選項，以使用一個命令透過原始程式碼來執行應用程式。 可用於在命令列中快速進行反覆開發。 命令相依于用 [`dotnet build`](dotnet-build.md) 來建立程式碼的命令。 建置的任何需求 (例如必須先還原專案) 也同樣適用於 `dotnet run`。

輸出檔會寫入至預設位置，也就是 `bin/<configuration>/<target>`。 例如，如果您有 `netcoreapp2.1` 應用程式並執行 `dotnet run`，輸出將會放置在 `bin/Debug/netcoreapp2.1` 中。 而且會視需要覆寫檔案。 暫存檔案會放置在 `obj` 目錄中。

如果專案指定多個架構，執行 `dotnet run` 會導致錯誤，除非使用 `-f|--framework <FRAMEWORK>` 選項來指定架構。

`dotnet run` 命令用於專案內容中，而非已建置的組件。 如果您改為嘗試執行與 Framework 相依的應用程式 DLL，您必須不透過命令使用 [dotnet](dotnet.md)。 例如，若要執行 `myapp.dll`，使用︰

```dotnetcli
dotnet myapp.dll
```

如需驅動程式的詳細資訊 `dotnet` ，請參閱 [.Net 命令列工具 (CLI) ](index.md) 主題。

為了執行應用程式，`dotnet run` 命令會從 NuGet 快取解析共用執行階段之外的應用程式相依性。 因為它會使用快取相依性，不建議您在生產環境中使用 `dotnet run` 執行應用程式。 相反地，使用 [`dotnet publish`](dotnet-publish.md) 命令[建立部署](../deploying/index.md)，並部署已發佈的輸出。

### <a name="implicit-restore"></a>隱含還原

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

## <a name="options"></a>選項

- **`--`**

  分隔 `dotnet run` 的引數與執行中應用程式的引數。 此分隔符號之後的所有引數會傳遞至執行的應用程式。

- **`-c|--configuration <CONFIGURATION>`**

  定義組建組態。 大部分專案的預設值為 `Debug` ，但您可以覆寫專案中的組建設定。

- **`-f|--framework <FRAMEWORK>`**

  使用指定的 [架構](../../standard/frameworks.md)，建立並執行應用程式。 架構必須在專案檔中指定。

- **`--force`**

  即使最後的還原成功，仍強制解析所有相依性。 指定這個旗標等同於刪除 *project.assets.json* 檔案。

- **`-h|--help`**

  印出命令的簡短說明。

- **`--interactive`**

  允許命令停止並等候使用者輸入或動作 (例如完成驗證)。 自 .NET Core 3.0 SDK 起提供。

- **`--launch-profile <NAME>`**

  啟動應用程式時使用的啟動設定檔名稱 (如果有的話)。 啟動設定檔是在檔案的 *launchSettings.js* 中定義，通常稱為 `Development` 、 `Staging` 和 `Production` 。 如需詳細資訊，請參閱 [使用多個環境](/aspnet/core/fundamentals/environments)。

- **`--no-build`**

  不會在執行前建置專案。 它也會隱含設定 `--no-restore` 旗標。

- **`--no-dependencies`**

  在還原包含專案對專案 (P2P) 參考的專案時，會還原根專案，而非參考。

- **`--no-launch-profile`**

  不會嘗試使用 *launchSettings.json* 來設定應用程式。

- **`--no-restore`**

  執行命令時，不會執行隱含還原。

- **`-p|--project <PATH>`**

  指定要執行的專案檔路徑 (資料夾名稱或完整路徑)。 如果未指定，則會預設為目前目錄。

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  指定要還原套件的目標執行階段。 如需執行階段識別項 (RID) 清單，請參閱 [RID 目錄](../rid-catalog.md)。 `-r` 自 .NET Core 3.0 SDK 起提供的簡短選項。

- **`-v|--verbosity <LEVEL>`**

  設定命令的詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。 預設值是 `m`。 自 .NET Core 2.1 SDK 起提供。

## <a name="examples"></a>範例

- 執行目前目錄中的專案：

  ```dotnetcli
  dotnet run
  ```

- 執行指定的專案：

  ```dotnetcli
  dotnet run --project ./projects/proj1/proj1.csproj
  ```

- 執行目前目錄中的專案 (因為已使用空白的 `--` 選項，所以這個範例中的 `--help` 引數會傳遞給應用程式)：

  ```dotnetcli
  dotnet run --configuration Release -- --help
  ```

- 還原目前目錄中專案的相依性和工具，只會顯示最基本的輸出，然後執行專案：

  ```dotnetcli
  dotnet run --verbosity m
  ```
