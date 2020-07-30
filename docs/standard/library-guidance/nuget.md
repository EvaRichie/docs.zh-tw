---
title: NuGet 與 .NET 程式庫
description: 針對 .NET 程式庫搭配 NuGet 進行封裝的最佳做法建議。
ms.date: 01/15/2019
ms.openlocfilehash: d9f8d7cc4402a87e1429791b57a0306b318dfbe4
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87382109"
---
# <a name="nuget"></a>NuGet

NuGet 是適用於 .NET 生態系統的套件管理員，也是開發人員探索並取得 .NET 開放原始碼程式庫的主要方式。 [NuGet.org](https://www.nuget.org/) \(英文\) 是 Microsoft 提供用來裝載 NuGet 套件的免費服務，它是公用 NuGet 套件的主要主機；但您也可以發佈至自訂的 NuGet 服務，例如 [MyGet](https://www.myget.org/) \(英文\) 與 [Azure Artifacts](https://azure.microsoft.com/services/devops/artifacts/)。

![NuGet](./media/nuget/nuget-logo.png "NuGet")

## <a name="create-a-nuget-package"></a>建立 NuGet 套件

NuGet 套件 (`*.nupkg`) 是包含 .NET 組件與相關聯中繼資料的 Zip 檔案。

有兩種主要的方式可用來建立 NuGet 套件。 較新且建議的方式，是從 SDK 樣式專案 (內容以 `<Project Sdk="Microsoft.NET.Sdk">` 作為開頭的專案) 建立套件。 系統會自動將組件與目標新增到套件中，並將剩餘的中繼資料新增到 MSBuild 檔案，例如套件名稱與版本號碼。 使用命令進行編譯會輸出檔案， [`dotnet pack`](../../core/tools/dotnet-pack.md) `*.nupkg` 而不是元件。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <AssemblyName>Contoso.Api</AssemblyName>
    <PackageVersion>1.1.0</PackageVersion>
    <Authors>John Doe</Authors>
  </PropertyGroup>
</Project>
```

較舊的 NuGet 套件建立方式，是使用 `*.nuspec` 檔案與 `nuget.exe` 命令列工具來建立。 nuspec 檔案可讓您做出大幅度的控制，但您必須仔細地指定要在最終的 NuGet 套件中包含哪些組件與目標。 這是一件很容易出錯的工作，也很容易在未來做出變更後忘記更新 nuspec 檔案。 nuspec 的優點在於您可以用它來針對尚未支援 SDK 樣式專案檔的架構建立 NuGet 套件。

✔️ 請考慮使用 SDK 樣式專案檔來建立 NuGet 套件。

## <a name="package-dependencies"></a>套件相依性

NuGet 套件相依性已詳述於[相依性](./dependencies.md)一文中。

## <a name="important-nuget-package-metadata"></a>重要的 NuGet 套件中繼資料

NuGet 套件能支援許多[中繼資料屬性](/nuget/reference/nuspec)。 下表包含 NuGet.org 上所有套件都應提供的核心中繼資料：

| MSBuild 屬性名稱              | Nuspec 名稱              | 描述  |
| ---------------------------------- | ------------------------ | ------------ |
| `PackageId`                        | `id`                       | 封裝識別碼。 如果來自識別碼的前置詞符合[準則](/nuget/reference/id-prefix-reservation)，便可以對它進行保留。 |
| `PackageVersion`                   | `version`                  | NuGet 套件版本。 如需詳細資訊，請參閱 [NuGet 套件版本](./versioning.md#nuget-package-version)。             |
| `Title`                            | `title`                    | 人類容易記住的套件標題。 預設值為 `PackageId`。             |
| `Description`                      | `description`              | 在 UI 中顯示的套件詳細描述。             |
| `Authors`                          | `authors`                  | 以逗號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。             |
| `PackageTags`                      | `tags`                     | 以空格分隔的標記與關鍵字清單，能描述套件。 標記會在搜尋套件時使用。             |
| `PackageIcon`                   | `icon`                  | 封裝中要當做封裝圖示使用之影像的路徑。 閱讀更多[ `icon` 中繼資料](/nuget/reference/nuspec#icon)的相關資訊。 |
| `PackageProjectUrl`                | `projectUrl`               | 專案首頁或來源存放庫的 URL。             |
| `PackageLicenseExpression`         | `license`                  | 專案授權的 [SPDX 識別碼](https://spdx.org/licenses/)。 只有 OSI 和 FSF 核准的授權可以使用識別碼。 其他授權應該使用 `PackageLicenseFile`。 閱讀更多[ `license` 中繼資料](/nuget/reference/nuspec#license)的相關資訊。 |

> [!IMPORTANT]
> 沒有授權的專案預設會具有[專屬著作權](https://choosealicense.com/no-permission/)，這會使其他人無法合法使用它。

✔️ 請考慮選擇具有符合 NuGet 的前置詞保留[準則](/nuget/reference/id-prefix-reservation)之前置詞的 NuGet 套件名稱。

✔️ 請務必為您的套件圖示使用 HTTPS href。

> NuGet.org 等網站會在啟用 HTTPS 的情況下執行，因此顯示非 HTTPS 影像將會產生混合內容警告。

✔️ 請務必使用大小為 64x64 且具有透明背景的套件圖示影像，以取得最佳檢視效果。

✔️ 請考慮設定[來源連結](./sourcelink.md)以將原始程式碼控制中繼資料新增到您的組件與 NuGet 套件。

> 來源連結會自動將 `RepositoryUrl` 和 `RepositoryType` 中繼資料新增到 NuGet 套件。 來源連結也會新增套件建置所根據確切原始碼的相關資訊。 例如，從 Git 存放庫建立的套件將會新增認可雜湊作為中繼資料。

## <a name="pre-release-packages"></a>發行前套件

具有版本尾碼的 NuGet 套件會被系統視為[發行前版本](/nuget/create-packages/prerelease-packages)。 根據預設，NuGet 套件管理員 UI 只會顯示穩定版本，除非使用者選擇加入發行前套件；這使得發行前套件很適合用來進行有限使用者測試。

```xml
<PackageVersion>1.0.1-beta1</PackageVersion>
```

> [!NOTE]
> 穩定套件無法相依於發行前套件。 您必須使自己的套件成為發行前版本，或是相依於較舊的穩定版本。

![NuGet 發行前套件相依性](./media/nuget/nuget-prerelease-package.png "NuGet 發行前套件相依性")

✔️ 請務必在進行測試、預覽或實驗時發佈發行前套件。

✔️ 請務必在套件準備好時發佈穩定版本，使其他穩定套件可以參考它。

## <a name="symbol-packages"></a>符號套件

符號檔 (`*.pdb`) 是由 .NET 編譯器連同組件一起產生。 符號檔會將執行位置對應至原始程式碼，使您可以在使用偵錯工具執行原始程式碼時逐步執行它。 NuGet 支援連同包含 .NET 組件的主要套件，一起[產生包含符號檔的個別符號套件 (`*.snupkg`)](/nuget/create-packages/symbol-packages-snupkg)。 符號套件的概念在於它們會被裝載在符號伺服器上，而且只會由 Visual Studio 之類的工具依需求下載。

NuGet.org 裝載自己的[符號伺服器存放庫](/nuget/create-packages/symbol-packages-snupkg#nugetorg-symbol-server)。 開發人員可以使用發佈至 NuGet.org 符號伺服器的符號，方法是將 `https://symbols.nuget.org/download/symbols` 新增至其[在 Visual Studio 中的符號來源](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)。

> [!IMPORTANT]
> NuGet.org 符號伺服器只支援 SDK 樣式專案所建立的新[便攜符號](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md)檔（ `*.pdb` ）。
>
> 若要在調試 .NET 程式庫時使用 NuGet.org 符號伺服器，開發人員必須具有 Visual Studio 2017 15.9 版或更新版本。

建立符號套件的替代方案是在主要的 NuGet 套件中內嵌符號檔。 主要的 NuGet 套件會較大，但內嵌的符號檔表示開發人員不需要設定 NuGet.org 符號伺服器。 如果您正在使用 SDK 樣式專案建置 NuGet 套件，您可以透過設定 `AllowedOutputExtensionsInPackageBuildOutputFolder` 屬性來內嵌符號檔：

```xml
<Project Sdk="Microsoft.NET.Sdk">
 <PropertyGroup>
    <!-- Include symbol files (*.pdb) in the built .nupkg -->
    <AllowedOutputExtensionsInPackageBuildOutputFolder>$(AllowedOutputExtensionsInPackageBuildOutputFolder);.pdb</AllowedOutputExtensionsInPackageBuildOutputFolder>
  </PropertyGroup>
</Project>
```

內嵌符號檔缺點是它們會讓使用 SDK 樣式專案編譯的 .NET 程式庫套件大小增加約 30%。 如果套件大小是個問題，您應該改為將符號發佈在符號套件中。

✔️ 請考慮將符號以符號套件 (`*.snupkg`) 形式發佈至 NuGet.org

> 符號套件 (`*.snupkg`) 提供開發人員良好的隨選偵錯體驗，不會讓主要套件大小過大，而對不想要偵錯 NuGet 套件的人在還原效能方面造成影響。
>
> 要注意的是，使用者可能需要在其 IDE 中尋找並設定 NuGet 符號伺服器（以一次性設定的形式）來取得符號檔。 Visual Studio 2019 16.1 版已將 NuGet. 組織的符號伺服器新增至預設符號伺服器清單。

>[!div class="step-by-step"]
>[上一個](strong-naming.md) 
>[下一步](dependencies.md)
