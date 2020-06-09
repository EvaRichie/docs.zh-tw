---
title: 使用實作 IDisposable 的物件
description: 瞭解如何使用在 .NET 中執行 IDisposable 介面的物件。 使用非受控資源的類型會執行 IDisposable，以允許資源回收。
ms.date: 05/13/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dispose method
- try/finally block
- garbage collection, encapsulating resources
ms.assetid: 81b2cdb5-c91a-4a31-9c83-eadc52da5cf0
ms.openlocfilehash: 7d5d4080f22aab6870a230d495b4a4b9ebcb3b96
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599850"
---
# <a name="using-objects-that-implement-idisposable"></a><span data-ttu-id="c250a-104">使用實作 IDisposable 的物件</span><span class="sxs-lookup"><span data-stu-id="c250a-104">Using objects that implement IDisposable</span></span>

<span data-ttu-id="c250a-105">通用語言執行平臺的垃圾收集行程會回收 managed 物件所使用的記憶體，但是使用非受控資源的類型 <xref:System.IDisposable> 會執行介面，以允許回收這些非受控資源所需的資源。</span><span class="sxs-lookup"><span data-stu-id="c250a-105">The common language runtime's garbage collector reclaims the memory used by managed objects, but types that use unmanaged resources implement the <xref:System.IDisposable> interface to allow the resources needed by these unmanaged resources to be reclaimed.</span></span> <span data-ttu-id="c250a-106">實作 <xref:System.IDisposable> 的物件使用完畢時，您應呼叫物件的 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 實作。</span><span class="sxs-lookup"><span data-stu-id="c250a-106">When you finish using an object that implements <xref:System.IDisposable>, you should call the object's <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> implementation.</span></span> <span data-ttu-id="c250a-107">您可以使用下列其中一種作法：</span><span class="sxs-lookup"><span data-stu-id="c250a-107">You can do this in one of two ways:</span></span>

- <span data-ttu-id="c250a-108">使用 c # `using` 語句（ `Using` 在 Visual Basic 中）。</span><span class="sxs-lookup"><span data-stu-id="c250a-108">With the C# `using` statement (`Using` in Visual Basic).</span></span>
- <span data-ttu-id="c250a-109">藉由執行 `try/finally` 區塊，並 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 在中呼叫 `finally` 。</span><span class="sxs-lookup"><span data-stu-id="c250a-109">By implementing a `try/finally` block, and calling the <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> in the `finally`.</span></span>

## <a name="the-using-statement"></a><span data-ttu-id="c250a-110">using 陳述式</span><span class="sxs-lookup"><span data-stu-id="c250a-110">The using statement</span></span>

<span data-ttu-id="c250a-111">C # 中的[ `using` 語句](../../csharp/language-reference/keywords/using-statement.md)和中的[ `Using` 語句](../../visual-basic/language-reference/statements/using-statement.md)Visual Basic 會簡化您必須撰寫的程式碼，以清除物件。</span><span class="sxs-lookup"><span data-stu-id="c250a-111">The [`using` statement](../../csharp/language-reference/keywords/using-statement.md) in C# and the [`Using` statement](../../visual-basic/language-reference/statements/using-statement.md) in Visual Basic simplify the code that you must write to cleanup an object.</span></span> <span data-ttu-id="c250a-112">`using` 陳述式會取得一項或多項資源、執行您指定的陳述式，然後自動處置該物件。</span><span class="sxs-lookup"><span data-stu-id="c250a-112">The `using` statement obtains one or more resources, executes the statements that you specify, and automatically disposes of the object.</span></span> <span data-ttu-id="c250a-113">不過，`using` 陳述式只對建構物件的方法範圍內所使用的物件有其實用之處。</span><span class="sxs-lookup"><span data-stu-id="c250a-113">However, the `using` statement is useful only for objects that are used within the scope of the method in which they are constructed.</span></span>

