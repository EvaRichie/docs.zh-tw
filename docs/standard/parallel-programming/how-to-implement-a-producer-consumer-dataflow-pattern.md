---
title: 如何：執行生產者-取用者資料流程模式
description: 瞭解如何在 .NET 中使用 TPL 資料流程程式庫來執行生產者-取用者資料流程模式。
ms.date: 09/24/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TPL dataflow library, implementing producer-consumer pattern
- Task Parallel Library, dataflows
- producer-consumer patterns, implementing [TPL]
ms.assetid: 47a1d38c-fe9c-44aa-bd15-937bd5659b0b
ms.openlocfilehash: fc68d9e678dab88ec5008b6c15ef17a5d20f25ae
ms.sourcegitcommit: d04388f94dbcd756ffd608536c869aee3242cdb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91206376"
---
# <a name="how-to-implement-a-producer-consumer-dataflow-pattern"></a>如何：執行生產者-取用者資料流程模式

在本文中，您將瞭解如何使用 TPL 資料流程程式庫來執行生產者-取用者模式。 在此模式中，「生產者」** 會將訊息傳送至訊息區塊，而「消費者」** 會從該區塊讀取訊息。

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="example"></a>範例

下列範例將示範使用資料流程的基本生產者-消費者模型。 `Produce` 方法會將包含隨機位元組資料的陣列寫入 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601?displayProperty=nameWithType> 物件中，而 `Consume` 方法會從 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601?displayProperty=nameWithType> 物件中讀取位元組。 藉由處理 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 和 <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> 介面而不是其衍生類型，您就可以撰寫可重複使用的程式碼來處理各種資料流程區塊類型。 這個範例會使用 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 類別。 由於 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> 類別會同時做為來源區塊和目標區塊，因此生產者和消費者可以使用共用物件來傳輸資料。

 `Produce` 方法會在迴圈中呼叫 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> 方法，將資料同步寫入目標區塊中。 `Produce` 方法將所有資料寫入目標區塊之後會呼叫 <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A> 方法，指出區塊將不會再提供任何額外的資料。 `Consume` 方法會使用 [async](../../csharp/language-reference/keywords/async.md) 和 [await](../../csharp/language-reference/operators/await.md) 運算子 (在 Visual Basic 中為 [Async](../../visual-basic/language-reference/modifiers/async.md) 和 [Await](../../visual-basic/language-reference/operators/await-operator.md)) 以非同步方式計算從 <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> 物件接收的位元組總數。 若要以非同步方式執行，`Consume` 方法會呼叫 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> 方法在來源區塊有可用資料，以及來源區塊永遠不再提供其他可用資料時收到通知。

 [!code-csharp[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#1)]
 [!code-vb[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#1)]

## <a name="robust-programming"></a>穩固程式設計

 前面的範例會使用單一消費者處理來源資料。 如果您的應用程式中有多個消費者，請使用 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 方法從來源區塊讀取資料，如下列範例所示。

 [!code-csharp[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#2)]
 [!code-vb[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#2)]

 沒有可用資料時，<xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> 方法會回傳 `False`。 如果多個消費者必須同時存取來源區塊，這個機制就能確保在呼叫 <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> 之後資料仍然可用。

## <a name="see-also"></a>另請參閱

- [資料流程](dataflow-task-parallel-library.md)
