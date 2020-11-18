---
title: Interop 與其他非同步模式和類型
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- asynchronous design patterns, .NET
- TAP, .NET support for
- Task-based Asynchronous Pattern, .NET support for
- .NET, asynchronous design patterns
ms.assetid: f120a5d9-933b-4d1d-acb6-f034a57c3749
ms.openlocfilehash: b0dd786e1922d75edcb0326cc9e98037c6e4945c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830320"
---
# <a name="interop-with-other-asynchronous-patterns-and-types"></a><span data-ttu-id="7470d-102">Interop 與其他非同步模式和類型</span><span class="sxs-lookup"><span data-stu-id="7470d-102">Interop with Other Asynchronous Patterns and Types</span></span>

<span data-ttu-id="7470d-103">.NET 中非同步模式的簡短歷程記錄：</span><span class="sxs-lookup"><span data-stu-id="7470d-103">A brief history of asynchronous patterns in .NET:</span></span>

- <span data-ttu-id="7470d-104">.NET Framework 1.0 引進了 <xref:System.IAsyncResult> 模式，也就是所謂的 [非同步程式設計模型 (APM) ](asynchronous-programming-model-apm.md)或 `Begin/End` 模式。</span><span class="sxs-lookup"><span data-stu-id="7470d-104">.NET Framework 1.0 introduced the <xref:System.IAsyncResult> pattern, otherwise known as the [Asynchronous Programming Model (APM)](asynchronous-programming-model-apm.md), or the `Begin/End` pattern.</span></span>
- <span data-ttu-id="7470d-105">.NET Framework 2.0 已將 [事件架構非同步模式新增 (EAP) ](event-based-asynchronous-pattern-eap.md)。</span><span class="sxs-lookup"><span data-stu-id="7470d-105">.NET Framework 2.0 added the [Event-based Asynchronous Pattern (EAP)](event-based-asynchronous-pattern-eap.md).</span></span>
- <span data-ttu-id="7470d-106">.NET Framework 4 引進了以工作 [為基礎的非同步模式 (](task-based-asynchronous-pattern-tap.md)點一下) ，它會取代 APM 和 EAP，並可讓您輕鬆地從先前的模式建立遷移常式。</span><span class="sxs-lookup"><span data-stu-id="7470d-106">.NET Framework 4 introduced the [Task-based Asynchronous Pattern (TAP)](task-based-asynchronous-pattern-tap.md), which supersedes both APM and EAP and provides the ability to easily build migration routines from the earlier patterns.</span></span>
  
## <a name="tasks-and-the-asynchronous-programming-model-apm"></a><span data-ttu-id="7470d-107">工作與非同步程式設計模型 (APM)</span><span class="sxs-lookup"><span data-stu-id="7470d-107">Tasks and the Asynchronous Programming Model (APM)</span></span>

