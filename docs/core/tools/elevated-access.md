---
title: Dotnet 命令的提升存取權限
description: 了解適用於需要提升存取權限的 dotnet 命令最佳做法。
author: wli3
ms.date: 06/26/2019
ms.openlocfilehash: b34a4d631ec0e5ef641e1ffbc91e081d25645157
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634047"
---
# <a name="elevated-access-for-dotnet-commands"></a>Dotnet 命令的提升存取權限

軟體開發最佳做法會引導開發人員撰寫需要最少權限的軟體。 但是，由於作業系統規則，有些軟體 (例如效能監視工具) 會需要系統管理員權限。 下列指導會描述使用 .NET Core 撰寫這類軟體時的支援案例。

下列命令可以提升的權限來執行：

- `dotnet tool` 命令，例如 [dotnet tool install](dotnet-tool-install.md)。
- `dotnet run --no-build`
- `dotnet-core-uninstall`

我們不建議執行其他提升的權限命令。 特別是，我們不建議針對使用 MSBuild 的命令提升權限，例如 [dotnet restore](dotnet-restore.md)、[dotnet build](dotnet-build.md) 和 [dotnet run](dotnet-run.md)。 主要問題是使用者在發出 dotnet 命令後，在根及限制帳戶之間來回轉換時的權限管理問題。 您可能會發現作為限制的使用者，您無法存取由根使用者建置的檔案。 雖然有數種方法可以解決這種情況，但您從一開始其實就可以避免它們。

只要您不是在根和受限帳戶之間來回轉換，您就可以將命令以 root 的形式執行。 例如，根據預設 Docker 容器會以根帳戶執行，因此它們便具有這種特性。

## <a name="global-tool-installation"></a>全域工具安裝

下列指示示範安裝、執行和卸載需要提高許可權來執行之 .NET 工具的建議方式。

<!-- markdownlint-disable MD025 -->

# <a name="windows"></a>[Windows](#tab/windows)

### <a name="install-the-tool"></a>安裝工具

若資料夾 `%ProgramFiles%\dotnet-tools` 已存在，請執行下列操作來檢查 "Users" 群組是否有寫入或修改該目錄的權限：

- 以滑鼠右鍵按一下 `%ProgramFiles%\dotnet-tools` 資料夾，然後選取 [ **屬性** ]。 [通用屬性] 對話方塊隨即開啟。
- 選取 [ **安全性** ] 索引標籤。在 [ **群組或使用者名稱** ] 底下，檢查 "Users" 群組是否有寫入或修改目錄的許可權。
- 若 "Users" 群組可以寫入或修改目錄，請在安裝工具時使用不同的目錄名稱，而非 *dotnet-tools* 。

若要安裝工具，請以提升權限的命令提示字元來執行下列命令。 它會在安裝期間建立 *dotnet-tools* 資料夾。

```dotnetcli
dotnet tool install PACKAGEID --tool-path "%ProgramFiles%\dotnet-tools".
```

### <a name="run-the-global-tool"></a>執行全域工具

**選項 1** ：搭配提升權限的命令提示字元使用完整路徑：

```cmd
"%ProgramFiles%\dotnet-tools\TOOLCOMMAND"
```

**選項 2** ：將新建立的資料夾新增到 `%Path%`。 您只需要執行此作業一次。

```cmd
setx Path "%Path%;%ProgramFiles%\dotnet-tools\"
```

然後使用以下項目執行：

```cmd
TOOLCOMMAND
```

### <a name="uninstall-the-global-tool"></a>解除安裝全域工具

在提升權限的命令提示字元中，鍵入下列命令：

```dotnetcli
dotnet tool uninstall PACKAGEID --tool-path "%ProgramFiles%\dotnet-tools"
```

# <a name="linux"></a>[Linux](#tab/linux)

[!INCLUDE [elevated-access-unix](../../../includes/elevated-access-unix.md)]

# <a name="macos"></a>[macOS](#tab/macos)

[!INCLUDE [elevated-access-unix](../../../includes/elevated-access-unix.md)]

---

## <a name="local-tools"></a>本機工具

本機工具範圍會限制在每一位使用者的每個子樹狀目錄中。 以提升的權限執行時，本機工具會將受限制使用者環境共用到提升權限的環境。 在 Linux 和 macOS 中，這會導致以僅限根使用者的存取來設定檔案。 若使用者切換回限制的帳戶，使用者便無法繼續存取或寫入檔案。 因此，我們不建議將需要提升權限的工具作為本機工具安裝。 請改為使用 `--tool-path` 選項及先前適用於全域工具的指導方針。

## <a name="elevation-during-development"></a>開發期間的提升權限

在開發期間，您可能需要提升的存取權限來測試您的應用程式。 例如，針對 IoT 應用程式，此案例相當常見。 我們建議您在不使用提升權限的情況下建置應用程式，然後使用提升權限來執行它。 有數種模式可以進行此操作，如下所示：

- 使用產生的可執行檔 (它可提供最佳的啟動效能)：

   ```dotnetcli
   dotnet build
   sudo ./bin/Debug/netcoreapp3.0/APPLICATIONNAME
   ```

- 搭配 `—no-build` 旗標使用 [dotnet run](dotnet-run.md) 來避免產生新的二進位檔案：

   ```dotnetcli
   dotnet build
   sudo dotnet run --no-build
   ```

## <a name="see-also"></a>另請參閱

- [.NET 工具總覽](global-tools.md)
