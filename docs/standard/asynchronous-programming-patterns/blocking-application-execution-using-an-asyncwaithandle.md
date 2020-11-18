---
title: 使用 AsyncWaitHandle 封鎖應用程式執行
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- blocks, asynchronous operations
- ending asynchronous operations
- asynchronous programming, ending operations
- asynchronous programming, blocking applications
- stopping asynchronous operations
- blocking application execution
ms.assetid: 3e32daf2-8161-4e8f-addd-9fd9ff101b03
ms.openlocfilehash: 15750575aaa4f937104bd36db5f9dedd4cd12f0a
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830463"
---
# <a name="blocking-application-execution-using-an-asyncwaithandle"></a>使用 AsyncWaitHandle 封鎖應用程式執行
等待非同步作業的結果而無法繼續執行其他工作的應用程式必須封鎖，直到作業完成為止。 使用下列其中一個選項，在等候非同步作業完成時封鎖應用程式的主執行緒：  
  
- 使用非同步作業 **Begin**_OperationName_ 方法所傳回 <xref:System.IAsyncResult> 的 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 屬性。 本主題將示範這個方法。  
  
- 呼叫非同步作業的 **End**_OperationName_ 方法。 如需示範此方法的範例，請參閱[以結束非同步作業的方式封鎖應用程式執行](blocking-application-execution-by-ending-an-async-operation.md)。  
  
 在非同步作業完成之前，使用一個或多個 <xref:System.Threading.WaitHandle> 物件封鎖的應用程式通常會呼叫 **Begin**_OperationName_ 方法，執行不需作業結果即可完成的任何工作，然後在非同步作業完成之前維持封鎖。 使用 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 來呼叫其中一個 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法，可在單一作業上封鎖應用程式。 若要在等待一組非同步作業完成時封鎖，請將相關的 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 物件儲存在陣列，並呼叫其中一個 <xref:System.Threading.WaitHandle.WaitAll%2A> 方法。 若要在等待一組非同步作業的任何一個作業完成時封鎖，請將相關的 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 物件儲存在陣列，並呼叫其中一個 <xref:System.Threading.WaitHandle.WaitAny%2A> 方法。  
  
## <a name="example"></a>範例  
 下列範例示範在 DNS 類別中使用非同步方法，以擷取使用者指定電腦的網域名稱系統資訊。 此範例示範使用與非同步作業相關聯的 <xref:System.Threading.WaitHandle> 進行封鎖。 請注意，因為使用此方式時並不需要 <xref:System.Net.Dns.BeginGetHostByName%2A>`requestCallback` 與`stateObject` 參數，所以已為其傳遞 `null` (在 Visual Basic 中為 `Nothing`)。  
  
 [!code-csharp[AsyncDesignPattern#2](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/Async_EndBlockWait.cs#2)]
 [!code-vb[AsyncDesignPattern#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/Async_EndBlockWait.vb#2)]  
  
## <a name="see-also"></a>請參閱

- [事件架構非同步模式 (EAP)](event-based-asynchronous-pattern-eap.md)
- [事件架構非同步模式概觀](event-based-asynchronous-pattern-overview.md)
