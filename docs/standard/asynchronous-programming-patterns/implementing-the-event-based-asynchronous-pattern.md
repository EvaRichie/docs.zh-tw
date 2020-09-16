---
title: 實作事件架構非同步模式
description: 瞭解如何在 .NET 中執行以事件為基礎的非同步模式 (EAP) 。 EAP 是封裝具有非同步功能之類別的標準方式。
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
- components [.NET Framework], asynchronous
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 43402d19-8d30-426d-8785-1a4478233bfa
ms.openlocfilehash: 466a0dd8a827cd869894106a0901bdab89601e25
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90559092"
---
# <a name="implementing-the-event-based-asynchronous-pattern"></a><span data-ttu-id="70de8-104">實作事件架構非同步模式</span><span class="sxs-lookup"><span data-stu-id="70de8-104">Implementing the Event-based Asynchronous Pattern</span></span>

<span data-ttu-id="70de8-105">如果您要撰寫的類別具有某些可能會造成明顯延遲的作業，請考慮藉由執行事件架構 [非同步模式](event-based-asynchronous-pattern-overview.md)，為其提供非同步功能。</span><span class="sxs-lookup"><span data-stu-id="70de8-105">If you are writing a class with some operations that may incur noticeable delays, consider giving it asynchronous functionality by implementing the [Event-based Asynchronous Pattern](event-based-asynchronous-pattern-overview.md).</span></span>

<span data-ttu-id="70de8-106">事件架構非同步模式提供標準化方式來封裝具有非同步功能的類別。</span><span class="sxs-lookup"><span data-stu-id="70de8-106">The Event-based Asynchronous Pattern provides a standardized way to package a class that has asynchronous features.</span></span> <span data-ttu-id="70de8-107">您的類別若是使用協助程式類別 (例如 <xref:System.ComponentModel.AsyncOperationManager>) 來實作，就能夠在任何應用程式模型下正確運作，這些模型包括 ASP.NET、主控台應用程式和 Windows Forms 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70de8-107">If implemented with helper classes like <xref:System.ComponentModel.AsyncOperationManager>, your class will work correctly under any application model, including ASP.NET, Console applications, and Windows Forms applications.</span></span>

