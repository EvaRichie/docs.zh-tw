---
title: 匿名記錄
description: 瞭解如何使用結構和匿名記錄，這是可協助運算元據的語言功能。
ms.date: 06/12/2019
ms.openlocfilehash: 13950048f02ab74362f8174725f5f8615d9d7654
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739811"
---
# <a name="anonymous-records"></a><span data-ttu-id="49169-103">匿名記錄</span><span class="sxs-lookup"><span data-stu-id="49169-103">Anonymous Records</span></span>

<span data-ttu-id="49169-104">匿名記錄是命名值的簡單匯總，不需要在使用之前宣告。</span><span class="sxs-lookup"><span data-stu-id="49169-104">Anonymous records are simple aggregates of named values that don't need to be declared before use.</span></span> <span data-ttu-id="49169-105">您可以將它們宣告為結構或參考型別。</span><span class="sxs-lookup"><span data-stu-id="49169-105">You can declare them as either structs or reference types.</span></span> <span data-ttu-id="49169-106">它們預設是參考型別。</span><span class="sxs-lookup"><span data-stu-id="49169-106">They're reference types by default.</span></span>

## <a name="syntax"></a><span data-ttu-id="49169-107">語法</span><span class="sxs-lookup"><span data-stu-id="49169-107">Syntax</span></span>

<span data-ttu-id="49169-108">下列範例示範匿名記錄語法。</span><span class="sxs-lookup"><span data-stu-id="49169-108">The following examples demonstrate the anonymous record syntax.</span></span> <span data-ttu-id="49169-109">分隔為 `[item]` 的專案是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="49169-109">Items delimited as `[item]` are optional.</span></span>

```fsharp
// Construct an anonymous record
let value-name = [struct] {| Label1: Type1; Label2: Type2; ...|}

// Use an anonymous record as a type parameter
let value-name = Type-Name<[struct] {| Label1: Type1; Label2: Type2; ...|}>

// Define a parameter with an anonymous record as input
let function-name (arg-name: [struct] {| Label1: Type1; Label2: Type2; ...|}) ...
```

## <a name="basic-usage"></a><span data-ttu-id="49169-110">基本使用方式</span><span class="sxs-lookup"><span data-stu-id="49169-110">Basic usage</span></span>

<span data-ttu-id="49169-111">匿名記錄最好被視為不需要在具現化之前宣告的 F # 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="49169-111">Anonymous records are best thought of as F# record types that don't need to be declared before instantiation.</span></span>

<span data-ttu-id="49169-112">例如，在這裡，您可以如何與產生匿名記錄的函式互動：</span><span class="sxs-lookup"><span data-stu-id="49169-112">For example, here how you can interact with a function that produces an anonymous record:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let r = 2.0
let stats = getCircleStats r
printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
    r stats.Diameter stats.Area stats.Circumference
```

<span data-ttu-id="49169-113">下列範例 `printCircleStats` 會使用接受匿名記錄做為輸入的函式來展開上一個範例：</span><span class="sxs-lookup"><span data-stu-id="49169-113">The following example expands on the previous one with a `printCircleStats` function that takes an anonymous record as input:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    {| Diameter = d; Area = a; Circumference = c |}

let printCircleStats r (stats: {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

<span data-ttu-id="49169-114">`printCircleStats`使用任何匿名記錄類型呼叫，而該類型與輸入類型沒有相同的「圖形」，將無法編譯：</span><span class="sxs-lookup"><span data-stu-id="49169-114">Calling `printCircleStats` with any anonymous record type that doesn't have the same "shape" as the input type will fail to compile:</span></span>

```fsharp
printCircleStats r {| Diameter = 2.0; Area = 4.0; MyCircumference = 12.566371 |}
// Two anonymous record types have mismatched sets of field names
// '["Area"; "Circumference"; "Diameter"]' and '["Area"; "Diameter"; "MyCircumference"]'
```

## <a name="struct-anonymous-records"></a><span data-ttu-id="49169-115">結構匿名記錄</span><span class="sxs-lookup"><span data-stu-id="49169-115">Struct anonymous records</span></span>

<span data-ttu-id="49169-116">您也可以使用選擇性關鍵字將匿名記錄定義為結構 `struct` 。</span><span class="sxs-lookup"><span data-stu-id="49169-116">Anonymous records can also be defined as struct with the optional `struct` keyword.</span></span> <span data-ttu-id="49169-117">下列範例會藉由產生和取用結構匿名記錄來擴大前一個範例：</span><span class="sxs-lookup"><span data-stu-id="49169-117">The following example augments the previous one by producing and consuming a struct anonymous record:</span></span>

```fsharp
open System

