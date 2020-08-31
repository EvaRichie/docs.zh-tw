---
description: in 參數修飾詞 - C# 參考
title: in 參數修飾詞 - C# 參考
ms.date: 03/19/2020
helpviewer_keywords:
- parameters [C#], in
- in parameters [C#]
ms.openlocfilehash: 613be9248e6ce9b974bcab1b59abd30469e9e180
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89118400"
---
# <a name="in-parameter-modifier-c-reference"></a><span data-ttu-id="8b92d-103">in 參數修飾詞 (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="8b92d-103">in parameter modifier (C# Reference)</span></span>

<span data-ttu-id="8b92d-104">`in` 關鍵字會導致引數由參考傳遞。</span><span class="sxs-lookup"><span data-stu-id="8b92d-104">The `in` keyword causes arguments to be passed by reference.</span></span> <span data-ttu-id="8b92d-105">它會使形式參數成為引數的別名，其必須為變數。</span><span class="sxs-lookup"><span data-stu-id="8b92d-105">It makes the formal parameter an alias for the argument, which must be a variable.</span></span> <span data-ttu-id="8b92d-106">換句話說，參數上的任何作業都會在引數上進行。</span><span class="sxs-lookup"><span data-stu-id="8b92d-106">In other words, any operation on the parameter is made on the argument.</span></span> <span data-ttu-id="8b92d-107">它就像 [ref](ref.md) 或 [out](out-parameter-modifier.md) 關鍵字，不同的是 `in` 引數不能被呼叫的方法修改。</span><span class="sxs-lookup"><span data-stu-id="8b92d-107">It is like the [ref](ref.md) or [out](out-parameter-modifier.md) keywords, except that `in` arguments cannot be modified by the called method.</span></span> <span data-ttu-id="8b92d-108">雖然 `ref` 引數可以被修改，`out` 引數則必須由呼叫方法修改，且那些修改在呼叫的內容中是可觀察的。</span><span class="sxs-lookup"><span data-stu-id="8b92d-108">Whereas `ref` arguments may be modified, `out` arguments must be modified by the called method, and those modifications are observable in the calling context.</span></span>

[!code-csharp-interactive[cs-in-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/InParameterModifier.cs#1)]  

<span data-ttu-id="8b92d-109">上述範例示範了 `in` 修飾詞在呼叫位置通常非必要。</span><span class="sxs-lookup"><span data-stu-id="8b92d-109">The preceding example demonstrates that the `in` modifier is usually unnecessary at the call site.</span></span> <span data-ttu-id="8b92d-110">而只有在宣告方法時才會需要該項目。</span><span class="sxs-lookup"><span data-stu-id="8b92d-110">It is only required in the method declaration.</span></span>

> [!NOTE]
> <span data-ttu-id="8b92d-111">`in` 關鍵字也可與泛型型別搭配使用，來指定類型參數是否為 Contravariant、屬於 `foreach` 陳述式的一部分，或是屬於 LINQ 查詢中的 `join` 子句。</span><span class="sxs-lookup"><span data-stu-id="8b92d-111">The `in` keyword can also be used with a generic type parameter to specify that the type parameter is contravariant, as part of a `foreach` statement, or as part of a `join` clause in a LINQ query.</span></span> <span data-ttu-id="8b92d-112">如需如何在這些內容中使用 `in` 關鍵字的詳細資訊，請參閱 [in](in.md)，其提供所有這些使用的連結。</span><span class="sxs-lookup"><span data-stu-id="8b92d-112">For more information on the use of the `in` keyword in these contexts, see [in](in.md), which provides links to all those uses.</span></span>
  
<span data-ttu-id="8b92d-113">傳遞為 `in` 引數的變數，必須先經過初始化，才能在方法呼叫中傳遞。</span><span class="sxs-lookup"><span data-stu-id="8b92d-113">Variables passed as `in` arguments must be initialized before being passed in a method call.</span></span> <span data-ttu-id="8b92d-114">但是，呼叫方法可能不會指派值或修改引數。</span><span class="sxs-lookup"><span data-stu-id="8b92d-114">However, the called method may not assign a value or modify the argument.</span></span>  

<span data-ttu-id="8b92d-115">`in` 參數修飾詞在 C# 7.2 與更新版本中可用。</span><span class="sxs-lookup"><span data-stu-id="8b92d-115">The `in` parameter modifier is available in C# 7.2 and later.</span></span> <span data-ttu-id="8b92d-116">先前的版本會產生編譯器錯誤 `CS8107` (C# 7.0 中無法使用 '唯讀參考' 功能。</span><span class="sxs-lookup"><span data-stu-id="8b92d-116">Previous versions generate compiler error `CS8107` ("Feature 'readonly references' is not available in C# 7.0.</span></span> <span data-ttu-id="8b92d-117">請使用語言版本 7.2 或更高的版本。」) 若要設定編譯器語言版本，請參閱[選取 C# 語言版本](../configure-language-version.md)。</span><span class="sxs-lookup"><span data-stu-id="8b92d-117">Please use language version 7.2 or greater.") To configure the compiler language version, see [Select the C# language version](../configure-language-version.md).</span></span>

<span data-ttu-id="8b92d-118">針對多載解析的目的，`in`、`ref` 和 `out` 關鍵字不被視為方法簽章的一部分。</span><span class="sxs-lookup"><span data-stu-id="8b92d-118">The `in`, `ref`, and `out` keywords are not considered part of the method signature for the purpose of overload resolution.</span></span> <span data-ttu-id="8b92d-119">因此，如果唯一的差別是一種方法採用 `ref` 或 `in` 引數，而另一種方法採用 `out` 引數，則無法對方法進行多載。</span><span class="sxs-lookup"><span data-stu-id="8b92d-119">Therefore, methods cannot be overloaded if the only difference is that one method takes a `ref` or `in` argument and the other takes an `out` argument.</span></span> <span data-ttu-id="8b92d-120">例如，將不會編譯下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8b92d-120">The following code, for example, will not compile:</span></span>  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded
    // methods that differ only on in, ref and out".
    public void SampleMethod(in int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
<span data-ttu-id="8b92d-121">允許取決於 `in` 是否存在的多載：</span><span class="sxs-lookup"><span data-stu-id="8b92d-121">Overloading based on the presence of `in` is allowed:</span></span>  
  
```csharp
class InOverloads
{
    public void SampleMethod(in int i) { }
    public void SampleMethod(int i) { }
}
```

## <a name="overload-resolution-rules"></a><span data-ttu-id="8b92d-122">多載解析規則</span><span class="sxs-lookup"><span data-stu-id="8b92d-122">Overload resolution rules</span></span>

<span data-ttu-id="8b92d-123">您可以透過了解 `in` 引數的動機，來了解傳值方式與 `in` 引數的方法多載解析規則。</span><span class="sxs-lookup"><span data-stu-id="8b92d-123">You can understand the overload resolution rules for methods with by value vs. `in` arguments by understanding the motivation for `in` arguments.</span></span> <span data-ttu-id="8b92d-124">使用 `in` 參數定義方法可能會使效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="8b92d-124">Defining methods using `in` parameters is a potential performance optimization.</span></span> <span data-ttu-id="8b92d-125">某些 `struct` 型別引數可能大小很大，在緊密迴圈或關鍵程式碼路徑中呼叫方法時，複製那些結構的成本便很重要。</span><span class="sxs-lookup"><span data-stu-id="8b92d-125">Some `struct` type arguments may be large in size, and when methods are called in tight loops or critical code paths, the cost of copying those structures is critical.</span></span> <span data-ttu-id="8b92d-126">方法會宣告 `in` 參數，以指定可以用傳址方式安全地傳遞引數，因為被呼叫的方法不會修改該引數的狀態。</span><span class="sxs-lookup"><span data-stu-id="8b92d-126">Methods declare `in` parameters to specify that arguments may be passed by reference safely because the called method does not modify the state of that argument.</span></span> <span data-ttu-id="8b92d-127">以傳址方式傳遞那些引數，可避免 (可能) 相當耗費資源的複製。</span><span class="sxs-lookup"><span data-stu-id="8b92d-127">Passing those arguments by reference avoids the (potentially) expensive copy.</span></span>

<span data-ttu-id="8b92d-128">針對呼叫位置的引數指定 `in` 通常是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="8b92d-128">Specifying `in` for arguments at the call site is typically optional.</span></span> <span data-ttu-id="8b92d-129">以傳值方式傳遞引數，和使用 `in` 修飾詞以傳址方式傳遞引數，兩者之間沒有語意差異。</span><span class="sxs-lookup"><span data-stu-id="8b92d-129">There is no semantic difference between passing arguments by value and passing them by reference using the `in` modifier.</span></span> <span data-ttu-id="8b92d-130">呼叫位置的 `in` 修飾詞是選擇性的，因為您不需要指出引數的值可能會變更。</span><span class="sxs-lookup"><span data-stu-id="8b92d-130">The `in` modifier at the call site is optional because you don't need to indicate that the argument's value might be changed.</span></span> <span data-ttu-id="8b92d-131">在呼叫位置明確地新增 `in` 修飾詞，可以確保引數是以傳址方式傳遞，而非以傳值方式傳遞。</span><span class="sxs-lookup"><span data-stu-id="8b92d-131">You explicitly add the `in` modifier at the call site to ensure the argument is passed by reference, not by value.</span></span> <span data-ttu-id="8b92d-132">明確地使用 `in` 有下列兩個效果：</span><span class="sxs-lookup"><span data-stu-id="8b92d-132">Explicitly using `in` has the following two effects:</span></span>

<span data-ttu-id="8b92d-133">首先，在呼叫位置指定 `in` 會強制編譯器選取定義了符合之 `in` 參數的方法。</span><span class="sxs-lookup"><span data-stu-id="8b92d-133">First, specifying `in` at the call site forces the compiler to select a method defined with a matching `in` parameter.</span></span> <span data-ttu-id="8b92d-134">否則，當兩個方法的差異只在於 `in` 是否存在時，傳值方式的多載是較佳的相符項目。</span><span class="sxs-lookup"><span data-stu-id="8b92d-134">Otherwise, when two methods differ only in the presence of `in`, the by value overload is a better match.</span></span>

<span data-ttu-id="8b92d-135">第二，指定 `in` 會宣告您以傳址方式傳遞引數的意圖。</span><span class="sxs-lookup"><span data-stu-id="8b92d-135">Second, specifying `in` declares your intent to pass an argument by reference.</span></span> <span data-ttu-id="8b92d-136">搭配 `in` 使用的引數必須代表可以直接參考的位置。</span><span class="sxs-lookup"><span data-stu-id="8b92d-136">The argument used with `in` must represent a location that can be directly referred to.</span></span> <span data-ttu-id="8b92d-137">`out` 和 `ref` 引數的相同一般規則同樣適用：您無法使用常數、一般屬性或其他會產生值的運算式。</span><span class="sxs-lookup"><span data-stu-id="8b92d-137">The same general rules for `out` and `ref` arguments apply: You cannot use constants, ordinary properties, or other expressions that produce values.</span></span> <span data-ttu-id="8b92d-138">否則，在呼叫位置省略 `in` 會通知編譯器，您將允許它建立暫存變數，傳遞唯讀參考給方法。</span><span class="sxs-lookup"><span data-stu-id="8b92d-138">Otherwise, omitting `in` at the call site informs the compiler that you will allow it to create a temporary variable to pass by read-only reference to the method.</span></span> <span data-ttu-id="8b92d-139">編譯器會建立暫存變數，以克服 `in` 引數的幾項限制：</span><span class="sxs-lookup"><span data-stu-id="8b92d-139">The compiler creates a temporary variable to overcome several restrictions with `in` arguments:</span></span>

- <span data-ttu-id="8b92d-140">暫存變數允許編譯時期常數作為 `in` 參數。</span><span class="sxs-lookup"><span data-stu-id="8b92d-140">A temporary variable allows compile-time constants as `in` parameters.</span></span>
- <span data-ttu-id="8b92d-141">暫存變數允許屬性或其他運算式作為 `in` 參數。</span><span class="sxs-lookup"><span data-stu-id="8b92d-141">A temporary variable allows properties, or other expressions for `in` parameters.</span></span>
- <span data-ttu-id="8b92d-142">暫存變數允許隱含從引數型別轉換成參數型別的引數。</span><span class="sxs-lookup"><span data-stu-id="8b92d-142">A temporary variable allows arguments where there is an implicit conversion from the argument type to the parameter type.</span></span>

<span data-ttu-id="8b92d-143">在所有先前的情況下，編譯器會建立暫存變數，儲存常數、屬性或其他運算式的值。</span><span class="sxs-lookup"><span data-stu-id="8b92d-143">In all the preceding instances, the compiler creates a temporary variable that stores the value of the constant, property, or other expression.</span></span>

<span data-ttu-id="8b92d-144">下列程式碼說明這些規則：</span><span class="sxs-lookup"><span data-stu-id="8b92d-144">The following code illustrates these rules:</span></span>

```csharp
static void Method(in int argument)
{
    // implementation removed
}

Method(5); // OK, temporary variable created.
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // OK, temporary int created with the value 0
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // passed by readonly reference
Method(in i); // passed by readonly reference, explicitly using `in`
```

<span data-ttu-id="8b92d-145">現在，假設可以使用另一個使用傳值引數的方法。</span><span class="sxs-lookup"><span data-stu-id="8b92d-145">Now, suppose another method using by value arguments was available.</span></span> <span data-ttu-id="8b92d-146">結果的變更如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="8b92d-146">The results change as shown in the following code:</span></span>

```csharp
static void Method(int argument)
{
    // implementation removed
}

static void Method(in int argument)
{
    // implementation removed
}

Method(5); // Calls overload passed by value
Method(5L); // CS1503: no implicit conversion from long to int
short s = 0;
Method(s); // Calls overload passed by value.
Method(in s); // CS1503: cannot convert from in short to in int
int i = 42;
Method(i); // Calls overload passed by value
Method(in i); // passed by readonly reference, explicitly using `in`
```

<span data-ttu-id="8b92d-147">以傳址方式傳遞引數的唯一方法呼叫，是最終的方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="8b92d-147">The only method call where the argument is passed by reference is the final one.</span></span>

> [!NOTE]
> <span data-ttu-id="8b92d-148">為簡單起見，上述程式碼使用 `int` 作為引數型別。</span><span class="sxs-lookup"><span data-stu-id="8b92d-148">The preceding code uses `int` as the argument type for simplicity.</span></span> <span data-ttu-id="8b92d-149">因為 `int` 在大多數新型電腦中，不會比參考大，所以將單一 `int` 以唯讀傳址方式傳遞並沒有好處。</span><span class="sxs-lookup"><span data-stu-id="8b92d-149">Because `int` is no larger than a reference in most modern machines, there is no benefit to passing a single `int` as a readonly reference.</span></span>

## <a name="limitations-on-in-parameters"></a><span data-ttu-id="8b92d-150">`in` 參數的限制</span><span class="sxs-lookup"><span data-stu-id="8b92d-150">Limitations on `in` parameters</span></span>

<span data-ttu-id="8b92d-151">您不可為下列幾種方法使用 `in`、`ref` 和 `out` 關鍵字：</span><span class="sxs-lookup"><span data-stu-id="8b92d-151">You can't use the `in`, `ref`, and `out` keywords for the following kinds of methods:</span></span>  
  
- <span data-ttu-id="8b92d-152">使用 [async](async.md) 修飾詞定義的 async 方法。</span><span class="sxs-lookup"><span data-stu-id="8b92d-152">Async methods, which you define by using the [async](async.md) modifier.</span></span>  
- <span data-ttu-id="8b92d-153">迭代器方法，其包括 [yield return](yield.md) 或 `yield break` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8b92d-153">Iterator methods, which include a [yield return](yield.md) or `yield break` statement.</span></span>
- <span data-ttu-id="8b92d-154">擴充方法的第一個引數不能有 `in` 修飾詞，除非該引數是結構。</span><span class="sxs-lookup"><span data-stu-id="8b92d-154">The first argument of an extension method cannot have the `in` modifier unless that argument is a struct.</span></span>
- <span data-ttu-id="8b92d-155">擴充方法的第一個引數，也就是該引數是泛型型別 (即使該型別限制為結構時也一樣 ) </span><span class="sxs-lookup"><span data-stu-id="8b92d-155">The first argument of an extension method where that argument is a generic type (even when that type is constrained to be a struct.)</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="8b92d-156">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="8b92d-156">C# Language Specification</span></span>  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a><span data-ttu-id="8b92d-157">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8b92d-157">See also</span></span>

- [<span data-ttu-id="8b92d-158">C # 參考</span><span class="sxs-lookup"><span data-stu-id="8b92d-158">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="8b92d-159">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="8b92d-159">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="8b92d-160">C # 關鍵字</span><span class="sxs-lookup"><span data-stu-id="8b92d-160">C# Keywords</span></span>](index.md)
- [<span data-ttu-id="8b92d-161">方法參數</span><span class="sxs-lookup"><span data-stu-id="8b92d-161">Method Parameters</span></span>](method-parameters.md)
- [<span data-ttu-id="8b92d-162">撰寫安全有效率的程式碼</span><span class="sxs-lookup"><span data-stu-id="8b92d-162">Write safe efficient code</span></span>](../../write-safe-efficient-code.md)
