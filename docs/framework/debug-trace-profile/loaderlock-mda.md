---
title: loaderLock MDA
description: 請參閱 .NET 中的 loaderLock managed 偵錯工具（MDA），它會偵測嘗試在持有 Windows OS 載入器鎖定的執行緒上執行 managed 程式碼。
ms.date: 03/30/2017
helpviewer_keywords:
- deadlocks [.NET Framework]
- LoaderLock MDA
- MDAs (managed debugging assistants), loader locks
- managed debugging assistants (MDAs), loader locks
- operating system loader locks
- loader locks
- locks, threads
ms.assetid: 8c10fa02-1b9c-4be5-ab03-451d943ac1ee
ms.openlocfilehash: 055b07a805c5f0b613519d6019950a9b249a4b38
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: zh-TW
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051618"
---
# <a name="loaderlock-mda"></a><span data-ttu-id="19a92-103">loaderLock MDA</span><span class="sxs-lookup"><span data-stu-id="19a92-103">loaderLock MDA</span></span>
<span data-ttu-id="19a92-104">`loaderLock` Managed 偵錯助理 (MDA) 偵測到在保留 Microsoft Windows 作業系統載入器鎖定的執行緒上，有執行 Managed 程式碼的嘗試。</span><span class="sxs-lookup"><span data-stu-id="19a92-104">The `loaderLock` managed debugging assistant (MDA) detects attempts to execute managed code on a thread that holds the Microsoft Windows operating system loader lock.</span></span>  <span data-ttu-id="19a92-105">所有這樣的執行都不合法，因為它可能會產生死結，並在作業系統載入器尚未初始化 DLL 之前就先使用 DLL。</span><span class="sxs-lookup"><span data-stu-id="19a92-105">Any such execution is illegal because it can lead to deadlocks and to use of DLLs before they have been initialized by the operating system's loader.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="19a92-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="19a92-106">Symptoms</span></span>  
 <span data-ttu-id="19a92-107">在作業系統的載入器鎖定內執行程式碼最常見的失敗，是嘗試呼叫也需要載入器鎖定的其他 Win32 函式時，執行緒會鎖死。</span><span class="sxs-lookup"><span data-stu-id="19a92-107">The most common failure when executing code inside the operating system's loader lock is that threads will deadlock when attempting to call other Win32 functions that also require the loader lock.</span></span>  <span data-ttu-id="19a92-108">這類函式範例包括 `LoadLibrary`、`GetProcAddress`、`FreeLibrary` 和 `GetModuleHandle`。</span><span class="sxs-lookup"><span data-stu-id="19a92-108">Examples of such functions are `LoadLibrary`, `GetProcAddress`, `FreeLibrary`, and `GetModuleHandle`.</span></span>  <span data-ttu-id="19a92-109">應用程式可能不會直接呼叫這些函式。像 <xref:System.Reflection.Assembly.Load%2A> 或平台叫用方法的第一個呼叫等較高層級的呼叫結果，可能是 Common Language Runtime (CLR) 呼叫這些函式。</span><span class="sxs-lookup"><span data-stu-id="19a92-109">The application might not directly call these functions; the common language runtime (CLR) might call these functions as the result of a higher level call like <xref:System.Reflection.Assembly.Load%2A> or the first call to a platform invoke method.</span></span>  
  
 <span data-ttu-id="19a92-110">當執行緒等候另一個執行緒開始或結束時，也會發生鎖死的情況。</span><span class="sxs-lookup"><span data-stu-id="19a92-110">Deadlocks can also occur if a thread is waiting for another thread to start or finish.</span></span>  <span data-ttu-id="19a92-111">當執行緒開始或結束執行時，它必須取得作業系統的載入器鎖定，以將事件傳遞給受影響的 DLL。</span><span class="sxs-lookup"><span data-stu-id="19a92-111">When a thread starts or finishes executing, it must acquire the operating system's loader lock to deliver events to affected DLLs.</span></span>  
  
 <span data-ttu-id="19a92-112">最後，就會發生作業系統載入器還未正確初始化 DLL 就先呼叫它們的情況。</span><span class="sxs-lookup"><span data-stu-id="19a92-112">Finally, there are cases where calls into DLLs can occur before those DLLs have been properly initialized by the operating system's loader.</span></span>  <span data-ttu-id="19a92-113">不同於透過檢查所有與死結有關的執行緒堆疊可診斷出的死結失敗，不使用這個 MDA，要診斷出使用了未初始化的 DLL 很困難。</span><span class="sxs-lookup"><span data-stu-id="19a92-113">Unlike the deadlock failures, which can be diagnosed by examining the stacks of all the threads involved in the deadlock, it is very difficult to diagnose the use of uninitialized DLLs without using this MDA.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="19a92-114">原因</span><span class="sxs-lookup"><span data-stu-id="19a92-114">Cause</span></span>  
 <span data-ttu-id="19a92-115">針對 .NET Framework 1.0 或 1.1 版建置的混合 Managed/Unmanaged C++ 組件，通常會在載入器鎖定內嘗試執行 Managed 程式碼，除非已特別注意；例如，與 **/NOENTRY** 連結。</span><span class="sxs-lookup"><span data-stu-id="19a92-115">Mixed managed/unmanaged C++ assemblies built for .NET Framework versions 1.0 or 1.1 generally attempt to execute managed code inside the loader lock unless special care has been taken, for example, linking with **/NOENTRY**.</span></span>
  
 <span data-ttu-id="19a92-116">針對 .NET Framework 2.0 版建置的混合 Managed/Unmanaged C++ 組件，較不容易發生這些問題，與使用 Unmanaged DLL 違反作業系統規則的應用程式，有相同的降低風險。</span><span class="sxs-lookup"><span data-stu-id="19a92-116">Mixed managed/unmanaged C++ assemblies built for .NET Framework version 2.0 are less susceptible to these problems, having the same reduced risk as applications using unmanaged DLLs that violate the operating system's rules.</span></span>  <span data-ttu-id="19a92-117">例如，如果 Unmanaged DLL 的 `DllMain` 進入點，呼叫 `CoCreateInstance` 取得已向 COM 公開的 Managed 物件，結果是在載入器鎖定內嘗試執行 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="19a92-117">For example, if an unmanaged DLL's `DllMain` entry point calls `CoCreateInstance` to obtain a managed object that has been exposed to COM, the result is an attempt to execute managed code inside the loader lock.</span></span> <span data-ttu-id="19a92-118">如需 .NET Framework 2.0 版或更新版本中的載入器鎖定問題的詳細資訊，請參閱[初始化混合組件](/cpp/dotnet/initialization-of-mixed-assemblies)。</span><span class="sxs-lookup"><span data-stu-id="19a92-118">For more information about loader lock issues in the .NET Framework version 2.0 and later, see [Initialization of Mixed Assemblies](/cpp/dotnet/initialization-of-mixed-assemblies).</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="19a92-119">解決方案</span><span class="sxs-lookup"><span data-stu-id="19a92-119">Resolution</span></span>  
 <span data-ttu-id="19a92-120">在 Visual C++ .NET 2002 和 Visual C++ .NET 2003 中，使用 `/clr` 編譯器選項編譯的 DLL，可能會在載入時出現不具決定性的死結；此問題稱為混合 DLL 載入或載入器鎖定問題。</span><span class="sxs-lookup"><span data-stu-id="19a92-120">In Visual C++ .NET 2002 and Visual C++ .NET 2003, DLLs compiled with the `/clr` compiler option could non-deterministically deadlock when loaded; this issue was called the mixed DLL loading or loader lock issue.</span></span> <span data-ttu-id="19a92-121">在 Visual C++ 2005 及更新版本中，混合 DLL 載入程序的所有不具決定性問題幾乎都已獲得解決。</span><span class="sxs-lookup"><span data-stu-id="19a92-121">In Visual C++ 2005 and later, almost all non-determinism has been removed from the mixed DLL loading process.</span></span> <span data-ttu-id="19a92-122">不過還是有些情況可能會發生載入器鎖定問題 (具決定性)。</span><span class="sxs-lookup"><span data-stu-id="19a92-122">However, there are a few remaining scenarios for which loader lock can (deterministically) occur.</span></span> <span data-ttu-id="19a92-123">如需其餘載入器鎖定問題的原因與解決方法的詳細說明，請參閱[初始化混合組件](/cpp/dotnet/initialization-of-mixed-assemblies)。</span><span class="sxs-lookup"><span data-stu-id="19a92-123">For a detailed account of the causes and resolutions for the remaining loader lock issues, see [Initialization of Mixed Assemblies](/cpp/dotnet/initialization-of-mixed-assemblies).</span></span> <span data-ttu-id="19a92-124">如果在該主題中找不出您的載入器鎖定問題，您必須檢查執行緒的堆疊，以判斷載入器鎖定發生的原因，以及如何修正此問題。</span><span class="sxs-lookup"><span data-stu-id="19a92-124">If that topic does not identify your loader lock problem, you have to examine the thread's stack to determine why the loader lock is occurring and how to correct the problem.</span></span> <span data-ttu-id="19a92-125">查看已啟動此 MDA 的執行緒堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="19a92-125">Look at the stack trace for the thread that has activated this MDA.</span></span>  <span data-ttu-id="19a92-126">在保留作業系統載入器鎖定時，執行緒嘗試以非法方式呼叫 Managed 程式碼。</span><span class="sxs-lookup"><span data-stu-id="19a92-126">The thread is attempting to illegally call into managed code while holding the operating system's loader lock.</span></span>  <span data-ttu-id="19a92-127">您可能會在堆疊上看到 DLL 的 `DllMain` 或對等進入點。</span><span class="sxs-lookup"><span data-stu-id="19a92-127">You will probably see a DLL's `DllMain` or equivalent entry point on the stack.</span></span>  <span data-ttu-id="19a92-128">可從這類進入點內部執行哪些合法作業的作業系統規則相當有限。</span><span class="sxs-lookup"><span data-stu-id="19a92-128">The operating system's rules for what you can legally do from inside such an entry point are quite limited.</span></span>  <span data-ttu-id="19a92-129">這些規則會排除所有 Managed 執行。</span><span class="sxs-lookup"><span data-stu-id="19a92-129">These rules preclude any managed execution.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="19a92-130">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="19a92-130">Effect on the Runtime</span></span>  
 <span data-ttu-id="19a92-131">一般而言，處理序內有數個執行緒會鎖死。</span><span class="sxs-lookup"><span data-stu-id="19a92-131">Typically, several threads inside the process will deadlock.</span></span>  <span data-ttu-id="19a92-132">其中一個執行緒很可能負責執行記憶體回收，因此這個死結對整個程序有很大的影響。</span><span class="sxs-lookup"><span data-stu-id="19a92-132">One of those threads is likely to be a thread responsible for performing a garbage collection, so this deadlock can have a major impact on the entire process.</span></span>  <span data-ttu-id="19a92-133">此外，它會防止需要作業系統載入器鎖定的任何其他作業，例如載入及卸載組件或 DLL，以及啟動或停止執行緒。</span><span class="sxs-lookup"><span data-stu-id="19a92-133">Furthermore, it will prevent any additional operations that require the operating system's loader lock, like loading and unloading assemblies or DLLs and starting or stopping threads.</span></span>  
  
 <span data-ttu-id="19a92-134">在某些罕見的情況下，也可能會在未初始化即被呼叫的 DLL 中，觸發存取違規或類似問題。</span><span class="sxs-lookup"><span data-stu-id="19a92-134">In some unusual cases, it is also possible for access violations or similar problems to be triggered in DLLs which are called before they have been initialized.</span></span>  
  
## <a name="output"></a><span data-ttu-id="19a92-135">輸出</span><span class="sxs-lookup"><span data-stu-id="19a92-135">Output</span></span>  
 <span data-ttu-id="19a92-136">此 MDA 會報告正在嘗試不合法的 Managed 執行。</span><span class="sxs-lookup"><span data-stu-id="19a92-136">This MDA reports that an illegal managed execution is being attempted.</span></span>  <span data-ttu-id="19a92-137">您需要檢查執行緒的堆疊，以判斷載入器鎖定發生的原因，以及如何修正此問題。</span><span class="sxs-lookup"><span data-stu-id="19a92-137">You need to examine the thread's stack to determine why the loader lock is occurring and how to correct the problem.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="19a92-138">組態</span><span class="sxs-lookup"><span data-stu-id="19a92-138">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <loaderLock/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="19a92-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="19a92-139">See also</span></span>

- [<span data-ttu-id="19a92-140">使用 Managed 偵錯助理診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="19a92-140">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