let getCircleStats radius =
    let d = radius * 2.0
    let a = Math.PI * (radius ** 2.0)
    let c = 2.0 * Math.PI * radius

    // Note that the keyword comes before the '{| |}' brace pair
    struct {| Area = a; Circumference = c; Diameter = d |}

// the 'struct' keyword also comes before the '{| |}' brace pair when declaring the parameter type
let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

let r = 2.0
let stats = getCircleStats r
printCircleStats r stats
```

### <a name="structness-inference"></a><span data-ttu-id="49169-118">Structness 推斷</span><span class="sxs-lookup"><span data-stu-id="49169-118">Structness inference</span></span>

<span data-ttu-id="49169-119">結構匿名記錄也允許「structness 推斷」，您不需要在呼叫位置指定 `struct` 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="49169-119">Struct anonymous records also allow for "structness inference" where you do not need to specify the `struct` keyword at the call site.</span></span> <span data-ttu-id="49169-120">在此範例中，您會在 `struct` 呼叫時省略關鍵字 `printCircleStats` ：</span><span class="sxs-lookup"><span data-stu-id="49169-120">In this example, you elide the `struct` keyword when calling `printCircleStats`:</span></span>

```fsharp

let printCircleStats r (stats: struct {| Area: float; Circumference: float; Diameter: float |}) =
    printfn "Circle with radius: %f has diameter %f, area %f, and circumference %f"
        r stats.Diameter stats.Area stats.Circumference

printCircleStats r {| Area = 4.0; Circumference = 12.6; Diameter = 12.6 |}
```

<span data-ttu-id="49169-121">反向模式-指定 `struct` 輸入類型不是結構匿名記錄時，將無法編譯。</span><span class="sxs-lookup"><span data-stu-id="49169-121">The reverse pattern - specifying `struct` when the input type is not a struct anonymous record - will fail to compile.</span></span>

## <a name="embedding-anonymous-records-within-other-types"></a><span data-ttu-id="49169-122">在其他類型中內嵌匿名記錄</span><span class="sxs-lookup"><span data-stu-id="49169-122">Embedding anonymous records within other types</span></span>

<span data-ttu-id="49169-123">宣告案例為記錄的 [區分](discriminated-unions.md) 等位是很有用的。</span><span class="sxs-lookup"><span data-stu-id="49169-123">It's useful to declare [discriminated unions](discriminated-unions.md) whose cases are records.</span></span> <span data-ttu-id="49169-124">但是，如果記錄中的資料與不同聯集的類型相同，您就必須將所有類型定義為相互遞迴。</span><span class="sxs-lookup"><span data-stu-id="49169-124">But if the data in the records is the same type as the discriminated union, you must define all types as mutually recursive.</span></span> <span data-ttu-id="49169-125">使用匿名記錄可避免這種限制。</span><span class="sxs-lookup"><span data-stu-id="49169-125">Using anonymous records avoids this restriction.</span></span> <span data-ttu-id="49169-126">以下是模式比對的範例型別和函數：</span><span class="sxs-lookup"><span data-stu-id="49169-126">What follows is an example type and function that pattern matches over it:</span></span>

```fsharp
type FullName = { FirstName: string; LastName: string }

