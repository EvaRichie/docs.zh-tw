---
title: FROM (Entity SQL)
ms.date: 03/30/2017
ms.assetid: ff3e3048-0d5d-4502-ae5c-9187fcbd0514
ms.openlocfilehash: 8affac82fb1813aa0282540b5dc2f47d42234a1b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91148047"
---
# <a name="from-entity-sql"></a><span data-ttu-id="5297d-102">FROM (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="5297d-102">FROM (Entity SQL)</span></span>

<span data-ttu-id="5297d-103">指定 [SELECT](select-entity-sql.md) 語句中使用的集合。</span><span class="sxs-lookup"><span data-stu-id="5297d-103">Specifies the collection used in [SELECT](select-entity-sql.md) statements.</span></span>

## <a name="syntax"></a><span data-ttu-id="5297d-104">語法</span><span class="sxs-lookup"><span data-stu-id="5297d-104">Syntax</span></span>

```sql
FROM expression [ ,...n ] AS C
```

## <a name="arguments"></a><span data-ttu-id="5297d-105">引數</span><span class="sxs-lookup"><span data-stu-id="5297d-105">Arguments</span></span>

`expression` \
<span data-ttu-id="5297d-106">任何有效的查詢運算式，該運算式可產生做為 `SELECT` 陳述式中之來源的集合。</span><span class="sxs-lookup"><span data-stu-id="5297d-106">Any valid query expression that yields a collection to use as a source in a `SELECT` statement.</span></span>

## <a name="remarks"></a><span data-ttu-id="5297d-107">備註</span><span class="sxs-lookup"><span data-stu-id="5297d-107">Remarks</span></span>

<span data-ttu-id="5297d-108">`FROM` 子句是一個或多個 `FROM` 子句項目的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="5297d-108">A `FROM` clause is a comma-separated list of one or more `FROM` clause items.</span></span> <span data-ttu-id="5297d-109">`FROM` 子句可以用來為 `SELECT` 陳述式指定一個或多個來源。</span><span class="sxs-lookup"><span data-stu-id="5297d-109">The `FROM` clause can be used to specify one or more sources for a `SELECT` statement.</span></span> <span data-ttu-id="5297d-110">`FROM` 子句最簡單的形式是單一查詢運算式，該運算式可識別做為 `SELECT` 陳述式中之來源的集合和別名 (Alias)，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5297d-110">The simplest form of a `FROM` clause is a single query expression that identifies a collection and an alias used as the source in a `SELECT` statement, as illustrated in the following example:</span></span>

`FROM C as c`

## <a name="from-clause-items"></a><span data-ttu-id="5297d-111">FROM 子句項目</span><span class="sxs-lookup"><span data-stu-id="5297d-111">FROM Clause Items</span></span>

