---
title: 投影作業
ms.date: 07/20/2015
ms.assetid: b8d38e6d-21cf-4619-8dbb-94476f4badc7
ms.openlocfilehash: 4795bdaba53949b34fe380ea9c51025ce43c40db
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396333"
---
# <a name="projection-operations-visual-basic"></a><span data-ttu-id="0d9e8-102">投射作業（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="0d9e8-102">Projection Operations (Visual Basic)</span></span>

<span data-ttu-id="0d9e8-103">投影是指將物件轉換成新形式的作業，而這個形式通常僅包含後續即將使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-103">Projection refers to the operation of transforming an object into a new form that often consists only of those properties that will be subsequently used.</span></span> <span data-ttu-id="0d9e8-104">透過使用投影，您可以建構根據每個物件所建立的新型別。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-104">By using projection, you can construct a new type that is built from each object.</span></span> <span data-ttu-id="0d9e8-105">您可以投影屬性並對其執行數學函式。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-105">You can project a property and perform a mathematical function on it.</span></span> <span data-ttu-id="0d9e8-106">您也可以投影原始物件，而不進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-106">You can also project the original object without changing it.</span></span>

<span data-ttu-id="0d9e8-107">執行投影的標準查詢運算子方法詳列於下一節。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-107">The standard query operator methods that perform projection are listed in the following section.</span></span>

## <a name="methods"></a><span data-ttu-id="0d9e8-108">方法</span><span class="sxs-lookup"><span data-stu-id="0d9e8-108">Methods</span></span>

|<span data-ttu-id="0d9e8-109">方法名稱</span><span class="sxs-lookup"><span data-stu-id="0d9e8-109">Method Name</span></span>|<span data-ttu-id="0d9e8-110">Description</span><span class="sxs-lookup"><span data-stu-id="0d9e8-110">Description</span></span>|<span data-ttu-id="0d9e8-111">Visual Basic 查詢運算式語法</span><span class="sxs-lookup"><span data-stu-id="0d9e8-111">Visual Basic Query Expression Syntax</span></span>|<span data-ttu-id="0d9e8-112">相關資訊</span><span class="sxs-lookup"><span data-stu-id="0d9e8-112">More Information</span></span>|
|-----------------|-----------------|------------------------------------------|----------------------|
|<span data-ttu-id="0d9e8-113">選取</span><span class="sxs-lookup"><span data-stu-id="0d9e8-113">Select</span></span>|<span data-ttu-id="0d9e8-114">投影以轉換函式為基礎的值。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-114">Projects values that are based on a transform function.</span></span>|`Select`|<xref:System.Linq.Enumerable.Select%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Select%2A?displayProperty=nameWithType>|
|<span data-ttu-id="0d9e8-115">SelectMany</span><span class="sxs-lookup"><span data-stu-id="0d9e8-115">SelectMany</span></span>|<span data-ttu-id="0d9e8-116">投影一連串以轉換函式為基礎的值，然後將這些值壓平合併成一個序列。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-116">Projects sequences of values that are based on a transform function and then flattens them into one sequence.</span></span>|<span data-ttu-id="0d9e8-117">使用多個 `From` 子句</span><span class="sxs-lookup"><span data-stu-id="0d9e8-117">Use multiple `From` clauses</span></span>|<xref:System.Linq.Enumerable.SelectMany%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.SelectMany%2A?displayProperty=nameWithType>|

## <a name="query-expression-syntax-examples"></a><span data-ttu-id="0d9e8-118">查詢運算式語法範例</span><span class="sxs-lookup"><span data-stu-id="0d9e8-118">Query Expression Syntax Examples</span></span>

### <a name="select"></a><span data-ttu-id="0d9e8-119">選取</span><span class="sxs-lookup"><span data-stu-id="0d9e8-119">Select</span></span>

<span data-ttu-id="0d9e8-120">下列範例使用 `Select` 子句，來投影字串清單中每個字串的第一個字母。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-120">The following example uses the `Select` clause to project the first letter from each string in a list of strings.</span></span>

```vb
Dim words = New List(Of String) From {"an", "apple", "a", "day"}

Dim query = From word In words
            Select word.Substring(0, 1)

Dim sb As New System.Text.StringBuilder()
For Each letter As String In query
    sb.AppendLine(letter)
Next

' Display the output.
MsgBox(sb.ToString())

' This code produces the following output:

' a
' a
' a
' d
```

