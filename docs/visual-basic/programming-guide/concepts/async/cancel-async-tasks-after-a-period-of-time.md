---
title: 在一段時間後取消非同步工作
ms.date: 07/20/2015
ms.assetid: a48045a3-6a99-42af-b824-af340f0b9a5d
ms.openlocfilehash: 048d4c19d459905ea579ede96c69230e718d55aa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396684"
---
# <a name="cancel-async-tasks-after-a-period-of-time-visual-basic"></a><span data-ttu-id="e4af2-102">在一段時間後取消非同步工作 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e4af2-102">Cancel Async Tasks after a Period of Time (Visual Basic)</span></span>

<span data-ttu-id="e4af2-103">如果不想等候作業完成，則可以使用 <xref:System.Threading.CancellationTokenSource.CancelAfter%2A?displayProperty=nameWithType> 方法，在一段時間之後取消非同步作業。</span><span class="sxs-lookup"><span data-stu-id="e4af2-103">You can cancel an asynchronous operation after a period of time by using the  <xref:System.Threading.CancellationTokenSource.CancelAfter%2A?displayProperty=nameWithType> method if you don't want to wait for the operation to finish.</span></span> <span data-ttu-id="e4af2-104">這個方法排定取消未在 `CancelAfter` 運算式所指定之2期間內完成的任何相關工作。</span><span class="sxs-lookup"><span data-stu-id="e4af2-104">This method schedules the cancellation of any associated tasks that aren’t complete within the period of time that’s designated by the `CancelAfter` expression.</span></span>

<span data-ttu-id="e4af2-105">這個範例會將新增至 [[取消非同步工作] 或 [工作清單（Visual Basic）](cancel-an-async-task-or-a-list-of-tasks.md) ] 中所開發的程式碼，以下載網站清單並顯示每一項的內容長度。</span><span class="sxs-lookup"><span data-stu-id="e4af2-105">This example adds to the code that’s developed in [Cancel an Async Task or a List of Tasks (Visual Basic)](cancel-an-async-task-or-a-list-of-tasks.md) to download a list of websites and to display the length of the contents of each one.</span></span>

> [!NOTE]
> <span data-ttu-id="e4af2-106">若要執行範例，您必須在電腦上安裝 Visual Studio 2012 或更新版本，以及 .NET Framework 4.5 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e4af2-106">To run the examples, you must have Visual Studio 2012 or later and the .NET Framework 4.5 or later installed on your computer.</span></span>

## <a name="downloading-the-example"></a><span data-ttu-id="e4af2-107">下載範例</span><span class="sxs-lookup"><span data-stu-id="e4af2-107">Downloading the Example</span></span>

<span data-ttu-id="e4af2-108">您可以從 [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea) (非同步範例：微調應用程式) 下載完整 Windows Presentation Foundation (WPF) 專案，然後遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="e4af2-108">You can download the complete Windows Presentation Foundation (WPF) project from [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea) and then follow these steps.</span></span>

1. <span data-ttu-id="e4af2-109">解壓縮您下載的檔案，然後啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e4af2-109">Decompress the file that you downloaded, and then start Visual Studio.</span></span>

2. <span data-ttu-id="e4af2-110">在功能表列上，依序選擇 [檔案] \*\*\*\*、[開啟舊檔] \*\*\*\* 及 [專案/方案] \*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="e4af2-110">On the menu bar, choose **File**, **Open**, **Project/Solution**.</span></span>

3. <span data-ttu-id="e4af2-111">在 [**開啟專案**] 對話方塊中，開啟保存解壓縮之範例程式碼的資料夾，然後開啟 AsyncFineTuningVB 的方案（.sln）檔案。</span><span class="sxs-lookup"><span data-stu-id="e4af2-111">In the **Open Project** dialog box, open the folder that holds the sample code that you decompressed, and then open the solution (.sln) file for AsyncFineTuningVB.</span></span>

4. <span data-ttu-id="e4af2-112">在方案總管\*\*\*\* 中，開啟 **CancelAfterTime** 專案的捷徑功能表，然後選擇 [設定為啟始專案]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="e4af2-112">In **Solution Explorer**, open the shortcut menu for the **CancelAfterTime** project, and then choose **Set as StartUp Project**.</span></span>

5. <span data-ttu-id="e4af2-113">選擇 F5 鍵以執行專案。</span><span class="sxs-lookup"><span data-stu-id="e4af2-113">Choose the F5 key to run the project.</span></span>

     <span data-ttu-id="e4af2-114">選擇 CTRL+F5 鍵以執行專案，而不進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="e4af2-114">Choose the Ctrl+F5 keys to run the project without debugging it.</span></span>

