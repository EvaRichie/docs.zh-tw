---
title: 模式比對
description: '瞭解如何在 F # 中使用模式來比較資料與邏輯結構、將資料分解為構成部分，或從資料中取出資訊。'
ms.date: 08/15/2020
ms.openlocfilehash: 6d284b941824bc15a8e872a4e28e22c0e159191d
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88811505"
---
# <a name="pattern-matching"></a><span data-ttu-id="665b0-103">模式比對</span><span class="sxs-lookup"><span data-stu-id="665b0-103">Pattern Matching</span></span>

<span data-ttu-id="665b0-104">模式是轉換輸入資料的規則。</span><span class="sxs-lookup"><span data-stu-id="665b0-104">Patterns are rules for transforming input data.</span></span> <span data-ttu-id="665b0-105">在 F # 語言中會使用它們來比較資料與邏輯結構或結構、將資料分解為構成部分，或從資料以各種方式將資訊解壓縮。</span><span class="sxs-lookup"><span data-stu-id="665b0-105">They are used throughout the F# language to compare data with a logical structure or structures, decompose data into constituent parts, or extract information from data in various ways.</span></span>

## <a name="remarks"></a><span data-ttu-id="665b0-106">備註</span><span class="sxs-lookup"><span data-stu-id="665b0-106">Remarks</span></span>

<span data-ttu-id="665b0-107">模式用於許多語言結構，例如 `match` 運算式。</span><span class="sxs-lookup"><span data-stu-id="665b0-107">Patterns are used in many language constructs, such as the `match` expression.</span></span> <span data-ttu-id="665b0-108">當您要處理系結中函式的引數 `let` 、lambda 運算式，以及與運算式相關聯的例外狀況處理常式時，就會使用這些函數 `try...with` 。</span><span class="sxs-lookup"><span data-stu-id="665b0-108">They are used when you are processing arguments for functions in `let` bindings, lambda expressions, and in the exception handlers associated with the `try...with` expression.</span></span> <span data-ttu-id="665b0-109">如需詳細資訊，請參閱 [Match 運算式](match-expressions.md)、 [let Bindings](./functions/let-bindings.md)、 [Lambda 運算式： `fun` 關鍵字](./functions/lambda-expressions-the-fun-keyword.md)和 [例外狀況： `try...with` 運算式](./exception-handling/the-try-with-expression.md)。</span><span class="sxs-lookup"><span data-stu-id="665b0-109">For more information, see [Match Expressions](match-expressions.md), [let Bindings](./functions/let-bindings.md), [Lambda Expressions: The `fun` Keyword](./functions/lambda-expressions-the-fun-keyword.md), and [Exceptions: The `try...with` Expression](./exception-handling/the-try-with-expression.md).</span></span>

<span data-ttu-id="665b0-110">例如，在運算式中 `match` ， *模式* 會跟在管道符號之後。</span><span class="sxs-lookup"><span data-stu-id="665b0-110">For example, in the `match` expression, the *pattern* is what follows the pipe symbol.</span></span>

```fsharp
match expression with
| pattern [ when condition ] -> result-expression
...
```

<span data-ttu-id="665b0-111">每個模式都是以某種方式轉換輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="665b0-111">Each pattern acts as a rule for transforming input in some way.</span></span> <span data-ttu-id="665b0-112">在 `match` 運算式中，會依序檢查每個模式，以查看輸入資料是否與模式相容。</span><span class="sxs-lookup"><span data-stu-id="665b0-112">In the `match` expression, each pattern is examined in turn to see if the input data is compatible with the pattern.</span></span> <span data-ttu-id="665b0-113">如果找到相符的結果運算式，就會執行結果運算式。</span><span class="sxs-lookup"><span data-stu-id="665b0-113">If a match is found, the result expression is executed.</span></span> <span data-ttu-id="665b0-114">如果找不到相符項，則會測試下一個模式規則。</span><span class="sxs-lookup"><span data-stu-id="665b0-114">If a match is not found, the next pattern rule is tested.</span></span> <span data-ttu-id="665b0-115">在比對[運算式](match-expressions.md)中說明選擇性的 when*條件*部分。</span><span class="sxs-lookup"><span data-stu-id="665b0-115">The optional when *condition* part is explained in [Match Expressions](match-expressions.md).</span></span>

