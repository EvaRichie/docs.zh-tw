---
title: '非同步檔案存取 (c # ) '
description: '瞭解如何在 c # 中使用 async 功能來存取檔案。 您可以呼叫非同步方法，而不需要使用回呼或跨方法分割程式碼。'
ms.date: 08/19/2020
ms.assetid: bb018fea-5313-4c80-ab3f-7c24b2145bd9
ms.openlocfilehash: 9a8db6004e8fff2cb39f0c350b403b56ea619e54
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88812038"
---
# <a name="asynchronous-file-access-c"></a>非同步檔案存取 (c # ) 

您可以使用非同步功能來存取檔案。 使用非同步功能，您就可以呼叫非同步方法，而不需要使用回呼或將您的程式碼分散到多種方法或 Lambda 運算式上。 若要讓同步程式碼變成非同步，只要呼叫非同步方法 (而不是同步方法)，然後將幾個關鍵字新增至程式碼即可。

您可能會基於下列原因將非同步功能新增至檔案存取呼叫：

> [!div class="checklist"]
>
> - 非同步功能可讓 UI 應用程式回應速度更快，因為啟動作業的 UI 執行緒可以執行其他工作。 如果 UI 執行緒必須執行相當耗時的程式碼 (例如超過 50 毫秒)，UI 可能會凍結到 I/O 完成，之後 UI 執行緒就可以再次處理鍵盤和滑鼠輸入以及其他事件。
> - 非同步功能藉由降低對執行緒的需求，來改善 ASP.NET 及其他伺服器架構應用程式的延展性。 如果應用程式針對每個回應使用專用執行緒，並同時處理一千個要求，則需要一千個執行緒。 非同步作業在等待期間，通常不需要使用執行緒。 它們可能會在結束時短暫使用現有的 I/O 完成執行緒。
> - 檔案存取作業的延遲在目前情況下可能很低，但未來可能會大幅增加。 例如，檔案可能會移至世界各地的伺服器。
> - 使用非同步功能所增加的額外負荷很小。
> - 您可以輕鬆地同時執行多個非同步工作。

## <a name="use-appropriate-classes"></a>使用適當的類別

本主題中的簡單範例會示範 <xref:System.IO.File.WriteAllTextAsync%2A?displayProperty=nameWithType> 和 <xref:System.IO.File.ReadAllTextAsync%2A?displayProperty=nameWithType> 。 若要對檔案 i/o 作業進行有限的控制，請使用 <xref:System.IO.FileStream> 類別，此類別的選項會導致作業系統層級發生非同步 i/o。 藉由使用這個選項，您可以避免在許多情況下封鎖執行緒集區執行緒。 若要啟用此選項，請在建構函式呼叫中指定 `useAsync=true` 或 `options=FileOptions.Asynchronous` 引數。

<xref:System.IO.StreamReader> <xref:System.IO.StreamWriter> 如果您透過指定檔案路徑來直接開啟此選項，就不能使用這個選項。 不過，如果您提供它們已開啟 <xref:System.IO.FileStream> 類別的 <xref:System.IO.Stream>，則可以使用此選項。 即使執行緒集區執行緒遭到封鎖，非同步呼叫的速度也會更快，因為 UI 執行緒在等候期間不會遭到封鎖。

## <a name="write-text"></a>寫入文字

下列範例會將文字寫入檔案。 在每個 await 陳述式中，此方法會立即結束。 當檔案 I/O 完成時，此方法會在 await 陳述式後面的陳述式繼續進行。 Async 修飾詞位於使用 await 語句的方法定義中。

### <a name="simple-example"></a>簡單範例

:::code language="csharp" source="snippets/file-access/Program.cs" id="SimpleWrite":::

### <a name="finite-control-example"></a>有限控制項範例

:::code language="csharp" source="snippets/file-access/Program.cs" id="WriteText":::

原始範例具有陳述式 `await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);`，這是下列兩個陳述式的縮減：

```csharp
Task theTask = sourceStream.WriteAsync(encodedText, 0, encodedText.Length);
await theTask;
```

第一個陳述式會傳回一個工作並開始處理檔案。 第二個陳述式具有 await，會立即結束方法並傳回其他工作。 稍後完成處理檔案之後，則會回到 await 後面的陳述式繼續執行。

## <a name="read-text"></a>讀取文字

下列範例會從檔案讀取文字。

### <a name="simple-example"></a>簡單範例

:::code language="csharp" source="snippets/file-access/Program.cs" id="SimpleRead":::

### <a name="finite-control-example"></a>有限控制項範例

此文字已經過緩衝處理，在本例中已置於 <xref:System.Text.StringBuilder>。 不同於上一個範例，await 的評估會產生一個值。 方法會傳回 <xref:System.IO.Stream.ReadAsync%2A> <xref:System.Threading.Tasks.Task> \<<xref:System.Int32>>，因此在作業完成之後，await 的評估會產生 `Int32` 值 `numRead` 。 如需詳細資訊，請參閱[非同步方法的傳回型別 (C#)](async-return-types.md)。

:::code language="csharp" source="snippets/file-access/Program.cs" id="ReadText":::

## <a name="parallel-asynchronous-io"></a>平行非同步 i/o

下列範例示範如何撰寫10個文字檔來進行平行處理。

### <a name="simple-example"></a>簡單範例

:::code language="csharp" source="snippets/file-access/Program.cs" id="SimpleParallelWrite":::

### <a name="finite-control-example"></a>有限控制項範例

針對每個檔案，<xref:System.IO.Stream.WriteAsync%2A> 方法會傳回一個工作，此工作之後會新增至工作清單。 `await Task.WhenAll(tasks);` 陳述式會在所有工作的檔案處理完成時結束方法，並在方法內繼續進行。

此範例會在工作完成之後，關閉 `finally` 區塊中的所有 <xref:System.IO.FileStream> 執行個體。 如果改為在 `using` 陳述式中建立每個 `FileStream`，`FileStream` 可能會在工作完成前就被處置。

任何效能提升幾乎都是從平行處理，而不是非同步處理。 非同步優點在於它不會佔用多個執行緒，也不會佔用使用者介面執行緒。

:::code language="csharp" source="snippets/file-access/Program.cs" id="ParallelWriteText":::

使用 <xref:System.IO.Stream.WriteAsync%2A> 和 <xref:System.IO.Stream.ReadAsync%2A> 方法時，您可以指定 <xref:System.Threading.CancellationToken>，這可用來在中途取消作業。 如需詳細資訊，請參閱 [managed 執行緒中的取消](../../../../standard/threading/cancellation-in-managed-threads.md)。

## <a name="see-also"></a>另請參閱

- [使用 async 和 await 進行非同步程式設計 (c # ) ](index.md)
- [非同步傳回類型 (c # ) ](async-return-types.md)
