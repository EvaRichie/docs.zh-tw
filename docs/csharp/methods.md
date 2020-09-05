---
title: 方法 - C# 手冊
description: 方法、方法參數和方法傳回值的概觀
ms.technology: csharp-fundamentals
ms.date: 05/21/2018
ms.assetid: 577a8527-1081-4b36-9b9e-0685b6553c6e
ms.openlocfilehash: 879c553f8df560a3e2f3dccdbbf0d7e8a05c50cd
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/05/2020
ms.locfileid: "89495534"
---
# <a name="methods-in-c"></a><span data-ttu-id="698de-103"> (c # 中的方法 ) </span><span class="sxs-lookup"><span data-stu-id="698de-103">Methods in (C#)</span></span>

<span data-ttu-id="698de-104">方法是包含一系列陳述式的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="698de-104">A method is a code block that contains a series of statements.</span></span> <span data-ttu-id="698de-105">程式會造成呼叫方法並指定任何所需的方法引數來執行陳述式。</span><span class="sxs-lookup"><span data-stu-id="698de-105">A program causes the statements to be executed by calling the method and specifying any required method arguments.</span></span> <span data-ttu-id="698de-106">在 C# 中，每個執行的指示是在方法的內容中執行。</span><span class="sxs-lookup"><span data-stu-id="698de-106">In C#, every executed instruction is performed in the context of a method.</span></span> <span data-ttu-id="698de-107">`Main` 方法是每個 C# 應用程式的進入點，而且它是由通用語言執行平台 (CLR) 啟動程式時呼叫。</span><span class="sxs-lookup"><span data-stu-id="698de-107">The `Main` method is the entry point for every C# application and it is called by the common language runtime (CLR) when the program is started.</span></span>

