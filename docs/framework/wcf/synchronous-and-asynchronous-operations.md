---
title: 同步和非同步作業
description: 瞭解如何執行和呼叫非同步服務作業。 WCF 服務和用戶端可以在應用程式的兩個層級上使用非同步作業。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF], synchronous operations
- service contracts [WCF], asynchronous operations
ms.assetid: db8a51cb-67e6-411b-9035-e5821ed350c9
ms.openlocfilehash: f14e206bb99215a7a9b2535f99feb9971274532b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96254190"
---
# <a name="synchronous-and-asynchronous-operations"></a><span data-ttu-id="87886-104">同步和非同步作業</span><span class="sxs-lookup"><span data-stu-id="87886-104">Synchronous and Asynchronous Operations</span></span>

<span data-ttu-id="87886-105">本主題討論實作和呼叫非同步服務作業。</span><span class="sxs-lookup"><span data-stu-id="87886-105">This topic discusses implementing and calling asynchronous service operations.</span></span>  
  
 <span data-ttu-id="87886-106">許多應用程式會非同步呼叫方法，因為這麼做使應用程式可以在方法呼叫執行的同時繼續進行有用的工作。</span><span class="sxs-lookup"><span data-stu-id="87886-106">Many applications call methods asynchronously because it enables the application to continue doing useful work while the method call runs.</span></span> <span data-ttu-id="87886-107">Windows Communication Foundation (WCF) 服務和用戶端可以在應用程式兩個不同的特定層級參與非同步作業呼叫，這能讓 WCF 應用程式在互動性的權衡之下，具有更大的彈性將輸送量最大化。</span><span class="sxs-lookup"><span data-stu-id="87886-107">Windows Communication Foundation (WCF) services and clients can participate in asynchronous operation calls at two distinct levels of the application, which provide WCF applications even more flexibility to maximize throughput balanced against interactivity.</span></span>  
  
## <a name="types-of-asynchronous-operations"></a><span data-ttu-id="87886-108">非同步作業的類型</span><span class="sxs-lookup"><span data-stu-id="87886-108">Types of Asynchronous Operations</span></span>  

 <span data-ttu-id="87886-109">WCF 中的所有服務合約，無論參數型別和傳回值為何，都會使用 WCF 屬性來指定用戶端與服務之間的特定訊息交換模式。</span><span class="sxs-lookup"><span data-stu-id="87886-109">All service contracts in WCF, no matter the parameters types and return values, use WCF attributes to specify a particular message exchange pattern between client and service.</span></span> <span data-ttu-id="87886-110">WCF 會自動將傳入和傳出訊息路由傳送至適當的服務作業或正在執行的用戶端程式碼。</span><span class="sxs-lookup"><span data-stu-id="87886-110">WCF automatically routes inbound and outbound messages to the appropriate service operation or running client code.</span></span>  
  
 <span data-ttu-id="87886-111">用戶端僅擁有服務合約，而這個服務合約會指定特定作業的訊息交換模式。</span><span class="sxs-lookup"><span data-stu-id="87886-111">The client possesses only the service contract, which specifies the message exchange pattern for a particular operation.</span></span> <span data-ttu-id="87886-112">只要觀察到基礎訊息交換模式，用戶端便可以提供開發人員所選擇的程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="87886-112">Clients can offer the developer any programming model they choose, so long as the underlying message exchange pattern is observed.</span></span> <span data-ttu-id="87886-113">同樣的，只要觀察到指定的訊息模式，服務便可以任何方式實作作業。</span><span class="sxs-lookup"><span data-stu-id="87886-113">So, too, can services implement operations in any manner, so long as the specified message pattern is observed.</span></span>  
  
 <span data-ttu-id="87886-114">服務合約與服務或用戶端實作無關，而這樣的獨立性可在 WCF 應用程式中進行下列形式的非同步執行：</span><span class="sxs-lookup"><span data-stu-id="87886-114">The independence of the service contract from either the service or client implementation enables the following forms of asynchronous execution in WCF applications:</span></span>  
  
- <span data-ttu-id="87886-115">用戶端可以使用同步訊息交換，以非同步方式叫用要求/回應作業。</span><span class="sxs-lookup"><span data-stu-id="87886-115">Clients can invoke request/response operations asynchronously using a synchronous message exchange.</span></span>  
  
