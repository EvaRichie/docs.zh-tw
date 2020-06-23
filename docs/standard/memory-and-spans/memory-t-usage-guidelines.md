---
title: Memory<T> 與 Span<T> 使用指導方針
description: 本文描述記憶體 <T> 和 Span <T> ，這是 .net Core 中可用於管線的結構化資料緩衝區。
ms.date: 10/01/2018
helpviewer_keywords:
- Memory&lt;T&gt; and Span&lt;T&gt; best practices
- using Memory&lt;T&gt; and Span&lt;T&gt;
ms.openlocfilehash: d9a50fa18e027b6df7415438e1a5584003f7a094
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245592"
---
# <a name="memoryt-and-spant-usage-guidelines"></a><span data-ttu-id="606d2-103">Memory\<T> 與 Span\<T> 使用指導方針</span><span class="sxs-lookup"><span data-stu-id="606d2-103">Memory\<T> and Span\<T> usage guidelines</span></span>

<span data-ttu-id="606d2-104">.NET Core 包含數個可代表記憶體任意連續區域的類型。</span><span class="sxs-lookup"><span data-stu-id="606d2-104">.NET Core includes a number of types that represent an arbitrary contiguous region of memory.</span></span> <span data-ttu-id="606d2-105">.NET Core 2.0 已導入 <xref:System.Span%601> 和 <xref:System.ReadOnlySpan%601>，其為可由受控或非受控記憶體所支援的輕量型記憶體緩衝區。</span><span class="sxs-lookup"><span data-stu-id="606d2-105">.NET Core 2.0 introduced <xref:System.Span%601> and <xref:System.ReadOnlySpan%601>, which are lightweight memory buffers that can be backed by managed or unmanaged memory.</span></span> <span data-ttu-id="606d2-106">因為這些型別只能儲存在堆疊上，所以有幾個案例 (包括非同步方法呼叫) 不適合使用它們。</span><span class="sxs-lookup"><span data-stu-id="606d2-106">Because these types can only be stored on the stack, they are unsuitable for a number of scenarios, including asynchronous method calls.</span></span> <span data-ttu-id="606d2-107">.NET Core 2.1 新增數個額外類型，包括 <xref:System.Memory%601>、<xref:System.ReadOnlyMemory%601>、<xref:System.Buffers.IMemoryOwner%601>，以及 <xref:System.Buffers.MemoryPool%601>。</span><span class="sxs-lookup"><span data-stu-id="606d2-107">.NET Core 2.1 adds a number of additional types, including <xref:System.Memory%601>, <xref:System.ReadOnlyMemory%601>, <xref:System.Buffers.IMemoryOwner%601>, and <xref:System.Buffers.MemoryPool%601>.</span></span> <span data-ttu-id="606d2-108"><xref:System.Memory%601> 和其相關類型與 <xref:System.Span%601> 類似，可以由受控和非受控記憶體支援。</span><span class="sxs-lookup"><span data-stu-id="606d2-108">Like <xref:System.Span%601>, <xref:System.Memory%601> and its related types can be backed by both managed and unmanaged memory.</span></span> <span data-ttu-id="606d2-109"><xref:System.Memory%601> 與 <xref:System.Span%601> 不同，可儲存在受控堆積上。</span><span class="sxs-lookup"><span data-stu-id="606d2-109">Unlike <xref:System.Span%601>, <xref:System.Memory%601> can be stored on the managed heap.</span></span>

<span data-ttu-id="606d2-110"><xref:System.Span%601> 和 <xref:System.Memory%601> 都是可用於管線中的結構化資料緩衝區。</span><span class="sxs-lookup"><span data-stu-id="606d2-110">Both <xref:System.Span%601> and <xref:System.Memory%601> are buffers of structured data that can be used in pipelines.</span></span> <span data-ttu-id="606d2-111">也就是說，它們是被設計成能使部分或所有資料都能有效率地被傳遞至管線中的元件，其可處理它們或選擇性地修改緩衝區。</span><span class="sxs-lookup"><span data-stu-id="606d2-111">That is, they are designed so that some or all of the data can be efficiently passed to components in the pipeline, which can process them and optionally modify the buffer.</span></span> <span data-ttu-id="606d2-112">由於 <xref:System.Memory%601> 和其相關類型皆可由多個元件或多個執行緒存取，開發人員必須遵循一些標準的使用指導方針，以產生強固的程式碼。</span><span class="sxs-lookup"><span data-stu-id="606d2-112">Because <xref:System.Memory%601> and its related types can be accessed by multiple components or by multiple threads, it's important that developers follow some standard usage guidelines to produce robust code.</span></span>

## <a name="owners-consumers-and-lifetime-management"></a><span data-ttu-id="606d2-113">擁有者、取用者及存留期管理</span><span class="sxs-lookup"><span data-stu-id="606d2-113">Owners, consumers, and lifetime management</span></span>

<span data-ttu-id="606d2-114">由於緩衝區可在 API 之間傳遞，且緩衝區有時可以從多個執行緒存取，因此考慮存留期管理是一件非常重要的工作。</span><span class="sxs-lookup"><span data-stu-id="606d2-114">Since buffers can be passed around between APIs, and since buffers can sometimes be accessed from multiple threads, it's important to consider lifetime management.</span></span> <span data-ttu-id="606d2-115">有三個核心概念：</span><span class="sxs-lookup"><span data-stu-id="606d2-115">There are three core concepts:</span></span>

- <span data-ttu-id="606d2-116">**擁有權**。</span><span class="sxs-lookup"><span data-stu-id="606d2-116">**Ownership**.</span></span> <span data-ttu-id="606d2-117">緩衝區執行個體的擁有者必須負責處理存留期管理，其中包括終結不再使用的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="606d2-117">The owner of a buffer instance is responsible for lifetime management, including destroying the buffer when it's no longer in use.</span></span> <span data-ttu-id="606d2-118">所有緩衝區都具有單一擁有者。</span><span class="sxs-lookup"><span data-stu-id="606d2-118">All buffers have a single owner.</span></span> <span data-ttu-id="606d2-119">擁有者通常是建立緩衝區，或是從處理站接收緩衝區的元件。</span><span class="sxs-lookup"><span data-stu-id="606d2-119">Generally the owner is the component that created the buffer or that received the buffer from a factory.</span></span> <span data-ttu-id="606d2-120">擁有權也可以被轉移；**元件 A** 可以將緩衝區的控制轉移給**元件 B**，這會使**元件 A** 無法繼續使用該緩衝區，且**元件 B** 需負責在該緩衝區不再使用時終結它。</span><span class="sxs-lookup"><span data-stu-id="606d2-120">Ownership can also be transferred; **Component-A** can relinquish control of the buffer to **Component-B**, at which point **Component-A** may no longer use the buffer, and **Component-B** becomes responsible for destroying the buffer when it's no longer in use.</span></span>

