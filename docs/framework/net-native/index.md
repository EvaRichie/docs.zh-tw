---
title: 使用 .NET Native 編譯應用程式
ms.date: 03/30/2017
helpviewer_keywords:
- native compilation
- .NET and native code
- compilation with .NET Native
- .NET Native
- C# and native compilation
ms.assetid: 47cd5648-9469-4b1d-804c-43cc04384045
ms.openlocfilehash: 7601a6d5e7f49b6d8fc434ef772e2e69740f02cf
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90543929"
---
# <a name="compiling-apps-with-net-native"></a><span data-ttu-id="16212-102">使用 .NET Native 編譯應用程式</span><span class="sxs-lookup"><span data-stu-id="16212-102">Compiling Apps with .NET Native</span></span>

<span data-ttu-id="16212-103">.NET Native 是一種先行編譯技術，可用於建立及部署 Visual Studio 2015 和更新版本隨附的 Windows 應用程式。</span><span class="sxs-lookup"><span data-stu-id="16212-103">.NET Native is a precompilation technology for building and deploying Windows apps that is included with Visual Studio 2015 and later versions.</span></span> <span data-ttu-id="16212-104">此工具可將以 Managed 程式碼 (C# 或 Visual Basic) 撰寫且目標為 .NET Framework 和 Windows 10 的應用程式發行版本自動編譯為機器碼。</span><span class="sxs-lookup"><span data-stu-id="16212-104">It automatically compiles the release version of apps that are written in managed code (C# or Visual Basic) and that target the .NET Framework and Windows 10 to native code.</span></span>

<span data-ttu-id="16212-105">一般而言，以 .NET Framework 為目標的應用程式會編譯成中繼語言 (IL)。</span><span class="sxs-lookup"><span data-stu-id="16212-105">Typically, apps that target the .NET Framework are compiled to intermediate language (IL).</span></span> <span data-ttu-id="16212-106">在執行階段，just-in-time (JIT) 編譯器會將 IL 轉譯成機器碼。</span><span class="sxs-lookup"><span data-stu-id="16212-106">At run time, the just-in-time (JIT) compiler translates the IL to native code.</span></span> <span data-ttu-id="16212-107">相反地，.NET Native 會將 Windows 應用程式直接編譯成機器碼。</span><span class="sxs-lookup"><span data-stu-id="16212-107">In contrast, .NET Native compiles Windows apps directly to native code.</span></span> <span data-ttu-id="16212-108">對開發人員而言，這表示：</span><span class="sxs-lookup"><span data-stu-id="16212-108">For developers, this means:</span></span>

- <span data-ttu-id="16212-109">您的應用程式會以原生程式碼的效能為特色。</span><span class="sxs-lookup"><span data-stu-id="16212-109">Your apps feature the performance of native code.</span></span> <span data-ttu-id="16212-110">通常，效能會優於第一個編譯為 IL 的程式碼，然後由 JIT 編譯程式編譯成機器碼。</span><span class="sxs-lookup"><span data-stu-id="16212-110">Usually, performance will be superior to code that is first compiled to IL and then compiled to native code by the JIT compiler.</span></span>

- <span data-ttu-id="16212-111">您可以繼續以 C# 或 Visual Basic 進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="16212-111">You can continue to program in C# or Visual Basic.</span></span>

- <span data-ttu-id="16212-112">您可以繼續利用 .NET Framework 所提供的資源，包括其類別庫、自動記憶體管理和記憶體回收，以及例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="16212-112">You can continue to take advantage of the resources provided by the .NET Framework, including its class library, automatic memory management and garbage collection, and exception handling.</span></span>

<span data-ttu-id="16212-113">對於您應用程式的使用者，.NET Native 提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="16212-113">For users of your apps, .NET Native offers these advantages:</span></span>

- <span data-ttu-id="16212-114">針對大部分的應用程式和案例加快執行時間。</span><span class="sxs-lookup"><span data-stu-id="16212-114">Faster execution times for the majority of apps and scenarios.</span></span>

- <span data-ttu-id="16212-115">讓大部分應用程式和案例的啟動時間更快。</span><span class="sxs-lookup"><span data-stu-id="16212-115">Faster startup times for the majority of apps and scenarios.</span></span>

- <span data-ttu-id="16212-116">低部署和更新成本。</span><span class="sxs-lookup"><span data-stu-id="16212-116">Low deployment and update costs.</span></span>

- <span data-ttu-id="16212-117">優化的應用程式記憶體使用量。</span><span class="sxs-lookup"><span data-stu-id="16212-117">Optimized app memory usage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16212-118">在大部分的應用程式和案例中，相較于編譯為 IL 或 NGEN 影像的應用程式，.NET Native 提供明顯更快速的啟動時間和優異的效能。</span><span class="sxs-lookup"><span data-stu-id="16212-118">For the vast majority of apps and scenarios, .NET Native offers significantly faster startup times and superior performance when compared to an app compiled to IL or to an NGEN image.</span></span> <span data-ttu-id="16212-119">不過，您的結果可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="16212-119">However, your results may vary.</span></span> <span data-ttu-id="16212-120">為了確保您的應用程式已受益于 .NET Native 的效能增強功能，您應該比較其效能與應用程式的 non-.NET 原生版本。</span><span class="sxs-lookup"><span data-stu-id="16212-120">To ensure that your app has benefited from the performance enhancements of .NET Native, you should compare its performance with that of the non-.NET Native version of your app.</span></span> <span data-ttu-id="16212-121">如需詳細資訊，請參閱 [效能會話總覽](/visualstudio/profiling/performance-session-overview)。</span><span class="sxs-lookup"><span data-stu-id="16212-121">For more information, see [Performance Session Overview](/visualstudio/profiling/performance-session-overview).</span></span>

<span data-ttu-id="16212-122">但 .NET Native 牽涉到一個以上的程式碼編譯。</span><span class="sxs-lookup"><span data-stu-id="16212-122">But .NET Native involves more than a compilation to native code.</span></span> <span data-ttu-id="16212-123">它會將轉換 .NET Framework 應用程式建置和執行的方式。</span><span class="sxs-lookup"><span data-stu-id="16212-123">It transforms the way that .NET Framework apps are built and executed.</span></span> <span data-ttu-id="16212-124">尤其是：</span><span class="sxs-lookup"><span data-stu-id="16212-124">In particular:</span></span>

- <span data-ttu-id="16212-125">在預先編譯期間，.NET Framework 的必要部分會以靜態方式連結到您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="16212-125">During precompilation, required portions of the .NET Framework are statically linked into your app.</span></span> <span data-ttu-id="16212-126">這樣可以讓應用程式以 .NET Framework 的 app-local 程式庫來執行，並且讓編譯器執行全域分析，以提供優異的效能。</span><span class="sxs-lookup"><span data-stu-id="16212-126">This allows the app to run with app-local libraries of the .NET Framework, and the compiler to perform global analysis to deliver performance wins.</span></span> <span data-ttu-id="16212-127">如此一來，即使 .NET Framework 更新之後，應用程式還是一貫地會以更快的速度啟動。</span><span class="sxs-lookup"><span data-stu-id="16212-127">As a result, apps launch consistently faster even after .NET Framework updates.</span></span>

- <span data-ttu-id="16212-128">.NET Native 執行時間已針對靜態先行編譯進行優化，而在大部分的情況下都提供優異的效能。</span><span class="sxs-lookup"><span data-stu-id="16212-128">The .NET Native runtime is optimized for static precompilation and in the vast majority of cases offers superior performance.</span></span> <span data-ttu-id="16212-129">同時，它還保留了開發人員會覺得生產力極佳的核心反映功能。</span><span class="sxs-lookup"><span data-stu-id="16212-129">At the same time, it retains the core reflection features that developers find so productive.</span></span>

- <span data-ttu-id="16212-130">.NET Native 使用與 c + + 編譯器相同的後端，其已針對靜態先行編譯案例進行優化。</span><span class="sxs-lookup"><span data-stu-id="16212-130">.NET Native uses the same back end as the C++ compiler, which is optimized for static precompilation scenarios.</span></span>

<span data-ttu-id="16212-131">.NET Native 能夠為 managed 程式碼開發人員帶來 c + + 的效能優勢，因為它在幕後使用與 c + + 相同或類似的工具，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="16212-131">.NET Native is able to bring the performance benefits of C++ to managed code developers because it uses the same or similar tools as C++ under the hood, as shown in this table.</span></span>

||<span data-ttu-id="16212-132">.NET Native</span><span class="sxs-lookup"><span data-stu-id="16212-132">.NET Native</span></span>|<span data-ttu-id="16212-133">C++</span><span class="sxs-lookup"><span data-stu-id="16212-133">C++</span></span>|
|-|----------------------------------------------------------------|-----------|
|<span data-ttu-id="16212-134">程式庫</span><span class="sxs-lookup"><span data-stu-id="16212-134">Libraries</span></span>|<span data-ttu-id="16212-135">.NET Framework + Windows 執行階段</span><span class="sxs-lookup"><span data-stu-id="16212-135">The .NET Framework + Windows Runtime</span></span>|<span data-ttu-id="16212-136">Win32 + Windows 執行階段</span><span class="sxs-lookup"><span data-stu-id="16212-136">Win32 + Windows Runtime</span></span>|
|<span data-ttu-id="16212-137">編譯器</span><span class="sxs-lookup"><span data-stu-id="16212-137">Compiler</span></span>|<span data-ttu-id="16212-138">UTC 最佳化編譯器</span><span class="sxs-lookup"><span data-stu-id="16212-138">UTC optimizing compiler</span></span>|<span data-ttu-id="16212-139">UTC 最佳化編譯器</span><span class="sxs-lookup"><span data-stu-id="16212-139">UTC optimizing compiler</span></span>|
|<span data-ttu-id="16212-140">已部署</span><span class="sxs-lookup"><span data-stu-id="16212-140">Deployed</span></span>|<span data-ttu-id="16212-141">可立即執行的二進位檔案</span><span class="sxs-lookup"><span data-stu-id="16212-141">Ready-to-run binaries</span></span>|<span data-ttu-id="16212-142">可立即執行的二進位檔案 (ASM)</span><span class="sxs-lookup"><span data-stu-id="16212-142">Ready-to-run binaries (ASM)</span></span>|
|<span data-ttu-id="16212-143">執行階段</span><span class="sxs-lookup"><span data-stu-id="16212-143">Runtime</span></span>|<span data-ttu-id="16212-144">MRT.dll (最小 CLR 執行階段)</span><span class="sxs-lookup"><span data-stu-id="16212-144">MRT.dll (Minimal CLR Runtime)</span></span>|<span data-ttu-id="16212-145">CRT.dll (C 執行階段)</span><span class="sxs-lookup"><span data-stu-id="16212-145">CRT.dll (C Runtime)</span></span>|

<span data-ttu-id="16212-146">針對適用於 Windows 10 的 Windows 應用程式，您要將應用程式封裝 (.appx 檔) 中的 .NET 機器碼編譯二進位檔上傳至 Windows 市集。</span><span class="sxs-lookup"><span data-stu-id="16212-146">For Windows apps for Windows 10, you upload .NET Native Code Compilation binaries in app packages (.appx files) to the Windows Store.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="16212-147">本節內容</span><span class="sxs-lookup"><span data-stu-id="16212-147">In This Section</span></span>

<span data-ttu-id="16212-148">如需有關使用 .NET 機器碼編譯來開發應用程式的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="16212-148">For more information about developing apps with .NET Native Code Compilation, see these topics:</span></span>

- [<span data-ttu-id="16212-149">開始使用 .NET 機器碼編譯：開發人員經驗逐步解說</span><span class="sxs-lookup"><span data-stu-id="16212-149">Getting Started with .NET Native Code Compilation: The Developer Experience Walkthrough</span></span>](getting-started-with-net-native.md)

- <span data-ttu-id="16212-150">[.NET 原生和編譯：](net-native-and-compilation.md) .NET 原生如何將您的專案編譯成原生程式碼。</span><span class="sxs-lookup"><span data-stu-id="16212-150">[.NET Native and Compilation:](net-native-and-compilation.md) How .NET Native compiles your project to native code.</span></span>

- [<span data-ttu-id="16212-151">反映和 .NET Native</span><span class="sxs-lookup"><span data-stu-id="16212-151">Reflection and .NET Native</span></span>](reflection-and-net-native.md)

  - [<span data-ttu-id="16212-152">依賴反映的 API</span><span class="sxs-lookup"><span data-stu-id="16212-152">APIs That Rely on Reflection</span></span>](apis-that-rely-on-reflection.md)

  - [<span data-ttu-id="16212-153">反映 API 參考</span><span class="sxs-lookup"><span data-stu-id="16212-153">Reflection API Reference</span></span>](net-native-reflection-api-reference.md)

  - [<span data-ttu-id="16212-154">執行階段指示詞 (rd.xml) 組態檔參考</span><span class="sxs-lookup"><span data-stu-id="16212-154">Runtime Directives (rd.xml) Configuration File Reference</span></span>](runtime-directives-rd-xml-configuration-file-reference.md)

- [<span data-ttu-id="16212-155">序列化和中繼資料</span><span class="sxs-lookup"><span data-stu-id="16212-155">Serialization and Metadata</span></span>](serialization-and-metadata.md)

- [<span data-ttu-id="16212-156">將您的 Windows 市集應用程式移轉至 .NET Native</span><span class="sxs-lookup"><span data-stu-id="16212-156">Migrating Your Windows Store App to .NET Native</span></span>](migrating-your-windows-store-app-to-net-native.md)

- [<span data-ttu-id="16212-157">.NET Native 一般疑難排解</span><span class="sxs-lookup"><span data-stu-id="16212-157">.NET Native General Troubleshooting</span></span>](net-native-general-troubleshooting.md)
