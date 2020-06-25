---
title: 建立適用於 dotnet new 的範本套件
description: 了解如何建立將會針對 dotnet new 命令建置範本套件的 csproj 檔案。
author: adegeo
ms.date: 12/10/2019
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 25264fff42c47f5bb660f68f85dbb123b5b2608c
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324334"
---
# <a name="tutorial-create-a-template-pack"></a><span data-ttu-id="bcf5d-103">教學課程：建立範本套件</span><span class="sxs-lookup"><span data-stu-id="bcf5d-103">Tutorial: Create a template pack</span></span>

<span data-ttu-id="bcf5d-104">透過 .NET Core，您可以建立及部署能產生專案、檔案，甚至是資源的範本。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-104">With .NET Core, you can create and deploy templates that generate projects, files, even resources.</span></span> <span data-ttu-id="bcf5d-105">本教學課程是系列中的第三部分，會教您如何建立、安裝和卸載範本以搭配 `dotnet new` 命令使用。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-105">This tutorial is part three of a series that teaches you how to create, install, and uninstall templates for use with the `dotnet new` command.</span></span>

<span data-ttu-id="bcf5d-106">在這部分的系列文章中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="bcf5d-106">In this part of the series you'll learn how to:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="bcf5d-107">建立 \* .csproj 專案以建立範本套件</span><span class="sxs-lookup"><span data-stu-id="bcf5d-107">Create a \*.csproj project to build a template pack</span></span>
> * <span data-ttu-id="bcf5d-108">設定專案檔以用於封裝</span><span class="sxs-lookup"><span data-stu-id="bcf5d-108">Configure the project file for packing</span></span>
> * <span data-ttu-id="bcf5d-109">從 NuGet 套件檔案安裝範本</span><span class="sxs-lookup"><span data-stu-id="bcf5d-109">Install a template from a NuGet package file</span></span>
> * <span data-ttu-id="bcf5d-110">依套件識別碼將範本解除安裝</span><span class="sxs-lookup"><span data-stu-id="bcf5d-110">Uninstall a template by package ID</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bcf5d-111">先決條件</span><span class="sxs-lookup"><span data-stu-id="bcf5d-111">Prerequisites</span></span>

* <span data-ttu-id="bcf5d-112">完成此教學課程系列的[第 1 部分](cli-templates-create-item-template.md)和[第 2 部分](cli-templates-create-project-template.md)。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-112">Complete [part 1](cli-templates-create-item-template.md) and [part 2](cli-templates-create-project-template.md) of this tutorial series.</span></span>

  <span data-ttu-id="bcf5d-113">此教學課程會使用在此教學課程系列的前兩個部分中所建立的兩個範本。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-113">This tutorial uses the two templates created in the first two parts of this tutorial.</span></span> <span data-ttu-id="bcf5d-114">只要您將範本當做資料夾複製到_working\templates \\ _資料夾，就可以使用不同的範本。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-114">You can use a different template as long as you copy the template, as a folder, into the _working\templates\\_ folder.</span></span>

* <span data-ttu-id="bcf5d-115">開啟終端機，並流覽至_工作 \\ _資料夾。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-115">Open a terminal and navigate to the _working\\_ folder.</span></span>

## <a name="create-a-template-pack-project"></a><span data-ttu-id="bcf5d-116">建立範本套件專案</span><span class="sxs-lookup"><span data-stu-id="bcf5d-116">Create a template pack project</span></span>

<span data-ttu-id="bcf5d-117">範本套件是將一或多個範本封裝到檔案內。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-117">A template pack is one or more templates packaged into a file.</span></span> <span data-ttu-id="bcf5d-118">當您安裝或解除安裝套件時，包含在套件中的所有範本也都會相對地被新增或移除。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-118">When you install or uninstall a pack, all templates contained in the pack are added or removed, respectively.</span></span> <span data-ttu-id="bcf5d-119">此教學課程系列之前的部分皆僅處理個別的範本。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-119">The previous parts of this tutorial series only worked with individual templates.</span></span> <span data-ttu-id="bcf5d-120">若要共用未封裝的範本，您必須複製範本資料夾並透過該資料夾來安裝。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-120">To share a non-packed template, you have to copy the template folder and install via that folder.</span></span> <span data-ttu-id="bcf5d-121">由於範本套件可以在其中具有多個範本且為單一檔案，因此共用會變得更加容易。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-121">Because a template pack can have more than one template in it, and is a single file, sharing is easier.</span></span>

