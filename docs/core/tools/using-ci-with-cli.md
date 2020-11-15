---
title: 使用 .NET SDK 和工具進行 (CI) 的持續整合
description: 瞭解如何在組建伺服器上使用 .NET SDK 和其工具，持續整合。
ms.date: 05/18/2017
ms.openlocfilehash: 6d92bf7250ab4aea33325b1a23e7661a296e9756
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2020
ms.locfileid: "94633814"
---
# <a name="using-the-net-sdk-and-tools-in-continuous-integration-ci"></a>在持續整合 (CI 中使用 .NET SDK 和工具) 

本檔概述如何在組建伺服器上使用 .NET SDK 和其工具。 .NET 工具組會以互動方式運作，其中的開發人員會在命令提示字元中輸入命令，以及自動執行 (CI) server 執行組建腳本的持續整合。 命令、選項、輸入和輸出都是相同的，您只需要提供取得工具的方式和建置應用程式的系統。 本文件著重於 CI 的工具取得案例，並包含設計建置指令碼並建立其結構的相關建議。

## <a name="installation-options-for-ci-build-servers"></a>CI 組建伺服器的安裝選項

### <a name="using-the-native-installers"></a>使用原生安裝程式

有針對 macOS、Linux 及 Windows 提供原生安裝程式。 安裝程式需要組建伺服器的管理員 (sudo) 存取權。 使用原生安裝程式的優點在於它會安裝工具執行時所需的所有原生相依性。 原生安裝程式也提供 SDK 的全系統安裝。

macOS 使用者應使用 PKG 安裝程式。 在 Linux 上，您可以選擇使用摘要套件管理員 (例如適用於 Ubuntu 的 apt-get 或適用於 CentOS 的 yum)，或使用套件本身 (DEB 或 RPM)。 在 Windows 上請使用 MSI 安裝程式。

