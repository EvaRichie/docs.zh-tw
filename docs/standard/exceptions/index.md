---
title: 在 .NET 中處理和擲回例外狀況
description: 瞭解如何在 .NET 中處理和擲回例外狀況。 例外狀況是 .NET 作業表示應用程式失敗的方式。
ms.date: 06/19/2018
helpviewer_keywords:
- exceptions [.NET], handling
- runtime, exceptions
- filtering exceptions
- errors [.NET], exceptions
- exceptions [.NET], throwing
- exceptions [.NET]
- common language runtime, exceptions
ms.assetid: f99a1d29-a2a8-47af-9707-9909f9010735
ms.openlocfilehash: c18482335947c8d24ba7ed6552bb78c70a0a054f
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94827993"
---
# <a name="handling-and-throwing-exceptions-in-net"></a><span data-ttu-id="a97ea-104">在 .NET 中處理和擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="a97ea-104">Handling and throwing exceptions in .NET</span></span>

<span data-ttu-id="a97ea-105">應用程式必須能以一致的方式處理執行期間發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a97ea-105">Applications must be able to handle errors that occur during execution in a consistent manner.</span></span> <span data-ttu-id="a97ea-106">.NET 提供模型，可以統一的方式通知應用程式的錯誤：.NET 作業會藉由擲回例外狀況指出失敗。</span><span class="sxs-lookup"><span data-stu-id="a97ea-106">.NET provides a model for notifying applications of errors in a uniform way: .NET operations indicate failure by throwing exceptions.</span></span>

## <a name="exceptions"></a><span data-ttu-id="a97ea-107">例外狀況</span><span class="sxs-lookup"><span data-stu-id="a97ea-107">Exceptions</span></span>

<span data-ttu-id="a97ea-108">例外狀況是執行程式所遇到的錯誤狀況或未預期的行為。</span><span class="sxs-lookup"><span data-stu-id="a97ea-108">An exception is any error condition or unexpected behavior that is encountered by an executing program.</span></span> <span data-ttu-id="a97ea-109">在發生程式碼或您呼叫的程式碼 (例如共用程式庫) 中有錯誤、無法使用作業系統資源、執行階段遇到非預期的狀況 (例如無法驗證的程式碼) 等情況時，就可能會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a97ea-109">Exceptions can be thrown because of a fault in your code or in code that you call (such as a shared library), unavailable operating system resources, unexpected conditions that the runtime encounters (such as code that can't be verified), and so on.</span></span> <span data-ttu-id="a97ea-110">您的應用程式可從一些狀況中復原，但有些狀況就無法復原。</span><span class="sxs-lookup"><span data-stu-id="a97ea-110">Your application can recover from some of these conditions, but not from others.</span></span> <span data-ttu-id="a97ea-111">雖然您可以從大部分的應用程式例外狀況中復原，但是無法從大部分的執行階段例外狀況中復原。</span><span class="sxs-lookup"><span data-stu-id="a97ea-111">Although you can recover from most application exceptions, you can't recover from most runtime exceptions.</span></span>

<span data-ttu-id="a97ea-112">在 .NET 中，例外狀況是繼承自 <xref:System.Exception?displayProperty=nameWithType> 類別的物件。</span><span class="sxs-lookup"><span data-stu-id="a97ea-112">In .NET, an exception is an object that inherits from the <xref:System.Exception?displayProperty=nameWithType> class.</span></span> <span data-ttu-id="a97ea-113">從發生問題的程式碼區域擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="a97ea-113">An exception is thrown from an area of code where a problem has occurred.</span></span> <span data-ttu-id="a97ea-114">例外狀況會向上傳遞堆疊，直到應用程式處理或程式終止它。</span><span class="sxs-lookup"><span data-stu-id="a97ea-114">The exception is passed up the stack until the application handles it or the program terminates.</span></span>

## <a name="exceptions-vs-traditional-error-handling-methods"></a><span data-ttu-id="a97ea-115">例外狀況與傳統錯誤處理方法的比較</span><span class="sxs-lookup"><span data-stu-id="a97ea-115">Exceptions vs. traditional error-handling methods</span></span>

<span data-ttu-id="a97ea-116">傳統上，一種語言的錯誤處理模型不是依賴語言唯一偵測錯誤的方式與尋找處理常式，就是依賴作業系統所提供的錯誤處理機制。</span><span class="sxs-lookup"><span data-stu-id="a97ea-116">Traditionally, a language's error-handling model relied on either the language's unique way of detecting errors and locating handlers for them, or on the error-handling mechanism provided by the operating system.</span></span> <span data-ttu-id="a97ea-117">.NET 實作例外狀況處理的方式具有下列優點：</span><span class="sxs-lookup"><span data-stu-id="a97ea-117">The way .NET implements exception handling provides the following advantages:</span></span>