<span data-ttu-id="665b0-116">下表顯示支援的模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-116">Supported patterns are shown in the following table.</span></span> <span data-ttu-id="665b0-117">在執行時間，輸入會根據表格中所列的順序，針對下列每個模式進行測試，而模式會以遞迴方式套用（從第一次到最後，當它們出現在您的程式碼中），並從左至右套用至每一行的模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-117">At run time, the input is tested against each of the following patterns in the order listed in the table, and patterns are applied recursively, from first to last as they appear in your code, and from left to right for the patterns on each line.</span></span>

|<span data-ttu-id="665b0-118">名稱</span><span class="sxs-lookup"><span data-stu-id="665b0-118">Name</span></span>|<span data-ttu-id="665b0-119">描述</span><span class="sxs-lookup"><span data-stu-id="665b0-119">Description</span></span>|<span data-ttu-id="665b0-120">範例</span><span class="sxs-lookup"><span data-stu-id="665b0-120">Example</span></span>|
|----|-----------|-------|
|<span data-ttu-id="665b0-121">常數模式</span><span class="sxs-lookup"><span data-stu-id="665b0-121">Constant pattern</span></span>|<span data-ttu-id="665b0-122">任何數值、字元或字串常值、列舉常數或已定義的常值識別碼</span><span class="sxs-lookup"><span data-stu-id="665b0-122">Any numeric, character, or string literal, an enumeration constant, or a defined literal identifier</span></span>|<span data-ttu-id="665b0-123">`1.0`, `"test"`, `30`, `Color.Red`</span><span class="sxs-lookup"><span data-stu-id="665b0-123">`1.0`, `"test"`, `30`, `Color.Red`</span></span>|
|<span data-ttu-id="665b0-124">識別碼模式</span><span class="sxs-lookup"><span data-stu-id="665b0-124">Identifier pattern</span></span>|<span data-ttu-id="665b0-125">差異聯集的 case 值、例外狀況標籤或作用中模式案例</span><span class="sxs-lookup"><span data-stu-id="665b0-125">A case value of a discriminated union, an exception label, or an active pattern case</span></span>|`Some(x)`<br /><br />`Failure(msg)`|
|<span data-ttu-id="665b0-126">變數模式</span><span class="sxs-lookup"><span data-stu-id="665b0-126">Variable pattern</span></span>|<span data-ttu-id="665b0-127">*識別碼*</span><span class="sxs-lookup"><span data-stu-id="665b0-127">*identifier*</span></span>|`a`|
|<span data-ttu-id="665b0-128">`as` 模式</span><span class="sxs-lookup"><span data-stu-id="665b0-128">`as` pattern</span></span>|<span data-ttu-id="665b0-129">*模式* as *識別碼*</span><span class="sxs-lookup"><span data-stu-id="665b0-129">*pattern* as *identifier*</span></span>|`(a, b) as tuple1`|
|<span data-ttu-id="665b0-130">或模式</span><span class="sxs-lookup"><span data-stu-id="665b0-130">OR pattern</span></span>|<span data-ttu-id="665b0-131">*pattern1* &#124; *pattern2*</span><span class="sxs-lookup"><span data-stu-id="665b0-131">*pattern1* &#124; *pattern2*</span></span>|<code>([h] &#124; [h; _])</code>|
|<span data-ttu-id="665b0-132">AND 模式</span><span class="sxs-lookup"><span data-stu-id="665b0-132">AND pattern</span></span>|<span data-ttu-id="665b0-133">*pattern1* &amp;*pattern2*</span><span class="sxs-lookup"><span data-stu-id="665b0-133">*pattern1* &amp; *pattern2*</span></span>|`(a, b) & (_, "test")`|
|<span data-ttu-id="665b0-134">缺點模式</span><span class="sxs-lookup"><span data-stu-id="665b0-134">Cons pattern</span></span>|<span data-ttu-id="665b0-135">*identifier* ：： *list-identifier*</span><span class="sxs-lookup"><span data-stu-id="665b0-135">*identifier* :: *list-identifier*</span></span>|`h :: t`|
|<span data-ttu-id="665b0-136">清單模式</span><span class="sxs-lookup"><span data-stu-id="665b0-136">List pattern</span></span>|<span data-ttu-id="665b0-137">[ *pattern_1*; ...; *pattern_n* ]</span><span class="sxs-lookup"><span data-stu-id="665b0-137">[ *pattern_1*; ... ; *pattern_n* ]</span></span>|`[ a; b; c ]`|
|<span data-ttu-id="665b0-138">陣列模式</span><span class="sxs-lookup"><span data-stu-id="665b0-138">Array pattern</span></span>|<span data-ttu-id="665b0-139">[&#124; *pattern_1*; ...; *pattern_n* &#124;]</span><span class="sxs-lookup"><span data-stu-id="665b0-139">[&#124; *pattern_1*; ..; *pattern_n* &#124;]</span></span>|<code>[&#124; a; b; c &#124;]</code>|
|<span data-ttu-id="665b0-140">括弧模式</span><span class="sxs-lookup"><span data-stu-id="665b0-140">Parenthesized pattern</span></span>|<span data-ttu-id="665b0-141"> ( *模式* ) </span><span class="sxs-lookup"><span data-stu-id="665b0-141">( *pattern* )</span></span>|`( a )`|
|<span data-ttu-id="665b0-142">元組模式</span><span class="sxs-lookup"><span data-stu-id="665b0-142">Tuple pattern</span></span>|<span data-ttu-id="665b0-143"> ( *pattern_1*， *pattern_n* ) </span><span class="sxs-lookup"><span data-stu-id="665b0-143">( *pattern_1*, ... , *pattern_n* )</span></span>|`( a, b )`|
|<span data-ttu-id="665b0-144">記錄模式</span><span class="sxs-lookup"><span data-stu-id="665b0-144">Record pattern</span></span>|<span data-ttu-id="665b0-145">{ *identifier1*  = *pattern_1*;... ;*identifier_n*  = *pattern_n* }</span><span class="sxs-lookup"><span data-stu-id="665b0-145">{ *identifier1* = *pattern_1*; ... ; *identifier_n* = *pattern_n* }</span></span>|`{ Name = name; }`|
|<span data-ttu-id="665b0-146">萬用字元模式</span><span class="sxs-lookup"><span data-stu-id="665b0-146">Wildcard pattern</span></span>|<span data-ttu-id="665b0-147">_</span><span class="sxs-lookup"><span data-stu-id="665b0-147">_</span></span>|`_`|
|<span data-ttu-id="665b0-148">搭配類型注釋的模式</span><span class="sxs-lookup"><span data-stu-id="665b0-148">Pattern together with type annotation</span></span>|<span data-ttu-id="665b0-149">*模式* ： *類型*</span><span class="sxs-lookup"><span data-stu-id="665b0-149">*pattern* : *type*</span></span>|`a : int`|
|<span data-ttu-id="665b0-150">類型測試模式</span><span class="sxs-lookup"><span data-stu-id="665b0-150">Type test pattern</span></span>|<span data-ttu-id="665b0-151">:?</span><span class="sxs-lookup"><span data-stu-id="665b0-151">:?</span></span> <span data-ttu-id="665b0-152">*類型* [as *識別碼* ]</span><span class="sxs-lookup"><span data-stu-id="665b0-152">*type* [ as *identifier* ]</span></span>|`:? System.DateTime as dt`|
|<span data-ttu-id="665b0-153">Null 模式</span><span class="sxs-lookup"><span data-stu-id="665b0-153">Null pattern</span></span>|<span data-ttu-id="665b0-154">null</span><span class="sxs-lookup"><span data-stu-id="665b0-154">null</span></span>|`null`|

## <a name="constant-patterns"></a><span data-ttu-id="665b0-155">常數模式</span><span class="sxs-lookup"><span data-stu-id="665b0-155">Constant Patterns</span></span>

<span data-ttu-id="665b0-156">常數模式包括數值、字元和字串常值、列舉常數 (包含) 包含的列舉型別名稱。</span><span class="sxs-lookup"><span data-stu-id="665b0-156">Constant patterns are numeric, character, and string literals, enumeration constants (with the enumeration type name included).</span></span> <span data-ttu-id="665b0-157">`match`只有常數模式的運算式可以與其他語言的 case 語句進行比較。</span><span class="sxs-lookup"><span data-stu-id="665b0-157">A `match` expression that has only constant patterns can be compared to a case statement in other languages.</span></span> <span data-ttu-id="665b0-158">輸入會與常值進行比較，如果值相等，則模式會相符。</span><span class="sxs-lookup"><span data-stu-id="665b0-158">The input is compared with the literal value and the pattern matches if the values are equal.</span></span> <span data-ttu-id="665b0-159">常值的型別必須與輸入的型別相容。</span><span class="sxs-lookup"><span data-stu-id="665b0-159">The type of the literal must be compatible with the type of the input.</span></span>

<span data-ttu-id="665b0-160">下列範例示範如何使用常值模式，並同時使用變數模式和或模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-160">The following example demonstrates the use of literal patterns, and also uses a variable pattern and an OR pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4801.fs)]

<span data-ttu-id="665b0-161">常值模式的另一個範例是以列舉常數為基礎的模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-161">Another example of a literal pattern is a pattern based on enumeration constants.</span></span> <span data-ttu-id="665b0-162">當您使用列舉常數時，必須指定列舉型別名稱。</span><span class="sxs-lookup"><span data-stu-id="665b0-162">You must specify the enumeration type name when you use enumeration constants.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4802.fs)]

## <a name="identifier-patterns"></a><span data-ttu-id="665b0-163">識別碼模式</span><span class="sxs-lookup"><span data-stu-id="665b0-163">Identifier Patterns</span></span>

<span data-ttu-id="665b0-164">如果模式是形成有效識別碼的字元字串，則識別碼的格式會決定模式的比對方式。</span><span class="sxs-lookup"><span data-stu-id="665b0-164">If the pattern is a string of characters that forms a valid identifier, the form of the identifier determines how the pattern is matched.</span></span> <span data-ttu-id="665b0-165">如果識別碼的長度超過單一字元，並以大寫字元開頭，則編譯器會嘗試使其符合識別碼模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-165">If the identifier is longer than a single character and starts with an uppercase character, the compiler tries to make a match to the identifier pattern.</span></span> <span data-ttu-id="665b0-166">此模式的識別碼可能是以常值屬性標記的值、差異聯集大小寫、例外狀況識別碼或使用中的模式案例。</span><span class="sxs-lookup"><span data-stu-id="665b0-166">The identifier for this pattern could be a value marked with the Literal attribute, a discriminated union case, an exception identifier, or an active pattern case.</span></span> <span data-ttu-id="665b0-167">如果找不到相符的識別碼，則比對會失敗，而下一個模式規則（變數模式）會與輸入進行比較。</span><span class="sxs-lookup"><span data-stu-id="665b0-167">If no matching identifier is found, the match fails and the next pattern rule, the variable pattern, is compared to the input.</span></span>

<span data-ttu-id="665b0-168">差異聯集模式可以是簡單名稱的案例，也可以具有值或包含多個值的元組。</span><span class="sxs-lookup"><span data-stu-id="665b0-168">Discriminated union patterns can be simple named cases or they can have a value, or a tuple containing multiple values.</span></span> <span data-ttu-id="665b0-169">如果有值，您必須指定值的識別碼。</span><span class="sxs-lookup"><span data-stu-id="665b0-169">If there is a value, you must specify an identifier for the value.</span></span> <span data-ttu-id="665b0-170">在元組的案例中，您必須為元組的每個專案提供具有識別碼的元組模式，或使用一個或多個命名聯集欄位的功能變數名稱來提供識別碼。</span><span class="sxs-lookup"><span data-stu-id="665b0-170">In the case of a tuple, you must supply a tuple pattern with an identifier for each element of the tuple or an identifier with a field name for one or more named union fields.</span></span> <span data-ttu-id="665b0-171">如需範例，請參閱本節中的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="665b0-171">See the code examples in this section for examples.</span></span>

<span data-ttu-id="665b0-172">此 `option` 類型是具有兩個案例的差異聯集， `Some` 以及 `None` 。</span><span class="sxs-lookup"><span data-stu-id="665b0-172">The `option` type is a discriminated union that has two cases, `Some` and `None`.</span></span> <span data-ttu-id="665b0-173">其中一個案例 (`Some`) 有一個值，但另一個 (`None`) 只是一個命名的案例。</span><span class="sxs-lookup"><span data-stu-id="665b0-173">One case (`Some`) has a value, but the other (`None`) is just a named case.</span></span> <span data-ttu-id="665b0-174">因此， `Some` 必須有與案例相關聯之值的變數 `Some` ，但 `None` 必須單獨出現。</span><span class="sxs-lookup"><span data-stu-id="665b0-174">Therefore, `Some` needs to have a variable for the value associated with the `Some` case, but `None` must appear by itself.</span></span> <span data-ttu-id="665b0-175">在下列程式碼中，會將變數 `var1` 指定為符合大小寫所取得的值 `Some` 。</span><span class="sxs-lookup"><span data-stu-id="665b0-175">In the following code, the variable `var1` is given the value that is obtained by matching to the `Some` case.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4803.fs)]

