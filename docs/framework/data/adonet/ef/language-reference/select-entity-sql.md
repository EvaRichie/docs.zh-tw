---
title: SELECT (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 9a33bd0d-ded1-41e7-ba3c-305502755e3b
ms.openlocfilehash: 860e2a9a3e484e8d09cad282be8c0126c8235b46
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202210"
---
# <a name="select-entity-sql"></a><span data-ttu-id="bc780-102">SELECT (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="bc780-102">SELECT (Entity SQL)</span></span>

<span data-ttu-id="bc780-103">指定查詢要傳回的項目。</span><span class="sxs-lookup"><span data-stu-id="bc780-103">Specifies the elements returned by a query.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="bc780-104">語法</span><span class="sxs-lookup"><span data-stu-id="bc780-104">Syntax</span></span>  
  
```sql  
SELECT [ ALL | DISTINCT ] [ topSubclause ] aliasedExpr
      [{ , aliasedExpr }] FROM fromClause [ WHERE whereClause ] [ GROUP BY groupByClause [ HAVING havingClause ] ] [ ORDER BY orderByClause ]  
-- or  
SELECT VALUE [ ALL | DISTINCT ] [ topSubclause ] expr FROM fromClause [ WHERE whereClause ] [ GROUP BY groupByClause [ HAVING havingClause ] ] [ ORDER BY orderByClause  
```  
  
## <a name="arguments"></a><span data-ttu-id="bc780-105">引數</span><span class="sxs-lookup"><span data-stu-id="bc780-105">Arguments</span></span>  

 <span data-ttu-id="bc780-106">ALL</span><span class="sxs-lookup"><span data-stu-id="bc780-106">ALL</span></span>  
 <span data-ttu-id="bc780-107">指定結果集可以出現重複的項目。</span><span class="sxs-lookup"><span data-stu-id="bc780-107">Specifies that duplicates can appear in the result set.</span></span> <span data-ttu-id="bc780-108">ALL 是預設值。</span><span class="sxs-lookup"><span data-stu-id="bc780-108">ALL is the default.</span></span>  
  
 <span data-ttu-id="bc780-109">DISTINCT</span><span class="sxs-lookup"><span data-stu-id="bc780-109">DISTINCT</span></span>  
 <span data-ttu-id="bc780-110">指定結果集只能出現唯一的結果。</span><span class="sxs-lookup"><span data-stu-id="bc780-110">Specifies that only unique results can appear in the result set.</span></span>  
  
 <span data-ttu-id="bc780-111">值</span><span class="sxs-lookup"><span data-stu-id="bc780-111">VALUE</span></span>  
 <span data-ttu-id="bc780-112">只允許指定一個項目，而且不加入資料列包裝函式。</span><span class="sxs-lookup"><span data-stu-id="bc780-112">Allows only one item to be specified, and does not add on a row wrapper.</span></span>  
  
 `topSubclause`  
 <span data-ttu-id="bc780-113">表示查詢所傳回第一組結果的數目，格式為 `top(expr)`。</span><span class="sxs-lookup"><span data-stu-id="bc780-113">Any valid expression that indicates the number of first results to return from the query, of the form `top(expr)`.</span></span>  
  
 <span data-ttu-id="bc780-114">[ORDER BY](order-by-entity-sql.md)運算子的 LIMIT 參數也可以讓您選取結果集中的前 n 個專案。</span><span class="sxs-lookup"><span data-stu-id="bc780-114">The LIMIT parameter of the [ORDER BY](order-by-entity-sql.md) operator also lets you select the first n items in the result set.</span></span>  
  
 `aliasedExpr`  
 <span data-ttu-id="bc780-115">以下格式的運算式：</span><span class="sxs-lookup"><span data-stu-id="bc780-115">An expression of the form:</span></span>  
  
 <span data-ttu-id="bc780-116">`expr` as `identifier` &#124; `expr`</span><span class="sxs-lookup"><span data-stu-id="bc780-116">`expr` as `identifier` &#124; `expr`</span></span>  
  
 `expr`  
 <span data-ttu-id="bc780-117">常值或運算式。</span><span class="sxs-lookup"><span data-stu-id="bc780-117">A literal or expression.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="bc780-118">備註</span><span class="sxs-lookup"><span data-stu-id="bc780-118">Remarks</span></span>  

 <span data-ttu-id="bc780-119">SELECT 子句會在已評估 [FROM](from-entity-sql.md)、 [GROUP BY](group-by-entity-sql.md)和 [HAVING](having-entity-sql.md) 子句之後進行評估。</span><span class="sxs-lookup"><span data-stu-id="bc780-119">The SELECT clause is evaluated after the [FROM](from-entity-sql.md), [GROUP BY](group-by-entity-sql.md), and [HAVING](having-entity-sql.md) clauses have been evaluated.</span></span> <span data-ttu-id="bc780-120">SELECT 子句只可參考目前範圍內 (來自 FROM 子句，或來自外部範圍) 的項目。</span><span class="sxs-lookup"><span data-stu-id="bc780-120">The SELECT clause can only refer to items currently in-scope (from the FROM clause, or from outer scopes).</span></span> <span data-ttu-id="bc780-121">如果指定了 GROUP BY 子句，SELECT 子句只可參考 GROUP BY 索引鍵的別名。</span><span class="sxs-lookup"><span data-stu-id="bc780-121">If a GROUP BY clause has been specified, the SELECT clause is only allowed to reference the aliases for the GROUP BY keys.</span></span> <span data-ttu-id="bc780-122">只允許在彙總函式中參考 FROM 子句項目。</span><span class="sxs-lookup"><span data-stu-id="bc780-122">Referring to the FROM clause items is only permitted in aggregate functions.</span></span>  
  
 <span data-ttu-id="bc780-123">位於 SELECT 關鍵字之後的一或多個查詢運算式就是所謂的選取清單，較正式的名稱則是投影。</span><span class="sxs-lookup"><span data-stu-id="bc780-123">The list of one or more query expressions following the SELECT keyword is known as the select list, or more formally as the projection.</span></span> <span data-ttu-id="bc780-124">投影最常見的形式是單一查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="bc780-124">The most general form of projection is a single query expression.</span></span> <span data-ttu-id="bc780-125">如果從集合 `member1` 選取成員 `collection1`，將會針對 `member1` 中的每一個物件產生所有 `collection1`值的新集合，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="bc780-125">If you select a member `member1` from a collection `collection1`, you will produce a new collection of all the `member1` values for each object in `collection1`, as illustrated in the following example.</span></span>  
  
```sql  
SELECT collection1.member1 FROM collection1  
```  
  
 <span data-ttu-id="bc780-126">例如，假設 `customers` 是 `Customer` 型別的集合，而後者具有 `Name` 型別的屬性 `string`，那麼從 `Name` 選取 `customers` 將會產生字串的集合，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="bc780-126">For example, if `customers` is a collection of type `Customer` that has a property `Name` that is of type `string`, selecting `Name` from `customers` will yield a collection of strings, as illustrated in the following example.</span></span>  
  
```sql  
SELECT customers.Name FROM customers AS c  
```  
  
 <span data-ttu-id="bc780-127">您也可以使用 JOIN 語法 (FULL、INNER、LEFT、OUTER、ON 和 RIGHT)。</span><span class="sxs-lookup"><span data-stu-id="bc780-127">It is also possible to use JOIN syntax (FULL, INNER, LEFT, OUTER, ON, and RIGHT).</span></span> <span data-ttu-id="bc780-128">ON 是內部聯結的必要項，但不可使用於交叉聯結。</span><span class="sxs-lookup"><span data-stu-id="bc780-128">ON is required for inner joins and is nto allowed for cross joins.</span></span>  
  
## <a name="row-and-value-select-clauses"></a><span data-ttu-id="bc780-129">資料列選取和值選取子句</span><span class="sxs-lookup"><span data-stu-id="bc780-129">Row and Value Select Clauses</span></span>  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="bc780-130">支援兩種 SELECT 子句的變異形式。</span><span class="sxs-lookup"><span data-stu-id="bc780-130">supports two variants of the SELECT clause.</span></span> <span data-ttu-id="bc780-131">第一個 variant、row select、是由 SELECT 關鍵字來識別，而且可以用來指定一個或多個應該投射出的值。因為資料列包裝函式是以隱含方式在傳回的值周圍加入，所以查詢運算式的結果一律是資料列的多重集。</span><span class="sxs-lookup"><span data-stu-id="bc780-131">The first variant, row select, is identified by the SELECT keyword, and can be used to specify one or more values that should be projected out. Because a row wrapper is implicitly added around the values returned, the result of the query expression is always a multiset of rows.</span></span>  
  
 <span data-ttu-id="bc780-132">資料列選取中的每一個查詢運算式必須指定一個別名。</span><span class="sxs-lookup"><span data-stu-id="bc780-132">Each query expression in a row select must specify an alias.</span></span> <span data-ttu-id="bc780-133">如果未指定別名，[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 會嘗試依據別名產生規則產生別名。</span><span class="sxs-lookup"><span data-stu-id="bc780-133">If no alias is specified,[!INCLUDE[esql](../../../../../../includes/esql-md.md)] attempts to generate an alias by using the alias generation rules.</span></span>  
  
 <span data-ttu-id="bc780-134">SELECT 子句的另一種變異形式是由 SELECT VALUE 關鍵字識別的值選取。</span><span class="sxs-lookup"><span data-stu-id="bc780-134">The other variant of the SELECT clause, value select, is identified by the SELECT VALUE keyword.</span></span> <span data-ttu-id="bc780-135">它只允許指定一個值，而且不加入資料列包裝函式。</span><span class="sxs-lookup"><span data-stu-id="bc780-135">It allows only one value to be specified, and does not add a row wrapper.</span></span>  
  
 <span data-ttu-id="bc780-136">資料列選取永遠可以用 VALUE SELECT 的方式表示，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="bc780-136">A row select is always expressible in terms of VALUE SELECT, as illustrated in the following example.</span></span>  
  
```sql  
SELECT 1 AS a, "abc" AS b FROM C  
SELECT VALUE ROW(1 AS a, "abc" AS b) FROM C
```  
  
## <a name="all-and-distinct-modifiers"></a><span data-ttu-id="bc780-137">All 和 Distinct 修飾詞</span><span class="sxs-lookup"><span data-stu-id="bc780-137">All and Distinct Modifiers</span></span>  

 <span data-ttu-id="bc780-138">[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中這兩種 SELECT 的變異形式都可以指定 ALL 或 DISTINCT 修飾詞。</span><span class="sxs-lookup"><span data-stu-id="bc780-138">Both variants of SELECT in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] allow the specification of an ALL or DISTINCT modifier.</span></span> <span data-ttu-id="bc780-139">如果指定了 DISTINCT 修飾詞，便會從查詢運算式 (到 SELECT 子句為止) 產生的集合中排除重複項目。</span><span class="sxs-lookup"><span data-stu-id="bc780-139">If the DISTINCT modifier is specified, duplicates are eliminated from the collection produced by the query expression (up to and including the SELECT clause).</span></span> <span data-ttu-id="bc780-140">如果指定了 ALL 修飾詞，就不會執行排除重複項目；ALL 是預設值。</span><span class="sxs-lookup"><span data-stu-id="bc780-140">If the ALL modifier is specified, no duplicate elimination is performed; ALL is the default.</span></span>  
  
## <a name="differences-from-transact-sql"></a><span data-ttu-id="bc780-141">與 Transact-SQL 的差異</span><span class="sxs-lookup"><span data-stu-id="bc780-141">Differences from Transact-SQL</span></span>  

 <span data-ttu-id="bc780-142">[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 與 Transact-SQL 的差異在於它不支援在 SELECT 子句中使用 \* 引數。</span><span class="sxs-lookup"><span data-stu-id="bc780-142">Unlike Transact-SQL, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] does not support use of the \* argument in the SELECT clause.</span></span>  <span data-ttu-id="bc780-143">[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 會從 FROM 子句參考集合別名，用此方式讓查詢投影出整個記錄，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="bc780-143">Instead, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] allows queries to project out entire records by referencing the collection aliases from the FROM clause, as illustrated in the following example.</span></span>  
  
```sql  
SELECT * FROM T1, T2  
```  
  
 <span data-ttu-id="bc780-144">先前的 Transact-SQL 查詢運算式會以 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 下列方式表示。</span><span class="sxs-lookup"><span data-stu-id="bc780-144">The previous Transact-SQL query expression is expressed in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] in the following way.</span></span>  
  
```sql  
SELECT a1, a2 FROM T1 AS a1, T2 AS a2  
```  
  
## <a name="example"></a><span data-ttu-id="bc780-145">範例</span><span class="sxs-lookup"><span data-stu-id="bc780-145">Example</span></span>  

 <span data-ttu-id="bc780-146">以下 Entity SQL 查詢使用 SELECT 運算子指定查詢要傳回的項目。</span><span class="sxs-lookup"><span data-stu-id="bc780-146">The following Entity SQL query uses the SELECT operator to specify the elements to be returned by a query.</span></span> <span data-ttu-id="bc780-147">此查詢是根據 AdventureWorks Sales Model。</span><span class="sxs-lookup"><span data-stu-id="bc780-147">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="bc780-148">若要編譯及執行此查詢，請遵循以下步驟：</span><span class="sxs-lookup"><span data-stu-id="bc780-148">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="bc780-149">遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。</span><span class="sxs-lookup"><span data-stu-id="bc780-149">Follow the procedure in [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span></span>  
  
2. <span data-ttu-id="bc780-150">將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：</span><span class="sxs-lookup"><span data-stu-id="bc780-150">Pass the following query as an argument to the `ExecuteStructuralTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#LESS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#less)]  
  
## <a name="see-also"></a><span data-ttu-id="bc780-151">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bc780-151">See also</span></span>

- [<span data-ttu-id="bc780-152">查詢運算式</span><span class="sxs-lookup"><span data-stu-id="bc780-152">Query Expressions</span></span>](query-expressions-entity-sql.md)
- [<span data-ttu-id="bc780-153">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="bc780-153">Entity SQL Reference</span></span>](entity-sql-reference.md)
- [<span data-ttu-id="bc780-154">頂端</span><span class="sxs-lookup"><span data-stu-id="bc780-154">TOP</span></span>](top-entity-sql.md)
