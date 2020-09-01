---
description: await 運算子 - C# 參考
title: await 運算子 - C# 參考
ms.date: 07/13/2020
f1_keywords:
- await_CSharpKeyword
helpviewer_keywords:
- await keyword [C#]
- await [C#]
ms.assetid: 50725c24-ac76-4ca7-bca1-dd57642ffedb
ms.openlocfilehash: 6531e696a6193bf1b1909c9f1be3f5beb4d7dd69
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89134363"
---
# <a name="await-operator-c-reference"></a>await 運算子 (C# 參考)

`await` 運算子會暫停封入[非同步](../keywords/async.md)方法的評估，直到其運算元所代表的非同步作業完成為止。 當非同步作業完成時，`await` 運算子會傳回作業的結果 (如果有的話)。 當 `await` 運算子套用至代表已完成之作業的運算元時，它會立即傳回作業的結果，而不會暫停封入方法。 `await` 運算子不會封鎖評估非同步方法的執行緒。 當運算子暫止 `await` 封閉式 async 方法時，控制項會返回方法的呼叫端。

在下列範例中，<xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A?displayProperty=nameWithType> 方法會傳回 `Task<byte[]>` 執行個體，代表在完成時產生位元組陣列的非同步作業。 `await` 運算子會暫停 `DownloadDocsMainPageAsync` 方法，直到作業完成為止。 當 `DownloadDocsMainPageAsync` 暫停時，控制權會返回 `Main` 方法，也就是 `DownloadDocsMainPageAsync` 的呼叫端。 `Main` 方法會執行直到需要 `DownloadDocsMainPageAsync` 方法所執行的非同步作業結果為止。 當 <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> 取得所有位元組時，會評估 `DownloadDocsMainPageAsync` 方法的其餘部分。 之後，會評估 `Main` 方法的其餘部分。

[!code-csharp[await example](snippets/shared/AwaitOperator.cs)]

上述範例會使用 [非同步 `Main` 方法](../../programming-guide/main-and-command-args/index.md)，可能是從 c # 7.1 開始。 如需詳細資訊，請參閱 [Main 方法中的 await 運算子](#await-operator-in-the-main-method)一節。

> [!NOTE]
> 如需非同步程式設計的簡介，請參閱[使用 async 和 await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)。 使用 `async` 和 `await` 進行非同步程式設計時，會遵循[以工作為基礎的非同步模式](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)。

您只能在以 [async](../keywords/async.md) 關鍵字修改的方法、[Lambda 運算式](lambda-expressions.md)或[匿名方法](delegate-operator.md)中使用 `await` 運算子。 在非同步方法中，您無法 `await` 在同步函式的主體、 [lock 語句](../keywords/lock-statement.md)的區塊內，以及 [不安全](../keywords/unsafe.md) 的內容中使用運算子。

`await` 運算子的運算元通常是下列其中一個 .NET 類型：<xref:System.Threading.Tasks.Task>、<xref:System.Threading.Tasks.Task%601>、<xref:System.Threading.Tasks.ValueTask> 或 <xref:System.Threading.Tasks.ValueTask%601>。 不過，任何可等候運算式都可以是 `await` 運算子的運算元。 如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[可等候運算式](~/_csharplang/spec/expressions.md#awaitable-expressions)一節。

如果運算式 `t` 的類型為 <xref:System.Threading.Tasks.Task%601> 或 <xref:System.Threading.Tasks.ValueTask%601>，則運算式 `await t` 的類型為 `TResult`。 如果 `t` 的類型為 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.ValueTask>，則 `await t` 的類型為 `void`。 在這兩種情況下，如果 `t` 擲回例外狀況，`await t` 會重新擲回該例外狀況。 如需例外狀況處理的詳細資訊，請參閱 [try-catch 陳述式](../keywords/try-catch.md)一文的[非同步方法中的例外狀況](../keywords/try-catch.md#exceptions-in-async-methods)一節。

`async`和 `await` 關鍵字可在 c # 5 和更新版本中使用。

## <a name="asynchronous-streams-and-disposables"></a>非同步資料流程和可處置專案

從 c # 8.0 開始，您可以使用非同步資料流程和可處置專案。

您可以使用 `await foreach` 語句來使用非同步資料資料流程。 如需詳細資訊，請參閱[c # 8.0 的新功能文章中](../../whats-new/csharp-8.md)的[ `foreach` 語句](../keywords/foreach-in.md)文章和[非同步資料流程](../../whats-new/csharp-8.md#asynchronous-streams)一節。

您可以使用 `await using` 語句來處理非同步可處置的物件，也就是實作為介面型別的物件 <xref:System.IAsyncDisposable> 。 如需詳細資訊，請參閱「[執行 DisposeAsync 方法](../../../standard/garbage-collection/implementing-disposeasync.md)」一文中的「[使用非同步可處置](../../../standard/garbage-collection/implementing-disposeasync.md#using-async-disposable)」一節。

## <a name="await-operator-in-the-main-method"></a>Main 方法中的 await 運算子

從 c # 7.1 開始， [ `Main` 方法](../../programming-guide/main-and-command-args/index.md)（也就是應用程式進入點）可以傳回 `Task` 或 `Task<int>` ，讓它成為非同步，以便您可以 `await` 在其主體中使用運算子。 在舊版 C# 中，若要確保 `Main` 方法會等候非同步作業完成，您可以擷取對應非同步方法所傳回 <xref:System.Threading.Tasks.Task%601> 執行個體的 <xref:System.Threading.Tasks.Task%601.Result?displayProperty=nameWithType> 屬性值。 針對不會產生值的非同步作業，您可以呼叫 <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> 方法。 如需如何選取語言版本的詳細資訊，請參閱 [c # 語言](../configure-language-version.md)版本設定。

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的 [Await 運算式](~/_csharplang/spec/expressions.md#await-expressions)一節。

## <a name="see-also"></a>另請參閱

- [C# 參考資料](../index.md)
- [C# 運算子與運算式](index.md)
- [async](../keywords/async.md)
- [非同步工作程式設計模型](../../programming-guide/concepts/async/task-asynchronous-programming-model.md)
- [非同步程式設計](../../async.md)
- [深入了解非同步](../../../standard/async-in-depth.md)
- [逐步解說：使用 async 和 await 存取 Web](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [教學課程：使用 c # 8.0 和 .NET Core 3.0 產生及使用非同步資料流程](../../tutorials/generate-consume-asynchronous-stream.md)
