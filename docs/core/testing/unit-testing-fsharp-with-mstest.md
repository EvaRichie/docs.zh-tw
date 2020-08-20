---
title: 使用 dotnet test 與 MSTest 為 .NET Core 中的 F# 進行單元測試
description: 透過逐步使用 dotnet test 和 MSTest 建置範例方案的互動式體驗，了解 .NET Core 中 F# 的單元測試概念。
author: billwagner
ms.author: wiwagn
ms.date: 08/30/2017
ms.openlocfilehash: 08aa0b4a36f399d4439a0f3b34e88a1b51e98215
ms.sourcegitcommit: c4a15c6c4ecbb8a46ad4e67d9b3ab9b8b031d849
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2020
ms.locfileid: "88656536"
---
# <a name="unit-testing-f-libraries-in-net-core-using-dotnet-test-and-mstest"></a>使用 dotnet test 與 MSTest 為 .NET Core 中的 F# 程式庫進行單元測試

本教學課程會引導您逐步進行建置範例方案的互動式體驗，以了解單元測試概念。 如果您想要使用預先建置的方案進行教學課程，請在開始之前[檢視或下載範例程式碼](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-with-fsharp-mstest/)。 如需下載指示，請參閱[範例和教學課程](../../samples-and-tutorials/index.md#view-and-download-samples)。

[!INCLUDE [testing an ASP.NET Core project from .NET Core](../../../includes/core-testing-note-aspnet.md)]

## <a name="creating-the-source-project"></a>建立來源專案

開啟 Shell 視窗。 建立名為 *unit-testing-with-fsharp* 的目錄來放置方案。
在這個新目錄中，執行 `dotnet new sln` 以建立新方案。 這樣可讓您更輕鬆地管理類別庫與單元測試專案。
在方案目錄中，建立 *MathService* 目錄。 到目前為止，目錄與檔案結構如下所示：

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
```

將 *MathService* 設定為目前的目錄，然後執行 `dotnet new classlib -lang "F#"` 以建立來源專案。  您建立會失敗的數學服務實作：

```fsharp
module MyMath =
    let squaresOfOdds xs = raise (System.NotImplementedException("You haven't written a test yet!"))
```

將目錄變更回 *unit-testing-with-fsharp* 目錄。 執行 `dotnet sln add .\MathService\MathService.fsproj` 以將類別庫專案加入方案中。

## <a name="creating-the-test-project"></a>建立測試專案

接著，建立 *MathService.Tests* 目錄。 下列大綱顯示目錄結構：

```console
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
```

將 *MathService.Tests* 目錄設定為目前的目錄，然後使用 `dotnet new mstest -lang "F#"` 建立新專案。 這會建立將 MStest 作為測試架構使用的測試專案。 產生的範本會在 *MathServiceTests.fsproj* 中設定測試執行器：

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0-preview-20170628-02" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.18" />
  <PackageReference Include="MSTest.TestFramework" Version="1.1.18" />
</ItemGroup>
```

測試專案需要其他套件來建立和執行單元測試。 上一個步驟中的 `dotnet new` 已新增 MSTest 和 MSTest 執行器。 現在，將 `MathService` 類別庫新增為專案的另一個相依性。 使用 `dotnet add reference` 命令：

```dotnetcli
dotnet add reference ../MathService/MathService.fsproj
```

您可以在 GitHub 的[範例存放庫](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-with-fsharp/MathService.Tests/MathService.Tests.fsproj)中看到完整檔案。

您有下列最終方案配置：

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

執行 *unit-testing-with-fsharp* 目錄中的 `dotnet sln add .\MathService.Tests\MathService.Tests.fsproj`。

## <a name="creating-the-first-test"></a>建立第一個測試

撰寫一個會失敗的測試，再使其通過，然後重複這個過程。 開啟 *Tests.fs* 並加入下列程式碼：

```fsharp
namespace MathService.Tests

open System
open Microsoft.VisualStudio.TestTools.UnitTesting
open MathService

[<TestClass>]
type TestClass () =

    [<TestMethod>]
    member this.TestMethodPassing() =
        Assert.IsTrue(true)

    [<TestMethod>]
     member this.FailEveryTime() = Assert.IsTrue(false)
```

`[<TestClass>]` 屬性表示包含測試的類別。 `[<TestMethod>]` 屬性表示由測試執行器執行的測試方法。 從 *unit-testing-with-fsharp* 目錄，執行 `dotnet test` 來建置測試和類別庫，然後執行測試。 MSTest 測試執行器包含執行測試的程式進入點。 `dotnet test` 會使用您建立的單元測試專案來開始測試執行器。

這兩個測試會顯示最基本的成功和失敗測試。 `My test` 成功，而 `Fail every time` 失敗。 現在，針對 `squaresOfOdds` 方法建立測試。 `squaresOfOdds` 方法會傳回屬於輸入序列一部分的所有奇數整數值平方清單。 您能以反覆方式建立會驗證功能的測試，而不需要嘗試一次撰寫所有那些函式。 將每個測試設定為通過表示為方法建立必要功能。

我們所能撰寫的最簡單測試是呼叫 `squaresOfOdds` 並傳遞所有偶數，其中結果應該是空整數序列。  該測試如下：

```fsharp
[<TestMethod>]
member this.TestEvenSequence() =
    let expected = Seq.empty<int> |> Seq.toList
    let actual = MyMath.squaresOfOdds [2; 4; 6; 8; 10]
    Assert.AreEqual(expected, actual)
```

請注意，`expected` 序列已被轉換為清單。 MSTest 程式庫仰賴許多標準 .NET 型別。 該相依性表示您的公用介面與預期結果支援 <xref:System.Collections.ICollection>，而非 <xref:System.Collections.IEnumerable>。

當您執行該測試時，您會看到您的測試失敗。 您尚未建立實作。 在可運作的 `Mathservice` 類別中撰寫最簡單的程式碼以讓此測試成功：

```fsharp
let squaresOfOdds xs =
    Seq.empty<int> |> Seq.toList
```

在 *unit-testing-with-fsharp* 目錄中，重新執行 `dotnet test`。 `dotnet test` 命令會依序執行 `MathService` 專案和 `MathService.Tests` 專案的建置。 建置這兩個專案之後，它將會執行此單一測試。 測試通過。

## <a name="completing-the-requirements"></a>完成需求

現在，您已經讓一個測試順利通過，您可以撰寫更多測試。 下一個簡單案例可搭配所具有的唯一奇數是 `1` 的序列運作。 數字 1 比較簡單，因為 1 的平方是 1。 該下一個測試如下：

```fsharp
[<TestMethod>]
member public this.TestOnesAndEvens() =
    let expected = [1; 1; 1; 1]
    let actual = MyMath.squaresOfOdds [2; 1; 4; 1; 6; 1; 8; 1; 10]
    Assert.AreEqual(expected, actual)
```

執行 `dotnet test` 會使得新測試失敗。 您必須更新 `squaresOfOdds` 方法以處理此新測試。 您必須將所有偶數從序列中篩選出來，以使此測試通過。 您可以透過撰寫小型篩選函式並使用 `Seq.filter` 來完成此動作：

```fsharp
let private isOdd x = x % 2 <> 0

let squaresOfOdds xs =
    xs
    |> Seq.filter isOdd |> Seq.toList
```

請注意對 `Seq.toList` 的呼叫。 那會建立清單，該清單會實作 <xref:System.Collections.ICollection> 介面。

還有一個步驟必須執行：計算每個奇數的平方。 透過撰寫新測試以開始：

```fsharp
[<TestMethod>]
member public this.TestSquaresOfOdds() =
    let expected = [1; 9; 25; 49; 81]
    let actual = MyMath.squaresOfOdds [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
    Assert.AreEqual(expected, actual)
```

您可以透過將已篩選的序列以管線方式傳遞到對應作業，以計算每個奇數的平方，來修正測試：

```fsharp
let private square x = x * x
let private isOdd x = x % 2 <> 0

let squaresOfOdds xs =
    xs
    |> Seq.filter isOdd
    |> Seq.map square
    |> Seq.toList
```

您已建置好小型的程式庫和該程式庫的一組單元測試， 您已建立方案結構，因此加入新套件與測試是一般工作流程的一部分。 您已集中大部分的時間與精力以解決應用程式目標。

## <a name="see-also"></a>請參閱

- [dotnet new](../tools/dotnet-new.md)
- [dotnet sln](../tools/dotnet-sln.md)
- [dotnet add reference](../tools/dotnet-add-reference.md)
- [dotnet test](../tools/dotnet-test.md)
