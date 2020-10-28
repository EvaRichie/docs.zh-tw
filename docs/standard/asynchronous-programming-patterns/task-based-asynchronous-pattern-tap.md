---
title: 以工作為基礎的非同步模式 (TAP)
description: 瞭解以工作為基礎的非同步模式 (點擊) 。 點一下是在 .NET 中進行開發時建議使用的非同步設計模式。
ms.date: 02/26/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- asynchronous design patterns, .NET
- TAP, .NET support for
- Task-based Asynchronous Pattern, .NET support for
- .NET, asynchronous design patterns
ms.assetid: 8cef1fcf-6f9f-417c-b21f-3fd8bac75007
ms.openlocfilehash: 2987e7baa52f627d1da41af21d05bfa22a247fbb
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/28/2020
ms.locfileid: "92889240"
---
# <a name="task-based-asynchronous-pattern"></a>以工作為基礎的非同步模式

以工作為基礎的非同步模式 (點) 是以 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> 命名空間中的和類型為基礎，而這些類型 <xref:System.Threading.Tasks?displayProperty=nameWithType> 是用來代表任意非同步作業。 TAP 是進行新的開發工作時，建議使用的非同步設計模式。  
  
## <a name="naming-parameters-and-return-types"></a>命名、參數和傳回型別

