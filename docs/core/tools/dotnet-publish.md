---
title: dotnet publish 命令
description: Dotnet publish 命令會將 .NET Core 專案或方案發行至目錄。
ms.date: 02/24/2020
ms.openlocfilehash: 697746291a8b34a856433049fe7264ad0ea4af7a
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2020
ms.locfileid: "83761898"
---
# <a name="dotnet-publish"></a><span data-ttu-id="12c41-103">dotnet publish</span><span class="sxs-lookup"><span data-stu-id="12c41-103">dotnet publish</span></span>

<span data-ttu-id="12c41-104">**本文適用于：** ✔️ .net CORE 2.1 SDK 和更新版本</span><span class="sxs-lookup"><span data-stu-id="12c41-104">**This article applies to:** ✔️ .NET Core 2.1 SDK and later versions</span></span>

## <a name="name"></a><span data-ttu-id="12c41-105">Name</span><span class="sxs-lookup"><span data-stu-id="12c41-105">Name</span></span>

<span data-ttu-id="12c41-106">`dotnet publish`-將應用程式及其相依性發佈至資料夾，以部署至主控系統。</span><span class="sxs-lookup"><span data-stu-id="12c41-106">`dotnet publish` - Publishes the application and its dependencies to a folder for deployment to a hosting system.</span></span>

## <a name="synopsis"></a><span data-ttu-id="12c41-107">概要</span><span class="sxs-lookup"><span data-stu-id="12c41-107">Synopsis</span></span>

```dotnetcli
dotnet publish [<PROJECT>|<SOLUTION>] [-c|--configuration <CONFIGURATION>]
    [-f|--framework <FRAMEWORK>] [--force] [--interactive]
    [--manifest <PATH_TO_MANIFEST_FILE>] [--no-build] [--no-dependencies]
    [--no-restore] [--nologo] [-o|--output <OUTPUT_DIRECTORY>]
    [-p:PublishReadyToRun=true] [-p:PublishSingleFile=true] [-p:PublishTrimmed=true]
    [-r|--runtime <RUNTIME_IDENTIFIER>] [--self-contained [true|false]]
    [--no-self-contained] [-v|--verbosity <LEVEL>]
    [--version-suffix <VERSION_SUFFIX>]

dotnet publish -h|--help
```

## <a name="description"></a><span data-ttu-id="12c41-108">Description</span><span class="sxs-lookup"><span data-stu-id="12c41-108">Description</span></span>

<span data-ttu-id="12c41-109">`dotnet publish` 會編譯應用程式，讀取在其專案檔中指定的相依性，然後將產生的一組檔案發行到目錄中。</span><span class="sxs-lookup"><span data-stu-id="12c41-109">`dotnet publish` compiles the application, reads through its dependencies specified in the project file, and publishes the resulting set of files to a directory.</span></span> <span data-ttu-id="12c41-110">此輸出包含下列資產：</span><span class="sxs-lookup"><span data-stu-id="12c41-110">The output includes the following assets:</span></span>

- <span data-ttu-id="12c41-111">組件中的中繼語言 (IL) 程式碼，副檔名為 *dll*。</span><span class="sxs-lookup"><span data-stu-id="12c41-111">Intermediate Language (IL) code in an assembly with a *dll* extension.</span></span>
- <span data-ttu-id="12c41-112">包含專案所有相依性的 *.deps.json json*檔案。</span><span class="sxs-lookup"><span data-stu-id="12c41-112">A *.deps.json* file that includes all of the dependencies of the project.</span></span>
- <span data-ttu-id="12c41-113">*.Runtimeconfig.json json*檔案，指定應用程式預期的共用執行時間，以及執行時間的其他設定選項（例如垃圾收集類型）。</span><span class="sxs-lookup"><span data-stu-id="12c41-113">A *.runtimeconfig.json* file that specifies the shared runtime that the application expects, as well as other configuration options for the runtime (for example, garbage collection type).</span></span>
- <span data-ttu-id="12c41-114">應用程式的相依性，這些相依性會從 NuGet 快取複製到輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="12c41-114">The application's dependencies, which are copied from the NuGet cache into the output folder.</span></span>

