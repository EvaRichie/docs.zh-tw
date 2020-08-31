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
# <a name="async-c-reference"></a><span data-ttu-id="638ba-103">async (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="638ba-103">async (C# Reference)</span></span>

<span data-ttu-id="638ba-104">使用 `async` 修飾詞可將方法、[Lambda 運算式](../operators/lambda-expressions.md)或[匿名方法](../operators/delegate-operator.md)指定為非同步。</span><span class="sxs-lookup"><span data-stu-id="638ba-104">Use the `async` modifier to specify that a method, [lambda expression](../operators/lambda-expressions.md), or [anonymous method](../operators/delegate-operator.md) is asynchronous.</span></span> <span data-ttu-id="638ba-105">如果您在方法或運算式上使用這個修飾詞，則它是指「非同步方法」\*\*。</span><span class="sxs-lookup"><span data-stu-id="638ba-105">If you use this modifier on a method or expression, it's referred to as an *async method*.</span></span> <span data-ttu-id="638ba-106">下例定義名為 `ExampleMethodAsync` 的非同步方法：</span><span class="sxs-lookup"><span data-stu-id="638ba-106">The following example defines an async method named `ExampleMethodAsync`:</span></span>

```csharp
public async Task<int> ExampleMethodAsync()
{
    //...
}
```

<span data-ttu-id="638ba-107">如果您不熟悉非同步程式設計或不了解非同步方法如何使用[ `await` 運算子](../operators/await.md)來執行可能長時間執行的工作，而不封鎖呼叫端的執行緒，請閱讀[使用 Async 和 await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)的簡介。</span><span class="sxs-lookup"><span data-stu-id="638ba-107">If you're new to asynchronous programming or do not understand how an async method uses the [`await` operator](../operators/await.md) to do potentially long-running work without blocking the caller's thread, read the introduction in [Asynchronous programming with async and await](../../programming-guide/concepts/async/index.md).</span></span> <span data-ttu-id="638ba-108">下列程式碼位於非同步方法中，會呼叫 <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=nameWithType> 方法：</span><span class="sxs-lookup"><span data-stu-id="638ba-108">The following code is found inside an async method and calls the <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=nameWithType> method:</span></span>

```csharp
string contents = await httpClient.GetStringAsync(requestUrl);
```

<span data-ttu-id="638ba-109">非同步方法會以同步方式執行，直到抵達第一個 `await` 運算式，此時方法會暫停，直到等候的工作完成。</span><span class="sxs-lookup"><span data-stu-id="638ba-109">An async method runs synchronously until it reaches its first `await` expression, at which point the method is suspended until the awaited task is complete.</span></span> <span data-ttu-id="638ba-110">同時，控制項會返回方法的呼叫端，如下一節中的範例所示。</span><span class="sxs-lookup"><span data-stu-id="638ba-110">In the meantime, control returns to the caller of the method, as the example in the next section shows.</span></span>

<span data-ttu-id="638ba-111">如果 `async` 關鍵字修改的方法不包含 `await` 運算式或陳述式，則方法會以同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="638ba-111">If the method that the `async` keyword modifies doesn't contain an `await` expression or statement, the method executes synchronously.</span></span> <span data-ttu-id="638ba-112">如果有任何非同步方法未包含 `await` 陳述式，編譯器警告就會發出警示，因為這種情況可能表示發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="638ba-112">A compiler warning alerts you to any async methods that don't contain `await` statements, because that situation might indicate an error.</span></span> <span data-ttu-id="638ba-113">請參閱[編譯器警告 (層級 1) CS4014](../compiler-messages/cs4014.md)。</span><span class="sxs-lookup"><span data-stu-id="638ba-113">See [Compiler Warning (level 1) CS4014](../compiler-messages/cs4014.md).</span></span>

 <span data-ttu-id="638ba-114">`async` 關鍵字與內容相關，它只有在修改方法、Lambda 運算式或匿名方法時，才是關鍵字。</span><span class="sxs-lookup"><span data-stu-id="638ba-114">The `async` keyword is contextual in that it's a keyword only when it modifies a method, a lambda expression, or an anonymous method.</span></span> <span data-ttu-id="638ba-115">在所有其他內容中，它會解譯為識別項。</span><span class="sxs-lookup"><span data-stu-id="638ba-115">In all other contexts, it's interpreted as an identifier.</span></span>

## <a name="example"></a><span data-ttu-id="638ba-116">範例</span><span class="sxs-lookup"><span data-stu-id="638ba-116">Example</span></span>
<span data-ttu-id="638ba-117">下列範例將示範非同步事件處理常式 `StartButton_Click` 與非同步方法 `ExampleMethodAsync` 之間的控制結構與流程。</span><span class="sxs-lookup"><span data-stu-id="638ba-117">The following example shows the structure and flow of control between an async event handler, `StartButton_Click`, and an async method, `ExampleMethodAsync`.</span></span> <span data-ttu-id="638ba-118">非同步方法的結果是網頁的字元數。</span><span class="sxs-lookup"><span data-stu-id="638ba-118">The result from the async method is the number of characters of a web page.</span></span> <span data-ttu-id="638ba-119">此程式碼適用於您在 Visual Studio 中建立的 Windows Presentation Foundation (WPF) 應用程式或 Windows 市集應用程式。請參閱有關設定應用程式的程式碼註解。</span><span class="sxs-lookup"><span data-stu-id="638ba-119">The code is suitable for a Windows Presentation Foundation (WPF) app or Windows Store app that you create in Visual Studio; see the code comments for setting up the app.</span></span>