- <span data-ttu-id="a97ea-118">.NET 程式語言擲回和處理例外狀況的方式都相同。</span><span class="sxs-lookup"><span data-stu-id="a97ea-118">Exception throwing and handling works the same for .NET programming languages.</span></span>

- <span data-ttu-id="a97ea-119">不需要任何特定語言語法以處理例外狀況，但可讓每一種語言定義屬於自己的語法。</span><span class="sxs-lookup"><span data-stu-id="a97ea-119">Doesn't require any particular language syntax for handling exceptions, but allows each language to define its own syntax.</span></span>

- <span data-ttu-id="a97ea-120">例外狀況可跨處理序，甚至是跨電腦界限擲回。</span><span class="sxs-lookup"><span data-stu-id="a97ea-120">Exceptions can be thrown across process and even machine boundaries.</span></span>

- <span data-ttu-id="a97ea-121">可將例外狀況處理程式碼加入應用程式，以增加程式可靠性。</span><span class="sxs-lookup"><span data-stu-id="a97ea-121">Exception-handling code can be added to an application to increase program reliability.</span></span>

<span data-ttu-id="a97ea-122">例外狀況優於其他錯誤通知方法，例如傳回碼。</span><span class="sxs-lookup"><span data-stu-id="a97ea-122">Exceptions offer advantages over other methods of error notification, such as return codes.</span></span> <span data-ttu-id="a97ea-123">不會發生未注意到失敗的情況，因為如果系統擲出例外狀況且您未加以處理，執行階段就會終止您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a97ea-123">Failures don't go unnoticed because if an exception is thrown and you don't handle it, the runtime terminates your application.</span></span> <span data-ttu-id="a97ea-124">無效值不會因為程式碼無法檢查失敗傳回碼，而持續在系統中散佈。</span><span class="sxs-lookup"><span data-stu-id="a97ea-124">Invalid values don't continue to propagate through the system as a result of code that fails to check for a failure return code.</span></span>

## <a name="common-exceptions"></a><span data-ttu-id="a97ea-125">常見例外狀況</span><span class="sxs-lookup"><span data-stu-id="a97ea-125">Common exceptions</span></span>

<span data-ttu-id="a97ea-126">下表列出一些常見的例外狀況，並提供可能造成這些例外狀況的原因範例。</span><span class="sxs-lookup"><span data-stu-id="a97ea-126">The following table lists some common exceptions with examples of what can cause them.</span></span>

| <span data-ttu-id="a97ea-127">例外狀況類型</span><span class="sxs-lookup"><span data-stu-id="a97ea-127">Exception type</span></span> | <span data-ttu-id="a97ea-128">說明</span><span class="sxs-lookup"><span data-stu-id="a97ea-128">Description</span></span> | <span data-ttu-id="a97ea-129">範例</span><span class="sxs-lookup"><span data-stu-id="a97ea-129">Example</span></span> |
| -------------- | ----------- | ------- |
| <xref:System.Exception> | <span data-ttu-id="a97ea-130">適用於所有例外狀況的基底類別。</span><span class="sxs-lookup"><span data-stu-id="a97ea-130">Base class for all exceptions.</span></span> | <span data-ttu-id="a97ea-131">無 (使用這個例外狀況的衍生類別)。</span><span class="sxs-lookup"><span data-stu-id="a97ea-131">None (use a derived class of this exception).</span></span> |
| <xref:System.IndexOutOfRangeException> | <span data-ttu-id="a97ea-132">只有當陣列索引不正確時，才由執行階段擲回。</span><span class="sxs-lookup"><span data-stu-id="a97ea-132">Thrown by the runtime only when an array is indexed improperly.</span></span> | <span data-ttu-id="a97ea-133">在陣列有效範圍之外對它進行索引：</span><span class="sxs-lookup"><span data-stu-id="a97ea-133">Indexing an array outside its valid range:</span></span> <br /> `arr[arr.Length+1]` |
| <xref:System.NullReferenceException> | <span data-ttu-id="a97ea-134">只有當參考 Null 物件時，才由執行階段擲回。</span><span class="sxs-lookup"><span data-stu-id="a97ea-134">Thrown by the runtime only when a null object is referenced.</span></span> | `object o = null;` <br /> `o.ToString();` |
| <xref:System.InvalidOperationException> | <span data-ttu-id="a97ea-135">當處於無效狀態時，由方法擲回。</span><span class="sxs-lookup"><span data-stu-id="a97ea-135">Thrown by methods when in an invalid state.</span></span> | <span data-ttu-id="a97ea-136">在從基礎集合將項目移除之後，呼叫 `Enumerator.MoveNext()`。</span><span class="sxs-lookup"><span data-stu-id="a97ea-136">Calling `Enumerator.MoveNext()` after removing an item from the underlying collection.</span></span> |
| <xref:System.ArgumentException> | <span data-ttu-id="a97ea-137">適用於所有引數例外狀況的基底類別。</span><span class="sxs-lookup"><span data-stu-id="a97ea-137">Base class for all argument exceptions.</span></span> | <span data-ttu-id="a97ea-138">無 (使用這個例外狀況的衍生類別)。</span><span class="sxs-lookup"><span data-stu-id="a97ea-138">None (use a derived class of this exception).</span></span> |
| <xref:System.ArgumentNullException> | <span data-ttu-id="a97ea-139">由不允許引數為 Null 的方法擲回。</span><span class="sxs-lookup"><span data-stu-id="a97ea-139">Thrown by methods that do not allow an argument to be null.</span></span> | `String s = null;` <br /> `"Calculate".IndexOf(s);`|
| <xref:System.ArgumentOutOfRangeException> | <span data-ttu-id="a97ea-140">由驗證引數是在指定範圍內的方法擲回。</span><span class="sxs-lookup"><span data-stu-id="a97ea-140">Thrown by methods that verify that arguments are in a given range.</span></span> | `String s = "string";` <br /> `s.Substring(s.Length+1);` |

