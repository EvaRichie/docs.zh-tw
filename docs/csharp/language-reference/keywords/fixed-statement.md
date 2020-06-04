---
title: fixed 陳述式 - C# 參考
ms.date: 05/10/2018
f1_keywords:
- fixed_CSharpKeyword
- fixed
helpviewer_keywords:
- fixed keyword [C#]
ms.openlocfilehash: d743daca2fa779e300c7e8ab430b1ffff10b434c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401910"
---
# <a name="fixed-statement-c-reference"></a><span data-ttu-id="a8333-102">fixed 陳述式 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="a8333-102">fixed Statement (C# Reference)</span></span>

<span data-ttu-id="a8333-103">`fixed` 陳述式可防止記憶體回收行程重新配置可移動的變數。</span><span class="sxs-lookup"><span data-stu-id="a8333-103">The `fixed` statement prevents the garbage collector from relocating a movable variable.</span></span> <span data-ttu-id="a8333-104">`fixed` 陳述式只能用於[不安全](unsafe.md)的內容中。</span><span class="sxs-lookup"><span data-stu-id="a8333-104">The `fixed` statement is only permitted in an [unsafe](unsafe.md) context.</span></span> <span data-ttu-id="a8333-105">您也可以使用 `fixed` 關鍵字來建立[大小固定的緩衝區](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md)。</span><span class="sxs-lookup"><span data-stu-id="a8333-105">You can also use the `fixed` keyword to create [fixed size buffers](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md).</span></span>

<span data-ttu-id="a8333-106">`fixed` 陳述式會將指標設定為 Managed 變數，並在陳述式執行期間「固定」該變數。</span><span class="sxs-lookup"><span data-stu-id="a8333-106">The `fixed` statement sets a pointer to a managed variable and "pins" that variable during the execution of the statement.</span></span> <span data-ttu-id="a8333-107">可移動之受控變數的指標只適用於 `fixed` 內容。</span><span class="sxs-lookup"><span data-stu-id="a8333-107">Pointers to movable managed variables are useful only in a `fixed` context.</span></span> <span data-ttu-id="a8333-108">如果未使用 `fixed` 內容，記憶體回收可能會意外地重新配置變數。</span><span class="sxs-lookup"><span data-stu-id="a8333-108">Without a `fixed` context, garbage collection could relocate the variables unpredictably.</span></span> <span data-ttu-id="a8333-109">C# 編譯器只能讓您將指標指派給 `fixed` 陳述式中的 Managed 變數。</span><span class="sxs-lookup"><span data-stu-id="a8333-109">The C# compiler only lets you assign a pointer to a managed variable in a `fixed` statement.</span></span>

[!code-csharp[Accessing fixed memory](snippets/FixedKeywordExamples.cs#1)]

<span data-ttu-id="a8333-110">您可以使用陣列、字串、固定大小緩衝區或變數位址，來初始化指標。</span><span class="sxs-lookup"><span data-stu-id="a8333-110">You can initialize a pointer by using an array, a string, a fixed-size buffer, or the address of a variable.</span></span> <span data-ttu-id="a8333-111">下列範例說明如何使用變數位址、陣列和字串：</span><span class="sxs-lookup"><span data-stu-id="a8333-111">The following example illustrates the use of variable addresses, arrays, and strings:</span></span>

[!code-csharp[Initializing fixed size buffers](snippets/FixedKeywordExamples.cs#2)]

<span data-ttu-id="a8333-112">從 C# 7.3 開始，`fixed` 陳述式對陣列、字串、固定大小緩衝區或 unmanaged 變數以外的其它型別都可運作。</span><span class="sxs-lookup"><span data-stu-id="a8333-112">Starting with C# 7.3, the `fixed` statement operates on additional types beyond arrays, strings, fixed size buffers, or unmanaged variables.</span></span> <span data-ttu-id="a8333-113">針對名稱為 `GetPinnableReference` 的方法，可以將任何實作方法的型別加以固定。</span><span class="sxs-lookup"><span data-stu-id="a8333-113">Any type that implements a method named `GetPinnableReference` can be pinned.</span></span> <span data-ttu-id="a8333-114">`GetPinnableReference` 必須傳回 [unmanaged 型別](../builtin-types/unmanaged-types.md)的 `ref` 變數。</span><span class="sxs-lookup"><span data-stu-id="a8333-114">The `GetPinnableReference` must return a `ref` variable of an [unmanaged type](../builtin-types/unmanaged-types.md).</span></span> <span data-ttu-id="a8333-115">.NET Core 2.0 中引入的 .NET 型別 <xref:System.Span%601?displayProperty=nameWithType> 和 <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> 使用此模式，而且可以加以固定。</span><span class="sxs-lookup"><span data-stu-id="a8333-115">The .NET types <xref:System.Span%601?displayProperty=nameWithType> and <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> introduced in .NET Core 2.0 make use of this pattern and can be pinned.</span></span> <span data-ttu-id="a8333-116">下列範例會顯示這一點：</span><span class="sxs-lookup"><span data-stu-id="a8333-116">This is shown in the following example:</span></span>

[!code-csharp[Accessing fixed memory](snippets/FixedKeywordExamples.cs#FixedSpan)]

<span data-ttu-id="a8333-117">如果您正在建立應該參與此模式的型別，請參閱 <xref:System.Span%601.GetPinnableReference?displayProperty=nameWithType> 以取得實作模式的範例。</span><span class="sxs-lookup"><span data-stu-id="a8333-117">If you are creating types that should participate in this pattern, see <xref:System.Span%601.GetPinnableReference?displayProperty=nameWithType> for an example of implementing the pattern.</span></span>

<span data-ttu-id="a8333-118">如果指標的型別全都相同，則可以在一個陳述式中初始化多個指標：</span><span class="sxs-lookup"><span data-stu-id="a8333-118">Multiple pointers can be initialized in one statement if they are all the same type:</span></span>

```csharp
fixed (byte* ps = srcarray, pd = dstarray) {...}
```

<span data-ttu-id="a8333-119">若要初始化不同類型的指標，只要巢狀 `fixed` 陳述式即可，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a8333-119">To initialize pointers of different types, simply nest `fixed` statements, as shown in the following example.</span></span>

[!code-csharp[Initializing multiple pointers](snippets/FixedKeywordExamples.cs#3)]

<span data-ttu-id="a8333-120">執行陳述式中的程式碼之後，任何固定的變數都會取消固定並受限於記憶體回收。</span><span class="sxs-lookup"><span data-stu-id="a8333-120">After the code in the statement is executed, any pinned variables are unpinned and subject to garbage collection.</span></span> <span data-ttu-id="a8333-121">因此，請不要指向 `fixed` 陳述式之外的變數。</span><span class="sxs-lookup"><span data-stu-id="a8333-121">Therefore, do not point to those variables outside the `fixed` statement.</span></span> <span data-ttu-id="a8333-122">`fixed` 陳述式中所宣告變數的範圍會設為該陳述式，使其更加簡單：</span><span class="sxs-lookup"><span data-stu-id="a8333-122">The variables declared in the `fixed` statement are scoped to that statement, making this easier:</span></span>

```csharp
fixed (byte* ps = srcarray, pd = dstarray)
{
   ...
}
// ps and pd are no longer in scope here.
```

<span data-ttu-id="a8333-123">在 `fixed` 陳述式中初始化的指標是唯讀變數。</span><span class="sxs-lookup"><span data-stu-id="a8333-123">Pointers initialized in `fixed` statements are readonly variables.</span></span> <span data-ttu-id="a8333-124">如果您要修改指標值，則必須宣告第二個指標變數並予以修改。</span><span class="sxs-lookup"><span data-stu-id="a8333-124">If you want to modify the pointer value, you must declare a second pointer variable, and modify that.</span></span> <span data-ttu-id="a8333-125">在 `fixed` 陳述式中宣告的變數無法修改：</span><span class="sxs-lookup"><span data-stu-id="a8333-125">The variable declared in the `fixed` statement cannot be modified:</span></span>

```csharp
fixed (byte* ps = srcarray, pd = dstarray)
{
    byte* pSourceCopy = ps;
    pSourceCopy++; // point to the next element.
    ps++; // invalid: cannot modify ps, as it is declared in the fixed statement.
}
```

<span data-ttu-id="a8333-126">您可以配置堆疊上的記憶體，此處不受記憶體回收限制，因此不需要釘選。</span><span class="sxs-lookup"><span data-stu-id="a8333-126">You can allocate memory on the stack, where it is not subject to garbage collection and therefore does not need to be pinned.</span></span> <span data-ttu-id="a8333-127">若要這麼做，請使用[ `stackalloc` 運算式](../operators/stackalloc.md)。</span><span class="sxs-lookup"><span data-stu-id="a8333-127">To do that, use a [`stackalloc` expression](../operators/stackalloc.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="a8333-128">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="a8333-128">C# language specification</span></span>

<span data-ttu-id="a8333-129">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的 [fixed 陳述式](~/_csharplang/spec/unsafe-code.md#the-fixed-statement)一節。</span><span class="sxs-lookup"><span data-stu-id="a8333-129">For more information, see [The fixed statement](~/_csharplang/spec/unsafe-code.md#the-fixed-statement) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="a8333-130">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a8333-130">See also</span></span>

- [<span data-ttu-id="a8333-131">C # 參考</span><span class="sxs-lookup"><span data-stu-id="a8333-131">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="a8333-132">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="a8333-132">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="a8333-133">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="a8333-133">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="a8333-134">不安全</span><span class="sxs-lookup"><span data-stu-id="a8333-134">unsafe</span></span>](unsafe.md)
- [<span data-ttu-id="a8333-135">指標類型</span><span class="sxs-lookup"><span data-stu-id="a8333-135">Pointer types</span></span>](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [<span data-ttu-id="a8333-136">固定大小緩衝區</span><span class="sxs-lookup"><span data-stu-id="a8333-136">Fixed Size Buffers</span></span>](../../programming-guide/unsafe-code-pointers/fixed-size-buffers.md)
