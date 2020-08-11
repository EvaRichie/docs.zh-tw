---
title: 針對 .NET Core 工具使用問題進行疑難排解
description: 探索執行 .NET Core 工具和可能的解決方案時常見的問題。
author: kdollard
ms.topic: troubleshooting
ms.date: 02/14/2020
ms.openlocfilehash: b98b2735770c8259c2daf94575fc087b91bb61fd
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88062632"
---
# <a name="troubleshoot-net-core-tool-usage-issues"></a>針對 .NET Core 工具使用問題進行疑難排解

當您嘗試安裝或執行 .NET Core 工具時，可能會遇到問題，這可以是全域工具或本機工具。 本文說明常見的根本原因和一些可能的解決方案。

## <a name="installed-net-core-tool-fails-to-run"></a>安裝的 .NET Core 工具無法執行

當 .NET Core 工具無法執行時，您很可能會遇到下列其中一個問題：

* 找不到工具的可執行檔。
* 找不到正確的 .NET Core 執行階段版本。

### <a name="executable-file-not-found"></a>找不到可執行檔

如果找不到可執行檔，您會看到類似下面的訊息：

```console
Could not execute because the specified command or file was not found.
Possible reasons for this include:
  * You misspelled a built-in dotnet command.
  * You intended to execute a .NET Core program, but dotnet-xyz does not exist.
  * You intended to run a global tool, but a dotnet-prefixed executable with this name could not be found on the PATH.
```

可執行檔的名稱會決定您叫用此工具的方式。 下表描述格式：

| 可執行檔名稱格式  | 調用格式   |
|-------------------------|---------------------|
| `dotnet-<toolName>.exe` | `dotnet <toolName>` |
| `<toolName>.exe`        | `<toolName>`        |

* 全域工具

  通用工具可以安裝在預設目錄或特定位置。 預設目錄如下：

  | OS          | 路徑                          |
  |-------------|-------------------------------|
  | Linux/macOS | `$HOME/.dotnet/tools`         |
  | Windows     | `%USERPROFILE%\.dotnet\tools` |

  如果您嘗試執行全域工具，請檢查 `PATH` 您電腦上的環境變數是否包含安裝通用工具的路徑，以及可執行檔是否在該路徑中。

  .NET Core CLI 嘗試在其第一次使用時，將預設位置新增至 PATH 環境變數。 不過，在某些情況下，位置可能不會自動新增至路徑：

  * 如果您使用的是 Linux，而且您已使用*gz*檔案安裝 .NET Core SDK，而不是 apt-get 或 rpm。
  * 如果您使用的是 macOS 10.15 "Catalina" 或更新版本。
  * 如果您使用 macOS 10.14 "Mojave" 或更早版本，且已使用*gz*檔案安裝 .NET Core SDK，而不是 *.pkg*。
  * 如果您已安裝 .NET Core 3.0 SDK，而且已將 `DOTNET_ADD_GLOBAL_TOOLS_TO_PATH` 環境變數設定為 `false` 。
  * 如果您已安裝 .NET Core 2.2 SDK 或更早版本，而且已將 `DOTNET_SKIP_FIRST_TIME_EXPERIENCE` 環境變數設定為 `true` 。

  在這些情況下，或如果您指定 `--tool-path` 選項， `PATH` 電腦上的環境變數不會自動包含您安裝通用工具的路徑。 在這種情況下，請將工具位置附加 (例如， `$HOME/.dotnet/tools` `PATH` 使用 shell 提供的任何方法來更新環境變數，以) 至環境變數。 如需詳細資訊，請參閱[.Net Core 工具](global-tools.md)。

* 本機工具

  如果您嘗試執行本機工具，請確認目前目錄或其任何父目錄中有一個稱為*dotnet-tools.js*的資訊清單檔。 這個檔案也可以存留在專案資料夾階層中名為 *.config*的資料夾底下，而不是根資料夾。 如果*dotnet-tools.js*存在，請開啟它，並檢查您嘗試執行的工具。 如果檔案未包含的專案 `"isRoot": true` ，則也請進一步檢查檔案階層，以取得其他工具資訊清單檔。

  如果您嘗試執行以指定路徑安裝的 .NET Core 工具，則需要在使用此工具時包含該路徑。 使用工具路徑安裝工具的範例如下：

  ```console
  ..\<toolDirectory>\dotnet-<toolName>
  ```

### <a name="runtime-not-found"></a>找不到執行時間

