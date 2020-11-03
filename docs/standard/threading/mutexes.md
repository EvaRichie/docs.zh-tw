---
title: Mutex
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- wait handles
- threading [.NET], Mutex class
- Mutex class, about Mutex class
- threading [.NET], cross-process synchronization
ms.assetid: 9dd06e25-12c0-4a9e-855a-452dc83803e2
ms.openlocfilehash: ba31fff03cfffda7cf2a40a3a82b2222e8951035
ms.sourcegitcommit: 7588b1f16b7608bc6833c05f91ae670c22ef56f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/02/2020
ms.locfileid: "93188987"
---
# <a name="mutexes"></a><span data-ttu-id="ac43d-102">Mutex</span><span class="sxs-lookup"><span data-stu-id="ac43d-102">Mutexes</span></span>

<span data-ttu-id="ac43d-103">您可以使用 <xref:System.Threading.Mutex> 物件來提供獨佔的資源存取權。</span><span class="sxs-lookup"><span data-stu-id="ac43d-103">You can use a <xref:System.Threading.Mutex> object to provide exclusive access to a resource.</span></span> <span data-ttu-id="ac43d-104"><xref:System.Threading.Mutex> 類別所使用的系統資源比 <xref:System.Threading.Monitor> 類別還多，但前者可跨越應用程式定義域的界限進行封送處理、可搭配多個等候使用，並可用來同步處理不同處理序內的執行緒。</span><span class="sxs-lookup"><span data-stu-id="ac43d-104">The <xref:System.Threading.Mutex> class uses more system resources than the <xref:System.Threading.Monitor> class, but it can be marshaled across application domain boundaries, it can be used with multiple waits, and it can be used to synchronize threads in different processes.</span></span> <span data-ttu-id="ac43d-105">如需受管理之同步處理機制的比較，請參閱[同步處理原始物件概觀](overview-of-synchronization-primitives.md)。</span><span class="sxs-lookup"><span data-stu-id="ac43d-105">For a comparison of managed synchronization mechanisms, see [Overview of Synchronization Primitives](overview-of-synchronization-primitives.md).</span></span>  
  
 <span data-ttu-id="ac43d-106">如需程式碼範例，請參閱 <xref:System.Threading.Mutex.%23ctor%2A> 建構函式的參考文件。</span><span class="sxs-lookup"><span data-stu-id="ac43d-106">For code examples, see the reference documentation for the <xref:System.Threading.Mutex.%23ctor%2A> constructors.</span></span>  
  
## <a name="using-mutexes"></a><span data-ttu-id="ac43d-107">使用 Mutex</span><span class="sxs-lookup"><span data-stu-id="ac43d-107">Using Mutexes</span></span>  
 <span data-ttu-id="ac43d-108">執行緒會呼叫 Mutex 的 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法來要求擁有權。</span><span class="sxs-lookup"><span data-stu-id="ac43d-108">A thread calls the <xref:System.Threading.WaitHandle.WaitOne%2A> method of a mutex to request ownership.</span></span> <span data-ttu-id="ac43d-109">該呼叫會封鎖起來，直到 Mutex 可供使用或直到選擇性的逾時間隔時間過去。</span><span class="sxs-lookup"><span data-stu-id="ac43d-109">The call blocks until the mutex is available, or until the optional timeout interval elapses.</span></span> <span data-ttu-id="ac43d-110">如果沒有任何執行緒擁有 Mutex，則 Mutex 的狀態為已發出訊號。</span><span class="sxs-lookup"><span data-stu-id="ac43d-110">The state of a mutex is signaled if no thread owns it.</span></span>  
  
 <span data-ttu-id="ac43d-111">執行緒會藉由呼叫 Mutex 的 <xref:System.Threading.Mutex.ReleaseMutex%2A> 方法來釋放它。</span><span class="sxs-lookup"><span data-stu-id="ac43d-111">A thread releases a mutex by calling its <xref:System.Threading.Mutex.ReleaseMutex%2A> method.</span></span> <span data-ttu-id="ac43d-112">Mutex 具有執行緒相似性；也就是說，Mutex 的釋放只能由擁有該 Mutex 的執行緒來執行。</span><span class="sxs-lookup"><span data-stu-id="ac43d-112">Mutexes have thread affinity; that is, the mutex can be released only by the thread that owns it.</span></span> <span data-ttu-id="ac43d-113">如果執行緒釋放非它擁有的 Mutex，執行緒中就會擲回 <xref:System.ApplicationException>。</span><span class="sxs-lookup"><span data-stu-id="ac43d-113">If a thread releases a mutex it does not own, an <xref:System.ApplicationException> is thrown in the thread.</span></span>  
  
 <span data-ttu-id="ac43d-114">因為 <xref:System.Threading.Mutex> 類別衍生自 <xref:System.Threading.WaitHandle>，您也可以呼叫 <xref:System.Threading.WaitHandle> 的靜態 <xref:System.Threading.WaitHandle.WaitAll%2A> 或 <xref:System.Threading.WaitHandle.WaitAny%2A> 方法，搭配其他等候控制代碼來要求 <xref:System.Threading.Mutex> 的擁有權。</span><span class="sxs-lookup"><span data-stu-id="ac43d-114">Because the <xref:System.Threading.Mutex> class derives from <xref:System.Threading.WaitHandle>, you can also call the static <xref:System.Threading.WaitHandle.WaitAll%2A> or <xref:System.Threading.WaitHandle.WaitAny%2A> methods of <xref:System.Threading.WaitHandle> to request ownership of a <xref:System.Threading.Mutex> in combination with other wait handles.</span></span>  
  
 <span data-ttu-id="ac43d-115">如果執行緒擁有 <xref:System.Threading.Mutex>，該執行緒就能在重複的等候要求呼叫中指定相同的 <xref:System.Threading.Mutex>，而不需封鎖其執行；但是，它也必須進行相同次數的 <xref:System.Threading.Mutex> 釋放作業，以釋放擁有權。</span><span class="sxs-lookup"><span data-stu-id="ac43d-115">If a thread owns a <xref:System.Threading.Mutex>, that thread can specify the same <xref:System.Threading.Mutex> in repeated wait-request calls without blocking its execution; however, it must release the <xref:System.Threading.Mutex> as many times to release ownership.</span></span>  
  
