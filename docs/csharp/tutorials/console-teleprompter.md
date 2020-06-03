---
title: 主控台應用程式
description: 本教學課程會教導您一些 .NET Core 和 C# 語言中的功能。
ms.date: 03/06/2017
ms.technology: csharp-fundamentals
ms.assetid: 883cd93d-50ce-4144-b7c9-2df28d9c11a0
ms.openlocfilehash: 06affa01b67edeea09088834cf131adb55650bbb
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82794659"
---
# <a name="console-app"></a>主控台應用程式

本教學課程會教導您一些 .NET Core 和 C# 語言中的功能。 您將了解：

- .NET Core CLI 的基本概念
- 「C# 主控台應用程式」的結構
- 主控台 I/O
- .NET 中檔案 I/O API 的基本概念
- .NET 中以工作為基礎的非同步程式設計的基本概念

您將建立一個可讀取文字檔的應用程式，並將該文字檔的內容回應至主控台。 對主控台之輸出的步調會符合可大聲朗讀它的步調。 您可以按 ' < ' （小於）或 ' > ' （大於）鍵，加速或減緩步調。

本教學課程中有許多功能。 讓我們逐一建立它們。

## <a name="prerequisites"></a>必要條件

- 設定您的電腦以執行 .NET Core。 您可以在[.Net Core 下載](https://dotnet.microsoft.com/download)頁面上找到安裝指示。 您可以在 Windows、Linux、macOS 或 Docker 容器中執行此應用程式。

- 安裝您慣用的程式碼編輯器。

## <a name="create-the-app"></a>建立應用程式

第一個步驟是建立新的應用程式。 請開啟命令提示字元，然後為您的應用程式建立新目錄。 使該目錄成為目前的目錄。 在命令提示字元處輸入命令 `dotnet new console`。 這會建立基本 "Hello World" 應用程式的起始檔案。

在您開始進行修改之前，讓我們先完成執行簡單 Hello World 應用程式的步驟。 在建立應用程式之後，請在命令提示字元處輸入 `dotnet restore`。 此命令會執行 NuGet 套件還原程序。 NuGet 是一個 .NET 套件管理員。 此命令會為您的專案下載任何遺漏的相依性。 由於這是一個新專案，因此沒有任何現有的相依性，所以第一次執行時將會下載 .NET Core 架構。 在這個初始步驟之後，當您新增新的相依套件或更新任何相依性的版本時，將只需要執行 `dotnet restore`。

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

還原套件之後，您需執行 `dotnet build`。 這會執行建置引擎並建立您的應用程式可執行檔。 最後，您需執行 `dotnet run` 來執行您的應用程式。

簡單的 Hello World 應用程式程式碼全部都在 Program.cs 中。 請使用您慣用的文字編輯器來開啟該檔案。 我們即將進行第一次變更。 在該檔案的開頭，您會看到 using 陳述式：

```csharp
using System;
```

此陳述式會告訴編譯器任何來自 `System` 命名空間的型別都在範圍內。 與您可能已使用的其他「物件導向」語言相同，C# 也使用命名空間來組織型別。 這個 Hello World 程式並無不同。 您可以看到命名空間中所包含的程式，而命名空間的名稱是根據目前目錄的名稱。 在本教學課程中，將命名空間的名稱變更為 `TeleprompterConsole`：

```csharp
namespace TeleprompterConsole
```

## <a name="reading-and-echoing-the-file"></a>讀取及回應檔案

要新增的第一個功能是能夠讀取文字檔，並對主控台顯示該全部文字。 首先，讓我們新增一個文字檔。 請從 GitHub 儲存機制將此[範例](https://github.com/dotnet/samples/tree/master/csharp/getting-started/console-teleprompter)的 [sampleQuotes.txt](https://github.com/dotnet/samples/raw/master/csharp/getting-started/console-teleprompter/sampleQuotes.txt) 檔案複製到您的專案目錄中。 這將作為您應用程式的指令碼。 如果您想要如何下載本主題之範例應用程式的資訊，請參閱[範例和教學課程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)主題中的指示。

接著，在您的 `Program` 類別 (就在 `Main` 方法下方) 中新增下列方法：

```csharp
static IEnumerable<string> ReadFrom(string file)
{
    string line;
    using (var reader = File.OpenText(file))
    {
        while ((line = reader.ReadLine()) != null)
        {
            yield return line;
        }
    }
}
```

此方法會使用來自兩個新命名空間的型別。 若要進行編譯，您必須將下列兩行新增至檔案頂端：

```csharp
using System.Collections.Generic;
using System.IO;
```

<xref:System.Collections.Generic.IEnumerable%601> 介面是在 <xref:System.Collections.Generic> 命名空間中定義。 <xref:System.IO.File> 類別是在 <xref:System.IO> 命名空間中定義。

此方法是 C# 方法的特殊型別，稱為「Iterator 方法」**。 列舉程式方法會傳回延遲評估的序列。 這意謂著序列中的每個項目會在取用序列的程式碼要求該項目時產生。 枚舉器方法是包含一或多個 [`yield return`](../language-reference/keywords/yield.md) 語句的方法。 `ReadFrom` 方法所傳回的物件包含用來產生序列中每個項目的程式碼。 在此範例中，這牽涉到從原始程式檔讀取下一行文字，並傳回該字串。 每次呼叫程式碼要求序列中的下一個項目時，程式碼都會從檔案讀取下一行文字，並傳回該文字。 完全讀取檔案後，序列會指出已沒有任何其他項目。

有兩個其他 C# 語法元素可能是您不熟悉的。 [`using`](../language-reference/keywords/using-statement.md)這個方法中的語句會管理資源清除。 在 `using` 陳述式中初始化的變數 (在此範例中為 `reader`) 必須實作 <xref:System.IDisposable> 介面。 該介面會定義單一方法 `Dispose`，而在應該釋出資源時應該呼叫此方法。 編譯器會在執行到達 `using` 陳述式的結尾大括號時產生該呼叫。 編譯器產生的程式碼會確保即使 using 陳述式所定義區塊中的程式碼擲回例外狀況，也會釋出資源。

定義 `reader` 變數時，是使用 `var` 關鍵字來定義。 [`var`](../language-reference/keywords/var.md)定義*隱含類型區域變數*。 這意謂著變數的型別取決於指派給該變數之物件的編譯階段型別。 在這裡，這是來自 <xref:System.IO.File.OpenText(System.String)> 方法的傳回值，是一個 <xref:System.IO.StreamReader> 物件。

現在，讓我們填入程式碼，以讀取方法中的檔案 `Main` ：

```csharp
var lines = ReadFrom("sampleQuotes.txt");
foreach (var line in lines)
{
    Console.WriteLine(line);
}
```

請執行程式 (使用 `dotnet run`)，然後您便可以看到每一行顯示在主控台中。

## <a name="adding-delays-and-formatting-output"></a>新增延遲及設定輸出格式

您的內容顯示速度太快，無法大聲朗讀。 現在您必須在輸出中新增延遲。 當您開始時，您將會建立一些可進行非同步處理的核心程式代碼。 不過，這些開頭的步驟會依循一些反模式。 在您新增程式碼時，註解中會指出這些反模式，然後在稍後的步驟中將會更新此程式碼。

這個部分有兩個步驟。 首先，您將更新 iterator 方法，以傳回單一單字，而不是整行。 這是透過這些修改來完成的。 請以下列程式碼取代 `yield return line;` 陳述式：

```csharp
var words = line.Split(' ');
foreach (var word in words)
{
    yield return word + " ";
}
yield return Environment.NewLine;
```

接著，您必須修改取用檔案行的方式，然後在寫入每個字之後新增延遲。 請以下列區塊取代 `Main` 方法中的 `Console.WriteLine(line)` 陳述式：

```csharp
Console.Write(line);
if (!string.IsNullOrWhiteSpace(line))
{
    var pause = Task.Delay(200);
    // Synchronously waiting on a task is an
    // anti-pattern. This will get fixed in later
    // steps.
    pause.Wait();
}
```

<xref:System.Threading.Tasks.Task> 類別是在 <xref:System.Threading.Tasks> 命名空間中，因此您必須在檔案開頭新增該 `using` 陳述式：

```csharp
using System.Threading.Tasks;
```

請執行範例並檢查輸出。 現在會顯示每個單字，後面接著 200 毫秒的延遲。 不過，顯示的輸出出現一些問題，因為來源文字檔有數行超過 80 個字元且沒有分行符號。 這在捲動時會相當難以閱讀。 這很容易修正。 您只需追蹤每一行的長度，並在行長度達到特定臨界值時產生新的一行。 請在保存行長度的 `ReadFrom` 方法中 `words` 的宣告之後宣告區域變數：

```csharp
var lineLength = 0;
```

接著，在 `yield return word + " ";` 陳述式之後 (在結尾大括號之前) 新增下列程式碼：

```csharp
lineLength += word.Length + 1;
if (lineLength > 70)
{
    yield return Environment.NewLine;
    lineLength = 0;
}
```

執行範例，您就能夠以預先設定的步調大聲讀出。

## <a name="async-tasks"></a>非同步工作

在最後一個步驟中，您將新增程式碼，以便在一個工作中以非同步方式寫入輸出，同時也執行另一個工作以讀取使用者的輸入（如果他們想要加速或減緩文字顯示），或完全停止文字顯示。 這有幾個步驟，而最後，您將會擁有所需的所有更新。 第一個步驟是建立非同步傳回 <xref:System.Threading.Tasks.Task> 方法，代表您到目前為止所建立的程式碼，以讀取和顯示該檔案。

將此方法新增至您的 `Program` 類別（它是從方法的主體取得 `Main` ）：

```csharp
private static async Task ShowTeleprompter()
{
    var words = ReadFrom("sampleQuotes.txt");
    foreach (var word in words)
    {
        Console.Write(word);
        if (!string.IsNullOrWhiteSpace(word))
        {
            await Task.Delay(200);
        }
    }
}
```

您會注意到兩個變更。 首先，在方法的主體中，此版本使用 `await` 關鍵字，而不是呼叫 <xref:System.Threading.Tasks.Task.Wait> 來同步等候工作完成。 為了這麼做，您必須將 `async` 修飾詞新增到方法簽章。 此方法會傳回 `Task`。 請注意，並沒有會傳回 `Task` 物件的傳回陳述式。 取而代之的是，會由編譯器在您使用 `await` 運算子時產生的程式碼建立 `Task` 物件。 您可以想像這個方法會在到達 `await` 時返回。 傳回的 `Task` 指出工作尚未完成。 方法會在所等候的工作完成時繼續執行。 當它執行到完成時，傳回的 `Task` 會指出它已完成。
呼叫程式碼可以監視傳回的 `Task` 以判斷它何時完成。

您可以在 `Main` 方法中呼叫這個新方法：

```csharp
ShowTeleprompter().Wait();
```

在這裡，`Main` 中的程式碼會執行同步等候。 您應該儘可能使用 `await` 運算子而不是同步等候。 但是，在主控台應用程式的 `Main` 方法中，您無法使用 `await` 運算子。 那會導致應用程式在所有工作完成之前即結束。

> [!NOTE]
> 如果您使用 C# 7.1 或更新版本，則可以使用 [`async` `Main` 方法](../whats-new/csharp-7-1.md#async-main)建立主控台應用程式。

接下來，您必須撰寫第二個非同步方法，以從主控台讀取並監看「<」（小於）、「>」（大於）和 ' X ' 或 ' x ' 索引鍵。 以下是您為該工作新增的方法：

```csharp
private static async Task GetInput()
{
    var delay = 200;
    Action work = () =>
    {
        do {
            var key = Console.ReadKey(true);
            if (key.KeyChar == '>')
            {
                delay -= 10;
            }
            else if (key.KeyChar == '<')
            {
                delay += 10;
            }
            else if (key.KeyChar == 'X' || key.KeyChar == 'x')
            {
                break;
            }
        } while (true);
    };
    await Task.Run(work);
}
```

這會建立 lambda 運算式來代表 <xref:System.Action> 從主控台讀取索引鍵的委派，並修改代表使用者按下 ' < ' （小於）或 ' > ' （大於）鍵時的延遲的本機變數。 委派方法會在使用者按下 ' X ' 或 ' x ' 鍵時完成，讓使用者可以隨時停止文字顯示。 此方法會使用 <xref:System.Console.ReadKey> 來封鎖並等候使用者按下按鍵。

若要完成此功能，您必須建立一個會傳回方法的新 `async Task`，該方法既會啟動這兩項工作 (`GetInput` 和 `ShowTeleprompter`)，也會管理這兩項工作之間的共用資料。

現在可以建立可處理這兩個工作之間共用資料的類別。 此類別包含兩個公用屬性：延遲和一個指出已完全讀取檔案的 `Done` 旗標：

```csharp
namespace TeleprompterConsole
{
    internal class TelePrompterConfig
    {
        public int DelayInMilliseconds { get; private set; } = 200;

        public void UpdateDelay(int increment) // negative to speed up
        {
            var newDelay = Min(DelayInMilliseconds + increment, 1000);
            newDelay = Max(newDelay, 20);
            DelayInMilliseconds = newDelay;
        }

        public bool Done { get; private set; }

        public void SetDone()
        {
            Done = true;
        }
    }
}
```

請將該類別放在新檔案中，然後如以上所示，將該類別包含在 `TeleprompterConsole` 命名空間中。 您也需要加入 `using static` 語句，以便在沒有封入 `Min` `Max` 類別或命名空間名稱的情況下，可以參考和方法。 [`using static`](../language-reference/keywords/using-static.md)語句會從一個類別匯入方法。 這與到目前為止所使用的 `using` 陳述式形成對比，該陳述式會從命名空間匯入所有類別。

```csharp
using static System.Math;
```

接著，您必須更新 `ShowTeleprompter` 和 `GetInput` 方法以使用新的 `config` 物件。 請撰寫一個最後的 `Task` 來傳回 `async` 方法，以啟動兩項工作並在第一個工作完成時結束：

```csharp
private static async Task RunTeleprompter()
{
    var config = new TelePrompterConfig();
    var displayTask = ShowTeleprompter(config);

    var speedTask = GetInput(config);
    await Task.WhenAny(displayTask, speedTask);
}
```

這裡的新方法是 <xref:System.Threading.Tasks.Task.WhenAny(System.Threading.Tasks.Task[])> 呼叫。 此方法會建立一個 `Task`，它會在其引數清單中的任何工作完成時便結束。

接著，您必須更新 `ShowTeleprompter` 和 `GetInput` 方法以使用 `config` 物件來設定延遲：

```csharp
private static async Task ShowTeleprompter(TelePrompterConfig config)
{
    var words = ReadFrom("sampleQuotes.txt");
    foreach (var word in words)
    {
        Console.Write(word);
        if (!string.IsNullOrWhiteSpace(word))
        {
            await Task.Delay(config.DelayInMilliseconds);
        }
    }
    config.SetDone();
}

private static async Task GetInput(TelePrompterConfig config)
{
    Action work = () =>
    {
        do {
            var key = Console.ReadKey(true);
            if (key.KeyChar == '>')
                config.UpdateDelay(-10);
            else if (key.KeyChar == '<')
                config.UpdateDelay(10);
            else if (key.KeyChar == 'X' || key.KeyChar == 'x')
                config.SetDone();
        } while (!config.Done);
    };
    await Task.Run(work);
}
```

這個新版本的 `ShowTeleprompter` 會呼叫 `TeleprompterConfig` 類別中的新方法。 現在，您必須更新 `Main` 以呼叫 `RunTeleprompter` 而不是 `ShowTeleprompter`：

```csharp
RunTeleprompter().Wait();
```

## <a name="conclusion"></a>結論

本教學課程示範一些與在主控台應用程式中工作有關的 C# 語言和 .NET Core 程式庫相關功能。 您可以利用這項知識作為基礎，進一步探索這裡介紹的語言和類別。 您已經瞭解檔案和主控台 i/o 的基本概念、封鎖和非封鎖使用以工作為基礎的非同步程式設計、c # 語言導覽，以及 c # 程式的組織方式，以及 .NET Core CLI。

如需檔案 I/O 的詳細資訊，請參閱[檔案和資料流 I/O](../../standard/io/index.md) 主題。 如需本教學課程中所使用非同步程式設計模型的詳細資訊，請參閱[以工作為基礎的非同步程式設計](../../standard/parallel-programming/task-based-asynchronous-programming.md)主題和[非同步程式設計](../async.md)主題。
