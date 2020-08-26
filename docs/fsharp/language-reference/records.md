---
title: 記錄
description: '瞭解 F # 記錄如何代表簡單的命名值匯總，並選擇性地包含成員。'
ms.date: 08/15/2020
ms.openlocfilehash: a72c0f15b58407e7d759e2fb5a1b35a7fc0d29e3
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88812350"
---
# <a name="records"></a><span data-ttu-id="397a5-103">記錄</span><span class="sxs-lookup"><span data-stu-id="397a5-103">Records</span></span>

<span data-ttu-id="397a5-104">記錄表示具名值的簡單彙總，並選擇性地搭配成員。</span><span class="sxs-lookup"><span data-stu-id="397a5-104">Records represent simple aggregates of named values, optionally with members.</span></span> <span data-ttu-id="397a5-105">可以是結構或參考型別。</span><span class="sxs-lookup"><span data-stu-id="397a5-105">They can either be structs or reference types.</span></span>  <span data-ttu-id="397a5-106">它們預設為參考類型。</span><span class="sxs-lookup"><span data-stu-id="397a5-106">They are reference types by default.</span></span>

## <a name="syntax"></a><span data-ttu-id="397a5-107">語法</span><span class="sxs-lookup"><span data-stu-id="397a5-107">Syntax</span></span>

```fsharp
[ attributes ]
type [accessibility-modifier] typename =
    { [ mutable ] label1 : type1;
      [ mutable ] label2 : type2;
      ... }
    [ member-list ]
```

## <a name="remarks"></a><span data-ttu-id="397a5-108">備註</span><span class="sxs-lookup"><span data-stu-id="397a5-108">Remarks</span></span>

<span data-ttu-id="397a5-109">在先前的語法中， *typename* 是記錄類型的名稱， *label1* 和 *label2* 是值的名稱（稱為 *標籤*），而 *type1* 和 *type2* 是這些值的類型。</span><span class="sxs-lookup"><span data-stu-id="397a5-109">In the previous syntax, *typename* is the name of the record type, *label1* and *label2* are names of values, referred to as *labels*, and *type1* and *type2* are the types of these values.</span></span> <span data-ttu-id="397a5-110">*成員清單* 是類型的選擇性成員清單。</span><span class="sxs-lookup"><span data-stu-id="397a5-110">*member-list* is the optional list of members for the type.</span></span>  <span data-ttu-id="397a5-111">您可以使用 `[<Struct>]` 屬性來建立結構記錄，而不是參考型別的記錄。</span><span class="sxs-lookup"><span data-stu-id="397a5-111">You can use the `[<Struct>]` attribute to create a struct record rather than a record which is a reference type.</span></span>

<span data-ttu-id="397a5-112">以下有一些範例。</span><span class="sxs-lookup"><span data-stu-id="397a5-112">Following are some examples.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1901.fs)]

<span data-ttu-id="397a5-113">當每個標籤都在不同的行上時，分號是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="397a5-113">When each label is on a separate line, the semicolon is optional.</span></span>

<span data-ttu-id="397a5-114">您可以在稱為 *記錄運算式*的運算式中設定值。</span><span class="sxs-lookup"><span data-stu-id="397a5-114">You can set values in expressions known as *record expressions*.</span></span> <span data-ttu-id="397a5-115">如果標籤與其他記錄類型) 的不同，則編譯器會從所使用的標籤推斷類型 (。</span><span class="sxs-lookup"><span data-stu-id="397a5-115">The compiler infers the type from the labels used (if the labels are sufficiently distinct from those of other record types).</span></span> <span data-ttu-id="397a5-116">括弧 ( {} ) 括住記錄運算式。</span><span class="sxs-lookup"><span data-stu-id="397a5-116">Braces ({ }) enclose the record expression.</span></span> <span data-ttu-id="397a5-117">下列程式碼會顯示記錄運算式，該運算式會使用具有標籤和的三個 float 元素來初始化記錄 `x` `y` `z` 。</span><span class="sxs-lookup"><span data-stu-id="397a5-117">The following code shows a record expression that initializes a record with three float elements with labels `x`, `y` and `z`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1907.fs)]