<span data-ttu-id="665b0-176">在下列範例中，差異聯 `PersonName` 集包含混合的字串和字元，表示可能的名稱形式。</span><span class="sxs-lookup"><span data-stu-id="665b0-176">In the following example, the `PersonName` discriminated union contains a mixture of strings and characters that represent possible forms of names.</span></span> <span data-ttu-id="665b0-177">差異聯集的案例為 `FirstOnly` 、 `LastOnly` 和 `FirstLast` 。</span><span class="sxs-lookup"><span data-stu-id="665b0-177">The cases of the discriminated union are `FirstOnly`, `LastOnly`, and `FirstLast`.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4804.fs)]

<span data-ttu-id="665b0-178">針對具有命名欄位的差異聯集，您可以使用等號 (=) 來將命名欄位的值解壓縮。</span><span class="sxs-lookup"><span data-stu-id="665b0-178">For discriminated unions that have named fields, you use the equals sign (=) to extract the value of a named field.</span></span> <span data-ttu-id="665b0-179">例如，請考慮使用類似如下的宣告的差異聯集。</span><span class="sxs-lookup"><span data-stu-id="665b0-179">For example, consider a discriminated union with a declaration like the following.</span></span>

```fsharp
type Shape =
    | Rectangle of height : float * width : float
    | Circle of radius : float
```