您可以在 [.NET Core 下載](https://dotnet.microsoft.com/download) \(英文\) 找到最新的穩定二進位檔。 如果您想要使用最新 (但可能不穩定) 的發行前版本工具，請使用 [dotnet/core-sdk GitHub 存放庫](https://github.com/dotnet/core-sdk#installers-and-binaries) \(英文\) 所提供的連結。 針對 Linux 發行版本，有提供 `tar.gz` 封存 (也稱為 `tarballs`)；請使用封存內的安裝指令碼來安裝 .NET Core。

### <a name="using-the-installer-script"></a>使用安裝程式指令碼

使用安裝程式指令碼可以在您的組建伺服器上進行非系統管理安裝，以及輕鬆地將取得工具的作業自動化。 指令碼會負責下載工具，然後將工具解壓縮至預設或指定位置以供使用。 您也可以指定要安裝的工具版本，以及指定要安裝整個 SDK 或只安裝共用執行階段。

在建置開始時，安裝程式指令碼會自動執行，以擷取和安裝所需的 SDK 版本。 「所需版本」是您專案所需建置的任何 SDK 版本。 指令碼可讓您將 SDK 安裝在伺服器上的本機目錄中，從安裝位置執行工具，然後在建置之後清除 (或讓 CI 服務清除)。 這可以為整個建置程序提供封裝和隔離。 您可以在 [dotnet-install](dotnet-install-script.md) 一文中找到安裝指令碼參考。

> [!NOTE]
> **Azure DevOps Services**
>
> 使用安裝程式指令碼時，不會自動安裝原生相依性。 如果作業系統沒有原生相依性，您必須加以安裝。 如需詳細資訊，請參閱 .Net 相依性 [和需求](../install/windows.md#dependencies)。

## <a name="ci-setup-examples"></a>CI 設定範例

本節描述如何使用 PowerShell 或 Bash 指令碼進行手動設定，以及描述幾個軟體即服務 (SaaS) CI 解決方案。 涵蓋的 SaaS CI 解決方案包括 [Travis CI](https://travis-ci.org/)、[AppVeyor](https://www.appveyor.com/) 及 [Azure Pipelines](/azure/devops/pipelines/index)。

### <a name="manual-setup"></a>手動設定

每個 SaaS 服務都有自己用於建立及設定建置程序的方法。 如果您使用上面未列出的其他 SaaS 解決方案，或需要進行超出預先封裝支援的自訂作業，就必須至少執行一些手動設定。

在一般情況下，手動設定需要您取得某一版本的工具 (或該工具的最新每晚組建)，然後執行您的建置指令碼。 您可以使用 PowerShell 或 bash 腳本來協調 .NET 命令，或使用可概述組建流程的專案檔。 [協調流程小節](#orchestrating-the-build)能提供這些選項的更多詳細資料。

在您建立執行手動 CI 組建伺服器設定的指令碼之後，請在您的開發電腦上使用該指令碼，以在本機針對測試目的建置程式碼。 一旦您確認指令碼可在本機正常執行之後，請將它部署到 CI 組建伺服器。 相對簡單的 PowerShell 腳本示範如何取得 .NET SDK，並將它安裝在 Windows 組建伺服器上：

```powershell
$ErrorActionPreference="Stop"
$ProgressPreference="SilentlyContinue"

# $LocalDotnet is the path to the locally-installed SDK to ensure the
#   correct version of the tools are executed.
$LocalDotnet=""
# $InstallDir and $CliVersion variables can come from options to the
#   script.
$InstallDir = "./cli-tools"
$CliVersion = "1.0.1"

# Test the path provided by $InstallDir to confirm it exists. If it
#   does, it's removed. This is not strictly required, but it's a
#   good way to reset the environment.
if (Test-Path $InstallDir)
{
    rm -Recurse $InstallDir
}
New-Item -Type "directory" -Path $InstallDir

Write-Host "Downloading the CLI installer..."

# Use the Invoke-WebRequest PowerShell cmdlet to obtain the
#   installation script and save it into the installation directory.
Invoke-WebRequest `
    -Uri "https://dot.net/v1/dotnet-install.ps1" `
    -OutFile "$InstallDir/dotnet-install.ps1"

Write-Host "Installing the CLI requested version ($CliVersion) ..."

# Install the SDK of the version specified in $CliVersion into the
#   specified location ($InstallDir).
& $InstallDir/dotnet-install.ps1 -Version $CliVersion `
    -InstallDir $InstallDir

Write-Host "Downloading and installation of the SDK is complete."

# $LocalDotnet holds the path to dotnet.exe for future use by the
#   script.
$LocalDotnet = "$InstallDir/dotnet"

# Run the build process now. Implement your build script here.
```

您可以在指令碼結尾處提供建置程序的實作。 指令碼會取得工具，然後執行您的建置程序。 針對 UNIX 電腦，以下 Bash 指令碼會以類似的方式執行 PowerShell 指令碼中描述的動作：

```bash
#!/bin/bash
INSTALLDIR="cli-tools"
CLI_VERSION=1.0.1
DOWNLOADER=$(which curl)
if [ -d "$INSTALLDIR" ]
then
    rm -rf "$INSTALLDIR"
fi
mkdir -p "$INSTALLDIR"
echo Downloading the CLI installer.
$DOWNLOADER https://dot.net/v1/dotnet-install.sh > "$INSTALLDIR/dotnet-install.sh"
chmod +x "$INSTALLDIR/dotnet-install.sh"
echo Installing the CLI requested version $CLI_VERSION. Please wait, installation may take a few minutes.
"$INSTALLDIR/dotnet-install.sh" --install-dir "$INSTALLDIR" --version $CLI_VERSION
if [ $? -ne 0 ]
then
    echo Download of $CLI_VERSION version of the CLI failed. Exiting now.
    exit 0
fi
echo The CLI has been installed.
LOCALDOTNET="$INSTALLDIR/dotnet"
# Run the build process now. Implement your build script here.
```

### <a name="travis-ci"></a>Travis CI

您可以設定 [TRAVIS CI](https://travis-ci.org/) ，以使用 `csharp` 語言和金鑰來安裝 .net SDK `dotnet` 。 如需詳細資訊，請參閱有關[建置 C#、F# 或 Visual Basic 專案](https://docs.travis-ci.com/user/languages/csharp/) \(英文\) 的官方 Travis CI 文件。 在您存取 Travis CI 資訊時，請留意這個由社群維護的 `language: csharp` 語言識別碼可適用於所有 .NET 語言，包括 F# 和 Mono。

Travis CI 會在「建置矩陣」中執行 macOS 和 Linux 作業，您可以在該矩陣中指定執行階段、環境及排除項/包含項的組合，以涵蓋應用程式的組建組合。 如需詳細資訊，請參閱 Travis CI 文件中的 [Customizing the Build](https://docs.travis-ci.com/user/customizing-the-build) (自訂組建) 一文。 MSBuild 型工具會在套件中包含 LTS (1.0.x) 和目前 (1.1.x) 執行階段，所以透過安裝 SDK，您就能獲得進行建置所需的一切項目。

### <a name="appveyor"></a>AppVeyor

[AppVeyor](https://www.appveyor.com/) \(英文\) 會搭配 `Visual Studio 2017` 組建背景工作角色映像安裝 .NET Core 1.0.1 SDK。 有不同版本 .NET SDK 的其他組建映射可供使用。 如需詳細資訊，請參閱 AppVeyor 文件中的 [appveyor.yml 範例](https://github.com/dotnet/docs/blob/master/appveyor.yml) \(英文\) 和 [組建背景工作角色映像](https://www.appveyor.com/docs/build-environment/#build-worker-images) \(英文\) 文章。

您可以使用安裝腳本，在子目錄中下載並解壓縮 .NET SDK 二進位檔，然後將它們新增至 `PATH` 環境變數。 加入組建矩陣，以執行與多個 .NET SDK 版本的整合測試：

```yaml
environment:
  matrix:
    - CLI_VERSION: 1.0.1
    - CLI_VERSION: Latest

install:
  # See appveyor.yml example for install script
```

### <a name="azure-devops-services"></a>Azure DevOps Services

將 Azure DevOps Services 設定為使用下列其中一種方法來建立 .NET 專案：

1. 使用您的命令從[手動設定步驟](#manual-setup)執行指令碼。
1. 建立由數個設定為使用 .NET 工具的 Azure DevOps Services 內建組建工作所組成的組建。

這兩種解決方案都是可行的。 您可以使用手動設定指令碼來控制接收到的工具版本，因為那些工具是以組建之一部分的形式下載的。 組建會從您必須建立的指令碼執行。 本文僅涵蓋手動選項。 如需有關使用 Azure DevOps Services 建置工作來組成組建的詳細資訊，請參閱 [Azure Pipelines](/azure/devops/pipelines/index)\(英文\) 文件。

若要在 Azure DevOps Services 中使用手動設定指令碼，請建立新的組建定義，並指定要針對建置步驟執行的指令碼。 這可使用 Azure DevOps Services 使用者介面來完成：

1. 從建立新的組建定義開始。 當您抵達會提供選項以定義要建立哪一種組建的畫面時，請選取 [空] 選項。

   ![選取空的組建定義](./media/using-ci-with-cli/select-empty-build-definition.png)

1. 設定要建置的存放庫之後，系統就會將您導向至組建定義。 選取 [ **新增組建步驟** ]：

   ![加入建置步驟](./media/using-ci-with-cli/add-build-step.png)

1. 系統會向您顯示 [工作目錄]。 目錄中包含您在組建中使用的工作。 因為您有指令碼，請選取 [PowerShell: 執行 PowerShell 指令碼] 的 [新增] 按鈕。

   ![新增 PowerShell 指令碼步驟](./media/using-ci-with-cli/add-powershell-script.png)

1. 設定建置步驟。 從您正在建置的存放庫加入指令碼：

   ![指定要執行的 PowerShell 指令碼](./media/using-ci-with-cli/powershell-script-path.png)

## <a name="orchestrating-the-build"></a>協調組建

本檔大部分說明如何取得 .NET 工具並設定各種 CI 服務，而不需提供如何使用 .NET Core 來協調或 *實際建立* 程式碼的資訊。 建置程序的結構方式取決於許多因素，無法在這裡以一一涵蓋。 如需有關使用各項技術來協調組建的詳細資訊，請探索 [Travis CI](https://travis-ci.org/)、[AppVeyor](https://www.appveyor.com/) 及 [Azure Pipelines](/azure/devops/pipelines/index) 文件集內所提供的資源與範例。

使用 .NET 工具為 .NET 程式碼建立組建程式的兩個一般方法，是直接使用 MSBuild 或使用 .NET 命令列命令。 您可以視自己對特定方法的熟悉程度並權衡其複雜度，來選擇要使用的方法。 MSBuild 可讓您以工作和目標的形式表示建置程序，但使用此方法必須額外學習 MSBuild 專案檔語法。 使用 .NET 命令列工具可能比較簡單，但需要您以指令碼語言（如或 PowerShell）撰寫協調流程邏輯 `bash` 。

## <a name="see-also"></a>另請參閱

- [.NET 下載 - Linux](https://dotnet.microsoft.com/download?initial-os=linux) \(英文\)