// Note that using a named record for Manager and Executive would require mutually recursive definitions.
type Employee =
    | Engineer of FullName
    | Manager of {| Name: FullName; Reports: Employee list |}
    | Executive of {| Name: FullName; Reports: Employee list; Assistant: Employee |}

let getFirstName e =
    match e with
    | Engineer fullName -> fullName.FirstName
    | Manager m -> m.Name.FirstName
    | Executive ex -> ex.Name.FirstName
```

## <a name="copy-and-update-expressions"></a><span data-ttu-id="49169-127">複製和更新運算式</span><span class="sxs-lookup"><span data-stu-id="49169-127">Copy and update expressions</span></span>

<span data-ttu-id="49169-128">匿名記錄支援具有 [複製和更新運算式](copy-and-update-record-expressions.md)的結構。</span><span class="sxs-lookup"><span data-stu-id="49169-128">Anonymous records support construction with [copy and update expressions](copy-and-update-record-expressions.md).</span></span> <span data-ttu-id="49169-129">例如，以下是您可以如何建立匿名記錄的新實例，以複製現有的資料：</span><span class="sxs-lookup"><span data-stu-id="49169-129">For example, here's how you can construct a new instance of an anonymous record that copies an existing one's data:</span></span>

```fsharp
let data = {| X = 1; Y = 2 |}
let data' = {| data with Y = 3 |}
```

<span data-ttu-id="49169-130">不過，不同于命名記錄，匿名記錄可讓您使用複製和更新運算式來建立完全不同的表單。</span><span class="sxs-lookup"><span data-stu-id="49169-130">However, unlike named records, anonymous records allow you to construct entirely different forms with copy and update expressions.</span></span> <span data-ttu-id="49169-131">下列範例會使用先前範例中的相同匿名記錄，並將它擴充至新的匿名記錄：</span><span class="sxs-lookup"><span data-stu-id="49169-131">The follow example takes the same anonymous record from the previous example and expands it into a new anonymous record:</span></span>

```fsharp
let data = {| X = 1; Y = 2 |}
let expandedData = {| data with Z = 3 |} // Gives {| X=1; Y=2; Z=3 |}
```

<span data-ttu-id="49169-132">您也可以從命名記錄的實例中，建立匿名記錄：</span><span class="sxs-lookup"><span data-stu-id="49169-132">It is also possible to construct anonymous records from instances of named records:</span></span>

```fsharp
type R = { X: int }
let data = { X = 1 }
let data' = {| data with Y = 2 |} // Gives {| X=1; Y=2 |}
```

<span data-ttu-id="49169-133">您也可以將資料複製到參考和結構匿名記錄：</span><span class="sxs-lookup"><span data-stu-id="49169-133">You can also copy data to and from reference and struct anonymous records:</span></span>

```fsharp
// Copy data from a reference record into a struct anonymous record
type R1 = { X: int }
let r1 = { X = 1 }

let data1 = struct {| r1 with Y = 1 |}

// Copy data from a struct record into a reference anonymous record
[<Struct>]
type R2 = { X: int }
let r2 = { X = 1 }

let data2 = {| r1 with Y = 1 |}

