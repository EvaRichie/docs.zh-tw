---
title: '如何使用 System.threading.tasks.task.whenall 擴充非同步逐步解說（c #）'
description: '瞭解如何使用 System.threading.tasks.task.whenall 來改善 c # 中非同步方案的效能。 這個方法會以非同步方式等候多個非同步作業。'
ms.date: 07/20/2015
ms.assetid: f6927ef2-dc6c-43f8-bc82-bbeac42de423
ms.openlocfilehash: 275f4aeca854f8938642dbea40bf7fd9dc5362d9
ms.sourcegitcommit: 40de8df14289e1e05b40d6e5c1daabd3c286d70c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86925211"
---
# <a name="how-to-extend-the-async-walkthrough-by-using-taskwhenall-c"></a><span data-ttu-id="cbed9-104">如何使用 System.threading.tasks.task.whenall 擴充非同步逐步解說（c #）</span><span class="sxs-lookup"><span data-stu-id="cbed9-104">How to extend the async walkthrough by using Task.WhenAll (C#)</span></span>

<span data-ttu-id="cbed9-105">您可以使用 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 方法，來提升[逐步解說：使用 Async 和 Await 存取 Web (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md) 中非同步方案的效能。</span><span class="sxs-lookup"><span data-stu-id="cbed9-105">You can improve the performance of the async solution in [Walkthrough: Accessing the Web by Using async and await (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md) by using the <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="cbed9-106">此方法會以非同步方式等候多個非同步作業進行，這些作業是以工作集合來表示。</span><span class="sxs-lookup"><span data-stu-id="cbed9-106">This method asynchronously awaits multiple asynchronous operations, which are represented as a collection of tasks.</span></span>

<span data-ttu-id="cbed9-107">您在此逐步解說中可能已注意到網站下載的速度各自不同。</span><span class="sxs-lookup"><span data-stu-id="cbed9-107">You might have noticed in the walkthrough that the websites download at different rates.</span></span> <span data-ttu-id="cbed9-108">有時其中一個網站的速度很慢，而導致所有其餘下載延後執行。</span><span class="sxs-lookup"><span data-stu-id="cbed9-108">Sometimes one of the websites is very slow, which delays all the remaining downloads.</span></span> <span data-ttu-id="cbed9-109">當您執行在此逐步解說中建立的非同步方案時，如果不想要等候，您可以輕鬆地結束程式；但更好的做法是同時啟動所有下載，並讓較快的下載繼續執行而不等候延遲的下載。</span><span class="sxs-lookup"><span data-stu-id="cbed9-109">When you run the asynchronous solutions that you build in the walkthrough, you can end the program easily if you don't want to wait, but a better option would be to start all the downloads at the same time and let faster downloads continue without waiting for the one that’s delayed.</span></span>

<span data-ttu-id="cbed9-110">您可以將 `Task.WhenAll` 方法套用至工作集合。</span><span class="sxs-lookup"><span data-stu-id="cbed9-110">You apply the `Task.WhenAll` method to a collection of tasks.</span></span> <span data-ttu-id="cbed9-111">套用 `WhenAll` 會傳回未完成的單一工作，直到集合中的所有工作都完成為止。</span><span class="sxs-lookup"><span data-stu-id="cbed9-111">The application of `WhenAll` returns a single task that isn’t complete until every task in the collection is completed.</span></span> <span data-ttu-id="cbed9-112">工作似乎會平行執行，但不會建立其他任何執行緒。</span><span class="sxs-lookup"><span data-stu-id="cbed9-112">The tasks appear to run in parallel, but no additional threads are created.</span></span> <span data-ttu-id="cbed9-113">工作可以依任何順序完成。</span><span class="sxs-lookup"><span data-stu-id="cbed9-113">The tasks can complete in any order.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbed9-114">下列程序描述在[逐步解說：使用 Async 和 Await 存取 Web (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md) 中開發之非同步應用程式的擴充。</span><span class="sxs-lookup"><span data-stu-id="cbed9-114">The following procedures describe extensions to the async applications that are developed in [Walkthrough: Accessing the Web by Using async and await (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span> <span data-ttu-id="cbed9-115">您可以藉由完成此逐步解說，或從[開發人員程式碼範例](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)下載程式碼，來開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbed9-115">You can develop the applications by either completing the walkthrough or downloading the code from [Developer Code Samples](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f).</span></span>
>
> <span data-ttu-id="cbed9-116">若要執行範例，您必須在電腦上安裝 Visual Studio 2012 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="cbed9-116">To run the example, you must have Visual Studio 2012 or later installed on your computer.</span></span>

### <a name="to-add-taskwhenall-to-your-geturlcontentsasync-solution"></a><span data-ttu-id="cbed9-117">將 Task.WhenAll 新增至您的 GetURLContentsAsync 方案</span><span class="sxs-lookup"><span data-stu-id="cbed9-117">To add Task.WhenAll to your GetURLContentsAsync solution</span></span>

1. <span data-ttu-id="cbed9-118">將 `ProcessURLAsync` 方法新增至在[逐步解說：使用 Async 和 Await 存取 Web (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md) 中開發的第一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbed9-118">Add the `ProcessURLAsync` method to the first application that's developed in [Walkthrough: Accessing the Web by Using async and await (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span>

    - <span data-ttu-id="cbed9-119">如果您已從[開發人員程式碼範例](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)下載程式碼，請開啟 AsyncWalkthrough 專案，然後將 `ProcessURLAsync` 新增至 MainWindow.xaml.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbed9-119">If you downloaded the code from  [Developer Code Samples](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f), open the AsyncWalkthrough project, and then add `ProcessURLAsync` to the MainWindow.xaml.cs file.</span></span>

    - <span data-ttu-id="cbed9-120">如果您藉由完成此逐步解說來開發程式碼，請將 `ProcessURLAsync` 新增至包含 `GetURLContentsAsync` 方法的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbed9-120">If you developed the code by completing the walkthrough, add `ProcessURLAsync` to the application that includes the `GetURLContentsAsync` method.</span></span> <span data-ttu-id="cbed9-121">此應用程式的 MainWindow.xaml.cs 檔案是＜逐步解說中完整的程式碼範例＞一節的第一個範例。</span><span class="sxs-lookup"><span data-stu-id="cbed9-121">The MainWindow.xaml.cs file for this application is the first example in the "Complete Code Examples from the Walkthrough" section.</span></span>

    <span data-ttu-id="cbed9-122">`ProcessURLAsync` 方法會合併原始逐步解說中 `SumPageSizesAsync` 之 `foreach` 迴圈主體內的動作。</span><span class="sxs-lookup"><span data-stu-id="cbed9-122">The `ProcessURLAsync` method consolidates the actions in the body of the `foreach` loop in `SumPageSizesAsync` in the original walkthrough.</span></span> <span data-ttu-id="cbed9-123">此方法會以非同步方式將指定網站的內容下載為位元組陣列，然後顯示並傳回位元組陣列的長度。</span><span class="sxs-lookup"><span data-stu-id="cbed9-123">The method asynchronously downloads the contents of a specified website as a byte array, and then displays and returns the length of the byte array.</span></span>

    ```csharp
    private async Task<int> ProcessURLAsync(string url)
    {
        var byteArray = await GetURLContentsAsync(url);
        DisplayResults(url, byteArray);
        return byteArray.Length;
    }
    ```

2. <span data-ttu-id="cbed9-124">將 `SumPageSizesAsync` 中的 `foreach` 迴圈註解化或刪除，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="cbed9-124">Comment out or delete the `foreach` loop in `SumPageSizesAsync`, as the following code shows.</span></span>

    ```csharp
    //var total = 0;
    //foreach (var url in urlList)
    //{
    //    byte[] urlContents = await GetURLContentsAsync(url);

    //    // The previous line abbreviates the following two assignment statements.
    //    // GetURLContentsAsync returns a Task<T>. At completion, the task
    //    // produces a byte array.
    //    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);
    //    //byte[] urlContents = await getContentsTask;

    //    DisplayResults(url, urlContents);

    //    // Update the total.
    //    total += urlContents.Length;
    //}
    ```

3. <span data-ttu-id="cbed9-125">建立工作集合。</span><span class="sxs-lookup"><span data-stu-id="cbed9-125">Create a collection of tasks.</span></span> <span data-ttu-id="cbed9-126">下列程式碼定義一個[查詢](../linq/index.md)，當 <xref:System.Linq.Enumerable.ToArray%2A> 方法執行此查詢時，會建立工作集合以下載每個網站的內容。</span><span class="sxs-lookup"><span data-stu-id="cbed9-126">The following code defines a [query](../linq/index.md) that, when executed by the <xref:System.Linq.Enumerable.ToArray%2A> method, creates a collection of tasks that download the contents of each website.</span></span> <span data-ttu-id="cbed9-127">工作會在評估查詢之後啟動。</span><span class="sxs-lookup"><span data-stu-id="cbed9-127">The tasks are started when the query is evaluated.</span></span>

    <span data-ttu-id="cbed9-128">將下列程式碼新增至 `urlList` 宣告後面的 `SumPageSizesAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="cbed9-128">Add the following code to method `SumPageSizesAsync` after the declaration of `urlList`.</span></span>

    ```csharp
    // Create a query.
    IEnumerable<Task<int>> downloadTasksQuery =
        from url in urlList select ProcessURLAsync(url);

    // Use ToArray to execute the query and start the download tasks.
    Task<int>[] downloadTasks = downloadTasksQuery.ToArray();
    ```

4. <span data-ttu-id="cbed9-129">將 `Task.WhenAll` 套用至工作集合 `downloadTasks`。</span><span class="sxs-lookup"><span data-stu-id="cbed9-129">Apply `Task.WhenAll` to the collection of tasks, `downloadTasks`.</span></span> <span data-ttu-id="cbed9-130">`Task.WhenAll` 會傳回當工作集合中所有工作完成後才會完成的單一工作。</span><span class="sxs-lookup"><span data-stu-id="cbed9-130">`Task.WhenAll` returns a single task that finishes when all the tasks in the collection of tasks have completed.</span></span>

    <span data-ttu-id="cbed9-131">在下列範例中，`await` 運算式會等候 `WhenAll` 傳回的單一工作完成。</span><span class="sxs-lookup"><span data-stu-id="cbed9-131">In the following example, the `await` expression awaits the completion of the single task that `WhenAll` returns.</span></span> <span data-ttu-id="cbed9-132">此運算式會評估為整數陣列，其中每個整數都是所下載網站的長度。</span><span class="sxs-lookup"><span data-stu-id="cbed9-132">The expression evaluates to an array of integers, where each integer is the length of a downloaded website.</span></span> <span data-ttu-id="cbed9-133">將下列程式碼新增至 `SumPageSizesAsync`，就在您於上一個步驟中新增的程式碼之後。</span><span class="sxs-lookup"><span data-stu-id="cbed9-133">Add the following code to `SumPageSizesAsync`, just after the code that you added in the previous step.</span></span>

    ```csharp
    // Await the completion of all the running tasks.
    int[] lengths = await Task.WhenAll(downloadTasks);

    //// The previous line is equivalent to the following two statements.
    //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);
    //int[] lengths = await whenAllTask;
    ```

5. <span data-ttu-id="cbed9-134">最後，使用 <xref:System.Linq.Enumerable.Sum%2A> 方法來計算所有網站的長度總和。</span><span class="sxs-lookup"><span data-stu-id="cbed9-134">Finally, use the <xref:System.Linq.Enumerable.Sum%2A> method to calculate the sum of the lengths of all the websites.</span></span> <span data-ttu-id="cbed9-135">將下列程式碼行新增至 `SumPageSizesAsync`。</span><span class="sxs-lookup"><span data-stu-id="cbed9-135">Add the following line to `SumPageSizesAsync`.</span></span>

    ```csharp
    int total = lengths.Sum();
    ```

### <a name="to-add-taskwhenall-to-the-httpclientgetbytearrayasync-solution"></a><span data-ttu-id="cbed9-136">將 Task.WhenAll 新增至 HttpClient.GetByteArrayAsync 方案</span><span class="sxs-lookup"><span data-stu-id="cbed9-136">To add Task.WhenAll to the HttpClient.GetByteArrayAsync solution</span></span>

1. <span data-ttu-id="cbed9-137">將下列版本的 `ProcessURLAsync` 新增至在[逐步解說：使用 Async 和 Await 存取 Web (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md) 中開發的第二個應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbed9-137">Add the following version of `ProcessURLAsync` to the second application that's developed in [Walkthrough: Accessing the Web by Using async and await (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span>

    - <span data-ttu-id="cbed9-138">如果您已從[開發人員程式碼範例](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f)下載程式碼，請開啟 AsyncWalkthrough_HttpClient 專案，然後將 `ProcessURLAsync` 新增至 MainWindow.xaml.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbed9-138">If you downloaded the code from [Developer Code Samples](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f), open the AsyncWalkthrough_HttpClient project, and then add `ProcessURLAsync` to the MainWindow.xaml.cs file.</span></span>

    - <span data-ttu-id="cbed9-139">如果您藉由完成此逐步解說來開發程式碼，請將 `ProcessURLAsync` 新增至使用 `HttpClient.GetByteArrayAsync` 方法的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbed9-139">If you developed the code by completing the walkthrough, add `ProcessURLAsync` to the application that uses the `HttpClient.GetByteArrayAsync` method.</span></span> <span data-ttu-id="cbed9-140">此應用程式的 MainWindow.xaml.cs 檔案是＜逐步解說中完整的程式碼範例＞一節的第二個範例。</span><span class="sxs-lookup"><span data-stu-id="cbed9-140">The MainWindow.xaml.cs file for this application is the second example in the "Complete Code Examples from the Walkthrough" section.</span></span>

    <span data-ttu-id="cbed9-141">`ProcessURLAsync` 方法會合併原始逐步解說中 `SumPageSizesAsync` 之 `foreach` 迴圈主體內的動作。</span><span class="sxs-lookup"><span data-stu-id="cbed9-141">The `ProcessURLAsync` method consolidates the actions in the body of the `foreach` loop in `SumPageSizesAsync` in the original walkthrough.</span></span> <span data-ttu-id="cbed9-142">此方法會以非同步方式將指定網站的內容下載為位元組陣列，然後顯示並傳回位元組陣列的長度。</span><span class="sxs-lookup"><span data-stu-id="cbed9-142">The method asynchronously downloads the contents of a specified website as a byte array, and then displays and returns the length of the byte array.</span></span>

    <span data-ttu-id="cbed9-143">其與上一個步驟中 `ProcessURLAsync` 方法的唯一差別，在於使用了 <xref:System.Net.Http.HttpClient> 執行個體 `client`。</span><span class="sxs-lookup"><span data-stu-id="cbed9-143">The only difference from the `ProcessURLAsync` method in the previous procedure is the use of the <xref:System.Net.Http.HttpClient> instance, `client`.</span></span>

    ```csharp
    async Task<int> ProcessURLAsync(string url, HttpClient client)
    {
        byte[] byteArray = await client.GetByteArrayAsync(url);
        DisplayResults(url, byteArray);
        return byteArray.Length;
    }
    ```

2. <span data-ttu-id="cbed9-144">將 `SumPageSizesAsync` 中的 `For Each` 或 `foreach` 迴圈註解化或刪除，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="cbed9-144">Comment out or delete the `For Each` or `foreach` loop in `SumPageSizesAsync`, as the following code shows.</span></span>

    ```csharp
    //var total = 0;
    //foreach (var url in urlList)
    //{
    //    // GetByteArrayAsync returns a Task<T>. At completion, the task
    //    // produces a byte array.
    //    byte[] urlContent = await client.GetByteArrayAsync(url);

    //    // The previous line abbreviates the following two assignment
    //    // statements.
    //    Task<byte[]> getContentTask = client.GetByteArrayAsync(url);
    //    byte[] urlContent = await getContentTask;

    //    DisplayResults(url, urlContent);

    //    // Update the total.
    //    total += urlContent.Length;
    //}
    ```

3. <span data-ttu-id="cbed9-145">定義一個[查詢](../linq/index.md)，當 <xref:System.Linq.Enumerable.ToArray%2A> 方法執行此查詢時，會建立工作集合以下載每個網站的內容。</span><span class="sxs-lookup"><span data-stu-id="cbed9-145">Define a [query](../linq/index.md) that, when executed by the <xref:System.Linq.Enumerable.ToArray%2A> method, creates a collection of tasks that download the contents of each website.</span></span> <span data-ttu-id="cbed9-146">工作會在評估查詢之後啟動。</span><span class="sxs-lookup"><span data-stu-id="cbed9-146">The tasks are started when the query is evaluated.</span></span>

    <span data-ttu-id="cbed9-147">將下列程式碼新增至 `client` 和 `urlList` 宣告後面的 `SumPageSizesAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="cbed9-147">Add the following code to method `SumPageSizesAsync` after the declaration of `client` and `urlList`.</span></span>

    ```csharp
    // Create a query.
    IEnumerable<Task<int>> downloadTasksQuery =
        from url in urlList select ProcessURLAsync(url, client);

    // Use ToArray to execute the query and start the download tasks.
    Task<int>[] downloadTasks = downloadTasksQuery.ToArray();
    ```

4. <span data-ttu-id="cbed9-148">接下來，將 `Task.WhenAll` 套用至工作集合 `downloadTasks`。</span><span class="sxs-lookup"><span data-stu-id="cbed9-148">Next, apply `Task.WhenAll` to the collection of tasks, `downloadTasks`.</span></span> <span data-ttu-id="cbed9-149">`Task.WhenAll` 會傳回當工作集合中所有工作完成後才會完成的單一工作。</span><span class="sxs-lookup"><span data-stu-id="cbed9-149">`Task.WhenAll` returns a single task that finishes when all the tasks in the collection of tasks have completed.</span></span>

    <span data-ttu-id="cbed9-150">在下列範例中，`await` 運算式會等候 `WhenAll` 傳回的單一工作完成。</span><span class="sxs-lookup"><span data-stu-id="cbed9-150">In the following example, the `await` expression awaits the completion of the single task that `WhenAll` returns.</span></span> <span data-ttu-id="cbed9-151">完成時，`await` 運算式會評估為整數陣列，其中每個整數都是所下載網站的長度。</span><span class="sxs-lookup"><span data-stu-id="cbed9-151">When complete, the `await` expression evaluates to an array of integers, where each integer is the length of a downloaded website.</span></span> <span data-ttu-id="cbed9-152">將下列程式碼新增至 `SumPageSizesAsync`，就在您於上一個步驟中新增的程式碼之後。</span><span class="sxs-lookup"><span data-stu-id="cbed9-152">Add the following code to `SumPageSizesAsync`, just after the code that you added in the previous step.</span></span>

    ```csharp
    // Await the completion of all the running tasks.
    int[] lengths = await Task.WhenAll(downloadTasks);

    //// The previous line is equivalent to the following two statements.
    //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);
    //int[] lengths = await whenAllTask;
    ```

5. <span data-ttu-id="cbed9-153">最後，使用 <xref:System.Linq.Enumerable.Sum%2A> 方法取得所有網站的長度總和。</span><span class="sxs-lookup"><span data-stu-id="cbed9-153">Finally, use the <xref:System.Linq.Enumerable.Sum%2A> method to get the sum of the lengths of all the websites.</span></span> <span data-ttu-id="cbed9-154">將下列程式碼行新增至 `SumPageSizesAsync`。</span><span class="sxs-lookup"><span data-stu-id="cbed9-154">Add the following line to `SumPageSizesAsync`.</span></span>

    ```csharp
    int total = lengths.Sum();
    ```

### <a name="to-test-the-taskwhenall-solutions"></a><span data-ttu-id="cbed9-155">測試 Task.WhenAll 方案</span><span class="sxs-lookup"><span data-stu-id="cbed9-155">To test the Task.WhenAll solutions</span></span>

- <span data-ttu-id="cbed9-156">針對任一方案，選擇 F5 鍵以執行程式，然後選擇 [開始]\*\*\*\* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cbed9-156">For either solution, choose the F5 key to run the program, and then choose the **Start** button.</span></span> <span data-ttu-id="cbed9-157">輸出應類似於[逐步解說：使用 Async 和 Await 存取 Web (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md) 中的非同步方案輸出。</span><span class="sxs-lookup"><span data-stu-id="cbed9-157">The output should resemble the output from the async solutions in [Walkthrough: Accessing the Web by Using async and await (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md).</span></span> <span data-ttu-id="cbed9-158">不過請注意，網站每次出現的順序都不同。</span><span class="sxs-lookup"><span data-stu-id="cbed9-158">However, notice that the websites appear in a different order each time.</span></span>

## <a name="example"></a><span data-ttu-id="cbed9-159">範例</span><span class="sxs-lookup"><span data-stu-id="cbed9-159">Example</span></span>

<span data-ttu-id="cbed9-160">下列程式碼顯示專案擴充，其使用 `GetURLContentsAsync` 方法從 Web 下載內容。</span><span class="sxs-lookup"><span data-stu-id="cbed9-160">The following code shows the extensions to the project that uses the `GetURLContentsAsync` method to download content from the web.</span></span>

```csharp
// Add the following using directives, and add a reference for System.Net.Http.
using System.Net.Http;
using System.IO;
using System.Net;

namespace AsyncExampleWPF_WhenAll
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private async void startButton_Click(object sender, RoutedEventArgs e)
        {
            resultsTextBox.Clear();

            // Two-step async call.
            Task sumTask = SumPageSizesAsync();
            await sumTask;

            // One-step async call.
            //await SumPageSizesAsync();

            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";
        }

        private async Task SumPageSizesAsync()
        {
            // Make a list of web addresses.
            List<string> urlList = SetUpURLList();

            // Create a query.
            IEnumerable<Task<int>> downloadTasksQuery =
                from url in urlList select ProcessURLAsync(url);

            // Use ToArray to execute the query and start the download tasks.
            Task<int>[] downloadTasks = downloadTasksQuery.ToArray();

            // You can do other work here before awaiting.

            // Await the completion of all the running tasks.
            int[] lengths = await Task.WhenAll(downloadTasks);

            //// The previous line is equivalent to the following two statements.
            //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);
            //int[] lengths = await whenAllTask;

            int total = lengths.Sum();

            //var total = 0;
            //foreach (var url in urlList)
            //{
            //    byte[] urlContents = await GetURLContentsAsync(url);

            //    // The previous line abbreviates the following two assignment statements.
            //    // GetURLContentsAsync returns a Task<T>. At completion, the task
            //    // produces a byte array.
            //    //Task<byte[]> getContentsTask = GetURLContentsAsync(url);
            //    //byte[] urlContents = await getContentsTask;

            //    DisplayResults(url, urlContents);

            //    // Update the total.
            //    total += urlContents.Length;
            //}

            // Display the total count for all of the websites.
            resultsTextBox.Text +=
                $"\r\n\r\nTotal bytes returned:  {total}\r\n";
        }

        private List<string> SetUpURLList()
        {
            List<string> urls = new List<string>
            {
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/windows/apps/br211380.aspx",
                "https://msdn.microsoft.com/library/hh290136.aspx",
                "https://msdn.microsoft.com/library/ee256749.aspx",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            };
            return urls;
        }

        // The actions from the foreach loop are moved to this async method.
        private async Task<int> ProcessURLAsync(string url)
        {
            var byteArray = await GetURLContentsAsync(url);
            DisplayResults(url, byteArray);
            return byteArray.Length;
        }

        private async Task<byte[]> GetURLContentsAsync(string url)
        {
            // The downloaded resource ends up in the variable named content.
            var content = new MemoryStream();

            // Initialize an HttpWebRequest for the current URL.
            var webReq = (HttpWebRequest)WebRequest.Create(url);

            // Send the request to the Internet resource and wait for
            // the response.
            using (WebResponse response = await webReq.GetResponseAsync())
            {
                // Get the data stream that is associated with the specified url.
                using (Stream responseStream = response.GetResponseStream())
                {
                    await responseStream.CopyToAsync(content);
                }
            }

            // Return the result as a byte array.
            return content.ToArray();

        }

        private void DisplayResults(string url, byte[] content)
        {
            // Display the length of each website. The string format
            // is designed to be used with a monospaced font, such as
            // Lucida Console or Global Monospace.
            var bytes = content.Length;
            // Strip off the "https://".
            var displayURL = url.Replace("https://", "");
            resultsTextBox.Text += $"\n{displayURL,-58} {bytes,8}";
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="cbed9-161">範例</span><span class="sxs-lookup"><span data-stu-id="cbed9-161">Example</span></span>

<span data-ttu-id="cbed9-162">下列程式碼顯示專案擴充，其使用 `HttpClient.GetByteArrayAsync` 方法從 Web 下載內容。</span><span class="sxs-lookup"><span data-stu-id="cbed9-162">The following code shows the extensions to the project that uses method `HttpClient.GetByteArrayAsync` to download content from the web.</span></span>

```csharp
// Add the following using directives, and add a reference for System.Net.Http.
using System.Net.Http;
using System.IO;
using System.Net;

namespace AsyncExampleWPF_HttpClient_WhenAll
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private async void startButton_Click(object sender, RoutedEventArgs e)
        {
            resultsTextBox.Clear();

            // One-step async call.
            await SumPageSizesAsync();

            // Two-step async call.
            //Task sumTask = SumPageSizesAsync();
            //await sumTask;

            resultsTextBox.Text += "\r\nControl returned to startButton_Click.\r\n";
        }

        private async Task SumPageSizesAsync()
        {
            // Make a list of web addresses.
            List<string> urlList = SetUpURLList();

            // Declare an HttpClient object and increase the buffer size. The
            // default buffer size is 65,536.
            HttpClient client = new HttpClient() { MaxResponseContentBufferSize = 1000000 };

            // Create a query.
            IEnumerable<Task<int>> downloadTasksQuery =
                from url in urlList select ProcessURLAsync(url, client);

            // Use ToArray to execute the query and start the download tasks.
            Task<int>[] downloadTasks = downloadTasksQuery.ToArray();

            // You can do other work here before awaiting.

            // Await the completion of all the running tasks.
            int[] lengths = await Task.WhenAll(downloadTasks);

            //// The previous line is equivalent to the following two statements.
            //Task<int[]> whenAllTask = Task.WhenAll(downloadTasks);
            //int[] lengths = await whenAllTask;

            int total = lengths.Sum();

            //var total = 0;
            //foreach (var url in urlList)
            //{
            //    // GetByteArrayAsync returns a Task<T>. At completion, the task
            //    // produces a byte array.
            //    byte[] urlContent = await client.GetByteArrayAsync(url);

            //    // The previous line abbreviates the following two assignment
            //    // statements.
            //    Task<byte[]> getContentTask = client.GetByteArrayAsync(url);
            //    byte[] urlContent = await getContentTask;

            //    DisplayResults(url, urlContent);

            //    // Update the total.
            //    total += urlContent.Length;
            //}

            // Display the total count for all of the web addresses.
            resultsTextBox.Text +=
                $"\r\n\r\nTotal bytes returned:  {total}\r\n";
        }

        private List<string> SetUpURLList()
        {
            List<string> urls = new List<string>
            {
                "https://msdn.microsoft.com",
                "https://msdn.microsoft.com/library/hh290136.aspx",
                "https://msdn.microsoft.com/library/ee256749.aspx",
                "https://msdn.microsoft.com/library/hh290138.aspx",
                "https://msdn.microsoft.com/library/hh290140.aspx",
                "https://msdn.microsoft.com/library/dd470362.aspx",
                "https://msdn.microsoft.com/library/aa578028.aspx",
                "https://msdn.microsoft.com/library/ms404677.aspx",
                "https://msdn.microsoft.com/library/ff730837.aspx"
            };
            return urls;
        }

        // The actions from the foreach loop are moved to this async method.
        async Task<int> ProcessURLAsync(string url, HttpClient client)
        {
            byte[] byteArray = await client.GetByteArrayAsync(url);
            DisplayResults(url, byteArray);
            return byteArray.Length;
        }

        private void DisplayResults(string url, byte[] content)
        {
            // Display the length of each web site. The string format
            // is designed to be used with a monospaced font, such as
            // Lucida Console or Global Monospace.
            var bytes = content.Length;
            // Strip off the "https://".
            var displayURL = url.Replace("https://", "");
            resultsTextBox.Text += $"\n{displayURL,-58} {bytes,8}";
        }
    }
}
```

## <a name="see-also"></a><span data-ttu-id="cbed9-163">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cbed9-163">See also</span></span>

- <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>
- [<span data-ttu-id="cbed9-164">逐步解說：使用 async 和 await 存取 Web (C#)</span><span class="sxs-lookup"><span data-stu-id="cbed9-164">Walkthrough: Accessing the Web by Using async and await (C#)</span></span>](./walkthrough-accessing-the-web-by-using-async-and-await.md)
