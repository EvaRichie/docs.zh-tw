---
title: where (泛型類型條件約束) - C# 參考
ms.date: 04/15/2020
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.openlocfilehash: 406c710cd884363c32b98336717732a09b3d1fc1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401871"
---
# <a name="where-generic-type-constraint-c-reference"></a><span data-ttu-id="966e5-102">where (泛型類型條件約束) (C# 參考)</span><span class="sxs-lookup"><span data-stu-id="966e5-102">where (generic type constraint) (C# Reference)</span></span>

<span data-ttu-id="966e5-103">泛型定義中的 `where` 子句指定型別上的條件約束，以用來作為泛型型別、方法、委派或本機函式中型別參數的引數。</span><span class="sxs-lookup"><span data-stu-id="966e5-103">The `where` clause in a generic definition specifies constraints on the types that are used as arguments for type parameters in a generic type, method, delegate, or local function.</span></span> <span data-ttu-id="966e5-104">條件約束可以指定介面、基類，或要求泛型型別為參考、值或非受控型別。</span><span class="sxs-lookup"><span data-stu-id="966e5-104">Constraints can specify interfaces, base classes, or require a generic type to be a reference, value, or unmanaged type.</span></span> <span data-ttu-id="966e5-105">它們會宣告類型引數必須具有的功能。</span><span class="sxs-lookup"><span data-stu-id="966e5-105">They declare capabilities that the type argument must have.</span></span>

<span data-ttu-id="966e5-106">例如，您可以宣告泛型類別 `MyGenericClass`，讓型別參數 `T` 實作 <xref:System.IComparable%601> 介面：</span><span class="sxs-lookup"><span data-stu-id="966e5-106">For example, you can declare a generic class, `MyGenericClass`, such that the type parameter `T` implements the <xref:System.IComparable%601> interface:</span></span>

