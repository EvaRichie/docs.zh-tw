---
title: async - C# 參考
ms.date: 05/22/2017
f1_keywords:
- async_CSharpKeyword
helpviewer_keywords:
- async keyword [C#]
- async method [C#]
- async [C#]
ms.assetid: 16f14f09-b2ce-42c7-a875-e4eca5d50674
ms.openlocfilehash: 279ea2f9875681401c9c7acab922d9e4424e6827
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88062531"
---
# <a name="async-c-reference"></a><span data-ttu-id="b21f4-102">async (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="b21f4-102">async (C# Reference)</span></span>

<span data-ttu-id="b21f4-103">使用 `async` 修飾詞可將方法、[Lambda 運算式](../operators/lambda-expressions.md)或[匿名方法](../operators/delegate-operator.md)指定為非同步。</span><span class="sxs-lookup"><span data-stu-id="b21f4-103">Use the `async` modifier to specify that a method, [lambda expression](../operators/lambda-expressions.md), or [anonymous method](../operators/delegate-operator.md) is asynchronous.</span></span> <span data-ttu-id="b21f4-104">如果您在方法或運算式上使用這個修飾詞，則它是指「非同步方法」\*\*。</span><span class="sxs-lookup"><span data-stu-id="b21f4-104">If you use this modifier on a method or expression, it's referred to as an *async method*.</span></span> <span data-ttu-id="b21f4-105">下例定義名為 `ExampleMethodAsync` 的非同步方法：</span><span class="sxs-lookup"><span data-stu-id="b21f4-105">The following example defines an async method named `ExampleMethodAsync`:</span></span>
  
```csharp  
public async Task<int> ExampleMethodAsync()  
{  
    // . . . .  
}  
```  

<span data-ttu-id="b21f4-106">如果您不熟悉非同步程式設計或不了解非同步方法如何使用[ `await` 運算子](../operators/await.md)來執行可能長時間執行的工作，而不封鎖呼叫端的執行緒，請閱讀[使用 Async 和 Await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)中的簡介。</span><span class="sxs-lookup"><span data-stu-id="b21f4-106">If you're new to asynchronous programming or do not understand how an async method uses the [`await` operator](../operators/await.md) to do potentially long-running work without blocking the caller's thread, read the introduction in [Asynchronous Programming with async and await](../../programming-guide/concepts/async/index.md).</span></span> <span data-ttu-id="b21f4-107">下列程式碼位於非同步方法中，會呼叫 <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=nameWithType> 方法：</span><span class="sxs-lookup"><span data-stu-id="b21f4-107">The following code is found inside an async method and calls the <xref:System.Net.Http.HttpClient.GetStringAsync%2a?displayProperty=nameWithType> method:</span></span>
  
```csharp  
string contents = await httpClient.GetStringAsync(requestUrl);  
```  
  
<span data-ttu-id="b21f4-108">非同步方法會以同步方式執行，直到抵達第一個 `await` 運算式，此時方法會暫停，直到等候的工作完成。</span><span class="sxs-lookup"><span data-stu-id="b21f4-108">An async method runs synchronously until it reaches its first `await` expression, at which point the method is suspended until the awaited task is complete.</span></span> <span data-ttu-id="b21f4-109">同時，控制項會返回方法的呼叫端，如下一節中的範例所示。</span><span class="sxs-lookup"><span data-stu-id="b21f4-109">In the meantime, control returns to the caller of the method, as the example in the next section shows.</span></span>  
  
<span data-ttu-id="b21f4-110">如果 `async` 關鍵字修改的方法不包含 `await` 運算式或陳述式，則方法會以同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="b21f4-110">If the method that the `async` keyword modifies doesn't contain an `await` expression or statement, the method executes synchronously.</span></span> <span data-ttu-id="b21f4-111">如果有任何非同步方法未包含 `await` 陳述式，編譯器警告就會發出警示，因為這種情況可能表示發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="b21f4-111">A compiler warning alerts you to any async methods that don't contain `await` statements, because that situation might indicate an error.</span></span> <span data-ttu-id="b21f4-112">請參閱[編譯器警告 (層級 1) CS4014](../compiler-messages/cs4014.md)。</span><span class="sxs-lookup"><span data-stu-id="b21f4-112">See [Compiler Warning (level 1) CS4014](../compiler-messages/cs4014.md).</span></span>  
  
 <span data-ttu-id="b21f4-113">`async` 關鍵字與內容相關，它只有在修改方法、Lambda 運算式或匿名方法時，才是關鍵字。</span><span class="sxs-lookup"><span data-stu-id="b21f4-113">The `async` keyword is contextual in that it's a keyword only when it modifies a method, a lambda expression, or an anonymous method.</span></span> <span data-ttu-id="b21f4-114">在所有其他內容中，它會解譯為識別項。</span><span class="sxs-lookup"><span data-stu-id="b21f4-114">In all other contexts, it's interpreted as an identifier.</span></span>  
  
## <a name="example"></a><span data-ttu-id="b21f4-115">範例</span><span class="sxs-lookup"><span data-stu-id="b21f4-115">Example</span></span>  
<span data-ttu-id="b21f4-116">下列範例將示範非同步事件處理常式 `StartButton_Click` 與非同步方法 `ExampleMethodAsync` 之間的控制結構與流程。</span><span class="sxs-lookup"><span data-stu-id="b21f4-116">The following example shows the structure and flow of control between an async event handler, `StartButton_Click`, and an async method, `ExampleMethodAsync`.</span></span> <span data-ttu-id="b21f4-117">非同步方法的結果是網頁的字元數。</span><span class="sxs-lookup"><span data-stu-id="b21f4-117">The result from the async method is the number of characters of a web page.</span></span> <span data-ttu-id="b21f4-118">此程式碼適用於您在 Visual Studio 中建立的 Windows Presentation Foundation (WPF) 應用程式或 Windows 市集應用程式。請參閱有關設定應用程式的程式碼註解。</span><span class="sxs-lookup"><span data-stu-id="b21f4-118">The code is suitable for a Windows Presentation Foundation (WPF) app or Windows Store app that you create in Visual Studio; see the code comments for setting up the app.</span></span>  

<span data-ttu-id="b21f4-119">您可以在 Visual Studio 中將此程式碼執行為 Windows Presentation Foundation (WPF) 應用程式或 Windows 市集應用程式。</span><span class="sxs-lookup"><span data-stu-id="b21f4-119">You can run this code in Visual Studio as a Windows Presentation Foundation (WPF) app or a Windows Store app.</span></span> <span data-ttu-id="b21f4-120">您需要名為 `StartButton` 的按鈕控制項和名為 `ResultsTextBox` 的文字方塊控制項。</span><span class="sxs-lookup"><span data-stu-id="b21f4-120">You need a Button control named `StartButton` and a Textbox control named `ResultsTextBox`.</span></span> <span data-ttu-id="b21f4-121">請記住要設定名稱和處理常式，如此才會有像下面這樣的內容：</span><span class="sxs-lookup"><span data-stu-id="b21f4-121">Remember to set the names and handler so that you have something like this:</span></span>  

```xaml
<Button Content="Button" HorizontalAlignment="Left" Margin="88,77,0,0" VerticalAlignment="Top" Width="75"  
        Click="StartButton_Click" Name="StartButton"/>  
<TextBox HorizontalAlignment="Left" Height="137" Margin="88,140,0,0" TextWrapping="Wrap"
         Text="&lt;Enter a URL&gt;" VerticalAlignment="Top" Width="310" Name="ResultsTextBox"/>  
```
  
<span data-ttu-id="b21f4-122">將程式碼執行為 WPF 應用程式：</span><span class="sxs-lookup"><span data-stu-id="b21f4-122">To run the code as a WPF app:</span></span>  

- <span data-ttu-id="b21f4-123">將此程式碼貼入 MainWindow.xaml.cs 的 `MainWindow` 類別。</span><span class="sxs-lookup"><span data-stu-id="b21f4-123">Paste this code into the `MainWindow` class in MainWindow.xaml.cs.</span></span>  
- <span data-ttu-id="b21f4-124">將參考新增至 System.Net.Http。</span><span class="sxs-lookup"><span data-stu-id="b21f4-124">Add a reference to System.Net.Http.</span></span>  
- <span data-ttu-id="b21f4-125">為 System.Net.Http 新增 `using` 指示詞。</span><span class="sxs-lookup"><span data-stu-id="b21f4-125">Add a `using` directive for System.Net.Http.</span></span>  
  
<span data-ttu-id="b21f4-126">將程式碼執行為 Windows 市集應用程式：</span><span class="sxs-lookup"><span data-stu-id="b21f4-126">To run the code as a Windows Store app:</span></span>  

- <span data-ttu-id="b21f4-127">將此程式碼貼入 MainPage.xaml.cs 的 `MainPage` 類別。</span><span class="sxs-lookup"><span data-stu-id="b21f4-127">Paste this code into the `MainPage` class in MainPage.xaml.cs.</span></span>  
- <span data-ttu-id="b21f4-128">為 System.Net.Http 和 System.Threading.Tasks 新增 using 指示詞。</span><span class="sxs-lookup"><span data-stu-id="b21f4-128">Add using directives for System.Net.Http and System.Threading.Tasks.</span></span>  
  
[!code-csharp[wpf-async](../../../../samples/snippets/csharp/language-reference/keywords/async/wpf/mainwindow.xaml.cs#1)]
  
> [!IMPORTANT]
> <span data-ttu-id="b21f4-129">如需工作以及等候工作時執行之程式碼的詳細資訊，請參閱[使用 async 和 await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)。</span><span class="sxs-lookup"><span data-stu-id="b21f4-129">For more information about tasks and the code that executes while waiting for a task, see [Asynchronous Programming with async and await](../../programming-guide/concepts/async/index.md).</span></span> <span data-ttu-id="b21f4-130">如需使用類似項目的完整 WPF 範例，請參閱[逐步解說：使用 async 和 await 存取 Web](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。</span><span class="sxs-lookup"><span data-stu-id="b21f4-130">For a full WPF example that uses similar elements, see [Walkthrough: Accessing the Web by Using Async and Await](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span>  
  
## <a name="return-types"></a><span data-ttu-id="b21f4-131">傳回型別</span><span class="sxs-lookup"><span data-stu-id="b21f4-131">Return Types</span></span>  
<span data-ttu-id="b21f4-132">非同步方法可有下列傳回型別：</span><span class="sxs-lookup"><span data-stu-id="b21f4-132">An async method can have the following return types:</span></span>

- <xref:System.Threading.Tasks.Task>
- <xref:System.Threading.Tasks.Task%601>
- <span data-ttu-id="b21f4-133">[void](../builtin-types/void.md)。</span><span class="sxs-lookup"><span data-stu-id="b21f4-133">[void](../builtin-types/void.md).</span></span> <span data-ttu-id="b21f4-134">除了用於事件處理常式以外的程式碼，通常不鼓勵使用 `async void` 方法，因為呼叫者無法 `await` 這些方法，且必須實作不同的機制來報告成功完成或錯誤狀況。</span><span class="sxs-lookup"><span data-stu-id="b21f4-134">`async void` methods are generally discouraged for code other than event handlers because callers cannot `await` those methods and must implement a different mechanism to report successful completion or error conditions.</span></span>
- <span data-ttu-id="b21f4-135">自 C# 7.0 開始，任何具有可存取 `GetAwaiter` 方法的型別。</span><span class="sxs-lookup"><span data-stu-id="b21f4-135">Starting with C# 7.0, any type that has an accessible `GetAwaiter` method.</span></span> <span data-ttu-id="b21f4-136">`System.Threading.Tasks.ValueTask<TResult>` 類型就是一個這種實作。</span><span class="sxs-lookup"><span data-stu-id="b21f4-136">The `System.Threading.Tasks.ValueTask<TResult>` type is one such implementation.</span></span> <span data-ttu-id="b21f4-137">新增 NuGet 套件 `System.Threading.Tasks.Extensions` 即可使用。</span><span class="sxs-lookup"><span data-stu-id="b21f4-137">It is available by adding the NuGet package `System.Threading.Tasks.Extensions`.</span></span>

<span data-ttu-id="b21f4-138">非同步方法不可宣告任何 [in](./in-parameter-modifier.md)、[ref](./ref.md) 或 [out](./out-parameter-modifier.md) 參數，也不可以有 [參考傳回值](../../programming-guide/classes-and-structs/ref-returns.md)，但可以呼叫有這類參數的方法。</span><span class="sxs-lookup"><span data-stu-id="b21f4-138">The async method can't declare any [in](./in-parameter-modifier.md), [ref](./ref.md) or [out](./out-parameter-modifier.md) parameters, nor can it have a [reference return value](../../programming-guide/classes-and-structs/ref-returns.md), but it can call methods that have such parameters.</span></span>  
  
<span data-ttu-id="b21f4-139">如果方法的 [return](./return.md) 陳述式指定 `TResult` 類型的運算元，請指定 `Task<TResult>` 作為非同步方法的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="b21f4-139">You specify `Task<TResult>` as the return type of an async method if the [return](./return.md) statement of the method specifies an operand of type `TResult`.</span></span> <span data-ttu-id="b21f4-140">如果方法完成時未傳回任何有意義的值，則使用 `Task`。</span><span class="sxs-lookup"><span data-stu-id="b21f4-140">You use `Task` if no meaningful value is returned when the method is completed.</span></span> <span data-ttu-id="b21f4-141">也就是說，呼叫方法會傳回 `Task`，但是當 `Task` 完成時，等候 `await` 的任何 `Task` 運算式都會判斷值為 `void`。</span><span class="sxs-lookup"><span data-stu-id="b21f4-141">That is, a call to the method returns a `Task`, but when the `Task` is completed, any `await` expression that's awaiting the `Task` evaluates to `void`.</span></span>  
  
<span data-ttu-id="b21f4-142">您主要是使用 `void` 傳回類型定義需要該傳回類型的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="b21f4-142">You use the `void` return type primarily to define event handlers, which require that return type.</span></span> <span data-ttu-id="b21f4-143">傳回 `void` 之非同步方法的呼叫端無法等候它，而且無法攔截方法擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b21f4-143">The caller of a `void`-returning async method can't await it and can't catch exceptions that the method throws.</span></span>  

<span data-ttu-id="b21f4-144">自 C# 7.0 開始，您會傳回另一個型別，通常是實值型別，具有 `GetAwaiter` 方法可將程式碼效能關鍵區段中的記憶體配置降至最低。</span><span class="sxs-lookup"><span data-stu-id="b21f4-144">Starting with C# 7.0, you return another type, typically a value type, that has a `GetAwaiter` method to minimize memory allocations in performance-critical sections of code.</span></span>

<span data-ttu-id="b21f4-145">如需詳細資訊和範例，請參閱[非同步方法的傳回型別](../../programming-guide/concepts/async/async-return-types.md)。</span><span class="sxs-lookup"><span data-stu-id="b21f4-145">For more information and examples, see [Async Return Types](../../programming-guide/concepts/async/async-return-types.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b21f4-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b21f4-146">See also</span></span>

- <xref:System.Runtime.CompilerServices.AsyncStateMachineAttribute>
- [<span data-ttu-id="b21f4-147">await</span><span class="sxs-lookup"><span data-stu-id="b21f4-147">await</span></span>](../operators/await.md)
- [<span data-ttu-id="b21f4-148">逐步解說：使用 Async 和 Await 存取 Web</span><span class="sxs-lookup"><span data-stu-id="b21f4-148">Walkthrough: Accessing the Web by Using Async and Await</span></span>](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [<span data-ttu-id="b21f4-149">使用 async 和 await 進行非同步程式設計</span><span class="sxs-lookup"><span data-stu-id="b21f4-149">Asynchronous Programming with async and await</span></span>](../../programming-guide/concepts/async/index.md)