<span data-ttu-id="397a5-118">如果有另一種類型也有相同的標籤，請勿使用縮寫的表單。</span><span class="sxs-lookup"><span data-stu-id="397a5-118">Do not use the shortened form if there could be another type that also has the same labels.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1903.fs)]

<span data-ttu-id="397a5-119">最近宣告類型的標籤優先于先前宣告的型別，因此在上述範例中， `mypoint3D` 會推斷為 `Point3D` 。</span><span class="sxs-lookup"><span data-stu-id="397a5-119">The labels of the most recently declared type take precedence over those of the previously declared type, so in the preceding example, `mypoint3D` is inferred to be `Point3D`.</span></span> <span data-ttu-id="397a5-120">您可以明確地指定記錄類型，如下列程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="397a5-120">You can explicitly specify the record type, as in the following code.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1908.fs)]

<span data-ttu-id="397a5-121">您可以針對記錄類型定義方法，就像類別類型一樣。</span><span class="sxs-lookup"><span data-stu-id="397a5-121">Methods can be defined for record types just as for class types.</span></span>

## <a name="creating-records-by-using-record-expressions"></a><span data-ttu-id="397a5-122">使用記錄運算式建立記錄</span><span class="sxs-lookup"><span data-stu-id="397a5-122">Creating Records by Using Record Expressions</span></span>

<span data-ttu-id="397a5-123">您可以使用記錄中定義的標籤來初始化記錄。</span><span class="sxs-lookup"><span data-stu-id="397a5-123">You can initialize records by using the labels that are defined in the record.</span></span> <span data-ttu-id="397a5-124">執行這項工作的運算式稱為「 *記錄運算式*」。</span><span class="sxs-lookup"><span data-stu-id="397a5-124">An expression that does this is referred to as a *record expression*.</span></span> <span data-ttu-id="397a5-125">使用大括弧來括住記錄運算式，並使用分號做為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="397a5-125">Use braces to enclose the record expression and use the semicolon as a delimiter.</span></span>

<span data-ttu-id="397a5-126">下列範例顯示如何建立記錄。</span><span class="sxs-lookup"><span data-stu-id="397a5-126">The following example shows how to create a record.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1904.fs)]

<span data-ttu-id="397a5-127">在記錄運算式和類型定義中，最後一個欄位後面的分號是選擇性的，不論這些欄位是否全都在同一行。</span><span class="sxs-lookup"><span data-stu-id="397a5-127">The semicolons after the last field in the record expression and in the type definition are optional, regardless of whether the fields are all in one line.</span></span>

<span data-ttu-id="397a5-128">當您建立記錄時，必須提供每個欄位的值。</span><span class="sxs-lookup"><span data-stu-id="397a5-128">When you create a record, you must supply values for each field.</span></span> <span data-ttu-id="397a5-129">您無法在初始化運算式中參考任何欄位的其他欄位值。</span><span class="sxs-lookup"><span data-stu-id="397a5-129">You cannot refer to the values of other fields in the initialization expression for any field.</span></span>

<span data-ttu-id="397a5-130">在下列程式碼中，的型別 `myRecord2` 是從欄位名稱推斷而來。</span><span class="sxs-lookup"><span data-stu-id="397a5-130">In the following code, the type of `myRecord2` is inferred from the names of the fields.</span></span> <span data-ttu-id="397a5-131">（選擇性）您可以明確地指定型別名稱。</span><span class="sxs-lookup"><span data-stu-id="397a5-131">Optionally, you can specify the type name explicitly.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