- <span data-ttu-id="87886-116">服務可以使用同步訊息交換，來以非同步方式實作要求/回應作業。</span><span class="sxs-lookup"><span data-stu-id="87886-116">Services can implement a request/response operation asynchronously using a synchronous message exchange.</span></span>  
  
- <span data-ttu-id="87886-117">不管用戶端或服務的實作如何，訊息交換可以是單向。</span><span class="sxs-lookup"><span data-stu-id="87886-117">Message exchanges can be one-way, regardless of the implementation of the client or service.</span></span>  
  
### <a name="suggested-asynchronous-scenarios"></a><span data-ttu-id="87886-118">建議的非同步案例</span><span class="sxs-lookup"><span data-stu-id="87886-118">Suggested Asynchronous Scenarios</span></span>  

 <span data-ttu-id="87886-119">如果作業服務實作發出封鎖呼叫 (例如進行 I/O 工作)，這時請在服務作業實作中使用非同步方法。</span><span class="sxs-lookup"><span data-stu-id="87886-119">Use an asynchronous approach in a service operation implementation if the operation service implementation makes a blocking call, such as doing I/O work.</span></span> <span data-ttu-id="87886-120">當您處於非同步作業實作中時，請嘗試呼叫非同步作業和方法，盡可能地延伸非同步呼叫路徑。</span><span class="sxs-lookup"><span data-stu-id="87886-120">When you are in an asynchronous operation implementation, try to call asynchronous operations and methods to extend the asynchronous call path as far as possible.</span></span> <span data-ttu-id="87886-121">例如，從 `BeginOperationTwo()` 內呼叫 `BeginOperationOne()`。</span><span class="sxs-lookup"><span data-stu-id="87886-121">For example, call a `BeginOperationTwo()` from within `BeginOperationOne()`.</span></span>  
  
- <span data-ttu-id="87886-122">在下列情況中，在用戶端中使用非同步化方法或呼叫應用程式：</span><span class="sxs-lookup"><span data-stu-id="87886-122">Use an asynchronous approach in a client or calling application in the following cases:</span></span>  
  
- <span data-ttu-id="87886-123">如果您是從中介層應用程式叫用作業。</span><span class="sxs-lookup"><span data-stu-id="87886-123">If you are invoking operations from a middle-tier application.</span></span> <span data-ttu-id="87886-124">(如需此類案例的詳細資訊，請參閱[中介層用戶端應用程式](./feature-details/middle-tier-client-applications.md))。</span><span class="sxs-lookup"><span data-stu-id="87886-124">(For more information about such scenarios, see [Middle-Tier Client Applications](./feature-details/middle-tier-client-applications.md).)</span></span>  
  
- <span data-ttu-id="87886-125">如果您是叫用 ASP.NET 頁面內的作業，請使用非同步頁面。</span><span class="sxs-lookup"><span data-stu-id="87886-125">If you are invoking operations within an ASP.NET page, use asynchronous pages.</span></span>  
  
- <span data-ttu-id="87886-126">如果您是從任何為單一執行緒的應用程式叫用作業，例如 Windows Forms 或 Windows Presentation Foundation (WPF)。</span><span class="sxs-lookup"><span data-stu-id="87886-126">If you are invoking operations from any application that is single threaded, such as Windows Forms or Windows Presentation Foundation (WPF).</span></span> <span data-ttu-id="87886-127">使用事件架構非同步呼叫模型時，結果事件會在 UI 執行緒上引發，並將回應新增至應用程式中，而不需要您自己去處理多個執行緒。</span><span class="sxs-lookup"><span data-stu-id="87886-127">When using the event-based asynchronous calling model, the result event is raised on the UI thread, adding responsiveness to the application without requiring you to handle multiple threads yourself.</span></span>  
  
- <span data-ttu-id="87886-128">一般而言，如果您在同步與非同步呼叫之間有選擇，請選擇非同步呼叫。</span><span class="sxs-lookup"><span data-stu-id="87886-128">In general, if you have a choice between a synchronous and asynchronous call, choose the asynchronous call.</span></span>  
  