6. <span data-ttu-id="e4af2-115">執行程式數次，確認輸出可能會顯示所有網站、沒有網站或某些網站的輸出。</span><span class="sxs-lookup"><span data-stu-id="e4af2-115">Run the program several times to verify that the output might show output for all websites, no websites, or some web sites.</span></span>

 <span data-ttu-id="e4af2-116">如果您不想要下載專案，您可以參閱本主題結尾的 Mainwindow.xaml。</span><span class="sxs-lookup"><span data-stu-id="e4af2-116">If you don't want to download the project, you can review the MainWindow.xaml.vb file at the end of this topic.</span></span>

## <a name="building-the-example"></a><span data-ttu-id="e4af2-117">建置範例</span><span class="sxs-lookup"><span data-stu-id="e4af2-117">Building the Example</span></span>

<span data-ttu-id="e4af2-118">本主題中的範例會新增至取消一項非同步工作[或工作清單（Visual Basic）](cancel-an-async-task-or-a-list-of-tasks.md)中所開發的專案，以取消工作清單。</span><span class="sxs-lookup"><span data-stu-id="e4af2-118">The example in this topic adds to the project that's developed in [Cancel an Async Task or a List of Tasks (Visual Basic)](cancel-an-async-task-or-a-list-of-tasks.md) to cancel a list of tasks.</span></span> <span data-ttu-id="e4af2-119">雖然未明確地使用 [取消]\*\*\*\* 按鈕，但是此範例會使用相同的 UI。</span><span class="sxs-lookup"><span data-stu-id="e4af2-119">The example uses the same UI, although the **Cancel** button isn’t used explicitly.</span></span>

<span data-ttu-id="e4af2-120">若要自行逐步建置範例，請遵循＜下載範例＞一節中的指示，但選擇 [CancelAListOfTasks]\*\*\*\* 作為 [啟始專案]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="e4af2-120">To build the example yourself, step by step, follow the instructions in the "Downloading the Example" section, but choose **CancelAListOfTasks** as the **StartUp Project**.</span></span> <span data-ttu-id="e4af2-121">將本主題中的變更新增至該專案。</span><span class="sxs-lookup"><span data-stu-id="e4af2-121">Add the changes in this topic to that project.</span></span>

<span data-ttu-id="e4af2-122">若要指定將工作標記為取消之前的最長時間，請將 `CancelAfter` 呼叫新增至 `startButton_Click`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="e4af2-122">To specify a maximum time before the tasks are marked as canceled, add a call to `CancelAfter` to `startButton_Click`, as the following example shows.</span></span> <span data-ttu-id="e4af2-123">新增的項目會以星號標記。</span><span class="sxs-lookup"><span data-stu-id="e4af2-123">The addition is marked with asterisks.</span></span>

```vb
Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)

    ' Instantiate the CancellationTokenSource.
    cts = New CancellationTokenSource()

    resultsTextBox.Clear()

    Try
        ' ***Set up the CancellationTokenSource to cancel after 2.5 seconds. (You
        ' can adjust the time.)
        cts.CancelAfter(2500)

        Await AccessTheWebAsync(cts.Token)
        resultsTextBox.Text &= vbCrLf & "Downloads complete."

    Catch ex As OperationCanceledException
        resultsTextBox.Text &= vbCrLf & "Downloads canceled." & vbCrLf

    Catch ex As Exception
        resultsTextBox.Text &= vbCrLf & "Downloads failed." & vbCrLf
    End Try

    ' Set the CancellationTokenSource to Nothing when the download is complete.
    cts = Nothing
End Sub
```

<span data-ttu-id="e4af2-124">執行程式數次，確認輸出可能會顯示所有網站、沒有網站或某些網站的輸出。</span><span class="sxs-lookup"><span data-stu-id="e4af2-124">Run the program several times to verify that the output might show output for all websites, no websites, or some web sites.</span></span> <span data-ttu-id="e4af2-125">下列輸出是一個範例：</span><span class="sxs-lookup"><span data-stu-id="e4af2-125">The following output is a sample:</span></span>

```console
Length of the downloaded string: 35990.

Length of the downloaded string: 407399.

Length of the downloaded string: 226091.

Downloads canceled.
```

## <a name="complete-example"></a><span data-ttu-id="e4af2-126">完整範例</span><span class="sxs-lookup"><span data-stu-id="e4af2-126">Complete Example</span></span>

<span data-ttu-id="e4af2-127">下列程式碼是範例的 Mainwindow.xaml 檔案的完整文字。</span><span class="sxs-lookup"><span data-stu-id="e4af2-127">The following code is the complete text of the MainWindow.xaml.vb file for the example.</span></span> <span data-ttu-id="e4af2-128">星號會標記已針對此範例新增的項目。</span><span class="sxs-lookup"><span data-stu-id="e4af2-128">Asterisks mark the elements that were added for this example.</span></span>

