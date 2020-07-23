---
title: 診斷工具概觀 - .NET Core
description: 可用來診斷 .NET Core 應用程式之工具與技術的概觀。
ms.date: 07/16/2020
ms.topic: overview
ms.openlocfilehash: dc64c03ee9c8cee6a5b3c5cc089b4a1a2c27f84a
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86924778"
---
# <a name="what-diagnostic-tools-are-available-in-net-core"></a><span data-ttu-id="6a39a-103">.NET Core 中有哪些診斷工具可供使用？</span><span class="sxs-lookup"><span data-stu-id="6a39a-103">What diagnostic tools are available in .NET Core?</span></span>

<span data-ttu-id="6a39a-104">軟體不一定會如您預期般地運作，但是 .NET Core 具有可協助您迅速且有效地診斷這些問題的工具與 API。</span><span class="sxs-lookup"><span data-stu-id="6a39a-104">Software doesn't always behave as you would expect, but .NET Core has tools and APIs that will help you diagnose these issues quickly and effectively.</span></span>

<span data-ttu-id="6a39a-105">此文章會協助您找出所需的各種工具。</span><span class="sxs-lookup"><span data-stu-id="6a39a-105">This article helps you find the various tools you need.</span></span>

## <a name="managed-debuggers"></a><span data-ttu-id="6a39a-106">受控偵錯工具</span><span class="sxs-lookup"><span data-stu-id="6a39a-106">Managed debuggers</span></span>

<span data-ttu-id="6a39a-107">[受管理的調試](managed-debuggers.md)程式可讓您與程式互動。</span><span class="sxs-lookup"><span data-stu-id="6a39a-107">[Managed debuggers](managed-debuggers.md) allow you to interact with your program.</span></span> <span data-ttu-id="6a39a-108">暫停、以累加方式執行、檢查及繼續等功能，可讓您取得您程式碼行為的見解。</span><span class="sxs-lookup"><span data-stu-id="6a39a-108">Pausing, incrementally executing, examining,  and resuming gives you insight into the behavior of your code.</span></span> <span data-ttu-id="6a39a-109">偵錯工具是診斷可輕易重現之功能性問題的第一個選擇。</span><span class="sxs-lookup"><span data-stu-id="6a39a-109">A debugger is the first choice for diagnosing functional problems that can be easily reproduced.</span></span>

## <a name="logging-and-tracing"></a><span data-ttu-id="6a39a-110">記錄和追蹤</span><span class="sxs-lookup"><span data-stu-id="6a39a-110">Logging and tracing</span></span>

<span data-ttu-id="6a39a-111">[記錄和追蹤](logging-tracing.md)是相關的技術。</span><span class="sxs-lookup"><span data-stu-id="6a39a-111">[Logging and tracing](logging-tracing.md) are related techniques.</span></span> <span data-ttu-id="6a39a-112">它們會參考檢測程式碼以建立記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6a39a-112">They refer to instrumenting code to create log files.</span></span> <span data-ttu-id="6a39a-113">那些檔案會記錄程式所執行之內容的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6a39a-113">The files record the details of what a program does.</span></span> <span data-ttu-id="6a39a-114">這些詳細資料可用來診斷最為複雜的問題。</span><span class="sxs-lookup"><span data-stu-id="6a39a-114">These details can be used to diagnose the most complex problems.</span></span> <span data-ttu-id="6a39a-115">透過與時間戳記結合，這些技術在調查效能方面的問題上也非常有用。</span><span class="sxs-lookup"><span data-stu-id="6a39a-115">When combined with time stamps, these techniques are also valuable in performance investigations.</span></span>

## <a name="unit-testing"></a><span data-ttu-id="6a39a-116">單元測試</span><span class="sxs-lookup"><span data-stu-id="6a39a-116">Unit testing</span></span>

<span data-ttu-id="6a39a-117">[單元測試](../testing/index.md)是持續整合和部署高品質軟體的重要元件。</span><span class="sxs-lookup"><span data-stu-id="6a39a-117">[Unit testing](../testing/index.md) is a key component of continuous integration and deployment of high-quality software.</span></span> <span data-ttu-id="6a39a-118">單元測試的設計是要在您中斷某個項目時提前警告您。</span><span class="sxs-lookup"><span data-stu-id="6a39a-118">Unit tests are designed to give you an early warning when you break something.</span></span>

## <a name="net-core-dotnet-diagnostic-global-tools"></a><span data-ttu-id="6a39a-119">.NET Core dotnet 診斷通用工具</span><span class="sxs-lookup"><span data-stu-id="6a39a-119">.NET Core dotnet diagnostic Global Tools</span></span>

### <a name="dotnet-counters"></a><span data-ttu-id="6a39a-120">dotnet-counters</span><span class="sxs-lookup"><span data-stu-id="6a39a-120">dotnet-counters</span></span>

<span data-ttu-id="6a39a-121">[dotnet-計數器](dotnet-counters.md)是效能監視工具，可進行第一層健全狀況監視和效能調查。</span><span class="sxs-lookup"><span data-stu-id="6a39a-121">[dotnet-counters](dotnet-counters.md) is a performance monitoring tool for first-level health monitoring and performance investigation.</span></span> <span data-ttu-id="6a39a-122">它會觀察透過 API 發佈的效能計數器值 <xref:System.Diagnostics.Tracing.EventCounter> 。</span><span class="sxs-lookup"><span data-stu-id="6a39a-122">It observes performance counter values published via the <xref:System.Diagnostics.Tracing.EventCounter> API.</span></span> <span data-ttu-id="6a39a-123">例如，您可以快速監視 CPU 使用率，或 .NET Core 應用程式中擲回的例外狀況率等事項。</span><span class="sxs-lookup"><span data-stu-id="6a39a-123">For example, you can quickly monitor things like the CPU usage or the rate of exceptions being thrown in your .NET Core application.</span></span>

