---
title: 傳遞實值類型的參數 - C# 程式設計手冊
description: '當您在 c # 中以傳值方式將實值型別變數傳遞給方法時，任何變更都不會影響原始資料。 若要變更值，請以傳址方式傳遞。'
ms.date: 07/20/2015
helpviewer_keywords:
- method parameters [C#], value types
- parameters [C#], value
ms.assetid: 193ab86f-5f9b-4359-ac29-7cdf8afad3a6
ms.openlocfilehash: ccc97e2f6e8c6b2b8fd15206a8bcd5cd8a5a8431
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91186064"
---
# <a name="passing-value-type-parameters-c-programming-guide"></a><span data-ttu-id="7e59f-104">傳遞實值類型的參數 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="7e59f-104">Passing Value-Type Parameters (C# Programming Guide)</span></span>

<span data-ttu-id="7e59f-105">相對於[參考型別](../../language-reference/keywords/reference-types.md)變數 (包含對其資料的參考)，[實值型別](../../language-reference/builtin-types/value-types.md)變數會直接包含資料。</span><span class="sxs-lookup"><span data-stu-id="7e59f-105">A [value-type](../../language-reference/builtin-types/value-types.md) variable contains its data directly as opposed to a [reference-type](../../language-reference/keywords/reference-types.md) variable, which contains a reference to its data.</span></span> <span data-ttu-id="7e59f-106">以傳值方式將實值型別變數傳遞至方法，意味著將變數的複本傳遞至方法。</span><span class="sxs-lookup"><span data-stu-id="7e59f-106">Passing a value-type variable to a method by value means passing a copy of the variable to the method.</span></span> <span data-ttu-id="7e59f-107">在方法內發生之參數的任何變更都不會影響在引數變數中所儲存的原始資料。</span><span class="sxs-lookup"><span data-stu-id="7e59f-107">Any changes to the parameter that take place inside the method have no effect on the original data stored in the argument variable.</span></span> <span data-ttu-id="7e59f-108">如果您想要讓呼叫的方法變更參數值，就必須使用 [ref](../../language-reference/keywords/ref.md) 或 [out](../../language-reference/keywords/out-parameter-modifier.md) 關鍵字，以傳址方式來傳遞它。</span><span class="sxs-lookup"><span data-stu-id="7e59f-108">If you want the called method to change the value of the argument, you must pass it by reference, using the [ref](../../language-reference/keywords/ref.md) or [out](../../language-reference/keywords/out-parameter-modifier.md) keyword.</span></span> <span data-ttu-id="7e59f-109">您也可以使用 [in](../../language-reference/keywords/in-parameter-modifier.md) 關鍵字以傳址方式傳遞值，以避免發生複製的情況，同時確保該值不會變更。</span><span class="sxs-lookup"><span data-stu-id="7e59f-109">You may also use the [in](../../language-reference/keywords/in-parameter-modifier.md) keyword to pass a value parameter by reference to avoid the copy while guaranteeing that the value will not be changed.</span></span> <span data-ttu-id="7e59f-110">為求簡化，下列範例使用 `ref`。</span><span class="sxs-lookup"><span data-stu-id="7e59f-110">For simplicity, the following examples use `ref`.</span></span>  
  
## <a name="passing-value-types-by-value"></a><span data-ttu-id="7e59f-111">以傳值方式傳遞實值型別</span><span class="sxs-lookup"><span data-stu-id="7e59f-111">Passing Value Types by Value</span></span>  

 <span data-ttu-id="7e59f-112">下列範例示範以傳值方式傳遞實值型別參數。</span><span class="sxs-lookup"><span data-stu-id="7e59f-112">The following example demonstrates passing value-type parameters by value.</span></span> <span data-ttu-id="7e59f-113">`n` 變數會以傳值方式傳遞至 `SquareIt` 方法。</span><span class="sxs-lookup"><span data-stu-id="7e59f-113">The variable `n` is passed by value to the method `SquareIt`.</span></span> <span data-ttu-id="7e59f-114">在方法內發生的任何變更都不會影響變數的原始值。</span><span class="sxs-lookup"><span data-stu-id="7e59f-114">Any changes that take place inside the method have no effect on the original value of the variable.</span></span>  
  
 [!code-csharp[csProgGuideParameters#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#3)]  
  
 <span data-ttu-id="7e59f-115">`n` 變數是實值型別。</span><span class="sxs-lookup"><span data-stu-id="7e59f-115">The variable `n` is a value type.</span></span> <span data-ttu-id="7e59f-116">它包含值為 `5` 的資料。</span><span class="sxs-lookup"><span data-stu-id="7e59f-116">It contains its data, the value `5`.</span></span> <span data-ttu-id="7e59f-117">叫用 `SquareIt` 時，會將 `n` 的內容複製到 `x` 參數，並在方法內部將其平方。</span><span class="sxs-lookup"><span data-stu-id="7e59f-117">When `SquareIt` is invoked, the contents of `n` are copied into the parameter `x`, which is squared inside the method.</span></span> <span data-ttu-id="7e59f-118">不過，在 `Main` 中，`n` 的值在呼叫`SquareIt` 方法前後是一樣的。</span><span class="sxs-lookup"><span data-stu-id="7e59f-118">In `Main`, however, the value of `n` is the same after calling the `SquareIt` method as it was before.</span></span> <span data-ttu-id="7e59f-119">發生在方法內部的變更只會影響區域變數 `x`。</span><span class="sxs-lookup"><span data-stu-id="7e59f-119">The change that takes place inside the method only affects the local variable `x`.</span></span>  
  
## <a name="passing-value-types-by-reference"></a><span data-ttu-id="7e59f-120">以傳址方式傳遞實值型別</span><span class="sxs-lookup"><span data-stu-id="7e59f-120">Passing Value Types by Reference</span></span>  

 <span data-ttu-id="7e59f-121">下列範例與上述範例相同，差別在於引數是以 `ref` 參數來傳遞。</span><span class="sxs-lookup"><span data-stu-id="7e59f-121">The following example is the same as the previous example, except that the argument is passed as a `ref` parameter.</span></span> <span data-ttu-id="7e59f-122">當方法中的 `x` 變更時，基礎引數的值 (`n`) 也會變更。</span><span class="sxs-lookup"><span data-stu-id="7e59f-122">The value of the underlying argument, `n`, is changed when `x` is changed in the method.</span></span>  
  
 [!code-csharp[csProgGuideParameters#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#4)]  
  
 <span data-ttu-id="7e59f-123">在此範例中，它不是所傳遞之 `n` 的值；而是傳遞對 `n` 的參考。</span><span class="sxs-lookup"><span data-stu-id="7e59f-123">In this example, it is not the value of `n` that is passed; rather, a reference to `n` is passed.</span></span> <span data-ttu-id="7e59f-124">`x` 參數不是 [int](../../language-reference/builtin-types/integral-numeric-types.md)；它是對 `int` 的參考，在此案例中，為對 `n` 的參考。</span><span class="sxs-lookup"><span data-stu-id="7e59f-124">The parameter `x` is not an [int](../../language-reference/builtin-types/integral-numeric-types.md); it is a reference to an `int`, in this case, a reference to `n`.</span></span> <span data-ttu-id="7e59f-125">因此，在方法內部將 `x` 平方時，實際平方的是 `x` 所參考的目標，即 `n`。</span><span class="sxs-lookup"><span data-stu-id="7e59f-125">Therefore, when `x` is squared inside the method, what actually is squared is what `x` refers to, `n`.</span></span>  
  
## <a name="swapping-value-types"></a><span data-ttu-id="7e59f-126">交換實值型別</span><span class="sxs-lookup"><span data-stu-id="7e59f-126">Swapping Value Types</span></span>  

 <span data-ttu-id="7e59f-127">變更引數值的常見範例是 swap 方法，您會在其中將兩個變數傳遞至方法，而此方法會交換它們的內容。</span><span class="sxs-lookup"><span data-stu-id="7e59f-127">A common example of changing the values of arguments is a swap method, where you pass two variables to the method, and the method swaps their contents.</span></span> <span data-ttu-id="7e59f-128">您必須以傳址方式將引數傳遞至 swap 方法。</span><span class="sxs-lookup"><span data-stu-id="7e59f-128">You must pass the arguments to the swap method by reference.</span></span> <span data-ttu-id="7e59f-129">否則，您會交換方法內部參數的區域複本，而不會在呼叫方法中發生任何變更。</span><span class="sxs-lookup"><span data-stu-id="7e59f-129">Otherwise, you swap local copies of the parameters inside the method, and no change occurs in the calling method.</span></span> <span data-ttu-id="7e59f-130">下例會交換整數值。</span><span class="sxs-lookup"><span data-stu-id="7e59f-130">The following example swaps integer values.</span></span>  
  
 [!code-csharp[csProgGuideParameters#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#5)]  
  
 <span data-ttu-id="7e59f-131">當您呼叫 `SwapByRef` 方法時，請在呼叫中使用 `ref` 關鍵字，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="7e59f-131">When you call the `SwapByRef` method, use the `ref` keyword in the call, as shown in the following example.</span></span>  
  
 [!code-csharp[csProgGuideParameters#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#6)]  
  
## <a name="see-also"></a><span data-ttu-id="7e59f-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7e59f-132">See also</span></span>

- [<span data-ttu-id="7e59f-133">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="7e59f-133">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="7e59f-134">傳遞參數</span><span class="sxs-lookup"><span data-stu-id="7e59f-134">Passing Parameters</span></span>](./passing-parameters.md)
- [<span data-ttu-id="7e59f-135">傳遞參考型別參數</span><span class="sxs-lookup"><span data-stu-id="7e59f-135">Passing Reference-Type Parameters</span></span>](./passing-reference-type-parameters.md)
