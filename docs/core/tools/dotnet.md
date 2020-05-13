---
title: dotnet 命令
description: 瞭解 dotnet 命令（.NET Core CLI 的一般驅動程式）及其使用方式。
ms.date: 02/13/2020
ms.openlocfilehash: 88e92b3ff5e8f68b980015a817434dd2d67df93a
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378846"
---
# <a name="dotnet-command"></a>dotnet 命令

**本文適用于：** ✔️ .net CORE 2.1 SDK 和更新版本

## <a name="name"></a>名稱

`dotnet`-.NET Core CLI 的泛型驅動程式。

## <a name="synopsis"></a>概要

若要取得可用命令和環境的相關資訊：

```dotnetcli
dotnet [--version] [--info] [--list-runtimes] [--list-sdks]

dotnet -h|--help
```

若要執行命令（需要 SDK 安裝）：

```dotnetcli
dotnet <COMMAND> [-d|--diagnostics] [-h|--help] [--verbosity <LEVEL>]
    [command-options] [arguments]
```

若要執行應用程式：

```dotnetcli
dotnet [--additionalprobingpath <PATH>] [--additional-deps <PATH>]
    [--fx-version <VERSION>]  [--roll-forward <SETTING>]
    <PATH_TO_APPLICATION> [arguments]

dotnet exec [--additionalprobingpath] [--additional-deps <PATH>]
    [--fx-version <VERSION>]  [--roll-forward <SETTING>]
    <PATH_TO_APPLICATION> [arguments]
```

`--roll-forward`自 .NET Core 3.x 開始提供。 `--roll-forward-on-no-candidate-fx`針對 .Net Core 2.x 使用。

## <a name="description"></a>描述

此 `dotnet` 命令有兩個功能：

- 它提供使用 .NET Core 專案的命令。

  例如，會 [`dotnet build`](dotnet-build.md) 建立專案。 每個命令都會定義自己的選項和引數。 所有的命令都支援 `--help` 選項來列印有關如何使用命令的簡短檔。

- 它會執行 .NET Core 應用程式。

  您可以指定應用程式檔的路徑 `.dll` 來執行應用程式。  若要執行應用程式，以尋找並執行進入點，在主控台應用程式的情況下，這是 `Main` 方法。 例如，會 `dotnet myapp.dll` 執行 `myapp` 應用程式。 若要瞭解部署選項，請參閱[.Net Core 應用程式部署](../deploying/index.md)。

## <a name="options"></a>選項

有不同的選項可供 `dotnet` 自己使用、用於執行命令，以及執行應用程式。

### <a name="options-for-dotnet-by-itself"></a>Dotnet 本身的選項

下列選項本身適用于 `dotnet` 。 例如 `dotnet --info`。 他們會列印環境的相關資訊。

- **`--info`**

  會印出關於 .NET Core 安裝和電腦環境的詳細資訊，例如目前作業系統和 .NET Core 版本的認可 SHA。

- **`--version`**

  印出使用中的 .NET Core SDK 版本。

- **`--list-runtimes`**

  印出已安裝的 .NET Core 執行時間清單。 X86 版本的 SDK 只會列出 x86 執行時間，而 x64 版本的 SDK 只會列出 x64 執行時間。

- **`--list-sdks`**

  印出已安裝的 .NET Core Sdk 清單。

- **`-h|--help`**

  印出可用命令的清單。

### <a name="sdk-options-for-running-a-command"></a>執行命令的 SDK 選項

下列選項適用于搭配 `dotnet` 命令。 例如 `dotnet build --help`。

- **`-d|--diagnostics`**

  啟用診斷輸出。

- **`-v|--verbosity <LEVEL>`**

  設定命令的詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。 在每個命令中都不支援。 若要判斷此選項是否可用，請參閱特定的命令頁面。

- **`-h|--help`**

  印出指定命令的文件，例如`dotnet build --help`。

- **`command options`**

  每個命令都會定義該命令的特定選項。 如需可用選項的清單，請參閱特定的命令頁。

### <a name="runtime-options"></a>執行時間選項

