---
title: invalidApartmentStateChange MDA
description: 瞭解 .NET 中的 invalidApartmentStateChange managed 偵錯工具（MDA），這會在 COM 單元狀態發生問題時啟動。
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid apartment state
- managed debugging assistants (MDAs), invalid apartment state
- InvalidApartmentStateChange MDA
- invalid apartment state changes
- threading [.NET Framework], apartment states
- apartment states
- threading [.NET Framework], managed debugging assistants
- COM apartment states
ms.assetid: e56fb9df-5286-4be7-b313-540c4d876cd7
ms.openlocfilehash: c6f7b6a5e450d4167946d22b2ada268ea2b0135f
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051823"
---
# <a name="invalidapartmentstatechange-mda"></a><span data-ttu-id="244cc-103">invalidApartmentStateChange MDA</span><span class="sxs-lookup"><span data-stu-id="244cc-103">invalidApartmentStateChange MDA</span></span>
<span data-ttu-id="244cc-104">`invalidApartmentStateChange` Managed 偵錯助理 (MDA) 是由下列兩個問題之一所啟動：</span><span class="sxs-lookup"><span data-stu-id="244cc-104">The `invalidApartmentStateChange` managed debugging assistant (MDS) is activated by either of two problems:</span></span>  
  
- <span data-ttu-id="244cc-105">嘗試變更執行緒的 COM Apartment 狀態，該執行緒已被 COM 初始化成不同的 Apartment 狀態。</span><span class="sxs-lookup"><span data-stu-id="244cc-105">An attempt is made to change the COM apartment state of a thread that has already been initialized by COM to a different apartment state.</span></span>  
  
- <span data-ttu-id="244cc-106">未預期的執行緒 COM Apartment 狀態變更。</span><span class="sxs-lookup"><span data-stu-id="244cc-106">The COM apartment state of a thread changes unexpectedly.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="244cc-107">徵狀</span><span class="sxs-lookup"><span data-stu-id="244cc-107">Symptoms</span></span>  
  
- <span data-ttu-id="244cc-108">執行緒的 COM Apartment 狀態不是原來要求的。</span><span class="sxs-lookup"><span data-stu-id="244cc-108">A thread's COM apartment state is not what was requested.</span></span> <span data-ttu-id="244cc-109">這可能會導致 Proxy 用於執行緒模型和目前執行緒模型不同的 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="244cc-109">This may cause proxies to be used for COM components that have a threading model different from the current one.</span></span> <span data-ttu-id="244cc-110">接著，在透過未設定跨 Apartment 封送處理的介面呼叫 COM 物件時，這可能會造成 <xref:System.InvalidCastException> 被擲回。</span><span class="sxs-lookup"><span data-stu-id="244cc-110">This in turn may cause an <xref:System.InvalidCastException> to be thrown when calling the COM object through interfaces that are not set up for cross-apartment marshaling.</span></span>  
  
- <span data-ttu-id="244cc-111">執行緒的 COM Apartment 狀態與預期的不同。</span><span class="sxs-lookup"><span data-stu-id="244cc-111">The COM apartment state of the thread is different than expected.</span></span> <span data-ttu-id="244cc-112">在[執行階段可呼叫包裝函式](../../standard/native-interop/runtime-callable-wrapper.md) (RCW) 上進行呼叫時，這會造成 <xref:System.Runtime.InteropServices.COMException> 具有 RPC_E_WRONG_THREAD 的 HRESULT 以及 <xref:System.InvalidCastException>。</span><span class="sxs-lookup"><span data-stu-id="244cc-112">This can cause a <xref:System.Runtime.InteropServices.COMException> with an HRESULT of RPC_E_WRONG_THREAD as well as a <xref:System.InvalidCastException> when making calls on a [Runtime Callable Wrapper](../../standard/native-interop/runtime-callable-wrapper.md) (RCW).</span></span> <span data-ttu-id="244cc-113">這也會造成多個執行緒同時存取某些單一執行緒的 COM 元件，導致損毀或資料遺失。</span><span class="sxs-lookup"><span data-stu-id="244cc-113">This can also cause some single-threaded COM components to be accessed by multiple threads at the same time, which can lead to corruption or data loss.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="244cc-114">原因</span><span class="sxs-lookup"><span data-stu-id="244cc-114">Cause</span></span>  
  
