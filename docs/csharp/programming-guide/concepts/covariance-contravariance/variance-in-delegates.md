---
title: 委派中的差異 (C#)
description: 瞭解 .NET 中的變異數支援如何讓您將方法簽章與所有委派中的委派類型進行比對。
ms.date: 07/20/2015
ms.assetid: 19de89d2-8224-4406-8964-2965b732b890
ms.openlocfilehash: 02b59dd97cedc6ab35c3122912ee528f7ca29238
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/04/2020
ms.locfileid: "89466127"
---
# <a name="variance-in-delegates-c"></a><span data-ttu-id="db7ad-103">委派中的差異 (C#)</span><span class="sxs-lookup"><span data-stu-id="db7ad-103">Variance in Delegates (C#)</span></span>
<span data-ttu-id="db7ad-104">.NET framework 3.5 推出差異支援，在 C# 中比對方法簽章和所有委派的委派型別。</span><span class="sxs-lookup"><span data-stu-id="db7ad-104">.NET Framework 3.5 introduced variance support for matching method signatures with delegate types in all delegates in C#.</span></span> <span data-ttu-id="db7ad-105">這表示您可以指派給委派的不只是具有相符簽章的方法，也可以是會傳回更多衍生型別 (共變數) 的方法，或接受衍生型別 (反變數) 比委派型別指定少的參數的方法。</span><span class="sxs-lookup"><span data-stu-id="db7ad-105">This means that you can assign to delegates not only methods that have matching signatures, but also methods that return more derived types (covariance) or that accept parameters that have less derived types (contravariance) than that specified by the delegate type.</span></span> <span data-ttu-id="db7ad-106">這包括泛型和非泛型委派。</span><span class="sxs-lookup"><span data-stu-id="db7ad-106">This includes both generic and non-generic delegates.</span></span>  
  
 <span data-ttu-id="db7ad-107">例如，請考慮下列程式碼，有兩個類別和兩個委派︰泛型和非泛型。</span><span class="sxs-lookup"><span data-stu-id="db7ad-107">For example, consider the following code, which has two classes and two delegates: generic and non-generic.</span></span>  
  
```csharp  
public class First { }  
public class Second : First { }  
public delegate First SampleDelegate(Second a);  
public delegate R SampleGenericDelegate<A, R>(A a);  
```  
  
 <span data-ttu-id="db7ad-108">當您建立 `SampleDelegate` 或 `SampleGenericDelegate<A, R>` 型別的委派時，您可以指派下列任一方法給這些委派。</span><span class="sxs-lookup"><span data-stu-id="db7ad-108">When you create delegates of the `SampleDelegate` or `SampleGenericDelegate<A, R>` types, you can assign any one of the following methods to those delegates.</span></span>  
  
```csharp  
// Matching signature.  
public static First ASecondRFirst(Second second)  
{ return new First(); }  
  
// The return type is more derived.  
public static Second ASecondRSecond(Second second)  
{ return new Second(); }  
  
// The argument type is less derived.  
public static First AFirstRFirst(First first)  
{ return new First(); }  
  
// The return type is more derived
// and the argument type is less derived.  
public static Second AFirstRSecond(First first)  
{ return new Second(); }  
```  
  
 <span data-ttu-id="db7ad-109">下列程式碼範例會示範方法簽章與委派型別之間的隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="db7ad-109">The following code example illustrates the implicit conversion between the method signature and the delegate type.</span></span>  
  
```csharp  
// Assigning a method with a matching signature
// to a non-generic delegate. No conversion is necessary.  
SampleDelegate dNonGeneric = ASecondRFirst;  
// Assigning a method with a more derived return type
// and less derived argument type to a non-generic delegate.  
// The implicit conversion is used.  
SampleDelegate dNonGenericConversion = AFirstRSecond;  
  
// Assigning a method with a matching signature to a generic delegate.  
// No conversion is necessary.  
SampleGenericDelegate<Second, First> dGeneric = ASecondRFirst;  
// Assigning a method with a more derived return type
// and less derived argument type to a generic delegate.  
// The implicit conversion is used.  
SampleGenericDelegate<Second, First> dGenericConversion = AFirstRSecond;  
```  
  
 <span data-ttu-id="db7ad-110">如需更多範例，請參閱[在委派中使用差異 (C#)](./using-variance-in-delegates.md) 和[針對 Func 與 Action 泛型委派使用差異 (C#)](./using-variance-for-func-and-action-generic-delegates.md)。</span><span class="sxs-lookup"><span data-stu-id="db7ad-110">For more examples, see [Using Variance in Delegates (C#)](./using-variance-in-delegates.md) and [Using Variance for Func and Action Generic Delegates (C#)](./using-variance-for-func-and-action-generic-delegates.md).</span></span>  
  
## <a name="variance-in-generic-type-parameters"></a><span data-ttu-id="db7ad-111">泛型型別參數中的差異</span><span class="sxs-lookup"><span data-stu-id="db7ad-111">Variance in Generic Type Parameters</span></span>  
 <span data-ttu-id="db7ad-112">在 .NET Framework 4 或更新版本中可以啟用委派之間的隱含轉換，因此具有泛型型別參數所指定的不同型別的泛型委派可互相指派，如果型別繼承自彼此，如差異所要求。</span><span class="sxs-lookup"><span data-stu-id="db7ad-112">In .NET Framework 4 or later you can enable implicit conversion between delegates, so that generic delegates that have different types specified by generic type parameters can be assigned to each other, if the types are inherited from each other as required by variance.</span></span>  
  
 <span data-ttu-id="db7ad-113">若要啟用隱含轉換，您必須使用 `in` 或 `out` 關鍵字，明確宣告委派中的泛型參數為 Covariant 或 Contravariant。</span><span class="sxs-lookup"><span data-stu-id="db7ad-113">To enable implicit conversion, you must explicitly declare generic parameters in a delegate as covariant or contravariant by using the `in` or `out` keyword.</span></span>  
  
 <span data-ttu-id="db7ad-114">下列程式碼範例示範如何建立具有 Covariant 泛型型別參數的委派。</span><span class="sxs-lookup"><span data-stu-id="db7ad-114">The following code example shows how you can create a delegate that has a covariant generic type parameter.</span></span>  
  
```csharp  
// Type T is declared covariant by using the out keyword.  
public delegate T SampleGenericDelegate <out T>();  
  
public static void Test()  
{  
    SampleGenericDelegate <String> dString = () => " ";  
  
    // You can assign delegates to each other,  
    // because the type T is declared covariant.  
    SampleGenericDelegate <Object> dObject = dString;
}  
```  
  
 <span data-ttu-id="db7ad-115">如果您使用唯一的差異支援來比對方法簽章與委派型別，請不要使用 `in` 和 `out` 關鍵字，因為您會發現，有時候您會使用相同的 lambda 運算式或方法具現化委派，但無法將一個委派指派給另一個。</span><span class="sxs-lookup"><span data-stu-id="db7ad-115">If you use only variance support to match method signatures with delegate types and do not use the `in` and `out` keywords, you may find that sometimes you can instantiate delegates with identical lambda expressions or methods, but you cannot assign one delegate to another.</span></span>  
  
 <span data-ttu-id="db7ad-116">在下列程式碼範例中，`SampleGenericDelegate<String>` 無法明確地轉換成 `SampleGenericDelegate<Object>`，雖然 `String` 繼承 `Object`。</span><span class="sxs-lookup"><span data-stu-id="db7ad-116">In the following code example, `SampleGenericDelegate<String>` cannot be explicitly converted to `SampleGenericDelegate<Object>`, although `String` inherits `Object`.</span></span> <span data-ttu-id="db7ad-117">您可以使用 `out` 關鍵字標記泛型參數 `T`，修正這個問題。</span><span class="sxs-lookup"><span data-stu-id="db7ad-117">You can fix this problem by marking the generic parameter `T` with the `out` keyword.</span></span>  
  
```csharp  
public delegate T SampleGenericDelegate<T>();  
  
public static void Test()  
{  
    SampleGenericDelegate<String> dString = () => " ";  
  
    // You can assign the dObject delegate  
    // to the same lambda expression as dString delegate  
    // because of the variance support for
    // matching method signatures with delegate types.  
    SampleGenericDelegate<Object> dObject = () => " ";  
  
    // The following statement generates a compiler error  
    // because the generic type T is not marked as covariant.  
    // SampleGenericDelegate <Object> dObject = dString;  
  
}  
```  
  
### <a name="generic-delegates-that-have-variant-type-parameters-in-net"></a><span data-ttu-id="db7ad-118">在 .NET 中具有 Variant 型別參數的泛型委派</span><span class="sxs-lookup"><span data-stu-id="db7ad-118">Generic Delegates That Have Variant Type Parameters in .NET</span></span>

<span data-ttu-id="db7ad-119">.NET Framework 4 推出差異支援，適用於數個現有泛型委派中的泛型型別參數：</span><span class="sxs-lookup"><span data-stu-id="db7ad-119">.NET Framework 4 introduced variance support for generic type parameters in several existing generic delegates:</span></span>  
  
- <span data-ttu-id="db7ad-120"><xref:System> 命名空間中的 `Action` 委派，例如 <xref:System.Action%601> 和 <xref:System.Action%602></span><span class="sxs-lookup"><span data-stu-id="db7ad-120">`Action` delegates from the <xref:System> namespace, for example, <xref:System.Action%601> and <xref:System.Action%602></span></span>  
  
- <span data-ttu-id="db7ad-121"><xref:System> 命名空間中的 `Func` 委派，例如 <xref:System.Func%601> 和 <xref:System.Func%602></span><span class="sxs-lookup"><span data-stu-id="db7ad-121">`Func` delegates from the <xref:System> namespace, for example, <xref:System.Func%601> and <xref:System.Func%602></span></span>  
  
- <span data-ttu-id="db7ad-122"><xref:System.Predicate%601> 委派</span><span class="sxs-lookup"><span data-stu-id="db7ad-122">The <xref:System.Predicate%601> delegate</span></span>  
  
- <span data-ttu-id="db7ad-123"><xref:System.Comparison%601> 委派</span><span class="sxs-lookup"><span data-stu-id="db7ad-123">The <xref:System.Comparison%601> delegate</span></span>  
  
- <span data-ttu-id="db7ad-124"><xref:System.Converter%602> 委派</span><span class="sxs-lookup"><span data-stu-id="db7ad-124">The <xref:System.Converter%602> delegate</span></span>  
  
 <span data-ttu-id="db7ad-125">如需詳細資訊及更多範例，請參閱[針對 Func 與 Action 泛型委派使用差異 (C#)](./using-variance-for-func-and-action-generic-delegates.md)。</span><span class="sxs-lookup"><span data-stu-id="db7ad-125">For more information and examples, see [Using Variance for Func and Action Generic Delegates (C#)](./using-variance-for-func-and-action-generic-delegates.md).</span></span>  
  
### <a name="declaring-variant-type-parameters-in-generic-delegates"></a><span data-ttu-id="db7ad-126">宣告泛型委派中的 Variant 型別參數</span><span class="sxs-lookup"><span data-stu-id="db7ad-126">Declaring Variant Type Parameters in Generic Delegates</span></span>  
 <span data-ttu-id="db7ad-127">如果泛型委派具有 Covariant 或 Contravariant 泛型型別參數，它可以稱之為「Variant 泛型委派」\*\*。</span><span class="sxs-lookup"><span data-stu-id="db7ad-127">If a generic delegate has covariant or contravariant generic type parameters, it can be referred to as a *variant generic delegate*.</span></span>  
  
 <span data-ttu-id="db7ad-128">您可以使用 `out` 關鍵字將泛型委派中的泛型型別參數宣告為 Covariant。</span><span class="sxs-lookup"><span data-stu-id="db7ad-128">You can declare a generic type parameter covariant in a generic delegate by using the `out` keyword.</span></span> <span data-ttu-id="db7ad-129">Covariant 型別僅可用為方法傳回型別，不能用為方法引數的型別。</span><span class="sxs-lookup"><span data-stu-id="db7ad-129">The covariant type can be used only as a method return type and not as a type of method arguments.</span></span> <span data-ttu-id="db7ad-130">以下程式碼範例會示範如何宣告 Covariant 泛型委派。</span><span class="sxs-lookup"><span data-stu-id="db7ad-130">The following code example shows how to declare a covariant generic delegate.</span></span>  
  
```csharp  
public delegate R DCovariant<out R>();  
```  
  
 <span data-ttu-id="db7ad-131">您可以使用 `in` 關鍵字將泛型委派中的泛型型別參數宣告為 Contravariant。</span><span class="sxs-lookup"><span data-stu-id="db7ad-131">You can declare a generic type parameter contravariant in a generic delegate by using the `in` keyword.</span></span> <span data-ttu-id="db7ad-132">Contravariant 型別僅可用為方法引數的型別，不能用為方法傳回型別。</span><span class="sxs-lookup"><span data-stu-id="db7ad-132">The contravariant type can be used only as a type of method arguments and not as a method return type.</span></span> <span data-ttu-id="db7ad-133">以下程式碼範例會示範如何宣告 Contravariant 泛型委派。</span><span class="sxs-lookup"><span data-stu-id="db7ad-133">The following code example shows how to declare a contravariant generic delegate.</span></span>  
  
```csharp  
public delegate void DContravariant<in A>(A a);  
```  
  
> [!IMPORTANT]
> <span data-ttu-id="db7ad-134">C# 中的 `ref`、`in` 和 `out` 參數不可標示為可變動。</span><span class="sxs-lookup"><span data-stu-id="db7ad-134">`ref`, `in`, and `out` parameters in C# can't be marked as variant.</span></span>  
  
 <span data-ttu-id="db7ad-135">您也可以支援相同委派中不同型別參數的差異和共變數。</span><span class="sxs-lookup"><span data-stu-id="db7ad-135">It is also possible to support both variance and covariance in the same delegate, but for different type parameters.</span></span> <span data-ttu-id="db7ad-136">下列範例會顯示這一點。</span><span class="sxs-lookup"><span data-stu-id="db7ad-136">This is shown in the following example.</span></span>  
  
```csharp  
public delegate R DVariant<in A, out R>(A a);  
```  
  
### <a name="instantiating-and-invoking-variant-generic-delegates"></a><span data-ttu-id="db7ad-137">具現化及叫用 Variant 泛型委派</span><span class="sxs-lookup"><span data-stu-id="db7ad-137">Instantiating and Invoking Variant Generic Delegates</span></span>  
 <span data-ttu-id="db7ad-138">您可以具現化及叫用 Variant 委派，一如您具現化及叫用非變異委派。</span><span class="sxs-lookup"><span data-stu-id="db7ad-138">You can instantiate and invoke variant delegates just as you instantiate and invoke invariant delegates.</span></span> <span data-ttu-id="db7ad-139">在下例中，委派是由 lambda 運算式具現化。</span><span class="sxs-lookup"><span data-stu-id="db7ad-139">In the following example, the delegate is instantiated by a lambda expression.</span></span>  
  
```csharp  
DVariant<String, String> dvariant = (String str) => str + " ";  
dvariant("test");  
```  
  
### <a name="combining-variant-generic-delegates"></a><span data-ttu-id="db7ad-140">結合 Variant 泛型委派</span><span class="sxs-lookup"><span data-stu-id="db7ad-140">Combining Variant Generic Delegates</span></span>  

<span data-ttu-id="db7ad-141">請勿合併 variant 委派。</span><span class="sxs-lookup"><span data-stu-id="db7ad-141">Don't combine variant delegates.</span></span> <span data-ttu-id="db7ad-142"><xref:System.Delegate.Combine%2A> 方法不支援 Variant 委派轉換，且委派的類型必須完全一致。</span><span class="sxs-lookup"><span data-stu-id="db7ad-142">The <xref:System.Delegate.Combine%2A> method does not support variant delegate conversion and expects delegates to be of exactly the same type.</span></span> <span data-ttu-id="db7ad-143">當您使用 <xref:System.Delegate.Combine%2A> 方法或使用 `+` 運算子合併委派時，這會導致執行階段例外狀況，如下列程式碼範例所示。</span><span class="sxs-lookup"><span data-stu-id="db7ad-143">This can lead to a run-time exception when you combine delegates either by using the <xref:System.Delegate.Combine%2A> method or by using the `+` operator, as shown in the following code example.</span></span>  
  
```csharp  
Action<object> actObj = x => Console.WriteLine("object: {0}", x);  
Action<string> actStr = x => Console.WriteLine("string: {0}", x);  
// All of the following statements throw exceptions at run time.  
// Action<string> actCombine = actStr + actObj;  
// actStr += actObj;  
// Delegate.Combine(actStr, actObj);  
```  
  
## <a name="variance-in-generic-type-parameters-for-value-and-reference-types"></a><span data-ttu-id="db7ad-144">實值型別和參考型別的泛型型別參數中的差異</span><span class="sxs-lookup"><span data-stu-id="db7ad-144">Variance in Generic Type Parameters for Value and Reference Types</span></span>  
 <span data-ttu-id="db7ad-145">僅參考型別支援泛型型別參數的差異。</span><span class="sxs-lookup"><span data-stu-id="db7ad-145">Variance for generic type parameters is supported for reference types only.</span></span> <span data-ttu-id="db7ad-146">例如，因為整數是實值型別，所以 `DVariant<int>` 無法以隱含方式轉換成`DVariant<Object>` 或 `DVariant<long>`。</span><span class="sxs-lookup"><span data-stu-id="db7ad-146">For example, `DVariant<int>` can't be implicitly converted to `DVariant<Object>` or `DVariant<long>`, because integer is a value type.</span></span>  
  
 <span data-ttu-id="db7ad-147">下例示範實值型別不支援的泛型型別參數的差異。</span><span class="sxs-lookup"><span data-stu-id="db7ad-147">The following example demonstrates that variance in generic type parameters is not supported for value types.</span></span>  
  
```csharp  
// The type T is covariant.  
public delegate T DVariant<out T>();  
  
// The type T is invariant.  
public delegate T DInvariant<T>();  
  
public static void Test()  
{  
    int i = 0;  
    DInvariant<int> dInt = () => i;  
    DVariant<int> dVariantInt = () => i;  
  
    // All of the following statements generate a compiler error  
    // because type variance in generic parameters is not supported  
    // for value types, even if generic type parameters are declared variant.  
    // DInvariant<Object> dObject = dInt;  
    // DInvariant<long> dLong = dInt;  
    // DVariant<Object> dVariantObject = dVariantInt;  
    // DVariant<long> dVariantLong = dVariantInt;
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="db7ad-148">另請參閱</span><span class="sxs-lookup"><span data-stu-id="db7ad-148">See also</span></span>

- [<span data-ttu-id="db7ad-149">泛型</span><span class="sxs-lookup"><span data-stu-id="db7ad-149">Generics</span></span>](../../../../standard/generics/index.md)
- [<span data-ttu-id="db7ad-150">針對 Func 與 Action 泛型委派使用變異數 (C#)</span><span class="sxs-lookup"><span data-stu-id="db7ad-150">Using Variance for Func and Action Generic Delegates (C#)</span></span>](./using-variance-for-func-and-action-generic-delegates.md)
- [<span data-ttu-id="db7ad-151">如何將委派合併 (多播委派) </span><span class="sxs-lookup"><span data-stu-id="db7ad-151">How to combine delegates (Multicast Delegates)</span></span>](../../delegates/how-to-combine-delegates-multicast-delegates.md)
