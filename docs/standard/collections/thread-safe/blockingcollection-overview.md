---
title: BlockingCollection 概觀
description: 深入瞭解 BlockingCollection <T> ，這是 .net 中的安全線程集合類別。 這個類別所提供的功能包括並行新增 & 從許多執行緒中取得專案。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- BlockingCollection, overview
ms.assetid: 987ea3d7-0ad5-4238-8b64-331ce4eb3f0b
ms.openlocfilehash: 550649ae8d5527b96e3a44edf44731c9c0586150
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95733499"
---
# <a name="blockingcollection-overview"></a><span data-ttu-id="6b1f9-104">BlockingCollection 概觀</span><span class="sxs-lookup"><span data-stu-id="6b1f9-104">BlockingCollection Overview</span></span>

<span data-ttu-id="6b1f9-105"><xref:System.Collections.Concurrent.BlockingCollection%601> 是提供下列功能的安全執行緒集合類別︰</span><span class="sxs-lookup"><span data-stu-id="6b1f9-105"><xref:System.Collections.Concurrent.BlockingCollection%601> is a thread-safe collection class that provides the following features:</span></span>  
  
- <span data-ttu-id="6b1f9-106">生產者-消費者模式的實作。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-106">An implementation of the Producer-Consumer pattern.</span></span>  
  
- <span data-ttu-id="6b1f9-107">同時從多個執行緒新增和擷取項目。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-107">Concurrent adding and taking of items from multiple threads.</span></span>  
  
- <span data-ttu-id="6b1f9-108">最佳最大容量。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-108">Optional maximum capacity.</span></span>  
  
- <span data-ttu-id="6b1f9-109">集合是空的或已滿時封鎖的插入和移除作業。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-109">Insertion and removal operations that block when collection is empty or full.</span></span>  
  
- <span data-ttu-id="6b1f9-110">不會封鎖或最多封鎖一段指定時間的插入和移除 "try" 作業。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-110">Insertion and removal "try" operations that do not block or that block up to a specified period of time.</span></span>  
  
- <span data-ttu-id="6b1f9-111">封裝任何可實作 <xref:System.Collections.Concurrent.IProducerConsumerCollection%601> 的集合類別</span><span class="sxs-lookup"><span data-stu-id="6b1f9-111">Encapsulates any collection type that implements <xref:System.Collections.Concurrent.IProducerConsumerCollection%601></span></span>  
  
- <span data-ttu-id="6b1f9-112">具有取消語彙基元的取消作業。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-112">Cancellation with cancellation tokens.</span></span>  
  
- <span data-ttu-id="6b1f9-113">`foreach` 的列舉有兩種 (在 Visual Basic 中為 `For Each`)：</span><span class="sxs-lookup"><span data-stu-id="6b1f9-113">Two kinds of enumeration with `foreach` (`For Each` in Visual Basic):</span></span>  
  
    1. <span data-ttu-id="6b1f9-114">唯讀列舉。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-114">Read-only enumeration.</span></span>  
  
    2. <span data-ttu-id="6b1f9-115">移除所列舉項目的列舉。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-115">Enumeration that removes items as they are enumerated.</span></span>  
  
