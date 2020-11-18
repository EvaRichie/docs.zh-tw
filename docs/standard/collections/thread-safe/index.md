---
title: 安全執行緒集合
description: 在 .NET 中使用並存命名空間（包括安全線程和可擴充的集合類別）開始使用安全線程集合。
ms.date: 03/30/2017
helpviewer_keywords:
- thread-safe collections, overview
ms.assetid: 2e7ca21f-786c-4367-96be-0cf3f3dcc6bd
ms.openlocfilehash: 5f64d7b6a9b3564248a2b6113724e948066bf45c
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94827746"
---
# <a name="thread-safe-collections"></a>安全執行緒集合
.NET Framework 4 引進了 <xref:System.Collections.Concurrent?displayProperty=nameWithType> 命名空間，其中包含數個兼具安全執行緒與調整能力的集合類別。 多個執行緒可以安全且有效率地新增或移除這些集合中的項目，而不需要利用使用者程式碼進行額外同步處理。 當您撰寫新的程式碼時，只要多個執行緒將同時寫入集合，就使用並行集合類別。 如果您僅讀取共用集合，則可以使用 <xref:System.Collections.Generic?displayProperty=nameWithType> 命名空間中的類別。 除非您需要將目標設為 .NET Framework 1.1 或舊版本的執行階段，否則建議您不要使用 1.0 集合類別。  
  
## <a name="thread-synchronization-in-the-net-framework-10-and-20-collections"></a>.NET Framework 1.0 和 2.0 集合中的執行緒同步處理  
 您可以在 <xref:System.Collections?displayProperty=nameWithType> 命名空間中找到 .NET Framework 1.0 中引進的集合。 這些包括常用 <xref:System.Collections.ArrayList> 和 <xref:System.Collections.Hashtable> 的集合透過 `Synchronized` 屬性來提供某種安全執行緒，而這個屬性會傳回集合的安全執行緒包裝函式。 包裝函式的運作方式是針對每個新增或移除作業鎖定整個集合。 因此，嘗試存取集合的每個執行緒都必須等待，直到輪到它取得一個鎖定。 這無法進行擴充，而且可能會造成大型集合的重大效能下降。 此外，設計未完全保護競爭情形。 如需詳細資訊，請參閱[泛型集合中的同步處理](/archive/blogs/bclteam/synchronization-in-generic-collections-brian-grunkemeyer)。  
  
 您可以在 <xref:System.Collections.Generic?displayProperty=nameWithType> 命名空間中找到 .NET Framework 2.0 中引進的集合類別， 包括 <xref:System.Collections.Generic.List%601>、<xref:System.Collections.Generic.Dictionary%602> 等。 這些類別提供相較起 .NET Framework 1.0 類別的改良型別安全和效能。 不過，.NET Framework 2.0 集合類別不會提供任何執行緒同步處理；在多個執行緒上同時新增或移除項目時，使用者程式碼必須提供所有同步處理。  
  
 建議您使用 NET Framework 4 中的並行集合類別，因為這些類別不僅提供 .NET Framework 2.0 集合類別的型別安全，而且提供比 .NET Framework 1.0 集合更高的效率及更完整的執行緒安全性。  
  
## <a name="fine-grained-locking-and-lock-free-mechanisms"></a>更細緻的鎖定和無鎖定機制  
 有些並行集合類型會使用輕量型同步處理機制，例如 .NET Framework 4 中新增的 <xref:System.Threading.SpinLock>、<xref:System.Threading.SpinWait>、<xref:System.Threading.SemaphoreSlim> 和 <xref:System.Threading.CountdownEvent>。 這些同步處理型別通常會先使用短期間的 *忙碌旋轉*，再讓執行緒進入真正的 Wait 狀態。 預期等候時間很短時，旋轉的費用遠低於等待，這包含昂貴的核心轉換。 針對使用旋轉的集合類別，這個效率表示多個執行緒可以使用極高的速率來新增和移除項目。 如需旋轉與封鎖比較的詳細資訊，請參閱 [SpinLock](../../threading/spinlock.md) 和 [SpinWait](../../threading/spinwait.md)。  
  
 <xref:System.Collections.Concurrent.ConcurrentQueue%601> 和 <xref:System.Collections.Concurrent.ConcurrentStack%601> 類別完全不使用鎖定。 相反地，它們依賴 <xref:System.Threading.Interlocked> 作業來取得安全執行緒。  
  
> [!NOTE]
> 因為並行集合類別支援 <xref:System.Collections.ICollection>，所以會提供 <xref:System.Collections.ICollection.IsSynchronized%2A> 和 <xref:System.Collections.ICollection.SyncRoot%2A> 屬性的實作，即使這些屬性無關也是一樣。 `IsSynchronized` 一律會傳回 `false`，而 `SyncRoot` 一律為 `null` (在 Visual Basic 中為 `Nothing`)。  
  
 下表列出 <xref:System.Collections.Concurrent?displayProperty=nameWithType> 命名空間中的集合類型。  
  
|類型|說明|  
|----------|-----------------|  
|<xref:System.Collections.Concurrent.BlockingCollection%601>|提供任何可實作 <xref:System.Collections.Concurrent.IProducerConsumerCollection%601> 之類型的界限和封鎖功能。 如需詳細資訊，請參閱 [BlockingCollection 概觀](blockingcollection-overview.md)。|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602>|索引鍵/值組字典的安全執行緒實作。|  
|<xref:System.Collections.Concurrent.ConcurrentQueue%601>|FIFO (先進先出) 佇列的安全執行緒實作。|  
|<xref:System.Collections.Concurrent.ConcurrentStack%601>|LIFO (後進先出) 堆疊的安全執行緒實作。|  
|<xref:System.Collections.Concurrent.ConcurrentBag%601>|未排序元素集合的安全執行緒實作。|  
|<xref:System.Collections.Concurrent.IProducerConsumerCollection%601>|類型必須實作以在 `BlockingCollection` 中使用的介面。|  
  
## <a name="related-topics"></a>相關主題  
  
|標題|說明|  
|-----------|-----------------|  
|[BlockingCollection 概觀](blockingcollection-overview.md)|描述 <xref:System.Collections.Concurrent.BlockingCollection%601> 類型所提供的功能。|  
|[作法：在 ConcurrentDictionary 中新增和移除項目](how-to-add-and-remove-items.md)|描述如何新增和移除 <xref:System.Collections.Concurrent.ConcurrentDictionary%602> 中的項目|  
|[作法：從 BlockingCollection 個別新增和擷取項目](how-to-add-and-take-items.md)|描述在未使用唯讀列舉值的情況下，如何新增和擷取封鎖回收中的項目。|  
|[作法：將界限和封鎖功能新增至集合](how-to-add-bounding-and-blocking.md)|描述如何使用任何集合類別作為 <xref:System.Collections.Concurrent.IProducerConsumerCollection%601> 集合的基礎儲存機制。|  
|[作法：使用 ForEach 來移除 BlockingCollection 中的項目](how-to-use-foreach-to-remove.md)|描述如何使用 `foreach` (在 Visual Basic 中為 `For Each`) 來移除封鎖集合中的所有項目。|  
|[作法：在管線中使用封鎖集合的陣列](how-to-use-arrays-of-blockingcollections.md)|描述如何同時使用多個封鎖回收來實作管線。|  
|[作法：使用 ConcurrentBag 建立物件集區](how-to-create-an-object-pool.md)|示範在您可以重複使用物件而非持續建立新物件的情況下，如何使用並行資料包改善效能。|  
  
## <a name="reference"></a>參考  
 <xref:System.Collections.Concurrent?displayProperty=nameWithType>