<span data-ttu-id="665b0-180">您可以使用模式比對運算式中的命名欄位，如下所示。</span><span class="sxs-lookup"><span data-stu-id="665b0-180">You can use the named fields in a pattern matching expression as follows.</span></span>

```fsharp
let matchShape shape =
    match shape with
    | Rectangle(height = h) -> printfn "Rectangle with length %f" h
    | Circle(r) -> printfn "Circle with radius %f" r
```

<span data-ttu-id="665b0-181">使用命名欄位是選擇性的，因此在上述範例中， `Circle(r)` 和都 `Circle(radius = r)` 有相同的效果。</span><span class="sxs-lookup"><span data-stu-id="665b0-181">The use of the named field is optional, so in the previous example, both `Circle(r)` and `Circle(radius = r)` have the same effect.</span></span>

<span data-ttu-id="665b0-182">當您指定多個欄位時，請使用分號 (; ) 作為分隔符號。</span><span class="sxs-lookup"><span data-stu-id="665b0-182">When you specify multiple fields, use the semicolon (;) as a separator.</span></span>

```fsharp
match shape with
| Rectangle(height = h; width = w) -> printfn "Rectangle with height %f and width %f" h w
| _ -> ()
```

<span data-ttu-id="665b0-183">現用模式可讓您定義更複雜的自訂模式比對。</span><span class="sxs-lookup"><span data-stu-id="665b0-183">Active patterns enable you to define more complex custom pattern matching.</span></span> <span data-ttu-id="665b0-184">如需使用中模式的詳細資訊，請參閱使用中的 [模式](active-patterns.md)。</span><span class="sxs-lookup"><span data-stu-id="665b0-184">For more information about active patterns, see [Active Patterns](active-patterns.md).</span></span>