## <a name="abandoned-mutexes"></a><span data-ttu-id="ac43d-116">遭到放棄的 Mutex</span><span class="sxs-lookup"><span data-stu-id="ac43d-116">Abandoned Mutexes</span></span>  
 <span data-ttu-id="ac43d-117">如果執行緒終止時未釋放 <xref:System.Threading.Mutex>，就表示已放棄 Mutex。</span><span class="sxs-lookup"><span data-stu-id="ac43d-117">If a thread terminates without releasing a <xref:System.Threading.Mutex>, the mutex is said to be abandoned.</span></span> <span data-ttu-id="ac43d-118">這通常代表程式在設計上有嚴重錯誤，因為 Mutex 所保護的資源可能仍處於不一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="ac43d-118">This often indicates a serious programming error because the resource the mutex is protecting might be left in an inconsistent state.</span></span> <span data-ttu-id="ac43d-119"><xref:System.Threading.AbandonedMutexException>在下一個取得 mutex 的執行緒中擲回。</span><span class="sxs-lookup"><span data-stu-id="ac43d-119">An <xref:System.Threading.AbandonedMutexException> is thrown in the next thread that acquires the mutex.</span></span>
  
 <span data-ttu-id="ac43d-120">如果是全系統 Mutex，遭到放棄的 Mutex 可能表示應用程式已意外終止 (例如，透過使用「Windows 工作管理員」)。</span><span class="sxs-lookup"><span data-stu-id="ac43d-120">In the case of a system-wide mutex, an abandoned mutex might indicate that an application has been terminated abruptly (for example, by using Windows Task Manager).</span></span>  
  
## <a name="local-and-system-mutexes"></a><span data-ttu-id="ac43d-121">本機和系統 Mutex</span><span class="sxs-lookup"><span data-stu-id="ac43d-121">Local and System Mutexes</span></span>  
 <span data-ttu-id="ac43d-122">Mutex 有兩種類型︰本機 Mutex 和具名的系統 Mutex。</span><span class="sxs-lookup"><span data-stu-id="ac43d-122">Mutexes are of two types: local mutexes and named system mutexes.</span></span> <span data-ttu-id="ac43d-123">如果您使用可接受名稱的建構函式來建立 <xref:System.Threading.Mutex> 物件，該物件便會與該名稱的作業系統物件相關聯。</span><span class="sxs-lookup"><span data-stu-id="ac43d-123">If you create a <xref:System.Threading.Mutex> object using a constructor that accepts a name, it is associated with an operating-system object of that name.</span></span> <span data-ttu-id="ac43d-124">具名的系統 Mutex 能在整個作業系統中看到，而且可用來同步處理處理序的活動。</span><span class="sxs-lookup"><span data-stu-id="ac43d-124">Named system mutexes are visible throughout the operating system and can be used to synchronize the activities of processes.</span></span> <span data-ttu-id="ac43d-125">您可以建立多個 <xref:System.Threading.Mutex> 物件來代表同一個具名系統 Mutex，而且可以使用 <xref:System.Threading.Mutex.OpenExisting%2A> 方法來開啟現有的具名系統 Mutex。</span><span class="sxs-lookup"><span data-stu-id="ac43d-125">You can create multiple <xref:System.Threading.Mutex> objects that represent the same named system mutex, and you can use the <xref:System.Threading.Mutex.OpenExisting%2A> method to open an existing named system mutex.</span></span>  
  
 <span data-ttu-id="ac43d-126">本機 Mutex只存在於您的處理序內。</span><span class="sxs-lookup"><span data-stu-id="ac43d-126">A local mutex exists only within your process.</span></span> <span data-ttu-id="ac43d-127">在處理序內，只要是參考了本機 <xref:System.Threading.Mutex> 物件的執行緒，就可使用本機 Mutex。</span><span class="sxs-lookup"><span data-stu-id="ac43d-127">It can be used by any thread in your process that has a reference to the local <xref:System.Threading.Mutex> object.</span></span> <span data-ttu-id="ac43d-128">每個 <xref:System.Threading.Mutex> 物件都是獨立的本機 Mutex。</span><span class="sxs-lookup"><span data-stu-id="ac43d-128">Each <xref:System.Threading.Mutex> object is a separate local mutex.</span></span>  
  
