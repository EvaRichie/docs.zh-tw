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
# <a name="using-an-asynccallback-delegate-to-end-an-asynchronous-operation"></a>使用 AsyncCallback 委派結束非同步作業
可等待非同步作業的結果而執行其他工作的應用程式不應封鎖等待，直到作業完成為止。 使用下列其中一個選項，在等候非同步作業完成時繼續執行指示：  
  
- 使用 <xref:System.AsyncCallback> 委派以處理不同執行緒中非同步作業的結果。 本主題將示範這個方法。  
  
- 使用 <xref:System.IAsyncResult.IsCompleted%2A> <xref:System.IAsyncResult> 非同步作業的 **Begin**_OperationName_ 方法所傳回之的屬性，判斷作業是否已完成。 如需說明這項技巧的範例，請參閱[輪詢非同步作業的狀態](polling-for-the-status-of-an-asynchronous-operation.md)。  
  
## <a name="example"></a>範例  
 下列範例示範在 <xref:System.Net.Dns> 類別中使用非同步方法，以擷取使用者指定電腦的網域名稱系統 (DNS) 資訊。 此範例會建立參考`ProcessDnsInformation`方法的 <xref:System.AsyncCallback> 委派。 此方法會呼叫每一個非同步要求一次以取得 DNS 資訊。  
  
 請注意，使用者指定的主機會傳遞給 <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.Object> 參數。 如需示範定義和使用更複雜狀態物件的範例，請參閱[使用 AsyncCallback 委派和狀態物件](using-an-asynccallback-delegate-and-state-object.md)。  
  
 [!code-csharp[AsyncDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateNoStateObject.cs#4)]
 [!code-vb[AsyncDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateNoState.vb#4)]  
  
## <a name="see-also"></a>請參閱

- [事件架構非同步模式 (EAP)](event-based-asynchronous-pattern-eap.md)
- [事件架構非同步模式概觀](event-based-asynchronous-pattern-overview.md)
- [使用 IAsyncResult 呼叫非同步方法](calling-asynchronous-methods-using-iasyncresult.md)
- [使用 AsyncCallback 委派和狀態物件](using-an-asynccallback-delegate-and-state-object.md)
