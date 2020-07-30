---
title: Boxing 和 Unboxing - C# 程式設計指南
description: '瞭解 c # 程式設計中的裝箱和取消裝箱。 請參閱程式碼範例，並查看其他可用的資源。'
ms.date: 07/20/2015
f1_keywords:
- cs.boxing
helpviewer_keywords:
- C# language, boxing
- C# language, unboxing
- unboxing [C#]
- boxing [C#]
ms.assetid: 8da9bbf4-bce9-4b08-b2e5-f64c11c56514
ms.openlocfilehash: 5a5bfcc79de8ba3ff66ca8aab9d86d69d89f9221
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87380692"
---
# <a name="boxing-and-unboxing-c-programming-guide"></a><span data-ttu-id="cd2d9-104">Boxing 和 Unboxing (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="cd2d9-104">Boxing and Unboxing (C# Programming Guide)</span></span>

<span data-ttu-id="cd2d9-105">Boxing 是將[實值型別](../../language-reference/builtin-types/value-types.md)轉換為 `object` 類型或是由這個實值型別實作之任何介面類型的程序。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-105">Boxing is the process of converting a [value type](../../language-reference/builtin-types/value-types.md) to the type `object` or to any interface type implemented by this value type.</span></span> <span data-ttu-id="cd2d9-106">當 common language runtime （CLR）方塊為實值型別時，它會將值包裝在實例內， <xref:System.Object?displayProperty=nameWithType> 並將其儲存在受控堆積上。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-106">When the common language runtime (CLR) boxes a value type, it wraps the value inside a <xref:System.Object?displayProperty=nameWithType> instance and stores it on the managed heap.</span></span> <span data-ttu-id="cd2d9-107">Unbox 處理則會從物件中擷取實值類型。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-107">Unboxing extracts the value type from the object.</span></span> <span data-ttu-id="cd2d9-108">Boxing 是隱含處理，unboxing 則是明確處理。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-108">Boxing is implicit; unboxing is explicit.</span></span> <span data-ttu-id="cd2d9-109">Boxing 和 unboxing 的概念是 C# 類型系統統一檢視的基礎，其中任何類型的值都可視為物件。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-109">The concept of boxing and unboxing underlies the C# unified view of the type system in which a value of any type can be treated as an object.</span></span>

<span data-ttu-id="cd2d9-110">在下列範例中，整數變數 `i` 會經過 *Box* 處理並且指派給 `o` 物件。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-110">In the following example, the integer variable `i` is *boxed* and assigned to object `o`.</span></span>

[!code-csharp[csProgGuideTypes#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#14)]

<span data-ttu-id="cd2d9-111">接著就可以對物件 `o` 進行 Unbox 處理，並將該物件指派給整數變數 `i`：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-111">The object `o` can then be unboxed and assigned to integer variable `i`:</span></span>

[!code-csharp[csProgGuideTypes#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#15)]

<span data-ttu-id="cd2d9-112">下列範例將說明在 C# 中使用 boxing 的方式。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-112">The following examples illustrate how boxing is used in C#.</span></span>

[!code-csharp[csProgGuideTypes#47](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#47)]

## <a name="performance"></a><span data-ttu-id="cd2d9-113">效能</span><span class="sxs-lookup"><span data-stu-id="cd2d9-113">Performance</span></span>

<span data-ttu-id="cd2d9-114">相對於單純的指派，boxing 和 unboxing 是會耗費大量運算資源的處理序。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-114">In relation to simple assignments, boxing and unboxing are computationally expensive processes.</span></span> <span data-ttu-id="cd2d9-115">當實值類型經過 Box 處理時，必須配置及建構新的物件。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-115">When a value type is boxed, a new object must be allocated and constructed.</span></span> <span data-ttu-id="cd2d9-116">Unboxing 所需的轉換雖然較為簡單，但也同樣需要大量運算資源。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-116">To a lesser degree, the cast required for unboxing is also expensive computationally.</span></span> <span data-ttu-id="cd2d9-117">如需詳細資訊，請參閱[效能](../../../framework/performance/performance-tips.md)。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-117">For more information, see [Performance](../../../framework/performance/performance-tips.md).</span></span>

## <a name="boxing"></a><span data-ttu-id="cd2d9-118">Box 處理</span><span class="sxs-lookup"><span data-stu-id="cd2d9-118">Boxing</span></span>

<span data-ttu-id="cd2d9-119">Boxing 可用來儲存記憶體回收堆積中的實值類型。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-119">Boxing is used to store value types in the garbage-collected heap.</span></span> <span data-ttu-id="cd2d9-120">Boxing 是一種隱含轉換，可將[實值型別](../../language-reference/builtin-types/value-types.md)轉換為 `object` 類型，或是由這個實值型別實作的任何介面類型。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-120">Boxing is an implicit conversion of a [value type](../../language-reference/builtin-types/value-types.md) to the type `object` or to any interface type implemented by this value type.</span></span> <span data-ttu-id="cd2d9-121">對實值類型進行 Boxing 處理時，會在堆積上配置物件執行個體，並將值複製到新物件中。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-121">Boxing a value type allocates an object instance on the heap and copies the value into the new object.</span></span>

<span data-ttu-id="cd2d9-122">請考慮下列實值類型變數的宣告：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-122">Consider the following declaration of a value-type variable:</span></span>

[!code-csharp[csProgGuideTypes#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#17)]

<span data-ttu-id="cd2d9-123">下列陳述式會以隱含方式對變數 `i` 套用 boxing 作業：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-123">The following statement implicitly applies the boxing operation on the variable `i`:</span></span>

[!code-csharp[csProgGuideTypes#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#18)]

<span data-ttu-id="cd2d9-124">這個陳述式的結果是在堆疊上建立物件參考 `o`，用於參考堆積中 `int` 類型的值。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-124">The result of this statement is creating an object reference `o`, on the stack, that references a value of the type `int`, on the heap.</span></span> <span data-ttu-id="cd2d9-125">這個值是指派給變數 `i` 之實值類型值的複本。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-125">This value is a copy of the value-type value assigned to the variable `i`.</span></span> <span data-ttu-id="cd2d9-126">`i` 和 `o` 這兩個變數之間的差異如下方 Boxing 轉換圖所示：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-126">The difference between the two variables, `i` and `o`, is illustrated in the following image of boxing conversion:</span></span>

![顯示 i 和 o 變數之間差異的圖形。](./media/boxing-and-unboxing/boxing-operation-i-o-variables.gif)

<span data-ttu-id="cd2d9-128">您也可以執行明確的 boxing 處理，如同下列範例中所示，但是明確的 boxing 處理並非必要：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-128">It is also possible to perform the boxing explicitly as in the following example, but explicit boxing is never required:</span></span>

[!code-csharp[csProgGuideTypes#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#19)]

## <a name="description"></a><span data-ttu-id="cd2d9-129">描述</span><span class="sxs-lookup"><span data-stu-id="cd2d9-129">Description</span></span>

<span data-ttu-id="cd2d9-130">這個範例會使用 Boxing 將整數變數 `i` 轉換為物件 `o`。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-130">This example converts an integer variable `i` to an object `o` by using boxing.</span></span> <span data-ttu-id="cd2d9-131">接著，儲存在變數 `i` 中的值就會從 `123` 變更為 `456`。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-131">Then, the value stored in the variable `i` is changed from `123` to `456`.</span></span> <span data-ttu-id="cd2d9-132">這個範例顯示，原始實值類型以及經過 Box 處理的物件分別使用不同的記憶體位置，因此可以儲存不同的值。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-132">The example shows that the original value type and the boxed object use separate memory locations, and therefore can store different values.</span></span>

## <a name="example"></a><span data-ttu-id="cd2d9-133">範例</span><span class="sxs-lookup"><span data-stu-id="cd2d9-133">Example</span></span>

[!code-csharp[csProgGuideTypes#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#16)]

## <a name="unboxing"></a><span data-ttu-id="cd2d9-134">Unbox 處理</span><span class="sxs-lookup"><span data-stu-id="cd2d9-134">Unboxing</span></span>

<span data-ttu-id="cd2d9-135">Unboxing 是將 `object` 類型明確轉換為[實值型別](../../language-reference/builtin-types/value-types.md)，或將介面類型明確轉換為實作介面之實值型別的程序。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-135">Unboxing is an explicit conversion from the type `object` to a [value type](../../language-reference/builtin-types/value-types.md) or from an interface type to a value type that implements the interface.</span></span> <span data-ttu-id="cd2d9-136">Unboxing 作業包含：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-136">An unboxing operation consists of:</span></span>

- <span data-ttu-id="cd2d9-137">檢查物件執行個體，確定它是所指定實值類型經過 Box 處理的值。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-137">Checking the object instance to make sure that it is a boxed value of the given value type.</span></span>

- <span data-ttu-id="cd2d9-138">將值從執行個體複製到實值類型變數。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-138">Copying the value from the instance into the value-type variable.</span></span>

<span data-ttu-id="cd2d9-139">下列陳述式將示範 boxing 和 unboxing 作業：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-139">The following statements demonstrate both boxing and unboxing operations:</span></span>

[!code-csharp[csProgGuideTypes#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#21)]

<span data-ttu-id="cd2d9-140">下圖示範上述陳述式的結果：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-140">The following figure demonstrates the result of the previous statements:</span></span>

![顯示 Unboxing 轉換的圖形。](./media/boxing-and-unboxing/unboxing-conversion-operation.gif)

<span data-ttu-id="cd2d9-142">若要在執行階段成功對實值類型進行 Unbox 處理，要進行 Unbox 處理的項目必須是物件的參考，而且該物件是先前對該實值類型的執行個體進行 Box 處理所建立的物件。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-142">For the unboxing of value types to succeed at run time, the item being unboxed must be a reference to an object that was previously created by boxing an instance of that value type.</span></span> <span data-ttu-id="cd2d9-143">嘗試對 `null` 進行 Unbox 處理會造成 <xref:System.NullReferenceException>。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-143">Attempting to unbox `null` causes a <xref:System.NullReferenceException>.</span></span> <span data-ttu-id="cd2d9-144">嘗試對不相容的實值類型參考進行 Unbox 處理會造成 <xref:System.InvalidCastException>。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-144">Attempting to unbox a reference to an incompatible value type causes an <xref:System.InvalidCastException>.</span></span>

## <a name="example"></a><span data-ttu-id="cd2d9-145">範例</span><span class="sxs-lookup"><span data-stu-id="cd2d9-145">Example</span></span>

<span data-ttu-id="cd2d9-146">下列範例將示範 Unboxing 無效且產生 `InvalidCastException` 的案例。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-146">The following example demonstrates a case of invalid unboxing and the resulting `InvalidCastException`.</span></span> <span data-ttu-id="cd2d9-147">若使用 `try` 和 `catch`，則會在發生錯誤時顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="cd2d9-147">Using `try` and `catch`, an error message is displayed when the error occurs.</span></span>

[!code-csharp[csProgGuideTypes#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#20)]

<span data-ttu-id="cd2d9-148">這個程式會輸出：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-148">This program outputs:</span></span>

`Specified cast is not valid. Error: Incorrect unboxing.`

<span data-ttu-id="cd2d9-149">如果您將陳述式：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-149">If you change the statement:</span></span>

```csharp
int j = (short) o;
```

<span data-ttu-id="cd2d9-150">變更為：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-150">to:</span></span>

```csharp
int j = (int) o;
```

<span data-ttu-id="cd2d9-151">轉換將會執行，而且您會得到下列輸出結果：</span><span class="sxs-lookup"><span data-stu-id="cd2d9-151">the conversion will be performed, and you will get the output:</span></span>

`Unboxing OK.`

## <a name="c-language-specification"></a><span data-ttu-id="cd2d9-152">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="cd2d9-152">C# language specification</span></span>

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="cd2d9-153">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cd2d9-153">See also</span></span>

- [<span data-ttu-id="cd2d9-154">C# 程式設計手冊</span><span class="sxs-lookup"><span data-stu-id="cd2d9-154">C# programming guide</span></span>](../index.md)
- [<span data-ttu-id="cd2d9-155">參考型別</span><span class="sxs-lookup"><span data-stu-id="cd2d9-155">Reference types</span></span>](../../language-reference/keywords/reference-types.md)
- [<span data-ttu-id="cd2d9-156">值類型</span><span class="sxs-lookup"><span data-stu-id="cd2d9-156">Value types</span></span>](../../language-reference/builtin-types/value-types.md)
