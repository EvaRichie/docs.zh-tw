---
title: 非同步程式設計模型 (APM)
description: 瞭解 .NET 中的非同步程式設計模型（APM）。 探索如何開始和結束非同步作業。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- ending asynchronous operations
- starting asynchronous operations
- beginning asynchronous operations
- asynchronous programming, ending operations
- asynchronous programming
- stopping asynchronous operations
- asynchronous programming, beginning operations
ms.assetid: c9b3501e-6bc6-40f9-8efd-4b6d9e39ccf0
ms.openlocfilehash: 5ab5d15d24aac80ef4a31c039f7af9dacce4a8d8
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84769180"
---
# <a name="asynchronous-programming-model-apm"></a>非同步程式設計模型 (APM)
使用 <xref:System.IAsyncResult> 設計模式的非同步作業會實作為兩種方法，一種名為 `BeginOperationName`，另一種名為 `EndOperationName`，這兩種方法分別負責開始和結束非同步作業 *OperationName*。 例如， <xref:System.IO.FileStream> 類別提供 <xref:System.IO.FileStream.BeginRead%2A> 和 <xref:System.IO.FileStream.EndRead%2A> 方法，以非同步方式讀取檔案的位元組。 這些方法實作 <xref:System.IO.FileStream.Read%2A> 方法的非同步版本。  
  
> [!NOTE]
> 從 .NET Framework 4 開始，工作平行程式庫會為非同步處理和平行程式設計提供新的模型。 如需詳細資訊，請參閱 [Task Parallel Library (TPL)](../parallel-programming/task-parallel-library-tpl.md) 和 [Task-based Asynchronous Pattern (TAP)](task-based-asynchronous-pattern-tap.md)。  
  
 呼叫 `BeginOperationName` 之後，應用程式可以繼續對進行呼叫的執行緒執行指令，而非同步作業會在不同的執行緒上執行。 每次呼叫 `BeginOperationName` 後，應用程式也要呼叫 `EndOperationName` 才能取得作業的結果。  
  
## <a name="beginning-an-asynchronous-operation"></a>開始非同步作業  
 `BeginOperationName` 方法開始非同步作業 *OperationName*，並傳回實作 <xref:System.IAsyncResult> 介面的物件。 <xref:System.IAsyncResult> 物件會儲存非同步作業的相關資訊。 下表顯示非同步作業的相關資訊。  
  
|member|描述|  
|------------|-----------------|  
|<xref:System.IAsyncResult.AsyncState%2A>|選擇性的應用程式特定物件，其中包含非同步作業的相關資訊。|  
|<xref:System.IAsyncResult.AsyncWaitHandle%2A>|<xref:System.Threading.WaitHandle> 可用來封鎖應用程式執行，直到非同步作業完成。|  
|<xref:System.IAsyncResult.CompletedSynchronously%2A>|這個值指出，非同步作業是否是在用來呼叫 `BeginOperationName` 的執行緒上完成的，而不是在個別 <xref:System.Threading.ThreadPool> 執行緒上完成。|  
|<xref:System.IAsyncResult.IsCompleted%2A>|指出非同步作業是否完成的值。|  
  
 `BeginOperationName` 方法會使用任何方法同步版本簽章中所宣告，以傳值或傳址方式傳遞的參數。 任何 out 參數都不是 `BeginOperationName` 方法簽章的一部分。 `BeginOperationName` 方法簽章還包括另外兩個參數。 它們之中的第一個定義 <xref:System.AsyncCallback> 委派，參考非同步作業完成時呼叫的方法。 如果不想在作業完成時叫用方法，呼叫端可以指定 `null` (在 Visual Basic 中為`Nothing` )。 第二個參數是使用者定義的物件。 這個物件可以用來將應用程式專屬的狀態資訊傳遞至非同步作業完成時叫用的方法。 如果 `BeginOperationName` 方法使用其他作業特定參數 (例如用來儲存從檔案讀取位元組的位元組陣列)，<xref:System.AsyncCallback> 和應用程式狀態物件就會是 `BeginOperationName` 方法簽章中最後的參數。  
  
 `BeginOperationName` 會立即將控制權傳回呼叫的執行緒。 如果 `BeginOperationName` 方法擲回例外狀況，則例外狀況會在非同步作業啟動之前擲回。 如果 `BeginOperationName` 方法擲回例外狀況，則不會叫用回呼方法。  
  
