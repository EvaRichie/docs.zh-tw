---
title: 使用 MSTest 與 .NET Core 為 C# 進行單元測試
description: 透過逐步使用 dotnet test 和 MSTest 建置範例方案的互動式體驗，了解 C# 與 .NET Core 中的單元測試概念。
author: ncarandini
ms.author: wiwagn
ms.date: 10/21/2020
ms.openlocfilehash: c6132251ecc4f453189937f93cf8024dcb8b91f5
ms.sourcegitcommit: 870bc4b4087510f6fba3c7b1c0d391f02bcc1f3e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2020
ms.locfileid: "92471605"
---
# <a name="unit-testing-c-with-mstest-and-net-core"></a>使用 MSTest 與 .NET Core 為 C# 進行單元測試

本教學課程會引導您逐步進行建置範例方案的互動式體驗，以了解單元測試概念。 如果您想要使用預先建置的方案進行教學課程，請在開始之前[檢視或下載範例程式碼](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-mstest/)。 如需下載指示，請參閱[範例和教學課程](../../samples-and-tutorials/index.md#view-and-download-samples)。

[!INCLUDE [testing an ASP.NET Core project from .NET Core](../../../includes/core-testing-note-aspnet.md)]

## <a name="create-the-source-project"></a>建立來源專案

開啟 Shell 視窗。 建立名稱為 *unit-testing-using-mstest* 的目錄來放置解決方案。 在這個新目錄中，執行 [`dotnet new sln`](../tools/dotnet-new.md) 以建立類別庫和測試專案的新方案檔。 接著，建立 *PrimeService* 目錄。 下列大綱顯示到目前為止的目錄與檔案結構：

```console
/unit-testing-using-mstest
    unit-testing-using-mstest.sln
    /PrimeService
```

使 *>primeservice* 成為目前的目錄並執行， [`dotnet new classlib`](../tools/dotnet-new.md) 以建立來源專案。 將 *Class1.cs* 重新命名為 *PrimeService.cs*。 建立會失敗的 `PrimeService` 類別實作：

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

將目錄變更回 *unit-testing-using-mstest* 目錄。 執行 [`dotnet sln add PrimeService/PrimeService.csproj`](../tools/dotnet-sln.md) 以將類別庫專案加入至方案。

## <a name="create-the-test-project"></a>建立測試專案

接著，建立 *PrimeService.Tests* 目錄。 下列大綱顯示目錄結構：

```console
/unit-testing-using-mstest
    unit-testing-using-mstest.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
```

使 *>primeservice* 成為目前的目錄的目錄， [`dotnet new mstest`](../tools/dotnet-new.md) 並使用建立新專案。 dotnet new 命令會建立將 MSTest 作為測試程式庫使用的測試專案。 產生的範本會在 *>primeservicetests.csproj .csproj* 檔案中設定測試執行器：

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0" />
  <PackageReference Include="MSTest.TestAdapter" Version="1.1.18" />
  <PackageReference Include="MSTest.TestFramework" Version="1.1.18" />
</ItemGroup>
```

測試專案需要其他套件來建立和執行單元測試。 上一個步驟中的 `dotnet new` 已新增 MSTest SDK、MSTest 測試架構和 MSTest 執行器。 現在，將 `PrimeService` 類別庫新增為專案的另一個相依性。 使用 [`dotnet add reference`](../tools/dotnet-add-reference.md) 命令：

```dotnetcli
dotnet add reference ../PrimeService/PrimeService.csproj
```

您可以在 GitHub 的[範例存放庫](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService.Tests.csproj)中看到完整檔案。

下列大綱顯示最終方案配置：

```console
/unit-testing-using-mstest
    unit-testing-using-mstest.sln
    /PrimeService
        Source Files
        PrimeService.csproj
    /PrimeService.Tests
        Test Source Files
        PrimeServiceTests.csproj
```

[`dotnet sln add .\PrimeService.Tests\PrimeService.Tests.csproj`](../tools/dotnet-sln.md)在*單元測試-使用-mstest*目錄中執行。

## <a name="create-the-first-test"></a>建立第一個測試

撰寫一個會失敗的測試，再使其通過，然後重複這個過程。 從 *>primeservice*中移除*UnitTest1.cs* ，然後使用下列內容建立名為*PrimeService_IsPrimeShould*的新 c # 檔案：

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    [TestClass]
    public class PrimeService_IsPrimeShould
    {
        [TestMethod]
        public void IsPrime_InputIs1_ReturnFalse()
        {
            var primeService = new PrimeService();
            bool result = primeService.IsPrime(1);

            Assert.IsFalse(result, "1 should not be prime");
        }
    }
}
```

[TestClass 屬性](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute)代表包含單元測試的類別。 [TestMethod 屬性](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute)表示方法是測試方法。

儲存此檔案，然後執行 [`dotnet test`](../tools/dotnet-test.md) 以建立測試和類別庫，然後執行測試。 MSTest 測試執行器包含執行測試的程式進入點。 `dotnet test` 會使用您建立的單元測試專案來開始測試執行器。

您的測試失敗。 您尚未建立實作。 在可運作的 `PrimeService` 類別中撰寫最簡單的程式碼以讓此測試成功：

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

在 *unit-testing-using-mstest* 目錄中，重新執行 `dotnet test`。 `dotnet test` 命令會依序執行 `PrimeService` 專案和 `PrimeService.Tests` 專案的建置。 建置這兩個專案之後，它將會執行此單一測試。 測試通過。

## <a name="add-more-features"></a>新增更多功能

現在，您已經讓一個測試順利通過，您可以撰寫更多測試。 還有一些其他適用於質數 0、-1 的簡單案例。 您可以使用 [TestMethod 屬性](xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute)新增新的測試，但這段過程很快就會單調乏味。 因此，還有其他 MSTest 屬性，可讓您撰寫類似的測試套件。  [DataTestMethod 屬性](xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataTestMethodAttribute)代表一套測試，這套測試會執行相同的程式碼，但具有不同的輸入引數。 您可以使用 [DataRow 屬性](xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataRowAttribute)來指定這些輸入的值。

您不需要建立新測試，只要套用這兩個屬性以建立單一資料驅動測試即可。 資料驅動型測試是一種測試方法，其會測試數個低於二 (最小質數) 的值：

[!code-csharp[Sample_TestCode](../../../samples/snippets/core/testing/unit-testing-using-mstest/csharp/PrimeService.Tests/PrimeService_IsPrimeShould.cs?name=Sample_TestCode)]

執行 `dotnet test`，然後會有兩個測試失敗。 若要使所有測試通過，請變更方法開頭的 `if` 子句：

```csharp
if (candidate < 2)
```

繼續在主要程式庫中新增更多測試、更多理論和更多程式碼，以反覆執行。 您有[測試的完成版](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-mstest/PrimeService.Tests/PrimeService_IsPrimeShould.cs)和[程式庫的完整實作](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-using-mstest/PrimeService/PrimeService.cs)。

您已建置好小型的程式庫和該程式庫的一組單元測試， 您已建立方案結構，因此加入新套件與測試是一般工作流程的一部分。 您已集中大部分的時間與精力以解決應用程式目標。

## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting>
- [在單元測試中使用 MSTest 架構](/visualstudio/test/using-microsoft-visualstudio-testtools-unittesting-members-in-unit-tests)
- [MSTest V2 測試架構文件](https://github.com/Microsoft/testfx-docs)
