---
title: 將 Windows Forms 應用程式移植到 .NET Core
description: 教您如何將 .NET Framework Windows Forms 應用程式移植到適用于 Windows 的 .NET Core。
author: Thraka
ms.author: adegeo
ms.date: 01/24/2020
ms.openlocfilehash: 71bd5740e1ea380fdde86328a5aed71fded64765
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89118542"
---
# <a name="how-to-port-a-windows-forms-desktop-app-to-net-core"></a><span data-ttu-id="280b5-103">如何將 Windows Forms desktop 應用程式移植到 .NET Core</span><span class="sxs-lookup"><span data-stu-id="280b5-103">How to port a Windows Forms desktop app to .NET Core</span></span>

<span data-ttu-id="280b5-104">本文說明如何將以 Windows Forms 為基礎的桌面應用程式從 .NET Framework 移植到 .NET Core 3.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="280b5-104">This article describes how to port your Windows Forms-based desktop app from .NET Framework to .NET Core 3.0 or later.</span></span> <span data-ttu-id="280b5-105">.NET Core 3.0 SDK 支源 Windows Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="280b5-105">The .NET Core 3.0 SDK includes support for Windows Forms applications.</span></span> <span data-ttu-id="280b5-106">Windows Forms 仍然是僅限 Windows 的架構，只能在 Windows 上執行。</span><span class="sxs-lookup"><span data-stu-id="280b5-106">Windows Forms is still a Windows-only framework and only runs on Windows.</span></span> <span data-ttu-id="280b5-107">本範例使用 .NET Core SDK CLI 來建立和管理您的專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-107">This example uses the .NET Core SDK CLI to create and manage your project.</span></span>

<span data-ttu-id="280b5-108">在此文章中，各種不同的名稱會用來識別用於移轉的檔案類型。</span><span class="sxs-lookup"><span data-stu-id="280b5-108">In this article, various names are used to identify types of files used for migration.</span></span> <span data-ttu-id="280b5-109">在移轉您的專案時，您的檔案會有不同的名稱，因此請在心裡將它們與下面所列的項目進行比對：</span><span class="sxs-lookup"><span data-stu-id="280b5-109">When migrating your project, your files will be named differently, so mentally match them to the ones listed below:</span></span>

| <span data-ttu-id="280b5-110">檔案</span><span class="sxs-lookup"><span data-stu-id="280b5-110">File</span></span> | <span data-ttu-id="280b5-111">描述</span><span class="sxs-lookup"><span data-stu-id="280b5-111">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="280b5-112">**MyApps.sln**</span><span class="sxs-lookup"><span data-stu-id="280b5-112">**MyApps.sln**</span></span> | <span data-ttu-id="280b5-113">方案檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="280b5-113">The name of the solution file.</span></span> |
| <span data-ttu-id="280b5-114">**MyForms.csproj**</span><span class="sxs-lookup"><span data-stu-id="280b5-114">**MyForms.csproj**</span></span> | <span data-ttu-id="280b5-115">要移植的 .NET Framework Windows Forms 專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="280b5-115">The name of the .NET Framework Windows Forms project to port.</span></span> |
| <span data-ttu-id="280b5-116">**MyFormsCore.csproj**</span><span class="sxs-lookup"><span data-stu-id="280b5-116">**MyFormsCore.csproj**</span></span> | <span data-ttu-id="280b5-117">您所建立的新 .NET Core 專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="280b5-117">The name of the new .NET Core project you create.</span></span> |
| <span data-ttu-id="280b5-118">**MyAppCore.exe**</span><span class="sxs-lookup"><span data-stu-id="280b5-118">**MyAppCore.exe**</span></span> | <span data-ttu-id="280b5-119">.NET Core Windows Forms 應用程式可執行檔。</span><span class="sxs-lookup"><span data-stu-id="280b5-119">The .NET Core Windows Forms app executable.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="280b5-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="280b5-120">Prerequisites</span></span>

