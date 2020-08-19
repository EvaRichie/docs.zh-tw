---
title: 執行階段套件存放區
description: 了解如何使用 .NET Core 所使用的執行階段套件存放區和目標資訊清單。
ms.date: 08/12/2017
ms.openlocfilehash: e9e27ef535dbd9e7197c323f7e49a9960aeff0f9
ms.sourcegitcommit: cbb19e56d48cf88375d35d0c27554d4722761e0d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/19/2020
ms.locfileid: "88608356"
---
# <a name="runtime-package-store"></a>執行階段套件存放區

從 .NET Core 2.0 開始，可針對目標環境中存在的已知套件集合封裝和部署應用程式。 優點是部署更快、磁碟空間使用量較少，而且啟動效能在某些情況下有所改善。

這項功能實作為「執行階段套件存放區」**，這是套件儲存所在磁碟的目錄 (通常在 macOS/Linux 是 */usr/local/share/dotnet/store*，在 Windows 是 *C:/Program Files/dotnet/store*)。 在此目錄下，有架構和[目標 Framework](../../standard/frameworks.md) 的子目錄。 檔案配置類似於[磁碟上的 NuGet 資產配置](/nuget/create-packages/supporting-multiple-target-frameworks#framework-version-folder-structure)方式：

```
\dotnet
    \store
        \x64
            \netcoreapp2.0
                \microsoft.applicationinsights
                \microsoft.aspnetcore
                ...
        \x86
            \netcoreapp2.0
                \microsoft.applicationinsights
                \microsoft.aspnetcore
                ...
```

「目標資訊清單」** 檔會列出執行階段套件存放區中的套件。 開發人員可在發佈其應用程式時，以此資訊清單為目標。 目標資訊清單通常是由目標生產環境的擁有者提供。

## <a name="preparing-a-runtime-environment"></a>準備執行階段環境

執行階段環境的系統管理員可以建置執行階段套件存放區和對應的目標資訊清單，以最佳化應用程式，取得更快的部署和較少的磁碟使用空間。

第一個步驟是建立「套件存放區資訊清單」**，列出撰寫執行階段套件存放區的套件。 此檔案格式與專案檔格式 (*csproj*) 相容。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <ItemGroup>
    <PackageReference Include="NUGET_PACKAGE" Version="VERSION" />
    <!-- Include additional packages here -->
  </ItemGroup>
</Project>
```

**範例**

下例使用套件存放區資訊清單 (*packages.csproj*) 將 [`Newtonsoft.Json`](https://www.nuget.org/packages/Newtonsoft.Json/) 和 [`Moq`](https://www.nuget.org/packages/moq/) 新增至執行階段套件存放區：

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
    <PackageReference Include="Moq" Version="4.7.63" />
  </ItemGroup>
</Project>
```

執行 `dotnet store` 加上套件存放區資訊清單、執行階段和架構，佈建執行階段套件存放區：

```dotnetcli
dotnet store --manifest <PATH_TO_MANIFEST_FILE> --runtime <RUNTIME_IDENTIFIER> --framework <FRAMEWORK>
```

**範例**

```dotnetcli
dotnet store --manifest packages.csproj --runtime win10-x64 --framework netcoreapp2.0 --framework-version 2.0.0
```

您可以 [`dotnet store`](../tools/dotnet-store.md) 在命令中重複選項和路徑，以將多個目標套件存放區資訊清單路徑傳遞至單一命令。

根據預設，命令的輸出位在使用者設定檔的 *.dotnet/store* 子目錄下的套件存放區中。 您可以使用 `--output <OUTPUT_DIRECTORY>` 選項指定不同的位置。 存放區的根目錄包含目標資訊清單 *artifact.xml* 檔案。 此檔案可供下載，並可供想要在發行時以此存放區為目標的應用程式作者使用。

**範例**

執行上例後，會產生以下 *artifact.xml* 檔案。 請注意，是的相依性 [`Castle.Core`](https://www.nuget.org/packages/Castle.Core/) `Moq` ，因此它會自動包含，並顯示在 *artifacts.xml* 資訊清單檔中。

```xml
<StoreArtifacts>
  <Package Id="Newtonsoft.Json" Version="10.0.3" />
  <Package Id="Castle.Core" Version="4.1.0" />
  <Package Id="Moq" Version="4.7.63" />
</StoreArtifacts>
```

## <a name="publishing-an-app-against-a-target-manifest"></a>針對目標資訊清單發行應用程式

如果您在磁片上有目標資訊清單檔案，您可以在使用下列命令發佈應用程式時，指定檔案的路徑 [`dotnet publish`](../tools/dotnet-publish.md) ：

```dotnetcli
dotnet publish --manifest <PATH_TO_MANIFEST_FILE>
```

**範例**

```dotnetcli
dotnet publish --manifest manifest.xml
```

您會將所產生的已發行應用程式，部署到有目標資訊清單所述套件的環境中。 無法這樣做，會導致應用程式無法啟動。

重複選項和路徑 (例如 `--manifest manifest1.xml --manifest manifest2.xml`)，以在發行應用程式時，指定多個目標資訊清單。 當您這樣做時，會針對提供給命令的目標資訊清單檔中指定的套件聯集修剪應用程式。

如果您部署的應用程式具有存在於部署中的資訊清單相依性 (組件位於 *bin* 資料夾)，主機對該組件「不會使用」** 執行階段套件存放區。 無論主機的執行階段套件存放區是否有 *bin* 資料夾組件，都使用它。

資訊清單中指示的相依性版本，必須符合執行階段套件存放區中的相依性版本。 如果目標資訊清單中的相依性版本與執行階段套件存放區的版本不相符，而應用程式的部署中不包含必要的套件版本，則應用程式無法啟動。 例外狀況包含目標資訊清單的名稱，為執行階段套件存放區組件所稱呼的名稱，有利於針對不符合進行疑難排解。

於發行時「修剪」** 部署，已發行的輸出只保留您指定的資訊清單套件特定版本。 主機必須要有指定版本的套件，應用程式才能啟動。

## <a name="specifying-target-manifests-in-the-project-file"></a>在專案檔中指定目標資訊清單

使用命令指定目標資訊清單的另一種 [`dotnet publish`](../tools/dotnet-publish.md) 方式，是在專案檔中將它們指定為標記下的以分號分隔的路徑清單 **\<TargetManifestFiles>** 。

```xml
<PropertyGroup>
  <TargetManifestFiles>manifest1.xml;manifest2.xml</TargetManifestFiles>
</PropertyGroup>
```

只有當應用程式的目標環境為已知時，例如 .NET Core 專案，才在專案檔中指定目標資訊清單。 這不是開放原始碼專案的情況。 開放原始碼專案的使用者通常會將它部署到不同的生產環境中。 這些生產環境通常會有不同的預先安裝的套件集。 您無法對這類環境中的目標資訊清單進行假設，因此您應該使用的 `--manifest` 選項 [`dotnet publish`](../tools/dotnet-publish.md) 。

## <a name="aspnet-core-implicit-store-net-core-20-only"></a>ASP.NET Core 隱含存放區 ( 僅限 .NET Core 2.0) 

ASP.NET Core 隱含存放區只適用於 ASP.NET Core 2.0。 強烈建議應用程式使用 ASP.NET Core 2.1 和更新版本，這些**不**會使用隱含存放區。 ASP.NET Core 2.1 和更新版本會使用共用的架構。

若為 .NET Core 2.0，當應用程式部署為與 [framework 相依的部署](index.md#publish-framework-dependent) 應用程式時，ASP.NET Core 的應用程式會隱含地使用執行時間套件存放區功能。 中的目標 [`Microsoft.NET.Sdk.Web`](https://github.com/aspnet/websdk) 包含在目標系統上參考隱含封裝存放區的資訊清單。 此外，相依于套件的任何 framework 相依應用程式都會 `Microsoft.AspNetCore.All` 產生已發佈的應用程式，其中只包含應用程式及其資產，而不包含中繼套件中所列的套件 `Microsoft.AspNetCore.All` 。 假設這些套件存在於目標系統上。

安裝 .NET Core SDK 時，執行階段套件存放區會安裝在主機上。 其他的安裝程式可能會提供執行階段套件存放區，包括 .NET Core SDK 的 Zip/tarball 安裝、`apt-get`、Red Hat Yum、.NET Core Windows Server 裝載組合，以及手動的執行階段套件存放區安裝。

部署與 [framework 相依的部署](index.md#publish-framework-dependent) 應用程式時，請確定目標環境已安裝 .NET Core SDK。 如果將應用程式部署到不包含 ASP.NET Core 的環境，您可以在專案檔中指定 set to 來退出隱含存放區，  **\<PublishWithAspNetCoreTargetManifest>** `false` 如下列範例所示：

```xml
<PropertyGroup>
  <PublishWithAspNetCoreTargetManifest>false</PublishWithAspNetCoreTargetManifest>
</PropertyGroup>
```

> [!NOTE]
> 針對獨立式 [部署](index.md#publish-self-contained) 應用程式，假設目標系統不一定包含所需的資訊清單套件。 因此， **\<PublishWithAspNetCoreTargetManifest>** 不能為 `true` 獨立應用程式設定為。

## <a name="see-also"></a>另請參閱

- [dotnet-publish](../tools/dotnet-publish.md)
- [dotnet-store](../tools/dotnet-store.md)
