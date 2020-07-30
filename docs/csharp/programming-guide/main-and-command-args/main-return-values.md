---
title: Main() 傳回值 - C# 程式設計指南
description: 瞭解 Main （）傳回值。 請參閱程式碼範例、編譯器產生的程式碼，以及查看其他可用的資源。
ms.date: 08/02/2017
helpviewer_keywords:
- Main method [C#], return values
ms.assetid: c2f5a1d8-1676-4bea-bc7e-44a97e72d5bc
ms.openlocfilehash: 4458f3cd7c8259c5725cfe5e853f826fe2ef61cc
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87382057"
---
# <a name="main-return-values-c-programming-guide"></a>Main() 傳回值 (C# 程式設計手冊)

`Main` 方法可以傳回 `void`：

 [!code-csharp[csProgGuideMain#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#12)]

它也可以傳回 `int`：

 [!code-csharp[csProgGuideMain#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#13)]

如果未使用來自 `Main` 的傳回值，則傳回 `void` 可允許使用比較簡單的程式碼。 不過，若是傳回一個整數，可讓程式將狀態資訊傳達給其他會叫用可執行檔的程式或指令碼。 從 `Main` 傳回的值會視為處理序的結束代碼。 如果 `void` 從傳回 `Main` ，結束代碼將會隱含地結束 `0` 。 下列範例示範如何存取來自 `Main` 的傳回值。

## <a name="example"></a>範例

此範例使用[.Net Core](../../../core/index.yml)命令列工具。 如果您不熟悉 .NET Core 命令列工具，您可以在這[篇入門文章](../../../core/tutorials/with-visual-studio-code.md)中瞭解它們。

修改 *program.cs* 中的 `Main` 方法，如下所示：

 [!code-csharp[csProgGuideMain#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#14)]

在 Windows 中執行程式時，任何從 `Main` 函式傳回的值，皆會儲存在環境變數中。 您可以從批次檔使用 `ERRORLEVEL` 或從 PowerShell 使用 `$LastExitCode` 來擷取此環境變數。

您可以使用 [dotnet CLI](../../../core/tools/dotnet.md) `dotnet build` 命令來建置應用程式。

接下來，建立 PowerShell 指令碼以執行此應用程式，並顯示結果。 將下列程式碼貼入文字檔，將它儲存為 `test.ps1`，並放到包含專案的資料夾中。 在 PowerShell 命令提示字元中鍵入 `test.ps1`，以執行 PowerShell 指令碼。

由於程式碼會傳回零，因為批次檔會報告成功。 不過，如果您將 MainReturnValTest.cs 變更為傳回非零值，然後重新編譯程式，則後續執行 powershell 腳本將會報告失敗。

```dotnetcli
dotnet run
```

```powershell
if ($LastExitCode -eq 0) {
    Write-Host "Execution succeeded"
} else
{
    Write-Host "Execution Failed"
}
Write-Host "Return value = " $LastExitCode
```

## <a name="sample-output"></a>範例輸出

```txt
Execution succeeded
Return value = 0
```

## <a name="async-main-return-values"></a>Async Main 傳回值

Async Main 傳回值會將呼叫 `Main` 中非同步方法所需的未定案程式碼，移至編譯器所產生的程式碼。 之前，您需要撰寫此建構以呼叫非同步程式碼，並確保您的程式會執行到非同步作業完成為止：

```csharp
public static void Main()
{
    AsyncConsoleWork().GetAwaiter().GetResult();
}

private static async Task<int> AsyncConsoleWork()
{
    // Main body here
    return 0;
}
```

現在，這會取代為：

[!code-csharp[AsyncMain](../../../../samples/snippets/csharp/main-arguments/program.cs#AsyncMain)]

新語法的優點是編譯器一律會產生正確的程式碼。

## <a name="compiler-generated-code"></a>編譯器產生的程式碼

當應用程式進入點傳回 `Task` 或 `Task<int>` 時，編譯器會產生新的進入點，以呼叫應用程式程式碼中宣告的進入點方法。 假設此進入點稱為 `$GeneratedMain`，編譯器會為這些進入點產生下列程式碼：

- `static Task Main()` 會導致編譯器發出 `private static void $GeneratedMain() => Main().GetAwaiter().GetResult();` 的對等項目
- `static Task Main(string[])` 會導致編譯器發出 `private static void $GeneratedMain(string[] args) => Main(args).GetAwaiter().GetResult();` 的對等項目
- `static Task<int> Main()` 會導致編譯器發出 `private static int $GeneratedMain() => Main().GetAwaiter().GetResult();` 的對等項目
- `static Task<int> Main(string[])` 會導致編譯器發出 `private static int $GeneratedMain(string[] args) => Main(args).GetAwaiter().GetResult();` 的對等項目

> [!NOTE]
>如果這些範例在 `Main` 方法上使用 `async` 修飾詞，編譯器會產生相同的程式碼。

## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [C # 參考](../index.md)
- [Main （）和命令列引數](index.md)
- [如何顯示命令列引數](./how-to-display-command-line-arguments.md)