- <span data-ttu-id="280b5-121">針對您想要執行的任何設計工具， [Visual Studio 2019 16.5 版或更新版本](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community&rel=16)。</span><span class="sxs-lookup"><span data-stu-id="280b5-121">[Visual Studio 2019 version 16.5 or later](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community&rel=16) for any designer work you want to do.</span></span> <span data-ttu-id="280b5-122">建議您更新至 [最新版本的 Visual Studio](https://visualstudio.microsoft.com/vs/)。</span><span class="sxs-lookup"><span data-stu-id="280b5-122">We recommend to update to the [latest version of Visual Studio](https://visualstudio.microsoft.com/vs/).</span></span>

  <span data-ttu-id="280b5-123">安裝下列 Visual Studio 工作負載：</span><span class="sxs-lookup"><span data-stu-id="280b5-123">Install the following Visual Studio workloads:</span></span>
  
  - <span data-ttu-id="280b5-124">.NET 桌面開發</span><span class="sxs-lookup"><span data-stu-id="280b5-124">.NET desktop development</span></span>
  - <span data-ttu-id="280b5-125">.NET Core 跨平台開發</span><span class="sxs-lookup"><span data-stu-id="280b5-125">.NET Core cross-platform development</span></span>

- <span data-ttu-id="280b5-126">在解決方案中運作的 Windows Forms 專案，可以毫無問題地建置並執行。</span><span class="sxs-lookup"><span data-stu-id="280b5-126">A working Windows Forms project in a solution that builds and runs without issue.</span></span>
- <span data-ttu-id="280b5-127">以 c # 編碼的專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-127">A project coded in C#.</span></span>

> [!NOTE]
> <span data-ttu-id="280b5-128">Visual Studio 2019 和更新版本支援 .NET Core Windows Forms 專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-128">.NET Core Windows Forms projects are supported in Visual Studio 2019 and later versions.</span></span> <span data-ttu-id="280b5-129">從 Visual Studio 2019 16.5 版開始支援 .NET Core Windows Forms 設計工具。</span><span class="sxs-lookup"><span data-stu-id="280b5-129">The .NET Core Windows Forms designer is supported starting in Visual Studio 2019 version 16.5.</span></span>
>
> <span data-ttu-id="280b5-130">若要啟用設計工具，請移至 [**工具**  >  **選項**  >  **環境**  >  **預覽功能**]，然後選取 [**使用適用于 .net Core 應用程式的預覽 Windows Forms 設計**工具] 選項。</span><span class="sxs-lookup"><span data-stu-id="280b5-130">To enable the designer, go to **Tools** > **Options** > **Environment** > **Preview Features** and select the **Use the preview Windows Forms designer for .NET Core apps** option.</span></span>

### <a name="consider"></a><span data-ttu-id="280b5-131">Consider</span><span class="sxs-lookup"><span data-stu-id="280b5-131">Consider</span></span>

<span data-ttu-id="280b5-132">移植 .NET Framework Windows Forms 應用程式時，您必須考量幾件事。</span><span class="sxs-lookup"><span data-stu-id="280b5-132">When porting a .NET Framework Windows Forms application, there are a few things you must consider.</span></span>

01. <span data-ttu-id="280b5-133">請檢查您的應用程式是否適合移轉。</span><span class="sxs-lookup"><span data-stu-id="280b5-133">Check that your application is a good candidate for migration.</span></span>

    <span data-ttu-id="280b5-134">使用 [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) 確定您的專案是否將移轉至 .NET Core 3.0。</span><span class="sxs-lookup"><span data-stu-id="280b5-134">Use the [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) to determine if your project will migrate to .NET Core 3.0.</span></span> <span data-ttu-id="280b5-135">如果您的專案有.NET Core 3.0 的問題，則分析器可協助您找出這些問題。</span><span class="sxs-lookup"><span data-stu-id="280b5-135">If your project has issues with .NET Core 3.0, the analyzer helps you identify those problems.</span></span>

01. <span data-ttu-id="280b5-136">您正在使用不同版本的 Windows Forms。</span><span class="sxs-lookup"><span data-stu-id="280b5-136">You're using a different version of Windows Forms.</span></span>

    <span data-ttu-id="280b5-137">當 .NET Core 3.0 Preview 1 發行時，Windows Forms 在 GitHub 上進入開放原始碼。</span><span class="sxs-lookup"><span data-stu-id="280b5-137">When .NET Core 3.0 Preview 1 was released, Windows Forms went open source on GitHub.</span></span> <span data-ttu-id="280b5-138">.NET Core Windows Forms 的程式碼是 .NET Framework Windows Forms 程式碼基底的分支。</span><span class="sxs-lookup"><span data-stu-id="280b5-138">The code for .NET Core Windows Forms is a fork of the .NET Framework Windows Forms codebase.</span></span> <span data-ttu-id="280b5-139">很可能存在一些差異，而您的應用程式將無法移植。</span><span class="sxs-lookup"><span data-stu-id="280b5-139">It's possible some differences exist and your app won't port.</span></span>

01. <span data-ttu-id="280b5-140">[Windows 相容性套件][compat-pack]可能可以協助您進行遷移。</span><span class="sxs-lookup"><span data-stu-id="280b5-140">The [Windows Compatibility Pack][compat-pack] may help you migrate.</span></span>

    <span data-ttu-id="280b5-141">.NET Core 3.0 中不提供 .NET Framework 中提供的某些 API。</span><span class="sxs-lookup"><span data-stu-id="280b5-141">Some APIs that are available in .NET Framework aren't available in .NET Core 3.0.</span></span> <span data-ttu-id="280b5-142">[Windows 相容性套件][compat-pack]新增許多這些 API，可能有助於您的 Windows Forms 應用程式與 .NET Core 相容。</span><span class="sxs-lookup"><span data-stu-id="280b5-142">The [Windows Compatibility Pack][compat-pack] adds many of these APIs and may help your Windows Forms app become compatible with .NET Core.</span></span>

01. <span data-ttu-id="280b5-143">更新專案所使用的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="280b5-143">Update the NuGet packages used by your project.</span></span>

    <span data-ttu-id="280b5-144">在任何移轉之前使用最新版本的 NuGet 套件永遠是最好的作法。</span><span class="sxs-lookup"><span data-stu-id="280b5-144">It's always a good practice to use the latest versions of NuGet packages before any migration.</span></span> <span data-ttu-id="280b5-145">如果您的應用程式會參考任何 NuGet 套件，請將它們更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="280b5-145">If your application is referencing any NuGet packages, update them to the latest version.</span></span> <span data-ttu-id="280b5-146">請確定您的應用程式建置成功。</span><span class="sxs-lookup"><span data-stu-id="280b5-146">Ensure your application builds successfully.</span></span> <span data-ttu-id="280b5-147">升級後，如果有任何套件錯誤，請將套件降級為不會中斷程式碼的最新版本。</span><span class="sxs-lookup"><span data-stu-id="280b5-147">After upgrading, if there are any package errors, downgrade the package to the latest version that doesn't break your code.</span></span>

## <a name="create-a-new-sdk-project"></a><span data-ttu-id="280b5-148">建立新的 SDK 專案</span><span class="sxs-lookup"><span data-stu-id="280b5-148">Create a new SDK project</span></span>

<span data-ttu-id="280b5-149">您所建立的新 .NET Core 3.0 專案必須與 .NET Framework 專案位於不同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="280b5-149">The new .NET Core 3.0 project you create must be in a different directory from your .NET Framework project.</span></span> <span data-ttu-id="280b5-150">如果它們都在相同的目錄中，則可能會與 **obj** 目錄中產生的檔案發生衝突。</span><span class="sxs-lookup"><span data-stu-id="280b5-150">If they're both in the same directory, you may run into conflicts with the files that are generated in the **obj** directory.</span></span> <span data-ttu-id="280b5-151">在此範例中，我們將在 **SolutionFolder** 目錄中建立名為 **MyFormsAppCore** 的目錄：</span><span class="sxs-lookup"><span data-stu-id="280b5-151">In this example, we'll create a directory named **MyFormsAppCore** in the **SolutionFolder** directory:</span></span>

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
└───MyFormsAppCore      <--- New folder for core project
```

<span data-ttu-id="280b5-152">接下來，您需要在 **MyFormsAppCore** 目錄中建立 **MyFormsCore.csproj** 專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-152">Next, you need to create the **MyFormsCore.csproj** project in the **MyFormsAppCore** directory.</span></span> <span data-ttu-id="280b5-153">您可以使用選擇的文字編輯器以手動方式建立此檔案。</span><span class="sxs-lookup"><span data-stu-id="280b5-153">You can create this file manually by using the text editor of choice.</span></span> <span data-ttu-id="280b5-154">貼上下列 XML：</span><span class="sxs-lookup"><span data-stu-id="280b5-154">Paste in the following XML:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="280b5-155">如果您不想以手動方式建立專案檔案，則您可以使用 Visual Studio 或 .NET Core SDK 產生專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-155">If you don't want to create the project file manually, you can use Visual Studio or the .NET Core SDK to generate the project.</span></span> <span data-ttu-id="280b5-156">但是，您必須刪除專案範本所產生的所有其他檔案，專案檔除外。</span><span class="sxs-lookup"><span data-stu-id="280b5-156">However, you must delete all other files generated by the project template except for the project file.</span></span> <span data-ttu-id="280b5-157">若要使用 SDK，請從 **SolutionFolder** 目錄執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="280b5-157">To use the SDK, run the following command from the **SolutionFolder** directory:</span></span>

```dotnetcli
dotnet new winforms -o MyFormsAppCore -n MyFormsCore
```

<span data-ttu-id="280b5-158">建立 **MyFormsCore.csproj** 後，您的目錄結構應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="280b5-158">After you create the **MyFormsCore.csproj**, your directory structure should look like the following:</span></span>

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
└───MyFormsAppCore
    └───MyFormsCore.csproj
```

<span data-ttu-id="280b5-159">使用**SolutionFolder**目錄中的 Visual Studio 或 .NET Core CLI，將 **>myformscore.csproj .csproj**專案加入至**MyApps .sln** ：</span><span class="sxs-lookup"><span data-stu-id="280b5-159">Add the **MyFormsCore.csproj** project to **MyApps.sln** with either Visual Studio or the .NET Core CLI from the **SolutionFolder** directory:</span></span>

```dotnetcli
dotnet sln add .\MyFormsAppCore\MyFormsCore.csproj
```

## <a name="fix-assembly-info-generation"></a><span data-ttu-id="280b5-160">修正組件資訊產生</span><span class="sxs-lookup"><span data-stu-id="280b5-160">Fix assembly info generation</span></span>

<span data-ttu-id="280b5-161">使用 .NET Framework 所建立的 Windows Forms 專案包含 `AssemblyInfo.cs` 檔案，該檔案包含組件屬性，例如要產生的組件版本。</span><span class="sxs-lookup"><span data-stu-id="280b5-161">Windows Forms projects that were created with .NET Framework include an `AssemblyInfo.cs` file, which contains assembly attributes such as the version of the assembly to be generated.</span></span> <span data-ttu-id="280b5-162">SDK 樣式專案會根據 SDK 專案檔自動為您產生此資訊。</span><span class="sxs-lookup"><span data-stu-id="280b5-162">SDK-style projects automatically generate this information for you based on the SDK project file.</span></span> <span data-ttu-id="280b5-163">同時具有兩種類型的「組件資訊」會發生衝突。</span><span class="sxs-lookup"><span data-stu-id="280b5-163">Having both types of "assembly info" creates a conflict.</span></span> <span data-ttu-id="280b5-164">藉由停用自動產生來解決此問題，這會強制專案使用現有的 `AssemblyInfo.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="280b5-164">Resolve this problem by disabling automatic generation, which forces the project to use your existing `AssemblyInfo.cs` file.</span></span>

<span data-ttu-id="280b5-165">加入至主要 `<PropertyGroup>` 節點有三個設定。</span><span class="sxs-lookup"><span data-stu-id="280b5-165">There are three settings to add to the main `<PropertyGroup>` node.</span></span>

- <span data-ttu-id="280b5-166">**GenerateAssemblyInfo**</span><span class="sxs-lookup"><span data-stu-id="280b5-166">**GenerateAssemblyInfo**</span></span>\
<span data-ttu-id="280b5-167">當您將此屬性設定為 `false`，它就不會產生組件屬性。</span><span class="sxs-lookup"><span data-stu-id="280b5-167">When you set this property to `false`, it won't generate the assembly attributes.</span></span> <span data-ttu-id="280b5-168">這可以避免與 .NET Framework 專案中的現有 `AssemblyInfo.cs` 檔案衝突。</span><span class="sxs-lookup"><span data-stu-id="280b5-168">This avoids the conflict with the existing `AssemblyInfo.cs` file from the .NET Framework project.</span></span>

- <span data-ttu-id="280b5-169">**集**</span><span class="sxs-lookup"><span data-stu-id="280b5-169">**AssemblyName**</span></span>\
<span data-ttu-id="280b5-170">這個屬性的值是您在編譯時所建立的二進位輸出。</span><span class="sxs-lookup"><span data-stu-id="280b5-170">The value of this property is the output binary created when you compile.</span></span> <span data-ttu-id="280b5-171">該名稱不需要加入副檔名。</span><span class="sxs-lookup"><span data-stu-id="280b5-171">The name doesn't need an extension added to it.</span></span> <span data-ttu-id="280b5-172">例如，使用 `MyCoreApp` 產生 `MyCoreApp.exe`。</span><span class="sxs-lookup"><span data-stu-id="280b5-172">For example, using `MyCoreApp` produces `MyCoreApp.exe`.</span></span>

- <span data-ttu-id="280b5-173">**RootNamespace**</span><span class="sxs-lookup"><span data-stu-id="280b5-173">**RootNamespace**</span></span>\
<span data-ttu-id="280b5-174">專案使用的預設命名空間。</span><span class="sxs-lookup"><span data-stu-id="280b5-174">The default namespace used by your project.</span></span> <span data-ttu-id="280b5-175">這應該與 .NET Framework 專案的預設命名空間相符。</span><span class="sxs-lookup"><span data-stu-id="280b5-175">This should match the default namespace of the .NET Framework project.</span></span>

<span data-ttu-id="280b5-176">將這三個元素新增至 `MyFormsCore.csproj` 檔案中的 `<PropertyGroup>` 節點：</span><span class="sxs-lookup"><span data-stu-id="280b5-176">Add these three elements to the `<PropertyGroup>` node in the `MyFormsCore.csproj` file:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>

    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
    <AssemblyName>MyCoreApp</AssemblyName>
    <RootNamespace>WindowsFormsApp1</RootNamespace>
  </PropertyGroup>

</Project>
```

## <a name="add-source-code"></a><span data-ttu-id="280b5-177">新增原始程式碼</span><span class="sxs-lookup"><span data-stu-id="280b5-177">Add source code</span></span>

<span data-ttu-id="280b5-178">現在，**MyFormsCore.csproj** 專案不會進行編譯任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="280b5-178">Right now, the **MyFormsCore.csproj** project doesn't compile any code.</span></span> <span data-ttu-id="280b5-179">根據預設，.NET Core 專案會自動包含目前目錄和任何子目錄中的所有原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="280b5-179">By default, .NET Core projects automatically include all source code in the current directory and any child directories.</span></span> <span data-ttu-id="280b5-180">您必須使用相對路徑，將專案設定為包含 .NET Framework 專案中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="280b5-180">You must configure the project to include code from the .NET Framework project using a relative path.</span></span> <span data-ttu-id="280b5-181">如果您的 .NET Framework 專案使用 **.resx** 檔案作為表單的圖示和資源，那麼您還需要包含這些檔案。</span><span class="sxs-lookup"><span data-stu-id="280b5-181">If your .NET Framework project used **.resx** files for icons and resources for your forms, you'll need to include those too.</span></span>

<span data-ttu-id="280b5-182">將下列 `<ItemGroup>` 節點新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-182">Add the following `<ItemGroup>` node to your project.</span></span> <span data-ttu-id="280b5-183">每個陳述式都包含一個檔案 Glob 模式，其中包含子目錄。</span><span class="sxs-lookup"><span data-stu-id="280b5-183">Each statement includes a file glob pattern that includes child directories.</span></span>

```xml
  <ItemGroup>
    <Compile Include="..\MyFormsApp\**\*.cs" />
    <EmbeddedResource Include="..\MyFormsApp\**\*.resx" />
  </ItemGroup>
```

<span data-ttu-id="280b5-184">或者，您可以為 .NET Framework 專案中的每個檔案建立 `<Compile>` 或 `<EmbeddedResource>` 項目。</span><span class="sxs-lookup"><span data-stu-id="280b5-184">Alternatively, you can create a `<Compile>` or `<EmbeddedResource>` entry for each file in your .NET Framework project.</span></span>

## <a name="add-nuget-packages"></a><span data-ttu-id="280b5-185">新增 NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="280b5-185">Add NuGet packages</span></span>

<span data-ttu-id="280b5-186">將 .NET Framework 專案參考的每個 NuGet 套件新增至 .NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-186">Add each NuGet package referenced by the .NET Framework project to the .NET Core project.</span></span>

<span data-ttu-id="280b5-187">很可能您的 .NET Framework Windows Forms 應用程式有一個 **packages.config** 檔案，其中包含您的專案所參考的 NuGet 套件的清單。</span><span class="sxs-lookup"><span data-stu-id="280b5-187">Most likely your .NET Framework Windows Forms app has a **packages.config** file that contains a list of all of the NuGet packages that are referenced by your project.</span></span> <span data-ttu-id="280b5-188">您可以查看這份清單以判斷要新增至 .NET Core 專案的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="280b5-188">You can look at this list to determine which NuGet packages to add to the .NET Core project.</span></span> <span data-ttu-id="280b5-189">例如，如果 .NET Framework 專案參考了 `MetroFramework`、`MetroFramework.Design` 和 `MetroFramework.Fonts` NuGet 套件，請使用 Visual Studio 或 **SolutionFolder** 目錄中的 .NET Core CLI 將每個套件新增至專案中：</span><span class="sxs-lookup"><span data-stu-id="280b5-189">For example, if the .NET Framework project referenced the `MetroFramework`, `MetroFramework.Design`, and `MetroFramework.Fonts` NuGet packages, add each to the project with either Visual Studio or the .NET Core CLI from the **SolutionFolder** directory:</span></span>

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework.Design
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package MetroFramework.Fonts
```

<span data-ttu-id="280b5-190">上述命令會將下列 NuGet 參考新增到 **MyFormsCore.csproj** 專案中：</span><span class="sxs-lookup"><span data-stu-id="280b5-190">The previous commands would add the following NuGet references to the **MyFormsCore.csproj** project:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="MetroFramework" Version="1.2.0.3" />
    <PackageReference Include="MetroFramework.Design" Version="1.2.0.3" />
    <PackageReference Include="MetroFramework.Fonts" Version="1.2.0.3" />
  </ItemGroup>
```

## <a name="port-control-libraries"></a><span data-ttu-id="280b5-191">移植控制項程式庫</span><span class="sxs-lookup"><span data-stu-id="280b5-191">Port control libraries</span></span>

<span data-ttu-id="280b5-192">如果您有要移植的 Windows Forms 控制項程式庫專案，則說明與移植 .NET Framework Windows Forms 應用程式專案相同，但少數設定除外。</span><span class="sxs-lookup"><span data-stu-id="280b5-192">If you have a Windows Forms Controls library project to port, the directions are the same as porting a .NET Framework Windows Forms app project, except for a few settings.</span></span> <span data-ttu-id="280b5-193">相對於編譯成可執行檔，您會編譯到程式庫。</span><span class="sxs-lookup"><span data-stu-id="280b5-193">And instead of compiling to an executable, you compile to a library.</span></span> <span data-ttu-id="280b5-194">除了包含原始程式碼的檔案 Glob 路徑之外，可執行檔的專案和程式庫專案之間的差異很小。</span><span class="sxs-lookup"><span data-stu-id="280b5-194">The difference between the executable project and the library project, besides paths for the file globs that include your source code, is minimal.</span></span>

<span data-ttu-id="280b5-195">使用上一個步驟的範例，讓我們展開我們正在使用的專案和檔案。</span><span class="sxs-lookup"><span data-stu-id="280b5-195">Using the previous step's example, lets expand what projects and files we're working with.</span></span>

| <span data-ttu-id="280b5-196">檔案</span><span class="sxs-lookup"><span data-stu-id="280b5-196">File</span></span> | <span data-ttu-id="280b5-197">描述</span><span class="sxs-lookup"><span data-stu-id="280b5-197">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="280b5-198">**MyApps.sln**</span><span class="sxs-lookup"><span data-stu-id="280b5-198">**MyApps.sln**</span></span> | <span data-ttu-id="280b5-199">方案檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="280b5-199">The name of the solution file.</span></span> |
| <span data-ttu-id="280b5-200">**MyControls.csproj**</span><span class="sxs-lookup"><span data-stu-id="280b5-200">**MyControls.csproj**</span></span> | <span data-ttu-id="280b5-201">要移植的 .NET Framework Windows Forms 控制項專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="280b5-201">The name of the .NET Framework Windows Forms Controls project to port.</span></span> |
| <span data-ttu-id="280b5-202">**MyControlsCore.csproj**</span><span class="sxs-lookup"><span data-stu-id="280b5-202">**MyControlsCore.csproj**</span></span> | <span data-ttu-id="280b5-203">您所建立的新 .NET Core 程式庫專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="280b5-203">The name of the new .NET Core library project you create.</span></span> |
| <span data-ttu-id="280b5-204">**MyCoreControls.dll**</span><span class="sxs-lookup"><span data-stu-id="280b5-204">**MyCoreControls.dll**</span></span> | <span data-ttu-id="280b5-205">.NET Core Windows Forms 控制項程式庫。</span><span class="sxs-lookup"><span data-stu-id="280b5-205">The .NET Core Windows Forms Controls library.</span></span> |

```
SolutionFolder
├───MyApps.sln
├───MyFormsApp
│   └───MyForms.csproj
├───MyFormsAppCore
│   └───MyFormsCore.csproj
│
├───MyFormsControls
│   └───MyControls.csproj
└───MyFormsControlsCore
    └───MyControlsCore.csproj   <--- New project for core controls
```

<span data-ttu-id="280b5-206">請考慮 `MyControlsCore.csproj` 專案與先前建立的 `MyFormsCore.csproj` 專案之間的差異。</span><span class="sxs-lookup"><span data-stu-id="280b5-206">Consider the differences between the `MyControlsCore.csproj` project and the previously created `MyFormsCore.csproj` project.</span></span>

```diff
 <Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

   <PropertyGroup>
-    <OutputType>WinExe</OutputType>
     <TargetFramework>netcoreapp3.0</TargetFramework>
     <UseWindowsForms>true</UseWindowsForms>

     <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
-    <AssemblyName>MyCoreApp</AssemblyName>
-    <RootNamespace>WindowsFormsApp1</RootNamespace>
+    <AssemblyName>MyControlsCore</AssemblyName>
+    <RootNamespace>WindowsFormsControlLibrary1</RootNamespace>
   </PropertyGroup>

   <ItemGroup>
-    <Compile Include="..\MyFormsApp\**\*.cs" />
-    <EmbeddedResource Include="..\MyFormsApp\**\*.resx" />
+    <Compile Include="..\MyFormsControls\**\*.cs" />
+    <EmbeddedResource Include="..\MyFormsControls\**\*.resx" />
   </ItemGroup>

 </Project>
```

<span data-ttu-id="280b5-207">以下是 .NET Core Windows Forms 控制項程式庫專案檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="280b5-207">Here is an example of what the .NET Core Windows Forms Controls library project file would look like:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.WindowsDesktop">

  <PropertyGroup>

    <TargetFramework>netcoreapp3.0</TargetFramework>
    <UseWindowsForms>true</UseWindowsForms>

    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
    <AssemblyName>MyCoreControls</AssemblyName>
    <RootNamespace>WindowsFormsControlLibrary1</RootNamespace>
  </PropertyGroup>

  <ItemGroup>
    <Compile Include="..\MyFormsControls\**\*.cs" />
    <EmbeddedResource Include="..\MyFormsControls\**\*.resx" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="280b5-208">如您所見，`<OutputType>` 節點已被刪除，編譯器預設會產生程式庫，而不是可執行檔。</span><span class="sxs-lookup"><span data-stu-id="280b5-208">As you can see, the `<OutputType>` node was removed, which defaults the compiler to produce a library instead of an executable.</span></span> <span data-ttu-id="280b5-209">`<AssemblyName>` 和 `<RootNamespace>` 已變更。</span><span class="sxs-lookup"><span data-stu-id="280b5-209">The `<AssemblyName>` and `<RootNamespace>` were changed.</span></span> <span data-ttu-id="280b5-210">具體來說，`<RootNamespace>` 應符合您正在移植的 Windows Forms 控制項程式庫的命名空間。</span><span class="sxs-lookup"><span data-stu-id="280b5-210">Specifically the `<RootNamespace>` should match the namespace of the Windows Forms Controls library you are porting.</span></span> <span data-ttu-id="280b5-211">最後，調整 `<Compile>` 和 `<EmbeddedResource>` 節點以指向要移植的 Windows Forms 控制項程式庫的資料夾。</span><span class="sxs-lookup"><span data-stu-id="280b5-211">And finally, the `<Compile>` and `<EmbeddedResource>` nodes were adjusted to point to the folder of the Windows Forms Controls library you are porting.</span></span>

<span data-ttu-id="280b5-212">接下來，在主要的 .NET Core **>myformscore.csproj .csproj** 專案中，加入新 .net Core Windows Forms 控制項程式庫的參考。</span><span class="sxs-lookup"><span data-stu-id="280b5-212">Next, in the main .NET Core **MyFormsCore.csproj** project, add a reference to the new .NET Core Windows Forms Control library.</span></span> <span data-ttu-id="280b5-213">使用 Visual Studio 或 **SolutionFolder** 目錄中的 .NET Core CLI 新增參考：</span><span class="sxs-lookup"><span data-stu-id="280b5-213">Add a reference with either Visual Studio or the .NET Core CLI from the **SolutionFolder** directory:</span></span>

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj reference .\MyFormsControlsCore\MyControlsCore.csproj
```

<span data-ttu-id="280b5-214">上一個命令會將下列內容新增到 **MyFormsCore.csproj** 專案：</span><span class="sxs-lookup"><span data-stu-id="280b5-214">The previous command adds the following to the **MyFormsCore.csproj** project:</span></span>

```xml
  <ItemGroup>
    <ProjectReference Include="..\MyFormsControlsCore\MyControlsCore.csproj" />
  </ItemGroup>
```

## <a name="compilation-problems"></a><span data-ttu-id="280b5-215">編譯問題</span><span class="sxs-lookup"><span data-stu-id="280b5-215">Compilation problems</span></span>

<span data-ttu-id="280b5-216">如果您在編譯專案時遇到問題，則您可能正在使用 .NET Framework 中提供但不適用於 .NET Core 的一些僅限 Windows 的 API。</span><span class="sxs-lookup"><span data-stu-id="280b5-216">If you have problems compiling your projects, you may be using some Windows-only APIs that are available in .NET Framework but not available in .NET Core.</span></span> <span data-ttu-id="280b5-217">您可以嘗試將 [Windows 相容性套件][compat-pack] NuGet 套件新增到您的專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-217">You can try adding the [Windows Compatibility Pack][compat-pack] NuGet package to your project.</span></span> <span data-ttu-id="280b5-218">此套件只能在 Windows 上執行，並為 .NET Core 和 .NET Standard 專案新增了大約 20,000 個 Windows API。</span><span class="sxs-lookup"><span data-stu-id="280b5-218">This package only runs on Windows and adds about 20,000 Windows APIs to .NET Core and .NET Standard projects.</span></span>

```dotnetcli
dotnet add .\MyFormsAppCore\MyFormsCore.csproj package Microsoft.Windows.Compatibility
```

<span data-ttu-id="280b5-219">上一個命令會將下列內容新增到 **MyFormsCore.csproj** 專案：</span><span class="sxs-lookup"><span data-stu-id="280b5-219">The previous command adds the following to the **MyFormsCore.csproj** project:</span></span>

```xml
  <ItemGroup>
    <PackageReference Include="Microsoft.Windows.Compatibility" Version="3.1.0" />
  </ItemGroup>
```

## <a name="windows-forms-designer"></a><span data-ttu-id="280b5-220">Windows Form 設計工具</span><span class="sxs-lookup"><span data-stu-id="280b5-220">Windows Forms Designer</span></span>

<span data-ttu-id="280b5-221">如此文章所述，Visual Studio 2019 僅支援 .NET Framework 專案中的表單設計工具。</span><span class="sxs-lookup"><span data-stu-id="280b5-221">As detailed in this article, Visual Studio 2019 only supports the Forms Designer in .NET Framework projects.</span></span> <span data-ttu-id="280b5-222">藉由建立並排.NET Core 專案，您可以在使用 .NET Framework 專案設計表單時，同時使用 .NET Core 測試您的專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-222">By creating a side-by-side .NET Core project, you can test your project with .NET Core while you use the .NET Framework project to design forms.</span></span> <span data-ttu-id="280b5-223">您的方案檔包含 .NET Framework 和 .NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-223">Your solution file includes both the .NET Framework and .NET Core projects.</span></span> <span data-ttu-id="280b5-224">在 .NET Framework 專案中新增和設計您的表單和控制項，且根據我們新增至 .NET Core 專案的檔案 Glob 模式，任何新的或已變更的檔案將自動包含在 .NET Core 專案中。</span><span class="sxs-lookup"><span data-stu-id="280b5-224">Add and design your forms and controls in the .NET Framework project, and based on the file glob patterns we added to the .NET Core projects, any new or changed files will automatically be included in the .NET Core projects.</span></span>

<span data-ttu-id="280b5-225">一旦 Visual Studio 2019 支援 Windows Form 設計工具，您就可以將 .NET Core 專案檔案的內容複製/貼上到 .NET Framework 專案檔案中。</span><span class="sxs-lookup"><span data-stu-id="280b5-225">Once Visual Studio 2019 supports the Windows Forms Designer, you can copy/paste the content of your .NET Core project file into the .NET Framework project file.</span></span> <span data-ttu-id="280b5-226">然後刪除新增了 `<Source>` 和 `<EmbeddedResource>` 項目的檔案 Glob 模式。</span><span class="sxs-lookup"><span data-stu-id="280b5-226">Then delete the file glob patterns added with the `<Source>` and `<EmbeddedResource>` items.</span></span> <span data-ttu-id="280b5-227">修正應用程式所使用之任何專案參考的路徑。</span><span class="sxs-lookup"><span data-stu-id="280b5-227">Fix the paths to any project reference used by your app.</span></span> <span data-ttu-id="280b5-228">這會有效地將 .NET Framework 專案升級至 .NET Core 專案。</span><span class="sxs-lookup"><span data-stu-id="280b5-228">This effectively upgrades the .NET Framework project to a .NET Core project.</span></span>

## <a name="next-steps"></a><span data-ttu-id="280b5-229">接下來的步驟</span><span class="sxs-lookup"><span data-stu-id="280b5-229">Next steps</span></span>

- <span data-ttu-id="280b5-230">瞭解 [從 .NET Framework 到 .Net Core 的重大變更](../compatibility/fx-core.md)。</span><span class="sxs-lookup"><span data-stu-id="280b5-230">Learn about [breaking changes from .NET Framework to .NET Core](../compatibility/fx-core.md).</span></span>
- <span data-ttu-id="280b5-231">深入了解 [Windows 相容性套件][compat-pack]。</span><span class="sxs-lookup"><span data-stu-id="280b5-231">Read more about the [Windows Compatibility Pack][compat-pack].</span></span>
- <span data-ttu-id="280b5-232">觀看[有關移植](https://www.youtube.com/watch?v=upVQEUc_KwU) .NET Framework Windows Form 專案到 .NET Core 的影片。</span><span class="sxs-lookup"><span data-stu-id="280b5-232">Watch a [video on porting](https://www.youtube.com/watch?v=upVQEUc_KwU) your .NET Framework Windows Forms project to .NET Core.</span></span>

[compat-pack]: windows-compat-pack.md
