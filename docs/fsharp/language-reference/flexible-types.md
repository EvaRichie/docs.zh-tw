---
title: 彈性類型
description: '瞭解如何使用 F # 彈性類型注釋，這表示參數、變數或值的類型與指定的類型相容。'
ms.date: 08/15/2020
ms.openlocfilehash: 44241ad082cd7f3de9e0cc6a48b8a8946e7b33d3
ms.sourcegitcommit: 8bfeb5930ca48b2ee6053f16082dcaf24d46d221
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2020
ms.locfileid: "88557746"
---
# <a name="flexible-types"></a><span data-ttu-id="d2de4-103">彈性類型</span><span class="sxs-lookup"><span data-stu-id="d2de4-103">Flexible Types</span></span>

<span data-ttu-id="d2de4-104">*彈性類型注釋*指出參數、變數或值的類型與指定的類型相容，其中的相容性是由類別或介面的物件導向階層中的位置所決定。</span><span class="sxs-lookup"><span data-stu-id="d2de4-104">A *flexible type annotation* indicates that a parameter, variable, or value has a type that is compatible with a specified type, where compatibility is determined by position in an object-oriented hierarchy of classes or interfaces.</span></span> <span data-ttu-id="d2de4-105">彈性型別特別適用于自動轉換類型階層中較高的類型時，但您仍然想要讓您的功能使用階層中的任何類型，或任何實介面的型別。</span><span class="sxs-lookup"><span data-stu-id="d2de4-105">Flexible types are useful specifically when the automatic conversion to types higher in the type hierarchy does not occur but you still want to enable your functionality to work with any type in the hierarchy or any type that implements an interface.</span></span>

## <a name="syntax"></a><span data-ttu-id="d2de4-106">語法</span><span class="sxs-lookup"><span data-stu-id="d2de4-106">Syntax</span></span>

```fsharp
#type
```

## <a name="remarks"></a><span data-ttu-id="d2de4-107">備註</span><span class="sxs-lookup"><span data-stu-id="d2de4-107">Remarks</span></span>

<span data-ttu-id="d2de4-108">在先前的語法中， *type* 代表基底類型或介面。</span><span class="sxs-lookup"><span data-stu-id="d2de4-108">In the previous syntax, *type* represents a base type or an interface.</span></span>

<span data-ttu-id="d2de4-109">彈性型別相當於具有條件約束的泛型型別，其條件約束會將允許的類型限制為與基底或介面類別型相容的類型。</span><span class="sxs-lookup"><span data-stu-id="d2de4-109">A flexible type is equivalent to a generic type that has a constraint that limits the allowed types to types that are compatible with the base or interface type.</span></span> <span data-ttu-id="d2de4-110">也就是說，下列兩行程式碼是相等的。</span><span class="sxs-lookup"><span data-stu-id="d2de4-110">That is, the following two lines of code are equivalent.</span></span>

```fsharp
#SomeType

'T when 'T :> SomeType
```

<span data-ttu-id="d2de4-111">彈性類型適用于數種類型的情況。</span><span class="sxs-lookup"><span data-stu-id="d2de4-111">Flexible types are useful in several types of situations.</span></span> <span data-ttu-id="d2de4-112">例如，當您有較高階的函式 (使用函式做為引數) 的函式時，讓函式傳回彈性型別通常會很有用。</span><span class="sxs-lookup"><span data-stu-id="d2de4-112">For example, when you have a higher order function (a function that takes a function as an argument), it is often useful to have the function return a flexible type.</span></span> <span data-ttu-id="d2de4-113">在下列範例中，在中使用具有 sequence 引數的彈性型別，可 `iterate2` 讓更高的 order 函數使用可產生序列、陣列、清單和任何其他可列舉型別的函數。</span><span class="sxs-lookup"><span data-stu-id="d2de4-113">In the following example, the use of a flexible type with a sequence argument in `iterate2` enables the higher order function to work with functions that generate sequences, arrays, lists, and any other enumerable type.</span></span>