- <span data-ttu-id="606d2-121">**耗用量**。</span><span class="sxs-lookup"><span data-stu-id="606d2-121">**Consumption**.</span></span> <span data-ttu-id="606d2-122">緩衝區執行個體的取用者可以透過從緩衝區執行個體進行讀取，或在某些情況下對它進行寫入，來使用該緩衝區執行個體。</span><span class="sxs-lookup"><span data-stu-id="606d2-122">The consumer of a buffer instance is allowed to use the buffer instance by reading from it and possibly writing to it.</span></span> <span data-ttu-id="606d2-123">緩衝區一次可以有一個取用者，除非已提供某種外部同步處理機制。</span><span class="sxs-lookup"><span data-stu-id="606d2-123">Buffers can have one consumer at a time unless some external synchronization mechanism is provided.</span></span> <span data-ttu-id="606d2-124">緩衝區的主動取用者不一定是緩衝區的擁有者。</span><span class="sxs-lookup"><span data-stu-id="606d2-124">The active consumer of a buffer isn't necessarily the buffer's owner.</span></span>

- <span data-ttu-id="606d2-125">**租用**。</span><span class="sxs-lookup"><span data-stu-id="606d2-125">**Lease**.</span></span> <span data-ttu-id="606d2-126">租用是特定元件可作為緩衝區取用者的時間長度。</span><span class="sxs-lookup"><span data-stu-id="606d2-126">The lease is the length of time that a particular component is allowed to be the consumer of the buffer.</span></span>

<span data-ttu-id="606d2-127">下列虛擬程式碼範例會說明這三個概念。</span><span class="sxs-lookup"><span data-stu-id="606d2-127">The following pseudo-code example illustrates these three concepts.</span></span> <span data-ttu-id="606d2-128">它包含能具現化 <xref:System.Char> 類型之 <xref:System.Memory%601> 緩衝區的 `Main` 方法，呼叫 `WriteInt32ToBuffer` 方法以將某個整數的字串表示法寫入該緩衝區，然後呼叫 `DisplayBufferToConsole` 方法來顯示該緩衝區的值。</span><span class="sxs-lookup"><span data-stu-id="606d2-128">It includes a `Main` method that instantiates a <xref:System.Memory%601> buffer of type <xref:System.Char>, calls the `WriteInt32ToBuffer` method to write the string representation of an integer to the buffer, and then calls the `DisplayBufferToConsole` method to display the value of the buffer.</span></span>

```csharp
using System;

class Program
{
    // Write 'value' as a human-readable string to the output buffer.
    void WriteInt32ToBuffer(int value, Buffer buffer);

    // Display the contents of the buffer to the console.
    void DisplayBufferToConsole(Buffer buffer);

    // Application code
    static void Main()
    {
        var buffer = CreateBuffer();
        try
        {
            int value = Int32.Parse(Console.ReadLine());
            WriteInt32ToBuffer(value, buffer);
            DisplayBufferToConsole(buffer);
        }
        finally
        {
            buffer.Destroy();
        }
    }
}
```

<span data-ttu-id="606d2-129">`Main` 方法會建立緩衝區 (在此範例中為 <xref:System.Span%601> 執行個體)，因此為其擁有者。</span><span class="sxs-lookup"><span data-stu-id="606d2-129">The `Main` method creates the buffer (in this case an <xref:System.Span%601> instance) and so is its owner.</span></span> <span data-ttu-id="606d2-130">因此，`Main` 必須負責在該緩衝區不再使用時終結它。</span><span class="sxs-lookup"><span data-stu-id="606d2-130">Therefore, `Main` is responsible for destroying the buffer when it's no longer in use.</span></span> <span data-ttu-id="606d2-131">它會透過呼叫緩衝區的 <xref:System.Span%601.Clear?displayProperty=nameWithType> 方法來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="606d2-131">It does this by calling the buffer's <xref:System.Span%601.Clear?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="606d2-132">(這裡的 <xref:System.Span%601.Clear> 方法實際上會清除緩衝區的記憶體，<xref:System.Span%601> 結構實際上沒有能終結緩衝區的方法)。</span><span class="sxs-lookup"><span data-stu-id="606d2-132">(The <xref:System.Span%601.Clear> method here actually clears the buffer's memory; the <xref:System.Span%601> structure doesn't actually have a method that destroys the buffer.)</span></span>

<span data-ttu-id="606d2-133">該緩衝區具有兩個取用者，`WriteInt32ToBuffer` 和 `DisplayBufferToConsole`。</span><span class="sxs-lookup"><span data-stu-id="606d2-133">The buffer has two consumers, `WriteInt32ToBuffer` and `DisplayBufferToConsole`.</span></span> <span data-ttu-id="606d2-134">一次只會有一個取用者 (先是 `WriteInt32ToBuffer`，然後是 `DisplayBufferToConsole`)，且這兩個取用者都不是該緩衝區的擁有者。</span><span class="sxs-lookup"><span data-stu-id="606d2-134">There is only one consumer at a time (first `WriteInt32ToBuffer`, then `DisplayBufferToConsole`), and neither of the consumers owns the buffer.</span></span> <span data-ttu-id="606d2-135">請注意，「取用者」一詞在此內容中並不代表針對緩衝區的唯讀檢視；如果將緩衝區的讀取/寫入檢視授與取用者，其將能修改緩衝區的內容 (如此範例中的 `WriteInt32ToBuffer`)。</span><span class="sxs-lookup"><span data-stu-id="606d2-135">Note also that "consumer" in this context doesn't imply a read-only view of the buffer; consumers can modify the buffer's contents, as `WriteInt32ToBuffer` does, if given a read/write view of the buffer.</span></span>

<span data-ttu-id="606d2-136">`WriteInt32ToBuffer` 方法在介於方法呼叫和方法傳回之間的時間內，針對該緩衝區會具有租用 (可取用該緩衝區)。</span><span class="sxs-lookup"><span data-stu-id="606d2-136">The `WriteInt32ToBuffer` method has a lease on (can consume) the buffer between the start of the method call and the time the method returns.</span></span> <span data-ttu-id="606d2-137">同樣地，在緩衝區執行期間，`DisplayBufferToConsole` 針對該緩衝區會具有租用，而該租用會在該方法回朔時釋放。</span><span class="sxs-lookup"><span data-stu-id="606d2-137">Similarly, `DisplayBufferToConsole` has a lease on the buffer while it's executing, and the lease is released when the method unwinds.</span></span> <span data-ttu-id="606d2-138">(沒有適用於租用管理的 API，「租用」本身是一種概念)。</span><span class="sxs-lookup"><span data-stu-id="606d2-138">(There is no API for lease management; a "lease" is a conceptual matter.)</span></span>