### <a name="implementing-an-asynchronous-service-operation"></a><span data-ttu-id="87886-129">實作非同步服務作業</span><span class="sxs-lookup"><span data-stu-id="87886-129">Implementing an Asynchronous Service Operation</span></span>  

 <span data-ttu-id="87886-130">您可以使用下列三個方法的其中一個來實作非同步服務作業：</span><span class="sxs-lookup"><span data-stu-id="87886-130">Asynchronous operations can be implemented by using one of the three following methods:</span></span>  
  
1. <span data-ttu-id="87886-131">工作架構非同步模式</span><span class="sxs-lookup"><span data-stu-id="87886-131">The task-based asynchronous pattern</span></span>  
  
2. <span data-ttu-id="87886-132">事件架構非同步模式</span><span class="sxs-lookup"><span data-stu-id="87886-132">The event-based asynchronous pattern</span></span>  
  
3. <span data-ttu-id="87886-133">IAsyncResult 非同步模式</span><span class="sxs-lookup"><span data-stu-id="87886-133">The IAsyncResult asynchronous pattern</span></span>  
  
#### <a name="task-based-asynchronous-pattern"></a><span data-ttu-id="87886-134">以工作為基礎的非同步模式</span><span class="sxs-lookup"><span data-stu-id="87886-134">Task-Based Asynchronous Pattern</span></span>  

 <span data-ttu-id="87886-135">工作架構非同步模式是實作非同步作業的慣用方式，因為這是最簡單且最直接的方式。</span><span class="sxs-lookup"><span data-stu-id="87886-135">The task-based asynchronous pattern is the preferred way to implement asynchronous operations because it is the easiest and most straight forward.</span></span> <span data-ttu-id="87886-136">若要使用這個方法，只需執行您的服務作業並指定工作的 \<T> 傳回型別，其中 T 是邏輯作業傳回的型別。</span><span class="sxs-lookup"><span data-stu-id="87886-136">To use this method simply implement your service operation and specify a return type of Task\<T>, where T is the type returned by the logical operation.</span></span> <span data-ttu-id="87886-137">例如：</span><span class="sxs-lookup"><span data-stu-id="87886-137">For example:</span></span>  
  
