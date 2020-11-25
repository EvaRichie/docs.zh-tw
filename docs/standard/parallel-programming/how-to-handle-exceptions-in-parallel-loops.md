---
title: 作法：處理平行迴圈中的例外狀況
description: 瞭解如何在 .NET 中處理平行迴圈中的例外狀況。 請參閱如何從 AggregateException 中的迴圈包裝所有例外狀況的範例。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to handle exceptions
ms.assetid: 512f0d5a-4636-4875-b766-88f20044f143
ms.openlocfilehash: 903db7f7318a9067c31af090490bab6dd70fa0ad
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/24/2020
ms.locfileid: "95734474"
---
# <a name="how-to-handle-exceptions-in-parallel-loops"></a>作法：處理平行迴圈中的例外狀況

<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> 多載沒有任何特殊機制可用來處理可能擲回的例外狀況。 在這種情況下，它們類似于一般 `for` 和 `foreach` 迴圈 (`For` 和 `For Each` Visual Basic) ; 未處理的例外狀況會導致迴圈在所有目前執行中的反復專案完成時立即終止。
  
 當您將自己的例外狀況處理邏輯加入平行迴圈時，請處理多個執行緒上可能同時擲回類似例外狀況的情況，以及某個執行緒上擲回的例外狀況導致在另一個執行緒上擲回另一個例外狀況的情況。 您可以來自此迴圈的所有例外狀況包裝在 <xref:System.AggregateException?displayProperty=nameWithType> 中，同時處理這兩種情況。 下列範例會示範一種可能的方式。  
  
> [!NOTE]
> 啟用 [Just My Code] 時，Visual Studio 在某些情況下會在擲回例外狀況的字行上中斷，並顯示錯誤訊息，指出「使用者程式碼未處理例外狀況」。 這個錯誤是良性的。 您可以按 F5 從中斷的地方繼續，並查看下面範例中示範的例外處理行為。 若要防止 Visual Studio 在遇到第一個錯誤時就中斷，只要取消核取 [工具]、[選項]、[偵錯]、[一般] 下的 [Just My Code] 核取方塊即可。  
  
## <a name="example"></a>範例  

 在此範例中，會攔截所有例外狀況，然後包裝於擲回的 <xref:System.AggregateException?displayProperty=nameWithType> 之中。 呼叫端可決定要處理哪一個例外狀況。  
  
 [!code-csharp[TPL_Exceptions#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_exceptions/cs/exceptions.cs#08)]
 [!code-vb[TPL_Exceptions#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_exceptions/vb/exceptionsinloops.vb#08)]  
  
## <a name="see-also"></a>另請參閱

- [資料平行處理](data-parallelism-task-parallel-library.md)
- [PLINQ 和 TPL 中的 Lambda 運算式](lambda-expressions-in-plinq-and-tpl.md)
