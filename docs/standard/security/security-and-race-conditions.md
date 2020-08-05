---
title: 安全性和競爭情形
'description:': Describes pitfalls to avoid around security holes exploited by race conditions, including dispose methods, constructors, cached objects, and finalizers.
ms.date: 07/15/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET], race conditions
- race conditions
- secure coding, race conditions
- code security, race conditions
ms.assetid: ea3edb80-b2e8-4e85-bfed-311b20cb59b6
ms.openlocfilehash: a667bf69ba72cbe203bd2603c4c6b7a1e58a6d43
ms.sourcegitcommit: b7a8b09828bab4e90f66af8d495ecd7024c45042
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87555106"
---
# <a name="security-and-race-conditions"></a><span data-ttu-id="1b784-102">安全性和競爭情形</span><span class="sxs-lookup"><span data-stu-id="1b784-102">Security and Race Conditions</span></span>

<span data-ttu-id="1b784-103">另一個考慮領域，是競爭情形所利用的安全性漏洞的潛能。</span><span class="sxs-lookup"><span data-stu-id="1b784-103">Another area of concern is the potential for security holes exploited by race conditions.</span></span> <span data-ttu-id="1b784-104">有數種方式可能會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="1b784-104">There are several ways in which this might happen.</span></span> <span data-ttu-id="1b784-105">接下來的子主題概述開發人員必須避免的一些主要陷阱。</span><span class="sxs-lookup"><span data-stu-id="1b784-105">The subtopics that follow outline some of the major pitfalls that the developer must avoid.</span></span>  
  
## <a name="race-conditions-in-the-dispose-method"></a><span data-ttu-id="1b784-106">Dispose 方法中的競爭條件</span><span class="sxs-lookup"><span data-stu-id="1b784-106">Race Conditions in the Dispose Method</span></span>  

<span data-ttu-id="1b784-107">如果類別的**dispose**方法 (如需詳細資訊，請參閱[垃圾收集](../garbage-collection/index.md)) 未同步處理，可能會多次執行**Dispose**內的清除程式碼，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="1b784-107">If a class's **Dispose** method (for more information, see [Garbage Collection](../garbage-collection/index.md)) is not synchronized, it is possible that cleanup code inside **Dispose** can be run more than once, as shown in the following example.</span></span>  
  
```vb  
Sub Dispose()  
    If Not (myObj Is Nothing) Then  
       Cleanup(myObj)  
       myObj = Nothing  
    End If  
End Sub  
```  
  
```csharp  
void Dispose()
{  
    if (myObj != null)
    {  
        Cleanup(myObj);  
        myObj = null;  
    }  
}  
```  
  
<span data-ttu-id="1b784-108">因為此**處置**執行不會同步處理，所以第一個 `Cleanup` 執行緒可能會呼叫，而第二個執行緒則會 `_myObj` 設定為**null**。</span><span class="sxs-lookup"><span data-stu-id="1b784-108">Because this **Dispose** implementation is not synchronized, it is possible for `Cleanup` to be called by first one thread and then a second thread before `_myObj` is set to **null**.</span></span> <span data-ttu-id="1b784-109">這是否為安全性考慮，取決於程式碼執行時會發生什麼事 `Cleanup` 。</span><span class="sxs-lookup"><span data-stu-id="1b784-109">Whether this is a security concern depends on what happens when the `Cleanup` code runs.</span></span> <span data-ttu-id="1b784-110">未同步處理**處置**的主要問題牽涉到使用像是檔案之類的資源控制碼。</span><span class="sxs-lookup"><span data-stu-id="1b784-110">A major issue with unsynchronized **Dispose** implementations involves the use of resource handles such as files.</span></span> <span data-ttu-id="1b784-111">不當處置可能會導致使用錯誤的控制碼，這通常會造成安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="1b784-111">Improper disposal can cause the wrong handle to be used, which often leads to security vulnerabilities.</span></span>  
  
## <a name="race-conditions-in-constructors"></a><span data-ttu-id="1b784-112">在函式中的競爭條件</span><span class="sxs-lookup"><span data-stu-id="1b784-112">Race Conditions in Constructors</span></span>