<span data-ttu-id="638ba-120">您可以在 Visual Studio 中將此程式碼執行為 Windows Presentation Foundation (WPF) 應用程式或 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="638ba-120">You can run this code in Visual Studio as a Windows Presentation Foundation (WPF) app or a Windows Store app.</span></span> <span data-ttu-id="638ba-121">您需要名為 `StartButton` 的按鈕控制項和名為 `ResultsTextBox` 的文字方塊控制項。</span><span class="sxs-lookup"><span data-stu-id="638ba-121">You need a Button control named `StartButton` and a Textbox control named `ResultsTextBox`.</span></span> <span data-ttu-id="638ba-122">請記住要設定名稱和處理常式，如此才會有像下面這樣的內容：</span><span class="sxs-lookup"><span data-stu-id="638ba-122">Remember to set the names and handler so that you have something like this:</span></span>

```xaml
<Button Content="Button" HorizontalAlignment="Left" Margin="88,77,0,0" VerticalAlignment="Top" Width="75"
        Click="StartButton_Click" Name="StartButton"/>
<TextBox HorizontalAlignment="Left" Height="137" Margin="88,140,0,0" TextWrapping="Wrap"
         Text="&lt;Enter a URL&gt;" VerticalAlignment="Top" Width="310" Name="ResultsTextBox"/>
```

<span data-ttu-id="638ba-123">將程式碼執行為 WPF 應用程式：</span><span class="sxs-lookup"><span data-stu-id="638ba-123">To run the code as a WPF app:</span></span>

- <span data-ttu-id="638ba-124">將此程式碼貼入 MainWindow.xaml.cs 的 `MainWindow` 類別。</span><span class="sxs-lookup"><span data-stu-id="638ba-124">Paste this code into the `MainWindow` class in MainWindow.xaml.cs.</span></span>
- <span data-ttu-id="638ba-125">將參考新增至 System.Net.Http。</span><span class="sxs-lookup"><span data-stu-id="638ba-125">Add a reference to System.Net.Http.</span></span>
- <span data-ttu-id="638ba-126">為 System.Net.Http 新增 `using` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="638ba-126">Add a `using` directive for System.Net.Http.</span></span>

<span data-ttu-id="638ba-127">將程式碼執行為 Windows 市集應用程式：</span><span class="sxs-lookup"><span data-stu-id="638ba-127">To run the code as a Windows Store app:</span></span>

- <span data-ttu-id="638ba-128">將此程式碼貼入 MainPage.xaml.cs 的 `MainPage` 類別。</span><span class="sxs-lookup"><span data-stu-id="638ba-128">Paste this code into the `MainPage` class in MainPage.xaml.cs.</span></span>
- <span data-ttu-id="638ba-129">為 System.Net.Http 和 System.Threading.Tasks 新增 using 指示詞。</span><span class="sxs-lookup"><span data-stu-id="638ba-129">Add using directives for System.Net.Http and System.Threading.Tasks.</span></span>

