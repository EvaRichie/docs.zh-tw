---
title: dotnet nuget push 命令
description: dotnet nuget push 命令會將套件推送至伺服器並發行。
author: karann-msft
ms.date: 02/14/2020
ms.openlocfilehash: 99e735f7bb18b7af1c12c3ef77fc150a19083542
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970651"
---
# <a name="dotnet-nuget-push"></a>dotnet nuget push

本文 **適用于：** ✔️ .net CORE 2.x SDK 和更新版本

## <a name="name"></a>名稱

`dotnet nuget push` - 將套件推送至伺服器並發行。

## <a name="synopsis"></a>概要

```dotnetcli
dotnet nuget push [<ROOT>] [-d|--disable-buffering] [--force-english-output]
    [--interactive] [-k|--api-key <API_KEY>] [-n|--no-symbols true]
    [--no-service-endpoint] [-s|--source <SOURCE>] [--skip-duplicate]
    [-sk|--symbol-api-key <API_KEY>] [-ss|--symbol-source <SOURCE>]
    [-t|--timeout <TIMEOUT>]

dotnet nuget push -h|--help
```

## <a name="description"></a>描述

`dotnet nuget push` 命令會將套件推送至伺服器並發行。 推送命令會使用在系統 NuGet 組態檔案或組態檔案鏈中找到的伺服器及認證詳細資料。 如需組態檔的詳細資訊，請參閱[設定 NuGet 行為](/nuget/consume-packages/configuring-nuget-behavior)。 NuGet 預設組態的取得方式如下：載入 *%AppData%\NuGet\NuGet.config* (Windows) 或 *$HOME/.local/share* (Linux/macOS)，接著從磁碟機根目錄開始直到目前目錄，載入其中的任何 *nuget.config* 或 *.nuget\nuget.config*。

此命令會推送現有的封裝。 它不會建立套件。 若要建立封裝，請使用 [`dotnet pack`](dotnet-pack.md) 。

## <a name="arguments"></a>引數

- **`ROOT`**

  指定套件推送目標的檔案路徑。

## <a name="options"></a>選項

- **`-d|--disable-buffering`**

  推送至 HTTP(S) 伺服器時停用緩衝處理以減少記憶體使用量。

- **`--force-english-output`**

  強制使用非變異英文文化特性來執行應用程式。

- **`-h|--help`**

  印出命令的簡短說明。

- **`--interactive`**

  允許命令進行封鎖及要求對驗證之類的作業採取手動動作。 自 .NET Core 2.2 SDK 起可用的選項。

- **`-k|--api-key <API_KEY>`**

  伺服器的 API 金鑰。

- **`-n|--no-symbols true`**

  不推送符號 (即使存在)。

- **`--no-service-endpoint`**

  不會將 "api/v2/package" 附加至來源 URL。 自 .NET Core 2.1 SDK 起可用的選項。

- **`-s|--source <SOURCE>`**

  指定伺服器 URL。 NuGet 會識別 UNC 或本機資料夾來源，只複製檔案，而不是使用 HTTP 推送。
  > [!IMPORTANT]
  > 從 NuGet 3.4.2 開始，除非 NuGet 設定檔指定值，否則此為必要參數 `DefaultPushSource` 。 如需詳細資訊，請參閱[設定 NuGet 行為](/nuget/consume-packages/configuring-nuget-behavior)。

- **`--skip-duplicate`**

  將多個封裝推送至 HTTP (S) server 時，會將任何409衝突回應視為警告，讓推送可以繼續。 自 .NET Core 3.1 SDK 起提供。

- **`-sk|--symbol-api-key <API_KEY>`**

  符號伺服器的 API 金鑰。

- **`-ss|--symbol-source <SOURCE>`**

  指定符號伺服器 URL。

- **`-t|--timeout <TIMEOUT>`**

  指定推送至伺服器的逾時 (以秒為單位)。 預設為 300 秒 (5 分鐘)。 指定 0 (零秒) 會套用預設值。

## <a name="examples"></a>範例

- 使用 API 金鑰，將 *foo. nupkg* 推送至 NuGet 設定檔中指定的預設推送來源：

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a
  ```

- 將 *foo. nupkg* 推送至官方 NuGet 伺服器，並指定 API 金鑰：

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://api.nuget.org/v3/index.json
  ```
  
  * 將 *foo.nupkg* 推送至自訂推送來源 `https://customsource`，指定 API 金鑰：

  ```dotnetcli
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
  ```

- 將 *foo. nupkg* 推送至 NuGet 設定檔中指定的預設推送來源：

  ```dotnetcli
  dotnet nuget push foo.nupkg
  ```

- 將 *foo. nupkg* 至預設符號來源：

  ```dotnetcli
  dotnet nuget push foo.symbols.nupkg
  ```

- 將 *foo. nupkg* 推送至 NuGet 設定檔中指定的預設推送來源，並提供360秒的超時時間：

  ```dotnetcli
  dotnet nuget push foo.nupkg --timeout 360
  ```

- 將目前目錄中的所有 *nupkg* 檔案推送至 NuGet 設定檔中指定的預設推送來源：

  ```dotnetcli
  dotnet nuget push "*.nupkg"
  ```

  > [!NOTE]
  > 如果此命令無法運作，可能是舊版 SDK (.NET Core 2.1 SDK 及更舊版本) 中有 Bug 所致。
  > 若要修正此問題，請升級您的 SDK 版本，或改為執行下列命令：`dotnet nuget push "**/*.nupkg"`
  
  > [!NOTE]
  > Shell （例如執行檔案萬用字元的 bash）必須要有內含引號。 如需詳細資訊，請參閱 [NuGet/Home # 4393](https://github.com/NuGet/Home/issues/4393#issuecomment-667618120)。

- 將所有 *nupkg* 檔案推送至 NuGet 設定檔中指定的預設推送來源，即使 HTTP (S) 伺服器傳回409衝突回應：

  ```dotnetcli
  dotnet nuget push "*.nupkg" --skip-duplicate
  ```

- 將目前目錄中的所有 *nupkg* 檔案推送至本機摘要目錄：

  ```dotnetcli
  dotnet nuget push "*.nupkg" -s c:\mydir
  ```

  此命令不會將封裝儲存在階層式資料夾結構中，建議您將效能優化。 如需詳細資訊，請參閱 [本機](/nuget/hosting-packages/local-feeds)摘要。  
