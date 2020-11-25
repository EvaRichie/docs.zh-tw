---
title: 作法：使用平行類別逐一查看檔案目錄
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to iterate directories
ms.assetid: 555e9f48-f53d-4774-9bcf-3e965c732ec5
ms.openlocfilehash: 75097485c78e9ded67f41d9632f5399c081b3a16
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734461"
---
# <a name="how-to-iterate-file-directories-with-the-parallel-class"></a><span data-ttu-id="1ea24-102">作法：使用平行類別逐一查看檔案目錄</span><span class="sxs-lookup"><span data-stu-id="1ea24-102">How to: Iterate File Directories with the Parallel Class</span></span>

<span data-ttu-id="1ea24-103">在許多情況下，檔案反覆運算是一項可以輕鬆平行處理的作業。</span><span class="sxs-lookup"><span data-stu-id="1ea24-103">In many cases, file iteration is an operation that can be easily parallelized.</span></span> <span data-ttu-id="1ea24-104">[如何：使用 PLINQ 逐一查看檔案目錄](how-to-iterate-file-directories-with-plinq.md)這個主題示範針對許多案例執行此工作的最簡單方式。</span><span class="sxs-lookup"><span data-stu-id="1ea24-104">The topic [How to: Iterate File Directories with PLINQ](how-to-iterate-file-directories-with-plinq.md) shows the easiest way to perform this task for many scenarios.</span></span> <span data-ttu-id="1ea24-105">不過，當您的程式碼需要處理在存取檔案系統時可能會出現的許多類型例外狀況時，便會提升此工作的複雜性。</span><span class="sxs-lookup"><span data-stu-id="1ea24-105">However, complications can arise when your code has to deal with the many types of exceptions that can arise when accessing the file system.</span></span> <span data-ttu-id="1ea24-106">下列範例會示範處理該問題的其中一種方式。</span><span class="sxs-lookup"><span data-stu-id="1ea24-106">The following example shows one approach to the problem.</span></span> <span data-ttu-id="1ea24-107">它會使用以堆疊為基礎的反覆運算來周遊位於特定目錄底下的所有檔案和資料夾，並能使程式碼能夠攔截並處理各種不同的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="1ea24-107">It uses a stack-based iteration to traverse all files and folders under a specified directory, and it enables your code to catch and handle various exceptions.</span></span> <span data-ttu-id="1ea24-108">當然，要如何處理例外狀況仍然取決於您。</span><span class="sxs-lookup"><span data-stu-id="1ea24-108">Of course, the way that you handle the exceptions is up to you.</span></span>  
  