TAP 使用單一方法表示非同步作業的啟始和完成。 這與非同步程式設計模型 (APM 或 `IAsyncResult`) 模式和事件架構非同步模式 (EAP) 形成對比。 APM 要求 `Begin` 和 `End` 方法。 EAP 需要一個具有 `Async` 尾碼的方法，也需要一或多個事件、事件處理常式委派類型，以及 `EventArg` 衍生型別。 TAP 中的非同步方法會在傳回可等候型別之方法的作業名稱後面包括 `Async` 尾碼，例如 <xref:System.Threading.Tasks.Task>、<xref:System.Threading.Tasks.Task%601>、<xref:System.Threading.Tasks.ValueTask> 和 <xref:System.Threading.Tasks.ValueTask%601>。 例如，`GetAsync` 表示傳回 `Task<String>` 的非同步 `Get` 作業。 如果您將 TAP 方法加入至已包含具有 `Async` 尾碼之 EAP 方法名稱的類別，請改用 `TaskAsync` 尾碼。 例如，如果類別已經有 `GetAsync` 方法，請使用 `GetTaskAsync` 這個名稱。 如果方法啟動非同步作業但不傳回可等候型別，則其名稱應以 `Begin`、`Start` 或其他動詞開頭，以表明此方法不傳回或擲回作業的結果。  
  
 TAP 方法會傳回 <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> 或 <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType>，取決於對應的同步方法傳回 void 或 `TResult` 類型。  
  
 TAP 方法的參數應該與其同步對應項目的參數相符，並且應該以相同順序提供。  不過，`out` 和 `ref` 參數不受限於這項規則，因此應完全避免使用。 所有可能會透過 `out` 或 `ref` 參數傳回的資料，都應該改成做為 `TResult` 所傳回 <xref:System.Threading.Tasks.Task%601> 的一部分傳回，而且應使用 Tuple 或自訂資料結構來容納多個值。 此外，也請考慮加入 <xref:System.Threading.CancellationToken> 參數，即使點一下方法的同步對應專案不提供。

 專門用於建立、管理或組合工作的方法 (其中方法的非同步用意以方法名稱或方法所屬的類型名稱清楚表示) 不需要遵循這個命名模式，這類方法通常稱為「組合器」  。 組合器的範例包括 <xref:System.Threading.Tasks.Task.WhenAll%2A> 和 <xref:System.Threading.Tasks.Task.WhenAny%2A>，並且將在[使用以工作為基礎的非同步模式](consuming-the-task-based-asynchronous-pattern.md)文件的[使用內建工作式組合器](consuming-the-task-based-asynchronous-pattern.md#combinators)一節中加以討論。  
  
 如需說明 TAP 語法與舊有非同步程式設計模式 (例如非同步程式設計模型 (APM) 和事件式非同步模式 (EAP)) 的語法之間差異的範例，請參閱[非同步程式設計模式](index.md)。  
  
## <a name="initiating-an-asynchronous-operation"></a>啟始非同步作業  
 以 TAP 為基礎的非同步方法可以先同步處理少量供作，例如驗證引數和啟始非同步作業，再傳回產生的工作。 同步工作量應盡量維持最少，這樣非同步方法才可以快速傳回。 快速退回的原因包括：  
  
- 非同步方法可能是從使用者介面 (UI) 執行緒叫用，而任何長時間執行的同步工作都可能影響應用程式的回應。  
  
- 可能有多個非同步方法同時啟動。 因此，在非同步方法的同步處理部分中，所有長時間執行的工作都可能延遲啟始其他非同步作業，因而降低並行的優勢。  
  
 在某些情況下，完成作業所需的工作量會比以非同步方式啟動作業所需的工作量還少。 若資料流中的讀取作業可以藉由已在記憶體中緩衝的資料獲得滿足，則從該資料流進行讀取就是這類情境的範例。 在這類情況下，作業會同步完成，而且可能會傳回已完成的工作。  
  
## <a name="exceptions"></a>例外狀況  
 非同步方法應只有在回應使用方式錯誤時，才引發從非同步方法呼叫擲回例外狀況。 使用方式錯誤一律不應發生在實際執行程式碼中。 例如，如果 `Nothing` 在 Visual Basic) 中傳遞 null 參考 (，因為其中一個方法的引數會導致 (通常以例外狀況) 表示的錯誤狀態 <xref:System.ArgumentNullException> ，所以您可以修改呼叫程式碼，以確保永遠不會傳遞 null 參考。 對於所有其他錯誤，非同步方法執行時發生的例外狀況應該指派給傳回的工作，即使非同步方法剛好在工作傳回前同步完成也一樣。 通常，工作最多只能包含一個例外狀況。 不過，如果工作表示多項作業 (例如 <xref:System.Threading.Tasks.Task.WhenAll%2A>)，則可能會有多個例外狀況與單一工作相關聯。  
  
## <a name="target-environment"></a>目標環境  
 當您實作 TAP 方法時，可以判斷非同步執行發生的位置。 您可以選擇線上程集區上執行工作負載、使用非同步 (i/o 來執行工作負載，而不需系結至大部分作業執行) 的執行緒、在特定 (執行緒上執行（例如 UI 執行緒) ），或使用任意數量的可能內容。 TAP 方法甚至可能沒有可執行的項目，而且可能只傳回 <xref:System.Threading.Tasks.Task>，指出系統中其他位置發生的情形 (例如，代表資料的工作抵達佇列的資料結構)。

 TAP 方法的呼叫端可能會透過同步等待產生的工作來阻止等待 TAP 方法完成，或是在非同步作業完成時執行其他 (接續) 程式碼。 接續程式碼 (Continuation Code) 的建立者可以控制執行程式碼的位置。 您可以明確建立接續程式碼、透過 <xref:System.Threading.Tasks.Task> 類別的方法建立 (例如 <xref:System.Threading.Tasks.Task.ContinueWith%2A>)，或使用建置於接續之上的語言支援以隱含方式建立 (例如 C# 中的 `await`、Visual Basic 中的 `Await`，或 F# 中的 `AwaitValue`)。  
  
## <a name="task-status"></a>工作狀態  
 <xref:System.Threading.Tasks.Task> 類別會提供非同步作業的生命週期，而該週期是以 <xref:System.Threading.Tasks.TaskStatus> 列舉表示。 為了支援從 <xref:System.Threading.Tasks.Task> 和 <xref:System.Threading.Tasks.Task%601> 衍生的類型隱密案例，以及支援分隔建構與排程，<xref:System.Threading.Tasks.Task> 類別會公開 <xref:System.Threading.Tasks.Task.Start%2A> 方法。 由公用 <xref:System.Threading.Tasks.Task> 建構函式所建立的工作稱為「靜止工作」(Cold Task)  ，因為這類工作的生命週期是從非排程的 <xref:System.Threading.Tasks.TaskStatus.Created> 狀態開始，而且只有在這些執行個體上呼叫 <xref:System.Threading.Tasks.Task.Start%2A> 時才會排程。

 所有其他工作都是從作用狀態開始其生命週期，也就是說，它們所代表的非同步作業已啟始，而且其工作狀態是 <xref:System.Threading.Tasks.TaskStatus.Created?displayProperty=nameWithType> 以外的列舉值。 從 TAP 方法傳回的所有工作都必須為啟用狀態。 **如果分流方法在內部使用工作的函式，將要傳回的工作具現化，則在傳回 <xref:System.Threading.Tasks.Task.Start%2A> 物件之前，請先在物件上呼叫該方法 <xref:System.Threading.Tasks.Task> 。** TAP 方法的消費者可以安全地假設傳回的工作為作用中，並且不應嘗試在任何從 TAP 方法傳回的 <xref:System.Threading.Tasks.Task.Start%2A> 上呼叫 <xref:System.Threading.Tasks.Task>。 在作用中工作上呼叫 <xref:System.Threading.Tasks.Task.Start%2A> 會導致 <xref:System.InvalidOperationException> 例外狀況。  
  
## <a name="cancellation-optional"></a>取消 (選擇性)  
 在 TAP 中，取消對於非同步方法實作者和非同步方法消費者而言都是選擇性的。 如果作業允許取消，則會公開可接受取消語彙基元 (<xref:System.Threading.CancellationToken> 執行個體) 的非同步方法多載。 依照慣例，參數會命名為 `cancellationToken`。  
  
 [!code-csharp[Conceptual.TAP#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#1)]
 [!code-vb[Conceptual.TAP#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#1)]  
  
 非同步作業會監視取消要求的這個語彙基元。 如果收到取消要求，它可以選擇接受該要求和取消作業。 如果取消要求導致工作尚未完成就結束，則 TAP 方法會傳回以 <xref:System.Threading.Tasks.TaskStatus.Canceled> 狀態結束的工作，而且沒有可用的結果，也不會擲回例外狀況。  <xref:System.Threading.Tasks.TaskStatus.Canceled> 狀態會視為工作的最後 (已完成) 狀態，並且包括 <xref:System.Threading.Tasks.TaskStatus.Faulted> 和 <xref:System.Threading.Tasks.TaskStatus.RanToCompletion> 狀態。 因此，如果工作處於 <xref:System.Threading.Tasks.TaskStatus.Canceled> 狀態，其 <xref:System.Threading.Tasks.Task.IsCompleted%2A> 屬性就會傳回 `true`。 當工作以 <xref:System.Threading.Tasks.TaskStatus.Canceled> 狀態完成時，工作中註冊的任何接續都會排程或執行，除非指定了像是 <xref:System.Threading.Tasks.TaskContinuationOptions.NotOnCanceled> 這類選項來選擇不接續。 任何藉由使用語言功能以非同步方式等候已取消之工作的程式碼都會繼續執行，但是會收到 <xref:System.OperationCanceledException> 或從其衍生的例外狀況。 透過 <xref:System.Threading.Tasks.Task.Wait%2A> 和 <xref:System.Threading.Tasks.Task.WaitAll%2A> 這類方法封鎖同步等候工作的程式碼也會繼續執行，但會產生例外狀況。  
  
 如果取消語彙基元在呼叫接受語彙基元的 TAP 方法之前就已要求取消，則 TAP 方法應傳回 <xref:System.Threading.Tasks.TaskStatus.Canceled> 工作。  不過，如果是在非同步作業執行時要求取消，則非同步作業不需要接受取消要求。  只有在作業因取消要求而結束時，傳回的工作才應該以 <xref:System.Threading.Tasks.TaskStatus.Canceled> 狀態結束。 如果已要求取消，但是仍然產生結果或例外狀況，則工作應以 <xref:System.Threading.Tasks.TaskStatus.RanToCompletion> 或 <xref:System.Threading.Tasks.TaskStatus.Faulted> 狀態結束。

 若是想要公開取消的非同步方法，您不需要提供不接受解除標記的多載。 對於無法取消的方法，請不要提供接受取消語彙基元的多載，這樣有助於向呼叫端表明目標方法實際上是否可以取消。  不需要取消的消費者程式碼可以呼叫接受 <xref:System.Threading.CancellationToken> 的方法，並且提供 <xref:System.Threading.CancellationToken.None%2A> 做為引數值。 <xref:System.Threading.CancellationToken.None%2A> 在功能上相當於預設的 <xref:System.Threading.CancellationToken>。  
  
## <a name="progress-reporting-optional"></a>進度報告 (選擇性)  
 某些非同步作業會因為提供進度通知而受益，這些通知通常用來更新使用者介面並提供有關非同步作業進度的資訊。

 在 TAP 中，進度是透過 <xref:System.IProgress%601> 介面處理，並且做為通常名為 `progress` 的參數傳遞至非同步方法。  在呼叫非同步方法時提供進度介面，有助於排除不當使用所造成的競爭情形 (也就是說，事件處理常式在作業啟動後才註冊是不正確的，而這樣可能導致遺失更新)。  更重要的是，進度介面支援各種不同的進度實作，取決於使用的程式碼。  例如，使用的程式碼可能只在意最新的進度更新，或是想要緩衝所有更新，也可能想要對每一個更新叫用一個動作，或是想要控制是否要將引動過程封送處理置特定執行緒。 您可以使用不同的介面執行方式來達成這些選項，並根據特定取用者的需求加以自訂。  就像處理取消一樣，TAP 實作應只在 API 支援進度通知時才提供 <xref:System.IProgress%601> 參數。

 例如，如果本文前面所討論的 `ReadAsync` 方法能夠以目前為止讀取之位元組數目的形式報告中繼進度，則進度回呼就可以是 <xref:System.IProgress%601> 介面：  
  
 [!code-csharp[Conceptual.TAP#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#2)]
 [!code-vb[Conceptual.TAP#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#2)]  
  
 如果 `FindFilesAsync` 方法傳回所有符合特定搜尋模式的檔案清單，則進度回呼可提供已完成的工作百分比和目前部分結果集的估計。 它可以使用元組來提供這項資訊：  
  
 [!code-csharp[Conceptual.TAP#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#3)]
 [!code-vb[Conceptual.TAP#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#3)]  
  
 或使用 API 專屬的資料類型：  
  
 [!code-csharp[Conceptual.TAP#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#4)]
 [!code-vb[Conceptual.TAP#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#4)]  
  
 在後者的情況下，特殊資料類型通常會加上 `ProgressInfo` 尾碼。  
  
 如果分路處理提供接受參數的多載 `progress` ，則必須允許引數為 `null` ，在此情況下不會報告任何進度。 點擊 [執行] 應該會以同步方式報告物件的進度，如此可 <xref:System.Progress%601> 讓非同步方法快速提供進度。 它也可讓進度的取用者判斷最適合處理資訊的方式和位置。 例如，進度執行個體可以選擇在擷取的同步處理內容上封送處理回呼並引發事件。  
  
## <a name="iprogresst-implementations"></a>IProgress 的 \<T> 實施  
.NET 提供可執行檔 <xref:System.Progress%601> 類別 <xref:System.IProgress%601> 。 <xref:System.Progress%601> 類別的宣告方式如下：  
  
```csharp  
public class Progress<T> : IProgress<T>  
{  
    public Progress();  
    public Progress(Action<T> handler);  
    protected virtual void OnReport(T value);  
    public event EventHandler<T>? ProgressChanged;  
}  
```
  
 <xref:System.Progress%601> 執行個體會公開 <xref:System.Progress%601.ProgressChanged> 事件，該事件是在每次非同步作業報告進度更新時引發。 <xref:System.Progress%601.ProgressChanged> 事件是在具現化 <xref:System.Threading.SynchronizationContext> 執行個體時所擷取的 <xref:System.Progress%601> 物件上引發。 如果沒有可用的同步處理內容，則會使用以執行緒集區為目標的預設內容。 處理常式可能會向這個事件註冊。 為了方便起見，您也可以對 <xref:System.Progress%601> 建構函式提供單一處理常式，該處理常式的行為就像是 <xref:System.Progress%601.ProgressChanged> 事件的事件處理常式。 進度更新會以非同步方式引發，以避免在事件處理常式執行時延遲非同步作業。 另一個 <xref:System.IProgress%601> 實作可以選擇套用不同的語意。  
  
## <a name="choosing-the-overloads-to-provide"></a>選擇要提供的多載  
 如果 TAP 實作同時使用了選擇性的 <xref:System.Threading.Tasks.TaskFactory.CancellationToken%2A> 和選擇性的 <xref:System.IProgress%601> 參數，則最多可能會需要四個多載：  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, CancellationToken cancellationToken);  
public Task MethodNameAsync(…, IProgress<T> progress);
public Task MethodNameAsync(…,
    CancellationToken cancellationToken, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken cancellationToken) As Task  
Public MethodNameAsync(…, progress As IProgress(Of T)) As Task
Public MethodNameAsync(…, cancellationToken As CancellationToken,
                       progress As IProgress(Of T)) As Task  
```  
  
 不過，許多點一下執行都不會提供取消或進度功能，因此需要單一方法：  
  
```csharp  
public Task MethodNameAsync(…);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
```  
  
 如果 TAP 實作支援取消或進度，但不是同時支援兩者，它可能會提供兩個多載：  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, CancellationToken cancellationToken);  
  
// … or …  
  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken) As Task  
  
' … or …  
  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, progress As IProgress(Of T)) As Task  
```  
  
 如果 TAP 實作同時支援取消和進度，它可能會公開全部四個多載。 但是，它只會提供下列兩者：  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…,
    CancellationToken cancellationToken, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken,
                       progress As IProgress(Of T)) As Task  
```  
  
 為了彌補兩個遺漏的中繼組合，開發人員可以針對 <xref:System.Threading.CancellationToken.None%2A> 參數傳遞 <xref:System.Threading.CancellationToken> 或預設的 `cancellationToken`，並且針對 `null` 參數傳遞 `progress`。  
  
 如果您預期每個使用點的方法都支援取消或進度，您可能會省略不接受相關參數的多載。  
  
 如果您決定要公開多個多載以進行取消或進度選擇項，則不支援取消或進度的多載，其行為就像是將它們傳遞給 <xref:System.Threading.CancellationToken.None%2A> 取消，或進行支援這些的多載 `null` 。  
  
## <a name="related-articles"></a>相關文章
  
|標題|描述|  
|-----------|-----------------|  
|[非同步程式設計模式](index.md)|介紹執行非同步作業的三種模式：工作式非同步模式 (TAP)、非同步程式設計模型 (APM) 和事件式非同步模式 (EAP)。|  
|[實作以工作為基礎的非同步模式](implementing-the-task-based-asynchronous-pattern.md)|描述三種實作工作式非同步模式 (TAP) 的方式：使用 Visual Studio 中的 C# 和 Visual Basic 編譯器、手動，或是透過編譯器和手動方法的組合。|  
|[使用以工作為基礎的非同步模式](consuming-the-task-based-asynchronous-pattern.md)|描述如何使用工作和回呼達到等待的目的，而不會遭到封鎖。|  
|[Interop 與其他非同步模式和類型](interop-with-other-asynchronous-patterns-and-types.md)|描述如何使用工作式非同步模式 (TAP) 實作非同步程式設計模型 (APM) 和事件式非同步模式 (EAP)。|
