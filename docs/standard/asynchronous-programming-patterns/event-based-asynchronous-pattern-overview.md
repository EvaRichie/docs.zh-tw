---
title: 事件架構非同步模式概觀
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 792aa8da-918b-458e-b154-9836b97735f3
ms.openlocfilehash: f4aac5afbb13cafa7bb0e9c1eb6bbd92ac41bf8c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289417"
---
# <a name="event-based-asynchronous-pattern-overview"></a><span data-ttu-id="2cef0-102">事件架構非同步模式概觀</span><span class="sxs-lookup"><span data-stu-id="2cef0-102">Event-based Asynchronous Pattern Overview</span></span>
<span data-ttu-id="2cef0-103">要同時執行許多工作，還能繼續回應使用者互動，這樣的應用程式通常都需要可以使用多執行緒的設計。</span><span class="sxs-lookup"><span data-stu-id="2cef0-103">Applications that perform many tasks simultaneously, yet remain responsive to user interaction, often require a design that uses multiple threads.</span></span> <span data-ttu-id="2cef0-104"><xref:System.Threading> 命名空間提供建立高效能多執行緒應用程式的所有必要工具，但是要有效地使用這些工具，需要具備多執行緒軟體工程的豐富經驗。</span><span class="sxs-lookup"><span data-stu-id="2cef0-104">The <xref:System.Threading> namespace provides all the tools necessary to create high-performance multithreaded applications, but using these tools effectively requires significant experience with multithreaded software engineering.</span></span> <span data-ttu-id="2cef0-105">對於較簡單的多執行緒應用程式，<xref:System.ComponentModel.BackgroundWorker> 元件提供了簡單明瞭的方案。</span><span class="sxs-lookup"><span data-stu-id="2cef0-105">For relatively simple multithreaded applications, the <xref:System.ComponentModel.BackgroundWorker> component provides a straightforward solution.</span></span> <span data-ttu-id="2cef0-106">如果是較為複雜精細的非同步應用程式，請考慮實作遵守事件架構非同步模式的類別。</span><span class="sxs-lookup"><span data-stu-id="2cef0-106">For more sophisticated asynchronous applications, consider implementing a class that adheres to the Event-based Asynchronous Pattern.</span></span>  
  
 <span data-ttu-id="2cef0-107">事件架構非同步模式提供多執行緒應用程式的優點，同時隱藏多執行緒設計中許多原有的複雜問題。</span><span class="sxs-lookup"><span data-stu-id="2cef0-107">The Event-based Asynchronous Pattern makes available the advantages of multithreaded applications while hiding many of the complex issues inherent in multithreaded design.</span></span> <span data-ttu-id="2cef0-108">使用支援此模式的類別，可以讓您：</span><span class="sxs-lookup"><span data-stu-id="2cef0-108">Using a class that supports this pattern can allow you to:</span></span>  
  
- <span data-ttu-id="2cef0-109">「在背景中」執行耗時的工作，像是下載及資料庫作業，而不會中斷應用程式。</span><span class="sxs-lookup"><span data-stu-id="2cef0-109">Perform time-consuming tasks, such as downloads and database operations, "in the background," without interrupting your application.</span></span>  
  
- <span data-ttu-id="2cef0-110">同時執行多項作業，並在每項作業完成時都收到通知。</span><span class="sxs-lookup"><span data-stu-id="2cef0-110">Execute multiple operations simultaneously, receiving notifications when each completes.</span></span>  
  
- <span data-ttu-id="2cef0-111">等候資源變成可供使用，而不需要停止 (「封鎖」) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2cef0-111">Wait for resources to become available without stopping ("blocking") your application.</span></span>  
  
