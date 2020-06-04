---
title: 如何：使用 Join 透過 LINQ 合併資料
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], joins
- joins [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- Group Join clause [Visual Basic]
- joining [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 5b00a478-035b-41c6-8918-be1a97728396
ms.openlocfilehash: de8c4ec3ab8a0f2335c034231c661380420fd31b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405000"
---
# <a name="how-to-combine-data-with-linq-by-using-joins-visual-basic"></a><span data-ttu-id="8f2b4-102">如何：使用 Joins 以 LINQ 合併資料 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="8f2b4-102">How to: Combine Data with LINQ by Using Joins (Visual Basic)</span></span>
<span data-ttu-id="8f2b4-103">Visual Basic 提供 `Join` 和 `Group Join` 查詢子句，可讓您根據集合之間的通用值，結合多個集合的內容。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-103">Visual Basic provides the `Join` and `Group Join` query clauses to enable you to combine the contents of multiple collections based on common values between the collections.</span></span> <span data-ttu-id="8f2b4-104">這些值稱為索引*鍵值*。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-104">These values are known as *key* values.</span></span> <span data-ttu-id="8f2b4-105">熟悉關係資料庫概念的開發人員會將 `Join` 子句辨識為內部聯結，並將 `Group Join` 子句視為有效的左方外部聯結。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-105">Developers familiar with relational database concepts will recognize the `Join` clause as an INNER JOIN and the `Group Join` clause as, effectively, a LEFT OUTER JOIN.</span></span>  
  
 <span data-ttu-id="8f2b4-106">本主題中的範例將示範使用 `Join` 和查詢子句結合資料的幾種方式 `Group Join` 。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-106">The examples in this topic demonstrate a few ways to combine data by using the `Join` and `Group Join` query clauses.</span></span>  
  
## <a name="create-a-project-and-add-sample-data"></a><span data-ttu-id="8f2b4-107">建立專案並新增範例資料</span><span class="sxs-lookup"><span data-stu-id="8f2b4-107">Create a Project and Add Sample Data</span></span>  
  
#### <a name="to-create-a-project-that-contains-sample-data-and-types"></a><span data-ttu-id="8f2b4-108">若要建立包含範例資料和類型的專案</span><span class="sxs-lookup"><span data-stu-id="8f2b4-108">To create a project that contains sample data and types</span></span>  
  
1. <span data-ttu-id="8f2b4-109">若要執行本主題中的範例，請開啟 Visual Studio 並加入新的 Visual Basic 主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-109">To run the samples in this topic, open Visual Studio and add a new Visual Basic Console Application project.</span></span> <span data-ttu-id="8f2b4-110">按兩下 Visual Basic 所建立的 Module1 檔案。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-110">Double-click the Module1.vb file created by Visual Basic.</span></span>  
  
2. <span data-ttu-id="8f2b4-111">本主題中的範例會使用 `Person` 下列程式碼範例中的和 `Pet` 類型和資料。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-111">The samples in this topic use the `Person` and `Pet` types and data from the following code example.</span></span> <span data-ttu-id="8f2b4-112">將此程式碼複製到 `Module1` Visual Basic 所建立的預設模組。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-112">Copy this code into the default `Module1` module created by Visual Basic.</span></span>  
  
     [!code-vb[VbLINQHowTos#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#1)]  
    [!code-vb[VbLINQHowTos#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#2)]  
  
## <a name="perform-an-inner-join-by-using-the-join-clause"></a><span data-ttu-id="8f2b4-113">使用 Join 子句執行內部聯結</span><span class="sxs-lookup"><span data-stu-id="8f2b4-113">Perform an Inner Join by Using the Join Clause</span></span>  
 <span data-ttu-id="8f2b4-114">內部聯結結合兩個集合中的資料。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-114">An INNER JOIN combines data from two collections.</span></span> <span data-ttu-id="8f2b4-115">包含指定之索引鍵值相符的專案。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-115">Items for which the specified key values match are included.</span></span> <span data-ttu-id="8f2b4-116">不會排除任何集合中任何來自其他集合之相符專案的專案。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-116">Any items from either collection that do not have a matching item in the other collection are excluded.</span></span>  
  
 <span data-ttu-id="8f2b4-117">在 Visual Basic 中，LINQ 提供兩個選項來執行內部聯結：隱含聯結和明確聯結。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-117">In Visual Basic, LINQ provides two options for performing an INNER JOIN: an implicit join and an explicit join.</span></span>  
  
 <span data-ttu-id="8f2b4-118">隱含聯結會指定要聯結在子句中的集合 `From` ，並在子句中識別相符的索引鍵欄位 `Where` 。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-118">An implicit join specifies the collections to be joined in a `From` clause and identifies the matching key fields in a `Where` clause.</span></span> <span data-ttu-id="8f2b4-119">Visual Basic 會根據指定的索引鍵欄位，隱含地聯結兩個集合。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-119">Visual Basic implicitly joins the two collections based on the specified key fields.</span></span>  
  
 <span data-ttu-id="8f2b4-120">`Join`當您想要特定于聯結中使用的索引鍵欄位時，可以使用子句來指定明確聯結。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-120">You can specify an explicit join by using the `Join` clause when you want to be specific about which key fields to use in the join.</span></span> <span data-ttu-id="8f2b4-121">在此情況下， `Where` 子句仍然可以用來篩選查詢結果。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-121">In this case, a `Where` clause can still be used to filter the query results.</span></span>  
  
#### <a name="to-perform-an-inner-join-by-using-the-join-clause"></a><span data-ttu-id="8f2b4-122">若要使用 Join 子句來執行內部聯結</span><span class="sxs-lookup"><span data-stu-id="8f2b4-122">To perform an Inner Join by using the Join clause</span></span>  
  
1. <span data-ttu-id="8f2b4-123">將下列程式碼新增至 `Module1` 專案中的模組，以查看隱含和明確內部聯結的範例。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-123">Add the following code to the `Module1` module in your project to see examples of both an implicit and explicit inner join.</span></span>  
  
     [!code-vb[VbLINQHowTos#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#4)]  
  
## <a name="perform-a-left-outer-join-by-using-the-group-join-clause"></a><span data-ttu-id="8f2b4-124">使用 Group Join 子句執行左方外部聯結</span><span class="sxs-lookup"><span data-stu-id="8f2b4-124">Perform a Left Outer Join by Using the Group Join Clause</span></span>  
 <span data-ttu-id="8f2b4-125">左方外部聯結包含來自聯結之左側集合中的所有專案，以及僅符合聯結之右端集合的值。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-125">A LEFT OUTER JOIN includes all the items from the left-side collection of the join and only matching values from the right-side collection of the join.</span></span> <span data-ttu-id="8f2b4-126">在左側集合中沒有相符專案的任何聯結之右端集合中的任何專案，都會從查詢結果中排除。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-126">Any items from the right-side collection of the join that do not have a matching item in the left-side collection are excluded from the query result.</span></span>  
  
 <span data-ttu-id="8f2b4-127">`Group Join`子句會執行左外部聯結。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-127">The `Group Join` clause performs, in effect, a LEFT OUTER JOIN.</span></span> <span data-ttu-id="8f2b4-128">通常所謂的「左方外部聯結」和「子句」傳回的差異在於， `Group Join` `Group Join` 子句會針對左側集合中的每個專案，從聯結的右端集合中將結果分組。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-128">The difference between what is typically known as a LEFT OUTER JOIN and what the `Group Join` clause returns is that the `Group Join` clause groups results from the right-side collection of the join for each item in the left-side collection.</span></span> <span data-ttu-id="8f2b4-129">在關係資料庫中，左方外部聯結會傳回未分組的結果，其中查詢結果中的每個專案都包含聯結中兩個集合的相符專案。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-129">In a relational database, a LEFT OUTER JOIN returns an ungrouped result in which each item in the query result contains matching items from both collections in the join.</span></span> <span data-ttu-id="8f2b4-130">在此情況下，會針對右側集合中的每個相符專案，重複聯結之左側集合中的專案。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-130">In this case, the items from the left-side collection of the join are repeated for each matching item from the right-side collection.</span></span> <span data-ttu-id="8f2b4-131">當您完成下一個程式時，您會看到這看起來的樣子。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-131">You will see what this looks like when you complete the next procedure.</span></span>  
  
 <span data-ttu-id="8f2b4-132">您可以藉 `Group Join` 由擴充您的查詢來傳回每個群組查詢結果的專案，藉此將查詢的結果當做未分組的結果來取得。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-132">You can retrieve the results of a `Group Join` query as an ungrouped result by extending your query to return an item for each grouped query result.</span></span> <span data-ttu-id="8f2b4-133">若要完成這項工作，您必須確定查詢已 `DefaultIfEmpty` 群組集合的方法。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-133">To accomplish this, you have to ensure that you query on the `DefaultIfEmpty` method of the grouped collection.</span></span> <span data-ttu-id="8f2b4-134">這可確保聯結的左側集合中的專案仍會包含在查詢結果中，即使它們沒有來自右邊集合的相符結果。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-134">This ensures that items from the left-side collection of the join are still included in the query result even if they have no matching results from the right-side collection.</span></span> <span data-ttu-id="8f2b4-135">您可以將程式碼加入至查詢，以便在聯結的右側集合中沒有相符的值時，提供預設的結果值。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-135">You can add code to your query to provide a default result value when there is no matching value from the right-side collection of the join.</span></span>  
  
#### <a name="to-perform-a-left-outer-join-by-using-the-group-join-clause"></a><span data-ttu-id="8f2b4-136">若要使用 Group Join 子句來執行左方外部聯結</span><span class="sxs-lookup"><span data-stu-id="8f2b4-136">To perform a Left Outer Join by using the Group Join clause</span></span>  
  
1. <span data-ttu-id="8f2b4-137">將下列程式碼新增至 `Module1` 專案中的模組，以查看群組左方外部聯結和取消分組左方外部聯結的範例。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-137">Add the following code to the `Module1` module in your project to see examples of both a grouped left outer join and an ungrouped left outer join.</span></span>  
  
     [!code-vb[VbLINQHowTos#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#3)]  
  
## <a name="perform-a-join-by-using-a-composite-key"></a><span data-ttu-id="8f2b4-138">使用複合索引鍵執行聯結</span><span class="sxs-lookup"><span data-stu-id="8f2b4-138">Perform a Join by Using a Composite Key</span></span>  
 <span data-ttu-id="8f2b4-139">您可以 `And` 在或子句中使用 `Join` 關鍵字 `Group Join` ，以識別要聯結之集合中的值相符時，所要使用的多個索引鍵欄位。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-139">You can use the `And` keyword in a `Join` or `Group Join` clause to identify multiple key fields to use when matching values from the collections being joined.</span></span> <span data-ttu-id="8f2b4-140">`And`關鍵字會指定所有指定的索引鍵欄位必須符合才能聯結的專案。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-140">The `And` keyword specifies that all specified key fields must match for items to be joined.</span></span>  
  
#### <a name="to-perform-a-join-by-using-a-composite-key"></a><span data-ttu-id="8f2b4-141">若要使用複合索引鍵執行聯結</span><span class="sxs-lookup"><span data-stu-id="8f2b4-141">To perform a Join by using a composite key</span></span>  
  
1. <span data-ttu-id="8f2b4-142">將下列程式碼加入至 `Module1` 專案中的模組，以查看使用複合索引鍵之聯結的範例。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-142">Add the following code to the `Module1` module in your project to see examples of a join that uses a composite key.</span></span>  
  
     [!code-vb[VbLINQHowTos#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#5)]  
  
## <a name="run-the-code"></a><span data-ttu-id="8f2b4-143">執行程式碼</span><span class="sxs-lookup"><span data-stu-id="8f2b4-143">Run the Code</span></span>  
  
#### <a name="to-add-code-to-run-the-examples"></a><span data-ttu-id="8f2b4-144">若要加入程式碼以執行範例</span><span class="sxs-lookup"><span data-stu-id="8f2b4-144">To add code to run the examples</span></span>  
  
1. <span data-ttu-id="8f2b4-145">使用下列程式碼取代專案中模組中的， `Sub Main` `Module1` 以執行本主題中的範例。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-145">Replace the `Sub Main` in the `Module1` module in your project with the following code to run the examples in this topic.</span></span>  
  
     [!code-vb[VbLINQHowTos#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#6)]  
  
2. <span data-ttu-id="8f2b4-146">按 F5 執行範例。</span><span class="sxs-lookup"><span data-stu-id="8f2b4-146">Press F5 to run the examples.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8f2b4-147">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8f2b4-147">See also</span></span>

- [<span data-ttu-id="8f2b4-148">LINQ</span><span class="sxs-lookup"><span data-stu-id="8f2b4-148">LINQ</span></span>](index.md)
- [<span data-ttu-id="8f2b4-149">Visual Basic 中的 LINQ 簡介</span><span class="sxs-lookup"><span data-stu-id="8f2b4-149">Introduction to LINQ in Visual Basic</span></span>](introduction-to-linq.md)
- [<span data-ttu-id="8f2b4-150">Join 子句</span><span class="sxs-lookup"><span data-stu-id="8f2b4-150">Join Clause</span></span>](../../../language-reference/queries/join-clause.md)
- [<span data-ttu-id="8f2b4-151">Group Join 子句</span><span class="sxs-lookup"><span data-stu-id="8f2b4-151">Group Join Clause</span></span>](../../../language-reference/queries/group-join-clause.md)
- [<span data-ttu-id="8f2b4-152">From 子句</span><span class="sxs-lookup"><span data-stu-id="8f2b4-152">From Clause</span></span>](../../../language-reference/queries/from-clause.md)
- [<span data-ttu-id="8f2b4-153">Where 子句</span><span class="sxs-lookup"><span data-stu-id="8f2b4-153">Where Clause</span></span>](../../../language-reference/queries/where-clause.md)
- [<span data-ttu-id="8f2b4-154">查詢</span><span class="sxs-lookup"><span data-stu-id="8f2b4-154">Queries</span></span>](../../../language-reference/queries/index.md)
- [<span data-ttu-id="8f2b4-155">使用 LINQ 轉換資料 (C#)</span><span class="sxs-lookup"><span data-stu-id="8f2b4-155">Data Transformations with LINQ (C#)</span></span>](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md)
