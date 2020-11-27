---
title: 重新進入 MDA
description: 檢查重新進入 MDA，如果物件堆積已損毀，或從原生轉換為 managed 程式碼時發生其他嚴重錯誤，則可能會啟用這項功能。
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged code, debugging
- transitioning threads unmanaged to managed code
- reentrancy MDA
- reentrancy without an orderly transition
- managed debugging assistants (MDAs), reentrancy
- illegal reentrancy
- MDAs (managed debugging assistants), reentrancy
- threading [.NET Framework], managed debugging assistants
- managed code, debugging
- native debugging, MDAs
ms.assetid: 7240c3f3-7df8-4b03-bbf1-17cdce142d45
ms.openlocfilehash: 0480b1a5aafbc8c4f9645ba83383d3a222d1f1c5
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96264578"
---
# <a name="reentrancy-mda"></a><span data-ttu-id="c2e16-103">重新進入 MDA</span><span class="sxs-lookup"><span data-stu-id="c2e16-103">reentrancy MDA</span></span>

<span data-ttu-id="c2e16-104">如果未透過循序轉換執行先前從 Managed 程式碼到機器碼的切換時嘗試從機器碼轉換成 Managed 程式碼，啟用 `reentrancy` Managed 偵錯助理 (MDA)。</span><span class="sxs-lookup"><span data-stu-id="c2e16-104">The `reentrancy` managed debugging assistant (MDA) is activated when an attempt is made to transition from native to managed code in cases where a prior switch from managed to native code was not performed through an orderly transition.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="c2e16-105">徵狀</span><span class="sxs-lookup"><span data-stu-id="c2e16-105">Symptoms</span></span>  

 <span data-ttu-id="c2e16-106">物件堆積損毀，或從機器碼轉換成 Managed 程式碼時發生其他嚴重錯誤。</span><span class="sxs-lookup"><span data-stu-id="c2e16-106">The object heap is corrupted or other serious errors are occurring when transitioning from native to managed code.</span></span>  
  
 <span data-ttu-id="c2e16-107">在機器碼與 Managed 程式碼之間依任一方向切換的執行緒，必須執行循序轉換。</span><span class="sxs-lookup"><span data-stu-id="c2e16-107">Threads that switch between native and managed code in either direction must perform an orderly transition.</span></span> <span data-ttu-id="c2e16-108">不過，作業系統中的特定低階擴充點 (例如向量化例外狀況處理常式) 允許從 Managed 程式碼切換成機器碼，而不需要執行循序轉換。</span><span class="sxs-lookup"><span data-stu-id="c2e16-108">However, certain low-level extensibility points in the operating system, such as the vectored exception handler, allow switches from managed to native code without performing an orderly transition.</span></span>  <span data-ttu-id="c2e16-109">這些參數是受作業系統控制，而不是受 Common Language Runtime (CLR) 控制。</span><span class="sxs-lookup"><span data-stu-id="c2e16-109">These switches are under operating system control, rather than under common language runtime (CLR) control.</span></span>  <span data-ttu-id="c2e16-110">任何在這些擴充點內執行的機器碼都必須避免回呼 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2e16-110">Any native code that executes inside these extensibility points must avoid calling back into managed code.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="c2e16-111">原因</span><span class="sxs-lookup"><span data-stu-id="c2e16-111">Cause</span></span>  

 <span data-ttu-id="c2e16-112">執行 Managed 程式碼時，已啟用低階作業系統擴充點 (例如向量化例外狀況處理常式)。</span><span class="sxs-lookup"><span data-stu-id="c2e16-112">A low-level operating system extensibility point, such as the vectored exception handler, has activated while executing managed code.</span></span>  <span data-ttu-id="c2e16-113">透過該擴充點叫用的應用程式碼將嘗試回呼至 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2e16-113">The application code that is invoked through that extensibility point is attempting to call back into managed code.</span></span>  
  
 <span data-ttu-id="c2e16-114">這個問題一律是由應用程式碼所造成。</span><span class="sxs-lookup"><span data-stu-id="c2e16-114">This problem is always caused by application code.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="c2e16-115">解決方法</span><span class="sxs-lookup"><span data-stu-id="c2e16-115">Resolution</span></span>  

 <span data-ttu-id="c2e16-116">檢查已啟用此 MDA 的執行緒堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="c2e16-116">Examine the stack trace for the thread that has activated this MDA.</span></span>  <span data-ttu-id="c2e16-117">執行緒將會嘗試不合法地呼叫 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2e16-117">The thread is attempting to illegally call into managed code.</span></span>  <span data-ttu-id="c2e16-118">堆疊追蹤應該顯示使用此擴充點的應用程式碼、提供此擴充點的作業系統程式碼，以及擴充點已中斷的 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="c2e16-118">The stack trace should reveal the application code using this extensibility point, the operating system code that provides this extensibility point, and the managed code that was interrupted by the extensibility point.</span></span>  
  
 <span data-ttu-id="c2e16-119">例如，您會看到 MDA 已在嘗試從向量化例外狀況處理常式呼叫 Managed 程式碼時啟用。</span><span class="sxs-lookup"><span data-stu-id="c2e16-119">For example, you will see the MDA activated in an attempt to call managed code from inside a vectored exception handler.</span></span>  <span data-ttu-id="c2e16-120">在堆疊上，您會看到作業系統例外狀況處理程式碼，以及觸發例外狀況的某個 Managed 程式碼 (例如 <xref:System.DivideByZeroException> 或 <xref:System.AccessViolationException>)。</span><span class="sxs-lookup"><span data-stu-id="c2e16-120">On the stack you will see the operating system exception handling code and some managed code triggering an exception such as a <xref:System.DivideByZeroException> or an <xref:System.AccessViolationException>.</span></span>  
  
 <span data-ttu-id="c2e16-121">在此範例中，正確的解決方式是使用 Unmanaged 程式碼完全實作向量化例外狀況處理常式。</span><span class="sxs-lookup"><span data-stu-id="c2e16-121">In this example, the correct resolution is to implement the vectored exception handler completely in unmanaged code.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="c2e16-122">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="c2e16-122">Effect on the Runtime</span></span>  

 <span data-ttu-id="c2e16-123">此 MDA 對 CLR 沒有影響。</span><span class="sxs-lookup"><span data-stu-id="c2e16-123">This MDA has no effect on the CLR.</span></span>  
  