當執行應用程式時，可以使用下列選項 `dotnet` 。 例如 `dotnet myapp.dll --roll-forward Major`。

- **`--additionalprobingpath <PATH>`**

  包含探查原則和要探查之組件的路徑。

- **`--additional-deps <PATH>`**

  其他 *.deps.json* 檔案的路徑。 *.Deps.json json*檔案包含相依性、編譯相依性和用來解決元件衝突的版本資訊的清單。 如需詳細資訊，請參閱 GitHub 上的 [Runtime Configuration Files](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md) (執行階段組態檔)。

- **`--depsfile <PATH_TO_DEPSFILE>`**

  *.Deps.json json*檔案的路徑。 *.Deps.json*檔案是一個設定檔，其中包含執行應用程式所需之相依性的相關資訊。 這個檔案是由 .NET Core SDK 所產生。

- **`--runtimeconfig`**

  *runtimeconfig.json* 檔案的路徑。 *.Runtimeconfig.json json*檔案是包含執行時間設定的設定檔。 如需詳細資訊，請參閱[.Net Core 執行時間設定](../run-time-config/index.md#runtimeconfigjson)。

- **`--roll-forward <SETTING>`****從 .NET Core SDK 3.0 開始提供。**

  控制如何將向前復原套用到應用程式。 `SETTING`可以是下列其中一個值。 如果未指定， `Minor` 則為預設值。

  - `LatestPatch`-向前復原至最高的修補程式版本。 這會停用次要版本向前復原。
  - `Minor`-如果遺漏要求的次要版本，則向前復原到最低的次要版本。 如果要求的次要版本存在，則會使用 LatestPatch 原則。
  - `Major`-如果要求的主要版本遺失，則向前復原至最低的主要版本，以及最低的次要版本。 如果要求的主要版本存在，則會使用 Minor 原則。
  - `LatestMinor`-向前復原到最高的次要版本，即使要求的次要版本存在也一樣。 適用於裝載案例的元件。
  - `LatestMajor`-向前復原到最高的主要和最高的次要版本，即使有要求的主要存在也一樣。 適用於裝載案例的元件。
  - `Disable`-不要向前復原。 只會繫結至指定的版本。 此原則不建議一般用途，因為它會停用向前復原到最新修補程式的功能。 只有測試時才建議使用這個值。

  除了以外 `Disable` ，所有設定都會使用最高可用的修補程式版本。

  您也可以在專案檔案屬性、執行時間設定檔案屬性和環境變數中設定向前復原行為。 如需詳細資訊，請參閱[主要版本執行時間向前](../whats-new/dotnet-core-3-0.md#major-version-runtime-roll-forward)復原。

- **`--roll-forward-on-no-candidate-fx <N>`****適用于 .Net Core 2.X SDK。**

  在必要的共用架構無法使用時定義行為。 `N` 可以是：

  - `0` - 對次要版本也停用向前復原。
  - `1` - 對次要版本向前復原，主要版本則不。 此為預設行為。
  - `2` - 對次要及主要版本向前復原。

  如需詳細資訊，請參閱[向前復原](../whats-new/dotnet-core-2-1.md#roll-forward)。

  從 .NET Core 3.0 開始，此選項會被取代 `--roll-forward` ，而應該改用該選項。

- **`--fx-version <VERSION>`**

  用來執行應用程式的 .NET Core 執行階段版本。

  此選項會覆寫應用程式檔案中第一個 framework 參考的版本 `.runtimeconfig.json` 。 這表示只有在只有一個架構參考時，它才會如預期般運作。 如果應用程式有一個以上的架構參考，使用這個選項可能會導致錯誤。

## <a name="dotnet-commands"></a>dotnet 命令

### <a name="general"></a>一般

| Command                                       | 函式                                                            |
| --------------------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)               | 建置 .NET Core 應用程式。                                     |
| [dotnet build-server](dotnet-build-server.md) | 與組建所啟動的伺服器互動。                          |
| [dotnet clean](dotnet-clean.md)               | 清除組建輸出。                                                |
| [dotnet help](dotnet-help.md)                 | 顯示命令更詳細的線上文件。           |
| [dotnet migrate](dotnet-migrate.md)           | 將有效的 Preview 2 專案移轉至 .NET Core SDK 1.0 專案。  |
| [dotnet msbuild](dotnet-msbuild.md)           | 提供對 MSBuild 命令列的存取。                        |
| [dotnet new](dotnet-new.md)                   | 初始化指定範本的 C# 或 F# 專案。                |
| [dotnet pack](dotnet-pack.md)                 | 建立您程式碼的 NuGet 套件。                               |
| [dotnet publish](dotnet-publish.md)           | 發行 .NET 與 Framework 相依的應用程式或獨立應用程式。 |
| [dotnet restore](dotnet-restore.md)           | 還原所指定應用程式的相依性。                  |
| [dotnet run](dotnet-run.md)                   | 從原始檔執行應用程式。                                   |
| [dotnet sln](dotnet-sln.md)                   | 要在方案檔中新增、移除及列出專案的選項。       |
| [dotnet store](dotnet-store.md)               | 在執行階段套件存放區中儲存組件。                     |
| [dotnet test](dotnet-test.md)                 | 使用測試執行器執行測試。                                     |

### <a name="project-references"></a>專案參考

Command | 函式
--- | ---
[dotnet add reference](dotnet-add-reference.md) | 新增專案參考。
[dotnet list reference](dotnet-list-reference.md) | 列出專案參考。
[dotnet remove reference](dotnet-remove-reference.md) | 移除專案參考。

### <a name="nuget-packages"></a>NuGet 套件

Command | 函式
--- | ---
[dotnet add package](dotnet-add-package.md) | 新增 NuGet 套件。
[dotnet remove package](dotnet-remove-package.md) | 移除 NuGet 套件。

### <a name="nuget-commands"></a>NuGet 命令

Command | 函式
--- | ---
[dotnet nuget delete](dotnet-nuget-delete.md) | 從伺服器刪除或取消列出套件。
[dotnet nuget push](dotnet-nuget-push.md) | 將套件推送至伺服器並發行。
[dotnet nuget locals](dotnet-nuget-locals.md) | 清除或列出本機 NuGet 資源，例如 http-request 快取、暫時快取，或整部電腦的全域套件資料夾。
[dotnet nuget add source](dotnet-nuget-add-source.md) | 新增 NuGet 來源。
[dotnet nuget disable source](dotnet-nuget-disable-source.md) | 停用 NuGet 來源。
[dotnet nuget enable source](dotnet-nuget-enable-source.md) | 啟用 NuGet 來源。
[dotnet nuget list source](dotnet-nuget-list-source.md) | 列出所有已設定的 NuGet 來源。
[dotnet nuget remove source](dotnet-nuget-remove-source.md) | 移除 NuGet 來源。
[dotnet nuget update source](dotnet-nuget-update-source.md) | 更新 NuGet 來源。

### <a name="global-tool-path-and-local-tools-commands"></a>全域、工具路徑和本機工具命令

工具是從 NuGet 套件安裝並從命令提示字元叫用的主控台應用程式。 您可以自行撰寫工具，或安裝由協力廠商撰寫的工具。 工具也稱為「通用工具」、「工具路徑工具」和「本機工具」。 如需詳細資訊，請參閱[.Net Core 工具總覽](global-tools.md)。 從 .NET Core SDK 2.1 開始提供全域和工具路徑工具。 從 .NET Core SDK 3.0 開始提供本機工具。

Command | 函式
--- | ---
[dotnet tool install](dotnet-tool-install.md) | 在您的電腦上安裝工具。
[dotnet tool list](dotnet-tool-list.md) | 列出目前安裝在您電腦上的所有全域、工具路徑或本機工具。
[dotnet tool uninstall](dotnet-tool-uninstall.md) | 從您的電腦卸載工具。
[dotnet tool update](dotnet-tool-update.md) | 更新安裝在您電腦上的工具。

### <a name="additional-tools"></a>其他工具

從 .NET Core SDK 2.1.300 開始，先前僅能透過 `DotnetCliToolReference` 於個別專案上使用的數個工具，現在皆已做為 .NET Core SDK 的一部分提供。 這些工具列於下列資料表中：

| 工具                                              | 函式                                                     |
| ------------------------------------------------- | ------------------------------------------------------------ |
| dev-certs                                         | 建立及管理開發憑證。                |
| [ef](/ef/core/miscellaneous/cli/dotnet)           | Entity Framework Core 命令列工具。                    |
| sql-cache                                         | SQL Server 快取命令列工具。                         |
| [user-secrets](/aspnet/core/security/app-secrets) | 管理開發使用者祕密。                            |
| [欣賞](/aspnet/core/tutorials/dotnet-watch)      | 啟動會在檔案變更時執行命令的檔案監看員。 |

如需每個工具的詳細資訊，請鍵入 `dotnet <tool-name> --help`。

## <a name="examples"></a>範例

建立新的 .NET Core 主控台應用程式：

```dotnetcli
dotnet new console
```

建置所指定目錄中的專案和其相依性：

```dotnetcli
dotnet build
```

執行應用程式：

```dotnetcli
dotnet myapp.dll
```

## <a name="environment-variables"></a>環境變數

- `DOTNET_ROOT`, `DOTNET_ROOT(x86)`

  指定 .NET Core 執行時間的位置（如果未安裝在預設位置）。 Windows 上的預設位置是 `C:\Program Files\dotnet` 。 Linux 和 macOS 上的預設位置是 `/usr/share/dotnet` 。 只有在透過產生的可執行檔（apphosts）來執行應用程式時，才會使用此環境變數。 `DOTNET_ROOT(x86)`在64位作業系統上執行32位可執行檔時，會改為使用。

- `DOTNET_PACKAGES`

  全域套件資料夾。 如果未設定，預設為 `~/.nuget/packages` (Unix) 或 `%userprofile%\.nuget\packages` (Windows)。

- `DOTNET_SERVICING`

  指定載入執行階段時，共用主機所使用的服務索引位置。

- `DOTNET_NOLOGO`

  指定是否要在第一次執行時顯示 .NET Core 歡迎畫面和遙測訊息。 設定為 `true` 可將這些訊息（值 `true` 、或已接受）設為靜音， `1` `yes` 或設定為以 `false` 允許（值 `false` 、 `0` 或 `no` 接受）。 如果未設定，預設值為 `false` ，而訊息會在第一次執行時顯示。 此旗標不會影響遙測（請參閱以選擇不傳送 `DOTNET_CLI_TELEMETRY_OPTOUT` 遙測資料）。

- `DOTNET_CLI_TELEMETRY_OPTOUT`

  指定是否收集 .NET Core 工作使用資料，並將其傳送給 Microsoft。 設為 `true` 以選擇加入遙測功能 (可接受的值為 `true`、`1` 或 `yes`)。 否則，請設為 `false` 以選擇退出遙測功能 (可接受的值為 `false`、`0` 或 `no`)。 如果未設定，預設值為 `false`，且遙測功能會處於作用狀態。

- `DOTNET_MULTILEVEL_LOOKUP`

  指定是否從全域位置解析 .NET Core 執行階段、共用架構或 SDK。 如果未設定，則會預設為1（邏輯 `true` ）。 設定為0（邏輯 `false` ），表示不從全域位置解析，而且已隔離 .Net Core 安裝。 如需多層級查閱的詳細資訊，請參閱 [Multi-level SharedFX Lookup](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/multilevel-sharedfx-lookup.md) (多層級 SharedFX 查閱)。

- `DOTNET_ROLL_FORWARD`**從 .Net Core 3.x 開始提供。**

  決定向前復原行為。 如需詳細資訊，請參閱本文稍 `--roll-forward` 早的選項。

- `DOTNET_ROLL_FORWARD_TO_PRERELEASE`**從 .Net Core 3.x 開始提供。**

  如果設定為 `1` （已啟用），則可從發行版本開始向前復原至發行前版本。 根據預設（ `0` -已停用），當要求 .Net Core 執行時間的發行版本時，向前復原只會考慮已安裝的發行版本。

  如需詳細資訊，請參閱[向前復原](../whats-new/dotnet-core-3-0.md#major-version-runtime-roll-forward)。

- `DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX`**適用于 .Net Core 2.x。**

  如果設定為 `0`，將停用次要版本向前復原。 如需詳細資訊，請參閱[向前復原](../whats-new/dotnet-core-2-1.md#roll-forward)。

  這項設定在 .NET Core 3.0 中由取代 `DOTNET_ROLL_FORWARD` 。 應改為使用新的設定。

- `DOTNET_CLI_UI_LANGUAGE`

  使用地區設定值（例如），設定 CLI UI 的語言 `en-us` 。 支援的值與 Visual Studio 相同。 如需詳細資訊，請參閱[Visual Studio 安裝檔](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2019)中的變更安裝程式語言一節。 .NET resource manager 規則適用，因此您不需要挑選完全相符的， &mdash; 也可以在樹狀結構中挑選子系 `CultureInfo` 。 例如，如果您將它設定為 `fr-CA` ，CLI 會尋找並使用 `fr` 翻譯。 如果您將它設定為不支援的語言，CLI 會切換回英文。

- `DOTNET_DISABLE_GUI_ERRORS`

  針對啟用 GUI 的產生可執行檔-停用對話方塊快顯視窗，這通常會顯示特定類別的錯誤。 `stderr`在這些情況下，它只會寫入並結束。
  
- `DOTNET_ADDITIONAL_DEPS`

  相當於 CLI 選項 `--additional-deps` 。

- `DOTNET_RUNTIME_ID`

  覆寫偵測到的 RID。

- `DOTNET_SHARED_STORE`

  「共用存放區」的位置，在某些情況下，元件解析會回復為。

- `DOTNET_STARTUP_HOOKS`

  從載入和執行啟動攔截的元件清單。

- `DOTNET_BUNDLE_EXTRACT_BASE_DIR`**從 .Net Core 3.x 開始提供。**

  指定在執行單一檔案應用程式之前，要解壓縮的目標目錄。

  如需詳細資訊，請參閱[單一檔案可執行檔](../whats-new/dotnet-core-3-0.md#single-file-executables)。

- `COREHOST_TRACE`, `COREHOST_TRACEFILE`, `COREHOST_TRACE_VERBOSITY`

  控制來自裝載元件（例如、和）的診斷追蹤 `dotnet.exe` `hostfxr` `hostpolicy` 。

  * `COREHOST_TRACE=[0/1]`-預設為 `0` -已停用追蹤。 如果設定為 `1` ，則會啟用診斷追蹤。
  * `COREHOST_TRACEFILE=<file path>`-只有在透過啟用追蹤時，才會有作用 `COREHOST_TRACE=1` 。 設定時，會將追蹤資訊寫入至指定的檔案，否則會將追蹤資訊寫入 `stderr` 。 **從 .NET Core 3.x 開始提供。**
  * `COREHOST_TRACE_VERBOSITY=[1/2/3/4]`-預設值為 `4` 。 只有在透過啟用追蹤時，才會使用此設定 `COREHOST_TRACE=1` 。 **從 .NET Core 3.x 開始提供。**
    * `4`-寫入所有追蹤資訊
    * `3`-只會寫入資訊、警告和錯誤訊息
    * `2`-只會寫入警告和錯誤訊息
    * `1`-僅寫入錯誤訊息

  取得應用程式啟動詳細追蹤資訊的一般方式是設定 `COREHOST_TRACE=1` 和 `COREHOST_TRACEFILE=host_trace.txt` ，然後執行應用程式。 `host_trace.txt`將會在目前目錄中建立新的檔案，並提供詳細資訊。

## <a name="see-also"></a>請參閱

- [Runtime Configuration Files](https://github.com/dotnet/cli/blob/master/Documentation/specs/runtime-configuration-file.md) (執行階段組態檔)
- [.NET Core 執行時間設定](../run-time-config/index.md)