### <a name="selectmany"></a><span data-ttu-id="0d9e8-121">SelectMany</span><span class="sxs-lookup"><span data-stu-id="0d9e8-121">SelectMany</span></span>

<span data-ttu-id="0d9e8-122">下列範例會使用多個 `From` 子句，來投影字串清單中每個字串的每個單字。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-122">The following example uses multiple `From` clauses to project each word from each string in a list of strings.</span></span>

```vb
Dim phrases = New List(Of String) From {"an apple a day", "the quick brown fox"}

Dim query = From phrase In phrases
            From word In phrase.Split(" "c)
            Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In query
    sb.AppendLine(str)
Next

' Display the output.
MsgBox(sb.ToString())

' This code produces the following output:

' an
' apple
' a
' day
' the
' quick
' brown
' fox
```

## <a name="select-versus-selectmany"></a><span data-ttu-id="0d9e8-123">Select 與 SelectMany 的比較</span><span class="sxs-lookup"><span data-stu-id="0d9e8-123">Select versus SelectMany</span></span>

<span data-ttu-id="0d9e8-124">`Select()` 和 `SelectMany()` 的工作是從來源值產生一或多個結果值。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-124">The work of both `Select()` and `SelectMany()` is to produce a result value (or values) from source values.</span></span> <span data-ttu-id="0d9e8-125">`Select()` 會針對每個來源值產生一個結果值。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-125">`Select()` produces one result value for every source value.</span></span> <span data-ttu-id="0d9e8-126">因此，整體結果是集合與來源集合中的項目數相同。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-126">The overall result is therefore a collection that has the same number of elements as the source collection.</span></span> <span data-ttu-id="0d9e8-127">相反地，`SelectMany()` 會產生單一整體結果，其中包含串連自每個來源值的子集合。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-127">In contrast, `SelectMany()` produces a single overall result that contains concatenated sub-collections from each source value.</span></span> <span data-ttu-id="0d9e8-128">當做引數傳遞至 `SelectMany()` 的轉換函式必須傳回每個來源值的可列舉值序列。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-128">The transform function that is passed as an argument to `SelectMany()` must return an enumerable sequence of values for each source value.</span></span> <span data-ttu-id="0d9e8-129">`SelectMany()` 會接著串連這些可列舉的序列，以建立一個大型的序列。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-129">These enumerable sequences are then concatenated by `SelectMany()` to create one large sequence.</span></span>

<span data-ttu-id="0d9e8-130">下列兩個圖顯示這兩個方法的動作之間的概念差異。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-130">The following two illustrations show the conceptual difference between the actions of these two methods.</span></span> <span data-ttu-id="0d9e8-131">在每個案例中，假設選取器 (轉換) 函式會從每個來源值選取花朵陣列。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-131">In each case, assume that the selector (transform) function selects the array of flowers from each source value.</span></span>

<span data-ttu-id="0d9e8-132">下圖描述 `Select()` 如何傳回其中的項目數與來源集合相同的集合。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-132">This illustration depicts how `Select()` returns a collection that has the same number of elements as the source collection.</span></span>