<span data-ttu-id="bcf5d-122">範本套件是以 NuGet 套件 (_.nupkg_) 檔案來代表。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-122">Template packs are represented by a NuGet package (_.nupkg_) file.</span></span> <span data-ttu-id="bcf5d-123">此外，和任何 NuGet 套件相同，您可以將範本套件上傳至 NuGet 摘要。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-123">And, like any NuGet package, you can upload the template pack to a NuGet feed.</span></span> <span data-ttu-id="bcf5d-124">`dotnet new -i` 命令支援從 NuGet 套件摘要安裝範本套件。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-124">The `dotnet new -i` command supports installing template pack from a NuGet package feed.</span></span> <span data-ttu-id="bcf5d-125">此外，您可以直接從 _.nupkg_ 檔案安裝範本套件。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-125">Additionally, you can install a template pack from a _.nupkg_ file directly.</span></span>

<span data-ttu-id="bcf5d-126">通常，您可以使用 C# 專案檔來編譯程式碼並產生二進位檔。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-126">Normally you use a C# project file to compile code and produce a binary.</span></span> <span data-ttu-id="bcf5d-127">不過，專案也可以用來產生範本套件。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-127">However, the project can also be used to generate a template pack.</span></span> <span data-ttu-id="bcf5d-128">透過變更 _.csproj_ 的設定，您會防止它編譯任何程式碼，並改為使它將您範本的所有資產包含為資源。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-128">By changing the settings of the _.csproj_, you can prevent it from compiling any code and instead include all the assets of your templates as resources.</span></span> <span data-ttu-id="bcf5d-129">在建置此專案之後，它會產生範本套件 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-129">When this project is built, it produces a template pack NuGet package.</span></span>

<span data-ttu-id="bcf5d-130">您建立的套件將會包含先前所建立的[項目範本](cli-templates-create-item-template.md)和[專案範本](cli-templates-create-project-template.md)。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-130">The pack you'll create will include the [item template](cli-templates-create-item-template.md) and [package template](cli-templates-create-project-template.md) previously created.</span></span> <span data-ttu-id="bcf5d-131">由於我們將這兩個範本分組到 _working\templates\\_ 資料夾，我們可以針對 _.csproj_ 檔案使用 _working_ 資料夾。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-131">Because we grouped the two templates into the _working\templates\\_ folder, we can use the _working_ folder for the _.csproj_ file.</span></span>

<span data-ttu-id="bcf5d-132">在您的終端機中，瀏覽至 _working_ 資料夾。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-132">In your terminal, navigate to the _working_ folder.</span></span> <span data-ttu-id="bcf5d-133">建立新專案，並將名稱設定為 `templatepack`，然後將輸出資料夾設定為目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-133">Create a new project and set the name to `templatepack` and the output folder to the current folder.</span></span>

```dotnetcli
dotnet new console -n templatepack -o .
```

<span data-ttu-id="bcf5d-134">`-n`參數會將 _.csproj_檔案名設定為_templatepack_。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-134">The `-n` parameter sets the _.csproj_ filename to _templatepack.csproj_.</span></span> <span data-ttu-id="bcf5d-135">`-o`參數會在目前的目錄中建立檔案。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-135">The `-o` parameter creates the files in the current directory.</span></span> <span data-ttu-id="bcf5d-136">您應該會看到類似以下輸出的結果。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-136">You should see a result similar to the following output.</span></span>

```dotnetcli
dotnet new console -n templatepack -o .
```

```console
The template "Console Application" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on .\templatepack.csproj...
  Restore completed in 52.38 ms for C:\working\templatepack.csproj.

Restore succeeded.
```

<span data-ttu-id="bcf5d-137">接下來，在您慣用的編輯器中開啟 _templatepack.csproj_ 檔案，並以下列 XML 取代其內容：</span><span class="sxs-lookup"><span data-stu-id="bcf5d-137">Next, open the _templatepack.csproj_ file in your favorite editor and replace the content with the following XML:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <PackageType>Template</PackageType>
    <PackageVersion>1.0</PackageVersion>
    <PackageId>AdatumCorporation.Utility.Templates</PackageId>
    <Title>AdatumCorporation Templates</Title>
    <Authors>Me</Authors>
    <Description>Templates to use when creating an application for Adatum Corporation.</Description>
    <PackageTags>dotnet-new;templates;contoso</PackageTags>

    <TargetFramework>netstandard2.0</TargetFramework>

    <IncludeContentInPack>true</IncludeContentInPack>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <ContentTargetFolders>content</ContentTargetFolders>
  </PropertyGroup>

  <ItemGroup>
    <Content Include="templates\**\*" Exclude="templates\**\bin\**;templates\**\obj\**" />
    <Compile Remove="**\*" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="bcf5d-138">上面 XML 中的 `<PropertyGroup>` 設定會被分成三個群組。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-138">The `<PropertyGroup>` settings in the XML above is broken into three groups.</span></span> <span data-ttu-id="bcf5d-139">第一個群組會處理 NuGet 套件的必要屬性。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-139">The first group deals with properties required for a NuGet package.</span></span> <span data-ttu-id="bcf5d-140">三個 `<Package` 設定和用來在 NuGet 摘要上識別您套件的 NuGet 套件屬性有關。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-140">The three `<Package` settings have to do with the NuGet package properties to identify your package on a NuGet feed.</span></span> <span data-ttu-id="bcf5d-141">特別是 `<PackageId>` 值，其是用來透過單一名稱 (而非目錄路徑) 將範本套件解除安裝。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-141">Specifically the `<PackageId>` value is used to uninstall the template pack with a single name instead of a directory path.</span></span> <span data-ttu-id="bcf5d-142">它也可以用來從 NuGet 摘要安裝範本套件。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-142">It can also be used to install the template pack from a NuGet feed.</span></span> <span data-ttu-id="bcf5d-143">其餘的設定 (例如 `<Title>` 和 `<PackageTags>`) 都與顯示在 NuGet 摘要上的中繼資料有關。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-143">The remaining settings such as `<Title>` and `<PackageTags>` have to do with metadata displayed on the NuGet feed.</span></span> <span data-ttu-id="bcf5d-144">如需 NuGet 設定的詳細資訊，請參閱 [NuGet 和 MSBuild 屬性](/nuget/reference/msbuild-targets)。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-144">For more information about NuGet settings, see [NuGet and MSBuild properties](/nuget/reference/msbuild-targets).</span></span>