<span data-ttu-id="70de8-108">如需實作事件架構非同步模式的範例，請參閱[如何：實作支援事件架構非同步模式的元件](component-that-supports-the-event-based-asynchronous-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="70de8-108">For an example that implements the Event-based Asynchronous Pattern, see [How to: Implement a Component That Supports the Event-based Asynchronous Pattern](component-that-supports-the-event-based-asynchronous-pattern.md).</span></span>

<span data-ttu-id="70de8-109">您可能會發現 <xref:System.ComponentModel.BackgroundWorker> 元件適用於簡單的非同步作業。</span><span class="sxs-lookup"><span data-stu-id="70de8-109">For simple asynchronous operations, you may find the <xref:System.ComponentModel.BackgroundWorker> component suitable.</span></span> <span data-ttu-id="70de8-110">如需 <xref:System.ComponentModel.BackgroundWorker> 的詳細資訊，請參閱 [如何：在背景執行作業](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)。</span><span class="sxs-lookup"><span data-stu-id="70de8-110">For more information about <xref:System.ComponentModel.BackgroundWorker>, see [How to: Run an Operation in the Background](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background).</span></span>

<span data-ttu-id="70de8-111">下列清單所描述的事件架構非同步模式功能，本主題會加以討論。</span><span class="sxs-lookup"><span data-stu-id="70de8-111">The following list describes the features of the Event-based Asynchronous Pattern discussed in this topic.</span></span>

- <span data-ttu-id="70de8-112">實作事件架構非同步模式的機會</span><span class="sxs-lookup"><span data-stu-id="70de8-112">Opportunities for Implementing the Event-based Asynchronous Pattern</span></span>

- <span data-ttu-id="70de8-113">為非同步方法命名</span><span class="sxs-lookup"><span data-stu-id="70de8-113">Naming Asynchronous Methods</span></span>

- <span data-ttu-id="70de8-114">選擇性地支援取消方法</span><span class="sxs-lookup"><span data-stu-id="70de8-114">Optionally Support Cancellation</span></span>

- <span data-ttu-id="70de8-115">選擇性地支援 IsBusy 屬性</span><span class="sxs-lookup"><span data-stu-id="70de8-115">Optionally Support the IsBusy Property</span></span>

- <span data-ttu-id="70de8-116">選擇性地提供進度報告支援</span><span class="sxs-lookup"><span data-stu-id="70de8-116">Optionally Provide Support for Progress Reporting</span></span>

- <span data-ttu-id="70de8-117">選擇性地提供可傳回累加結果的支援</span><span class="sxs-lookup"><span data-stu-id="70de8-117">Optionally Provide Support for Returning Incremental Results</span></span>

- <span data-ttu-id="70de8-118">在方法中處理 Out 和 Ref 參數</span><span class="sxs-lookup"><span data-stu-id="70de8-118">Handling Out and Ref Parameters in Methods</span></span>

## <a name="opportunities-for-implementing-the-event-based-asynchronous-pattern"></a><span data-ttu-id="70de8-119">實作事件架構非同步模式的機會</span><span class="sxs-lookup"><span data-stu-id="70de8-119">Opportunities for Implementing the Event-based Asynchronous Pattern</span></span>

<span data-ttu-id="70de8-120">若有下列情況，請考慮實作事件架構非同步模式：</span><span class="sxs-lookup"><span data-stu-id="70de8-120">Consider implementing the Event-based Asynchronous Pattern when:</span></span>

- <span data-ttu-id="70de8-121">類別的用戶端不需要非同步作業可使用 <xref:System.Threading.WaitHandle> 和 <xref:System.IAsyncResult> 物件，這表示輪詢和 <xref:System.Threading.WaitHandle.WaitAll%2A> 或 <xref:System.Threading.WaitHandle.WaitAny%2A> 都必須由用戶端所建立。</span><span class="sxs-lookup"><span data-stu-id="70de8-121">Clients of your class do not need <xref:System.Threading.WaitHandle> and <xref:System.IAsyncResult> objects available for asynchronous operations, meaning that polling and <xref:System.Threading.WaitHandle.WaitAll%2A> or <xref:System.Threading.WaitHandle.WaitAny%2A> will need to be built up by the client.</span></span>

- <span data-ttu-id="70de8-122">您想要由用戶端使用熟悉的事件/委派模型來管理非同步作業。</span><span class="sxs-lookup"><span data-stu-id="70de8-122">You want asynchronous operations to be managed by the client with the familiar event/delegate model.</span></span>

<span data-ttu-id="70de8-123">任何作業都適合進行非同步實作，但您應該考慮那些預期會產生較長延遲的作業。</span><span class="sxs-lookup"><span data-stu-id="70de8-123">Any operation is a candidate for an asynchronous implementation, but those you expect to incur long latencies should be considered.</span></span> <span data-ttu-id="70de8-124">用戶端會呼叫方法並在完成時收到通知的作業尤其適合，因為您不必進一步介入。</span><span class="sxs-lookup"><span data-stu-id="70de8-124">Especially appropriate are operations in which clients call a method and are notified on completion, with no further intervention required.</span></span> <span data-ttu-id="70de8-125">會持續執行，並定期將進度、累加結果或狀態變更通知用戶端的作業也很適合。</span><span class="sxs-lookup"><span data-stu-id="70de8-125">Also appropriate are operations which run continuously, periodically notifying clients of progress, incremental results, or state changes.</span></span>

<span data-ttu-id="70de8-126">如需有關如何決定何時該支援事件架構非同步模式的詳細資訊，請參閱[決定何時實作事件架構非同步模式](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)。</span><span class="sxs-lookup"><span data-stu-id="70de8-126">For more information on deciding when to support the Event-based Asynchronous Pattern, see [Deciding When to Implement the Event-based Asynchronous Pattern](deciding-when-to-implement-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="naming-asynchronous-methods"></a><span data-ttu-id="70de8-127">為非同步方法命名</span><span class="sxs-lookup"><span data-stu-id="70de8-127">Naming Asynchronous Methods</span></span>

<span data-ttu-id="70de8-128">對於您要為其提供非同步對應的每一個 MethodName\*\* 同步方法：</span><span class="sxs-lookup"><span data-stu-id="70de8-128">For each synchronous method *MethodName* for which you want to provide an asynchronous counterpart:</span></span>

<span data-ttu-id="70de8-129">定義_方法方法_的**非同步**方法：</span><span class="sxs-lookup"><span data-stu-id="70de8-129">Define a _MethodName_**Async** method that:</span></span>

- <span data-ttu-id="70de8-130">傳回 `void`。</span><span class="sxs-lookup"><span data-stu-id="70de8-130">Returns `void`.</span></span>

- <span data-ttu-id="70de8-131">使用與 MethodName\*\* 方法相同的參數。</span><span class="sxs-lookup"><span data-stu-id="70de8-131">Takes the same parameters as the *MethodName* method.</span></span>

- <span data-ttu-id="70de8-132">接受多個引動過程。</span><span class="sxs-lookup"><span data-stu-id="70de8-132">Accepts multiple invocations.</span></span>

<span data-ttu-id="70de8-133">（選擇性）定義 _方法名稱_**非同步** 多載，與 _方法名稱_**相同，但**有一個稱為的額外物件值參數 `userState` 。</span><span class="sxs-lookup"><span data-stu-id="70de8-133">Optionally define a _MethodName_**Async** overload, identical to _MethodName_**Async**, but with an additional object-valued parameter called `userState`.</span></span> <span data-ttu-id="70de8-134">需要這麼做的前提是，您已準備好管理您擁有之方法的多個並行引動過程，在此情況下，`userState` 值會傳回給所有的事件處理常式，以供區別該方法的各個引動過程。</span><span class="sxs-lookup"><span data-stu-id="70de8-134">Do this if you're prepared to manage multiple concurrent invocations of your method, in which case the `userState` value will be delivered back to all event handlers to distinguish invocations of the method.</span></span> <span data-ttu-id="70de8-135">您也可以純粹為了能有位置可儲存使用者狀態以供日後擷取，而選擇這樣做。</span><span class="sxs-lookup"><span data-stu-id="70de8-135">You may also choose to do this simply as a place to store user state for later retrieval.</span></span>

<span data-ttu-id="70de8-136">針對每個個別的_方法名稱_，**非同步**方法簽章：</span><span class="sxs-lookup"><span data-stu-id="70de8-136">For each separate _MethodName_**Async** method signature:</span></span>

1. <span data-ttu-id="70de8-137">在相同的類別中定義下列事件來作為方法︰</span><span class="sxs-lookup"><span data-stu-id="70de8-137">Define the following event in the same class as the method:</span></span>

    ```vb
    Public Event MethodNameCompleted As MethodNameCompletedEventHandler
    ```

    ```csharp
    public event MethodNameCompletedEventHandler MethodNameCompleted;
    ```

2. <span data-ttu-id="70de8-138">定義下列委派和 <xref:System.ComponentModel.AsyncCompletedEventArgs>。</span><span class="sxs-lookup"><span data-stu-id="70de8-138">Define the following delegate and <xref:System.ComponentModel.AsyncCompletedEventArgs>.</span></span> <span data-ttu-id="70de8-139">此外，這些項目可能會在類別本身之外來定義，但會在相同的命名空間中。</span><span class="sxs-lookup"><span data-stu-id="70de8-139">These will likely be defined outside of the class itself, but in the same namespace.</span></span>

    ```vb
    Public Delegate Sub MethodNameCompletedEventHandler( _
        ByVal sender As Object, _
        ByVal e As MethodNameCompletedEventArgs)

    Public Class MethodNameCompletedEventArgs
        Inherits System.ComponentModel.AsyncCompletedEventArgs
    Public ReadOnly Property Result() As MyReturnType
    End Property
    ```

    ```csharp
    public delegate void MethodNameCompletedEventHandler(object sender,
        MethodNameCompletedEventArgs e);

    public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs
    {
        public MyReturnType Result { get; }
    }
    ```

    - <span data-ttu-id="70de8-140">確定 _方法_**>completedeventargs** 類別會將其成員公開為唯讀屬性，而不是欄位，因為欄位會防止資料系結。</span><span class="sxs-lookup"><span data-stu-id="70de8-140">Ensure that the _MethodName_**CompletedEventArgs** class exposes its members as read-only properties, and not fields, as fields prevent data binding.</span></span>

    - <span data-ttu-id="70de8-141">不要為不會產生結果的方法定義任何 <xref:System.ComponentModel.AsyncCompletedEventArgs> 衍生類別。</span><span class="sxs-lookup"><span data-stu-id="70de8-141">Do not define any <xref:System.ComponentModel.AsyncCompletedEventArgs>-derived classes for methods that do not produce results.</span></span> <span data-ttu-id="70de8-142">只要使用 <xref:System.ComponentModel.AsyncCompletedEventArgs> 本身的執行個體。</span><span class="sxs-lookup"><span data-stu-id="70de8-142">Simply use an instance of <xref:System.ComponentModel.AsyncCompletedEventArgs> itself.</span></span>

      > [!NOTE]
      > <span data-ttu-id="70de8-143">只要可行且適當，重複使用委派和 <xref:System.ComponentModel.AsyncCompletedEventArgs> 型別也是完全可以接受的。</span><span class="sxs-lookup"><span data-stu-id="70de8-143">It is perfectly acceptable, when feasible and appropriate, to reuse delegate and <xref:System.ComponentModel.AsyncCompletedEventArgs> types.</span></span> <span data-ttu-id="70de8-144">在此情況下，其命名將不會與方法名稱一致，因為給定的委派和 <xref:System.ComponentModel.AsyncCompletedEventArgs> 不會繫結至單一方法。</span><span class="sxs-lookup"><span data-stu-id="70de8-144">In this case, the naming will not be as consistent with the method name, since a given delegate and <xref:System.ComponentModel.AsyncCompletedEventArgs> won't be tied to a single method.</span></span>

## <a name="optionally-support-cancellation"></a><span data-ttu-id="70de8-145">選擇性地支援取消方法</span><span class="sxs-lookup"><span data-stu-id="70de8-145">Optionally Support Cancellation</span></span>

<span data-ttu-id="70de8-146">如果您的類別會支援取消非同步作業，請如下所述對用戶端公開取消方法。</span><span class="sxs-lookup"><span data-stu-id="70de8-146">If your class will support canceling asynchronous operations, cancellation should be exposed to the client as described below.</span></span> <span data-ttu-id="70de8-147">請注意，在定義取消支援之前，您必須先達成兩個決策點︰</span><span class="sxs-lookup"><span data-stu-id="70de8-147">Note that there are two decision points that need to be reached before defining your cancellation support:</span></span>

- <span data-ttu-id="70de8-148">您的類別 (包括其未來預期的新增項目) 是否只有一個支援取消方法的非同步作業？</span><span class="sxs-lookup"><span data-stu-id="70de8-148">Does your class, including future anticipated additions to it, have only one asynchronous operation that supports cancellation?</span></span>

- <span data-ttu-id="70de8-149">可支援取消方法的非同步作業能否支援多個暫止作業？</span><span class="sxs-lookup"><span data-stu-id="70de8-149">Can the asynchronous operations that support cancellation support multiple pending operations?</span></span> <span data-ttu-id="70de8-150">也就是說，方法方法的_MethodName_**非同步**方法是否接受 `userState` 參數，並在等候任何作業完成之前允許多個調用？</span><span class="sxs-lookup"><span data-stu-id="70de8-150">That is, does the _MethodName_**Async** method take a `userState` parameter, and does it allow multiple invocations before waiting for any to finish?</span></span>

<span data-ttu-id="70de8-151">使用下表中對於這兩個問題的回答，來判斷您的取消方法應該使用的簽章。</span><span class="sxs-lookup"><span data-stu-id="70de8-151">Use the answers to these two questions in the table below to determine what the signature for your cancellation method should be.</span></span>

### <a name="visual-basic"></a><span data-ttu-id="70de8-152">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="70de8-152">Visual Basic</span></span>

||<span data-ttu-id="70de8-153">支援多個同時作業</span><span class="sxs-lookup"><span data-stu-id="70de8-153">Multiple Simultaneous Operations Supported</span></span>|<span data-ttu-id="70de8-154">一次只有一個作業</span><span class="sxs-lookup"><span data-stu-id="70de8-154">Only One Operation at a Time</span></span>|
|------|------------------------------------------------|----------------------------------|
|<span data-ttu-id="70de8-155">整個類別只有一個非同步作業</span><span class="sxs-lookup"><span data-stu-id="70de8-155">One Async Operation in entire class</span></span>|`Sub MethodNameAsyncCancel(ByVal userState As Object)`|`Sub MethodNameAsyncCancel()`|
|<span data-ttu-id="70de8-156">類別中有多個非同步作業</span><span class="sxs-lookup"><span data-stu-id="70de8-156">Multiple Async Operations in class</span></span>|`Sub CancelAsync(ByVal userState As Object)`|`Sub CancelAsync()`|

### <a name="c"></a><span data-ttu-id="70de8-157">C\#</span><span class="sxs-lookup"><span data-stu-id="70de8-157">C\#</span></span>

||<span data-ttu-id="70de8-158">支援多個同時作業</span><span class="sxs-lookup"><span data-stu-id="70de8-158">Multiple Simultaneous Operations Supported</span></span>|<span data-ttu-id="70de8-159">一次只有一個作業</span><span class="sxs-lookup"><span data-stu-id="70de8-159">Only One Operation at a Time</span></span>|
|------|------------------------------------------------|----------------------------------|
|<span data-ttu-id="70de8-160">整個類別只有一個非同步作業</span><span class="sxs-lookup"><span data-stu-id="70de8-160">One Async Operation in entire class</span></span>|`void MethodNameAsyncCancel(object userState);`|`void MethodNameAsyncCancel();`|
|<span data-ttu-id="70de8-161">類別中有多個非同步作業</span><span class="sxs-lookup"><span data-stu-id="70de8-161">Multiple Async Operations in class</span></span>|`void CancelAsync(object userState);`|`void CancelAsync();`|

<span data-ttu-id="70de8-162">如果您定義 `CancelAsync(object userState)` 方法，用戶端必須小心地選擇它們的狀態值，以便能夠區別物件上所叫用的所有非同步方法，而不只是能夠區別單一非同步方法的所有引動過程。</span><span class="sxs-lookup"><span data-stu-id="70de8-162">If you define the `CancelAsync(object userState)` method, clients must be careful when choosing their state values to make them capable of distinguishing among all asynchronous methods invoked on the object, and not just between all invocations of a single asynchronous method.</span></span>

<span data-ttu-id="70de8-163">決定命名單一非同步 _操作版本的方法名稱_**>asynccancel** ，是根據能夠更輕鬆地在設計環境中探索方法，例如 Visual Studio 的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="70de8-163">The decision to name the single-async-operation version _MethodName_**AsyncCancel** is based on being able to more easily discover the method in a design environment like Visual Studio's IntelliSense.</span></span> <span data-ttu-id="70de8-164">這會將相關的成員群組在一起，並讓與非同步功能無關的其他成員可與它們區別開來。</span><span class="sxs-lookup"><span data-stu-id="70de8-164">This groups the related members and distinguishes them from other members that have nothing to do with asynchronous functionality.</span></span> <span data-ttu-id="70de8-165">如果您預期後續版本中可能會新增其他非同步作業，您最好要定義 `CancelAsync`。</span><span class="sxs-lookup"><span data-stu-id="70de8-165">If you expect that there may be additional asynchronous operations added in subsequent versions, it is better to define `CancelAsync`.</span></span>

<span data-ttu-id="70de8-166">請勿將上述表格中的多個方法定義到相同類別中。</span><span class="sxs-lookup"><span data-stu-id="70de8-166">Do not define multiple methods from the table above in the same class.</span></span> <span data-ttu-id="70de8-167">這麼做毫無意義，而且類別介面也會因為方法數量暴增而變得雜亂。</span><span class="sxs-lookup"><span data-stu-id="70de8-167">That will not make sense, or it will clutter the class interface with a proliferation of methods.</span></span>

<span data-ttu-id="70de8-168">這些方法通常會立即傳回，而且作業實際上不一定會取消。</span><span class="sxs-lookup"><span data-stu-id="70de8-168">These methods typically will return immediately, and the operation may or may not actually cancel.</span></span> <span data-ttu-id="70de8-169">在「 _方法名稱_**已完成** 」事件的事件處理常式中， _方法名稱_**>completedeventargs** 物件包含 `Cancelled` 欄位，用戶端可以使用此欄位來判斷是否發生取消。</span><span class="sxs-lookup"><span data-stu-id="70de8-169">In the event handler for the _MethodName_**Completed** event, the _MethodName_**CompletedEventArgs** object contains a `Cancelled` field, which clients can use to determine whether the cancellation occurred.</span></span>

<span data-ttu-id="70de8-170">請遵守[實作事件架構非同步模式的最佳作法](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)中所述的取消語意。</span><span class="sxs-lookup"><span data-stu-id="70de8-170">Abide by the cancellation semantics described in [Best Practices for Implementing the Event-based Asynchronous Pattern](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="optionally-support-the-isbusy-property"></a><span data-ttu-id="70de8-171">選擇性地支援 IsBusy 屬性</span><span class="sxs-lookup"><span data-stu-id="70de8-171">Optionally Support the IsBusy Property</span></span>

<span data-ttu-id="70de8-172">如果您的類別不支援多個並行引動過程，請考慮公開 `IsBusy` 屬性。</span><span class="sxs-lookup"><span data-stu-id="70de8-172">If your class does not support multiple concurrent invocations, consider exposing an `IsBusy` property.</span></span> <span data-ttu-id="70de8-173">這可讓開發人員判斷 _方法方法_**的非同步** 方法是否正在執行，而不會從 _方法方法_**非同步** 方法攔截例外狀況。</span><span class="sxs-lookup"><span data-stu-id="70de8-173">This allows developers to determine whether a _MethodName_**Async** method is running without catching an exception from the _MethodName_**Async** method.</span></span>

<span data-ttu-id="70de8-174">請遵守[實作事件架構非同步模式的最佳作法](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)中所述的 `IsBusy` 語意。</span><span class="sxs-lookup"><span data-stu-id="70de8-174">Abide by the `IsBusy` semantics described in [Best Practices for Implementing the Event-based Asynchronous Pattern](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="optionally-provide-support-for-progress-reporting"></a><span data-ttu-id="70de8-175">選擇性地提供進度報告支援</span><span class="sxs-lookup"><span data-stu-id="70de8-175">Optionally Provide Support for Progress Reporting</span></span>

<span data-ttu-id="70de8-176">非同步作業經常需要在其作業期間報告進度。</span><span class="sxs-lookup"><span data-stu-id="70de8-176">It is frequently desirable for an asynchronous operation to report progress during its operation.</span></span> <span data-ttu-id="70de8-177">事件架構非同步模式提供了這方面的指導方針。</span><span class="sxs-lookup"><span data-stu-id="70de8-177">The Event-based Asynchronous Pattern provides a guideline for doing so.</span></span>

- <span data-ttu-id="70de8-178">選擇性地定義要供非同步作業引發，並在適當的執行緒上叫用的事件。</span><span class="sxs-lookup"><span data-stu-id="70de8-178">Optionally define an event to be raised by the asynchronous operation and invoked on the appropriate thread.</span></span> <span data-ttu-id="70de8-179"><xref:System.ComponentModel.ProgressChangedEventArgs> 物件帶有以整數值表示的進度指示器，其值應該會介於 0 到 100 之間。</span><span class="sxs-lookup"><span data-stu-id="70de8-179">The <xref:System.ComponentModel.ProgressChangedEventArgs> object carries an integer-valued progress indicator that is expected to be between 0 and 100.</span></span>

- <span data-ttu-id="70de8-180">將此事件命名如下︰</span><span class="sxs-lookup"><span data-stu-id="70de8-180">Name this event as follows:</span></span>

  - <span data-ttu-id="70de8-181">`ProgressChanged`，如果類別具有多個非同步作業 (或預期會有成長，而會在未來的版本中包含多個非同步作業)。</span><span class="sxs-lookup"><span data-stu-id="70de8-181">`ProgressChanged` if the class has multiple asynchronous operations (or is expected to grow to include multiple asynchronous operations in future versions);</span></span>

  - <span data-ttu-id="70de8-182">如果類別具有單一非同步作業，則為_方法名稱_**>progresschanged** 。</span><span class="sxs-lookup"><span data-stu-id="70de8-182">_MethodName_**ProgressChanged** if the class has a single asynchronous operation.</span></span>

  <span data-ttu-id="70de8-183">這個命名選擇和取消方法的選擇類似，後者在＜選擇性地支援取消方法＞一節中有所說明。</span><span class="sxs-lookup"><span data-stu-id="70de8-183">This naming choice parallels that made for the cancellation method, as described in the Optionally Support Cancellation section.</span></span>

<span data-ttu-id="70de8-184">此事件應使用 <xref:System.ComponentModel.ProgressChangedEventHandler> 委派簽章和 <xref:System.ComponentModel.ProgressChangedEventArgs> 類別。</span><span class="sxs-lookup"><span data-stu-id="70de8-184">This event should use the <xref:System.ComponentModel.ProgressChangedEventHandler> delegate signature and the <xref:System.ComponentModel.ProgressChangedEventArgs> class.</span></span> <span data-ttu-id="70de8-185">或者，如果您可以提供更具網域特性的進度指示器 (例如，下載作業的已讀位元組數和位元組總數)，就應該定義 <xref:System.ComponentModel.ProgressChangedEventArgs> 的衍生類別。</span><span class="sxs-lookup"><span data-stu-id="70de8-185">Alternatively, if a more domain-specific progress indicator can be provided (for instance, bytes read and total bytes for a download operation), then you should define a derived class of <xref:System.ComponentModel.ProgressChangedEventArgs>.</span></span>

<span data-ttu-id="70de8-186">請注意 `ProgressChanged` ，此類別只有一個或 _方法_**>progresschanged** 事件，不論它支援的非同步方法數目為何。</span><span class="sxs-lookup"><span data-stu-id="70de8-186">Note that there is only one `ProgressChanged` or _MethodName_**ProgressChanged** event for the class, regardless of the number of asynchronous methods it supports.</span></span> <span data-ttu-id="70de8-187">用戶端預期會使用 `userState` 傳遞給 _方法名稱_**非同步** 方法的物件，來區別多個並行作業上的進度更新。</span><span class="sxs-lookup"><span data-stu-id="70de8-187">Clients are expected to use the `userState` object that is passed to the _MethodName_**Async** methods to distinguish among progress updates on multiple concurrent operations.</span></span>

<span data-ttu-id="70de8-188">有時候可能會有多個作業都支援進度報告，而各自傳回不同的進度指示器。</span><span class="sxs-lookup"><span data-stu-id="70de8-188">There may be situations in which multiple operations support progress and each returns a different indicator for progress.</span></span> <span data-ttu-id="70de8-189">在此情況下，使用單一的 `ProgressChanged` 事件就不是合適的作法，因此您可能會考慮支援多個 `ProgressChanged` 事件。</span><span class="sxs-lookup"><span data-stu-id="70de8-189">In this case, a single `ProgressChanged` event is not appropriate, and you may consider supporting multiple `ProgressChanged` events.</span></span> <span data-ttu-id="70de8-190">在此情況下，請針對每個_方法名稱_的**非同步**方法使用_方法名稱_**>progresschanged**的命名模式。</span><span class="sxs-lookup"><span data-stu-id="70de8-190">In this case use a naming pattern of _MethodName_**ProgressChanged** for each _MethodName_**Async** method.</span></span>

<span data-ttu-id="70de8-191">請遵守[實作事件架構非同步模式的最佳作法](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)中所述的進度報告語意。</span><span class="sxs-lookup"><span data-stu-id="70de8-191">Abide by the progress-reporting semantics described [Best Practices for Implementing the Event-based Asynchronous Pattern](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="optionally-provide-support-for-returning-incremental-results"></a><span data-ttu-id="70de8-192">選擇性地提供可傳回累加結果的支援</span><span class="sxs-lookup"><span data-stu-id="70de8-192">Optionally Provide Support for Returning Incremental Results</span></span>

<span data-ttu-id="70de8-193">有時候非同步作業會在完成之前傳回累加結果。</span><span class="sxs-lookup"><span data-stu-id="70de8-193">Sometimes an asynchronous operation can return incremental results prior to completion.</span></span> <span data-ttu-id="70de8-194">您有許多選項可用來支援這種情況。</span><span class="sxs-lookup"><span data-stu-id="70de8-194">There are a number of options that can be used to support this scenario.</span></span> <span data-ttu-id="70de8-195">下面有一些範例。</span><span class="sxs-lookup"><span data-stu-id="70de8-195">Some examples follow.</span></span>

### <a name="single-operation-class"></a><span data-ttu-id="70de8-196">單一作業類別</span><span class="sxs-lookup"><span data-stu-id="70de8-196">Single-operation Class</span></span>

<span data-ttu-id="70de8-197">如果您的類別只支援單一非同步作業，而且該作業可傳回累加結果，則請︰</span><span class="sxs-lookup"><span data-stu-id="70de8-197">If your class only supports a single asynchronous operation, and that operation is able to return incremental results, then:</span></span>

- <span data-ttu-id="70de8-198">擴充 <xref:System.ComponentModel.ProgressChangedEventArgs> 類型以攜帶累加結果資料，並使用此擴充資料定義 _方法名稱_**>progresschanged** 事件。</span><span class="sxs-lookup"><span data-stu-id="70de8-198">Extend the <xref:System.ComponentModel.ProgressChangedEventArgs> type to carry the incremental result data, and define a _MethodName_**ProgressChanged** event with this extended data.</span></span>

- <span data-ttu-id="70de8-199">當報告有累加結果時，引發這個 _方法_**>progresschanged** 事件。</span><span class="sxs-lookup"><span data-stu-id="70de8-199">Raise this _MethodName_**ProgressChanged** event when there is an incremental result to report.</span></span>

<span data-ttu-id="70de8-200">這項解決方案特別適用于單一非同步作業類別，因為在「所有作業」上發生的相同事件不會傳回累加的結果，因為 _方法_**>progresschanged** 事件的確沒有問題。</span><span class="sxs-lookup"><span data-stu-id="70de8-200">This solution applies specifically to a single-async-operation class because there is no problem with the same event occurring to return incremental results on "all operations", as the _MethodName_**ProgressChanged** event does.</span></span>

### <a name="multiple-operation-class-with-homogeneous-incremental-results"></a><span data-ttu-id="70de8-201">具有同質累加結果的多重作業類別</span><span class="sxs-lookup"><span data-stu-id="70de8-201">Multiple-operation Class with Homogeneous Incremental Results</span></span>

<span data-ttu-id="70de8-202">在此案例中，您的類別會支援多個非同步方法，每個方法都能傳回累加結果，而且這些累加結果全都有相同型別的資料。</span><span class="sxs-lookup"><span data-stu-id="70de8-202">In this case, your class supports multiple asynchronous methods, each capable of returning incremental results, and these incremental results all have the same type of data.</span></span>

<span data-ttu-id="70de8-203">請遵循上述的單一作業類別模型，因為同樣的 <xref:System.EventArgs> 結構適用於所有累加結果。</span><span class="sxs-lookup"><span data-stu-id="70de8-203">Follow the model described above for single-operation classes, as the same <xref:System.EventArgs> structure will work for all incremental results.</span></span> <span data-ttu-id="70de8-204">定義 `ProgressChanged` 事件而非 _方法_**>progresschanged** 事件，因為它會套用到多個非同步方法。</span><span class="sxs-lookup"><span data-stu-id="70de8-204">Define a `ProgressChanged` event instead of a _MethodName_**ProgressChanged** event, since it applies to multiple asynchronous methods.</span></span>

### <a name="multiple-operation-class-with-heterogeneous-incremental-results"></a><span data-ttu-id="70de8-205">具有異質累加結果的多重作業類別</span><span class="sxs-lookup"><span data-stu-id="70de8-205">Multiple-operation Class with Heterogeneous Incremental Results</span></span>

<span data-ttu-id="70de8-206">如果您的類別支援多個非同步方法，而且各會傳回不同型別的資料，您應該︰</span><span class="sxs-lookup"><span data-stu-id="70de8-206">If your class supports multiple asynchronous methods, each returning a different type of data, you should:</span></span>

- <span data-ttu-id="70de8-207">將累加結果報告和進度報告區隔開來。</span><span class="sxs-lookup"><span data-stu-id="70de8-207">Separate your incremental result reporting from your progress reporting.</span></span>

- <span data-ttu-id="70de8-208">針對每個非同步方法 _定義個別的方法_**>progresschanged** 事件， <xref:System.EventArgs> 以處理該方法的累加結果資料。</span><span class="sxs-lookup"><span data-stu-id="70de8-208">Define a separate _MethodName_**ProgressChanged** event with appropriate <xref:System.EventArgs> for each asynchronous method to handle that method's incremental result data.</span></span>

<span data-ttu-id="70de8-209">如[實作事件架構非同步模式的最佳作法](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)所述，在適當的執行緒上叫用該事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="70de8-209">Invoke that event handler on the appropriate thread as described in [Best Practices for Implementing the Event-based Asynchronous Pattern](best-practices-for-implementing-the-event-based-asynchronous-pattern.md).</span></span>

## <a name="handling-out-and-ref-parameters-in-methods"></a><span data-ttu-id="70de8-210">在方法中處理 Out 和 Ref 參數</span><span class="sxs-lookup"><span data-stu-id="70de8-210">Handling Out and Ref Parameters in Methods</span></span>

<span data-ttu-id="70de8-211">一般而言，雖然我們不建議您在 .NET Framework 中使用 `out` 和 `ref`，但如果它們存在，請遵循以下規則︰</span><span class="sxs-lookup"><span data-stu-id="70de8-211">Although the use of `out` and `ref` is, in general, discouraged in the .NET Framework, here are the rules to follow when they are present:</span></span>

<span data-ttu-id="70de8-212">假設同步方法為 MethodName\*\*：</span><span class="sxs-lookup"><span data-stu-id="70de8-212">Given a synchronous method *MethodName*:</span></span>

- <span data-ttu-id="70de8-213">`out`*方法名稱*的參數不應該是_方法名稱_為**Async**的一部分。</span><span class="sxs-lookup"><span data-stu-id="70de8-213">`out` parameters to *MethodName* should not be part of _MethodName_**Async**.</span></span> <span data-ttu-id="70de8-214">相反地，它們應該 _是方法名稱_**>completedeventargs** 的一部分，其名稱與 (*方法* 名稱中的對等參數相同，除非) 有更適當的名稱。</span><span class="sxs-lookup"><span data-stu-id="70de8-214">Instead, they should be part of _MethodName_**CompletedEventArgs** with the same name as its parameter equivalent in *MethodName* (unless there is a more appropriate name).</span></span>

- <span data-ttu-id="70de8-215">`ref`*方法*名稱的參數應該會以_方法名稱_**Async**的一部分形式出現，並_作為方法名稱_ (**>completedeventargs**的一部分，除非有*MethodName*更適當的名稱) 。</span><span class="sxs-lookup"><span data-stu-id="70de8-215">`ref` parameters to *MethodName* should appear as part of _MethodName_**Async**, and as part of _MethodName_**CompletedEventArgs** with the same name as its parameter equivalent in *MethodName* (unless there is a more appropriate name).</span></span>

<span data-ttu-id="70de8-216">例如，假設：</span><span class="sxs-lookup"><span data-stu-id="70de8-216">For example, given:</span></span>

```vb
Public Function MethodName(ByVal arg1 As String, ByRef arg2 As String, ByRef arg3 As String) As Integer
```

```csharp
public int MethodName(string arg1, ref string arg2, out string arg3);
```

<span data-ttu-id="70de8-217">您的非同步方法與其 <xref:System.ComponentModel.AsyncCompletedEventArgs> 類別看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="70de8-217">Your asynchronous method and its <xref:System.ComponentModel.AsyncCompletedEventArgs> class would look like this:</span></span>

```vb
Public Sub MethodNameAsync(ByVal arg1 As String, ByVal arg2 As String)

Public Class MethodNameCompletedEventArgs
    Inherits System.ComponentModel.AsyncCompletedEventArgs
    Public ReadOnly Property Result() As Integer
    End Property
    Public ReadOnly Property Arg2() As String
    End Property
    Public ReadOnly Property Arg3() As String
    End Property
End Class
```

```csharp
public void MethodNameAsync(string arg1, string arg2);

public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs
{
    public int Result { get; };
    public string Arg2 { get; };
    public string Arg3 { get; };
}
```

## <a name="see-also"></a><span data-ttu-id="70de8-218">另請參閱</span><span class="sxs-lookup"><span data-stu-id="70de8-218">See also</span></span>

- <xref:System.ComponentModel.ProgressChangedEventArgs>
- <xref:System.ComponentModel.AsyncCompletedEventArgs>
- [<span data-ttu-id="70de8-219">作法：實作支援事件架構非同步模式的元件</span><span class="sxs-lookup"><span data-stu-id="70de8-219">How to: Implement a Component That Supports the Event-based Asynchronous Pattern</span></span>](component-that-supports-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="70de8-220">作法：在背景執行作業</span><span class="sxs-lookup"><span data-stu-id="70de8-220">How to: Run an Operation in the Background</span></span>](/dotnet/desktop/winforms/controls/how-to-run-an-operation-in-the-background)
- [<span data-ttu-id="70de8-221">作法：實作使用背景作業的表單</span><span class="sxs-lookup"><span data-stu-id="70de8-221">How to: Implement a Form That Uses a Background Operation</span></span>](/dotnet/desktop/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation)
- [<span data-ttu-id="70de8-222">決定何時實作事件架構非同步模式</span><span class="sxs-lookup"><span data-stu-id="70de8-222">Deciding When to Implement the Event-based Asynchronous Pattern</span></span>](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="70de8-223">實作事件架構非同步模式的最佳作法</span><span class="sxs-lookup"><span data-stu-id="70de8-223">Best Practices for Implementing the Event-based Asynchronous Pattern</span></span>](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [<span data-ttu-id="70de8-224">事件架構非同步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="70de8-224">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
