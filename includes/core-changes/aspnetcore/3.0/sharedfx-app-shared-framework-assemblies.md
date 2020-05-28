---
ms.openlocfilehash: d598d8d3203e804e5e935c3564b0053f9fc2e9a6
ms.sourcegitcommit: ee5b798427f81237a3c23d1fd81fff7fdc21e8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/28/2020
ms.locfileid: "84144958"
---
### <a name="shared-framework-assemblies-removed-from-microsoftaspnetcoreapp"></a>共用架構：從 AspNetCore 移除的元件

從 ASP.NET Core 3.0 開始，ASP.NET Core 共用架構（ `Microsoft.AspNetCore.App` ）只包含由 Microsoft 完全開發、支援及維護的第一方元件。

#### <a name="change-description"></a>變更描述

請將變更視為 ASP.NET Core 「平臺」的界限重新定義。 共用架構會[由任何人透過 GitHub 可建置](https://github.com/dotnet/source-build)，並會繼續為您的應用程式提供 .net Core 共用架構的現有優點。 其中一些優點包括較小的部署大小、集中式修補，以及更快速的啟動時間。

在變更過程中，會引進一些值得注意的重大變更 `Microsoft.AspNetCore.App` 。

#### <a name="version-introduced"></a>引進的版本

3.0

#### <a name="old-behavior"></a>舊的行為

透過 `Microsoft.AspNetCore.App` 專案檔中的元素所參考的專案 `<PackageReference>` 。

此外，還 `Microsoft.AspNetCore.App` 包含下列子元件：

- Json.NET （ `Newtonsoft.Json` ）
- Entity Framework Core （前面加上的元件 `Microsoft.EntityFrameworkCore.` ）
- Roslyn （ `Microsoft.CodeAnalysis` ）

#### <a name="new-behavior"></a>新的行為

的參考不再 `Microsoft.AspNetCore.App` 需要 `<PackageReference>` 專案檔中的元素。 .NET Core SDK 支援名為的新專案 `<FrameworkReference>` ，它會取代的使用 `<PackageReference>` 。

如需詳細資訊，請參閱[dotnet/aspnetcore # 3612](https://github.com/dotnet/aspnetcore/issues/3612)。

Entity Framework Core 隨附為 NuGet 套件。 這種變更會將出貨模型與 .NET 上的所有其他資料存取程式庫對齊。 它提供 Entity Framework Core 最簡單的途徑來繼續進行創新，同時支援各種不同的 .NET 平臺。 從共用架構移出 Entity Framework Core 不會影響其狀態，因為它是 Microsoft 開發、支援及可維護的程式庫。 [.Net Core 支援原則](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)會繼續加以涵蓋。

Json.NET 和 Entity Framework Core 會繼續與 ASP.NET Core 搭配使用。 不過，它們不會包含在共用架構中。

如需詳細資訊，請參閱[.Net Core 3.0 中的 JSON 未來](https://github.com/dotnet/announcements/issues/90)。 另請參閱已從共用架構移除的[完整二進位檔清單](https://github.com/dotnet/aspnetcore/issues/3755)。

#### <a name="reason-for-change"></a>變更的原因

這項變更可簡化的耗用量 `Microsoft.AspNetCore.App` ，並減少 NuGet 套件與共享架構之間的重複。

如需這種變更動機的詳細資訊，請參閱[這篇 blog 文章](https://devblogs.microsoft.com/aspnet/a-first-look-at-changes-coming-in-asp-net-core-3-0/)。

#### <a name="recommended-action"></a>建議的動作

專案不需要使用中的元件 `Microsoft.AspNetCore.App` 做為 NuGet 套件。 為了簡化 ASP.NET Core 共用架構的目標和使用，已不再產生許多自 ASP.NET Core 1.0 所隨附的 NuGet 套件。 這些套件提供的 Api 仍然可供應用程式使用 `<FrameworkReference>` `Microsoft.AspNetCore.App` 。 常見的 API 範例包括 Kestrel、MVC 和 Razor。

這項變更不適用於透過 ASP.NET Core 2.x 參考的所有二進位檔 `Microsoft.AspNetCore.App` 。 值得注意的例外狀況包括：

- `Microsoft.Extensions`繼續以 .NET Standard 為目標的程式庫會以 NuGet 套件的形式提供（請參閱 <https://github.com/dotnet/extensions> ）。
- 不屬於的 ASP.NET Core 小組所產生的 Api `Microsoft.AspNetCore.App` 。 例如，下列元件會以 NuGet 套件的形式提供：
  - Entity Framework Core
  - 提供協力廠商整合的 Api
  - 實驗性功能
  - 相依性無法[滿足共用架構中的需求](https://github.com/dotnet/aspnetcore/blob/4e44e5bcbedd961cc0d4f6b846699c7c494f5597/docs/SharedFramework.md)的 api
- 維護 Json.NET 支援的 MVC 延伸模組。 API 會以 NuGet 套件形式提供，以支援使用 Json.NET 和 MVC。
- SignalR .NET 用戶端將繼續支援 .NET Standard 並以 NuGet 套件形式出貨。 其目的是要用於許多 .NET 執行時間，例如 Xamarin 和 UWP。

如需詳細資訊，請參閱[在3.0 中停止產生共用架構元件的封裝](https://github.com/dotnet/aspnetcore/issues/3756)。 如需討論，請參閱[dotnet/aspnetcore # 3757](https://github.com/dotnet/aspnetcore/issues/3757)。

#### <a name="category"></a>類別

ASP.NET Core

#### <a name="affected-apis"></a>受影響的 API

- <xref:Microsoft.CodeAnalysis?displayProperty=nameWithType>
- <xref:Microsoft.EntityFrameworkCore?displayProperty=nameWithType>

<!--

#### Affected APIs

- `N:Microsoft.CodeAnalysis`
- `N:Microsoft.EntityFrameworkCore`

-->
