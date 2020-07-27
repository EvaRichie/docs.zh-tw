---
title: .NET 字彙表
description: 了解 .NET 文件中所使用之特定詞彙的意義。
ms.date: 01/22/2019
ms.technology: dotnet-standard
ms.openlocfilehash: 529b1d9142ddf7982a6712c355c10666f0414d73
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87163123"
---
# <a name="net-glossary"></a><span data-ttu-id="19d82-103">.NET 字彙表</span><span class="sxs-lookup"><span data-stu-id="19d82-103">.NET Glossary</span></span>

<span data-ttu-id="19d82-104">此字彙表的主要目標是釐清經常出現在 .NET 文件中但沒有定義之特定詞彙和縮略字的意義。</span><span class="sxs-lookup"><span data-stu-id="19d82-104">The primary goal of this glossary is to clarify meanings of selected terms and acronyms that appear frequently in the .NET documentation without definitions.</span></span>

## <a name="aot"></a><span data-ttu-id="19d82-105">AOT</span><span class="sxs-lookup"><span data-stu-id="19d82-105">AOT</span></span>

<span data-ttu-id="19d82-106">預先編譯器。</span><span class="sxs-lookup"><span data-stu-id="19d82-106">Ahead-of-time compiler.</span></span>

<span data-ttu-id="19d82-107">此編譯器類似於 [JIT](#jit)，也會將 [IL](#il) 轉譯成機器碼。</span><span class="sxs-lookup"><span data-stu-id="19d82-107">Similar to [JIT](#jit), this compiler also translates [IL](#il) to machine code.</span></span> <span data-ttu-id="19d82-108">相較於 JIT 編譯，AOT 編譯會在執行應用程式之前發生，而且通常會在不同的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="19d82-108">In contrast to JIT compilation, AOT compilation happens before the application is executed and is usually performed on a different machine.</span></span> <span data-ttu-id="19d82-109">因為 AOT 工具鏈不會在執行時間編譯，所以不需要將花費在編譯的時間降到最低。</span><span class="sxs-lookup"><span data-stu-id="19d82-109">Because AOT tool chains don't compile at run time, they don't have to minimize time spent compiling.</span></span> <span data-ttu-id="19d82-110">這表示它們可以花更多的時間在最佳化。</span><span class="sxs-lookup"><span data-stu-id="19d82-110">That means they can spend more time optimizing.</span></span> <span data-ttu-id="19d82-111">由於 AOT 的內容是整個應用程式，因此 AOT 編譯器也會執行跨模組連結和整個程式分析，這表示會追蹤所有參考並產生單一可執行檔。</span><span class="sxs-lookup"><span data-stu-id="19d82-111">Since the context of AOT is the entire application, the AOT compiler also performs cross-module linking and whole-program analysis, which means that all references are followed and a single executable is produced.</span></span>

<span data-ttu-id="19d82-112">請參閱 [CoreRT](#corert) 及 [.NET Native](#net-native)。</span><span class="sxs-lookup"><span data-stu-id="19d82-112">See [CoreRT](#corert) and [.NET Native](#net-native).</span></span>

## <a name="aspnet"></a><span data-ttu-id="19d82-113">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="19d82-113">ASP.NET</span></span>

<span data-ttu-id="19d82-114">隨附於 .NET Framework 的原始 ASP.NET 實作。</span><span class="sxs-lookup"><span data-stu-id="19d82-114">The original ASP.NET implementation that ships with the .NET Framework.</span></span>

<span data-ttu-id="19d82-115">有時 ASP.NET 是指包括 ASP.NET Core 在內之兩個 ASP.NET 實作的籠統名詞。</span><span class="sxs-lookup"><span data-stu-id="19d82-115">Sometimes ASP.NET is an umbrella term that refers to both ASP.NET implementations including ASP.NET Core.</span></span> <span data-ttu-id="19d82-116">該詞彙在任何指定的執行個體中所代表的意義取決於內容。</span><span class="sxs-lookup"><span data-stu-id="19d82-116">The meaning that the term carries in any given instance is determined by context.</span></span> <span data-ttu-id="19d82-117">當您想要清楚指出您不是使用 ASP.NET 來表示這兩個實作為時，請參閱 ASP.NET 4.x。</span><span class="sxs-lookup"><span data-stu-id="19d82-117">Refer to ASP.NET 4.x when you want to make it clear that you're not using ASP.NET to mean both implementations.</span></span>

<span data-ttu-id="19d82-118">請參閱 [ASP.NET 文件](/aspnet/#pivot=aspnet)。</span><span class="sxs-lookup"><span data-stu-id="19d82-118">See [ASP.NET documentation](/aspnet/#pivot=aspnet).</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="19d82-119">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="19d82-119">ASP.NET Core</span></span>

<span data-ttu-id="19d82-120">以 .NET Core 為基礎之 ASP.NET 的跨平臺、高效能、開放原始碼的執行。</span><span class="sxs-lookup"><span data-stu-id="19d82-120">A cross-platform, high-performance, open-source implementation of ASP.NET built on .NET Core.</span></span>

<span data-ttu-id="19d82-121">請參閱 [ASP.NET Core 文件](/aspnet/#pivot=core)。</span><span class="sxs-lookup"><span data-stu-id="19d82-121">See [ASP.NET Core documentation](/aspnet/#pivot=core).</span></span>

## <a name="assembly"></a><span data-ttu-id="19d82-122">組件 (assembly)</span><span class="sxs-lookup"><span data-stu-id="19d82-122">assembly</span></span>

<span data-ttu-id="19d82-123">*.Dll* / *.exe*檔案，其中包含可由應用程式或其他元件呼叫的 api 集合。</span><span class="sxs-lookup"><span data-stu-id="19d82-123">A *.dll*/*.exe* file that can contain a collection of APIs that can be called by applications or other assemblies.</span></span>

<span data-ttu-id="19d82-124">一個組件可以包含介面、類別、結構、列舉和委派等類型。</span><span class="sxs-lookup"><span data-stu-id="19d82-124">An assembly may include types such as interfaces, classes, structures, enumerations, and delegates.</span></span> <span data-ttu-id="19d82-125">專案的 *bin* 資料夾中的組件有時稱為「二進位檔」\*\*。</span><span class="sxs-lookup"><span data-stu-id="19d82-125">Assemblies in a project's *bin* folder are sometimes referred to as *binaries*.</span></span> <span data-ttu-id="19d82-126">另請參閱[程式庫](#library)。</span><span class="sxs-lookup"><span data-stu-id="19d82-126">See also [library](#library).</span></span>

## <a name="clr"></a><span data-ttu-id="19d82-127">CLR</span><span class="sxs-lookup"><span data-stu-id="19d82-127">CLR</span></span>

<span data-ttu-id="19d82-128">Common Language Runtime。</span><span class="sxs-lookup"><span data-stu-id="19d82-128">Common Language Runtime.</span></span>

<span data-ttu-id="19d82-129">確切意義取決於內容，但通用語言執行時間通常是指 .NET Framework 的執行時間。</span><span class="sxs-lookup"><span data-stu-id="19d82-129">The exact meaning depends on the context, but Common Language Runtime usually refers to the runtime of .NET Framework.</span></span> <span data-ttu-id="19d82-130">CLR 會處理記憶體配置和管理。</span><span class="sxs-lookup"><span data-stu-id="19d82-130">The CLR handles memory allocation and management.</span></span> <span data-ttu-id="19d82-131">CLR 也是虛擬機器，不僅會執行應用程式，也會使用[JIT](#jit)編譯器即時產生和編譯器代碼。</span><span class="sxs-lookup"><span data-stu-id="19d82-131">The CLR is also a virtual machine that not only executes apps but also generates and compiles code on-the-fly using a [JIT](#jit) compiler.</span></span> <span data-ttu-id="19d82-132">目前的 Microsoft CLR 實作僅限 Windows。</span><span class="sxs-lookup"><span data-stu-id="19d82-132">The current Microsoft CLR implementation is Windows only.</span></span>

## <a name="coreclr"></a><span data-ttu-id="19d82-133">CoreCLR</span><span class="sxs-lookup"><span data-stu-id="19d82-133">CoreCLR</span></span>

<span data-ttu-id="19d82-134">.NET Core Common Language Runtime。</span><span class="sxs-lookup"><span data-stu-id="19d82-134">.NET Core Common Language Runtime.</span></span>

<span data-ttu-id="19d82-135">此 CLR 是從與 CLR 相同的程式碼基底所建置。</span><span class="sxs-lookup"><span data-stu-id="19d82-135">This CLR is built from the same code base as the CLR.</span></span> <span data-ttu-id="19d82-136">一開始，CoreCLR 是 Silverlight 的執行階段，其設計目的是為了在多個平台上執行，特別是 Windows 和 OS X。CoreCLR 現在是 .NET Core 的一部分，代表 CLR 的簡化版本。</span><span class="sxs-lookup"><span data-stu-id="19d82-136">Originally, CoreCLR was the runtime of Silverlight and was designed to run on multiple platforms, specifically Windows and OS X. CoreCLR is now part of .NET Core and represents a simplified version of the CLR.</span></span> <span data-ttu-id="19d82-137">它仍然是[跨平台](#cross-platform)執行階段，現在支援許多 Linux 發行版本。</span><span class="sxs-lookup"><span data-stu-id="19d82-137">It's still a [cross-platform](#cross-platform) runtime, now including support for many Linux distributions.</span></span> <span data-ttu-id="19d82-138">CoreCLR 也是具有 JIT 和程式碼執行功能的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="19d82-138">CoreCLR is also a virtual machine with JIT and code execution capabilities.</span></span>

## <a name="corefx"></a><span data-ttu-id="19d82-139">CoreFx</span><span class="sxs-lookup"><span data-stu-id="19d82-139">CoreFx</span></span>

<span data-ttu-id="19d82-140">.NET Core 基底類別庫 (BCL)</span><span class="sxs-lookup"><span data-stu-id="19d82-140">.NET Core Base Class Library (BCL)</span></span>

> [!TIP]
> <span data-ttu-id="19d82-141">*Fx*代表*架構*。</span><span class="sxs-lookup"><span data-stu-id="19d82-141">*Fx* stands for *framework*.</span></span>

<span data-ttu-id="19d82-142">組成系統的一組程式庫。 \*（以及 Microsoft 的有限範圍）。 \*命名空間.</span><span class="sxs-lookup"><span data-stu-id="19d82-142">A set of libraries that comprise the System.\* (and to a limited extent Microsoft.\*) namespaces.</span></span> <span data-ttu-id="19d82-143">BCL 是 ASP.NET Core 等較高層級的應用程式架構建置所在之較低層級的一般目的架構。</span><span class="sxs-lookup"><span data-stu-id="19d82-143">The BCL is a general purpose, lower-level framework that higher-level application frameworks, such as ASP.NET Core, build on.</span></span> <span data-ttu-id="19d82-144">.Net Core BCL 的原始程式碼包含在[.Net core 運行](https://github.com/dotnet/runtime)時間存放庫中。</span><span class="sxs-lookup"><span data-stu-id="19d82-144">The source code of the .NET Core BCL is contained in the [.NET Core runtime repository](https://github.com/dotnet/runtime).</span></span> <span data-ttu-id="19d82-145">不過，大多數的 .NET Core API 也適用於 .NET Framework；因此您可以將 CoreFX 視為 .NET Framework BCL 的分支。</span><span class="sxs-lookup"><span data-stu-id="19d82-145">However, the majority of the .NET Core APIs are also available in the .NET Framework, so you can think of CoreFX as a fork of the .NET Framework BCL.</span></span>

## <a name="corert"></a><span data-ttu-id="19d82-146">CoreRT</span><span class="sxs-lookup"><span data-stu-id="19d82-146">CoreRT</span></span>

<span data-ttu-id="19d82-147">.NET Core 執行階段。</span><span class="sxs-lookup"><span data-stu-id="19d82-147">.NET Core runtime.</span></span>

<span data-ttu-id="19d82-148">相較於 CLR/CoreCLR，CoreRT 不是虛擬機器，這表示它不會包含即時產生和執行程式碼的功能，因為它不包含 [JIT](#jit)。</span><span class="sxs-lookup"><span data-stu-id="19d82-148">In contrast to the CLR/CoreCLR, CoreRT is not a virtual machine, which means it doesn't include the facilities to generate and run code on-the-fly because it doesn't include a [JIT](#jit).</span></span> <span data-ttu-id="19d82-149">不過，它會包含[GC](#gc)以及執行時間類型識別（RTTI）和反映的功能。</span><span class="sxs-lookup"><span data-stu-id="19d82-149">It does, however, include the [GC](#gc) and the ability for run-time type identification (RTTI) and reflection.</span></span> <span data-ttu-id="19d82-150">不過，其型別系統已設計成不需要反映的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="19d82-150">However, its type system is designed so that metadata for reflection isn't required.</span></span> <span data-ttu-id="19d82-151">不需要中繼資料，可讓[AOT](#aot)工具鏈連結掉不必要的中繼資料，而且更重要的是識別應用程式不會使用的程式碼。</span><span class="sxs-lookup"><span data-stu-id="19d82-151">Not requiring metadata enables having an [AOT](#aot) tool chain that can link away superfluous metadata and (more importantly) identify code that the app doesn't use.</span></span> <span data-ttu-id="19d82-152">CoreRT 正在開發中。</span><span class="sxs-lookup"><span data-stu-id="19d82-152">CoreRT is in development.</span></span>

<span data-ttu-id="19d82-153">請參閱[.NET Native 和 CoreRT 的簡介](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md)。</span><span class="sxs-lookup"><span data-stu-id="19d82-153">See [Intro to .NET Native and CoreRT](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md).</span></span>

## <a name="cross-platform"></a><span data-ttu-id="19d82-154">跨平台</span><span class="sxs-lookup"><span data-stu-id="19d82-154">cross-platform</span></span>

<span data-ttu-id="19d82-155">能夠開發和執行可在多個不同的作業系統（例如 Linux、Windows 和 iOS）上使用的應用程式，而不需要特別針對每一種作業系統進行重寫。</span><span class="sxs-lookup"><span data-stu-id="19d82-155">The ability to develop and execute an application that can be used on multiple different operating systems, such as Linux, Windows, and iOS, without having to rewrite specifically for each one.</span></span> <span data-ttu-id="19d82-156">這可讓程式碼重複使用，以及不同平臺上的應用程式之間的一致性。</span><span class="sxs-lookup"><span data-stu-id="19d82-156">This enables code reuse and consistency between applications on different platforms.</span></span>

## <a name="ecosystem"></a><span data-ttu-id="19d82-157">生態系統</span><span class="sxs-lookup"><span data-stu-id="19d82-157">ecosystem</span></span>

<span data-ttu-id="19d82-158">用來建置及執行適用於指定技術之應用程式的所有執行階段軟體、開發工具和社群資源。</span><span class="sxs-lookup"><span data-stu-id="19d82-158">All of the runtime software, development tools, and community resources that are used to build and run applications for a given technology.</span></span>

<span data-ttu-id="19d82-159">「.NET 生態系統」一詞與「.NET 堆疊」等類似詞彙的不同之處在於，前者包含協力廠商應用程式和程式庫。</span><span class="sxs-lookup"><span data-stu-id="19d82-159">The term ".NET ecosystem" differs from similar terms such as ".NET stack" in its inclusion of third-party apps and libraries.</span></span> <span data-ttu-id="19d82-160">以下是用於句子中的範例：</span><span class="sxs-lookup"><span data-stu-id="19d82-160">Here's an example in a sentence:</span></span>

- <span data-ttu-id="19d82-161">「[.NET Standard](#net-standard) 背後的動機是在 .NET 生態系統中建立更高的一致性。」</span><span class="sxs-lookup"><span data-stu-id="19d82-161">"The motivation behind the [.NET Standard](#net-standard) is to establish greater uniformity in the .NET ecosystem."</span></span>

## <a name="framework"></a><span data-ttu-id="19d82-162">架構</span><span class="sxs-lookup"><span data-stu-id="19d82-162">framework</span></span>

<span data-ttu-id="19d82-163">一般而言，一組功能齊全的 API 可加快開發和部署以特定技術為基礎的應用程式。</span><span class="sxs-lookup"><span data-stu-id="19d82-163">In general, a comprehensive collection of APIs that facilitates development and deployment of applications that are based on a particular technology.</span></span> <span data-ttu-id="19d82-164">ASP.NET Core 和 Windows Forms 即為此一般意義的應用程式架構範例。</span><span class="sxs-lookup"><span data-stu-id="19d82-164">In this general sense, ASP.NET Core and Windows Forms are examples of application frameworks.</span></span> <span data-ttu-id="19d82-165">另請參閱[程式庫](#library)。</span><span class="sxs-lookup"><span data-stu-id="19d82-165">See also [library](#library).</span></span>

<span data-ttu-id="19d82-166">「架構」一字在下列詞彙中有更特定的技術意義：</span><span class="sxs-lookup"><span data-stu-id="19d82-166">The word "framework" has a more specific technical meaning in the following terms:</span></span>

- [<span data-ttu-id="19d82-167">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="19d82-167">.NET Framework</span></span>](#net-framework)
- [<span data-ttu-id="19d82-168">目標 framework</span><span class="sxs-lookup"><span data-stu-id="19d82-168">target framework</span></span>](#target-framework)
- [<span data-ttu-id="19d82-169">TFM (目標 Framework Moniker)</span><span class="sxs-lookup"><span data-stu-id="19d82-169">TFM (target framework moniker)</span></span>](#tfm)

<span data-ttu-id="19d82-170">在現有的文件中，「架構」有時是指 [.NET 實作](#implementation-of-net)。</span><span class="sxs-lookup"><span data-stu-id="19d82-170">In the existing documentation, "framework" sometimes refers to an [implementation of .NET](#implementation-of-net).</span></span> <span data-ttu-id="19d82-171">例如，某篇文章可能會將 .NET Core 稱為架構。</span><span class="sxs-lookup"><span data-stu-id="19d82-171">For example, an article may call .NET Core a framework.</span></span> <span data-ttu-id="19d82-172">我們計劃從文件中排除這個令人混淆的用法。</span><span class="sxs-lookup"><span data-stu-id="19d82-172">We plan to eliminate this confusing usage from the documentation.</span></span>

## <a name="gc"></a><span data-ttu-id="19d82-173">GC</span><span class="sxs-lookup"><span data-stu-id="19d82-173">GC</span></span>

<span data-ttu-id="19d82-174">記憶體回收行程。</span><span class="sxs-lookup"><span data-stu-id="19d82-174">Garbage collector.</span></span>

<span data-ttu-id="19d82-175">記憶體回收行程是自動記憶體管理的實作。</span><span class="sxs-lookup"><span data-stu-id="19d82-175">The garbage collector is an implementation of automatic memory management.</span></span>  <span data-ttu-id="19d82-176">GC 會釋放不再使用之物件所佔用的記憶體。</span><span class="sxs-lookup"><span data-stu-id="19d82-176">The GC frees memory occupied by objects that are no longer in use.</span></span>

<span data-ttu-id="19d82-177">請參閱[記憶體回收](garbage-collection/index.md)。</span><span class="sxs-lookup"><span data-stu-id="19d82-177">See [Garbage Collection](garbage-collection/index.md).</span></span>

## <a name="il"></a><span data-ttu-id="19d82-178">IL</span><span class="sxs-lookup"><span data-stu-id="19d82-178">IL</span></span>

<span data-ttu-id="19d82-179">中繼語言。</span><span class="sxs-lookup"><span data-stu-id="19d82-179">Intermediate language.</span></span>

<span data-ttu-id="19d82-180">較高階的 .NET 語言 (例如 C#) 可向下編譯成硬體無從驗證的指令集，稱為中繼語言 (IL)。</span><span class="sxs-lookup"><span data-stu-id="19d82-180">Higher-level .NET languages, such as C#, compile down to a hardware-agnostic instruction set, which is called Intermediate Language (IL).</span></span> <span data-ttu-id="19d82-181">IL 有時稱為 MSIL (Microsoft IL) 或 CIL (Common IL)。</span><span class="sxs-lookup"><span data-stu-id="19d82-181">IL is sometimes referred to as MSIL (Microsoft IL) or CIL (Common IL).</span></span>

## <a name="jit"></a><span data-ttu-id="19d82-182">JIT</span><span class="sxs-lookup"><span data-stu-id="19d82-182">JIT</span></span>

<span data-ttu-id="19d82-183">Just-in-Time 編譯器。</span><span class="sxs-lookup"><span data-stu-id="19d82-183">Just-in-time compiler.</span></span>

<span data-ttu-id="19d82-184">此編譯器類似於 [AOT](#aot)，會將 [IL](#il) 轉譯成處理器了解的機器碼。</span><span class="sxs-lookup"><span data-stu-id="19d82-184">Similar to [AOT](#aot), this compiler translates [IL](#il) to machine code that the processor understands.</span></span> <span data-ttu-id="19d82-185">不同於 AOT，JIT 編譯會視需要發生，而且會在必須執行程式碼的相同電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="19d82-185">Unlike AOT, JIT compilation happens on demand and is performed on the same machine that the code needs to run on.</span></span> <span data-ttu-id="19d82-186">由於 JIT 編譯會在應用程式執行期間發生，因此編譯時間會是執行階段的一部分。</span><span class="sxs-lookup"><span data-stu-id="19d82-186">Since JIT compilation occurs during execution of the application, compile time is part of the run time.</span></span> <span data-ttu-id="19d82-187">因此，JIT 編譯器必須在最佳化程式碼所花費的時間與結果程式碼可能省下的時間之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="19d82-187">Thus, JIT compilers have to balance time spent optimizing code against the savings that the resulting code can produce.</span></span> <span data-ttu-id="19d82-188">但 JIT 知道實際硬體，因此開發人員不需要提供不同的實作。</span><span class="sxs-lookup"><span data-stu-id="19d82-188">But a JIT knows the actual hardware and can free developers from having to ship different implementations.</span></span>

## <a name="implementation-of-net"></a><span data-ttu-id="19d82-189">.NET 實作</span><span class="sxs-lookup"><span data-stu-id="19d82-189">implementation of .NET</span></span>

<span data-ttu-id="19d82-190">.NET 的執行包括：</span><span class="sxs-lookup"><span data-stu-id="19d82-190">An implementation of .NET includes:</span></span>

- <span data-ttu-id="19d82-191">一或多個執行階段。</span><span class="sxs-lookup"><span data-stu-id="19d82-191">One or more runtimes.</span></span> <span data-ttu-id="19d82-192">範例：CLR、CoreCLR、CoreRT。</span><span class="sxs-lookup"><span data-stu-id="19d82-192">Examples: CLR, CoreCLR, CoreRT.</span></span>
- <span data-ttu-id="19d82-193">實作 .NET Standard 版本並可能包含其他 API 的類別庫。</span><span class="sxs-lookup"><span data-stu-id="19d82-193">A class library that implements a version of the .NET Standard and may include additional APIs.</span></span> <span data-ttu-id="19d82-194">範例：.NET Framework 基底類別庫、.NET Core 基底類別庫。</span><span class="sxs-lookup"><span data-stu-id="19d82-194">Examples: .NET Framework Base Class Library, .NET Core Base Class Library.</span></span>
- <span data-ttu-id="19d82-195">(選擇性) 一或多個應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="19d82-195">Optionally, one or more application frameworks.</span></span> <span data-ttu-id="19d82-196">範例：ASP.NET、Windows Forms 和 WPF 會包含在 .NET Framework 中。</span><span class="sxs-lookup"><span data-stu-id="19d82-196">Examples: ASP.NET, Windows Forms, and WPF are included in the .NET Framework.</span></span>
- <span data-ttu-id="19d82-197">(選擇性) 開發工具。</span><span class="sxs-lookup"><span data-stu-id="19d82-197">Optionally, development tools.</span></span> <span data-ttu-id="19d82-198">某些開發工具可在多個實作之間共用。</span><span class="sxs-lookup"><span data-stu-id="19d82-198">Some development tools are shared among multiple implementations.</span></span>

<span data-ttu-id="19d82-199">.NET 實作的範例：</span><span class="sxs-lookup"><span data-stu-id="19d82-199">Examples of .NET implementations:</span></span>

- [<span data-ttu-id="19d82-200">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="19d82-200">.NET Framework</span></span>](#net-framework)
- [<span data-ttu-id="19d82-201">.NET Core</span><span class="sxs-lookup"><span data-stu-id="19d82-201">.NET Core</span></span>](#net-core)
- [<span data-ttu-id="19d82-202">通用 Windows 平台 (UWP)</span><span class="sxs-lookup"><span data-stu-id="19d82-202">Universal Windows Platform (UWP)</span></span>](#uwp)

## <a name="library"></a><span data-ttu-id="19d82-203">圖書館</span><span class="sxs-lookup"><span data-stu-id="19d82-203">library</span></span>

<span data-ttu-id="19d82-204">可由應用程式或其他程式庫呼叫的 API 集合。</span><span class="sxs-lookup"><span data-stu-id="19d82-204">A collection of APIs that can be called by apps or other libraries.</span></span> <span data-ttu-id="19d82-205">.NET 程式庫是由一或多個[組件](#assembly)組成。</span><span class="sxs-lookup"><span data-stu-id="19d82-205">A .NET library is composed of one or more [assemblies](#assembly).</span></span>

<span data-ttu-id="19d82-206">程式庫和[架構](#framework)等字在使用時通常同義。</span><span class="sxs-lookup"><span data-stu-id="19d82-206">The words library and [framework](#framework) are often used synonymously.</span></span>

## <a name="metapackage"></a><span data-ttu-id="19d82-207">中繼套件</span><span class="sxs-lookup"><span data-stu-id="19d82-207">metapackage</span></span>

<span data-ttu-id="19d82-208">沒有自己的程式庫，而只是一份相依性清單的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="19d82-208">A NuGet package that has no library of its own but is only a list of dependencies.</span></span> <span data-ttu-id="19d82-209">內含的套件可以選擇性地建立目標 Framework 的 API。</span><span class="sxs-lookup"><span data-stu-id="19d82-209">The included packages can optionally establish the API for a target framework.</span></span>

## <a name="mono"></a><span data-ttu-id="19d82-210">單聲道</span><span class="sxs-lookup"><span data-stu-id="19d82-210">Mono</span></span>

<span data-ttu-id="19d82-211">Mono 是開放原始碼、[跨平台](#cross-platform)的 .NET 實作，主要用於需要小型執行階段時。</span><span class="sxs-lookup"><span data-stu-id="19d82-211">Mono is an open source, [cross-platform](#cross-platform) .NET implementation that is mainly used when a small runtime is required.</span></span> <span data-ttu-id="19d82-212">它是在 Android、Mac、iOS、tvOS 和 watchOS 上提供 Xamarin 應用程式的執行時間，主要著重于需要少量使用量的應用程式。</span><span class="sxs-lookup"><span data-stu-id="19d82-212">It is the runtime that powers Xamarin applications on Android, Mac, iOS, tvOS, and watchOS and is focused primarily on apps that require a small footprint.</span></span>

<span data-ttu-id="19d82-213">它支援目前發行的所有 .NET Standard 版本。</span><span class="sxs-lookup"><span data-stu-id="19d82-213">It supports all of the currently published .NET Standard versions.</span></span>

<span data-ttu-id="19d82-214">在過去，Mono 實作較大型的 .NET Framework API，並模擬 UNIX 上最熱門的其中一些功能。</span><span class="sxs-lookup"><span data-stu-id="19d82-214">Historically, Mono implemented the larger API of the .NET Framework and emulated some of the most popular capabilities on Unix.</span></span> <span data-ttu-id="19d82-215">它有時可用來執行依賴這些 UNIX 功能的 .NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="19d82-215">It is sometimes used to run .NET applications that rely on those capabilities on Unix.</span></span>

<span data-ttu-id="19d82-216">Mono 通常可搭配 Just-In-Time 編譯器使用，但也提供適用於 iOS 等平台的完整靜態編譯器 (預先編譯)。</span><span class="sxs-lookup"><span data-stu-id="19d82-216">Mono is typically used with a just-in-time compiler, but it also features a full static compiler (ahead-of-time compilation) that is used on platforms like iOS.</span></span>

<span data-ttu-id="19d82-217">若要深入了解 Mono，請參閱 [Mono 文件](https://www.mono-project.com/docs/)。</span><span class="sxs-lookup"><span data-stu-id="19d82-217">To learn more about Mono, see the [Mono documentation](https://www.mono-project.com/docs/).</span></span>

## <a name="net"></a><span data-ttu-id="19d82-218">.NET</span><span class="sxs-lookup"><span data-stu-id="19d82-218">.NET</span></span>

<span data-ttu-id="19d82-219">[.NET Standard](#net-standard) 以及所有 [.NET 實作](#implementation-of-net)和工作負載的籠統詞彙。</span><span class="sxs-lookup"><span data-stu-id="19d82-219">The umbrella term for [.NET Standard](#net-standard) and all [.NET implementations](#implementation-of-net) and workloads.</span></span> <span data-ttu-id="19d82-220">一律全大寫，永不「.Net」。</span><span class="sxs-lookup"><span data-stu-id="19d82-220">Always fully capitalized, never ".Net".</span></span>

<span data-ttu-id="19d82-221">請參閱[.net 指南](index.yml)</span><span class="sxs-lookup"><span data-stu-id="19d82-221">See the [.NET guide](index.yml)</span></span>

## <a name="net-core"></a><span data-ttu-id="19d82-222">.NET Core</span><span class="sxs-lookup"><span data-stu-id="19d82-222">.NET Core</span></span>

<span data-ttu-id="19d82-223">.NET 的跨平臺、高效能、開放原始碼的執行。</span><span class="sxs-lookup"><span data-stu-id="19d82-223">A cross-platform, high-performance, open-source implementation of .NET.</span></span> <span data-ttu-id="19d82-224">包括 Core Common Language Runtime (CoreCLR)、Core AOT 執行階段 (CoreRT 開發中)、Core 基底類別庫，以及 Core SDK。</span><span class="sxs-lookup"><span data-stu-id="19d82-224">Includes the Core Common Language Runtime (CoreCLR), the Core AOT Runtime (CoreRT, in development), the Core Base Class Library, and the Core SDK.</span></span>

<span data-ttu-id="19d82-225">請參閱 [.NET Core](../core/index.yml)。</span><span class="sxs-lookup"><span data-stu-id="19d82-225">See [.NET Core](../core/index.yml).</span></span>

## <a name="net-core-cli"></a><span data-ttu-id="19d82-226">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="19d82-226">.NET Core CLI</span></span>

<span data-ttu-id="19d82-227">用於開發 .NET Core 應用程式的跨平台工具鏈。</span><span class="sxs-lookup"><span data-stu-id="19d82-227">A cross-platform toolchain for developing .NET Core applications.</span></span>

<span data-ttu-id="19d82-228">請參閱[.NET Core CLI](../core/tools/index.md)。</span><span class="sxs-lookup"><span data-stu-id="19d82-228">See [.NET Core CLI](../core/tools/index.md).</span></span>

## <a name="net-core-sdk"></a><span data-ttu-id="19d82-229">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="19d82-229">.NET Core SDK</span></span>

<span data-ttu-id="19d82-230">可讓開發人員建立 .NET Core 應用程式和程式庫的一組程式庫和工具。</span><span class="sxs-lookup"><span data-stu-id="19d82-230">A set of libraries and tools that allow developers to create .NET Core applications and libraries.</span></span> <span data-ttu-id="19d82-231">包括用於建置應用程式的 [.NET Core CLI](#net-core-cli)、用於建置及執行應用程式的 .NET Core 程式庫和執行階段，以及執行 CLI 命令及執行應用程式的 dotnet 可執行檔 (*dotnet.exe*)。</span><span class="sxs-lookup"><span data-stu-id="19d82-231">Includes the [.NET Core CLI](#net-core-cli) for building apps, .NET Core libraries and runtime for building and running apps, and the dotnet executable (*dotnet.exe*) that runs CLI commands and runs applications.</span></span>

<span data-ttu-id="19d82-232">請參閱 [.NET Core SDK 概觀](../core/sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="19d82-232">See [.NET Core SDK Overview](../core/sdk.md).</span></span>

## <a name="net-framework"></a><span data-ttu-id="19d82-233">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="19d82-233">.NET Framework</span></span>

<span data-ttu-id="19d82-234">只會在 Windows 上執行的 .NET 實作。</span><span class="sxs-lookup"><span data-stu-id="19d82-234">An implementation of .NET that runs only on Windows.</span></span> <span data-ttu-id="19d82-235">包括 Common Language Runtime (CLR)、基底類別庫，以及 ASP.NET、Windows Forms 和 WPF 等應用程式架構程式庫。</span><span class="sxs-lookup"><span data-stu-id="19d82-235">Includes the Common Language Runtime (CLR), the Base Class Library, and application framework libraries such as ASP.NET, Windows Forms, and WPF.</span></span>

<span data-ttu-id="19d82-236">請參閱 [.NET Framework 指南](../framework/index.yml)。</span><span class="sxs-lookup"><span data-stu-id="19d82-236">See [.NET Framework Guide](../framework/index.yml).</span></span>

## <a name="net-native"></a><span data-ttu-id="19d82-237">.NET Native</span><span class="sxs-lookup"><span data-stu-id="19d82-237">.NET Native</span></span>

<span data-ttu-id="19d82-238">產生機器碼預先編譯 (AOT) 而不是 Just-In-Time (JIT) 的編譯器工具鏈。</span><span class="sxs-lookup"><span data-stu-id="19d82-238">A compiler tool chain that produces native code ahead-of-time (AOT), as opposed to just-in-time (JIT).</span></span>

<span data-ttu-id="19d82-239">編譯會在開發人員的電腦上發生，其運作方式類似於 C++ 編譯器和連結器。</span><span class="sxs-lookup"><span data-stu-id="19d82-239">Compilation happens on the developer's machine similar to the way a C++ compiler and linker works.</span></span> <span data-ttu-id="19d82-240">它會移除未使用的程式碼，並花更多時間在最佳化。</span><span class="sxs-lookup"><span data-stu-id="19d82-240">It removes unused code and spends more time optimizing it.</span></span> <span data-ttu-id="19d82-241">它會從程式庫擷取程式碼，並將其合併成可執行檔。</span><span class="sxs-lookup"><span data-stu-id="19d82-241">It extracts code from libraries and merges them into the executable.</span></span> <span data-ttu-id="19d82-242">結果會是代表整個應用程式的單一模組。</span><span class="sxs-lookup"><span data-stu-id="19d82-242">The result is a single module that represents the entire app.</span></span>

<span data-ttu-id="19d82-243">UWP 是 .NET Native 第一個支援的應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="19d82-243">UWP was the first application framework supported by .NET Native.</span></span> <span data-ttu-id="19d82-244">現在，我們支援建置適用於 Windows、macOS 和 Linux 的原生主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="19d82-244">Now, we support building native console apps for Windows, macOS, and Linux.</span></span>

<span data-ttu-id="19d82-245">請參閱 [Intro to .NET Native and CoreRT](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md) (.NET Native 和 CoreRT 簡介)</span><span class="sxs-lookup"><span data-stu-id="19d82-245">See [Intro to .NET Native and CoreRT](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md)</span></span>

## <a name="net-standard"></a><span data-ttu-id="19d82-246">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="19d82-246">.NET Standard</span></span>

<span data-ttu-id="19d82-247">可用於每個 .NET 實作之 .NET API 的型式規格。</span><span class="sxs-lookup"><span data-stu-id="19d82-247">A formal specification of .NET APIs that are available in each .NET implementation.</span></span>

<span data-ttu-id="19d82-248">.NET Standard 規格在文件中有時稱為程式庫。</span><span class="sxs-lookup"><span data-stu-id="19d82-248">The .NET Standard specification is sometimes called a library in the documentation.</span></span> <span data-ttu-id="19d82-249">由於程式庫不只包含規格 (介面)，還包含 API 實作，因此將 .NET Standard 稱為「程式庫」會造成誤導。</span><span class="sxs-lookup"><span data-stu-id="19d82-249">Because a library includes API implementations, not only specifications (interfaces), it's misleading to call .NET Standard a "library."</span></span> <span data-ttu-id="19d82-250">我們計劃從文件中排除該用法，只有參考 .NET Standard 中繼套件的名稱 (`NETStandard.Library`) 時除外。</span><span class="sxs-lookup"><span data-stu-id="19d82-250">We plan to eliminate that usage from the documentation, except in reference to the name of the .NET Standard metapackage (`NETStandard.Library`).</span></span>

<span data-ttu-id="19d82-251">請參閱 [.NET Standard](net-standard.md)。</span><span class="sxs-lookup"><span data-stu-id="19d82-251">See [.NET Standard](net-standard.md).</span></span>

## <a name="ngen"></a><span data-ttu-id="19d82-252">NGEN</span><span class="sxs-lookup"><span data-stu-id="19d82-252">NGEN</span></span>

<span data-ttu-id="19d82-253">原生 (映像) 產生。</span><span class="sxs-lookup"><span data-stu-id="19d82-253">Native (image) generation.</span></span>

<span data-ttu-id="19d82-254">您可以將這項技術視為永續性 JIT 編譯器。</span><span class="sxs-lookup"><span data-stu-id="19d82-254">You can think of this technology as a persistent JIT compiler.</span></span> <span data-ttu-id="19d82-255">它通常會在執行程式碼的電腦上編譯程式碼，但編譯通常會發生在安裝期間。</span><span class="sxs-lookup"><span data-stu-id="19d82-255">It usually compiles code on the machine where the code is executed, but compilation typically occurs at install time.</span></span>

## <a name="package"></a><span data-ttu-id="19d82-256">套件</span><span class="sxs-lookup"><span data-stu-id="19d82-256">package</span></span>

<span data-ttu-id="19d82-257">NuGet 套件 (簡稱套件) 是 *.zip* 檔案，其中包含一或多個同名組件及其他中繼資料 (例如作者名稱)。</span><span class="sxs-lookup"><span data-stu-id="19d82-257">A NuGet package &mdash; or just a package &mdash; is a *.zip* file with one or more assemblies of the same name along with additional metadata such as the author name.</span></span>

<span data-ttu-id="19d82-258">*.zip* 檔案包含一個 *.nupkg* 延伸模組和許多特定資產 (例如 *.dll* 檔案和 *.xml* 檔案)，可搭配多個架構和版本使用。</span><span class="sxs-lookup"><span data-stu-id="19d82-258">The *.zip* file has a *.nupkg* extension and may contain assets, such as *.dll* files and *.xml* files, for use with multiple target frameworks and versions.</span></span> <span data-ttu-id="19d82-259">安裝於應用程式或程式庫時，會根據應用程式或程式庫所指定的目標 Framework 來選取適當的資產。</span><span class="sxs-lookup"><span data-stu-id="19d82-259">When installed in an app or library, the appropriate assets are selected based on the target framework specified by the app or library.</span></span> <span data-ttu-id="19d82-260">定義介面的資產位於 *ref* 資料夾中，而定義實作的資產則位於 *lib* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="19d82-260">The assets that define the interface are in the *ref* folder, and the assets that define the implementation are in the *lib* folder.</span></span>

## <a name="platform"></a><span data-ttu-id="19d82-261">平台</span><span class="sxs-lookup"><span data-stu-id="19d82-261">platform</span></span>

<span data-ttu-id="19d82-262">作業系統及其執行所在的硬體，例如 Windows、macOS、Linux、iOS 和 Android。</span><span class="sxs-lookup"><span data-stu-id="19d82-262">An operating system and the hardware it runs on, such as Windows, macOS, Linux, iOS, and Android.</span></span>

<span data-ttu-id="19d82-263">以下是用於句子中的範例：</span><span class="sxs-lookup"><span data-stu-id="19d82-263">Here are examples of usage in sentences:</span></span>

- <span data-ttu-id="19d82-264">「.NET Core 是 .NET 的跨平台實作。」</span><span class="sxs-lookup"><span data-stu-id="19d82-264">".NET Core is a cross-platform implementation of .NET."</span></span>
- <span data-ttu-id="19d82-265">「PCL 設定檔代表 Microsoft 平台，而 .NET Standard 則無從驗證平台。」</span><span class="sxs-lookup"><span data-stu-id="19d82-265">"PCL profiles represent Microsoft platforms, while the .NET Standard is agnostic to platform."</span></span>

<span data-ttu-id="19d82-266">.NET 文件經常使用「.NET 平台」來表示 .NET 實作或包含所有實作的 .NET 堆疊。</span><span class="sxs-lookup"><span data-stu-id="19d82-266">The .NET documentation frequently uses ".NET platform" to mean either an implementation of .NET or the .NET stack including all implementations.</span></span> <span data-ttu-id="19d82-267">這兩種用法通常會與主要 (OS/硬體) 意義混淆，因此我們計劃從文件中排除這些用法。</span><span class="sxs-lookup"><span data-stu-id="19d82-267">Both of these usages tend to get confused with the primary (OS/hardware) meaning, so we plan to eliminate these usages from the documentation.</span></span>

## <a name="runtime"></a><span data-ttu-id="19d82-268">執行階段</span><span class="sxs-lookup"><span data-stu-id="19d82-268">runtime</span></span>

<span data-ttu-id="19d82-269">受管理程式的執行環境。</span><span class="sxs-lookup"><span data-stu-id="19d82-269">The execution environment for a managed program.</span></span>

<span data-ttu-id="19d82-270">OS 是執行階段環境的一部分，但不是 .NET 執行階段的一部分。</span><span class="sxs-lookup"><span data-stu-id="19d82-270">The OS is part of the runtime environment but is not part of the .NET runtime.</span></span> <span data-ttu-id="19d82-271">以下是 .NET 執行階段的一些範例：</span><span class="sxs-lookup"><span data-stu-id="19d82-271">Here are some examples of .NET runtimes:</span></span>

- <span data-ttu-id="19d82-272">Common Language Runtime (CLR)</span><span class="sxs-lookup"><span data-stu-id="19d82-272">Common Language Runtime (CLR)</span></span>
- <span data-ttu-id="19d82-273">Core Common Language Runtime (CoreCLR)</span><span class="sxs-lookup"><span data-stu-id="19d82-273">Core Common Language Runtime (CoreCLR)</span></span>
- <span data-ttu-id="19d82-274">.NET Native (適用於 UWP)</span><span class="sxs-lookup"><span data-stu-id="19d82-274">.NET Native (for UWP)</span></span>
- <span data-ttu-id="19d82-275">Mono 執行階段</span><span class="sxs-lookup"><span data-stu-id="19d82-275">Mono runtime</span></span>

<span data-ttu-id="19d82-276">.NET 文件有時會使用「執行階段」來表示 .NET 實作。</span><span class="sxs-lookup"><span data-stu-id="19d82-276">The .NET documentation sometimes uses "runtime" to mean an implementation of .NET.</span></span> <span data-ttu-id="19d82-277">例如，在下列句子中，「執行階段」應該取代成「實作」：</span><span class="sxs-lookup"><span data-stu-id="19d82-277">For example, in the following sentences "runtime" should be replaced with "implementation":</span></span>

- <span data-ttu-id="19d82-278">「不同的 .NET 執行階段會實作特定版本的 .NET Standard。」</span><span class="sxs-lookup"><span data-stu-id="19d82-278">"The various .NET runtimes implement specific versions of .NET Standard."</span></span>
- <span data-ttu-id="19d82-279">「要在多個執行階段上執行的程式庫應以此架構為目標。」</span><span class="sxs-lookup"><span data-stu-id="19d82-279">"Libraries that are intended to run on multiple runtimes should target this framework."</span></span> <span data-ttu-id="19d82-280">(指的是 .NET Standard)</span><span class="sxs-lookup"><span data-stu-id="19d82-280">(referring to .NET Standard)</span></span>
- <span data-ttu-id="19d82-281">「不同的 .NET 執行階段會實作特定版本的 .NET Standard。</span><span class="sxs-lookup"><span data-stu-id="19d82-281">"The various .NET runtimes implement specific versions of .NET Standard.</span></span> <span data-ttu-id="19d82-282">…</span><span class="sxs-lookup"><span data-stu-id="19d82-282">…</span></span> <span data-ttu-id="19d82-283">每個 .NET 執行階段版本會宣佈它所支援的最高 .NET Standard 版本...」</span><span class="sxs-lookup"><span data-stu-id="19d82-283">Each .NET runtime version advertises the highest .NET Standard version it supports …"</span></span>

<span data-ttu-id="19d82-284">我們計劃排除這個不一致的用法。</span><span class="sxs-lookup"><span data-stu-id="19d82-284">We plan to eliminate this inconsistent usage.</span></span>

## <a name="stack"></a><span data-ttu-id="19d82-285">堆疊</span><span class="sxs-lookup"><span data-stu-id="19d82-285">stack</span></span>

<span data-ttu-id="19d82-286">可搭配使用以建置及執行應用程式的一組程式設計技術。</span><span class="sxs-lookup"><span data-stu-id="19d82-286">A set of programming technologies that are used together to build and run applications.</span></span>

<span data-ttu-id="19d82-287">「.NET 堆疊」是指 .NET Standard 和所有 .NET 實作。</span><span class="sxs-lookup"><span data-stu-id="19d82-287">"The .NET stack" refers to the .NET Standard and all .NET implementations.</span></span> <span data-ttu-id="19d82-288">「一個 .NET 堆疊」一詞可能是指 .NET 的一項實作。</span><span class="sxs-lookup"><span data-stu-id="19d82-288">The phrase "a .NET stack" may refer to one implementation of .NET.</span></span>

## <a name="target-framework"></a><span data-ttu-id="19d82-289">Target Framework - 目標 Framework</span><span class="sxs-lookup"><span data-stu-id="19d82-289">target framework</span></span>

<span data-ttu-id="19d82-290">.NET 應用程式或程式庫依賴的 API 集合。</span><span class="sxs-lookup"><span data-stu-id="19d82-290">The collection of APIs that a .NET app or library relies on.</span></span>

<span data-ttu-id="19d82-291">應用程式或程式庫可以將目標設為某個版本的 .NET Standard (例如 .NET Standard 2.0)，這會是跨所有 .NET 實作之一組標準化 API 的規格。</span><span class="sxs-lookup"><span data-stu-id="19d82-291">An app or library can target a version of .NET Standard (for example, .NET Standard 2.0), which is specification for a standardized set of APIs across all .NET implementations.</span></span> <span data-ttu-id="19d82-292">應用程式或程式庫也可以將目標設為某個版本的特定 .NET 實作；在此情況下，它可以存取實作特定的 API。</span><span class="sxs-lookup"><span data-stu-id="19d82-292">An app or library can also target a version of a specific .NET implementation, in which case it gets access to implementation-specific APIs.</span></span> <span data-ttu-id="19d82-293">例如，以 Xamarin.iOS 為目標的應用程式可以存取 Xamarin 提供的 iOS API 包裝函式。</span><span class="sxs-lookup"><span data-stu-id="19d82-293">For example, an app that targets Xamarin.iOS gets access to Xamarin-provided iOS API wrappers.</span></span>

<span data-ttu-id="19d82-294">針對某些目標 Framework (例如 .NET Framework)，可用的 API 是由 .NET 實作安裝在系統上的組件所定義，這可能包含應用程式架構 API (例如 ASP.NET、WinForms)。</span><span class="sxs-lookup"><span data-stu-id="19d82-294">For some target frameworks (for example, the .NET Framework) the available APIs are defined by the assemblies that a .NET implementation installs on a system, which may include application framework APIs (for example, ASP.NET, WinForms).</span></span> <span data-ttu-id="19d82-295">針對以套件為基礎的目標 Framework (例如 .NET Standard 和 .NET Core)，架構 API 是由安裝在應用程式或程式庫中的套件所定義。</span><span class="sxs-lookup"><span data-stu-id="19d82-295">For package-based target frameworks (such as .NET Standard and .NET Core), the framework APIs are defined by the packages installed in the app or library.</span></span> <span data-ttu-id="19d82-296">在此情況下，目標 Framework 會隱含指定一個中繼套件，該套件會參考組成架構的所有套件。</span><span class="sxs-lookup"><span data-stu-id="19d82-296">In that case, the target framework implicitly specifies a metapackage that references all the packages that together make up the framework.</span></span>

<span data-ttu-id="19d82-297">請參閱[目標 Framework](frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="19d82-297">See [Target Frameworks](frameworks.md).</span></span>

## <a name="tfm"></a><span data-ttu-id="19d82-298">TFM</span><span class="sxs-lookup"><span data-stu-id="19d82-298">TFM</span></span>

<span data-ttu-id="19d82-299">目標 Framework Moniker。</span><span class="sxs-lookup"><span data-stu-id="19d82-299">Target framework moniker.</span></span>

<span data-ttu-id="19d82-300">用於指定 .NET 應用程式或程式庫之目標 Framework 的標準化語彙基元格式。</span><span class="sxs-lookup"><span data-stu-id="19d82-300">A standardized token format for specifying the target framework of a .NET app or library.</span></span> <span data-ttu-id="19d82-301">目標 Framework 通常會由簡短名稱參考，例如 `net462`。</span><span class="sxs-lookup"><span data-stu-id="19d82-301">Target frameworks are typically referenced by a short name, such as `net462`.</span></span> <span data-ttu-id="19d82-302">雖然有完整格式的 TFM (例如 .NETFramework,Version=4.6.2)，但通常不會用來指定目標 Framework。</span><span class="sxs-lookup"><span data-stu-id="19d82-302">Long-form TFMs (such as .NETFramework,Version=4.6.2) exist but are not generally used to specify a target framework.</span></span>

<span data-ttu-id="19d82-303">請參閱[目標 Framework](frameworks.md)。</span><span class="sxs-lookup"><span data-stu-id="19d82-303">See [Target Frameworks](frameworks.md).</span></span>

## <a name="uwp"></a><span data-ttu-id="19d82-304">UWP</span><span class="sxs-lookup"><span data-stu-id="19d82-304">UWP</span></span>

<span data-ttu-id="19d82-305">通用 Windows 平台。</span><span class="sxs-lookup"><span data-stu-id="19d82-305">Universal Windows Platform.</span></span>

<span data-ttu-id="19d82-306">用於建置適用於物聯網 (IoT) 之現代化觸控式 Windows 應用程式和軟體的 .NET 實作。</span><span class="sxs-lookup"><span data-stu-id="19d82-306">An implementation of .NET that is used for building modern, touch-enabled Windows applications and software for the Internet of Things (IoT).</span></span> <span data-ttu-id="19d82-307">其設計目的是要整合您可能想要設為目標的不同裝置類型，包括電腦、平板電腦、手機，甚至是 Xbox。</span><span class="sxs-lookup"><span data-stu-id="19d82-307">It's designed to unify the different types of devices that you may want to target, including PCs, tablets, phones, and even the Xbox.</span></span> <span data-ttu-id="19d82-308">UWP 提供許多服務 (例如集中式應用程式存放區)、一個執行環境 (AppContainer)，以及用來取代 Win32 (WinRT) 的一組 Windows API。</span><span class="sxs-lookup"><span data-stu-id="19d82-308">UWP provides many services, such as a centralized app store, an execution environment (AppContainer), and a set of Windows APIs to use instead of Win32 (WinRT).</span></span> <span data-ttu-id="19d82-309">應用程式可以用 c + +、c #、Visual Basic 和 JavaScript 撰寫。</span><span class="sxs-lookup"><span data-stu-id="19d82-309">Apps can be written in C++, C#, Visual Basic, and JavaScript.</span></span> <span data-ttu-id="19d82-310">使用 c # 和 Visual Basic 時，.net Api 是由 .NET Core 提供。</span><span class="sxs-lookup"><span data-stu-id="19d82-310">When using C# and Visual Basic, the .NET APIs are provided by .NET Core.</span></span>

## <a name="see-also"></a><span data-ttu-id="19d82-311">另請參閱</span><span class="sxs-lookup"><span data-stu-id="19d82-311">See also</span></span>

- [<span data-ttu-id="19d82-312">.NET 指南</span><span class="sxs-lookup"><span data-stu-id="19d82-312">.NET Guide</span></span>](index.yml)
- [<span data-ttu-id="19d82-313">.NET Framework 指南</span><span class="sxs-lookup"><span data-stu-id="19d82-313">.NET Framework Guide</span></span>](../framework/index.yml)
- [<span data-ttu-id="19d82-314">.NET Core</span><span class="sxs-lookup"><span data-stu-id="19d82-314">.NET Core</span></span>](../core/index.yml)
- [<span data-ttu-id="19d82-315">ASP.NET 總覽</span><span class="sxs-lookup"><span data-stu-id="19d82-315">ASP.NET Overview</span></span>](/aspnet/index#pivot=aspnet)
- [<span data-ttu-id="19d82-316">ASP.NET Core 總覽</span><span class="sxs-lookup"><span data-stu-id="19d82-316">ASP.NET Core Overview</span></span>](/aspnet/index#pivot=core)
