---
title: 作法：取消連結資料流程區塊
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dataflow blocks, unlinking in TPL
- Task Parallel Library, dataflows
- TPL dataflow library, unlinking dataflow blocks
ms.assetid: 40f0208d-4618-47f7-85cf-4913d07d2d7d
ms.openlocfilehash: e981d1b9b3adc638a84de1c119ad849ec533d16e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95722359"
---
# <a name="how-to-unlink-dataflow-blocks"></a>作法：取消連結資料流程區塊

本文件將說明如何解除目標資料流程區塊與其來源之間的連結。

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="example"></a>範例  

 下列範例會建立三個 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 物件，每一個 `TrySolution` 方法都會計算一個值。 這個範例只要求來自第一次呼叫 `TrySolution` 的結果必須完成。  
  
 [!code-csharp[TPLDataflow_ReceiveAny#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_receiveany/cs/dataflowreceiveany.cs#1)]
 [!code-vb[TPLDataflow_ReceiveAny#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_receiveany/vb/dataflowreceiveany.vb#1)]  
  
 為了要從第一個完成的 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 接收值，這個範例會定義 `ReceiveFromAny(T)` 方法。 `ReceiveFromAny(T)` 方法可接受 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 物件陣列，並且將這些物件連結至 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 物件。 當您使用 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 方法將來源資料流程區塊連結至目標區塊時，來源會在有可用資料時將訊息傳播至目標。 由於 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 類別只接受提供給它的第一個訊息，因此 `ReceiveFromAny(T)` 方法會藉由呼叫 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A> 方法產生其結果。 這樣就會產生提供給 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 物件的第一個訊息。 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601.LinkTo%2A> 方法有一個會採用 <xref:System.Threading.Tasks.Dataflow.DataflowLinkOptions> 物件和 <xref:System.Threading.Tasks.Dataflow.DataflowLinkOptions.MaxMessages> 屬性的多載版本，當它設為 `1` 時，就會指示來源區塊在目標收到來自來源的第一個訊息之後，中斷與目標的連結。 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 物件一定要與其來源中斷連結，因為在 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 物件接收訊息之後，就不再需要來源陣列與 <xref:System.Threading.Tasks.Dataflow.WriteOnceBlock%601> 物件之間的關聯性。  
  
 若要在其中一個對 `TrySolution` 的呼叫計算出值之後讓其餘呼叫結束，`TrySolution` 方法會採用 <xref:System.Threading.CancellationToken> 物件，該物件會在 `ReceiveFromAny(T)` 的呼叫傳回之後取消。 <xref:System.Threading.SpinWait.SpinUntil%2A> 方法會在這個 <xref:System.Threading.CancellationToken> 物件取消時傳回。  
  
## <a name="see-also"></a>另請參閱

- [資料流程](dataflow-task-parallel-library.md)