<span data-ttu-id="d2de4-114">請考慮下列兩個函式，其中一個會傳回序列，另一個則會傳回彈性型別。</span><span class="sxs-lookup"><span data-stu-id="d2de4-114">Consider the following two functions, one of which returns a sequence, the other of which returns a flexible type.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4101.fs)]

<span data-ttu-id="d2de4-115">另舉一個範例，請考慮採用 [Seq](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-seqmodule.html#concat) 程式庫函數：</span><span class="sxs-lookup"><span data-stu-id="d2de4-115">As another example, consider the [Seq.concat](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-collections-seqmodule.html#concat) library function:</span></span>

```fsharp
val concat: sequences:seq<#seq<'T>> -> seq<'T>
```

<span data-ttu-id="d2de4-116">您可以將下列任何可列舉的序列傳遞給此函式：</span><span class="sxs-lookup"><span data-stu-id="d2de4-116">You can pass any of the following enumerable sequences to this function:</span></span>

- <span data-ttu-id="d2de4-117">清單清單</span><span class="sxs-lookup"><span data-stu-id="d2de4-117">A list of lists</span></span>
- <span data-ttu-id="d2de4-118">陣列清單</span><span class="sxs-lookup"><span data-stu-id="d2de4-118">A list of arrays</span></span>
- <span data-ttu-id="d2de4-119">清單的陣列</span><span class="sxs-lookup"><span data-stu-id="d2de4-119">An array of lists</span></span>
- <span data-ttu-id="d2de4-120">序列的陣列</span><span class="sxs-lookup"><span data-stu-id="d2de4-120">An array of sequences</span></span>
- <span data-ttu-id="d2de4-121">可列舉序列的任何其他組合</span><span class="sxs-lookup"><span data-stu-id="d2de4-121">Any other combination of enumerable sequences</span></span>

<span data-ttu-id="d2de4-122">下列 `Seq.concat` 程式碼會使用來示範您可以使用彈性類型來支援的案例。</span><span class="sxs-lookup"><span data-stu-id="d2de4-122">The following code uses `Seq.concat` to demonstrate the scenarios that you can support by using flexible types.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4102.fs)]

<span data-ttu-id="d2de4-123">輸出如下。</span><span class="sxs-lookup"><span data-stu-id="d2de4-123">The output is as follows.</span></span>

```console
seq [1; 2; 3; 4; ...]
seq [1; 2; 3; 4; ...]
seq [1; 2; 3; 4; ...]
seq [1; 2; 3; 4; ...]
seq [1; 2; 3; 4; ...]
```

<span data-ttu-id="d2de4-124">在 F # 中，如同其他物件導向的語言，有一些內容會將實介面的衍生類型或型別自動轉換成基底類型或介面型別。</span><span class="sxs-lookup"><span data-stu-id="d2de4-124">In F#, as in other object-oriented languages, there are contexts in which derived types or types that implement interfaces are automatically converted to a base type or interface type.</span></span> <span data-ttu-id="d2de4-125">這些自動轉換會在直接引數中進行，但不會在型別位於從屬位置、成為更複雜型別的一部分（例如函式類型的傳回型別），或做為型別引數。</span><span class="sxs-lookup"><span data-stu-id="d2de4-125">These automatic conversions occur in direct arguments, but not when the type is in a subordinate position, as part of a more complex type such as a return type of a function type, or as a type argument.</span></span> <span data-ttu-id="d2de4-126">因此，當您要套用它的型別是更複雜型別的一部分時，彈性型別標記法主要很有用。</span><span class="sxs-lookup"><span data-stu-id="d2de4-126">Thus, the flexible type notation is primarily useful when the type you are applying it to is part of a more complex type.</span></span>

## <a name="see-also"></a><span data-ttu-id="d2de4-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d2de4-127">See also</span></span>

- [<span data-ttu-id="d2de4-128">F # 語言參考</span><span class="sxs-lookup"><span data-stu-id="d2de4-128">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="d2de4-129">泛型</span><span class="sxs-lookup"><span data-stu-id="d2de4-129">Generics</span></span>](./generics/index.md)