.NET Core 工具是與[架構相依的應用程式](../deploying/index.md#publish-runtime-dependent)，這表示它們會依賴安裝在您電腦上的 .net core 執行時間。 如果找不到預期的執行時間，它們會遵循一般的 .NET Core 執行時間向前復原規則，例如：

* 應用程式會向前復原到指定的主要和次要版本的最高修補程式版本。
* 如果沒有符合的主要和次要版本號碼相符的執行時間，則會使用下一個較高的次要版本。
* 預覽版本的執行階段之間或預覽版本和發行版本之間，不會進行向前復原。 因此，使用預覽版本所建立的 .NET Core 工具必須由作者重建並重新發行，並重新安裝。

在兩個常見的案例中，預設不會進行向前復原：

* 只有較低版本的執行時間可供使用。 向前復原只會選取較新版本的執行時間。
* 只有較高的執行時間主要版本可供使用。 向前復原不會跨越主要版本界限。

如果應用程式找不到適當的執行時間，它就無法執行並報告錯誤。

您可以使用下列其中一個命令，找出您的電腦上已安裝的 .NET Core 執行時間：

```dotnetcli
dotnet --list-runtimes
dotnet --info
```

如果您認為此工具應該支援您目前已安裝的執行階段版本，您可以洽詢工具作者，並查看他們是否可以更新版本號碼或多目標。 一旦使用更新的版本號碼將其工具套件重新編譯並重新發佈至 NuGet 之後，您就可以更新您的複本。 雖然不會發生這種情況，最快的解決方案是安裝可與您嘗試執行的工具搭配運作的執行階段版本。 若要下載特定的 .NET Core 執行階段版本，請造訪[.Net core 下載頁面](https://dotnet.microsoft.com/download/dotnet-core)。

如果您將 .NET Core SDK 安裝到非預設位置，則必須將環境變數設定 `DOTNET_ROOT` 為包含 `dotnet` 可執行檔的目錄。

## <a name="net-core-tool-installation-fails"></a>.NET Core 工具安裝失敗

安裝 .NET Core 的全域或本機工具可能會失敗的原因有很多。 當工具安裝失敗時，您會看到類似下面的訊息：

```console
Tool '{0}' failed to install. This failure may have been caused by:

* You are attempting to install a preview release and did not use the --version option to specify the version.
* A package by this name was found, but it was not a .NET Core tool.
* The required NuGet feed cannot be accessed, perhaps because of an Internet connection problem.
* You mistyped the name of the tool.

For more reasons, including package naming enforcement, visit https://aka.ms/failure-installing-tool
```

為了協助診斷這些失敗，NuGet 訊息會直接向使用者顯示，以及先前的訊息。 NuGet 訊息可協助您找出問題。

### <a name="package-naming-enforcement"></a>封裝命名強制執行

Microsoft 已變更工具的套件識別碼指引，導致找不到具有預測名稱的一些工具。 新的指引是所有的 Microsoft 工具前面都會加上 "Microsoft"。 這個前置詞是保留的，只能用於以 Microsoft 授權憑證簽署的封裝。

在轉換期間，有些 Microsoft 工具會有舊版的套件識別碼，有些則會有新的表單：

```dotnetcli
dotnet tool install -g Microsoft.<toolName>
dotnet tool install -g <toolName>
```

更新套件識別碼時，您必須變更為新的套件識別碼，才能取得最新的更新。 具有簡化工具名稱的套件將會被取代。

### <a name="preview-releases"></a>預覽版本

* 您正嘗試安裝預覽版本，但未使用 `--version` 選項來指定版本。

處於預覽狀態的 .NET Core 工具必須以部分名稱指定，以表示其為預覽狀態。 您不需要包含整個預覽。 假設版本號碼採用預期的格式，您可以使用類似下列的範例：

```dotnetcli
dotnet tool install -g --version 1.1.0-pre <toolName>
```

### <a name="package-isnt-a-net-core-tool"></a>套件不是 .NET Core 工具

* 找到這個名稱的 NuGet 套件，但它不是 .NET Core 工具。

如果您嘗試安裝屬於一般 NuGet 套件而不是 .NET Core 工具的 NuGet 套件，您會看到類似下面的錯誤：

> NU1212：的專案套件組合無效 `<ToolName>` 。 DotnetToolReference 專案樣式只能包含 DotnetTool 類型的參考。

### <a name="nuget-feed-cant-be-accessed"></a>無法存取 NuGet 摘要

* 無法存取所需的 NuGet 摘要，可能是因為網際網路連線問題所致。

工具安裝需要存取包含工具套件的 NuGet 摘要。 如果饋送無法使用，則會失敗。 您可以使用來變更摘要 `nuget.config` 、要求特定檔案 `nuget.config` ，或使用參數指定其他摘要 `--add-source` 。 根據預設，NuGet 會針對無法連接的任何摘要擲回錯誤。 旗標 `--ignore-failed-sources` 可以略過這些無法連線的來源。

### <a name="package-id-incorrect"></a>套件識別碼不正確

* 您的工具名稱輸入錯誤。

失敗的常見原因是工具名稱不正確。 這可能是因為錯誤錯誤而發生，或是因為工具已移動或已被取代。 針對 NuGet.org 上的工具，確保您的名稱正確的方法之一，就是在 NuGet.org 搜尋工具並複製安裝命令。

## <a name="see-also"></a>另請參閱

* [.NET Core 工具](global-tools.md)