<span data-ttu-id="397a5-132">當您必須複製現有的記錄，而且可能變更部分域值時，另一種形式的記錄結構可能很有用。</span><span class="sxs-lookup"><span data-stu-id="397a5-132">Another form of record construction can be useful when you have to copy an existing record, and possibly change some of the field values.</span></span> <span data-ttu-id="397a5-133">下面這行程式碼將說明這一點。</span><span class="sxs-lookup"><span data-stu-id="397a5-133">The following line of code illustrates this.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

<span data-ttu-id="397a5-134">這種形式的記錄運算式稱為「 *複製和更新記錄運算式*」。</span><span class="sxs-lookup"><span data-stu-id="397a5-134">This form of the record expression is called the *copy and update record expression*.</span></span>

<span data-ttu-id="397a5-135">依預設，記錄是不可變的;不過，您可以使用複製和更新運算式，輕鬆地建立修改過的記錄。</span><span class="sxs-lookup"><span data-stu-id="397a5-135">Records are immutable by default; however, you can easily create modified records by using a copy and update expression.</span></span> <span data-ttu-id="397a5-136">您也可以明確地指定可變欄位。</span><span class="sxs-lookup"><span data-stu-id="397a5-136">You can also explicitly specify a mutable field.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1909.fs)]

<span data-ttu-id="397a5-137">請勿使用 DefaultValue 屬性搭配記錄欄位。</span><span class="sxs-lookup"><span data-stu-id="397a5-137">Don't use the DefaultValue attribute with record fields.</span></span> <span data-ttu-id="397a5-138">更好的方法是使用已初始化為預設值的欄位來定義記錄的預設實例，然後使用複製和更新記錄運算式來設定與預設值不同的任何欄位。</span><span class="sxs-lookup"><span data-stu-id="397a5-138">A better approach is to define default instances of records with fields that are initialized to default values and then use a copy and update record expression to set any fields that differ from the default values.</span></span>

```fsharp
// Rather than use [<DefaultValue>], define a default record.
type MyRecord =
    { Field1 : int
      Field2 : int }

let defaultRecord1 = { Field1 = 0; Field2 = 0 }
let defaultRecord2 = { Field1 = 1; Field2 = 25 }

// Use the with keyword to populate only a few chosen fields
// and leave the rest with default values.
let rr3 = { defaultRecord1 with Field2 = 42 }
```

## <a name="creating-mutually-recursive-records"></a><span data-ttu-id="397a5-139">建立相互遞迴記錄</span><span class="sxs-lookup"><span data-stu-id="397a5-139">Creating Mutually Recursive Records</span></span>

<span data-ttu-id="397a5-140">建立記錄時，您可能會想要讓它相依于您稍後要定義的另一種類型。</span><span class="sxs-lookup"><span data-stu-id="397a5-140">Sometime when creating a record, you may want to have it depend on another type that you would like to define afterwards.</span></span> <span data-ttu-id="397a5-141">這是編譯錯誤，除非您將記錄類型定義為相互遞迴。</span><span class="sxs-lookup"><span data-stu-id="397a5-141">This is a compile error unless you define the record types to be mutually recursive.</span></span>

<span data-ttu-id="397a5-142">使用關鍵字來定義相互遞迴記錄 `and` 。</span><span class="sxs-lookup"><span data-stu-id="397a5-142">Defining mutually recursive records is done with the `and` keyword.</span></span> <span data-ttu-id="397a5-143">這可讓您將2個以上的記錄類型連結在一起。</span><span class="sxs-lookup"><span data-stu-id="397a5-143">This lets you link 2 or more record types together.</span></span>

<span data-ttu-id="397a5-144">例如，下列程式碼會將 `Person` 和 `Address` 類型定義為相互遞迴：</span><span class="sxs-lookup"><span data-stu-id="397a5-144">For example, the following code defines a `Person` and `Address` type as mutually recursive:</span></span>