## <a name="memoryt-and-the-ownerconsumer-model"></a><span data-ttu-id="606d2-139">記憶體 \<T> 和擁有者/消費者模型</span><span class="sxs-lookup"><span data-stu-id="606d2-139">Memory\<T> and the owner/consumer model</span></span>

<span data-ttu-id="606d2-140">如同[擁有者、取用者及存留期管理](#owners-consumers-and-lifetime-management)一節所述，緩衝區一律會有一個擁有者。</span><span class="sxs-lookup"><span data-stu-id="606d2-140">As the [Owners, consumers, and lifetime management](#owners-consumers-and-lifetime-management) section notes, a buffer always has an owner.</span></span> <span data-ttu-id="606d2-141">.NET Core 支援兩種擁有權模型：</span><span class="sxs-lookup"><span data-stu-id="606d2-141">.NET Core supports two ownership models:</span></span>

- <span data-ttu-id="606d2-142">支援單一擁有權的模型。</span><span class="sxs-lookup"><span data-stu-id="606d2-142">A model that supports single ownership.</span></span> <span data-ttu-id="606d2-143">緩衝區在其存留期的整個期間，都會有單一的擁有者。</span><span class="sxs-lookup"><span data-stu-id="606d2-143">A buffer has a single owner for its entire lifetime.</span></span>

- <span data-ttu-id="606d2-144">支援擁有權傳輸的模型。</span><span class="sxs-lookup"><span data-stu-id="606d2-144">A model that supports ownership transfer.</span></span> <span data-ttu-id="606d2-145">緩衝區的擁有權可以從其原始擁有者 (其建立者) 轉換到另一個元件，而該元件將會接手負責該緩衝區的存留期管理。</span><span class="sxs-lookup"><span data-stu-id="606d2-145">Ownership of a buffer can be transferred from its original owner (its creator) to another component, which then becomes responsible for the buffer's lifetime management.</span></span> <span data-ttu-id="606d2-146">該擁有者接著可以再次將擁有權轉換到又另一個元件，依此類推。</span><span class="sxs-lookup"><span data-stu-id="606d2-146">That owner can in turn transfer ownership to another component, and so on.</span></span>

<span data-ttu-id="606d2-147">您會使用 <xref:System.Buffers.IMemoryOwner%601?displayProperty=nameWithType> 介面來明確管理緩衝區的擁有權。</span><span class="sxs-lookup"><span data-stu-id="606d2-147">You use the <xref:System.Buffers.IMemoryOwner%601?displayProperty=nameWithType> interface to explicitly manage the ownership of a buffer.</span></span> <span data-ttu-id="606d2-148"><xref:System.Buffers.IMemoryOwner%601> 同時支援這兩種擁有權模型。</span><span class="sxs-lookup"><span data-stu-id="606d2-148"><xref:System.Buffers.IMemoryOwner%601> supports both ownership models.</span></span> <span data-ttu-id="606d2-149">具有 <xref:System.Buffers.IMemoryOwner%601> 參考的元件會擁有緩衝區。</span><span class="sxs-lookup"><span data-stu-id="606d2-149">The component that has an <xref:System.Buffers.IMemoryOwner%601> reference owns the buffer.</span></span> <span data-ttu-id="606d2-150">下列範例會使用 <xref:System.Buffers.IMemoryOwner%601?> 實例來反映緩衝區的擁有權 <xref:System.Memory%601> 。</span><span class="sxs-lookup"><span data-stu-id="606d2-150">The following example uses an <xref:System.Buffers.IMemoryOwner%601?> instance to reflect the ownership of a <xref:System.Memory%601> buffer.</span></span>

[!code-csharp[ownership](~/samples/snippets/standard/buffers/memory-t/owner/owner.cs)]

<span data-ttu-id="606d2-151">我們也可以使用撰寫此範例 [`using`](../../csharp/language-reference/keywords/using-statement.md) ：</span><span class="sxs-lookup"><span data-stu-id="606d2-151">We can also write this example with the [`using`](../../csharp/language-reference/keywords/using-statement.md):</span></span>

[!code-csharp[ownership-using](~/samples/snippets/standard/buffers/memory-t/owner-using/owner-using.cs)]

<span data-ttu-id="606d2-152">在此程式碼中：</span><span class="sxs-lookup"><span data-stu-id="606d2-152">In this code:</span></span>

- <span data-ttu-id="606d2-153">`Main` 方法會保留針對 <xref:System.Buffers.IMemoryOwner%601> 執行個體的參考，因此 `Main` 方法是該緩衝區的擁有者。</span><span class="sxs-lookup"><span data-stu-id="606d2-153">The `Main` method holds the reference to the <xref:System.Buffers.IMemoryOwner%601> instance, so the `Main` method is the owner of the buffer.</span></span>

- <span data-ttu-id="606d2-154">`WriteInt32ToBuffer` 和 `DisplayBufferToConsole` 方法接受 <xref:System.Memory%601> 作為公用 API。</span><span class="sxs-lookup"><span data-stu-id="606d2-154">The `WriteInt32ToBuffer` and `DisplayBufferToConsole` methods accept <xref:System.Memory%601> as a public API.</span></span> <span data-ttu-id="606d2-155">因此，它們是該緩衝區的取用者。</span><span class="sxs-lookup"><span data-stu-id="606d2-155">Therefore, they are consumers of the buffer.</span></span> <span data-ttu-id="606d2-156">且它們之間一次只有一個會取用緩衝區。</span><span class="sxs-lookup"><span data-stu-id="606d2-156">And they only consume it one at a time.</span></span>

<span data-ttu-id="606d2-157">雖然 `WriteInt32ToBuffer` 方法的目的是要將值寫入緩衝區，但 `DisplayBufferToConsole` 方法則不會這麼做。</span><span class="sxs-lookup"><span data-stu-id="606d2-157">Although the `WriteInt32ToBuffer` method is intended to write a value to the buffer, the `DisplayBufferToConsole` method isn't.</span></span> <span data-ttu-id="606d2-158">為了反映此情況，它可以接受 <xref:System.ReadOnlyMemory%601>類型的引數。</span><span class="sxs-lookup"><span data-stu-id="606d2-158">To reflect this, it could have accepted an argument of type <xref:System.ReadOnlyMemory%601>.</span></span> <span data-ttu-id="606d2-159">如需有關的詳細資訊 <xref:System.ReadOnlyMemory%601> ，請參閱[規則 #2： \<T> \<T> 如果緩衝區應該是唯讀的，請使用 ReadOnlySpan 或 ReadOnlyMemory](#rule-2)。</span><span class="sxs-lookup"><span data-stu-id="606d2-159">For more information on <xref:System.ReadOnlyMemory%601>, see [Rule #2: Use ReadOnlySpan\<T> or ReadOnlyMemory\<T> if the buffer should be read-only](#rule-2).</span></span>

### <a name="ownerless-memoryt-instances"></a><span data-ttu-id="606d2-160">"Ownerless" 記憶體 \<T> 實例</span><span class="sxs-lookup"><span data-stu-id="606d2-160">"Ownerless" Memory\<T> instances</span></span>

<span data-ttu-id="606d2-161">您可以在不使用 <xref:System.Buffers.IMemoryOwner%601> 的情況下建立 <xref:System.Memory%601> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="606d2-161">You can create a <xref:System.Memory%601> instance without using <xref:System.Buffers.IMemoryOwner%601>.</span></span> <span data-ttu-id="606d2-162">在此情況下，緩衝區的擁有權是隱含而非明確的，且僅支援單一擁有者模型。</span><span class="sxs-lookup"><span data-stu-id="606d2-162">In this case, ownership of the buffer is implicit rather than explicit, and only the single-owner model is supported.</span></span> <span data-ttu-id="606d2-163">您可以這麼做來達到此目的：</span><span class="sxs-lookup"><span data-stu-id="606d2-163">You can do this by:</span></span>

- <span data-ttu-id="606d2-164">直接呼叫其中一個 <xref:System.Memory%601> 建構函式並傳遞 `T[]`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="606d2-164">Calling one of the  <xref:System.Memory%601> constructors directly, passing in a `T[]`, as the following example does.</span></span>

- <span data-ttu-id="606d2-165">呼叫 [String.AsMemory](xref:System.MemoryExtensions.AsMemory(System.String)) 擴充方法來產生 `ReadOnlyMemory<char>` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="606d2-165">Calling the [String.AsMemory](xref:System.MemoryExtensions.AsMemory(System.String)) extension method to produce a `ReadOnlyMemory<char>` instance.</span></span>

[!code-csharp[ownerless-memory](~/samples/snippets/standard/buffers/memory-t/ownerless/ownerless.cs)]

<span data-ttu-id="606d2-166">一開始建立 <xref:System.Memory%601> 執行個體的方法，便是緩衝區的隱含擁有者。</span><span class="sxs-lookup"><span data-stu-id="606d2-166">The method that initially creates the <xref:System.Memory%601> instance is the implicit owner of the buffer.</span></span> <span data-ttu-id="606d2-167">擁有權並無法被轉移到任何其他元件，因為沒有 <xref:System.Buffers.IMemoryOwner%601> 執行個體來促成該轉移。</span><span class="sxs-lookup"><span data-stu-id="606d2-167">Ownership cannot be transferred to any other component because there is no <xref:System.Buffers.IMemoryOwner%601> instance to facilitate the transfer.</span></span> <span data-ttu-id="606d2-168">(或者，您也可以想像執行階段的記憶體回收行程擁有該緩衝區，而所有方法皆只是取用該緩衝區)。</span><span class="sxs-lookup"><span data-stu-id="606d2-168">(As an alternative, you can also imagine that the runtime's garbage collector owns the buffer, and all methods just consume the buffer.)</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="606d2-169">使用指導方針</span><span class="sxs-lookup"><span data-stu-id="606d2-169">Usage guidelines</span></span>

<span data-ttu-id="606d2-170">由於記憶體區塊具有擁有者，同時會被傳遞至多個元件，且某些元件則會在特定的記憶體區塊上運作，因此有必要針對 <xref:System.Memory%601> 和 <xref:System.Span%601> 的使用建立指導方針。</span><span class="sxs-lookup"><span data-stu-id="606d2-170">Because a memory block is owned but is intended to be passed to multiple components, some of which may operate upon a particular memory block simultaneously, it is important to establish guidelines for using both <xref:System.Memory%601> and <xref:System.Span%601>.</span></span>  <span data-ttu-id="606d2-171">指導方針之所以必要，是因為：</span><span class="sxs-lookup"><span data-stu-id="606d2-171">Guidelines are necessary because:</span></span>

- <span data-ttu-id="606d2-172">元件可能會在記憶體區塊的擁有者釋放它之後，保留針對該記憶體區塊的參考。</span><span class="sxs-lookup"><span data-stu-id="606d2-172">It is possible for a component to retain a reference to a memory block after its owner has released it.</span></span>

- <span data-ttu-id="606d2-173">元件可能會和另一個元件同時在緩衝區上運作，並在期間損毀緩衝區中的資料。</span><span class="sxs-lookup"><span data-stu-id="606d2-173">It is possible for a component to operate on a buffer at the same time that another component is operating on it, in the process corrupting the data in the buffer.</span></span>

- <span data-ttu-id="606d2-174">雖然 <xref:System.Span%601> 的堆疊配置特性能對效能進行最佳化，並使 <xref:System.Span%601> 成為在記憶體區塊上運作的偏好類型，但它也會使 <xref:System.Span%601> 受制於某些顯著限制。</span><span class="sxs-lookup"><span data-stu-id="606d2-174">While the stack-allocated nature of <xref:System.Span%601> optimizes performance and makes <xref:System.Span%601> the preferred type for operating on a memory block, it also subjects <xref:System.Span%601> to some major restrictions.</span></span> <span data-ttu-id="606d2-175">請務必了解 <xref:System.Span%601> 和 <xref:System.Memory%601>的個別使用時機。</span><span class="sxs-lookup"><span data-stu-id="606d2-175">It is important to know when to use a <xref:System.Span%601> and when to use <xref:System.Memory%601>.</span></span>

<span data-ttu-id="606d2-176">下列為針對順利使用 <xref:System.Memory%601> 和其相關類型的建議。</span><span class="sxs-lookup"><span data-stu-id="606d2-176">The following are our recommendations for successfully using <xref:System.Memory%601> and its related types.</span></span> <span data-ttu-id="606d2-177">適用于和的 <xref:System.Memory%601> 指引 <xref:System.Span%601> 也適用于 <xref:System.ReadOnlyMemory%601> 和 <xref:System.ReadOnlySpan%601> ，除非我們明確注意其他事項。</span><span class="sxs-lookup"><span data-stu-id="606d2-177">Guidance that applies to <xref:System.Memory%601> and <xref:System.Span%601> also applies to <xref:System.ReadOnlyMemory%601> and <xref:System.ReadOnlySpan%601> unless we explicitly note otherwise.</span></span>

<span data-ttu-id="606d2-178">**規則 #1：若是同步 API，請使用 Span \<T> 而不是記憶體 \<T> 作為參數（如果可能的話）。**</span><span class="sxs-lookup"><span data-stu-id="606d2-178">**Rule #1: For a synchronous API, use Span\<T> instead of Memory\<T> as a parameter if possible.**</span></span>

<span data-ttu-id="606d2-179"><xref:System.Span%601> 比起 <xref:System.Memory%601> 更為靈活，且可以代表較廣泛類型的連續記憶體緩衝區。</span><span class="sxs-lookup"><span data-stu-id="606d2-179"><xref:System.Span%601> is more versatile than <xref:System.Memory%601> and can represent a wider variety of contiguous memory buffers.</span></span> <span data-ttu-id="606d2-180"><xref:System.Span%601> 也能夠提供比 <xref:System.Memory%601> 更為優異的效能。</span><span class="sxs-lookup"><span data-stu-id="606d2-180"><xref:System.Span%601> also offers better performance than <xref:System.Memory%601>.</span></span> <span data-ttu-id="606d2-181">最後，您可以使用 <xref:System.Memory%601.Span?displayProperty=nameWithType> 屬性將實例轉換成 <xref:System.Memory%601> ，雖然無法進行 <xref:System.Span%601> 跨 \<T> 記憶體 \<T> 轉換。</span><span class="sxs-lookup"><span data-stu-id="606d2-181">Finally, you can use the <xref:System.Memory%601.Span?displayProperty=nameWithType> property to convert a <xref:System.Memory%601> instance to a <xref:System.Span%601>, although Span\<T>-to-Memory\<T> conversion isn't possible.</span></span> <span data-ttu-id="606d2-182">因此如果您的呼叫端具有 <xref:System.Memory%601> 執行個體，它們仍然可以搭配 <xref:System.Span%601> 參數來呼叫您的方法。</span><span class="sxs-lookup"><span data-stu-id="606d2-182">So if your callers happen to have a <xref:System.Memory%601> instance, they'll be able to call your methods with <xref:System.Span%601> parameters anyway.</span></span>

<span data-ttu-id="606d2-183">使用 <xref:System.Span%601> 類型 (而非 <xref:System.Memory%601> 類型) 的參數也可以協助您寫入到正確的使用方法實作。</span><span class="sxs-lookup"><span data-stu-id="606d2-183">Using a parameter of type <xref:System.Span%601> instead of type <xref:System.Memory%601> also helps you write a correct consuming method implementation.</span></span> <span data-ttu-id="606d2-184">您將能自動取得編譯時間檢查，以確保您不會嘗試在方法租用以外的時間嘗試存取緩衝區 (將於稍後詳述)。</span><span class="sxs-lookup"><span data-stu-id="606d2-184">You'll automatically get compile-time checks to ensure that you're not attempting to access the buffer beyond your method's lease (more on this later).</span></span>

<span data-ttu-id="606d2-185">有時候，您將必須使用 <xref:System.Memory%601> 參數來取代 <xref:System.Span%601> 參數，就算您是完全同步也一樣。</span><span class="sxs-lookup"><span data-stu-id="606d2-185">Sometimes, you'll have to use a <xref:System.Memory%601> parameter instead of a <xref:System.Span%601> parameter, even if you're fully synchronous.</span></span> <span data-ttu-id="606d2-186">也許您仰賴的某個 API 僅接受 <xref:System.Memory%601> 引數。</span><span class="sxs-lookup"><span data-stu-id="606d2-186">Perhaps an API that you depend accepts only <xref:System.Memory%601> arguments.</span></span> <span data-ttu-id="606d2-187">這並沒有關係，但您必須記得以同步處理方式使用 <xref:System.Memory%601> 所會帶來的取捨。</span><span class="sxs-lookup"><span data-stu-id="606d2-187">This is fine, but be aware of the tradeoffs involved when using <xref:System.Memory%601> synchronously.</span></span>

<a name="rule-2"></a>

<span data-ttu-id="606d2-188">**規則 #2： \<T> \<T> 如果緩衝區應該是唯讀的，請使用 ReadOnlySpan 或 ReadOnlyMemory。**</span><span class="sxs-lookup"><span data-stu-id="606d2-188">**Rule #2: Use ReadOnlySpan\<T> or ReadOnlyMemory\<T> if the buffer should be read-only.**</span></span>

<span data-ttu-id="606d2-189">在稍早的範例中，`DisplayBufferToConsole` 方法只會從緩衝區讀取，它並不會修改緩衝區的內容。</span><span class="sxs-lookup"><span data-stu-id="606d2-189">In the earlier examples, the `DisplayBufferToConsole` method only reads from the buffer; it doesn't modify the contents of the buffer.</span></span> <span data-ttu-id="606d2-190">方法簽章應變更為下列項目。</span><span class="sxs-lookup"><span data-stu-id="606d2-190">The method signature should be changed to the following.</span></span>

```csharp
void DisplayBufferToConsole(ReadOnlyMemory<char> buffer);
```

<span data-ttu-id="606d2-191">事實上，如果我們將此規則與規則 #1 結合，我們便能進一步將方法簽章重新撰寫為下列項目：</span><span class="sxs-lookup"><span data-stu-id="606d2-191">In fact, if we combine this rule and Rule #1, we can do even better and rewrite the method signature as follows:</span></span>

```csharp
void DisplayBufferToConsole(ReadOnlySpan<char> buffer);
```

<span data-ttu-id="606d2-192">`DisplayBufferToConsole` 方法現在能與幾乎所有已知的緩衝區類型搭配運作：`T[]`、搭配 [stackalloc](../../csharp/language-reference/operators/stackalloc.md) 配置的儲存體等。</span><span class="sxs-lookup"><span data-stu-id="606d2-192">The `DisplayBufferToConsole` method now works with virtually every buffer type imaginable: `T[]`, storage allocated with [stackalloc](../../csharp/language-reference/operators/stackalloc.md), and so on.</span></span> <span data-ttu-id="606d2-193">您甚至可以直接將 <xref:System.String> 傳遞給它！</span><span class="sxs-lookup"><span data-stu-id="606d2-193">You can even pass a <xref:System.String> directly into it!</span></span>

<span data-ttu-id="606d2-194">**規則 #3：如果您的方法接受記憶體 \<T> 並傳回 `void` ，在方法傳回之後，您就不能使用記憶體 \<T> 實例。**</span><span class="sxs-lookup"><span data-stu-id="606d2-194">**Rule #3: If your method accepts Memory\<T> and returns `void`, you must not use the Memory\<T> instance after your method returns.**</span></span>

<span data-ttu-id="606d2-195">這與稍早提及的「租用」相關。</span><span class="sxs-lookup"><span data-stu-id="606d2-195">This relates to the "lease" concept mentioned earlier.</span></span> <span data-ttu-id="606d2-196">會傳回 void 的方法針對 <xref:System.Memory%601> 執行個體的租用，會在該方法進入時開始，並在方法離開時結束。</span><span class="sxs-lookup"><span data-stu-id="606d2-196">A void-returning method's lease on the <xref:System.Memory%601> instance begins when the method is entered, and it ends when the method exits.</span></span> <span data-ttu-id="606d2-197">請參考下列範例，其會根據來自主控台的輸入，以迴圈方式呼叫 `Log`。</span><span class="sxs-lookup"><span data-stu-id="606d2-197">Consider the following example, which calls `Log` in a loop based on input from the console.</span></span>

[!code-csharp[void-returning](~/samples/snippets/standard/buffers/memory-t/void-returning/void-returning.cs#1)]

<span data-ttu-id="606d2-198">如果 `Log` 是完全同步的方法，此程式碼會依預期的方式運作，因為記憶體執行個體在任何時候皆只有一個作用中的取用者。</span><span class="sxs-lookup"><span data-stu-id="606d2-198">If `Log` is a fully synchronous method, this code will behave as expected because there is only one active consumer of the memory instance at any given time.</span></span>
<span data-ttu-id="606d2-199">但想像 `Log` 具有此實作的情況。</span><span class="sxs-lookup"><span data-stu-id="606d2-199">But imagine instead that `Log` has this implementation.</span></span>

```csharp
// !!! INCORRECT IMPLEMENTATION !!!
static void Log(ReadOnlyMemory<char> message)
{
    // Run in background so that we don't block the main thread while performing IO.
    Task.Run(() =>
    {
        StreamWriter sw = File.AppendText(@".\input-numbers.dat");
        sw.WriteLine(message);
    });
}
```

<span data-ttu-id="606d2-200">在此實作中，`Log` 會違反其租用，因為在原始方法已傳回之後，它仍然會於背景嘗試使用 <xref:System.Memory%601> 執行個體。</span><span class="sxs-lookup"><span data-stu-id="606d2-200">In this implementation, `Log` violates its lease because it still attempts to use the <xref:System.Memory%601> instance in the background after the original method has returned.</span></span> <span data-ttu-id="606d2-201">在 `Log` 嘗試從緩衝區讀取時，`Main` 方法可能會對緩衝區造成變動，並進一步導致資料損毀。</span><span class="sxs-lookup"><span data-stu-id="606d2-201">The `Main` method could mutate the buffer while `Log` attempts to read from it, which could result in data corruption.</span></span>

<span data-ttu-id="606d2-202">有幾個方式可以解決此情況：</span><span class="sxs-lookup"><span data-stu-id="606d2-202">There are several ways to resolve this:</span></span>

- <span data-ttu-id="606d2-203">`Log` 方法可以傳回 <xref:System.Threading.Tasks.Task> 而非 `void`，如下列 `Log` 方法的實作所示。</span><span class="sxs-lookup"><span data-stu-id="606d2-203">The `Log` method can return a <xref:System.Threading.Tasks.Task> instead of `void`, as the following implementation of the `Log` method does.</span></span>

   [!code-csharp[task-returning](~/samples/snippets/standard/buffers/memory-t/task-returning2/task-returning2.cs#1)]

- <span data-ttu-id="606d2-204">可以改為以下列方式實作 `Log`：</span><span class="sxs-lookup"><span data-stu-id="606d2-204">`Log` can instead be implemented as follows:</span></span>

   [!code-csharp[defensive-copy](~/samples/snippets/standard/buffers/memory-t/task-returning/task-returning.cs#1)]

<span data-ttu-id="606d2-205">**規則 #4：如果您的方法接受記憶體 \<T> 並傳回工作，則在 \<T> 工作轉換為結束狀態之後，您就不能使用記憶體實例。**</span><span class="sxs-lookup"><span data-stu-id="606d2-205">**Rule #4: If your method accepts a Memory\<T> and returns a Task, you must not use the Memory\<T> instance after the Task transitions to a terminal state.**</span></span>

<span data-ttu-id="606d2-206">這基本上是規則 #3 的非同步變化。</span><span class="sxs-lookup"><span data-stu-id="606d2-206">This is just the async variant of Rule #3.</span></span> <span data-ttu-id="606d2-207">先前範例的 `Log` 方法可以透過下列方式撰寫來符合此規則：</span><span class="sxs-lookup"><span data-stu-id="606d2-207">The `Log` method from the earlier example can be written as follows to comply with this rule:</span></span>

[!code-csharp[task-returning-async](~/samples/snippets/standard/buffers/memory-t/void-returning-async/void-returning-async.cs#1)]

<span data-ttu-id="606d2-208">在這裡，「終止狀態」表示工作已轉換為已完成、已發生錯誤，或已取消的狀態。</span><span class="sxs-lookup"><span data-stu-id="606d2-208">Here, "terminal state" means that the task transitions to a completed, faulted, or canceled state.</span></span> <span data-ttu-id="606d2-209">換句話說，「終止狀態」的意思是「任何會導致等候擲回或繼續執行的項目」。</span><span class="sxs-lookup"><span data-stu-id="606d2-209">In other words, "terminal state" means "anything that would cause await to throw or to continue execution."</span></span>

<span data-ttu-id="606d2-210">此指南適用於會傳回 <xref:System.Threading.Tasks.Task>、<xref:System.Threading.Tasks.Task%601>、<xref:System.Threading.Tasks.ValueTask%601>，或任何類似類型的方法。</span><span class="sxs-lookup"><span data-stu-id="606d2-210">This guidance applies to methods that return <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.ValueTask%601>, or any similar type.</span></span>

<span data-ttu-id="606d2-211">**規則 #5：如果您的函式接受記憶體 \<T> 做為參數，則會假設已構造物件上的實例方法是記憶體實例的取用者 \<T> 。**</span><span class="sxs-lookup"><span data-stu-id="606d2-211">**Rule #5: If your constructor accepts Memory\<T> as a parameter, instance methods on the constructed object are assumed to be consumers of the Memory\<T> instance.**</span></span>

<span data-ttu-id="606d2-212">請考慮下列範例：</span><span class="sxs-lookup"><span data-stu-id="606d2-212">Consider the following example:</span></span>

```csharp
class OddValueExtractor
{
    public OddValueExtractor(ReadOnlyMemory<int> input);
    public bool TryReadNextOddValue(out int value);
}

void PrintAllOddValues(ReadOnlyMemory<int> input)
{
    var extractor = new OddValueExtractor(input);
    while (extractor.TryReadNextOddValue(out int value))
    {
      Console.WriteLine(value);
    }
}
```

<span data-ttu-id="606d2-213">在這裡，`OddValueExtractor` 建構函式會接受 `ReadOnlyMemory<int>` 作為建構函式參數，因此建構函式本身是 `ReadOnlyMemory<int>` 執行個體的取用者，且已傳回值上的所有執行個體方法也都會是原始 `ReadOnlyMemory<int>` 執行個體的取用者。</span><span class="sxs-lookup"><span data-stu-id="606d2-213">Here, the `OddValueExtractor` constructor accepts a `ReadOnlyMemory<int>` as a constructor parameter, so the constructor itself is a consumer of the `ReadOnlyMemory<int>` instance, and all instance methods on the returned value are also consumers of the original `ReadOnlyMemory<int>` instance.</span></span> <span data-ttu-id="606d2-214">這代表 `TryReadNextOddValue` 會取用 `ReadOnlyMemory<int>` 執行個體，就算該執行個體不會直接被傳遞至 `TryReadNextOddValue` 方法也一樣。</span><span class="sxs-lookup"><span data-stu-id="606d2-214">This means that `TryReadNextOddValue` consumes the `ReadOnlyMemory<int>` instance, even though the instance isn't passed directly to the `TryReadNextOddValue` method.</span></span>

<span data-ttu-id="606d2-215">**規則 #6：如果您的類型上有可設定的記憶體 \<T> 類型屬性（或對等的實例方法），則會假設該物件上的實例方法是記憶體實例的取用者 \<T> 。**</span><span class="sxs-lookup"><span data-stu-id="606d2-215">**Rule #6: If you have a settable Memory\<T>-typed property (or an equivalent instance method) on your type, instance methods on that object are assumed to be consumers of the Memory\<T> instance.**</span></span>

<span data-ttu-id="606d2-216">這基本上是規則 #5 的變化。</span><span class="sxs-lookup"><span data-stu-id="606d2-216">This is really just a variant of Rule #5.</span></span> <span data-ttu-id="606d2-217">此規則之所以存在，是因為我們會假設屬性設定者或對等方法會擷取或保留其輸入，好讓相同物件上的執行個體方法能夠運用擷取的狀態。</span><span class="sxs-lookup"><span data-stu-id="606d2-217">This rule exists because property setters or equivalent methods are assumed to capture and persist their inputs, so instance methods on the same object may utilize the captured state.</span></span>

<span data-ttu-id="606d2-218">下列範例會觸發此規則：</span><span class="sxs-lookup"><span data-stu-id="606d2-218">The following example triggers this rule:</span></span>

```csharp
class Person
{
    // Settable property.
    public Memory<char> FirstName { get; set; }

    // alternatively, equivalent "setter" method
    public SetFirstName(Memory<char> value);

    // alternatively, a public settable field
    public Memory<char> FirstName;
}
```

<span data-ttu-id="606d2-219">**規則 #7：如果您有 Imemoryowner t> \<T> 參考，您必須在某個時間點處置它，或轉移其擁有權（但不能兩者）。**</span><span class="sxs-lookup"><span data-stu-id="606d2-219">**Rule #7: If you have an IMemoryOwner\<T> reference, you must at some point dispose of it or transfer its ownership (but not both).**</span></span>

<span data-ttu-id="606d2-220">由於 <xref:System.Memory%601> 執行個體可由受控或非受控記憶體支援，擁有者必須在 <xref:System.Memory%601> 執行個體上的作業完成時呼叫 <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="606d2-220">Since a <xref:System.Memory%601> instance may be backed by either managed or unmanaged memory, the owner must call <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType> when work performed on the <xref:System.Memory%601> instance is complete.</span></span> <span data-ttu-id="606d2-221">或者，擁有者可以將 <xref:System.Buffers.IMemoryOwner%601> 執行個體的擁有權轉換給不同的元件，而在轉換之後，取得擁有權的元件便必須負責在適當的時機呼叫 <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType> (將於稍後詳述)。</span><span class="sxs-lookup"><span data-stu-id="606d2-221">Alternatively, the owner may transfer ownership of the <xref:System.Buffers.IMemoryOwner%601> instance to a different component, at which point the acquiring component becomes responsible for calling <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType> at the appropriate time (more on this later).</span></span>

<span data-ttu-id="606d2-222">若未呼叫 <xref:System.Buffers.MemoryPool%601.Dispose%2A> 方法，可能會導致非受控的記憶體流失或其他效能降低。</span><span class="sxs-lookup"><span data-stu-id="606d2-222">Failure to call the <xref:System.Buffers.MemoryPool%601.Dispose%2A> method may lead to unmanaged memory leaks or other performance degradation.</span></span>

<span data-ttu-id="606d2-223">此規則也適用於呼叫 Factory 方法 (例如 <xref:System.Buffers.MemoryPool%601.Rent%2A?displayProperty=nameWithType>) 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="606d2-223">This rule also applies to code that calls factory methods like <xref:System.Buffers.MemoryPool%601.Rent%2A?displayProperty=nameWithType>.</span></span> <span data-ttu-id="606d2-224">呼叫者會成為傳回 <xref:System.Buffers.IMemoryOwner%601> 的擁有者，並須負責在完成時處置執行個體。</span><span class="sxs-lookup"><span data-stu-id="606d2-224">The caller becomes the owner of the returned <xref:System.Buffers.IMemoryOwner%601> and is responsible for disposing of the instance when finished.</span></span>

<span data-ttu-id="606d2-225">**規則 #8：如果您的 \<T> API 介面中有 imemoryowner t> 參數，即表示您接受該實例的擁有權。**</span><span class="sxs-lookup"><span data-stu-id="606d2-225">**Rule #8: If you have an IMemoryOwner\<T> parameter in your API surface, you are accepting ownership of that instance.**</span></span>

<span data-ttu-id="606d2-226">接受此類型的執行個體，便代表您的元件意圖取得此執行個體的擁有權。</span><span class="sxs-lookup"><span data-stu-id="606d2-226">Accepting an instance of this type signals that your component intends to take ownership of this instance.</span></span> <span data-ttu-id="606d2-227">您的元件必須負責進行規則 #7 中所述的適當處置。</span><span class="sxs-lookup"><span data-stu-id="606d2-227">Your component becomes responsible for proper disposal according to Rule #7.</span></span>

<span data-ttu-id="606d2-228">將 <xref:System.Buffers.IMemoryOwner%601> 執行個體的擁有權轉換給另一個元件的任何元件，都不應該在方法呼叫完成之後繼續使用該執行個體。</span><span class="sxs-lookup"><span data-stu-id="606d2-228">Any component that transfers ownership of the <xref:System.Buffers.IMemoryOwner%601> instance to a different component should no longer use that instance after the method call completes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="606d2-229">如果您的建構函式會接受 <xref:System.Buffers.IMemoryOwner%601> 作為參數，其類型應實作 <xref:System.IDisposable>，且您的 <xref:System.IDisposable.Dispose%2A> 方法應該要呼叫 <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType>。</span><span class="sxs-lookup"><span data-stu-id="606d2-229">If your constructor accepts <xref:System.Buffers.IMemoryOwner%601> as a parameter, its type should implement <xref:System.IDisposable>, and your <xref:System.IDisposable.Dispose%2A> method should call <xref:System.Buffers.MemoryPool%601.Dispose%2A?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="606d2-230">**規則 #9：如果您要包裝同步 p/invoke 方法，您的 API 應該接受 Span \<T> 做為參數。**</span><span class="sxs-lookup"><span data-stu-id="606d2-230">**Rule #9: If you're wrapping a synchronous p/invoke method, your API should accept Span\<T> as a parameter.**</span></span>

<span data-ttu-id="606d2-231">根據規則 #1，<xref:System.Span%601> 通常是應該用於同步 API 的正確類型。</span><span class="sxs-lookup"><span data-stu-id="606d2-231">According to Rule #1, <xref:System.Span%601> is generally the correct type to use for synchronous APIs.</span></span> <span data-ttu-id="606d2-232">您可以透過 <xref:System.Span%601> 關鍵字釘選實例 [`fixed`](../../csharp/language-reference/keywords/fixed-statement.md) ，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="606d2-232">You can pin <xref:System.Span%601> instances via the [`fixed`](../../csharp/language-reference/keywords/fixed-statement.md) keyword, as in the following example.</span></span>

```csharp
using System.Runtime.InteropServices;

[DllImport(...)]
private static extern unsafe int ExportedMethod(byte* pbData, int cbData);

public unsafe int ManagedWrapper(Span<byte> data)
{
    fixed (byte* pbData = &MemoryMarshal.GetReference(data))
    {
        int retVal = ExportedMethod(pbData, data.Length);

        /* error checking retVal goes here */

        return retVal;
    }
}
```

<span data-ttu-id="606d2-233">在先前的範例中，`pbData` 在如輸入 span 為空白之類的情況下，可能會是 Null。</span><span class="sxs-lookup"><span data-stu-id="606d2-233">In the previous example, `pbData` can be null if, for example, the input span is empty.</span></span> <span data-ttu-id="606d2-234">如果匯出的方法一定需要 `pbData` 是非 Null (就算 `cbData` 是 0)，則可以如下所示實作該方法：</span><span class="sxs-lookup"><span data-stu-id="606d2-234">If the exported method absolutely requires that `pbData` be non-null, even if `cbData` is 0, the method can be implemented as follows:</span></span>

```csharp
public unsafe int ManagedWrapper(Span<byte> data)
{
    fixed (byte* pbData = &MemoryMarshal.GetReference(data))
    {
        byte dummy = 0;
        int retVal = ExportedMethod((pbData != null) ? pbData : &dummy, data.Length);

        /* error checking retVal goes here */

        return retVal;
    }
}
```

<span data-ttu-id="606d2-235">**規則 #10：如果您要包裝非同步 p/invoke 方法，您的 API 應該接受記憶體 \<T> 作為參數。**</span><span class="sxs-lookup"><span data-stu-id="606d2-235">**Rule #10: If you're wrapping an asynchronous p/invoke method, your API should accept Memory\<T> as a parameter.**</span></span>

<span data-ttu-id="606d2-236">由於您無法 [`fixed`](../../csharp/language-reference/keywords/fixed-statement.md) 跨非同步作業使用關鍵字，因此您可以使用 <xref:System.Memory%601.Pin%2A?displayProperty=nameWithType> 方法來釘選 <xref:System.Memory%601> 實例，而不論實例所代表的連續記憶體種類為何。</span><span class="sxs-lookup"><span data-stu-id="606d2-236">Since you cannot use the [`fixed`](../../csharp/language-reference/keywords/fixed-statement.md) keyword across asynchronous operations, you use the <xref:System.Memory%601.Pin%2A?displayProperty=nameWithType> method to pin <xref:System.Memory%601> instances, regardless of the kind of contiguous memory the instance represents.</span></span> <span data-ttu-id="606d2-237">下列範例示範如何使用此 API 來執行非同步 p/invoke 呼叫。</span><span class="sxs-lookup"><span data-stu-id="606d2-237">The following example shows how to use this API to perform an asynchronous p/invoke call.</span></span>

```csharp
using System.Runtime.InteropServices;

[UnmanagedFunctionPointer(...)]
private delegate void OnCompletedCallback(IntPtr state, int result);

[DllImport(...)]
private static extern unsafe int ExportedAsyncMethod(byte* pbData, int cbData, IntPtr pState, IntPtr lpfnOnCompletedCallback);

private static readonly IntPtr _callbackPtr = GetCompletionCallbackPointer();

public unsafe Task<int> ManagedWrapperAsync(Memory<byte> data)
{
    // setup
    var tcs = new TaskCompletionSource<int>();
    var state = new MyCompletedCallbackState
    {
        Tcs = tcs
    };
    var pState = (IntPtr)GCHandle.Alloc(state);

    var memoryHandle = data.Pin();
    state.MemoryHandle = memoryHandle;

    // make the call
    int result;
    try
    {
        result = ExportedAsyncMethod((byte*)memoryHandle.Pointer, data.Length, pState, _callbackPtr);
    }
    catch
    {
        ((GCHandle)pState).Free(); // cleanup since callback won't be invoked
        memoryHandle.Dispose();
        throw;
    }

    if (result != PENDING)
    {
        // Operation completed synchronously; invoke callback manually
        // for result processing and cleanup.
        MyCompletedCallbackImplementation(pState, result);
    }

    return tcs.Task;
}

private static void MyCompletedCallbackImplementation(IntPtr state, int result)
{
    GCHandle handle = (GCHandle)state;
    var actualState = (MyCompletedCallbackState)(handle.Target);
    handle.Free();
    actualState.MemoryHandle.Dispose();

    /* error checking result goes here */

    if (error)
    {
        actualState.Tcs.SetException(...);
    }
    else
    {
        actualState.Tcs.SetResult(result);
    }
}

private static IntPtr GetCompletionCallbackPointer()
{
    OnCompletedCallback callback = MyCompletedCallbackImplementation;
    GCHandle.Alloc(callback); // keep alive for lifetime of application
    return Marshal.GetFunctionPointerForDelegate(callback);
}

private class MyCompletedCallbackState
{
    public TaskCompletionSource<int> Tcs;
    public MemoryHandle MemoryHandle;
}
```

## <a name="see-also"></a><span data-ttu-id="606d2-238">另請參閱</span><span class="sxs-lookup"><span data-stu-id="606d2-238">See also</span></span>

- <xref:System.Memory%601?displayProperty=nameWithType>
- <xref:System.Buffers.IMemoryOwner%601?displayProperty=nameWithType>
- <xref:System.Span%601?displayProperty=nameWithType>