```csharp  
public class SampleService:ISampleService
{
   // ...  
   public async Task<string> SampleMethodTaskAsync(string msg)
   {
      return Task<string>.Factory.StartNew(() =>
      {
         return msg;
      });
   }  
   // ...  
}  
```  
  
 <span data-ttu-id="87886-138">SampleMethodTaskAsync 作業會傳回 Task，因為邏輯作業會傳回 \<string> 字串。</span><span class="sxs-lookup"><span data-stu-id="87886-138">The SampleMethodTaskAsync operation returns Task\<string> because the logical operation returns a string.</span></span> <span data-ttu-id="87886-139">如需工作架構非同步模式的詳細資訊，請參閱[工作架構非同步模式](https://go.microsoft.com/fwlink/?LinkId=232504) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="87886-139">For more information about the task-based asynchronous pattern, see [The Task-Based Asynchronous Pattern](https://go.microsoft.com/fwlink/?LinkId=232504).</span></span>  
  
> [!WARNING]
> <span data-ttu-id="87886-140">使用工作架構非同步模式時，如果在等待作業完成期間發生例外狀況，則可能擲回 T:System.AggregateException。</span><span class="sxs-lookup"><span data-stu-id="87886-140">When using the task-based asynchronous pattern, a T:System.AggregateException may be thrown if an exception occurs while waiting on the completion of the operation.</span></span> <span data-ttu-id="87886-141">這個例外狀況可能在用戶端或服務上發生</span><span class="sxs-lookup"><span data-stu-id="87886-141">This exception may occur on the client or services</span></span>  
  
#### <a name="event-based-asynchronous-pattern"></a><span data-ttu-id="87886-142">事件架構非同步模式</span><span class="sxs-lookup"><span data-stu-id="87886-142">Event-Based Asynchronous Pattern</span></span>  

 <span data-ttu-id="87886-143">支援事件架構非同步模式的服務會有一個或多個名為 MethodNameAsync 的方法。</span><span class="sxs-lookup"><span data-stu-id="87886-143">A service that supports the Event-based Asynchronous Pattern will have one or more operations named MethodNameAsync.</span></span> <span data-ttu-id="87886-144">這些方法可能鏡像在目前執行緒上執行相同作業的同步版本。</span><span class="sxs-lookup"><span data-stu-id="87886-144">These methods may mirror synchronous versions, which perform the same operation on the current thread.</span></span> <span data-ttu-id="87886-145">這個類別可能也具有 MethodNameCompleted 事件，並且具有 MethodNameAsyncCancel (或簡單地說 CancelAsync) 方法。</span><span class="sxs-lookup"><span data-stu-id="87886-145">The class may also have a MethodNameCompleted event and it may have a MethodNameAsyncCancel (or simply CancelAsync) method.</span></span> <span data-ttu-id="87886-146">想要呼叫作業的用戶端將會定義要在作業完成時呼叫的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="87886-146">A client wishing to call the operation will define an event handler to be called when the operation completes,</span></span>  
  
 <span data-ttu-id="87886-147">下列程式碼片段示範如何使用事件架構非同步模式宣告非同步作業。</span><span class="sxs-lookup"><span data-stu-id="87886-147">The following code snippet illustrates how to declare asynchronous operations using the event-based asynchronous pattern.</span></span>  
  
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
  
 <span data-ttu-id="87886-148">如需事件架構非同步模式的詳細資訊，請參閱[事件架構非同步模式](../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="87886-148">For more information about the Event-based Asynchronous Pattern, see [The Event-Based Asynchronous Pattern](../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md).</span></span>  
  
#### <a name="iasyncresult-asynchronous-pattern"></a><span data-ttu-id="87886-149">IAsyncResult 非同步模式</span><span class="sxs-lookup"><span data-stu-id="87886-149">IAsyncResult Asynchronous Pattern</span></span>  

 <span data-ttu-id="87886-150">您可以使用 .NET Framework 非同步程式設計模式，並將 `<Begin>` <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> 屬性設定為，以非同步方式執行服務作業 `true` 。</span><span class="sxs-lookup"><span data-stu-id="87886-150">A service operation can be implemented in an asynchronous fashion using the .NET Framework asynchronous programming pattern and marking the `<Begin>` method with the <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> property set to `true`.</span></span> <span data-ttu-id="87886-151">在此情況下，會使用和同步作業相同的形式，在中繼資料中公開非同步作業：非同步作業會公開為具有要求訊息和相關聯之回應訊息的單一作業。</span><span class="sxs-lookup"><span data-stu-id="87886-151">In this case, the asynchronous operation is exposed in metadata in the same form as a synchronous operation: It is exposed as a single operation with a request message and a correlated response message.</span></span> <span data-ttu-id="87886-152">用戶端程式設計模型接著就會做出選擇。</span><span class="sxs-lookup"><span data-stu-id="87886-152">Client programming models then have a choice.</span></span> <span data-ttu-id="87886-153">只要在叫用服務時發生要求/回應訊息交換，這些程式設計模型就會將此模式表示為同步作業或非同步作業。</span><span class="sxs-lookup"><span data-stu-id="87886-153">They can represent this pattern as a synchronous operation or as an asynchronous one, so long as when the service is invoked a request-response message exchange takes place.</span></span>  
  
 <span data-ttu-id="87886-154">一般而言，基於系統的非同步本質，您不應該相依於執行緒。</span><span class="sxs-lookup"><span data-stu-id="87886-154">In general, with the asynchronous nature of the systems, you should not take a dependency on the threads.</span></span>  <span data-ttu-id="87886-155">將資料傳遞至作業分派處理之各種階段最可靠的方式就是使用延伸模組。</span><span class="sxs-lookup"><span data-stu-id="87886-155">The most reliable way of passing data to various stages of operation dispatch processing is to use extensions.</span></span>  
  
 <span data-ttu-id="87886-156">如需範例，請參閱[如何：實作非同步服務作業](how-to-implement-an-asynchronous-service-operation.md)。</span><span class="sxs-lookup"><span data-stu-id="87886-156">For an example, see [How to: Implement an Asynchronous Service Operation](how-to-implement-an-asynchronous-service-operation.md).</span></span>  
  
 <span data-ttu-id="87886-157">若不管在用戶端應用程式中呼叫合約作業的方式，而要定義以非同步方式執行的合約作業 `X`：</span><span class="sxs-lookup"><span data-stu-id="87886-157">To define a contract operation `X` that is executed asynchronously regardless of how it is called in the client application:</span></span>  
  
- <span data-ttu-id="87886-158">使用模式 `BeginOperation` 和 `EndOperation` 定義兩種方法。</span><span class="sxs-lookup"><span data-stu-id="87886-158">Define two methods using the pattern `BeginOperation` and `EndOperation`.</span></span>  
  
- <span data-ttu-id="87886-159">`BeginOperation` 方法包含用於作業的 `in` 和 `ref` 參數，並會傳回 <xref:System.IAsyncResult> 型別。</span><span class="sxs-lookup"><span data-stu-id="87886-159">The `BeginOperation` method includes `in` and `ref` parameters for the operation and returns an <xref:System.IAsyncResult> type.</span></span>  
  
- <span data-ttu-id="87886-160">`EndOperation` 方法包含 <xref:System.IAsyncResult> 參數、`out` 和 `ref` 參數，並會傳回作業的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="87886-160">The `EndOperation` method includes an <xref:System.IAsyncResult> parameter as well as the `out` and `ref` parameters and returns the operations return type.</span></span>  
  
 <span data-ttu-id="87886-161">以下列方法為例：</span><span class="sxs-lookup"><span data-stu-id="87886-161">For example, see the following method.</span></span>  
  
```csharp  
int DoWork(string data, ref string inout, out string outonly)  
```  
  
```vb  
Function DoWork(ByVal data As String, ByRef inout As String, _out outonly As out) As Integer  
```  
  
 <span data-ttu-id="87886-162">若要建立非同步作業，這兩個方法將會：</span><span class="sxs-lookup"><span data-stu-id="87886-162">To create an asynchronous operation, the two methods would be:</span></span>  
  
```csharp  
[OperationContract(AsyncPattern=true)]
IAsyncResult BeginDoWork(string data,
                         ref string inout,
                         AsyncCallback callback,
                         object state);
int EndDoWork(ref string inout, out string outonly, IAsyncResult result);  
```  
  
```vb  
<OperationContract(AsyncPattern := True)>
Function BeginDoWork(ByVal data As String, _
                     ByRef inout As String, _
                     ByVal callback As AsyncCallback, _
                     ByVal state As Object) As IAsyncResult
Function EndDoWork(ByRef inout As String, ByRef outonly As String, ByVal result As IAsyncResult) As Integer  
```  
  
> [!NOTE]
> <span data-ttu-id="87886-163"><xref:System.ServiceModel.OperationContractAttribute> 屬性只會套用至 `BeginDoWork` 方法。</span><span class="sxs-lookup"><span data-stu-id="87886-163">The <xref:System.ServiceModel.OperationContractAttribute> attribute is applied only to the `BeginDoWork` method.</span></span> <span data-ttu-id="87886-164">產生的合約具有一個名為 `DoWork` 的 WSDL 作業。</span><span class="sxs-lookup"><span data-stu-id="87886-164">The resulting contract has one WSDL operation named `DoWork`.</span></span>  
  
### <a name="client-side-asynchronous-invocations"></a><span data-ttu-id="87886-165">用戶端非同步叫用</span><span class="sxs-lookup"><span data-stu-id="87886-165">Client-Side Asynchronous Invocations</span></span>  

 <span data-ttu-id="87886-166">WCF 用戶端應用程式可以使用前述三個非同步呼叫模型中的任何一個模型</span><span class="sxs-lookup"><span data-stu-id="87886-166">A WCF client application can use any of three asynchronous calling models described previously</span></span>  
  
 <span data-ttu-id="87886-167">使用工作架構模型時，只需使用 await 關鍵字呼叫作業，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="87886-167">When using the task-based model, simply call the operation using the await keyword as shown in the following code snippet.</span></span>  
  
```csharp  
await simpleServiceClient.SampleMethodTaskAsync("hello, world");  
```  
  
 <span data-ttu-id="87886-168">使用事件架構非同步模式時，只需要加入事件處理常式以接收回應的通知 -- 結果事件會自動在使用者介面執行緒上引發。</span><span class="sxs-lookup"><span data-stu-id="87886-168">Using the event-based asynchronous pattern only requires adding an event handler to receive a notification of the response -- and the resulting event is raised on the user interface thread automatically.</span></span> <span data-ttu-id="87886-169">若要使用此方法，請使用 [ServiceModel 中繼資料公用程式工具 (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md) 同時指定 **/async** 和 **/tcv:Version35** 命令選項，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="87886-169">To use this approach, specify both the **/async** and **/tcv:Version35** command options with the [ServiceModel Metadata Utility Tool (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md), as in the following example.</span></span>  
  
```console  
svcutil http://localhost:8000/servicemodelsamples/service/mex /async /tcv:Version35  
```  
  
 <span data-ttu-id="87886-170">當完成時，Svcutil.exe 會產生 WCF 用戶端類別，其中的事件基礎結構能夠呼叫應用程式去實作與指派事件處理常式，以接收回應並採取適當的動作。</span><span class="sxs-lookup"><span data-stu-id="87886-170">When this is done, Svcutil.exe generates a WCF client class with the event infrastructure that enables the calling application to implement and assign an event handler to receive the response and take the appropriate action.</span></span> <span data-ttu-id="87886-171">如需完整範例，請參閱[如何：以非同步方式呼叫服務作業](./feature-details/how-to-call-wcf-service-operations-asynchronously.md)。</span><span class="sxs-lookup"><span data-stu-id="87886-171">For a complete example, see [How to: Call Service Operations Asynchronously](./feature-details/how-to-call-wcf-service-operations-asynchronously.md).</span></span>  
  
 <span data-ttu-id="87886-172">不過，事件架構非同步模型僅適用于 .NET Framework 3.5。</span><span class="sxs-lookup"><span data-stu-id="87886-172">The event-based asynchronous model, however, is only available in .NET Framework 3.5.</span></span> <span data-ttu-id="87886-173">此外，在使用建立 WCF 用戶端通道時，即使在 .NET Framework 3.5 中也不支援 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="87886-173">In addition, it is not supported even in .NET Framework 3.5 when a WCF client channel is created by using a <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType>.</span></span> <span data-ttu-id="87886-174">透過 WCF 用戶端通道物件，您必須使用 <xref:System.IAsyncResult?displayProperty=nameWithType> 物件以非同步方式叫用您的作業。</span><span class="sxs-lookup"><span data-stu-id="87886-174">With WCF client channel objects, you must use <xref:System.IAsyncResult?displayProperty=nameWithType> objects to invoke your operations asynchronously.</span></span> <span data-ttu-id="87886-175">若要使用此方法，請使用 [ServiceModel 中繼資料公用程式工具 (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md) 指定 **/async** 命令選項，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="87886-175">To use this approach, specify the **/async** command option with the [ServiceModel Metadata Utility Tool (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md), as in the following example.</span></span>  
  
```console  
svcutil http://localhost:8000/servicemodelsamples/service/mex /async
```  
  
 <span data-ttu-id="87886-176">這會產生服務合約，其中的每個作業會模型化為其 `<Begin>` 屬性會設為 <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> 的 `true` 方法，和對應的 `<End>` 方法。</span><span class="sxs-lookup"><span data-stu-id="87886-176">This generates a service contract in which each operation is modeled as a `<Begin>` method with the <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> property set to `true` and a corresponding `<End>` method.</span></span> <span data-ttu-id="87886-177">如需使用 <xref:System.ServiceModel.ChannelFactory%601> 的完整範例，請參閱[如何：使用通道處理站以非同步方式呼叫作業](./feature-details/how-to-call-operations-asynchronously-using-a-channel-factory.md)。</span><span class="sxs-lookup"><span data-stu-id="87886-177">For a complete example using a <xref:System.ServiceModel.ChannelFactory%601>, see [How to: Call Operations Asynchronously Using a Channel Factory](./feature-details/how-to-call-operations-asynchronously-using-a-channel-factory.md).</span></span>  
  
 <span data-ttu-id="87886-178">無論何種情況下，即使是以同步方式實作服務，應用程式仍可以使用非同步方式叫用作業，而透過相同的方式，應用程式可以使用相同的模式，以非同步方式叫用本機同步方法。</span><span class="sxs-lookup"><span data-stu-id="87886-178">In either case, applications can invoke an operation asynchronously even if the service is implemented synchronously, in the same way that an application can use the same pattern to invoke asynchronously a local synchronous method.</span></span> <span data-ttu-id="87886-179">作業的執行方式對用戶端來說並不重要;當回應訊息送達時，其內容會分派至用戶端的非同步 <`End`> 方法，而用戶端會抓取資訊。</span><span class="sxs-lookup"><span data-stu-id="87886-179">How the operation is implemented is not significant to the client; when the response message arrives, its content is dispatched to the client's asynchronous <`End`> method and the client retrieves the information.</span></span>  
  
### <a name="one-way-message-exchange-patterns"></a><span data-ttu-id="87886-180">單向訊息交換模式</span><span class="sxs-lookup"><span data-stu-id="87886-180">One-Way Message Exchange Patterns</span></span>  

 <span data-ttu-id="87886-181">您也可以建立非同步訊息交換模式，而在這個模式中，用戶端或服務可以不管另一端，以任何方向傳送單向作業 (這是 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=nameWithType> 為 `true` 的作業，而且沒有相關聯的回應) </span><span class="sxs-lookup"><span data-stu-id="87886-181">You can also create an asynchronous message exchange pattern in which one-way operations (operations for which the <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=nameWithType> is `true` have no correlated response) can be sent in either direction by the client or service independently of the other side.</span></span> <span data-ttu-id="87886-182"> (這種情況下，會使用雙工訊息交換模式搭配單向訊息 ) 。在此情況下，服務合約會指定單向訊息交換，讓任一端都能以非同步呼叫或實作為方式來執行，或不適當的方式。</span><span class="sxs-lookup"><span data-stu-id="87886-182">(This uses the duplex message exchange pattern with one-way messages.) In this case, the service contract specifies a one-way message exchange that either side can implement as asynchronous calls or implementations, or not, as appropriate.</span></span> <span data-ttu-id="87886-183">一般來說，當合約為單向訊息交換時，就可以大量地非同步實作，因為一旦傳送訊息時，應用程式不會等待回覆就可繼續執行其他工作。</span><span class="sxs-lookup"><span data-stu-id="87886-183">Generally, when the contract is an exchange of one-way messages, the implementations can largely be asynchronous because once a message is sent the application does not wait for a reply and can continue doing other work.</span></span>  
  
### <a name="event-based-asynchronous-clients-and-message-contracts"></a><span data-ttu-id="87886-184">事件架構非同步用戶端和訊息合約</span><span class="sxs-lookup"><span data-stu-id="87886-184">Event-based Asynchronous Clients and Message Contracts</span></span>  

 <span data-ttu-id="87886-185">事件架構非同步模型的設計方針指出，如果傳回多個值，則其中一個值會傳回做為 `Result` 屬性，其他值則傳回做為 <xref:System.EventArgs> 物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="87886-185">The design guidelines for the event-based asynchronous model state that if more than one value is returned, one value is returned as the `Result` property and the others are returned as properties on the <xref:System.EventArgs> object.</span></span> <span data-ttu-id="87886-186">這麼做的結果就是，如果用戶端使用事件架構非同步命令選項匯入中繼資料，且作業傳回多個值，則預設 <xref:System.EventArgs> 物件會傳回一個值做為 `Result` 屬性，而其餘則做為 <xref:System.EventArgs> 物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="87886-186">One result of this is that if a client imports metadata using the event-based asynchronous command options and the operation returns more than one value, the default <xref:System.EventArgs> object returns one value as the `Result` property and the remainder are properties of the <xref:System.EventArgs> object.</span></span>  
  
 <span data-ttu-id="87886-187">如果您要以 `Result` 屬性的形式接收訊息物件，並讓傳回值以該物件屬性的形式呈現，請使用 **/messageContract** 命令選項。</span><span class="sxs-lookup"><span data-stu-id="87886-187">If you want to receive the message object as the `Result` property and have the returned values as properties on that object, use the **/messageContract** command option.</span></span> <span data-ttu-id="87886-188">這會產生一個簽章，此簽章會將回應訊息傳回做為 `Result` 物件的 <xref:System.EventArgs> 屬性。</span><span class="sxs-lookup"><span data-stu-id="87886-188">This generates a signature that returns the response message as the `Result` property on the <xref:System.EventArgs> object.</span></span> <span data-ttu-id="87886-189">然後，所有的內部傳回值都成為回應訊息物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="87886-189">All internal return values are then properties of the response message object.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="87886-190">另請參閱</span><span class="sxs-lookup"><span data-stu-id="87886-190">See also</span></span>

- <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>
- <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A>
