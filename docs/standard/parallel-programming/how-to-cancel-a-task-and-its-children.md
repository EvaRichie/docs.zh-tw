---
title: 作法：取消工作及其子系
description: 請參閱如何在 .NET 中取消工作及其子系的範例。 這些範例涵蓋從可取消的工作建立的步驟，到工作已取消的通知。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to cancel
ms.assetid: 08574301-8331-4719-ad50-9cf7f6ff3048
ms.openlocfilehash: 66daf00680b65aace1ce6367761e3ed81596d33b
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662676"
---
# <a name="how-to-cancel-a-task-and-its-children"></a>作法：取消工作及其子系
這些範例示範如何執行下列工作：  
  
1. 建立和啟動可取消的工作。  
  
2. 將取消權杖傳送至您的使用者委派或工作執行個體 (選擇性)。  
  
3. 注意並回應使用者委派中的取消要求。  
  
4. 注意已取消工作的呼叫端執行緒 (選擇性)。  
  
 呼叫端執行緒不會強制結束工作；它只會通知已要求取消。 如果工作已在執行，則是由使用者委派來通知要求並適當回應。 如果在工作執行前要求取消，則永遠不會執行使用者委派，且工作物件會轉換成 Canceled 狀態。  
  
## <a name="example"></a>範例  
 此範例示範如何終止 <xref:System.Threading.Tasks.Task> 及其子系，以回應取消要求。 這個範例也會說明在使用者委派藉由擲回 <xref:System.Threading.Tasks.TaskCanceledException> 結束時，呼叫端執行緒可以選擇性地使用 <xref:System.Threading.Tasks.Task.Wait%2A> 方法或 <xref:System.Threading.Tasks.Task.WaitAll%2A> 方法等候工作完成。 在這種情況下，您必須使用 `try/catch` 區塊來處理呼叫端執行緒上的例外狀況。  
  
 [!code-csharp[TPL_Cancellation#04](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cancellation/cs/cancel1.cs#04)]
 [!code-vb[TPL_Cancellation#04](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cancellation/vb/cancel1.vb#04)]  
  
 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 類別已和基礎是 <xref:System.Threading.CancellationTokenSource?displayProperty=nameWithType> 及 <xref:System.Threading.CancellationToken?displayProperty=nameWithType> 型別的取消模型完全整合。 如需詳細資訊，請參閱[受控執行緒中的取消作業](../threading/cancellation-in-managed-threads.md)和[工作取消](task-cancellation.md)。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Threading.CancellationTokenSource?displayProperty=nameWithType>
- <xref:System.Threading.CancellationToken?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>
- [以工作為基礎的非同步程式設計](task-based-asynchronous-programming.md)
- [附加與中斷連結的子工作](attached-and-detached-child-tasks.md)
- [PLINQ 和 TPL 中的 Lambda 運算式](lambda-expressions-in-plinq-and-tpl.md)