<span data-ttu-id="c250a-114">下列範例會使用 `using` 陳述式建立和發行 <xref:System.IO.StreamReader?displayProperty=nameWithType> 物件。</span><span class="sxs-lookup"><span data-stu-id="c250a-114">The following example uses the `using` statement to create and release a <xref:System.IO.StreamReader?displayProperty=nameWithType> object.</span></span>

[!code-csharp[Conceptual.Disposable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using1.cs#1)]
[!code-vb[Conceptual.Disposable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using1.vb#1)]

<span data-ttu-id="c250a-115">雖然類別會實作為 <xref:System.IO.StreamReader> <xref:System.IDisposable> 介面，這表示它會使用非受控資源，但此範例並不會明確地呼叫 <xref:System.IO.StreamReader.Dispose%2A?displayProperty=nameWithType> 方法。</span><span class="sxs-lookup"><span data-stu-id="c250a-115">Although the <xref:System.IO.StreamReader> class implements the <xref:System.IDisposable> interface, which indicates that it uses an unmanaged resource, the example doesn't explicitly call the <xref:System.IO.StreamReader.Dispose%2A?displayProperty=nameWithType> method.</span></span> <span data-ttu-id="c250a-116">當 C# 或 Visual Basic 編譯器遇到 `using` 陳述式時，會發出相當於下列明確包含 `try/finally` 區塊之程式碼的中繼語言 (IL)。</span><span class="sxs-lookup"><span data-stu-id="c250a-116">When the C# or Visual Basic compiler encounters the `using` statement, it emits intermediate language (IL) that is equivalent to the following code that explicitly contains a `try/finally` block.</span></span>

[!code-csharp[Conceptual.Disposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using3.cs#3)]
[!code-vb[Conceptual.Disposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using3.vb#3)]

<span data-ttu-id="c250a-117">C# `using` 陳述式還可讓您以單一陳述式取得多項資源，其內部相當於巢狀的 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c250a-117">The C# `using` statement also allows you to acquire multiple resources in a single statement, which is internally equivalent to nested `using` statements.</span></span> <span data-ttu-id="c250a-118">下列範例會將兩個 <xref:System.IO.StreamReader> 物件具現化，以便讀取兩個不同檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="c250a-118">The following example instantiates two <xref:System.IO.StreamReader> objects to read the contents of two different files.</span></span>

[!code-csharp[Conceptual.Disposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using4.cs#4)]

## <a name="tryfinally-block"></a><span data-ttu-id="c250a-119">Try/finally 區塊</span><span class="sxs-lookup"><span data-stu-id="c250a-119">Try/finally block</span></span>

<span data-ttu-id="c250a-120">您可以選擇直接實作 `try/finally` 區塊，而不將 `try/finally` 區塊包裝在 `using` 陳述式中。</span><span class="sxs-lookup"><span data-stu-id="c250a-120">Instead of wrapping a `try/finally` block in a `using` statement, you may choose to implement the `try/finally` block directly.</span></span> <span data-ttu-id="c250a-121">這可能是您的個人編碼樣式，或者您可能會因為下列其中一個原因而想要這麼做：</span><span class="sxs-lookup"><span data-stu-id="c250a-121">It may be your personal coding style, or you might want to do this for one of the following reasons:</span></span>

- <span data-ttu-id="c250a-122">包含 `catch` 區塊以處理區塊中擲回的例外狀況 `try` 。</span><span class="sxs-lookup"><span data-stu-id="c250a-122">To include a `catch` block to handle exceptions thrown in the `try` block.</span></span> <span data-ttu-id="c250a-123">否則，在語句中擲回的任何例外狀況 `using` 都不會被處理。</span><span class="sxs-lookup"><span data-stu-id="c250a-123">Otherwise, any exceptions thrown within the `using` statement are unhandled.</span></span>

- <span data-ttu-id="c250a-124">若要將實作 <xref:System.IDisposable> 且範圍對於物件宣告所在區塊並非區域的物件具現化。</span><span class="sxs-lookup"><span data-stu-id="c250a-124">To instantiate an object that implements <xref:System.IDisposable> whose scope is not local to the block within which it is declared.</span></span>

<span data-ttu-id="c250a-125">下列範例類似上述範例，不過它會使用 `try/catch/finally` 區塊具現化、使用和處置 <xref:System.IO.StreamReader> 物件，以及處理 <xref:System.IO.StreamReader> 建構函式和其 <xref:System.IO.StreamReader.ReadToEnd%2A> 方法擲回的所有例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c250a-125">The following example is similar to the previous example, except that it uses a `try/catch/finally` block to instantiate, use, and dispose of a <xref:System.IO.StreamReader> object, and to handle any exceptions thrown by the <xref:System.IO.StreamReader> constructor and its <xref:System.IO.StreamReader.ReadToEnd%2A> method.</span></span> <span data-ttu-id="c250a-126">區塊中的程式碼 `finally` <xref:System.IDisposable> 會在 `null` 呼叫方法之前，檢查所執行的物件 <xref:System.IDisposable.Dispose%2A> 。</span><span class="sxs-lookup"><span data-stu-id="c250a-126">The code in the `finally` block checks that the object that implements <xref:System.IDisposable> isn't `null` before it calls the <xref:System.IDisposable.Dispose%2A> method.</span></span> <span data-ttu-id="c250a-127">若未這樣做，可能導致執行階段產生 <xref:System.NullReferenceException> 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="c250a-127">Failure to do this can result in a <xref:System.NullReferenceException> exception at run time.</span></span>

[!code-csharp[Conceptual.Disposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using5.cs#6)]
[!code-vb[Conceptual.Disposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using5.vb#6)]

<span data-ttu-id="c250a-128">如果您的程式語言不支援 `using` 陳述式，但是允許直接呼叫 <xref:System.IDisposable.Dispose%2A> 方法，而使得您選擇實作或必須實作 `try/finally` 區塊，則可以遵循這個基本模式。</span><span class="sxs-lookup"><span data-stu-id="c250a-128">You can follow this basic pattern if you choose to implement or must implement a `try/finally` block, because your programming language doesn't support a `using` statement but does allow direct calls to the <xref:System.IDisposable.Dispose%2A> method.</span></span>

## <a name="idisposable-instance-members"></a><span data-ttu-id="c250a-129">IDisposable 實例成員</span><span class="sxs-lookup"><span data-stu-id="c250a-129">IDisposable instance members</span></span>

<span data-ttu-id="c250a-130">如果類別將 <xref:System.IDisposable> 實作為實例成員（也就是欄位或屬性），則類別也應該會執行 <xref:System.IDisposable> 。</span><span class="sxs-lookup"><span data-stu-id="c250a-130">If a class holds an <xref:System.IDisposable> implementation as an instance member, either a field or a property, the class should also implement <xref:System.IDisposable>.</span></span> <span data-ttu-id="c250a-131">如需詳細資訊，請參閱[執行 cascade dispose](implementing-dispose.md#cascade-dispose-calls)。</span><span class="sxs-lookup"><span data-stu-id="c250a-131">For more information, see [implement a cascade dispose](implementing-dispose.md#cascade-dispose-calls).</span></span>

## <a name="see-also"></a><span data-ttu-id="c250a-132">請參閱</span><span class="sxs-lookup"><span data-stu-id="c250a-132">See also</span></span>

- [<span data-ttu-id="c250a-133">清除 Unmanaged 資源</span><span class="sxs-lookup"><span data-stu-id="c250a-133">Cleaning up unmanaged resources</span></span>](unmanaged.md)
- [<span data-ttu-id="c250a-134">using 語句（c # 參考）</span><span class="sxs-lookup"><span data-stu-id="c250a-134">using Statement (C# Reference)</span></span>](../../csharp/language-reference/keywords/using-statement.md)
- [<span data-ttu-id="c250a-135">Using 陳述式 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="c250a-135">Using Statement (Visual Basic)</span></span>](../../visual-basic/language-reference/statements/using-statement.md)