> [!NOTE]
> <span data-ttu-id="698de-108">本主題討論具名的方法。</span><span class="sxs-lookup"><span data-stu-id="698de-108">This topic discusses named methods.</span></span> <span data-ttu-id="698de-109">如需匿名函式的資訊，請參閱[匿名函式](programming-guide/statements-expressions-operators/anonymous-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="698de-109">For information about anonymous functions, see [Anonymous Functions](programming-guide/statements-expressions-operators/anonymous-functions.md).</span></span>

<a name="signatures"></a>

## <a name="method-signatures"></a><span data-ttu-id="698de-110">方法簽章</span><span class="sxs-lookup"><span data-stu-id="698de-110">Method signatures</span></span>

<span data-ttu-id="698de-111">指定下列項目以 `class` 或 `struct` 宣告方法：</span><span class="sxs-lookup"><span data-stu-id="698de-111">Methods are declared in a `class` or `struct` by specifying:</span></span>

- <span data-ttu-id="698de-112">選擇性的存取層級，例如 `public` 或 `private`。</span><span class="sxs-lookup"><span data-stu-id="698de-112">An optional access level, such as `public` or `private`.</span></span> <span data-ttu-id="698de-113">預設為 `private`。</span><span class="sxs-lookup"><span data-stu-id="698de-113">The default is `private`.</span></span>
- <span data-ttu-id="698de-114">選擇性修飾詞，例如 `abstract` 或 `sealed`。</span><span class="sxs-lookup"><span data-stu-id="698de-114">Optional modifiers such as `abstract` or `sealed`.</span></span>
- <span data-ttu-id="698de-115">傳回值，或如果方法為無，則為 `void`。</span><span class="sxs-lookup"><span data-stu-id="698de-115">The return value, or `void` if the method has none.</span></span>
- <span data-ttu-id="698de-116">方法名稱。</span><span class="sxs-lookup"><span data-stu-id="698de-116">The method name.</span></span>
- <span data-ttu-id="698de-117">任何方法參數。</span><span class="sxs-lookup"><span data-stu-id="698de-117">Any method parameters.</span></span> <span data-ttu-id="698de-118">方法參數會放在括號中，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="698de-118">Method parameters are enclosed in parentheses and are separated by commas.</span></span> <span data-ttu-id="698de-119">空括號表示方法不需要任何參數。</span><span class="sxs-lookup"><span data-stu-id="698de-119">Empty parentheses indicate that the method requires no parameters.</span></span>

<span data-ttu-id="698de-120">這些組件一起構成方法簽章。</span><span class="sxs-lookup"><span data-stu-id="698de-120">These parts together form the method signature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="698de-121">方法的傳回類型不是方法多載用途的方法簽章的一部分。</span><span class="sxs-lookup"><span data-stu-id="698de-121">A return type of a method is not part of the signature of the method for the purposes of method overloading.</span></span> <span data-ttu-id="698de-122">不過，在判斷委派與所指向的方法之間的相容性時，它是方法簽章的一部分。</span><span class="sxs-lookup"><span data-stu-id="698de-122">However, it is part of the signature of the method when determining the compatibility between a delegate and the method that it points to.</span></span>

<span data-ttu-id="698de-123">下例定義名為 `Motorcycle` 的類別，包含五個方法：</span><span class="sxs-lookup"><span data-stu-id="698de-123">The following example defines a class named `Motorcycle` that contains five methods:</span></span>

[!code-csharp[csSnippets.Methods#40](../../samples/snippets/csharp/concepts/methods/methods40.cs#40)]

<span data-ttu-id="698de-124">請注意，`Motorcycle` 類別包含多載方法 `Drive`。</span><span class="sxs-lookup"><span data-stu-id="698de-124">Note that the `Motorcycle` class includes an overloaded method, `Drive`.</span></span> <span data-ttu-id="698de-125">兩種方法有相同的名稱，但是必須依其參數型別區別。</span><span class="sxs-lookup"><span data-stu-id="698de-125">Two methods have the same name, but must be differentiated by their parameter types.</span></span>

<a name="invocation"></a>

## <a name="method-invocation"></a><span data-ttu-id="698de-126">方法引動過程</span><span class="sxs-lookup"><span data-stu-id="698de-126">Method invocation</span></span>

<span data-ttu-id="698de-127">方法可以是「執行個體」\*\* 或「靜態」\*\*。</span><span class="sxs-lookup"><span data-stu-id="698de-127">Methods can be either *instance* or *static*.</span></span> <span data-ttu-id="698de-128">叫用執行個體方法需要您具現化物件並針對該物件呼叫方法，執行個體方法會在該執行個體及資料上運作。</span><span class="sxs-lookup"><span data-stu-id="698de-128">Invoking an instance method requires that you instantiate an object and call the method on that object; an instance method operates on that instance and its data.</span></span> <span data-ttu-id="698de-129">您可以參考方法所屬的類型名稱來叫用靜態方法，靜態方法不操作執行個體資料。</span><span class="sxs-lookup"><span data-stu-id="698de-129">You invoke a static method by referencing the name of the type to which the method belongs; static methods do not operate on instance data.</span></span> <span data-ttu-id="698de-130">嘗試透過物件執行個體呼叫靜態方法會產生編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="698de-130">Attempting to call a static method through an object instance generates a compiler error.</span></span>

<span data-ttu-id="698de-131">呼叫方法就像是存取欄位。</span><span class="sxs-lookup"><span data-stu-id="698de-131">Calling a method is like accessing a field.</span></span> <span data-ttu-id="698de-132">在物件名稱後 (如果呼叫的是執行個體方法) 或型別名稱後 (如果呼叫的是 `static` 方法)，加上句點、方法名稱及括弧。</span><span class="sxs-lookup"><span data-stu-id="698de-132">After the object name (if you are calling an instance method) or the type name (if you are calling a `static` method), add a period, the name of the method, and parentheses.</span></span> <span data-ttu-id="698de-133">引數會在括號中列出，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="698de-133">Arguments are listed within the parentheses, and are separated by commas.</span></span>

<span data-ttu-id="698de-134">方法定義會指定所需的任何參數的名稱和類型。</span><span class="sxs-lookup"><span data-stu-id="698de-134">The method definition specifies the names and types of any parameters that are required.</span></span> <span data-ttu-id="698de-135">在呼叫端叫用方法時，它會針對每個參數提供具體值及呼叫的引數。</span><span class="sxs-lookup"><span data-stu-id="698de-135">When a caller invokes the method, it provides concrete values, called arguments, for each parameter.</span></span> <span data-ttu-id="698de-136">引數必須與參數型別相容，但在呼叫程式碼中使用的引數，其引數名稱不需要與方法中定義的具名參數相同。</span><span class="sxs-lookup"><span data-stu-id="698de-136">The arguments must be compatible with the parameter type, but the argument name, if one is used in the calling code, does not have to be the same as the parameter named defined in the method.</span></span> <span data-ttu-id="698de-137">在下例中，`Square` 方法包含名為 *i* 之 `int` 型別的單一參數。</span><span class="sxs-lookup"><span data-stu-id="698de-137">In the following example, the `Square` method includes a single parameter of type `int` named *i*.</span></span> <span data-ttu-id="698de-138">第一個方法呼叫會傳遞給 `Square` 方法型別 `int` 的 *num* 變數，第二個傳遞數值常數，第三個傳遞運算式。</span><span class="sxs-lookup"><span data-stu-id="698de-138">The first method call passes the `Square` method a variable of type `int` named *num*; the second, a numeric constant; and the third, an expression.</span></span>

[!code-csharp[csSnippets.Methods#74](../../samples/snippets/csharp/concepts/methods/params74.cs#74)]

<span data-ttu-id="698de-139">最常見的方法引動過程形式過去使用位置引數，現在則依方法參數的順序來提供引數。</span><span class="sxs-lookup"><span data-stu-id="698de-139">The most common form of method invocation used positional arguments; it supplies arguments in the same order as method parameters.</span></span> <span data-ttu-id="698de-140">因此可以如下列範例所示呼叫 `Motorcycle` 類別的方法。</span><span class="sxs-lookup"><span data-stu-id="698de-140">The methods of the `Motorcycle` class can therefore be called as in the following example.</span></span> <span data-ttu-id="698de-141">例如，呼叫 `Drive` 方法包含兩個引數，它們會對應至方法語法的兩個參數。</span><span class="sxs-lookup"><span data-stu-id="698de-141">The call to the `Drive` method, for example, includes two arguments that correspond to the two parameters in the method's syntax.</span></span> <span data-ttu-id="698de-142">第一個成為 `miles` 參數的值，第二個是 `speed` 參數的值。</span><span class="sxs-lookup"><span data-stu-id="698de-142">The first becomes the value of the `miles` parameter, the second the value of the `speed` parameter.</span></span>

[!code-csharp[csSnippets.Methods#41](../../samples/snippets/csharp/concepts/methods/methods40.cs#41)]

<span data-ttu-id="698de-143">叫用方法時，您也可以使用「具名引數」\*\*，而不是使用位置引數。</span><span class="sxs-lookup"><span data-stu-id="698de-143">You can also used *named arguments* instead of positional arguments when invoking a method.</span></span> <span data-ttu-id="698de-144">使用具名引數時，您指定參數名稱，後面接著冒號 (":") 和引數。</span><span class="sxs-lookup"><span data-stu-id="698de-144">When using named arguments, you specify the parameter name followed by a colon (":") and the argument.</span></span> <span data-ttu-id="698de-145">方法的引數會以任意順序出現，只要有所有必要的引數。</span><span class="sxs-lookup"><span data-stu-id="698de-145">Arguments to the method can appear in any order, as long as all required arguments are present.</span></span> <span data-ttu-id="698de-146">下例使用具名引數來叫用 `TestMotorcycle.Drive` 方法。</span><span class="sxs-lookup"><span data-stu-id="698de-146">The following example uses named arguments to invoke the `TestMotorcycle.Drive` method.</span></span> <span data-ttu-id="698de-147">本例中，具名引數的傳遞順序與方法參數清單的順序相反。</span><span class="sxs-lookup"><span data-stu-id="698de-147">In this example, the named arguments are passed in the opposite order from the method's parameter list.</span></span>

[!code-csharp[csSnippets.Methods#45](../../samples/snippets/csharp/concepts/methods/named1.cs#45)]

<span data-ttu-id="698de-148">您可以使用位置引數和具名引數來叫用方法。</span><span class="sxs-lookup"><span data-stu-id="698de-148">You can invoke a method using both positional arguments and named arguments.</span></span> <span data-ttu-id="698de-149">不過，當命名的引數位於正確位置時，位置引數只能跟在具名引數的後面。</span><span class="sxs-lookup"><span data-stu-id="698de-149">However, positional arguments can only follow named arguments when the named arguments are in the correct positions.</span></span> <span data-ttu-id="698de-150">下例會使用一個位置引數和一個具名引數，從前一個範例叫用 `TestMotorcycle.Drive` 方法。</span><span class="sxs-lookup"><span data-stu-id="698de-150">The following example invokes the `TestMotorcycle.Drive` method from the previous example using one positional argument and one named argument.</span></span>

[!code-csharp[csSnippets.Methods#46](../../samples/snippets/csharp/concepts/methods/named2.cs#46)]

<a name="inherited"></a>

## <a name="inherited-and-overridden-methods"></a><span data-ttu-id="698de-151">繼承和覆寫方法</span><span class="sxs-lookup"><span data-stu-id="698de-151">Inherited and overridden methods</span></span>

<span data-ttu-id="698de-152">除了在型別中明確定義的成員外，型別會繼承在其基底類別中定義的成員。</span><span class="sxs-lookup"><span data-stu-id="698de-152">In addition to the members that are explicitly defined in a type, a type inherits members defined in its base classes.</span></span> <span data-ttu-id="698de-153">因為受管理的類型系統中之所有類型，都是直接或間接繼承自 <xref:System.Object> 類別，所以所有的類型都會繼承其成員，例如 <xref:System.Object.Equals(System.Object)>、<xref:System.Object.GetType> 及 <xref:System.Object.ToString>。</span><span class="sxs-lookup"><span data-stu-id="698de-153">Since all types in the managed type system inherit directly or indirectly from the <xref:System.Object> class, all types inherit its members, such as <xref:System.Object.Equals(System.Object)>, <xref:System.Object.GetType>, and <xref:System.Object.ToString>.</span></span> <span data-ttu-id="698de-154">下例定義 `Person` 類別、具現化兩個 `Person` 物件，並呼叫 `Person.Equals` 方法以判斷兩個物件是否相等。</span><span class="sxs-lookup"><span data-stu-id="698de-154">The following example defines a `Person` class, instantiates two `Person` objects, and calls the `Person.Equals` method to determine whether the two objects are equal.</span></span> <span data-ttu-id="698de-155">但是 `Equals` 方法不是在 `Person` 類別中定義，它繼承自 <xref:System.Object>。</span><span class="sxs-lookup"><span data-stu-id="698de-155">The `Equals` method, however, is not defined in the `Person` class; it is inherited from <xref:System.Object>.</span></span>

[!code-csharp[csSnippets.Methods#104](../../samples/snippets/csharp/concepts/methods/inherited1.cs#104)]

<span data-ttu-id="698de-156">型別可以使用 `override` 關鍵字並提供覆寫方法的實作，來覆寫繼承的成員。</span><span class="sxs-lookup"><span data-stu-id="698de-156">Types can override inherited members by using the `override` keyword and providing an implementation for the overridden method.</span></span> <span data-ttu-id="698de-157">方法簽章必須與覆寫方法的簽章相同。</span><span class="sxs-lookup"><span data-stu-id="698de-157">The method signature must be the same as that of the overridden method.</span></span> <span data-ttu-id="698de-158">下例與前一範例相似，不同之處在於它會覆寫 <xref:System.Object.Equals(System.Object)> 方法。</span><span class="sxs-lookup"><span data-stu-id="698de-158">The following example is like the previous one, except that it overrides the <xref:System.Object.Equals(System.Object)> method.</span></span> <span data-ttu-id="698de-159">(它也會覆寫 <xref:System.Object.GetHashCode> 方法，因為兩種方法都是為了提供一致的結果。)</span><span class="sxs-lookup"><span data-stu-id="698de-159">(It also overrides the <xref:System.Object.GetHashCode> method, since the two methods are intended to provide consistent results.)</span></span>

[!code-csharp[csSnippets.Methods#105](../../samples/snippets/csharp/concepts/methods/overridden1.cs#105)]

<a name="passing"></a>

## <a name="passing-parameters"></a><span data-ttu-id="698de-160">傳遞參數</span><span class="sxs-lookup"><span data-stu-id="698de-160">Passing parameters</span></span>

<span data-ttu-id="698de-161">C# 中的類型為「實值型別」**「參考型別」**。</span><span class="sxs-lookup"><span data-stu-id="698de-161">Types in C# are either *value types* or *reference types*.</span></span> <span data-ttu-id="698de-162">如需內建實數值型別的清單，請參閱 [類型](./tour-of-csharp/types.md)。</span><span class="sxs-lookup"><span data-stu-id="698de-162">For a list of built-in value types, see [Types](./tour-of-csharp/types.md).</span></span> <span data-ttu-id="698de-163">根據預設，實值型別和參考型別都會以傳值方式傳遞至方法。</span><span class="sxs-lookup"><span data-stu-id="698de-163">By default, both value types and reference types are passed to a method by value.</span></span>

<a name="byval"></a>

### <a name="passing-parameters-by-value"></a><span data-ttu-id="698de-164">以傳值方式傳遞參數</span><span class="sxs-lookup"><span data-stu-id="698de-164">Passing parameters by value</span></span>

<span data-ttu-id="698de-165">以傳值方式將實值型別傳遞至方法時，會將物件複本而不是物件本身傳遞至方法。</span><span class="sxs-lookup"><span data-stu-id="698de-165">When a value type is passed to a method by value, a copy of the object instead of the object itself is passed to the method.</span></span> <span data-ttu-id="698de-166">因此，當控制回到呼叫端時，呼叫的方法中的物件變更不會影響原始物件。</span><span class="sxs-lookup"><span data-stu-id="698de-166">Therefore, changes to the object in the called method have no effect on the original object when control returns to the caller.</span></span>

<span data-ttu-id="698de-167">下例會以傳值方式將實值型別傳遞至方法，而呼叫的方法會嘗試變更實值型別的值。</span><span class="sxs-lookup"><span data-stu-id="698de-167">The following example passes a value type to a method by value, and the called method attempts to change the value type's value.</span></span> <span data-ttu-id="698de-168">它會定義 `int` 型別的變數 (它是實值型別)、將其值初始化為 20，再將它傳遞給名為 `ModifyValue` 的方法，此方法會將變數值變更為 30。</span><span class="sxs-lookup"><span data-stu-id="698de-168">It defines a variable of type `int`, which is a value type, initializes its value to 20, and passes it to a method named `ModifyValue` that changes the variable's value to 30.</span></span> <span data-ttu-id="698de-169">但傳回方法時，變數的值會維持不變。</span><span class="sxs-lookup"><span data-stu-id="698de-169">When the method returns, however, the variable's value remains unchanged.</span></span>

[!code-csharp[csSnippets.Methods#10](../../samples/snippets/csharp/concepts/methods/byvalue10.cs#10)]

<span data-ttu-id="698de-170">當參考型別的物件以傳值方式傳遞至方法時，就會以傳值方式傳遞物件參考。</span><span class="sxs-lookup"><span data-stu-id="698de-170">When an object of a reference type is passed to a method by value, a reference to the object is passed by value.</span></span> <span data-ttu-id="698de-171">也就是說，此方法接收的不是物件本身，而是指出物件位置的引數。</span><span class="sxs-lookup"><span data-stu-id="698de-171">That is, the method receives not the object itself, but an argument that indicates the location of the object.</span></span> <span data-ttu-id="698de-172">如果您使用此參考來變更物件成員，當控制回到呼叫方法時，變更即會反映在物件中。</span><span class="sxs-lookup"><span data-stu-id="698de-172">If you change a member of the object by using this reference, the change is reflected in the object when control returns to the calling method.</span></span> <span data-ttu-id="698de-173">不過，當控制回到呼叫端時，取代傳遞至方法的物件不會影響原始物件。</span><span class="sxs-lookup"><span data-stu-id="698de-173">However, replacing the object passed to the method has no effect on the original object when control returns to the caller.</span></span>

<span data-ttu-id="698de-174">下例會定義名為`SampleRefType` 的類別 (此為參考型別)。</span><span class="sxs-lookup"><span data-stu-id="698de-174">The following example defines a class (which is a reference type) named `SampleRefType`.</span></span> <span data-ttu-id="698de-175">它會具現化 `SampleRefType` 物件、將 44 指派給其 `value` 欄位，再將物件傳遞至 `ModifyObject` 方法。</span><span class="sxs-lookup"><span data-stu-id="698de-175">It instantiates a `SampleRefType` object, assigns 44 to its `value` field, and passes the object to the `ModifyObject` method.</span></span> <span data-ttu-id="698de-176">本例會執行基本上與上一個範例相同的動作，依傳值方式將引數傳遞至方法。</span><span class="sxs-lookup"><span data-stu-id="698de-176">This example does essentially the same thing as the previous example -- it passes an argument by value to a method.</span></span> <span data-ttu-id="698de-177">但因為使用了參考型別，所以結果會不同。</span><span class="sxs-lookup"><span data-stu-id="698de-177">But because a reference type is used, the result is different.</span></span> <span data-ttu-id="698de-178">在 `ModifyObject` 中對 `obj.value` 欄位的修改，也會將 `Main` 方法中引數 `rt` 的 `value` 欄位變更成 33，如範例輸出所示。</span><span class="sxs-lookup"><span data-stu-id="698de-178">The modification that is made in `ModifyObject` to the `obj.value` field also changes the `value` field of the argument, `rt`, in the `Main` method to 33, as the output from the example shows.</span></span>

[!code-csharp[csSnippets.Methods#42](../../samples/snippets/csharp/concepts/methods/byvalue42.cs#42)]

<a name="byref"></a>

### <a name="passing-parameters-by-reference"></a><span data-ttu-id="698de-179">以傳址方式傳遞參數</span><span class="sxs-lookup"><span data-stu-id="698de-179">Passing parameters by reference</span></span>

<span data-ttu-id="698de-180">當您想要變更方法中的引數值，且想要在控制回到呼叫方法時反映該變更時，您必須以傳址方式傳遞參數。</span><span class="sxs-lookup"><span data-stu-id="698de-180">You pass a parameter by reference when you want to change the value of an argument in a method and want to reflect that change when control returns to the calling method.</span></span> <span data-ttu-id="698de-181">若要以傳址方式傳遞參數，請使用 [`ref`](language-reference/keywords/ref.md) 或 [`out`](language-reference/keywords/out-parameter-modifier.md) 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="698de-181">To pass a parameter by reference, you use the [`ref`](language-reference/keywords/ref.md) or [`out`](language-reference/keywords/out-parameter-modifier.md) keyword.</span></span> <span data-ttu-id="698de-182">您也可以使用傳址方式傳遞值，以避免複製但仍使用關鍵字防止修改 [`in`](language-reference/keywords/in-parameter-modifier.md) 。</span><span class="sxs-lookup"><span data-stu-id="698de-182">You can also pass a value by reference to avoid copying but still prevent modifications using the [`in`](language-reference/keywords/in-parameter-modifier.md) keyword.</span></span>

<span data-ttu-id="698de-183">下例與前例相同，唯一差異是值以傳址方式傳遞至 `ModifyValue` 方法。</span><span class="sxs-lookup"><span data-stu-id="698de-183">The following example is identical to the previous one, except the value is passed by reference to the `ModifyValue` method.</span></span> <span data-ttu-id="698de-184">在 `ModifyValue` 方法中修改參數值時，當控制回到呼叫端時會反映值的變更。</span><span class="sxs-lookup"><span data-stu-id="698de-184">When the value of the parameter is modified in the `ModifyValue` method, the change in value is reflected when control returns to the caller.</span></span>

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/byref106.cs#106)]

<span data-ttu-id="698de-185">依 ref 參數使用的常見模式包含交換變數值。</span><span class="sxs-lookup"><span data-stu-id="698de-185">A common pattern that uses by ref parameters involves swapping the values of variables.</span></span> <span data-ttu-id="698de-186">您以傳址方式將兩個變數傳遞至方法，且該方法會交換其內容。</span><span class="sxs-lookup"><span data-stu-id="698de-186">You pass two variables to a method by reference, and the method swaps their contents.</span></span> <span data-ttu-id="698de-187">下例會交換整數值。</span><span class="sxs-lookup"><span data-stu-id="698de-187">The following example swaps integer values.</span></span>

[!code-csharp[csSnippets.Methods#106](../../samples/snippets/csharp/concepts/methods/swap107.cs#107)]

<span data-ttu-id="698de-188">傳遞參考型別參數可讓您變更參考本身的值，而不是其個別項目或欄位的值。</span><span class="sxs-lookup"><span data-stu-id="698de-188">Passing a reference-type parameter allows you to change the value of the reference itself, rather than the value of its individual elements or fields.</span></span>

<a name="paramarray"></a>

### <a name="parameter-arrays"></a><span data-ttu-id="698de-189">參數陣列</span><span class="sxs-lookup"><span data-stu-id="698de-189">Parameter arrays</span></span>

<span data-ttu-id="698de-190">有時候，指定方法之引數確切數目的需求會有限制。</span><span class="sxs-lookup"><span data-stu-id="698de-190">Sometimes, the requirement that you specify the exact number of arguments to your method is restrictive.</span></span> <span data-ttu-id="698de-191">使用 `params` 關鍵字指出某參數是參數陣列，可使用數目可變的引數來呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="698de-191">By using the `params` keyword to indicate that a parameter is a parameter array, you allow your method to be called with a variable number of arguments.</span></span> <span data-ttu-id="698de-192">以 `params` 關鍵字標記的參數必須是陣列型別，而且必須是方法參數清單中的最後一個參數。</span><span class="sxs-lookup"><span data-stu-id="698de-192">The parameter tagged with the `params` keyword must be an array type, and it must be the last parameter in the method's parameter list.</span></span>

<span data-ttu-id="698de-193">然後呼叫端以下列三種方式之一來叫用方法︰</span><span class="sxs-lookup"><span data-stu-id="698de-193">A caller can then invoke the method in either of three ways:</span></span>

- <span data-ttu-id="698de-194">傳遞包含所需項目數目的適當型別陣列。</span><span class="sxs-lookup"><span data-stu-id="698de-194">By passing an array of the appropriate type that contains the desired number of elements.</span></span>
- <span data-ttu-id="698de-195">將適當型別各個引數的逗點分隔清單傳遞給方法。</span><span class="sxs-lookup"><span data-stu-id="698de-195">By passing a comma-separated list of individual arguments of the appropriate type to the method.</span></span>
- <span data-ttu-id="698de-196">不提供引數給參數陣列。</span><span class="sxs-lookup"><span data-stu-id="698de-196">By not providing an argument to the parameter array.</span></span>

<span data-ttu-id="698de-197">下列範例會定義能從參數陣列中傳回所有母音，名為 `GetVowels` 的方法。</span><span class="sxs-lookup"><span data-stu-id="698de-197">The following example defines a method named `GetVowels` that returns all the vowels from a parameter array.</span></span> <span data-ttu-id="698de-198">`Main` 方法會示範這三種叫用方法的方式。</span><span class="sxs-lookup"><span data-stu-id="698de-198">The `Main` method illustrates all three ways of invoking the method.</span></span> <span data-ttu-id="698de-199">呼叫者不需要針對包含 `params` 修飾詞的參數提供任何引數。</span><span class="sxs-lookup"><span data-stu-id="698de-199">Callers are not required to supply any arguments for parameters that include the `params` modifier.</span></span> <span data-ttu-id="698de-200">在此情況下，參數會是 `null`。</span><span class="sxs-lookup"><span data-stu-id="698de-200">In that case, the parameter is `null`.</span></span>

[!code-csharp[csSnippets.Methods#75](~/samples/snippets/csharp/concepts/methods/params75.cs#75)]

<a name="optional"></a>

## <a name="optional-parameters-and-arguments"></a><span data-ttu-id="698de-201">選擇性參數和引數</span><span class="sxs-lookup"><span data-stu-id="698de-201">Optional parameters and arguments</span></span>

<span data-ttu-id="698de-202">方法定義可以指定其參數為必要項目或選擇項目。</span><span class="sxs-lookup"><span data-stu-id="698de-202">A method definition can specify that its parameters are required or that they are optional.</span></span> <span data-ttu-id="698de-203">根據預設，參數為必要項目。</span><span class="sxs-lookup"><span data-stu-id="698de-203">By default, parameters are required.</span></span> <span data-ttu-id="698de-204">在方法定義中包含參數的預設值即可指定選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="698de-204">Optional parameters are specified by including the parameter's default value in the method definition.</span></span> <span data-ttu-id="698de-205">呼叫此方法時，如不為選擇性參數提供任何引數，則改用預設值。</span><span class="sxs-lookup"><span data-stu-id="698de-205">When the method is called, if no argument is supplied for an optional parameter, the default value is used instead.</span></span>

<span data-ttu-id="698de-206">參數的預設值必須由下列運算式種類之一指派︰</span><span class="sxs-lookup"><span data-stu-id="698de-206">The parameter's default value must be assigned by one of the following kinds of expressions:</span></span>

- <span data-ttu-id="698de-207">常數，例如常值字串或數字。</span><span class="sxs-lookup"><span data-stu-id="698de-207">A constant, such as a literal string or number.</span></span>
- <span data-ttu-id="698de-208">`new ValType()` 形式的運算式，其中 `ValType` 是實值型別。</span><span class="sxs-lookup"><span data-stu-id="698de-208">An expression of the form `new ValType()`, where `ValType` is a value type.</span></span> <span data-ttu-id="698de-209">請注意，這會叫用實值型別的隱含無參數建構函式，它不是該型別的實際成員。</span><span class="sxs-lookup"><span data-stu-id="698de-209">Note that this invokes the value type's implicit parameterless constructor, which is not an actual member of the type.</span></span>
- <span data-ttu-id="698de-210">`default(ValType)` 形式的運算式，其中 `ValType` 是實值型別。</span><span class="sxs-lookup"><span data-stu-id="698de-210">An expression of the form `default(ValType)`, where `ValType` is a value type.</span></span>

<span data-ttu-id="698de-211">如果方法同時包含必要和選擇性參數，則選擇性參數會定義在參數清單結尾，在所有必要參數的後面。</span><span class="sxs-lookup"><span data-stu-id="698de-211">If a method includes both required and optional parameters, optional parameters are defined at the end of the parameter list, after all required parameters.</span></span>

<span data-ttu-id="698de-212">下例會定義 `ExampleMethod` 方法，它有一個必要參數和兩個選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="698de-212">The following example defines a method, `ExampleMethod`, that has one required and two optional parameters.</span></span>

[!code-csharp[csSnippets.Methods#21](../../samples/snippets/csharp/concepts/methods/optional1.cs#21)]

<span data-ttu-id="698de-213">如果使用位置引數叫用了有多個選擇性引數的方法，則呼叫端必須為所有選擇性參數提供引數，從第一個到最後一個。</span><span class="sxs-lookup"><span data-stu-id="698de-213">If a method with multiple optional arguments is invoked using positional arguments, the caller must supply an argument for all optional parameters from the first one to the last one for which an argument is supplied.</span></span> <span data-ttu-id="698de-214">以 `ExampleMethod` 方法為例，當呼叫端為 `description` 參數提供引數時，它也必須為 `optionalInt` 參數提供一個引數。</span><span class="sxs-lookup"><span data-stu-id="698de-214">In the case of the  `ExampleMethod` method, for example, if the caller supplies an argument for the `description` parameter, it must also supply one for the `optionalInt` parameter.</span></span> <span data-ttu-id="698de-215">`opt.ExampleMethod(2, 2, "Addition of 2 and 2");` 是有效的方法呼叫，而 `opt.ExampleMethod(2, , "Addition of 2 and 0");` 會產生「引數遺失」編譯器錯誤。</span><span class="sxs-lookup"><span data-stu-id="698de-215">`opt.ExampleMethod(2, 2, "Addition of 2 and 2");` is a valid method call; `opt.ExampleMethod(2, , "Addition of 2 and 0");` generates an "Argument missing" compiler error.</span></span>

<span data-ttu-id="698de-216">如果使用具名引數或位置和具名引數的組合來呼叫方法，則呼叫端可以省略方法呼叫中最後一個位置引數之後的任何引數。</span><span class="sxs-lookup"><span data-stu-id="698de-216">If a method is called using named arguments or a combination of positional and named arguments, the caller can omit any arguments that follow the last positional argument in the method call.</span></span>

<span data-ttu-id="698de-217">下例呼叫三次 `ExampleMethod` 方法。</span><span class="sxs-lookup"><span data-stu-id="698de-217">The following example calls the `ExampleMethod` method three times.</span></span>  <span data-ttu-id="698de-218">前兩個方法呼叫使用位置引數。</span><span class="sxs-lookup"><span data-stu-id="698de-218">The first two method calls use positional arguments.</span></span> <span data-ttu-id="698de-219">第一個省略了這兩個選擇性引數，而第二個省略了最後一個引數。</span><span class="sxs-lookup"><span data-stu-id="698de-219">The first omits both optional arguments, while the second omits the last argument.</span></span> <span data-ttu-id="698de-220">第三個方法呼叫提供了必要參數的位置引數，但在使用具名引數將值提供給 `description` 參數時省略 `optionalInt` 引數。</span><span class="sxs-lookup"><span data-stu-id="698de-220">The third method call supplies a positional argument for the required parameter, but uses a named argument to supply a value to the `description` parameter while omitting the `optionalInt` argument.</span></span>

[!code-csharp[csSnippets.Methods#22](../../samples/snippets/csharp/concepts/methods/optional1.cs#22)]

<span data-ttu-id="698de-221">使用選擇性參數會影響「多載解析」\*\*，或 C# 編譯器判斷依方法呼叫應叫用哪個特定多載的方式，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="698de-221">The use of optional parameters affects *overload resolution*, or the way in which the C# compiler determines which particular overload should be invoked by a method call, as follows:</span></span>

- <span data-ttu-id="698de-222">如果每個參數都是選擇性或為依名稱或位置對應要呼叫之陳述式的單一引數，且該引數可以轉換成參數的型別，則方法、索引子或建構函式就是執行的候選項目。</span><span class="sxs-lookup"><span data-stu-id="698de-222">A method, indexer, or constructor is a candidate for execution if each of its parameters either is optional or corresponds, by name or by position, to a single argument in the calling statement, and that argument can be converted to the type of the parameter.</span></span>
- <span data-ttu-id="698de-223">如果找到多個候選項目，則慣用轉換的多載解析規則會套用至明確指定的引數。</span><span class="sxs-lookup"><span data-stu-id="698de-223">If more than one candidate is found, overload resolution rules for preferred conversions are applied to the arguments that are explicitly specified.</span></span> <span data-ttu-id="698de-224">會忽略選擇性參數的省略引數。</span><span class="sxs-lookup"><span data-stu-id="698de-224">Omitted arguments for optional parameters are ignored.</span></span>
- <span data-ttu-id="698de-225">如果兩個候選項目的評斷結果一樣好，則偏向沒有選擇性參數的候選項目，其會在呼叫中省略引數。</span><span class="sxs-lookup"><span data-stu-id="698de-225">If two candidates are judged to be equally good, preference goes to a candidate that does not have optional parameters for which arguments were omitted in the call.</span></span> <span data-ttu-id="698de-226">這是多載解析一般偏好參數較少之候選項目的結果。</span><span class="sxs-lookup"><span data-stu-id="698de-226">This is a consequence of a general preference in overload resolution for candidates that have fewer parameters.</span></span>

<a name="return"></a>

## <a name="return-values"></a><span data-ttu-id="698de-227">傳回值</span><span class="sxs-lookup"><span data-stu-id="698de-227">Return values</span></span>

<span data-ttu-id="698de-228">方法可以傳回值給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="698de-228">Methods can return a value to the caller.</span></span> <span data-ttu-id="698de-229">針對傳回型別，如果列在方法名稱前面的型別不是 `void`，則方法可以使用 `return` 關鍵字傳回值。</span><span class="sxs-lookup"><span data-stu-id="698de-229">If the return type (the type listed before the method name) is not `void`, the method can return the value by using the `return` keyword.</span></span> <span data-ttu-id="698de-230">在 `return` 關鍵字後面接著符合傳回型別的變數、常數或運算式的陳述式，會將該值傳回給方法呼叫端。</span><span class="sxs-lookup"><span data-stu-id="698de-230">A statement with the `return` keyword followed by a variable, constant, or expression that matches the return type will return that value to the method caller.</span></span> <span data-ttu-id="698de-231">具有非 void 傳回類型的方法需要使用 `return` 關鍵字以傳回值。</span><span class="sxs-lookup"><span data-stu-id="698de-231">Methods with a non-void return type are required to use the `return` keyword to return a value.</span></span> <span data-ttu-id="698de-232">`return` 關鍵字也會停止執行方法。</span><span class="sxs-lookup"><span data-stu-id="698de-232">The `return` keyword also stops the execution of the method.</span></span>

<span data-ttu-id="698de-233">如果傳回類型為 `void`，不含值的 `return` 陳述式對於停止方法的執行仍很有用。</span><span class="sxs-lookup"><span data-stu-id="698de-233">If the return type is `void`, a `return` statement without a value is still useful to stop the execution of the method.</span></span> <span data-ttu-id="698de-234">若沒有 `return` 關鍵字，在方法到達程式碼區塊的結尾時，方法將會停止執行。</span><span class="sxs-lookup"><span data-stu-id="698de-234">Without the `return` keyword, the method will stop executing when it reaches the end of the code block.</span></span>

<span data-ttu-id="698de-235">例如，這兩種方法使用 `return` 關鍵字傳回整數：</span><span class="sxs-lookup"><span data-stu-id="698de-235">For example, these two methods use the `return` keyword to return integers:</span></span>

[!code-csharp[csSnippets.Methods#44](../../samples/snippets/csharp/concepts/methods/return44.cs#44)]

<span data-ttu-id="698de-236">若要使用從方法傳回的值，呼叫方法可以在使用相同類型值的任意位置使用方法呼叫本身即已足夠。</span><span class="sxs-lookup"><span data-stu-id="698de-236">To use a value returned from a method, the calling method can use the method call itself anywhere a value of the same type would be sufficient.</span></span> <span data-ttu-id="698de-237">您也可以指派傳回值給變數。</span><span class="sxs-lookup"><span data-stu-id="698de-237">You can also assign the return value to a variable.</span></span> <span data-ttu-id="698de-238">例如，下列兩個程式碼範例會達到相同的目標：</span><span class="sxs-lookup"><span data-stu-id="698de-238">For example, the following two code examples accomplish the same goal:</span></span>

[!code-csharp[csSnippets.Methods#45](../../samples/snippets/csharp/concepts/methods/return44.cs#45)]

[!code-csharp[csSnippets.Methods#46](../../samples/snippets/csharp/concepts/methods/return44.cs#46)]

<span data-ttu-id="698de-239">使用區域變數，在此情況下的 `result`來儲存值是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="698de-239">Using a local variable, in this case, `result`, to store a value is optional.</span></span> <span data-ttu-id="698de-240">它有助於程式碼的可讀性，或如果您需要儲存方法的整個範圍引數的原始值，則可能為必要。</span><span class="sxs-lookup"><span data-stu-id="698de-240">It may help the readability of the code, or it may be necessary if you need to store the original value of the argument for the entire scope of the method.</span></span>

<span data-ttu-id="698de-241">有時候，您希望自己的方法傳回的不止單一值。</span><span class="sxs-lookup"><span data-stu-id="698de-241">Sometimes, you want your method to return more than a single value.</span></span> <span data-ttu-id="698de-242">從 C# 7.0 開始，您可以使用「Tuple 型別」\*\* 和「Tuple 常值」\*\* 輕鬆達到這個目標。</span><span class="sxs-lookup"><span data-stu-id="698de-242">Starting with C# 7.0, you can do this easily by using *tuple types* and *tuple literals*.</span></span> <span data-ttu-id="698de-243">Tuple 型別會定義 Tuple 項目的資料類型。</span><span class="sxs-lookup"><span data-stu-id="698de-243">The tuple type defines the data types of the tuple's elements.</span></span> <span data-ttu-id="698de-244">Tuple 常值會提供傳回 Tuple 的實際值。</span><span class="sxs-lookup"><span data-stu-id="698de-244">Tuple literals provide the actual values of the returned tuple.</span></span> <span data-ttu-id="698de-245">在下列範例中，`(string, string, string, int)` 會定義由 `GetPersonalInfo` 方法所傳回的 Tuple 類型。</span><span class="sxs-lookup"><span data-stu-id="698de-245">In the following example, `(string, string, string, int)` defines the tuple type that is returned by the `GetPersonalInfo` method.</span></span> <span data-ttu-id="698de-246">運算式 `(per.FirstName, per.MiddleName, per.LastName, per.Age)` 是 Tuple 常值，方法會傳回 `PersonInfo` 物件的名字、中間名和姓氏以及年齡。</span><span class="sxs-lookup"><span data-stu-id="698de-246">The expression `(per.FirstName, per.MiddleName, per.LastName, per.Age)` is the tuple literal; the method returns the first, middle, and last name, along with the age, of a `PersonInfo` object.</span></span>

```csharp
public (string, string, string, int) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

<span data-ttu-id="698de-247">然後呼叫端使用傳回的 Tuple 及程式碼，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="698de-247">The caller can then consume the returned tuple with code like the following:</span></span>

```csharp
var person = GetPersonalInfo("111111111")
Console.WriteLine("{person.Item1} {person.Item3}: age = {person.Item4}");
```

<span data-ttu-id="698de-248">在 Tuple 型別定義中也可以將名稱指派給 Tuple 項目。</span><span class="sxs-lookup"><span data-stu-id="698de-248">Names can also be assigned to the tuple elements in the tuple type definition.</span></span> <span data-ttu-id="698de-249">下例示範使用具名項目的 `GetPersonalInfo` 方法替代版本：</span><span class="sxs-lookup"><span data-stu-id="698de-249">The following example shows an alternate version of the `GetPersonalInfo` method that uses named elements:</span></span>

```csharp
public (string FName, string MName, string LName, int Age) GetPersonalInfo(string id)
{
    PersonInfo per = PersonInfo.RetrieveInfoById(id);
    return (per.FirstName, per.MiddleName, per.LastName, per.Age);
}
```

<span data-ttu-id="698de-250">前一次的 `GetPersonInfo` 方法呼叫可修改如下︰</span><span class="sxs-lookup"><span data-stu-id="698de-250">The previous call to the `GetPersonInfo` method can then be modified as follows:</span></span>

```csharp
var person = GetPersonalInfo("111111111");
Console.WriteLine("{person.FName} {person.LName}: age = {person.Age}");
```

<span data-ttu-id="698de-251">如果方法將陣列當作引數傳遞並修改個別項目的值，方法就不需要傳回陣列，雖然您可選擇這樣做以取得良好的值樣式或功能性流程。</span><span class="sxs-lookup"><span data-stu-id="698de-251">If a method is passed an array as an argument and modifies the value of individual elements, it is not necessary for the method to return the array, although you may choose to do so for good style or functional flow of values.</span></span>  <span data-ttu-id="698de-252">這是因為 C# 會以傳值方式傳遞所有的參考型別，而陣列參考的值是陣列的指標。</span><span class="sxs-lookup"><span data-stu-id="698de-252">This is because C# passes all reference types by value, and the value of an array reference is the pointer to the array.</span></span> <span data-ttu-id="698de-253">在下例中，以 `DoubleValues` 方法完成的 `values` 陣列內容變更，都可透過任何具有陣列參考的程式碼觀察到。</span><span class="sxs-lookup"><span data-stu-id="698de-253">In the following example, changes to the contents of the `values` array that are made in the `DoubleValues` method are observable by any code that has a reference to the array.</span></span>

[!code-csharp[csSnippets.Methods#101](../../samples/snippets/csharp/concepts/methods/returnarray1.cs#101)]

<a name="extension"></a>

## <a name="extension-methods"></a><span data-ttu-id="698de-254">擴充方法</span><span class="sxs-lookup"><span data-stu-id="698de-254">Extension methods</span></span>

<span data-ttu-id="698de-255">一般來說，有兩種方式可將方法加入至現有的型別︰</span><span class="sxs-lookup"><span data-stu-id="698de-255">Ordinarily, there are two ways to add a method to an existing type:</span></span>

- <span data-ttu-id="698de-256">修改該型別的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="698de-256">Modify the source code for that type.</span></span> <span data-ttu-id="698de-257">如果您未擁有型別的原始程式碼，當然就無法這樣做。</span><span class="sxs-lookup"><span data-stu-id="698de-257">You cannot do this, of course, if you do not own the type's source code.</span></span> <span data-ttu-id="698de-258">而如果您同時新增任何私用資料欄位以支援方法，這會成為一項重大變更。</span><span class="sxs-lookup"><span data-stu-id="698de-258">And this becomes a breaking change if you also add any private data fields to support the method.</span></span>
- <span data-ttu-id="698de-259">在衍生類別中定義新的方法。</span><span class="sxs-lookup"><span data-stu-id="698de-259">Define the new method in a derived class.</span></span> <span data-ttu-id="698de-260">方法不能以使用其他型別繼承的這種方式新增，例如結構和列舉。</span><span class="sxs-lookup"><span data-stu-id="698de-260">A method cannot be added in this way using inheritance for other types, such as structures and enumerations.</span></span> <span data-ttu-id="698de-261">也不能用來將方法「新增」至密封的類別。</span><span class="sxs-lookup"><span data-stu-id="698de-261">Nor can it be used to "add" a method to a sealed class.</span></span>

<span data-ttu-id="698de-262">擴充方法可讓您將方法「新增」至現有的類型，但不必修改型別本身或在繼承的型別中實作新方法。</span><span class="sxs-lookup"><span data-stu-id="698de-262">Extension methods let you "add" a method to an existing type without modifying the type itself or implementing the new method in an inherited type.</span></span> <span data-ttu-id="698de-263">擴充方法也不必和其擴充型別位於相同的組件中。</span><span class="sxs-lookup"><span data-stu-id="698de-263">The extension method also does not have to reside in the same assembly as the type it extends.</span></span> <span data-ttu-id="698de-264">呼叫擴充方法就像它是型別的定義成員一樣。</span><span class="sxs-lookup"><span data-stu-id="698de-264">You call an extension method as if it were a defined member of a type.</span></span>

<span data-ttu-id="698de-265">如需詳細資訊，請參閱[擴充方法](programming-guide/classes-and-structs/extension-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="698de-265">For more information, see [Extension Methods](programming-guide/classes-and-structs/extension-methods.md).</span></span>

<a name="async"></a>

## <a name="async-methods"></a><span data-ttu-id="698de-266">非同步方法</span><span class="sxs-lookup"><span data-stu-id="698de-266">Async Methods</span></span>

<span data-ttu-id="698de-267">使用非同步功能，您就可以呼叫非同步方法，而不需要使用明確回呼或手動將您的程式碼分散到多種方法或 lambda 運算式上。</span><span class="sxs-lookup"><span data-stu-id="698de-267">By using the async feature, you can invoke asynchronous methods without using explicit callbacks or manually splitting your code across multiple methods or lambda expressions.</span></span>

<span data-ttu-id="698de-268">如果您使用 [async](language-reference/keywords/async.md) 修飾詞來標示方法，可以在方法中使用 [await](language-reference/operators/await.md) 運算子。</span><span class="sxs-lookup"><span data-stu-id="698de-268">If you mark a method with the [async](language-reference/keywords/async.md) modifier, you can use the [await](language-reference/operators/await.md) operator in the method.</span></span> <span data-ttu-id="698de-269">當控制項到達 async 方法的 `await` 運算式時，如果等候的工作未完成，控制會回到呼叫端，而有 `await` 關鍵字之方法中的進度會暫停，直到等候的工作完成。</span><span class="sxs-lookup"><span data-stu-id="698de-269">When control reaches an `await` expression in the async method, control returns to the caller if the awaited task is not completed, and progress in the method with the `await` keyword is suspended until the awaited task completes.</span></span> <span data-ttu-id="698de-270">當工作完成時，方法中的執行可以繼續。</span><span class="sxs-lookup"><span data-stu-id="698de-270">When the task is complete, execution can resume in the method.</span></span>

> [!NOTE]
> <span data-ttu-id="698de-271">非同步方法會在遇到第一個尚未完成的等候物件，或到達非同步方法的結尾（以先發生者為准）時，傳回給呼叫端。</span><span class="sxs-lookup"><span data-stu-id="698de-271">An async method returns to the caller when either it encounters the first awaited object that's not yet complete or it gets to the end of the async method, whichever occurs first.</span></span>

<span data-ttu-id="698de-272">非同步方法可以有 <xref:System.Threading.Tasks.Task%601>、<xref:System.Threading.Tasks.Task> 或 `void` 的傳回類型。</span><span class="sxs-lookup"><span data-stu-id="698de-272">An async method can have a return type of <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.Task>, or `void`.</span></span> <span data-ttu-id="698de-273">`void` 傳回型別主要用於定義需要 `void` 傳回型別的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="698de-273">The `void` return type is used primarily to define event handlers, where a `void` return type is required.</span></span> <span data-ttu-id="698de-274">傳回 `void` 的非同步方法無法等候，而且 void 傳回方法的呼叫端無法攔截方法擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="698de-274">An async method that returns `void` can't be awaited, and the caller of a void-returning method can't catch exceptions that the method throws.</span></span> <span data-ttu-id="698de-275">從 C# 7.0 開始，非同步方法可具備[任何類似工作的傳回類型](./whats-new/csharp-7.md#generalized-async-return-types)。</span><span class="sxs-lookup"><span data-stu-id="698de-275">Starting with C# 7.0, an async method can have [any task-like return type](./whats-new/csharp-7.md#generalized-async-return-types).</span></span>

<span data-ttu-id="698de-276">在下例中，`DelayAsync` 是包含會傳回整數之 return 陳述式的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="698de-276">In the following example, `DelayAsync` is an async method that has a return statement that returns an integer.</span></span> <span data-ttu-id="698de-277">因為它是非同步方法，所以其方法宣告必須有傳回型別 `Task<int>`。</span><span class="sxs-lookup"><span data-stu-id="698de-277">Because it is an async method, its method declaration must have a return type of `Task<int>`.</span></span> <span data-ttu-id="698de-278">因為傳回型別是 `Task<int>`，所以 `DoSomethingAsync` 中 `await` 運算式的評估會產生整數，如下列 `int result = await delayTask` 陳述式所示。</span><span class="sxs-lookup"><span data-stu-id="698de-278">Because the return type is `Task<int>`, the evaluation of the `await` expression in `DoSomethingAsync` produces an integer, as the following `int result = await delayTask` statement demonstrates.</span></span>

:::code language="csharp" source="programming-guide/classes-and-structs/snippets/classes-and-structs/methods/Program.cs":::

<span data-ttu-id="698de-279">非同步方法不可以宣告任何 [in](language-reference/keywords/in-parameter-modifier.md)、[ref](language-reference/keywords/ref.md) 或 [out](language-reference/keywords/out-parameter-modifier.md) 參數，但是可以呼叫具有這類參數的方法。</span><span class="sxs-lookup"><span data-stu-id="698de-279">An async method can't declare any [in](language-reference/keywords/in-parameter-modifier.md), [ref](language-reference/keywords/ref.md), or [out](language-reference/keywords/out-parameter-modifier.md) parameters, but it can call methods that have such parameters.</span></span>

 <span data-ttu-id="698de-280">如需非同步方法的詳細資訊，請參閱 [使用 async 和 await 進行非同步程式設計](async.md) 和非同步傳回 [類型](programming-guide/concepts/async/async-return-types.md)。</span><span class="sxs-lookup"><span data-stu-id="698de-280">For more information about async methods, see [Asynchronous programming with async and await](async.md) and [Async return types](programming-guide/concepts/async/async-return-types.md).</span></span>

<a name="expr"></a>

## <a name="expression-bodied-members"></a><span data-ttu-id="698de-281">運算式主體成員</span><span class="sxs-lookup"><span data-stu-id="698de-281">Expression-bodied members</span></span>

<span data-ttu-id="698de-282">方法定義只是立即傳回運算式的結果，或是具有單一陳述式做為方法的主體是很常見的。</span><span class="sxs-lookup"><span data-stu-id="698de-282">It is common to have method definitions that simply return immediately with the result of an expression, or that have a single statement as the body of the method.</span></span>  <span data-ttu-id="698de-283">使用 `=>`定義這類方法有個語法捷徑：</span><span class="sxs-lookup"><span data-stu-id="698de-283">There is a syntax shortcut for defining such methods using `=>`:</span></span>

```csharp
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);
```

<span data-ttu-id="698de-284">如果方法傳回 `void` 或為非同步方法，則方法的主體必須是陳述式運算式 (如同 Lambda)。</span><span class="sxs-lookup"><span data-stu-id="698de-284">If the method returns `void` or is an async method, the body of the method must be a statement expression (same as with lambdas).</span></span>  <span data-ttu-id="698de-285">針對屬性和索引子，它們必須是唯讀，而且您不會使用 `get` 存取子關鍵字。</span><span class="sxs-lookup"><span data-stu-id="698de-285">For properties and indexers, they must be read-only, and you do not use the `get` accessor keyword.</span></span>

<a name="iterators"></a>

## <a name="iterators"></a><span data-ttu-id="698de-286">迭代器</span><span class="sxs-lookup"><span data-stu-id="698de-286">Iterators</span></span>

<span data-ttu-id="698de-287">迭代器會對集合執行自訂的反覆項目，例如清單或陣列。</span><span class="sxs-lookup"><span data-stu-id="698de-287">An iterator performs a custom iteration over a collection, such as a list or an array.</span></span> <span data-ttu-id="698de-288">迭代器會使用 [yield return](language-reference/keywords/yield.md) 陳述式來一次傳回一個項目。</span><span class="sxs-lookup"><span data-stu-id="698de-288">An iterator uses the [yield return](language-reference/keywords/yield.md) statement to return each element one at a time.</span></span> <span data-ttu-id="698de-289">達到 `yield return` 陳述式時，即會記住目前的位置，讓呼叫端可以要求序列中的下一個項目。</span><span class="sxs-lookup"><span data-stu-id="698de-289">When a `yield return` statement is reached, the current location is remembered so that the caller can request the next element in the sequence.</span></span>

<span data-ttu-id="698de-290">迭代器的傳回類型可以是 <xref:System.Collections.IEnumerable>、 <xref:System.Collections.Generic.IEnumerable%601>、 <xref:System.Collections.IEnumerator>或 <xref:System.Collections.Generic.IEnumerator%601>。</span><span class="sxs-lookup"><span data-stu-id="698de-290">The return type of an iterator can be <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, or <xref:System.Collections.Generic.IEnumerator%601>.</span></span>

<span data-ttu-id="698de-291">如需詳細資訊，請參閱 [反覆運算](programming-guide/concepts/iterators.md)器。</span><span class="sxs-lookup"><span data-stu-id="698de-291">For more information, see [Iterators](programming-guide/concepts/iterators.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="698de-292">請參閱</span><span class="sxs-lookup"><span data-stu-id="698de-292">See also</span></span>

- [<span data-ttu-id="698de-293">存取修飾詞</span><span class="sxs-lookup"><span data-stu-id="698de-293">Access Modifiers</span></span>](language-reference/keywords/access-modifiers.md)
- [<span data-ttu-id="698de-294">靜態類別和靜態類別成員</span><span class="sxs-lookup"><span data-stu-id="698de-294">Static Classes and Static Class Members</span></span>](programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
- [<span data-ttu-id="698de-295">繼承</span><span class="sxs-lookup"><span data-stu-id="698de-295">Inheritance</span></span>](programming-guide/classes-and-structs/inheritance.md)
- [<span data-ttu-id="698de-296">抽象和密封類別以及類別成員</span><span class="sxs-lookup"><span data-stu-id="698de-296">Abstract and Sealed Classes and Class Members</span></span>](programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)
- [<span data-ttu-id="698de-297">params</span><span class="sxs-lookup"><span data-stu-id="698de-297">params</span></span>](language-reference/keywords/params.md)
- [<span data-ttu-id="698de-298">擴展</span><span class="sxs-lookup"><span data-stu-id="698de-298">out</span></span>](language-reference/keywords/out-parameter-modifier.md)
- [<span data-ttu-id="698de-299">ref</span><span class="sxs-lookup"><span data-stu-id="698de-299">ref</span></span>](language-reference/keywords/ref.md)
- [<span data-ttu-id="698de-300">in</span><span class="sxs-lookup"><span data-stu-id="698de-300">in</span></span>](language-reference/keywords/in-parameter-modifier.md)
- [<span data-ttu-id="698de-301">傳遞參數</span><span class="sxs-lookup"><span data-stu-id="698de-301">Passing Parameters</span></span>](programming-guide/classes-and-structs/passing-parameters.md)