<span data-ttu-id="665b0-185">在例外狀況處理常式內容中的模式比對中，會使用識別碼為例外狀況的情況。</span><span class="sxs-lookup"><span data-stu-id="665b0-185">The case in which the identifier is an exception is used in pattern matching in the context of exception handlers.</span></span> <span data-ttu-id="665b0-186">如需例外狀況處理中的模式比對的詳細資訊，請參閱 [例外狀況： `try...with` 運算式](./exception-handling/the-try-with-expression.md)。</span><span class="sxs-lookup"><span data-stu-id="665b0-186">For information about pattern matching in exception handling, see [Exceptions: The `try...with` Expression](./exception-handling/the-try-with-expression.md).</span></span>

## <a name="variable-patterns"></a><span data-ttu-id="665b0-187">變數模式</span><span class="sxs-lookup"><span data-stu-id="665b0-187">Variable Patterns</span></span>

<span data-ttu-id="665b0-188">變數模式會將符合的值指派給變數名稱，然後在符號右邊的執行運算式中使用 `->` 。</span><span class="sxs-lookup"><span data-stu-id="665b0-188">The variable pattern assigns the value being matched to a variable name, which is then available for use in the execution expression to the right of the `->` symbol.</span></span> <span data-ttu-id="665b0-189">變數模式只會比對任何輸入，但變數模式通常會出現在其他模式內，因此可讓您將更複雜的結構（例如元組和陣列）分解為變數。</span><span class="sxs-lookup"><span data-stu-id="665b0-189">A variable pattern alone matches any input, but variable patterns often appear within other patterns, therefore enabling more complex structures such as tuples and arrays to be decomposed into variables.</span></span>