<span data-ttu-id="bcf5d-145">必須設定 `<TargetFramework>` 設定，來使 MSBuild 能在您執行封裝命令以編譯及封裝專案時能夠正常執行。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-145">The `<TargetFramework>` setting must be set so that MSBuild will run properly when you run the pack command to compile and pack the project.</span></span>

<span data-ttu-id="bcf5d-146">最後的三個設定與在建立 NuGet 套件時正確設定專案，以將範本包含在 NuGet 套件中適當的資料夾有關。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-146">The last three settings have to do with configuring the project correctly to include the templates in the appropriate folder in the NuGet pack when it's created.</span></span>

<span data-ttu-id="bcf5d-147">`<ItemGroup>` 包含兩個設定。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-147">The `<ItemGroup>` contains two settings.</span></span> <span data-ttu-id="bcf5d-148">首先，`<Content>` 設定會將 _templates_ 資料夾中的所有項目包含為內容。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-148">First, the `<Content>` setting includes everything in the _templates_ folder as content.</span></span> <span data-ttu-id="bcf5d-149">它也會排除任何 _bin_ 資料夾或 _obj_ 資料夾，以防止包含任何已編譯的程式碼 (如果您已測試並編譯您的範本的話)。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-149">It's also set to exclude any _bin_ folder or _obj_ folder to prevent any compiled code (if you tested and compiled your templates) from being included.</span></span> <span data-ttu-id="bcf5d-150">再來，`<Compile>` 設定會將所有程式碼檔案排除在編譯之外，無論它們位於何處。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-150">Second, the `<Compile>` setting excludes all code files from compiling no matter where they're located.</span></span> <span data-ttu-id="bcf5d-151">此設定能防止用來建立範本套件的專案嘗試編譯 _templates_ 資料夾階層中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-151">This setting prevents the project being used to create a template pack from trying to compile the code in the _templates_ folder hierarchy.</span></span>

## <a name="build-and-install"></a><span data-ttu-id="bcf5d-152">建置及安裝</span><span class="sxs-lookup"><span data-stu-id="bcf5d-152">Build and install</span></span>

<span data-ttu-id="bcf5d-153">儲存此檔案，然後執行封裝命令</span><span class="sxs-lookup"><span data-stu-id="bcf5d-153">Save this file and then run the pack command</span></span>

```dotnetcli
dotnet pack
```

<span data-ttu-id="bcf5d-154">此命令將會建置您的專案，然後在 _working\bin\Debug_ 資料夾中建立 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-154">This command will build your project and create a NuGet package in This should be the _working\bin\Debug_ folder.</span></span>

```dotnetcli
dotnet pack
```

```console
Microsoft (R) Build Engine version 16.2.0-preview-19278-01+d635043bd for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 123.86 ms for C:\working\templatepack.csproj.

  templatepack -> C:\working\bin\Debug\netstandard2.0\templatepack.dll
  Successfully created package 'C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg'.
```

<span data-ttu-id="bcf5d-155">接下來，請使用 `dotnet new -i PATH_TO_NUPKG_FILE` 命令來安裝範本套件檔案。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-155">Next, install the template pack file with the `dotnet new -i PATH_TO_NUPKG_FILE` command.</span></span>

