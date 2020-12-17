---
title: 利用 NUnit 與 .NET Core 進行 C# 單元測試
description: 使用 dotnet test 與 NUnit 逐步建置解決方案範例的互動式體驗，了解 C# 與 .NET Core 中的單元測試概念。
author: rprouse
ms.date: 08/31/2018
ms.openlocfilehash: 9c9982b047f7b3c5a03ecdd2fabfa2a0edce4558
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633932"
---
# <a name="unit-testing-c-with-nunit-and-net-core"></a><span data-ttu-id="bcf85-103">利用 NUnit 與 .NET Core 進行 C# 單元測試</span><span class="sxs-lookup"><span data-stu-id="bcf85-103">Unit testing C# with NUnit and .NET Core</span></span>

<span data-ttu-id="bcf85-104">本教學課程會引導您逐步進行建置範例方案的互動式體驗，以了解單元測試概念。</span><span class="sxs-lookup"><span data-stu-id="bcf85-104">This tutorial takes you through an interactive experience building a sample solution step-by-step to learn unit testing concepts.</span></span> <span data-ttu-id="bcf85-105">如果您想要使用預先建置的方案進行教學課程，請在開始之前[檢視或下載範例程式碼](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/)。</span><span class="sxs-lookup"><span data-stu-id="bcf85-105">If you prefer to follow the tutorial using a pre-built solution, [view or download the sample code](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/) before you begin.</span></span> <span data-ttu-id="bcf85-106">如需下載指示，請參閱[範例和教學課程](../../samples-and-tutorials/index.md#view-and-download-samples)。</span><span class="sxs-lookup"><span data-stu-id="bcf85-106">For download instructions, see [Samples and Tutorials](../../samples-and-tutorials/index.md#view-and-download-samples).</span></span>

[!INCLUDE [testing an ASP.NET Core project from .NET Core](../../../includes/core-testing-note-aspnet.md)]

## <a name="prerequisites"></a><span data-ttu-id="bcf85-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="bcf85-107">Prerequisites</span></span>

- <span data-ttu-id="bcf85-108">[.NET Core 2.1 SDK](https://dotnet.microsoft.com/download) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bcf85-108">[.NET Core 2.1 SDK](https://dotnet.microsoft.com/download) or later versions.</span></span>
- <span data-ttu-id="bcf85-109">您偏好的文字編輯器或程式碼編輯器。</span><span class="sxs-lookup"><span data-stu-id="bcf85-109">A text editor or code editor of your choice.</span></span>

## <a name="creating-the-source-project"></a><span data-ttu-id="bcf85-110">建立來源專案</span><span class="sxs-lookup"><span data-stu-id="bcf85-110">Creating the source project</span></span>

<span data-ttu-id="bcf85-111">開啟 Shell 視窗。</span><span class="sxs-lookup"><span data-stu-id="bcf85-111">Open a shell window.</span></span> <span data-ttu-id="bcf85-112">建立名稱為 *unit-testing-using-nunit* 的目錄來放置解決方案。</span><span class="sxs-lookup"><span data-stu-id="bcf85-112">Create a directory called *unit-testing-using-nunit* to hold the solution.</span></span> <span data-ttu-id="bcf85-113">在此新目錄中，執行下列命令以針對類別庫與測試專案建立新方案檔：</span><span class="sxs-lookup"><span data-stu-id="bcf85-113">Inside this new directory, run the following command to create a new solution file for the class library and the test project:</span></span>

```dotnetcli
dotnet new sln
```

<span data-ttu-id="bcf85-114">接著，建立 *PrimeService* 目錄。</span><span class="sxs-lookup"><span data-stu-id="bcf85-114">Next, create a *PrimeService* directory.</span></span> <span data-ttu-id="bcf85-115">下列大綱顯示到目前為止的目錄與檔案結構：</span><span class="sxs-lookup"><span data-stu-id="bcf85-115">The following outline shows the directory and file structure so far:</span></span>

```console
/unit-testing-using-nunit
    unit-testing-using-nunit.sln
    /PrimeService
```

<span data-ttu-id="bcf85-116">將 *PrimeService* 設為目前的目錄，然後執行下列命令以建立來源專案：</span><span class="sxs-lookup"><span data-stu-id="bcf85-116">Make *PrimeService* the current directory and run the following command to create the source project:</span></span>

```dotnetcli
dotnet new classlib
```

<span data-ttu-id="bcf85-117">將 *Class1.cs* 重新命名為 *PrimeService.cs*。</span><span class="sxs-lookup"><span data-stu-id="bcf85-117">Rename *Class1.cs* to *PrimeService.cs*.</span></span> <span data-ttu-id="bcf85-118">建立會失敗的 `PrimeService` 類別實作：</span><span class="sxs-lookup"><span data-stu-id="bcf85-118">You create a failing implementation of the `PrimeService` class:</span></span>

```csharp
using System;

namespace Prime.Services
{
    public class PrimeService
    {
        public bool IsPrime(int candidate)
        {
            throw new NotImplementedException("Please create a test first.");
        }
    }
}
```

<span data-ttu-id="bcf85-119">將目錄變更回 *unit-testing-using-nunit* 目錄。</span><span class="sxs-lookup"><span data-stu-id="bcf85-119">Change the directory back to the *unit-testing-using-nunit* directory.</span></span> <span data-ttu-id="bcf85-120">執行下列命令，將類別庫專案新增至方案：</span><span class="sxs-lookup"><span data-stu-id="bcf85-120">Run the following command to add the class library project to the solution:</span></span>

```dotnetcli
dotnet sln add PrimeService/PrimeService.csproj
```

## <a name="creating-the-test-project"></a><span data-ttu-id="bcf85-121">建立測試專案</span><span class="sxs-lookup"><span data-stu-id="bcf85-121">Creating the test project</span></span>

<span data-ttu-id="bcf85-122">接著，建立 *PrimeService.Tests* 目錄。</span><span class="sxs-lookup"><span data-stu-id="bcf85-122">Next, create the *PrimeService.Tests* directory.</span></span> <span data-ttu-id="bcf85-123">下列大綱顯示目錄結構：</span><span class="sxs-lookup"><span data-stu-id="bcf85-123">The following outline shows the directory structure:</span></span>

```console
/unit-testing-using-nunit
    unit-testing-using-nunit.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
```

<span data-ttu-id="bcf85-124">將 *PrimeService.Tests* 目錄設為目前的目錄，然後使用下列命令建立新的專案：</span><span class="sxs-lookup"><span data-stu-id="bcf85-124">Make the *PrimeService.Tests* directory the current directory and create a new project using the following command:</span></span>

```dotnetcli
dotnet new nunit
```

<span data-ttu-id="bcf85-125">[dotnet new](../tools/dotnet-new.md) 命令會建立將 NUnit 用作測試程式庫的測試專案。</span><span class="sxs-lookup"><span data-stu-id="bcf85-125">The [dotnet new](../tools/dotnet-new.md) command creates a test project that uses NUnit as the test library.</span></span> <span data-ttu-id="bcf85-126">產生的範本會在 *PrimeService.Tests.csproj* 檔案中設定測試執行器：</span><span class="sxs-lookup"><span data-stu-id="bcf85-126">The generated template configures the test runner in the *PrimeService.Tests.csproj* file:</span></span>

[!code-xml[Packages](~/samples/snippets/core/testing/unit-testing-using-nunit/csharp/PrimeService.Tests/PrimeService.Tests.csproj#Packages)]

<span data-ttu-id="bcf85-127">測試專案需要其他套件來建立和執行單元測試。</span><span class="sxs-lookup"><span data-stu-id="bcf85-127">The test project requires other packages to create and run unit tests.</span></span> <span data-ttu-id="bcf85-128">上一個步驟中的 `dotnet new`，新增了 Microsoft 測試 SDK、NUnit 測試架構以及 NUnit 測試配接器。</span><span class="sxs-lookup"><span data-stu-id="bcf85-128">`dotnet new` in the previous step added the Microsoft test SDK, the NUnit test framework, and the NUnit test adapter.</span></span> <span data-ttu-id="bcf85-129">現在，將 `PrimeService` 類別庫新增為專案的另一個相依性。</span><span class="sxs-lookup"><span data-stu-id="bcf85-129">Now, add the `PrimeService` class library as another dependency to the project.</span></span> <span data-ttu-id="bcf85-130">使用 [`dotnet add reference`](../tools/dotnet-add-reference.md) 命令：</span><span class="sxs-lookup"><span data-stu-id="bcf85-130">Use the [`dotnet add reference`](../tools/dotnet-add-reference.md) command:</span></span>

```dotnetcli
dotnet add reference ../PrimeService/PrimeService.csproj
```

<span data-ttu-id="bcf85-131">您可以在 GitHub 的[範例存放庫](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService.Tests.csproj)中看到完整檔案。</span><span class="sxs-lookup"><span data-stu-id="bcf85-131">You can see the entire file in the [samples repository](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService.Tests.csproj) on GitHub.</span></span>

<span data-ttu-id="bcf85-132">下列大綱顯示最終方案配置：</span><span class="sxs-lookup"><span data-stu-id="bcf85-132">The following outline shows the final solution layout:</span></span>

```console
/unit-testing-using-nunit
    unit-testing-using-nunit.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
        Test Source Files
        PrimeService.Tests.csproj
```

<span data-ttu-id="bcf85-133">在 *unit-testing-using-nunit* 目錄中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="bcf85-133">Execute the following command in the *unit-testing-using-nunit* directory:</span></span>

```dotnetcli
dotnet sln add ./PrimeService.Tests/PrimeService.Tests.csproj
```

## <a name="creating-the-first-test"></a><span data-ttu-id="bcf85-134">建立第一個測試</span><span class="sxs-lookup"><span data-stu-id="bcf85-134">Creating the first test</span></span>

<span data-ttu-id="bcf85-135">撰寫一個會失敗的測試，再使其通過，然後重複這個過程。</span><span class="sxs-lookup"><span data-stu-id="bcf85-135">You write one failing test, make it pass, then repeat the process.</span></span> <span data-ttu-id="bcf85-136">在 *PrimeService.Tests* 目錄中，將 *UnitTest1.cs* 檔案重新命名為 *PrimeService_IsPrimeShould.cs*，並將其整個內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="bcf85-136">In the *PrimeService.Tests* directory, rename the *UnitTest1.cs* file to *PrimeService_IsPrimeShould.cs* and replace its entire contents with the following code:</span></span>

```csharp
using NUnit.Framework;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    [TestFixture]
    public class PrimeService_IsPrimeShould
    {
        private PrimeService _primeService;

        [SetUp]
        public void SetUp()
        {
            _primeService = new PrimeService();
        }

        [Test]
        public void IsPrime_InputIs1_ReturnFalse()
        {
            var result = _primeService.IsPrime(1);

            Assert.IsFalse(result, "1 should not be prime");
        }
    }
}
```

<span data-ttu-id="bcf85-137">`[TestFixture]` 屬性代表包含單元測試的類別。</span><span class="sxs-lookup"><span data-stu-id="bcf85-137">The `[TestFixture]` attribute denotes a class that contains unit tests.</span></span> <span data-ttu-id="bcf85-138">`[Test]` 屬性指出方法是測試方法。</span><span class="sxs-lookup"><span data-stu-id="bcf85-138">The `[Test]` attribute indicates a method is a test method.</span></span>

<span data-ttu-id="bcf85-139">儲存此檔案，然後執行 [`dotnet test`](../tools/dotnet-test.md) 以建立測試和類別庫，然後執行測試。</span><span class="sxs-lookup"><span data-stu-id="bcf85-139">Save this file and execute [`dotnet test`](../tools/dotnet-test.md) to build the tests and the class library and then run the tests.</span></span> <span data-ttu-id="bcf85-140">NUnit 測試執行器包含執行測試的程式進入點。</span><span class="sxs-lookup"><span data-stu-id="bcf85-140">The NUnit test runner contains the program entry point to run your tests.</span></span> <span data-ttu-id="bcf85-141">`dotnet test` 會使用您建立的單元測試專案來開始測試執行器。</span><span class="sxs-lookup"><span data-stu-id="bcf85-141">`dotnet test` starts the test runner using the unit test project you've created.</span></span>

<span data-ttu-id="bcf85-142">您的測試失敗。</span><span class="sxs-lookup"><span data-stu-id="bcf85-142">Your test fails.</span></span> <span data-ttu-id="bcf85-143">您尚未建立實作。</span><span class="sxs-lookup"><span data-stu-id="bcf85-143">You haven't created the implementation yet.</span></span> <span data-ttu-id="bcf85-144">在可運作的 `PrimeService` 類別中撰寫最簡單的程式碼以讓此測試成功：</span><span class="sxs-lookup"><span data-stu-id="bcf85-144">Make this test pass by writing the simplest code in the `PrimeService` class that works:</span></span>

```csharp
public bool IsPrime(int candidate)
{
    if (candidate == 1)
    {
        return false;
    }
    throw new NotImplementedException("Please create a test first.");
}
```

<span data-ttu-id="bcf85-145">在 *unit-testing-using-nunit* 目錄中，再次執行 `dotnet test`。</span><span class="sxs-lookup"><span data-stu-id="bcf85-145">In the *unit-testing-using-nunit* directory, run `dotnet test` again.</span></span> <span data-ttu-id="bcf85-146">`dotnet test` 命令會依序執行 `PrimeService` 專案和 `PrimeService.Tests` 專案的建置。</span><span class="sxs-lookup"><span data-stu-id="bcf85-146">The `dotnet test` command runs a build for the `PrimeService` project and then for the `PrimeService.Tests` project.</span></span> <span data-ttu-id="bcf85-147">建置這兩個專案之後，它將會執行此單一測試。</span><span class="sxs-lookup"><span data-stu-id="bcf85-147">After building both projects, it runs this single test.</span></span> <span data-ttu-id="bcf85-148">測試通過。</span><span class="sxs-lookup"><span data-stu-id="bcf85-148">It passes.</span></span>

## <a name="adding-more-features"></a><span data-ttu-id="bcf85-149">新增更多功能</span><span class="sxs-lookup"><span data-stu-id="bcf85-149">Adding more features</span></span>

<span data-ttu-id="bcf85-150">現在，您已經讓一個測試順利通過，您可以撰寫更多測試。</span><span class="sxs-lookup"><span data-stu-id="bcf85-150">Now that you've made one test pass, it's time to write more.</span></span> <span data-ttu-id="bcf85-151">還有一些其他適用於質數 0、-1 的簡單案例。</span><span class="sxs-lookup"><span data-stu-id="bcf85-151">There are a few other simple cases for prime numbers: 0, -1.</span></span> <span data-ttu-id="bcf85-152">您可以使用 `[Test]` 屬性來加入新測試，但很快就會單調乏味。</span><span class="sxs-lookup"><span data-stu-id="bcf85-152">You could add new tests with the `[Test]` attribute, but that quickly becomes tedious.</span></span> <span data-ttu-id="bcf85-153">另有其他 NUnit 屬性可供您撰寫類似測試的套件。</span><span class="sxs-lookup"><span data-stu-id="bcf85-153">There are other NUnit attributes that enable you to write a suite of similar tests.</span></span>  <span data-ttu-id="bcf85-154">`[TestCase]` 屬性可用於建立執行相同程式碼，但輸入引數不同的測試套件。</span><span class="sxs-lookup"><span data-stu-id="bcf85-154">A `[TestCase]` attribute is used to create a suite of tests that execute the same code but have different input arguments.</span></span> <span data-ttu-id="bcf85-155">您可以使用 `[TestCase]` 屬性來指定這些輸入值。</span><span class="sxs-lookup"><span data-stu-id="bcf85-155">You can use the `[TestCase]` attribute to specify values for those inputs.</span></span>

<span data-ttu-id="bcf85-156">您不需要建立新的測試，只要套用此屬性來建立單一資料驅動型測試即可。</span><span class="sxs-lookup"><span data-stu-id="bcf85-156">Instead of creating new tests, apply this attribute to create a single data driven test.</span></span> <span data-ttu-id="bcf85-157">資料驅動型測試是一種測試方法，其會測試數個低於二 (最小質數) 的值：</span><span class="sxs-lookup"><span data-stu-id="bcf85-157">The data driven test is a method that tests several values less than two, which is the lowest prime number:</span></span>

[!code-csharp[Sample_TestCode](~/samples/snippets/core/testing/unit-testing-using-nunit/csharp/PrimeService.Tests/PrimeService_IsPrimeShould.cs?name=Sample_TestCode)]

<span data-ttu-id="bcf85-158">執行 `dotnet test`，然後會有兩個測試失敗。</span><span class="sxs-lookup"><span data-stu-id="bcf85-158">Run `dotnet test`, and two of these tests fail.</span></span> <span data-ttu-id="bcf85-159">若要讓所有測試都能通過，請變更 *PrimeService.cs* 檔案中 `Main` 方法開頭處的 `if` 子句：</span><span class="sxs-lookup"><span data-stu-id="bcf85-159">To make all of the tests pass, change the `if` clause at the beginning of the `Main` method in the *PrimeService.cs* file:</span></span>

```csharp
if (candidate < 2)
```

<span data-ttu-id="bcf85-160">繼續在主要程式庫中新增更多測試、更多理論和更多程式碼，以反覆執行。</span><span class="sxs-lookup"><span data-stu-id="bcf85-160">Continue to iterate by adding more tests, more theories, and more code in the main library.</span></span> <span data-ttu-id="bcf85-161">您有[測試的完成版](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService_IsPrimeShould.cs)和[程式庫的完整實作](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService/PrimeService.cs)。</span><span class="sxs-lookup"><span data-stu-id="bcf85-161">You have the [finished version of the tests](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService.Tests/PrimeService_IsPrimeShould.cs) and the [complete implementation of the library](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-nunit/PrimeService/PrimeService.cs).</span></span>

<span data-ttu-id="bcf85-162">您已建置好小型的程式庫和該程式庫的一組單元測試，</span><span class="sxs-lookup"><span data-stu-id="bcf85-162">You've built a small library and a set of unit tests for that library.</span></span> <span data-ttu-id="bcf85-163">您已建立方案結構，因此加入新套件與測試是一般工作流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="bcf85-163">You've structured the solution so that adding new packages and tests is part of the normal workflow.</span></span> <span data-ttu-id="bcf85-164">您已集中大部分的時間與精力以解決應用程式目標。</span><span class="sxs-lookup"><span data-stu-id="bcf85-164">You've concentrated most of your time and effort on solving the goals of the application.</span></span>