<span data-ttu-id="5297d-112">每個 `FROM` 子句項目會參考 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢中的一個來源集合。</span><span class="sxs-lookup"><span data-stu-id="5297d-112">Each `FROM` clause item refers to a source collection in the [!INCLUDE[esql](../../../../../../includes/esql-md.md)] query.</span></span> [!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="5297d-113">支援下列 `FROM` 子句項目類別：簡單 `FROM` 子句項目、`JOIN FROM` 子句項目，以及 `APPLY FROM` 子句項目。</span><span class="sxs-lookup"><span data-stu-id="5297d-113">supports the following classes of `FROM` clause items: simple `FROM` clause items, `JOIN FROM` clause items, and `APPLY FROM` clause items.</span></span> <span data-ttu-id="5297d-114">下列章節將更詳細說明這些 `FROM` 子句項目。</span><span class="sxs-lookup"><span data-stu-id="5297d-114">Each of these `FROM` clause items is described in more detail in the following sections.</span></span>

### <a name="simple-from-clause-item"></a><span data-ttu-id="5297d-115">簡單 FROM 子句項目</span><span class="sxs-lookup"><span data-stu-id="5297d-115">Simple FROM Clause Item</span></span>

<span data-ttu-id="5297d-116">最簡單的 `FROM` 子句項目是可識別集合和別名的單一運算式。</span><span class="sxs-lookup"><span data-stu-id="5297d-116">The simplest `FROM` clause item is a single expression that identifies a collection and an alias.</span></span> <span data-ttu-id="5297d-117">運算式可以是實體集或子查詢，或是型別為集合的任何其他運算式。</span><span class="sxs-lookup"><span data-stu-id="5297d-117">The expression can simply be an entity set, or a subquery, or any other expression that is a collection type.</span></span> <span data-ttu-id="5297d-118">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="5297d-118">The following is an example:</span></span>

```sql
LOB.Customers as c
```

<span data-ttu-id="5297d-119">別名規格是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="5297d-119">The alias specification is optional.</span></span> <span data-ttu-id="5297d-120">上述 from 子句項目的替代規格可以是：</span><span class="sxs-lookup"><span data-stu-id="5297d-120">An alternate specification of the above from clause item could be the following:</span></span>

```sql
LOB.Customers
```

<span data-ttu-id="5297d-121">如果未指定別名，[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 會嘗試依據集合運算式產生別名。</span><span class="sxs-lookup"><span data-stu-id="5297d-121">If no alias is specified, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] attempts to generate an alias based on the collection expression.</span></span>

### <a name="join-from-clause-item"></a><span data-ttu-id="5297d-122">JOIN FROM 子句項目</span><span class="sxs-lookup"><span data-stu-id="5297d-122">JOIN FROM Clause Item</span></span>

<span data-ttu-id="5297d-123">`JOIN FROM` 子句項目代表介於兩個 `FROM` 子句項目之間的聯結。</span><span class="sxs-lookup"><span data-stu-id="5297d-123">A `JOIN FROM` clause item represents a join between two `FROM` clause items.</span></span> [!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="5297d-124">支援交叉聯結、內部聯結、左右外部連結，以及完整外部連結。</span><span class="sxs-lookup"><span data-stu-id="5297d-124">supports cross joins, inner joins, left and right outer joins, and full outer joins.</span></span> <span data-ttu-id="5297d-125">這些聯結的支援方式類似于 Transact-sql 中的支援。</span><span class="sxs-lookup"><span data-stu-id="5297d-125">All these joins are supported similar to the way that they are supported in Transact-SQL.</span></span> <span data-ttu-id="5297d-126">如同在 Transact-sql 中，與相關的兩個 `FROM` 子句專案 `JOIN` 必須是獨立的。</span><span class="sxs-lookup"><span data-stu-id="5297d-126">As in Transact-SQL, the two `FROM` clause items involved in the `JOIN` must be independent.</span></span> <span data-ttu-id="5297d-127">也就是不能相互關聯。</span><span class="sxs-lookup"><span data-stu-id="5297d-127">That is, they cannot be correlated.</span></span> <span data-ttu-id="5297d-128">`CROSS APPLY` 或 `OUTER APPLY` 適用於這些案例。</span><span class="sxs-lookup"><span data-stu-id="5297d-128">A `CROSS APPLY` or `OUTER APPLY` can be used for these cases.</span></span>

#### <a name="cross-joins"></a><span data-ttu-id="5297d-129">交叉聯結</span><span class="sxs-lookup"><span data-stu-id="5297d-129">Cross Joins</span></span>

<span data-ttu-id="5297d-130">`CROSS JOIN` 查詢運算式可產生兩個集合的笛卡兒乘積，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5297d-130">A `CROSS JOIN` query expression produces the Cartesian product of the two collections, as illustrated in the following example:</span></span>

`FROM C AS c CROSS JOIN D as d`

#### <a name="inner-joins"></a><span data-ttu-id="5297d-131">內部聯結</span><span class="sxs-lookup"><span data-stu-id="5297d-131">Inner Joins</span></span>

<span data-ttu-id="5297d-132">`INNER JOIN` 查詢運算式可產生兩個集合的受限笛卡兒乘積，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5297d-132">An `INNER JOIN` produces a constrained Cartesian product of the two collections, as illustrated in the following example:</span></span>

`FROM C AS c [INNER] JOIN D AS d ON e`

<span data-ttu-id="5297d-133">前述查詢運算式可對照右集合的每個項目處理左集合的每個項目的組合，其中 `ON` 條件為 true。</span><span class="sxs-lookup"><span data-stu-id="5297d-133">The previous query expression processes a combination of every element of the collection on the left paired against every element of the collection on the right, where the `ON` condition is true.</span></span> <span data-ttu-id="5297d-134">如果未指定 `ON` 條件，`INNER JOIN` 會退化成 `CROSS JOIN`。</span><span class="sxs-lookup"><span data-stu-id="5297d-134">If no `ON` condition is specified, an `INNER JOIN` degenerates to a `CROSS JOIN`.</span></span>

#### <a name="left-outer-joins-and-right-outer-joins"></a><span data-ttu-id="5297d-135">左外部聯結和右外部聯結</span><span class="sxs-lookup"><span data-stu-id="5297d-135">Left Outer Joins and Right Outer Joins</span></span>

<span data-ttu-id="5297d-136">`OUTER JOIN` 查詢運算式可產生兩個集合的受限笛卡兒乘積，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5297d-136">An `OUTER JOIN` query expression produces a constrained Cartesian product of the two collections, as illustrated in the following example:</span></span>

`FROM C AS c LEFT OUTER JOIN D AS d ON e`

<span data-ttu-id="5297d-137">前述查詢運算式可對照右集合的每個項目處理左集合的每個項目的組合，其中 `ON` 條件為 true。</span><span class="sxs-lookup"><span data-stu-id="5297d-137">The previous query expression processes a combination of every element of the collection on the left paired against every element of the collection on the right, where the `ON` condition is true.</span></span> <span data-ttu-id="5297d-138">如果 `ON` 條件為 false，該運算式仍會對照右項目處理左項目的單一例項，但其結果值會是 null。</span><span class="sxs-lookup"><span data-stu-id="5297d-138">If the `ON` condition is false, the expression still processes a single instance of the element on the left paired against the element on the right, with the value null.</span></span>

<span data-ttu-id="5297d-139">`RIGHT OUTER JOIN` 也可以用類似方式表示。</span><span class="sxs-lookup"><span data-stu-id="5297d-139">A `RIGHT OUTER JOIN` may be expressed in a similar manner.</span></span>

#### <a name="full-outer-joins"></a><span data-ttu-id="5297d-140">完整外部聯結</span><span class="sxs-lookup"><span data-stu-id="5297d-140">Full Outer Joins</span></span>

<span data-ttu-id="5297d-141">明確的 `FULL OUTER JOIN` 查詢運算式可產生兩個集合的受限笛卡兒乘積，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5297d-141">An explicit `FULL OUTER JOIN` produces a constrained Cartesian product of the two collections as illustrated in the following example:</span></span>

`FROM C AS c FULL OUTER JOIN D AS d ON e`

<span data-ttu-id="5297d-142">前述查詢運算式可對照右集合的每個項目處理左集合的每個項目的組合，其中 `ON` 條件為 true。</span><span class="sxs-lookup"><span data-stu-id="5297d-142">The previous query expression processes a combination of every element of the collection on the left paired against every element of the collection on the right, where the `ON` condition is true.</span></span> <span data-ttu-id="5297d-143">如果 `ON` 條件為 false，該運算式仍會對照右項目處理左項目的一個例項，但其結果值會是 null。</span><span class="sxs-lookup"><span data-stu-id="5297d-143">If the `ON` condition is false, the expression still processes one instance of the element on the left paired against the element on the right, with the value null.</span></span> <span data-ttu-id="5297d-144">如果也對照左項目處理右項目的一個例項，其結果值會是 null。</span><span class="sxs-lookup"><span data-stu-id="5297d-144">It also processes one instance of the element on the right paired against the element on the left, with the value null.</span></span>

> [!NOTE]
> <span data-ttu-id="5297d-145">為了維持與 SQL-92 的相容性，在 Transact-sql 中，外部關鍵字是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="5297d-145">To preserve compatibility with SQL-92, in Transact-SQL the OUTER keyword is optional.</span></span> <span data-ttu-id="5297d-146">因此，`LEFT JOIN`、`RIGHT JOIN` 和 `FULL JOIN` 是 `LEFT OUTER JOIN`、`RIGHT OUTER JOIN` 和 `FULL OUTER JOIN` 的同義字。</span><span class="sxs-lookup"><span data-stu-id="5297d-146">Therefore, `LEFT JOIN`, `RIGHT JOIN`, and `FULL JOIN` are synonyms for `LEFT OUTER JOIN`, `RIGHT OUTER JOIN`, and `FULL OUTER JOIN`.</span></span>

### <a name="apply-clause-item"></a><span data-ttu-id="5297d-147">APPLY Clause 子句項目</span><span class="sxs-lookup"><span data-stu-id="5297d-147">APPLY Clause Item</span></span>

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="5297d-148">可支援兩種 `APPLY`：`CROSS APPLY` 和 `OUTER APPLY`。</span><span class="sxs-lookup"><span data-stu-id="5297d-148">supports two kinds of `APPLY`: `CROSS APPLY` and `OUTER APPLY`.</span></span>

<span data-ttu-id="5297d-149">`CROSS APPLY` 會以評估右運算式產生之集合的項目來產生左集合的每個項目的唯一配對。</span><span class="sxs-lookup"><span data-stu-id="5297d-149">A `CROSS APPLY` produces a unique pairing of each element of the collection on the left with an element of the collection produced by evaluating the expression on the right.</span></span> <span data-ttu-id="5297d-150">使用 `CROSS APPLY`，右運算式的作用相依於左項目，如下列關聯的集合範例所示：</span><span class="sxs-lookup"><span data-stu-id="5297d-150">With a `CROSS APPLY`, the expression on the right is functionally dependent on the element on the left, as illustrated in the following associated collection example:</span></span>

`SELECT c, f FROM C AS c CROSS APPLY c.Assoc AS f`

<span data-ttu-id="5297d-151">`CROSS APPLY` 和聯結清單類似。</span><span class="sxs-lookup"><span data-stu-id="5297d-151">The behavior of `CROSS APPLY` is similar to the join list.</span></span> <span data-ttu-id="5297d-152">如果右運算式評估為空集合，`CROSS APPLY` 不會為左項目的那個例項產生配對。</span><span class="sxs-lookup"><span data-stu-id="5297d-152">If the expression on the right evaluates to an empty collection, the `CROSS APPLY` produces no pairings for that instance of the element on the left.</span></span>

<span data-ttu-id="5297d-153">`OUTER APPLY` 除了即使在右運算式評估為空集合時還是會產生配對之外，都跟 `CROSS APPLY` 類似。</span><span class="sxs-lookup"><span data-stu-id="5297d-153">An `OUTER APPLY` resembles a `CROSS APPLY`, except a pairing is still produced even when the expression on the right evaluates to an empty collection.</span></span> <span data-ttu-id="5297d-154">以下是 `OUTER APPLY` 的範例：</span><span class="sxs-lookup"><span data-stu-id="5297d-154">The following is an example of an `OUTER APPLY`:</span></span>

`SELECT c, f FROM C AS c OUTER APPLY c.Assoc AS f`

> [!NOTE]
> <span data-ttu-id="5297d-155">與 Transact-sql 不同的是，在中不需要明確的 unnest 步驟 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 。</span><span class="sxs-lookup"><span data-stu-id="5297d-155">Unlike in Transact-SQL, there is no need for an explicit unnest step in [!INCLUDE[esql](../../../../../../includes/esql-md.md)].</span></span>

> [!NOTE]
> <span data-ttu-id="5297d-156">`CROSS` 和 `OUTER APPLY` 運算子是在 SQL Server 2005 中引進。</span><span class="sxs-lookup"><span data-stu-id="5297d-156">`CROSS` and `OUTER APPLY` operators were introduced in SQL Server 2005.</span></span> <span data-ttu-id="5297d-157">在某些案例中，查詢管線可能產生含有 `CROSS APPLY` 和 (或) `OUTER APPLY` 運算子的 Transact-SQL。</span><span class="sxs-lookup"><span data-stu-id="5297d-157">In some cases, the query pipeline might produce Transact-SQL that contains `CROSS APPLY` and/or `OUTER APPLY` operators.</span></span> <span data-ttu-id="5297d-158">由於某些後端提供者（包括 SQL Server 2005 之前的 SQL Server 版本）不支援這些運算子，因此這類查詢無法在這些後端提供者上執行。</span><span class="sxs-lookup"><span data-stu-id="5297d-158">Because some backend providers, including versions of SQL Server earlier than SQL Server 2005, do not support these operators, such queries cannot be executed on these backend providers.</span></span>
>
> <span data-ttu-id="5297d-159">下列一些典型的案例可能導致 `CROSS APPLY` 和 (或) `OUTER APPLY` 運算子出現在輸出查詢中：AnyElement 是在相互關聯的子查詢之上或是在導覽產生的集合之上；在 LINQ 查詢中使用的群組方法接受元素選擇器；在查詢中明確指定 `CROSS APPLY` 或 `OUTER APPLY`；在查詢中的 `DEREF` 建構是在 `REF` 建構之上。</span><span class="sxs-lookup"><span data-stu-id="5297d-159">Some typical scenarios that might lead to the presence of `CROSS APPLY` and/or `OUTER APPLY` operators in the output query are the following: a correlated subquery with paging; AnyElement over a correlated subquery or over a collection produced by navigation; LINQ queries that use grouping methods that accept an element selector; a query in which a `CROSS APPLY` or an `OUTER APPLY` are explicitly specified; a query that has a `DEREF` construct over a `REF` construct.</span></span>

## <a name="multiple-collections-in-the-from-clause"></a><span data-ttu-id="5297d-160">FROM 子句中的多個集合</span><span class="sxs-lookup"><span data-stu-id="5297d-160">Multiple Collections in the FROM Clause</span></span>

<span data-ttu-id="5297d-161">`FROM` 子句可以包含一個以上的集合並用逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="5297d-161">The `FROM` clause can contain more than one collection separated by commas.</span></span> <span data-ttu-id="5297d-162">這些案例中假設集合聯結在一起。</span><span class="sxs-lookup"><span data-stu-id="5297d-162">In these cases, the collections are assumed to be joined together.</span></span> <span data-ttu-id="5297d-163">請將這些集合視為 n 向 CROSS JOIN。</span><span class="sxs-lookup"><span data-stu-id="5297d-163">Think of these as an n-way CROSS JOIN.</span></span>

<span data-ttu-id="5297d-164">在下列範例中， `C` 和是 `D` 獨立的集合，但 `c.Names` 相依于 `C` 。</span><span class="sxs-lookup"><span data-stu-id="5297d-164">In the following example, `C` and `D` are independent collections, but `c.Names` is dependent on `C`.</span></span>

```sql
FROM C AS c, D AS d, c.Names AS e
```

<span data-ttu-id="5297d-165">上一個範例在邏輯上等同於下列範例：</span><span class="sxs-lookup"><span data-stu-id="5297d-165">The previous example is logically equivalent to the following example:</span></span>

`FROM (C AS c JOIN D AS d) CROSS APPLY c.Names AS e`

## <a name="left-correlation"></a><span data-ttu-id="5297d-166">左方相互關聯</span><span class="sxs-lookup"><span data-stu-id="5297d-166">Left Correlation</span></span>

 <span data-ttu-id="5297d-167">`FROM` 子句可以參考之前子句中指定的項目。</span><span class="sxs-lookup"><span data-stu-id="5297d-167">Items in the `FROM` clause can refer to items specified in earlier clauses.</span></span> <span data-ttu-id="5297d-168">在下列範例中，`C` 和 `D` 是互為獨立的集合，但是 `c.Names` 相依於 `C`：</span><span class="sxs-lookup"><span data-stu-id="5297d-168">In the following example, `C` and `D` are independent collections, but `c.Names` is dependent on `C`:</span></span>

```sql
from C as c, D as d, c.Names as e
```

<span data-ttu-id="5297d-169">這在邏輯上等同於：</span><span class="sxs-lookup"><span data-stu-id="5297d-169">This is logically equivalent to:</span></span>

```sql
from (C as c join D as d) cross apply c.Names as e
```

## <a name="semantics"></a><span data-ttu-id="5297d-170">語意</span><span class="sxs-lookup"><span data-stu-id="5297d-170">Semantics</span></span>

<span data-ttu-id="5297d-171">就邏輯而言，`FROM` 子句中的項目被假設為 `n` 向交叉聯結的一部分 (單向交叉聯結的案例除外)。</span><span class="sxs-lookup"><span data-stu-id="5297d-171">Logically, the collections in the `FROM` clause are assumed to be part of an `n`-way cross join (except in the case of a 1-way cross join).</span></span> <span data-ttu-id="5297d-172">別名在 `FROM` 子句中的處理方向是由左至右，而且會被入至目前範圍，以供日後參考。</span><span class="sxs-lookup"><span data-stu-id="5297d-172">Aliases in the `FROM` clause are processed left to right, and are added to the current scope for later reference.</span></span> <span data-ttu-id="5297d-173">`FROM` 子句被假設為產生資料列的多重集 (Multiset)。</span><span class="sxs-lookup"><span data-stu-id="5297d-173">The `FROM` clause is assumed to produce a multiset of rows.</span></span> <span data-ttu-id="5297d-174">`FROM` 子句中的每個項目 (Item) 都會有一個欄位，其代表集合項目 (Item) 的單一項目 (Element)。</span><span class="sxs-lookup"><span data-stu-id="5297d-174">There will be one field for each item in the `FROM` clause that represents a single element from that collection item.</span></span>

<span data-ttu-id="5297d-175">`FROM` 子句在邏輯上會產生型別為 Row(c, d, e) 之資料列的多重集，其中 c、d 和 e 被假設為是 `C`、`D` 和 `c.Names` 的項目型別。</span><span class="sxs-lookup"><span data-stu-id="5297d-175">The `FROM` clause logically produces a multiset of rows of type Row(c, d, e) where fields c, d, and e are assumed to be of the element type of `C`, `D`, and `c.Names`.</span></span>

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] <span data-ttu-id="5297d-176">在範圍中會為每個簡單 `FROM` 子句引入別名。</span><span class="sxs-lookup"><span data-stu-id="5297d-176">introduces an alias for each simple `FROM` clause item in scope.</span></span> <span data-ttu-id="5297d-177">例如，下列 FROM 子句程式碼片段中引入範圍內的名稱是 c、d 和 e。</span><span class="sxs-lookup"><span data-stu-id="5297d-177">For example, in the following FROM clause snippet, The names introduced into scope are c, d, and e.</span></span>

```sql
from (C as c join D as d) cross apply c.Names as e
```

<span data-ttu-id="5297d-178">在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] (與 transact-sql) 不同的是， `FROM` 子句只會將別名引入範圍中。</span><span class="sxs-lookup"><span data-stu-id="5297d-178">In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] (unlike Transact-SQL), the `FROM` clause only introduces the aliases into scope.</span></span> <span data-ttu-id="5297d-179">對這些集合的資料行 (屬性) 的任何參考都必須以別名限定。</span><span class="sxs-lookup"><span data-stu-id="5297d-179">Any references to columns (properties) of these collections must be qualified with the alias.</span></span>

