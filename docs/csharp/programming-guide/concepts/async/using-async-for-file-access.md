---
title: 使用非同步方式存取檔案 (C#)
ms.date: 07/20/2015
ms.assetid: bb018fea-5313-4c80-ab3f-7c24b2145bd9
ms.openlocfilehash: 8e0a62c2263ed3fd11eb4accb54978ef439ac010
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396953"
---
# <a name="using-async-for-file-access-c"></a><span data-ttu-id="41793-102">使用非同步方式存取檔案 (C#)</span><span class="sxs-lookup"><span data-stu-id="41793-102">Using Async for File Access (C#)</span></span>
<span data-ttu-id="41793-103">您可以使用非同步功能來存取檔案。</span><span class="sxs-lookup"><span data-stu-id="41793-103">You can use the async feature to access files.</span></span> <span data-ttu-id="41793-104">使用非同步功能，您就可以呼叫非同步方法，而不需要使用回呼或將您的程式碼分散到多種方法或 Lambda 運算式上。</span><span class="sxs-lookup"><span data-stu-id="41793-104">By using the async feature, you can call into asynchronous methods without using callbacks or splitting your code across multiple methods or lambda expressions.</span></span> <span data-ttu-id="41793-105">若要讓同步程式碼變成非同步，只要呼叫非同步方法 (而不是同步方法)，然後將幾個關鍵字新增至程式碼即可。</span><span class="sxs-lookup"><span data-stu-id="41793-105">To make synchronous code asynchronous, you just call an asynchronous method instead of a synchronous method and add a few keywords to the code.</span></span>  
  
 <span data-ttu-id="41793-106">您可能會基於下列原因將非同步功能新增至檔案存取呼叫：</span><span class="sxs-lookup"><span data-stu-id="41793-106">You might consider the following reasons for adding asynchrony to file access calls:</span></span>  
  
- <span data-ttu-id="41793-107">非同步功能可讓 UI 應用程式回應速度更快，因為啟動作業的 UI 執行緒可以執行其他工作。</span><span class="sxs-lookup"><span data-stu-id="41793-107">Asynchrony makes UI applications more responsive because the UI thread that launches the operation can perform other work.</span></span> <span data-ttu-id="41793-108">如果 UI 執行緒必須執行相當耗時的程式碼 (例如超過 50 毫秒)，UI 可能會凍結到 I/O 完成，之後 UI 執行緒就可以再次處理鍵盤和滑鼠輸入以及其他事件。</span><span class="sxs-lookup"><span data-stu-id="41793-108">If the UI thread must execute code that takes a long time (for example, more than 50 milliseconds), the UI may freeze until the I/O is complete and the UI thread can again process keyboard and mouse input and other events.</span></span>  
  
- <span data-ttu-id="41793-109">非同步功能藉由降低對執行緒的需求，來改善 ASP.NET 及其他伺服器架構應用程式的延展性。</span><span class="sxs-lookup"><span data-stu-id="41793-109">Asynchrony improves the scalability of ASP.NET and other server-based applications by reducing the need for threads.</span></span> <span data-ttu-id="41793-110">如果應用程式針對每個回應使用專用執行緒，並同時處理一千個要求，則需要一千個執行緒。</span><span class="sxs-lookup"><span data-stu-id="41793-110">If the application uses a dedicated thread per response and a thousand requests are being handled simultaneously, a thousand threads are needed.</span></span> <span data-ttu-id="41793-111">非同步作業在等候期間通常不需要使用執行緒。</span><span class="sxs-lookup"><span data-stu-id="41793-111">Asynchronous operations often don’t need to use a thread during the wait.</span></span> <span data-ttu-id="41793-112">它們可能會在結束時短暫使用現有的 I/O 完成執行緒。</span><span class="sxs-lookup"><span data-stu-id="41793-112">They use the existing I/O completion thread briefly at the end.</span></span>  
  
- <span data-ttu-id="41793-113">檔案存取作業的延遲在目前情況下可能很低，但未來可能會大幅增加。</span><span class="sxs-lookup"><span data-stu-id="41793-113">The latency of a file access operation might be very low under current conditions, but the latency may greatly increase in the future.</span></span> <span data-ttu-id="41793-114">例如，檔案可能會移至世界各地的伺服器。</span><span class="sxs-lookup"><span data-stu-id="41793-114">For example, a file may be moved to a server that's across the world.</span></span>  
  
- <span data-ttu-id="41793-115">使用非同步功能所增加的額外負荷很小。</span><span class="sxs-lookup"><span data-stu-id="41793-115">The added overhead of using the Async feature is small.</span></span>  
  
- <span data-ttu-id="41793-116">您可以輕鬆地同時執行多個非同步工作。</span><span class="sxs-lookup"><span data-stu-id="41793-116">Asynchronous tasks can easily be run in parallel.</span></span>  
  
## <a name="running-the-examples"></a><span data-ttu-id="41793-117">執行範例</span><span class="sxs-lookup"><span data-stu-id="41793-117">Running the Examples</span></span>  
 <span data-ttu-id="41793-118">為了執行本主題中的範例，您可以建立 **WPF 應用程式**或 **Windows Forms 應用程式**，然後新增一個**按鈕**。</span><span class="sxs-lookup"><span data-stu-id="41793-118">To run the examples in this topic, you can create a **WPF Application** or a **Windows Forms Application** and then add a **Button**.</span></span> <span data-ttu-id="41793-119">在按鈕的 `Click` 事件中，新增呼叫至每個範例中的第一個方法。</span><span class="sxs-lookup"><span data-stu-id="41793-119">In the button's `Click` event, add a call to the first method in each example.</span></span>  
  
 <span data-ttu-id="41793-120">在下列範例中，請加入下列指示詞 `using` 。</span><span class="sxs-lookup"><span data-stu-id="41793-120">In the following examples, include the following `using` directives.</span></span>  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Diagnostics;  
using System.IO;  
using System.Text;  
using System.Threading.Tasks;  
```  
  
## <a name="use-of-the-filestream-class"></a><span data-ttu-id="41793-121">使用 FileStream 類別</span><span class="sxs-lookup"><span data-stu-id="41793-121">Use of the FileStream Class</span></span>  
 <span data-ttu-id="41793-122">本主題中的範例使用 <xref:System.IO.FileStream> 類別，其所包含的一個選項會導致在作業系統層級發生非同步 I/O。</span><span class="sxs-lookup"><span data-stu-id="41793-122">The examples in this topic use the <xref:System.IO.FileStream> class, which has an option that causes asynchronous I/O to occur at the operating system level.</span></span> <span data-ttu-id="41793-123">您可以在許多情況下，使用此選項來避免封鎖 ThreadPool 執行緒。</span><span class="sxs-lookup"><span data-stu-id="41793-123">By using this option, you can avoid blocking a ThreadPool thread in many cases.</span></span> <span data-ttu-id="41793-124">若要啟用此選項，請在建構函式呼叫中指定 `useAsync=true` 或 `options=FileOptions.Asynchronous` 引數。</span><span class="sxs-lookup"><span data-stu-id="41793-124">To enable this option, you specify the `useAsync=true` or `options=FileOptions.Asynchronous` argument in the constructor call.</span></span>  
  
 <span data-ttu-id="41793-125">如果您藉由指定檔案路徑來直接開啟它們，就無法搭配使用這個選項與 <xref:System.IO.StreamReader> 和 <xref:System.IO.StreamWriter>。</span><span class="sxs-lookup"><span data-stu-id="41793-125">You can’t use this option with <xref:System.IO.StreamReader> and <xref:System.IO.StreamWriter> if you open them directly by specifying a file path.</span></span> <span data-ttu-id="41793-126">不過，如果您提供它們已開啟 <xref:System.IO.FileStream> 類別的 <xref:System.IO.Stream>，則可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="41793-126">However, you can use this option if you provide them a <xref:System.IO.Stream> that the <xref:System.IO.FileStream> class opened.</span></span> <span data-ttu-id="41793-127">請注意，即使已封鎖 ThreadPool 執行緒，非同步呼叫在 UI 應用程式中還是更快，因為在等候期間不會封鎖 UI 執行緒。</span><span class="sxs-lookup"><span data-stu-id="41793-127">Note that asynchronous calls are faster in UI apps even if a ThreadPool thread is blocked, because the UI thread isn’t blocked during the wait.</span></span>  
  
## <a name="writing-text"></a><span data-ttu-id="41793-128">寫入文字</span><span class="sxs-lookup"><span data-stu-id="41793-128">Writing Text</span></span>  
 <span data-ttu-id="41793-129">下列範例會將文字寫入檔案。</span><span class="sxs-lookup"><span data-stu-id="41793-129">The following example writes text to a file.</span></span> <span data-ttu-id="41793-130">在每個 await 陳述式中，此方法會立即結束。</span><span class="sxs-lookup"><span data-stu-id="41793-130">At each await statement, the method immediately exits.</span></span> <span data-ttu-id="41793-131">當檔案 I/O 完成時，此方法會在 await 陳述式後面的陳述式繼續進行。</span><span class="sxs-lookup"><span data-stu-id="41793-131">When the file I/O is complete, the method resumes at the statement that follows the await statement.</span></span> <span data-ttu-id="41793-132">請注意，使用 await 陳述式的方法定義中會有 async 修飾詞。</span><span class="sxs-lookup"><span data-stu-id="41793-132">Note that the async modifier is in the definition of methods that use the await statement.</span></span>  
  
```csharp  
public async Task ProcessWriteAsync()  
{  
    string filePath = @"temp2.txt";  
    string text = "Hello World\r\n";  
  
    await WriteTextAsync(filePath, text);  
}  
  
private async Task WriteTextAsync(string filePath, string text)  
{  
    byte[] encodedText = Encoding.Unicode.GetBytes(text);  
  
    using (FileStream sourceStream = new FileStream(filePath,  
        FileMode.Append, FileAccess.Write, FileShare.None,  
        bufferSize: 4096, useAsync: true))  
    {  
        await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
    };  
}  
```  
  
 <span data-ttu-id="41793-133">原始範例具有陳述式 `await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);`，這是下列兩個陳述式的縮減：</span><span class="sxs-lookup"><span data-stu-id="41793-133">The original example has the statement `await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);`, which is a contraction of the following two statements:</span></span>  
  
```csharp  
Task theTask = sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
await theTask;  
```  
  
 <span data-ttu-id="41793-134">第一個陳述式會傳回一個工作並開始處理檔案。</span><span class="sxs-lookup"><span data-stu-id="41793-134">The first statement returns a task and causes file processing to start.</span></span> <span data-ttu-id="41793-135">第二個陳述式具有 await，會立即結束方法並傳回其他工作。</span><span class="sxs-lookup"><span data-stu-id="41793-135">The second statement with the await causes the method to immediately exit and return a different task.</span></span> <span data-ttu-id="41793-136">稍後完成處理檔案之後，則會回到 await 後面的陳述式繼續執行。</span><span class="sxs-lookup"><span data-stu-id="41793-136">When the file processing later completes, execution returns to the statement that follows the await.</span></span> <span data-ttu-id="41793-137">如需詳細資訊，請參閱[非同步程式中的控制流程 (C#)](./control-flow-in-async-programs.md)。</span><span class="sxs-lookup"><span data-stu-id="41793-137">For more information, see  [Control Flow in Async Programs (C#)](./control-flow-in-async-programs.md).</span></span>  
  
## <a name="reading-text"></a><span data-ttu-id="41793-138">讀取文字</span><span class="sxs-lookup"><span data-stu-id="41793-138">Reading Text</span></span>  
 <span data-ttu-id="41793-139">下列範例會從檔案讀取文字。</span><span class="sxs-lookup"><span data-stu-id="41793-139">The following example reads text from a file.</span></span> <span data-ttu-id="41793-140">此文字已經過緩衝處理，在本例中已置於 <xref:System.Text.StringBuilder>。</span><span class="sxs-lookup"><span data-stu-id="41793-140">The text is buffered and, in this case, placed into a <xref:System.Text.StringBuilder>.</span></span> <span data-ttu-id="41793-141">不同於上一個範例，await 的評估會產生一個值。</span><span class="sxs-lookup"><span data-stu-id="41793-141">Unlike in the previous example, the evaluation of the await produces a value.</span></span> <span data-ttu-id="41793-142"><xref:System.IO.Stream.ReadAsync%2A> 方法會傳回 <xref:System.Threading.Tasks.Task>\<<xref:System.Int32>>，因此在作業完成之後，await 的評估會產生 `Int32` 值 (`numRead`)。</span><span class="sxs-lookup"><span data-stu-id="41793-142">The <xref:System.IO.Stream.ReadAsync%2A> method returns a <xref:System.Threading.Tasks.Task>\<<xref:System.Int32>>, so the evaluation of the await produces an `Int32` value (`numRead`) after the operation completes.</span></span> <span data-ttu-id="41793-143">如需詳細資訊，請參閱[非同步方法的傳回型別 (C#)](./async-return-types.md)。</span><span class="sxs-lookup"><span data-stu-id="41793-143">For more information, see [Async Return Types (C#)](./async-return-types.md).</span></span>  
  
```csharp  
public async Task ProcessReadAsync()  
{  
    string filePath = @"temp2.txt";  
  
    if (File.Exists(filePath) == false)  
    {  
        Debug.WriteLine("file not found: " + filePath);  
    }  
    else  
    {  
        try  
        {  
            string text = await ReadTextAsync(filePath);  
            Debug.WriteLine(text);  
        }  
        catch (Exception ex)  
        {  
            Debug.WriteLine(ex.Message);  
        }  
    }  
}  
  