```console
C:\working> dotnet new -i C:\working\bin\Debug\AdatumCorporation.Utility.Templates.1.0.0.nupkg
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name            Language          Tags
-------------------------------------------------------------------------------------------------------------------------------
Example templates: string extensions              stringext             [C#]              Common/Code
Console Application                               console               [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync          [C#]              Common/Console/C#8
Class library                                     classlib              [C#], F#, VB      Common/Library
```

<span data-ttu-id="bcf5d-156">如果您將 NuGet 套件上傳至 NuGet 摘要，您可以使用 `dotnet new -i PACKAGEID` 命令；其中 `PACKAGEID` 和 _.csproj_ 檔案中的 `<PackageId>` 設定相同。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-156">If you uploaded the NuGet package to a NuGet feed, you can use the `dotnet new -i PACKAGEID` command where `PACKAGEID` is the same as the `<PackageId>` setting from the _.csproj_ file.</span></span> <span data-ttu-id="bcf5d-157">此套件識別碼和 NuGet 套件識別碼相同。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-157">This package ID is the same as the NuGet package identifier.</span></span>

## <a name="uninstall-the-template-pack"></a><span data-ttu-id="bcf5d-158">將範本套件解除安裝</span><span class="sxs-lookup"><span data-stu-id="bcf5d-158">Uninstall the template pack</span></span>

<span data-ttu-id="bcf5d-159">無論您安裝範本套件的方法為何 (直接透過 _.nupkg_ 檔案或是透過 NuGet 摘要)，移除範本套件的方法也是相同的。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-159">No matter how you installed the template pack, either with the _.nupkg_ file directly or by NuGet feed, removing a template pack is the same.</span></span> <span data-ttu-id="bcf5d-160">使用您想要解除安裝之範本的 `<PackageId>`。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-160">Use the `<PackageId>` of the template you want to uninstall.</span></span> <span data-ttu-id="bcf5d-161">您可以透過執行 `dotnet new -u` 命令來取得已安裝範本的清單。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-161">You can get a list of templates that are installed by running the `dotnet new -u` command.</span></span>

```dotnetcli
dotnet new -u
```

```console
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ItemTemplates
    Templates:
      dotnet gitignore file (gitignore)
      global.json file (globaljson)
      NuGet Config (nugetconfig)
      Solution File (sln)
      Dotnet local tool manifest file (tool-manifest)
      Web Config (webconfig)

... cut to save space ...

  NUnit3.DotNetNew.Template
    Templates:
      NUnit 3 Test Project (nunit) C#
      NUnit 3 Test Item (nunit-test) C#
      NUnit 3 Test Project (nunit) F#
      NUnit 3 Test Item (nunit-test) F#
      NUnit 3 Test Project (nunit) VB
      NUnit 3 Test Item (nunit-test) VB
  AdatumCorporation.Utility.Templates
    Templates:
      Example templates: async project (consoleasync) C#
      Example templates: string extensions (stringext) C#
```

<span data-ttu-id="bcf5d-162">執行 `dotnet new -u AdatumCorporation.Utility.Templates` 來將範本解除安裝。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-162">Run `dotnet new -u AdatumCorporation.Utility.Templates` to uninstall the template.</span></span> <span data-ttu-id="bcf5d-163">`dotnet new` 命令將會輸出說明資訊，其應該會省略您先前所安裝的範本。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-163">The `dotnet new` command will output help information that should omit the templates you previously installed.</span></span>

<span data-ttu-id="bcf5d-164">恭喜！</span><span class="sxs-lookup"><span data-stu-id="bcf5d-164">Congratulations!</span></span> <span data-ttu-id="bcf5d-165">您已安裝並解除安裝範本套件。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-165">you've installed and uninstalled a template pack.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcf5d-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcf5d-166">Next steps</span></span>

<span data-ttu-id="bcf5d-167">若要深入了解範本 (您已經了解其大部分的內容)，請參閱 [dotnet new 的自訂範本](../tools/custom-templates.md)一文。</span><span class="sxs-lookup"><span data-stu-id="bcf5d-167">To learn more about templates, most of which you've already learned, see the [Custom templates for dotnet new](../tools/custom-templates.md) article.</span></span>

* <span data-ttu-id="bcf5d-168">[dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki) (維基百科：dotnet/templating GitHub 存放庫)</span><span class="sxs-lookup"><span data-stu-id="bcf5d-168">[dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki)</span></span>
* <span data-ttu-id="bcf5d-169">[dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples) (dotnet/dotnet-template-samples GitHub 存放庫)</span><span class="sxs-lookup"><span data-stu-id="bcf5d-169">[dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples)</span></span>
* [<span data-ttu-id="bcf5d-170">JSON 結構描述保存區的 *template.json* 結構描述</span><span class="sxs-lookup"><span data-stu-id="bcf5d-170">*template.json* schema at the JSON Schema Store</span></span>](http://json.schemastore.org/template)
