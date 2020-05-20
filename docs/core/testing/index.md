---
title: .NET Core 與 .NET Standard 中的單元測試
description: 此文章提供 .NET Core 與 .NET Standard 專案單元測試的簡短概觀。
author: ardalis
ms.author: wiwagn
ms.date: 05/18/2020
zone_pivot_groups: unit-testing-framework-set-one
ms.openlocfilehash: e15f80b173389cdff86c6e62013e9c0f21171dd6
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83703099"
---
# <a name="unit-testing-in-net-core-and-net-standard"></a><span data-ttu-id="88f0e-103">.NET Core 與 .NET Standard 中的單元測試</span><span class="sxs-lookup"><span data-stu-id="88f0e-103">Unit testing in .NET Core and .NET Standard</span></span>

<span data-ttu-id="88f0e-104">.NET Core 使單元測試的建立便得更加輕鬆。</span><span class="sxs-lookup"><span data-stu-id="88f0e-104">.NET Core makes it easy to create unit tests.</span></span> <span data-ttu-id="88f0e-105">本文會介紹單元測試，並示範它們和其他種類測試之間的差異。</span><span class="sxs-lookup"><span data-stu-id="88f0e-105">This article introduces unit tests and illustrates how they differ from other kinds of tests.</span></span> <span data-ttu-id="88f0e-106">接近頁面底部的連結資源，會向您示範如何將測試專案新增到解決方案。</span><span class="sxs-lookup"><span data-stu-id="88f0e-106">The linked resources near the bottom of the page show you how to add a test project to your solution.</span></span> <span data-ttu-id="88f0e-107">在您設定好測試專案後，就能使用命令列或 Visual Studio 來執行單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-107">After you set up your test project, you will be able to run your unit tests using the command line or Visual Studio.</span></span>