private async Task<string> ReadTextAsync(string filePath)  
{  
    using (FileStream sourceStream = new FileStream(filePath,  
        FileMode.Open, FileAccess.Read, FileShare.Read,  
        bufferSize: 4096, useAsync: true))  
    {  
        StringBuilder sb = new StringBuilder();  
  
        byte[] buffer = new byte[0x1000];  
        int numRead;  
        while ((numRead = await sourceStream.ReadAsync(buffer, 0, buffer.Length)) != 0)  
        {  
            string text = Encoding.Unicode.GetString(buffer, 0, numRead);  
            sb.Append(text);  
        }  
  
        return sb.ToString();  
    }  
}  
```  
  
## <a name="parallel-asynchronous-io"></a><span data-ttu-id="41793-144">平行非同步 I/O</span><span class="sxs-lookup"><span data-stu-id="41793-144">Parallel Asynchronous I/O</span></span>  
 <span data-ttu-id="41793-145">下列範例示範如何平行處理寫入 10 個文字檔的作業。</span><span class="sxs-lookup"><span data-stu-id="41793-145">The following example demonstrates parallel processing by writing 10 text files.</span></span> <span data-ttu-id="41793-146">針對每個檔案，<xref:System.IO.Stream.WriteAsync%2A> 方法會傳回一個工作，此工作之後會新增至工作清單。</span><span class="sxs-lookup"><span data-stu-id="41793-146">For each file, the <xref:System.IO.Stream.WriteAsync%2A> method returns a task that is then added to a list of tasks.</span></span> <span data-ttu-id="41793-147">`await Task.WhenAll(tasks);` 陳述式會在所有工作的檔案處理完成時結束方法，並在方法內繼續進行。</span><span class="sxs-lookup"><span data-stu-id="41793-147">The `await Task.WhenAll(tasks);` statement exits the method and resumes within the method when file processing is complete for all of the tasks.</span></span>  
  
 <span data-ttu-id="41793-148">此範例會在工作完成之後，關閉 `finally` 區塊中的所有 <xref:System.IO.FileStream> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="41793-148">The example closes all <xref:System.IO.FileStream> instances in a `finally` block after the tasks are complete.</span></span> <span data-ttu-id="41793-149">如果改為在 `using` 陳述式中建立每個 `FileStream`，`FileStream` 可能會在工作完成前就被處置。</span><span class="sxs-lookup"><span data-stu-id="41793-149">If each `FileStream` was instead created in a `using` statement, the `FileStream` might be disposed of before the task was complete.</span></span>  
  
 <span data-ttu-id="41793-150">請注意，任何效能提升幾乎完全來自平行處理，而不是非同步處理。</span><span class="sxs-lookup"><span data-stu-id="41793-150">Note that any performance boost is almost entirely from the parallel processing and not the asynchronous processing.</span></span> <span data-ttu-id="41793-151">非同步的優點在於不會佔用多個執行緒，而且不會佔用使用者介面執行緒。</span><span class="sxs-lookup"><span data-stu-id="41793-151">The advantages of asynchrony are that it doesn’t tie up multiple threads, and that it doesn’t tie up the user interface thread.</span></span>  
  
```csharp  
public async Task ProcessWriteMultAsync()  
{  
    string folder = @"tempfolder\";  
    List<Task> tasks = new List<Task>();  
    List<FileStream> sourceStreams = new List<FileStream>();  
  
    try  
    {  
        for (int index = 1; index <= 10; index++)  
        {  
            string text = "In file " + index.ToString() + "\r\n";  
  
            string fileName = "thefile" + index.ToString("00") + ".txt";  
            string filePath = folder + fileName;  
  
            byte[] encodedText = Encoding.Unicode.GetBytes(text);  
  
            FileStream sourceStream = new FileStream(filePath,  
                FileMode.Append, FileAccess.Write, FileShare.None,  
                bufferSize: 4096, useAsync: true);  
  
            Task theTask = sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
            sourceStreams.Add(sourceStream);  
  
            tasks.Add(theTask);  
        }  
  
        await Task.WhenAll(tasks);  
    }  
  
    finally  
    {  
        foreach (FileStream sourceStream in sourceStreams)  
        {  
            sourceStream.Close();  
        }  
    }  
}  
```  
  
 <span data-ttu-id="41793-152">使用 <xref:System.IO.Stream.WriteAsync%2A> 和 <xref:System.IO.Stream.ReadAsync%2A> 方法時，您可以指定 <xref:System.Threading.CancellationToken>，這可用來在中途取消作業。</span><span class="sxs-lookup"><span data-stu-id="41793-152">When using the <xref:System.IO.Stream.WriteAsync%2A> and <xref:System.IO.Stream.ReadAsync%2A> methods, you can specify a <xref:System.Threading.CancellationToken>, which you can use to cancel the operation mid-stream.</span></span> <span data-ttu-id="41793-153">如需詳細資訊，請參閱[微調非同步應用程式 (C#)](./fine-tuning-your-async-application.md) 和 [Managed 執行緒中的取消作業](../../../../standard/threading/cancellation-in-managed-threads.md)。</span><span class="sxs-lookup"><span data-stu-id="41793-153">For more information, see [Fine-Tuning Your Async Application (C#)](./fine-tuning-your-async-application.md) and [Cancellation in Managed Threads](../../../../standard/threading/cancellation-in-managed-threads.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="41793-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="41793-154">See also</span></span>

- [<span data-ttu-id="41793-155">使用 Async 和 Await 進行非同步程式設計 (C#)</span><span class="sxs-lookup"><span data-stu-id="41793-155">Asynchronous Programming with async and await (C#)</span></span>](./index.md)
- [<span data-ttu-id="41793-156">非同步方法的傳回型別 (C#)</span><span class="sxs-lookup"><span data-stu-id="41793-156">Async Return Types (C#)</span></span>](./async-return-types.md)
- [<span data-ttu-id="41793-157">非同步程式中的控制流程（c #）</span><span class="sxs-lookup"><span data-stu-id="41793-157">Control Flow in Async Programs (C#)</span></span>](./control-flow-in-async-programs.md)
