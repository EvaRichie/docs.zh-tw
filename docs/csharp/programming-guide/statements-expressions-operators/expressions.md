---
title: 運算式 - C# 程式設計指南
description: '瞭解 c # 程式設計中的運算式，例如調用、查詢、lambda、常值和簡單名稱。'
ms.date: 05/11/2017
helpviewer_keywords:
- expressions [C#]
- C# language, expressions
ms.assetid: c7d8feb0-0e58-4f94-8bf6-4d070550a832
ms.openlocfilehash: 5bcfdae27c30bd5d845f621ac4b5b20ff37612a0
ms.sourcegitcommit: 552b4b60c094559db9d8178fa74f5bafaece0caf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87381823"
---
# <a name="expressions-c-programming-guide"></a><span data-ttu-id="93321-103">運算式 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="93321-103">Expressions (C# Programming Guide)</span></span>

<span data-ttu-id="93321-104">「運算式」\*\* 是一連串的一或多個運算元以及零或多個[運算子](../../language-reference/operators/index.md)，可以評估為單一值、物件、方法或命名空間。</span><span class="sxs-lookup"><span data-stu-id="93321-104">An *expression* is a sequence of one or more operands and zero or more [operators](../../language-reference/operators/index.md) that can be evaluated to a single value, object, method, or namespace.</span></span> <span data-ttu-id="93321-105">運算式可以包含常值、方法呼叫、運算子和其運算元，或「簡單名稱」\*\*。</span><span class="sxs-lookup"><span data-stu-id="93321-105">Expressions can consist of a literal value, a method invocation, an operator and its operands, or a *simple name*.</span></span> <span data-ttu-id="93321-106">簡單名稱可以是變數、型別成員、方法參數、命名空間或型別的名稱。</span><span class="sxs-lookup"><span data-stu-id="93321-106">Simple names can be the name of a variable, type member, method parameter, namespace or type.</span></span>  
  
 <span data-ttu-id="93321-107">運算式可以使用運算子 (後者又可能使用其他運算式當作參數) 或方法呼叫 (它的參數又可能是其他方法呼叫)，因此運算式的範圍可以從簡單到非常複雜。</span><span class="sxs-lookup"><span data-stu-id="93321-107">Expressions can use operators that in turn use other expressions as parameters, or method calls whose parameters are in turn other method calls, so expressions can range from simple to very complex.</span></span> <span data-ttu-id="93321-108">下列是兩個運算式範例：</span><span class="sxs-lookup"><span data-stu-id="93321-108">Following are two examples of expressions:</span></span>  
  
```csharp  
((x < 10) && ( x > 5)) || ((x > 20) && (x < 25));

System.Convert.ToInt32("35");  
```  
  
## <a name="expression-values"></a><span data-ttu-id="93321-109">運算式值</span><span class="sxs-lookup"><span data-stu-id="93321-109">Expression values</span></span>

 <span data-ttu-id="93321-110">在大部分使用運算式的內容中 (例如在陳述式或方法參數中)，運算式必須評估為某個值。</span><span class="sxs-lookup"><span data-stu-id="93321-110">In most of the contexts in which expressions are used, for example in statements or method parameters, the expression is expected to evaluate to some value.</span></span> <span data-ttu-id="93321-111">如果 x 和 y 是整數，則運算式 `x + y` 評估為數值。</span><span class="sxs-lookup"><span data-stu-id="93321-111">If x and y are integers, the expression `x + y` evaluates to a numeric value.</span></span> <span data-ttu-id="93321-112">運算式 `new MyClass()` 評估為 `MyClass` 類別之新執行個體的參考。</span><span class="sxs-lookup"><span data-stu-id="93321-112">The expression `new MyClass()` evaluates to a reference to a new instance of a `MyClass` class.</span></span> <span data-ttu-id="93321-113">運算式 `myClass.ToString()` 評估為字串，因為這是方法的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="93321-113">The expression `myClass.ToString()` evaluates to a string because that is the return type of the method.</span></span> <span data-ttu-id="93321-114">不過，雖然命名空間名稱分類為運算式，但是未評估為值，因此絕不會有任何運算式的最終結果。</span><span class="sxs-lookup"><span data-stu-id="93321-114">However, although a namespace name is classified as an expression, it does not evaluate to a value and therefore can never be the final result of any expression.</span></span> <span data-ttu-id="93321-115">您無法將命名空間名稱傳遞給方法參數，或用於新的運算式，或將它指派給變數。</span><span class="sxs-lookup"><span data-stu-id="93321-115">You cannot pass a namespace name to a method parameter, or use it in a new expression, or assign it to a variable.</span></span> <span data-ttu-id="93321-116">您只能將它用作較大運算式中的子運算式。</span><span class="sxs-lookup"><span data-stu-id="93321-116">You can only use it as a sub-expression in a larger expression.</span></span> <span data-ttu-id="93321-117">這也適用於類型 (與 <xref:System.Type?displayProperty=nameWithType> 物件不同)、方法群組名稱 (與特定方法不同) 以及事件 [add](../../language-reference/keywords/add.md) 和 [remove](../../language-reference/keywords/remove.md) 存取子。</span><span class="sxs-lookup"><span data-stu-id="93321-117">The same is true for types (as distinct from <xref:System.Type?displayProperty=nameWithType> objects), method group names (as distinct from specific methods), and event [add](../../language-reference/keywords/add.md) and [remove](../../language-reference/keywords/remove.md) accessors.</span></span>  
  
 <span data-ttu-id="93321-118">每個值都有關聯型別。</span><span class="sxs-lookup"><span data-stu-id="93321-118">Every value has an associated type.</span></span> <span data-ttu-id="93321-119">例如，如果 x 和 y 都是 `int` 類型的變數，則運算式 `x + y` 的值也會輸入為 `int`。</span><span class="sxs-lookup"><span data-stu-id="93321-119">For example, if x and y are both variables of type `int`, the value of the expression `x + y` is also typed as `int`.</span></span> <span data-ttu-id="93321-120">如果將值指派給不同類型的變數，或者，如果 x 和 y 是不同的類型，則會套用類型轉換規則。</span><span class="sxs-lookup"><span data-stu-id="93321-120">If the value is assigned to a variable of a different type, or if x and y are different types, the rules of type conversion are applied.</span></span> <span data-ttu-id="93321-121">如需這類轉換運作方式的詳細資訊，請參閱[轉換和類型轉換](../types/casting-and-type-conversions.md)。</span><span class="sxs-lookup"><span data-stu-id="93321-121">For more information about how such conversions work, see [Casting and Type Conversions](../types/casting-and-type-conversions.md).</span></span>  
  
## <a name="overflows"></a><span data-ttu-id="93321-122">溢出</span><span class="sxs-lookup"><span data-stu-id="93321-122">Overflows</span></span>

 <span data-ttu-id="93321-123">如果值大於實值型別的最大值，則數值運算式可能會造成溢位。</span><span class="sxs-lookup"><span data-stu-id="93321-123">Numeric expressions may cause overflows if the value is larger than the maximum value of the value's type.</span></span> <span data-ttu-id="93321-124">如需詳細資訊，請參閱[已檢查和未核](../../language-reference/keywords/checked-and-unchecked.md)取，以及[內建數值轉換](../../language-reference/builtin-types/numeric-conversions.md)一文的[明確數值轉換](../../language-reference/builtin-types/numeric-conversions.md#explicit-numeric-conversions)一節。</span><span class="sxs-lookup"><span data-stu-id="93321-124">For more information, see [Checked and Unchecked](../../language-reference/keywords/checked-and-unchecked.md) and the [Explicit numeric conversions](../../language-reference/builtin-types/numeric-conversions.md#explicit-numeric-conversions) section of the [Built-in numeric conversions](../../language-reference/builtin-types/numeric-conversions.md) article.</span></span>
  
## <a name="operator-precedence-and-associativity"></a><span data-ttu-id="93321-125">運算子優先順序和關聯性</span><span class="sxs-lookup"><span data-stu-id="93321-125">Operator precedence and associativity</span></span>

 <span data-ttu-id="93321-126">運算式的評估方式受到關聯性和運算子優先順序規則的管理。</span><span class="sxs-lookup"><span data-stu-id="93321-126">The manner in which an expression is evaluated is governed by the rules of associativity and operator precedence.</span></span> <span data-ttu-id="93321-127">如需詳細資訊，請參閱 [運算子](../../language-reference/operators/index.md)。</span><span class="sxs-lookup"><span data-stu-id="93321-127">For more information, see [Operators](../../language-reference/operators/index.md).</span></span>  
  
 <span data-ttu-id="93321-128">大多數的運算式 (指派運算式和方法叫用運算式除外) 必須內嵌在陳述式中。</span><span class="sxs-lookup"><span data-stu-id="93321-128">Most expressions, except assignment expressions and method invocation expressions, must be embedded in a statement.</span></span> <span data-ttu-id="93321-129">如需詳細資訊，請參閱[陳述式](./statements.md)。</span><span class="sxs-lookup"><span data-stu-id="93321-129">For more information, see [Statements](./statements.md).</span></span>  
  
## <a name="literals-and-simple-names"></a><span data-ttu-id="93321-130">常值和簡單名稱</span><span class="sxs-lookup"><span data-stu-id="93321-130">Literals and simple names</span></span>

 <span data-ttu-id="93321-131">兩個最簡單類型的運算式是常值和簡單名稱。</span><span class="sxs-lookup"><span data-stu-id="93321-131">The two simplest types of expressions are literals and simple names.</span></span> <span data-ttu-id="93321-132">常值是沒有名稱的常數值。</span><span class="sxs-lookup"><span data-stu-id="93321-132">A literal is a constant value that has no name.</span></span> <span data-ttu-id="93321-133">例如，在下列程式碼範例中，`5` 和 `"Hello World"` 都是常值︰</span><span class="sxs-lookup"><span data-stu-id="93321-133">For example, in the following code example, both `5` and `"Hello World"` are literal values:</span></span>  
  
 [!code-csharp[csProgGuideStatements#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#2)]  
  
 <span data-ttu-id="93321-134">如需常值的詳細資訊，請參閱[類型](/dotnet/csharp/language-reference/keywords)。</span><span class="sxs-lookup"><span data-stu-id="93321-134">For more information on literals, see [Types](/dotnet/csharp/language-reference/keywords).</span></span>  
  
 <span data-ttu-id="93321-135">在上述範例中，`i` 和 `s` 是識別區域變數的簡單名稱。</span><span class="sxs-lookup"><span data-stu-id="93321-135">In the preceding example, both `i` and `s` are simple names that identify local variables.</span></span> <span data-ttu-id="93321-136">在運算式中使用這些變數時，變數名稱會評估為目前儲存在記憶體中變數位置的值。</span><span class="sxs-lookup"><span data-stu-id="93321-136">When those variables are used in an expression, the variable name evaluates to the value that is currently stored in the variable's location in memory.</span></span> <span data-ttu-id="93321-137">下列範例會顯示這一點：</span><span class="sxs-lookup"><span data-stu-id="93321-137">This is shown in the following example:</span></span>  
  
 [!code-csharp[csProgGuideStatements#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#3)]

## <a name="invocation-expressions"></a><span data-ttu-id="93321-138">叫用運算式</span><span class="sxs-lookup"><span data-stu-id="93321-138">Invocation expressions</span></span>

 <span data-ttu-id="93321-139">在下列程式碼範例中，`DoWork` 呼叫是叫用運算式。</span><span class="sxs-lookup"><span data-stu-id="93321-139">In the following code example, the call to `DoWork` is an invocation expression.</span></span>  
  
```csharp
DoWork();  
```  
  
 <span data-ttu-id="93321-140">方法叫用需要後面接著括弧和任何方法參數的方法名稱，這是先前範例中的名稱，或另一個運算式的結果。</span><span class="sxs-lookup"><span data-stu-id="93321-140">A method invocation requires the name of the method, either as a name as in the previous example, or as the result of another expression, followed by parenthesis and any method parameters.</span></span> <span data-ttu-id="93321-141">如需詳細資訊，請參閱[方法](../classes-and-structs/methods.md)。</span><span class="sxs-lookup"><span data-stu-id="93321-141">For more information, see [Methods](../classes-and-structs/methods.md).</span></span> <span data-ttu-id="93321-142">委派叫用會使用以括弧括住的委派和方法參數名稱。</span><span class="sxs-lookup"><span data-stu-id="93321-142">A delegate invocation uses the name of a delegate and method parameters in parenthesis.</span></span> <span data-ttu-id="93321-143">如需詳細資訊，請參閱 [委派](../delegates/index.md)中定義的介面的私用 C++ 專屬實作。</span><span class="sxs-lookup"><span data-stu-id="93321-143">For more information, see [Delegates](../delegates/index.md).</span></span> <span data-ttu-id="93321-144">如果方法傳回值，則方法叫用和委派叫用會評估為方法的傳回值。</span><span class="sxs-lookup"><span data-stu-id="93321-144">Method invocations and delegate invocations evaluate to the return value of the method, if the method returns a value.</span></span> <span data-ttu-id="93321-145">傳回 void 的方法不能用來取代運算式中的值。</span><span class="sxs-lookup"><span data-stu-id="93321-145">Methods that return void cannot be used in place of a value in an expression.</span></span>  

## <a name="query-expressions"></a><span data-ttu-id="93321-146">查詢運算式</span><span class="sxs-lookup"><span data-stu-id="93321-146">Query expressions</span></span>

 <span data-ttu-id="93321-147">運算式的相同規則通常會套用到查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="93321-147">The same rules for expressions in general apply to query expressions.</span></span> <span data-ttu-id="93321-148">如需詳細資訊，請參閱 [LINQ](../../linq/index.md)。</span><span class="sxs-lookup"><span data-stu-id="93321-148">For more information, see [LINQ](../../linq/index.md).</span></span>  
  
## <a name="lambda-expressions"></a><span data-ttu-id="93321-149">Lambda 運算式</span><span class="sxs-lookup"><span data-stu-id="93321-149">Lambda expressions</span></span>

 <span data-ttu-id="93321-150">Lambda 運算式代表「內嵌方法」，而這種方法沒有名稱，但可以有輸入參數和多個陳述式。</span><span class="sxs-lookup"><span data-stu-id="93321-150">Lambda expressions represent "inline methods" that have no name but can have input parameters and multiple statements.</span></span> <span data-ttu-id="93321-151">它們廣泛用於 LINQ，以將引數傳遞給方法。</span><span class="sxs-lookup"><span data-stu-id="93321-151">They are used extensively in LINQ to pass arguments to methods.</span></span> <span data-ttu-id="93321-152">根據所使用的內容，會將 Lambda 運算式編譯為委派或運算式樹狀架構。</span><span class="sxs-lookup"><span data-stu-id="93321-152">Lambda expressions are compiled to either delegates or expression trees depending on the context in which they are used.</span></span> <span data-ttu-id="93321-153">如需詳細資訊，請參閱[Lambda 運算式](lambda-expressions.md)。</span><span class="sxs-lookup"><span data-stu-id="93321-153">For more information, see [Lambda Expressions](lambda-expressions.md).</span></span>  
  
## <a name="expression-trees"></a><span data-ttu-id="93321-154">運算式樹狀架構</span><span class="sxs-lookup"><span data-stu-id="93321-154">Expression trees</span></span>

<span data-ttu-id="93321-155">運算式樹狀架構會將運算式代表為資料結構。</span><span class="sxs-lookup"><span data-stu-id="93321-155">Expression trees enable expressions to be represented as data structures.</span></span> <span data-ttu-id="93321-156">LINQ 提供者廣泛使用它們，以將查詢運算式轉譯為某個其他內容中有意義的程式碼，例如 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="93321-156">They are used extensively by LINQ providers to translate query expressions into code that is meaningful in some other context, such as a SQL database.</span></span> <span data-ttu-id="93321-157">如需詳細資訊，請參閱[運算式樹狀架構 (C#)](../concepts/expression-trees/index.md)。</span><span class="sxs-lookup"><span data-stu-id="93321-157">For more information, see [Expression Trees (C#)](../concepts/expression-trees/index.md).</span></span>
  
## <a name="expression-body-definitions"></a><span data-ttu-id="93321-158">運算式主體定義</span><span class="sxs-lookup"><span data-stu-id="93321-158">Expression body definitions</span></span>

<span data-ttu-id="93321-159">C# 支援「運算式主體成員」\*\*，可讓您提供方法、建構函式、完成項、屬性和索引子的精簡運算式主體定義。</span><span class="sxs-lookup"><span data-stu-id="93321-159">C# supports *expression-bodied members*, which allow you to supply a concise expression body definition for methods, constructors, finalizers, properties, and indexers.</span></span> <span data-ttu-id="93321-160">如需詳細資訊，請參閱[運算式主體成員](expression-bodied-members.md)。</span><span class="sxs-lookup"><span data-stu-id="93321-160">For more information, see [Expression-bodied members](expression-bodied-members.md).</span></span>

## <a name="remarks"></a><span data-ttu-id="93321-161">備註</span><span class="sxs-lookup"><span data-stu-id="93321-161">Remarks</span></span>

 <span data-ttu-id="93321-162">只要從運算式識別變數、物件屬性或物件索引子存取，就會使用該項目的值作為運算式的值。</span><span class="sxs-lookup"><span data-stu-id="93321-162">Whenever a variable, object property, or object indexer access is identified from an expression, the value of that item is used as the value of the expression.</span></span> <span data-ttu-id="93321-163">只要運算式最後評估為必要類型，就可以將運算式放在 C# 中需要值或物件的任何位置。</span><span class="sxs-lookup"><span data-stu-id="93321-163">An expression can be placed anywhere in C# where a value or object is required, as long as the expression ultimately evaluates to the required type.</span></span>  

## <a name="c-language-specification"></a><span data-ttu-id="93321-164">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="93321-164">C# language specification</span></span>

<span data-ttu-id="93321-165">如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[運算式](~/_csharplang/spec/expressions.md)一節。</span><span class="sxs-lookup"><span data-stu-id="93321-165">For more information, see the [Expressions](~/_csharplang/spec/expressions.md) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="93321-166">另請參閱</span><span class="sxs-lookup"><span data-stu-id="93321-166">See also</span></span>

- [<span data-ttu-id="93321-167">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="93321-167">C# Programming Guide</span></span>](../index.md)
- [<span data-ttu-id="93321-168">運算子</span><span class="sxs-lookup"><span data-stu-id="93321-168">Operators</span></span>](../../language-reference/operators/index.md)
- [<span data-ttu-id="93321-169">方法</span><span class="sxs-lookup"><span data-stu-id="93321-169">Methods</span></span>](../classes-and-structs/methods.md)
- [<span data-ttu-id="93321-170">委派</span><span class="sxs-lookup"><span data-stu-id="93321-170">Delegates</span></span>](../delegates/index.md)
- [<span data-ttu-id="93321-171">類型</span><span class="sxs-lookup"><span data-stu-id="93321-171">Types</span></span>](../types/index.md)
- [<span data-ttu-id="93321-172">LINQ</span><span class="sxs-lookup"><span data-stu-id="93321-172">LINQ</span></span>](../../linq/index.md)
