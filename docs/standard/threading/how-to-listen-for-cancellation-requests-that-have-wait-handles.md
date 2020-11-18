---
title: 作法：接聽具有等候控制代碼的取消要求
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cancellation, waiting with wait handles
ms.assetid: 6e2aa49b-fc84-4bcf-962b-17db98b7edcb
ms.openlocfilehash: ec5bc796532381b3e21e4dddc037a927b7e68833
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826439"
---
# <a name="how-to-listen-for-cancellation-requests-that-have-wait-handles"></a>作法：接聽具有等候控制代碼的取消要求
如果方法正在等待要接收訊號的事件時遭到封鎖，則它無法檢查取消語彙基元的值並及時回應。 第一個範例示範如何在您使用 <xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> 之類的事件 (不以原生方式支援統一取消架構) 時，解決這個問題。 第二個範例示範使用 <xref:System.Threading.ManualResetEventSlim?displayProperty=nameWithType> 以支援統一取消的更簡化方法。  
  
> [!NOTE]
> 啟用 [Just My Code] 時，Visual Studio 在某些情況下會在擲回例外狀況的字行上中斷，並顯示錯誤訊息，指出「使用者程式碼未處理例外狀況」。 這個錯誤是良性的。 您可以按 F5 鍵繼續，並查看下面範例中示範的例外狀況處理行為。 若要防止 Visual Studio 在遇到第一個錯誤時就中斷，只要取消核取 [工具]、[選項]、[偵錯]、[一般] 下的 [Just My Code] 核取方塊即可。  
  
## <a name="example"></a>範例  
 下列範例使用 <xref:System.Threading.ManualResetEvent>，來示範如何解除封鎖不支援統一取消的等候控制代碼。  
  
 [!code-csharp[Cancellation#9](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex9.cs#9)]
 [!code-vb[Cancellation#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex9.vb#9)]  
  
## <a name="example"></a>範例  
 下列範例使用 <xref:System.Threading.ManualResetEventSlim>，來示範如何解除封鎖不支援統一取消的協調基本類型。 相同的方法可以與其他輕量型協調基本類型搭配使用，例如 <xref:System.Threading.Semaphore>`Slim` 和 <xref:System.Threading.CountdownEvent>。  
  
 [!code-csharp[Cancellation#10](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex10.cs#10)]
 [!code-vb[Cancellation#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex10.vb#10)]  
  
## <a name="see-also"></a>請參閱

- [Managed 執行緒中的取消](cancellation-in-managed-threads.md)