## <a name="ending-an-asynchronous-operation"></a>結束非同步作業  
 `EndOperationName` 方法會結束非同步作業 *OperationName*。 `EndOperationName` 方法的傳回值型別與其同步版本所傳回的型別相同，而且是非同步作業專屬。 例如， <xref:System.IO.FileStream.EndRead%2A> 方法會傳回從 <xref:System.IO.FileStream> 讀取的位元組數目，而 <xref:System.Net.Dns.EndGetHostByName%2A> 方法會傳回包含主機電腦相關資訊的 <xref:System.Net.IPHostEntry> 物件。 `EndOperationName` 方法會使用在此方法同步版本簽章中所宣告的任何 out 或 ref 參數。 除了同步方法中的參數外，`EndOperationName` 方法還包括 <xref:System.IAsyncResult> 參數。 呼叫者必須傳遞 `BeginOperationName` 的對應呼叫所傳回的執行個體。  
  
 如果呼叫 `EndOperationName` 時，<xref:System.IAsyncResult> 物件所代表的非同步作業還沒有完成，`EndOperationName` 就會封鎖呼叫執行緒，直到非同步作業完成為止。 非同步作業所擲回的例外狀況都是從 `EndOperationName` 方法擲回。 使用相同的 `EndOperationName` 多次呼叫 <xref:System.IAsyncResult> 方法的效果尚未定義。 使用並非由相關 Begin 方法所傳回的 <xref:System.IAsyncResult> 呼叫 `EndOperationName` 方法的方式，也同樣尚未定義。  
  
> [!NOTE]
> 對任一未定義的情況，實施者應該考慮擲回 <xref:System.InvalidOperationException>。  
  
> [!NOTE]
> 這個設計模式的實施者應該告知呼叫端，非同步作業已透過將 <xref:System.IAsyncResult.IsCompleted%2A> 設定為 true、呼叫非同步回呼方法 (如果有指定) 和傳送訊號給 <xref:System.IAsyncResult.AsyncWaitHandle%2A>而完成。  
  
 應用程式開發人員有數項設計選擇，可存取非同步作業的結果。 正確的選擇取決於當作業完成時，應用程式是否有可以執行的指示。 如果應用程式一直到接收到非同步作業的結果，都無法執行任何額外的工作，它就必須封鎖直到取得結果為止。 若要封鎖到非同步作業完成，您可以使用下列方法的其中之一：  
  
- 從應用程式的主要執行緒呼叫 `EndOperationName`，並封鎖應用程式的執行，直到作業完成為止。 如需說明這項技巧的範例，請參閱[以結束非同步作業的方式封鎖應用程式執行](blocking-application-execution-by-ending-an-async-operation.md)。  
  
- 使用 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 應用程式執行，直到一或多個作業完成為止。 如需說明這項技巧的範例，請參閱 [Blocking Application Execution Using an AsyncWaitHandle](blocking-application-execution-using-an-asyncwaithandle.md)。  
  
 在非同步作業完成時不需要封鎖的應用程式，可以使用下列方法的其中之一：  
  
- 定期檢查 <xref:System.IAsyncResult.IsCompleted%2A> 屬性以輪詢作業完成狀態，並在作業完成時呼叫 `EndOperationName`。 如需說明這項技巧的範例，請參閱 [Polling for the Status of an Asynchronous Operation](polling-for-the-status-of-an-asynchronous-operation.md)。  
  
- 使用 <xref:System.AsyncCallback> 委派指定作業完成時要叫用的方法。 如需說明這項技巧的範例，請參閱 [Using an AsyncCallback Delegate to End an Asynchronous Operation](using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)。  
  
## <a name="see-also"></a>另請參閱

- [事件架構非同步模式 (EAP)](event-based-asynchronous-pattern-eap.md)
- [以非同步的方式呼叫同步方法](calling-synchronous-methods-asynchronously.md) \(部分機器翻譯\)
- [使用 AsyncCallback 委派和狀態物件](using-an-asynccallback-delegate-and-state-object.md)
