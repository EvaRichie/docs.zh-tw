---
title: 輪詢非同步作業的狀態
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- asynchronous programming, status polling
- polling asynchronous operation status
- status information [.NET Framework], asynchronous operations
ms.assetid: b541af31-dacb-4e20-8847-1b1ff7c35363
ms.openlocfilehash: f10b4ae5617edc8cf8a38a6cbac999e10a935dc2
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291379"
---
# <a name="polling-for-the-status-of-an-asynchronous-operation"></a><span data-ttu-id="1c4db-102">輪詢非同步作業的狀態</span><span class="sxs-lookup"><span data-stu-id="1c4db-102">Polling for the Status of an Asynchronous Operation</span></span>
<span data-ttu-id="1c4db-103">可等待非同步作業的結果而執行其他工作的應用程式不應封鎖等待，直到作業完成為止。</span><span class="sxs-lookup"><span data-stu-id="1c4db-103">Applications that can do other work while waiting for the results of an asynchronous operation should not block waiting until the operation completes.</span></span> <span data-ttu-id="1c4db-104">使用下列其中一個選項，在等候非同步作業完成時繼續執行指示：</span><span class="sxs-lookup"><span data-stu-id="1c4db-104">Use one of the following options to continue executing instructions while waiting for an asynchronous operation to complete:</span></span>  
  
- <span data-ttu-id="1c4db-105">使用 <xref:System.IAsyncResult.IsCompleted%2A> <xref:System.IAsyncResult> 非同步作業的**Begin**_OperationName_方法所傳回之的屬性，來判斷作業是否已完成。</span><span class="sxs-lookup"><span data-stu-id="1c4db-105">Use the <xref:System.IAsyncResult.IsCompleted%2A> property of the <xref:System.IAsyncResult> returned by the asynchronous operation's **Begin**_OperationName_ method to determine whether the operation has completed.</span></span> <span data-ttu-id="1c4db-106">此方法稱為輪詢且會在本主題中示範。</span><span class="sxs-lookup"><span data-stu-id="1c4db-106">This approach is known as polling and is demonstrated in this topic.</span></span>  
  
- <span data-ttu-id="1c4db-107">使用 <xref:System.AsyncCallback> 委派以處理不同執行緒中非同步作業的結果。</span><span class="sxs-lookup"><span data-stu-id="1c4db-107">Use an <xref:System.AsyncCallback> delegate to process the results of the asynchronous operation in a separate thread.</span></span> <span data-ttu-id="1c4db-108">如需示範此方法的範例，請參閱[使用 AsyncCallback 委派結束非同步作業](using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)。</span><span class="sxs-lookup"><span data-stu-id="1c4db-108">For an example that demonstrates this approach, see [Using an AsyncCallback Delegate to End an Asynchronous Operation](using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="1c4db-109">範例</span><span class="sxs-lookup"><span data-stu-id="1c4db-109">Example</span></span>  
 <span data-ttu-id="1c4db-110">下列範例示範在 <xref:System.Net.Dns> 類別中使用非同步方法，以擷取使用者指定電腦的網域名稱系統資訊。</span><span class="sxs-lookup"><span data-stu-id="1c4db-110">The following code example demonstrates using asynchronous methods in the <xref:System.Net.Dns> class to retrieve Domain Name System information for a user-specified computer.</span></span> <span data-ttu-id="1c4db-111">此範例會啟動非同步作業，然後在主控台中列印句點 (".")，直到作業完成為止。</span><span class="sxs-lookup"><span data-stu-id="1c4db-111">This example starts the asynchronous operation and then prints periods (".") at the console until the operation is complete.</span></span> <span data-ttu-id="1c4db-112">請注意，因為使用此方式時並不需要 <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.AsyncCallback> 與 <xref:System.Object> 參數，所以已為這些引數傳遞 **null** (在 Visual Basic 中為 **Nothing**)。</span><span class="sxs-lookup"><span data-stu-id="1c4db-112">Note that **null** (**Nothing** in Visual Basic) is passed for the <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.AsyncCallback> and <xref:System.Object> parameters because these arguments are not required when using this approach.</span></span>  
  
 [!code-csharp[AsyncDesignPattern#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_Poll.cs#3)]
 [!code-vb[AsyncDesignPattern#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_Poll.vb#3)]  
  
## <a name="see-also"></a><span data-ttu-id="1c4db-113">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1c4db-113">See also</span></span>

- [<span data-ttu-id="1c4db-114">事件架構非同步模式 (EAP)</span><span class="sxs-lookup"><span data-stu-id="1c4db-114">Event-based Asynchronous Pattern (EAP)</span></span>](event-based-asynchronous-pattern-eap.md)
- [<span data-ttu-id="1c4db-115">事件架構非同步模式概觀</span><span class="sxs-lookup"><span data-stu-id="1c4db-115">Event-based Asynchronous Pattern Overview</span></span>](event-based-asynchronous-pattern-overview.md)