<span data-ttu-id="88f0e-108">如果您要測試**ASP.NET Core**專案，請參閱[ASP.NET Core 中的整合測試](/aspnet/core/test/integration-tests#test-app-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="88f0e-108">If you're testing an **ASP.NET Core** project, see [Integration tests in ASP.NET Core](/aspnet/core/test/integration-tests#test-app-prerequisites).</span></span>

<span data-ttu-id="88f0e-109">.NET Core 2.0 及較新版本均支援 [.NET Standard 2.0](../../standard/net-standard.md)，而我們會使用其程式庫來示範單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-109">.NET Core 2.0 and later supports [.NET Standard 2.0](../../standard/net-standard.md), and we will use its libraries to demonstrate unit tests.</span></span>

<span data-ttu-id="88f0e-110">您可以使用適用於 C#、F# 和 Visual Basic 的內建 .NET Core 2.0 及更新的單元測試專案範本，作為您個人專案的起點。</span><span class="sxs-lookup"><span data-stu-id="88f0e-110">You are able to use built-in .NET Core 2.0 and later unit test project templates for C#, F# and Visual Basic as a starting point for your personal project.</span></span>

## <a name="what-are-unit-tests"></a><span data-ttu-id="88f0e-111">什麼是單元測試？</span><span class="sxs-lookup"><span data-stu-id="88f0e-111">What are unit tests?</span></span>

<span data-ttu-id="88f0e-112">使用自動化測試是很好的方式，這種方式能確保應用程式按照作者想要的結果執行。</span><span class="sxs-lookup"><span data-stu-id="88f0e-112">Having automated tests is a great way to ensure a software application does what its authors intend it to do.</span></span> <span data-ttu-id="88f0e-113">軟體應用程式的測試有多種類型。</span><span class="sxs-lookup"><span data-stu-id="88f0e-113">There are multiple types of tests for software applications.</span></span> <span data-ttu-id="88f0e-114">其中包括整合測試、Web 測試、負載測試等等。</span><span class="sxs-lookup"><span data-stu-id="88f0e-114">These include integration tests, web tests, load tests, and others.</span></span> <span data-ttu-id="88f0e-115">**單元測試**會測試個別軟體元件和方法。</span><span class="sxs-lookup"><span data-stu-id="88f0e-115">**Unit tests** test individual software components and methods.</span></span> <span data-ttu-id="88f0e-116">單元測試應該只在開發人員的控制下用於測試程式碼，</span><span class="sxs-lookup"><span data-stu-id="88f0e-116">Unit tests should only test code within the developer’s control.</span></span> <span data-ttu-id="88f0e-117">而不應用來測試基礎結構考量。</span><span class="sxs-lookup"><span data-stu-id="88f0e-117">They should not test infrastructure concerns.</span></span> <span data-ttu-id="88f0e-118">基礎結構考量包括資料庫、檔案系統和網路資源。</span><span class="sxs-lookup"><span data-stu-id="88f0e-118">Infrastructure concerns include databases, file systems, and network resources.</span></span>

<span data-ttu-id="88f0e-119">此外，也請記得撰寫測試時可採用最佳做法。</span><span class="sxs-lookup"><span data-stu-id="88f0e-119">Also, keep in mind there are best practices for writing tests.</span></span> <span data-ttu-id="88f0e-120">舉例來說，[測試驅動開發 (TDD)](https://deviq.com/test-driven-development/) 可在撰寫單元測試前，用在單元測試要檢查的程式碼上。</span><span class="sxs-lookup"><span data-stu-id="88f0e-120">For example, [Test Driven Development (TDD)](https://deviq.com/test-driven-development/) is when a unit test is written before the code it is meant to check.</span></span> <span data-ttu-id="88f0e-121">使用 TDD 就像是在寫書之前打好草稿。</span><span class="sxs-lookup"><span data-stu-id="88f0e-121">TDD is like creating an outline for a book before we write it.</span></span> <span data-ttu-id="88f0e-122">它的目標是協助開發人員撰寫更簡單、更易讀且更有效率的程式碼。</span><span class="sxs-lookup"><span data-stu-id="88f0e-122">It is meant to help developers write simpler, more readable, and efficient code.</span></span>

> [!NOTE]
> <span data-ttu-id="88f0e-123">ASP.NET 小組遵循了[這些慣例](https://github.com/dotnet/aspnetcore/wiki/Engineering-guidelines#unit-tests-and-functional-tests)，來協助開發人員為測試類型與方法下個好名稱。</span><span class="sxs-lookup"><span data-stu-id="88f0e-123">The ASP.NET team follows [these conventions](https://github.com/dotnet/aspnetcore/wiki/Engineering-guidelines#unit-tests-and-functional-tests) to help developers come up with good names for test classes and methods.</span></span>

<span data-ttu-id="88f0e-124">請試著不要在撰寫單元測試時於基礎結構導入相依性。</span><span class="sxs-lookup"><span data-stu-id="88f0e-124">Try not to introduce dependencies on infrastructure when writing unit tests.</span></span> <span data-ttu-id="88f0e-125">相依性會導致測試變慢且不穩定，它們應該留給整合測試使用。</span><span class="sxs-lookup"><span data-stu-id="88f0e-125">These make the tests slow and brittle, and should be reserved for integration tests.</span></span> <span data-ttu-id="88f0e-126">您可以遵循 [Explicit Dependencies Principle](https://deviq.com/explicit-dependencies-principle/) (明確相依性準則) 的內容，並使用 [Dependency Injection](/aspnet/core/fundamentals/dependency-injection) (相依性注入)，來在應用程式中避免這些相依性。</span><span class="sxs-lookup"><span data-stu-id="88f0e-126">You can avoid these dependencies in your application by following the [Explicit Dependencies Principle](https://deviq.com/explicit-dependencies-principle/) and using [Dependency Injection](/aspnet/core/fundamentals/dependency-injection).</span></span> <span data-ttu-id="88f0e-127">您也可以將單元測試保留在個別專案中，和您的整合測試分開。</span><span class="sxs-lookup"><span data-stu-id="88f0e-127">You can also keep your unit tests in a separate project from your integration tests.</span></span> <span data-ttu-id="88f0e-128">這能確保您的單元測試專案不會對基礎結構套件具有參考或相依性。</span><span class="sxs-lookup"><span data-stu-id="88f0e-128">This ensures your unit test project doesn’t have references to or dependencies on infrastructure packages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88f0e-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88f0e-129">Next steps</span></span>

<span data-ttu-id="88f0e-130">.NET Core 專案單元測試的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="88f0e-130">More information on unit testing in .NET Core projects:</span></span>

<span data-ttu-id="88f0e-131">以下語言支援 .NET Core 單元測試專案：</span><span class="sxs-lookup"><span data-stu-id="88f0e-131">.NET Core unit test projects are supported for:</span></span>

- [<span data-ttu-id="88f0e-132">C#</span><span class="sxs-lookup"><span data-stu-id="88f0e-132">C#</span></span>](../../csharp/index.yml)
- [<span data-ttu-id="88f0e-133">F#</span><span class="sxs-lookup"><span data-stu-id="88f0e-133">F#</span></span>](../../fsharp/index.yml)
- [<span data-ttu-id="88f0e-134">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="88f0e-134">Visual Basic</span></span>](../../visual-basic/index.yml)

<span data-ttu-id="88f0e-135">您也可以選擇數個單元測試架構：</span><span class="sxs-lookup"><span data-stu-id="88f0e-135">You can also choose between several unit test frameworks:</span></span>

- [<span data-ttu-id="88f0e-136">xUnit</span><span class="sxs-lookup"><span data-stu-id="88f0e-136">xUnit</span></span>](https://xunit.net/)
- [<span data-ttu-id="88f0e-137">NUnit</span><span class="sxs-lookup"><span data-stu-id="88f0e-137">NUnit</span></span>](https://nunit.org)
- [<span data-ttu-id="88f0e-138">MSTest</span><span class="sxs-lookup"><span data-stu-id="88f0e-138">MSTest</span></span>](https://github.com/Microsoft/testfx-docs)

<span data-ttu-id="88f0e-139">您可以從以下逐步解說學到更多：</span><span class="sxs-lookup"><span data-stu-id="88f0e-139">You can learn more in the following walkthroughs:</span></span>

:::zone pivot="mstest"

- <span data-ttu-id="88f0e-140">使用 [*MSTest* 與 *C#* 搭配 .NET Core CLI](unit-testing-with-mstest.md) 來建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-140">Create unit tests using [*MSTest* and *C#* with the .NET Core CLI](unit-testing-with-mstest.md).</span></span>
- <span data-ttu-id="88f0e-141">使用 [*MSTest* 與 *F#* 搭配 .NET Core CLI](unit-testing-fsharp-with-mstest.md) 來建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-141">Create unit tests using [*MSTest* and *F#* with the .NET Core CLI](unit-testing-fsharp-with-mstest.md).</span></span>
- <span data-ttu-id="88f0e-142">使用 [*MSTest* 與 *Visual Basic* 搭配 .NET Core CLI](unit-testing-visual-basic-with-mstest.md) 來建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-142">Create unit tests using [*MSTest* and *Visual Basic* with the .NET Core CLI](unit-testing-visual-basic-with-mstest.md).</span></span>

:::zone-end
:::zone pivot="xunit"

- <span data-ttu-id="88f0e-143">使用 [*xUnit* 與 *C#* 搭配 .NET Core CLI](unit-testing-with-dotnet-test.md) 來建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-143">Create unit tests using [*xUnit* and *C#* with the .NET Core CLI](unit-testing-with-dotnet-test.md).</span></span>
- <span data-ttu-id="88f0e-144">使用 [*xUnit* 與 *F#* 搭配 .NET Core CLI](unit-testing-fsharp-with-dotnet-test.md) 來建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-144">Create unit tests using [*xUnit* and *F#* with the .NET Core CLI](unit-testing-fsharp-with-dotnet-test.md).</span></span>
- <span data-ttu-id="88f0e-145">使用 [*xUnit* 與 *Visual Basic* 搭配 .NET Core CLI](unit-testing-visual-basic-with-dotnet-test.md) 來建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-145">Create unit tests using [*xUnit* and *Visual Basic* with the .NET Core CLI](unit-testing-visual-basic-with-dotnet-test.md).</span></span>

:::zone-end
:::zone pivot="nunit"

- <span data-ttu-id="88f0e-146">使用 [*NUnit* 及 *C#* 搭配 .NET Core CLI](unit-testing-with-nunit.md) 建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-146">Create unit tests using [*NUnit* and *C#* with the .NET Core CLI](unit-testing-with-nunit.md).</span></span>
- <span data-ttu-id="88f0e-147">使用 [*NUnit* 及 *#* 搭配 .NET Core CLI](unit-testing-fsharp-with-nunit.md) 建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-147">Create unit tests using [*NUnit* and *F#* with the .NET Core CLI](unit-testing-fsharp-with-nunit.md).</span></span>
- <span data-ttu-id="88f0e-148">使用 [*Unit* 及 *Visual Basic* 搭配 .NET Core CLI](unit-testing-visual-basic-with-nunit.md) 來建立單元測試。</span><span class="sxs-lookup"><span data-stu-id="88f0e-148">Create unit tests using [*NUnit* and *Visual Basic* with the .NET Core CLI](unit-testing-visual-basic-with-nunit.md).</span></span>

:::zone-end

<span data-ttu-id="88f0e-149">您可以從以下文章學到更多：</span><span class="sxs-lookup"><span data-stu-id="88f0e-149">You can learn more in the following articles:</span></span>

- <span data-ttu-id="88f0e-150">Visual Studio Enterprise 為 .NET Core 提供了絕佳的測試工具。</span><span class="sxs-lookup"><span data-stu-id="88f0e-150">Visual Studio Enterprise offers great testing tools for .NET Core.</span></span> <span data-ttu-id="88f0e-151">若要深入了解，可參閱[即時單元測試](/visualstudio/test/live-unit-testing)或[程式碼涵蓋範圍](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md#working-with-code-coverage)。</span><span class="sxs-lookup"><span data-stu-id="88f0e-151">Check out [Live Unit Testing](/visualstudio/test/live-unit-testing) or [code coverage](https://github.com/Microsoft/vstest-docs/blob/master/docs/analyze.md#working-with-code-coverage) to learn more.</span></span>
- <span data-ttu-id="88f0e-152">如需如何執行選擇性單元測試的詳細資訊，請參閱[執行選擇性單元測試](selective-unit-tests.md)或[使用 Visual Studio 來包含及排除測試](/visualstudio/test/live-unit-testing#include-and-exclude-test-projects-and-test-methods)。</span><span class="sxs-lookup"><span data-stu-id="88f0e-152">For more information on how to run selective unit tests, see [Running selective unit tests](selective-unit-tests.md), or [including and excluding tests with Visual Studio](/visualstudio/test/live-unit-testing#include-and-exclude-test-projects-and-test-methods).</span></span>
- <span data-ttu-id="88f0e-153">[如何搭配 xUnit 使用 .NET Core 和 Visual Studio](https://xunit.github.io/docs/getting-started-dotnet-core.html)。</span><span class="sxs-lookup"><span data-stu-id="88f0e-153">[How to use xUnit with .NET Core and Visual Studio](https://xunit.github.io/docs/getting-started-dotnet-core.html).</span></span>
