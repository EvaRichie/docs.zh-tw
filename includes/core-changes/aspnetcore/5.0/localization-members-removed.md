---
ms.openlocfilehash: 6deeb7debce9b731f3871b7de0ad8df8a8cdafea
ms.sourcegitcommit: 7370aa8203b6036cea1520021b5511d0fd994574
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/02/2020
ms.locfileid: "82728270"
---
### <a name="localization-resourcemanagerwithculturestringlocalizer-class-and-withculture-interface-member-removed"></a><span data-ttu-id="be616-101">當地語系化：已移除 ResourceManagerWithCultureStringLocalizer 類別和 WithCulture 介面成員</span><span class="sxs-lookup"><span data-stu-id="be616-101">Localization: ResourceManagerWithCultureStringLocalizer class and WithCulture interface member removed</span></span>

<span data-ttu-id="be616-102">已移除 .NET 5.0 Preview 1 中的[ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1)類別和[WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1)方法。</span><span class="sxs-lookup"><span data-stu-id="be616-102">The [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) class and [WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) method were removed in .NET 5.0 Preview 1.</span></span>

<span data-ttu-id="be616-103">如需內容，請參閱[aspnet/公告 # 346](https://github.com/aspnet/Announcements/issues/346)和[dotnet/aspnetcore # 3324](https://github.com/dotnet/aspnetcore/issues/3324)。</span><span class="sxs-lookup"><span data-stu-id="be616-103">For context, see [aspnet/Announcements#346](https://github.com/aspnet/Announcements/issues/346) and [dotnet/aspnetcore#3324](https://github.com/dotnet/aspnetcore/issues/3324).</span></span> <span data-ttu-id="be616-104">如需這種變更的討論，請參閱[dotnet/aspnetcore # 7756](https://github.com/dotnet/aspnetcore/issues/7756)。</span><span class="sxs-lookup"><span data-stu-id="be616-104">For discussion on this change, see [dotnet/aspnetcore#7756](https://github.com/dotnet/aspnetcore/issues/7756).</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="be616-105">引進的版本</span><span class="sxs-lookup"><span data-stu-id="be616-105">Version introduced</span></span>

<span data-ttu-id="be616-106">5.0 Preview 1</span><span class="sxs-lookup"><span data-stu-id="be616-106">5.0 Preview 1</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="be616-107">舊的行為</span><span class="sxs-lookup"><span data-stu-id="be616-107">Old behavior</span></span>

<span data-ttu-id="be616-108">在 `ResourceManagerWithCultureStringLocalizer` `ResourceManagerStringLocalizer.WithCulture` [.Net Core 3.0 Preview 3 和更新版本中](/dotnet/core/compatibility/2.2-3.0#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete)，類別和方法已過時。</span><span class="sxs-lookup"><span data-stu-id="be616-108">The `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method are [obsolete in .NET Core 3.0 Preview 3 and later](/dotnet/core/compatibility/2.2-3.0#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete).</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="be616-109">新的行為</span><span class="sxs-lookup"><span data-stu-id="be616-109">New behavior</span></span>

<span data-ttu-id="be616-110">已 `ResourceManagerWithCultureStringLocalizer` `ResourceManagerStringLocalizer.WithCulture` 移除 .Net 5.0 Preview 1 中的類別和方法。</span><span class="sxs-lookup"><span data-stu-id="be616-110">The `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method have been removed in .NET 5.0 Preview 1.</span></span> <span data-ttu-id="be616-111">如需進行變更的清查，請參閱[dotnet/extensions # 2562](https://github.com/dotnet/extensions/pull/2562/files)的提取要求。</span><span class="sxs-lookup"><span data-stu-id="be616-111">For an inventory of the changes made, see the pull request at [dotnet/extensions#2562](https://github.com/dotnet/extensions/pull/2562/files).</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="be616-112">變更的原因</span><span class="sxs-lookup"><span data-stu-id="be616-112">Reason for change</span></span>

<span data-ttu-id="be616-113">[ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1)類別和[ResourceManagerStringLocalizer. WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1)方法通常是當地語系化使用者的混淆來源。</span><span class="sxs-lookup"><span data-stu-id="be616-113">The [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) class and [ResourceManagerStringLocalizer.WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) method were often sources of confusion for users of localization.</span></span> <span data-ttu-id="be616-114">建立自訂的執行時，混淆特別高 <xref:Microsoft.Extensions.Localization.IStringLocalizer> 。</span><span class="sxs-lookup"><span data-stu-id="be616-114">The confusion was especially high when creating a custom <xref:Microsoft.Extensions.Localization.IStringLocalizer> implementation.</span></span> <span data-ttu-id="be616-115">此類別和方法可讓取用者認為 `IStringLocalizer` 實例預期會是「每一語言，每個資源」的印象。</span><span class="sxs-lookup"><span data-stu-id="be616-115">This class and method give consumers the impression that an `IStringLocalizer` instance is expected to be "per-language, per-resource".</span></span> <span data-ttu-id="be616-116">實際上，實例應該只是「每個資源」。</span><span class="sxs-lookup"><span data-stu-id="be616-116">In reality, the instance should only be "per-resource".</span></span> <span data-ttu-id="be616-117">在執行時間， <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> 屬性會決定要使用的語言。</span><span class="sxs-lookup"><span data-stu-id="be616-117">At run time, the <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> property determines the language to be used.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="be616-118">建議的動作</span><span class="sxs-lookup"><span data-stu-id="be616-118">Recommended action</span></span>

<span data-ttu-id="be616-119">停止使用 `ResourceManagerWithCultureStringLocalizer` 類別和 `ResourceManagerStringLocalizer.WithCulture` 方法。</span><span class="sxs-lookup"><span data-stu-id="be616-119">Stop using the `ResourceManagerWithCultureStringLocalizer` class and the `ResourceManagerStringLocalizer.WithCulture` method.</span></span>

#### <a name="category"></a><span data-ttu-id="be616-120">類別</span><span class="sxs-lookup"><span data-stu-id="be616-120">Category</span></span>

<span data-ttu-id="be616-121">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="be616-121">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="be616-122">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="be616-122">Affected APIs</span></span>

- [<span data-ttu-id="be616-123">ResourceManagerWithCultureStringLocalizer</span><span class="sxs-lookup"><span data-stu-id="be616-123">ResourceManagerWithCultureStringLocalizer</span></span>](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1)
- [<span data-ttu-id="be616-124">ResourceManagerStringLocalizer.WithCulture</span><span class="sxs-lookup"><span data-stu-id="be616-124">ResourceManagerStringLocalizer.WithCulture</span></span>](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1)

<!--

#### Affected APIs

- `T:Microsoft.Extensions.Localization.ResourceManagerWithCultureStringLocalizer`
- `Overload:Microsoft.Extensions.Localization.ResourceManagerStringLocalizer.WithCulture`

-->
