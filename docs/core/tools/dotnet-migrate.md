---
title: dotnet migrate 命令
description: dotnet migrate 命令會移轉專案及其所有相依性。
ms.date: 02/14/2020
ms.openlocfilehash: 2e7f9ae5a1d11c54280d914b04df761f0d5aff99
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84284088"
---
# <a name="dotnet-migrate"></a>dotnet migrate

**本文適用于：** ✔️ .net CORE 2.x SDK

## <a name="name"></a>Name

`dotnet migrate` - 將 Preview 2 .NET Core 專案移轉至 .NET Core SDK 型專案。

## <a name="synopsis"></a>概要

```dotnetcli
dotnet migrate [<SOLUTION_FILE|PROJECT_DIR>] [--format-report-file-json <REPORT_FILE>]
    [-r|--report-file <REPORT_FILE>] [-s|--skip-project-references [Debug|Release]]
    [--skip-backup] [-t|--template-file <TEMPLATE_FILE>] [-v|--sdk-package-version]
    [-x|--xproj-file]

dotnet migrate -h|--help
```

## <a name="description"></a>描述

此命令已被取代。 `dotnet migrate`從 .Net Core 3.0 SDK 開始，不再提供此命令。 它只能將 Preview 2 .NET Core 專案遷移至不支援的 1.x .NET Core 專案。

根據預設，命令會移轉根專案和根專案包含的任何專案參考。 這個行為會 `--skip-project-references` 在執行時間使用選項來停用。

可針對下列資產進行移轉：

* 單一專案，方法是指定要遷移的*專案. json*檔案。
* 在*global.asax*檔案中指定的所有目錄，方法是傳遞*json*檔案的路徑。
* *solution.sln* 檔案，移轉方案參考的專案。
* 指定之目錄的所有子目錄，以遞迴方式進行。

`dotnet migrate` 命令會在 `backup` 目錄 (若目錄不存在則會建立) 中保留移轉的 *project.json* 檔案。 使用 `--skip-backup` 選項會覆寫此行為。

根據預設，移轉作業會將移轉程序的狀態輸出到標準輸出 (STDOUT)。 如果使用 `--report-file <REPORT_FILE>` 選項，則輸出會儲存到指定的檔案。

`dotnet migrate` 命令只支援有效的 Preview 2 *project.json* 型專案。 這表示您無法使用它將 DNX 或 Preview 1 *project.json* 型專案直接移轉到 MSBuild/csproj 專案。 您必須先手動將專案移轉到 Preview 2 *project.json* 型專案，然後再使用 `dotnet migrate` 命令移轉該專案。

## <a name="arguments"></a>引數

`PROJECT_JSON/GLOBAL_JSON/SOLUTION_FILE/PROJECT_DIR`

下列其中一項的路徑：

* 要移轉的 *project.json* 檔案。
* *global.json* 檔案：會移轉 *global.json* 中指定的資料夾。
* *solution.sln* 檔案：會移轉方案參考的專案。
* 要移轉的目錄：會在指定目錄內遞迴地搜尋要移轉的 *project.json* 檔案。

如果未指定，則預設值是目前的目錄。

## <a name="options"></a>選項

`--format-report-file-json <REPORT_FILE>`

將移轉報告檔案輸出為 JSON，而非使用者訊息。

`-h|--help`

印出命令的簡短說明。

`-r|--report-file <REPORT_FILE>`

除了主控台外，也將移轉報告輸出到檔案。

`-s|--skip-project-references [Debug|Release]`

略過移轉專案參考。 根據預設，專案參考是以遞迴方式移轉。

`--skip-backup`

在成功遷移之後 *，略*過將* \* xproj*移至目錄的*專案。* `backup`

`-t|--template-file <TEMPLATE_FILE>`

要用於移轉的範本 csproj 檔案。 根據預設，會使用 `dotnet new console` 所置放的相同範本。

`-v|--sdk-package-version <VERSION>`

在已移轉之應用程式中參考的 SDK 套件版本。 預設為 `dotnet new` 中的 SDK 版本。

`-x|--xproj-file <FILE>`

要使用之 xproj 檔案的路徑。 當專案目錄中有多個 xproj 時為必要。

## <a name="examples"></a>範例

移轉目前目錄中的專案和所有其專案對專案相依性：

`dotnet migrate`

移轉 *global.json* 檔案包含的所有專案：

`dotnet migrate path/to/global.json`

只移轉目前的專案而不移轉專案對專案 (P2P) 相依性。 此外，使用特定的 SDK 版本：

`dotnet migrate -s -v 1.0.0-preview4`
