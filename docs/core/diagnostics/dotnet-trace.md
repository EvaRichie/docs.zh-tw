---
title: dotnet-追蹤工具-.NET Core
description: 安裝和使用 dotnet 追蹤命令列工具。
ms.date: 11/21/2019
ms.openlocfilehash: 25178a0e59ce9edb69d15ee761c1b9e56aa5eb3a
ms.sourcegitcommit: b4f8849c47c1a7145eb26ce68bc9f9976e0dbec3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2020
ms.locfileid: "87517304"
---
# <a name="dotnet-trace-performance-analysis-utility"></a><span data-ttu-id="cd685-103">dotnet-追蹤效能分析公用程式</span><span class="sxs-lookup"><span data-stu-id="cd685-103">dotnet-trace performance analysis utility</span></span>

<span data-ttu-id="cd685-104">**本文適用于：** ✔️ .net CORE 3.0 SDK 和更新版本</span><span class="sxs-lookup"><span data-stu-id="cd685-104">**This article applies to:** ✔️ .NET Core 3.0 SDK and later versions</span></span>

## <a name="install-dotnet-trace"></a><span data-ttu-id="cd685-105">安裝 dotnet-追蹤</span><span class="sxs-lookup"><span data-stu-id="cd685-105">Install dotnet-trace</span></span>

