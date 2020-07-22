---
title: 方法 - C# 程式設計手冊
description: 'C # 中的方法是包含一系列語句的程式碼區塊。 程式會藉由呼叫方法並指定引數來執行語句。'
ms.date: 07/20/2015
helpviewer_keywords:
- methods [C#]
- C# language, methods
ms.assetid: cc738f07-e8cd-4683-9585-9f40c0667c37
ms.openlocfilehash: db35b48d4d7e70a54b38342e79fa2881b3857bd7
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86864146"
---
# <a name="methods-c-programming-guide"></a><span data-ttu-id="0902f-104">方法 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="0902f-104">Methods (C# Programming Guide)</span></span>

<span data-ttu-id="0902f-105">方法是包含一系列陳述式的程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="0902f-105">A method is a code block that contains a series of statements.</span></span> <span data-ttu-id="0902f-106">程式會造成呼叫方法並指定任何所需的方法引數來執行陳述式。</span><span class="sxs-lookup"><span data-stu-id="0902f-106">A program causes the statements to be executed by calling the method and specifying any required method arguments.</span></span> <span data-ttu-id="0902f-107">在 C# 中，每個執行的指示是在方法的內容中執行。</span><span class="sxs-lookup"><span data-stu-id="0902f-107">In C#, every executed instruction is performed in the context of a method.</span></span> <span data-ttu-id="0902f-108">`Main`方法是每個 c # 應用程式的進入點，而且會在程式啟動時由 common language runtime （CLR）呼叫。</span><span class="sxs-lookup"><span data-stu-id="0902f-108">The `Main` method is the entry point for every C# application and it's called by the common language runtime (CLR) when the program is started.</span></span>

> [!NOTE]
> <span data-ttu-id="0902f-109">本文討論命名的方法。</span><span class="sxs-lookup"><span data-stu-id="0902f-109">This article discusses named methods.</span></span> <span data-ttu-id="0902f-110">如需匿名函式的資訊，請參閱[匿名函式](../statements-expressions-operators/anonymous-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="0902f-110">For information about anonymous functions, see [Anonymous Functions](../statements-expressions-operators/anonymous-functions.md).</span></span>

## <a name="method-signatures"></a><span data-ttu-id="0902f-111">方法簽章</span><span class="sxs-lookup"><span data-stu-id="0902f-111">Method signatures</span></span>

<span data-ttu-id="0902f-112">方法是在[類別](../../language-reference/keywords/class.md)、[結構](../../language-reference/builtin-types/struct.md)或[介面](../interfaces/index.md)中宣告，藉由指定存取層級（例如 `public` 或 `private` ）、選擇性修飾詞（例如 `abstract` 或）、傳回 `sealed` 值、方法的名稱，以及任何方法參數。</span><span class="sxs-lookup"><span data-stu-id="0902f-112">Methods are declared in a [class](../../language-reference/keywords/class.md), [struct](../../language-reference/builtin-types/struct.md), or [interface](../interfaces/index.md) by specifying the access level such as `public` or `private`, optional modifiers such as `abstract` or `sealed`, the return value, the name of the method, and any method parameters.</span></span> <span data-ttu-id="0902f-113">這些部份放在一起即為方法的簽章。</span><span class="sxs-lookup"><span data-stu-id="0902f-113">These parts together are the signature of the method.</span></span>

> [!NOTE]
> <span data-ttu-id="0902f-114">方法的傳回類型不是方法多載用途的方法簽章的一部分。</span><span class="sxs-lookup"><span data-stu-id="0902f-114">A return type of a method is not part of the signature of the method for the purposes of method overloading.</span></span> <span data-ttu-id="0902f-115">不過，在判斷委派與所指向的方法之間的相容性時，它是方法簽章的一部分。</span><span class="sxs-lookup"><span data-stu-id="0902f-115">However, it is part of the signature of the method when determining the compatibility between a delegate and the method that it points to.</span></span>

<span data-ttu-id="0902f-116">方法參數會放在括號中，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="0902f-116">Method parameters are enclosed in parentheses and are separated by commas.</span></span> <span data-ttu-id="0902f-117">空括號表示方法不需要任何參數。</span><span class="sxs-lookup"><span data-stu-id="0902f-117">Empty parentheses indicate that the method requires no parameters.</span></span> <span data-ttu-id="0902f-118">這個類別包含四個方法：</span><span class="sxs-lookup"><span data-stu-id="0902f-118">This class contains four methods:</span></span>

[!code-csharp[csProgGuideObjects#40](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#40)]

## <a name="method-access"></a><span data-ttu-id="0902f-119">方法存取</span><span class="sxs-lookup"><span data-stu-id="0902f-119">Method access</span></span>

<span data-ttu-id="0902f-120">在物件上呼叫方法，就像是存取欄位。</span><span class="sxs-lookup"><span data-stu-id="0902f-120">Calling a method on an object is like accessing a field.</span></span> <span data-ttu-id="0902f-121">在物件名稱後面加上句點、方法的名稱與括號。</span><span class="sxs-lookup"><span data-stu-id="0902f-121">After the object name, add a period, the name of the method, and parentheses.</span></span> <span data-ttu-id="0902f-122">引數會在括號中列出，並以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="0902f-122">Arguments are listed within the parentheses, and are separated by commas.</span></span> <span data-ttu-id="0902f-123">因此可以如下列範例所示呼叫 `Motorcycle` 類別的方法：</span><span class="sxs-lookup"><span data-stu-id="0902f-123">The methods of the `Motorcycle` class can therefore be called as in the following example:</span></span>

[!code-csharp[csProgGuideObjects#41](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#41)]

## <a name="method-parameters-vs-arguments"></a><span data-ttu-id="0902f-124">方法參數與引數的比較</span><span class="sxs-lookup"><span data-stu-id="0902f-124">Method parameters vs. arguments</span></span>

<span data-ttu-id="0902f-125">方法定義會指定所需的任何參數的名稱和類型。</span><span class="sxs-lookup"><span data-stu-id="0902f-125">The method definition specifies the names and types of any parameters that are required.</span></span> <span data-ttu-id="0902f-126">在呼叫程式碼呼叫此方法時，它會提供對每個參數呼叫的引數的具體值。</span><span class="sxs-lookup"><span data-stu-id="0902f-126">When calling code calls the method, it provides concrete values called arguments for each parameter.</span></span> <span data-ttu-id="0902f-127">引數必須與參數類型相容，但是在呼叫程式碼中使用的引數名稱（如果有的話）不需要與方法中所定義的參數相同。</span><span class="sxs-lookup"><span data-stu-id="0902f-127">The arguments must be compatible with the parameter type but the argument name (if any) used in the calling code doesn't have to be the same as the parameter named defined in the method.</span></span> <span data-ttu-id="0902f-128">例如：</span><span class="sxs-lookup"><span data-stu-id="0902f-128">For example:</span></span>

[!code-csharp[csProgGuideObjects#74](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#74)]

## <a name="passing-by-reference-vs-passing-by-value"></a><span data-ttu-id="0902f-129">以傳址方式傳遞與以傳值方式傳遞</span><span class="sxs-lookup"><span data-stu-id="0902f-129">Passing by reference vs. passing by value</span></span>

<span data-ttu-id="0902f-130">根據預設，當實[數值型別](../../language-reference/builtin-types/value-types.md)的實例傳遞至方法時，會傳遞其複本，而不是實例本身。</span><span class="sxs-lookup"><span data-stu-id="0902f-130">By default, when an instance of a [value type](../../language-reference/builtin-types/value-types.md) is passed to a method, its copy is passed instead of the instance itself.</span></span> <span data-ttu-id="0902f-131">因此，對引數所做的變更不會影響呼叫方法中的原始實例。</span><span class="sxs-lookup"><span data-stu-id="0902f-131">Therefore, changes to the argument have no effect on the original instance in the calling method.</span></span> <span data-ttu-id="0902f-132">若要以傳址方式傳遞實數值型別的實例，請使用 `ref` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="0902f-132">To pass a value-type instance by reference, use the `ref` keyword.</span></span> <span data-ttu-id="0902f-133">如需詳細資訊，請參閱[傳遞實值型別參數](./passing-value-type-parameters.md)。</span><span class="sxs-lookup"><span data-stu-id="0902f-133">For more information, see [Passing Value-Type Parameters](./passing-value-type-parameters.md).</span></span>

<span data-ttu-id="0902f-134">傳遞參考類型的物件至方法時，會傳遞物件的參考。</span><span class="sxs-lookup"><span data-stu-id="0902f-134">When an object of a reference type is passed to a method, a reference to the object is passed.</span></span> <span data-ttu-id="0902f-135">也就是說，此方法接收的不是物件本身，而是指出物件位置的引數。</span><span class="sxs-lookup"><span data-stu-id="0902f-135">That is, the method receives not the object itself but an argument that indicates the location of the object.</span></span> <span data-ttu-id="0902f-136">如果您使用此參考變更物件的成員，變更會反映在呼叫方法的引數中，即使以傳值方式傳遞物件。</span><span class="sxs-lookup"><span data-stu-id="0902f-136">If you change a member of the object by using this reference, the change is reflected in the argument in the calling method, even if you pass the object by value.</span></span>

<span data-ttu-id="0902f-137">您可以使用關鍵字建立參考型別 `class` ，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="0902f-137">You create a reference type by using the `class` keyword, as the following example shows:</span></span>

[!code-csharp[csProgGuideObjects#42](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#42)]

<span data-ttu-id="0902f-138">現在，如果您將此類型為基礎的物件傳遞至方法，即會傳遞物件的參考。</span><span class="sxs-lookup"><span data-stu-id="0902f-138">Now, if you pass an object that is based on this type to a method, a reference to the object is passed.</span></span> <span data-ttu-id="0902f-139">下列範例會將類型的物件傳遞 `SampleRefType` 給方法 `ModifyObject` ：</span><span class="sxs-lookup"><span data-stu-id="0902f-139">The following example passes an object of type `SampleRefType` to method `ModifyObject`:</span></span>

[!code-csharp[csProgGuideObjects#75](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#75)]

<span data-ttu-id="0902f-140">此範例會執行與上一個範例基本上相同的動作，依傳值方式將引數傳遞至方法。</span><span class="sxs-lookup"><span data-stu-id="0902f-140">The example does essentially the same thing as the previous example in that it passes an argument by value to a method.</span></span> <span data-ttu-id="0902f-141">但是，由於使用參考類型，結果會不同。</span><span class="sxs-lookup"><span data-stu-id="0902f-141">But, because a reference type is used, the result is different.</span></span> <span data-ttu-id="0902f-142">`ModifyObject` 中對參數 `value` 的 `obj`欄位做的修改，也會變更 `value` 方法中引數 `rt`的 `TestRefType` 欄位。</span><span class="sxs-lookup"><span data-stu-id="0902f-142">The modification that is made in `ModifyObject` to the `value` field of the parameter, `obj`, also changes the `value` field of the argument, `rt`, in the `TestRefType` method.</span></span> <span data-ttu-id="0902f-143">`TestRefType` 方法會顯示 33 做為輸出。</span><span class="sxs-lookup"><span data-stu-id="0902f-143">The `TestRefType` method displays 33 as the output.</span></span>

<span data-ttu-id="0902f-144">如需如何依傳址和依傳值方式來傳遞參考型別的詳細資訊，請參閱[傳遞參考型別參數](./passing-reference-type-parameters.md)和[參考型別](../../language-reference/keywords/reference-types.md)。</span><span class="sxs-lookup"><span data-stu-id="0902f-144">For more information about how to pass reference types by reference and by value, see [Passing Reference-Type Parameters](./passing-reference-type-parameters.md) and [Reference Types](../../language-reference/keywords/reference-types.md).</span></span>

## <a name="return-values"></a><span data-ttu-id="0902f-145">傳回值</span><span class="sxs-lookup"><span data-stu-id="0902f-145">Return values</span></span>

<span data-ttu-id="0902f-146">方法可以傳回值給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="0902f-146">Methods can return a value to the caller.</span></span> <span data-ttu-id="0902f-147">針對傳回類型，如果列在方法名稱前面的類型不是 `void`，方法可以使用 `return` 關鍵字傳回值。</span><span class="sxs-lookup"><span data-stu-id="0902f-147">If the return type, the type listed before the method name, is not `void`, the method can return the value by using the `return` keyword.</span></span> <span data-ttu-id="0902f-148">具有 `return` 關鍵字後面接著符合傳回類型值的陳述式，會將該值傳回給方法呼叫者。</span><span class="sxs-lookup"><span data-stu-id="0902f-148">A statement with the `return` keyword followed by a value that matches the return type will return that value to the method caller.</span></span>

<span data-ttu-id="0902f-149">可以透過傳值方式將值傳回給呼叫者，或者，從 C# 7.0 開始，是[以傳址方式](ref-returns.md)。</span><span class="sxs-lookup"><span data-stu-id="0902f-149">The value can be returned to the caller by value or, starting with C# 7.0, [by reference](ref-returns.md).</span></span> <span data-ttu-id="0902f-150">如果 `ref` 關鍵字用於方法簽章中，並且接在每個 `return` 關鍵字後面，則會以傳址方式將值傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="0902f-150">Values are returned to the caller by reference if the `ref` keyword is used in the method signature and it follows each `return` keyword.</span></span> <span data-ttu-id="0902f-151">例如，下列方法簽章和傳回陳述式指出方法以傳址方式將變數名稱 `estDistance` 傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="0902f-151">For example, the following method signature and return statement indicate that the method returns a variable names `estDistance` by reference to the caller.</span></span>

```csharp
public ref double GetEstimatedDistance()
{
    return ref estDistance;
}
```

<span data-ttu-id="0902f-152">`return` 關鍵字也會停止執行方法。</span><span class="sxs-lookup"><span data-stu-id="0902f-152">The `return` keyword also stops the execution of the method.</span></span> <span data-ttu-id="0902f-153">如果傳回類型為 `void`，不含值的 `return` 陳述式對於停止方法的執行仍很有用。</span><span class="sxs-lookup"><span data-stu-id="0902f-153">If the return type is `void`, a `return` statement without a value is still useful to stop the execution of the method.</span></span> <span data-ttu-id="0902f-154">若沒有 `return` 關鍵字，在方法到達程式碼區塊的結尾時，方法將會停止執行。</span><span class="sxs-lookup"><span data-stu-id="0902f-154">Without the `return` keyword, the method will stop executing when it reaches the end of the code block.</span></span> <span data-ttu-id="0902f-155">具有非 void 傳回類型的方法需要使用 `return` 關鍵字以傳回值。</span><span class="sxs-lookup"><span data-stu-id="0902f-155">Methods with a non-void return type are required to use the `return` keyword to return a value.</span></span> <span data-ttu-id="0902f-156">例如，這兩種方法使用 `return` 關鍵字傳回整數：</span><span class="sxs-lookup"><span data-stu-id="0902f-156">For example, these two methods use the `return` keyword to return integers:</span></span>

[!code-csharp[csProgGuideObjects#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#44)]

<span data-ttu-id="0902f-157">若要使用從方法傳回的值，呼叫方法可以在使用相同類型值的任意位置使用方法呼叫本身即已足夠。</span><span class="sxs-lookup"><span data-stu-id="0902f-157">To use a value returned from a method, the calling method can use the method call itself anywhere a value of the same type would be sufficient.</span></span> <span data-ttu-id="0902f-158">您也可以指派傳回值給變數。</span><span class="sxs-lookup"><span data-stu-id="0902f-158">You can also assign the return value to a variable.</span></span> <span data-ttu-id="0902f-159">例如，下列兩個程式碼範例會達到相同的目標：</span><span class="sxs-lookup"><span data-stu-id="0902f-159">For example, the following two code examples accomplish the same goal:</span></span>

[!code-csharp[csProgGuideObjects#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#45)]

[!code-csharp[csProgGuideObjects#46](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#46)]

<span data-ttu-id="0902f-160">使用區域變數，在此情況下的 `result`來儲存值是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="0902f-160">Using a local variable, in this case, `result`, to store a value is optional.</span></span> <span data-ttu-id="0902f-161">它有助於程式碼的可讀性，或如果您需要儲存方法的整個範圍引數的原始值，則可能為必要。</span><span class="sxs-lookup"><span data-stu-id="0902f-161">It may help the readability of the code, or it may be necessary if you need to store the original value of the argument for the entire scope of the method.</span></span>

<span data-ttu-id="0902f-162">若要從方法使用以傳址方式傳回的值，則在您想要修改 [ref 區域變數](ref-returns.md#ref-locals)的值時必須宣告該變數。</span><span class="sxs-lookup"><span data-stu-id="0902f-162">To use a value returned by reference from a method, you must declare a [ref local](ref-returns.md#ref-locals) variable if you intend to modify its value.</span></span> <span data-ttu-id="0902f-163">例如，如果 `Planet.GetEstimatedDistance` 方法以傳址方式傳回 <xref:System.Double> 值，您可以使用下列這類程式碼將它定義為 ref 區域變數：</span><span class="sxs-lookup"><span data-stu-id="0902f-163">For example, if the `Planet.GetEstimatedDistance` method returns a <xref:System.Double> value by reference, you can define it as a ref local variable with code like the following:</span></span>

```csharp
ref int distance = plant
```

<span data-ttu-id="0902f-164">如果呼叫函式已將陣列傳入 `M`，則不需要從修改陣列內容的 `M` 方法傳回多維度陣列。</span><span class="sxs-lookup"><span data-stu-id="0902f-164">Returning a multi-dimensional array from a method, `M`, that modifies the array's contents is not necessary if the calling function passed the array into `M`.</span></span>  <span data-ttu-id="0902f-165">您可能會從 `M` 針對值的良好樣式或功能流程傳回產生的陣列，但這不需要，因為 C# 會以傳值方式傳遞所有參考型別，而且陣列參考的值是陣列的指標。</span><span class="sxs-lookup"><span data-stu-id="0902f-165">You may return the resulting array from `M` for good style or functional flow of values, but it is not necessary because C# passes all reference types by value, and the value of an array reference is the pointer to the array.</span></span> <span data-ttu-id="0902f-166">在方法中 `M` ，任何具有陣列參考的程式碼都可以觀察陣列內容的任何變更，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="0902f-166">In the method `M`, any changes to the array's contents are observable by any code that has a reference to the array, as shown in the following example:</span></span>

```csharp
static void Main(string[] args)
{
    int[,] matrix = new int[2, 2];
    FillMatrix(matrix);
    // matrix is now full of -1
}

public static void FillMatrix(int[,] matrix)
{
    for (int i = 0; i < matrix.GetLength(0); i++)
    {
        for (int j = 0; j < matrix.GetLength(1); j++)
        {
            matrix[i, j] = -1;
        }
    }
}
```

<span data-ttu-id="0902f-167">如需詳細資訊，請參閱 [return](../../language-reference/keywords/return.md)。</span><span class="sxs-lookup"><span data-stu-id="0902f-167">For more information, see [return](../../language-reference/keywords/return.md).</span></span>

## <a name="async-methods"></a><span data-ttu-id="0902f-168">非同步方法</span><span class="sxs-lookup"><span data-stu-id="0902f-168">Async methods</span></span>

<span data-ttu-id="0902f-169">使用非同步功能，您就可以呼叫非同步方法，而不需要使用明確回呼或手動將您的程式碼分散到多種方法或 lambda 運算式上。</span><span class="sxs-lookup"><span data-stu-id="0902f-169">By using the async feature, you can invoke asynchronous methods without using explicit callbacks or manually splitting your code across multiple methods or lambda expressions.</span></span>

<span data-ttu-id="0902f-170">如果您使用 [async](../../language-reference/keywords/async.md) 修飾詞來標示方法，可以在方法中使用 [await](../../language-reference/operators/await.md) 運算子。</span><span class="sxs-lookup"><span data-stu-id="0902f-170">If you mark a method with the [async](../../language-reference/keywords/async.md) modifier, you can use the [await](../../language-reference/operators/await.md) operator in the method.</span></span> <span data-ttu-id="0902f-171">當控制項到達 async 方法的 await 運算式時，控制項會傳回給呼叫者，方法中的進度會暫停，直到等候的工作完成。</span><span class="sxs-lookup"><span data-stu-id="0902f-171">When control reaches an await expression in the async method, control returns to the caller, and progress in the method is suspended until the awaited task completes.</span></span> <span data-ttu-id="0902f-172">當工作完成時，方法中的執行可以繼續。</span><span class="sxs-lookup"><span data-stu-id="0902f-172">When the task is complete, execution can resume in the method.</span></span>

> [!NOTE]
> <span data-ttu-id="0902f-173">非同步方法會在遇到第一個未完成的等候物件或是到達非同步方法的結尾時 (以先發生者為準)，傳回呼叫者</span><span class="sxs-lookup"><span data-stu-id="0902f-173">An async method returns to the caller when either it encounters the first awaited object that’s not yet complete or it gets to the end of the async method, whichever occurs first.</span></span>

<span data-ttu-id="0902f-174">非同步方法的傳回類型可以是 <xref:System.Threading.Tasks.Task%601>、 <xref:System.Threading.Tasks.Task>或 void。</span><span class="sxs-lookup"><span data-stu-id="0902f-174">An async method can have a return type of <xref:System.Threading.Tasks.Task%601>, <xref:System.Threading.Tasks.Task>, or void.</span></span> <span data-ttu-id="0902f-175">void 傳回類型主要用於定義需要 void 傳回類型的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="0902f-175">The void return type is used primarily to define event handlers, where a void return type is required.</span></span> <span data-ttu-id="0902f-176">傳回 void 類型的非同步方法無法等候，而且 void 傳回方法的呼叫者無法攔截方法擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0902f-176">An async method that returns void can't be awaited, and the caller of a void-returning method can't catch exceptions that the method throws.</span></span>

<span data-ttu-id="0902f-177">在下列範例中， `DelayAsync` 是會傳回類型 <xref:System.Threading.Tasks.Task%601>的非同步方法。</span><span class="sxs-lookup"><span data-stu-id="0902f-177">In the following example, `DelayAsync` is an async method that has a return type of <xref:System.Threading.Tasks.Task%601>.</span></span> <span data-ttu-id="0902f-178">`DelayAsync` 具有傳回整數的 `return` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="0902f-178">`DelayAsync` has a `return` statement that returns an integer.</span></span> <span data-ttu-id="0902f-179">因此 `DelayAsync` 的方法宣告必須具有傳回類型 `Task<int>`。</span><span class="sxs-lookup"><span data-stu-id="0902f-179">Therefore the method declaration of `DelayAsync` must have a return type of `Task<int>`.</span></span> <span data-ttu-id="0902f-180">因為傳回類型是 `Task<int>`， `await` 中 `DoSomethingAsync` 運算式的評估會產生整數，如下列陳述式所示範： `int result = await delayTask`。</span><span class="sxs-lookup"><span data-stu-id="0902f-180">Because the return type is `Task<int>`, the evaluation of the `await` expression in `DoSomethingAsync` produces an integer as the following statement demonstrates: `int result = await delayTask`.</span></span>

<span data-ttu-id="0902f-181">`startButton_Click` 方法是傳回類型為 void 的非同步方法的範例。</span><span class="sxs-lookup"><span data-stu-id="0902f-181">The `startButton_Click` method is an example of an async method that has a return type of void.</span></span> <span data-ttu-id="0902f-182">因為 `DoSomethingAsync` 是非同步方法，對 `DoSomethingAsync` 的呼叫工作必須等候，如下列陳述式所示： `await DoSomethingAsync();`。</span><span class="sxs-lookup"><span data-stu-id="0902f-182">Because `DoSomethingAsync` is an async method, the task for the call to `DoSomethingAsync` must be awaited, as the following statement shows: `await DoSomethingAsync();`.</span></span> <span data-ttu-id="0902f-183">`startButton_Click` 方法都必須定義 `async` 修飾詞，因為方法有 `await` 運算式。</span><span class="sxs-lookup"><span data-stu-id="0902f-183">The `startButton_Click` method must be defined with the `async` modifier because the method has an `await` expression.</span></span>

[!code-csharp[csAsyncMethod#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csasyncmethod/cs/mainwindow.xaml.cs#2)]

<span data-ttu-id="0902f-184">非同步方法不可以宣告任何 [ref](../../language-reference/keywords/ref.md) 或 [out](../../language-reference/keywords/out-parameter-modifier.md) 參數，但是可以呼叫具有這類參數的方法。</span><span class="sxs-lookup"><span data-stu-id="0902f-184">An async method can't declare any [ref](../../language-reference/keywords/ref.md) or [out](../../language-reference/keywords/out-parameter-modifier.md) parameters, but it can call methods that have such parameters.</span></span>

<span data-ttu-id="0902f-185">如需非同步方法的詳細資訊，請參閱[使用 async 和 await 進行非同步程式設計](../concepts/async/index.md)、[非同步程式中的控制流程](../concepts/async/control-flow-in-async-programs.md)和[非同步傳回類型](../concepts/async/async-return-types.md)。</span><span class="sxs-lookup"><span data-stu-id="0902f-185">For more information about async methods, see [Asynchronous Programming with async and await](../concepts/async/index.md), [Control Flow in Async Programs](../concepts/async/control-flow-in-async-programs.md), and [Async Return Types](../concepts/async/async-return-types.md).</span></span>

## <a name="expression-body-definitions"></a><span data-ttu-id="0902f-186">運算式主體定義</span><span class="sxs-lookup"><span data-stu-id="0902f-186">Expression body definitions</span></span>

<span data-ttu-id="0902f-187">方法定義只是立即傳回運算式的結果，或是具有單一陳述式做為方法的主體是很常見的。</span><span class="sxs-lookup"><span data-stu-id="0902f-187">It is common to have method definitions that simply return immediately with the result of an expression, or that have a single statement as the body of the method.</span></span> <span data-ttu-id="0902f-188">使用 `=>`定義這類方法有個語法捷徑：</span><span class="sxs-lookup"><span data-stu-id="0902f-188">There is a syntax shortcut for defining such methods using `=>`:</span></span>

```csharp
public Point Move(int dx, int dy) => new Point(x + dx, y + dy);
public void Print() => Console.WriteLine(First + " " + Last);
// Works with operators, properties, and indexers too.
public static Complex operator +(Complex a, Complex b) => a.Add(b);
public string Name => First + " " + Last;
public Customer this[long id] => store.LookupCustomer(id);
```

<span data-ttu-id="0902f-189">如果方法會傳回 `void` 或非同步方法，則方法的主體必須是陳述式運算式 (如同 lambda)。</span><span class="sxs-lookup"><span data-stu-id="0902f-189">If the method returns `void` or is an async method, then the body of the method must be a statement expression (same as with lambdas).</span></span> <span data-ttu-id="0902f-190">若為屬性和索引子，它們必須是唯讀，因此您不應使用 `get` 存取子關鍵字。</span><span class="sxs-lookup"><span data-stu-id="0902f-190">For properties and indexers, they must be read only, and you don't use the `get` accessor keyword.</span></span>

## <a name="iterators"></a><span data-ttu-id="0902f-191">迭代器</span><span class="sxs-lookup"><span data-stu-id="0902f-191">Iterators</span></span>

<span data-ttu-id="0902f-192">迭代器會對集合執行自訂的反覆項目，例如清單或陣列。</span><span class="sxs-lookup"><span data-stu-id="0902f-192">An iterator performs a custom iteration over a collection, such as a list or an array.</span></span> <span data-ttu-id="0902f-193">迭代器會使用 [yield return](../../language-reference/keywords/yield.md) 陳述式來一次傳回一個項目。</span><span class="sxs-lookup"><span data-stu-id="0902f-193">An iterator uses the [yield return](../../language-reference/keywords/yield.md) statement to return each element one at a time.</span></span> <span data-ttu-id="0902f-194">當 [yield return](../../language-reference/keywords/yield.md) 到達陳述式時，會記住在程式碼中的目前位置。</span><span class="sxs-lookup"><span data-stu-id="0902f-194">When a [yield return](../../language-reference/keywords/yield.md) statement is reached, the current location in code is remembered.</span></span> <span data-ttu-id="0902f-195">下一次呼叫迭代器時，便會從這個位置重新開始執行。</span><span class="sxs-lookup"><span data-stu-id="0902f-195">Execution is restarted from that location when the iterator is called the next time.</span></span>

<span data-ttu-id="0902f-196">您會使用 [foreach](../../language-reference/keywords/foreach-in.md) 陳述式，透過用戶端程式碼呼叫迭代器。</span><span class="sxs-lookup"><span data-stu-id="0902f-196">You call an iterator from client code by using a [foreach](../../language-reference/keywords/foreach-in.md) statement.</span></span>

<span data-ttu-id="0902f-197">迭代器的傳回類型可以是 <xref:System.Collections.IEnumerable>、 <xref:System.Collections.Generic.IEnumerable%601>、 <xref:System.Collections.IEnumerator>或 <xref:System.Collections.Generic.IEnumerator%601>。</span><span class="sxs-lookup"><span data-stu-id="0902f-197">The return type of an iterator can be <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, or <xref:System.Collections.Generic.IEnumerator%601>.</span></span>

<span data-ttu-id="0902f-198">如需詳細資訊，請參閱[反覆運算](../concepts/iterators.md)器。</span><span class="sxs-lookup"><span data-stu-id="0902f-198">For more information, see [Iterators](../concepts/iterators.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="0902f-199">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="0902f-199">C# language specification</span></span>

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="0902f-200">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0902f-200">See also</span></span>

- [<span data-ttu-id="0902f-201">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="0902f-201">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="0902f-202">類別和結構</span><span class="sxs-lookup"><span data-stu-id="0902f-202">Classes and Structs</span></span>](index.md)
- [<span data-ttu-id="0902f-203">存取修飾詞</span><span class="sxs-lookup"><span data-stu-id="0902f-203">Access Modifiers</span></span>](access-modifiers.md)
- [<span data-ttu-id="0902f-204">靜態類別和靜態類別成員</span><span class="sxs-lookup"><span data-stu-id="0902f-204">Static Classes and Static Class Members</span></span>](static-classes-and-static-class-members.md)
- [<span data-ttu-id="0902f-205">繼承</span><span class="sxs-lookup"><span data-stu-id="0902f-205">Inheritance</span></span>](inheritance.md)
- [<span data-ttu-id="0902f-206">抽象和密封類別以及類別成員</span><span class="sxs-lookup"><span data-stu-id="0902f-206">Abstract and Sealed Classes and Class Members</span></span>](abstract-and-sealed-classes-and-class-members.md)
- [<span data-ttu-id="0902f-207">params</span><span class="sxs-lookup"><span data-stu-id="0902f-207">params</span></span>](../../language-reference/keywords/params.md)
- [<span data-ttu-id="0902f-208">return</span><span class="sxs-lookup"><span data-stu-id="0902f-208">return</span></span>](../../language-reference/keywords/return.md)
- [<span data-ttu-id="0902f-209">脫銷</span><span class="sxs-lookup"><span data-stu-id="0902f-209">out</span></span>](../../language-reference/keywords/out.md)
- [<span data-ttu-id="0902f-210">ref</span><span class="sxs-lookup"><span data-stu-id="0902f-210">ref</span></span>](../../language-reference/keywords/ref.md)
- [<span data-ttu-id="0902f-211">傳遞參數</span><span class="sxs-lookup"><span data-stu-id="0902f-211">Passing Parameters</span></span>](passing-parameters.md)