- <span data-ttu-id="2cef0-112">使用熟悉的事件和委派模型，與暫止的非同步作業通訊。</span><span class="sxs-lookup"><span data-stu-id="2cef0-112">Communicate with pending asynchronous operations using the familiar events-and-delegates model.</span></span> <span data-ttu-id="2cef0-113">如需使用事件處理常式和委派的詳細資訊，請參閱[事件](../events/index.md)。</span><span class="sxs-lookup"><span data-stu-id="2cef0-113">For more information on using event handlers and delegates, see [Events](../events/index.md).</span></span>  
  
 <span data-ttu-id="2cef0-114">支援事件架構非同步模式的類別，會有一或多個名為 _MethodName_**Async** 的方法。</span><span class="sxs-lookup"><span data-stu-id="2cef0-114">A class that supports the Event-based Asynchronous Pattern will have one or more methods named _MethodName_**Async**.</span></span> <span data-ttu-id="2cef0-115">這些方法可能鏡像在目前執行緒上執行相同作業的同步版本。</span><span class="sxs-lookup"><span data-stu-id="2cef0-115">These methods may mirror synchronous versions, which perform the same operation on the current thread.</span></span> <span data-ttu-id="2cef0-116">這個類別可能也具有 _MethodName_**Completed** 事件，且具有 _MethodName_**AsyncCancel** (或簡稱 **CancelAsync**) 方法。</span><span class="sxs-lookup"><span data-stu-id="2cef0-116">The class may also have a _MethodName_**Completed** event and it may have a _MethodName_**AsyncCancel** (or simply **CancelAsync**) method.</span></span>  
  
 <span data-ttu-id="2cef0-117"><xref:System.Windows.Forms.PictureBox> 是支援事件架構非同步模式的一般元件。</span><span class="sxs-lookup"><span data-stu-id="2cef0-117"><xref:System.Windows.Forms.PictureBox> is a typical component that supports the Event-based Asynchronous Pattern.</span></span> <span data-ttu-id="2cef0-118">您可以呼叫影像的 <xref:System.Windows.Forms.PictureBox.Load%2A> 方法以同步下載影像，但如果影像非常龐大或是網路連接相當緩慢，則在下載作業完成及傳回 <xref:System.Windows.Forms.PictureBox.Load%2A> 的呼叫之前，應用程式都會是停止回應狀態。</span><span class="sxs-lookup"><span data-stu-id="2cef0-118">You can download an image synchronously by calling its <xref:System.Windows.Forms.PictureBox.Load%2A> method, but if the image is large, or if the network connection is slow, your application will stop responding until the download operation is completed and the call to <xref:System.Windows.Forms.PictureBox.Load%2A> returns.</span></span>  
  
 <span data-ttu-id="2cef0-119">如果要讓應用程式在載入影像時持續執行，您可以呼叫 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> 方法並處理 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 事件，就像處理其他任何事件一樣。</span><span class="sxs-lookup"><span data-stu-id="2cef0-119">If you want your application to keep running while the image is loading, you can call the <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> method and handle the <xref:System.Windows.Forms.PictureBox.LoadCompleted> event, just as you would handle any other event.</span></span> <span data-ttu-id="2cef0-120">當您呼叫 <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> 方法時，應用程式就會繼續執行，同時下載會在個別的執行緒上 (「在背景中」) 進行。</span><span class="sxs-lookup"><span data-stu-id="2cef0-120">When you call the <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> method, your application will continue to run while the download proceeds on a separate thread ("in the background").</span></span> <span data-ttu-id="2cef0-121">當影像載入作業完成時，就會呼叫您的事件處理常式，此時事件處理常式便可以檢查 <xref:System.ComponentModel.AsyncCompletedEventArgs> 參數，以判斷下載是否順利完成。</span><span class="sxs-lookup"><span data-stu-id="2cef0-121">Your event handler will be called when the image-loading operation is complete, and your event handler can examine the <xref:System.ComponentModel.AsyncCompletedEventArgs> parameter to determine if the download completed successfully.</span></span>  
  
 <span data-ttu-id="2cef0-122">事件架構非同步模式需要能夠取消非同步作業，而 <xref:System.Windows.Forms.PictureBox> 控制項以它所具有的 <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> 方法支援這項需求。</span><span class="sxs-lookup"><span data-stu-id="2cef0-122">The Event-based Asynchronous Pattern requires that an asynchronous operation can be canceled, and the <xref:System.Windows.Forms.PictureBox> control supports this requirement with its <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> method.</span></span> <span data-ttu-id="2cef0-123">呼叫 <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> 便會發出要求讓暫止的下載停止，而且在取消工作時，就會引發 <xref:System.Windows.Forms.PictureBox.LoadCompleted> 事件。</span><span class="sxs-lookup"><span data-stu-id="2cef0-123">Calling <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> submits a request to stop the pending download, and when the task is canceled, the <xref:System.Windows.Forms.PictureBox.LoadCompleted> event is raised.</span></span>  
  
