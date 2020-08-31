---
description: async - C# 參考
title: async - C# 參考
ms.date: 05/22/2017
f1_keywords:
- async_CSharpKeyword
helpviewer_keywords:
- async keyword [C#]
- async method [C#]
- async [C#]
ms.assetid: 16f14f09-b2ce-42c7-a875-e4eca5d50674
ms.openlocfilehash: 5a70389c9c423300fad03123cfc4738dfe10e481
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89118516"
---
# <a name="async-c-reference"></a>async (C# 參考)

使用 `async` 修飾詞可將方法、[Lambda 運算式](../operators/lambda-expressions.md)或[匿名方法](../operators/delegate-operator.md)指定為非同步。 如果您在方法或運算式上使用這個修飾詞，則它是指「非同步方法」**。 下例定義名為 `ExampleMethodAsync` 的非同步方法：

```csharp
public async Task<int> ExampleMethodAsync()
{
    //...
}
```

如果您不熟悉非同步程式設計或不了解非同步方法如何使用[ `await` 運算子](../operators/await.md)來執行可能長時間執行的工作，而不封鎖呼叫端的執行緒，請閱讀[使用 Async 和 await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)的簡介。 下列程式碼位於非同步方法中，會呼叫 <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=nameWithType> 方法：

```csharp
string contents = await httpClient.GetStringAsync(requestUrl);
```

非同步方法會以同步方式執行，直到抵達第一個 `await` 運算式，此時方法會暫停，直到等候的工作完成。 同時，控制項會返回方法的呼叫端，如下一節中的範例所示。

如果 `async` 關鍵字修改的方法不包含 `await` 運算式或陳述式，則方法會以同步方式執行。 如果有任何非同步方法未包含 `await` 陳述式，編譯器警告就會發出警示，因為這種情況可能表示發生錯誤。 請參閱[編譯器警告 (層級 1) CS4014](../compiler-messages/cs4014.md)。

 `async` 關鍵字與內容相關，它只有在修改方法、Lambda 運算式或匿名方法時，才是關鍵字。 在所有其他內容中，它會解譯為識別項。

## <a name="example"></a>範例
下列範例將示範非同步事件處理常式 `StartButton_Click` 與非同步方法 `ExampleMethodAsync` 之間的控制結構與流程。 非同步方法的結果是網頁的字元數。 此程式碼適用於您在 Visual Studio 中建立的 Windows Presentation Foundation (WPF) 應用程式或 Windows 市集應用程式。請參閱有關設定應用程式的程式碼註解。

您可以在 Visual Studio 中將此程式碼執行為 Windows Presentation Foundation (WPF) 應用程式或 Windows 市集應用程式。 您需要名為 `StartButton` 的按鈕控制項和名為 `ResultsTextBox` 的文字方塊控制項。 請記住要設定名稱和處理常式，如此才會有像下面這樣的內容：

```xaml
<Button Content="Button" HorizontalAlignment="Left" Margin="88,77,0,0" VerticalAlignment="Top" Width="75"
        Click="StartButton_Click" Name="StartButton"/>
<TextBox HorizontalAlignment="Left" Height="137" Margin="88,140,0,0" TextWrapping="Wrap"
         Text="&lt;Enter a URL&gt;" VerticalAlignment="Top" Width="310" Name="ResultsTextBox"/>
```

將程式碼執行為 WPF 應用程式：

- 將此程式碼貼入 MainWindow.xaml.cs 的 `MainWindow` 類別。
- 將參考新增至 System.Net.Http。
- 為 System.Net.Http 新增 `using` 指示詞。

將程式碼執行為 Windows 市集應用程式：

- 將此程式碼貼入 MainPage.xaml.cs 的 `MainPage` 類別。
- 為 System.Net.Http 和 System.Threading.Tasks 新增 using 指示詞。

[!code-csharp[wpf-async](../../../../samples/snippets/csharp/language-reference/keywords/async/wpf/mainwindow.xaml.cs#1)]

> [!IMPORTANT]
> 如需有關在等候工作時執行之工作和程式碼的詳細資訊，請參閱 [使用 async 和 await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)。 如需使用類似專案的完整主控台範例，請參閱 [在完成時處理非同步工作 (c # ) ](../../programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md)。

## <a name="return-types"></a>傳回型別
非同步方法可有下列傳回型別：

- <xref:System.Threading.Tasks.Task>
- <xref:System.Threading.Tasks.Task%601>
- [void](../builtin-types/void.md)。 除了用於事件處理常式以外的程式碼，通常不鼓勵使用 `async void` 方法，因為呼叫者無法 `await` 這些方法，且必須實作不同的機制來報告成功完成或錯誤狀況。
- 自 C# 7.0 開始，任何具有可存取 `GetAwaiter` 方法的型別。 `System.Threading.Tasks.ValueTask<TResult>` 類型就是一個這種實作。 新增 NuGet 套件 `System.Threading.Tasks.Extensions` 即可使用。

非同步方法不可宣告任何 [in](./in-parameter-modifier.md)、[ref](./ref.md) 或 [out](./out-parameter-modifier.md) 參數，也不可以有 [參考傳回值](../../programming-guide/classes-and-structs/ref-returns.md)，但可以呼叫有這類參數的方法。

如果方法的 [return](./return.md) 陳述式指定 `TResult` 類型的運算元，請指定 `Task<TResult>` 作為非同步方法的傳回型別。 如果方法完成時未傳回任何有意義的值，則使用 `Task`。 也就是說，呼叫方法會傳回 `Task`，但是當 `Task` 完成時，等候 `await` 的任何 `Task` 運算式都會判斷值為 `void`。

您主要是使用 `void` 傳回類型定義需要該傳回類型的事件處理常式。 傳回 `void` 之非同步方法的呼叫端無法等候它，而且無法攔截方法擲回的例外狀況。

自 C# 7.0 開始，您會傳回另一個型別，通常是實值型別，具有 `GetAwaiter` 方法可將程式碼效能關鍵區段中的記憶體配置降至最低。

如需詳細資訊和範例，請參閱[非同步方法的傳回型別](../../programming-guide/concepts/async/async-return-types.md)。

## <a name="see-also"></a>另請參閱

- <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>
- [await](../operators/await.md)
- [使用 async 和 await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)
- [在非同步工作完成時進行處理](../../programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md)