### <a name="access-control-security-for-system-mutexes"></a><span data-ttu-id="ac43d-129">系統 Mutex 的存取控制安全性</span><span class="sxs-lookup"><span data-stu-id="ac43d-129">Access Control Security for System Mutexes</span></span>  

<span data-ttu-id="ac43d-130">.NET 提供針對命名系統物件查詢和設定 Windows 存取控制安全性的能力。</span><span class="sxs-lookup"><span data-stu-id="ac43d-130">.NET provides the ability to query and set Windows access control security for named system objects.</span></span> <span data-ttu-id="ac43d-131">我們會建議您在建立系統 Mutex 後就為其提供保護，因為系統物件為全域所有，因此非您所擁有的程式碼也可將其鎖定。</span><span class="sxs-lookup"><span data-stu-id="ac43d-131">Protecting system mutexes from the moment of creation is recommended because system objects are global and therefore can be locked by code other than your own.</span></span>  
  
 <span data-ttu-id="ac43d-132">如需適用於 Mutex 的存取控制安全性相關資訊，請參閱 <xref:System.Security.AccessControl.MutexSecurity> 和 <xref:System.Security.AccessControl.MutexAccessRule> 類別、<xref:System.Security.AccessControl.MutexRights> 列舉、<xref:System.Threading.Mutex.GetAccessControl%2A>、<xref:System.Threading.Mutex.SetAccessControl%2A>、<xref:System.Threading.Mutex> 類別的 <xref:System.Threading.Mutex.OpenExisting%2A> 方法，以及 <xref:System.Threading.Mutex.%23ctor%28System.Boolean%2CSystem.String%2CSystem.Boolean%40%2CSystem.Security.AccessControl.MutexSecurity%29> 建構函式。</span><span class="sxs-lookup"><span data-stu-id="ac43d-132">For information on access control security for mutexes, see the <xref:System.Security.AccessControl.MutexSecurity> and <xref:System.Security.AccessControl.MutexAccessRule> classes, the <xref:System.Security.AccessControl.MutexRights> enumeration, the <xref:System.Threading.Mutex.GetAccessControl%2A>, <xref:System.Threading.Mutex.SetAccessControl%2A>, and <xref:System.Threading.Mutex.OpenExisting%2A> methods of the <xref:System.Threading.Mutex> class, and the <xref:System.Threading.Mutex.%23ctor%28System.Boolean%2CSystem.String%2CSystem.Boolean%40%2CSystem.Security.AccessControl.MutexSecurity%29> constructor.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ac43d-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="ac43d-133">See also</span></span>

- <xref:System.Threading.Mutex?displayProperty=nameWithType>
- <xref:System.Threading.Mutex.%23ctor%2A>
- <xref:System.Security.AccessControl.MutexSecurity?displayProperty=nameWithType>
- <xref:System.Security.AccessControl.MutexAccessRule?displayProperty=nameWithType>
- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- [<span data-ttu-id="ac43d-134">執行緒物件和功能</span><span class="sxs-lookup"><span data-stu-id="ac43d-134">Threading objects and features</span></span>](threading-objects-and-features.md)
- [<span data-ttu-id="ac43d-135">執行緒和執行緒</span><span class="sxs-lookup"><span data-stu-id="ac43d-135">Threads and threading</span></span>](threads-and-threading.md)
- [<span data-ttu-id="ac43d-136">執行緒</span><span class="sxs-lookup"><span data-stu-id="ac43d-136">Threading</span></span>](index.md)
