---
title: 如何：使用 SpinWait 實作兩階段等候作業
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinWait, how to synchronize two-phase wait
ms.assetid: b2ac4e4a-051a-4f65-b4b9-f8e103aff195
ms.openlocfilehash: 4b2bc79a7b652c34334d5a78d9c9af328993ff44
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84279202"
---
# <a name="how-to-use-spinwait-to-implement-a-two-phase-wait-operation"></a><span data-ttu-id="bd2f0-102">如何：使用 SpinWait 實作兩階段等候作業</span><span class="sxs-lookup"><span data-stu-id="bd2f0-102">How to: Use SpinWait to Implement a Two-Phase Wait Operation</span></span>
<span data-ttu-id="bd2f0-103">下列範例示範如何使用 <xref:System.Threading.SpinWait?displayProperty=nameWithType> 物件來實作兩階段等候作業。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-103">The following example shows how to use a <xref:System.Threading.SpinWait?displayProperty=nameWithType> object to implement a two-phase wait operation.</span></span> <span data-ttu-id="bd2f0-104">在第一個階段中，同步處理物件 `Latch` 會在它檢查鎖定是否已變成可用時，進行數個週期的微調。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-104">In the first phase, the synchronization object, a `Latch`, spins for a few cycles while it checks whether the lock has become available.</span></span> <span data-ttu-id="bd2f0-105">在第二個階段中，如果鎖定已變成可用，則 `Wait` 方法會傳回，而不需使用 <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> 來執行等候；否則 `Wait` 會執行等候。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-105">In the second phase, if the lock becomes available, then the `Wait` method returns without using the <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> to perform its wait; otherwise, `Wait` performs the wait.</span></span>  
  
## <a name="example"></a><span data-ttu-id="bd2f0-106">範例</span><span class="sxs-lookup"><span data-stu-id="bd2f0-106">Example</span></span>  
 <span data-ttu-id="bd2f0-107">此範例示範非常基本的閂鎖同步處理原始物件實作。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-107">This example shows a very basic implementation of a Latch synchronization primitive.</span></span> <span data-ttu-id="bd2f0-108">預期等候時間很短時，您就能使用這個資料結構。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-108">You can use this data structure when wait times are expected to be very short.</span></span> <span data-ttu-id="bd2f0-109">此範例僅供示範使用。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-109">This example is for demonstration purposes only.</span></span> <span data-ttu-id="bd2f0-110">如果您在程式中需要閂鎖類型功能，請考慮使用 <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-110">If you require latch-type functionality in your program, consider using <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType>.</span></span>  
  
 [!code-csharp[CDS_SpinWait#03](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinwait/cs/spinwait03.cs#03)]
 [!code-vb[CDS_SpinWait#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinwait/vb/spinwait2.vb#03)]  
  
 <span data-ttu-id="bd2f0-111">閂鎖只會使用 <xref:System.Threading.SpinWait> 物件就地微調，直到下一個對 `SpinOnce` 的呼叫導致 <xref:System.Threading.SpinWait> 讓出執行緒的時間配量。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-111">The latch uses the <xref:System.Threading.SpinWait> object to spin in place only until the next call to `SpinOnce` causes the <xref:System.Threading.SpinWait> to yield the time slice of the thread.</span></span> <span data-ttu-id="bd2f0-112">此時，閂鎖會藉由呼叫 <xref:System.Threading.ManualResetEvent> 上的 <xref:System.Threading.WaitHandle.WaitOne%2A> 並傳入逾時值的其餘部分，以使它自己進行內容切換。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-112">At that point, the latch causes its own context switch by calling <xref:System.Threading.WaitHandle.WaitOne%2A> on the <xref:System.Threading.ManualResetEvent> and passing in the remainder of the time-out value.</span></span>  
  
 <span data-ttu-id="bd2f0-113">記錄輸出會藉由取得鎖定，而不使用 <xref:System.Threading.ManualResetEvent>，來顯示閂鎖能夠提升效能的頻率。</span><span class="sxs-lookup"><span data-stu-id="bd2f0-113">The logging output shows how often the Latch was able to increase performance by acquiring the lock without using the <xref:System.Threading.ManualResetEvent>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="bd2f0-114">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bd2f0-114">See also</span></span>

- [<span data-ttu-id="bd2f0-115">SpinWait</span><span class="sxs-lookup"><span data-stu-id="bd2f0-115">SpinWait</span></span>](spinwait.md)
- [<span data-ttu-id="bd2f0-116">執行緒物件和功能</span><span class="sxs-lookup"><span data-stu-id="bd2f0-116">Threading Objects and Features</span></span>](threading-objects-and-features.md)
