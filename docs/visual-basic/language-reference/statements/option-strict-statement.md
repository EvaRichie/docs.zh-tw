---
title: Long
ms.date: 07/20/2015
f1_keywords:
- vb.Strict
- vb.OptionStrict
helpviewer_keywords:
- Strict keyword [Visual Basic]
- Option Strict statement [Visual Basic]
- conversions [Visual Basic], implicit
- late binding [Visual Basic]
- implicit conversions [Visual Basic]
ms.assetid: 5883e0c1-a920-4274-8e46-b0ff047eaee5
ms.openlocfilehash: 9c86ae6be86591445dde3cc4e7bdd38aa4a7f0fa
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404339"
---
# <a name="option-strict-statement"></a><span data-ttu-id="64e61-102">Long</span><span class="sxs-lookup"><span data-stu-id="64e61-102">Option Strict Statement</span></span>
<span data-ttu-id="64e61-103">將隱含資料類型轉換限制為僅限擴輾轉換、不允許晚期繫結，而且不允許產生類型的隱含 `Object` 類型。</span><span class="sxs-lookup"><span data-stu-id="64e61-103">Restricts implicit data type conversions to only widening conversions, disallows late binding, and disallows implicit typing that results in an `Object` type.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="64e61-104">語法</span><span class="sxs-lookup"><span data-stu-id="64e61-104">Syntax</span></span>  
  
```vb  
Option Strict { On | Off }  
```  
  
## <a name="parts"></a><span data-ttu-id="64e61-105">組件</span><span class="sxs-lookup"><span data-stu-id="64e61-105">Parts</span></span>  
  
|<span data-ttu-id="64e61-106">詞彙</span><span class="sxs-lookup"><span data-stu-id="64e61-106">Term</span></span>|<span data-ttu-id="64e61-107">定義</span><span class="sxs-lookup"><span data-stu-id="64e61-107">Definition</span></span>|  
|---|---|  
|`On`|<span data-ttu-id="64e61-108">選擇性。</span><span class="sxs-lookup"><span data-stu-id="64e61-108">Optional.</span></span> <span data-ttu-id="64e61-109">啟用 `Option Strict` 檢查。</span><span class="sxs-lookup"><span data-stu-id="64e61-109">Enables `Option Strict` checking.</span></span>|  
|`Off`|<span data-ttu-id="64e61-110">選擇性。</span><span class="sxs-lookup"><span data-stu-id="64e61-110">Optional.</span></span> <span data-ttu-id="64e61-111">停用 `Option Strict` 檢查。</span><span class="sxs-lookup"><span data-stu-id="64e61-111">Disables `Option Strict` checking.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="64e61-112">備註</span><span class="sxs-lookup"><span data-stu-id="64e61-112">Remarks</span></span>  
 <span data-ttu-id="64e61-113">當 `Option Strict On` 檔案 `Option Strict` 中出現或時，下列情況會導致編譯時期錯誤：</span><span class="sxs-lookup"><span data-stu-id="64e61-113">When `Option Strict On` or `Option Strict` appears in a file, the following conditions cause a compile-time error:</span></span>  
  
- <span data-ttu-id="64e61-114">隱含縮小轉換</span><span class="sxs-lookup"><span data-stu-id="64e61-114">Implicit narrowing conversions</span></span>  
  
- <span data-ttu-id="64e61-115">晚期繫結</span><span class="sxs-lookup"><span data-stu-id="64e61-115">Late binding</span></span>  
  
- <span data-ttu-id="64e61-116">導致 `Object` 類型的隱含類型化</span><span class="sxs-lookup"><span data-stu-id="64e61-116">Implicit typing that results in an `Object` type</span></span>  
  
