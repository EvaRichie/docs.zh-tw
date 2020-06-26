---
title: gcManagedToUnmanaged MDA
description: 請參閱錯誤 gcmanagedtounmanaged managed 偵錯工具。 此 MDA 可能會因為在轉換到非受控碼期間過早垃圾收集而啟動。
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), garbage collection
- GcManagedToUnmanaged MDA
- GC managed to unmanaged
- transitioning threads managed to unmanaged code
- threading [.NET Framework], garbage collection
- managed to unmanaged garbage collection
- managed debugging assistants (MDAs), garbage collection
- threading [.NET Framework], managed debugging assistants
- garbage collection, run-time errors
ms.assetid: 7417f837-805e-4fed-a430-ca919c8421dc
ms.openlocfilehash: 76c621a1f2bb780d38228f2a84d4c77441774770
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85415910"
---
# <a name="gcmanagedtounmanaged-mda"></a><span data-ttu-id="3e608-104">gcManagedToUnmanaged MDA</span><span class="sxs-lookup"><span data-stu-id="3e608-104">gcManagedToUnmanaged MDA</span></span>
<span data-ttu-id="3e608-105">每當執行緒從 Managed 轉換到 Unmanaged 程式碼時，`gcManagedToUnmanaged` Managed 偵錯助理 (MDA) 會造成記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="3e608-105">The `gcManagedToUnmanaged` managed debugging assistant (MDA) causes a garbage collection whenever a thread transitions from managed to unmanaged code.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="3e608-106">徵狀</span><span class="sxs-lookup"><span data-stu-id="3e608-106">Symptoms</span></span>  
 <span data-ttu-id="3e608-107">嘗試使用已公開至 COM 的 Managed 物件時，Unmanaged 使用者元件會擲回存取違規。</span><span class="sxs-lookup"><span data-stu-id="3e608-107">An unmanaged user component throws an access violation when trying to use a managed object that had been exposed to COM.</span></span> <span data-ttu-id="3e608-108">COM 物件似乎已發行。</span><span class="sxs-lookup"><span data-stu-id="3e608-108">The COM object appears to have been released.</span></span> <span data-ttu-id="3e608-109">存取違規不具決定性。</span><span class="sxs-lookup"><span data-stu-id="3e608-109">The access violation is nondeterministic.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="3e608-110">原因</span><span class="sxs-lookup"><span data-stu-id="3e608-110">Cause</span></span>  
 <span data-ttu-id="3e608-111">如果 Unmanaged 元件不是正確計算 Managed COM 物件的參考，執行階段可以收集已公開至 COM 的 Managed 物件，而 Unmanaged 元件仍會保存物件的參考。</span><span class="sxs-lookup"><span data-stu-id="3e608-111">If an unmanaged component is not reference counting a managed COM object correctly, then the runtime could collect a managed object exposed to COM when the unmanaged component still holds a reference to the object.</span></span> <span data-ttu-id="3e608-112">執行階段會在記憶體回收期間呼叫 <xref:System.Runtime.InteropServices.Marshal.Release%2A>，因此如果使用者元件在發生記憶體回收之前使用物件，就不會被回收。</span><span class="sxs-lookup"><span data-stu-id="3e608-112">The runtime calls <xref:System.Runtime.InteropServices.Marshal.Release%2A> during garbage collections, so if the user component uses the object before the garbage collection occurs, then it will not yet have been collected.</span></span> <span data-ttu-id="3e608-113">這是不具決定性的來源。</span><span class="sxs-lookup"><span data-stu-id="3e608-113">This is the source of the nondeterminism.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="3e608-114">解決方案</span><span class="sxs-lookup"><span data-stu-id="3e608-114">Resolution</span></span>  
 <span data-ttu-id="3e608-115">啟用此助理可減少從物件可供回收，到呼叫 <xref:System.Runtime.InteropServices.Marshal.Release%2A> 之間的時間，有助於追蹤哪一個 Unmanaged 元件最先嘗試存取已收集的物件。</span><span class="sxs-lookup"><span data-stu-id="3e608-115">Enabling this assistant reduces the time between when the object is eligible for collection and <xref:System.Runtime.InteropServices.Marshal.Release%2A> is called, helping to track down which unmanaged component first tries to access the collected object.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="3e608-116">對執行階段的影響</span><span class="sxs-lookup"><span data-stu-id="3e608-116">Effect on the Runtime</span></span>  
 <span data-ttu-id="3e608-117">每當執行緒從 Managed 轉換到 Unmanaged 程式碼時，會造成記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="3e608-117">Causes a garbage collection whenever a thread transitions from managed to unmanaged code.</span></span>  
  
## <a name="output"></a><span data-ttu-id="3e608-118">輸出</span><span class="sxs-lookup"><span data-stu-id="3e608-118">Output</span></span>  
 <span data-ttu-id="3e608-119">此 MDA 不會產生輸出。</span><span class="sxs-lookup"><span data-stu-id="3e608-119">This MDA produces no output.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="3e608-120">設定</span><span class="sxs-lookup"><span data-stu-id="3e608-120">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <gcManagedToUnmanaged/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="3e608-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3e608-121">See also</span></span>

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [<span data-ttu-id="3e608-122">使用 Managed 偵錯助理診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="3e608-122">Diagnosing Errors with Managed Debugging Assistants</span></span>](diagnosing-errors-with-managed-debugging-assistants.md)
- [<span data-ttu-id="3e608-123">Interop 封送處理</span><span class="sxs-lookup"><span data-stu-id="3e608-123">Interop Marshaling</span></span>](../interop/interop-marshaling.md)
- [<span data-ttu-id="3e608-124">gcUnmanagedToManaged</span><span class="sxs-lookup"><span data-stu-id="3e608-124">gcUnmanagedToManaged</span></span>](gcunmanagedtomanaged-mda.md)