<span data-ttu-id="665b0-190">下列範例示範在元組模式內的變數模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-190">The following example demonstrates a variable pattern within a tuple pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4805.fs)]

## <a name="as-pattern"></a><span data-ttu-id="665b0-191">as 模式</span><span class="sxs-lookup"><span data-stu-id="665b0-191">as Pattern</span></span>

<span data-ttu-id="665b0-192">`as`模式是一種已 `as` 附加子句的模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-192">The `as` pattern is a pattern that has an `as` clause appended to it.</span></span> <span data-ttu-id="665b0-193">子句會將 `as` 相符的值系結至運算式的執行運算式中可使用的名稱 `match` ，或者，如果在系結中使用此模式，則會將 `let` 名稱加入至區域範圍的系結。</span><span class="sxs-lookup"><span data-stu-id="665b0-193">The `as` clause binds the matched value to a name that can be used in the execution expression of a `match` expression, or, in the case where this pattern is used in a `let` binding, the name is added as a binding to the local scope.</span></span>

<span data-ttu-id="665b0-194">下列範例會使用 `as` 模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-194">The following example uses an `as` pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4806.fs)]

## <a name="or-pattern"></a><span data-ttu-id="665b0-195">或模式</span><span class="sxs-lookup"><span data-stu-id="665b0-195">OR Pattern</span></span>

<span data-ttu-id="665b0-196">當輸入資料可以比對多個模式，而您想要執行與結果相同的程式碼時，就會使用或模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-196">The OR pattern is used when input data can match multiple patterns, and you want to execute the same code as a result.</span></span> <span data-ttu-id="665b0-197">或模式兩側的類型都必須相容。</span><span class="sxs-lookup"><span data-stu-id="665b0-197">The types of both sides of the OR pattern must be compatible.</span></span>

<span data-ttu-id="665b0-198">下列範例示範或模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-198">The following example demonstrates the OR pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4807.fs)]

## <a name="and-pattern"></a><span data-ttu-id="665b0-199">AND 模式</span><span class="sxs-lookup"><span data-stu-id="665b0-199">AND Pattern</span></span>

<span data-ttu-id="665b0-200">和模式要求輸入必須符合兩個模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-200">The AND pattern requires that the input match two patterns.</span></span> <span data-ttu-id="665b0-201">和模式兩邊的類型都必須相容。</span><span class="sxs-lookup"><span data-stu-id="665b0-201">The types of both sides of the AND pattern must be compatible.</span></span>

<span data-ttu-id="665b0-202">下列範例類似于 `detectZeroTuple` 本主題稍後的「元組模式」一節中所示，但在這裡， `var1` 和 `var2` 都是使用和模式來取得值。</span><span class="sxs-lookup"><span data-stu-id="665b0-202">The following example is like `detectZeroTuple` shown in the Tuple Pattern section later in this topic, but here both `var1` and `var2` are obtained as values by using the AND pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4808.fs)]

## <a name="cons-pattern"></a><span data-ttu-id="665b0-203">缺點模式</span><span class="sxs-lookup"><span data-stu-id="665b0-203">Cons Pattern</span></span>

<span data-ttu-id="665b0-204">缺點模式可用來將清單分解為第一個元素、 *head*，以及包含其餘元素（ *結尾*）的清單。</span><span class="sxs-lookup"><span data-stu-id="665b0-204">The cons pattern is used to decompose a list into the first element, the *head*, and a list that contains the remaining elements, the *tail*.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4809.fs)]

## <a name="list-pattern"></a><span data-ttu-id="665b0-205">清單模式</span><span class="sxs-lookup"><span data-stu-id="665b0-205">List Pattern</span></span>

<span data-ttu-id="665b0-206">清單模式可將清單分解成多個元素。</span><span class="sxs-lookup"><span data-stu-id="665b0-206">The list pattern enables lists to be decomposed into a number of elements.</span></span> <span data-ttu-id="665b0-207">清單模式本身只能比對特定元素數目的清單。</span><span class="sxs-lookup"><span data-stu-id="665b0-207">The list pattern itself can match only lists of a specific number of elements.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4810.fs)]

## <a name="array-pattern"></a><span data-ttu-id="665b0-208">陣列模式</span><span class="sxs-lookup"><span data-stu-id="665b0-208">Array Pattern</span></span>

