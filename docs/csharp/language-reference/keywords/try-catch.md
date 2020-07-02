---
title: try-catch - C# 參考
ms.date: 07/20/2015
f1_keywords:
- try
- try_CSharpKeyword
- catch
- catch_CSharpKeyword
helpviewer_keywords:
- catch keyword [C#]
- try-catch statement [C#]
ms.assetid: cb5503c7-bfa1-4610-8fc2-ddcd2e84c438
ms.openlocfilehash: 4715a27a94ac86c5e4955c0e8be95c6ee4a28507
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619698"
---
# <a name="try-catch-c-reference"></a><span data-ttu-id="6e325-102">try-catch (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="6e325-102">try-catch (C# Reference)</span></span>

<span data-ttu-id="6e325-103">try-catch 陳述式包含 `try` 區塊後面接著一個或多個 `catch` 子句，指定不同例外狀況的處理常式。</span><span class="sxs-lookup"><span data-stu-id="6e325-103">The try-catch statement consists of a `try` block followed by one or more `catch` clauses, which specify handlers for different exceptions.</span></span>

<span data-ttu-id="6e325-104">擲回例外狀況時，Common Language Runtime (CLR) 會尋找處理此例外狀況的 `catch` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="6e325-104">When an exception is thrown, the common language runtime (CLR) looks for the `catch` statement that handles this exception.</span></span> <span data-ttu-id="6e325-105">如果目前執行的方法不包含這類 `catch` 區塊，CLR 會在呼叫堆疊上查看呼叫目前方法的方法，依此類推。</span><span class="sxs-lookup"><span data-stu-id="6e325-105">If the currently executing method does not contain such a `catch` block, the CLR looks at the method that called the current method, and so on up the call stack.</span></span> <span data-ttu-id="6e325-106">如果找不到 `catch` 區塊，則 CLR 會向使用者顯示未處理的例外狀況訊息，並停止執行程式。</span><span class="sxs-lookup"><span data-stu-id="6e325-106">If no `catch` block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="6e325-107">`try` 區塊包含可能會造成例外狀況的防護程式碼。</span><span class="sxs-lookup"><span data-stu-id="6e325-107">The `try` block contains the guarded code that may cause the exception.</span></span> <span data-ttu-id="6e325-108">區塊會執行直到例外狀況擲回，或已成功完成。</span><span class="sxs-lookup"><span data-stu-id="6e325-108">The block is executed until an exception is thrown or it is completed successfully.</span></span> <span data-ttu-id="6e325-109">例如，以下的轉換 `null` 物件嘗試會引發 <xref:System.NullReferenceException> 例外狀況：</span><span class="sxs-lookup"><span data-stu-id="6e325-109">For example, the following attempt to cast a `null` object raises the <xref:System.NullReferenceException> exception:</span></span>

```csharp
object o2 = null;
try
{
    int i2 = (int)o2;   // Error
}
```

<span data-ttu-id="6e325-110">雖然可以不含引數使用 `catch` 子句，來攔截任何類型的例外狀況，不建議使用這種用法。</span><span class="sxs-lookup"><span data-stu-id="6e325-110">Although the `catch` clause can be used without arguments to catch any type of exception, this usage is not recommended.</span></span> <span data-ttu-id="6e325-111">一般而言，您應該只攔截那些您知道如何從中復原的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-111">In general, you should only catch those exceptions that you know how to recover from.</span></span> <span data-ttu-id="6e325-112">因此，您應該永遠指定衍生自 <xref:System.Exception?displayProperty=nameWithType> 的物件引數，例如：</span><span class="sxs-lookup"><span data-stu-id="6e325-112">Therefore, you should always specify an object argument derived from <xref:System.Exception?displayProperty=nameWithType> For example:</span></span>

```csharp
catch (InvalidCastException e)
{
}
```

<span data-ttu-id="6e325-113">您可以在相同 try catch 陳述式中的子句中使用多個特定的 `catch`。</span><span class="sxs-lookup"><span data-stu-id="6e325-113">It is possible to use more than one specific `catch` clause in the same try-catch statement.</span></span> <span data-ttu-id="6e325-114">在此情況下，`catch` 子句的順序很重要，因為會依順序檢查 `catch` 子句。</span><span class="sxs-lookup"><span data-stu-id="6e325-114">In this case, the order of the `catch` clauses is important because the `catch` clauses are examined in order.</span></span> <span data-ttu-id="6e325-115">在較不特定的例外狀況之前攔截較特定的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-115">Catch the more specific exceptions before the less specific ones.</span></span> <span data-ttu-id="6e325-116">如果您排序 catch 區塊，使得永遠不會達到較新的區塊，編譯器會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6e325-116">The compiler produces an error if you order your catch blocks so that a later block can never be reached.</span></span>

<span data-ttu-id="6e325-117">使用 `catch` 引數是篩選您想要處理的例外狀況的一種方式。</span><span class="sxs-lookup"><span data-stu-id="6e325-117">Using `catch` arguments is one way to filter for the exceptions you want to handle.</span></span>  <span data-ttu-id="6e325-118">您也可以使用例外狀況篩選，進一步檢查例外狀況來決定是否要處理。</span><span class="sxs-lookup"><span data-stu-id="6e325-118">You can also use an exception filter that further examines the exception to decide whether to handle it.</span></span>  <span data-ttu-id="6e325-119">如果例外狀況篩選會傳回 false，則搜尋處理常式會繼續。</span><span class="sxs-lookup"><span data-stu-id="6e325-119">If the exception filter returns false, then the search for a handler continues.</span></span>

```csharp
catch (ArgumentException e) when (e.ParamName == "…")
{
}
```

<span data-ttu-id="6e325-120">例外狀況篩選條件優於攔截和重新擲回 (說明如下所示)，因為篩選條件不會損壞堆疊。</span><span class="sxs-lookup"><span data-stu-id="6e325-120">Exception filters are preferable to catching and rethrowing (explained below) because filters leave the stack unharmed.</span></span>  <span data-ttu-id="6e325-121">如果之後的處理常式傾印堆疊，您可以看到例外狀況原本來自何處，而不是只重新擲回的最後一個位置。</span><span class="sxs-lookup"><span data-stu-id="6e325-121">If a later handler dumps the stack, you can see where the exception originally came from, rather than just the last place it was rethrown.</span></span>  <span data-ttu-id="6e325-122">例外狀況篩選條件運算式的常見用法是記錄。</span><span class="sxs-lookup"><span data-stu-id="6e325-122">A common use of exception filter expressions is logging.</span></span>  <span data-ttu-id="6e325-123">您可以建立一律會傳回 false 同時會輸出到記錄檔的篩選，您可以持續記錄例外狀況，而不必處理它們並重新擲回。</span><span class="sxs-lookup"><span data-stu-id="6e325-123">You can create a filter that always returns false that also outputs to a log, you can log exceptions as they go by without having to handle them and rethrow.</span></span>

<span data-ttu-id="6e325-124">[throw](throw.md) 陳述式可以在 `catch` 區塊中用來重新擲回 `catch` 陳述式攔截到的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-124">A [throw](throw.md) statement can be used in a `catch` block to re-throw the exception that is caught by the `catch` statement.</span></span> <span data-ttu-id="6e325-125">下列範例會從 <xref:System.IO.IOException> 例外狀況擷取來源資訊，然後將例外狀況擲回父方法。</span><span class="sxs-lookup"><span data-stu-id="6e325-125">The following example extracts source information from an <xref:System.IO.IOException> exception, and then throws the exception to the parent method.</span></span>

```csharp
catch (FileNotFoundException e)
{
    // FileNotFoundExceptions are handled here.
}
catch (IOException e)
{
    // Extract some information from this exception, and then
    // throw it to the parent method.
    if (e.Source != null)
        Console.WriteLine("IOException source: {0}", e.Source);
    throw;
}
```

<span data-ttu-id="6e325-126">您可以攔截一個例外狀況，並擲回不同的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-126">You can catch one exception and throw a different exception.</span></span> <span data-ttu-id="6e325-127">執行此動作時，請將您攔截的例外狀況指定為內部例外狀況，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6e325-127">When you do this, specify the exception that you caught as the inner exception, as shown in the following example.</span></span>

```csharp
catch (InvalidCastException e)
{
    // Perform some action here, and then throw a new exception.
    throw new YourCustomException("Put your error message here.", e);
}
```

<span data-ttu-id="6e325-128">指定的條件為 true 時，您可以也重新擲回例外狀況時，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6e325-128">You can also re-throw an exception when a specified condition is true, as shown in the following example.</span></span>

```csharp
catch (InvalidCastException e)
{
    if (e.Data == null)
    {
        throw;
    }
    else
    {
        // Take some action.
    }
}
```

> [!NOTE]
> <span data-ttu-id="6e325-129">也可以使用例外狀況篩選，以通常更為簡潔的方式取得類似的結果 (以及未修改堆疊，如本文件稍早所述)。</span><span class="sxs-lookup"><span data-stu-id="6e325-129">It is also possible to use an exception filter to get a similar result in an often cleaner fashion (as well as not modifying the stack, as explained earlier in this document).</span></span> <span data-ttu-id="6e325-130">下列範例的呼叫端行為類似於上一個範例。</span><span class="sxs-lookup"><span data-stu-id="6e325-130">The following example has a similar behavior for callers as the previous example.</span></span> <span data-ttu-id="6e325-131">此函式會在 `e.Data` 為 `null` 時，將 `InvalidCastException` 擲回呼叫端。</span><span class="sxs-lookup"><span data-stu-id="6e325-131">The function throws the `InvalidCastException` back to the caller when `e.Data` is `null`.</span></span>
>
> ```csharp
> catch (InvalidCastException e) when (e.Data != null)
> {
>     // Take some action.
> }
> ```

<span data-ttu-id="6e325-132">從 `try` 區塊內，僅初始化其中宣告的變數。</span><span class="sxs-lookup"><span data-stu-id="6e325-132">From inside a `try` block, initialize only variables that are declared therein.</span></span> <span data-ttu-id="6e325-133">否則，在區塊的執行完成之前，可能會發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-133">Otherwise, an exception can occur before the execution of the block is completed.</span></span> <span data-ttu-id="6e325-134">例如，在下列程式碼範例中，變數 `n` 是在 `try` 區塊內初始化。</span><span class="sxs-lookup"><span data-stu-id="6e325-134">For example, in the following code example, the variable `n` is initialized inside the `try` block.</span></span> <span data-ttu-id="6e325-135">在 `Write(n)` 陳述式中的 `try` 區塊外嘗試使用此變數，將產生編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="6e325-135">An attempt to use this variable outside the `try` block in the `Write(n)` statement will generate a compiler error.</span></span>

```csharp
static void Main()
{
    int n;
    try
    {
        // Do not initialize this variable here.
        n = 123;
    }
    catch
    {
    }
    // Error: Use of unassigned local variable 'n'.
    Console.Write(n);
}
```

<span data-ttu-id="6e325-136">如需 catch 的詳細資訊，請參閱 [try-catch-finally](try-catch-finally.md)。</span><span class="sxs-lookup"><span data-stu-id="6e325-136">For more information about catch, see [try-catch-finally](try-catch-finally.md).</span></span>

## <a name="exceptions-in-async-methods"></a><span data-ttu-id="6e325-137">非同步方法中的例外狀況</span><span class="sxs-lookup"><span data-stu-id="6e325-137">Exceptions in async methods</span></span>

<span data-ttu-id="6e325-138">非同步方法會標記 [async](async.md) 修飾詞，而且通常包含一或多個 await 運算式或陳述式。</span><span class="sxs-lookup"><span data-stu-id="6e325-138">An async method is marked  by an  [async](async.md) modifier and usually contains one or more await expressions or statements.</span></span> <span data-ttu-id="6e325-139">await 運算式會將 [await](../operators/await.md) 運算子套用至 <xref:System.Threading.Tasks.Task> 或 <xref:System.Threading.Tasks.Task%601>。</span><span class="sxs-lookup"><span data-stu-id="6e325-139">An await expression applies the [await](../operators/await.md) operator to a <xref:System.Threading.Tasks.Task> or <xref:System.Threading.Tasks.Task%601>.</span></span>

<span data-ttu-id="6e325-140">當控制項到達 `await` 方法時，方法中的進度會暫停，直到等候的工作完成。</span><span class="sxs-lookup"><span data-stu-id="6e325-140">When control reaches an `await` in the async method, progress in the method is suspended until the awaited task completes.</span></span> <span data-ttu-id="6e325-141">當工作完成時，方法中的執行可以繼續。</span><span class="sxs-lookup"><span data-stu-id="6e325-141">When the task  is complete, execution can resume in the method.</span></span> <span data-ttu-id="6e325-142">如需詳細資訊，請參閱[使用 async 和 await 進行非同步程式設計](../../programming-guide/concepts/async/index.md)和[非同步程式中的控制流程](../../programming-guide/concepts/async/control-flow-in-async-programs.md)。</span><span class="sxs-lookup"><span data-stu-id="6e325-142">For more information, see [Asynchronous Programming with async and await](../../programming-guide/concepts/async/index.md) and [Control Flow in Async Programs](../../programming-guide/concepts/async/control-flow-in-async-programs.md).</span></span>

<span data-ttu-id="6e325-143">套用 `await` 完成的工作可能因為傳回工作的方法中未處理的例外狀況而處於錯誤的狀態。</span><span class="sxs-lookup"><span data-stu-id="6e325-143">The completed task to which `await` is applied might be in a faulted state because of an unhandled exception in the method that returns the task.</span></span> <span data-ttu-id="6e325-144">等候工作擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-144">Awaiting the task throws an exception.</span></span> <span data-ttu-id="6e325-145">如果傳回工作的非同步程序被取消，工作也可能以取消的狀態結束。</span><span class="sxs-lookup"><span data-stu-id="6e325-145">A task can also end up in a canceled state if the asynchronous process that returns it is canceled.</span></span> <span data-ttu-id="6e325-146">等候已取消的工作會擲回 `OperationCanceledException`。</span><span class="sxs-lookup"><span data-stu-id="6e325-146">Awaiting a canceled task throws  an `OperationCanceledException`.</span></span> <span data-ttu-id="6e325-147">如需如何取消非同步處理序的詳細資訊，請參閱[微調非同步應用程式](../../programming-guide/concepts/async/fine-tuning-your-async-application.md)。</span><span class="sxs-lookup"><span data-stu-id="6e325-147">For more information about how to cancel an asynchronous process, see [Fine-Tuning Your Async Application](../../programming-guide/concepts/async/fine-tuning-your-async-application.md).</span></span>

<span data-ttu-id="6e325-148">若要攔截例外狀況，請在 `try` 區塊中等候工作，並在關聯的 `catch` 區塊中攔截例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-148">To catch the exception, await the task in a `try` block, and catch the exception in the associated `catch` block.</span></span> <span data-ttu-id="6e325-149">如需範例，請參閱[非同步方法範例](#async-method-example)一節。</span><span class="sxs-lookup"><span data-stu-id="6e325-149">For an example, see the [Async method example](#async-method-example) section.</span></span>

<span data-ttu-id="6e325-150">工作可能處於錯誤狀態，因為在等候的非同步方法中發生多個例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-150">A task can be in a faulted state because multiple exceptions occurred in the awaited async method.</span></span> <span data-ttu-id="6e325-151">例如，工作可能是對 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 呼叫的結果。</span><span class="sxs-lookup"><span data-stu-id="6e325-151">For example, the task might be the result of a call to <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="6e325-152">當您等候這類工作時，只會攔截到其中一個例外狀況，而且您無法預測會攔截的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-152">When you await such a task, only one of the exceptions is caught, and you can't predict which exception will be caught.</span></span> <span data-ttu-id="6e325-153">如需範例，請參閱 [Task.WhenAll 範例](#taskwhenall-example)一節。</span><span class="sxs-lookup"><span data-stu-id="6e325-153">For an example, see the [Task.WhenAll example](#taskwhenall-example) section.</span></span>

## <a name="example"></a><span data-ttu-id="6e325-154">範例</span><span class="sxs-lookup"><span data-stu-id="6e325-154">Example</span></span>

<span data-ttu-id="6e325-155">在下列範例中，`try` 區塊包含可能會造成例外狀況的對 `ProcessString` 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="6e325-155">In the following example, the `try` block contains a call to the `ProcessString` method that may cause an exception.</span></span> <span data-ttu-id="6e325-156">`catch` 子句包含只會在螢幕上顯示訊息的例外狀況處理常式。</span><span class="sxs-lookup"><span data-stu-id="6e325-156">The `catch` clause contains the exception handler that just displays a message on the screen.</span></span> <span data-ttu-id="6e325-157">從 `ProcessString` 內呼叫 `throw` 陳述式時 ，系統會尋找 `catch` 陳述式，並顯示訊息 `Exception caught`。</span><span class="sxs-lookup"><span data-stu-id="6e325-157">When the `throw` statement is called from inside `ProcessString`, the system looks for the `catch` statement and displays the message `Exception caught`.</span></span>

[!code-csharp[csrefKeywordsExceptions#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsExceptions/CS/csrefKeywordsExceptions.cs#2)]

## <a name="two-catch-blocks-example"></a><span data-ttu-id="6e325-158">兩個 catch 區塊範例</span><span class="sxs-lookup"><span data-stu-id="6e325-158">Two catch blocks example</span></span>

<span data-ttu-id="6e325-159">在下列範例中，使用了兩個 catch 區塊，並會攔截會先出現的最特定例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-159">In the following example, two catch blocks are used, and the most specific exception, which comes first, is caught.</span></span>

<span data-ttu-id="6e325-160">若要攔截最不特定的例外狀況，您可以使用下列陳述式取代 `ProcessString` 中的 throw 陳述式：`throw new Exception()`。</span><span class="sxs-lookup"><span data-stu-id="6e325-160">To catch the least specific exception, you can replace the throw statement in `ProcessString` with the following statement: `throw new Exception()`.</span></span>

<span data-ttu-id="6e325-161">如果您先在範例中放置最特定的 catch 區塊，會出現下列錯誤訊息：`A previous catch clause already catches all exceptions of this or a super type ('System.Exception')`。</span><span class="sxs-lookup"><span data-stu-id="6e325-161">If you place the least-specific catch block first in the example, the following  error message appears: `A previous catch clause already catches all exceptions of this or a super type ('System.Exception')`.</span></span>

[!code-csharp[csrefKeywordsExceptions#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsExceptions/CS/csrefKeywordsExceptions.cs#3)]

## <a name="async-method-example"></a><span data-ttu-id="6e325-162">非同步方法範例</span><span class="sxs-lookup"><span data-stu-id="6e325-162">Async method example</span></span>

<span data-ttu-id="6e325-163">下列範例說明非同步方法的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="6e325-163">The following example illustrates exception handling for async methods.</span></span> <span data-ttu-id="6e325-164">若要擷取非同步工作擲回的例外狀況，請將 `await` 運算式放置在 `try` 區塊中，並攔截 `catch` 區塊中的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-164">To catch an exception that an async task throws, place the `await` expression in a `try` block, and catch the exception in a `catch` block.</span></span>

<span data-ttu-id="6e325-165">取消註解範例中的 `throw new Exception` 行來示範例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="6e325-165">Uncomment the `throw new Exception` line in the example to demonstrate exception handling.</span></span> <span data-ttu-id="6e325-166">工作的 `IsFaulted` 屬性設定為 `True`，工作的 `Exception.InnerException` 屬性設定為例外狀況，並在 `catch` 區塊攔截例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-166">The task's `IsFaulted` property is set to `True`, the task's `Exception.InnerException` property is set to the exception, and the exception is caught in the `catch` block.</span></span>

<span data-ttu-id="6e325-167">取消註解 `throw new OperationCanceledException` 行來示範取消非同步處理序時會發生的情況。</span><span class="sxs-lookup"><span data-stu-id="6e325-167">Uncomment the `throw new OperationCanceledException` line to demonstrate what happens when you cancel an asynchronous process.</span></span> <span data-ttu-id="6e325-168">工作的 `IsCanceled` 屬性設定為 `true`，並在 `catch` 區塊攔截例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-168">The task's `IsCanceled` property is set to `true`, and the exception is caught in the `catch` block.</span></span> <span data-ttu-id="6e325-169">在不適用這個範例的部分情況下，工作的 `IsFaulted` 屬性會設定為 `true` 而 `IsCanceled` 設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="6e325-169">Under some conditions that don't apply to this example, the task's `IsFaulted` property is set to `true` and `IsCanceled` is set to `false`.</span></span>

[!code-csharp[csAsyncExceptions#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csasyncexceptions/cs/class1.cs#2)]  

## <a name="taskwhenall-example"></a><span data-ttu-id="6e325-170">Task.WhenAll 範例</span><span class="sxs-lookup"><span data-stu-id="6e325-170">Task.WhenAll example</span></span>

<span data-ttu-id="6e325-171">下列範例說明多項工作可能會導致多個例外狀況的例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="6e325-171">The following example illustrates exception handling where multiple tasks can result in multiple exceptions.</span></span> <span data-ttu-id="6e325-172">`try` 區塊會等候對 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 的呼叫傳回的工作。</span><span class="sxs-lookup"><span data-stu-id="6e325-172">The `try` block awaits the task that's returned by a call to <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="6e325-173">當套用所有項目的三項工作都完成時，工作即完成。</span><span class="sxs-lookup"><span data-stu-id="6e325-173">The task is complete when the three tasks to which WhenAll is applied are complete.</span></span>

<span data-ttu-id="6e325-174">這三個工作都會造成例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6e325-174">Each of the three tasks causes an exception.</span></span> <span data-ttu-id="6e325-175">`catch` 區塊會逐一查看例外狀況，這可以在 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 傳回的工作的 `Exception.InnerExceptions` 屬性中找到。</span><span class="sxs-lookup"><span data-stu-id="6e325-175">The `catch` block iterates through the exceptions, which are found in the `Exception.InnerExceptions` property of the task that was returned by <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>.</span></span>

[!code-csharp[csAsyncExceptions#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csasyncexceptions/cs/class1.cs#4)]

## <a name="c-language-specification"></a><span data-ttu-id="6e325-176">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="6e325-176">C# language specification</span></span>

<span data-ttu-id="6e325-177">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的 [try 陳述式](~/_csharplang/spec/statements.md#the-try-statement)一節。</span><span class="sxs-lookup"><span data-stu-id="6e325-177">For more information, see [The try statement](~/_csharplang/spec/statements.md#the-try-statement) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6e325-178">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6e325-178">See also</span></span>

- [<span data-ttu-id="6e325-179">C # 參考</span><span class="sxs-lookup"><span data-stu-id="6e325-179">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="6e325-180">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="6e325-180">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="6e325-181">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="6e325-181">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="6e325-182">try、throw 和 catch 陳述式 (C++)</span><span class="sxs-lookup"><span data-stu-id="6e325-182">try, throw, and catch Statements (C++)</span></span>](/cpp/cpp/try-throw-and-catch-statements-cpp)
- [<span data-ttu-id="6e325-183">放棄</span><span class="sxs-lookup"><span data-stu-id="6e325-183">throw</span></span>](throw.md)
- [<span data-ttu-id="6e325-184">try-最後</span><span class="sxs-lookup"><span data-stu-id="6e325-184">try-finally</span></span>](try-finally.md)
- [<span data-ttu-id="6e325-185">如何：明確擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="6e325-185">How to: Explicitly Throw Exceptions</span></span>](../../../standard/exceptions/how-to-explicitly-throw-exceptions.md)
