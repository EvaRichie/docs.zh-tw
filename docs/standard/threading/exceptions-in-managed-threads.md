---
title: Managed 執行緒中的例外狀況
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- unhandled exceptions,in managed threads
- threading [.NET Framework],unhandled exceptions
- threading [.NET Framework],exceptions in managed threads
- managed threading
ms.assetid: 11294769-2e89-43cb-890e-ad4ad79cfbee
ms.openlocfilehash: 56900ddab5e1e6ee5375c8979dc19694d4ad9c54
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84279694"
---
# <a name="exceptions-in-managed-threads"></a><span data-ttu-id="26886-102">Managed 執行緒中的例外狀況</span><span class="sxs-lookup"><span data-stu-id="26886-102">Exceptions in Managed Threads</span></span>
<span data-ttu-id="26886-103">從 .NET Framework version 2.0 開始，通用語言執行平台允許執行緒中大多數未處理的例外狀況自然地繼續。</span><span class="sxs-lookup"><span data-stu-id="26886-103">Starting with the .NET Framework version 2.0, the common language runtime allows most unhandled exceptions in threads to proceed naturally.</span></span> <span data-ttu-id="26886-104">在大多數情況下，這表示未處理的例外狀況導致應用程式終止。</span><span class="sxs-lookup"><span data-stu-id="26886-104">In most cases this means that the unhandled exception causes the application to terminate.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="26886-105">這是 .NET Framework 1.0 和 1.1 的重大變更，其針對許多未處理的例外狀況提供了防護網 — 例如，執行緒集區執行緒中的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="26886-105">This is a significant change from the .NET Framework versions 1.0 and 1.1, which provide a backstop for many unhandled exceptions — for example, unhandled exceptions in thread pool threads.</span></span> <span data-ttu-id="26886-106">請參閱本主題後面的[從舊版變更](#ChangeFromPreviousVersions)。</span><span class="sxs-lookup"><span data-stu-id="26886-106">See [Change from Previous Versions](#ChangeFromPreviousVersions) later in this topic.</span></span>  
  
 <span data-ttu-id="26886-107">通用語言執行平台針對用於控制程式流程的特定未處理例外狀況提供了防護網︰</span><span class="sxs-lookup"><span data-stu-id="26886-107">The common language runtime provides a backstop for certain unhandled exceptions that are used for controlling program flow:</span></span>  
  
- <span data-ttu-id="26886-108">因為呼叫了 <xref:System.Threading.Thread.Abort%2A>，而導致執行緒中擲回 <xref:System.Threading.ThreadAbortException>。</span><span class="sxs-lookup"><span data-stu-id="26886-108">A <xref:System.Threading.ThreadAbortException> is thrown in a thread because <xref:System.Threading.Thread.Abort%2A> was called.</span></span>  
  
- <span data-ttu-id="26886-109">因為正在卸載執行緒執行所在的應用程式定義域，而在執行緒中擲回 <xref:System.AppDomainUnloadedException>。</span><span class="sxs-lookup"><span data-stu-id="26886-109">An <xref:System.AppDomainUnloadedException> is thrown in a thread because the application domain in which the thread is executing is being unloaded.</span></span>  
  
- <span data-ttu-id="26886-110">通用語言執行平台或主機處理序會藉由擲回內部例外狀況來終止執行緒。</span><span class="sxs-lookup"><span data-stu-id="26886-110">The common language runtime or a host process terminates the thread by throwing an internal exception.</span></span>  
  
 <span data-ttu-id="26886-111">如果在通用語言執行平台所建立的執行緒中有上述任何未處理的例外狀況，則此例外狀況會終止執行緒，但通用語言執行平台不允許例外狀況進一步繼續作業。</span><span class="sxs-lookup"><span data-stu-id="26886-111">If any of these exceptions are unhandled in threads created by the common language runtime, the exception terminates the thread, but the common language runtime does not allow the exception to proceed further.</span></span>  
  
 <span data-ttu-id="26886-112">如果未在主要執行緒中，或在從 Unmanaged 程式碼進入執行平台的執行緒中處理這些例外狀況，這些例外狀況會正常進行，而導致應用程式終止。</span><span class="sxs-lookup"><span data-stu-id="26886-112">If these exceptions are unhandled in the main thread, or in threads that entered the runtime from unmanaged code, they proceed normally, resulting in termination of the application.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="26886-113">在任何 Managed 程式碼有機會安裝例外狀況處理常式之前，執行平台可能會擲回未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="26886-113">It is possible for the runtime to throw an unhandled exception before any managed code has had a chance to install an exception handler.</span></span> <span data-ttu-id="26886-114">即使 Managed 程式碼沒有機會處理這類例外狀況，但允許例外狀況自然地進行。</span><span class="sxs-lookup"><span data-stu-id="26886-114">Even though managed code had no chance to handle such an exception, the exception is allowed to proceed naturally.</span></span>  
  
## <a name="exposing-threading-problems-during-development"></a><span data-ttu-id="26886-115">公開開發期間的執行緒問題</span><span class="sxs-lookup"><span data-stu-id="26886-115">Exposing Threading Problems During Development</span></span>  
 <span data-ttu-id="26886-116">若允許執行緒以無訊息模式失敗，而不終止應用程式，則可能偵測不到嚴重的程式設計問題。</span><span class="sxs-lookup"><span data-stu-id="26886-116">When threads are allowed to fail silently, without terminating the application, serious programming problems can go undetected.</span></span> <span data-ttu-id="26886-117">這是長時間執行的服務和其他應用程式特有的問題。</span><span class="sxs-lookup"><span data-stu-id="26886-117">This is a particular problem for services and other applications which run for extended periods.</span></span> <span data-ttu-id="26886-118">因為執行緒失敗，所以程式狀態會逐漸變差。</span><span class="sxs-lookup"><span data-stu-id="26886-118">As threads fail, program state gradually becomes corrupted.</span></span> <span data-ttu-id="26886-119">應用程式效能可能會降低，或應用程式可能會停止回應。</span><span class="sxs-lookup"><span data-stu-id="26886-119">Application performance may degrade, or the application might become unresponsive.</span></span>  
  
 <span data-ttu-id="26886-120">允許執行緒中的未處理例外狀況自然地進行，直到作業系統終止程式，公開開發和測試期間的這類問題為止。</span><span class="sxs-lookup"><span data-stu-id="26886-120">Allowing unhandled exceptions in threads to proceed naturally, until the operating system terminates the program, exposes such problems during development and testing.</span></span> <span data-ttu-id="26886-121">程式終止的錯誤報告可支援偵錯。</span><span class="sxs-lookup"><span data-stu-id="26886-121">Error reports on program terminations support debugging.</span></span>  
  
<a name="ChangeFromPreviousVersions"></a>
## <a name="change-from-previous-versions"></a><span data-ttu-id="26886-122">從舊版變更</span><span class="sxs-lookup"><span data-stu-id="26886-122">Change from Previous Versions</span></span>  
 <span data-ttu-id="26886-123">最重大的變更與 Managed 執行緒有關。</span><span class="sxs-lookup"><span data-stu-id="26886-123">The most significant change pertains to managed threads.</span></span> <span data-ttu-id="26886-124">在 .NET Framework 1.0 和 1.1 版中，通用語言執行平台會針對下列情況中未處理的例外狀況提供防護網：</span><span class="sxs-lookup"><span data-stu-id="26886-124">In the .NET Framework versions 1.0 and 1.1, the common language runtime provides a backstop for unhandled exceptions in the following situations:</span></span>  
  
- <span data-ttu-id="26886-125">執行緒集區執行緒上不會有未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="26886-125">There is no such thing as an unhandled exception on a thread pool thread.</span></span> <span data-ttu-id="26886-126">當工作擲回未處理的例外狀況時，執行平台會將例外狀況堆疊追蹤列印到主控台，然後將執行緒傳回到執行緒集區。</span><span class="sxs-lookup"><span data-stu-id="26886-126">When a task throws an exception that it does not handle, the runtime prints the exception stack trace to the console and then returns the thread to the thread pool.</span></span>  
  
- <span data-ttu-id="26886-127">使用 <xref:System.Threading.Thread> 類別的 <xref:System.Threading.Thread.Start%2A> 方法建立的執行緒上不會有未處理例外狀況之類的項目。</span><span class="sxs-lookup"><span data-stu-id="26886-127">There is no such thing as an unhandled exception on a thread created with the <xref:System.Threading.Thread.Start%2A> method of the <xref:System.Threading.Thread> class.</span></span> <span data-ttu-id="26886-128">在此種執行緒上執行的程式碼擲回未處理的例外狀況時，執行平台會將例外狀況堆疊追蹤列印到主控台，然後正常終止執行緒。</span><span class="sxs-lookup"><span data-stu-id="26886-128">When code running on such a thread throws an exception that it does not handle, the runtime prints the exception stack trace to the console and then gracefully terminates the thread.</span></span>  
  
- <span data-ttu-id="26886-129">完成項執行緒上不會有未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="26886-129">There is no such thing as an unhandled exception on the finalizer thread.</span></span> <span data-ttu-id="26886-130">當完成項擲回未處理的例外狀況時，執行平台會將例外狀況堆疊追蹤列印到主控台，然後允許完成項執行緒繼續執行完成項。</span><span class="sxs-lookup"><span data-stu-id="26886-130">When a finalizer throws an exception that it does not handle, the runtime prints the exception stack trace to the console and then allows the finalizer thread to resume running finalizers.</span></span>  
  
 <span data-ttu-id="26886-131">Managed 執行緒的前景或背景狀態不會影響此行為。</span><span class="sxs-lookup"><span data-stu-id="26886-131">The foreground or background status of a managed thread does not affect this behavior.</span></span>  
  
 <span data-ttu-id="26886-132">若為源自於 Unmanaged 程式碼的執行緒上未處理的例外狀況，差別更加細微。</span><span class="sxs-lookup"><span data-stu-id="26886-132">For unhandled exceptions on threads originating in unmanaged code, the difference is more subtle.</span></span> <span data-ttu-id="26886-133">對於已通過機器碼之執行緒上的 Managed 例外狀況或原生例外狀況而言，執行階段 JIT-attach 對話方塊的順序優先於作業系統對話方塊。</span><span class="sxs-lookup"><span data-stu-id="26886-133">The runtime JIT-attach dialog preempts the operating system dialog for managed exceptions or native exceptions on threads that have passed through native code.</span></span> <span data-ttu-id="26886-134">在所有情況下，此處理序會終止。</span><span class="sxs-lookup"><span data-stu-id="26886-134">The process terminates in all cases.</span></span>  
  
### <a name="migrating-code"></a><span data-ttu-id="26886-135">移轉程式碼</span><span class="sxs-lookup"><span data-stu-id="26886-135">Migrating Code</span></span>  
 <span data-ttu-id="26886-136">一般而言，變更會公開先前無法辨識的程式設計問題，以便修正這些問題。</span><span class="sxs-lookup"><span data-stu-id="26886-136">In general, the change will expose previously unrecognized programming problems so that they can be fixed.</span></span> <span data-ttu-id="26886-137">不過，在某些情況下，程式設計人員可能已利用執行階段防護網來終止執行緒。</span><span class="sxs-lookup"><span data-stu-id="26886-137">In some cases, however, programmers might have taken advantage of the runtime backstop, for example to terminate threads.</span></span> <span data-ttu-id="26886-138">視情況而定，它們應該考慮下列其中一個移轉策略︰</span><span class="sxs-lookup"><span data-stu-id="26886-138">Depending on the situation, they should consider one of the following migration strategies:</span></span>  
  
- <span data-ttu-id="26886-139">重新建構程式碼，讓執行緒在收到訊號時依正常程序結束。</span><span class="sxs-lookup"><span data-stu-id="26886-139">Restructure the code so the thread exits gracefully when a signal is received.</span></span>  
  
- <span data-ttu-id="26886-140">使用 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 方法來中止執行緒。</span><span class="sxs-lookup"><span data-stu-id="26886-140">Use the <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> method to abort the thread.</span></span>  
  
- <span data-ttu-id="26886-141">如果執行緒必須停止，處理序終止作業才能繼續，請讓執行緒成為背景執行緒，以便在處理序結束時自動終止。</span><span class="sxs-lookup"><span data-stu-id="26886-141">If a thread must be stopped so that process termination can proceed, make the thread a background thread so that it is automatically terminated on process exit.</span></span>  
  
 <span data-ttu-id="26886-142">在所有情況下，此策略應該遵循例外狀況的設計方針。</span><span class="sxs-lookup"><span data-stu-id="26886-142">In all cases, the strategy should follow the design guidelines for exceptions.</span></span> <span data-ttu-id="26886-143">請參閱[例外狀況的設計方針](../design-guidelines/exceptions.md)。</span><span class="sxs-lookup"><span data-stu-id="26886-143">See [Design Guidelines for Exceptions](../design-guidelines/exceptions.md).</span></span>  
  
### <a name="application-compatibility-flag"></a><span data-ttu-id="26886-144">應用程式相容性旗標</span><span class="sxs-lookup"><span data-stu-id="26886-144">Application Compatibility Flag</span></span>  
 <span data-ttu-id="26886-145">系統管理員可以在應用程式組態檔的 `<runtime>` 區段中放置相容性旗標，做為暫存的相容性度量。</span><span class="sxs-lookup"><span data-stu-id="26886-145">As a temporary compatibility measure, administrators can place a compatibility flag in the `<runtime>` section of the application configuration file.</span></span> <span data-ttu-id="26886-146">這會導致通用語言執行平台還原為 1.0 和 1.1 版的行為。</span><span class="sxs-lookup"><span data-stu-id="26886-146">This causes the common language runtime to revert to the behavior of versions 1.0 and 1.1.</span></span>  
  
```xml  
<legacyUnhandledExceptionPolicy enabled="1"/>  
```  
  
## <a name="host-override"></a><span data-ttu-id="26886-147">主機覆寫</span><span class="sxs-lookup"><span data-stu-id="26886-147">Host Override</span></span>  
 <span data-ttu-id="26886-148">在 .NET Framework 2.0 版中，Unmanaged 主機可以使用裝載 API 中的 [ICLRPolicyManager](../../framework/unmanaged-api/hosting/iclrpolicymanager-interface.md) 介面，覆寫通用語言執行平台的預設未處理例外狀況原則。</span><span class="sxs-lookup"><span data-stu-id="26886-148">In the .NET Framework version 2.0, an unmanaged host can use the [ICLRPolicyManager](../../framework/unmanaged-api/hosting/iclrpolicymanager-interface.md) interface in the Hosting API to override the default unhandled exception policy of the common language runtime.</span></span> <span data-ttu-id="26886-149">[Iclrpolicymanager:: Setunhandledexceptionpolicy](../../framework/unmanaged-api/hosting/iclrpolicymanager-setunhandledexceptionpolicy-method.md) 函數用來設定未處理例外狀況的原則。</span><span class="sxs-lookup"><span data-stu-id="26886-149">The [ICLRPolicyManager::SetUnhandledExceptionPolicy](../../framework/unmanaged-api/hosting/iclrpolicymanager-setunhandledexceptionpolicy-method.md) function is used to set the policy for unhandled exceptions.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="26886-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="26886-150">See also</span></span>

- [<span data-ttu-id="26886-151">Managed 執行緒基本概念</span><span class="sxs-lookup"><span data-stu-id="26886-151">Managed Threading Basics</span></span>](managed-threading-basics.md)