// Copy the reference anonymous record data into a struct anonymous record
let data3 = struct {| data2 with Z = r2.X |}
```

## <a name="properties-of-anonymous-records"></a><span data-ttu-id="49169-134">匿名記錄的屬性</span><span class="sxs-lookup"><span data-stu-id="49169-134">Properties of anonymous records</span></span>

<span data-ttu-id="49169-135">匿名記錄有許多特性，對於完全瞭解其使用方式而言是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="49169-135">Anonymous records have a number of characteristics that are essential to fully understanding how they can be used.</span></span>

### <a name="anonymous-records-are-nominal"></a><span data-ttu-id="49169-136">匿名記錄為名義</span><span class="sxs-lookup"><span data-stu-id="49169-136">Anonymous records are nominal</span></span>

<span data-ttu-id="49169-137">匿名記錄是 [名義類型](https://en.wikipedia.org/wiki/Nominal_type_system)。</span><span class="sxs-lookup"><span data-stu-id="49169-137">Anonymous records are [nominal types](https://en.wikipedia.org/wiki/Nominal_type_system).</span></span> <span data-ttu-id="49169-138">最好將它們視為命名 [記錄](records.md) 類型 (這也是不需要前置宣告的名義) 。</span><span class="sxs-lookup"><span data-stu-id="49169-138">They are best thought as named [record](records.md) types (which are also nominal) that do not require an up-front declaration.</span></span>

<span data-ttu-id="49169-139">請考慮下列兩個匿名記錄宣告的範例：</span><span class="sxs-lookup"><span data-stu-id="49169-139">Consider the following example with two anonymous record declarations:</span></span>

```fsharp
let x = {| X = 1 |}
let y = {| Y = 1 |}
```

<span data-ttu-id="49169-140">`x`和 `y` 值有不同的類型，且彼此不相容。</span><span class="sxs-lookup"><span data-stu-id="49169-140">The `x` and `y` values have different types and are not compatible with one another.</span></span> <span data-ttu-id="49169-141">它們不會 equatable，而且也不能比較。</span><span class="sxs-lookup"><span data-stu-id="49169-141">They are not equatable and they are not comparable.</span></span> <span data-ttu-id="49169-142">為了說明這一點，請考慮對等的命名記錄：</span><span class="sxs-lookup"><span data-stu-id="49169-142">To illustrate this, consider a named record equivalent:</span></span>

```fsharp
type X = { X: int }
type Y = { Y: int }

let x = { X = 1 }
let y = { Y = 1 }
```

<span data-ttu-id="49169-143">與類型相等或比較有關的匿名記錄與其命名記錄相等時，並沒有任何固有的差異。</span><span class="sxs-lookup"><span data-stu-id="49169-143">There isn't anything inherently different about anonymous records when compared with their named record equivalents when concerning type equivalency or comparison.</span></span>

### <a name="anonymous-records-use-structural-equality-and-comparison"></a><span data-ttu-id="49169-144">匿名記錄會使用結構相等和比較</span><span class="sxs-lookup"><span data-stu-id="49169-144">Anonymous records use structural equality and comparison</span></span>

<span data-ttu-id="49169-145">就像記錄類型一樣，匿名記錄是結構 equatable 且可比較的。</span><span class="sxs-lookup"><span data-stu-id="49169-145">Like record types, anonymous records are structurally equatable and comparable.</span></span> <span data-ttu-id="49169-146">只有在所有組成類型都支援相等和比較（例如記錄類型）的情況下，才會出現此情況。</span><span class="sxs-lookup"><span data-stu-id="49169-146">This is only true if all constituent types support equality and comparison, like with record types.</span></span> <span data-ttu-id="49169-147">若要支援相等或比較，兩個匿名記錄必須具有相同的「圖形」。</span><span class="sxs-lookup"><span data-stu-id="49169-147">To support equality or comparison, two anonymous records must have the same "shape".</span></span>

```fsharp
{| a = 1+1 |} = {| a = 2 |} // true
{| a = 1+1 |} > {| a = 1 |} // true

// error FS0001: Two anonymous record types have mismatched sets of field names '["a"]' and '["a"; "b"]'
{| a = 1 + 1 |} = {| a = 2;  b = 1|}
```

### <a name="anonymous-records-are-serializable"></a><span data-ttu-id="49169-148">匿名記錄可序列化</span><span class="sxs-lookup"><span data-stu-id="49169-148">Anonymous records are serializable</span></span>

<span data-ttu-id="49169-149">您可以將匿名記錄序列化，就像您可以使用命名記錄一樣。</span><span class="sxs-lookup"><span data-stu-id="49169-149">You can serialize anonymous records just as you can with named records.</span></span> <span data-ttu-id="49169-150">以下是使用 [Newtonsoft.Js的](https://www.nuget.org/packages/Newtonsoft.Json/)範例：</span><span class="sxs-lookup"><span data-stu-id="49169-150">Here is an example using [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/):</span></span>

```fsharp
open Newtonsoft.Json

