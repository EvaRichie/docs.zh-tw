---
title: 使用 .NET Core CLI 開發程式庫
description: 瞭解如何使用 .NET Core CLI 建立 .NET Core 程式庫。 您將建立支援多個架構的程式庫。
author: cartermp
ms.topic: how-to
ms.date: 05/01/2017
ms.openlocfilehash: 7aadaf7bf7819d52a57c3a137beff46d924d8cb0
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396206"
---
# <a name="develop-libraries-with-the-net-core-cli"></a><span data-ttu-id="cf205-104">使用 .NET Core CLI 開發程式庫</span><span class="sxs-lookup"><span data-stu-id="cf205-104">Develop libraries with the .NET Core CLI</span></span>

<span data-ttu-id="cf205-105">本文說明如何使用 .NET Core CLI 撰寫適用于 .NET 的程式庫。</span><span class="sxs-lookup"><span data-stu-id="cf205-105">This article covers how to write libraries for .NET using the .NET Core CLI.</span></span> <span data-ttu-id="cf205-106">CLI 提供可在所有支援的作業系統上運作的有效率且低階體驗。</span><span class="sxs-lookup"><span data-stu-id="cf205-106">The CLI provides an efficient and low-level experience that works across any supported OS.</span></span> <span data-ttu-id="cf205-107">您仍然可以使用 Visual Studio 來建置程式庫，而且，如果那是您偏好的體驗，[請參閱 Visual Studio 指南](library-with-visual-studio.md)。</span><span class="sxs-lookup"><span data-stu-id="cf205-107">You can still build libraries with Visual Studio, and if that is your preferred experience [refer to the Visual Studio guide](library-with-visual-studio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf205-108">先決條件</span><span class="sxs-lookup"><span data-stu-id="cf205-108">Prerequisites</span></span>

<span data-ttu-id="cf205-109">您需要在電腦上安裝 [.NET Core SDK 和 CLI](https://dotnet.microsoft.com/download)。</span><span class="sxs-lookup"><span data-stu-id="cf205-109">You need [the .NET Core SDK and CLI](https://dotnet.microsoft.com/download) installed on your machine.</span></span>

<span data-ttu-id="cf205-110">針對這份文件中處理 .NET Framework 版本的一節，您需要在 Windows 電腦上安裝 [.NET Framework](https://dotnet.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="cf205-110">For the sections of this document dealing with .NET Framework versions, you need the [.NET Framework](https://dotnet.microsoft.com) installed on a Windows machine.</span></span>

<span data-ttu-id="cf205-111">此外，如果您想要支援較舊的 .NET Framework 目標，則需要從[.net 下載封存頁面](https://dotnet.microsoft.com/download/archives)安裝目標套件或開發人員套件。</span><span class="sxs-lookup"><span data-stu-id="cf205-111">Additionally, if you wish to support older .NET Framework targets, you need to install targeting packs or developer packs from the [.NET download archives page](https://dotnet.microsoft.com/download/archives).</span></span> <span data-ttu-id="cf205-112">請參閱這張表格︰</span><span class="sxs-lookup"><span data-stu-id="cf205-112">Refer to this table:</span></span>

| <span data-ttu-id="cf205-113">.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="cf205-113">.NET Framework version</span></span> | <span data-ttu-id="cf205-114">要下載的項目</span><span class="sxs-lookup"><span data-stu-id="cf205-114">What to download</span></span>                                       |
| ---------------------- | ------------------------------------------------------ |
| <span data-ttu-id="cf205-115">4.6.1</span><span class="sxs-lookup"><span data-stu-id="cf205-115">4.6.1</span></span>                  | <span data-ttu-id="cf205-116">.NET Framework 4.6.1 目標套件</span><span class="sxs-lookup"><span data-stu-id="cf205-116">.NET Framework 4.6.1 Targeting Pack</span></span>                    |
| <span data-ttu-id="cf205-117">4.6</span><span class="sxs-lookup"><span data-stu-id="cf205-117">4.6</span></span>                    | <span data-ttu-id="cf205-118">.NET Framework 4.6 目標套件</span><span class="sxs-lookup"><span data-stu-id="cf205-118">.NET Framework 4.6 Targeting Pack</span></span>                      |
| <span data-ttu-id="cf205-119">4.5.2</span><span class="sxs-lookup"><span data-stu-id="cf205-119">4.5.2</span></span>                  | <span data-ttu-id="cf205-120">.NET Framework 4.5.2 開發人員套件</span><span class="sxs-lookup"><span data-stu-id="cf205-120">.NET Framework 4.5.2 Developer Pack</span></span>                    |
| <span data-ttu-id="cf205-121">4.5.1</span><span class="sxs-lookup"><span data-stu-id="cf205-121">4.5.1</span></span>                  | <span data-ttu-id="cf205-122">.NET Framework 4.5.1 開發人員套件</span><span class="sxs-lookup"><span data-stu-id="cf205-122">.NET Framework 4.5.1 Developer Pack</span></span>                    |
| <span data-ttu-id="cf205-123">4.5</span><span class="sxs-lookup"><span data-stu-id="cf205-123">4.5</span></span>                    | <span data-ttu-id="cf205-124">適用於 Windows 8 的 Windows 軟體開發套件</span><span class="sxs-lookup"><span data-stu-id="cf205-124">Windows Software Development Kit for Windows 8</span></span>         |
| <span data-ttu-id="cf205-125">4.0</span><span class="sxs-lookup"><span data-stu-id="cf205-125">4.0</span></span>                    | <span data-ttu-id="cf205-126">適用於 Windows 7 的 Windows SDK 及 .NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="cf205-126">Windows SDK for Windows 7 and .NET Framework 4</span></span>         |
| <span data-ttu-id="cf205-127">2.0、3.0 和 3.5</span><span class="sxs-lookup"><span data-stu-id="cf205-127">2.0, 3.0, and 3.5</span></span>      | <span data-ttu-id="cf205-128">.NET Framework 3.5 SP1 執行階段 (或 Windows 8+ 版本)</span><span class="sxs-lookup"><span data-stu-id="cf205-128">.NET Framework 3.5 SP1 Runtime (or Windows 8+ version)</span></span> |

## <a name="how-to-target-the-net-standard"></a><span data-ttu-id="cf205-129">如何將目標設為 .NET Standard</span><span class="sxs-lookup"><span data-stu-id="cf205-129">How to target the .NET Standard</span></span>

<span data-ttu-id="cf205-130">如果您不熟悉 .NET Standard，請參閱[.NET Standard](../../standard/net-standard.md)以深入瞭解。</span><span class="sxs-lookup"><span data-stu-id="cf205-130">If you're not familiar with .NET Standard, refer to [.NET Standard](../../standard/net-standard.md) to learn more.</span></span>

<span data-ttu-id="cf205-131">在該文章中，有一個表格會將 .NET Standard 版本對應至各種不同的執行方式：</span><span class="sxs-lookup"><span data-stu-id="cf205-131">In that article, there is a table that maps .NET Standard versions to various implementations:</span></span>

[!INCLUDE [net-standard-table](../../../includes/net-standard-table.md)]

<span data-ttu-id="cf205-132">以下是這個資料表在建立程式庫時的意義︰</span><span class="sxs-lookup"><span data-stu-id="cf205-132">Here's what this table means for the purposes of creating a library:</span></span>

<span data-ttu-id="cf205-133">您挑選的 .NET Standard 版本將會在存取最新的 Api 與將更多 .NET 部署和 .NET Standard 版本的能力之間進行取捨。</span><span class="sxs-lookup"><span data-stu-id="cf205-133">The version of .NET Standard you pick will be a tradeoff between access to the newest APIs and the ability to target more .NET implementations and .NET Standard versions.</span></span> <span data-ttu-id="cf205-134">您可以藉由挑選版本的 `netstandardX.X` （其中 `X.X` 是版本號碼），並將它新增至您的專案檔（ `.csproj` 或），來控制目標設為平臺和版本的範圍 `.fsproj` 。</span><span class="sxs-lookup"><span data-stu-id="cf205-134">You control the range of targetable platforms and versions by picking a version of `netstandardX.X` (where `X.X` is a version number) and adding it to your project file (`.csproj` or `.fsproj`).</span></span>

<span data-ttu-id="cf205-135">根據您的需求，您有三個主要選項會以 .NET Standard 為目標。</span><span class="sxs-lookup"><span data-stu-id="cf205-135">You have three primary options when targeting .NET Standard, depending on your needs.</span></span>

1. <span data-ttu-id="cf205-136">您可以使用範本所提供的預設 .NET Standard 版本， `netstandard1.4` 這可讓您存取 .NET Standard 上大部分的 api，同時仍然與 UWP、.NET Framework 4.6.1 和 .NET Standard 2.0 相容。</span><span class="sxs-lookup"><span data-stu-id="cf205-136">You can use the default version of .NET Standard supplied by templates, `netstandard1.4`, which gives you access to most APIs on .NET Standard while still being compatible with UWP, .NET Framework 4.6.1, and .NET Standard 2.0.</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <TargetFramework>netstandard1.4</TargetFramework>
      </PropertyGroup>
    </Project>
    ```

2. <span data-ttu-id="cf205-137">您可以在專案檔的節點中修改值，以使用較低或較高版本的 .NET Standard `TargetFramework` 。</span><span class="sxs-lookup"><span data-stu-id="cf205-137">You can use a lower or higher version of .NET Standard by modifying the value in the `TargetFramework` node of your project file.</span></span>

    <span data-ttu-id="cf205-138">.NET Standard 版本具備回溯相容。</span><span class="sxs-lookup"><span data-stu-id="cf205-138">.NET Standard versions are backward compatible.</span></span> <span data-ttu-id="cf205-139">這表示 `netstandard1.0` 程式庫是在 `netstandard1.1` 平台和更高版本上執行。</span><span class="sxs-lookup"><span data-stu-id="cf205-139">That means that `netstandard1.0` libraries run on `netstandard1.1` platforms and higher.</span></span> <span data-ttu-id="cf205-140">不過，沒有向前相容性。</span><span class="sxs-lookup"><span data-stu-id="cf205-140">However, there is no forward compatibility.</span></span> <span data-ttu-id="cf205-141">較低的 .NET Standard 平臺無法參考更高版本。</span><span class="sxs-lookup"><span data-stu-id="cf205-141">Lower .NET Standard platforms cannot reference higher ones.</span></span> <span data-ttu-id="cf205-142">這表示 `netstandard1.0` 程式庫無法參考目標設為 `netstandard1.1` 或更高版本的程式庫。</span><span class="sxs-lookup"><span data-stu-id="cf205-142">This means that `netstandard1.0` libraries cannot reference libraries targeting `netstandard1.1` or higher.</span></span> <span data-ttu-id="cf205-143">針對您的需求，選取正確混合使用 API 與平台支援的標準版本。</span><span class="sxs-lookup"><span data-stu-id="cf205-143">Select the Standard version that has the right mix of APIs and platform support for your needs.</span></span> <span data-ttu-id="cf205-144">現在建議使用 `netstandard1.4`。</span><span class="sxs-lookup"><span data-stu-id="cf205-144">We recommend `netstandard1.4` for now.</span></span>

3. <span data-ttu-id="cf205-145">如果您想要以 .NET Framework 版本4.0 或以下為目標，或您想要使用 .NET Framework 中提供的 API，但不是在 .NET Standard 中（例如 `System.Drawing` ），請閱讀下列各節，並瞭解如何使用多目標。</span><span class="sxs-lookup"><span data-stu-id="cf205-145">If you want to target .NET Framework versions 4.0 or below, or you wish to use an API available in .NET Framework but not in .NET Standard (for example, `System.Drawing`), read the following sections and learn how to multitarget.</span></span>

## <a name="how-to-target-net-framework"></a><span data-ttu-id="cf205-146">如何以 .NET Framework 為目標</span><span class="sxs-lookup"><span data-stu-id="cf205-146">How to target .NET Framework</span></span>

> [!NOTE]
> <span data-ttu-id="cf205-147">這些指示假設您已在電腦上安裝 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="cf205-147">These instructions assume you have .NET Framework installed on your machine.</span></span> <span data-ttu-id="cf205-148">請參閱安裝相依性的[必要條件](#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="cf205-148">Refer to the [Prerequisites](#prerequisites) to get dependencies installed.</span></span>

<span data-ttu-id="cf205-149">請記住，已不再支援此處使用的部分 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="cf205-149">Keep in mind that some of the .NET Framework versions used here are no longer supported.</span></span> <span data-ttu-id="cf205-150">如需不支援的版本，請參閱 [.NET Framework Support Lifecycle Policy FAQ](https://support.microsoft.com/gp/framework_faq/en-us) (.NET Framework 支援週期原則 FAQ)。</span><span class="sxs-lookup"><span data-stu-id="cf205-150">Refer to the [.NET Framework Support Lifecycle Policy FAQ](https://support.microsoft.com/gp/framework_faq/en-us) about unsupported versions.</span></span>

<span data-ttu-id="cf205-151">如果您想要達到開發人員和專案的數目上限，請使用 .NET Framework 4.0 作為基準目標。</span><span class="sxs-lookup"><span data-stu-id="cf205-151">If you want to reach the maximum number of developers and projects, use .NET Framework 4.0 as your baseline target.</span></span> <span data-ttu-id="cf205-152">若要以 .NET Framework 為目標，請先使用對應至您想要支援之 .NET Framework 版本的正確目標 Framework 標記（TFM）。</span><span class="sxs-lookup"><span data-stu-id="cf205-152">To target .NET Framework, begin by using the correct Target Framework Moniker (TFM) that corresponds to the .NET Framework version you wish to support.</span></span>

| <span data-ttu-id="cf205-153">.NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="cf205-153">.NET Framework version</span></span> | <span data-ttu-id="cf205-154">TFM</span><span class="sxs-lookup"><span data-stu-id="cf205-154">TFM</span></span>      |
| ---------------------- | -------- |
| <span data-ttu-id="cf205-155">.NET Framework 2.0</span><span class="sxs-lookup"><span data-stu-id="cf205-155">.NET Framework 2.0</span></span>     | `net20`  |
| <span data-ttu-id="cf205-156">.NET Framework 3.0</span><span class="sxs-lookup"><span data-stu-id="cf205-156">.NET Framework 3.0</span></span>     | `net30`  |
| <span data-ttu-id="cf205-157">.NET Framework 3.5</span><span class="sxs-lookup"><span data-stu-id="cf205-157">.NET Framework 3.5</span></span>     | `net35`  |
| <span data-ttu-id="cf205-158">.NET Framework 4.0</span><span class="sxs-lookup"><span data-stu-id="cf205-158">.NET Framework 4.0</span></span>     | `net40`  |
| <span data-ttu-id="cf205-159">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="cf205-159">.NET Framework 4.5</span></span>     | `net45`  |
| <span data-ttu-id="cf205-160">.NET Framework 4.5.1</span><span class="sxs-lookup"><span data-stu-id="cf205-160">.NET Framework 4.5.1</span></span>   | `net451` |
| <span data-ttu-id="cf205-161">.NET Framework 4.5.2</span><span class="sxs-lookup"><span data-stu-id="cf205-161">.NET Framework 4.5.2</span></span>   | `net452` |
| <span data-ttu-id="cf205-162">.NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="cf205-162">.NET Framework 4.6</span></span>     | `net46`  |
| <span data-ttu-id="cf205-163">.NET Framework 4.6.1</span><span class="sxs-lookup"><span data-stu-id="cf205-163">.NET Framework 4.6.1</span></span>   | `net461` |
| <span data-ttu-id="cf205-164">.NET Framework 4.6.2</span><span class="sxs-lookup"><span data-stu-id="cf205-164">.NET Framework 4.6.2</span></span>   | `net462` |
| <span data-ttu-id="cf205-165">.NET Framework 4.7</span><span class="sxs-lookup"><span data-stu-id="cf205-165">.NET Framework 4.7</span></span>     | `net47`  |
| <span data-ttu-id="cf205-166">.NET Framework 4.8</span><span class="sxs-lookup"><span data-stu-id="cf205-166">.NET Framework 4.8</span></span>     | `net48`  |

<span data-ttu-id="cf205-167">您接著將這個 TFM 插入專案檔的 `TargetFramework` 區段。</span><span class="sxs-lookup"><span data-stu-id="cf205-167">You then insert this TFM into the `TargetFramework` section of your project file.</span></span> <span data-ttu-id="cf205-168">例如，以下說明如何撰寫以 .NET Framework 4.0 為目標的程式庫：</span><span class="sxs-lookup"><span data-stu-id="cf205-168">For example, here's how you would write a library that targets .NET Framework 4.0:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>net40</TargetFramework>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="cf205-169">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="cf205-169">And that's it!</span></span> <span data-ttu-id="cf205-170">雖然這只會針對 .NET Framework 4 進行編譯，但是您可以在較新版本的 .NET Framework 上使用程式庫。</span><span class="sxs-lookup"><span data-stu-id="cf205-170">Although this compiled only for .NET Framework 4, you can use the library on newer versions of .NET Framework.</span></span>

## <a name="how-to-multitarget"></a><span data-ttu-id="cf205-171">如何使用多目標</span><span class="sxs-lookup"><span data-stu-id="cf205-171">How to multitarget</span></span>

> [!NOTE]
> <span data-ttu-id="cf205-172">下列指示假設您已在電腦上安裝 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="cf205-172">The following instructions assume you have the .NET Framework installed on your machine.</span></span> <span data-ttu-id="cf205-173">請參閱[必要條件](#prerequisites)小節，了解您需要安裝的相依性以及其下載位置。</span><span class="sxs-lookup"><span data-stu-id="cf205-173">Refer to the [Prerequisites](#prerequisites) section to learn which dependencies you need to install and where to download them from.</span></span>

<span data-ttu-id="cf205-174">當您的專案同時支援 .NET Framework 和 .NET Core 時，可能需要將目標設為舊版 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="cf205-174">You may need to target older versions of the .NET Framework when your project supports both the .NET Framework and .NET Core.</span></span> <span data-ttu-id="cf205-175">在這個案例中，如果您想要為較新的目標使用較新的 API 和語言建構，請在程式碼中使用 `#if` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="cf205-175">In this scenario, if you want to use newer APIs and language constructs for the newer targets, use `#if` directives in your code.</span></span> <span data-ttu-id="cf205-176">您也可能需要針對設為目標的每個平台新增不同的套件和相依性，以包含每個案例所需的不同 API。</span><span class="sxs-lookup"><span data-stu-id="cf205-176">You also might need to add different packages and dependencies for each platform you're targeting to include the different APIs needed for each case.</span></span>

<span data-ttu-id="cf205-177">例如，假設您的程式庫透過 HTTP 執行網路作業。</span><span class="sxs-lookup"><span data-stu-id="cf205-177">For example, let's say you have a library that performs networking operations over HTTP.</span></span> <span data-ttu-id="cf205-178">針對 .NET Standard 和 .NET Framework 4.5 版或更高版本，您可以使用 `System.Net.Http` 命名空間中的 `HttpClient` 類別。</span><span class="sxs-lookup"><span data-stu-id="cf205-178">For .NET Standard and the .NET Framework versions 4.5 or higher, you can use the `HttpClient` class from the `System.Net.Http` namespace.</span></span> <span data-ttu-id="cf205-179">不過，舊版 .NET Framework 沒有 `HttpClient` 類別，因此您可以改用這些項目之 `System.Net` 命名空間中的 `WebClient` 類別。</span><span class="sxs-lookup"><span data-stu-id="cf205-179">However, earlier versions of the .NET Framework don't have the `HttpClient` class, so you could use the `WebClient` class from the `System.Net` namespace for those instead.</span></span>

<span data-ttu-id="cf205-180">專案檔如下所示：</span><span class="sxs-lookup"><span data-stu-id="cf205-180">Your project file could look like this:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFrameworks>netstandard1.4;net40;net45</TargetFrameworks>
  </PropertyGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.0 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net40'">
    <Reference Include="System.Net" />
  </ItemGroup>

  <!-- Need to conditionally bring in references for the .NET Framework 4.5 target -->
  <ItemGroup Condition="'$(TargetFramework)' == 'net45'">
    <Reference Include="System.Net.Http" />
    <Reference Include="System.Threading.Tasks" />
  </ItemGroup>
</Project>
```

<span data-ttu-id="cf205-181">您可在這裡發現三個主要變更︰</span><span class="sxs-lookup"><span data-stu-id="cf205-181">You'll notice three major changes here:</span></span>

1. <span data-ttu-id="cf205-182">`TargetFramework` 節點已取代為 `TargetFrameworks`，而且其內表示三個 TFM。</span><span class="sxs-lookup"><span data-stu-id="cf205-182">The `TargetFramework` node has been replaced by `TargetFrameworks`, and three TFMs are expressed inside.</span></span>
1. <span data-ttu-id="cf205-183">提取至一個 .NET Framework 參考的 `net40` 目標有一個 `<ItemGroup>` 節點。</span><span class="sxs-lookup"><span data-stu-id="cf205-183">There is an `<ItemGroup>` node for the `net40` target pulling in one .NET Framework reference.</span></span>
1. <span data-ttu-id="cf205-184">提取至兩個 .NET Framework 參考的 `net45` 目標有一個 `<ItemGroup>` 節點。</span><span class="sxs-lookup"><span data-stu-id="cf205-184">There is an `<ItemGroup>` node for the `net45` target pulling in two .NET Framework references.</span></span>

<span data-ttu-id="cf205-185">建置系統會得知 `#if` 指示詞中所使用的下列前置處理器符號︰</span><span class="sxs-lookup"><span data-stu-id="cf205-185">The build system is aware of the following preprocessor symbols used in `#if` directives:</span></span>

[!INCLUDE [Preprocessor symbols](../../../includes/preprocessor-symbols.md)]

<span data-ttu-id="cf205-186">以下是利用個別目標之條件式編譯的範例︰</span><span class="sxs-lookup"><span data-stu-id="cf205-186">Here is an example making use of conditional compilation per-target:</span></span>

```csharp
using System;
using System.Text.RegularExpressions;
#if NET40
// This only compiles for the .NET Framework 4 targets
using System.Net;
#else
 // This compiles for all other targets
using System.Net.Http;
using System.Threading.Tasks;
#endif

namespace MultitargetLib
{
    public class Library
    {
#if NET40
        private readonly WebClient _client = new WebClient();
        private readonly object _locker = new object();
#else
        private readonly HttpClient _client = new HttpClient();
#endif

#if NET40
        // .NET Framework 4.0 does not have async/await
        public string GetDotNetCount()
        {
            string url = "https://www.dotnetfoundation.org/";

            var uri = new Uri(url);

            string result = "";

            // Lock here to provide thread-safety.
            lock(_locker)
            {
                result = _client.DownloadString(uri);
            }

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"Dotnet Foundation mentions .NET {dotNetCount} times!";
        }
#else
        // .NET 4.5+ can use async/await!
        public async Task<string> GetDotNetCountAsync()
        {
            string url = "https://www.dotnetfoundation.org/";

            // HttpClient is thread-safe, so no need to explicitly lock here
            var result = await _client.GetStringAsync(url);

            int dotNetCount = Regex.Matches(result, ".NET").Count;

            return $"dotnetfoundation.org mentions .NET {dotNetCount} times in its HTML!";
        }
#endif
    }
}
```

<span data-ttu-id="cf205-187">如果您使用 `dotnet build` 建置此專案，則會在 `bin/` 資料夾下方發現三個目錄：</span><span class="sxs-lookup"><span data-stu-id="cf205-187">If you build this project with `dotnet build`, you'll notice three directories under the `bin/` folder:</span></span>

```
net40/
net45/
netstandard1.4/
```

<span data-ttu-id="cf205-188">所有這些都包含每個目標的 `.dll` 檔案。</span><span class="sxs-lookup"><span data-stu-id="cf205-188">Each of these contain the `.dll` files for each target.</span></span>

## <a name="how-to-test-libraries-on-net-core"></a><span data-ttu-id="cf205-189">如何測試 .NET Core 上的程式庫</span><span class="sxs-lookup"><span data-stu-id="cf205-189">How to test libraries on .NET Core</span></span>

<span data-ttu-id="cf205-190">重要的是一定要可以跨平台進行測試。</span><span class="sxs-lookup"><span data-stu-id="cf205-190">It's important to be able to test across platforms.</span></span> <span data-ttu-id="cf205-191">您可以使用現成的 [xUnit](https://xunit.github.io/) 或 MSTest。</span><span class="sxs-lookup"><span data-stu-id="cf205-191">You can use either [xUnit](https://xunit.github.io/) or MSTest out of the box.</span></span> <span data-ttu-id="cf205-192">兩者都完全適用於在 .NET Core 上對程式庫進行單元測試。</span><span class="sxs-lookup"><span data-stu-id="cf205-192">Both are perfectly suitable for unit testing your library on .NET Core.</span></span> <span data-ttu-id="cf205-193">如何設定具有測試專案的方案，將取決於[方案結構](#structuring-a-solution)。</span><span class="sxs-lookup"><span data-stu-id="cf205-193">How you set up your solution with test projects will depend on the [structure of your solution](#structuring-a-solution).</span></span> <span data-ttu-id="cf205-194">下列範例假設測試及來源目錄位於相同的最上層目錄中。</span><span class="sxs-lookup"><span data-stu-id="cf205-194">The following example assumes that the test and source directories live in the same top-level directory.</span></span>

> [!NOTE]
> <span data-ttu-id="cf205-195">這會使用一些[.NET Core CLI](../tools/index.md)命令。</span><span class="sxs-lookup"><span data-stu-id="cf205-195">This uses some [.NET Core CLI](../tools/index.md) commands.</span></span> <span data-ttu-id="cf205-196">如需詳細資訊，請參閱 [dotnet new](../tools/dotnet-new.md) 及 [dotnet sln](../tools/dotnet-sln.md)。</span><span class="sxs-lookup"><span data-stu-id="cf205-196">See [dotnet new](../tools/dotnet-new.md) and [dotnet sln](../tools/dotnet-sln.md) for more information.</span></span>

1. <span data-ttu-id="cf205-197">設定方案。</span><span class="sxs-lookup"><span data-stu-id="cf205-197">Set up your solution.</span></span> <span data-ttu-id="cf205-198">您可以使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="cf205-198">You can do so with the following commands:</span></span>

   ```dotnetcli
   mkdir SolutionWithSrcAndTest
   cd SolutionWithSrcAndTest
   dotnet new sln
   dotnet new classlib -o MyProject
   dotnet new xunit -o MyProject.Test
   dotnet sln add MyProject/MyProject.csproj
   dotnet sln add MyProject.Test/MyProject.Test.csproj
   ```

   <span data-ttu-id="cf205-199">這會建立專案，並將它們同時連結在方案中。</span><span class="sxs-lookup"><span data-stu-id="cf205-199">This will create projects and link them together in a solution.</span></span> <span data-ttu-id="cf205-200">您的 `SolutionWithSrcAndTest` 目錄應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="cf205-200">Your directory for `SolutionWithSrcAndTest` should look like this:</span></span>

   ```
   /SolutionWithSrcAndTest
   |__SolutionWithSrcAndTest.sln
   |__MyProject/
   |__MyProject.Test/
   ```

1. <span data-ttu-id="cf205-201">巡覽至測試專案的目錄，並將參考從 `MyProject` 新增至 `MyProject.Test`。</span><span class="sxs-lookup"><span data-stu-id="cf205-201">Navigate to the test project's directory and add a reference to `MyProject.Test` from `MyProject`.</span></span>

   ```dotnetcli
   cd MyProject.Test
   dotnet add reference ../MyProject/MyProject.csproj
   ```

1. <span data-ttu-id="cf205-202">還原套件並建置專案︰</span><span class="sxs-lookup"><span data-stu-id="cf205-202">Restore packages and build projects:</span></span>

   ```dotnetcli
   dotnet restore
   dotnet build
   ```

   [!INCLUDE[DotNet Restore Note](../../../includes/dotnet-restore-note.md)]

1. <span data-ttu-id="cf205-203">執行 `dotnet test` 命令，確認已執行 xUnit。</span><span class="sxs-lookup"><span data-stu-id="cf205-203">Verify that xUnit runs by executing the `dotnet test` command.</span></span> <span data-ttu-id="cf205-204">如果您選擇使用 MSTest，則應該會改為執行 MSTest 主控台執行器。</span><span class="sxs-lookup"><span data-stu-id="cf205-204">If you chose to use MSTest, then the MSTest console runner should run instead.</span></span>

<span data-ttu-id="cf205-205">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="cf205-205">And that's it!</span></span> <span data-ttu-id="cf205-206">您現在可以使用命令列工具，在所有平臺上測試您的程式庫。</span><span class="sxs-lookup"><span data-stu-id="cf205-206">You can now test your library across all platforms using command-line tools.</span></span> <span data-ttu-id="cf205-207">若要在設定好所有項目之後立即繼續測試，測試程式庫就會非常簡單︰</span><span class="sxs-lookup"><span data-stu-id="cf205-207">To continue testing now that you have everything set up, testing your library is very simple:</span></span>

1. <span data-ttu-id="cf205-208">對程式庫進行變更。</span><span class="sxs-lookup"><span data-stu-id="cf205-208">Make changes to your library.</span></span>
1. <span data-ttu-id="cf205-209">在測試目錄中，從命令列中使用 `dotnet test` 命令來執行測試。</span><span class="sxs-lookup"><span data-stu-id="cf205-209">Run tests from the command line, in your test directory, with `dotnet test` command.</span></span>

<span data-ttu-id="cf205-210">當您叫用 `dotnet test` 命令時，將會自動重建程式碼。</span><span class="sxs-lookup"><span data-stu-id="cf205-210">Your code will be automatically rebuilt when you invoke `dotnet test` command.</span></span>

## <a name="how-to-use-multiple-projects"></a><span data-ttu-id="cf205-211">如何使用多個專案</span><span class="sxs-lookup"><span data-stu-id="cf205-211">How to use multiple projects</span></span>

<span data-ttu-id="cf205-212">較大程式庫的常見需求是將功能放在不同的專案中。</span><span class="sxs-lookup"><span data-stu-id="cf205-212">A common need for larger libraries is to place functionality in different projects.</span></span>

<span data-ttu-id="cf205-213">假設您想要建立可在慣用 c # 和 F # 中使用的程式庫。</span><span class="sxs-lookup"><span data-stu-id="cf205-213">Imagine you want to build a library that could be consumed in idiomatic C# and F#.</span></span> <span data-ttu-id="cf205-214">這表示您的程式庫取用者以 c # 或 F # 的自然方式取用它。</span><span class="sxs-lookup"><span data-stu-id="cf205-214">That would mean that consumers of your library consume it in ways that are natural to C# or F#.</span></span> <span data-ttu-id="cf205-215">例如，在 C# 中，您可能會如下使用程式庫︰</span><span class="sxs-lookup"><span data-stu-id="cf205-215">For example, in C# you might consume the library like this:</span></span>

```csharp
using AwesomeLibrary.CSharp;

public Task DoThings(Data data)
{
    var convertResult = await AwesomeLibrary.ConvertAsync(data);
    var result = AwesomeLibrary.Process(convertResult);
    // do something with result
}
```

<span data-ttu-id="cf205-216">在 F# 中，它可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="cf205-216">In F#, it might look like this:</span></span>

```fsharp
open AwesomeLibrary.FSharp

let doWork data = async {
    let! result = AwesomeLibrary.AsyncConvert data // Uses an F# async function rather than C# async method
    // do something with result
}
```

<span data-ttu-id="cf205-217">這類使用案例表示針對 C# 和 F#，正在存取的 API 必須具有不同的結構。</span><span class="sxs-lookup"><span data-stu-id="cf205-217">Consumption scenarios like this mean that the APIs being accessed have to have a different structure for C# and F#.</span></span>  <span data-ttu-id="cf205-218">完成這項作業的常見方法將程式庫的所有邏輯都納入核心專案，而且 C# 和 F# 專案定義呼叫該核心專案的 API 層。</span><span class="sxs-lookup"><span data-stu-id="cf205-218">A common approach to accomplishing this is to factor all of the logic of a library into a core project, with C# and F# projects defining the API layers that call into that core project.</span></span>  <span data-ttu-id="cf205-219">區段的其餘部分將使用下列名稱︰</span><span class="sxs-lookup"><span data-stu-id="cf205-219">The rest of the section will use the following names:</span></span>

* <span data-ttu-id="cf205-220">**Awesomelibrary.fsharp** -包含程式庫所有邏輯的核心專案</span><span class="sxs-lookup"><span data-stu-id="cf205-220">**AwesomeLibrary.Core** - A core project that contains all logic for the library</span></span>
* <span data-ttu-id="cf205-221">**Awesomelibrary.fsharp. CSharp** -具有公用 api 的專案，適用于 C 中的耗用量#</span><span class="sxs-lookup"><span data-stu-id="cf205-221">**AwesomeLibrary.CSharp** - A project with public APIs intended for consumption in C#</span></span>
* <span data-ttu-id="cf205-222">**Awesomelibrary.fsharp. fsharp.core** -具有公用 api 的專案，適用于 F 中的耗用量#</span><span class="sxs-lookup"><span data-stu-id="cf205-222">**AwesomeLibrary.FSharp** - A project with public APIs intended for consumption in F#</span></span>

<span data-ttu-id="cf205-223">您可以在終端機中執行下列命令，以產生與本指南相同的結構︰</span><span class="sxs-lookup"><span data-stu-id="cf205-223">You can run the following commands in your terminal to produce the same structure as this guide:</span></span>

```dotnetcli
mkdir AwesomeLibrary && cd AwesomeLibrary
dotnet new sln
mkdir AwesomeLibrary.Core && cd AwesomeLibrary.Core && dotnet new classlib
cd ..
mkdir AwesomeLibrary.CSharp && cd AwesomeLibrary.CSharp && dotnet new classlib
cd ..
mkdir AwesomeLibrary.FSharp && cd AwesomeLibrary.FSharp && dotnet new classlib -lang "F#"
cd ..
dotnet sln add AwesomeLibrary.Core/AwesomeLibrary.Core.csproj
dotnet sln add AwesomeLibrary.CSharp/AwesomeLibrary.CSharp.csproj
dotnet sln add AwesomeLibrary.FSharp/AwesomeLibrary.FSharp.fsproj
```

<span data-ttu-id="cf205-224">這會新增上述三個專案，以及將它們連結在一起的方案檔。</span><span class="sxs-lookup"><span data-stu-id="cf205-224">This will add the three projects above and a solution file that links them together.</span></span> <span data-ttu-id="cf205-225">建立方案檔和連結專案可讓您從最上層還原和建立專案。</span><span class="sxs-lookup"><span data-stu-id="cf205-225">Creating the solution file and linking projects will allow you to restore and build projects from a top level.</span></span>

### <a name="project-to-project-referencing"></a><span data-ttu-id="cf205-226">專案對專案參考</span><span class="sxs-lookup"><span data-stu-id="cf205-226">Project-to-project referencing</span></span>

<span data-ttu-id="cf205-227">參考專案的最佳方式是使用 .NET Core CLI 來新增專案參考。</span><span class="sxs-lookup"><span data-stu-id="cf205-227">The best way to reference a project is to use the .NET Core CLI to add a project reference.</span></span> <span data-ttu-id="cf205-228">從 **AwesomeLibrary.CSharp** 及 **AwesomeLibrary.FSharp** 專案目錄中，您可以執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="cf205-228">From the **AwesomeLibrary.CSharp** and **AwesomeLibrary.FSharp** project directories, you can run the following command:</span></span>

```dotnetcli
dotnet add reference ../AwesomeLibrary.Core/AwesomeLibrary.Core.csproj
```

<span data-ttu-id="cf205-229">**AwesomeLibrary.CSharp** 及 **AwesomeLibrary.FSharp** 的專案檔現在參考 **AwesomeLibrary.Core** 作為 `ProjectReference` 目標。</span><span class="sxs-lookup"><span data-stu-id="cf205-229">The project files for both **AwesomeLibrary.CSharp** and **AwesomeLibrary.FSharp** will now reference **AwesomeLibrary.Core** as a `ProjectReference` target.</span></span>  <span data-ttu-id="cf205-230">檢查專案檔並查看其中的下列內容，即可確認這項作業︰</span><span class="sxs-lookup"><span data-stu-id="cf205-230">You can verify this by inspecting the project files and seeing the following in them:</span></span>

```xml
<ItemGroup>
  <ProjectReference Include="..\AwesomeLibrary.Core\AwesomeLibrary.Core.csproj" />
</ItemGroup>
```

<span data-ttu-id="cf205-231">如果您不想要使用 .NET Core CLI，則可以手動將這個區段新增至每個專案檔。</span><span class="sxs-lookup"><span data-stu-id="cf205-231">You can add this section to each project file manually if you prefer not to use the .NET Core CLI.</span></span>

### <a name="structuring-a-solution"></a><span data-ttu-id="cf205-232">建構方案</span><span class="sxs-lookup"><span data-stu-id="cf205-232">Structuring a solution</span></span>

<span data-ttu-id="cf205-233">多專案方案的另一個重要部分是建立不錯的整體專案結構。</span><span class="sxs-lookup"><span data-stu-id="cf205-233">Another important aspect of multi-project solutions is establishing a good overall project structure.</span></span> <span data-ttu-id="cf205-234">不過，您可以視需要組織程式碼，而且只要您使用 `dotnet sln add` 將每個專案連結至方案檔，就可以在方案層級執行 `dotnet restore` 及 `dotnet build`。</span><span class="sxs-lookup"><span data-stu-id="cf205-234">You can organize code however you like, and as long as you link each project to your solution file with `dotnet sln add`, you will be able to run `dotnet restore` and `dotnet build` at the solution level.</span></span>
