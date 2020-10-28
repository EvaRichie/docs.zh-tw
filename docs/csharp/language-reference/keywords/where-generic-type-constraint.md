---
description: where (泛型類型條件約束) - C# 參考
title: where (泛型類型條件約束) - C# 參考
ms.date: 04/15/2020
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
- classconstraint_CSharpKeyword
- structconstraint_CSharpKeyword
- enumconstraint_CSharpKeyword
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.openlocfilehash: ff2d50b2148ea62e5bef5eceda547a976e4abf02
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687319"
---
# <a name="where-generic-type-constraint-c-reference"></a><span data-ttu-id="ae3b1-103">where (泛型類型條件約束) (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="ae3b1-103">where (generic type constraint) (C# Reference)</span></span>

<span data-ttu-id="ae3b1-104">泛型定義中的 `where` 子句指定型別上的條件約束，以用來作為泛型型別、方法、委派或本機函式中型別參數的引數。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-104">The `where` clause in a generic definition specifies constraints on the types that are used as arguments for type parameters in a generic type, method, delegate, or local function.</span></span> <span data-ttu-id="ae3b1-105">條件約束可以指定介面、基類或要求泛型型別作為參考、值或非受控型別。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-105">Constraints can specify interfaces, base classes, or require a generic type to be a reference, value, or unmanaged type.</span></span> <span data-ttu-id="ae3b1-106">它們會宣告型別引數必須具有的功能。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-106">They declare capabilities that the type argument must have.</span></span>

<span data-ttu-id="ae3b1-107">例如，您可以宣告泛型類別 `MyGenericClass`，讓型別參數 `T` 實作 <xref:System.IComparable%601> 介面：</span><span class="sxs-lookup"><span data-stu-id="ae3b1-107">For example, you can declare a generic class, `MyGenericClass`, such that the type parameter `T` implements the <xref:System.IComparable%601> interface:</span></span>

