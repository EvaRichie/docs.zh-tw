---
title: 陣列
description: '瞭解如何在 F # 程式設計語言中建立和使用陣列。'
ms.date: 05/16/2016
ms.openlocfilehash: f95ca3274e098fda044973a48205cb591ec30b27
ms.sourcegitcommit: c37e8d4642fef647ebab0e1c618ecc29ddfe2a0f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87855604"
---
# <a name="arrays"></a><span data-ttu-id="c4b18-103">陣列</span><span class="sxs-lookup"><span data-stu-id="c4b18-103">Arrays</span></span>

<span data-ttu-id="c4b18-104">陣列是固定大小、以零為基底、可變動的連續資料元素集合，這些專案全都屬於相同的類型。</span><span class="sxs-lookup"><span data-stu-id="c4b18-104">Arrays are fixed-size, zero-based, mutable collections of consecutive data elements that are all of the same type.</span></span>

> [!NOTE]
> <span data-ttu-id="c4b18-105">F # 的 docs.microsoft.com API 參考不完整。</span><span class="sxs-lookup"><span data-stu-id="c4b18-105">The docs.microsoft.com API reference for F# is not complete.</span></span> <span data-ttu-id="c4b18-106">如果您遇到任何中斷的連結，請改為參考[F # 核心程式庫檔](https://fsharp.github.io/fsharp-core-docs/)。</span><span class="sxs-lookup"><span data-stu-id="c4b18-106">If you encounter any broken links, reference [F# Core Library Documentation](https://fsharp.github.io/fsharp-core-docs/) instead.</span></span>

## <a name="create-arrays"></a><span data-ttu-id="c4b18-107">建立陣列</span><span class="sxs-lookup"><span data-stu-id="c4b18-107">Create arrays</span></span>

<span data-ttu-id="c4b18-108">您可以透過數種方式來建立陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-108">You can create arrays in several ways.</span></span> <span data-ttu-id="c4b18-109">您可以藉由列出介於和之間的連續值，並以分號分隔，來建立小型陣列 `[|` `|]` ，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-109">You can create a small array by listing consecutive values between `[|` and `|]` and separated by semicolons, as shown in the following examples.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet1.fs)]

<span data-ttu-id="c4b18-110">您也可以將每個元素放在不同的行上，在此情況下，分號分隔符號是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="c4b18-110">You can also put each element on a separate line, in which case the semicolon separator is optional.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet2.fs)]

<span data-ttu-id="c4b18-111">陣列元素的類型是從使用的常值推斷而來，且必須一致。</span><span class="sxs-lookup"><span data-stu-id="c4b18-111">The type of the array elements is inferred from the literals used and must be consistent.</span></span> <span data-ttu-id="c4b18-112">下列程式碼會造成錯誤，因為1.0 是 float，而2和3是整數。</span><span class="sxs-lookup"><span data-stu-id="c4b18-112">The following code causes an error because 1.0 is a float and 2 and 3 are integers.</span></span>

```fsharp
// Causes an error.
// let array2 = [| 1.0; 2; 3 |]
```

<span data-ttu-id="c4b18-113">您也可以使用順序運算式來建立陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-113">You can also use sequence expressions to create arrays.</span></span> <span data-ttu-id="c4b18-114">以下範例會建立從1到10的整數的平方陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-114">Following is an example that creates an array of squares of integers from 1 to 10.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet3.fs)]

<span data-ttu-id="c4b18-115">若要建立陣列，其中所有元素都初始化為零，請使用 `Array.zeroCreate` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-115">To create an array in which all the elements are initialized to zero, use `Array.zeroCreate`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet4.fs)]

## <a name="access-elements"></a><span data-ttu-id="c4b18-116">Access 元素</span><span class="sxs-lookup"><span data-stu-id="c4b18-116">Access elements</span></span>

<span data-ttu-id="c4b18-117">您可以使用點運算子 (`.`) 和方括弧 (和) 來存取陣列 `[` 元素 `]` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-117">You can access array elements by using a dot operator (`.`) and brackets (`[` and `]`).</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet5.fs)]

<span data-ttu-id="c4b18-118">陣列索引從0開始。</span><span class="sxs-lookup"><span data-stu-id="c4b18-118">Array indexes start at 0.</span></span>

<span data-ttu-id="c4b18-119">您也可以使用配量標記法來存取陣列元素，這可讓您指定陣列的子範圍。</span><span class="sxs-lookup"><span data-stu-id="c4b18-119">You can also access array elements by using slice notation, which enables you to specify a subrange of the array.</span></span> <span data-ttu-id="c4b18-120">配量標記法的範例如下。</span><span class="sxs-lookup"><span data-stu-id="c4b18-120">Examples of slice notation follow.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet51.fs)]

<span data-ttu-id="c4b18-121">當使用配量標記法時，會建立陣列的新複本。</span><span class="sxs-lookup"><span data-stu-id="c4b18-121">When slice notation is used, a new copy of the array is created.</span></span>

## <a name="array-types-and-modules"></a><span data-ttu-id="c4b18-122">陣列類型和模組</span><span class="sxs-lookup"><span data-stu-id="c4b18-122">Array types and modules</span></span>

<span data-ttu-id="c4b18-123">所有 F # 陣列的類型都是 .NET Framework 類型 <xref:System.Array?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-123">The type of all F# arrays is the .NET Framework type <xref:System.Array?displayProperty=nameWithType>.</span></span> <span data-ttu-id="c4b18-124">因此，F # 陣列支援中提供的所有功能 <xref:System.Array?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-124">Therefore, F# arrays support all the functionality available in <xref:System.Array?displayProperty=nameWithType>.</span></span>

<span data-ttu-id="c4b18-125">Library 模組 [`Microsoft.FSharp.Collections.Array`](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1) 支援一維陣列上的作業。</span><span class="sxs-lookup"><span data-stu-id="c4b18-125">The library module [`Microsoft.FSharp.Collections.Array`](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1) supports operations on one-dimensional arrays.</span></span> <span data-ttu-id="c4b18-126">模組 `Array2D` 、 `Array3D` 和包含的函式， `Array4D` 分別支援兩個、三個和四個維度之陣列的作業。</span><span class="sxs-lookup"><span data-stu-id="c4b18-126">The modules `Array2D`, `Array3D`, and `Array4D` contain functions that support operations on arrays of two, three, and four dimensions, respectively.</span></span> <span data-ttu-id="c4b18-127">您可以使用，建立大於四的次序陣列 <xref:System.Array?displayProperty=nameWithType> 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-127">You can create arrays of rank greater than four by using <xref:System.Array?displayProperty=nameWithType>.</span></span>

### <a name="simple-functions"></a><span data-ttu-id="c4b18-128">簡單函式</span><span class="sxs-lookup"><span data-stu-id="c4b18-128">Simple functions</span></span>