### <a name="dotnet-dump"></a><span data-ttu-id="6a39a-124">dotnet-dump</span><span class="sxs-lookup"><span data-stu-id="6a39a-124">dotnet-dump</span></span>

<span data-ttu-id="6a39a-125">[Dotnet](dotnet-dump.md)傾印工具是在不使用原生偵錯工具的情況下，收集和分析 Windows 和 Linux 核心傾印的方式。</span><span class="sxs-lookup"><span data-stu-id="6a39a-125">The [dotnet-dump](dotnet-dump.md) tool is a way to collect and analyze Windows and Linux core dumps without a native debugger.</span></span>

### <a name="dotnet-trace"></a><span data-ttu-id="6a39a-126">dotnet-trace</span><span class="sxs-lookup"><span data-stu-id="6a39a-126">dotnet-trace</span></span>

<span data-ttu-id="6a39a-127">.NET Core 包含 `EventPipe` 要在其中公開診斷資料的呼叫。</span><span class="sxs-lookup"><span data-stu-id="6a39a-127">.NET Core includes what is called the `EventPipe` through which diagnostics data is exposed.</span></span> <span data-ttu-id="6a39a-128">[Dotnet 追蹤](dotnet-trace.md)工具可讓您從應用程式取用有趣的分析資料，以在需要執行速度緩慢的根本原因應用程式時提供協助。</span><span class="sxs-lookup"><span data-stu-id="6a39a-128">The [dotnet-trace](dotnet-trace.md) tool allows you to consume interesting profiling data from your app that can help in scenarios where you need to root cause apps running slow.</span></span>

## <a name="net-core-diagnostics-tutorials"></a><span data-ttu-id="6a39a-129">.NET Core 診斷教學課程</span><span class="sxs-lookup"><span data-stu-id="6a39a-129">.NET Core diagnostics tutorials</span></span>

### <a name="debug-a-memory-leak"></a><span data-ttu-id="6a39a-130">針對記憶體流失進行偵錯</span><span class="sxs-lookup"><span data-stu-id="6a39a-130">Debug a memory leak</span></span>

<span data-ttu-id="6a39a-131">[教學課程：偵測記憶體](debug-memory-leak.md)流失會逐步解說找出記憶體流失的情況。</span><span class="sxs-lookup"><span data-stu-id="6a39a-131">[Tutorial: Debug a memory leak](debug-memory-leak.md) walks through finding a memory leak.</span></span> <span data-ttu-id="6a39a-132">[Dotnet 計數器](dotnet-counters.md)工具是用來確認流失，而[dotnet](dotnet-dump.md)傾印工具是用來診斷遺漏的問題。</span><span class="sxs-lookup"><span data-stu-id="6a39a-132">The [dotnet-counters](dotnet-counters.md) tool is used to confirm the leak and the [dotnet-dump](dotnet-dump.md) tool is used to diagnose the leak.</span></span>

### <a name="debug-high-cpu-usage"></a><span data-ttu-id="6a39a-133">高 CPU 使用率的調試</span><span class="sxs-lookup"><span data-stu-id="6a39a-133">Debug high CPU usage</span></span>

<span data-ttu-id="6a39a-134">[教學課程：高 cpu 使用量](debug-highcpu.md)的檢查會逐步引導您調查高 cpu 使用量。</span><span class="sxs-lookup"><span data-stu-id="6a39a-134">[Tutorial: Debug high CPU usage](debug-highcpu.md) walks you through investigating high CPU usage.</span></span> <span data-ttu-id="6a39a-135">它會使用[dotnet 計數器](dotnet-counters.md)工具來確認高 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="6a39a-135">It uses the [dotnet-counters](dotnet-counters.md) tool to confirm the high CPU usage.</span></span> <span data-ttu-id="6a39a-136">接著，它會逐步引導您使用[效能分析公用程式（ `dotnet-trace` ）或 Linux 的追蹤](dotnet-trace.md) `perf` 來收集和查看 CPU 使用量設定檔。</span><span class="sxs-lookup"><span data-stu-id="6a39a-136">It then walks you through using [Trace for performance analysis utility (`dotnet-trace`)](dotnet-trace.md) or Linux `perf` to collect and view CPU usage profile.</span></span>

### <a name="debug-deadlock"></a><span data-ttu-id="6a39a-137">Debug 鎖死</span><span class="sxs-lookup"><span data-stu-id="6a39a-137">Debug deadlock</span></span>

<span data-ttu-id="6a39a-138">[教學課程： Debug 鎖死](debug-deadlock.md)會顯示如何使用[dotnet](dotnet-dump.md)傾印工具來調查執行緒和鎖定。</span><span class="sxs-lookup"><span data-stu-id="6a39a-138">[Tutorial: Debug deadlock](debug-deadlock.md) shows you how to use the [dotnet-dump](dotnet-dump.md) tool to investigate threads and locks.</span></span>
