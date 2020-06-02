---
title: 作法：取消 PLINQ 查詢
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- PLINQ queries, how to cancel
- cancellation, PLINQ
ms.assetid: 80b14640-edfa-4153-be1b-3e003d3e9c1a
ms.openlocfilehash: 09405a8a9f5d96d80454bcc98cbf29db54df6725
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288208"
---
# <a name="how-to-cancel-a-plinq-query"></a>作法：取消 PLINQ 查詢
下列範例說明取消 PLINQ 查詢的兩種方式。 第一個範例示範如何取消大部分由資料周遊所組成的查詢。 第二個範例示範如何取消包含需要大量計算之使用者函式的查詢。

> [!NOTE]
> 啟用 [Just My Code] 時，Visual Studio 會在擲回例外狀況的字行上中斷，並顯示錯誤訊息，指出「使用者程式碼未處理例外狀況」。 這個錯誤是良性的。 您可以按 F5 鍵繼續，並查看下面範例中示範的例外狀況處理行為。 若要防止 Visual Studio 在遇到第一個錯誤時就中斷，只要取消核取 [工具]、[選項]、[偵錯]、[一般]**** 下的 [Just My Code] 核取方塊即可。
>
> 這個範例是為了示範用法，執行速度可能比不上對應的循序 LINQ to Objects 查詢。 如需加速的詳細資訊，請參閱[認識 PLINQ 中的加速](understanding-speedup-in-plinq.md)。

## <a name="example"></a>範例

[!code-csharp[PLINQ#16](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#16)]
[!code-vb[PLINQ#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#16)]

PLINQ 架構不會將單一 <xref:System.OperationCanceledException> 累計到 <xref:System.AggregateException?displayProperty=nameWithType>；<xref:System.OperationCanceledException> 必須在個別的 catch 區塊中處理。 如果一或多個使用者委派擲回 OperationCanceledException(externalCT) (使用外部 <xref:System.Threading.CancellationToken?displayProperty=nameWithType>)，但沒有其他例外狀況，而查詢定義為 `AsParallel().WithCancellation(externalCT)`，PLINQ 將會發出單一 <xref:System.OperationCanceledException> (externalCT) 而不是 <xref:System.AggregateException?displayProperty=nameWithType>。 不過，如果一位使用者委派擲回 <xref:System.OperationCanceledException>，另一個委派擲回其他例外狀況類型，則這兩個例外狀況將會累計到 <xref:System.AggregateException>。

取消作業的一般指引如下：

1. 如果您執行使用者委派取消，您應該通知 PLINQ 有關外部的， <xref:System.Threading.CancellationToken> 並擲回 <xref:System.OperationCanceledException> （externalCT）。

2. 如果發生取消，而且沒有擲回其他例外狀況，則會處理， <xref:System.OperationCanceledException> 而非 <xref:System.AggregateException> 。

## <a name="example"></a>範例

下列範例示範當使用者程式碼中含有計算成本很高之函數時，應如何處理取消作業。

[!code-csharp[PLINQ#17](../../../samples/snippets/csharp/VS_Snippets_Misc/plinq/cs/plinqsamples.cs#17)]
[!code-vb[PLINQ#17](../../../samples/snippets/visualbasic/VS_Snippets_Misc/plinq/vb/plinqsnippets1.vb#17)]

處理使用者程式碼中的取消作業時，不需在查詢定義中使用 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A>。 不過，我們建議您務必使用 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> ，因為 <xref:System.Linq.ParallelEnumerable.WithCancellation%2A> 不會影響查詢效能，而且可讓查詢運算子和您的使用者程式碼來處理取消作業。

為確保系統回應能力，建議您每毫秒檢查一次是否有取消作業；不過，系統可以接受最多 10 毫秒的任何週期。 此頻率對您的程式碼效能應該沒有負面影響。

在處置枚舉器時（例如，當程式碼在反復查看查詢結果的 foreach （針對 Visual Basic 中的每個）迴圈中中斷時，會取消查詢，但不會擲回任何例外狀況。

## <a name="see-also"></a>另請參閱

- <xref:System.Linq.ParallelEnumerable>
- [平行 LINQ (PLINQ)](introduction-to-plinq.md)
- [Managed 執行緒中的取消作業](../threading/cancellation-in-managed-threads.md)
