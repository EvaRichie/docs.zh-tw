---
title: 卸載工具
description: 概述 .NET Core 卸載工具，這是一個引導式工具，可讓您控制 .NET Core Sdk 和執行時間的清理。
author: sfoslund
ms.date: 05/27/2020
ms.openlocfilehash: dcfa12a3ec5fe0e8a29c5897ee4c71bfc7352eda
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84590795"
---
# <a name="net-core-uninstall-tool"></a><span data-ttu-id="07349-103">.NET Core 解除安裝工具</span><span class="sxs-lookup"><span data-stu-id="07349-103">.NET Core Uninstall Tool</span></span>

<span data-ttu-id="07349-104">[.Net Core 卸載工具](https://aka.ms/dotnet-core-uninstall-tool)（ `dotnet-core-uninstall` ）可讓您從系統中移除 .net Core sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-104">The [.NET Core Uninstall Tool](https://aka.ms/dotnet-core-uninstall-tool) (`dotnet-core-uninstall`) lets you remove .NET Core SDKs and Runtimes from a system.</span></span> <span data-ttu-id="07349-105">有一組選項可用來指定您要卸載的版本。</span><span class="sxs-lookup"><span data-stu-id="07349-105">A collection of options is available to specify which versions you want to uninstall.</span></span>

<span data-ttu-id="07349-106">此工具支援 Windows 和 macOS。</span><span class="sxs-lookup"><span data-stu-id="07349-106">The tool supports Windows and macOS.</span></span> <span data-ttu-id="07349-107">目前不支援 Linux。</span><span class="sxs-lookup"><span data-stu-id="07349-107">Linux is currently not supported.</span></span>

<span data-ttu-id="07349-108">在 Windows 上，此工具只能使用下列其中一個安裝程式來卸載已安裝的 Sdk 和執行時間：</span><span class="sxs-lookup"><span data-stu-id="07349-108">On Windows, the tool can only uninstall SDKs and Runtimes that were installed using one of the following installers:</span></span>

- <span data-ttu-id="07349-109">.NET Core SDK 和執行時間安裝程式。</span><span class="sxs-lookup"><span data-stu-id="07349-109">The .NET Core SDK and runtime installer.</span></span>
- <span data-ttu-id="07349-110">Visual Studio 安裝程式的版本早于 Visual Studio 2019 16.3 版。</span><span class="sxs-lookup"><span data-stu-id="07349-110">The Visual Studio installer in versions earlier than Visual Studio 2019 version 16.3.</span></span>

<span data-ttu-id="07349-111">在 macOS 上，此工具只能卸載位於 */usr/local/share/dotnet*資料夾中的 sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-111">On macOS, the tool can only uninstall SDKs and runtimes located in the */usr/local/share/dotnet* folder.</span></span>

<span data-ttu-id="07349-112">基於這些限制，此工具可能無法卸載您電腦上的所有 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-112">Because of these limitations, the tool may not be able to uninstall all of the .NET Core SDKs and runtimes on your machine.</span></span> <span data-ttu-id="07349-113">您可以使用 `dotnet --info` 命令來尋找已安裝的所有 .Net Core sdk 和執行時間，包括此工具無法移除的 sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-113">You can use the `dotnet --info` command to find all of the .NET Core SDKs and runtimes installed, including those SDKs and runtimes that this tool can't remove.</span></span> <span data-ttu-id="07349-114">`dotnet-core-uninstall list`命令會顯示哪些 sdk 可以使用工具卸載。</span><span class="sxs-lookup"><span data-stu-id="07349-114">The `dotnet-core-uninstall list` command displays which SDKs can be uninstalled with the tool.</span></span>

## <a name="install-the-tool"></a><span data-ttu-id="07349-115">安裝工具</span><span class="sxs-lookup"><span data-stu-id="07349-115">Install the tool</span></span>

<span data-ttu-id="07349-116">您可以從[工具的 [版本] 頁面](https://aka.ms/dotnet-core-uninstall-tool)下載 .Net Core 卸載工具，並在[dotnet/cli-實驗室](https://github.com/dotnet/cli-lab)GitHub 存放庫中尋找原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="07349-116">You can download the .NET Core Uninstall Tool from [the tool's releases page](https://aka.ms/dotnet-core-uninstall-tool) and find the source code at the [dotnet/cli-lab](https://github.com/dotnet/cli-lab) GitHub repository.</span></span>

> [!NOTE]
> <span data-ttu-id="07349-117">此工具需要提高許可權，才能卸載 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-117">The tool requires elevation to uninstall .NET Core SDKs and runtimes.</span></span> <span data-ttu-id="07349-118">因此，它應該安裝在受寫入保護的目錄中，例如 Windows 上的*C:\Program*檔案或 macOS 上的 */usr/local/bin* 。</span><span class="sxs-lookup"><span data-stu-id="07349-118">Therefore, it should be installed in a write-protected directory such as *C:\Program Files* on Windows or */usr/local/bin* on macOS.</span></span> <span data-ttu-id="07349-119">另請參閱[dotnet 命令的更高存取權](../tools/elevated-access.md)。</span><span class="sxs-lookup"><span data-stu-id="07349-119">See also [Elevated access for dotnet commands](../tools/elevated-access.md).</span></span> <span data-ttu-id="07349-120">如需詳細資訊，請參閱[詳細的安裝指示](https://aka.ms/dotnet-core-uninstall-tool)。</span><span class="sxs-lookup"><span data-stu-id="07349-120">For more information, see the [detailed installation instructions](https://aka.ms/dotnet-core-uninstall-tool).</span></span>

## <a name="run-the-tool"></a><span data-ttu-id="07349-121">執行工具</span><span class="sxs-lookup"><span data-stu-id="07349-121">Run the tool</span></span>

<span data-ttu-id="07349-122">下列步驟顯示執行卸載工具的建議方法：</span><span class="sxs-lookup"><span data-stu-id="07349-122">The following steps show the recommended approach for running the uninstall tool:</span></span>

- [<span data-ttu-id="07349-123">步驟 1-顯示已安裝的 .NET Core Sdk 和執行時間</span><span class="sxs-lookup"><span data-stu-id="07349-123">Step 1 - Display installed .NET Core SDKs and runtimes</span></span>](#step-1---display-installed-net-core-sdks-and-runtimes)
- [<span data-ttu-id="07349-124">步驟 2-進行試執行</span><span class="sxs-lookup"><span data-stu-id="07349-124">Step 2 - Do a dry run</span></span>](#step-2---do-a-dry-run)
- [<span data-ttu-id="07349-125">步驟 3-卸載 .NET Core Sdk 和執行時間</span><span class="sxs-lookup"><span data-stu-id="07349-125">Step 3 - Uninstall .NET Core SDKs and Runtimes</span></span>](#step-3---uninstall-net-core-sdks-and-runtimes)
- [<span data-ttu-id="07349-126">步驟 4-刪除 NuGet fallback 資料夾（選擇性）</span><span class="sxs-lookup"><span data-stu-id="07349-126">Step 4 - Delete the NuGet fallback folder (optional)</span></span>](#step-4---delete-the-nuget-fallback-folder-optional)

### <a name="step-1---display-installed-net-core-sdks-and-runtimes"></a><span data-ttu-id="07349-127">步驟 1-顯示已安裝的 .NET Core Sdk 和執行時間</span><span class="sxs-lookup"><span data-stu-id="07349-127">Step 1 - Display installed .NET Core SDKs and runtimes</span></span>

<span data-ttu-id="07349-128">此 `dotnet-core-uninstall list` 命令會列出已安裝的 .Net Core sdk 和可使用此工具移除的執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-128">The `dotnet-core-uninstall list` command lists the installed .NET Core SDKs and runtimes that can be removed with this tool.</span></span> <span data-ttu-id="07349-129">Visual Studio 可能需要一些 Sdk 和執行時間，而且會顯示不建議將它們卸載的原因。</span><span class="sxs-lookup"><span data-stu-id="07349-129">Some SDKs and runtimes may be required by Visual Studio and they're displayed with a note of why it isn't recommended to uninstall them.</span></span>

> [!NOTE]
> <span data-ttu-id="07349-130">`dotnet-core-uninstall list`在大部分情況下，命令的輸出不會符合輸出中已安裝的版本清單 `dotnet --info` 。</span><span class="sxs-lookup"><span data-stu-id="07349-130">The output of the `dotnet-core-uninstall list` command will not match the list of installed versions in the output of `dotnet --info` in most cases.</span></span> <span data-ttu-id="07349-131">具體而言，此工具不會顯示 zip 檔案所安裝或受 Visual Studio 管理的版本（任何以 Visual Studio 2019 16.3 或更新版本安裝的版本）。</span><span class="sxs-lookup"><span data-stu-id="07349-131">Specifically, this tool will not display versions installed by zip files or managed by Visual Studio (any version installed with Visual Studio 2019 16.3 or later).</span></span> <span data-ttu-id="07349-132">檢查版本是否由 Visual Studio 管理的其中一種方式是在中加以查看 `Add or Remove Programs` ，其中 Visual Studio 的受控版本會在其顯示名稱中標示為。</span><span class="sxs-lookup"><span data-stu-id="07349-132">One way to check if a version is managed by Visual Studio is to view it in `Add or Remove Programs`, where Visual Studio managed versions are marked as such in their display names.</span></span>

<span data-ttu-id="07349-133">**dotnet-核心-卸載清單**</span><span class="sxs-lookup"><span data-stu-id="07349-133">**dotnet-core-uninstall list**</span></span>

#### <a name="synopsis"></a><span data-ttu-id="07349-134">概要</span><span class="sxs-lookup"><span data-stu-id="07349-134">Synopsis</span></span>

```console
dotnet-core-uninstall list [options]
```

#### <a name="options"></a><span data-ttu-id="07349-135">選項</span><span class="sxs-lookup"><span data-stu-id="07349-135">Options</span></span>

## <a name="windows"></a>[<span data-ttu-id="07349-136">Windows</span><span class="sxs-lookup"><span data-stu-id="07349-136">Windows</span></span>](#tab/windows)

* **`--aspnet-runtime`**

  <span data-ttu-id="07349-137">列出所有可使用此工具卸載的 ASP.NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-137">Lists all the ASP.NET Core runtimes that can be uninstalled with this tool.</span></span>

* **`--hosting-bundle`**

  <span data-ttu-id="07349-138">列出所有可使用此工具卸載的 .NET Core 裝載套件組合。</span><span class="sxs-lookup"><span data-stu-id="07349-138">Lists all the .NET Core hosting bundles that can be uninstalled with this tool.</span></span>

* **`--runtime`**

  <span data-ttu-id="07349-139">列出所有可使用此工具卸載的 .NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-139">Lists all .NET Core runtimes that can be uninstalled with this tool.</span></span>

* **`--sdk`**

  <span data-ttu-id="07349-140">列出所有可使用此工具卸載的 .NET Core Sdk。</span><span class="sxs-lookup"><span data-stu-id="07349-140">Lists all .NET Core SDKs that can be uninstalled with this tool.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="07349-141">設定詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="07349-141">Sets the verbosity level.</span></span> <span data-ttu-id="07349-142">允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="07349-142">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="07349-143">預設值為 `normal`。</span><span class="sxs-lookup"><span data-stu-id="07349-143">The default value is `normal`.</span></span>

* **`--x64`**

  <span data-ttu-id="07349-144">列出所有可使用此工具卸載的 x64 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-144">Lists all x64 .NET Core SDKs and runtimes that can be uninstalled with this tool.</span></span>

* **`--x86`**

  <span data-ttu-id="07349-145">列出所有可使用此工具卸載的 x86 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-145">Lists all x86 .NET Core SDKs and runtimes that can be uninstalled with this tool.</span></span>

## <a name="macos"></a>[<span data-ttu-id="07349-146">macOS</span><span class="sxs-lookup"><span data-stu-id="07349-146">macOS</span></span>](#tab/macos)

* **`--runtime`**

  <span data-ttu-id="07349-147">列出所有可使用此工具卸載的 .NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-147">Lists all .NET Core runtimes that can be uninstalled with this tool.</span></span>

* **`--sdk`**

  <span data-ttu-id="07349-148">列出所有可使用此工具卸載的 .NET Core Sdk。</span><span class="sxs-lookup"><span data-stu-id="07349-148">Lists all .NET Core SDKs that can be uninstalled with this tool.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="07349-149">設定詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="07349-149">Sets the verbosity level.</span></span> <span data-ttu-id="07349-150">允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="07349-150">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="07349-151">預設值為 `normal`。</span><span class="sxs-lookup"><span data-stu-id="07349-151">The default value is `normal`.</span></span>
  
---

#### <a name="examples"></a><span data-ttu-id="07349-152">範例</span><span class="sxs-lookup"><span data-stu-id="07349-152">Examples</span></span>

* <span data-ttu-id="07349-153">列出所有可使用此工具移除的 .NET Core Sdk 和執行時間：</span><span class="sxs-lookup"><span data-stu-id="07349-153">List all .NET Core SDKs and runtimes that can be removed with this tool:</span></span>

  ```console
  dotnet-core-uninstall list
  ```

* <span data-ttu-id="07349-154">列出所有 x64 .NET Core Sdk 和執行時間：</span><span class="sxs-lookup"><span data-stu-id="07349-154">List all x64 .NET Core SDKs and runtimes:</span></span>

  ```console
  dotnet-core-uninstall list --x64
  ```

* <span data-ttu-id="07349-155">列出所有的 x86 .NET Core Sdk：</span><span class="sxs-lookup"><span data-stu-id="07349-155">List all x86 .NET Core SDKs:</span></span>

  ```console
  dotnet-core-uninstall list --sdk --x86
  ```

### <a name="step-2---do-a-dry-run"></a><span data-ttu-id="07349-156">步驟 2-進行試執行</span><span class="sxs-lookup"><span data-stu-id="07349-156">Step 2 - Do a dry run</span></span>

<span data-ttu-id="07349-157">`dotnet-core-uninstall dry-run`和 `dotnet-core-uninstall whatif` 命令會顯示 .Net Core sdk 和執行時間，將會根據所提供的選項而移除，而不需執行卸載。</span><span class="sxs-lookup"><span data-stu-id="07349-157">The `dotnet-core-uninstall dry-run` and `dotnet-core-uninstall whatif` commands display the .NET Core SDKs and runtimes that will be removed based on the options provided without performing the uninstall.</span></span> <span data-ttu-id="07349-158">這些命令是同義字。</span><span class="sxs-lookup"><span data-stu-id="07349-158">These commands are synonyms.</span></span>

<span data-ttu-id="07349-159">**dotnet-核心-卸載試執行和 dotnet-核心-卸載 whatif**</span><span class="sxs-lookup"><span data-stu-id="07349-159">**dotnet-core-uninstall dry-run and dotnet-core-uninstall whatif**</span></span>

#### <a name="synopsis"></a><span data-ttu-id="07349-160">概要</span><span class="sxs-lookup"><span data-stu-id="07349-160">Synopsis</span></span>

```console
dotnet-core-uninstall dry-run [options] [<VERSION>...]

dotnet-core-uninstall whatif [options] [<VERSION>...]
```

#### <a name="arguments"></a><span data-ttu-id="07349-161">引數</span><span class="sxs-lookup"><span data-stu-id="07349-161">Arguments</span></span>

* **`VERSION`**

  <span data-ttu-id="07349-162">要卸載的指定版本。</span><span class="sxs-lookup"><span data-stu-id="07349-162">The specified version to uninstall.</span></span> <span data-ttu-id="07349-163">您可以逐一列出數個版本，並以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="07349-163">You may list several versions one after the other, separated by spaces.</span></span> <span data-ttu-id="07349-164">也支援回應檔案。</span><span class="sxs-lookup"><span data-stu-id="07349-164">Response files are also supported.</span></span>

  > [!TIP]
  > <span data-ttu-id="07349-165">回應檔案是將所有版本放在命令列上的替代方案。</span><span class="sxs-lookup"><span data-stu-id="07349-165">Response files are an alternative to placing all the versions on the command line.</span></span>
  > <span data-ttu-id="07349-166">它們是文字檔，通常 \* 副檔名為 .rsp，而每個版本都會列在個別的一行上。</span><span class="sxs-lookup"><span data-stu-id="07349-166">They're text files, typically with a \*.rsp extension, and each version is listed on a separate line.</span></span>
  > <span data-ttu-id="07349-167">若要指定引數的回應檔 `VERSION` ，請使用 \@ 緊接在回應檔名稱後面的字元。</span><span class="sxs-lookup"><span data-stu-id="07349-167">To specify a response file for the `VERSION` argument, use the \@ character immediately followed by the response file name.</span></span>

#### <a name="options"></a><span data-ttu-id="07349-168">選項</span><span class="sxs-lookup"><span data-stu-id="07349-168">Options</span></span>

## <a name="windows"></a>[<span data-ttu-id="07349-169">Windows</span><span class="sxs-lookup"><span data-stu-id="07349-169">Windows</span></span>](#tab/windows)

* **`--all`**

  <span data-ttu-id="07349-170">移除所有 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-170">Removes all .NET Core SDKs and runtimes.</span></span>

* **`--all-below <VERSION>[ <VERSION>...]`**

  <span data-ttu-id="07349-171">只移除版本小於指定版本的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-171">Removes only the .NET Core SDKs and runtimes with a version smaller than the specified version.</span></span> <span data-ttu-id="07349-172">指定的版本仍會安裝。</span><span class="sxs-lookup"><span data-stu-id="07349-172">The specified version remains installed.</span></span>

* **`--all-but <VERSIONS>[ <VERSION>...]`**

  <span data-ttu-id="07349-173">除了指定的版本之外，移除所有 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-173">Removes all .NET Core SDKs and runtimes, except those versions specified.</span></span>

* **`--all-but-latest`**

  <span data-ttu-id="07349-174">移除 .NET Core Sdk 和執行時間，但不含最高版本。</span><span class="sxs-lookup"><span data-stu-id="07349-174">Removes .NET Core SDKs and runtimes, except the one highest version.</span></span>

* **`--all-lower-patches`**

  <span data-ttu-id="07349-175">移除由較高修補程式取代的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-175">Removes .NET Core SDKs and runtimes superseded by higher patches.</span></span> <span data-ttu-id="07349-176">此選項可保護 global. json。</span><span class="sxs-lookup"><span data-stu-id="07349-176">This option protects global.json.</span></span>

* **`--all-previews`**

  <span data-ttu-id="07349-177">移除標示為預覽的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-177">Removes .NET Core SDKs and runtimes marked as previews.</span></span>

* **`--all-previews-but-latest`**

  <span data-ttu-id="07349-178">移除標記為預覽的 .NET Core Sdk 和執行時間，但最高預覽版本除外。</span><span class="sxs-lookup"><span data-stu-id="07349-178">Removes .NET Core SDKs and runtimes marked as previews except the one highest preview.</span></span>

* **`--aspnet-runtime`**

  <span data-ttu-id="07349-179">只移除 ASP.NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-179">Removes ASP.NET Core runtimes only.</span></span>

* **`--hosting-bundle`**

  <span data-ttu-id="07349-180">只會移除 .NET Core 執行時間和裝載套件組合。</span><span class="sxs-lookup"><span data-stu-id="07349-180">Removes .NET Core runtime and hosting bundles only.</span></span>

* **`--major-minor <MAJOR_MINOR>`**

  <span data-ttu-id="07349-181">移除符合指定版本的 .NET Core Sdk 和執行時間 `major.minor` 。</span><span class="sxs-lookup"><span data-stu-id="07349-181">Removes .NET Core SDKs and runtimes that match the specified `major.minor` version.</span></span>

* **`--runtime`**

  <span data-ttu-id="07349-182">只會移除 .NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-182">Removes .NET Core runtimes only.</span></span>

* **`--sdk`**

  <span data-ttu-id="07349-183">僅移除 .NET Core Sdk。</span><span class="sxs-lookup"><span data-stu-id="07349-183">Removes .NET Core SDKs only.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="07349-184">設定詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="07349-184">Sets the verbosity level.</span></span> <span data-ttu-id="07349-185">允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="07349-185">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="07349-186">預設值為 `normal`。</span><span class="sxs-lookup"><span data-stu-id="07349-186">The default value is `normal`.</span></span>

* **`--x64`**

  <span data-ttu-id="07349-187">必須搭配 `--sdk` 、和使用， `--runtime` `--aspnet-runtime` 才能移除 x64 sdk 或執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-187">Must be used with `--sdk`, `--runtime`, and `--aspnet-runtime` to remove x64 SDKs or runtimes.</span></span>

* **`--x86`**

  <span data-ttu-id="07349-188">必須搭配 `--sdk` 、和使用， `--runtime` `--aspnet-runtime` 才能移除 x86 sdk 或執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-188">Must be used with `--sdk`, `--runtime`, and `--aspnet-runtime` to remove x86 SDKs or runtimes.</span></span>

* <span data-ttu-id="07349-189">**`--force`** 強制移除 Visual Studio 可能使用的版本。</span><span class="sxs-lookup"><span data-stu-id="07349-189">**`--force`** Forces removal of versions that might be used by Visual Studio.</span></span>

<span data-ttu-id="07349-190">注意：</span><span class="sxs-lookup"><span data-stu-id="07349-190">Notes:</span></span>

1. <span data-ttu-id="07349-191">只 `--sdk` `--runtime` 需要、、 `--aspnet-runtime` 和 `--hosting-bundle` 其中一個。</span><span class="sxs-lookup"><span data-stu-id="07349-191">Exactly one of `--sdk`, `--runtime`, `--aspnet-runtime`, and `--hosting-bundle` is required.</span></span>
2. <span data-ttu-id="07349-192">`--all`、 `--all-below` 、 `--all-but` 、 `--all-but-latest` 、 `--all-lower-patches` 、、、 `--all-previews` `--all-previews-but-latest` `--major-minor` 和 `[<VERSION>...]` 是獨佔的。</span><span class="sxs-lookup"><span data-stu-id="07349-192">`--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`, and `[<VERSION>...]` are exclusive.</span></span>
3. <span data-ttu-id="07349-193">如果 `--x64` `--x86` 未指定或，則會移除 x64 和 x86。</span><span class="sxs-lookup"><span data-stu-id="07349-193">If `--x64` or `--x86` aren't specified, then both x64 and x86 will be removed.</span></span>

## <a name="macos"></a>[<span data-ttu-id="07349-194">macOS</span><span class="sxs-lookup"><span data-stu-id="07349-194">macOS</span></span>](#tab/macos)

* **`--all`**

  <span data-ttu-id="07349-195">移除所有 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-195">Removes all .NET Core SDKs and runtimes.</span></span>

* **`--all-below <VERSION>[ <VERSION>...]`**

  <span data-ttu-id="07349-196">移除指定版本底下的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-196">Removes .NET Core SDKs and runtimes below the specified version.</span></span> <span data-ttu-id="07349-197">指定的版本將會保留。</span><span class="sxs-lookup"><span data-stu-id="07349-197">The specified version will remain.</span></span>

* **`--all-but <VERSIONS>[ <VERSION>...]`**

  <span data-ttu-id="07349-198">除了指定的版本之外，移除 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-198">Removes .NET Core SDKs and runtimes, except those versions specified.</span></span>

* **`--all-but-latest`**

  <span data-ttu-id="07349-199">移除 .NET Core Sdk 和執行時間，但不含最高版本。</span><span class="sxs-lookup"><span data-stu-id="07349-199">Removes .NET Core SDKs and runtimes, except the one highest version.</span></span>

* **`--all-lower-patches`**

  <span data-ttu-id="07349-200">移除由較高修補程式取代的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-200">Removes .NET Core SDKs and runtimes superseded by higher patches.</span></span> <span data-ttu-id="07349-201">此選項可保護 global. json。</span><span class="sxs-lookup"><span data-stu-id="07349-201">This option protects global.json.</span></span>

* **`--all-previews`**

  <span data-ttu-id="07349-202">移除標示為預覽的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-202">Removes .NET Core SDKs and runtimes marked as previews.</span></span>

* **`--all-previews-but-latest`**

  <span data-ttu-id="07349-203">移除標記為預覽的 .NET Core Sdk 和執行時間，但最高預覽版本除外。</span><span class="sxs-lookup"><span data-stu-id="07349-203">Removes .NET Core SDKs and runtimes marked as previews except the one highest preview.</span></span>

* **`--major-minor <MAJOR_MINOR>`**

  <span data-ttu-id="07349-204">移除符合指定版本的 .NET Core Sdk 和執行時間 `major.minor` 。</span><span class="sxs-lookup"><span data-stu-id="07349-204">Removes .NET Core SDKs and runtimes that match the specified `major.minor` version.</span></span>

* **`--runtime`**

  <span data-ttu-id="07349-205">只會移除 .NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-205">Removes .NET Core runtimes only.</span></span>

* **`--sdk`**

  <span data-ttu-id="07349-206">僅移除 .NET Core Sdk。</span><span class="sxs-lookup"><span data-stu-id="07349-206">Removes .NET Core SDKs only.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="07349-207">設定詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="07349-207">Sets the verbosity level.</span></span> <span data-ttu-id="07349-208">允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="07349-208">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="07349-209">預設值為 `normal`。</span><span class="sxs-lookup"><span data-stu-id="07349-209">The default value is `normal`.</span></span>
  
* <span data-ttu-id="07349-210">**`--force`** 強制移除 Visual Studio 或 Sdk 可能使用的版本。</span><span class="sxs-lookup"><span data-stu-id="07349-210">**`--force`** Forces removal of versions that might be used by Visual Studio or SDKs.</span></span>

<span data-ttu-id="07349-211">注意：</span><span class="sxs-lookup"><span data-stu-id="07349-211">Notes:</span></span>

1. <span data-ttu-id="07349-212">只有其中一個 `--sdk` 和 `--runtime` 是必要的。</span><span class="sxs-lookup"><span data-stu-id="07349-212">Exactly one of `--sdk` and `--runtime` is required.</span></span>
2. <span data-ttu-id="07349-213">`--all`、 `--all-below` 、 `--all-but` 、 `--all-but-latest` 、 `--all-lower-patches` 、、、 `--all-previews` `--all-previews-but-latest` `--major-minor` 和 `[<VERSION>...]` 是獨佔的。</span><span class="sxs-lookup"><span data-stu-id="07349-213">`--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`, and `[<VERSION>...]` are exclusive.</span></span>

---

#### <a name="examples"></a><span data-ttu-id="07349-214">範例</span><span class="sxs-lookup"><span data-stu-id="07349-214">Examples</span></span>

> [!NOTE]
> <span data-ttu-id="07349-215">根據預設，Visual Studio 或其他 Sdk 可能需要的 .NET Core Sdk 和執行時間不會包含在 `dotnet-core-uninstall dry-run` 輸出中。</span><span class="sxs-lookup"><span data-stu-id="07349-215">By default, .NET Core SDKs and runtimes that may be required by Visual Studio or other SDKs are not included in `dotnet-core-uninstall dry-run` output.</span></span> <span data-ttu-id="07349-216">在下列範例中，某些指定的 Sdk 和執行時間可能不會包含在輸出中，視電腦的狀態而定。</span><span class="sxs-lookup"><span data-stu-id="07349-216">In the following examples, some of the specified SDKs and runtimes may not be included in the output, depending on the state of the machine.</span></span> <span data-ttu-id="07349-217">若要包含所有 Sdk 和執行時間，請將它們明確列出為引數或使用 `--force` 選項。</span><span class="sxs-lookup"><span data-stu-id="07349-217">To include all SDKs and runtimes, list them explicitly as arguments or use the `--force` option.</span></span>

* <span data-ttu-id="07349-218">試執行移除所有已被較高修補程式取代的 .NET Core 執行時間：</span><span class="sxs-lookup"><span data-stu-id="07349-218">Dry run of removing all .NET Core runtimes that have been superseded by higher patches:</span></span>

  ```console
  dotnet-core-uninstall dry-run --all-lower-patches --runtime
  ```

* <span data-ttu-id="07349-219">在版本下方移除所有 .NET Core Sdk 的試執行 `2.2.301` ：</span><span class="sxs-lookup"><span data-stu-id="07349-219">Dry run of removing all .NET Core SDKs below the version `2.2.301`:</span></span>

  ```console
  dotnet-core-uninstall whatif --all-below 2.2.301 --sdk
  ```

### <a name="step-3---uninstall-net-core-sdks-and-runtimes"></a><span data-ttu-id="07349-220">步驟 3-卸載 .NET Core Sdk 和執行時間</span><span class="sxs-lookup"><span data-stu-id="07349-220">Step 3 - Uninstall .NET Core SDKs and Runtimes</span></span>

<span data-ttu-id="07349-221">`dotnet-core-uninstall remove`卸載選項組合所指定的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-221">`dotnet-core-uninstall remove` uninstalls .NET Core SDKs and Runtimes that are specified by a collection of options.</span></span> <span data-ttu-id="07349-222">此工具無法用來卸載版本5.0 或更高版本的 Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-222">The tool can't be used to uninstall SDKs and Runtimes with version 5.0 or above.</span></span>

<span data-ttu-id="07349-223">由於此工具具有破壞性的行為，因此**強烈**建議您在執行 [移除] 命令之前先進行試執行。</span><span class="sxs-lookup"><span data-stu-id="07349-223">Since this tool has a destructive behavior, it's **highly** recommended that you do a dry run before running the remove command.</span></span> <span data-ttu-id="07349-224">試執行會顯示當您使用命令時，將會移除哪些 .NET Core Sdk 和執行時間 `remove` 。</span><span class="sxs-lookup"><span data-stu-id="07349-224">The dry run will show you what .NET Core SDKs and runtimes will be removed when you use the `remove` command.</span></span> <span data-ttu-id="07349-225">請參閱[我應該移除版本嗎？](../install/remove-runtime-sdk-versions.md#should-i-remove-a-version)以瞭解哪些 sdk 和執行時間可以安全地移除。</span><span class="sxs-lookup"><span data-stu-id="07349-225">Refer to [Should I remove a version?](../install/remove-runtime-sdk-versions.md#should-i-remove-a-version) to learn which SDKs and runtimes are safe to remove.</span></span>

> [!CAUTION]
> <span data-ttu-id="07349-226">請記住下列注意事項：</span><span class="sxs-lookup"><span data-stu-id="07349-226">Keep in mind the following caveats:</span></span>
>
>- <span data-ttu-id="07349-227">這項工具可以卸載電腦上的檔案所需的 .NET Core SDK 版本 `global.json` 。</span><span class="sxs-lookup"><span data-stu-id="07349-227">This tool can uninstall versions of the .NET Core SDK that are required by `global.json` files on your machine.</span></span> <span data-ttu-id="07349-228">您可以從[下載 .Net core](https://dotnet.microsoft.com/download/dotnet-core)頁面重新安裝 .Net core sdk。</span><span class="sxs-lookup"><span data-stu-id="07349-228">You can reinstall .NET Core SDKs from the [Download .NET Core](https://dotnet.microsoft.com/download/dotnet-core) page.</span></span>
>- <span data-ttu-id="07349-229">這項工具可以卸載電腦上架構相依應用程式所需的 .NET Core 執行階段版本。</span><span class="sxs-lookup"><span data-stu-id="07349-229">This tool can uninstall versions of the .NET Core runtime that are required by framework dependent applications on your machine.</span></span> <span data-ttu-id="07349-230">您可以從 [[下載 .Net core](https://dotnet.microsoft.com/download/dotnet-core) ] 頁面重新安裝 .net core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-230">You can reinstall .NET Core runtimes from the [Download .NET Core](https://dotnet.microsoft.com/download/dotnet-core) page.</span></span>
>- <span data-ttu-id="07349-231">這項工具可以卸載 Visual Studio 依賴之 .NET Core SDK 和執行時間的版本。</span><span class="sxs-lookup"><span data-stu-id="07349-231">This tool can uninstall versions of the .NET Core SDK and runtime that Visual Studio relies on.</span></span> <span data-ttu-id="07349-232">如果您中斷 Visual Studio 安裝，請在 Visual Studio 安裝程式中執行 [修復]，以回到作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="07349-232">If you break your Visual Studio installation, run "Repair" in the Visual Studio installer to get back to a working state.</span></span>

<span data-ttu-id="07349-233">根據預設，所有命令都會保留 Visual Studio 或其他 Sdk 可能需要的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-233">By default, all commands keep the .NET Core SDKs and runtimes that may be required by Visual Studio or other SDKs.</span></span> <span data-ttu-id="07349-234">這些 Sdk 和執行時間可以藉由將它們明確地列為引數或使用選項來進行卸載 `--force` 。</span><span class="sxs-lookup"><span data-stu-id="07349-234">These SDKs and runtimes can be uninstalled by listing them explicitly as arguments or by using the `--force` option.</span></span>

<span data-ttu-id="07349-235">此工具需要提高許可權，才能卸載 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-235">The tool requires elevation to uninstall .NET Core SDKs and runtimes.</span></span> <span data-ttu-id="07349-236">在 Windows 上的系統管理員命令提示字元中，以及 `sudo` 在 macOS 上執行工具。</span><span class="sxs-lookup"><span data-stu-id="07349-236">Run the tool in an Administrator command prompt on Windows and with `sudo` on macOS.</span></span> <span data-ttu-id="07349-237">`dry-run`和 `whatif` 命令不需要提高許可權。</span><span class="sxs-lookup"><span data-stu-id="07349-237">The `dry-run` and `whatif` commands don't require elevation.</span></span>

<span data-ttu-id="07349-238">**dotnet-核心-卸載移除**</span><span class="sxs-lookup"><span data-stu-id="07349-238">**dotnet-core-uninstall remove**</span></span>

#### <a name="synopsis"></a><span data-ttu-id="07349-239">概要</span><span class="sxs-lookup"><span data-stu-id="07349-239">Synopsis</span></span>

```console
dotnet-core-uninstall remove [options] [<VERSION>...]
```

#### <a name="arguments"></a><span data-ttu-id="07349-240">引數</span><span class="sxs-lookup"><span data-stu-id="07349-240">Arguments</span></span>

* **`VERSION`**

  <span data-ttu-id="07349-241">要卸載的指定版本。</span><span class="sxs-lookup"><span data-stu-id="07349-241">The specified version to uninstall.</span></span> <span data-ttu-id="07349-242">您可以逐一列出數個版本，並以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="07349-242">You may list several versions one after the other, separated by spaces.</span></span> <span data-ttu-id="07349-243">也支援回應檔案。</span><span class="sxs-lookup"><span data-stu-id="07349-243">Response files are also supported.</span></span>

  > [!TIP]
  > <span data-ttu-id="07349-244">回應檔案是將所有版本放在命令列上的替代方案。</span><span class="sxs-lookup"><span data-stu-id="07349-244">Response files are an alternative to placing all the versions on the command line.</span></span>
  > <span data-ttu-id="07349-245">它們是文字檔，通常 \* 副檔名為 .rsp，而每個版本都會列在個別的一行上。</span><span class="sxs-lookup"><span data-stu-id="07349-245">They're text files, typically with a \*.rsp extension, and each version is listed on a separate line.</span></span>
  > <span data-ttu-id="07349-246">若要指定引數的回應檔 `VERSION` ，請使用 \@ 緊接在回應檔名稱後面的字元。</span><span class="sxs-lookup"><span data-stu-id="07349-246">To specify a response file for the `VERSION` argument, use the \@ character immediately followed by the response file name.</span></span>

#### <a name="options"></a><span data-ttu-id="07349-247">選項</span><span class="sxs-lookup"><span data-stu-id="07349-247">Options</span></span>

## <a name="windows"></a>[<span data-ttu-id="07349-248">Windows</span><span class="sxs-lookup"><span data-stu-id="07349-248">Windows</span></span>](#tab/windows)

* **`--all`**

  <span data-ttu-id="07349-249">移除所有 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-249">Removes all .NET Core SDKs and runtimes.</span></span>

* **`--all-below <VERSION>[ <VERSION>...]`**

  <span data-ttu-id="07349-250">只移除版本小於指定版本的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-250">Removes only the .NET Core SDKs and runtimes with a version smaller than the specified version.</span></span> <span data-ttu-id="07349-251">指定的版本仍會安裝。</span><span class="sxs-lookup"><span data-stu-id="07349-251">The specified version remains installed.</span></span>

* **`--all-but <VERSIONS>[ <VERSION>...]`**

  <span data-ttu-id="07349-252">除了指定的版本之外，移除所有 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-252">Removes all .NET Core SDKs and runtimes, except those versions specified.</span></span>

* **`--all-but-latest`**

  <span data-ttu-id="07349-253">移除 .NET Core Sdk 和執行時間，但不含最高版本。</span><span class="sxs-lookup"><span data-stu-id="07349-253">Removes .NET Core SDKs and runtimes, except the one highest version.</span></span>

* **`--all-lower-patches`**

  <span data-ttu-id="07349-254">移除由較高修補程式取代的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-254">Removes .NET Core SDKs and runtimes superseded by higher patches.</span></span> <span data-ttu-id="07349-255">此選項可保護 global. json。</span><span class="sxs-lookup"><span data-stu-id="07349-255">This option protects global.json.</span></span>

* **`--all-previews`**

  <span data-ttu-id="07349-256">移除標示為預覽的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-256">Removes .NET Core SDKs and runtimes marked as previews.</span></span>

* **`--all-previews-but-latest`**

  <span data-ttu-id="07349-257">移除標記為預覽的 .NET Core Sdk 和執行時間，但最高預覽版本除外。</span><span class="sxs-lookup"><span data-stu-id="07349-257">Removes .NET Core SDKs and runtimes marked as previews except the one highest preview.</span></span>

* **`--aspnet-runtime`**

  <span data-ttu-id="07349-258">只移除 ASP.NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-258">Removes ASP.NET Core runtimes only.</span></span>

* **`--hosting-bundle`**

  <span data-ttu-id="07349-259">只會移除 .NET Core 裝載套件組合。</span><span class="sxs-lookup"><span data-stu-id="07349-259">Removes .NET Core hosting bundles only.</span></span>

* **`--major-minor <MAJOR_MINOR>`**

  <span data-ttu-id="07349-260">移除符合指定版本的 .NET Core Sdk 和執行時間 `major.minor` 。</span><span class="sxs-lookup"><span data-stu-id="07349-260">Removes .NET Core SDKs and runtimes that match the specified `major.minor` version.</span></span>

* **`--runtime`**

  <span data-ttu-id="07349-261">只會移除 .NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-261">Removes .NET Core runtimes only.</span></span>

* **`--sdk`**

  <span data-ttu-id="07349-262">僅移除 .NET Core Sdk。</span><span class="sxs-lookup"><span data-stu-id="07349-262">Removes .NET Core SDKs only.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="07349-263">設定詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="07349-263">Sets the verbosity level.</span></span> <span data-ttu-id="07349-264">允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="07349-264">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="07349-265">預設值為 `normal`。</span><span class="sxs-lookup"><span data-stu-id="07349-265">The default value is `normal`.</span></span>

* **`--x64`**

  <span data-ttu-id="07349-266">必須搭配 `--sdk` 、和使用， `--runtime` `--aspnet-runtime` 才能移除 x64 sdk 或執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-266">Must be used with `--sdk`, `--runtime`, and `--aspnet-runtime` to remove x64 SDKs or runtimes.</span></span>

* **`--x86`**

  <span data-ttu-id="07349-267">必須搭配 `--sdk` 、和使用， `--runtime` `--aspnet-runtime` 才能移除 x86 sdk 或執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-267">Must be used with `--sdk`, `--runtime`, and `--aspnet-runtime` to remove x86 SDKs or runtimes.</span></span>

* <span data-ttu-id="07349-268">**`-y, --yes`** 執行命令，而不需要有 [是] 或 [否] 確認。</span><span class="sxs-lookup"><span data-stu-id="07349-268">**`-y, --yes`** Executes the command without requiring a yes or no confirmation.</span></span>

* <span data-ttu-id="07349-269">**`--force`** 強制移除 Visual Studio 可能使用的版本。</span><span class="sxs-lookup"><span data-stu-id="07349-269">**`--force`** Forces removal of versions that might be used by Visual Studio.</span></span>

<span data-ttu-id="07349-270">注意：</span><span class="sxs-lookup"><span data-stu-id="07349-270">Notes:</span></span>

1. <span data-ttu-id="07349-271">只 `--sdk` `--runtime` 需要、、 `--aspnet-runtime` 和 `--hosting-bundle` 其中一個。</span><span class="sxs-lookup"><span data-stu-id="07349-271">Exactly one of `--sdk`, `--runtime`, `--aspnet-runtime`, and `--hosting-bundle` is required.</span></span>
2. <span data-ttu-id="07349-272">`--all`、 `--all-below` 、 `--all-but` 、 `--all-but-latest` 、 `--all-lower-patches` 、、、 `--all-previews` `--all-previews-but-latest` `--major-minor` 和 `[<VERSION>...]` 是獨佔的。</span><span class="sxs-lookup"><span data-stu-id="07349-272">`--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`, and `[<VERSION>...]` are exclusive.</span></span>
3. <span data-ttu-id="07349-273">如果 `--x64` `--x86` 未指定或，則會移除 x64 和 x86。</span><span class="sxs-lookup"><span data-stu-id="07349-273">If `--x64` or `--x86` aren't specified, then both x64 and x86 will be removed.</span></span>

## <a name="macos"></a>[<span data-ttu-id="07349-274">macOS</span><span class="sxs-lookup"><span data-stu-id="07349-274">macOS</span></span>](#tab/macos)

* **`--all`**

  <span data-ttu-id="07349-275">移除所有 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-275">Removes all .NET Core SDKs and runtimes.</span></span>

* **`--all-below <VERSION>[ <VERSION>...]`**

  <span data-ttu-id="07349-276">移除指定版本底下的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-276">Removes .NET Core SDKs and runtimes below the specified version.</span></span> <span data-ttu-id="07349-277">指定的版本將會保留。</span><span class="sxs-lookup"><span data-stu-id="07349-277">The specified version will remain.</span></span>

* **`--all-but <VERSIONS>[ <VERSION>...]`**

  <span data-ttu-id="07349-278">除了指定的版本之外，移除 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-278">Removes .NET Core SDKs and runtimes, except those versions specified.</span></span>

* **`--all-but-latest`**

  <span data-ttu-id="07349-279">移除 .NET Core Sdk 和執行時間，但不含最高版本。</span><span class="sxs-lookup"><span data-stu-id="07349-279">Removes .NET Core SDKs and runtimes, except the one highest version.</span></span>

* **`--all-lower-patches`**

  <span data-ttu-id="07349-280">移除由較高修補程式取代的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-280">Removes .NET Core SDKs and runtimes superseded by higher patches.</span></span> <span data-ttu-id="07349-281">此選項可保護 global. json。</span><span class="sxs-lookup"><span data-stu-id="07349-281">This option protects global.json.</span></span>

* **`--all-previews`**

  <span data-ttu-id="07349-282">移除標示為預覽的 .NET Core Sdk 和執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-282">Removes .NET Core SDKs and runtimes marked as previews.</span></span>

* **`--all-previews-but-latest`**

  <span data-ttu-id="07349-283">移除標記為預覽的 .NET Core Sdk 和執行時間，但最高預覽版本除外。</span><span class="sxs-lookup"><span data-stu-id="07349-283">Removes .NET Core SDKs and runtimes marked as previews except the one highest preview.</span></span>

* **`--major-minor <MAJOR_MINOR>`**

  <span data-ttu-id="07349-284">移除符合指定版本的 .NET Core Sdk 和執行時間 `major.minor` 。</span><span class="sxs-lookup"><span data-stu-id="07349-284">Removes .NET Core SDKs and runtimes that match the specified `major.minor` version.</span></span>

* **`--runtime`**

  <span data-ttu-id="07349-285">只會移除 .NET Core 執行時間。</span><span class="sxs-lookup"><span data-stu-id="07349-285">Removes .NET Core runtimes only.</span></span>

* **`--sdk`**

  <span data-ttu-id="07349-286">僅移除 .NET Core Sdk。</span><span class="sxs-lookup"><span data-stu-id="07349-286">Removes .NET Core SDKs only.</span></span>

* **`-v, --verbosity <LEVEL>`**

  <span data-ttu-id="07349-287">設定詳細資訊層級。</span><span class="sxs-lookup"><span data-stu-id="07349-287">Sets the verbosity level.</span></span> <span data-ttu-id="07349-288">允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。</span><span class="sxs-lookup"><span data-stu-id="07349-288">Allowed values are `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]`, and `diag[nostic]`.</span></span> <span data-ttu-id="07349-289">預設值為 `normal`。</span><span class="sxs-lookup"><span data-stu-id="07349-289">The default value is `normal`.</span></span>

* <span data-ttu-id="07349-290">**`-y, --yes`** 執行命令，而不需要 Y/N 確認。</span><span class="sxs-lookup"><span data-stu-id="07349-290">**`-y, --yes`** Executes the command without requiring Y/N confirmation.</span></span>
  
* <span data-ttu-id="07349-291">**`--force`** 強制移除 Visual Studio 或 Sdk 可能使用的版本。</span><span class="sxs-lookup"><span data-stu-id="07349-291">**`--force`** Forces removal of versions that might be used by Visual Studio or SDKs.</span></span>

<span data-ttu-id="07349-292">注意：</span><span class="sxs-lookup"><span data-stu-id="07349-292">Notes:</span></span>

1. <span data-ttu-id="07349-293">只有其中一個 `--sdk` 和 `--runtime` 是必要的。</span><span class="sxs-lookup"><span data-stu-id="07349-293">Exactly one of `--sdk` and `--runtime` is required.</span></span>
2. <span data-ttu-id="07349-294">`--all`、 `--all-below` 、 `--all-but` 、 `--all-but-latest` 、 `--all-lower-patches` 、、、 `--all-previews` `--all-previews-but-latest` `--major-minor` 和 `[<VERSION>...]` 是獨佔的。</span><span class="sxs-lookup"><span data-stu-id="07349-294">`--all`, `--all-below`, `--all-but`, `--all-but-latest`, `--all-lower-patches`, `--all-previews`, `--all-previews-but-latest`, `--major-minor`, and `[<VERSION>...]` are exclusive.</span></span>

---

#### <a name="examples"></a><span data-ttu-id="07349-295">範例</span><span class="sxs-lookup"><span data-stu-id="07349-295">Examples</span></span>

> [!NOTE]
> <span data-ttu-id="07349-296">根據預設，Visual Studio 或其他 Sdk 可能需要的 .NET Core Sdk 和執行時間會保留下來。</span><span class="sxs-lookup"><span data-stu-id="07349-296">By default, .NET Core SDKs and runtimes that may be required by Visual Studio or other SDKs are kept.</span></span> <span data-ttu-id="07349-297">在下列範例中，某些指定的 Sdk 和執行時間可能會保留，視電腦的狀態而定。</span><span class="sxs-lookup"><span data-stu-id="07349-297">In the following examples, some of the specified SDKs and runtimes may remain, depending on the state of the machine.</span></span> <span data-ttu-id="07349-298">若要移除所有 Sdk 和執行時間，請將它們明確列出為引數或使用 `--force` 選項。</span><span class="sxs-lookup"><span data-stu-id="07349-298">To remove all SDKs and runtimes, list them explicitly as arguments or use the `--force` option.</span></span>

* <span data-ttu-id="07349-299">移除版本除外的所有 .NET Core 執行時間， `3.0.0-preview6-27804-01` 而不需要進行 Y/N 確認：</span><span class="sxs-lookup"><span data-stu-id="07349-299">Remove all .NET Core runtimes except the version `3.0.0-preview6-27804-01` without requiring Y/N confirmation:</span></span>

  ```console
  dotnet-core-uninstall remove --all-but 3.0.0-preview6-27804-01 --runtime --yes
  ```

* <span data-ttu-id="07349-300">移除所有 .NET Core 1.1 Sdk，而不需要進行 Y/n 確認：</span><span class="sxs-lookup"><span data-stu-id="07349-300">Remove all .NET Core 1.1 SDKs without requiring Y/n confirmation:</span></span>

  ```console
  dotnet-core-uninstall remove --sdk --major-minor 1.1 -y
  ```

* <span data-ttu-id="07349-301">移除沒有主控台輸出的 .NET Core 1.1.11 SDK：</span><span class="sxs-lookup"><span data-stu-id="07349-301">Remove the .NET Core 1.1.11 SDK with no console output:</span></span>

  ```console
  dotnet-core-uninstall remove 1.1.11 --sdk --yes --verbosity q
  ```

* <span data-ttu-id="07349-302">移除此工具可安全移除的所有 .NET Core Sdk：</span><span class="sxs-lookup"><span data-stu-id="07349-302">Remove all .NET Core SDKs that can safely be removed by this tool:</span></span>

  ```console
  dotnet-core-uninstall remove --all --sdk
  ```

* <span data-ttu-id="07349-303">移除此工具可移除的所有 .NET Core Sdk，包括 Visual Studio 可能需要的 Sdk （不建議）：</span><span class="sxs-lookup"><span data-stu-id="07349-303">Remove all .NET Core SDKs that can be removed by this tool, including those SDKs that may be required by Visual Studio (not recommended):</span></span>

  ```console
  dotnet-core-uninstall remove --all --sdk --force
  ```

* <span data-ttu-id="07349-304">移除回應檔中指定的所有 .NET Core Sdk`versions.rsp`</span><span class="sxs-lookup"><span data-stu-id="07349-304">Remove all .NET Core SDKs that are specified in the response file `versions.rsp`</span></span>

  ```console
  dotnet-core-uninstall remove --sdk @versions.rsp
  ```

  <span data-ttu-id="07349-305">*版本 .rsp*的內容如下所示：</span><span class="sxs-lookup"><span data-stu-id="07349-305">The content of *versions.rsp* is as follows:</span></span>
  
  ```text
  2.2.300
  2.1.700
  ```

### <a name="step-4---delete-the-nuget-fallback-folder-optional"></a><span data-ttu-id="07349-306">步驟 4-刪除 NuGet fallback 資料夾（選擇性）</span><span class="sxs-lookup"><span data-stu-id="07349-306">Step 4 - Delete the NuGet fallback folder (optional)</span></span>

<span data-ttu-id="07349-307">在某些情況下，您不再需要， `NuGetFallbackFolder` 而且可能想要將它刪除。</span><span class="sxs-lookup"><span data-stu-id="07349-307">In some cases, you no longer need the `NuGetFallbackFolder` and may wish to delete it.</span></span> <span data-ttu-id="07349-308">如需刪除此資料夾的詳細資訊，請參閱[移除 NuGetFallbackFolder](../install/remove-runtime-sdk-versions.md#remove-the-nuget-fallback-folder)。</span><span class="sxs-lookup"><span data-stu-id="07349-308">For more information about deleting this folder, see [Remove the NuGetFallbackFolder](../install/remove-runtime-sdk-versions.md#remove-the-nuget-fallback-folder).</span></span>

## <a name="uninstall-the-tool"></a><span data-ttu-id="07349-309">卸載工具</span><span class="sxs-lookup"><span data-stu-id="07349-309">Uninstall the tool</span></span>

## <a name="windows"></a>[<span data-ttu-id="07349-310">Windows</span><span class="sxs-lookup"><span data-stu-id="07349-310">Windows</span></span>](#tab/windows)

1. <span data-ttu-id="07349-311">開啟 [新增或移除程式]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="07349-311">Open **Add or Remove Programs**.</span></span>
2. <span data-ttu-id="07349-312">搜尋 `Microsoft .NET Core SDK Uninstall Tool`。</span><span class="sxs-lookup"><span data-stu-id="07349-312">Search for `Microsoft .NET Core SDK Uninstall Tool`.</span></span>
3. <span data-ttu-id="07349-313">選取 [解除安裝]。</span><span class="sxs-lookup"><span data-stu-id="07349-313">Select **Uninstall**.</span></span>

## <a name="macos"></a>[<span data-ttu-id="07349-314">macOS</span><span class="sxs-lookup"><span data-stu-id="07349-314">macOS</span></span>](#tab/macos)

<span data-ttu-id="07349-315">從安裝的目錄中刪除已下載的*dotnet-core-uninstall gz*檔案。</span><span class="sxs-lookup"><span data-stu-id="07349-315">Delete the downloaded *dotnet-core-uninstall.tar.gz* file from the directory where it was installed.</span></span> <span data-ttu-id="07349-316">如果您將此檔案的內容解壓縮至另一個目錄，請務必一併刪除該內容。</span><span class="sxs-lookup"><span data-stu-id="07349-316">If you unzipped the contents of this file into another directory, be sure to delete that content as well.</span></span>

---
