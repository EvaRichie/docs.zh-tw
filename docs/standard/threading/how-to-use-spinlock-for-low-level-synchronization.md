---
title: 操作說明：使用 SpinLock 進行低階同步處理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinLock, how to use
ms.assetid: a9ed3e4e-4f29-4207-b730-ed0a51ecbc19
ms.openlocfilehash: 148ef5e9d5c570ef04bc6e716a884db5e688d91a
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826387"
---
# <a name="how-to-use-spinlock-for-low-level-synchronization"></a><span data-ttu-id="d6229-102">操作說明：使用 SpinLock 進行低階同步處理</span><span class="sxs-lookup"><span data-stu-id="d6229-102">How to: use SpinLock for low-level synchronization</span></span>

<span data-ttu-id="d6229-103">下列範例示範如何使用 <xref:System.Threading.SpinLock>。</span><span class="sxs-lookup"><span data-stu-id="d6229-103">The following example demonstrates how to use a <xref:System.Threading.SpinLock>.</span></span> <span data-ttu-id="d6229-104">在此範例中，重要的區段會執行最少量的工作，因此適合作為 <xref:System.Threading.SpinLock> 的候選項。</span><span class="sxs-lookup"><span data-stu-id="d6229-104">In this example, the critical section performs a minimal amount of work, which makes it a good candidate for a <xref:System.Threading.SpinLock>.</span></span> <span data-ttu-id="d6229-105">相較於標準鎖定，少量增加工作可提升 <xref:System.Threading.SpinLock> 的效能。</span><span class="sxs-lookup"><span data-stu-id="d6229-105">Increasing the work a small amount increases the performance of the <xref:System.Threading.SpinLock> compared to a standard lock.</span></span> <span data-ttu-id="d6229-106">不過，在增加到達某一程度後，SpinLock 的成本就會變成高於標準鎖定。</span><span class="sxs-lookup"><span data-stu-id="d6229-106">However, there is a point at which a SpinLock becomes more expensive than a standard lock.</span></span> <span data-ttu-id="d6229-107">您可以使用程式碼剖析工具中的並行分析功能，來查看哪一種鎖定型別可在您的程式中提供較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="d6229-107">You can use the concurrency profiling functionality in the profiling tools to see which type of lock provides better performance in your program.</span></span> <span data-ttu-id="d6229-108">如需詳細資訊，請參閱[並行視覺化檢視](/visualstudio/profiling/concurrency-visualizer)。</span><span class="sxs-lookup"><span data-stu-id="d6229-108">For more information, see [Concurrency Visualizer](/visualstudio/profiling/concurrency-visualizer).</span></span>  
  
 [!code-csharp[CDS_SpinLock#02](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#02)]
 [!code-vb[CDS_SpinLock#02](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_vb.vb#02)]  
  
 <span data-ttu-id="d6229-109">當共用資源的鎖定不會保留很久時，<xref:System.Threading.SpinLock> 可能很實用。</span><span class="sxs-lookup"><span data-stu-id="d6229-109"><xref:System.Threading.SpinLock> might be useful when a lock on a shared resource is not going to be held for very long.</span></span> <span data-ttu-id="d6229-110">在這類情況下，多核心電腦上的已封鎖執行緒可以有效率地微調幾個週期，直到鎖定釋放為止。</span><span class="sxs-lookup"><span data-stu-id="d6229-110">In such cases, on multi-core computers it can be efficient for the blocked thread to spin for a few cycles until the lock is released.</span></span> <span data-ttu-id="d6229-111">藉由微調，執行緒不會變成鎖定狀態 (這是需要大量 CPU 的程序)。</span><span class="sxs-lookup"><span data-stu-id="d6229-111">By spinning, the thread does not become blocked, which is a CPU-intensive process.</span></span> <span data-ttu-id="d6229-112">在某些情況下，<xref:System.Threading.SpinLock> 將停止微調，以避免耗盡邏輯處理器或在具備超執行緒的系統上反轉優先順序。</span><span class="sxs-lookup"><span data-stu-id="d6229-112"><xref:System.Threading.SpinLock> will stop spinning under certain conditions to prevent starvation of logical processors or priority inversion on systems with Hyper-Threading.</span></span>  
  
 <span data-ttu-id="d6229-113">這個範例會使用 <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> 類別，此類別需要使用者同步處理以進行多執行緒存取。</span><span class="sxs-lookup"><span data-stu-id="d6229-113">This example uses the <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType> class, which requires user synchronization for multi-threaded access.</span></span> <span data-ttu-id="d6229-114">另一個選項是使用 <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType> ，這不需要任何使用者鎖定。</span><span class="sxs-lookup"><span data-stu-id="d6229-114">Another option is to use the <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType>, which does not require any user locks.</span></span>  
  
 <span data-ttu-id="d6229-115">請注意 `false` 在的呼叫中使用 <xref:System.Threading.SpinLock.Exit%2A?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="d6229-115">Note the use of `false` in the call to <xref:System.Threading.SpinLock.Exit%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="d6229-116">這可提供最佳效能。</span><span class="sxs-lookup"><span data-stu-id="d6229-116">This provides the best performance.</span></span> <span data-ttu-id="d6229-117">`true`在 IA64 架構上指定以使用記憶體隔離，這會清除寫入緩衝區，以確保鎖定現在可供其他執行緒進入。</span><span class="sxs-lookup"><span data-stu-id="d6229-117">Specify `true` on IA64 architectures to use the memory fence, which flushes the write buffers to ensure that the lock is now available for other threads to enter.</span></span>
  
## <a name="see-also"></a><span data-ttu-id="d6229-118">請參閱</span><span class="sxs-lookup"><span data-stu-id="d6229-118">See also</span></span>

- [<span data-ttu-id="d6229-119">執行緒物件和功能</span><span class="sxs-lookup"><span data-stu-id="d6229-119">Threading objects and features</span></span>](threading-objects-and-features.md)
- [<span data-ttu-id="d6229-120">lock 陳述式 (C#)</span><span class="sxs-lookup"><span data-stu-id="d6229-120">lock statement (C#)</span></span>](../../csharp/language-reference/keywords/lock-statement.md)
- [<span data-ttu-id="d6229-121">SyncLock 陳述式 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="d6229-121">SyncLock statement (Visual Basic)</span></span>](../../visual-basic/language-reference/statements/synclock-statement.md)
