---
title: 如何：啟用 SpinLock 中的執行緒追蹤模式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinLock, how to enable thread-tracking
ms.assetid: 62ee2e68-0bdd-4869-afc9-f0a57a11ae01
ms.openlocfilehash: c33978226a02f65fdc495762af9286ba2daf9454
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723736"
---
# <a name="how-to-enable-thread-tracking-mode-in-spinlock"></a><span data-ttu-id="84caf-102">如何：啟用 SpinLock 中的執行緒追蹤模式</span><span class="sxs-lookup"><span data-stu-id="84caf-102">How to: Enable Thread-Tracking Mode in SpinLock</span></span>

<span data-ttu-id="84caf-103"><xref:System.Threading.SpinLock?displayProperty=nameWithType> 是低階的互斥鎖定，適用於等候時間非常短的案例。</span><span class="sxs-lookup"><span data-stu-id="84caf-103"><xref:System.Threading.SpinLock?displayProperty=nameWithType> is a low-level mutual exclusion lock that you can use for scenarios that have very short wait times.</span></span> <span data-ttu-id="84caf-104"><xref:System.Threading.SpinLock> 是不可重入的。</span><span class="sxs-lookup"><span data-stu-id="84caf-104"><xref:System.Threading.SpinLock> is not re-entrant.</span></span> <span data-ttu-id="84caf-105">當執行緒進入鎖定之後，必須正確地結束鎖定之後，才可再次進入。</span><span class="sxs-lookup"><span data-stu-id="84caf-105">After a thread enters the lock, it must exit the lock correctly before it can enter again.</span></span> <span data-ttu-id="84caf-106">一般而言，重新進入鎖定的任何嘗試都會導致死結，而死結可能很難偵錯。</span><span class="sxs-lookup"><span data-stu-id="84caf-106">Typically, any attempt to re-enter the lock would cause deadlock, and deadlocks can be very difficult to debug.</span></span> <span data-ttu-id="84caf-107">為了協助開發，<xref:System.Threading.SpinLock?displayProperty=nameWithType> 支援一個執行緒追蹤模式，此模式會導致在執行緒嘗試重新進入它已經保留的鎖定時擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="84caf-107">As an aid to development, <xref:System.Threading.SpinLock?displayProperty=nameWithType> supports a thread-tracking mode that causes an exception to be thrown when a thread attempts to re-enter a lock that it already holds.</span></span> <span data-ttu-id="84caf-108">這可讓您更容易找出未正確結束鎖定的點。</span><span class="sxs-lookup"><span data-stu-id="84caf-108">This lets you more easily locate the point at which the lock was not exited correctly.</span></span> <span data-ttu-id="84caf-109">您可以使用採取布林值輸入參數的 <xref:System.Threading.SpinLock> 建構函式並傳入 `true` 的引數，來開啟執行緒追蹤模式。</span><span class="sxs-lookup"><span data-stu-id="84caf-109">You can turn on thread-tracking mode by using the <xref:System.Threading.SpinLock> constructor that takes a Boolean input parameter, and passing in an argument of `true`.</span></span> <span data-ttu-id="84caf-110">當您完成開發和測試階段之後，關閉執行緒追蹤模式以提升效能。</span><span class="sxs-lookup"><span data-stu-id="84caf-110">After you complete the development and testing phases, turn off thread-tracking mode for better performance.</span></span>  
  
## <a name="example"></a><span data-ttu-id="84caf-111">範例</span><span class="sxs-lookup"><span data-stu-id="84caf-111">Example</span></span>  

 <span data-ttu-id="84caf-112">下列範例示範執行緒追蹤模式。</span><span class="sxs-lookup"><span data-stu-id="84caf-112">The following example demonstrates thread-tracking mode.</span></span> <span data-ttu-id="84caf-113">正確結束鎖定的程式碼行會標記為註解，以模擬會導致其中一個下列結果的編碼錯誤：</span><span class="sxs-lookup"><span data-stu-id="84caf-113">The lines that correctly exit the lock are commented out to simulate a coding error that causes one of the following results:</span></span>  
  
- <span data-ttu-id="84caf-114">如果 <xref:System.Threading.SpinLock> 是使用 `true` (在 Visual Basic 中為 `True`) 的引數所建立，即會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="84caf-114">An exception is thrown if the <xref:System.Threading.SpinLock> was created by using an argument of `true` (`True` in Visual Basic).</span></span>  
  
- <span data-ttu-id="84caf-115">如果 <xref:System.Threading.SpinLock> 是使用 `false` (在 Visual Basic 中為 `False`) 的引數所建立，即會鎖死。</span><span class="sxs-lookup"><span data-stu-id="84caf-115">Deadlock if the <xref:System.Threading.SpinLock> was created by using an argument of `false` (`False` in Visual Basic).</span></span>  
  
 [!code-csharp[CDS_SpinLock#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#01)]
 [!code-vb[CDS_SpinLock#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_threadtracking.vb#01)]  
  
## <a name="see-also"></a><span data-ttu-id="84caf-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="84caf-116">See also</span></span>

- [<span data-ttu-id="84caf-117">SpinLock</span><span class="sxs-lookup"><span data-stu-id="84caf-117">SpinLock</span></span>](spinlock.md)