> [!CAUTION]
> <span data-ttu-id="2cef0-124">產生 <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> 要求時剛好完成下載也是可能發生的，因此 <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> 可能無法反映取消的要求。</span><span class="sxs-lookup"><span data-stu-id="2cef0-124">It is possible that the download will finish just as the <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> request is made, so <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> may not reflect the request to cancel.</span></span> <span data-ttu-id="2cef0-125">這種情況稱為「競爭情形」\*\*(Race Condition)，這是多執行緒程式設計中的常見問題。</span><span class="sxs-lookup"><span data-stu-id="2cef0-125">This is called a *race condition* and is a common issue in multithreaded programming.</span></span> <span data-ttu-id="2cef0-126">如需多執行緒程式設計問題的詳細資訊，請參閱[受控執行緒處理的最佳做法](../threading/managed-threading-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="2cef0-126">For more information on issues in multithreaded programming, see [Managed Threading Best Practices](../threading/managed-threading-best-practices.md).</span></span>  
  
## <a name="characteristics-of-the-event-based-asynchronous-pattern"></a><span data-ttu-id="2cef0-127">事件架構非同步模式的特性</span><span class="sxs-lookup"><span data-stu-id="2cef0-127">Characteristics of the Event-based Asynchronous Pattern</span></span>  
 <span data-ttu-id="2cef0-128">事件架構非同步模式可能會採用數種格式，需視特定類別所支援作業的複雜度而定。</span><span class="sxs-lookup"><span data-stu-id="2cef0-128">The Event-based Asynchronous Pattern may take several forms, depending on the complexity of the operations supported by a particular class.</span></span> <span data-ttu-id="2cef0-129">最簡單的類別可以有單一的 _MethodName_**Async** 方法和對應的 _MethodName_**Completed** 事件。</span><span class="sxs-lookup"><span data-stu-id="2cef0-129">The simplest classes may have a single _MethodName_**Async** method and a corresponding _MethodName_**Completed** event.</span></span> <span data-ttu-id="2cef0-130">比較複雜的類別則可以有數個 _MethodName_**Async** 方法，每一個方法都有對應的 _MethodName_**Completed** 事件，以及這些方法的同步版本。</span><span class="sxs-lookup"><span data-stu-id="2cef0-130">More complex classes may have several _MethodName_**Async** methods, each with a corresponding _MethodName_**Completed** event, as well as synchronous versions of these methods.</span></span> <span data-ttu-id="2cef0-131">這些類別可以選擇性地支援每個非同步方法的取消、進度報告和累加結果。</span><span class="sxs-lookup"><span data-stu-id="2cef0-131">Classes can optionally support cancellation, progress reporting, and incremental results for each asynchronous method.</span></span>  
  
 <span data-ttu-id="2cef0-132">非同步方法也可以支援多次暫止呼叫 (多個並行引動過程)，讓您的程式碼能在完成其他暫止作業之前，對這種方法呼叫任意次數。</span><span class="sxs-lookup"><span data-stu-id="2cef0-132">An asynchronous method may also support multiple pending calls (multiple concurrent invocations), allowing your code to call it any number of times before it completes other pending operations.</span></span> <span data-ttu-id="2cef0-133">要正確地處理這種情況，您的應用程式可能需要追蹤每個作業的完成狀態。</span><span class="sxs-lookup"><span data-stu-id="2cef0-133">Correctly handling this situation may require your application to track the completion of each operation.</span></span>  
  
### <a name="examples-of-the-event-based-asynchronous-pattern"></a><span data-ttu-id="2cef0-134">事件架構非同步模式的範例</span><span class="sxs-lookup"><span data-stu-id="2cef0-134">Examples of the Event-based Asynchronous Pattern</span></span>  
 <span data-ttu-id="2cef0-135"><xref:System.Media.SoundPlayer> 和 <xref:System.Windows.Forms.PictureBox> 元件代表事件架構非同步模式的簡單實作。</span><span class="sxs-lookup"><span data-stu-id="2cef0-135">The <xref:System.Media.SoundPlayer> and <xref:System.Windows.Forms.PictureBox> components represent simple implementations of the Event-based Asynchronous Pattern.</span></span> <span data-ttu-id="2cef0-136"><xref:System.Net.WebClient> 和 <xref:System.ComponentModel.BackgroundWorker> 元件則代表事件架構非同步模式的較複雜實作。</span><span class="sxs-lookup"><span data-stu-id="2cef0-136">The <xref:System.Net.WebClient> and <xref:System.ComponentModel.BackgroundWorker> components represent more complex implementations of the Event-based Asynchronous Pattern.</span></span>  
  
 <span data-ttu-id="2cef0-137">以下是符合此模式的範例類別宣告：</span><span class="sxs-lookup"><span data-stu-id="2cef0-137">Below is an example class declaration that conforms to the pattern:</span></span>  
  
```vb  
Public Class AsyncExample  
    ' Synchronous methods.  
    Public Function Method1(ByVal param As String) As Integer
    Public Sub Method2(ByVal param As Double)
  
    ' Asynchronous methods.  
    Overloads Public Sub Method1Async(ByVal param As String)
    Overloads Public Sub Method1Async(ByVal param As String, ByVal userState As Object)
    Public Event Method1Completed As Method1CompletedEventHandler  
  
    Overloads Public Sub Method2Async(ByVal param As Double)
    Overloads Public Sub Method2Async(ByVal param As Double, ByVal userState As Object)
    Public Event Method2Completed As Method2CompletedEventHandler  
  
    Public Sub CancelAsync(ByVal userState As Object)
  
    Public ReadOnly Property IsBusy () As Boolean  
  
    ' Class implementation not shown.  
End Class  
```  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
```  
  
 <span data-ttu-id="2cef0-138">虛擬 `AsyncExample` 類別具有兩個方法，這兩種方法都支援同步和非同步引動過程。</span><span class="sxs-lookup"><span data-stu-id="2cef0-138">The fictitious `AsyncExample` class has two methods, both of which support synchronous and asynchronous invocations.</span></span> <span data-ttu-id="2cef0-139">同步多載的行為與任何方法呼叫都一樣，並且會在呼叫的執行緒上執行作業；如果作業相當耗時，在呼叫傳回之前，可能會明顯出現延遲。</span><span class="sxs-lookup"><span data-stu-id="2cef0-139">The synchronous overloads behave like any method call and execute the operation on the calling thread; if the operation is time-consuming, there may be a noticeable delay before the call returns.</span></span> <span data-ttu-id="2cef0-140">非同步多載會在另一個執行緒上啟動作業，然後立即傳回，讓呼叫的執行緒能夠繼續進行，同時作業依然能「在背景中」執行。</span><span class="sxs-lookup"><span data-stu-id="2cef0-140">The asynchronous overloads will start the operation on another thread and then return immediately, allowing the calling thread to continue while the operation executes "in the background."</span></span>  
  
### <a name="asynchronous-method-overloads"></a><span data-ttu-id="2cef0-141">非同步方法多載</span><span class="sxs-lookup"><span data-stu-id="2cef0-141">Asynchronous Method Overloads</span></span>  
 <span data-ttu-id="2cef0-142">非同步作業具有兩種可能的多載：單一引動過程和多個引動過程。</span><span class="sxs-lookup"><span data-stu-id="2cef0-142">There are potentially two overloads for the asynchronous operations: single-invocation and multiple-invocation.</span></span> <span data-ttu-id="2cef0-143">您可以根據其方法簽章來區別這兩種格式：多個引動過程格式具有稱為 `userState` 的額外參數。</span><span class="sxs-lookup"><span data-stu-id="2cef0-143">You can distinguish these two forms by their method signatures: the multiple-invocation form has an extra parameter called `userState`.</span></span> <span data-ttu-id="2cef0-144">這種格式使您的程式碼能夠呼叫 `Method1Async(string param, object userState)` 多次，而不需要等候任何暫止的非同步作業完成。</span><span class="sxs-lookup"><span data-stu-id="2cef0-144">This form makes it possible for your code to call `Method1Async(string param, object userState)` multiple times without waiting for any pending asynchronous operations to finish.</span></span> <span data-ttu-id="2cef0-145">另一方面，如果您在先前的引動過程完成之前，嘗試呼叫 `Method1Async(string param)`，此方法就會引發 <xref:System.InvalidOperationException>。</span><span class="sxs-lookup"><span data-stu-id="2cef0-145">If, on the other hand, you try to call `Method1Async(string param)` before a previous invocation has completed, the method raises an <xref:System.InvalidOperationException>.</span></span>  
  
 <span data-ttu-id="2cef0-146">多個引動過程多載的 `userState` 參數可讓您區別各種非同步作業。</span><span class="sxs-lookup"><span data-stu-id="2cef0-146">The `userState` parameter for the multiple-invocation overloads allows you to distinguish among asynchronous operations.</span></span> <span data-ttu-id="2cef0-147">您可以為 `Method1Async(string param, object userState)` 的每個呼叫提供唯一值 (例如，GUID 或雜湊碼)，當每個作業完成時，事件處理常式就可以判斷是哪個作業的執行個體引發了完成事件。</span><span class="sxs-lookup"><span data-stu-id="2cef0-147">You provide a unique value (for example, a GUID or hash code) for each call to `Method1Async(string param, object userState)`, and when each operation is completed, your event handler can determine which instance of the operation raised the completion event.</span></span>  
  
### <a name="tracking-pending-operations"></a><span data-ttu-id="2cef0-148">追蹤暫止的作業</span><span class="sxs-lookup"><span data-stu-id="2cef0-148">Tracking Pending Operations</span></span>  
 <span data-ttu-id="2cef0-149">如果使用多個引動過程多載，程式碼就必須持續追蹤暫止工作的 `userState` 物件 (工作 ID)。</span><span class="sxs-lookup"><span data-stu-id="2cef0-149">If you use the multiple-invocation overloads, your code will need to keep track of the `userState` objects (task IDs) for pending tasks.</span></span> <span data-ttu-id="2cef0-150">對於 `Method1Async(string param, object userState)` 的每個呼叫，一般都會產生新的、唯一的 `userState` 物件，並將該物件加入至集合中。</span><span class="sxs-lookup"><span data-stu-id="2cef0-150">For each call to `Method1Async(string param, object userState)`, you will typically generate a new, unique `userState` object and add it to a collection.</span></span> <span data-ttu-id="2cef0-151">當對應至這個 `userState` 物件的工作引發完成事件時，完成方法實作就會檢查 <xref:System.ComponentModel.AsyncCompletedEventArgs.UserState%2A?displayProperty=nameWithType>，並將它從您的集合中移除。</span><span class="sxs-lookup"><span data-stu-id="2cef0-151">When the task corresponding to this `userState` object raises the completion event, your completion method implementation will examine <xref:System.ComponentModel.AsyncCompletedEventArgs.UserState%2A?displayProperty=nameWithType> and remove it from your collection.</span></span> <span data-ttu-id="2cef0-152">如果使用這種方式，`userState` 參數就會成為工作 ID。</span><span class="sxs-lookup"><span data-stu-id="2cef0-152">Used this way, the `userState` parameter takes the role of a task ID.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="2cef0-153">在對多個引動過程多載的呼叫中，請務必謹慎地為 `userState` 提供唯一值。</span><span class="sxs-lookup"><span data-stu-id="2cef0-153">You must be careful to provide a unique value for `userState` in your calls to multiple-invocation overloads.</span></span> <span data-ttu-id="2cef0-154">非唯一的工作 ID 將會使非同步類別擲回 <xref:System.ArgumentException>。</span><span class="sxs-lookup"><span data-stu-id="2cef0-154">Non-unique task IDs will cause the asynchronous class throw an <xref:System.ArgumentException>.</span></span>  
  
### <a name="canceling-pending-operations"></a><span data-ttu-id="2cef0-155">取消暫止的作業</span><span class="sxs-lookup"><span data-stu-id="2cef0-155">Canceling Pending Operations</span></span>  
 <span data-ttu-id="2cef0-156">在非同步作業完成之前，隨時都能取消這些作業是非常重要的。</span><span class="sxs-lookup"><span data-stu-id="2cef0-156">It is important to be able to cancel asynchronous operations at any time before their completion.</span></span> <span data-ttu-id="2cef0-157">實作事件架構非同步模式的類別會具有 `CancelAsync` 方法 (如果只有一個非同步方法) 或 _MethodName_**AsyncCancel** 方法 (如果有多個非同步方法)。</span><span class="sxs-lookup"><span data-stu-id="2cef0-157">Classes that implement the Event-based Asynchronous Pattern will have a `CancelAsync` method (if there is only one asynchronous method) or a _MethodName_**AsyncCancel** method (if there are multiple asynchronous methods).</span></span>  
  
 <span data-ttu-id="2cef0-158">允許多個引動過程的方法使用 `userState` 參數，該參數可用於追蹤每個工作的存留期。</span><span class="sxs-lookup"><span data-stu-id="2cef0-158">Methods that allow multiple invocations take a `userState` parameter, which can be used to track the lifetime of each task.</span></span> <span data-ttu-id="2cef0-159">`CancelAsync` 使用 `userState` 參數，該參數可讓您取消特定的暫止工作。</span><span class="sxs-lookup"><span data-stu-id="2cef0-159">`CancelAsync` takes a `userState` parameter, which allows you to cancel particular pending tasks.</span></span>  
  
 <span data-ttu-id="2cef0-160">您無法取消一次只能支援一個暫止作業的方法 (例如 `Method1Async(string param)`)。</span><span class="sxs-lookup"><span data-stu-id="2cef0-160">Methods that support only a single pending operation at a time, like `Method1Async(string param)`, are not cancelable.</span></span>  
  
### <a name="receiving-progress-updates-and-incremental-results"></a><span data-ttu-id="2cef0-161">接收進度更新和累加結果</span><span class="sxs-lookup"><span data-stu-id="2cef0-161">Receiving Progress Updates and Incremental Results</span></span>  
 <span data-ttu-id="2cef0-162">遵守事件架構非同步模式的類別，可能會選擇性地提供用來追蹤進度和累加結果的事件。</span><span class="sxs-lookup"><span data-stu-id="2cef0-162">A class that adheres to the Event-based Asynchronous Pattern may optionally provide an event for tracking progress and incremental results.</span></span> <span data-ttu-id="2cef0-163">這個事件通常會命名為 `ProgressChanged` 或 _MethodName_**ProgressChanged**，且它的對應事件處理常式將會使用 <xref:System.ComponentModel.ProgressChangedEventArgs> 參數。</span><span class="sxs-lookup"><span data-stu-id="2cef0-163">This will typically be named `ProgressChanged` or _MethodName_**ProgressChanged**, and its corresponding event handler will take a <xref:System.ComponentModel.ProgressChangedEventArgs> parameter.</span></span>  
  
 <span data-ttu-id="2cef0-164">`ProgressChanged` 事件的事件處理常式可以檢查 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A?displayProperty=nameWithType> 屬性，以判斷已經完成非同步工作的百分比。</span><span class="sxs-lookup"><span data-stu-id="2cef0-164">The event handler for the `ProgressChanged` event can examine the <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A?displayProperty=nameWithType> property to determine what percentage of an asynchronous task has been completed.</span></span> <span data-ttu-id="2cef0-165">這個屬性的範圍會介於 0 到 100 之間，並且可以用來更新 <xref:System.Windows.Forms.ProgressBar.Value%2A> 的 <xref:System.Windows.Forms.ProgressBar> 屬性。</span><span class="sxs-lookup"><span data-stu-id="2cef0-165">This property will range from 0 to 100, and it can be used to update the <xref:System.Windows.Forms.ProgressBar.Value%2A> property of a <xref:System.Windows.Forms.ProgressBar>.</span></span> <span data-ttu-id="2cef0-166">如果正在暫止多個非同步作業，您可以使用 <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A?displayProperty=nameWithType> 屬性來區別哪個作業在報告進度。</span><span class="sxs-lookup"><span data-stu-id="2cef0-166">If multiple asynchronous operations are pending, you can use the <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A?displayProperty=nameWithType> property to distinguish which operation is reporting progress.</span></span>  
  
 <span data-ttu-id="2cef0-167">有些類別可以在進行非同步作業時報告累加結果。</span><span class="sxs-lookup"><span data-stu-id="2cef0-167">Some classes may report incremental results as asynchronous operations proceed.</span></span> <span data-ttu-id="2cef0-168">這些結果將會儲存在衍生自 <xref:System.ComponentModel.ProgressChangedEventArgs> 的類別中，並且會顯示為衍生類別中的屬性。</span><span class="sxs-lookup"><span data-stu-id="2cef0-168">These results will be stored in a class that derives from <xref:System.ComponentModel.ProgressChangedEventArgs> and they will appear as properties in the derived class.</span></span> <span data-ttu-id="2cef0-169">您可以像是存取 `ProgressChanged` 屬性一般，存取 <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> 事件之事件處理常式中的這些結果。</span><span class="sxs-lookup"><span data-stu-id="2cef0-169">You can access these results in the event handler for the `ProgressChanged` event, just as you would access the <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> property.</span></span> <span data-ttu-id="2cef0-170">如果正在暫止多個非同步作業，您可以使用 <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A> 屬性來區別哪個作業在報告累加結果。</span><span class="sxs-lookup"><span data-stu-id="2cef0-170">If multiple asynchronous operations are pending, you can use the <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A> property to distinguish which operation is reporting incremental results.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2cef0-171">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2cef0-171">See also</span></span>

- <xref:System.ComponentModel.ProgressChangedEventArgs>
- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.AsyncCompletedEventArgs>
- [<span data-ttu-id="2cef0-172">如何：使用支援事件架構非同步模式的元件</span><span class="sxs-lookup"><span data-stu-id="2cef0-172">How to: Use Components That Support the Event-based Asynchronous Pattern</span></span>](how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="2cef0-173">操作說明：在背景執行作業</span><span class="sxs-lookup"><span data-stu-id="2cef0-173">How to: Run an Operation in the Background</span></span>](../../framework/winforms/controls/how-to-run-an-operation-in-the-background.md)
- [<span data-ttu-id="2cef0-174">操作說明：實作使用背景作業的表單</span><span class="sxs-lookup"><span data-stu-id="2cef0-174">How to: Implement a Form That Uses a Background Operation</span></span>](../../framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)
- [<span data-ttu-id="2cef0-175">事件架構非同步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="2cef0-175">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
- [<span data-ttu-id="2cef0-176">實作事件架構非同步模式的最佳作法</span><span class="sxs-lookup"><span data-stu-id="2cef0-176">Best Practices for Implementing the Event-based Asynchronous Pattern</span></span>](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="2cef0-177">決定何時實作事件架構非同步模式</span><span class="sxs-lookup"><span data-stu-id="2cef0-177">Deciding When to Implement the Event-based Asynchronous Pattern</span></span>](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)