[!code-csharp[using an interface constraint](snippets/GenericWhereConstraints.cs#1)]

> [!NOTE]
> <span data-ttu-id="966e5-107">如需查詢運算式中 where 子句的詳細資訊，請參閱 [where 子句](where-clause.md)。</span><span class="sxs-lookup"><span data-stu-id="966e5-107">For more information on the where clause in a query expression, see [where clause](where-clause.md).</span></span>

<span data-ttu-id="966e5-108">`where` 子句也可以包含基底類別條件約束。</span><span class="sxs-lookup"><span data-stu-id="966e5-108">The `where` clause can also include a base class constraint.</span></span> <span data-ttu-id="966e5-109">基類條件約束指出要當做該泛型型別之型別引數使用的型別，其具有指定的類別做為基類，或為該基類。</span><span class="sxs-lookup"><span data-stu-id="966e5-109">The base class constraint states that a type to be used as a type argument for that generic type has the specified class as a base class, or is that base class.</span></span> <span data-ttu-id="966e5-110">如果使用基底類別條件約束，則它必須出現在該型別參數的任何其他條件約束之前。</span><span class="sxs-lookup"><span data-stu-id="966e5-110">If the base class constraint is used, it must appear before any other constraints on that type parameter.</span></span> <span data-ttu-id="966e5-111">某些型別不允許作為基底類別條件約束：<xref:System.Object>、<xref:System.Array> 和 <xref:System.ValueType>。</span><span class="sxs-lookup"><span data-stu-id="966e5-111">Some types are disallowed as a base class constraint: <xref:System.Object>, <xref:System.Array>, and <xref:System.ValueType>.</span></span> <span data-ttu-id="966e5-112">在 c # 7.3 之前， <xref:System.Enum> 、 <xref:System.Delegate> 和 <xref:System.MulticastDelegate> 也不允許做為基類條件約束。</span><span class="sxs-lookup"><span data-stu-id="966e5-112">Before C# 7.3, <xref:System.Enum>, <xref:System.Delegate>, and <xref:System.MulticastDelegate> were also disallowed as base class constraints.</span></span> <span data-ttu-id="966e5-113">下列範例會顯示現在可以指定為基底類別的型別：</span><span class="sxs-lookup"><span data-stu-id="966e5-113">The following example shows the types that can now be specified as a base class:</span></span>

[!code-csharp[using an interface constraint](snippets/GenericWhereConstraints.cs#2)]

<span data-ttu-id="966e5-114">在 c # 8.0 和更新版本中可為 null 的內容中，會強制執行基類類型的 null 屬性。</span><span class="sxs-lookup"><span data-stu-id="966e5-114">In a nullable context in C# 8.0 and later, the nullability of the base class type is enforced.</span></span> <span data-ttu-id="966e5-115">如果基類不可為 null （例如 `Base` ），則類型引數必須是不可為 null。</span><span class="sxs-lookup"><span data-stu-id="966e5-115">If the base class is non-nullable (for example `Base`), the type argument must be non-nullable.</span></span> <span data-ttu-id="966e5-116">如果基類可為 null （例如 `Base?` ），則類型引數可能是可為 null 或不可為 null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="966e5-116">If the base class is nullable (for example `Base?`), the type argument may be either a nullable or non-nullable reference type.</span></span> <span data-ttu-id="966e5-117">當基類不可為 null 時，如果類型引數是可為 null 的參考型別，則編譯器會發出警告。</span><span class="sxs-lookup"><span data-stu-id="966e5-117">The compiler issues a warning if the type argument is a nullable reference type when the base class is non-nullable.</span></span>

<span data-ttu-id="966e5-118">`where` 子句可以指定型別是 `class` 或 `struct`。</span><span class="sxs-lookup"><span data-stu-id="966e5-118">The `where` clause can specify that the type is a `class` or a `struct`.</span></span> <span data-ttu-id="966e5-119">`struct` 條件約束不需要指定 `System.ValueType` 的基底類別條件約束。</span><span class="sxs-lookup"><span data-stu-id="966e5-119">The `struct` constraint removes the need to specify a base class constraint of `System.ValueType`.</span></span> <span data-ttu-id="966e5-120">`System.ValueType` 型別不能用作基底類別條件約束。</span><span class="sxs-lookup"><span data-stu-id="966e5-120">The `System.ValueType` type may not be used as a base class constraint.</span></span> <span data-ttu-id="966e5-121">下列範例顯示 `class` 和 `struct` 條件約束：</span><span class="sxs-lookup"><span data-stu-id="966e5-121">The following example shows both the `class` and `struct` constraints:</span></span>

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#3)]

<span data-ttu-id="966e5-122">在 c # 8.0 和更新版本中的可為 null 內容中， `class` 條件約束要求類型必須是不可為 null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="966e5-122">In a nullable context in C# 8.0 and later, the `class` constraint requires a type to be a non-nullable reference type.</span></span> <span data-ttu-id="966e5-123">若要允許可為 null 的參考型別，請使用 `class?` 條件約束，這可同時允許可為 null 和不可為 null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="966e5-123">To allow nullable reference types, use the `class?` constraint, which allows both nullable and non-nullable reference types.</span></span>

<span data-ttu-id="966e5-124">`where`子句可以包含 `notnull` 條件約束。</span><span class="sxs-lookup"><span data-stu-id="966e5-124">The `where` clause may include the `notnull` constraint.</span></span> <span data-ttu-id="966e5-125">`notnull`條件約束會將類型參數限制為不可為 null 的類型。</span><span class="sxs-lookup"><span data-stu-id="966e5-125">The `notnull` constraint limits the type parameter to non-nullable types.</span></span> <span data-ttu-id="966e5-126">該類型可能是實[數值型別](../builtin-types/value-types.md)或不可為 null 的參考型別。</span><span class="sxs-lookup"><span data-stu-id="966e5-126">That type may be a [value type](../builtin-types/value-types.md) or a non-nullable reference type.</span></span> <span data-ttu-id="966e5-127">`notnull`從 c # 8.0 開始，針對[ `nullable enable` 內容](../../nullable-references.md#nullable-contexts)中編譯的程式碼提供條件約束。</span><span class="sxs-lookup"><span data-stu-id="966e5-127">The `notnull` constraint is available starting in C# 8.0 for code compiled in a [`nullable enable` context](../../nullable-references.md#nullable-contexts).</span></span> <span data-ttu-id="966e5-128">與其他條件約束不同的是，如果類型引數違反 `notnull` 條件約束，則編譯器會產生警告，而不是錯誤。</span><span class="sxs-lookup"><span data-stu-id="966e5-128">Unlike other constraints, if a type argument violates the `notnull` constraint, the compiler generates a warning instead of an error.</span></span> <span data-ttu-id="966e5-129">只有在內容中才會產生警告 `nullable enable` 。</span><span class="sxs-lookup"><span data-stu-id="966e5-129">Warnings are only generated in a `nullable enable` context.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="966e5-130">包含條件約束的泛型宣告 `notnull` 可以在可為 null 的遺忘式內容中使用，但編譯器不會強制執行條件約束。</span><span class="sxs-lookup"><span data-stu-id="966e5-130">Generic declarations that include the `notnull` constraint can be used in a nullable oblivious context, but compiler does not enforce the constraint.</span></span>

[!code-csharp[using the nonnull constraint](snippets/GenericWhereConstraints.cs#NotNull)]

<span data-ttu-id="966e5-131">`where` 子句也可能包含 `unmanaged` 條件約束。</span><span class="sxs-lookup"><span data-stu-id="966e5-131">The `where` clause may also include an `unmanaged` constraint.</span></span> <span data-ttu-id="966e5-132">`unmanaged` 條件約束會將型別參數限制為稱為[「非受控型別」](../builtin-types/unmanaged-types.md)的型別。</span><span class="sxs-lookup"><span data-stu-id="966e5-132">The `unmanaged` constraint limits the type parameter to types known as [unmanaged types](../builtin-types/unmanaged-types.md).</span></span> <span data-ttu-id="966e5-133">`unmanaged` 條件約束可讓您更輕鬆地使用 C# 撰寫低階 Interop 程式碼。</span><span class="sxs-lookup"><span data-stu-id="966e5-133">The `unmanaged` constraint makes it easier to write low-level interop code in C#.</span></span> <span data-ttu-id="966e5-134">此條件約束會啟用所有非受控型別的可重複使用常式。</span><span class="sxs-lookup"><span data-stu-id="966e5-134">This constraint enables reusable routines across all unmanaged types.</span></span> <span data-ttu-id="966e5-135">`unmanaged` 條件約束不能與 `class` 或 `struct` 條件約束合併使用。</span><span class="sxs-lookup"><span data-stu-id="966e5-135">The `unmanaged` constraint can't be combined with the `class` or `struct` constraint.</span></span> <span data-ttu-id="966e5-136">`unmanaged` 條件約束會強制型別必須是 `struct`：</span><span class="sxs-lookup"><span data-stu-id="966e5-136">The `unmanaged` constraint enforces that the type must be a `struct`:</span></span>

[!code-csharp[using the unmanaged constraint](snippets/GenericWhereConstraints.cs#4)]

<span data-ttu-id="966e5-137">`where` 子句也可能包含建構函式條件約束 `new()`。</span><span class="sxs-lookup"><span data-stu-id="966e5-137">The `where` clause may also include a constructor constraint, `new()`.</span></span> <span data-ttu-id="966e5-138">該條件約束可讓您使用 `new` 運算子建立型別參數執行個體。</span><span class="sxs-lookup"><span data-stu-id="966e5-138">That constraint makes it possible to create an instance of a type parameter using the `new` operator.</span></span> <span data-ttu-id="966e5-139">[New （）條件約束](new-constraint.md)可讓編譯器知道提供的任何型別引數都必須具有可存取的無參數函數。</span><span class="sxs-lookup"><span data-stu-id="966e5-139">The [new() Constraint](new-constraint.md) lets the compiler know that any type argument supplied must have an accessible parameterless constructor.</span></span> <span data-ttu-id="966e5-140">例如：</span><span class="sxs-lookup"><span data-stu-id="966e5-140">For example:</span></span>

[!code-csharp[using the new constraint](snippets/GenericWhereConstraints.cs#5)]

<span data-ttu-id="966e5-141">`new()` 條件約束會出現在 `where` 子句中的最後。</span><span class="sxs-lookup"><span data-stu-id="966e5-141">The `new()` constraint appears last in the `where` clause.</span></span> <span data-ttu-id="966e5-142">`new()` 條件約束不能與 `struct` 或 `unmanaged` 條件約束合併使用。</span><span class="sxs-lookup"><span data-stu-id="966e5-142">The `new()` constraint can't be combined with the `struct` or `unmanaged` constraints.</span></span> <span data-ttu-id="966e5-143">所有滿足這些條件約束的型別都必須具有可存取的無參數建構函式，讓 `new()` 條件約束成為備援。</span><span class="sxs-lookup"><span data-stu-id="966e5-143">All types satisfying those constraints must have an accessible parameterless constructor, making the `new()` constraint redundant.</span></span>

<span data-ttu-id="966e5-144">若有多個類型參數，請對每個類型參數使用一個 `where` 子句，例如：</span><span class="sxs-lookup"><span data-stu-id="966e5-144">With multiple type parameters, use one `where` clause for each type parameter, for example:</span></span>

[!code-csharp[using multiple where constraints](snippets/GenericWhereConstraints.cs#6)]

<span data-ttu-id="966e5-145">您也可以將條件約束附加至泛型方法的型別參數，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="966e5-145">You can also attach constraints to type parameters of generic methods, as shown in the following example:</span></span>

[!code-csharp[where constraints with generic methods](snippets/GenericWhereConstraints.cs#7)]

<span data-ttu-id="966e5-146">請注意，描述委派類型參數條件約束的語法與方法的語法相同︰</span><span class="sxs-lookup"><span data-stu-id="966e5-146">Notice that the syntax to describe type parameter constraints on delegates is the same as that of methods:</span></span>

[!code-csharp[where constraints with generic methods](snippets/GenericWhereConstraints.cs#8)]

<span data-ttu-id="966e5-147">如需泛型委派的資訊，請參閱[泛型委派](../../programming-guide/generics/generic-delegates.md)。</span><span class="sxs-lookup"><span data-stu-id="966e5-147">For information on generic delegates, see [Generic Delegates](../../programming-guide/generics/generic-delegates.md).</span></span>

<span data-ttu-id="966e5-148">如需條件約束語法和用法的詳細資料，請參閱[類型參數的條件約束](../../programming-guide/generics/constraints-on-type-parameters.md)。</span><span class="sxs-lookup"><span data-stu-id="966e5-148">For details on the syntax and use of constraints, see [Constraints on Type Parameters](../../programming-guide/generics/constraints-on-type-parameters.md).</span></span>

## <a name="c-language-specification"></a><span data-ttu-id="966e5-149">C# 語言規格</span><span class="sxs-lookup"><span data-stu-id="966e5-149">C# language specification</span></span>

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a><span data-ttu-id="966e5-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="966e5-150">See also</span></span>

- [<span data-ttu-id="966e5-151">C # 參考</span><span class="sxs-lookup"><span data-stu-id="966e5-151">C# Reference</span></span>](../index.md)
- [<span data-ttu-id="966e5-152">C # 程式設計指南</span><span class="sxs-lookup"><span data-stu-id="966e5-152">C# Programming Guide</span></span>](../../programming-guide/index.md)
- [<span data-ttu-id="966e5-153">泛型簡介</span><span class="sxs-lookup"><span data-stu-id="966e5-153">Introduction to Generics</span></span>](../../programming-guide/generics/index.md)
- [<span data-ttu-id="966e5-154">new 條件約束</span><span class="sxs-lookup"><span data-stu-id="966e5-154">new Constraint</span></span>](./new-constraint.md)
- [<span data-ttu-id="966e5-155">型別參數的條件約束</span><span class="sxs-lookup"><span data-stu-id="966e5-155">Constraints on Type Parameters</span></span>](../../programming-guide/generics/constraints-on-type-parameters.md)