## <a name="bounding-and-blocking-support"></a><span data-ttu-id="6b1f9-116">界限和封鎖支援</span><span class="sxs-lookup"><span data-stu-id="6b1f9-116">Bounding and Blocking Support</span></span>  

 <span data-ttu-id="6b1f9-117"><xref:System.Collections.Concurrent.BlockingCollection%601> 支援界限和封鎖。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-117"><xref:System.Collections.Concurrent.BlockingCollection%601> supports bounding and blocking.</span></span> <span data-ttu-id="6b1f9-118">界限表示您可以設定集合的最大容量。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-118">Bounding means you can set the maximum capacity of the collection.</span></span> <span data-ttu-id="6b1f9-119">界限在某些情況下十分重要，原因是它可讓您控制記憶體中集合的大小上限，並且防止產生執行緒移到使用執行緒的太前面。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-119">Bounding is important in certain scenarios because it enables you to control the maximum size of the collection in memory, and it prevents the producing threads from moving too far ahead of the consuming threads.</span></span>  
  
 <span data-ttu-id="6b1f9-120">多個執行緒或工作可以同時將項目新增至集合，如果集合達到其指定的最大容量，則會在移除項目之前封鎖產生執行緒。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-120">Multiple threads or tasks can add items to the collection concurrently, and if the collection reaches its specified maximum capacity, the producing threads will block until an item is removed.</span></span> <span data-ttu-id="6b1f9-121">多位消費者可以同時移除項目，如果集合變成空的，則會在生產者新增項目之前封鎖使用執行緒。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-121">Multiple consumers can remove items concurrently, and if the collection becomes empty, the consuming threads will block until a producer adds an item.</span></span> <span data-ttu-id="6b1f9-122">產生執行緒可以呼叫 <xref:System.Collections.Concurrent.BlockingCollection%601.CompleteAdding%2A>，表示無法再新增項目。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-122">A producing thread can call <xref:System.Collections.Concurrent.BlockingCollection%601.CompleteAdding%2A> to indicate that no more items will be added.</span></span> <span data-ttu-id="6b1f9-123">消費者會監視 <xref:System.Collections.Concurrent.BlockingCollection%601.IsCompleted%2A> 屬性，以得知集合何時變成空的，以及何時無法再新增項目。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-123">Consumers monitor the <xref:System.Collections.Concurrent.BlockingCollection%601.IsCompleted%2A> property to know when the collection is empty and no more items will be added.</span></span> <span data-ttu-id="6b1f9-124">下列範例示範界限容量為 100 的簡單 BlockingCollection。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-124">The following example shows a simple BlockingCollection with a bounded capacity of 100.</span></span> <span data-ttu-id="6b1f9-125">只要符合某個外部條件，生產者工作就會將項目新增至集合，然後呼叫 <xref:System.Collections.Concurrent.BlockingCollection%601.CompleteAdding%2A>。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-125">A producer task adds items to the collection as long as some external condition is true, and then calls <xref:System.Collections.Concurrent.BlockingCollection%601.CompleteAdding%2A>.</span></span> <span data-ttu-id="6b1f9-126">在 <xref:System.Collections.Concurrent.BlockingCollection%601.IsCompleted%2A> 屬性為 true 之前，消費者工作會擷取項目。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-126">The consumer task takes items until the <xref:System.Collections.Concurrent.BlockingCollection%601.IsCompleted%2A> property is true.</span></span>  
  
 [!code-csharp[CDS_BlockingCollection#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/blockingcollection.cs#04)]
 [!code-vb[CDS_BlockingCollection#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/introsnippetsbc.vb#04)]  
  
 <span data-ttu-id="6b1f9-127">如需完整範例，請參閱[如何：從 BlockingCollection 個別新增和擷取項目](how-to-add-and-take-items.md)。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-127">For a complete example, see [How to: Add and Take Items Individually from a BlockingCollection](how-to-add-and-take-items.md).</span></span>  
  
## <a name="timed-blocking-operations"></a><span data-ttu-id="6b1f9-128">計時封鎖作業</span><span class="sxs-lookup"><span data-stu-id="6b1f9-128">Timed Blocking Operations</span></span>  

 <span data-ttu-id="6b1f9-129">在界限集合的計時封鎖 <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> 和 <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> 作業上，方法會嘗試新增或擷取項目。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-129">In timed blocking <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> and <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> operations on bounded collections, the method tries to add or take an item.</span></span> <span data-ttu-id="6b1f9-130">如果項目可用，則會將它置入依傳址所傳遞的變數，而且方法會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-130">If an item is available it is placed into the variable that was passed in by reference, and the method returns true.</span></span> <span data-ttu-id="6b1f9-131">如果在指定的逾時期間之後未擷取任何項目，則方法會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-131">If no item is retrieved after a specified time-out period the method returns false.</span></span> <span data-ttu-id="6b1f9-132">執行緒接著可以先執行一些其他有用工作，再重新嘗試存取集合。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-132">The thread is then free to do some other useful work before trying again to access the collection.</span></span> <span data-ttu-id="6b1f9-133">如需計時封鎖存取的範例，請參閱[如何：從 BlockingCollection 個別新增和擷取項目](how-to-add-and-take-items.md)中的第二個範例。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-133">For an example of timed blocking access, see the second example in [How to: Add and Take Items Individually from a BlockingCollection](how-to-add-and-take-items.md).</span></span>  
  
## <a name="cancelling-add-and-take-operations"></a><span data-ttu-id="6b1f9-134">取消新增和擷取作業</span><span class="sxs-lookup"><span data-stu-id="6b1f9-134">Cancelling Add and Take Operations</span></span>  

 <span data-ttu-id="6b1f9-135">新增和擷取作業一般會透過迴圈形式執行。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-135">Add and Take operations are typically performed in a loop.</span></span> <span data-ttu-id="6b1f9-136">您可以將 <xref:System.Threading.CancellationToken> 傳入 <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> 或 <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> 方法來取消迴圈，然後檢查每個反覆項目上語彙基元之 <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-136">You can cancel a loop by passing in a <xref:System.Threading.CancellationToken> to the <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> or <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> method, and then checking the value of the token's <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> property on each iteration.</span></span> <span data-ttu-id="6b1f9-137">如果值為 true，則是由您決定透過清除任何資源並結束迴圈來回應取消要求。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-137">If the value is true, then it is up to you to respond the cancellation request by cleaning up any resources and exiting the loop.</span></span> <span data-ttu-id="6b1f9-138">下列範例示範採用取消語彙基元之 <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> 的多載，以及使用它的程式碼︰</span><span class="sxs-lookup"><span data-stu-id="6b1f9-138">The following example shows an overload of <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> that takes a cancellation token, and the code that uses it:</span></span>  
  
 [!code-csharp[CDS_BlockingCollection#05](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/blockingcollection.cs#05)]
 [!code-vb[CDS_BlockingCollection#05](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/introsnippetsbc.vb#05)]  
  
 <span data-ttu-id="6b1f9-139">如需如何新增取消支援的範例，請參閱[如何：從 BlockingCollection 個別新增和擷取項目](how-to-add-and-take-items.md)中的第二個範例。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-139">For an example of how to add cancellation support, see the second example in [How to: Add and Take Items Individually from a BlockingCollection](how-to-add-and-take-items.md).</span></span>  
  
## <a name="specifying-the-collection-type"></a><span data-ttu-id="6b1f9-140">指定集合類型</span><span class="sxs-lookup"><span data-stu-id="6b1f9-140">Specifying the Collection Type</span></span>  

 <span data-ttu-id="6b1f9-141">在您建立 <xref:System.Collections.Concurrent.BlockingCollection%601> 時，不僅可以指定界限容量，還可以指定要使用的集合類型。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-141">When you create a <xref:System.Collections.Concurrent.BlockingCollection%601>, you can specify not only the bounded capacity but also the type of collection to use.</span></span> <span data-ttu-id="6b1f9-142">例如，您可以針對先進先出 (FIFO) 行為指定 <xref:System.Collections.Concurrent.ConcurrentQueue%601>，或針對後進先出 (LIFO) 行為指定 <xref:System.Collections.Concurrent.ConcurrentStack%601>。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-142">For example, you could specify a <xref:System.Collections.Concurrent.ConcurrentQueue%601> for first in-first out (FIFO) behavior, or a <xref:System.Collections.Concurrent.ConcurrentStack%601> for last in-first out (LIFO) behavior.</span></span> <span data-ttu-id="6b1f9-143">您可以使用任何可實作 <xref:System.Collections.Concurrent.IProducerConsumerCollection%601> 介面的集合類別。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-143">You can use any collection class that implements the <xref:System.Collections.Concurrent.IProducerConsumerCollection%601> interface.</span></span> <span data-ttu-id="6b1f9-144"><xref:System.Collections.Concurrent.BlockingCollection%601> 的預設集合類型為 <xref:System.Collections.Concurrent.ConcurrentQueue%601>。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-144">The default collection type for <xref:System.Collections.Concurrent.BlockingCollection%601> is <xref:System.Collections.Concurrent.ConcurrentQueue%601>.</span></span> <span data-ttu-id="6b1f9-145">下列程式碼範例示範如何建立容量為 1000 並使用 <xref:System.Collections.Concurrent.ConcurrentBag%601> 之字串的 <xref:System.Collections.Concurrent.BlockingCollection%601>：</span><span class="sxs-lookup"><span data-stu-id="6b1f9-145">The following code example shows how to create a <xref:System.Collections.Concurrent.BlockingCollection%601> of strings that has a capacity of 1000 and uses a <xref:System.Collections.Concurrent.ConcurrentBag%601>:</span></span>  
  
```vb  
Dim bc = New BlockingCollection(Of String)(New ConcurrentBag(Of String()), 1000)  
```  
  
```csharp  
BlockingCollection<string> bc = new BlockingCollection<string>(new ConcurrentBag<string>(), 1000 );  
```  
  
 <span data-ttu-id="6b1f9-146">如需詳細資訊，請參閱[操作說明：將界限和封鎖功能加入至集合](how-to-add-bounding-and-blocking.md)。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-146">For more information, see [How to: Add Bounding and Blocking Functionality to a Collection](how-to-add-bounding-and-blocking.md).</span></span>  
  
## <a name="ienumerable-support"></a><span data-ttu-id="6b1f9-147">IEnumerable 支援</span><span class="sxs-lookup"><span data-stu-id="6b1f9-147">IEnumerable Support</span></span>  

 <span data-ttu-id="6b1f9-148"><xref:System.Collections.Concurrent.BlockingCollection%601> 提供 <xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A> 方法讓消費者可以使用 `foreach` (Visual Basic 中的 `For Each`) 移除項目，直到收集完成為止；這表示集合會是空的，而且不會再新增任何項目。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-148"><xref:System.Collections.Concurrent.BlockingCollection%601> provides a <xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A> method that enables consumers to use `foreach` (`For Each` in Visual Basic) to remove items until the collection is completed, which means it is empty and no more items will be added.</span></span> <span data-ttu-id="6b1f9-149">如需詳細資訊，請參閱[如何：使用 ForEach 來移除 BlockingCollection 中的項目](how-to-use-foreach-to-remove.md)。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-149">For more information, see [How to: Use ForEach to Remove Items in a BlockingCollection](how-to-use-foreach-to-remove.md).</span></span>  
  
## <a name="using-many-blockingcollections-as-one"></a><span data-ttu-id="6b1f9-150">將多個 BlockingCollection 當成一個使用</span><span class="sxs-lookup"><span data-stu-id="6b1f9-150">Using Many BlockingCollections As One</span></span>  

 <span data-ttu-id="6b1f9-151">如果消費者需要同時從多個集合擷取項目，您可以建立 <xref:System.Collections.Concurrent.BlockingCollection%601> 陣列，並使用將新增至或擷取自陣列中任何集合的靜態方法 (例如 <xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny%2A> 和 <xref:System.Collections.Concurrent.BlockingCollection%601.AddToAny%2A>)。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-151">For scenarios in which a consumer needs to take items from multiple collections simultaneously, you can create arrays of <xref:System.Collections.Concurrent.BlockingCollection%601> and use the static methods such as <xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny%2A> and <xref:System.Collections.Concurrent.BlockingCollection%601.AddToAny%2A> that will add to or take from any of the collections in the array.</span></span> <span data-ttu-id="6b1f9-152">如果封鎖其中一個集合，則方法會立即嘗試另一個集合，直到找到可執行作業的集合為止。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-152">If one collection is blocking, the method immediately tries another until it finds one that can perform the operation.</span></span> <span data-ttu-id="6b1f9-153">如需詳細資訊，請參閱[如何：在管線中使用封鎖回收的陣列](how-to-use-arrays-of-blockingcollections.md)。</span><span class="sxs-lookup"><span data-stu-id="6b1f9-153">For more information, see [How to: Use Arrays of Blocking Collections in a Pipeline](how-to-use-arrays-of-blockingcollections.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6b1f9-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6b1f9-154">See also</span></span>

- <xref:System.Collections.Concurrent?displayProperty=nameWithType>
- [<span data-ttu-id="6b1f9-155">集合和資料結構</span><span class="sxs-lookup"><span data-stu-id="6b1f9-155">Collections and Data Structures</span></span>](../index.md)
- [<span data-ttu-id="6b1f9-156">安全執行緒集合</span><span class="sxs-lookup"><span data-stu-id="6b1f9-156">Thread-Safe Collections</span></span>](index.md)
