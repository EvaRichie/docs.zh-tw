---
title: .NET Core 2.1 的新功能
description: 了解 .NET Core 2.1 所提供的新功能。
dev_langs:
- csharp
- vb
ms.date: 10/10/2018
ms.openlocfilehash: f125a6a8d9287cb515478a10c2679c07817ae9a6
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91087358"
---
# <a name="whats-new-in-net-core-21"></a>.NET Core 2.1 的新功能

.NET Core 2.1 包含針對下列區域的增強與新功能：

- [Tooling](#tooling)
- [向前復原](#roll-forward)
- [部署](#deployment)
- [Windows 相容性套件](#windows-compatibility-pack)
- [JIT 編譯改進功能](#jit-compiler-improvements)
- [API 變更](#api-changes)

## <a name="tooling"></a>Tooling

隨附於 .NET Core 2.1 的工具 .NET Core 2.1 SDK (2.1.300 版) 包含下列變更與增強功能：

### <a name="build-performance-improvements"></a>建置效能改進

.NET Core 2.1 的主要重點在於改進建置時間效能，特別是針對累加建置。 這些效能改進適用於使用 `dotnet build` 的命令列建置和 Visual Studio 中的建置。 改進的一些個別區域包含：

- 針對套件資產解析，僅解析組建所使用的資產，而非所有資產。

- 組件參考的快取。

- 使用長時間執行的 SDK 組建伺服器，這些是跨越個別 `dotnet build` 引動過程的處理序。 它們消除了每次執行 `dotnet build` 時，需要以 JIT 編譯大型程式碼區塊的需求。 組建伺服器處理序可使用下列命令自動終止：

   ```dotnetcli
   dotnet buildserver shutdown
   ```

### <a name="new-cli-commands"></a>新的 CLI 命令

先前僅能透過 `DotnetCliToolReference` 於個別專案上使用的數個工具，現在皆已做為 .NET Core SDK 的一部分提供。 這些工具包括：

- `dotnet watch` 提供檔案系統監看員，能先等候檔案變更再執行一組指定的命令。 例如，下列命令會自動重建目前的專案，並在其中的檔案發生變更時產生詳細資訊輸出：

   ```dotnetcli
   dotnet watch -- --verbose build
   ```

   請注意到位於 `--verbose` 選項之前的 `--` 選項。 它能將直接傳遞給 `dotnet watch` 命令的選項，與傳遞給子 `dotnet` 處理序的引數分隔開來。 如果沒有它的話，`--verbose` 選項將會套用至 `dotnet watch` 命令，而非 `dotnet build` 命令。
  
   如需詳細資訊，請參閱 [使用 dotnet Watch 開發 ASP.NET Core 應用程式](/aspnet/core/tutorials/dotnet-watch)。

- `dotnet dev-certs` 能產生和管理在開發 ASP.NET Core 應用程式期間使用的憑證。

- `dotnet user-secrets` 能管理 ASP.NET Core 中使用者祕密存放區中的祕密。

- `dotnet sql-cache` 能在 Microsoft SQL Server 資料庫中建立資料表和索引以用於分散式快取。

- `dotnet ef` 是用來管理 Entity Framework Core 應用程式中資料庫、<xref:Microsoft.EntityFrameworkCore.DbContext> 物件和移轉作業的工具。 如需詳細資訊，請參閱 [EF Core .NET 命令列工具](/ef/core/miscellaneous/cli/dotnet)。

### <a name="global-tools"></a>通用工具

.NET Core 2.1 支援*通用工具*，亦即從命令列以通用方式提供的自訂工具。 舊版 .NET Core 的擴充性模型，只能透過使用 `DotnetCliToolReference` 來使自訂工具可供每個專案使用。

若要安裝通用工具，您需使用 [dotnet tool install](../tools/dotnet-tool-install.md) 命令。 例如：

```dotnetcli
dotnet tool install -g dotnetsay
```

安裝之後，您就可在命令列中指定工具名稱來執行該工具。 如需詳細資訊，請參閱 [.NET Core 通用工具概觀](../tools/global-tools.md)。

### <a name="tool-management-with-the-dotnet-tool-command"></a>使用 `dotnet tool` 命令來管理工具

在 .NET Core 2.1 SDK 中，所有工具作業都使用 `dotnet tool` 命令。 有下列選項可供使用：

- [`dotnet tool install`](../tools/dotnet-tool-install.md) 以安裝工具。

- [`dotnet tool update`](../tools/dotnet-tool-update.md) 卸載並重新安裝工具，以有效地加以更新。

- [`dotnet tool list`](../tools/dotnet-tool-list.md) 列出目前已安裝的工具。

- [`dotnet tool uninstall`](../tools/dotnet-tool-uninstall.md) 卸載目前已安裝的工具。

## <a name="roll-forward"></a>向前復原

從 .NET Core 2.0 開始，所有 .NET Core 應用程式都會自動向前復原為系統上安裝的最新次要版本**。

從 .NET Core 2.0 開始，如果用來建立應用程式的 .NET Core 版本不存在於執行時間，應用程式會自動針對最新安裝的 .NET Core *次要版本* 執行。 換句話說，如果應用程式是使用 .NET Core 2.0 建置，而主機系統上不存在 .NET Core 2.0，但是有 .NET Core 2.1，則該應用程式會搭配 NET Core 2.1 執行。

> [!IMPORTANT]
> 此向前復原行為不適用於預覽版本。 根據預設，也不會套用至主要版本，但可透過以下設定進行變更。

您可以透過變更無候選版共用架構的向前復原設定，來修改此行為。 可用的設定為：

- `0` - 停用次要版本向前復原行為。 使用此設定，為 .NET Core 2.0.0 建置的應用程式會向前復原為 .NET Core 2.0.1，而不是 .NET Core 2.2.0 或 .NET Core 3.0.0。
- `1` - 啟用次要版本向前復原行為。 這是設定的預設值。 使用此設定，為 .NET Core 2.0.0 建置的應用程式會依安裝的版本向前復原為 .NET Core 2.0.1 或 NET Core 2.2.0，但不會是 .NET Core 3.0.0。
- `2` - 啟用次要與主要版本的向前復原行為。 若已設定，那麼即使是其他主要版本也會列入考量，因此為 .NET Core 2.0.0 建置的應用程式會向前復原為 .NET Core 3.0.0。

您可用以下三種方式的任一種修改此設定：

- 將 `DOTNET_ROLL_FORWARD_ON_NO_CANDIDATE_FX` 環境變數設定為所需的值。

- 將下面一行新增至 *.runtimeconfig.json* 檔案，並使用所需的值：

   ```json
   "rollForwardOnNoCandidateFx" : 0
   ```

- 使用 [.NET Core CLI](../tools/index.md)時，請將下列選項新增至 .net Core 命令的所需值，例如 `run` ：

   ```dotnetcli
   dotnet run --rollForwardOnNoCandidateFx=0
   ```

修補版本向前復原與此設定無關，而且如有任何次要或主要版本向前復原，在套用之後就會完成。

## <a name="deployment"></a>部署

### <a name="self-contained-application-servicing"></a>獨立的應用程式服務

`dotnet publish` 現在會搭配服務執行階段版本發佈獨立應用程式。 當您搭配 .NET Core 2.1 SDK (2.1.300 版) 發佈獨立應用程式時，應用程式就會包含該 SDK 已知的最新服務執行階段版本。 當您升級至最新的 SDK 時，您將會使用最新的 .NET Core 執行階段版本進行發佈。 這適用於 .NET Core 1.0 執行階段和更新版本。

獨立發行版本依賴 NuGet.org 上的執行階段版本。您的電腦上不需要有服務的執行時間。

使用 .NET Core 2.0 SDK 時，獨立應用程式會搭配 .NET Core 2.0.0 執行階段一起發佈，除非有透過 `RuntimeFrameworkVersion` 屬性指定其他版本。 使用這個新的行為時，您將不再需要設定這個屬性來為獨立應用程式選取較高的執行階段版本。 從現在起，最簡單的方法將會是一律搭配 .NET Core 2.1 SDK (2.1.300 版) 發佈。

如需詳細資訊，請參閱[獨立式部署執行階段向前復原](../deploying/runtime-patch-selection.md)。

## <a name="windows-compatibility-pack"></a>Windows 相容性套件

當您從 .NET Framework 將現有的程式碼移植到 .NET Core 時，可以使用 [Windows 相容性套件](https://www.nuget.org/packages/Microsoft.Windows.Compatibility) \(英文\)。 與 .NET Core 所提供 API 相比，它還額外提供超過 20,000 個 API。 這些 API 包括 <xref:System.Drawing?displayProperty=nameWithType> 命名空間中的類型、<xref:System.Diagnostics.EventLog> 類別、WMI、效能計數器、Windows 服務，以及Windows 登錄類型和成員。

## <a name="jit-compiler-improvements"></a>JIT 編譯器的改進項目

.NET Core 併入新的 JIT 編譯器技術，稱為「階層式編譯」**(也稱為「調適型最佳化」**)，可大幅地提升效能。 階層式編譯是可選擇加入的設定。

由 JIT 編譯器所執行的其中一項重要工作，是將程式碼的執行最佳化。 不過，針對很少使用的程式碼路徑，編譯器將程式碼最佳化的時間，可能會比執行階段執行未最佳化程式碼的時間還要久。 階層式編譯會在 JIT 編譯中引入兩個階段：

- **第一層**：盡快產生程式碼。

- **第二層**：針對那些經常執行的方法產生最佳化的程式碼。 編譯的第二層會以平行方式執行以增強效能。

您能以兩種方式選擇加入階層式編譯。

- 若要在使用 .NET Core 2.1 SDK 的所有專案中使用階層式編譯，請設定下列環境變數：

  ```console
  COMPlus_TieredCompilation="1"
  ```

- 若要針對個別專案使用階層式編譯，請在 MSBuild 專案檔的 `<PropertyGroup>` 區段中加入 `<TieredCompilation>` 屬性，如下列範例所示：

   ```xml
   <PropertyGroup>
      <!-- other property definitions -->

      <TieredCompilation>true</TieredCompilation>
   </PropertyGroup>
   ```

## <a name="api-changes"></a>API 變更

### <a name="spant-and-memoryt"></a>`Span<T>` 和 `Memory<T>`

.NET core 2.1 包含一些新的類型，可讓處理陣列和其他記憶體類型變得更有效率。 新的類型包括：

- <xref:System.Span%601?displayProperty=nameWithType> 和 <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>。

- <xref:System.Memory%601?displayProperty=nameWithType> 和 <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType>。

沒有這些類型的話，當您傳遞項目作為陣列的一部份或記憶體緩衝區的某個區段時，必須先複製該資料的某些部分，然後才能將它傳遞給方法。 這些類型能提供該資料的虛擬檢視，以免除額外配置記憶體和複製作業的需求。

下列範例使用 <xref:System.Span%601> 和 <xref:System.Memory%601> 執行個體來提供陣列中 10 個元素的虛擬檢視。

[!code-csharp[Span\<T>](./snippets/dotnet-core-2-1/csharp/program.cs)]

[!code-vb[Memory\<T>](./snippets/dotnet-core-2-1/vb/program.vb)]

### <a name="brotli-compression"></a>Brotli 壓縮

.NET Core 2.1 新增對 Brotli 壓縮和解壓縮的支援。 Brotli 是定義於 [RFC 7932](https://www.ietf.org/rfc/rfc7932.txt) \(英文\) 中的一般用途無失真壓縮演算法，並受到大部分網頁瀏覽器和主流 Web 伺服器的支援。 您可以使用資料流形式的 <xref:System.IO.Compression.BrotliStream?displayProperty=nameWithType> 類別，或是高效能範圍型的 <xref:System.IO.Compression.BrotliEncoder?displayProperty=nameWithType> 和 <xref:System.IO.Compression.BrotliDecoder?displayProperty=nameWithType> 類別。 下列範例說明搭配 <xref:System.IO.Compression.BrotliStream> 類別進行壓縮：

[!code-csharp[Brotli compression](./snippets/dotnet-core-2-1/csharp/brotli.cs#1)]

[!code-vb[Brotli compression](./snippets/dotnet-core-2-1/vb/brotli.vb#1)]

<xref:System.IO.Compression.BrotliStream> 行為與 <xref:System.IO.Compression.DeflateStream> 和 <xref:System.IO.Compression.GZipStream> 相同，這可讓您輕鬆地將呼叫這些 API 的程式碼轉換為 <xref:System.IO.Compression.BrotliStream>。

### <a name="new-cryptography-apis-and-cryptography-improvements"></a>新的密碼編譯 API 和密碼編譯改進功能

.NET Core 2.1 包含許多針對密碼編譯 API 的增強功能：

- <xref:System.Security.Cryptography.Pkcs.SignedCms?displayProperty=nameWithType> 可在 System.Security.Cryptography.Pkcs 套件中取得。 其實作與 .NET Framework 中的 <xref:System.Security.Cryptography.Pkcs.SignedCms> 類別相同。

- <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHash%2A?displayProperty=nameWithType> 和 <xref:System.Security.Cryptography.X509Certificates.X509Certificate.GetCertHashString%2A?displayProperty=nameWithType> 方法的新多載能接受雜湊演算法識別項，使呼叫端可使用 SHA-1 以外的演算法來取得憑證指紋值。

- 新的 <xref:System.Span%601> 型密碼編譯 API 可用於雜湊、HMAC、亂數密碼編譯產生、非對稱簽章產生、非對稱簽章處理，以及 RSA 加密。

- 透過使用以 <xref:System.Span%601> 為基礎的實作，能使 <xref:System.Security.Cryptography.Rfc2898DeriveBytes?displayProperty=nameWithType> 的效能提升大約 15%。

- 新的 <xref:System.Security.Cryptography.CryptographicOperations?displayProperty=nameWithType> 類別包含兩種新方法：

  - <xref:System.Security.Cryptography.CryptographicOperations.FixedTimeEquals%2A> 會在固定的一段時間傳回任意兩個相同長度的輸入，這很適合用於密碼編譯驗證來避免影響計時側邊通道資訊。

  - <xref:System.Security.Cryptography.CryptographicOperations.ZeroMemory%2A> 為會清除記憶體的常式，且無法進行最佳化。

- 靜態 <xref:System.Security.Cryptography.RandomNumberGenerator.Fill%2A?displayProperty=nameWithType> 方法會以隨機值填滿 <xref:System.Span%601>。

- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms?displayProperty=nameWithType>Linux 和 macOS 現在支援。

- 橢圓曲線 Diffie-Hellman (ECDH) 現在可用於 <xref:System.Security.Cryptography.ECDiffieHellman?displayProperty=nameWithType> 類別系列。 介面區與在 .NET Framework 中的介面區相同。

- <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType> 傳回的執行個體可使用 SHA-2 摘要搭配 OAEP 進行加密或解密，以及使用 RSA-PSS 來產生或驗證簽章。

### <a name="sockets-improvements"></a>通訊端增強功能

.NET Core 包含新的類型 <xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType>，以及重新撰寫的 <xref:System.Net.Http.HttpMessageHandler?displayProperty=nameWithType>，來形成較高層級網路 API 的基礎。  舉例來說，<xref:System.Net.Http.SocketsHttpHandler?displayProperty=nameWithType> 是 <xref:System.Net.Http.HttpClient> 實作的基礎。 在舊版的 .NET Core 當中，較高層級的 API 是以原生網路實作為基礎。

在 .NET Core 2.1 中導入的通訊端實作有一些優點：

- 與之前的實作相比，能提供顯著的效能提升。

- 消除平台相依性，並進一步簡化部署和維護作業。

- 橫跨所有 .NET Core 平台的一致行為。

<xref:System.Net.Http.SocketsHttpHandler> 是 .NET Core 2.1 中的預設實作。 不過，您可以呼叫 <xref:System.AppContext.SetSwitch%2A?displayProperty=nameWithType> 方法來將應用程式設定為使用舊版的 <xref:System.Net.Http.HttpClientHandler> 類別：

```csharp
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", false);
```

```vb
AppContext.SetSwitch("System.Net.Http.UseSocketsHttpHandler", False)
```

您也可以使用環境變數來選擇退出使用以 <xref:System.Net.Http.SocketsHttpHandler> 為基礎的通訊端實作。 若要這麼做，請將 `DOTNET_SYSTEM_NET_HTTP_USESOCKETSHTTPHANDLER` 設為 `false` 或 0。

在 Windows 上，您也可以選擇使用依賴原生實作的 <xref:System.Net.Http.WinHttpHandler?displayProperty=nameWithType>，或是將 <xref:System.Net.Http.SocketsHttpHandler> 類別的執行個體傳遞到 <xref:System.Net.Http.HttpClient> 建構函式來使用該類別。

在 Linux 和 macOS 上，您只能針對個別處理序設定 <xref:System.Net.Http.HttpClient>。 在 Linux 上，如果您要使用舊的 <xref:System.Net.Http.HttpClient> 實作，便需要部署 [libcurl](https://curl.haxx.se/libcurl/) \(英文\)。 (它會隨 .NET Core 2.0 一起安裝)

### <a name="breaking-changes"></a>重大變更

如需有關中斷變更的詳細資訊，請參閱 [從版本2.0 遷移至2.1 的重大變更](../compatibility/2.0-2.1.md)。

## <a name="see-also"></a>另請參閱

- [.NET Core 3.1 的新功能](dotnet-core-3-1.md)
- [EF Core 2.1 的新功能](/ef/core/what-is-new/ef-core-2.1)
- [ASP.NET Core 2.1 的新功能](/aspnet/core/aspnetcore-2.1)
