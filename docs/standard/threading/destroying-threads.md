---
title: 終結執行緒
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- destroying threads
- threading [.NET Framework], destroying threads
ms.assetid: df54e648-c5d1-47c9-bd29-8e4438c1db6d
ms.openlocfilehash: 9f69773ec19008ebafd28a68e4e2007b6f9bb979
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84279811"
---
# <a name="destroying-threads"></a>終結執行緒

若要終止執行緒的執行，您通常會使用[合作式取消模型](cancellation-in-managed-threads.md)。 有時候，無法以合作方式停止執行緒，因為它會執行協力廠商程式碼，而不是針對合作取消所設計。 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>.NET Framework 中的方法可以用來強制終止 managed 執行緒。 當您呼叫時 <xref:System.Threading.Thread.Abort%2A> ，Common Language Runtime 會在目標執行緒中擲回，目標執行緒 <xref:System.Threading.ThreadAbortException> 可以攔截。 如需詳細資訊，請參閱<xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>。 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>.Net Core 不支援方法。 如果您需要終止在 .NET Core 中強制執行協力廠商程式碼，請在個別進程中執行它，然後使用 <xref:System.Diagnostics.Process.Kill%2A?displayProperty=nameWithType> 。

> [!NOTE]
> 如果執行緒在其 <xref:System.Threading.Thread.Abort%2A> 方法被呼叫時正在執行非受控碼，執行階段就會將它標示為 <xref:System.Threading.ThreadState.AbortRequested?displayProperty=nameWithType>。 當執行緒返回受控碼時，會擲回例外狀況。  
  
 一旦中止執行緒之後，就無法重新啟動。  
  
 <xref:System.Threading.Thread.Abort%2A> 方法不會造成執行緒立即中止，因為目標執行緒可以攔截 <xref:System.Threading.ThreadAbortException> 並執行 `finally` 區塊中任意數量的程式碼。 如果您需要等候，直到執行緒結束，則可呼叫 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>。 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> 是一個封鎖呼叫，在執行緒實際停止執行或已經過選擇性的逾時間隔之後才會返回。 中止的執行緒可以呼叫 <xref:System.Threading.Thread.ResetAbort%2A> 方法，或在 `finally` 區塊中執行未繫結的處理，因此，如果您未指定逾時，則不保證會等候結束。  
  
 正在對 <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> 方法的呼叫中等候的執行緒可由呼叫 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 的其他執行緒來中斷。  
  
## <a name="handling-threadabortexception"></a>處理 ThreadAbortException  
 如果您預期執行緒會中止，無論是從您自己的程式碼呼叫 <xref:System.Threading.Thread.Abort%2A>，還是卸載執行緒執行所在的應用程式定義域 (<xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> 使用 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 來終止執行緒)，您的執行緒都必須處理 <xref:System.Threading.ThreadAbortException> 並執行 `finally` 子句中的任何最終處理，如下列程式碼所示。  
  
```vb  
Try  
    ' Code that is executing when the thread is aborted.  
Catch ex As ThreadAbortException  
    ' Clean-up code can go here.  
    ' If there is no Finally clause, ThreadAbortException is  
    ' re-thrown by the system at the end of the Catch clause.
Finally  
    ' Clean-up code can go here.  
End Try  
' Do not put clean-up code here, because the exception
' is rethrown at the end of the Finally clause.  
```  
  
```csharp  
try
{  
    // Code that is executing when the thread is aborted.  
}
catch (ThreadAbortException ex)
{  
    // Clean-up code can go here.  
    // If there is no Finally clause, ThreadAbortException is  
    // re-thrown by the system at the end of the Catch clause.
}  
// Do not put clean-up code here, because the exception
// is rethrown at the end of the Finally clause.  
```  
  
 清除程式碼必須位於 `catch` 子句或 `finally` 子句，因為系統必須在 `finally` 子句結尾處重新擲回 <xref:System.Threading.ThreadAbortException>，如果沒有 `finally` 子句，則會在 `catch` 子句結尾處重新擲回。  
  
 您可以呼叫 <xref:System.Threading.Thread.ResetAbort%2A?displayProperty=nameWithType> 方法來防止系統重新擲回例外狀況。 但是，只有當您自己的程式碼會造成 <xref:System.Threading.ThreadAbortException>，才應採取此作法。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Threading.ThreadAbortException>
- <xref:System.Threading.Thread>
- [使用執行緒和執行緒處理](using-threads-and-threading.md)