[!code-csharp[using an interface constraint](snippets/GenericWhereConstraints.cs#1)]

> [!NOTE]
> <span data-ttu-id="ae3b1-108">如需查詢運算式中 where 子句的詳細資訊，請參閱 [where 子句](where-clause.md)。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-108">For more information on the where clause in a query expression, see [where clause](where-clause.md).</span></span>

<span data-ttu-id="ae3b1-109">`where` 子句也可以包含基底類別條件約束。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-109">The `where` clause can also include a base class constraint.</span></span> <span data-ttu-id="ae3b1-110">基類條件約束指出要當做該泛型型別的型別引數使用的型別具有指定的類別做為基類，或者是基類。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-110">The base class constraint states that a type to be used as a type argument for that generic type has the specified class as a base class, or is that base class.</span></span> <span data-ttu-id="ae3b1-111">如果使用基底類別條件約束，則它必須出現在該型別參數的任何其他條件約束之前。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-111">If the base class constraint is used, it must appear before any other constraints on that type parameter.</span></span> <span data-ttu-id="ae3b1-112">某些型別不允許作為基底類別條件約束：<xref:System.Object>、<xref:System.Array> 和 <xref:System.ValueType>。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-112">Some types are disallowed as a base class constraint: <xref:System.Object>, <xref:System.Array>, and <xref:System.ValueType>.</span></span> <span data-ttu-id="ae3b1-113">在 c # 7.3 之前，、 <xref:System.Enum> <xref:System.Delegate> 和 <xref:System.MulticastDelegate> 也不允許作為基類條件約束。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-113">Before C# 7.3, <xref:System.Enum>, <xref:System.Delegate>, and <xref:System.MulticastDelegate> were also disallowed as base class constraints.</span></span> <span data-ttu-id="ae3b1-114">下列範例會顯示現在可以指定為基底類別的型別：</span><span class="sxs-lookup"><span data-stu-id="ae3b1-114">The following example shows the types that can now be specified as a base class:</span></span>

[!code-csharp[using an interface constraint](snippets/GenericWhereConstraints.cs#2)]

<span data-ttu-id="ae3b1-115">在 c # 8.0 和更新版本中可為 null 的內容中，會強制執行基底類別型別的可 null 性。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-115">In a nullable context in C# 8.0 and later, the nullability of the base class type is enforced.</span></span> <span data-ttu-id="ae3b1-116">如果基類不是可為 null 的 (例如 `Base`) ，則類型引數必須不可為 null。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-116">If the base class is non-nullable (for example `Base`), the type argument must be non-nullable.</span></span> <span data-ttu-id="ae3b1-117">如果基類可為 null (例如 `Base?`) ，則型別引數可以是可為 null 或不可為 null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-117">If the base class is nullable (for example `Base?`), the type argument may be either a nullable or non-nullable reference type.</span></span> <span data-ttu-id="ae3b1-118">當基類不可為 null 時，如果類型引數是可為 null 的參考型別，則編譯器會發出警告。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-118">The compiler issues a warning if the type argument is a nullable reference type when the base class is non-nullable.</span></span>

<span data-ttu-id="ae3b1-119">`where` 子句可以指定型別是 `class` 或 `struct`。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-119">The `where` clause can specify that the type is a `class` or a `struct`.</span></span> <span data-ttu-id="ae3b1-120">`struct` 條件約束不需要指定 `System.ValueType` 的基底類別條件約束。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-120">The `struct` constraint removes the need to specify a base class constraint of `System.ValueType`.</span></span> <span data-ttu-id="ae3b1-121">`System.ValueType` 型別不能用作基底類別條件約束。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-121">The `System.ValueType` type may not be used as a base class constraint.</span></span> <span data-ttu-id="ae3b1-122">下列範例顯示 `class` 和 `struct` 條件約束：</span><span class="sxs-lookup"><span data-stu-id="ae3b1-122">The following example shows both the `class` and `struct` constraints:</span></span>

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#3)]

<span data-ttu-id="ae3b1-123">在 c # 8.0 和更新版本中可為 null 的內容中， `class` 條件約束需要型別為不可為 null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-123">In a nullable context in C# 8.0 and later, the `class` constraint requires a type to be a non-nullable reference type.</span></span> <span data-ttu-id="ae3b1-124">若要允許可為 null 的參考型別，請使用 `class?` 條件約束，此條件約束允許可為 null 且不可為 null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-124">To allow nullable reference types, use the `class?` constraint, which allows both nullable and non-nullable reference types.</span></span>

<span data-ttu-id="ae3b1-125">`where`子句可能包含 `notnull` 條件約束。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-125">The `where` clause may include the `notnull` constraint.</span></span> <span data-ttu-id="ae3b1-126">`notnull`條件約束會將類型參數限制為不可為 null 的類型。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-126">The `notnull` constraint limits the type parameter to non-nullable types.</span></span> <span data-ttu-id="ae3b1-127">該型別可以是實 [值型](../builtin-types/value-types.md) 別，也可以是不可為 null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-127">That type may be a [value type](../builtin-types/value-types.md) or a non-nullable reference type.</span></span> <span data-ttu-id="ae3b1-128">`notnull`從 c # 8.0 開始，可以在[ `nullable enable` 內容](../../nullable-references.md#nullable-contexts)中編譯的程式碼使用條件約束。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-128">The `notnull` constraint is available starting in C# 8.0 for code compiled in a [`nullable enable` context](../../nullable-references.md#nullable-contexts).</span></span> <span data-ttu-id="ae3b1-129">與其他條件約束不同的是，如果型別引數違反 `notnull` 條件約束，則編譯器會產生警告而非錯誤。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-129">Unlike other constraints, if a type argument violates the `notnull` constraint, the compiler generates a warning instead of an error.</span></span> <span data-ttu-id="ae3b1-130">只有在內容中才會產生警告 `nullable enable` 。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-130">Warnings are only generated in a `nullable enable` context.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae3b1-131">包含條件約束的泛型宣告 `notnull` 可用於可為 null 的無警示內容中，但編譯器不會強制執行條件約束。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-131">Generic declarations that include the `notnull` constraint can be used in a nullable oblivious context, but compiler does not enforce the constraint.</span></span>

[!code-csharp[using the nonnull constraint](snippets/GenericWhereConstraints.cs#NotNull)]

<span data-ttu-id="ae3b1-132">`where` 子句也可能包含 `unmanaged` 條件約束。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-132">The `where` clause may also include an `unmanaged` constraint.</span></span> <span data-ttu-id="ae3b1-133">`unmanaged` 條件約束會將型別參數限制為稱為[「非受控型別」](../builtin-types/unmanaged-types.md)的型別。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-133">The `unmanaged` constraint limits the type parameter to types known as [unmanaged types](../builtin-types/unmanaged-types.md).</span></span> <span data-ttu-id="ae3b1-134">`unmanaged` 條件約束可讓您更輕鬆地使用 C# 撰寫低階 Interop 程式碼。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-134">The `unmanaged` constraint makes it easier to write low-level interop code in C#.</span></span> <span data-ttu-id="ae3b1-135">此條件約束會啟用所有非受控型別的可重複使用常式。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-135">This constraint enables reusable routines across all unmanaged types.</span></span> <span data-ttu-id="ae3b1-136">`unmanaged` 條件約束不能與 `class` 或 `struct` 條件約束合併使用。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-136">The `unmanaged` constraint can't be combined with the `class` or `struct` constraint.</span></span> <span data-ttu-id="ae3b1-137">`unmanaged` 條件約束會強制型別必須是 `struct`：</span><span class="sxs-lookup"><span data-stu-id="ae3b1-137">The `unmanaged` constraint enforces that the type must be a `struct`:</span></span>

[!code-csharp[using the unmanaged constraint](snippets/GenericWhereConstraints.cs#4)]

<span data-ttu-id="ae3b1-138">`where` 子句也可能包含建構函式條件約束 `new()`。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-138">The `where` clause may also include a constructor constraint, `new()`.</span></span> <span data-ttu-id="ae3b1-139">該條件約束可讓您使用 `new` 運算子建立型別參數執行個體。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-139">That constraint makes it possible to create an instance of a type parameter using the `new` operator.</span></span> <span data-ttu-id="ae3b1-140">[新的 ( # A1 條件約束](new-constraint.md)可讓編譯器知道任何提供的型別引數都必須具有可存取的無參數函式。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-140">The [new() Constraint](new-constraint.md) lets the compiler know that any type argument supplied must have an accessible parameterless constructor.</span></span> <span data-ttu-id="ae3b1-141">例如：</span><span class="sxs-lookup"><span data-stu-id="ae3b1-141">For example:</span></span>

[!code-csharp[using the new constraint](snippets/GenericWhereConstraints.cs#5)]

<span data-ttu-id="ae3b1-142">`new()` 條件約束會出現在 `where` 子句中的最後。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-142">The `new()` constraint appears last in the `where` clause.</span></span> <span data-ttu-id="ae3b1-143">`new()` 條件約束不能與 `struct` 或 `unmanaged` 條件約束合併使用。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-143">The `new()` constraint can't be combined with the `struct` or `unmanaged` constraints.</span></span> <span data-ttu-id="ae3b1-144">所有滿足這些條件約束的型別都必須具有可存取的無參數建構函式，讓 `new()` 條件約束成為備援。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-144">All types satisfying those constraints must have an accessible parameterless constructor, making the `new()` constraint redundant.</span></span>

<span data-ttu-id="ae3b1-145">若有多個類型參數，請對每個類型參數使用一個 `where` 子句，例如：</span><span class="sxs-lookup"><span data-stu-id="ae3b1-145">With multiple type parameters, use one `where` clause for each type parameter, for example:</span></span>

[!code-csharp[using multiple where constraints](snippets/GenericWhereConstraints.cs#6)]

<span data-ttu-id="ae3b1-146">您也可以將條件約束附加至泛型方法的型別參數，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="ae3b1-146">You can also attach constraints to type parameters of generic methods, as shown in the following example:</span></span>

[!code-csharp[where constraints with generic methods](snippets/GenericWhereConstraints.cs#7)]

<span data-ttu-id="ae3b1-147">請注意，描述委派類型參數條件約束的語法與方法的語法相同︰</span><span class="sxs-lookup"><span data-stu-id="ae3b1-147">Notice that the syntax to describe type parameter constraints on delegates is the same as that of methods:</span></span>

[!code-csharp[where constraints with generic methods](snippets/GenericWhereConstraints.cs#8)]

<span data-ttu-id="ae3b1-148">如需泛型委派的資訊，請參閱[泛型委派](../../programming-guide/generics/generic-delegates.md)。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-148">For information on generic delegates, see [Generic Delegates](../../programming-guide/generics/generic-delegates.md).</span></span>

<span data-ttu-id="ae3b1-149">如需條件約束語法和用法的詳細資料，請參閱[類型參數的條件約束](../../programming-guide/generics/constraints-on-type-parameters.md)。</span><span class="sxs-lookup"><span data-stu-id="ae3b1-149">For details on the syntax and use of constraints, see [Constraints on Type Parameters](../../programming-guide/generics/constraints-on-type-parameters.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="ae3b1-150">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="ae3b1-150">C# language specification</span></span>

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="ae3b1-151">請參閱</span><span class="sxs-lookup"><span data-stu-id="ae3b1-151">See also</span></span>

- [<span data-ttu-id="ae3b1-152">C # 參考</span><span class="sxs-lookup"><span data-stu-id="ae3b1-152">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="ae3b1-153">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="ae3b1-153">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="ae3b1-154">泛型簡介</span><span class="sxs-lookup"><span data-stu-id="ae3b1-154">Introduction to Generics</span></span>](../../programming-guide/generics/index.md)
- [<span data-ttu-id="ae3b1-155">new 條件約束</span><span class="sxs-lookup"><span data-stu-id="ae3b1-155">new Constraint</span></span>](./new-constraint.md)
- [<span data-ttu-id="ae3b1-156">型別參數的條件約束</span><span class="sxs-lookup"><span data-stu-id="ae3b1-156">Constraints on Type Parameters</span></span>](../../programming-guide/generics/constraints-on-type-parameters.md)
