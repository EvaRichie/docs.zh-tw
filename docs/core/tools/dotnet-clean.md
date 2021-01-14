---
title: dotnet clean 命令
description: dotnet clean 命令會清除目前的目錄。
ms.date: 02/14/2020
ms.openlocfilehash: 1023f13c7662abb7dad613128631c7644ca15bb9
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189599"
---
# <a name="dotnet-clean"></a>dotnet clean

本文 **適用于：** ✔️ .net CORE 2.x SDK 和更新版本

## <a name="name"></a>名稱

`dotnet clean` - 清除專案的輸出。

## <a name="synopsis"></a>概要

```dotnetcli
dotnet clean [<PROJECT>|<SOLUTION>] [-c|--configuration <CONFIGURATION>]
    [-f|--framework <FRAMEWORK>] [--interactive]
    [--nologo] [-o|--output <OUTPUT_DIRECTORY>]
    [-r|--runtime <RUNTIME_IDENTIFIER>] [-v|--verbosity <LEVEL>]

dotnet clean -h|--help
```

## <a name="description"></a>Description

`dotnet clean` 命令會清除前一個組建的輸出。 它會實作為 [MSBuild 目標](/visualstudio/msbuild/msbuild-targets)，因此命令在執行的時候會評估專案。 只會清除在建置期間建立的輸出。 中繼 (*obj*) 和最後輸出 (*bin*) 這兩個資料夾都會清除。

## <a name="arguments"></a>引數

`PROJECT | SOLUTION`

要清除的 MSBuild 專案或方案。 MSBuild 會在目前工作目錄中搜尋副檔名以 *proj* 或 *sln* 結尾的檔案，並使用該檔案。

## <a name="options"></a>選項

* **`-c|--configuration <CONFIGURATION>`**

  定義組建組態。 大部分專案的預設值為 `Debug` ，但您可以覆寫專案中的組建設定。 如果在建置階段指定此選項，清除時才需要使用它。

* **`-f|--framework <FRAMEWORK>`**

  在建置時間指定的[架構](../../standard/frameworks.md)。 架構必須定義於[專案檔](../project-sdk/overview.md)中。 如果在建置階段指定架構，則您必須在清除時指定該架構。

* **`-h|--help`**

  印出命令的簡短說明。

* **`--interactive`**

  可讓命令停止，並等候使用者輸入或進行動作。 例如完成驗證。 自 .NET Core 3.0 SDK 起提供。

* **`--nologo`**

  不要顯示程式啟始橫幅或著作權訊息。 自 .NET Core 3.0 SDK 起提供。

* **`-o|--output <OUTPUT_DIRECTORY>`**

  包含要清除組建成品的目錄。 如果您在建置專案時指定架構，請搭配輸出目錄參數來指定 `-f|--framework <FRAMEWORK>` 參數。

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  清除指定執行階段的輸出資料夾。 建立[獨立性部署 (SCD)](../deploying/index.md#publish-self-contained) 時會使用此選項。

* **`-v|--verbosity <LEVEL>`**

  設定 MSBuild 詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。 預設為 `normal`。

## <a name="examples"></a>範例

* 清除專案的預設組建︰

  ```dotnetcli
  dotnet clean
  ```

* 清除使用發行組態來建置的專案︰

  ```dotnetcli
  dotnet clean --configuration Release
  ```