## <a name="pulling-up-keys-from-nested-queries"></a><span data-ttu-id="5297d-180">從巢狀查詢取出索引鍵</span><span class="sxs-lookup"><span data-stu-id="5297d-180">Pulling Up Keys from Nested Queries</span></span>

<span data-ttu-id="5297d-181">不支援某些需要從巢狀查詢取出索引鍵的查詢類型。</span><span class="sxs-lookup"><span data-stu-id="5297d-181">Certain types of queries that require pulling up keys from a nested query are not supported.</span></span> <span data-ttu-id="5297d-182">例如，以下是有效的查詢：</span><span class="sxs-lookup"><span data-stu-id="5297d-182">For example, the following query is valid:</span></span>

```sql
select c.Orders from Customers as c
```

<span data-ttu-id="5297d-183">但是，以下是無效的查詢，因為巢狀查詢沒有索引鍵：</span><span class="sxs-lookup"><span data-stu-id="5297d-183">However, the following query is not valid, because the nested query does not have any keys:</span></span>

```sql
select {1} from {2, 3}
```

## <a name="see-also"></a><span data-ttu-id="5297d-184">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5297d-184">See also</span></span>

- [<span data-ttu-id="5297d-185">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="5297d-185">Entity SQL Reference</span></span>](entity-sql-reference.md)
- [<span data-ttu-id="5297d-186">查詢運算式</span><span class="sxs-lookup"><span data-stu-id="5297d-186">Query Expressions</span></span>](query-expressions-entity-sql.md)
- [<span data-ttu-id="5297d-187">可為 Null 的結構類型</span><span class="sxs-lookup"><span data-stu-id="5297d-187">Nullable Structured Types</span></span>](nullable-structured-types-entity-sql.md)
