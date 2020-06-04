---
title: 篩選資料
ms.date: 07/20/2015
ms.assetid: 7749519a-7edc-49fe-aef9-6a353864af6c
ms.openlocfilehash: f7a1aa76dc93cc03952e55f5f8fc3f75176a3f9f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84383413"
---
# <a name="filtering-data-visual-basic"></a><span data-ttu-id="292af-102">篩選資料（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="292af-102">Filtering Data (Visual Basic)</span></span>

<span data-ttu-id="292af-103">篩選指的是將結果集限制為只包含符合指定條件之元素的作業，</span><span class="sxs-lookup"><span data-stu-id="292af-103">Filtering refers to the operation of restricting the result set to contain only those elements that satisfy a specified condition.</span></span> <span data-ttu-id="292af-104">也稱為選取。</span><span class="sxs-lookup"><span data-stu-id="292af-104">It is also known as selection.</span></span>

<span data-ttu-id="292af-105">下圖顯示字元序列的篩選結果。</span><span class="sxs-lookup"><span data-stu-id="292af-105">The following illustration shows the results of filtering a sequence of characters.</span></span> <span data-ttu-id="292af-106">篩選作業的述詞指定字元必須為 'A'。</span><span class="sxs-lookup"><span data-stu-id="292af-106">The predicate for the filtering operation specifies that the character must be 'A'.</span></span>

![顯示 LINQ 篩選作業的圖表](./media/filtering-data/linq-filter-operation.png)

<span data-ttu-id="292af-108">執行選取的標準查詢運算子方法詳列於下一節。</span><span class="sxs-lookup"><span data-stu-id="292af-108">The standard query operator methods that perform selection are listed in the following section.</span></span>

## <a name="methods"></a><span data-ttu-id="292af-109">方法</span><span class="sxs-lookup"><span data-stu-id="292af-109">Methods</span></span>

|<span data-ttu-id="292af-110">方法名稱</span><span class="sxs-lookup"><span data-stu-id="292af-110">Method Name</span></span>|<span data-ttu-id="292af-111">Description</span><span class="sxs-lookup"><span data-stu-id="292af-111">Description</span></span>|<span data-ttu-id="292af-112">Visual Basic 查詢運算式語法</span><span class="sxs-lookup"><span data-stu-id="292af-112">Visual Basic Query Expression Syntax</span></span>|<span data-ttu-id="292af-113">相關資訊</span><span class="sxs-lookup"><span data-stu-id="292af-113">More Information</span></span>|
|-----------------|-----------------|------------------------------------------|----------------------|
|<span data-ttu-id="292af-114">OfType</span><span class="sxs-lookup"><span data-stu-id="292af-114">OfType</span></span>|<span data-ttu-id="292af-115">根據可轉換為所指定類型的能力來選取值。</span><span class="sxs-lookup"><span data-stu-id="292af-115">Selects values, depending on their ability to be cast to a specified type.</span></span>|<span data-ttu-id="292af-116">不適用。</span><span class="sxs-lookup"><span data-stu-id="292af-116">Not applicable.</span></span>|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=nameWithType>|
|<span data-ttu-id="292af-117">Where</span><span class="sxs-lookup"><span data-stu-id="292af-117">Where</span></span>|<span data-ttu-id="292af-118">根據述詞函式來選取值。</span><span class="sxs-lookup"><span data-stu-id="292af-118">Selects values that are based on a predicate function.</span></span>|`Where`|<xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType>|

## <a name="query-expression-syntax-example"></a><span data-ttu-id="292af-119">查詢運算式語法範例</span><span class="sxs-lookup"><span data-stu-id="292af-119">Query Expression Syntax Example</span></span>

<span data-ttu-id="292af-120">下列範例會使用， `Where` 從陣列中篩選具有特定長度的字串。</span><span class="sxs-lookup"><span data-stu-id="292af-120">The following example uses the `Where` to filter from an array those strings that have a specific length.</span></span>

```vb
Dim words() As String = {"the", "quick", "brown", "fox", "jumps"}

Dim query = From word In words
            Where word.Length = 3
            Select word

Dim sb As New System.Text.StringBuilder()
For Each str As String In query
    sb.AppendLine(str)
Next

' Display the results.
MsgBox(sb.ToString())

' This code produces the following output:

' the
' fox
```

## <a name="see-also"></a><span data-ttu-id="292af-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="292af-121">See also</span></span>

- <xref:System.Linq>
- [<span data-ttu-id="292af-122">標準查詢運算子概觀 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="292af-122">Standard Query Operators Overview (Visual Basic)</span></span>](standard-query-operators-overview.md)
- [<span data-ttu-id="292af-123">Where 子句</span><span class="sxs-lookup"><span data-stu-id="292af-123">Where Clause</span></span>](../../../language-reference/queries/where-clause.md)
- [<span data-ttu-id="292af-124">如何：篩選查詢結果</span><span class="sxs-lookup"><span data-stu-id="292af-124">How to: Filter Query Results</span></span>](../../language-features/linq/how-to-filter-query-results-by-using-linq.md)
- [<span data-ttu-id="292af-125">如何：使用反映查詢元件的中繼資料（LINQ）（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="292af-125">How to: Query An Assembly's Metadata with Reflection (LINQ) (Visual Basic)</span></span>](how-to-query-an-assembly-s-metadata-with-reflection-linq.md)
- [<span data-ttu-id="292af-126">如何：查詢具有指定之屬性或名稱的檔案（Visual Basic）</span><span class="sxs-lookup"><span data-stu-id="292af-126">How to: Query for Files with a Specified Attribute or Name (Visual Basic)</span></span>](how-to-query-for-files-with-a-specified-attribute-or-name.md)
- [<span data-ttu-id="292af-127">如何：依任何字或欄位排序或篩選文字資料 (LINQ) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="292af-127">How to: Sort or Filter Text Data by Any Word or Field (LINQ) (Visual Basic)</span></span>](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