<span data-ttu-id="1b784-113">在某些應用程式中，其他執行緒可能會在其類別的函式完全執行之前存取類別成員。</span><span class="sxs-lookup"><span data-stu-id="1b784-113">In some applications, it might be possible for other threads to access class members before their class constructors have completely run.</span></span> <span data-ttu-id="1b784-114">您應該檢查所有類別的程式，以確保在發生這種情況時沒有安全性問題，或視需要同步處理執行緒。</span><span class="sxs-lookup"><span data-stu-id="1b784-114">You should review all class constructors to make sure that there are no security issues if this should happen, or synchronize threads if necessary.</span></span>  
  
## <a name="race-conditions-with-cached-objects"></a><span data-ttu-id="1b784-115">具有快取物件的競爭條件</span><span class="sxs-lookup"><span data-stu-id="1b784-115">Race Conditions with Cached Objects</span></span>  

<span data-ttu-id="1b784-116">如果類別的其他部分未適當地同步處理，則快取安全性資訊或使用代碼[啟用安全性判斷](../../framework/misc/using-the-assert-method.md)提示作業的程式碼，也可能會受到競爭條件的影響，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="1b784-116">Code that caches security information or uses the code access security [Assert](../../framework/misc/using-the-assert-method.md) operation might also be vulnerable to race conditions if other parts of the class are not appropriately synchronized, as shown in the following example.</span></span>  
  
```vb  
Sub SomeSecureFunction()  
    If SomeDemandPasses() Then  
        fCallersOk = True  
        DoOtherWork()  
        fCallersOk = False  
    End If  
End Sub  
  
Sub DoOtherWork()  
    If fCallersOK Then  
        DoSomethingTrusted()  
    Else  
        DemandSomething()  
        DoSomethingTrusted()  
    End If  
End Sub  
```  
  
```csharp  
void SomeSecureFunction()
{  
    if (SomeDemandPasses())
    {  
        fCallersOk = true;  
        DoOtherWork();  
        fCallersOk = false;  
    }  
}  
void DoOtherWork()
{  
    if (fCallersOK)
    {  
        DoSomethingTrusted();  
    }  
    else
    {  
        DemandSomething();  
        DoSomethingTrusted();  
    }  
}  
```  
  
<span data-ttu-id="1b784-117">如果有其他路徑 `DoOtherWork` 可以從具有相同物件的另一個執行緒呼叫，則不受信任的呼叫端可以超過需求。</span><span class="sxs-lookup"><span data-stu-id="1b784-117">If there are other paths to `DoOtherWork` that can be called from another thread with the same object, an untrusted caller can slip past a demand.</span></span>  
  
<span data-ttu-id="1b784-118">如果您的程式碼會快取安全性資訊，請確定您已針對此弱點進行檢查。</span><span class="sxs-lookup"><span data-stu-id="1b784-118">If your code caches security information, make sure that you review it for this vulnerability.</span></span>  
  
## <a name="race-conditions-in-finalizers"></a><span data-ttu-id="1b784-119">完成項中的競爭條件</span><span class="sxs-lookup"><span data-stu-id="1b784-119">Race Conditions in Finalizers</span></span>  

<span data-ttu-id="1b784-120">競爭條件也可能發生在參考靜態或非受控資源的物件中，然後它會在其完成項中釋出。</span><span class="sxs-lookup"><span data-stu-id="1b784-120">Race conditions can also occur in an object that references a static or unmanaged resource that it then frees in its finalizer.</span></span> <span data-ttu-id="1b784-121">如果多個物件共用在類別的完成項中操作的資源，則物件必須同步處理該資源的所有存取。</span><span class="sxs-lookup"><span data-stu-id="1b784-121">If multiple objects share a resource that is manipulated in a class's finalizer, the objects must synchronize all access to that resource.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1b784-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1b784-122">See also</span></span>

- [<span data-ttu-id="1b784-123">安全程式碼撰寫方針</span><span class="sxs-lookup"><span data-stu-id="1b784-123">Secure Coding Guidelines</span></span>](secure-coding-guidelines.md)
- [<span data-ttu-id="1b784-124">ASP.NET Core 安全性</span><span class="sxs-lookup"><span data-stu-id="1b784-124">ASP.NET Core Security</span></span>](/aspnet/core/security/)