<span data-ttu-id="e4af2-129">請注意，您必須新增 <xref:System.Net.Http> 的參考。</span><span class="sxs-lookup"><span data-stu-id="e4af2-129">Notice that you must add a reference for <xref:System.Net.Http>.</span></span>

<span data-ttu-id="e4af2-130">您可以從 [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea) (非同步範例：微調應用程式) 下載專案。</span><span class="sxs-lookup"><span data-stu-id="e4af2-130">You can download the project from [Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea).</span></span>

```vb
' Add an Imports directive and a reference for System.Net.Http.
Imports System.Net.Http

' Add the following Imports directive for System.Threading.
Imports System.Threading

Class MainWindow

    ' Declare a System.Threading.CancellationTokenSource.
    Dim cts As CancellationTokenSource

    Private Async Sub startButton_Click(sender As Object, e As RoutedEventArgs)

        ' Instantiate the CancellationTokenSource.
        cts = New CancellationTokenSource()

        resultsTextBox.Clear()

        Try
            ' ***Set up the CancellationTokenSource to cancel after 2.5 seconds. (You
            ' can adjust the time.)
            cts.CancelAfter(2500)

            Await AccessTheWebAsync(cts.Token)
            resultsTextBox.Text &= vbCrLf & "Downloads complete."

        Catch ex As OperationCanceledException
            resultsTextBox.Text &= vbCrLf & "Downloads canceled." & vbCrLf

        Catch ex As Exception
            resultsTextBox.Text &= vbCrLf & "Downloads failed." & vbCrLf
        End Try

        ' Set the CancellationTokenSource to Nothing when the download is complete.
        cts = Nothing
    End Sub

    ' You can still include a Cancel button if you want to.
    Private Sub cancelButton_Click(sender As Object, e As RoutedEventArgs)

        If cts IsNot Nothing Then
            cts.Cancel()
        End If
    End Sub

    ' Provide a parameter for the CancellationToken.
    ' Change the return type to Task because the method has no return statement.
    Async Function AccessTheWebAsync(ct As CancellationToken) As Task

        Dim client As HttpClient = New HttpClient()

        ' Call SetUpURLList to make a list of web addresses.
        Dim urlList As List(Of String) = SetUpURLList()

        ' Process each element in the list of web addresses.
        For Each url In urlList
            ' GetAsync returns a Task(Of HttpResponseMessage).
            ' Argument ct carries the message if the Cancel button is chosen.
            ' Note that the Cancel button can cancel all remaining downloads.
            Dim response As HttpResponseMessage = Await client.GetAsync(url, ct)

            ' Retrieve the website contents from the HttpResponseMessage.
            Dim urlContents As Byte() = Await response.Content.ReadAsByteArrayAsync()

            resultsTextBox.Text &=
                vbCrLf & $"Length of the downloaded string: {urlContents.Length}." & vbCrLf
        Next
    End Function

    ' Add a method that creates a list of web addresses.
    Private Function SetUpURLList() As List(Of String)

        Dim urls = New List(Of String) From
            {
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            }
        Return urls
    End Function

End Class

' Sample output:

' Length of the downloaded string: 35990.

' Length of the downloaded string: 407399.

' Length of the downloaded string: 226091.

' Downloads canceled.
```

## <a name="see-also"></a><span data-ttu-id="e4af2-131">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e4af2-131">See also</span></span>

- [<span data-ttu-id="e4af2-132">使用 Async 和 Await 進行非同步程式設計 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e4af2-132">Asynchronous Programming with Async and Await (Visual Basic)</span></span>](index.md)
- [<span data-ttu-id="e4af2-133">逐步解說：使用 Async 和 Await 存取 Web (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e4af2-133">Walkthrough: Accessing the Web by Using Async and Await (Visual Basic)</span></span>](walkthrough-accessing-the-web-by-using-async-and-await.md)
- [<span data-ttu-id="e4af2-134">取消一項非同步工作或工作清單 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e4af2-134">Cancel an Async Task or a List of Tasks (Visual Basic)</span></span>](cancel-an-async-task-or-a-list-of-tasks.md)
- [<span data-ttu-id="e4af2-135">微調非同步應用程式 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="e4af2-135">Fine-Tuning Your Async Application (Visual Basic)</span></span>](fine-tuning-your-async-application.md)
- <span data-ttu-id="e4af2-136">[Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea) (非同步範例：微調應用程式)</span><span class="sxs-lookup"><span data-stu-id="e4af2-136">[Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea)</span></span>