### <a name="from-apm-to-tap"></a><span data-ttu-id="7470d-108">從 APM 到 TAP</span><span class="sxs-lookup"><span data-stu-id="7470d-108">From APM to TAP</span></span>  
 <span data-ttu-id="7470d-109">由於 [非同步程式設計模型 (APM) ](asynchronous-programming-model-apm.md) 模式是結構化的，因此很容易就能建立包裝函式，以將 apm 執行公開為點一下執行。</span><span class="sxs-lookup"><span data-stu-id="7470d-109">Because the [Asynchronous Programming Model (APM)](asynchronous-programming-model-apm.md) pattern is structured, it is quite easy to build a wrapper to expose an APM implementation as a TAP implementation.</span></span> <span data-ttu-id="7470d-110">.NET Framework 4 和更新版本會以方法多載的形式包含 helper 常式 <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> ，以提供這項轉譯。</span><span class="sxs-lookup"><span data-stu-id="7470d-110">.NET Framework 4 and later versions include helper routines in the form of <xref:System.Threading.Tasks.TaskFactory.FromAsync%2A> method overloads to provide this translation.</span></span>  
  
 <span data-ttu-id="7470d-111">請考慮 <xref:System.IO.Stream> 類別以及其 <xref:System.IO.Stream.BeginRead%2A> 與 <xref:System.IO.Stream.EndRead%2A> 方法，此類方法代表同步 <xref:System.IO.Stream.Read%2A> 方法的 APM 對應項目：</span><span class="sxs-lookup"><span data-stu-id="7470d-111">Consider the <xref:System.IO.Stream> class and its <xref:System.IO.Stream.BeginRead%2A> and <xref:System.IO.Stream.EndRead%2A> methods, which represent the APM counterpart to the synchronous <xref:System.IO.Stream.Read%2A> method:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#1)]
 [!code-vb[Conceptual.AsyncInterop#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#1)]  
[!code-csharp[Conceptual.AsyncInterop#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#2)]
[!code-vb[Conceptual.AsyncInterop#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#2)]  
[!code-csharp[Conceptual.AsyncInterop#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Stream1.cs#3)]
[!code-vb[Conceptual.AsyncInterop#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/stream1.vb#3)]  
  
 <span data-ttu-id="7470d-112">您可以使用 <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> 方法來實作這項作業的 TAP 包裝函式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7470d-112">You can use the <xref:System.Threading.Tasks.TaskFactory%601.FromAsync%2A?displayProperty=nameWithType> method to implement a TAP wrapper for this operation as follows:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wrap1.cs#4)]
 [!code-vb[Conceptual.AsyncInterop#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wrap1.vb#4)]  
  
 <span data-ttu-id="7470d-113">這個實作相似下面這個：</span><span class="sxs-lookup"><span data-stu-id="7470d-113">This implementation is similar to the following:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wrap2.cs#5)]
 [!code-vb[Conceptual.AsyncInterop#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wrap2.vb#5)]  
  
### <a name="from-tap-to-apm"></a><span data-ttu-id="7470d-114">從 TAP 到 APM</span><span class="sxs-lookup"><span data-stu-id="7470d-114">From TAP to APM</span></span>  
 <span data-ttu-id="7470d-115">如果您現有的基礎結構預期 APM 模式，則您也需進行 TAP 實作，並在預期 APM 實作的位置加以使用。</span><span class="sxs-lookup"><span data-stu-id="7470d-115">If your existing infrastructure expects the APM pattern, you'll also want to take a TAP implementation and use it where an APM implementation is expected.</span></span>  <span data-ttu-id="7470d-116">由於可以組成工作，並且 <xref:System.Threading.Tasks.Task> 類別會實作 <xref:System.IAsyncResult>，因此您可以使用簡單的 Helper 函式來完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="7470d-116">Because tasks can be composed and  the <xref:System.Threading.Tasks.Task> class implements <xref:System.IAsyncResult>, you can use a straightforward helper function to do this.</span></span> <span data-ttu-id="7470d-117">下列程式碼會使用 <xref:System.Threading.Tasks.Task%601> 類別的擴充功能，但是您可以針對非泛型工作使用幾乎完全相同的函式。</span><span class="sxs-lookup"><span data-stu-id="7470d-117">The following code uses an extension of the <xref:System.Threading.Tasks.Task%601> class, but you can use an almost identical function for non-generic tasks.</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM1.cs#6)]
 [!code-vb[Conceptual.AsyncInterop#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM1.vb#6)]  
  
 <span data-ttu-id="7470d-118">現在，考量一下有下列 TAP 實作的案例：</span><span class="sxs-lookup"><span data-stu-id="7470d-118">Now, consider a case where you have the following TAP implementation:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#7)]
 [!code-vb[Conceptual.AsyncInterop#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#7)]  
  
 <span data-ttu-id="7470d-119">而且您想要提供此 APM 實作：</span><span class="sxs-lookup"><span data-stu-id="7470d-119">and you want to provide this APM implementation:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#8)]
 [!code-vb[Conceptual.AsyncInterop#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#8)]  
[!code-csharp[Conceptual.AsyncInterop#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#9)]
[!code-vb[Conceptual.AsyncInterop#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#9)]  
  
 <span data-ttu-id="7470d-120">下列範例將示範如何移轉至 APM：</span><span class="sxs-lookup"><span data-stu-id="7470d-120">The following example demonstrates one migration to APM:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/APM2.cs#10)]
 [!code-vb[Conceptual.AsyncInterop#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/APM2.vb#10)]  
  
## <a name="tasks-and-the-event-based-asynchronous-pattern-eap"></a><span data-ttu-id="7470d-121">工作與事件架構非同步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="7470d-121">Tasks and the Event-based Asynchronous Pattern (EAP)</span></span>  
 <span data-ttu-id="7470d-122">包裝 [Event-based Asynchronous Pattern (EAP)](event-based-asynchronous-pattern-eap.md) 實作會比包裝 APM 模式更為複雜，原因是 EAP 模式擁有較多的變化，結構也不如 APM 模式嚴謹。</span><span class="sxs-lookup"><span data-stu-id="7470d-122">Wrapping an [Event-based Asynchronous Pattern (EAP)](event-based-asynchronous-pattern-eap.md) implementation is more involved than wrapping an APM pattern, because the EAP pattern has more variation and less structure than the APM pattern.</span></span>  <span data-ttu-id="7470d-123">供示範所用，下列程式碼包裝了 `DownloadStringAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="7470d-123">To demonstrate, the following code wraps the `DownloadStringAsync` method.</span></span>  <span data-ttu-id="7470d-124">`DownloadStringAsync` 會接受 URI、在下載時引發 `DownloadProgressChanged` 事件，以報告多個進行中的統計資料，然後在完成時引發 `DownloadStringCompleted` 。</span><span class="sxs-lookup"><span data-stu-id="7470d-124">`DownloadStringAsync` accepts a URI, raises the `DownloadProgressChanged` event while downloading in order to report multiple statistics on progress, and raises the `DownloadStringCompleted` event when it's done.</span></span>  <span data-ttu-id="7470d-125">最終結果是字串，其中包含指定之 URI 頁面的內容。</span><span class="sxs-lookup"><span data-stu-id="7470d-125">The final result is a string that contains the contents of the page at the specified URI.</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/EAP1.cs#11)]
 [!code-vb[Conceptual.AsyncInterop#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/EAP1.vb#11)]  
  
## <a name="tasks-and-wait-handles"></a><span data-ttu-id="7470d-126">工作與等候控制代碼</span><span class="sxs-lookup"><span data-stu-id="7470d-126">Tasks and Wait Handles</span></span>  
  
### <a name="from-wait-handles-to-tap"></a><span data-ttu-id="7470d-127">從等候控制代碼到 TAP</span><span class="sxs-lookup"><span data-stu-id="7470d-127">From Wait Handles to TAP</span></span>  
 <span data-ttu-id="7470d-128">雖然等候控制代碼不會實作非同步模式，但進階開發人員可能會在等候控制代碼設定完成後，使用 <xref:System.Threading.WaitHandle> 類別與 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType> 方法，用於非同步通知。</span><span class="sxs-lookup"><span data-stu-id="7470d-128">Although wait handles don't implement an asynchronous pattern, advanced developers may use the <xref:System.Threading.WaitHandle> class and the <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A?displayProperty=nameWithType> method for asynchronous notifications when a wait handle is set.</span></span>  <span data-ttu-id="7470d-129">您可以包裝 <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A> 方法，以啟用等候控制代碼上任何同步等候的工作式替代方案：</span><span class="sxs-lookup"><span data-stu-id="7470d-129">You can wrap the <xref:System.Threading.ThreadPool.RegisterWaitForSingleObject%2A> method to enable a task-based alternative to any synchronous wait on a wait handle:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wait1.cs#12)]
 [!code-vb[Conceptual.AsyncInterop#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wait1.vb#12)]  
  
 <span data-ttu-id="7470d-130">有了此方法，您可以使用非同步方法中現有的 <xref:System.Threading.WaitHandle> 實作。</span><span class="sxs-lookup"><span data-stu-id="7470d-130">With this method, you can use existing <xref:System.Threading.WaitHandle> implementations in asynchronous methods.</span></span>  <span data-ttu-id="7470d-131">例如，如果您想要節流處理任何特定時間執行的非同步作業數目，可以利用旗號 (<xref:System.Threading.SemaphoreSlim?displayProperty=nameWithType> 物件)。</span><span class="sxs-lookup"><span data-stu-id="7470d-131">For example, if you want to throttle the number of asynchronous operations that are executing at any particular time, you can utilize a semaphore (a <xref:System.Threading.SemaphoreSlim?displayProperty=nameWithType> object).</span></span>  <span data-ttu-id="7470d-132">您可以藉由將信號的計數初始化為 *n*，在您每次想要執行作業時等待信號，並在完成作業時釋放信號，以節流至 *n* 個並存執行的作業數目：</span><span class="sxs-lookup"><span data-stu-id="7470d-132">You can throttle to *N* the number of operations that run concurrently by initializing the semaphore's count to *N*, waiting on the semaphore any time you want to perform an operation, and releasing the semaphore when you're done with an operation:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#13](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Semaphore1.cs#13)]
 [!code-vb[Conceptual.AsyncInterop#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Semaphore1.vb#13)]  
  
 <span data-ttu-id="7470d-133">您也可以建置非同步的旗號，而該旗號不會依賴等候控制代碼，並會完全與工作一同合作。</span><span class="sxs-lookup"><span data-stu-id="7470d-133">You can also build an asynchronous semaphore that does not rely on wait handles and instead works completely with tasks.</span></span> <span data-ttu-id="7470d-134">若要這樣做，您可以使用像是 [Consuming the Task-based Asynchronous Pattern](consuming-the-task-based-asynchronous-pattern.md) 中所討論的技術，用以在 <xref:System.Threading.Tasks.Task>。</span><span class="sxs-lookup"><span data-stu-id="7470d-134">To do this, you can use techniques such as those discussed in [Consuming the Task-based Asynchronous Pattern](consuming-the-task-based-asynchronous-pattern.md) for building data structures on top of <xref:System.Threading.Tasks.Task>.</span></span>  
  
### <a name="from-tap-to-wait-handles"></a><span data-ttu-id="7470d-135">從 TAP 到等候控制代碼</span><span class="sxs-lookup"><span data-stu-id="7470d-135">From TAP to Wait Handles</span></span>  
 <span data-ttu-id="7470d-136">如先前所述， <xref:System.Threading.Tasks.Task> 類別會實作 <xref:System.IAsyncResult>，且該實作會公開 <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle%2A> 屬性，而該屬性會傳回 <xref:System.Threading.Tasks.Task> 完成時將進行設定的等候控制代碼。</span><span class="sxs-lookup"><span data-stu-id="7470d-136">As previously mentioned, the <xref:System.Threading.Tasks.Task> class implements <xref:System.IAsyncResult>, and that implementation exposes an <xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle%2A> property that returns a wait handle that will be set when the <xref:System.Threading.Tasks.Task> completes.</span></span>  <span data-ttu-id="7470d-137">您可以取得 <xref:System.Threading.WaitHandle> 的 <xref:System.Threading.Tasks.Task> ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7470d-137">You can get a <xref:System.Threading.WaitHandle> for a <xref:System.Threading.Tasks.Task> as follows:</span></span>  
  
 [!code-csharp[Conceptual.AsyncInterop#14](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.AsyncInterop/cs/Wait1.cs#14)]
 [!code-vb[Conceptual.AsyncInterop#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.AsyncInterop/vb/Wait1.vb#14)]  
  
## <a name="see-also"></a><span data-ttu-id="7470d-138">請參閱</span><span class="sxs-lookup"><span data-stu-id="7470d-138">See also</span></span>

- [<span data-ttu-id="7470d-139">以工作為基礎的非同步模式 (TAP)</span><span class="sxs-lookup"><span data-stu-id="7470d-139">Task-based Asynchronous Pattern (TAP)</span></span>](task-based-asynchronous-pattern-tap.md)
- [<span data-ttu-id="7470d-140">實作以工作為基礎的非同步模式</span><span class="sxs-lookup"><span data-stu-id="7470d-140">Implementing the Task-based Asynchronous Pattern</span></span>](implementing-the-task-based-asynchronous-pattern.md)
- [<span data-ttu-id="7470d-141">使用以工作為基礎的非同步模式</span><span class="sxs-lookup"><span data-stu-id="7470d-141">Consuming the Task-based Asynchronous Pattern</span></span>](consuming-the-task-based-asynchronous-pattern.md)
