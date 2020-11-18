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
# <a name="threading-objects-and-features"></a>執行緒物件和功能

除了 <xref:System.Threading.Thread?displayProperty=nameWithType> 類別以外，.NET 還會提供一些類別來協助您開發多執行緒應用程式。 下列文章概述這些類別：

|標題|說明|  
|-----------|-----------------|  
|[Managed 執行緒集區](the-managed-thread-pool.md)|描述 <xref:System.Threading.ThreadPool?displayProperty=nameWithType> 類別，這個類別提供 .NET 受控背景工作執行緒集區。|  
|[計時器](timers.md)|說明可用於多執行緒環境的 .NET 計時器。|
|[同步處理原始物件概觀](overview-of-synchronization-primitives.md)|描述可用來同步對共用資源的存取或控制執行緒互動的類型。|
|[EventWaitHandle](eventwaithandle.md)|說明 <xref:System.Threading.EventWaitHandle?displayProperty=nameWithType> 類別，該類別代表執行緒同步事件。|
|[CountdownEvent](countdownevent.md)|說明 <xref:System.Threading.CountdownEvent?displayProperty=nameWithType> 類別，該類別代表執行緒同步事件，會在計數為零時變成已設定。|
|[Mutex](mutexes.md)|說明 <xref:System.Threading.Mutex?displayProperty=nameWithType> 類別，該類別能授與對共用資源的獨佔存取權。|
|[Semaphore 和 SemaphoreSlim](semaphore-and-semaphoreslim.md)|描述 <xref:System.Threading.Semaphore?displayProperty=nameWithType> 類別，它能限制可以同時存取共用資源或資源集區的執行緒數目。|
|[屏障](barrier.md)|說明 <xref:System.Threading.Barrier?displayProperty=nameWithType> 類別，該類別會實作屏障模式以便協調階段式作業中的執行緒。|
|[SpinLock](spinlock.md)|描述 <xref:System.Threading.SpinLock?displayProperty=nameWithType> 結構，這是適用於特定低階鎖定案例之 <xref:System.Threading.Monitor?displayProperty=nameWithType> 類別的輕量型替代方案。|
|[SpinWait](spinwait.md)|描述 <xref:System.Threading.SpinWait?displayProperty=nameWithType> 結構，它能提供微調式等候的支援。|

## <a name="see-also"></a>請參閱

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.WaitHandle?displayProperty=nameWithType>
- <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- [使用執行緒和執行緒處理](using-threads-and-threading.md)
- [非同步檔案 i/o](../io/asynchronous-file-i-o.md)
- [平行程式設計](../parallel-programming/index.md)
- [工作平行程式庫 (TPL)](../parallel-programming/task-parallel-library-tpl.md)
