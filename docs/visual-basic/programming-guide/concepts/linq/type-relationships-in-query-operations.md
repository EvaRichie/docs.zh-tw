---
title: 查詢作業中的類型關聯性
ms.date: 07/20/2015
helpviewer_keywords:
- variable relationships [LINQ in Visual Basic]
- type information inferred [LINQ in Visual Basic]
- type relationships [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], type relationships
- data sources [LINQ in Visual Basic], type relationships
- LINQ [Visual Basic], type relationships
- inferring type information [LINQ in Visual Basic]
- relationships [LINQ in Visual Basic]
ms.assetid: b5ff4da5-f3fd-4a8e-aaac-1cbf52fa16f6
ms.openlocfilehash: 73a287541ddf115510bf6ab5c830eafac370cc3a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406725"
---
# <a name="type-relationships-in-query-operations-visual-basic"></a><span data-ttu-id="6afd4-102">查詢作業中的類型關聯性 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="6afd4-102">Type Relationships in Query Operations (Visual Basic)</span></span>

<span data-ttu-id="6afd4-103">用於語言整合式查詢（LINQ）查詢作業的變數是強型別，而且必須彼此相容。</span><span class="sxs-lookup"><span data-stu-id="6afd4-103">Variables used in Language-Integrated Query (LINQ) query operations are strongly typed and must be compatible with each other.</span></span> <span data-ttu-id="6afd4-104">強型別會用於資料來源、查詢本身和查詢執行中。</span><span class="sxs-lookup"><span data-stu-id="6afd4-104">Strong typing is used in the data source, in the query itself, and in the query execution.</span></span> <span data-ttu-id="6afd4-105">下圖識別用來描述 LINQ 查詢的詞彙。</span><span class="sxs-lookup"><span data-stu-id="6afd4-105">The following illustration identifies terms used to describe a LINQ query.</span></span> <span data-ttu-id="6afd4-106">如需查詢各部分的詳細資訊，請參閱[基本查詢作業（Visual Basic）](basic-query-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="6afd4-106">For more information about the parts of a query, see [Basic Query Operations (Visual Basic)](basic-query-operations.md).</span></span>

![顯示反白顯示專案之虛擬代碼查詢的螢幕擷取畫面。](./media/type-relationships-in-query-operations/linq-query-description-terms.png)

<span data-ttu-id="6afd4-108">查詢中的範圍變數類型必須與資料來源中的元素類型相容。</span><span class="sxs-lookup"><span data-stu-id="6afd4-108">The type of the range variable in the query must be compatible with the type of the elements in the data source.</span></span> <span data-ttu-id="6afd4-109">查詢變數的類型必須與子句中定義的 sequence 元素相容 `Select` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-109">The type of the query variable must be compatible with the sequence element defined in the `Select` clause.</span></span> <span data-ttu-id="6afd4-110">最後，順序元素的類型也必須與執行查詢的語句中所使用之迴圈控制變數的類型相容 `For Each` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-110">Finally, the type of the sequence elements also must be compatible with the type of the loop control variable that is used in the `For Each` statement that executes the query.</span></span> <span data-ttu-id="6afd4-111">這種強型別有助於在編譯時期識別類型錯誤。</span><span class="sxs-lookup"><span data-stu-id="6afd4-111">This strong typing facilitates identification of type errors at compile time.</span></span>

<span data-ttu-id="6afd4-112">Visual Basic 藉由實作為區欄位型別推斷（也稱為*隱含*類型），讓強型別變得方便。</span><span class="sxs-lookup"><span data-stu-id="6afd4-112">Visual Basic makes strong typing convenient by implementing local type inference, also known as *implicit typing*.</span></span> <span data-ttu-id="6afd4-113">上述範例中會使用該功能，您會在整個 LINQ 範例和檔中看到其使用方式。</span><span class="sxs-lookup"><span data-stu-id="6afd4-113">That feature is used in the previous example, and you will see it used throughout the LINQ samples and documentation.</span></span> <span data-ttu-id="6afd4-114">在 Visual Basic 中，只會使用不含子句的語句來完成區欄位型別推斷 `Dim` `As` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-114">In Visual Basic, local type inference is accomplished simply by using a `Dim` statement without an `As` clause.</span></span> <span data-ttu-id="6afd4-115">在下列範例中， `city` 是強型別（string）。</span><span class="sxs-lookup"><span data-stu-id="6afd4-115">In the following example, `city` is strongly typed as a string.</span></span>

[!code-vb[VbLINQTypeRels#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#1)]

> [!NOTE]
> <span data-ttu-id="6afd4-116">區欄位型別推斷只有在設為時才適用 `Option Infer` `On` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-116">Local type inference works only when `Option Infer` is set to `On`.</span></span> <span data-ttu-id="6afd4-117">如需詳細資訊，請參閱[Option 推斷語句](../../../language-reference/statements/option-infer-statement.md)。</span><span class="sxs-lookup"><span data-stu-id="6afd4-117">For more information, see [Option Infer Statement](../../../language-reference/statements/option-infer-statement.md).</span></span>

<span data-ttu-id="6afd4-118">不過，即使您在查詢中使用區欄位型別推斷，資料來源中的變數、查詢變數和查詢執行迴圈中都會出現相同的類型關聯性。</span><span class="sxs-lookup"><span data-stu-id="6afd4-118">However, even if you use local type inference in a query, the same type relationships are present among the variables in the data source, the query variable, and the query execution loop.</span></span> <span data-ttu-id="6afd4-119">當您撰寫 LINQ 查詢，或使用檔中的範例和程式碼範例時，對這些型別關聯性有基本瞭解非常有用。</span><span class="sxs-lookup"><span data-stu-id="6afd4-119">It is useful to have a basic understanding of these type relationships when you are writing LINQ queries, or working with the samples and code examples in the documentation.</span></span>

<span data-ttu-id="6afd4-120">針對不符合從資料來源傳回之類型的範圍變數，您可能需要指定明確的類型。</span><span class="sxs-lookup"><span data-stu-id="6afd4-120">You may need to specify an explicit type for a range variable that does not match the type returned from the data source.</span></span> <span data-ttu-id="6afd4-121">您可以使用子句來指定範圍變數的類型 `As` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-121">You can specify the type of the range variable by using an `As` clause.</span></span> <span data-ttu-id="6afd4-122">不過，如果轉換是[縮小轉換](../../language-features/data-types/widening-and-narrowing-conversions.md)，而且設定為，這會導致錯誤 `Option Strict` `On` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-122">However, this results in an error if the conversion is a [narrowing conversion](../../language-features/data-types/widening-and-narrowing-conversions.md) and `Option Strict` is set to `On`.</span></span> <span data-ttu-id="6afd4-123">因此，我們建議您在從資料來源抓取的值上執行轉換。</span><span class="sxs-lookup"><span data-stu-id="6afd4-123">Therefore, we recommend that you perform the conversion on the values retrieved from the data source.</span></span> <span data-ttu-id="6afd4-124">您可以使用方法，將資料來源中的值轉換成明確範圍變數類型 <xref:System.Linq.Enumerable.Cast%2A> 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-124">You can convert the values from the data source to the explicit range variable type by using the <xref:System.Linq.Enumerable.Cast%2A> method.</span></span> <span data-ttu-id="6afd4-125">您也可以將子句中選取的值 `Select` ，轉換成與範圍變數類型不同的明確類型。</span><span class="sxs-lookup"><span data-stu-id="6afd4-125">You can also cast the values selected in the `Select` clause to an explicit type that is different from the type of the range variable.</span></span> <span data-ttu-id="6afd4-126">下列程式碼說明這些點。</span><span class="sxs-lookup"><span data-stu-id="6afd4-126">These points are illustrated in the following code.</span></span>

[!code-vb[VbLINQTypeRels#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#4)]

## <a name="queries-that-return-entire-elements-of-the-source-data"></a><span data-ttu-id="6afd4-127">傳回來源資料之整個元素的查詢</span><span class="sxs-lookup"><span data-stu-id="6afd4-127">Queries That Return Entire Elements of the Source Data</span></span>

<span data-ttu-id="6afd4-128">下列範例顯示的 LINQ 查詢作業會傳回從來源資料選取的一系列元素。</span><span class="sxs-lookup"><span data-stu-id="6afd4-128">The following example shows a LINQ query operation that returns a sequence of elements selected from the source data.</span></span> <span data-ttu-id="6afd4-129">來源（ `names` ）包含字串陣列，而查詢輸出則是包含以字母 M 開頭之字串的序列。</span><span class="sxs-lookup"><span data-stu-id="6afd4-129">The source, `names`, contains an array of strings, and the query output is a sequence containing strings that start with the letter M.</span></span>

[!code-vb[VbLINQTypeRels#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#2)]

<span data-ttu-id="6afd4-130">這相當於下列程式碼，但更短且更容易撰寫。</span><span class="sxs-lookup"><span data-stu-id="6afd4-130">This is equivalent to the following code, but is much shorter and easier to write.</span></span> <span data-ttu-id="6afd4-131">在 Visual Basic 中，依賴查詢中的區欄位型別推斷是慣用的樣式。</span><span class="sxs-lookup"><span data-stu-id="6afd4-131">Reliance on local type inference in queries is the preferred style in Visual Basic.</span></span>

[!code-vb[VbLINQTypeRels#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#3)]

<span data-ttu-id="6afd4-132">下列關聯性存在於上述程式碼範例中，不論是隱含或明確地決定類型。</span><span class="sxs-lookup"><span data-stu-id="6afd4-132">The following relationships exist in both of the previous code examples, whether the types are determined implicitly or explicitly.</span></span>

1. <span data-ttu-id="6afd4-133">資料來源中的專案類型， `names` 是查詢中範圍變數的類型 `name` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-133">The type of the elements in the data source, `names`, is the type of the range variable, `name`, in the query.</span></span>

2. <span data-ttu-id="6afd4-134">所選取物件的類型會 `name` 決定查詢變數的類型 `mNames` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-134">The type of the object that is selected, `name`, determines the type of the query variable, `mNames`.</span></span> <span data-ttu-id="6afd4-135">以下 `name` 是字串，因此查詢變數是 Visual Basic 中的 IEnumerable （Of string）。</span><span class="sxs-lookup"><span data-stu-id="6afd4-135">Here `name` is a string, so the query variable is IEnumerable(Of String) in Visual Basic.</span></span>

3. <span data-ttu-id="6afd4-136">在中定義的查詢 `mNames` 會在迴圈中執行 `For Each` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-136">The query defined in `mNames` is executed in the `For Each` loop.</span></span> <span data-ttu-id="6afd4-137">迴圈會逐一查看執行查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="6afd4-137">The loop iterates over the result of executing the query.</span></span> <span data-ttu-id="6afd4-138">因為 `mNames` 在執行時，會傳回一連串的字串，所以迴圈反覆運算變數 `nm` 也是字串。</span><span class="sxs-lookup"><span data-stu-id="6afd4-138">Because `mNames`, when it is executed, will return a sequence of strings, the loop iteration variable, `nm`, also is a string.</span></span>

## <a name="queries-that-return-one-field-from-selected-elements"></a><span data-ttu-id="6afd4-139">從選取的元素傳回一個欄位的查詢</span><span class="sxs-lookup"><span data-stu-id="6afd4-139">Queries That Return One Field from Selected Elements</span></span>

<span data-ttu-id="6afd4-140">下列範例顯示的 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 查詢作業會傳回一個序列，其中包含從資料來源選取之每個元素的一個部分。</span><span class="sxs-lookup"><span data-stu-id="6afd4-140">The following example shows a [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] query operation that returns a sequence containing only one part of each element selected from the data source.</span></span> <span data-ttu-id="6afd4-141">查詢會接受物件的集合 `Customer` 做為其資料來源，並僅投射 `Name` 結果中的屬性。</span><span class="sxs-lookup"><span data-stu-id="6afd4-141">The query takes a collection of `Customer` objects as its data source and projects only the `Name` property in the result.</span></span> <span data-ttu-id="6afd4-142">因為客戶名稱是字串，所以查詢會產生一連串的字串做為輸出。</span><span class="sxs-lookup"><span data-stu-id="6afd4-142">Because the customer name is a string, the query produces a sequence of strings as output.</span></span>

```vb
' Method GetTable returns a table of Customer objects.
Dim customers = db.GetTable(Of Customer)()
Dim custNames = From cust In customers
                Where cust.City = "London"
                Select cust.Name

For Each custName In custNames
    Console.WriteLine(custName)
Next
```

<span data-ttu-id="6afd4-143">變數之間的關聯性類似于較簡單的範例。</span><span class="sxs-lookup"><span data-stu-id="6afd4-143">The relationships between variables are like those in the simpler example.</span></span>

1. <span data-ttu-id="6afd4-144">資料來源中的專案類型， `customers` 是查詢中範圍變數的類型 `cust` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-144">The type of the elements in the data source, `customers`, is the type of the range variable, `cust`, in the query.</span></span> <span data-ttu-id="6afd4-145">在此範例中，該類型為 `Customer` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-145">In this example, that type is `Customer`.</span></span>

2. <span data-ttu-id="6afd4-146">語句會傳回 `Select` `Name` 每個物件的屬性， `Customer` 而不是整個物件。</span><span class="sxs-lookup"><span data-stu-id="6afd4-146">The `Select` statement returns the `Name` property of each `Customer` object instead of the whole object.</span></span> <span data-ttu-id="6afd4-147">因為 `Name` 是字串，所以查詢變數 `custNames` 會再次是 IEnumerable （of string），而不是 `Customer` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-147">Because `Name` is a string, the query variable, `custNames`, will again be IEnumerable(Of String), not of `Customer`.</span></span>

3. <span data-ttu-id="6afd4-148">因為 `custNames` 代表字串序列，所以 `For Each` 迴圈的反復專案變數 `custName` 必須是字串。</span><span class="sxs-lookup"><span data-stu-id="6afd4-148">Because `custNames` represents a sequence of strings, the `For Each` loop's iteration variable, `custName`, must be a string.</span></span>

<span data-ttu-id="6afd4-149">如果沒有區欄位型別推斷，上一個範例會更難以撰寫和瞭解，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="6afd4-149">Without local type inference, the previous example would be more cumbersome to write and to understand, as the following example shows.</span></span>

```vb
' Method GetTable returns a table of Customer objects.
 Dim customers As Table(Of Customer) = db.GetTable(Of Customer)()
 Dim custNames As IEnumerable(Of String) =
     From cust As Customer In customers
     Where cust.City = "London"
     Select cust.Name

 For Each custName As String In custNames
     Console.WriteLine(custName)
 Next
```

## <a name="queries-that-require-anonymous-types"></a><span data-ttu-id="6afd4-150">需要匿名型別的查詢</span><span class="sxs-lookup"><span data-stu-id="6afd4-150">Queries That Require Anonymous Types</span></span>

<span data-ttu-id="6afd4-151">下列範例會顯示更複雜的情況。</span><span class="sxs-lookup"><span data-stu-id="6afd4-151">The following example shows a more complex situation.</span></span> <span data-ttu-id="6afd4-152">在上述範例中，明確地指定所有變數的類型並不方便。</span><span class="sxs-lookup"><span data-stu-id="6afd4-152">In the previous example, it was inconvenient to specify types for all the variables explicitly.</span></span> <span data-ttu-id="6afd4-153">在此範例中，這是不可能的。</span><span class="sxs-lookup"><span data-stu-id="6afd4-153">In this example, it is impossible.</span></span> <span data-ttu-id="6afd4-154">`Customer`此查詢中的子句會傳回原始物件的兩個屬性，而不是從資料來源中選取整個專案，或從每個專案中選取單一欄位 `Select` `Customer` ： `Name` 和 `City` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-154">Instead of selecting entire `Customer` elements from the data source, or a single field from each element, the `Select` clause in this query returns two properties of the original `Customer` object: `Name` and `City`.</span></span> <span data-ttu-id="6afd4-155">為了回應 `Select` 子句，編譯器會定義包含這兩個屬性的匿名型別。</span><span class="sxs-lookup"><span data-stu-id="6afd4-155">In response to the `Select` clause, the compiler defines an anonymous type that contains those two properties.</span></span> <span data-ttu-id="6afd4-156">`nameCityQuery`在迴圈中執行的結果 `For Each` 是新的匿名型別之實例的集合。</span><span class="sxs-lookup"><span data-stu-id="6afd4-156">The result of executing `nameCityQuery` in the `For Each` loop is a collection of instances of the new anonymous type.</span></span> <span data-ttu-id="6afd4-157">因為匿名型別沒有可用的名稱，所以您不能明確地指定或的型別 `nameCityQuery` `custInfo` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-157">Because the anonymous type has no usable name, you cannot specify the type of `nameCityQuery` or `custInfo` explicitly.</span></span> <span data-ttu-id="6afd4-158">也就是說，如果使用匿名型別，您就不需要使用型別名稱來取代 `String` 中的 `IEnumerable(Of String)` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-158">That is, with an anonymous type, you have no type name to use in place of `String` in `IEnumerable(Of String)`.</span></span> <span data-ttu-id="6afd4-159">如需詳細資訊，請參閱[匿名](../../language-features/objects-and-classes/anonymous-types.md)型別。</span><span class="sxs-lookup"><span data-stu-id="6afd4-159">For more information, see [Anonymous Types](../../language-features/objects-and-classes/anonymous-types.md).</span></span>

```vb
' Method GetTable returns a table of Customer objects.
Dim customers = db.GetTable(Of Customer)()
Dim nameCityQuery = From cust In customers
                    Where cust.City = "London"
                    Select cust.Name, cust.City

For Each custInfo In nameCityQuery
    Console.WriteLine(custInfo.Name)
Next
```

<span data-ttu-id="6afd4-160">雖然無法針對上述範例中的所有變數指定類型，但關聯性仍然相同。</span><span class="sxs-lookup"><span data-stu-id="6afd4-160">Although it is not possible to specify types for all the variables in the previous example, the relationships remain the same.</span></span>

1. <span data-ttu-id="6afd4-161">資料來源中的專案類型再次是查詢中的範圍變數類型。</span><span class="sxs-lookup"><span data-stu-id="6afd4-161">The type of the elements in the data source is again the type of the range variable in the query.</span></span> <span data-ttu-id="6afd4-162">在此範例中， `cust` 是的實例 `Customer` 。</span><span class="sxs-lookup"><span data-stu-id="6afd4-162">In this example, `cust` is an instance of `Customer`.</span></span>

2. <span data-ttu-id="6afd4-163">因為 `Select` 語句會產生匿名型別，所以查詢變數 `nameCityQuery` 必須以匿名型別隱含地輸入。</span><span class="sxs-lookup"><span data-stu-id="6afd4-163">Because the `Select` statement produces an anonymous type, the query variable, `nameCityQuery`, must be implicitly typed as an anonymous type.</span></span> <span data-ttu-id="6afd4-164">匿名型別沒有可用的名稱，因此無法明確指定。</span><span class="sxs-lookup"><span data-stu-id="6afd4-164">An anonymous type has no usable name, and therefore cannot be specified explicitly.</span></span>

3. <span data-ttu-id="6afd4-165">迴圈中的反覆運算變數類型 `For Each` 是在步驟2中建立的匿名型別。</span><span class="sxs-lookup"><span data-stu-id="6afd4-165">The type of the iteration variable in the `For Each` loop is the anonymous type created in step 2.</span></span> <span data-ttu-id="6afd4-166">因為類型沒有可用的名稱，所以必須隱含地判斷迴圈反覆運算變數的類型。</span><span class="sxs-lookup"><span data-stu-id="6afd4-166">Because the type has no usable name, the type of the loop iteration variable must be determined implicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="6afd4-167">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6afd4-167">See also</span></span>

- [<span data-ttu-id="6afd4-168">使用 Visual Basic 撰寫 LINQ 入門</span><span class="sxs-lookup"><span data-stu-id="6afd4-168">Getting Started with LINQ in Visual Basic</span></span>](getting-started-with-linq.md)
- [<span data-ttu-id="6afd4-169">匿名類型</span><span class="sxs-lookup"><span data-stu-id="6afd4-169">Anonymous Types</span></span>](../../language-features/objects-and-classes/anonymous-types.md)
- [<span data-ttu-id="6afd4-170">區域型別推斷</span><span class="sxs-lookup"><span data-stu-id="6afd4-170">Local Type Inference</span></span>](../../language-features/variables/local-type-inference.md)
- [<span data-ttu-id="6afd4-171">Visual Basic 中的 LINQ 簡介</span><span class="sxs-lookup"><span data-stu-id="6afd4-171">Introduction to LINQ in Visual Basic</span></span>](../../language-features/linq/introduction-to-linq.md)
- [<span data-ttu-id="6afd4-172">LINQ</span><span class="sxs-lookup"><span data-stu-id="6afd4-172">LINQ</span></span>](../../language-features/linq/index.md)
- [<span data-ttu-id="6afd4-173">查詢</span><span class="sxs-lookup"><span data-stu-id="6afd4-173">Queries</span></span>](../../../language-reference/queries/index.md)