<span data-ttu-id="665b0-209">陣列模式與清單模式類似，可用於分解特定長度的陣列。</span><span class="sxs-lookup"><span data-stu-id="665b0-209">The array pattern resembles the list pattern and can be used to decompose arrays of a specific length.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4811.fs)]

## <a name="parenthesized-pattern"></a><span data-ttu-id="665b0-210">括弧模式</span><span class="sxs-lookup"><span data-stu-id="665b0-210">Parenthesized Pattern</span></span>

<span data-ttu-id="665b0-211">括弧可在模式周圍分組，以達成所需的關聯性。</span><span class="sxs-lookup"><span data-stu-id="665b0-211">Parentheses can be grouped around patterns to achieve the desired associativity.</span></span> <span data-ttu-id="665b0-212">在下列範例中，括弧是用來控制和模式之間的關聯性，以及缺點模式之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="665b0-212">In the following example, parentheses are used to control associativity between an AND pattern and a cons pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4812.fs)]

## <a name="tuple-pattern"></a><span data-ttu-id="665b0-213">元組模式</span><span class="sxs-lookup"><span data-stu-id="665b0-213">Tuple Pattern</span></span>

<span data-ttu-id="665b0-214">元組模式會比對元組形式的輸入，並使用元組中的每個位置的模式比對變數，將元組分解為其組成元素。</span><span class="sxs-lookup"><span data-stu-id="665b0-214">The tuple pattern matches input in tuple form and enables the tuple to be decomposed into its constituent elements by using pattern matching variables for each position in the tuple.</span></span>

<span data-ttu-id="665b0-215">下列範例將示範元組模式，也會使用常值模式、變數模式和萬用字元模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-215">The following example demonstrates the tuple pattern and also uses literal patterns, variable patterns, and the wildcard pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4813.fs)]

## <a name="record-pattern"></a><span data-ttu-id="665b0-216">記錄模式</span><span class="sxs-lookup"><span data-stu-id="665b0-216">Record Pattern</span></span>

<span data-ttu-id="665b0-217">記錄模式用於分解記錄，以將欄位值解壓縮。</span><span class="sxs-lookup"><span data-stu-id="665b0-217">The record pattern is used to decompose records to extract the values of fields.</span></span> <span data-ttu-id="665b0-218">模式不需要參考記錄的所有欄位;任何省略的欄位都不會參與比對，也不會解壓縮。</span><span class="sxs-lookup"><span data-stu-id="665b0-218">The pattern does not have to reference all fields of the record; any omitted fields just do not participate in matching and are not extracted.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4814.fs)]

## <a name="wildcard-pattern"></a><span data-ttu-id="665b0-219">萬用字元模式</span><span class="sxs-lookup"><span data-stu-id="665b0-219">Wildcard Pattern</span></span>

<span data-ttu-id="665b0-220">萬用字元模式是以底線 () 字元表示，並比對 `_` 任何輸入（如同變數模式），但會捨棄輸入而不是指派給變數。</span><span class="sxs-lookup"><span data-stu-id="665b0-220">The wildcard pattern is represented by the underscore (`_`) character and matches any input, just like the variable pattern, except that the input is discarded instead of assigned to a variable.</span></span> <span data-ttu-id="665b0-221">萬用字元模式通常用於其他模式中，作為符號右邊運算式中不需要的值預留位置 `->` 。</span><span class="sxs-lookup"><span data-stu-id="665b0-221">The wildcard pattern is often used within other patterns as a placeholder for values that are not needed in the expression to the right of the `->` symbol.</span></span> <span data-ttu-id="665b0-222">萬用字元模式也經常用於模式清單的結尾，以符合任何不相符的輸入。</span><span class="sxs-lookup"><span data-stu-id="665b0-222">The wildcard pattern is also frequently used at the end of a list of patterns to match any unmatched input.</span></span> <span data-ttu-id="665b0-223">本主題的許多程式碼範例會示範萬用字元模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-223">The wildcard pattern is demonstrated in many code examples in this topic.</span></span> <span data-ttu-id="665b0-224">請參閱上述程式碼中的一個範例。</span><span class="sxs-lookup"><span data-stu-id="665b0-224">See the preceding code for one example.</span></span>

## <a name="patterns-that-have-type-annotations"></a><span data-ttu-id="665b0-225">具有類型注釋的模式</span><span class="sxs-lookup"><span data-stu-id="665b0-225">Patterns That Have Type Annotations</span></span>