## <a name="output"></a><span data-ttu-id="c2e16-124">輸出</span><span class="sxs-lookup"><span data-stu-id="c2e16-124">Output</span></span>  

 <span data-ttu-id="c2e16-125">MDA 報告正在嘗試不合法的重新進入。</span><span class="sxs-lookup"><span data-stu-id="c2e16-125">The MDA reports that illegal reentrancy is being attempted.</span></span>  <span data-ttu-id="c2e16-126">檢查執行緒的堆疊，以判斷發生此問題的原因和其更正方式。</span><span class="sxs-lookup"><span data-stu-id="c2e16-126">Examine the thread's stack to determine why this is happening and how to correct the problem.</span></span> <span data-ttu-id="c2e16-127">以下是範例輸出。</span><span class="sxs-lookup"><span data-stu-id="c2e16-127">The following is sample output.</span></span>  
  
```output
Additional Information: Attempting to call into managed code without
transitioning out first.  Do not attempt to run managed code inside
low-level native extensibility points. Managed Debugging Assistant
'Reentrancy' has detected a problem in 'D:\ConsoleApplication1\  
ConsoleApplication1\bin\Debug\ConsoleApplication1.vshost.exe'.  
```  
  
## <a name="configuration"></a><span data-ttu-id="c2e16-128">設定</span><span class="sxs-lookup"><span data-stu-id="c2e16-128">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <reentrancy />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a><span data-ttu-id="c2e16-129">範例</span><span class="sxs-lookup"><span data-stu-id="c2e16-129">Example</span></span>  

 <span data-ttu-id="c2e16-130">下列程式碼範例會導致擲回 <xref:System.AccessViolationException>。</span><span class="sxs-lookup"><span data-stu-id="c2e16-130">The following code example causes an <xref:System.AccessViolationException> to be thrown.</span></span>  <span data-ttu-id="c2e16-131">在支援向量化例外狀況處理的 Windows 版本上，這會呼叫 Managed 向量化例外狀況處理常式。</span><span class="sxs-lookup"><span data-stu-id="c2e16-131">On versions of Windows that support vectored exception handling, this will cause the managed vectored exception handler to be called.</span></span>  <span data-ttu-id="c2e16-132">如果啟用 `reentrancy` MDA，則會在透過作業系統的向量化例外狀況處理支援程式碼嘗試呼叫 `MyHandler` 期間啟用 MDA。</span><span class="sxs-lookup"><span data-stu-id="c2e16-132">If the `reentrancy` MDA is enabled, the MDA will activate during the attempted call to `MyHandler` from the operating system's vectored exception handling support code.</span></span>  
  
```csharp
using System;  
public delegate int ExceptionHandler(IntPtr ptrExceptionInfo);  
  
public class Reenter
{  
    public static ExceptionHandler keepAlive;  
  
    [System.Runtime.InteropServices.DllImport("kernel32", ExactSpelling=true,
        CharSet=System.Runtime.InteropServices.CharSet.Auto)]  
    public static extern IntPtr AddVectoredExceptionHandler(int bFirst,
        ExceptionHandler handler);  
  
    static int MyHandler(IntPtr ptrExceptionInfo)
    {  
        // EXCEPTION_CONTINUE_SEARCH  
        return 0;  
    }  
    void Run() {}  
  
    static void Main()
    {  
        keepAlive = new ExceptionHandler(Reenter.MyHandler);  
        IntPtr ret = AddVectoredExceptionHandler(1, keepAlive);  
        try
        {  
            // Dispatch on null should AV.  
            Reenter r = null;
            r.Run();  
        }
        catch { }  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="c2e16-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c2e16-133">See also</span></span>

- [<span data-ttu-id="c2e16-134">診斷 Managed 偵錯助理的錯誤</span><span class="sxs-lookup"><span data-stu-id="c2e16-134">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
