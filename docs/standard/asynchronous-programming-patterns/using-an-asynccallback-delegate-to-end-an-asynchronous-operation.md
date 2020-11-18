---
title: 使用 AsyncCallback 委派結束非同步作業
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ending asynchronous operations
- asynchronous programming, ending operations
- AsyncCallback delegate
- stopping asynchronous operations
ms.assetid: 9d97206c-8917-406c-8961-7d0909d84eeb
ms.openlocfilehash: 55cc78bbfdda97a4d5ec8a2028fb3b0d7a9659e5
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94829124"
---
# <a name="using-an-asynccallback-delegate-to-end-an-asynchronous-operation"></a><span data-ttu-id="47f89-102">使用 AsyncCallback 委派結束非同步作業</span><span class="sxs-lookup"><span data-stu-id="47f89-102">Using an AsyncCallback Delegate to End an Asynchronous Operation</span></span>
<span data-ttu-id="47f89-103">可等待非同步作業的結果而執行其他工作的應用程式不應封鎖等待，直到作業完成為止。</span><span class="sxs-lookup"><span data-stu-id="47f89-103">Applications that can do other work while waiting for the results of an asynchronous operation should not block waiting until the operation completes.</span></span> <span data-ttu-id="47f89-104">使用下列其中一個選項，在等候非同步作業完成時繼續執行指示：</span><span class="sxs-lookup"><span data-stu-id="47f89-104">Use one of the following options to continue executing instructions while waiting for an asynchronous operation to complete:</span></span>  
  
- <span data-ttu-id="47f89-105">使用 <xref:System.AsyncCallback> 委派以處理不同執行緒中非同步作業的結果。</span><span class="sxs-lookup"><span data-stu-id="47f89-105">Use an <xref:System.AsyncCallback> delegate to process the results of the asynchronous operation in a separate thread.</span></span> <span data-ttu-id="47f89-106">本主題將示範這個方法。</span><span class="sxs-lookup"><span data-stu-id="47f89-106">This approach is demonstrated in this topic.</span></span>  
  
- <span data-ttu-id="47f89-107">使用 <xref:System.IAsyncResult.IsCompleted%2A> <xref:System.IAsyncResult> 非同步作業的 **Begin**_OperationName_ 方法所傳回之的屬性，判斷作業是否已完成。</span><span class="sxs-lookup"><span data-stu-id="47f89-107">Use the <xref:System.IAsyncResult.IsCompleted%2A> property of the <xref:System.IAsyncResult> returned by the asynchronous operation's **Begin**_OperationName_ method to determine whether the operation has completed.</span></span> <span data-ttu-id="47f89-108">如需說明這項技巧的範例，請參閱[輪詢非同步作業的狀態](polling-for-the-status-of-an-asynchronous-operation.md)。</span><span class="sxs-lookup"><span data-stu-id="47f89-108">For an example that demonstrates this approach, see [Polling for the Status of an Asynchronous Operation](polling-for-the-status-of-an-asynchronous-operation.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="47f89-109">範例</span><span class="sxs-lookup"><span data-stu-id="47f89-109">Example</span></span>  
 <span data-ttu-id="47f89-110">下列範例示範在 <xref:System.Net.Dns> 類別中使用非同步方法，以擷取使用者指定電腦的網域名稱系統 (DNS) 資訊。</span><span class="sxs-lookup"><span data-stu-id="47f89-110">The following code example demonstrates using asynchronous methods in the <xref:System.Net.Dns> class to retrieve Domain Name System (DNS) information for user-specified computers.</span></span> <span data-ttu-id="47f89-111">此範例會建立參考`ProcessDnsInformation`方法的 <xref:System.AsyncCallback> 委派。</span><span class="sxs-lookup"><span data-stu-id="47f89-111">This example creates an <xref:System.AsyncCallback> delegate that references the `ProcessDnsInformation` method.</span></span> <span data-ttu-id="47f89-112">此方法會呼叫每一個非同步要求一次以取得 DNS 資訊。</span><span class="sxs-lookup"><span data-stu-id="47f89-112">This method is called once for each asynchronous request for DNS information.</span></span>  
  
 <span data-ttu-id="47f89-113">請注意，使用者指定的主機會傳遞給 <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.Object> 參數。</span><span class="sxs-lookup"><span data-stu-id="47f89-113">Note that the user-specified host is passed to the <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.Object> parameter.</span></span> <span data-ttu-id="47f89-114">如需示範定義和使用更複雜狀態物件的範例，請參閱[使用 AsyncCallback 委派和狀態物件](using-an-asynccallback-delegate-and-state-object.md)。</span><span class="sxs-lookup"><span data-stu-id="47f89-114">For an example that demonstrates defining and using a more complex state object, see [Using an AsyncCallback Delegate and State Object](using-an-asynccallback-delegate-and-state-object.md).</span></span>  
  
 [!code-csharp[AsyncDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateNoStateObject.cs#4)]
 [!code-vb[AsyncDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateNoState.vb#4)]  
  
## <a name="see-also"></a><span data-ttu-id="47f89-115">請參閱</span><span class="sxs-lookup"><span data-stu-id="47f89-115">See also</span></span>

- [<span data-ttu-id="47f89-116">事件架構非同步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="47f89-116">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
- [<span data-ttu-id="47f89-117">事件架構非同步模式概觀</span><span class="sxs-lookup"><span data-stu-id="47f89-117">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)
- [<span data-ttu-id="47f89-118">使用 IAsyncResult 呼叫非同步方法</span><span class="sxs-lookup"><span data-stu-id="47f89-118">Calling Asynchronous Methods Using IAsyncResult</span></span>](calling-asynchronous-methods-using-iasyncresult.md)
- [<span data-ttu-id="47f89-119">使用 AsyncCallback 委派和狀態物件</span><span class="sxs-lookup"><span data-stu-id="47f89-119">Using an AsyncCallback Delegate and State Object</span></span>](using-an-asynccallback-delegate-and-state-object.md)