[!code-csharp[wpf-async](../../../../samples/snippets/csharp/language-reference/keywords/async/wpf/mainwindow.xaml.cs#1)]

> [!IMPORTANT]
> <span data-ttu-id="638ba-130">如需有關在等候工作時執行之工作和程式碼的詳細資訊，請參閱 [使用 async 和 await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)。</span><span class="sxs-lookup"><span data-stu-id="638ba-130">For more information about tasks and the code that executes while waiting for a task, see [Asynchronous programming with async and await](../../programming-guide/concepts/async/index.md).</span></span> <span data-ttu-id="638ba-131">如需使用類似專案的完整主控台範例，請參閱 [在完成時處理非同步工作 (c # ) ](../../programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md)。</span><span class="sxs-lookup"><span data-stu-id="638ba-131">For a full console example that uses similar elements, see [Process asynchronous tasks as they complete (C#)](../../programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md).</span></span>

## <a name="return-types"></a><span data-ttu-id="638ba-132">傳回型別</span><span class="sxs-lookup"><span data-stu-id="638ba-132">Return Types</span></span>
<span data-ttu-id="638ba-133">非同步方法可有下列傳回型別：</span><span class="sxs-lookup"><span data-stu-id="638ba-133">An async method can have the following return types:</span></span>

- <xref:System.Threading.Tasks.Task>
- <xref:System.Threading.Tasks.Task%601>
- <span data-ttu-id="638ba-134">[void](../builtin-types/void.md)。</span><span class="sxs-lookup"><span data-stu-id="638ba-134">[void](../builtin-types/void.md).</span></span> <span data-ttu-id="638ba-135">除了用於事件處理常式以外的程式碼，通常不鼓勵使用 `async void` 方法，因為呼叫者無法 `await` 這些方法，且必須實作不同的機制來報告成功完成或錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="638ba-135">`async void` methods are generally discouraged for code other than event handlers because callers cannot `await` those methods and must implement a different mechanism to report successful completion or error conditions.</span></span>
- <span data-ttu-id="638ba-136">自 C# 7.0 開始，任何具有可存取 `GetAwaiter` 方法的型別。</span><span class="sxs-lookup"><span data-stu-id="638ba-136">Starting with C# 7.0, any type that has an accessible `GetAwaiter` method.</span></span> <span data-ttu-id="638ba-137">`System.Threading.Tasks.ValueTask<TResult>` 類型就是一個這種實作。</span><span class="sxs-lookup"><span data-stu-id="638ba-137">The `System.Threading.Tasks.ValueTask<TResult>` type is one such implementation.</span></span> <span data-ttu-id="638ba-138">新增 NuGet 套件 `System.Threading.Tasks.Extensions` 即可使用。</span><span class="sxs-lookup"><span data-stu-id="638ba-138">It is available by adding the NuGet package `System.Threading.Tasks.Extensions`.</span></span>

<span data-ttu-id="638ba-139">非同步方法不可宣告任何 [in](./in-parameter-modifier.md)、[ref](./ref.md) 或 [out](./out-parameter-modifier.md) 參數，也不可以有 [參考傳回值](../../programming-guide/classes-and-structs/ref-returns.md)，但可以呼叫有這類參數的方法。</span><span class="sxs-lookup"><span data-stu-id="638ba-139">The async method can't declare any [in](./in-parameter-modifier.md), [ref](./ref.md) or [out](./out-parameter-modifier.md) parameters, nor can it have a [reference return value](../../programming-guide/classes-and-structs/ref-returns.md), but it can call methods that have such parameters.</span></span>

<span data-ttu-id="638ba-140">如果方法的 [return](./return.md) 陳述式指定 `TResult` 類型的運算元，請指定 `Task<TResult>` 作為非同步方法的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="638ba-140">You specify `Task<TResult>` as the return type of an async method if the [return](./return.md) statement of the method specifies an operand of type `TResult`.</span></span> <span data-ttu-id="638ba-141">如果方法完成時未傳回任何有意義的值，則使用 `Task`。</span><span class="sxs-lookup"><span data-stu-id="638ba-141">You use `Task` if no meaningful value is returned when the method is completed.</span></span> <span data-ttu-id="638ba-142">也就是說，呼叫方法會傳回 `Task`，但是當 `Task` 完成時，等候 `await` 的任何 `Task` 運算式都會判斷值為 `void`。</span><span class="sxs-lookup"><span data-stu-id="638ba-142">That is, a call to the method returns a `Task`, but when the `Task` is completed, any `await` expression that's awaiting the `Task` evaluates to `void`.</span></span>

<span data-ttu-id="638ba-143">您主要是使用 `void` 傳回類型定義需要該傳回類型的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="638ba-143">You use the `void` return type primarily to define event handlers, which require that return type.</span></span> <span data-ttu-id="638ba-144">傳回 `void` 之非同步方法的呼叫端無法等候它，而且無法攔截方法擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="638ba-144">The caller of a `void`-returning async method can't await it and can't catch exceptions that the method throws.</span></span>

<span data-ttu-id="638ba-145">自 C# 7.0 開始，您會傳回另一個型別，通常是實值型別，具有 `GetAwaiter` 方法可將程式碼效能關鍵區段中的記憶體配置降至最低。</span><span class="sxs-lookup"><span data-stu-id="638ba-145">Starting with C# 7.0, you return another type, typically a value type, that has a `GetAwaiter` method to minimize memory allocations in performance-critical sections of code.</span></span>

<span data-ttu-id="638ba-146">如需詳細資訊和範例，請參閱[非同步方法的傳回型別](../../programming-guide/concepts/async/async-return-types.md)。</span><span class="sxs-lookup"><span data-stu-id="638ba-146">For more information and examples, see [Async Return Types](../../programming-guide/concepts/async/async-return-types.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="638ba-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="638ba-147">See also</span></span>

- <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>
- [<span data-ttu-id="638ba-148">await</span><span class="sxs-lookup"><span data-stu-id="638ba-148">await</span></span>](../operators/await.md)
- [<span data-ttu-id="638ba-149">使用 async 和 await 進行非同步程式設計</span><span class="sxs-lookup"><span data-stu-id="638ba-149">Asynchronous programming with async and await</span></span>](../../programming-guide/concepts/async/index.md)
- [<span data-ttu-id="638ba-150">在非同步工作完成時進行處理</span><span class="sxs-lookup"><span data-stu-id="638ba-150">Process asynchronous tasks as they complete</span></span>](../../programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md)