<span data-ttu-id="cd685-106">`dotnet-trace`使用[dotnet tool install](../tools/dotnet-tool-install.md)命令來安裝[NuGet 套件](https://www.nuget.org/packages/dotnet-trace)：</span><span class="sxs-lookup"><span data-stu-id="cd685-106">Install `dotnet-trace` [NuGet package](https://www.nuget.org/packages/dotnet-trace) with the [dotnet tool install](../tools/dotnet-tool-install.md) command:</span></span>

```dotnetcli
dotnet tool install --global dotnet-trace
```

## <a name="synopsis"></a><span data-ttu-id="cd685-107">概要</span><span class="sxs-lookup"><span data-stu-id="cd685-107">Synopsis</span></span>

```console
dotnet-trace [-h, --help] [--version] <command>
```

## <a name="description"></a><span data-ttu-id="cd685-108">說明</span><span class="sxs-lookup"><span data-stu-id="cd685-108">Description</span></span>

<span data-ttu-id="cd685-109">`dotnet-trace`工具：</span><span class="sxs-lookup"><span data-stu-id="cd685-109">The `dotnet-trace` tool:</span></span>

* <span data-ttu-id="cd685-110">是跨平臺 .NET Core 工具。</span><span class="sxs-lookup"><span data-stu-id="cd685-110">Is a cross-platform .NET Core tool.</span></span>
* <span data-ttu-id="cd685-111">可在不使用原生分析工具的情況下，收集執行中進程的 .NET Core 追蹤。</span><span class="sxs-lookup"><span data-stu-id="cd685-111">Enables the collection of .NET Core traces of a running process without a native profiler.</span></span>
* <span data-ttu-id="cd685-112">是圍繞 .NET Core 執行時間的跨平臺技術所建立 `EventPipe` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-112">Is built around the cross-platform `EventPipe` technology of the .NET Core runtime.</span></span>
* <span data-ttu-id="cd685-113">在 Windows、Linux 或 macOS 上提供相同的體驗。</span><span class="sxs-lookup"><span data-stu-id="cd685-113">Delivers the same experience on Windows, Linux, or macOS.</span></span>

## <a name="options"></a><span data-ttu-id="cd685-114">選項</span><span class="sxs-lookup"><span data-stu-id="cd685-114">Options</span></span>

- **`-h|--help`**

  <span data-ttu-id="cd685-115">顯示命令列說明。</span><span class="sxs-lookup"><span data-stu-id="cd685-115">Shows command-line help.</span></span>

- **`--version`**

  <span data-ttu-id="cd685-116">顯示 dotnet 追蹤公用程式的版本。</span><span class="sxs-lookup"><span data-stu-id="cd685-116">Displays the version of the dotnet-trace utility.</span></span>

## <a name="commands"></a><span data-ttu-id="cd685-117">命令</span><span class="sxs-lookup"><span data-stu-id="cd685-117">Commands</span></span>

| <span data-ttu-id="cd685-118">命令</span><span class="sxs-lookup"><span data-stu-id="cd685-118">Command</span></span>                                                   |
|-----------------------------------------------------------|
| [<span data-ttu-id="cd685-119">dotnet-追蹤收集</span><span class="sxs-lookup"><span data-stu-id="cd685-119">dotnet-trace collect</span></span>](#dotnet-trace-collect)             |
| [<span data-ttu-id="cd685-120">dotnet-追蹤轉換</span><span class="sxs-lookup"><span data-stu-id="cd685-120">dotnet-trace convert</span></span>](#dotnet-trace-convert)             |
| [<span data-ttu-id="cd685-121">dotnet-追蹤 ps</span><span class="sxs-lookup"><span data-stu-id="cd685-121">dotnet-trace ps</span></span>](#dotnet-trace-ps)                       |
| [<span data-ttu-id="cd685-122">dotnet-追蹤清單-設定檔</span><span class="sxs-lookup"><span data-stu-id="cd685-122">dotnet-trace list-profiles</span></span>](#dotnet-trace-list-profiles) |

## <a name="dotnet-trace-collect"></a><span data-ttu-id="cd685-123">dotnet-追蹤收集</span><span class="sxs-lookup"><span data-stu-id="cd685-123">dotnet-trace collect</span></span>

<span data-ttu-id="cd685-124">從執行中的進程收集診斷追蹤。</span><span class="sxs-lookup"><span data-stu-id="cd685-124">Collects a diagnostic trace from a running process.</span></span>

### <a name="synopsis"></a><span data-ttu-id="cd685-125">概要</span><span class="sxs-lookup"><span data-stu-id="cd685-125">Synopsis</span></span>

```console
dotnet-trace collect [--buffersize <size>] [--clreventlevel <clreventlevel>] [--clrevents <clrevents>]
    [--format <Chromium|NetTrace|Speedscope>] [-h|--help]
    [-n, --name <name>]  [-o|--output <trace-file-path>] [-p|--process-id <pid>]
    [--profile <profile-name>] [--providers <list-of-comma-separated-providers>]
```

### <a name="options"></a><span data-ttu-id="cd685-126">選項</span><span class="sxs-lookup"><span data-stu-id="cd685-126">Options</span></span>

- **`--buffersize <size>`**

  <span data-ttu-id="cd685-127">設定記憶體中迴圈緩衝區的大小（以 mb 為單位）。</span><span class="sxs-lookup"><span data-stu-id="cd685-127">Sets the size of the in-memory circular buffer, in megabytes.</span></span> <span data-ttu-id="cd685-128">預設值： 256 MB。</span><span class="sxs-lookup"><span data-stu-id="cd685-128">Default 256 MB.</span></span>

- **`--clreventlevel <clreventlevel>`**

  <span data-ttu-id="cd685-129">要發出之 CLR 事件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cd685-129">Verbosity of CLR events to be emitted.</span></span>

- **`--clrevents <clrevents>`**

  <span data-ttu-id="cd685-130">要發出的 CLR 運行時間事件清單。</span><span class="sxs-lookup"><span data-stu-id="cd685-130">List of CLR runtime events to emit.</span></span>

- **`--format {Chromium|NetTrace|Speedscope}`**

  <span data-ttu-id="cd685-131">設定追蹤檔案轉換的輸出格式。</span><span class="sxs-lookup"><span data-stu-id="cd685-131">Sets the output format for the trace file conversion.</span></span> <span data-ttu-id="cd685-132">預設值為 `NetTrace`。</span><span class="sxs-lookup"><span data-stu-id="cd685-132">The default is `NetTrace`.</span></span>

- **`-n, --name <name>`**

  <span data-ttu-id="cd685-133">要從中收集追蹤的進程名稱。</span><span class="sxs-lookup"><span data-stu-id="cd685-133">The name of the process to collect the trace from.</span></span>

- **`-o|--output <trace-file-path>`**

  <span data-ttu-id="cd685-134">所收集追蹤資料的輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="cd685-134">The output path for the collected trace data.</span></span> <span data-ttu-id="cd685-135">如果未指定，則會預設為 `trace.nettrace` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-135">If not specified, it defaults to `trace.nettrace`.</span></span>

- **`-p|--process-id <PID>`**

  <span data-ttu-id="cd685-136">要從中收集追蹤的處理序識別碼。</span><span class="sxs-lookup"><span data-stu-id="cd685-136">The process id to collect the trace from.</span></span>

- **`--profile <profile-name>`**

  <span data-ttu-id="cd685-137">一組命名的預先定義提供者設定，可讓您簡潔地指定一般追蹤案例。</span><span class="sxs-lookup"><span data-stu-id="cd685-137">A named pre-defined set of provider configurations that allows common tracing scenarios to be specified succinctly.</span></span>

- **`--providers <list-of-comma-separated-providers>`**

  <span data-ttu-id="cd685-138">要啟用的提供者清單（以逗號分隔） `EventPipe` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-138">A comma-separated list of `EventPipe` providers to be enabled.</span></span> <span data-ttu-id="cd685-139">這些提供者會補充所隱含的任何提供者 `--profile <profile-name>` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-139">These providers supplement any providers implied by `--profile <profile-name>`.</span></span> <span data-ttu-id="cd685-140">如果特定提供者有任何不一致的情況，則此設定的優先順序會高於設定檔的隱含設定。</span><span class="sxs-lookup"><span data-stu-id="cd685-140">If there's any inconsistency for a particular provider, this configuration takes precedence over the implicit configuration from the profile.</span></span>

  <span data-ttu-id="cd685-141">這份提供者清單的格式如下：</span><span class="sxs-lookup"><span data-stu-id="cd685-141">This list of providers is in the form:</span></span>

  - `Provider[,Provider]`
  - <span data-ttu-id="cd685-142">`Provider`的格式為： `KnownProviderName[:Flags[:Level][:KeyValueArgs]]` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-142">`Provider` is in the form: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]`.</span></span>
  - <span data-ttu-id="cd685-143">`KeyValueArgs`的格式為： `[key1=value1][;key2=value2]` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-143">`KeyValueArgs` is in the form: `[key1=value1][;key2=value2]`.</span></span>

## <a name="dotnet-trace-convert"></a><span data-ttu-id="cd685-144">dotnet-追蹤轉換</span><span class="sxs-lookup"><span data-stu-id="cd685-144">dotnet-trace convert</span></span>

<span data-ttu-id="cd685-145">將 `nettrace` 追蹤轉換為替代的格式，以搭配替代的追蹤分析工具使用。</span><span class="sxs-lookup"><span data-stu-id="cd685-145">Converts `nettrace` traces to alternate formats for use with alternate trace analysis tools.</span></span>

### <a name="synopsis"></a><span data-ttu-id="cd685-146">概要</span><span class="sxs-lookup"><span data-stu-id="cd685-146">Synopsis</span></span>

```console
dotnet-trace convert [<input-filename>] [--format <Chromium|NetTrace|Speedscope>] [-h|--help] [-o|--output <output-filename>]
```

### <a name="arguments"></a><span data-ttu-id="cd685-147">引數</span><span class="sxs-lookup"><span data-stu-id="cd685-147">Arguments</span></span>

- **`<input-filename>`**

  <span data-ttu-id="cd685-148">要轉換的輸入追蹤檔案。</span><span class="sxs-lookup"><span data-stu-id="cd685-148">Input trace file to be converted.</span></span> <span data-ttu-id="cd685-149">預設為*nettrace*。</span><span class="sxs-lookup"><span data-stu-id="cd685-149">Defaults to *trace.nettrace*.</span></span>

### <a name="options"></a><span data-ttu-id="cd685-150">選項</span><span class="sxs-lookup"><span data-stu-id="cd685-150">Options</span></span>

- **`--format <Chromium|NetTrace|Speedscope>`**

  <span data-ttu-id="cd685-151">設定追蹤檔案轉換的輸出格式。</span><span class="sxs-lookup"><span data-stu-id="cd685-151">Sets the output format for the trace file conversion.</span></span>

- **`-o|--output <output-filename>`**

  <span data-ttu-id="cd685-152">輸出檔案名。</span><span class="sxs-lookup"><span data-stu-id="cd685-152">Output filename.</span></span> <span data-ttu-id="cd685-153">將會加入目標格式的副檔名。</span><span class="sxs-lookup"><span data-stu-id="cd685-153">Extension of target format will be added.</span></span>

## <a name="dotnet-trace-ps"></a><span data-ttu-id="cd685-154">dotnet-追蹤 ps</span><span class="sxs-lookup"><span data-stu-id="cd685-154">dotnet-trace ps</span></span>

 <span data-ttu-id="cd685-155">列出可從中收集追蹤的 dotnet 進程。</span><span class="sxs-lookup"><span data-stu-id="cd685-155">Lists the dotnet processes that traces can be collected from.</span></span>

### <a name="synopsis"></a><span data-ttu-id="cd685-156">概要</span><span class="sxs-lookup"><span data-stu-id="cd685-156">Synopsis</span></span>

```console
dotnet-trace ps [-h|--help]
```

## <a name="dotnet-trace-list-profiles"></a><span data-ttu-id="cd685-157">dotnet-追蹤清單-設定檔</span><span class="sxs-lookup"><span data-stu-id="cd685-157">dotnet-trace list-profiles</span></span>

<span data-ttu-id="cd685-158">列出預先建立的追蹤設定檔，其中包含每個設定檔中提供者和篩選器的描述。</span><span class="sxs-lookup"><span data-stu-id="cd685-158">Lists pre-built tracing profiles with a description of what providers and filters are in each profile.</span></span>

### <a name="synopsis"></a><span data-ttu-id="cd685-159">概要</span><span class="sxs-lookup"><span data-stu-id="cd685-159">Synopsis</span></span>

```console
dotnet-trace list-profiles [-h|--help]
```

## <a name="collect-a-trace-with-dotnet-trace"></a><span data-ttu-id="cd685-160">使用 dotnet-trace 收集追蹤</span><span class="sxs-lookup"><span data-stu-id="cd685-160">Collect a trace with dotnet-trace</span></span>

<span data-ttu-id="cd685-161">若要使用來收集追蹤 `dotnet-trace` ：</span><span class="sxs-lookup"><span data-stu-id="cd685-161">To collect traces using `dotnet-trace`:</span></span>

- <span data-ttu-id="cd685-162">取得要從中收集追蹤的 .NET Core 應用程式的處理序識別碼（PID）。</span><span class="sxs-lookup"><span data-stu-id="cd685-162">Get the process identifier (PID) of the .NET Core application to collect traces from.</span></span>

  - <span data-ttu-id="cd685-163">例如，在 Windows 上，您可以使用 [工作管理員] 或 `tasklist` 命令。</span><span class="sxs-lookup"><span data-stu-id="cd685-163">On Windows, you can use Task Manager or the `tasklist` command, for example.</span></span>
  - <span data-ttu-id="cd685-164">例如，在 Linux 上為 `ps` 命令。</span><span class="sxs-lookup"><span data-stu-id="cd685-164">On Linux, for example, the `ps` command.</span></span>
  - [<span data-ttu-id="cd685-165">dotnet-追蹤 ps</span><span class="sxs-lookup"><span data-stu-id="cd685-165">dotnet-trace ps</span></span>](#dotnet-trace-ps)

- <span data-ttu-id="cd685-166">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="cd685-166">Run the following command:</span></span>

  ```console
  dotnet-trace collect --process-id <PID>
  ```

  <span data-ttu-id="cd685-167">上述命令會產生類似下列的輸出：</span><span class="sxs-lookup"><span data-stu-id="cd685-167">The preceding command generates output similar to the following:</span></span>

  ```console
  Press <Enter> to exit...
  Connecting to process: <Full-Path-To-Process-Being-Profiled>/dotnet.exe
  Collecting to file: <Full-Path-To-Trace>/trace.nettrace
  Session Id: <SessionId>
  Recording trace 721.025 (KB)
  ```

- <span data-ttu-id="cd685-168">按下鍵以停止收集 `<Enter>` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-168">Stop collection by pressing the `<Enter>` key.</span></span> <span data-ttu-id="cd685-169">`dotnet-trace`將會完成記錄事件至*nettrace*檔案。</span><span class="sxs-lookup"><span data-stu-id="cd685-169">`dotnet-trace` will finish logging events to the *trace.nettrace* file.</span></span>

## <a name="view-the-trace-captured-from-dotnet-trace"></a><span data-ttu-id="cd685-170">查看從 dotnet 所捕獲的追蹤</span><span class="sxs-lookup"><span data-stu-id="cd685-170">View the trace captured from dotnet-trace</span></span>

<span data-ttu-id="cd685-171">在 Windows 上，您可以在[PerfView](https://github.com/microsoft/perfview)上查看*nettrace*檔案以供分析：針對其他平臺上所收集的追蹤，追蹤檔案可以移至 Windows 機器，以在 PerfView 上查看。</span><span class="sxs-lookup"><span data-stu-id="cd685-171">On Windows, *.nettrace* files can be viewed on [PerfView](https://github.com/microsoft/perfview) for analysis: For traces collected on other platforms, the trace file can be moved to a Windows machine to be viewed on PerfView.</span></span>

<span data-ttu-id="cd685-172">在 Linux 上，您可以藉由將的輸出格式變更 `dotnet-trace` 為來查看追蹤 `speedscope` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-172">On Linux, the trace can be viewed by changing the output format of `dotnet-trace` to `speedscope`.</span></span> <span data-ttu-id="cd685-173">您可以使用選項來變更輸出檔案格式 `-f|--format` - `-f speedscope` 將會 `dotnet-trace` 產生檔案 `speedscope` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-173">The output file format can be changed using the `-f|--format` option - `-f speedscope` will make `dotnet-trace` produce a `speedscope` file.</span></span> <span data-ttu-id="cd685-174">您可以選擇 `nettrace` （預設選項）和 `speedscope` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-174">You can choose between `nettrace` (the default option) and `speedscope`.</span></span> <span data-ttu-id="cd685-175">`Speedscope`檔案可以在開啟 <https://www.speedscope.app> 。</span><span class="sxs-lookup"><span data-stu-id="cd685-175">`Speedscope` files can be opened at <https://www.speedscope.app>.</span></span>

> [!NOTE]
> <span data-ttu-id="cd685-176">.NET Core 執行時間會產生格式的追蹤 `nettrace` 。</span><span class="sxs-lookup"><span data-stu-id="cd685-176">The .NET Core runtime generates traces in the `nettrace` format.</span></span> <span data-ttu-id="cd685-177">追蹤完成後，追蹤會轉換成 speedscope （如果有指定的話）。</span><span class="sxs-lookup"><span data-stu-id="cd685-177">The traces are converted to speedscope (if specified) after the trace is completed.</span></span> <span data-ttu-id="cd685-178">由於某些轉換可能會導致資料遺失，因此原始檔案 `nettrace` 會保留在轉換後的檔案旁邊。</span><span class="sxs-lookup"><span data-stu-id="cd685-178">Since some conversions may result in loss of data, the original `nettrace` file is preserved next to the converted file.</span></span>

## <a name="use-dotnet-trace-to-collect-counter-values-over-time"></a><span data-ttu-id="cd685-179">使用 dotnet 追蹤來收集一段時間的計數器值</span><span class="sxs-lookup"><span data-stu-id="cd685-179">Use dotnet-trace to collect counter values over time</span></span>

<span data-ttu-id="cd685-180">`dotnet-trace`可以</span><span class="sxs-lookup"><span data-stu-id="cd685-180">`dotnet-trace` can:</span></span>

* <span data-ttu-id="cd685-181">用於 `EventCounter` 效能相關環境中的基本健全狀況監視。</span><span class="sxs-lookup"><span data-stu-id="cd685-181">Use `EventCounter` for basic health monitoring in performance-sensitive environments.</span></span> <span data-ttu-id="cd685-182">例如，在生產環境中。</span><span class="sxs-lookup"><span data-stu-id="cd685-182">For example, in production.</span></span>
* <span data-ttu-id="cd685-183">收集追蹤，讓它們不需要即時查看。</span><span class="sxs-lookup"><span data-stu-id="cd685-183">Collect traces so they don't need to be viewed in real time.</span></span>

<span data-ttu-id="cd685-184">例如，若要收集執行時間效能計數器值，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="cd685-184">For example, to collect runtime performance counter values, use the following command:</span></span>

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1
```

<span data-ttu-id="cd685-185">上述命令會告訴執行時間計數器每秒報告一次，以進行輕量的健全狀況監視。</span><span class="sxs-lookup"><span data-stu-id="cd685-185">The preceding command tells the runtime counters to report once every second for lightweight health monitoring.</span></span> <span data-ttu-id="cd685-186">取代 `EventCounterIntervalSec=1` 為較高的值（例如，60），可讓您在計數器資料中收集較小的追蹤。</span><span class="sxs-lookup"><span data-stu-id="cd685-186">Replacing `EventCounterIntervalSec=1` with a higher value (for example, 60) allows collection of a smaller trace with less granularity in the counter data.</span></span>

<span data-ttu-id="cd685-187">下列命令可減少額外負荷和追蹤大小，而不是上述其中一個：</span><span class="sxs-lookup"><span data-stu-id="cd685-187">The following command reduces overhead and trace size more than the preceding one:</span></span>

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1,Microsoft-Windows-DotNETRuntime:0:1,Microsoft-DotNETCore-SampleProfiler:0:1
```

<span data-ttu-id="cd685-188">上述命令會停用運行時間事件和 managed 堆疊 profiler。</span><span class="sxs-lookup"><span data-stu-id="cd685-188">The preceding command disables runtime events and the managed stack profiler.</span></span>

## <a name="net-providers"></a><span data-ttu-id="cd685-189">.NET 提供者</span><span class="sxs-lookup"><span data-stu-id="cd685-189">.NET Providers</span></span>

<span data-ttu-id="cd685-190">.NET Core 執行時間支援下列 .NET 提供者。</span><span class="sxs-lookup"><span data-stu-id="cd685-190">The .NET Core runtime supports the following .NET providers.</span></span> <span data-ttu-id="cd685-191">.NET Core 會使用相同的關鍵字來同時啟用 `Event Tracing for Windows (ETW)` 和 `EventPipe` 追蹤。</span><span class="sxs-lookup"><span data-stu-id="cd685-191">.NET Core uses the same keywords to enable both `Event Tracing for Windows (ETW)` and `EventPipe` traces.</span></span>

| <span data-ttu-id="cd685-192">提供者名稱</span><span class="sxs-lookup"><span data-stu-id="cd685-192">Provider name</span></span>                            | <span data-ttu-id="cd685-193">資訊</span><span class="sxs-lookup"><span data-stu-id="cd685-193">Information</span></span> |
|------------------------------------------|-------------|
| `Microsoft-Windows-DotNETRuntime`        | [<span data-ttu-id="cd685-194">執行階段提供者</span><span class="sxs-lookup"><span data-stu-id="cd685-194">The Runtime Provider</span></span>](../../framework/performance/clr-etw-providers.md#the-runtime-provider)<br>[<span data-ttu-id="cd685-195">CLR 執行時間關鍵字</span><span class="sxs-lookup"><span data-stu-id="cd685-195">CLR Runtime Keywords</span></span>](../../framework/performance/clr-etw-keywords-and-levels.md#runtime) |
| `Microsoft-Windows-DotNETRuntimeRundown` | [<span data-ttu-id="cd685-196">取消提供者</span><span class="sxs-lookup"><span data-stu-id="cd685-196">The Rundown Provider</span></span>](../../framework/performance/clr-etw-providers.md#the-rundown-provider)<br>[<span data-ttu-id="cd685-197">CLR 取消關鍵字</span><span class="sxs-lookup"><span data-stu-id="cd685-197">CLR Rundown Keywords</span></span>](../../framework/performance/clr-etw-keywords-and-levels.md#rundown) |
| `Microsoft-DotNETCore-SampleProfiler`    | <span data-ttu-id="cd685-198">啟用範例 profiler。</span><span class="sxs-lookup"><span data-stu-id="cd685-198">Enables the sample profiler.</span></span> |
