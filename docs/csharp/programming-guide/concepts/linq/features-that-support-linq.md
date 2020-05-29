---
title: 支援 LINQ 的 C# 功能
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], features supporting LINQ
ms.assetid: 524b0078-ebfd-45a7-b390-f2ceb9d84797
ms.openlocfilehash: 32ba8f5e60b3ed2efd813a8ae32e5f4009eb790d
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202413"
---
# <a name="c-features-that-support-linq"></a><span data-ttu-id="323d6-102">支援 LINQ 的 C# 功能</span><span class="sxs-lookup"><span data-stu-id="323d6-102">C# Features That Support LINQ</span></span>

<span data-ttu-id="323d6-103">下節將介紹 C# 3.0 中引進的新語言建構。</span><span class="sxs-lookup"><span data-stu-id="323d6-103">The following section introduces new language constructs introduced in C# 3.0.</span></span> <span data-ttu-id="323d6-104">雖然這些新功能全都適用于 LINQ 查詢的程度，但它們並不限於 LINQ，而且可以在任何您覺得有用的內容中使用。</span><span class="sxs-lookup"><span data-stu-id="323d6-104">Although these new features are all used to a degree with LINQ queries, they are not limited to LINQ and can be used in any context where you find them useful.</span></span>

## <a name="query-expressions"></a><span data-ttu-id="323d6-105">查詢運算式</span><span class="sxs-lookup"><span data-stu-id="323d6-105">Query Expressions</span></span>

<span data-ttu-id="323d6-106">查詢運算式使用類似 SQL 或 XQuery 的宣告式語法來查詢 IEnumerable 集合。</span><span class="sxs-lookup"><span data-stu-id="323d6-106">Query expressions use a declarative syntax similar to SQL or XQuery to query over IEnumerable collections.</span></span> <span data-ttu-id="323d6-107">在編譯時期，查詢語法會轉換成 LINQ 提供者的標準查詢運算子擴充方法的實作為方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="323d6-107">At compile time query syntax is converted to method calls to a LINQ provider's implementation of the standard query operator extension methods.</span></span> <span data-ttu-id="323d6-108">應用程式使用 `using` 指示詞來指定適當的命名空間，藉此控制範圍內的標準查詢運算子。</span><span class="sxs-lookup"><span data-stu-id="323d6-108">Applications control the standard query operators that are in scope by specifying the appropriate namespace with a `using` directive.</span></span> <span data-ttu-id="323d6-109">下列查詢運算式會擷取字串的陣列，然後根據字串的第一個字元分組字串，再排序這些群組。</span><span class="sxs-lookup"><span data-stu-id="323d6-109">The following query expression takes an array of strings, groups them according to the first character in the string, and orders the groups.</span></span>

```csharp
var query = from str in stringArray
            group str by str[0] into stringGroup
            orderby stringGroup.Key
            select stringGroup;
```

<span data-ttu-id="323d6-110">如需詳細資訊，請參閱 [LINQ 查詢運算式](../../../linq/index.md)。</span><span class="sxs-lookup"><span data-stu-id="323d6-110">For more information, see [LINQ Query Expressions](../../../linq/index.md).</span></span>

## <a name="implicitly-typed-variables-var"></a><span data-ttu-id="323d6-111">隱含型別變數 (var)</span><span class="sxs-lookup"><span data-stu-id="323d6-111">Implicitly Typed Variables (var)</span></span>

<span data-ttu-id="323d6-112">除了在宣告和初始化變數時明確指定類型，您還可以使用 [var](../../../language-reference/keywords/var.md) 修飾詞，指示編譯器推斷並指派類型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="323d6-112">Instead of explicitly specifying a type when you declare and initialize a variable, you can use the [var](../../../language-reference/keywords/var.md) modifier to instruct the compiler to infer and assign the type, as shown here:</span></span>

```csharp
var number = 5;
var name = "Virginia";
var query = from str in stringArray
            where str[0] == 'm'
            select str;
```

<span data-ttu-id="323d6-113">宣告為的變數，與 `var` 您明確指定類型的變數一樣強型別。</span><span class="sxs-lookup"><span data-stu-id="323d6-113">Variables declared as `var` are just as strongly typed as variables whose type you specify explicitly.</span></span> <span data-ttu-id="323d6-114">`var` 可用來建立匿名型別，但僅可用於區域變數。</span><span class="sxs-lookup"><span data-stu-id="323d6-114">The use of `var` makes it possible to create anonymous types, but it can be used only for local variables.</span></span> <span data-ttu-id="323d6-115">陣列也可以使用隱含型別進行宣告。</span><span class="sxs-lookup"><span data-stu-id="323d6-115">Arrays can also be declared with implicit typing.</span></span>

