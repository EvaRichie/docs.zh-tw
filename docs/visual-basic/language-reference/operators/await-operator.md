---
title: Await 運算子
ms.date: 07/20/2015
f1_keywords:
- vb.Await
helpviewer_keywords:
- Await operator [Visual Basic]
- Await [Visual Basic]
ms.assetid: 6b1ce283-e92b-4ba7-b081-7be7b3d37af9
ms.openlocfilehash: 9d55ba82547dfcb0336c3a3fd12521c0dcb3eb58
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371826"
---
# <a name="await-operator-visual-basic"></a><span data-ttu-id="9a4f2-102">Await 運算子 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="9a4f2-102">Await Operator (Visual Basic)</span></span>

<span data-ttu-id="9a4f2-103">您在非同步方法或 Lambda 運算式的運算元中套用 `Await` 運算子，讓方法暫停執行，直到等候的工作完成。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-103">You apply the `Await` operator to an operand in an asynchronous method or lambda expression to suspend execution of the method until the awaited task completes.</span></span> <span data-ttu-id="9a4f2-104">工作代表進行中的工作。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-104">The task represents ongoing work.</span></span>

<span data-ttu-id="9a4f2-105">使用的方法 `Await` 必須有[Async](../modifiers/async.md)修飾詞。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-105">The method in which `Await` is used must have an [Async](../modifiers/async.md) modifier.</span></span> <span data-ttu-id="9a4f2-106">這種方法是使用 `Async` 修飾詞所定義，且通常包含一或多個 `Await` 運算式，我們稱之為「非同步方法」\*\*。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-106">Such a method, defined by using the `Async` modifier, and usually containing one or more `Await` expressions, is referred to as an *async method*.</span></span>

> [!NOTE]
> <span data-ttu-id="9a4f2-107">`Async` 和 `Await` 關鍵字是在 Visual Studio 2012 中引入。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-107">The `Async` and `Await` keywords were introduced in Visual Studio 2012.</span></span> <span data-ttu-id="9a4f2-108">如需非同步程式設計的簡介，請參閱[使用 async 和 Await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-108">For an introduction to async programming, see [Asynchronous Programming with Async and Await](../../programming-guide/concepts/async/index.md).</span></span>