```fsharp
// Create a Person type and use the Address type that is not defined
type Person =
  { Name: string
    Age: int
    Address: Address }
// Define the Address type which is used in the Person record
and Address =
  { Line1: string
    Line2: string
    PostCode: string
    Occupant: Person }
```

<span data-ttu-id="397a5-145">如果您要定義先前的範例而不指定 `and` 關鍵字，則不會進行編譯。</span><span class="sxs-lookup"><span data-stu-id="397a5-145">If you were to define the previous example without the `and` keyword, then it would not compile.</span></span> <span data-ttu-id="397a5-146">`and`相互遞迴定義必須有關鍵詞。</span><span class="sxs-lookup"><span data-stu-id="397a5-146">The `and` keyword is required for mutually recursive definitions.</span></span>

## <a name="pattern-matching-with-records"></a><span data-ttu-id="397a5-147">使用記錄進行模式比對</span><span class="sxs-lookup"><span data-stu-id="397a5-147">Pattern Matching with Records</span></span>

<span data-ttu-id="397a5-148">記錄可以搭配模式比對使用。</span><span class="sxs-lookup"><span data-stu-id="397a5-148">Records can be used with pattern matching.</span></span> <span data-ttu-id="397a5-149">您可以明確指定某些欄位，並提供變數給將在相符時指派的其他欄位。</span><span class="sxs-lookup"><span data-stu-id="397a5-149">You can specify some fields explicitly and provide variables for other fields that will be assigned when a match occurs.</span></span> <span data-ttu-id="397a5-150">下列程式碼範例會說明這點。</span><span class="sxs-lookup"><span data-stu-id="397a5-150">The following code example illustrates this.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1910.fs)]

<span data-ttu-id="397a5-151">此程式碼的輸出如下所示。</span><span class="sxs-lookup"><span data-stu-id="397a5-151">The output of this code is as follows.</span></span>

```console
Point is at the origin.
Point is on the x-axis. Value is 100.000000.
Point is at (10.000000, 0.000000, -1.000000).
```

## <a name="records-and-members"></a><span data-ttu-id="397a5-152">記錄和成員</span><span class="sxs-lookup"><span data-stu-id="397a5-152">Records and members</span></span>

<span data-ttu-id="397a5-153">您可以在記錄上指定成員，就像您可以使用類別一樣。</span><span class="sxs-lookup"><span data-stu-id="397a5-153">You can specify members on records much like you can with classes.</span></span> <span data-ttu-id="397a5-154">不支援欄位。</span><span class="sxs-lookup"><span data-stu-id="397a5-154">There is no support for fields.</span></span> <span data-ttu-id="397a5-155">常見的方法是定義 `Default` 靜態成員，以便輕鬆地記錄結構：</span><span class="sxs-lookup"><span data-stu-id="397a5-155">A common approach is to define a `Default` static member for easy record construction:</span></span>

```fsharp
type Person =
  { Name: string
    Age: int
    Address: string }

    static member Default =
        { Name = "Phillip"
          Age = 12
          Address = "123 happy fun street" }

let defaultPerson = Person.Default
```

<span data-ttu-id="397a5-156">如果您使用自我識別碼，該識別碼會參考其成員所呼叫之記錄的實例：</span><span class="sxs-lookup"><span data-stu-id="397a5-156">If you use a self identifier, that identifier refers to the instance of the record whose member is called:</span></span>

```fsharp
type Person =
  { Name: string
    Age: int
    Address: string }

    member this.WeirdToString() =
        this.Name + this.Address + string this.Age

let p = { Name = "a"; Age = 12; Address = "abc123 }
let weirdString = p.WeirdToString()
```

## <a name="differences-between-records-and-classes"></a><span data-ttu-id="397a5-157">記錄與類別之間的差異</span><span class="sxs-lookup"><span data-stu-id="397a5-157">Differences Between Records and Classes</span></span>