<span data-ttu-id="323d6-116">如需詳細資訊，請參閱[隱含型別區域變數](../../classes-and-structs/implicitly-typed-local-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="323d6-116">For more information, see [Implicitly Typed Local Variables](../../classes-and-structs/implicitly-typed-local-variables.md).</span></span>

## <a name="object-and-collection-initializers"></a><span data-ttu-id="323d6-117">物件和集合初始設定式</span><span class="sxs-lookup"><span data-stu-id="323d6-117">Object and Collection Initializers</span></span>

<span data-ttu-id="323d6-118">物件和集合初始設定式可以初始化物件，而不需要明確呼叫物件的建構函式。</span><span class="sxs-lookup"><span data-stu-id="323d6-118">Object and collection initializers make it possible to initialize objects without explicitly calling a constructor for the object.</span></span> <span data-ttu-id="323d6-119">初始設定式通常會用於將來源資料投影為新資料類型的查詢運算式中。</span><span class="sxs-lookup"><span data-stu-id="323d6-119">Initializers are typically used in query expressions when they project the source data into a new data type.</span></span> <span data-ttu-id="323d6-120">假設有個名為 `Customer` 的類別具有公用的 `Name` 和 `Phone` 屬性，則可如下列程式碼所示使用物件初始設定式：</span><span class="sxs-lookup"><span data-stu-id="323d6-120">Assuming a class named `Customer` with public `Name` and `Phone` properties, the object initializer can be used as in the following code:</span></span>

```csharp
var cust = new Customer { Name = "Mike", Phone = "555-1212" };
```

<span data-ttu-id="323d6-121">延續我們的 `Customer` 類別，假設有一個稱為 `IncomingOrders` 的資料來源，而其每個訂單都有大型的 `OrderSize`，我們想要根據該訂單建立新的 `Customer`。</span><span class="sxs-lookup"><span data-stu-id="323d6-121">Continuing with our `Customer` class, assume that there is a data source called `IncomingOrders`, and that for each order with a large `OrderSize`, we would like to create a new `Customer` based off of that order.</span></span> <span data-ttu-id="323d6-122">您可以針對此資料來源執行 LINQ 查詢，並使用物件初始化來填滿集合：</span><span class="sxs-lookup"><span data-stu-id="323d6-122">A LINQ query can be executed on this data source and use object initialization to fill a collection:</span></span>

```csharp
var newLargeOrderCustomers = from o in IncomingOrders
                            where o.OrderSize > 5
                            select new Customer { Name = o.Name, Phone = o.Phone };
```

<span data-ttu-id="323d6-123">資料來源底下可能有比 `Customer` 類別更多的屬性 (例如 `OrderSize`)，但使用物件初始化時，從查詢傳回的資料會塑造為我們想要的資料型別；我們選擇與我們的類別相關的資料。</span><span class="sxs-lookup"><span data-stu-id="323d6-123">The data source may have more properties lying under the hood than the `Customer` class such as `OrderSize`, but with object initialization, the data returned from the query is molded into the desired data type; we choose the data that is relevant to our class.</span></span> <span data-ttu-id="323d6-124">因此，我們現在有使用新的 `Customer` 填滿的 `IEnumerable`，這正是我們所需要的。</span><span class="sxs-lookup"><span data-stu-id="323d6-124">As a result, we now have an `IEnumerable` filled with the new `Customer`s we wanted.</span></span> <span data-ttu-id="323d6-125">上述內容也可以使用 LINQ 的方法語法撰寫：</span><span class="sxs-lookup"><span data-stu-id="323d6-125">The above can also be written in LINQ's method syntax:</span></span>

```csharp
var newLargeOrderCustomers = IncomingOrders.Where(x => x.OrderSize > 5).Select(y => new Customer { Name = y.Name, Phone = y.Phone });
```

<span data-ttu-id="323d6-126">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="323d6-126">For more information, see:</span></span>

- [<span data-ttu-id="323d6-127">物件和集合初始設定式</span><span class="sxs-lookup"><span data-stu-id="323d6-127">Object and Collection Initializers</span></span>](../../classes-and-structs/object-and-collection-initializers.md)

- [<span data-ttu-id="323d6-128">標準查詢運算子的查詢運算式語法</span><span class="sxs-lookup"><span data-stu-id="323d6-128">Query Expression Syntax for Standard Query Operators</span></span>](./query-expression-syntax-for-standard-query-operators.md)

## <a name="anonymous-types"></a><span data-ttu-id="323d6-129">匿名類型</span><span class="sxs-lookup"><span data-stu-id="323d6-129">Anonymous Types</span></span>

<span data-ttu-id="323d6-130">匿名型別是由編譯器所建構，只有編譯器才知道類型名稱。</span><span class="sxs-lookup"><span data-stu-id="323d6-130">An anonymous type is constructed by the compiler and the type name is only available to the compiler.</span></span> <span data-ttu-id="323d6-131">匿名型別提供了一個便利的方法，暫時將查詢結果中的一組屬性分組，而不需要另外定義具名類型。</span><span class="sxs-lookup"><span data-stu-id="323d6-131">Anonymous types provide a convenient way to group a set of properties temporarily in a query result without having to define a separate named type.</span></span> <span data-ttu-id="323d6-132">匿名型別是以新的運算式和物件初始設定式進行初始化，如下所示：</span><span class="sxs-lookup"><span data-stu-id="323d6-132">Anonymous types are initialized with a new expression and an object initializer, as shown here:</span></span>

```csharp
select new {name = cust.Name, phone = cust.Phone};
```

<span data-ttu-id="323d6-133">如需詳細資訊，請參閱[匿名](../../classes-and-structs/anonymous-types.md)型別。</span><span class="sxs-lookup"><span data-stu-id="323d6-133">For more information, see [Anonymous Types](../../classes-and-structs/anonymous-types.md).</span></span>

## <a name="extension-methods"></a><span data-ttu-id="323d6-134">擴充方法</span><span class="sxs-lookup"><span data-stu-id="323d6-134">Extension Methods</span></span>

<span data-ttu-id="323d6-135">擴充方法是一種可以與類型相關聯的靜態方法，因此可以像呼叫類型上的執行個體方法一樣呼叫它。</span><span class="sxs-lookup"><span data-stu-id="323d6-135">An extension method is a static method that can be associated with a type, so that it can be called as if it were an instance method on the type.</span></span> <span data-ttu-id="323d6-136">這項功能實際上可讓您「新增」方法至現有的類型，而不需要實際修改這些類型。</span><span class="sxs-lookup"><span data-stu-id="323d6-136">This feature enables you to, in effect, "add" new methods to existing types without actually modifying them.</span></span> <span data-ttu-id="323d6-137">標準查詢運算子是一組擴充方法，可為任何可執行檔型別提供 LINQ 查詢功能 <xref:System.Collections.Generic.IEnumerable%601> 。</span><span class="sxs-lookup"><span data-stu-id="323d6-137">The standard query operators are a set of extension methods that provide LINQ query functionality for any type that implements <xref:System.Collections.Generic.IEnumerable%601>.</span></span>

<span data-ttu-id="323d6-138">如需詳細資訊，請參閱[擴充方法](../../classes-and-structs/extension-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="323d6-138">For more information, see [Extension Methods](../../classes-and-structs/extension-methods.md).</span></span>

## <a name="lambda-expressions"></a><span data-ttu-id="323d6-139">Lambda 運算式</span><span class="sxs-lookup"><span data-stu-id="323d6-139">Lambda Expressions</span></span>

<span data-ttu-id="323d6-140">Lambda 運算式是一種內嵌函式，其使用 => 運算子分隔輸入參數與函式主體，而且可以在編譯期間轉換成委派或運算式樹狀架構。</span><span class="sxs-lookup"><span data-stu-id="323d6-140">A lambda expression is an inline function that uses the => operator to separate input parameters from the function body and can be converted at compile time to a delegate or an expression tree.</span></span> <span data-ttu-id="323d6-141">在 LINQ 程式設計中，當您對標準查詢運算子進行直接方法呼叫時，將會遇到 lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="323d6-141">In LINQ programming, you will encounter lambda expressions when you make direct method calls to the standard query operators.</span></span>

<span data-ttu-id="323d6-142">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="323d6-142">For more information, see:</span></span>

- [<span data-ttu-id="323d6-143">匿名函式</span><span class="sxs-lookup"><span data-stu-id="323d6-143">Anonymous Functions</span></span>](../../statements-expressions-operators/anonymous-functions.md)

- [<span data-ttu-id="323d6-144">Lambda 運算式</span><span class="sxs-lookup"><span data-stu-id="323d6-144">Lambda Expressions</span></span>](../../statements-expressions-operators/lambda-expressions.md)

- [<span data-ttu-id="323d6-145">運算式樹狀架構 (C#)</span><span class="sxs-lookup"><span data-stu-id="323d6-145">Expression Trees (C#)</span></span>](../expression-trees/index.md)

## <a name="see-also"></a><span data-ttu-id="323d6-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="323d6-146">See also</span></span>

- [<span data-ttu-id="323d6-147">Language-Integrated Query (LINQ) (C#)</span><span class="sxs-lookup"><span data-stu-id="323d6-147">Language-Integrated Query (LINQ) (C#)</span></span>](./index.md)