<span data-ttu-id="9a4f2-109">一般來說，您套用運算子的工作 `Await` 就是呼叫方法的傳回值，該方法會執行以工作為[基礎的非同步模式](https://www.microsoft.com/download/details.aspx?id=19957)，也就是 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601> 。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-109">Typically, the task to which you apply the `Await` operator is the return value from a call to a method that implements the [Task-Based Asynchronous Pattern](https://www.microsoft.com/download/details.aspx?id=19957), that is, a <xref:System.Threading.Tasks.Task> or a <xref:System.Threading.Tasks.Task%601>.</span></span>

<span data-ttu-id="9a4f2-110">在下列程式碼中，<xref:System.Net.Http.HttpClient> 方法 <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> 會傳回 `getContentsTask`，也就是 `Task(Of Byte())`。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-110">In the following code, the <xref:System.Net.Http.HttpClient> method <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> returns `getContentsTask`, a `Task(Of Byte())`.</span></span> <span data-ttu-id="9a4f2-111">這個工作可保證作業完成時，一定會產生實際位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-111">The task is a promise to produce the actual byte array when the operation is complete.</span></span> <span data-ttu-id="9a4f2-112">`Await` 運算子會套用至 `getContentsTask` 以暫停在 `SumPageSizesAsync` 中執行，直到 `getContentsTask` 完成。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-112">The `Await` operator is applied to `getContentsTask` to suspend execution in `SumPageSizesAsync` until `getContentsTask` is complete.</span></span> <span data-ttu-id="9a4f2-113">同時，控制權會返回 `SumPageSizesAsync` 的呼叫端。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-113">In the meantime, control is returned to the caller of `SumPageSizesAsync`.</span></span> <span data-ttu-id="9a4f2-114">當 `getContentsTask` 完成之後，`Await` 運算式會評估為位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-114">When `getContentsTask` is finished, the `Await` expression evaluates to a byte array.</span></span>

```vb
Private Async Function SumPageSizesAsync() As Task

    ' To use the HttpClient type in desktop apps, you must include a using directive and add a
    ' reference for the System.Net.Http namespace.
    Dim client As HttpClient = New HttpClient()
    ' . . .
    Dim getContentsTask As Task(Of Byte()) = client.GetByteArrayAsync(url)
    Dim urlContents As Byte() = Await getContentsTask

    ' Equivalently, now that you see how it works, you can write the same thing in a single line.
    'Dim urlContents As Byte() = Await client.GetByteArrayAsync(url)
    ' . . .
End Function
```

> [!IMPORTANT]
> <span data-ttu-id="9a4f2-115">如需完整範例，請參閱[逐步解說：使用 async 和 await 存取 Web](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-115">For the complete example, see [Walkthrough: Accessing the Web by Using Async and Await](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span> <span data-ttu-id="9a4f2-116">您可以從 Microsoft 網站的[開發人員程式碼範例](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f) 下載此範例。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-116">You can download the sample from [Developer Code Samples](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f) on the Microsoft website.</span></span> <span data-ttu-id="9a4f2-117">此範例位於 AsyncWalkthrough_HttpClient 專案中。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-117">The example is in the AsyncWalkthrough_HttpClient project.</span></span>

<span data-ttu-id="9a4f2-118">如果將 `Await` 套用至傳回 `Task(Of TResult)` 之方法呼叫的結果，則 `Await` 運算式的類型為 TResult。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-118">If `Await` is applied to the result of a method call that returns a `Task(Of TResult)`, the type of the `Await` expression is TResult.</span></span> <span data-ttu-id="9a4f2-119">如果 `Await` 套用至傳回 `Task` 之方法呼叫的結果，則 `Await` 運算式不會傳回值。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-119">If `Await` is applied to the result of a method call that returns a `Task`, the `Await` expression doesn't return a value.</span></span> <span data-ttu-id="9a4f2-120">下列範例會說明其間的差異。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-120">The following example illustrates the difference.</span></span>

```vb
' Await used with a method that returns a Task(Of TResult).
Dim result As TResult = Await AsyncMethodThatReturnsTaskTResult()

' Await used with a method that returns a Task.
Await AsyncMethodThatReturnsTask()
```

<span data-ttu-id="9a4f2-121">`Await` 運算式或陳述式不會封鎖其執行所在的執行緒。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-121">An `Await` expression or statement does not block the thread on which it is executing.</span></span> <span data-ttu-id="9a4f2-122">但是它會造成編譯器將 `Await` 運算式之後的其餘非同步方法註冊為所等候工作的接續。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-122">Instead, it causes the compiler to sign up the rest of the async method, after the `Await` expression, as a continuation on the awaited task.</span></span> <span data-ttu-id="9a4f2-123">控制權接著會返回非同步方法的呼叫端。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-123">Control then returns to the caller of the async method.</span></span> <span data-ttu-id="9a4f2-124">當工作完成時，它會叫用其接續，並從中斷處繼續執行非同步方法。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-124">When the task completes, it invokes its continuation, and execution of the async method resumes where it left off.</span></span>

<span data-ttu-id="9a4f2-125">`Await` 運算式可能只會在 `Async` 修飾詞所標示之立即封入方法或 Lambda 運算式主體中發生。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-125">An `Await` expression can occur only in the body of an immediately enclosing method or lambda expression that is marked by an `Async` modifier.</span></span> <span data-ttu-id="9a4f2-126">*Await*一詞僅作為該內容中的關鍵字。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-126">The term *Await* serves as a keyword only in that context.</span></span> <span data-ttu-id="9a4f2-127">在其他內容中，它會解譯為識別項。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-127">Elsewhere, it is interpreted as an identifier.</span></span> <span data-ttu-id="9a4f2-128">在 `Async` 方法或 lambda 運算式中， `Await` 運算式不能出現在查詢運算式中、Try 的 `Catch` 或 `Finally` 區塊中[。Catch .。。Finally 語句](../statements/try-catch-finally-statement.md)，在或迴圈的迴圈控制變數運算式 `For` 中 `For Each` ，或在[SyncLock](../statements/synclock-statement.md)語句的主體中。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-128">Within the `Async` method or lambda expression, an `Await` expression cannot occur in a query expression, in the `Catch` or `Finally` block of a [Try…Catch…Finally statement](../statements/try-catch-finally-statement.md), in the loop control variable expression of a `For` or `For Each` loop, or in the body of a [SyncLock](../statements/synclock-statement.md) statement.</span></span>

## <a name="exceptions"></a><span data-ttu-id="9a4f2-129">例外狀況</span><span class="sxs-lookup"><span data-stu-id="9a4f2-129">Exceptions</span></span>

<span data-ttu-id="9a4f2-130">大部分的非同步方法會傳回 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-130">Most async methods return a <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="9a4f2-131">傳回的工作屬性會隨附其狀態和記錄的相關資訊，例如工作是否完成、非同步方法是否造成例外狀況或已取消，以及最終結果為何。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-131">The properties of the returned task carry information about its status and history, such as whether the task is complete, whether the async method caused an exception or was canceled, and what the final result is.</span></span> <span data-ttu-id="9a4f2-132">`Await` 運算子存取這些屬性。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-132">The `Await` operator accesses those properties.</span></span>

<span data-ttu-id="9a4f2-133">如果您在等候工作傳回非同步方法時導致例外狀況，`Await` 運算子會重新擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-133">If you await a task-returning async method that causes an exception, the  `Await` operator rethrows the exception.</span></span>

<span data-ttu-id="9a4f2-134">如果您等候已取消的工作傳回非同步方法，則 `Await` 運算子會重新擲回 <xref:System.OperationCanceledException>。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-134">If you await a task-returning async method that is canceled, the `Await` operator rethrows an <xref:System.OperationCanceledException>.</span></span>

<span data-ttu-id="9a4f2-135">處於錯誤狀態的單一工作可能反映多個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-135">A single task that is in a faulted state can reflect multiple exceptions.</span></span>  <span data-ttu-id="9a4f2-136">例如，工作可能是對 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 呼叫的結果。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-136">For example, the task might be the result of a call to <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="9a4f2-137">當您等候這類工作時，await 作業只會重新擲回其中一個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-137">When you await such a task, the await operation rethrows only one of the exceptions.</span></span> <span data-ttu-id="9a4f2-138">不過，您無法預測重新擲回哪個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-138">However, you can't predict which of the exceptions is rethrown.</span></span>

<span data-ttu-id="9a4f2-139">如需非同步方法中錯誤處理的範例，請參閱[嘗試 .。。Catch .。。Finally 語句](../statements/try-catch-finally-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-139">For examples of error handling in async methods, see [Try...Catch...Finally Statement](../statements/try-catch-finally-statement.md).</span></span>

## <a name="example"></a><span data-ttu-id="9a4f2-140">範例</span><span class="sxs-lookup"><span data-stu-id="9a4f2-140">Example</span></span>

<span data-ttu-id="9a4f2-141">下列 Windows Form 範例說明如何在非同步方法 `WaitAsynchronouslyAsync` 中使用 `Await`。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-141">The following Windows Forms example illustrates the use of `Await` in an async method, `WaitAsynchronouslyAsync`.</span></span> <span data-ttu-id="9a4f2-142">請對照該方法的行為與 `WaitSynchronously` 的行為。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-142">Contrast the behavior of that method with the behavior of `WaitSynchronously`.</span></span> <span data-ttu-id="9a4f2-143">若沒有 `Await` 運算子，儘管在定義中使用 `WaitSynchronously` 修飾詞並在主體中呼叫 `Async`，<xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> 仍會以同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="9a4f2-143">Without an `Await` operator, `WaitSynchronously` runs synchronously despite the use of the `Async` modifier in its definition and a call to <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType> in its body.</span></span>

```vb
Private Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
    ' Call the method that runs asynchronously.
    Dim result As String = Await WaitAsynchronouslyAsync()

    ' Call the method that runs synchronously.
    'Dim result As String = Await WaitSynchronously()

    ' Display the result.
    TextBox1.Text &= result
End Sub

' The following method runs asynchronously. The UI thread is not
' blocked during the delay. You can move or resize the Form1 window
' while Task.Delay is running.
Public Async Function WaitAsynchronouslyAsync() As Task(Of String)
    Await Task.Delay(10000)
    Return "Finished"
End Function

' The following method runs synchronously, despite the use of Async.
' You cannot move or resize the Form1 window while Thread.Sleep
' is running because the UI thread is blocked.
Public Async Function WaitSynchronously() As Task(Of String)
    ' Import System.Threading for the Sleep method.
    Thread.Sleep(10000)
    Return "Finished"
End Function
```

## <a name="see-also"></a><span data-ttu-id="9a4f2-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9a4f2-144">See also</span></span>

- [<span data-ttu-id="9a4f2-145">使用 Async 和 Await 進行非同步程式設計</span><span class="sxs-lookup"><span data-stu-id="9a4f2-145">Asynchronous Programming with Async and Await</span></span>](../../programming-guide/concepts/async/index.md)
- [<span data-ttu-id="9a4f2-146">逐步解說：使用 Async 和 Await 存取 Web</span><span class="sxs-lookup"><span data-stu-id="9a4f2-146">Walkthrough: Accessing the Web by Using Async and Await</span></span>](../../programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)
- [<span data-ttu-id="9a4f2-147">非同步</span><span class="sxs-lookup"><span data-stu-id="9a4f2-147">Async</span></span>](../modifiers/async.md)