let phillip' = {| name="Phillip"; age=28 |}
let philStr = JsonConvert.SerializeObject(phillip')

let phillip = JsonConvert.DeserializeObject<{|name: string; age: int|}>(philStr)
printfn $"Name: {phillip.name} Age: %d{phillip.age}"
```

<span data-ttu-id="49169-151">匿名記錄適用于透過網路傳送輕量資料，而不需要事先為您的序列化/還原序列化類型定義網域。</span><span class="sxs-lookup"><span data-stu-id="49169-151">Anonymous records are useful for sending lightweight data over a network without the need to define a domain for your serialized/deserialized types up front.</span></span>

### <a name="anonymous-records-interoperate-with-c-anonymous-types"></a><span data-ttu-id="49169-152">匿名記錄與 c # 匿名型別交互操作</span><span class="sxs-lookup"><span data-stu-id="49169-152">Anonymous records interoperate with C# anonymous types</span></span>

<span data-ttu-id="49169-153">您可以使用需要使用 [c # 匿名型別](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)的 .net API。</span><span class="sxs-lookup"><span data-stu-id="49169-153">It is possible to use a .NET API that requires the use of [C# anonymous types](../../csharp/programming-guide/classes-and-structs/anonymous-types.md).</span></span> <span data-ttu-id="49169-154">C # 匿名型別很容易使用匿名記錄來與相交互操作。</span><span class="sxs-lookup"><span data-stu-id="49169-154">C# anonymous types are trivial to interoperate with by using anonymous records.</span></span> <span data-ttu-id="49169-155">下列範例示範如何使用匿名記錄來呼叫需要匿名型別的 [LINQ](../../csharp/programming-guide/concepts/linq/index.md) 多載：</span><span class="sxs-lookup"><span data-stu-id="49169-155">The following example shows how to use anonymous records to call a [LINQ](../../csharp/programming-guide/concepts/linq/index.md) overload that requires an anonymous type:</span></span>

```fsharp
open System.Linq

let names = [ "Ana"; "Felipe"; "Emilia"]
let nameGrouping = names.Select(fun n -> {| Name = n; FirstLetter = n.[0] |})
for ng in nameGrouping do
    printfn $"{ng.Name} has first letter {ng.FirstLetter}"
```

<span data-ttu-id="49169-156">在整個 .NET 中，有許多其他的 Api 都需要使用匿名型別來傳遞。</span><span class="sxs-lookup"><span data-stu-id="49169-156">There are a multitude of other APIs used throughout .NET that require the use of passing in an anonymous type.</span></span> <span data-ttu-id="49169-157">匿名記錄是您使用它們的工具。</span><span class="sxs-lookup"><span data-stu-id="49169-157">Anonymous records are your tool for working with them.</span></span>

## <a name="limitations"></a><span data-ttu-id="49169-158">限制</span><span class="sxs-lookup"><span data-stu-id="49169-158">Limitations</span></span>

<span data-ttu-id="49169-159">匿名記錄對於其使用方式有一些限制。</span><span class="sxs-lookup"><span data-stu-id="49169-159">Anonymous records have some restrictions in their usage.</span></span> <span data-ttu-id="49169-160">有些是其設計固有的，但有些則適合變更。</span><span class="sxs-lookup"><span data-stu-id="49169-160">Some are inherent to their design, but others are amenable to change.</span></span>

### <a name="limitations-with-pattern-matching"></a><span data-ttu-id="49169-161">模式比對的限制</span><span class="sxs-lookup"><span data-stu-id="49169-161">Limitations with pattern matching</span></span>

<span data-ttu-id="49169-162">匿名記錄不支援模式比對，不同于命名記錄。</span><span class="sxs-lookup"><span data-stu-id="49169-162">Anonymous records do not support pattern matching, unlike named records.</span></span> <span data-ttu-id="49169-163">有三個原因：</span><span class="sxs-lookup"><span data-stu-id="49169-163">There are three reasons:</span></span>

1. <span data-ttu-id="49169-164">模式必須考慮匿名記錄的每個欄位，與命名的記錄類型不同。</span><span class="sxs-lookup"><span data-stu-id="49169-164">A pattern would have to account for every field of an anonymous record, unlike named record types.</span></span> <span data-ttu-id="49169-165">這是因為匿名記錄不支援結構化 subtyping –它們是名義類型。</span><span class="sxs-lookup"><span data-stu-id="49169-165">This is because anonymous records do not support structural subtyping – they are nominal types.</span></span>
2. <span data-ttu-id="49169-166">由於 (1) ，因此無法在模式比對運算式中使用其他模式，因為每個不同的模式會代表不同的匿名記錄類型。</span><span class="sxs-lookup"><span data-stu-id="49169-166">Because of (1), there is no ability to have additional patterns in a pattern match expression, as each distinct pattern would imply a different anonymous record type.</span></span>
3. <span data-ttu-id="49169-167">由於 (3) ，任何匿名記錄模式都比使用 "dot" 標記法更詳細。</span><span class="sxs-lookup"><span data-stu-id="49169-167">Because of (3), any anonymous record pattern would be more verbose than the use of “dot” notation.</span></span>

<span data-ttu-id="49169-168">有開放語言的建議，可 [讓您在有限的內容中進行模式](https://github.com/fsharp/fslang-suggestions/issues/713)比對。</span><span class="sxs-lookup"><span data-stu-id="49169-168">There is an open language suggestion to [allow pattern matching in limited contexts](https://github.com/fsharp/fslang-suggestions/issues/713).</span></span>

### <a name="limitations-with-mutability"></a><span data-ttu-id="49169-169">可變動性的限制</span><span class="sxs-lookup"><span data-stu-id="49169-169">Limitations with mutability</span></span>

<span data-ttu-id="49169-170">目前無法以資料定義匿名記錄 `mutable` 。</span><span class="sxs-lookup"><span data-stu-id="49169-170">It is not currently possible to define an anonymous record with `mutable` data.</span></span> <span data-ttu-id="49169-171">有開放的 [語言建議](https://github.com/fsharp/fslang-suggestions/issues/732) 可允許可變數據。</span><span class="sxs-lookup"><span data-stu-id="49169-171">There is an [open language suggestion](https://github.com/fsharp/fslang-suggestions/issues/732) to allow mutable data.</span></span>

### <a name="limitations-with-struct-anonymous-records"></a><span data-ttu-id="49169-172">結構匿名記錄的限制</span><span class="sxs-lookup"><span data-stu-id="49169-172">Limitations with struct anonymous records</span></span>

<span data-ttu-id="49169-173">您無法將結構匿名記錄宣告為 `IsByRefLike` 或 `IsReadOnly` 。</span><span class="sxs-lookup"><span data-stu-id="49169-173">It is not possible to declare struct anonymous records as `IsByRefLike` or `IsReadOnly`.</span></span> <span data-ttu-id="49169-174">和匿名記錄有 [開放的語言建議](https://github.com/fsharp/fslang-suggestions/issues/712) `IsByRefLike` `IsReadOnly` 。</span><span class="sxs-lookup"><span data-stu-id="49169-174">There is an [open language suggestion](https://github.com/fsharp/fslang-suggestions/issues/712) to for `IsByRefLike` and `IsReadOnly` anonymous records.</span></span>