<span data-ttu-id="c4b18-129">[`Array.get`](https://msdn.microsoft.com/library/dd93e85d-7e80-4d76-8de0-b6d45bcf07bc)取得元素。</span><span class="sxs-lookup"><span data-stu-id="c4b18-129">[`Array.get`](https://msdn.microsoft.com/library/dd93e85d-7e80-4d76-8de0-b6d45bcf07bc) gets an element.</span></span> <span data-ttu-id="c4b18-130">[`Array.length`](https://msdn.microsoft.com/library/0d775b6a-4a8f-4bd1-83e5-843b3251725f)提供陣列的長度。</span><span class="sxs-lookup"><span data-stu-id="c4b18-130">[`Array.length`](https://msdn.microsoft.com/library/0d775b6a-4a8f-4bd1-83e5-843b3251725f) gives the length of an array.</span></span> <span data-ttu-id="c4b18-131">[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790)將元素設定為指定的值。</span><span class="sxs-lookup"><span data-stu-id="c4b18-131">[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790) sets an element to a specified value.</span></span> <span data-ttu-id="c4b18-132">下列程式碼範例說明如何使用這些函數。</span><span class="sxs-lookup"><span data-stu-id="c4b18-132">The following code example illustrates the use of these functions.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet9.fs)]

<span data-ttu-id="c4b18-133">輸出如下。</span><span class="sxs-lookup"><span data-stu-id="c4b18-133">The output is as follows.</span></span>

```console
0 1 2 3 4 5 6 7 8 9
```

### <a name="functions-that-create-arrays"></a><span data-ttu-id="c4b18-134">建立陣列的函式</span><span class="sxs-lookup"><span data-stu-id="c4b18-134">Functions that create arrays</span></span>

<span data-ttu-id="c4b18-135">有數個函式會建立陣列，而不需要現有的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-135">Several functions create arrays without requiring an existing array.</span></span> <span data-ttu-id="c4b18-136">[`Array.empty`](https://msdn.microsoft.com/library/c3694b92-1c16-4c54-9bf2-fe398fadce32)建立不包含任何元素的新陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-136">[`Array.empty`](https://msdn.microsoft.com/library/c3694b92-1c16-4c54-9bf2-fe398fadce32) creates a new array that does not contain any elements.</span></span> <span data-ttu-id="c4b18-137">[`Array.create`](https://msdn.microsoft.com/library/e848c8d6-1142-4080-9727-8dacc26066be)建立指定大小的陣列，並將所有元素設定為提供的值。</span><span class="sxs-lookup"><span data-stu-id="c4b18-137">[`Array.create`](https://msdn.microsoft.com/library/e848c8d6-1142-4080-9727-8dacc26066be) creates an array of a specified size and sets all the elements to provided values.</span></span> <span data-ttu-id="c4b18-138">[`Array.init`](https://msdn.microsoft.com/library/ee898089-63b0-40aa-910c-5ae7e32f6665)建立陣列，並指定要產生元素的維度和函式。</span><span class="sxs-lookup"><span data-stu-id="c4b18-138">[`Array.init`](https://msdn.microsoft.com/library/ee898089-63b0-40aa-910c-5ae7e32f6665) creates an array, given a dimension and a function to generate the elements.</span></span> <span data-ttu-id="c4b18-139">[`Array.zeroCreate`](https://msdn.microsoft.com/library/fa5b8e7a-1b5b-411c-8622-b58d7a14d3b2)建立陣列，其中所有的元素都會初始化為數組類型的零值。</span><span class="sxs-lookup"><span data-stu-id="c4b18-139">[`Array.zeroCreate`](https://msdn.microsoft.com/library/fa5b8e7a-1b5b-411c-8622-b58d7a14d3b2) creates an array in which all the elements are initialized to the zero value for the array's type.</span></span> <span data-ttu-id="c4b18-140">下列程式碼會示範這些函數。</span><span class="sxs-lookup"><span data-stu-id="c4b18-140">The following code demonstrates these functions.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet91.fs)]

<span data-ttu-id="c4b18-141">輸出如下。</span><span class="sxs-lookup"><span data-stu-id="c4b18-141">The output is as follows.</span></span>

```console
Length of empty array: 0
Area of floats set to 5.0: [|5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0|]
Array of squares: [|0; 1; 4; 9; 16; 25; 36; 49; 64; 81|]
```

<span data-ttu-id="c4b18-142">[`Array.copy`](https://msdn.microsoft.com/library/9d0202f1-1ea0-475e-9d66-4f8ccc3c5b5f)建立新的陣列，其中包含從現有陣列複製的元素。</span><span class="sxs-lookup"><span data-stu-id="c4b18-142">[`Array.copy`](https://msdn.microsoft.com/library/9d0202f1-1ea0-475e-9d66-4f8ccc3c5b5f) creates a new array that contains elements that are copied from an existing array.</span></span> <span data-ttu-id="c4b18-143">請注意，複製是淺層複製，這表示如果元素類型是參考型別，則只會複製參考，而不會複製基礎物件。</span><span class="sxs-lookup"><span data-stu-id="c4b18-143">Note that the copy is a shallow copy, which means that if the element type is a reference type, only the reference is copied, not the underlying object.</span></span> <span data-ttu-id="c4b18-144">下列程式碼範例會說明這點。</span><span class="sxs-lookup"><span data-stu-id="c4b18-144">The following code example illustrates this.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet11.fs)]

<span data-ttu-id="c4b18-145">上述程式碼的輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="c4b18-145">The output of the preceding code is as follows:</span></span>

```console
[|Test1; Test2; |]
[|; Test2; |]
```

<span data-ttu-id="c4b18-146">此字串 `Test1` 只會出現在第一個陣列中，因為建立新專案的作業會覆寫中的參考， `firstArray` 但不會影響仍然存在於中之空字串的原始參考 `secondArray` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-146">The string `Test1` appears only in the first array because the operation of creating a new element overwrites the reference in `firstArray` but does not affect the original reference to an empty string that is still present in `secondArray`.</span></span> <span data-ttu-id="c4b18-147">此字串 `Test2` 會出現在這兩個數組中，因為類型的作業 `Insert` <xref:System.Text.StringBuilder?displayProperty=nameWithType> 會影響 <xref:System.Text.StringBuilder?displayProperty=nameWithType> 在這兩個數組中所參考的基礎物件。</span><span class="sxs-lookup"><span data-stu-id="c4b18-147">The string `Test2` appears in both arrays because the `Insert` operation on the <xref:System.Text.StringBuilder?displayProperty=nameWithType> type affects the underlying <xref:System.Text.StringBuilder?displayProperty=nameWithType> object, which is referenced in both arrays.</span></span>

<span data-ttu-id="c4b18-148">[`Array.sub`](https://msdn.microsoft.com/library/40fb12ba-41d7-4ef0-b33a-56727deeef9d)從陣列的子範圍產生新的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-148">[`Array.sub`](https://msdn.microsoft.com/library/40fb12ba-41d7-4ef0-b33a-56727deeef9d) generates a new array from a subrange of an array.</span></span> <span data-ttu-id="c4b18-149">您可以藉由提供起始索引和長度來指定子範圍。</span><span class="sxs-lookup"><span data-stu-id="c4b18-149">You specify the subrange by providing the starting index and the length.</span></span> <span data-ttu-id="c4b18-150">下列程式碼示範 `Array.sub` 的用法。</span><span class="sxs-lookup"><span data-stu-id="c4b18-150">The following code demonstrates the use of `Array.sub`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet12.fs)]

<span data-ttu-id="c4b18-151">輸出顯示子陣列從專案5開始，且包含10個元素。</span><span class="sxs-lookup"><span data-stu-id="c4b18-151">The output shows that the subarray starts at element 5 and contains 10 elements.</span></span>

```console
[|5; 6; 7; 8; 9; 10; 11; 12; 13; 14|]
```

<span data-ttu-id="c4b18-152">[`Array.append`](https://msdn.microsoft.com/library/08836310-5036-4474-b9a2-2c73e2293911)結合兩個現有的陣列，以建立新的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-152">[`Array.append`](https://msdn.microsoft.com/library/08836310-5036-4474-b9a2-2c73e2293911) creates a new array by combining two existing arrays.</span></span>

<span data-ttu-id="c4b18-153">下列程式碼示範**陣列. append**。</span><span class="sxs-lookup"><span data-stu-id="c4b18-153">The following code demonstrates **Array.append**.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet13.fs)]

<span data-ttu-id="c4b18-154">上述程式碼的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-154">The output of the preceding code is as follows.</span></span>

```console
[|1; 2; 3; 4; 5; 6|]
```

<span data-ttu-id="c4b18-155">[`Array.choose`](https://msdn.microsoft.com/library/f5c8a5e2-637f-44d4-b35c-be96a6618b09)選取要包含在新陣列中之陣列的元素。</span><span class="sxs-lookup"><span data-stu-id="c4b18-155">[`Array.choose`](https://msdn.microsoft.com/library/f5c8a5e2-637f-44d4-b35c-be96a6618b09) selects elements of an array to include in a new array.</span></span> <span data-ttu-id="c4b18-156">下列程式碼示範 `Array.choose` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-156">The following code demonstrates `Array.choose`.</span></span> <span data-ttu-id="c4b18-157">請注意，陣列的元素類型不一定要符合選項類型中所傳回值的類型。</span><span class="sxs-lookup"><span data-stu-id="c4b18-157">Note that the element type of the array does not have to match the type of the value returned in the option type.</span></span> <span data-ttu-id="c4b18-158">在此範例中，專案類型為， `int` 而選項是多項式函式的結果（ `elem*elem - 1` 做為浮點數）。</span><span class="sxs-lookup"><span data-stu-id="c4b18-158">In this example, the element type is `int` and the option is the result of a polynomial function, `elem*elem - 1`, as a floating point number.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet14.fs)]

<span data-ttu-id="c4b18-159">上述程式碼的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-159">The output of the preceding code is as follows.</span></span>

```console
[|3.0; 15.0; 35.0; 63.0; 99.0|]
```

<span data-ttu-id="c4b18-160">[`Array.collect`](https://msdn.microsoft.com/library/c3b60c3b-9455-48c9-bc2b-e88f0434342a)在現有陣列的每個陣列元素上執行指定的函式，然後收集函數所產生的專案，並將它們結合到新的陣列中。</span><span class="sxs-lookup"><span data-stu-id="c4b18-160">[`Array.collect`](https://msdn.microsoft.com/library/c3b60c3b-9455-48c9-bc2b-e88f0434342a) runs a specified function on each array element of an existing array and then collects the elements generated by the function and combines them into a new array.</span></span> <span data-ttu-id="c4b18-161">下列程式碼示範 `Array.collect` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-161">The following code demonstrates `Array.collect`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet15.fs)]

<span data-ttu-id="c4b18-162">上述程式碼的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-162">The output of the preceding code is as follows.</span></span>

```console
[|0; 1; 0; 1; 2; 3; 4; 5; 0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10|]
```

<span data-ttu-id="c4b18-163">[`Array.concat`](https://msdn.microsoft.com/library/f7219b79-1ec8-4a25-96b1-edbedb358302)採用一連串的陣列，並將它們結合成單一陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-163">[`Array.concat`](https://msdn.microsoft.com/library/f7219b79-1ec8-4a25-96b1-edbedb358302) takes a sequence of arrays and combines them into a single array.</span></span> <span data-ttu-id="c4b18-164">下列程式碼示範 `Array.concat` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-164">The following code demonstrates `Array.concat`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet16.fs)]

<span data-ttu-id="c4b18-165">上述程式碼的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-165">The output of the preceding code is as follows.</span></span>

```console
[|(1, 1, 1); (1, 2, 2); (1, 3, 3); (2, 1, 2); (2, 2, 4); (2, 3, 6); (3, 1, 3);
(3, 2, 6); (3, 3, 9)|]
```

<span data-ttu-id="c4b18-166">[`Array.filter`](https://msdn.microsoft.com/library/b885b214-47fc-4639-9664-b8c183a39ede)採用布林條件函式，並產生新的陣列，其中只包含來自輸入陣列的條件為 true 的元素。</span><span class="sxs-lookup"><span data-stu-id="c4b18-166">[`Array.filter`](https://msdn.microsoft.com/library/b885b214-47fc-4639-9664-b8c183a39ede) takes a Boolean condition function and generates a new array that contains only those elements from the input array for which the condition is true.</span></span> <span data-ttu-id="c4b18-167">下列程式碼示範 `Array.filter` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-167">The following code demonstrates `Array.filter`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet17.fs)]

<span data-ttu-id="c4b18-168">上述程式碼的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-168">The output of the preceding code is as follows.</span></span>

```console
[|2; 4; 6; 8; 10|]
```

<span data-ttu-id="c4b18-169">[`Array.rev`](https://msdn.microsoft.com/library/1bbf822c-763b-4794-af21-97d2e48ef709)藉由反轉現有陣列的順序，產生新的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-169">[`Array.rev`](https://msdn.microsoft.com/library/1bbf822c-763b-4794-af21-97d2e48ef709) generates a new array by reversing the order of an existing array.</span></span> <span data-ttu-id="c4b18-170">下列程式碼示範 `Array.rev` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-170">The following code demonstrates `Array.rev`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet18.fs)]

<span data-ttu-id="c4b18-171">上述程式碼的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-171">The output of the preceding code is as follows.</span></span>

```console
"Hello world!"
```

<span data-ttu-id="c4b18-172">您可以使用管線運算子 () ，輕鬆地結合陣列模組中的函數，以轉換陣列 `|>` ，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-172">You can easily combine functions in the array module that transform arrays by using the pipeline operator (`|>`), as shown in the following example.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet19.fs)]

<span data-ttu-id="c4b18-173">輸出為</span><span class="sxs-lookup"><span data-stu-id="c4b18-173">The output is</span></span>

```console
[|100; 36; 16; 4|]
```

### <a name="multidimensional-arrays"></a><span data-ttu-id="c4b18-174">多維陣列</span><span class="sxs-lookup"><span data-stu-id="c4b18-174">Multidimensional arrays</span></span>

<span data-ttu-id="c4b18-175">多維陣列可以建立，但是沒有寫入多維陣列常值的語法。</span><span class="sxs-lookup"><span data-stu-id="c4b18-175">A multidimensional array can be created, but there is no syntax for writing a multidimensional array literal.</span></span> <span data-ttu-id="c4b18-176">使用運算子 [`array2D`](https://msdn.microsoft.com/library/1d52503d-2990-49fc-8fd3-6b0e508aa236) ，從陣列元素的序列順序建立陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-176">Use the operator [`array2D`](https://msdn.microsoft.com/library/1d52503d-2990-49fc-8fd3-6b0e508aa236) to create an array from a sequence of sequences of array elements.</span></span> <span data-ttu-id="c4b18-177">序列可以是陣列或清單常值。</span><span class="sxs-lookup"><span data-stu-id="c4b18-177">The sequences can be array or list literals.</span></span> <span data-ttu-id="c4b18-178">例如，下列程式碼會建立二維陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-178">For example, the following code creates a two-dimensional array.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet20.fs)]

<span data-ttu-id="c4b18-179">您也可以使用函式 [`Array2D.init`](https://msdn.microsoft.com/library/9de07e95-bc21-4927-b5b4-08fdec882c7b) 來初始化兩個維度的陣列，而類似的函數適用于三和四個維度的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-179">You can also use the function [`Array2D.init`](https://msdn.microsoft.com/library/9de07e95-bc21-4927-b5b4-08fdec882c7b) to initialize arrays of two dimensions, and similar functions are available for arrays of three and four dimensions.</span></span> <span data-ttu-id="c4b18-180">這些函式會採用用來建立元素的函式。</span><span class="sxs-lookup"><span data-stu-id="c4b18-180">These functions take a function that is used to create the elements.</span></span> <span data-ttu-id="c4b18-181">若要建立二維陣列，其中包含設定為初始值的專案，而不是指定函式，請使用函式 [`Array2D.create`](https://msdn.microsoft.com/library/36c9d980-b241-4a20-bc64-bcfa0205d804) ，此函數也適用于最多四個維度的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-181">To create a two-dimensional array that contains elements set to an initial value instead of specifying a function, use the [`Array2D.create`](https://msdn.microsoft.com/library/36c9d980-b241-4a20-bc64-bcfa0205d804) function, which is also available for arrays up to four dimensions.</span></span> <span data-ttu-id="c4b18-182">下列程式碼範例會先示範如何建立陣列陣列，其中包含所需的元素，然後使用 `Array2D.init` 來產生所需的二維陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-182">The following code example first shows how to create an array of arrays that contain the desired elements, and then uses `Array2D.init` to generate the desired two-dimensional array.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet21.fs)]

<span data-ttu-id="c4b18-183">陣列的索引和配量語法支援最高至等級4的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-183">Array indexing and slicing syntax is supported for arrays up to rank 4.</span></span> <span data-ttu-id="c4b18-184">當您指定多個維度中的索引時，您可以使用逗號來分隔索引，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-184">When you specify an index in multiple dimensions, you use commas to separate the indexes, as illustrated in the following code example.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet22.fs)]

<span data-ttu-id="c4b18-185">二維陣列的類型會寫出為 (例如，、 `<type>[,]` `int[,]` `double[,]`) ，而三維陣列的類型則會寫入為 `<type>[,,]` ，而對於較高維度的陣列則為。</span><span class="sxs-lookup"><span data-stu-id="c4b18-185">The type of a two-dimensional array is written out as `<type>[,]` (for example, `int[,]`, `double[,]`), and the type of a three-dimensional array is written as `<type>[,,]`, and so on for arrays of higher dimensions.</span></span>

<span data-ttu-id="c4b18-186">只有一維陣列可用的函數子集也適用于多維陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-186">Only a subset of the functions available for one-dimensional arrays is also available for multidimensional arrays.</span></span> <span data-ttu-id="c4b18-187">如需詳細資訊，請參閱 [`Collections.Array Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array-module-%5bfsharp%5d) 、、 [`Collections.Array2D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array2d-module-%5bfsharp%5d) [`Collections.Array3D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array3d-module-%5bfsharp%5d) 和 [`Collections.Array4D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array4d-module-%5bfsharp%5d) 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-187">For more information, see [`Collections.Array Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array-module-%5bfsharp%5d), [`Collections.Array2D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array2d-module-%5bfsharp%5d), [`Collections.Array3D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array3d-module-%5bfsharp%5d), and [`Collections.Array4D Module`](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array4d-module-%5bfsharp%5d).</span></span>

### <a name="array-slicing-and-multidimensional-arrays"></a><span data-ttu-id="c4b18-188">陣列切割和多維陣列</span><span class="sxs-lookup"><span data-stu-id="c4b18-188">Array slicing and multidimensional arrays</span></span>

<span data-ttu-id="c4b18-189">在 (矩陣) 的二維陣列中，您可以藉由指定範圍，並使用萬用字元 (`*`) 字元來指定整個資料列或資料行，來將子矩陣解壓縮。</span><span class="sxs-lookup"><span data-stu-id="c4b18-189">In a two-dimensional array (a matrix), you can extract a sub-matrix by specifying ranges and using a wildcard (`*`) character to specify whole rows or columns.</span></span>

```fsharp
// Get rows 1 to N from an NxM matrix (returns a matrix):
matrix.[1.., *]

// Get rows 1 to 3 from a matrix (returns a matrix):
matrix.[1..3, *]

// Get columns 1 to 3 from a matrix (returns a matrix):
matrix.[*, 1..3]

// Get a 3x3 submatrix:
matrix.[1..3, 1..3]
```

<span data-ttu-id="c4b18-190">從 F # 3.1，您可以將多維陣列分解成相同或較低維度的 subarrays。</span><span class="sxs-lookup"><span data-stu-id="c4b18-190">As of F# 3.1, you can decompose a multidimensional array into subarrays of the same or lower dimension.</span></span> <span data-ttu-id="c4b18-191">例如，您可以藉由指定單一資料列或資料行，從矩陣取得向量。</span><span class="sxs-lookup"><span data-stu-id="c4b18-191">For example, you can obtain a vector from a matrix by specifying a single row or column.</span></span>

```fsharp
// Get row 3 from a matrix as a vector:
matrix.[3, *]

// Get column 3 from a matrix as a vector:
matrix.[*, 3]
```

<span data-ttu-id="c4b18-192">您可以針對實作為元素存取運算子和多載方法的類型使用此切割語法 `GetSlice` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-192">You can use this slicing syntax for types that implement the element access operators and overloaded `GetSlice` methods.</span></span> <span data-ttu-id="c4b18-193">例如，下列程式碼會建立包裝 F # 2D 陣列的矩陣類型、執行專案屬性以提供陣列索引編制的支援，以及執行的三個版本 `GetSlice` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-193">For example, the following code creates a Matrix type that wraps the F# 2D array, implements an Item property to provide support for array indexing, and implements three versions of `GetSlice`.</span></span> <span data-ttu-id="c4b18-194">如果您可以使用此程式碼當做矩陣類型的範本，則可以使用本節所述的所有切割作業。</span><span class="sxs-lookup"><span data-stu-id="c4b18-194">If you can use this code as a template for your matrix types, you can use all the slicing operations that this section describes.</span></span>

```fsharp
type Matrix<'T>(N: int, M: int) =
    let internalArray = Array2D.zeroCreate<'T> N M

    member this.Item
        with get(a: int, b: int) = internalArray.[a, b]
        and set(a: int, b: int) (value:'T) = internalArray.[a, b] <- value

    member this.GetSlice(rowStart: int option, rowFinish : int option, colStart: int option, colFinish : int option) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[rowStart..rowFinish, colStart..colFinish]

    member this.GetSlice(row: int, colStart: int option, colFinish: int option) =
        let colStart =
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish =
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[row, colStart..colFinish]

    member this.GetSlice(rowStart: int option, rowFinish: int option, col: int) =
        let rowStart =
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        internalArray.[rowStart..rowFinish, col]

module test =
    let generateTestMatrix x y =
        let matrix = new Matrix<float>(3, 3)
        for i in 0..2 do
            for j in 0..2 do
                matrix.[i, j] <- float(i) * x - float(j) * y
        matrix

    let test1 = generateTestMatrix 2.3 1.1
    let submatrix = test1.[0..1, 0..1]
    printfn "%A" submatrix

    let firstRow = test1.[0,*]
    let secondRow = test1.[1,*]
    let firstCol = test1.[*,0]
    printfn "%A" firstCol
```

### <a name="boolean-functions-on-arrays"></a><span data-ttu-id="c4b18-195">陣列上的布耳函數</span><span class="sxs-lookup"><span data-stu-id="c4b18-195">Boolean functions on arrays</span></span>

<span data-ttu-id="c4b18-196">[`Array.exists`](https://msdn.microsoft.com/library/8e47ad6c-c065-4876-8cb4-ec960ec3e5c9) [`Array.exists2`](https://msdn.microsoft.com/library/2e384a6a-f99d-4e23-b677-250ffbc1dd8e) 一或兩個數組中的函式和測試專案分別為。</span><span class="sxs-lookup"><span data-stu-id="c4b18-196">The functions [`Array.exists`](https://msdn.microsoft.com/library/8e47ad6c-c065-4876-8cb4-ec960ec3e5c9) and [`Array.exists2`](https://msdn.microsoft.com/library/2e384a6a-f99d-4e23-b677-250ffbc1dd8e) test elements in either one or two arrays, respectively.</span></span> <span data-ttu-id="c4b18-197">`true`如果符合條件的) 有元素 (或元素組，則這些函式會接受測試函數並傳回 `Array.exists2` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-197">These functions take a test function and return `true` if there is an element (or element pair for `Array.exists2`) that satisfies the condition.</span></span>

<span data-ttu-id="c4b18-198">下列程式碼示範和的用法 `Array.exists` `Array.exists2` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-198">The following code demonstrates the use of `Array.exists` and `Array.exists2`.</span></span> <span data-ttu-id="c4b18-199">在這些範例中，會藉由只套用其中一個引數（在這些情況下為函數引數）來建立新的函式。</span><span class="sxs-lookup"><span data-stu-id="c4b18-199">In these examples, new functions are created by applying only one of the arguments, in these cases, the function argument.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet23.fs)]

<span data-ttu-id="c4b18-200">上述程式碼的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-200">The output of the preceding code is as follows.</span></span>

```console
true
false
false
true
```

<span data-ttu-id="c4b18-201">同樣地，函 [`Array.forall`](https://msdn.microsoft.com/library/d88f2cd0-fa7f-45cf-ac15-31eae9086cc4) 式會測試陣列，以判斷每個元素是否符合布林條件。</span><span class="sxs-lookup"><span data-stu-id="c4b18-201">Similarly, the function [`Array.forall`](https://msdn.microsoft.com/library/d88f2cd0-fa7f-45cf-ac15-31eae9086cc4) tests an array to determine whether every element satisfies a Boolean condition.</span></span> <span data-ttu-id="c4b18-202">此變化 [`Array.forall2`](https://msdn.microsoft.com/library/c68f61a1-030c-4024-b705-c4768b6c96b9) 會使用包含兩個相等長度陣列之元素的布林函式，來執行相同的工作。</span><span class="sxs-lookup"><span data-stu-id="c4b18-202">The variation [`Array.forall2`](https://msdn.microsoft.com/library/c68f61a1-030c-4024-b705-c4768b6c96b9) does the same thing by using a Boolean function that involves elements of two arrays of equal length.</span></span> <span data-ttu-id="c4b18-203">下列程式碼說明這些函式的用法。</span><span class="sxs-lookup"><span data-stu-id="c4b18-203">The following code illustrates the use of these functions.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet24.fs)]

<span data-ttu-id="c4b18-204">這些範例的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="c4b18-204">The output for these examples is as follows.</span></span>

```console
false
true
true
false
```

### <a name="search-arrays"></a><span data-ttu-id="c4b18-205">搜尋陣列</span><span class="sxs-lookup"><span data-stu-id="c4b18-205">Search arrays</span></span>

<span data-ttu-id="c4b18-206">[`Array.find`](https://msdn.microsoft.com/library/db6d920a-de19-4520-85a4-d83de77c1b33)採用布耳函數，並傳回函式傳回的第一個專案 `true` ， <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> 如果找不到符合條件的專案，則會引發。</span><span class="sxs-lookup"><span data-stu-id="c4b18-206">[`Array.find`](https://msdn.microsoft.com/library/db6d920a-de19-4520-85a4-d83de77c1b33) takes a Boolean function and returns the first element for which the function returns `true`, or raises a <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> if no element that satisfies the condition is found.</span></span> <span data-ttu-id="c4b18-207">[`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f)類似，但它會傳回專案的 `Array.find` 索引，而不是元素本身。</span><span class="sxs-lookup"><span data-stu-id="c4b18-207">[`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) is like `Array.find`, except that it returns the index of the element instead of the element itself.</span></span>

<span data-ttu-id="c4b18-208">下列 `Array.find` 程式碼會使用和 `Array.findIndex` 來尋找同時為完美方形和完美 cube 的數位。</span><span class="sxs-lookup"><span data-stu-id="c4b18-208">The following code uses `Array.find` and `Array.findIndex` to locate a number that is both a perfect square and perfect cube.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet25.fs)]

<span data-ttu-id="c4b18-209">輸出如下。</span><span class="sxs-lookup"><span data-stu-id="c4b18-209">The output is as follows.</span></span>

```console
The first element that is both a square and a cube is 64 and its index is 62.
```

<span data-ttu-id="c4b18-210">[`Array.tryFind`](https://msdn.microsoft.com/library/7bd65f6c-df77-454c-ac3a-6f7baecec9d9)類似于 `Array.find` ，但它的結果是選項類型， `None` 如果找不到任何元素，則會傳回。</span><span class="sxs-lookup"><span data-stu-id="c4b18-210">[`Array.tryFind`](https://msdn.microsoft.com/library/7bd65f6c-df77-454c-ac3a-6f7baecec9d9) is like `Array.find`, except that its result is an option type, and it returns `None` if no element is found.</span></span> <span data-ttu-id="c4b18-211">`Array.tryFind``Array.find`當您不知道相符的元素是否在陣列中時，應該使用而不是。</span><span class="sxs-lookup"><span data-stu-id="c4b18-211">`Array.tryFind` should be used instead of `Array.find` when you do not know whether a matching element is in the array.</span></span> <span data-ttu-id="c4b18-212">同樣地， [`Array.tryFindIndex`](https://msdn.microsoft.com/library/da82f7fe-95e9-4fd5-a924-cd3c9d10618a) 類似于 [`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) 選項類型為傳回值的例外。</span><span class="sxs-lookup"><span data-stu-id="c4b18-212">Similarly, [`Array.tryFindIndex`](https://msdn.microsoft.com/library/da82f7fe-95e9-4fd5-a924-cd3c9d10618a) is like [`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) except that the option type is the return value.</span></span> <span data-ttu-id="c4b18-213">如果找不到任何元素，則選項為 `None` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-213">If no element is found, the option is `None`.</span></span>

<span data-ttu-id="c4b18-214">下列程式碼示範 `Array.tryFind` 的用法。</span><span class="sxs-lookup"><span data-stu-id="c4b18-214">The following code demonstrates the use of `Array.tryFind`.</span></span> <span data-ttu-id="c4b18-215">此程式碼視先前的程式碼而定。</span><span class="sxs-lookup"><span data-stu-id="c4b18-215">This code depends on the previous code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet26.fs)]

<span data-ttu-id="c4b18-216">輸出如下。</span><span class="sxs-lookup"><span data-stu-id="c4b18-216">The output is as follows.</span></span>

```console
Found an element: 1
Found an element: 729
Failed to find a matching element.
```

<span data-ttu-id="c4b18-217">[`Array.tryPick`](https://msdn.microsoft.com/library/72d45f85-037b-43a9-97fd-17239f72713e)當您需要轉換專案，以及找出元素時，請使用。</span><span class="sxs-lookup"><span data-stu-id="c4b18-217">Use [`Array.tryPick`](https://msdn.microsoft.com/library/72d45f85-037b-43a9-97fd-17239f72713e) when you need to transform an element in addition to finding it.</span></span> <span data-ttu-id="c4b18-218">結果是第一個專案，函式會將轉換的元素當做選項值傳回， `None` 如果找不到這類元素，則為。</span><span class="sxs-lookup"><span data-stu-id="c4b18-218">The result is the first element for which the function returns the transformed element as an option value, or `None` if no such element is found.</span></span>

<span data-ttu-id="c4b18-219">下列程式碼示範 `Array.tryPick` 的用法。</span><span class="sxs-lookup"><span data-stu-id="c4b18-219">The following code shows the use of `Array.tryPick`.</span></span> <span data-ttu-id="c4b18-220">在此情況下，會定義數個本機 helper 函式來簡化程式碼，而不是 lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="c4b18-220">In this case, instead of a lambda expression, several local helper functions are defined to simplify the code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet27.fs)]

<span data-ttu-id="c4b18-221">輸出如下。</span><span class="sxs-lookup"><span data-stu-id="c4b18-221">The output is as follows.</span></span>

```console
Found an element 1 with square root 1 and cube root 1.
Found an element 64 with square root 8 and cube root 4.
Found an element 729 with square root 27 and cube root 9.
Found an element 4096 with square root 64 and cube root 16.
Did not find an element that is both a perfect square and a perfect cube.
```

### <a name="perform-computations-on-arrays"></a><span data-ttu-id="c4b18-222">在陣列上執行計算</span><span class="sxs-lookup"><span data-stu-id="c4b18-222">Perform computations on arrays</span></span>

<span data-ttu-id="c4b18-223">函 [`Array.average`](https://msdn.microsoft.com/library/7029f2b9-91ea-41cb-be1b-466a5a0db20e) 式會傳回陣列中每個元素的平均值。</span><span class="sxs-lookup"><span data-stu-id="c4b18-223">The [`Array.average`](https://msdn.microsoft.com/library/7029f2b9-91ea-41cb-be1b-466a5a0db20e) function returns the average of each element in an array.</span></span> <span data-ttu-id="c4b18-224">它受限於支援精確除以整數的元素類型，其中包括浮點類型，而不是整數類型。</span><span class="sxs-lookup"><span data-stu-id="c4b18-224">It is limited to element types that support exact division by an integer, which includes floating point types but not integral types.</span></span> <span data-ttu-id="c4b18-225">函式會傳回 [`Array.averageBy`](https://msdn.microsoft.com/library/e9d64609-06a3-48f0-bc07-226ab0f85c54) 每個元素上呼叫函式的結果平均值。</span><span class="sxs-lookup"><span data-stu-id="c4b18-225">The [`Array.averageBy`](https://msdn.microsoft.com/library/e9d64609-06a3-48f0-bc07-226ab0f85c54) function returns the average of the results of calling a function on each element.</span></span> <span data-ttu-id="c4b18-226">針對整數類型的陣列，您可以使用 `Array.averageBy` ，並讓函式將每個專案轉換成浮點類型以進行計算。</span><span class="sxs-lookup"><span data-stu-id="c4b18-226">For an array of integral type, you can use `Array.averageBy` and have the function convert each element to a floating point type for the computation.</span></span>

<span data-ttu-id="c4b18-227">[`Array.max`](https://msdn.microsoft.com/library/f03fbda0-fce6-40e2-a85d-79c9d81f710b) [`Array.min`](https://msdn.microsoft.com/library/d6b3da5f-bac0-4355-9846-4b72d95bc3fd) 如果元素類型支援，請使用或來取得最大或最小專案。</span><span class="sxs-lookup"><span data-stu-id="c4b18-227">Use [`Array.max`](https://msdn.microsoft.com/library/f03fbda0-fce6-40e2-a85d-79c9d81f710b) or [`Array.min`](https://msdn.microsoft.com/library/d6b3da5f-bac0-4355-9846-4b72d95bc3fd) to get the maximum or minimum element, if the element type supports it.</span></span> <span data-ttu-id="c4b18-228">同樣地， [`Array.maxBy`](https://msdn.microsoft.com/library/18dbe7c5-482e-4766-8e01-12a76f847045) 和 [`Array.minBy`](https://msdn.microsoft.com/library/24091583-be78-4cc9-9fab-de6d7506af4f) 允許先執行函式，可能會轉換成支援比較的類型。</span><span class="sxs-lookup"><span data-stu-id="c4b18-228">Similarly, [`Array.maxBy`](https://msdn.microsoft.com/library/18dbe7c5-482e-4766-8e01-12a76f847045) and [`Array.minBy`](https://msdn.microsoft.com/library/24091583-be78-4cc9-9fab-de6d7506af4f) allow a function to be executed first, perhaps to transform to a type that supports comparison.</span></span>

<span data-ttu-id="c4b18-229">[`Array.sum`](https://msdn.microsoft.com/library/4ffdb8c8-cd94-4b0b-9e5c-a7c9c17963c2)加入陣列的元素，並 [`Array.sumBy`](https://msdn.microsoft.com/library/41698ba6-1adc-4169-8cc5-7a0e3f8de56b) 在每個專案上呼叫函式，並將結果加在一起。</span><span class="sxs-lookup"><span data-stu-id="c4b18-229">[`Array.sum`](https://msdn.microsoft.com/library/4ffdb8c8-cd94-4b0b-9e5c-a7c9c17963c2) adds the elements of an array, and [`Array.sumBy`](https://msdn.microsoft.com/library/41698ba6-1adc-4169-8cc5-7a0e3f8de56b) calls a function on each element and adds the results together.</span></span>

<span data-ttu-id="c4b18-230">若要在陣列中的每個元素上執行函式，而不儲存傳回值，請使用 [`Array.iter`](https://msdn.microsoft.com/library/94eba0f1-ecd7-459f-b89f-ed2a2923e516) 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-230">To execute a function on each element in an array without storing the return values, use [`Array.iter`](https://msdn.microsoft.com/library/94eba0f1-ecd7-459f-b89f-ed2a2923e516).</span></span> <span data-ttu-id="c4b18-231">對於涉及兩個相等長度陣列的函數，請使用 [`Array.iter2`](https://msdn.microsoft.com/library/018aa9b9-f186-4142-be8a-a62462794fdc) 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-231">For a function involving two arrays of equal length, use [`Array.iter2`](https://msdn.microsoft.com/library/018aa9b9-f186-4142-be8a-a62462794fdc).</span></span> <span data-ttu-id="c4b18-232">如果您也需要保留函數結果的陣列，請使用 [`Array.map`](https://msdn.microsoft.com/library/38cbe824-0480-47be-85fd-df3afdd97a45) 或，這會在 [`Array.map2`](https://msdn.microsoft.com/library/bb7aafe8-4a1f-45b9-92fc-1af9eafbea5c) 兩個數組上一次操作。</span><span class="sxs-lookup"><span data-stu-id="c4b18-232">If you also need to keep an array of the results of the function, use [`Array.map`](https://msdn.microsoft.com/library/38cbe824-0480-47be-85fd-df3afdd97a45) or [`Array.map2`](https://msdn.microsoft.com/library/bb7aafe8-4a1f-45b9-92fc-1af9eafbea5c), which operates on two arrays at a time.</span></span>

<span data-ttu-id="c4b18-233">變數的變化 [`Array.iteri`](https://msdn.microsoft.com/library/8bbe2ed4-ada7-4906-ac3e-cb09f9db6486) 和允許專案的 [`Array.iteri2`](https://msdn.microsoft.com/library/c041b91f-6080-45b7-867b-2ed983a90405) 索引會包含在計算中， [`Array.mapi`](https://msdn.microsoft.com/library/f7e45994-b0a1-49e6-8fb5-5641cea8fde4) 而和則相同 [`Array.mapi2`](https://msdn.microsoft.com/library/5edb33d2-47da-44e1-9290-40c00c47d5b0) 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-233">The variations [`Array.iteri`](https://msdn.microsoft.com/library/8bbe2ed4-ada7-4906-ac3e-cb09f9db6486) and [`Array.iteri2`](https://msdn.microsoft.com/library/c041b91f-6080-45b7-867b-2ed983a90405) allow the index of the element to be involved in the computation; the same is true for [`Array.mapi`](https://msdn.microsoft.com/library/f7e45994-b0a1-49e6-8fb5-5641cea8fde4) and [`Array.mapi2`](https://msdn.microsoft.com/library/5edb33d2-47da-44e1-9290-40c00c47d5b0).</span></span>

<span data-ttu-id="c4b18-234">函式、、、、 [`Array.fold`](https://msdn.microsoft.com/library/5ed9dd3b-3694-4567-94d0-fd9a24474e09) [`Array.foldBack`](https://msdn.microsoft.com/library/1121a453-dead-4711-a0ca-cc147752989c) [`Array.reduce`](https://msdn.microsoft.com/library/fd62a985-89fe-4f49-a9d4-0c808ac6749d) [`Array.reduceBack`](https://msdn.microsoft.com/library/4fdd4cbe-2238-4c5c-b286-597a7e9036f9) [`Array.scan`](https://msdn.microsoft.com/library/f6893608-9146-450d-9ebb-a0016803fbb0) 和 [`Array.scanBack`](https://msdn.microsoft.com/library/7610f406-7a5c-41db-a0ca-8e2a2a4826ad) 包含陣列所有元素的執行演算法。</span><span class="sxs-lookup"><span data-stu-id="c4b18-234">The functions [`Array.fold`](https://msdn.microsoft.com/library/5ed9dd3b-3694-4567-94d0-fd9a24474e09), [`Array.foldBack`](https://msdn.microsoft.com/library/1121a453-dead-4711-a0ca-cc147752989c), [`Array.reduce`](https://msdn.microsoft.com/library/fd62a985-89fe-4f49-a9d4-0c808ac6749d), [`Array.reduceBack`](https://msdn.microsoft.com/library/4fdd4cbe-2238-4c5c-b286-597a7e9036f9), [`Array.scan`](https://msdn.microsoft.com/library/f6893608-9146-450d-9ebb-a0016803fbb0), and [`Array.scanBack`](https://msdn.microsoft.com/library/7610f406-7a5c-41db-a0ca-8e2a2a4826ad) execute algorithms that involve all the elements of an array.</span></span> <span data-ttu-id="c4b18-235">同樣地，變數 [`Array.fold2`](https://msdn.microsoft.com/library/5c845087-d041-476e-8cc4-53ae6849ef79) 和會 [`Array.foldBack2`](https://msdn.microsoft.com/library/aa51b405-df20-4c51-9998-a6530f7db862) 在兩個數組上執行計算。</span><span class="sxs-lookup"><span data-stu-id="c4b18-235">Similarly, the variations [`Array.fold2`](https://msdn.microsoft.com/library/5c845087-d041-476e-8cc4-53ae6849ef79) and [`Array.foldBack2`](https://msdn.microsoft.com/library/aa51b405-df20-4c51-9998-a6530f7db862) perform computations on two arrays.</span></span>

<span data-ttu-id="c4b18-236">這些用來執行計算的函式會對應至[清單模組](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)中相同名稱的函式。</span><span class="sxs-lookup"><span data-stu-id="c4b18-236">These functions for performing computations correspond to the functions of the same name in the [List module](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788).</span></span> <span data-ttu-id="c4b18-237">如需使用範例，請參閱[清單](lists.md)。</span><span class="sxs-lookup"><span data-stu-id="c4b18-237">For usage examples, see [Lists](lists.md).</span></span>

### <a name="modify-arrays"></a><span data-ttu-id="c4b18-238">修改陣列</span><span class="sxs-lookup"><span data-stu-id="c4b18-238">Modify arrays</span></span>

<span data-ttu-id="c4b18-239">[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790)將元素設定為指定的值。</span><span class="sxs-lookup"><span data-stu-id="c4b18-239">[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790) sets an element to a specified value.</span></span> <span data-ttu-id="c4b18-240">[`Array.fill`](https://msdn.microsoft.com/library/c83c9886-81d9-44f9-a195-61c7b87f7df2)將陣列中的元素範圍設定為指定的值。</span><span class="sxs-lookup"><span data-stu-id="c4b18-240">[`Array.fill`](https://msdn.microsoft.com/library/c83c9886-81d9-44f9-a195-61c7b87f7df2) sets a range of elements in an array to a specified value.</span></span> <span data-ttu-id="c4b18-241">下列程式碼提供的範例 `Array.fill` 。</span><span class="sxs-lookup"><span data-stu-id="c4b18-241">The following code provides an example of `Array.fill`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/arrays/snippet28.fs)]

<span data-ttu-id="c4b18-242">輸出如下。</span><span class="sxs-lookup"><span data-stu-id="c4b18-242">The output is as follows.</span></span>

```console
[|1; 2; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 23; 24; 25|]
```

<span data-ttu-id="c4b18-243">您可以使用 [`Array.blit`](https://msdn.microsoft.com/library/675e13e4-7fb9-4e0d-a5be-a112830de667) ，將一個陣列的子區段複製到另一個陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-243">You can use [`Array.blit`](https://msdn.microsoft.com/library/675e13e4-7fb9-4e0d-a5be-a112830de667) to copy a subsection of one array to another array.</span></span>

### <a name="convert-to-and-from-other-types"></a><span data-ttu-id="c4b18-244">與其他類型相互轉換</span><span class="sxs-lookup"><span data-stu-id="c4b18-244">Convert to and from other types</span></span>

<span data-ttu-id="c4b18-245">[`Array.ofList`](https://msdn.microsoft.com/library/e7225239-f561-45a4-b0b5-69a1cdcae78b)從清單建立陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-245">[`Array.ofList`](https://msdn.microsoft.com/library/e7225239-f561-45a4-b0b5-69a1cdcae78b) creates an array from a list.</span></span> <span data-ttu-id="c4b18-246">[`Array.ofSeq`](https://msdn.microsoft.com/library/6bedf5e0-4b22-46da-b09c-6aa09eff220c)從序列建立陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-246">[`Array.ofSeq`](https://msdn.microsoft.com/library/6bedf5e0-4b22-46da-b09c-6aa09eff220c) creates an array from a sequence.</span></span> <span data-ttu-id="c4b18-247">[`Array.toList`](https://msdn.microsoft.com/library/4deff724-0be4-4688-92e7-9d67a1097786)和會 [`Array.toSeq`](https://msdn.microsoft.com/library/ac28dbab-406c-4fe0-ab08-c1ce5e247af4) 從陣列類型轉換成這些其他集合類型。</span><span class="sxs-lookup"><span data-stu-id="c4b18-247">[`Array.toList`](https://msdn.microsoft.com/library/4deff724-0be4-4688-92e7-9d67a1097786) and [`Array.toSeq`](https://msdn.microsoft.com/library/ac28dbab-406c-4fe0-ab08-c1ce5e247af4) convert to these other collection types from the array type.</span></span>

### <a name="sort-arrays"></a><span data-ttu-id="c4b18-248">排序陣列</span><span class="sxs-lookup"><span data-stu-id="c4b18-248">Sort arrays</span></span>

<span data-ttu-id="c4b18-249">使用 [`Array.sort`](https://msdn.microsoft.com/library/c6679075-e7eb-463c-9be5-c89be140c312) 來排序陣列，方法是使用泛型比較函數。</span><span class="sxs-lookup"><span data-stu-id="c4b18-249">Use [`Array.sort`](https://msdn.microsoft.com/library/c6679075-e7eb-463c-9be5-c89be140c312) to sort an array by using the generic comparison function.</span></span> <span data-ttu-id="c4b18-250">使用 [`Array.sortBy`](https://msdn.microsoft.com/library/144498dc-091d-4575-a229-c0bcbd61426b) 來指定產生值（稱為索引*鍵*）的函式，以使用索引鍵上的泛型比較函數進行排序。</span><span class="sxs-lookup"><span data-stu-id="c4b18-250">Use [`Array.sortBy`](https://msdn.microsoft.com/library/144498dc-091d-4575-a229-c0bcbd61426b) to specify a function that generates a value, referred to as a *key*, to sort by using the generic comparison function on the key.</span></span> <span data-ttu-id="c4b18-251">[`Array.sortWith`](https://msdn.microsoft.com/library/699d3638-4244-4f42-8496-45f53d43ce95)如果您想要提供自訂比較函數，請使用。</span><span class="sxs-lookup"><span data-stu-id="c4b18-251">Use [`Array.sortWith`](https://msdn.microsoft.com/library/699d3638-4244-4f42-8496-45f53d43ce95) if you want to provide a custom comparison function.</span></span> <span data-ttu-id="c4b18-252">`Array.sort`、 `Array.sortBy` 和 `Array.sortWith` 全都會以新陣列的形式傳回已排序的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-252">`Array.sort`, `Array.sortBy`, and `Array.sortWith` all return the sorted array as a new array.</span></span> <span data-ttu-id="c4b18-253">變體 [`Array.sortInPlace`](https://msdn.microsoft.com/library/36f39947-8a88-4823-9e9b-e9d838d292e0) 、 [`Array.sortInPlaceBy`](https://msdn.microsoft.com/library/7fb9d2dd-d461-4c67-8b43-b5c59fc12c3f) 和會 [`Array.sortInPlaceWith`](https://msdn.microsoft.com/library/454f9e11-972d-47a6-a854-8031cb0c7b0b) 修改現有的陣列，而不是傳回新的陣列。</span><span class="sxs-lookup"><span data-stu-id="c4b18-253">The variations [`Array.sortInPlace`](https://msdn.microsoft.com/library/36f39947-8a88-4823-9e9b-e9d838d292e0), [`Array.sortInPlaceBy`](https://msdn.microsoft.com/library/7fb9d2dd-d461-4c67-8b43-b5c59fc12c3f), and [`Array.sortInPlaceWith`](https://msdn.microsoft.com/library/454f9e11-972d-47a6-a854-8031cb0c7b0b) modify the existing array instead of returning a new one.</span></span>

### <a name="arrays-and-tuples"></a><span data-ttu-id="c4b18-254">陣列和元組</span><span class="sxs-lookup"><span data-stu-id="c4b18-254">Arrays and tuples</span></span>

<span data-ttu-id="c4b18-255">函式會將 [`Array.zip`](https://msdn.microsoft.com/library/23e086b8-b266-4db2-8b68-e88e6a8e2187) [`Array.unzip`](https://msdn.microsoft.com/library/a529b47c-2e2b-4f79-ad44-c578432d2f48) 元組配對的陣列轉換成陣列的元組，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="c4b18-255">The functions [`Array.zip`](https://msdn.microsoft.com/library/23e086b8-b266-4db2-8b68-e88e6a8e2187) and [`Array.unzip`](https://msdn.microsoft.com/library/a529b47c-2e2b-4f79-ad44-c578432d2f48) convert arrays of tuple pairs to tuples of arrays and vice versa.</span></span> <span data-ttu-id="c4b18-256">[`Array.zip3`](https://msdn.microsoft.com/library/1745744a-d2ca-4c3e-b825-3f15d9f4000d)和 [`Array.unzip3`](https://msdn.microsoft.com/library/bc3e6db0-f334-444f-8c30-813942880677) 很相似，不同之處在于它們會與三個數組的三個元素或元組的元組搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c4b18-256">[`Array.zip3`](https://msdn.microsoft.com/library/1745744a-d2ca-4c3e-b825-3f15d9f4000d) and [`Array.unzip3`](https://msdn.microsoft.com/library/bc3e6db0-f334-444f-8c30-813942880677) are similar except that they work with tuples of three elements or tuples of three arrays.</span></span>

## <a name="parallel-computations-on-arrays"></a><span data-ttu-id="c4b18-257">陣列上的平行計算</span><span class="sxs-lookup"><span data-stu-id="c4b18-257">Parallel computations on arrays</span></span>

<span data-ttu-id="c4b18-258">模組 [`Array.Parallel`](https://msdn.microsoft.com/library/60f30b77-5af4-4050-9a5c-bcdb3f5cbb09) 包含在陣列上執行平行計算的函數。</span><span class="sxs-lookup"><span data-stu-id="c4b18-258">The module [`Array.Parallel`](https://msdn.microsoft.com/library/60f30b77-5af4-4050-9a5c-bcdb3f5cbb09) contains functions for performing parallel computations on arrays.</span></span> <span data-ttu-id="c4b18-259">在版本4之前以 .NET Framework 版本為目標的應用程式中，無法使用此模組。</span><span class="sxs-lookup"><span data-stu-id="c4b18-259">This module is not available in applications that target versions of the .NET Framework prior to version 4.</span></span>

## <a name="see-also"></a><span data-ttu-id="c4b18-260">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c4b18-260">See also</span></span>

- [<span data-ttu-id="c4b18-261">F # 語言參考</span><span class="sxs-lookup"><span data-stu-id="c4b18-261">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="c4b18-262">F# 類型</span><span class="sxs-lookup"><span data-stu-id="c4b18-262">F# Types</span></span>](fsharp-types.md)