## <a name="see-also"></a><span data-ttu-id="a97ea-141">請參閱</span><span class="sxs-lookup"><span data-stu-id="a97ea-141">See also</span></span>

- [<span data-ttu-id="a97ea-142">例外狀況類別和屬性</span><span class="sxs-lookup"><span data-stu-id="a97ea-142">Exception Class and Properties</span></span>](exception-class-and-properties.md)
- [<span data-ttu-id="a97ea-143">操作說明：使用 Try/Catch 區塊攔截例外狀況</span><span class="sxs-lookup"><span data-stu-id="a97ea-143">How to: Use the Try-Catch Block to Catch Exceptions</span></span>](how-to-use-the-try-catch-block-to-catch-exceptions.md)
- [<span data-ttu-id="a97ea-144">如何：使用 Catch 區塊中的特定例外狀況</span><span class="sxs-lookup"><span data-stu-id="a97ea-144">How to: Use Specific Exceptions in a Catch Block</span></span>](how-to-use-specific-exceptions-in-a-catch-block.md)
- [<span data-ttu-id="a97ea-145">如何：明確擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="a97ea-145">How to: Explicitly Throw Exceptions</span></span>](how-to-explicitly-throw-exceptions.md)
- [<span data-ttu-id="a97ea-146">操作說明：建立使用者定義的例外狀況</span><span class="sxs-lookup"><span data-stu-id="a97ea-146">How to: Create User-Defined Exceptions</span></span>](how-to-create-user-defined-exceptions.md)
- [<span data-ttu-id="a97ea-147">使用使用者篩選的例外狀況處理常式</span><span class="sxs-lookup"><span data-stu-id="a97ea-147">Using User-Filtered Exception Handlers</span></span>](using-user-filtered-exception-handlers.md)
- [<span data-ttu-id="a97ea-148">如何：使用 finally 區塊</span><span class="sxs-lookup"><span data-stu-id="a97ea-148">How to: Use Finally Blocks</span></span>](how-to-use-finally-blocks.md)
- [<span data-ttu-id="a97ea-149">處理 COM Interop 例外狀況</span><span class="sxs-lookup"><span data-stu-id="a97ea-149">Handling COM Interop Exceptions</span></span>](handling-com-interop-exceptions.md)
- [<span data-ttu-id="a97ea-150">例外狀況的最佳做法</span><span class="sxs-lookup"><span data-stu-id="a97ea-150">Best Practices for Exceptions</span></span>](best-practices-for-exceptions.md)
- [<span data-ttu-id="a97ea-151">每個開發人員在執行時間中需要瞭解例外狀況的相關資訊</span><span class="sxs-lookup"><span data-stu-id="a97ea-151">What Every Dev needs to Know About Exceptions in the Runtime</span></span>](https://github.com/dotnet/runtime/blob/master/docs/design/coreclr/botr/exceptions.md)