## <a name="example"></a><span data-ttu-id="1ea24-109">範例</span><span class="sxs-lookup"><span data-stu-id="1ea24-109">Example</span></span>  

 <span data-ttu-id="1ea24-110">下列範例會循序逐一查看目錄，但是以平行方式處理檔案。</span><span class="sxs-lookup"><span data-stu-id="1ea24-110">The following example iterates the directories sequentially, but processes the files in parallel.</span></span> <span data-ttu-id="1ea24-111">當您有大型的檔案/目錄比率時，這應該是最好的方法。</span><span class="sxs-lookup"><span data-stu-id="1ea24-111">This is probably the best approach when you have a large file-to-directory ratio.</span></span> <span data-ttu-id="1ea24-112">您也可以平行處理目錄反覆運算，並以循序方式存取每個檔案。</span><span class="sxs-lookup"><span data-stu-id="1ea24-112">It is also possible to parallelize the directory iteration, and access each file sequentially.</span></span> <span data-ttu-id="1ea24-113">除非您是特別鎖定具有大量處理器的電腦，否則同時對兩個迴圈進行平行處理應該不會很有效率。</span><span class="sxs-lookup"><span data-stu-id="1ea24-113">It is probably not efficient to parallelize both loops unless you are specifically targeting a machine with a large number of processors.</span></span> <span data-ttu-id="1ea24-114">不過無論如何，您都應該徹底地測試應用程式以判斷最佳方法。</span><span class="sxs-lookup"><span data-stu-id="1ea24-114">However, as in all cases, you should test your application thoroughly to determine the best approach.</span></span>  
  
 [!code-csharp[TPL_Parallel#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_file.cs#08)]
 [!code-vb[TPL_Parallel#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/fileiteration08.vb#08)]  
  
 <span data-ttu-id="1ea24-115">在此範例中，檔案 I/O 是以同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="1ea24-115">In this example, the file I/O is performed synchronously.</span></span> <span data-ttu-id="1ea24-116">處理大型檔案或低速的網路連線時，您應該考慮以非同步方式存取檔案。</span><span class="sxs-lookup"><span data-stu-id="1ea24-116">When dealing with large files or slow network connections, it might be preferable to access the files asynchronously.</span></span> <span data-ttu-id="1ea24-117">您可以結合非同步 I/O 技術與平行反覆運算。</span><span class="sxs-lookup"><span data-stu-id="1ea24-117">You can combine asynchronous I/O techniques with parallel iteration.</span></span> <span data-ttu-id="1ea24-118">如需詳細資訊，請參閱 [TPL 和傳統 .Net 非同步程式設計](tpl-and-traditional-async-programming.md)。</span><span class="sxs-lookup"><span data-stu-id="1ea24-118">For more information, see [TPL and Traditional .NET Asynchronous Programming](tpl-and-traditional-async-programming.md).</span></span>  
  
 <span data-ttu-id="1ea24-119">這個範例會使用本機 `fileCount` 變數維護已處理檔案的總數。</span><span class="sxs-lookup"><span data-stu-id="1ea24-119">The example uses the local `fileCount` variable to maintain a count of the total number of files processed.</span></span> <span data-ttu-id="1ea24-120">由於可能會有多個工作同時存取這個變數，因此會透過呼叫 <xref:System.Threading.Interlocked.Add%2A?displayProperty=nameWithType> 方法同步處理其存取。</span><span class="sxs-lookup"><span data-stu-id="1ea24-120">Because the variable might be accessed concurrently by multiple tasks, access to it is synchronized by calling the <xref:System.Threading.Interlocked.Add%2A?displayProperty=nameWithType> method.</span></span>  
  
 <span data-ttu-id="1ea24-121">請注意，若有例外狀況在主執行緒上擲出，由 <xref:System.Threading.Tasks.Parallel.ForEach%2A> 啟動的執行緒可能會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="1ea24-121">Note that if an exception is thrown on the main thread, the threads that are started by the <xref:System.Threading.Tasks.Parallel.ForEach%2A> method might continue to run.</span></span> <span data-ttu-id="1ea24-122">若要停止這些執行緒，您可以在例外處理常式中設定布林值變數，並在平行迴圈的每個反覆運算上檢查其值。</span><span class="sxs-lookup"><span data-stu-id="1ea24-122">To stop these threads, you can set a Boolean variable in your exception handlers, and check its value on each iteration of the parallel loop.</span></span> <span data-ttu-id="1ea24-123">若該值指出有擲出例外狀況，請使用 <xref:System.Threading.Tasks.ParallelLoopState> 變數來停止或中斷迴圈。</span><span class="sxs-lookup"><span data-stu-id="1ea24-123">If the value indicates that an exception has been thrown, use the <xref:System.Threading.Tasks.ParallelLoopState> variable to stop or break from the loop.</span></span> <span data-ttu-id="1ea24-124">如需詳細資訊，請參閱[如何：停止或中斷 Parallel.For 迴圈](/previous-versions/dotnet/netframework-4.0/dd460721(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="1ea24-124">For more information, see [How to: Stop or Break from a Parallel.For Loop](/previous-versions/dotnet/netframework-4.0/dd460721(v=vs.100)).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1ea24-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1ea24-125">See also</span></span>

- [<span data-ttu-id="1ea24-126">資料平行處理</span><span class="sxs-lookup"><span data-stu-id="1ea24-126">Data Parallelism</span></span>](data-parallelism-task-parallel-library.md)