<span data-ttu-id="665b0-226">模式可以有類型注釋。</span><span class="sxs-lookup"><span data-stu-id="665b0-226">Patterns can have type annotations.</span></span> <span data-ttu-id="665b0-227">這些行為類似其他類型注釋和參考參考，例如其他類型注釋。</span><span class="sxs-lookup"><span data-stu-id="665b0-227">These behave like other type annotations and guide inference like other type annotations.</span></span> <span data-ttu-id="665b0-228">模式中的類型注釋周圍需要括弧。</span><span class="sxs-lookup"><span data-stu-id="665b0-228">Parentheses are required around type annotations in patterns.</span></span> <span data-ttu-id="665b0-229">下列程式碼顯示具有類型注釋的模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-229">The following code shows a pattern that has a type annotation.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4815.fs)]

## <a name="type-test-pattern"></a><span data-ttu-id="665b0-230">類型測試模式</span><span class="sxs-lookup"><span data-stu-id="665b0-230">Type Test Pattern</span></span>

<span data-ttu-id="665b0-231">型別測試模式是用來比對輸入與型別。</span><span class="sxs-lookup"><span data-stu-id="665b0-231">The type test pattern is used to match the input against a type.</span></span> <span data-ttu-id="665b0-232">如果輸入類型與 (的相符項或) 類型中所指定之類型的衍生型別相符，則比對成功。</span><span class="sxs-lookup"><span data-stu-id="665b0-232">If the input type is a match to (or a derived type of) the type specified in the pattern, the match succeeds.</span></span>

<span data-ttu-id="665b0-233">下列範例示範型別測試模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-233">The following example demonstrates the type test pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4816.fs)]

<span data-ttu-id="665b0-234">如果您只是要檢查識別碼是否屬於特定的衍生類型，則不需要模式的 `as identifier` 部分，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="665b0-234">If you're only checking if an identifier is of a particular derived type, you don't need the `as identifier` part of the pattern, as shown in the following example:</span></span>

```fsharp
type A() = class end
type B() = inherit A()
type C() = inherit A()

let m (a: A) =
    match a with
    | :? B -> printfn "It's a B"
    | :? C -> printfn "It's a C"
    | _ -> ()
```

## <a name="null-pattern"></a><span data-ttu-id="665b0-235">Null 模式</span><span class="sxs-lookup"><span data-stu-id="665b0-235">Null Pattern</span></span>

<span data-ttu-id="665b0-236">Null 模式符合當您使用允許 null 值的類型時，可能出現的 null 值。</span><span class="sxs-lookup"><span data-stu-id="665b0-236">The null pattern matches the null value that can appear when you are working with types that allow a null value.</span></span> <span data-ttu-id="665b0-237">當與 .NET Framework 程式碼交互操作時，經常會使用 Null 模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-237">Null patterns are frequently used when interoperating with .NET Framework code.</span></span> <span data-ttu-id="665b0-238">例如，.NET API 的傳回值可能是運算式的輸入 `match` 。</span><span class="sxs-lookup"><span data-stu-id="665b0-238">For example, the return value of a .NET API might be the input to a `match` expression.</span></span> <span data-ttu-id="665b0-239">您可以根據傳回值是否為 null，以及傳回值的其他特性來控制程式流程。</span><span class="sxs-lookup"><span data-stu-id="665b0-239">You can control program flow based on whether the return value is null, and also on other characteristics of the returned value.</span></span> <span data-ttu-id="665b0-240">您可以使用 null 模式來防止 null 值傳播至程式的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="665b0-240">You can use the null pattern to prevent null values from propagating to the rest of your program.</span></span>

<span data-ttu-id="665b0-241">下列範例會使用 null 模式和變數模式。</span><span class="sxs-lookup"><span data-stu-id="665b0-241">The following example uses the null pattern and the variable pattern.</span></span>

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet4817.fs)]

## <a name="see-also"></a><span data-ttu-id="665b0-242">另請參閱</span><span class="sxs-lookup"><span data-stu-id="665b0-242">See also</span></span>

- [<span data-ttu-id="665b0-243">比對運算式</span><span class="sxs-lookup"><span data-stu-id="665b0-243">Match Expressions</span></span>](match-expressions.md)
- [<span data-ttu-id="665b0-244">現用模式</span><span class="sxs-lookup"><span data-stu-id="665b0-244">Active Patterns</span></span>](active-patterns.md)
- [<span data-ttu-id="665b0-245">F # 語言參考</span><span class="sxs-lookup"><span data-stu-id="665b0-245">F# Language Reference</span></span>](index.md)