![顯示 Select&#40;&#41; 之動作的圖形](./media/projection-operations/select-action-graphic.png)

<span data-ttu-id="0d9e8-134">下圖描述 `SelectMany()` 如何將中繼陣列序列串連成一個最終結果值，其中包含每個中繼陣列中的所有值。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-134">This illustration depicts how `SelectMany()` concatenates the intermediate sequence of arrays into one final result value that contains each value from each intermediate array.</span></span>

![顯示 SelectMany&#40;&#41; 之動作的圖形。](./media/projection-operations/select-many-action-graphic.png )

### <a name="code-example"></a><span data-ttu-id="0d9e8-136">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="0d9e8-136">Code Example</span></span>

<span data-ttu-id="0d9e8-137">下列範例會比較 `Select()` 和 `SelectMany()` 的行為。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-137">The following example compares the behavior of `Select()` and `SelectMany()`.</span></span> <span data-ttu-id="0d9e8-138">程式碼會從來源集合的每個花名清單中擷取前兩個項目，以建立「花束」(Bouquet)。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-138">The code creates a "bouquet" of flowers by taking the first two items from each list of flower names in the source collection.</span></span> <span data-ttu-id="0d9e8-139">在此範例中，轉換函式 <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29> 所使用的「單一值」本身就是值集合。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-139">In this example, the "single value" that the transform function <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29> uses is itself a collection of values.</span></span> <span data-ttu-id="0d9e8-140">這需要額外的 `For Each` 迴圈，以列舉每個子序列中的每個字串。</span><span class="sxs-lookup"><span data-stu-id="0d9e8-140">This requires the extra `For Each` loop in order to enumerate each string in each sub-sequence.</span></span>

```vb
Class Bouquet
    Public Flowers As List(Of String)
End Class

Sub SelectVsSelectMany()
    Dim bouquets = New List(Of Bouquet) From {
        New Bouquet With {.Flowers = New List(Of String)(New String() {"sunflower", "daisy", "daffodil", "larkspur"})},
        New Bouquet With {.Flowers = New List(Of String)(New String() {"tulip", "rose", "orchid"})},
        New Bouquet With {.Flowers = New List(Of String)(New String() {"gladiolis", "lily", "snapdragon", "aster", "protea"})},
        New Bouquet With {.Flowers = New List(Of String)(New String() {"larkspur", "lilac", "iris", "dahlia"})}}

    Dim output As New System.Text.StringBuilder

    ' Select()
    Dim query1 = bouquets.Select(Function(b) b.Flowers)

    output.AppendLine("Using Select():")
    For Each flowerList In query1
        For Each str As String In flowerList
            output.AppendLine(str)
        Next
    Next

    ' SelectMany()
    Dim query2 = bouquets.SelectMany(Function(b) b.Flowers)

    output.AppendLine(vbCrLf & "Using SelectMany():")
    For Each str As String In query2
        output.AppendLine(str)
    Next

    ' Display the output
    MsgBox(output.ToString())

    ' This code produces the following output:
    '
    ' Using Select():
    ' sunflower
    ' daisy
    ' daffodil
    ' larkspur
    ' tulip
    ' rose
    ' orchid
    ' gladiolis
    ' lily
    ' snapdragon
    ' aster
    ' protea
    ' larkspur
    ' lilac
    ' iris
    ' dahlia

    ' Using SelectMany()
    ' sunflower
    ' daisy
    ' daffodil
    ' larkspur
    ' tulip
    ' rose
    ' orchid
    ' gladiolis
    ' lily
    ' snapdragon
    ' aster
    ' protea
    ' larkspur
    ' lilac
    ' iris
    ' dahlia

End Sub
```

## <a name="see-also"></a><span data-ttu-id="0d9e8-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0d9e8-141">See also</span></span>

- <xref:System.Linq>
- [<span data-ttu-id="0d9e8-142">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0d9e8-142">Standard Query Operators Overview (Visual Basic)</span></span>](standard-query-operators-overview.md)
- [<span data-ttu-id="0d9e8-143">Select 子句</span><span class="sxs-lookup"><span data-stu-id="0d9e8-143">Select Clause</span></span>](../../../language-reference/queries/select-clause.md)
- [<span data-ttu-id="0d9e8-144">如何：使用 Joins 合併資料</span><span class="sxs-lookup"><span data-stu-id="0d9e8-144">How to: Combine Data with Joins</span></span>](../../language-features/linq/how-to-combine-data-with-linq-by-using-joins.md)
- [<span data-ttu-id="0d9e8-145">如何：從多個來源填入物件集合（LINQ）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="0d9e8-145">How to: Populate Object Collections from Multiple Sources (LINQ) (Visual Basic)</span></span>](how-to-populate-object-collections-from-multiple-sources-linq.md)
- [<span data-ttu-id="0d9e8-146">如何：將 LINQ 查詢結果當做特定類型傳回</span><span class="sxs-lookup"><span data-stu-id="0d9e8-146">How to: Return a LINQ Query Result as a Specific Type</span></span>](../../language-features/linq/how-to-return-a-linq-query-result-as-a-specific-type.md)
- [<span data-ttu-id="0d9e8-147">如何：使用群組將檔案分割成許多檔案（LINQ）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="0d9e8-147">How to: Split a File Into Many Files by Using Groups (LINQ) (Visual Basic)</span></span>](how-to-split-a-file-into-many-files-by-using-groups-linq.md)