<span data-ttu-id="397a5-158">記錄欄位與類別不同之處在于它們會自動公開為屬性，並用於建立和複製記錄。</span><span class="sxs-lookup"><span data-stu-id="397a5-158">Record fields differ from classes in that they are automatically exposed as properties, and they are used in the creation and copying of records.</span></span> <span data-ttu-id="397a5-159">記錄結構與類別結構也不同。</span><span class="sxs-lookup"><span data-stu-id="397a5-159">Record construction also differs from class construction.</span></span> <span data-ttu-id="397a5-160">在記錄類型中，您無法定義函數。</span><span class="sxs-lookup"><span data-stu-id="397a5-160">In a record type, you cannot define a constructor.</span></span> <span data-ttu-id="397a5-161">相反地，本主題所述的結構語法也適用。</span><span class="sxs-lookup"><span data-stu-id="397a5-161">Instead, the construction syntax described in this topic applies.</span></span> <span data-ttu-id="397a5-162">類別在兩個函式參數、欄位和屬性之間沒有直接關聯性。</span><span class="sxs-lookup"><span data-stu-id="397a5-162">Classes have no direct relationship between constructor parameters, fields, and properties.</span></span>

<span data-ttu-id="397a5-163">如同 union 和 structure 型別，記錄具有結構化相等的語法。</span><span class="sxs-lookup"><span data-stu-id="397a5-163">Like union and structure types, records have structural equality semantics.</span></span> <span data-ttu-id="397a5-164">類別具有參考相等的語法。</span><span class="sxs-lookup"><span data-stu-id="397a5-164">Classes have reference equality semantics.</span></span> <span data-ttu-id="397a5-165">下列程式碼範例示範此工作。</span><span class="sxs-lookup"><span data-stu-id="397a5-165">The following code example demonstrates this.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1911.fs)]

<span data-ttu-id="397a5-166">此程式碼的輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="397a5-166">The output of this code is as follows:</span></span>

```console
The records are equal.
```

<span data-ttu-id="397a5-167">如果您以類別撰寫相同的程式碼，這兩個類別物件將會不相等，因為這兩個值會在堆積上代表兩個物件，而只有位址會 (比較，除非類別類型會覆寫 `System.Object.Equals`) 的方法。</span><span class="sxs-lookup"><span data-stu-id="397a5-167">If you write the same code with classes, the two class objects would be unequal because the two values would represent two objects on the heap and only the addresses would be compared (unless the class type overrides the `System.Object.Equals` method).</span></span>

<span data-ttu-id="397a5-168">如果您需要記錄的參考相等，請在 `[<ReferenceEquality>]` 記錄上方加入屬性。</span><span class="sxs-lookup"><span data-stu-id="397a5-168">If you need reference equality for records, add the attribute `[<ReferenceEquality>]` above the record.</span></span>

## <a name="see-also"></a><span data-ttu-id="397a5-169">另請參閱</span><span class="sxs-lookup"><span data-stu-id="397a5-169">See also</span></span>

- [<span data-ttu-id="397a5-170">F# 類型</span><span class="sxs-lookup"><span data-stu-id="397a5-170">F# Types</span></span>](fsharp-types.md)
- [<span data-ttu-id="397a5-171">類別</span><span class="sxs-lookup"><span data-stu-id="397a5-171">Classes</span></span>](classes.md)
- [<span data-ttu-id="397a5-172">F # 語言參考</span><span class="sxs-lookup"><span data-stu-id="397a5-172">F# Language Reference</span></span>](index.md)
- [<span data-ttu-id="397a5-173">參考相等</span><span class="sxs-lookup"><span data-stu-id="397a5-173">Reference-Equality</span></span>](https://fsharp.github.io/fsharp-core-docs/reference/fsharp-core-referenceequalityattribute.html)
- [<span data-ttu-id="397a5-174">模式比對</span><span class="sxs-lookup"><span data-stu-id="397a5-174">Pattern Matching</span></span>](pattern-matching.md)
