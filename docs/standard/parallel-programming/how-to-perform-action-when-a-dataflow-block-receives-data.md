---
title: 作法：在資料流程區塊收到資料時執行動作
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- TPL dataflow library, receiving data
ms.assetid: fc2585dc-965e-4632-ace7-73dd02684ed3
ms.openlocfilehash: 3a709e40908afcbd1a228aab00fe36be43097826
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94825724"
---
# <a name="how-to-perform-action-when-a-dataflow-block-receives-data"></a>作法：在資料流程區塊收到資料時執行動作
「執行資料流程區塊」(Execution Dataflow Block) 類型會在收到資料時呼叫使用者提供的委派。 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601?displayProperty=nameWithType>、<xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=nameWithType> 和 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=nameWithType> 類別都是執行資料流程區塊類型。 當您將工作函式提供給執行資料流程區塊時，可以使用 `delegate` 關鍵字 (在 Visual Basic 中為 `Sub`)、<xref:System.Action%601>、<xref:System.Func%602> 或 Lambda 運算式。 本文件將說明如何使用 <xref:System.Func%602> 和 Lambda 運算式在執行區塊中執行動作。  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="example"></a>範例  
 下列範例會使用資料流程從磁碟讀取檔案，並計算該檔案中等於零的位元組數。 它會使用 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 讀取檔案並計算零位元組的數目，並且使用 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 將零位元組的數目列印至主控台。 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 物件會指定 <xref:System.Func%602> 物件在區塊收到資料時執行工作。 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 物件會使用 Lambda 運算式將讀取的零位元組數目列印至主控台。  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#1)]
 [!code-vb[TPLDataflow_ExecutionBlocks#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#1)]  
  
 雖然您可以提供 Lambda 運算式給 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 物件，但是這個範例會使用 <xref:System.Func%602> 讓其他程式碼能夠使用 `CountBytes` 方法。 由於要執行的工作是這個工作所專屬，而且對於其他程式碼可能不太實用，因此 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 物件會使用 Lambda 運算式。 如需 Lambda 運算式如何在工作平行程式庫中運作的詳細資訊，請參閱 [PLINQ 和 TPL 中的 Lambda 運算式](lambda-expressions-in-plinq-and-tpl.md)。  
  
 [資料流程](dataflow-task-parallel-library.md)檔中的委派類型的區段摘要，會摘要說明您可以提供給 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 、 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 和物件的委派類型 <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602> 。 表中也會指出委派類型是以同步或非同步方式運作。  
  
## <a name="robust-programming"></a>穩固程式設計  
 這個範例會將 <xref:System.Func%602> 類型的委派提供給 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 物件，以同步方式執行資料流程區塊的工作。 若要讓資料流程區塊以非同步方式執行，請將 <xref:System.Func%601> 類型的委派提供給資料流程區塊。 當資料流程區塊以非同步方式執行時，資料流程區塊的工作會在傳回的 <xref:System.Threading.Tasks.Task%601> 物件完成後才完成。 下列範例會修改 `CountBytes` 方法並使用 [async](../../csharp/language-reference/keywords/async.md) 和 [await](../../csharp/language-reference/operators/await.md) 運算子 (在 Visual Basic 中為 [Async](../../visual-basic/language-reference/modifiers/async.md) 和 [Await](../../visual-basic/language-reference/operators/await-operator.md))，以非同步方式計算所提供檔案中零位元組的總數。 <xref:System.IO.FileStream.ReadAsync%2A> 方法會以非同步方式執行讀取作業。  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#2)]
 [!code-vb[TPLDataflow_ExecutionBlocks#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#2)]  
  
 您也可以使用非同步 Lambda 運算式在執行資料流程區塊中執行動作。 下列範例會修改前一個範例中使用的 <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> 物件，讓它使用 Lambda 運算式以非同步方式執行工作。  
  
 [!code-csharp[TPLDataflow_ExecutionBlocks#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_executionblocks/cs/dataflowexecutionblocks.cs#3)]
 [!code-vb[TPLDataflow_ExecutionBlocks#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_executionblocks/vb/dataflowexecutionblocks.vb#3)]  
  
## <a name="see-also"></a>請參閱

- [資料流程](dataflow-task-parallel-library.md)
