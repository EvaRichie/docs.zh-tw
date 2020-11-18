---
title: 執行緒物件和功能
ms.date: 10/01/2018
helpviewer_keywords:
- threading [.NET], features
- managed threading
ms.assetid: 239b2e8d-581b-4ca3-992b-0e8525b9321c
ms.openlocfilehash: 8a66904a6db3fa45d8a42dec4e1e42883c1c3e98
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826166"
---
# <a name="threading-objects-and-features"></a><span data-ttu-id="64650-102">執行緒物件和功能</span><span class="sxs-lookup"><span data-stu-id="64650-102">Threading objects and features</span></span>

<span data-ttu-id="64650-103">除了 <xref:System.Threading.Thread?displayProperty=nameWithType> 類別以外，.NET 還會提供一些類別來協助您開發多執行緒應用程式。</span><span class="sxs-lookup"><span data-stu-id="64650-103">Along with the <xref:System.Threading.Thread?displayProperty=nameWithType> class, .NET provides a number of classes that help you develop multithreaded applications.</span></span> <span data-ttu-id="64650-104">下列文章概述這些類別：</span><span class="sxs-lookup"><span data-stu-id="64650-104">The following articles provide overview of those classes:</span></span>

|<span data-ttu-id="64650-105">標題</span><span class="sxs-lookup"><span data-stu-id="64650-105">Title</span></span>|<span data-ttu-id="64650-106">說明</span><span class="sxs-lookup"><span data-stu-id="64650-106">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="64650-107">Managed 執行緒集區</span><span class="sxs-lookup"><span data-stu-id="64650-107">The managed thread pool</span></span>](the-managed-thread-pool.md)|<span data-ttu-id="64650-108">描述 <xref:System.Threading.ThreadPool?displayProperty=nameWithType> 類別，這個類別提供 .NET 受控背景工作執行緒集區。</span><span class="sxs-lookup"><span data-stu-id="64650-108">Describes the <xref:System.Threading.ThreadPool?displayProperty=nameWithType> class, which provides a pool of worker threads that are managed by .NET.</span></span>|  
|[<span data-ttu-id="64650-109">計時器</span><span class="sxs-lookup"><span data-stu-id="64650-109">Timers</span></span>](timers.md)|<span data-ttu-id="64650-110">說明可用於多執行緒環境的 .NET 計時器。</span><span class="sxs-lookup"><span data-stu-id="64650-110">Describes .NET timers that can be used in a multithreaded environment.</span></span>|
|[<span data-ttu-id="64650-111">同步處理原始物件概觀</span><span class="sxs-lookup"><span data-stu-id="64650-111">Overview of synchronization primitives</span></span>](overview-of-synchronization-primitives.md)|<span data-ttu-id="64650-112">描述可用來同步對共用資源的存取或控制執行緒互動的類型。</span><span class="sxs-lookup"><span data-stu-id="64650-112">Describes types that can be used to synchronize access to a shared resource or control thread interaction.</span></span>|
|[<span data-ttu-id="64650-113">EventWaitHandle</span><span class="sxs-lookup"><span data-stu-id="64650-113">EventWaitHandle</span></span>](eventwaithandle.md)|<span data-ttu-id="64650-114">說明 <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType> 類別，該類別代表執行緒同步事件。</span><span class="sxs-lookup"><span data-stu-id="64650-114">Describes the <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType> class, which represents a thread synchronization event.</span></span>|
|[<span data-ttu-id="64650-115">CountdownEvent</span><span class="sxs-lookup"><span data-stu-id="64650-115">CountdownEvent</span></span>](countdownevent.md)|<span data-ttu-id="64650-116">說明 <xref:System.Threading.CountdownEvent?displayProperty=nameWithType> 類別，該類別代表執行緒同步事件，會在計數為零時變成已設定。</span><span class="sxs-lookup"><span data-stu-id="64650-116">Describes the <xref:System.Threading.CountdownEvent?displayProperty=nameWithType> class, which represents a thread synchronization event that becomes set when its count is zero.</span></span>|
|[<span data-ttu-id="64650-117">Mutex</span><span class="sxs-lookup"><span data-stu-id="64650-117">Mutexes</span></span>](mutexes.md)|<span data-ttu-id="64650-118">說明 <xref:System.Threading.Mutex?displayProperty=nameWithType> 類別，該類別能授與對共用資源的獨佔存取權。</span><span class="sxs-lookup"><span data-stu-id="64650-118">Describes the <xref:System.Threading.Mutex?displayProperty=nameWithType> class, which grants exclusive access to a shared resource.</span></span>|
|[<span data-ttu-id="64650-119">Semaphore 和 SemaphoreSlim</span><span class="sxs-lookup"><span data-stu-id="64650-119">Semaphore and SemaphoreSlim</span></span>](semaphore-and-semaphoreslim.md)|<span data-ttu-id="64650-120">描述 <xref:System.Threading.Semaphore?displayProperty=nameWithType> 類別，它能限制可以同時存取共用資源或資源集區的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="64650-120">Describes the <xref:System.Threading.Semaphore?displayProperty=nameWithType> class, which limits number of threads that can access a shared resource or a pool of resources concurrently.</span></span>|
|[<span data-ttu-id="64650-121">屏障</span><span class="sxs-lookup"><span data-stu-id="64650-121">Barrier</span></span>](barrier.md)|<span data-ttu-id="64650-122">說明 <xref:System.Threading.Barrier?displayProperty=nameWithType> 類別，該類別會實作屏障模式以便協調階段式作業中的執行緒。</span><span class="sxs-lookup"><span data-stu-id="64650-122">Describes the <xref:System.Threading.Barrier?displayProperty=nameWithType> class, which implements the barrier pattern for coordination of threads in phased operations.</span></span>|
|[<span data-ttu-id="64650-123">SpinLock</span><span class="sxs-lookup"><span data-stu-id="64650-123">SpinLock</span></span>](spinlock.md)|<span data-ttu-id="64650-124">描述 <xref:System.Threading.SpinLock?displayProperty=nameWithType> 結構，這是適用於特定低階鎖定案例之 <xref:System.Threading.Monitor?displayProperty=nameWithType> 類別的輕量型替代方案。</span><span class="sxs-lookup"><span data-stu-id="64650-124">Describes the <xref:System.Threading.SpinLock?displayProperty=nameWithType> structure, which is a lightweight alternative to the <xref:System.Threading.Monitor?displayProperty=nameWithType> class for certain low-level locking scenarios.</span></span>|
|[<span data-ttu-id="64650-125">SpinWait</span><span class="sxs-lookup"><span data-stu-id="64650-125">SpinWait</span></span>](spinwait.md)|<span data-ttu-id="64650-126">描述 <xref:System.Threading.SpinWait?displayProperty=nameWithType> 結構，它能提供微調式等候的支援。</span><span class="sxs-lookup"><span data-stu-id="64650-126">Describes the <xref:System.Threading.SpinWait?displayProperty=nameWithType> structure, which provides support for spin-based waiting.</span></span>|

## <a name="see-also"></a><span data-ttu-id="64650-127">請參閱</span><span class="sxs-lookup"><span data-stu-id="64650-127">See also</span></span>

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.WaitHandle?displayProperty=nameWithType>
- <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- [<span data-ttu-id="64650-128">使用執行緒和執行緒處理</span><span class="sxs-lookup"><span data-stu-id="64650-128">Using threads and threading</span></span>](using-threads-and-threading.md)
- [<span data-ttu-id="64650-129">非同步檔案 i/o</span><span class="sxs-lookup"><span data-stu-id="64650-129">Asynchronous File I/O</span></span>](../io/asynchronous-file-i-o.md)
- [<span data-ttu-id="64650-130">平行程式設計</span><span class="sxs-lookup"><span data-stu-id="64650-130">Parallel Programming</span></span>](../parallel-programming/index.md)
- [<span data-ttu-id="64650-131">工作平行程式庫 (TPL)</span><span class="sxs-lookup"><span data-stu-id="64650-131">Task Parallel Library (TPL)</span></span>](../parallel-programming/task-parallel-library-tpl.md)