> [!NOTE]
> <span data-ttu-id="64e61-117">在 [[編譯] 頁面上，[專案設計](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)工具] （[Visual Basic]）可設定的警告設定中，有三個設定會對應到造成編譯時期錯誤的三個條件。</span><span class="sxs-lookup"><span data-stu-id="64e61-117">In the warning configurations that you can set on the [Compile Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic), there are three settings that correspond to the three conditions that cause a compile-time error.</span></span> <span data-ttu-id="64e61-118">如需有關如何使用這些設定的詳細資訊，請參閱本主題稍後[的在 IDE 中設定警告設定](option-strict-statement.md#conditions)。</span><span class="sxs-lookup"><span data-stu-id="64e61-118">For information about how to use these settings, see [To set warning configurations in the IDE](option-strict-statement.md#conditions) later in this topic.</span></span>  
  
 <span data-ttu-id="64e61-119">語句會關閉 `Option Strict Off` 所有三個條件的錯誤和警告檢查，即使相關聯的 IDE 設定指定要開啟這些錯誤或警告。</span><span class="sxs-lookup"><span data-stu-id="64e61-119">The `Option Strict Off` statement turns off error and warning checking for all three conditions, even if the associated IDE settings specify to turn on these errors or warnings.</span></span> <span data-ttu-id="64e61-120">`Option Strict On`語句會針對這三個條件開啟錯誤和警告檢查，即使相關聯的 IDE 設定指定要關閉這些錯誤或警告。</span><span class="sxs-lookup"><span data-stu-id="64e61-120">The `Option Strict On` statement turns on error and warning checking for all three conditions, even if the associated IDE settings specify to turn off these errors or warnings.</span></span>  
  
 <span data-ttu-id="64e61-121">如果使用的話， `Option Strict` 語句必須出現在檔案中的任何其他程式碼語句之前。</span><span class="sxs-lookup"><span data-stu-id="64e61-121">If used, the `Option Strict` statement must appear before any other code statements in a file.</span></span>  
  
 <span data-ttu-id="64e61-122">當您將設定 `Option Strict` 為時 `On` ，Visual Basic 會檢查是否已針對所有程式設計項目指定資料類型。</span><span class="sxs-lookup"><span data-stu-id="64e61-122">When you set `Option Strict` to `On`, Visual Basic checks that data types are specified for all programming elements.</span></span> <span data-ttu-id="64e61-123">您可以明確指定資料類型，或使用區欄位型別推斷來指定。</span><span class="sxs-lookup"><span data-stu-id="64e61-123">Data types can be specified explicitly, or specified by using local type inference.</span></span> <span data-ttu-id="64e61-124">建議您為所有的程式設計項目指定資料類型，原因如下：</span><span class="sxs-lookup"><span data-stu-id="64e61-124">Specifying data types for all your programming elements is recommended, for the following reasons:</span></span>  
  
- <span data-ttu-id="64e61-125">它會針對您的變數和參數啟用 IntelliSense 支援。</span><span class="sxs-lookup"><span data-stu-id="64e61-125">It enables IntelliSense support for your variables and parameters.</span></span> <span data-ttu-id="64e61-126">這可讓您在輸入程式碼時看到其屬性和其他成員。</span><span class="sxs-lookup"><span data-stu-id="64e61-126">This enables you to see their properties and other members as you type code.</span></span>  
  
- <span data-ttu-id="64e61-127">它可讓編譯器執行類型檢查。</span><span class="sxs-lookup"><span data-stu-id="64e61-127">It enables the compiler to perform type checking.</span></span> <span data-ttu-id="64e61-128">類型檢查可協助您尋找在執行時間因類型轉換錯誤而失敗的語句。</span><span class="sxs-lookup"><span data-stu-id="64e61-128">Type checking helps you find statements that can fail at run time because of type conversion errors.</span></span> <span data-ttu-id="64e61-129">它也會識別不支援這些方法之物件上方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="64e61-129">It also identifies calls to methods on objects that do not support those methods.</span></span>  
  
- <span data-ttu-id="64e61-130">它會加速程式碼的執行。</span><span class="sxs-lookup"><span data-stu-id="64e61-130">It speeds up the execution of code.</span></span> <span data-ttu-id="64e61-131">其中一個原因是，如果您沒有指定程式設計項目的資料類型，Visual Basic 編譯器會為它指派 `Object` 類型。</span><span class="sxs-lookup"><span data-stu-id="64e61-131">One reason for this is that if you do not specify a data type for a programming element, the Visual Basic compiler assigns it the `Object` type.</span></span> <span data-ttu-id="64e61-132">已編譯的程式碼可能必須在 `Object` 和其他資料類型之間來回轉換，以降低效能。</span><span class="sxs-lookup"><span data-stu-id="64e61-132">Compiled code might have to convert back and forth between `Object` and other data types, which reduces performance.</span></span>  
  
## <a name="implicit-narrowing-conversion-errors"></a><span data-ttu-id="64e61-133">隱含縮小轉換錯誤</span><span class="sxs-lookup"><span data-stu-id="64e61-133">Implicit Narrowing Conversion Errors</span></span>  
 <span data-ttu-id="64e61-134">隱含資料類型轉換是縮小轉換時，會發生隱含縮小轉換錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e61-134">Implicit narrowing conversion errors occur when there is an implicit data type conversion that is a narrowing conversion.</span></span>  
  
 <span data-ttu-id="64e61-135">Visual Basic 可以將許多資料類型轉換成其他資料類型。</span><span class="sxs-lookup"><span data-stu-id="64e61-135">Visual Basic can convert many data types to other data types.</span></span> <span data-ttu-id="64e61-136">當某個資料類型的值轉換成具有較少精確度或較小容量的資料類型時，可能會發生資料遺失。</span><span class="sxs-lookup"><span data-stu-id="64e61-136">Data loss can occur when the value of one data type is converted to a data type that has less precision or a smaller capacity.</span></span> <span data-ttu-id="64e61-137">如果這類縮小轉換失敗，就會發生執行階段錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e61-137">A run-time error occurs if such a narrowing conversion fails.</span></span> <span data-ttu-id="64e61-138">`Option Strict`確保這些縮小轉換的編譯時間通知，讓您可以避免它們。</span><span class="sxs-lookup"><span data-stu-id="64e61-138">`Option Strict` ensures compile-time notification of these narrowing conversions so that you can avoid them.</span></span> <span data-ttu-id="64e61-139">如需詳細資訊，請參閱[隱含和明確轉換](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)和[擴展和縮小轉換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。</span><span class="sxs-lookup"><span data-stu-id="64e61-139">For more information, see [Implicit and Explicit Conversions](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md) and [Widening and Narrowing Conversions](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md).</span></span>  
  
 <span data-ttu-id="64e61-140">可能造成錯誤的轉換包括運算式中發生的隱含轉換。</span><span class="sxs-lookup"><span data-stu-id="64e61-140">Conversions that can cause errors include implicit conversions that occur in expressions.</span></span> <span data-ttu-id="64e61-141">如需詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="64e61-141">For more information, see the following topics:</span></span>  
  
- [<span data-ttu-id="64e61-142">+ 運算子</span><span class="sxs-lookup"><span data-stu-id="64e61-142">+ Operator</span></span>](../operators/addition-operator.md)  
  
- [<span data-ttu-id="64e61-143">+ = 運算子</span><span class="sxs-lookup"><span data-stu-id="64e61-143">+= Operator</span></span>](../operators/addition-assignment-operator.md)  
  
- [<span data-ttu-id="64e61-144">\ 運算子（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="64e61-144">\ Operator (Visual Basic)</span></span>](../operators/integer-division-operator.md)  
  
- [<span data-ttu-id="64e61-145">/= 運算子（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="64e61-145">/= Operator (Visual Basic)</span></span>](../operators/floating-point-division-assignment-operator.md)  
  
- [<span data-ttu-id="64e61-146">Char 資料類型</span><span class="sxs-lookup"><span data-stu-id="64e61-146">Char Data Type</span></span>](../data-types/char-data-type.md)  
  
 <span data-ttu-id="64e61-147">當您使用[& 運算子](../operators/concatenation-operator.md)來串連字號串時，會將字串的所有轉換視為擴展。</span><span class="sxs-lookup"><span data-stu-id="64e61-147">When you concatenate strings by using the [& Operator](../operators/concatenation-operator.md), all conversions to the strings are considered to be widening.</span></span> <span data-ttu-id="64e61-148">因此，即使是 on，這些轉換也不會產生隱含的縮小轉換錯誤 `Option Strict` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-148">So these conversions do not generate an implicit narrowing conversion error, even if `Option Strict` is on.</span></span>  
  
 <span data-ttu-id="64e61-149">當您呼叫的方法具有與對應參數不同的資料類型引數時，如果為 on，則縮小轉換會導致編譯時期錯誤 `Option Strict` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-149">When you call a method that has an argument that has a data type different from the corresponding parameter, a narrowing conversion causes a compile-time error if `Option Strict` is on.</span></span> <span data-ttu-id="64e61-150">您可以使用擴輾轉換或明確轉換來避免編譯時期錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e61-150">You can avoid the compile-time error by using a widening conversion or an explicit conversion.</span></span>  
  
 <span data-ttu-id="64e61-151">在編譯時間會抑制隱含縮小轉換錯誤，以從集合中的元素轉換 `For Each…Next` 為迴圈控制變數。</span><span class="sxs-lookup"><span data-stu-id="64e61-151">Implicit narrowing conversion errors are suppressed at compile-time for conversions from the elements in a `For Each…Next` collection to the loop control variable.</span></span> <span data-ttu-id="64e61-152">即使是 on，也會發生這種情況 `Option Strict` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-152">This occurs even if `Option Strict` is on.</span></span> <span data-ttu-id="64e61-153">如需詳細資訊，請參閱[For Each ... 中的「縮小轉換」一節。下一個語句](for-each-next-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="64e61-153">For more information, see the "Narrowing Conversions" section in [For Each...Next Statement](for-each-next-statement.md).</span></span>  
  
## <a name="late-binding-errors"></a><span data-ttu-id="64e61-154">晚期繫結錯誤</span><span class="sxs-lookup"><span data-stu-id="64e61-154">Late Binding Errors</span></span>  
 <span data-ttu-id="64e61-155">當物件指派給宣告為 `Object` 類型之變數的屬性或方法時，該物件即為「晚期繫結」。</span><span class="sxs-lookup"><span data-stu-id="64e61-155">An object is late bound when it is assigned to a property or method of a variable that is declared to be of type `Object`.</span></span> <span data-ttu-id="64e61-156">如需詳細資訊，請參閱[早期和晚期繫結](../../programming-guide/language-features/early-late-binding/index.md)。</span><span class="sxs-lookup"><span data-stu-id="64e61-156">For more information, see [Early and Late Binding](../../programming-guide/language-features/early-late-binding/index.md).</span></span>  
  
## <a name="implicit-object-type-errors"></a><span data-ttu-id="64e61-157">隱含物件類型錯誤</span><span class="sxs-lookup"><span data-stu-id="64e61-157">Implicit Object Type Errors</span></span>  
 <span data-ttu-id="64e61-158">無法推斷宣告變數的適當類型時，會發生隱含物件類型錯誤，因此推斷類型為 `Object`。</span><span class="sxs-lookup"><span data-stu-id="64e61-158">Implicit object type errors occur when an appropriate type cannot be inferred for a declared variable, so a type of `Object` is inferred.</span></span> <span data-ttu-id="64e61-159">這主要是發生在您使用 `Dim` 陳述式宣告變數而未使用 `As` 子句，並且 `Option Infer` 已設為關閉的時候。</span><span class="sxs-lookup"><span data-stu-id="64e61-159">This primarily occurs when you use a `Dim` statement to declare a variable without using an `As` clause, and `Option Infer` is off.</span></span> <span data-ttu-id="64e61-160">如需詳細資訊，請參閱[Option 推斷語句](option-infer-statement.md)和[Visual Basic 語言規格](../../reference/language-specification/index.md)。</span><span class="sxs-lookup"><span data-stu-id="64e61-160">For more information, see [Option Infer Statement](option-infer-statement.md) and the [Visual Basic Language Specification](../../reference/language-specification/index.md).</span></span>  
  
 <span data-ttu-id="64e61-161">針對方法參數， `As` 如果為 off，子句是選擇性的 `Option Strict` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-161">For method parameters, the `As` clause is optional if `Option Strict` is off.</span></span> <span data-ttu-id="64e61-162">不過，如果有任何一個參數使用 `As` 子句，則它們都必須使用它。</span><span class="sxs-lookup"><span data-stu-id="64e61-162">However, if any one parameter uses an `As` clause, they all must use it.</span></span> <span data-ttu-id="64e61-163">如果 `Option Strict` 為 on，則 `As` 每個參數定義都需要子句。</span><span class="sxs-lookup"><span data-stu-id="64e61-163">If `Option Strict` is on, the `As` clause is required for every parameter definition.</span></span>  
  
 <span data-ttu-id="64e61-164">如果您在不使用子句的情況下宣告變數， `As` 並將它設定為 `Nothing` ，則變數的類型為 `Object` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-164">If you declare a variable without using an `As` clause and set it to `Nothing`, the variable has a type of `Object`.</span></span> <span data-ttu-id="64e61-165">當 `Option Strict` 是 on，且為 on 時，在此情況下不會發生編譯時期錯誤 `Option Infer` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-165">No compile-time error occurs in this case when `Option Strict` is on and `Option Infer` is on.</span></span> <span data-ttu-id="64e61-166">其中一個範例是 `Dim something = Nothing` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-166">An example of this is `Dim something = Nothing`.</span></span>  
  
### <a name="default-data-types-and-values"></a><span data-ttu-id="64e61-167">預設資料類型和值</span><span class="sxs-lookup"><span data-stu-id="64e61-167">Default Data Types and Values</span></span>  
 <span data-ttu-id="64e61-168">下表描述在[Dim 語句](dim-statement.md)中指定資料類型和初始化運算式的各種組合結果。</span><span class="sxs-lookup"><span data-stu-id="64e61-168">The following table describes the results of various combinations of specifying the data type and initializer in a [Dim Statement](dim-statement.md).</span></span>  
  
|<span data-ttu-id="64e61-169">指定了資料類型？</span><span class="sxs-lookup"><span data-stu-id="64e61-169">Data type specified?</span></span>|<span data-ttu-id="64e61-170">指定了初始設定式？</span><span class="sxs-lookup"><span data-stu-id="64e61-170">Initializer specified?</span></span>|<span data-ttu-id="64e61-171">範例</span><span class="sxs-lookup"><span data-stu-id="64e61-171">Example</span></span>|<span data-ttu-id="64e61-172">結果</span><span class="sxs-lookup"><span data-stu-id="64e61-172">Result</span></span>|  
|---|---|---|---|  
|<span data-ttu-id="64e61-173">No</span><span class="sxs-lookup"><span data-stu-id="64e61-173">No</span></span>|<span data-ttu-id="64e61-174">否</span><span class="sxs-lookup"><span data-stu-id="64e61-174">No</span></span>|`Dim qty`|<span data-ttu-id="64e61-175">如果 `Option Strict` 已關閉 (預設值)，此變數會設定為 `Nothing`。</span><span class="sxs-lookup"><span data-stu-id="64e61-175">If `Option Strict` is off (the default), the variable is set to `Nothing`.</span></span><br /><br /> <span data-ttu-id="64e61-176">如果 `Option Strict` 已開啟，就會發生編譯時間錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e61-176">If `Option Strict` is on, a compile-time error occurs.</span></span>|  
|<span data-ttu-id="64e61-177">否</span><span class="sxs-lookup"><span data-stu-id="64e61-177">No</span></span>|<span data-ttu-id="64e61-178">是</span><span class="sxs-lookup"><span data-stu-id="64e61-178">Yes</span></span>|`Dim qty = 5`|<span data-ttu-id="64e61-179">如果 `Option Infer` 已開啟 (預設值)，此變數會採用初始設定式的資料類型。</span><span class="sxs-lookup"><span data-stu-id="64e61-179">If `Option Infer` is on (the default), the variable takes the data type of the initializer.</span></span> <span data-ttu-id="64e61-180">請參閱[區欄位型別推斷](../../programming-guide/language-features/variables/local-type-inference.md)。</span><span class="sxs-lookup"><span data-stu-id="64e61-180">See [Local Type Inference](../../programming-guide/language-features/variables/local-type-inference.md).</span></span><br /><br /> <span data-ttu-id="64e61-181">如果 `Option Infer` 已關閉，且 `Option Strict` 也已關閉，此變數會採用 `Object` 的資料類型。</span><span class="sxs-lookup"><span data-stu-id="64e61-181">If `Option Infer` is off and `Option Strict` is off, the variable takes the data type of `Object`.</span></span><br /><br /> <span data-ttu-id="64e61-182">如果 `Option Infer` 已關閉，但是 `Option Strict` 已開啟，就會發生編譯時間錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e61-182">If `Option Infer` is off and `Option Strict` is on, a compile-time error occurs.</span></span>|  
|<span data-ttu-id="64e61-183">是</span><span class="sxs-lookup"><span data-stu-id="64e61-183">Yes</span></span>|<span data-ttu-id="64e61-184">No</span><span class="sxs-lookup"><span data-stu-id="64e61-184">No</span></span>|`Dim qty As Integer`|<span data-ttu-id="64e61-185">變數會初始化為資料類型的預設值。</span><span class="sxs-lookup"><span data-stu-id="64e61-185">The variable is initialized to the default value for the data type.</span></span> <span data-ttu-id="64e61-186">如需詳細資訊，請參閱[Dim 語句](dim-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="64e61-186">For more information, see [Dim Statement](dim-statement.md).</span></span>|  
|<span data-ttu-id="64e61-187">Yes</span><span class="sxs-lookup"><span data-stu-id="64e61-187">Yes</span></span>|<span data-ttu-id="64e61-188">Yes</span><span class="sxs-lookup"><span data-stu-id="64e61-188">Yes</span></span>|`Dim qty  As Integer = 5`|<span data-ttu-id="64e61-189">如果初始設定式的資料類型無法轉換成指定的資料類型，就會發生編譯時期錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e61-189">If the data type of the initializer is not convertible to the specified data type, a compile-time error occurs.</span></span>|  
  
## <a name="when-an-option-strict-statement-is-not-present"></a><span data-ttu-id="64e61-190">當 Option Strict 語句不存在時</span><span class="sxs-lookup"><span data-stu-id="64e61-190">When an Option Strict Statement Is Not Present</span></span>  
 <span data-ttu-id="64e61-191">如果原始程式碼不包含 `Option Strict` 語句，則會使用 [編譯] 頁面上的 [ **Option strict** ] 設定[（[專案設計工具] （Visual Basic）](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) 。</span><span class="sxs-lookup"><span data-stu-id="64e61-191">If the source code does not contain an `Option Strict` statement, the **Option strict** setting on the [Compile Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) is used.</span></span> <span data-ttu-id="64e61-192">[**編譯] 頁面**有一些設定，可對產生錯誤的條件提供額外的控制。</span><span class="sxs-lookup"><span data-stu-id="64e61-192">The **Compile Page** has settings that provide additional control over the conditions that generate an error.</span></span>  
  
 <span data-ttu-id="64e61-193">如果您使用命令列編譯器，您可以使用[-optionstrict](../../reference/command-line-compiler/optionstrict.md)編譯器選項來指定的設定 `Option Strict` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-193">If you are using the command-line compiler, you can use the [-optionstrict](../../reference/command-line-compiler/optionstrict.md) compiler option to specify a setting for `Option Strict`.</span></span>  
  
### <a name="to-set-option-strict-in-the-ide"></a><span data-ttu-id="64e61-194">若要在 IDE 中設定 Option Strict</span><span class="sxs-lookup"><span data-stu-id="64e61-194">To set Option Strict in the IDE</span></span>  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
1. <span data-ttu-id="64e61-195">在 [**方案總管**中，選取專案。</span><span class="sxs-lookup"><span data-stu-id="64e61-195">In **Solution Explorer**, select a project.</span></span> <span data-ttu-id="64e61-196">按一下 [專案]\*\*\*\* 功能表上的 [屬性]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="64e61-196">On the **Project** menu, click **Properties**.</span></span>  
  
2. <span data-ttu-id="64e61-197">在 [**編譯**] 索引標籤上，于 [**選項 Strict** ] 方塊中設定值。</span><span class="sxs-lookup"><span data-stu-id="64e61-197">On the **Compile** tab, set the value in the **Option Strict** box.</span></span>  
  
### <a name="to-set-warning-configurations-in-the-ide"></a><a name="conditions"></a><span data-ttu-id="64e61-198">若要在 IDE 中設定警告設定</span><span class="sxs-lookup"><span data-stu-id="64e61-198">To set warning configurations in the IDE</span></span>  
 <span data-ttu-id="64e61-199">當您使用 [[編譯] 頁面時，[專案設計工具] （Visual Basic）](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) ，而不是 `Option Strict` 語句，您可以進一步控制產生錯誤的條件。</span><span class="sxs-lookup"><span data-stu-id="64e61-199">When you use the [Compile Page, Project Designer (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) instead of an `Option Strict` statement, you have additional control over the conditions that generate errors.</span></span> <span data-ttu-id="64e61-200">[**編譯] 頁面**的 [**警告**設定] 區段中，具有對應于當為 on 時造成編譯時期錯誤的三個條件 `Option Strict` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-200">The **Warning configurations** section of the **Compile Page** has settings that correspond to the three conditions that cause a compile-time error when `Option Strict` is on.</span></span> <span data-ttu-id="64e61-201">以下是這些設定：</span><span class="sxs-lookup"><span data-stu-id="64e61-201">Following are these settings:</span></span>  
  
- <span data-ttu-id="64e61-202">**隱含轉換**</span><span class="sxs-lookup"><span data-stu-id="64e61-202">**Implicit conversion**</span></span>  
  
- <span data-ttu-id="64e61-203">**晚期繫結，執行階段時呼叫可能失敗**</span><span class="sxs-lookup"><span data-stu-id="64e61-203">**Late binding; call could fail at run time**</span></span>  
  
- <span data-ttu-id="64e61-204">**隱含類型，假設是 Object**</span><span class="sxs-lookup"><span data-stu-id="64e61-204">**Implicit type; object assumed**</span></span>  
  
 <span data-ttu-id="64e61-205">當您將 [Option Strict]\*\*\*\* 設定為 [On]\*\*\*\* 時，這三個警告組態設定都會設定為 [錯誤]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="64e61-205">When you set **Option Strict** to **On**, all three of these warning configuration settings are set to **Error**.</span></span> <span data-ttu-id="64e61-206">當您將 [Option Strict]\*\*\*\* 設定為 [Off]\*\*\*\* 時，所有三個設定都會設定為 [無]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="64e61-206">When you set **Option Strict** to **Off**, all three settings are set to **None**.</span></span>  
  
 <span data-ttu-id="64e61-207">您可以將每個警告組態個別變更為 [無]\*\*\*\*、[警告]\*\*\*\* 或 [錯誤]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="64e61-207">You can individually change each warning configuration setting to **None**, **Warning**, or **Error**.</span></span> <span data-ttu-id="64e61-208">如果三個警告設定都設為 [**錯誤**]， `On` 則會出現在方塊中 `Option strict` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-208">If all three warning configuration settings are set to **Error**, `On` appears in the `Option strict` box.</span></span> <span data-ttu-id="64e61-209">如果這三個全都設定為 [**無**]，則 `Off` 會出現在此方塊中。</span><span class="sxs-lookup"><span data-stu-id="64e61-209">If all three are set to **None**, `Off` appears in this box.</span></span> <span data-ttu-id="64e61-210">若為這些設定的其他任何組合，則會出現 [(自訂)]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="64e61-210">For any other combination of these settings, **(custom)** appears.</span></span>  
  
### <a name="to-set-the-option-strict-default-setting-for-new-projects"></a><span data-ttu-id="64e61-211">設定新專案的 Option Strict 預設設定</span><span class="sxs-lookup"><span data-stu-id="64e61-211">To set the Option Strict default setting for new projects</span></span>  
 <span data-ttu-id="64e61-212">當您建立專案時，[**編譯**] 索引標籤上的 [ **option strict** ] 設定會設定為 [**選項**] 對話方塊中的 [ **option strict** ] 設定。</span><span class="sxs-lookup"><span data-stu-id="64e61-212">When you create a project, the **Option Strict** setting on the **Compile** tab is set to the **Option Strict** setting in the **Options** dialog box.</span></span>  
  
 <span data-ttu-id="64e61-213">若要 `Option Strict` 在此對話方塊中設定，請在 [**工具**] 功能表上，按一下 [**選項**]。</span><span class="sxs-lookup"><span data-stu-id="64e61-213">To set `Option Strict` in this dialog box, on the **Tools** menu, click **Options**.</span></span> <span data-ttu-id="64e61-214">在 [選項]\*\*\*\* 對話方塊中，展開 [專案和方案]\*\*\*\*，然後按一下 [VB 預設值]\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="64e61-214">In the **Options** dialog box, expand **Projects and Solutions**, and then click **VB Defaults**.</span></span> <span data-ttu-id="64e61-215">**VB 預設值**中的初始預設設定為 `Off` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-215">The initial default setting in **VB Defaults** is `Off`.</span></span>  
  
### <a name="to-set-option-strict-on-the-command-line"></a><span data-ttu-id="64e61-216">若要在命令列上設定 Option Strict</span><span class="sxs-lookup"><span data-stu-id="64e61-216">To set Option Strict on the command line</span></span>  
 <span data-ttu-id="64e61-217">在**vbc**命令中包含[-optionstrict](../../reference/command-line-compiler/optionstrict.md)編譯器選項。</span><span class="sxs-lookup"><span data-stu-id="64e61-217">Include the [-optionstrict](../../reference/command-line-compiler/optionstrict.md) compiler option in the **vbc** command.</span></span>  
  
## <a name="example"></a><span data-ttu-id="64e61-218">範例</span><span class="sxs-lookup"><span data-stu-id="64e61-218">Example</span></span>  
 <span data-ttu-id="64e61-219">下列範例示範以縮小轉換的隱含類型轉換所造成的編譯時期錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e61-219">The following examples demonstrate compile-time errors caused by implicit type conversions that are narrowing conversions.</span></span> <span data-ttu-id="64e61-220">這個錯誤類別會對應至 [**編譯] 頁面**上的**隱含轉換**條件。</span><span class="sxs-lookup"><span data-stu-id="64e61-220">This category of errors corresponds to the **Implicit conversion** condition on the **Compile Page**.</span></span>  
  
 [!code-vb[VbVbalrStatements#161](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#161)]  
  
## <a name="example"></a><span data-ttu-id="64e61-221">範例</span><span class="sxs-lookup"><span data-stu-id="64e61-221">Example</span></span>  
 <span data-ttu-id="64e61-222">下列範例示範晚期繫結所造成的編譯時期錯誤。</span><span class="sxs-lookup"><span data-stu-id="64e61-222">The following example demonstrates a compile-time error caused by late binding.</span></span> <span data-ttu-id="64e61-223">這個錯誤類別會對應至晚期繫結; 在 [**編譯] 頁面**上，[**呼叫可能會在執行時間失敗**] 條件。</span><span class="sxs-lookup"><span data-stu-id="64e61-223">This category of errors corresponds to the **Late binding; call could fail at run time** condition on the **Compile Page**.</span></span>  
  
 [!code-vb[VbVbalrStatements#162](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#162)]  
  
## <a name="example"></a><span data-ttu-id="64e61-224">範例</span><span class="sxs-lookup"><span data-stu-id="64e61-224">Example</span></span>  
 <span data-ttu-id="64e61-225">下列範例示範以隱含類型宣告的變數所造成的錯誤 `Object` 。</span><span class="sxs-lookup"><span data-stu-id="64e61-225">The following examples demonstrate errors caused by variables that are declared with an implicit type of `Object`.</span></span> <span data-ttu-id="64e61-226">這個類別的錯誤對應于**隱含類型;** 在 [**編譯] 頁面**上的 [物件假設] 條件。</span><span class="sxs-lookup"><span data-stu-id="64e61-226">This category of errors corresponds to the **Implicit type; object assumed** condition on the **Compile Page**.</span></span>  
  
 [!code-vb[VbVbalrStatements#163](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#163)]  
  
 [!code-vb[VbVbalrStatements#164](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class13.vb#164)]  
  
## <a name="see-also"></a><span data-ttu-id="64e61-227">另請參閱</span><span class="sxs-lookup"><span data-stu-id="64e61-227">See also</span></span>

- [<span data-ttu-id="64e61-228">Widening and Narrowing Conversions</span><span class="sxs-lookup"><span data-stu-id="64e61-228">Widening and Narrowing Conversions</span></span>](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [<span data-ttu-id="64e61-229">隱含和明確轉換</span><span class="sxs-lookup"><span data-stu-id="64e61-229">Implicit and Explicit Conversions</span></span>](../../programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
- [<span data-ttu-id="64e61-230">專案設計工具、編譯頁 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="64e61-230">Compile Page, Project Designer (Visual Basic)</span></span>](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
- [<span data-ttu-id="64e61-231">Option Explicit 陳述式</span><span class="sxs-lookup"><span data-stu-id="64e61-231">Option Explicit Statement</span></span>](option-explicit-statement.md)
- [<span data-ttu-id="64e61-232">Type Conversion Functions</span><span class="sxs-lookup"><span data-stu-id="64e61-232">Type Conversion Functions</span></span>](../functions/type-conversion-functions.md)
- [<span data-ttu-id="64e61-233">如何：存取物件的成員</span><span class="sxs-lookup"><span data-stu-id="64e61-233">How to: Access Members of an Object</span></span>](../../programming-guide/language-features/variables/how-to-access-members-of-an-object.md)
- [<span data-ttu-id="64e61-234">XML 中內嵌的運算式</span><span class="sxs-lookup"><span data-stu-id="64e61-234">Embedded Expressions in XML</span></span>](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md)
- [<span data-ttu-id="64e61-235">寬鬆委派轉換</span><span class="sxs-lookup"><span data-stu-id="64e61-235">Relaxed Delegate Conversion</span></span>](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [<span data-ttu-id="64e61-236">Late Binding in Office Solutions</span><span class="sxs-lookup"><span data-stu-id="64e61-236">Late Binding in Office Solutions</span></span>](/visualstudio/vsto/late-binding-in-office-solutions)
- [<span data-ttu-id="64e61-237">-optionstrict</span><span class="sxs-lookup"><span data-stu-id="64e61-237">-optionstrict</span></span>](../../reference/command-line-compiler/optionstrict.md)
- [<span data-ttu-id="64e61-238">選項對話方塊、專案、Visual Basic 預設值</span><span class="sxs-lookup"><span data-stu-id="64e61-238">Visual Basic Defaults, Projects, Options Dialog Box</span></span>](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
