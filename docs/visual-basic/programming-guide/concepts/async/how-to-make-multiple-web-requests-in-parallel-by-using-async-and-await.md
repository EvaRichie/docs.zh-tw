---
title: 如何：使用 Async 和 Await，同時發出多個 Web 要求
ms.date: 07/20/2015
ms.assetid: a894b99b-7cfd-4a38-adfb-20d24f986730
ms.openlocfilehash: 40bab392af94ba941c2562e885a8d2e08aeea5b9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396580"
---
# <a name="how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await-visual-basic"></a><span data-ttu-id="4b131-102">如何：使用 Async 和 Await，同時發出多個 Web 要求 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="4b131-102">How to: Make Multiple Web Requests in Parallel by Using Async and Await (Visual Basic)</span></span>

<span data-ttu-id="4b131-103">在非同步方法中，工作會在建立後啟動。</span><span class="sxs-lookup"><span data-stu-id="4b131-103">In an async method, tasks are started when they’re created.</span></span> <span data-ttu-id="4b131-104">[Await](../../../language-reference/operators/await-operator.md)運算子會套用至方法中的工作點，在此情況下無法繼續處理，直到工作完成為止。</span><span class="sxs-lookup"><span data-stu-id="4b131-104">The [Await](../../../language-reference/operators/await-operator.md) operator is applied to the task at the point in the method where processing can’t continue until the task finishes.</span></span> <span data-ttu-id="4b131-105">通常，工作會在建立後等候完成，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="4b131-105">Often a task is awaited as soon as it’s created, as the following example shows.</span></span>

```vb
Dim result = Await someWebAccessMethodAsync(url)
```

<span data-ttu-id="4b131-106">不過，如果您的程式有其他要完成的工作不需要等候此工作完成，您可以將建立工作與等候工作分開進行。</span><span class="sxs-lookup"><span data-stu-id="4b131-106">However, you can separate creating the task from awaiting the task if your program has other work to accomplish that doesn’t depend on the completion of the task.</span></span>

```vb
' The following line creates and starts the task.
Dim myTask = someWebAccessMethodAsync(url)

' While the task is running, you can do other work that does not depend
' on the results of the task.
' . . . . .

' The application of Await suspends the rest of this method until the task is
' complete.
Dim result = Await myTask
```

<span data-ttu-id="4b131-107">從工作啟動到等候完成的這段期間，您可以啟動其他工作。</span><span class="sxs-lookup"><span data-stu-id="4b131-107">Between starting a task and awaiting it, you can start other tasks.</span></span> <span data-ttu-id="4b131-108">其他工作會以隱含方式平行執行，但不會建立其他任何執行緒。</span><span class="sxs-lookup"><span data-stu-id="4b131-108">The additional tasks implicitly run in parallel, but no additional threads are created.</span></span>

<span data-ttu-id="4b131-109">下列程式會啟動三個非同步的網頁下載，然後依呼叫順序等候完成。</span><span class="sxs-lookup"><span data-stu-id="4b131-109">The following program starts three asynchronous web downloads and then awaits them in the order in which they’re called.</span></span> <span data-ttu-id="4b131-110">請注意，當您執行此程式時，這些工作不一定會依建立和等候順序完成。</span><span class="sxs-lookup"><span data-stu-id="4b131-110">Notice, when you run the program, that the tasks don’t always finish in the order in which they’re created and awaited.</span></span> <span data-ttu-id="4b131-111">這些工作會在建立後開始執行，而且其中一或多個工作可能會在此方法到達 await 運算式之前就已完成。</span><span class="sxs-lookup"><span data-stu-id="4b131-111">They start to run when they’re created, and one or more of the tasks might finish before the method reaches the await expressions.</span></span>

> [!NOTE]
> <span data-ttu-id="4b131-112">若要完成此專案，您必須在電腦上安裝 Visual Studio 2012 或更高版本以及 .NET Framework 4.5 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="4b131-112">To complete this project, you must have Visual Studio 2012 or higher and the .NET Framework 4.5 or higher installed on your computer.</span></span>

<span data-ttu-id="4b131-113">如需同時啟動多個工作的另一個範例，請參閱[如何：使用 System.threading.tasks.task.whenall 擴充非同步逐步解說（Visual Basic）](how-to-extend-the-async-walkthrough-by-using-task-whenall.md)。</span><span class="sxs-lookup"><span data-stu-id="4b131-113">For another example that starts multiple tasks at the same time, see [How to: Extend the Async Walkthrough by Using Task.WhenAll (Visual Basic)](how-to-extend-the-async-walkthrough-by-using-task-whenall.md).</span></span>