- <span data-ttu-id="244cc-115">執行緒先前已初始化成不同的 COM Apartment 狀態。</span><span class="sxs-lookup"><span data-stu-id="244cc-115">The thread was previously initialized to a different COM apartment state.</span></span> <span data-ttu-id="244cc-116">請注意，可以明確或隱含方式設定執行緒的 Apartment 狀態。</span><span class="sxs-lookup"><span data-stu-id="244cc-116">Note that the apartment state of a thread can be set either explicitly or implicitly.</span></span> <span data-ttu-id="244cc-117">明確的作業包括 <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=nameWithType> 屬性以及 <xref:System.Threading.Thread.SetApartmentState%2A> 和 <xref:System.Threading.Thread.TrySetApartmentState%2A> 方法。</span><span class="sxs-lookup"><span data-stu-id="244cc-117">The explicit operations include the <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=nameWithType> property and the <xref:System.Threading.Thread.SetApartmentState%2A> and <xref:System.Threading.Thread.TrySetApartmentState%2A> methods.</span></span> <span data-ttu-id="244cc-118">使用 <xref:System.Threading.Thread.Start%2A> 方法建立的執行緒，會以隱含方式設成 <xref:System.Threading.ApartmentState.MTA>，除非啟動執行緒之前呼叫 <xref:System.Threading.Thread.SetApartmentState%2A>。</span><span class="sxs-lookup"><span data-stu-id="244cc-118">A thread created using the <xref:System.Threading.Thread.Start%2A> method is implicitly set to <xref:System.Threading.ApartmentState.MTA> unless <xref:System.Threading.Thread.SetApartmentState%2A> is called before the thread is started.</span></span> <span data-ttu-id="244cc-119">應用程式的主執行緒也會以隱含方式初始化為 <xref:System.Threading.ApartmentState.MTA>，除非在 Main 方法上指定 <xref:System.STAThreadAttribute> 屬性。</span><span class="sxs-lookup"><span data-stu-id="244cc-119">The main thread of the application is also implicitly initialized to <xref:System.Threading.ApartmentState.MTA> unless the <xref:System.STAThreadAttribute> attribute is specified on the main method.</span></span>  
  
- <span data-ttu-id="244cc-120">在執行緒上呼叫具有不同並行模型的 `CoUninitialize` 方法 (或 `CoInitializeEx` 方法)。</span><span class="sxs-lookup"><span data-stu-id="244cc-120">The `CoUninitialize` method (or the `CoInitializeEx` method) with a different concurrency model is called on the thread.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="244cc-121">解決方案</span><span class="sxs-lookup"><span data-stu-id="244cc-121">Resolution</span></span>  
 <span data-ttu-id="244cc-122">請先設定執行緒的 Apartment 狀態再開始執行，或將 <xref:System.STAThreadAttribute> 屬性或 <xref:System.MTAThreadAttribute> 屬性套用到應用程式的 Main 方法。</span><span class="sxs-lookup"><span data-stu-id="244cc-122">Set the apartment state of the thread before it begins executing, or apply either the <xref:System.STAThreadAttribute> attribute or the <xref:System.MTAThreadAttribute> attribute to the main method of the application.</span></span>  
  
 <span data-ttu-id="244cc-123">第二個原因，在理想情況下，應該修改呼叫 `CoUninitialize` 方法的程式碼以延遲呼叫，直到執行緒即將終止且沒有任何 RCW 為止，執行緒仍繼續使用它們的基礎 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="244cc-123">For the second cause, ideally, the code that calls the `CoUninitialize` method should be modified to delay the call until the thread is about to terminate and there are no RCWs and their underlying COM components still in use by the thread.</span></span> <span data-ttu-id="244cc-124">不過，如果不可能修改呼叫 `CoUninitialize` 方法的程式碼，則不應從未以此方式初始化的執行緒中使用任何 RCW。</span><span class="sxs-lookup"><span data-stu-id="244cc-124">However, if it is not possible to modify the code that calls the `CoUninitialize` method, then no RCWs should be used from threads that are uninitialized in this way.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="244cc-125">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="244cc-125">Effect on the Runtime</span></span>  
 <span data-ttu-id="244cc-126">此 MDA 對 CLR 沒有影響。</span><span class="sxs-lookup"><span data-stu-id="244cc-126">This MDA has no effect on the CLR.</span></span>  
  
## <a name="output"></a><span data-ttu-id="244cc-127">輸出</span><span class="sxs-lookup"><span data-stu-id="244cc-127">Output</span></span>  
 <span data-ttu-id="244cc-128">目前執行緒的 COM Apartment 狀態和程式碼之前嘗試套用的狀態。</span><span class="sxs-lookup"><span data-stu-id="244cc-128">The COM apartment state of the current thread, and the state that the code was attempting to apply.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="244cc-129">組態</span><span class="sxs-lookup"><span data-stu-id="244cc-129">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidApartmentStateChange />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a><span data-ttu-id="244cc-130">範例</span><span class="sxs-lookup"><span data-stu-id="244cc-130">Example</span></span>  
 <span data-ttu-id="244cc-131">下列程式碼範例示範可以啟動此 MDA 的情況。</span><span class="sxs-lookup"><span data-stu-id="244cc-131">The following code example demonstrates a situation that can activate this MDA.</span></span>  
  
```csharp
using System.Threading;  
namespace ApartmentStateMDA  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Thread.CurrentThread.SetApartmentState(ApartmentState.STA);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="244cc-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="244cc-132">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="244cc-133">使用 Managed 偵錯助理診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="244cc-133">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="244cc-134">Interop 封送處理</span><span class="sxs-lookup"><span data-stu-id="244cc-134">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
