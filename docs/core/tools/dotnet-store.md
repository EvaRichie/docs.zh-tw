---
title: dotnet store 命令
description: "'dotnet store' 命令會在執行階段套件存放區中儲存指定的組件。"
ms.date: 02/14/2020
ms.openlocfilehash: 8efb11c6bf648bc7787d5627e02b180abb8a0afd
ms.sourcegitcommit: b201d177e01480a139622f3bf8facd367657a472
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634333"
---
# <a name="dotnet-store"></a>dotnet store

本文 **適用于：** ✔️ .net CORE 2.x SDK 和更新版本

## <a name="name"></a>名稱

`dotnet store` - 會在[執行階段套件存放區](../deploying/runtime-store.md)中儲存指定的組件。

## <a name="synopsis"></a>概要

```dotnetcli
dotnet store -m|--manifest <PATH_TO_MANIFEST_FILE>
    -f|--framework <FRAMEWORK_VERSION> -r|--runtime <RUNTIME_IDENTIFIER>
    [--framework-version <FRAMEWORK_VERSION>] [--output <OUTPUT_DIRECTORY>]
    [--skip-optimization] [--skip-symbols] [-v|--verbosity <LEVEL>]
    [--working-dir <WORKING_DIRECTORY>]

dotnet store -h|--help
```

## <a name="description"></a>描述

`dotnet store` 會在[執行階段套件存放區](../deploying/runtime-store.md)中儲存指定的組件。 根據預設，會針對目標執行階段和架構最佳化組件。 如需詳細資訊，請參閱[執行階段套件存放區](../deploying/runtime-store.md)主題。

## <a name="required-options"></a>必要選項

- **`-f|--framework <FRAMEWORK>`**

  指定[目標 Framework](../../standard/frameworks.md)。 必須在專案檔中指定此目標架構。

- **`-m|--manifest <PATH_TO_MANIFEST_FILE>`**

  「套件存放區資訊清單檔」是 XML 檔，包含要儲存的套件清單。 資訊清單檔的格式相容於 SDK 樣式專案格式。 因此，參考所需套件的專案檔可以搭配 `-m|--manifest` 選項，將組件儲存在執行階段套件存放區中。 若要指定多個資訊清單檔，請為每個檔案重複選項和路徑。 例如：`--manifest packages1.csproj --manifest packages2.csproj`。

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  要設為目標的 [執行時間識別碼](../rid-catalog.md) 。

## <a name="optional-options"></a>選擇性的選項

- **`--framework-version <FRAMEWORK_VERSION>`**

  指定 .NET SDK 版本。 此選項可讓您在 `-f|--framework` 選項指定的 Framework 之外，選取特定的 Framework 版本。

- **`-h|--help`**

  顯示說明資訊。

- **`-o|--output <OUTPUT_DIRECTORY>`**

  指定執行階段套件存放區的路徑。 如果未指定，則會預設為使用者設定檔 .NET 安裝目錄的 *儲存* 子目錄。

- **`--skip-optimization`**

  略過最佳化階段。

- **`--skip-symbols`**

  略過符號產生。 目前，只能在 Windows 和 Linux 產生符號。

- **`-v|--verbosity <LEVEL>`**

  設定命令的詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

- **`-w|--working-dir <WORKING_DIRECTORY>`**

  命令使用的工作目錄。 如未指定，則使用目前目錄的 *obj* 子目錄。

## <a name="examples"></a>範例

- 儲存 .NET Core 2.0.0 的 *packages.csproj* 專案中指定的套件：

  ```dotnetcli
  dotnet store --manifest packages.csproj --framework-version 2.0.0
  ```

- 儲存 *packages.csproj* 中指定的套件，不需要最佳化：

  ```dotnetcli
  dotnet store --manifest packages.csproj --skip-optimization
  ```

## <a name="see-also"></a>另請參閱

- [執行階段套件存放區](../deploying/runtime-store.md)
