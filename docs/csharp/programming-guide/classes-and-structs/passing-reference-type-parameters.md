---
title: 傳遞參考類型的參數 - C# 程式設計手冊
description: '當您在 c # 中以傳值方式傳遞參考型別參數時，參考物件中的資料可能會變更，但不能變更參考本身的值。'
ms.date: 07/20/2015
helpviewer_keywords:
- method parameters [C#], reference types
- parameters [C#], reference
ms.assetid: 9e6eb65c-942e-48ab-920a-b7ba9df4ea20
ms.openlocfilehash: 315c1193de12a8fb5c066e023bb98bc228ce85bb
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91154115"
---
# <a name="passing-reference-type-parameters-c-programming-guide"></a><span data-ttu-id="3ea14-103">傳遞參考類型的參數 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="3ea14-103">Passing Reference-Type Parameters (C# Programming Guide)</span></span>

<span data-ttu-id="3ea14-104">[參考型別](../../language-reference/keywords/reference-types.md)的變數不會直接包含其資料；它會包含其資料的參考。</span><span class="sxs-lookup"><span data-stu-id="3ea14-104">A variable of a [reference type](../../language-reference/keywords/reference-types.md) does not contain its data directly; it contains a reference to its data.</span></span> <span data-ttu-id="3ea14-105">以值的方式傳遞參考型別參數時，可以變更屬於參考資料的資料，例如類別成員的值。</span><span class="sxs-lookup"><span data-stu-id="3ea14-105">When you pass a reference-type parameter by value, it is possible to change the data belonging to the referenced object, such as the value of a class member.</span></span> <span data-ttu-id="3ea14-106">但您無法變更參考本身的值；例如，您無法使用相同的參考，為新的物件配置記憶體，並讓其保存在方法之外。</span><span class="sxs-lookup"><span data-stu-id="3ea14-106">However, you cannot change the value of the reference itself; for example, you cannot use the same reference to allocate memory for a new object and have it persist outside the method.</span></span> <span data-ttu-id="3ea14-107">若要這樣做，請使用 [ref](../../language-reference/keywords/ref.md) 或 [out](../../language-reference/keywords/out-parameter-modifier.md) 關鍵字來傳遞參數。</span><span class="sxs-lookup"><span data-stu-id="3ea14-107">To do that, pass the parameter using the [ref](../../language-reference/keywords/ref.md) or [out](../../language-reference/keywords/out-parameter-modifier.md) keyword.</span></span> <span data-ttu-id="3ea14-108">為求簡化，下列範例使用 `ref`。</span><span class="sxs-lookup"><span data-stu-id="3ea14-108">For simplicity, the following examples use `ref`.</span></span>  
  
## <a name="passing-reference-types-by-value"></a><span data-ttu-id="3ea14-109">以傳值方式傳遞參考型別</span><span class="sxs-lookup"><span data-stu-id="3ea14-109">Passing Reference Types by Value</span></span>  

 <span data-ttu-id="3ea14-110">下列範例示範以傳值方式將 `arr` 參考型別參數傳遞至 `Change` 方法。</span><span class="sxs-lookup"><span data-stu-id="3ea14-110">The following example demonstrates passing a reference-type parameter, `arr`, by value, to a method, `Change`.</span></span> <span data-ttu-id="3ea14-111">因為參數是對 `arr` 的參考，所以可以變更陣列元素的值。</span><span class="sxs-lookup"><span data-stu-id="3ea14-111">Because the parameter is a reference to `arr`, it is possible to change the values of the array elements.</span></span> <span data-ttu-id="3ea14-112">不過，嘗試將參數重新指派至不同的記憶體位置只能在方法內運作，而且不會影響原始的 `arr` 變數。</span><span class="sxs-lookup"><span data-stu-id="3ea14-112">However, the attempt to reassign the parameter to a different memory location only works inside the method and does not affect the original variable, `arr`.</span></span>  
  
 [!code-csharp[csProgGuideParameters#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#7)]  
  
 <span data-ttu-id="3ea14-113">在上述範例中，作為參考型別的 `arr` 陣列傳遞至方法時，不會使用 `ref` 參數。</span><span class="sxs-lookup"><span data-stu-id="3ea14-113">In the preceding example, the array, `arr`, which is a reference type, is passed to the method without the `ref` parameter.</span></span> <span data-ttu-id="3ea14-114">在這種情況下，指向 `arr` 的參考複本會傳遞至方法。</span><span class="sxs-lookup"><span data-stu-id="3ea14-114">In such a case, a copy of the reference, which points to `arr`, is passed to the method.</span></span> <span data-ttu-id="3ea14-115">輸出顯示方法可以變更陣列元素的內容，在此情況下為 `1` 到 `888`。</span><span class="sxs-lookup"><span data-stu-id="3ea14-115">The output shows that it is possible for the method to change the contents of an array element, in this case from `1` to `888`.</span></span> <span data-ttu-id="3ea14-116">不過，在 `Change` 方法內部使用 [new](../../language-reference/operators/new-operator.md) 運算子來配置新的記憶體部分，會讓 `pArray` 參數參考新的陣列。</span><span class="sxs-lookup"><span data-stu-id="3ea14-116">However, allocating a new portion of memory by using the [new](../../language-reference/operators/new-operator.md) operator inside the `Change` method makes the variable `pArray` reference a new array.</span></span> <span data-ttu-id="3ea14-117">因此，之後的任何變更將不會影響在 `Main` 內部建立的 `arr` 原始陣列。</span><span class="sxs-lookup"><span data-stu-id="3ea14-117">Thus, any changes after that will not affect the original array, `arr`, which is created inside `Main`.</span></span> <span data-ttu-id="3ea14-118">事實上，在此範例中會建立兩個陣列，一個在 `Main` 內部，另一個在 `Change` 方法內部。</span><span class="sxs-lookup"><span data-stu-id="3ea14-118">In fact, two arrays are created in this example, one inside `Main` and one inside the `Change` method.</span></span>  
  
## <a name="passing-reference-types-by-reference"></a><span data-ttu-id="3ea14-119">以傳址式傳遞參考型別</span><span class="sxs-lookup"><span data-stu-id="3ea14-119">Passing Reference Types by Reference</span></span>  

 <span data-ttu-id="3ea14-120">下列範例與上述範例相同，差別在於 `ref` 關鍵字會新增方法標題和呼叫。</span><span class="sxs-lookup"><span data-stu-id="3ea14-120">The following example is the same as the previous example, except that the `ref` keyword is added to the method header and call.</span></span> <span data-ttu-id="3ea14-121">任何在方法中進行的變更會影響呼叫端程式中的原始變數。</span><span class="sxs-lookup"><span data-stu-id="3ea14-121">Any changes that take place in the method affect the original variable in the calling program.</span></span>  
  
 [!code-csharp[csProgGuideParameters#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#8)]  
  
 <span data-ttu-id="3ea14-122">方法內部進行的所有變更都會影響 `Main` 中的原始陣列。</span><span class="sxs-lookup"><span data-stu-id="3ea14-122">All of the changes that take place inside the method affect the original array in `Main`.</span></span> <span data-ttu-id="3ea14-123">事實上，原始陣列會使用 `new` 運算子重新配置。</span><span class="sxs-lookup"><span data-stu-id="3ea14-123">In fact, the original array is reallocated using the `new` operator.</span></span> <span data-ttu-id="3ea14-124">因此，在呼叫 `Change` 方法之後，所有對 `arr` 的參考都會指向在 `Change` 方法中建立的五個項目陣列。</span><span class="sxs-lookup"><span data-stu-id="3ea14-124">Thus, after calling the `Change` method, any reference to `arr` points to the five-element array, which is created in the `Change` method.</span></span>  
  
## <a name="swapping-two-strings"></a><span data-ttu-id="3ea14-125">交換兩個字串</span><span class="sxs-lookup"><span data-stu-id="3ea14-125">Swapping Two Strings</span></span>  

 <span data-ttu-id="3ea14-126">以傳址方式傳遞參考型別參數的絶佳範例就是交換字串。</span><span class="sxs-lookup"><span data-stu-id="3ea14-126">Swapping strings is a good example of passing reference-type parameters by reference.</span></span> <span data-ttu-id="3ea14-127">在此範例中，`str1` 和 `str2` 兩個字串會在 `Main` 中初始化，並作為 `ref` 關鍵字修改的參數傳遞給 `SwapStrings` 方法。</span><span class="sxs-lookup"><span data-stu-id="3ea14-127">In the example, two strings, `str1` and `str2`, are initialized in `Main` and passed to the `SwapStrings` method as parameters modified by the `ref` keyword.</span></span> <span data-ttu-id="3ea14-128">兩個字串也會在方法和 `Main` 內部交換。</span><span class="sxs-lookup"><span data-stu-id="3ea14-128">The two strings are swapped inside the method and inside `Main` as well.</span></span>  
  
 [!code-csharp[csProgGuideParameters#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#9)]  
  
 <span data-ttu-id="3ea14-129">在此範例中，參數需要以傳址方式傳遞以影響呼叫端程式中的變數。</span><span class="sxs-lookup"><span data-stu-id="3ea14-129">In this example, the parameters need to be passed by reference to affect the variables in the calling program.</span></span> <span data-ttu-id="3ea14-130">如果您移除了方法標頭和方法呼叫中的 `ref` 關鍵字，就不會在呼叫端程式中進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="3ea14-130">If you remove the `ref` keyword from both the method header and the method call, no changes will take place in the calling program.</span></span>  
  
 <span data-ttu-id="3ea14-131">如需字串的詳細資訊，請參閱 [string](../../language-reference/builtin-types/reference-types.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea14-131">For more information about strings, see [string](../../language-reference/builtin-types/reference-types.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3ea14-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3ea14-132">See also</span></span>

- [<span data-ttu-id="3ea14-133">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="3ea14-133">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="3ea14-134">傳遞參數</span><span class="sxs-lookup"><span data-stu-id="3ea14-134">Passing Parameters</span></span>](./passing-parameters.md)
- [<span data-ttu-id="3ea14-135">ref</span><span class="sxs-lookup"><span data-stu-id="3ea14-135">ref</span></span>](../../language-reference/keywords/ref.md)
- [<span data-ttu-id="3ea14-136">in</span><span class="sxs-lookup"><span data-stu-id="3ea14-136">in</span></span>](../../language-reference/keywords/in-parameter-modifier.md)
- [<span data-ttu-id="3ea14-137">out</span><span class="sxs-lookup"><span data-stu-id="3ea14-137">out</span></span>](../../language-reference/keywords/out.md)
- [<span data-ttu-id="3ea14-138">參考型別</span><span class="sxs-lookup"><span data-stu-id="3ea14-138">Reference Types</span></span>](../../language-reference/keywords/reference-types.md)
