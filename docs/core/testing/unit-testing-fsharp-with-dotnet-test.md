---
title: 使用 dotnet test 與 xUnit 為 .NET Core 中的 F# 進行單元測試
description: 透過逐步使用 dotnet test 和 xUnit 建置範例方案的互動式體驗，了解 .NET Core 中 F# 的單元測試概念。
author: billwagner
ms.author: wiwagn
ms.date: 08/30/2017
ms.openlocfilehash: e0f2b6f88a650f412148f51cc0236fa46ed8c618
ms.sourcegitcommit: c4a15c6c4ecbb8a46ad4e67d9b3ab9b8b031d849
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88656549"
---
# <a name="unit-testing-f-libraries-in-net-core-using-dotnet-test-and-xunit"></a><span data-ttu-id="4339a-103">使用 dotnet test 與 xUnit 為 .NET Core 中的 F# 程式庫進行單元測試</span><span class="sxs-lookup"><span data-stu-id="4339a-103">Unit testing F# libraries in .NET Core using dotnet test and xUnit</span></span>

<span data-ttu-id="4339a-104">本教學課程會引導您逐步進行建置範例方案的互動式體驗，以了解單元測試概念。</span><span class="sxs-lookup"><span data-stu-id="4339a-104">This tutorial takes you through an interactive experience building a sample solution step-by-step to learn unit testing concepts.</span></span> <span data-ttu-id="4339a-105">如果您想要使用預先建置的方案進行教學課程，請在開始之前[檢視或下載範例程式碼](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-with-fsharp/)。</span><span class="sxs-lookup"><span data-stu-id="4339a-105">If you prefer to follow the tutorial using a pre-built solution, [view or download the sample code](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-with-fsharp/) before you begin.</span></span> <span data-ttu-id="4339a-106">如需下載指示，請參閱[範例和教學課程](../../samples-and-tutorials/index.md#view-and-download-samples)。</span><span class="sxs-lookup"><span data-stu-id="4339a-106">For download instructions, see [Samples and Tutorials](../../samples-and-tutorials/index.md#view-and-download-samples).</span></span>

[!INCLUDE [testing an ASP.NET Core project from .NET Core](../../../includes/core-testing-note-aspnet.md)]

## <a name="creating-the-source-project"></a><span data-ttu-id="4339a-107">建立來源專案</span><span class="sxs-lookup"><span data-stu-id="4339a-107">Creating the source project</span></span>

<span data-ttu-id="4339a-108">開啟 Shell 視窗。</span><span class="sxs-lookup"><span data-stu-id="4339a-108">Open a shell window.</span></span> <span data-ttu-id="4339a-109">建立名為 *unit-testing-with-fsharp* 的目錄來放置方案。</span><span class="sxs-lookup"><span data-stu-id="4339a-109">Create a directory called *unit-testing-with-fsharp* to hold the solution.</span></span>
<span data-ttu-id="4339a-110">在這個新目錄中，執行 `dotnet new sln` 以建立新方案。</span><span class="sxs-lookup"><span data-stu-id="4339a-110">Inside this new directory, run `dotnet new sln` to create a new solution.</span></span> <span data-ttu-id="4339a-111">這樣可讓您更輕鬆地管理類別庫與單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="4339a-111">This makes it easier to manage both the class library and the unit test project.</span></span>
<span data-ttu-id="4339a-112">在方案目錄中，建立 *MathService* 目錄。</span><span class="sxs-lookup"><span data-stu-id="4339a-112">Inside the solution directory, create a *MathService* directory.</span></span> <span data-ttu-id="4339a-113">到目前為止，目錄與檔案結構如下所示：</span><span class="sxs-lookup"><span data-stu-id="4339a-113">The directory and file structure thus far is shown below:</span></span>

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
```

<span data-ttu-id="4339a-114">將 *>mathservice.tests* 設為目前的目錄，然後執行 `dotnet new classlib -lang "F#"` 以建立來源專案。</span><span class="sxs-lookup"><span data-stu-id="4339a-114">Make *MathService* the current directory, and run `dotnet new classlib -lang "F#"` to create the source project.</span></span> <span data-ttu-id="4339a-115">您建立會失敗的數學服務實作：</span><span class="sxs-lookup"><span data-stu-id="4339a-115">You'll create a failing implementation of the math service:</span></span>

```fsharp
module MyMath =
    let squaresOfOdds xs = raise (System.NotImplementedException("You haven't written a test yet!"))
```

<span data-ttu-id="4339a-116">將目錄變更回 *unit-testing-with-fsharp* 目錄。</span><span class="sxs-lookup"><span data-stu-id="4339a-116">Change the directory back to the *unit-testing-with-fsharp* directory.</span></span> <span data-ttu-id="4339a-117">執行 `dotnet sln add .\MathService\MathService.fsproj` 以將類別庫專案加入方案中。</span><span class="sxs-lookup"><span data-stu-id="4339a-117">Run `dotnet sln add .\MathService\MathService.fsproj` to add the class library project to the solution.</span></span>

## <a name="creating-the-test-project"></a><span data-ttu-id="4339a-118">建立測試專案</span><span class="sxs-lookup"><span data-stu-id="4339a-118">Creating the test project</span></span>

<span data-ttu-id="4339a-119">接著，建立 *MathService.Tests* 目錄。</span><span class="sxs-lookup"><span data-stu-id="4339a-119">Next, create the *MathService.Tests* directory.</span></span> <span data-ttu-id="4339a-120">下列大綱顯示目錄結構：</span><span class="sxs-lookup"><span data-stu-id="4339a-120">The following outline shows the directory structure:</span></span>

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
```

<span data-ttu-id="4339a-121">將 *MathService.Tests* 目錄設定為目前的目錄，然後使用 `dotnet new xunit -lang "F#"` 建立新專案。</span><span class="sxs-lookup"><span data-stu-id="4339a-121">Make the *MathService.Tests* directory the current directory and create a new project using `dotnet new xunit -lang "F#"`.</span></span> <span data-ttu-id="4339a-122">這樣會建立將 xUnit 作為測試程式庫的測試專案。</span><span class="sxs-lookup"><span data-stu-id="4339a-122">This creates a test project that uses xUnit as the test library.</span></span> <span data-ttu-id="4339a-123">產生的範本會在 *MathServiceTests.fsproj* 中設定測試執行器：</span><span class="sxs-lookup"><span data-stu-id="4339a-123">The generated template configures the test runner in the *MathServiceTests.fsproj*:</span></span>

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0-preview-20170628-02" />
  <PackageReference Include="xunit" Version="2.2.0" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0" />
</ItemGroup>
```

<span data-ttu-id="4339a-124">測試專案需要其他套件來建立和執行單元測試。</span><span class="sxs-lookup"><span data-stu-id="4339a-124">The test project requires other packages to create and run unit tests.</span></span> <span data-ttu-id="4339a-125">上一個步驟中的 `dotnet new` 已新增 xUnit 和 xUnit 執行器。</span><span class="sxs-lookup"><span data-stu-id="4339a-125">`dotnet new` in the previous step added xUnit and the xUnit runner.</span></span> <span data-ttu-id="4339a-126">現在，將 `MathService` 類別庫新增為專案的另一個相依性。</span><span class="sxs-lookup"><span data-stu-id="4339a-126">Now, add the `MathService` class library as another dependency to the project.</span></span> <span data-ttu-id="4339a-127">使用 `dotnet add reference` 命令：</span><span class="sxs-lookup"><span data-stu-id="4339a-127">Use the `dotnet add reference` command:</span></span>

```dotnetcli
dotnet add reference ../MathService/MathService.fsproj
```

<span data-ttu-id="4339a-128">您可以在 GitHub 的[範例存放庫](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-with-fsharp/MathService.Tests/MathService.Tests.fsproj)中看到完整檔案。</span><span class="sxs-lookup"><span data-stu-id="4339a-128">You can see the entire file in the [samples repository](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-with-fsharp/MathService.Tests/MathService.Tests.fsproj) on GitHub.</span></span>

<span data-ttu-id="4339a-129">您有下列最終方案配置：</span><span class="sxs-lookup"><span data-stu-id="4339a-129">You have the following final solution layout:</span></span>

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
        Test Source Files
        MathServiceTests.fsproj
```

<span data-ttu-id="4339a-130">執行 *unit-testing-with-fsharp* 目錄中的 `dotnet sln add .\MathService.Tests\MathService.Tests.fsproj`。</span><span class="sxs-lookup"><span data-stu-id="4339a-130">Execute `dotnet sln add .\MathService.Tests\MathService.Tests.fsproj` in the *unit-testing-with-fsharp* directory.</span></span>

## <a name="creating-the-first-test"></a><span data-ttu-id="4339a-131">建立第一個測試</span><span class="sxs-lookup"><span data-stu-id="4339a-131">Creating the first test</span></span>

<span data-ttu-id="4339a-132">撰寫一個會失敗的測試，再使其通過，然後重複這個過程。</span><span class="sxs-lookup"><span data-stu-id="4339a-132">You write one failing test, make it pass, then repeat the process.</span></span> <span data-ttu-id="4339a-133">開啟 *Tests.fs* 並加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="4339a-133">Open *Tests.fs* and add the following code:</span></span>

```fsharp
[<Fact>]
let ``My test`` () =
    Assert.True(true)

[<Fact>]
let ``Fail every time`` () = Assert.True(false)
```

<span data-ttu-id="4339a-134">`[<Fact>]` 屬性表示由測試執行器執行的測試方法。</span><span class="sxs-lookup"><span data-stu-id="4339a-134">The `[<Fact>]` attribute denotes a test method that is run by the test runner.</span></span> <span data-ttu-id="4339a-135">從 *unit-testing-with-fsharp*，執行 `dotnet test` 來建置測試和類別庫，然後執行測試。</span><span class="sxs-lookup"><span data-stu-id="4339a-135">From the *unit-testing-with-fsharp*, execute `dotnet test` to build the tests and the class library and then run the tests.</span></span> <span data-ttu-id="4339a-136">xUnit 測試執行器包含執行測試的程式進入點。</span><span class="sxs-lookup"><span data-stu-id="4339a-136">The xUnit test runner contains the program entry point to run your tests.</span></span> <span data-ttu-id="4339a-137">`dotnet test` 會使用您建立的單元測試專案來開始測試執行器。</span><span class="sxs-lookup"><span data-stu-id="4339a-137">`dotnet test` starts the test runner using the unit test project you've created.</span></span>

<span data-ttu-id="4339a-138">這兩個測試會顯示最基本的成功和失敗測試。</span><span class="sxs-lookup"><span data-stu-id="4339a-138">These two tests show the most basic passing and failing tests.</span></span> <span data-ttu-id="4339a-139">`My test` 成功，而 `Fail every time` 失敗。</span><span class="sxs-lookup"><span data-stu-id="4339a-139">`My test` passes, and `Fail every time` fails.</span></span> <span data-ttu-id="4339a-140">現在，針對 `squaresOfOdds` 方法建立測試。</span><span class="sxs-lookup"><span data-stu-id="4339a-140">Now, create a test for the `squaresOfOdds` method.</span></span> <span data-ttu-id="4339a-141">`squaresOfOdds` 方法會傳回屬於輸入序列一部分的所有奇數整數值平方序列。</span><span class="sxs-lookup"><span data-stu-id="4339a-141">The `squaresOfOdds` method returns a sequence of the squares of all odd integer values that are part of the input sequence.</span></span> <span data-ttu-id="4339a-142">您能以反覆方式建立會驗證功能的測試，而不需要嘗試一次撰寫所有那些函式。</span><span class="sxs-lookup"><span data-stu-id="4339a-142">Rather than trying to write all of those functions at once, you can iteratively create tests that validate the functionality.</span></span> <span data-ttu-id="4339a-143">將每個測試設定為通過表示為方法建立必要功能。</span><span class="sxs-lookup"><span data-stu-id="4339a-143">Making each test pass means creating the necessary functionality for the method.</span></span>

<span data-ttu-id="4339a-144">我們所能撰寫的最簡單測試是呼叫 `squaresOfOdds` 並傳遞所有偶數，其中結果應該是空整數序列。</span><span class="sxs-lookup"><span data-stu-id="4339a-144">The simplest test we can write is to call `squaresOfOdds` with all even numbers, where the result should be an empty sequence of integers.</span></span>  <span data-ttu-id="4339a-145">該測試如下：</span><span class="sxs-lookup"><span data-stu-id="4339a-145">Here's that test:</span></span>

```fsharp
[<Fact>]
let ``Sequence of Evens returns empty collection`` () =
    let expected = Seq.empty<int>
    let actual = MyMath.squaresOfOdds [2; 4; 6; 8; 10]
    Assert.Equal<Collections.Generic.IEnumerable<int>>(expected, actual)
```

<span data-ttu-id="4339a-146">您的測試失敗。</span><span class="sxs-lookup"><span data-stu-id="4339a-146">Your test fails.</span></span> <span data-ttu-id="4339a-147">您尚未建立實作。</span><span class="sxs-lookup"><span data-stu-id="4339a-147">You haven't created the implementation yet.</span></span> <span data-ttu-id="4339a-148">在可運作的 `MathService` 類別中撰寫最簡單的程式碼以讓此測試成功：</span><span class="sxs-lookup"><span data-stu-id="4339a-148">Make this test pass by writing the simplest code in the `MathService` class that works:</span></span>

```fsharp
let squaresOfOdds xs =
    Seq.empty<int>
```

<span data-ttu-id="4339a-149">在 *unit-testing-with-fsharp* 目錄中，重新執行 `dotnet test`。</span><span class="sxs-lookup"><span data-stu-id="4339a-149">In the *unit-testing-with-fsharp* directory, run `dotnet test` again.</span></span> <span data-ttu-id="4339a-150">`dotnet test` 命令會依序執行 `MathService` 專案和 `MathService.Tests` 專案的建置。</span><span class="sxs-lookup"><span data-stu-id="4339a-150">The `dotnet test` command runs a build for the `MathService` project and then for the `MathService.Tests` project.</span></span> <span data-ttu-id="4339a-151">建置這兩個專案之後，它將會執行此單一測試。</span><span class="sxs-lookup"><span data-stu-id="4339a-151">After building both projects, it runs this single test.</span></span> <span data-ttu-id="4339a-152">測試通過。</span><span class="sxs-lookup"><span data-stu-id="4339a-152">It passes.</span></span>

## <a name="completing-the-requirements"></a><span data-ttu-id="4339a-153">完成需求</span><span class="sxs-lookup"><span data-stu-id="4339a-153">Completing the requirements</span></span>

<span data-ttu-id="4339a-154">現在，您已經讓一個測試順利通過，您可以撰寫更多測試。</span><span class="sxs-lookup"><span data-stu-id="4339a-154">Now that you've made one test pass, it's time to write more.</span></span> <span data-ttu-id="4339a-155">下一個簡單案例可搭配所具有的唯一奇數是 `1` 的序列運作。</span><span class="sxs-lookup"><span data-stu-id="4339a-155">The next simple case works with a sequence whose only odd number is `1`.</span></span> <span data-ttu-id="4339a-156">數字 1 比較簡單，因為 1 的平方是 1。</span><span class="sxs-lookup"><span data-stu-id="4339a-156">The number 1 is easier because the square of 1 is 1.</span></span> <span data-ttu-id="4339a-157">該下一個測試如下：</span><span class="sxs-lookup"><span data-stu-id="4339a-157">Here's that next test:</span></span>

```fsharp
[<Fact>]
let ``Sequences of Ones and Evens returns Ones`` () =
    let expected = [1; 1; 1; 1]
    let actual = MyMath.squaresOfOdds [2; 1; 4; 1; 6; 1; 8; 1; 10]
    Assert.Equal<Collections.Generic.IEnumerable<int>>(expected, actual)
```

<span data-ttu-id="4339a-158">執行 `dotnet test` 會執行您的測試並顯示新測試失敗。</span><span class="sxs-lookup"><span data-stu-id="4339a-158">Executing `dotnet test` runs your tests and shows you that the new test fails.</span></span> <span data-ttu-id="4339a-159">現在，更新 `squaresOfOdds` 方法以處理此新測試。</span><span class="sxs-lookup"><span data-stu-id="4339a-159">Now, update the `squaresOfOdds` method to handle this new test.</span></span> <span data-ttu-id="4339a-160">您會將所有偶數從序列中篩選出來，以使此測試通過。</span><span class="sxs-lookup"><span data-stu-id="4339a-160">You filter all the even numbers out of the sequence to make this test pass.</span></span> <span data-ttu-id="4339a-161">您可以透過撰寫小型篩選函式並使用 `Seq.filter` 來完成此動作：</span><span class="sxs-lookup"><span data-stu-id="4339a-161">You can do that by writing a small filter function and using `Seq.filter`:</span></span>

```fsharp
let private isOdd x = x % 2 <> 0

let squaresOfOdds xs =
    xs
    |> Seq.filter isOdd
```

<span data-ttu-id="4339a-162">還有一個步驟必須執行：計算每個奇數的平方。</span><span class="sxs-lookup"><span data-stu-id="4339a-162">There's one more step to go: square each of the odd numbers.</span></span> <span data-ttu-id="4339a-163">透過撰寫新測試以開始：</span><span class="sxs-lookup"><span data-stu-id="4339a-163">Start by writing a new test:</span></span>

```fsharp
[<Fact>]
let ``SquaresOfOdds works`` () =
    let expected = [1; 9; 25; 49; 81]
    let actual = MyMath.squaresOfOdds [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
    Assert.Equal(expected, actual)
```

<span data-ttu-id="4339a-164">您可以透過將已篩選的序列以管線方式傳遞到對應作業，以計算每個奇數的平方，來修正測試：</span><span class="sxs-lookup"><span data-stu-id="4339a-164">You can fix the test by piping the filtered sequence through a map operation to compute the square of each odd number:</span></span>

```fsharp
let private square x = x * x
let private isOdd x = x % 2 <> 0

let squaresOfOdds xs =
    xs
    |> Seq.filter isOdd
    |> Seq.map square
```

<span data-ttu-id="4339a-165">您已建置好小型的程式庫和該程式庫的一組單元測試，</span><span class="sxs-lookup"><span data-stu-id="4339a-165">You've built a small library and a set of unit tests for that library.</span></span> <span data-ttu-id="4339a-166">您已建立方案結構，因此加入新套件與測試是一般工作流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="4339a-166">You've structured the solution so that adding new packages and tests is part of the normal workflow.</span></span> <span data-ttu-id="4339a-167">您已集中大部分的時間與精力以解決應用程式目標。</span><span class="sxs-lookup"><span data-stu-id="4339a-167">You've concentrated most of your time and effort on solving the goals of the application.</span></span>

## <a name="see-also"></a><span data-ttu-id="4339a-168">請參閱</span><span class="sxs-lookup"><span data-stu-id="4339a-168">See also</span></span>

- [<span data-ttu-id="4339a-169">dotnet new</span><span class="sxs-lookup"><span data-stu-id="4339a-169">dotnet new</span></span>](../tools/dotnet-new.md)
- [<span data-ttu-id="4339a-170">dotnet sln</span><span class="sxs-lookup"><span data-stu-id="4339a-170">dotnet sln</span></span>](../tools/dotnet-new.md)
- [<span data-ttu-id="4339a-171">dotnet add reference</span><span class="sxs-lookup"><span data-stu-id="4339a-171">dotnet add reference</span></span>](../tools/dotnet-add-reference.md)
- [<span data-ttu-id="4339a-172">dotnet test</span><span class="sxs-lookup"><span data-stu-id="4339a-172">dotnet test</span></span>](../tools/dotnet-test.md)