<span data-ttu-id="4b131-114">您可以從[開發人員程式碼範例](https://code.msdn.microsoft.com/Async-Make-Multiple-Web-49adb82e)下載此範例的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4b131-114">You can download the code for this example from [Developer Code Samples](https://code.msdn.microsoft.com/Async-Make-Multiple-Web-49adb82e).</span></span>

### <a name="to-set-up-the-project"></a><span data-ttu-id="4b131-115">若要設定專案</span><span class="sxs-lookup"><span data-stu-id="4b131-115">To set up the project</span></span>

1. <span data-ttu-id="4b131-116">若要設定 WPF 應用程式，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4b131-116">To set up a WPF application, complete the following steps.</span></span> <span data-ttu-id="4b131-117">您可以在[逐步解說：使用 Async 和 Await 存取 Web （Visual Basic）](walkthrough-accessing-the-web-by-using-async-and-await.md)中找到這些步驟的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="4b131-117">You can find detailed instructions for these steps in [Walkthrough: Accessing the Web by Using Async and Await (Visual Basic)](walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span>

    - <span data-ttu-id="4b131-118">建立 WPF 應用程式，其中包含一個文字方塊和一個按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b131-118">Create a WPF application that contains a text box and a button.</span></span> <span data-ttu-id="4b131-119">將按鈕命名為 `startButton`，並將文字方塊命名為 `resultsTextBox`。</span><span class="sxs-lookup"><span data-stu-id="4b131-119">Name the button `startButton`, and name the text box `resultsTextBox`.</span></span>

    - <span data-ttu-id="4b131-120">加入 <xref:System.Net.Http> 的參考。</span><span class="sxs-lookup"><span data-stu-id="4b131-120">Add a reference for <xref:System.Net.Http>.</span></span>

    - <span data-ttu-id="4b131-121">在 Mainwindow.xaml 檔案中，新增的 `Imports` 語句 `System.Net.Http` 。</span><span class="sxs-lookup"><span data-stu-id="4b131-121">In the MainWindow.xaml.vb file, add an `Imports` statement for `System.Net.Http`.</span></span>

### <a name="to-add-the-code"></a><span data-ttu-id="4b131-122">新增程式碼</span><span class="sxs-lookup"><span data-stu-id="4b131-122">To add the code</span></span>

1. <span data-ttu-id="4b131-123">在設計視窗 Mainwindow.xaml 中，按兩下按鈕以 `startButton_Click` 在 mainwindow.xaml 中建立事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="4b131-123">In the design window, MainWindow.xaml, double-click the button to create the `startButton_Click` event handler in MainWindow.xaml.vb.</span></span>

2. <span data-ttu-id="4b131-124">複製下列程式碼，並將它貼入 Mainwindow.xaml 的主體 `startButton_Click` 中。</span><span class="sxs-lookup"><span data-stu-id="4b131-124">Copy the following code, and paste it into the body of `startButton_Click` in MainWindow.xaml.vb.</span></span>

    ```vb
    resultsTextBox.Clear()
    Await CreateMultipleTasksAsync()
    resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."
    ```

     <span data-ttu-id="4b131-125">此程式碼會呼叫非同步方法 `CreateMultipleTasksAsync` 來驅動應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b131-125">The code calls an asynchronous method, `CreateMultipleTasksAsync`, which drives the application.</span></span>

3. <span data-ttu-id="4b131-126">將下列支援方法新增至專案：</span><span class="sxs-lookup"><span data-stu-id="4b131-126">Add the following support methods to the project:</span></span>

    - <span data-ttu-id="4b131-127">`ProcessURLAsync` 使用 <xref:System.Net.Http.HttpClient> 方法，將網站內容下載為位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="4b131-127">`ProcessURLAsync` uses an <xref:System.Net.Http.HttpClient> method to download the contents of a website as a byte array.</span></span> <span data-ttu-id="4b131-128">然後，支援方法 `ProcessURLAsync` 會顯示並傳回陣列的長度。</span><span class="sxs-lookup"><span data-stu-id="4b131-128">The support method, `ProcessURLAsync` then displays and returns the length of the array.</span></span>

    - <span data-ttu-id="4b131-129">`DisplayResults` 會顯示每個 URL 的位元組陣列中的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="4b131-129">`DisplayResults` displays the number of bytes in the byte array for each URL.</span></span> <span data-ttu-id="4b131-130">當每個工作完成下載時，即會顯示此畫面。</span><span class="sxs-lookup"><span data-stu-id="4b131-130">This display shows when each task has finished downloading.</span></span>

     <span data-ttu-id="4b131-131">複製下列方法，並將它們貼入 `startButton_Click` mainwindow.xaml 中的事件處理常式後面。</span><span class="sxs-lookup"><span data-stu-id="4b131-131">Copy the following methods, and paste them after the `startButton_Click` event handler in MainWindow.xaml.vb.</span></span>

    ```vb
    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)

        Dim byteArray = Await client.GetByteArrayAsync(url)
        DisplayResults(url, byteArray)
        Return byteArray.Length
    End Function

    Private Sub DisplayResults(url As String, content As Byte())

        ' Display the length of each website. The string format
        ' is designed to be used with a monospaced font, such as
        ' Lucida Console or Global Monospace.
        Dim bytes = content.Length
        ' Strip off the "https://".
        Dim displayURL = url.Replace("https://", "")
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)
    End Sub
    ```

4. <span data-ttu-id="4b131-132">最後，定義 `CreateMultipleTasksAsync` 方法以執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="4b131-132">Finally, define method `CreateMultipleTasksAsync`, which performs the following steps.</span></span>

    - <span data-ttu-id="4b131-133">方法宣告 `HttpClient` 物件，需要存取 `ProcessURLAsync` 中的方法<xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>。</span><span class="sxs-lookup"><span data-stu-id="4b131-133">The method declares an `HttpClient` object,which you need  to access method <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> in `ProcessURLAsync`.</span></span>

    - <span data-ttu-id="4b131-134">方法會建立並啟動三個 <xref:System.Threading.Tasks.Task%601> 類型的工作，其中 `TResult` 是整數。</span><span class="sxs-lookup"><span data-stu-id="4b131-134">The method creates and starts three tasks of type <xref:System.Threading.Tasks.Task%601>, where `TResult` is an integer.</span></span> <span data-ttu-id="4b131-135">當每個工作完成時，`DisplayResults` 會顯示工作的 URL 和下載內容的長度。</span><span class="sxs-lookup"><span data-stu-id="4b131-135">As each task finishes, `DisplayResults` displays the task's URL and the length of the downloaded contents.</span></span> <span data-ttu-id="4b131-136">因為工作是以非同步方式執行，所以結果出現的順序可能會因宣告的順序而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4b131-136">Because the tasks are running asynchronously, the order in which the results appear might differ from the order in which they were declared.</span></span>

    - <span data-ttu-id="4b131-137">此方法會等候每個工作完成。</span><span class="sxs-lookup"><span data-stu-id="4b131-137">The method awaits the completion of each task.</span></span> <span data-ttu-id="4b131-138">每個 `Await` 運算子會暫停執行 `CreateMultipleTasksAsync`，直到等候的工作完成為止。</span><span class="sxs-lookup"><span data-stu-id="4b131-138">Each `Await` operator suspends execution of `CreateMultipleTasksAsync` until the awaited task is finished.</span></span> <span data-ttu-id="4b131-139">此運算子也會從每個完成的工作擷取透過呼叫 `ProcessURLAsync` 傳回的值。</span><span class="sxs-lookup"><span data-stu-id="4b131-139">The operator also retrieves the return value from the call to `ProcessURLAsync` from each completed task.</span></span>

    - <span data-ttu-id="4b131-140">完成工作並擷取整數值之後，此方法會加總網站的長度並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="4b131-140">When the tasks have been completed and the integer values have been retrieved, the method sums the lengths of the websites and displays the result.</span></span>

     <span data-ttu-id="4b131-141">將下列方法複製並貼到您的方案中。</span><span class="sxs-lookup"><span data-stu-id="4b131-141">Copy the following method, and paste it into your solution.</span></span>

    ```vb
    Private Async Function CreateMultipleTasksAsync() As Task

        ' Declare an HttpClient object, and increase the buffer size. The
        ' default buffer size is 65,536.
        Dim client As HttpClient =
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}

        ' Create and start the tasks. As each task finishes, DisplayResults
        ' displays its length.
        Dim download1 As Task(Of Integer) =
            ProcessURLAsync("https://msdn.microsoft.com", client)
        Dim download2 As Task(Of Integer) =
            ProcessURLAsync("https://msdn.microsoft.com/library/hh156528(VS.110).aspx", client)
        Dim download3 As Task(Of Integer) =
            ProcessURLAsync("https://msdn.microsoft.com/library/67w7t67f.aspx", client)

        ' Await each task.
        Dim length1 As Integer = Await download1
        Dim length2 As Integer = Await download2
        Dim length3 As Integer = Await download3

        Dim total As Integer = length1 + length2 + length3

        ' Display the total count for all of the websites.
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &
                                             "Total bytes returned:  {0}" & vbCrLf, total)
    End Function
    ```

5. <span data-ttu-id="4b131-142">選擇 F5 鍵以執行程式，然後選擇 [開始]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b131-142">Choose the F5 key to run the program, and then choose the **Start** button.</span></span>

     <span data-ttu-id="4b131-143">執行此程式幾次，確認這三個工作不一定會依相同順序完成，而且其完成順序不一定是建立和等候順序。</span><span class="sxs-lookup"><span data-stu-id="4b131-143">Run the program several times to verify that the three tasks don’t always finish in the same order and that the order in which they finish isn't necessarily the order in which they’re created and awaited.</span></span>

## <a name="example"></a><span data-ttu-id="4b131-144">範例</span><span class="sxs-lookup"><span data-stu-id="4b131-144">Example</span></span>

<span data-ttu-id="4b131-145">下列程式碼包含完整的範例。</span><span class="sxs-lookup"><span data-stu-id="4b131-145">The following code contains the full example.</span></span>

```vb
' Add the following Imports statements, and add a reference for System.Net.Http.
Imports System.Net.Http

Class MainWindow

    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click
        resultsTextBox.Clear()
        Await CreateMultipleTasksAsync()
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."
    End Sub

    Private Async Function CreateMultipleTasksAsync() As Task

        ' Declare an HttpClient object, and increase the buffer size. The
        ' default buffer size is 65,536.
        Dim client As HttpClient =
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}

        ' Create and start the tasks. As each task finishes, DisplayResults
        ' displays its length.
        Dim download1 As Task(Of Integer) =
            ProcessURLAsync("https://msdn.microsoft.com", client)
        Dim download2 As Task(Of Integer) =
            ProcessURLAsync("https://msdn.microsoft.com/library/hh156528(VS.110).aspx", client)
        Dim download3 As Task(Of Integer) =
            ProcessURLAsync("https://msdn.microsoft.com/library/67w7t67f.aspx", client)

        ' Await each task.
        Dim length1 As Integer = Await download1
        Dim length2 As Integer = Await download2
        Dim length3 As Integer = Await download3

        Dim total As Integer = length1 + length2 + length3

        ' Display the total count for all of the websites.
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &
                                             "Total bytes returned:  {0}" & vbCrLf, total)
    End Function

    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)

        Dim byteArray = Await client.GetByteArrayAsync(url)
        DisplayResults(url, byteArray)
        Return byteArray.Length
    End Function

    Private Sub DisplayResults(url As String, content As Byte())

        ' Display the length of each website. The string format
        ' is designed to be used with a monospaced font, such as
        ' Lucida Console or Global Monospace.
        Dim bytes = content.Length
        ' Strip off the "https://".
        Dim displayURL = url.Replace("https://", "")
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)
    End Sub
End Class
```

## <a name="see-also"></a><span data-ttu-id="4b131-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4b131-146">See also</span></span>

- [<span data-ttu-id="4b131-147">逐步解說：使用 Async 和 Await 存取 Web (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="4b131-147">Walkthrough: Accessing the Web by Using Async and Await (Visual Basic)</span></span>](walkthrough-accessing-the-web-by-using-async-and-await.md)
- [<span data-ttu-id="4b131-148">使用 Async 和 Await 進行非同步程式設計 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="4b131-148">Asynchronous Programming with Async and Await (Visual Basic)</span></span>](index.md)
- [<span data-ttu-id="4b131-149">如何：使用 Task.WhenAll 擴充非同步逐步解說的內容 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="4b131-149">How to: Extend the Async Walkthrough by Using Task.WhenAll (Visual Basic)</span></span>](how-to-extend-the-async-walkthrough-by-using-task-whenall.md)