<span data-ttu-id="12c41-115">`dotnet publish`　命令的輸出已準備好部署到裝載系統 (例如伺服器、電腦、Mac、膝上型電腦) 以供執行。</span><span class="sxs-lookup"><span data-stu-id="12c41-115">The `dotnet publish` command's output is ready for deployment to a hosting system (for example, a server, PC, Mac, laptop) for execution.</span></span> <span data-ttu-id="12c41-116">這是準備應用程式以供部署的唯一正式支援的方法。</span><span class="sxs-lookup"><span data-stu-id="12c41-116">It's the only officially supported way to prepare the application for deployment.</span></span> <span data-ttu-id="12c41-117">根據專案指定的部署類型，主機系統上可能會安裝 (或不安裝) .NET Core 共用執行階段。</span><span class="sxs-lookup"><span data-stu-id="12c41-117">Depending on the type of deployment that the project specifies, the hosting system may or may not have the .NET Core shared runtime installed on it.</span></span> <span data-ttu-id="12c41-118">如需詳細資訊，請參閱[使用 .NET Core CLI 發佈 .Net Core 應用程式](../deploying/deploy-with-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="12c41-118">For more information, see [Publish .NET Core apps with the .NET Core CLI](../deploying/deploy-with-cli.md).</span></span>

### <a name="implicit-restore"></a><span data-ttu-id="12c41-119">隱含還原</span><span class="sxs-lookup"><span data-stu-id="12c41-119">Implicit restore</span></span>

[!INCLUDE[dotnet restore note](~/includes/dotnet-restore-note.md)]

### <a name="msbuild"></a><span data-ttu-id="12c41-120">MSBuild</span><span class="sxs-lookup"><span data-stu-id="12c41-120">MSBuild</span></span>

<span data-ttu-id="12c41-121">`dotnet publish` 命令會呼叫 MSBuild，這會叫用 `Publish` 目標。</span><span class="sxs-lookup"><span data-stu-id="12c41-121">The `dotnet publish` command calls MSBuild, which invokes the `Publish` target.</span></span> <span data-ttu-id="12c41-122">所有傳遞給 `dotnet publish` 的參數都會傳遞給 MSBuild。</span><span class="sxs-lookup"><span data-stu-id="12c41-122">Any parameters passed to `dotnet publish` are passed to MSBuild.</span></span> <span data-ttu-id="12c41-123">`-c` 和 `-o` 參數會分別對應至 MSBuild 的 `Configuration` 和 `OutputPath` 屬性。</span><span class="sxs-lookup"><span data-stu-id="12c41-123">The `-c` and `-o` parameters map to MSBuild's `Configuration` and `OutputPath` properties, respectively.</span></span>

<span data-ttu-id="12c41-124">此 `dotnet publish` 命令接受 MSBuild 選項，例如 `-p` 用於設定屬性和 `-l` 定義記錄器。</span><span class="sxs-lookup"><span data-stu-id="12c41-124">The `dotnet publish` command accepts MSBuild options, such as `-p` for setting properties and `-l` to define a logger.</span></span> <span data-ttu-id="12c41-125">例如，您可以使用下列格式來設定 MSBuild 屬性： `-p:<NAME>=<VALUE>` 。</span><span class="sxs-lookup"><span data-stu-id="12c41-125">For example, you can set an MSBuild property by using the format: `-p:<NAME>=<VALUE>`.</span></span> <span data-ttu-id="12c41-126">您也可以參考 *.pubxml*檔案來設定發行相關屬性，例如：</span><span class="sxs-lookup"><span data-stu-id="12c41-126">You can also set publish-related properties by referring to a *.pubxml* file, for example:</span></span>

```dotnetcli
dotnet publish -p:PublishProfile=Properties\PublishProfiles\FolderProfile.pubxml
```

<span data-ttu-id="12c41-127">如需詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="12c41-127">For more information, see the following resources:</span></span>

- [<span data-ttu-id="12c41-128">MSBuild 命令列參考</span><span class="sxs-lookup"><span data-stu-id="12c41-128">MSBuild command-line reference</span></span>](/visualstudio/msbuild/msbuild-command-line-reference)
- [<span data-ttu-id="12c41-129">Visual Studio ASP.NET Core 應用程式部署的發行設定檔（. .pubxml）</span><span class="sxs-lookup"><span data-stu-id="12c41-129">Visual Studio publish profiles (.pubxml) for ASP.NET Core app deployment</span></span>](/aspnet/core/host-and-deploy/visual-studio-publish-profiles)
- [<span data-ttu-id="12c41-130">dotnet msbuild</span><span class="sxs-lookup"><span data-stu-id="12c41-130">dotnet msbuild</span></span>](dotnet-msbuild.md)

## <a name="arguments"></a><span data-ttu-id="12c41-131">引數</span><span class="sxs-lookup"><span data-stu-id="12c41-131">Arguments</span></span>

- **`PROJECT|SOLUTION`**

  <span data-ttu-id="12c41-132">要發行的專案或方案。</span><span class="sxs-lookup"><span data-stu-id="12c41-132">The project or solution to publish.</span></span>
  
  * <span data-ttu-id="12c41-133">`PROJECT`是[c #](csproj.md)、f # 或 Visual Basic 專案檔的路徑和檔案名，或是包含 c #、f # 或 Visual Basic 專案檔之目錄的路徑。</span><span class="sxs-lookup"><span data-stu-id="12c41-133">`PROJECT` is the path and filename of a [C#](csproj.md), F#, or Visual Basic project file, or the path to a directory that contains a C#, F#, or Visual Basic project file.</span></span> <span data-ttu-id="12c41-134">如果未指定目錄，則會預設為目前目錄。</span><span class="sxs-lookup"><span data-stu-id="12c41-134">If the directory is not specified, it defaults to the current directory.</span></span>

  * <span data-ttu-id="12c41-135">`SOLUTION`是方案檔（*.sln*副檔名）的路徑和檔案名，或包含方案檔之目錄的路徑。</span><span class="sxs-lookup"><span data-stu-id="12c41-135">`SOLUTION` is the path and filename of a solution file (*.sln* extension), or the path to a directory that contains a solution file.</span></span> <span data-ttu-id="12c41-136">如果未指定目錄，則會預設為目前目錄。</span><span class="sxs-lookup"><span data-stu-id="12c41-136">If the directory is not specified, it defaults to the current directory.</span></span> <span data-ttu-id="12c41-137">自 .NET Core 3.0 SDK 起提供。</span><span class="sxs-lookup"><span data-stu-id="12c41-137">Available since .NET Core 3.0 SDK.</span></span>

## <a name="options"></a><span data-ttu-id="12c41-138">選項</span><span class="sxs-lookup"><span data-stu-id="12c41-138">Options</span></span>

- **`-c|--configuration <CONFIGURATION>`**

  <span data-ttu-id="12c41-139">定義組建組態。</span><span class="sxs-lookup"><span data-stu-id="12c41-139">Defines the build configuration.</span></span> <span data-ttu-id="12c41-140">大部分專案的預設值為 `Debug` ，但您可以覆寫專案中的組建設定。</span><span class="sxs-lookup"><span data-stu-id="12c41-140">The default for most projects is `Debug`, but you can override the build configuration settings in your project.</span></span>

- **`-f|--framework <FRAMEWORK>`**

  <span data-ttu-id="12c41-141">發行所指定[目標架構](../../standard/frameworks.md)的應用程式。</span><span class="sxs-lookup"><span data-stu-id="12c41-141">Publishes the application for the specified [target framework](../../standard/frameworks.md).</span></span> <span data-ttu-id="12c41-142">您必須在專案檔中指定此目標架構。</span><span class="sxs-lookup"><span data-stu-id="12c41-142">You must specify the target framework in the project file.</span></span>

- **`--force`**

  <span data-ttu-id="12c41-143">即使最後的還原成功，仍強制解析所有相依性。</span><span class="sxs-lookup"><span data-stu-id="12c41-143">Forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="12c41-144">指定這個旗標等同於刪除 *project.assets.json* 檔案。</span><span class="sxs-lookup"><span data-stu-id="12c41-144">Specifying this flag is the same as deleting the *project.assets.json* file.</span></span>

- **`-h|--help`**

  <span data-ttu-id="12c41-145">印出命令的簡短說明。</span><span class="sxs-lookup"><span data-stu-id="12c41-145">Prints out a short help for the command.</span></span>

- **`--interactive`**

  <span data-ttu-id="12c41-146">可讓命令停止，並等候使用者輸入或進行動作。</span><span class="sxs-lookup"><span data-stu-id="12c41-146">Allows the command to stop and wait for user input or action.</span></span> <span data-ttu-id="12c41-147">例如完成驗證。</span><span class="sxs-lookup"><span data-stu-id="12c41-147">For example, to complete authentication.</span></span> <span data-ttu-id="12c41-148">自 .NET Core 3.0 SDK 起提供。</span><span class="sxs-lookup"><span data-stu-id="12c41-148">Available since .NET Core 3.0 SDK.</span></span>

- **`--manifest <PATH_TO_MANIFEST_FILE>`**

  <span data-ttu-id="12c41-149">指定一或多個[目標資訊清單](../deploying/runtime-store.md)，用以修剪應用程式發行的套件集。</span><span class="sxs-lookup"><span data-stu-id="12c41-149">Specifies one or several [target manifests](../deploying/runtime-store.md) to use to trim the set of packages published with the app.</span></span> <span data-ttu-id="12c41-150">資訊清單檔案是[ `dotnet store` 命令](dotnet-store.md)輸出的一部分。</span><span class="sxs-lookup"><span data-stu-id="12c41-150">The manifest file is part of the output of the [`dotnet store` command](dotnet-store.md).</span></span> <span data-ttu-id="12c41-151">若要指定多個資訊清單，請為每個資訊清單新增 `--manifest` 選項。</span><span class="sxs-lookup"><span data-stu-id="12c41-151">To specify multiple manifests, add a `--manifest` option for each manifest.</span></span>

- **`--no-build`**

  <span data-ttu-id="12c41-152">不會在發佈前建置專案。</span><span class="sxs-lookup"><span data-stu-id="12c41-152">Doesn't build the project before publishing.</span></span> <span data-ttu-id="12c41-153">選項也會隱含設定 `--no-restore` 旗標。</span><span class="sxs-lookup"><span data-stu-id="12c41-153">It also implicitly sets the `--no-restore` flag.</span></span>

- **`--no-dependencies`**

  <span data-ttu-id="12c41-154">忽略專案對專案參考，並且只還原根專案。</span><span class="sxs-lookup"><span data-stu-id="12c41-154">Ignores project-to-project references and only restores the root project.</span></span>

- **`--nologo`**

  <span data-ttu-id="12c41-155">不要顯示程式啟始橫幅或著作權訊息。</span><span class="sxs-lookup"><span data-stu-id="12c41-155">Doesn't display the startup banner or the copyright message.</span></span> <span data-ttu-id="12c41-156">自 .NET Core 3.0 SDK 起提供。</span><span class="sxs-lookup"><span data-stu-id="12c41-156">Available since .NET Core 3.0 SDK.</span></span>

- **`--no-restore`**

  <span data-ttu-id="12c41-157">執行命令時，不會執行隱含還原。</span><span class="sxs-lookup"><span data-stu-id="12c41-157">Doesn't execute an implicit restore when running the command.</span></span>

- **`-o|--output <OUTPUT_DIRECTORY>`**

  <span data-ttu-id="12c41-158">指定輸出目錄的路徑。</span><span class="sxs-lookup"><span data-stu-id="12c41-158">Specifies the path for the output directory.</span></span>
  
  <span data-ttu-id="12c41-159">如果未指定，則預設為 *[project_file_folder]./bin/[configuration]/[framework]/publish/(適用*，適用于執行時間相依的可執行檔和跨平臺二進位檔。</span><span class="sxs-lookup"><span data-stu-id="12c41-159">If not specified, it defaults to *[project_file_folder]./bin/[configuration]/[framework]/publish/* for a runtime-dependent executable and cross-platform binaries.</span></span> <span data-ttu-id="12c41-160">針對獨立可執行檔，其預設為 *[project_file_folder]/bin/[configuration]/[framework]/[runtime]/publish/(適用*。</span><span class="sxs-lookup"><span data-stu-id="12c41-160">It defaults to *[project_file_folder]/bin/[configuration]/[framework]/[runtime]/publish/* for a self-contained executable.</span></span>

  <span data-ttu-id="12c41-161">在 Web 專案中，如果輸出檔案夾位於專案資料夾中，後續 `dotnet publish` 的命令會產生嵌套的輸出檔案夾。</span><span class="sxs-lookup"><span data-stu-id="12c41-161">In a web project, if the output folder is in the project folder, successive `dotnet publish` commands result in nested output folders.</span></span> <span data-ttu-id="12c41-162">例如，如果專案資料夾是*myproject*，且發行輸出檔案夾為*myproject/publish*，而您執行了 `dotnet publish` 兩次，則第二個執行會將內容檔案（例如 *.config*和*json*檔案）放在*myproject/publish/publish*中。</span><span class="sxs-lookup"><span data-stu-id="12c41-162">For example, if the project folder is *myproject*, and the publish output folder is *myproject/publish*, and you run `dotnet publish` twice, the second run puts content files such as *.config* and *.json* files in *myproject/publish/publish*.</span></span> <span data-ttu-id="12c41-163">若要避免建立發行資料夾的嵌套，請指定不是**直接**在專案資料夾底下的 publish 資料夾，或是從專案中排除 publish 資料夾。</span><span class="sxs-lookup"><span data-stu-id="12c41-163">To avoid nesting publish folders, specify a publish folder that is not **directly** under the project folder, or exclude the publish folder from the project.</span></span> <span data-ttu-id="12c41-164">若要排除名為*publishoutput*的發行資料夾，請將下列元素新增至 `PropertyGroup` *.csproj*檔案中的專案：</span><span class="sxs-lookup"><span data-stu-id="12c41-164">To exclude a publish folder named *publishoutput*, add the following element to a `PropertyGroup` element in the *.csproj* file:</span></span>

  ```xml
  <DefaultItemExcludes>$(DefaultItemExcludes);publishoutput**</DefaultItemExcludes>
  ```

  - <span data-ttu-id="12c41-165">.NET Core 3.x SDK 和更新版本</span><span class="sxs-lookup"><span data-stu-id="12c41-165">.NET Core 3.x SDK and later</span></span>
  
    <span data-ttu-id="12c41-166">如果在發行專案時指定相對路徑，則產生的輸出目錄會相對於目前的工作目錄，而不是專案檔位置。</span><span class="sxs-lookup"><span data-stu-id="12c41-166">If a relative path is specified when publishing a project, the output directory generated is relative to the current working directory, not to the project file location.</span></span>

    <span data-ttu-id="12c41-167">如果在發行方案時指定相對路徑，所有專案的所有輸出都會進入相對於目前工作目錄的指定資料夾。</span><span class="sxs-lookup"><span data-stu-id="12c41-167">If a relative path is specified when publishing a solution, all output for all projects goes into the specified folder relative to the current working directory.</span></span> <span data-ttu-id="12c41-168">若要讓 [發行輸出] 移至每個專案的個別資料夾，請使用 msbuild `PublishDir` 屬性（而非選項）來指定相對路徑 `--output` 。</span><span class="sxs-lookup"><span data-stu-id="12c41-168">To make publish output go to separate folders for each project, specify a relative path by using the msbuild `PublishDir` property instead of the `--output` option.</span></span> <span data-ttu-id="12c41-169">例如， `dotnet publish -p:PublishDir=.\publish` 會將每個專案的發行輸出傳送至 `publish` 包含專案檔之資料夾下的資料夾。</span><span class="sxs-lookup"><span data-stu-id="12c41-169">For example, `dotnet publish -p:PublishDir=.\publish` sends publish output for each project to a `publish` folder under the folder that contains the project file.</span></span>

  - <span data-ttu-id="12c41-170">.NET Core 2.x SDK</span><span class="sxs-lookup"><span data-stu-id="12c41-170">.NET Core 2.x SDK</span></span>
  
    <span data-ttu-id="12c41-171">如果在發行專案時指定相對路徑，則產生的輸出目錄會相對於專案檔案位置，而不是目前的工作目錄。</span><span class="sxs-lookup"><span data-stu-id="12c41-171">If a relative path is specified when publishing a project, the output directory generated is relative to the project file location, not to the current working directory.</span></span>

    <span data-ttu-id="12c41-172">如果在發行方案時指定相對路徑，則每個專案的輸出都會進入與專案檔位置相對的個別資料夾。</span><span class="sxs-lookup"><span data-stu-id="12c41-172">If a relative path is specified when publishing a solution, each project's output goes into a separate folder relative to the project file location.</span></span> <span data-ttu-id="12c41-173">如果在發行方案時指定了絕對路徑，所有專案的所有發行輸出都會進入指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="12c41-173">If an absolute path is specified when publishing a solution, all publish output for all projects goes into the specified folder.</span></span>

- **`-p:PublishReadyToRun=true`**

  <span data-ttu-id="12c41-174">將應用程式元件編譯為 ReadyToRun （R2R）格式。</span><span class="sxs-lookup"><span data-stu-id="12c41-174">Compiles application assemblies as ReadyToRun (R2R) format.</span></span> <span data-ttu-id="12c41-175">R2R 是一種預先(AOT) 編譯。</span><span class="sxs-lookup"><span data-stu-id="12c41-175">R2R is a form of ahead-of-time (AOT) compilation.</span></span> <span data-ttu-id="12c41-176">如需詳細資訊，請參閱[ReadyToRun images](../whats-new/dotnet-core-3-0.md#readytorun-images)。</span><span class="sxs-lookup"><span data-stu-id="12c41-176">For more information, see [ReadyToRun images](../whats-new/dotnet-core-3-0.md#readytorun-images).</span></span> <span data-ttu-id="12c41-177">自 .NET Core 3.0 SDK 起提供。</span><span class="sxs-lookup"><span data-stu-id="12c41-177">Available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="12c41-178">我們建議您在發行設定檔中指定這個選項，而不是在命令列上。</span><span class="sxs-lookup"><span data-stu-id="12c41-178">We recommend that you specify this option in a publish profile rather than on the command line.</span></span> <span data-ttu-id="12c41-179">如需詳細資訊，請參閱[MSBuild](#msbuild)。</span><span class="sxs-lookup"><span data-stu-id="12c41-179">For more information, see [MSBuild](#msbuild).</span></span>

- **`-p:PublishSingleFile=true`**

  <span data-ttu-id="12c41-180">將應用程式封裝成平臺特定的單一檔案可執行檔。</span><span class="sxs-lookup"><span data-stu-id="12c41-180">Packages the app into a platform-specific single-file executable.</span></span> <span data-ttu-id="12c41-181">可執行檔會自我解壓縮，並包含執行應用程式所需的所有相依性（包括原生）。</span><span class="sxs-lookup"><span data-stu-id="12c41-181">The executable is self-extracting and contains all dependencies (including native) that are required to run the app.</span></span> <span data-ttu-id="12c41-182">第一次執行應用程式時，系統會將應用程式解壓縮到以應用程式名稱和組建識別碼為基礎的目錄。</span><span class="sxs-lookup"><span data-stu-id="12c41-182">When the app is first run, the application is extracted to a directory based on the app name and build identifier.</span></span> <span data-ttu-id="12c41-183">再次執行應用程式時的啟動速度會更快。</span><span class="sxs-lookup"><span data-stu-id="12c41-183">Startup is faster when the application is run again.</span></span> <span data-ttu-id="12c41-184">除非使用新版本，否則應用程式不需要第二次解壓縮。</span><span class="sxs-lookup"><span data-stu-id="12c41-184">The application doesn't need to extract itself a second time unless a new version is used.</span></span> <span data-ttu-id="12c41-185">自 .NET Core 3.0 SDK 起提供。</span><span class="sxs-lookup"><span data-stu-id="12c41-185">Available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="12c41-186">如需單一檔案發佈的詳細資訊，請參閱[單一檔案搭配程式設計文件](https://github.com/dotnet/designs/blob/master/accepted/2020/single-file/design.md)。</span><span class="sxs-lookup"><span data-stu-id="12c41-186">For more information about single-file publishing, see the [single-file bundler design document](https://github.com/dotnet/designs/blob/master/accepted/2020/single-file/design.md).</span></span>

  <span data-ttu-id="12c41-187">我們建議您在發行設定檔中指定這個選項，而不是在命令列上。</span><span class="sxs-lookup"><span data-stu-id="12c41-187">We recommend that you specify this option in a publish profile rather than on the command line.</span></span> <span data-ttu-id="12c41-188">如需詳細資訊，請參閱[MSBuild](#msbuild)。</span><span class="sxs-lookup"><span data-stu-id="12c41-188">For more information, see [MSBuild](#msbuild).</span></span>

- **`-p:PublishTrimmed=true`**

  <span data-ttu-id="12c41-189">在發行獨立的可執行檔時，修剪未使用的程式庫，以減少應用程式的部署大小。</span><span class="sxs-lookup"><span data-stu-id="12c41-189">Trims unused libraries to reduce the deployment size of an app when publishing a self-contained executable.</span></span> <span data-ttu-id="12c41-190">如需詳細資訊，請參閱[修剪獨立部署和可執行檔](../deploying/trim-self-contained.md)。</span><span class="sxs-lookup"><span data-stu-id="12c41-190">For more information, see [Trim self-contained deployments and executables](../deploying/trim-self-contained.md).</span></span> <span data-ttu-id="12c41-191">自 .NET Core 3.0 SDK 起提供。</span><span class="sxs-lookup"><span data-stu-id="12c41-191">Available since .NET Core 3.0 SDK.</span></span>

  <span data-ttu-id="12c41-192">我們建議您在發行設定檔中指定這個選項，而不是在命令列上。</span><span class="sxs-lookup"><span data-stu-id="12c41-192">We recommend that you specify this option in a publish profile rather than on the command line.</span></span> <span data-ttu-id="12c41-193">如需詳細資訊，請參閱[MSBuild](#msbuild)。</span><span class="sxs-lookup"><span data-stu-id="12c41-193">For more information, see [MSBuild](#msbuild).</span></span>

- **`--self-contained [true|false]`**

  <span data-ttu-id="12c41-194">使用您的應用程式發行 .NET Core 執行階段，讓目標電腦不需要安裝執行階段。</span><span class="sxs-lookup"><span data-stu-id="12c41-194">Publishes the .NET Core runtime with your application so the runtime doesn't need to be installed on the target machine.</span></span> <span data-ttu-id="12c41-195">如果已 `true` 指定執行時間識別碼，而且專案是可執行檔專案（而不是程式庫專案），則預設值為。</span><span class="sxs-lookup"><span data-stu-id="12c41-195">Default is `true` if a runtime identifier is specified and the project is an executable project (not a library project).</span></span> <span data-ttu-id="12c41-196">如需詳細資訊，請參閱[.Net core 應用程式](../deploying/index.md)[使用 .NET Core CLI 發佈和發行 .net core](../deploying/deploy-with-cli.md)應用程式。</span><span class="sxs-lookup"><span data-stu-id="12c41-196">For more information, see [.NET Core application publishing](../deploying/index.md) and [Publish .NET Core apps with the .NET Core CLI](../deploying/deploy-with-cli.md).</span></span>

  <span data-ttu-id="12c41-197">如果在不指定或的情況下使用此選項 `true` `false` ，則預設值為 `true` 。</span><span class="sxs-lookup"><span data-stu-id="12c41-197">If this option is used without specifying `true` or `false`, the default is `true`.</span></span> <span data-ttu-id="12c41-198">在此情況下，請不要在之後立即放置方案或專案引數 `--self-contained` ，因為 `true` `false` 在該位置中必須有或。</span><span class="sxs-lookup"><span data-stu-id="12c41-198">In that case, don't put the solution or project argument immediately after `--self-contained`, because `true` or `false` is expected in that position.</span></span>

- **`--no-self-contained`**

  <span data-ttu-id="12c41-199">相當於 `--self-contained false`。</span><span class="sxs-lookup"><span data-stu-id="12c41-199">Equivalent to `--self-contained false`.</span></span> <span data-ttu-id="12c41-200">自 .NET Core 3.0 SDK 起提供。</span><span class="sxs-lookup"><span data-stu-id="12c41-200">Available since .NET Core 3.0 SDK.</span></span>

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  <span data-ttu-id="12c41-201">發行所指定執行階段的應用程式。</span><span class="sxs-lookup"><span data-stu-id="12c41-201">Publishes the application for a given runtime.</span></span> <span data-ttu-id="12c41-202">如需執行階段識別項 (RID) 清單，請參閱 [RID 目錄](../rid-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="12c41-202">For a list of Runtime Identifiers (RIDs), see the [RID catalog](../rid-catalog.md).</span></span> <span data-ttu-id="12c41-203">如需詳細資訊，請參閱[.Net core 應用程式](../deploying/index.md)[使用 .NET Core CLI 發佈和發行 .net core](../deploying/deploy-with-cli.md)應用程式。</span><span class="sxs-lookup"><span data-stu-id="12c41-203">For more information, see [.NET Core application publishing](../deploying/index.md) and [Publish .NET Core apps with the .NET Core CLI](../deploying/deploy-with-cli.md).</span></span>

- **`-v|--verbosity <LEVEL>`**

  <span data-ttu-id="12c41-204">設定命令的詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="12c41-204">Sets the verbosity level of the command.</span></span> <span data-ttu-id="12c41-205">允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="12c41-205">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="12c41-206">預設值為 `minimal`。</span><span class="sxs-lookup"><span data-stu-id="12c41-206">Default value is `minimal`.</span></span>

- **`--version-suffix <VERSION_SUFFIX>`**

  <span data-ttu-id="12c41-207">定義要取代專案檔案的版本欄位中之星號 (`*`) 的版本尾碼。</span><span class="sxs-lookup"><span data-stu-id="12c41-207">Defines the version suffix to replace the asterisk (`*`) in the version field of the project file.</span></span>

## <a name="examples"></a><span data-ttu-id="12c41-208">範例</span><span class="sxs-lookup"><span data-stu-id="12c41-208">Examples</span></span>

- <span data-ttu-id="12c41-209">針對目前目錄中的專案建立[執行時間相依的跨平臺二進位](../deploying/index.md#produce-a-cross-platform-binary)檔：</span><span class="sxs-lookup"><span data-stu-id="12c41-209">Create a [runtime-dependent cross-platform binary](../deploying/index.md#produce-a-cross-platform-binary) for the project in the current directory:</span></span>

  ```dotnetcli
  dotnet publish
  ```

  <span data-ttu-id="12c41-210">從 .NET Core 3.0 SDK 開始，此範例也會建立目前平臺的[執行時間相依可執行檔](../deploying/index.md#publish-runtime-dependent)。</span><span class="sxs-lookup"><span data-stu-id="12c41-210">Starting with .NET Core 3.0 SDK, this example also creates a [runtime-dependent executable](../deploying/index.md#publish-runtime-dependent) for the current platform.</span></span>

- <span data-ttu-id="12c41-211">針對特定執行時間，為目前目錄中的專案建立[獨立可執行檔](../deploying/index.md#publish-self-contained)：</span><span class="sxs-lookup"><span data-stu-id="12c41-211">Create a [self-contained executable](../deploying/index.md#publish-self-contained) for the project in the current directory, for a specific runtime:</span></span>

  ```dotnetcli
  dotnet publish --runtime osx.10.11-x64
  ```

  <span data-ttu-id="12c41-212">RID 必須在專案檔中。</span><span class="sxs-lookup"><span data-stu-id="12c41-212">The RID must be in the project file.</span></span>

- <span data-ttu-id="12c41-213">針對特定平臺，為目前目錄中的專案建立[執行時間相依的可執行檔](../deploying/index.md#publish-runtime-dependent)：</span><span class="sxs-lookup"><span data-stu-id="12c41-213">Create a [runtime-dependent executable](../deploying/index.md#publish-runtime-dependent) for the project in the current directory, for a specific platform:</span></span>

  ```dotnetcli
  dotnet publish --runtime osx.10.11-x64 --self-contained false
  ```

  <span data-ttu-id="12c41-214">RID 必須在專案檔中。</span><span class="sxs-lookup"><span data-stu-id="12c41-214">The RID must be in the project file.</span></span> <span data-ttu-id="12c41-215">這個範例適用于 .NET Core 3.0 SDK 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="12c41-215">This example applies to .NET Core 3.0 SDK and later versions.</span></span>

- <span data-ttu-id="12c41-216">針對特定的執行時間和目標架構，在目前目錄中發佈專案：</span><span class="sxs-lookup"><span data-stu-id="12c41-216">Publish the project in the current directory, for a specific runtime and target framework:</span></span>

  ```dotnetcli
  dotnet publish --framework netcoreapp3.1 --runtime osx.10.11-x64
  ```

- <span data-ttu-id="12c41-217">發行指定的專案檔：</span><span class="sxs-lookup"><span data-stu-id="12c41-217">Publish the specified project file:</span></span>

  ```dotnetcli
  dotnet publish ~/projects/app1/app1.csproj
  ```

- <span data-ttu-id="12c41-218">發行目前的應用程式，但不要在還原作業期間還原專案對專案（P2P）參考，只有根專案：</span><span class="sxs-lookup"><span data-stu-id="12c41-218">Publish the current application but don't restore project-to-project (P2P) references, just the root project during the restore operation:</span></span>

  ```dotnetcli
  dotnet publish --no-dependencies
  ```

## <a name="see-also"></a><span data-ttu-id="12c41-219">另請參閱</span><span class="sxs-lookup"><span data-stu-id="12c41-219">See also</span></span>

- [<span data-ttu-id="12c41-220">.NET Core 應用程式發行總覽</span><span class="sxs-lookup"><span data-stu-id="12c41-220">.NET Core application publishing overview</span></span>](../deploying/index.md)
- [<span data-ttu-id="12c41-221">使用 .NET Core CLI 發佈 .NET Core 應用程式</span><span class="sxs-lookup"><span data-stu-id="12c41-221">Publish .NET Core apps with the .NET Core CLI</span></span>](../deploying/deploy-with-cli.md)
- [<span data-ttu-id="12c41-222">目標 Framework</span><span class="sxs-lookup"><span data-stu-id="12c41-222">Target frameworks</span></span>](../../standard/frameworks.md)
- [<span data-ttu-id="12c41-223">執行時間識別碼（RID）目錄</span><span class="sxs-lookup"><span data-stu-id="12c41-223">Runtime IDentifier (RID) catalog</span></span>](../rid-catalog.md)
- [<span data-ttu-id="12c41-224">使用 macOS Catalina Notarization</span><span class="sxs-lookup"><span data-stu-id="12c41-224">Working with macOS Catalina Notarization</span></span>](../install/macos-notarization-issues.md)
- [<span data-ttu-id="12c41-225">已發行應用程式的目錄結構</span><span class="sxs-lookup"><span data-stu-id="12c41-225">Directory structure of a published application</span></span>](/aspnet/core/hosting/directory-structure)
- [<span data-ttu-id="12c41-226">MSBuild 命令列參考</span><span class="sxs-lookup"><span data-stu-id="12c41-226">MSBuild command-line reference</span></span>](/visualstudio/msbuild/msbuild-command-line-reference)
- [<span data-ttu-id="12c41-227">Visual Studio ASP.NET Core 應用程式部署的發行設定檔（. .pubxml）</span><span class="sxs-lookup"><span data-stu-id="12c41-227">Visual Studio publish profiles (.pubxml) for ASP.NET Core app deployment</span></span>](/aspnet/core/host-and-deploy/visual-studio-publish-profiles)
- [<span data-ttu-id="12c41-228">dotnet msbuild</span><span class="sxs-lookup"><span data-stu-id="12c41-228">dotnet msbuild</span></span>](dotnet-msbuild.md)
- [<span data-ttu-id="12c41-229">ILLInk。工作</span><span class="sxs-lookup"><span data-stu-id="12c41-229">ILLInk.Tasks</span></span>](https://aka.ms/dotnet-illink)
