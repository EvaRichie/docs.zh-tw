---
title: GROUP BY (Entity SQL)
ms.date: 03/30/2017
ms.assetid: cf4f4972-4724-4945-ba44-943a08549139
ms.openlocfilehash: 281d5d2df389f0952f0552747fa12b67b14d470c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204485"
---
# <a name="group-by-entity-sql"></a><span data-ttu-id="710ee-102">GROUP BY (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="710ee-102">GROUP BY (Entity SQL)</span></span>

<span data-ttu-id="710ee-103">指定要放置查詢 ([SELECT](select-entity-sql.md)) 運算式所傳回物件的群組。</span><span class="sxs-lookup"><span data-stu-id="710ee-103">Specifies groups into which objects returned by a query ([SELECT](select-entity-sql.md)) expression are to be placed.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="710ee-104">語法</span><span class="sxs-lookup"><span data-stu-id="710ee-104">Syntax</span></span>  
  
```sql  
[ GROUP BY aliasedExpression [ ,...n ] ]  
```  
  
## <a name="arguments"></a><span data-ttu-id="710ee-105">引數</span><span class="sxs-lookup"><span data-stu-id="710ee-105">Arguments</span></span>  

 `aliasedExpression`  
 <span data-ttu-id="710ee-106">在其中執行群組作業的任何有效查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="710ee-106">Any valid query expression on which grouping is performed.</span></span> <span data-ttu-id="710ee-107">`expression` 可以是屬性，或參考 FROM 子句所傳回之屬性的非彙總運算式。</span><span class="sxs-lookup"><span data-stu-id="710ee-107">`expression` can be a property or a non-aggregate expression that references a property returned by the FROM clause.</span></span> <span data-ttu-id="710ee-108">GROUP BY 子句中的每一個運算式都必評估為可以比較是否相等的型別</span><span class="sxs-lookup"><span data-stu-id="710ee-108">Each expression in a GROUP BY clause must evaluate to a type that can be compared for equality.</span></span> <span data-ttu-id="710ee-109">這些型別通常是純量基本型別，例如數值、字串和日期。</span><span class="sxs-lookup"><span data-stu-id="710ee-109">These types are generally scalar primitives such as numbers, strings, and dates.</span></span> <span data-ttu-id="710ee-110">您不可依集合來群組。</span><span class="sxs-lookup"><span data-stu-id="710ee-110">You cannot group by a collection.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="710ee-111">備註</span><span class="sxs-lookup"><span data-stu-id="710ee-111">Remarks</span></span>  

 <span data-ttu-id="710ee-112">如果 SELECT 子句中包含彙總函式 \<select list> ，GROUP BY 會計算每個群組的摘要值。</span><span class="sxs-lookup"><span data-stu-id="710ee-112">If aggregate functions are included in the SELECT clause \<select list>, GROUP BY calculates a summary value for each group.</span></span> <span data-ttu-id="710ee-113">當指定 GROUP BY 時，GROUP BY 清單應該包括選取清單中之任何非彙總運算式中的每一個屬性名稱，否則，GROUP BY 運算式必須完全符合選取清單運算式。</span><span class="sxs-lookup"><span data-stu-id="710ee-113">When GROUP BY is specified, either each property name in any nonaggregate expression in the select list should be included in the GROUP BY list, or the GROUP BY expression must exactly match the select list expression.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="710ee-114">如果未指定 ORDER BY 子句，由 GROUP BY 子句傳回的群組將不會依照任何特定順序。</span><span class="sxs-lookup"><span data-stu-id="710ee-114">If the ORDER BY clause is not specified, groups returned by the GROUP BY clause are not in any particular order.</span></span> <span data-ttu-id="710ee-115">若要指定特定資料排序，建議您一律使用 ORDER BY 子句。</span><span class="sxs-lookup"><span data-stu-id="710ee-115">To specify a particular ordering of the data, we recommend that you always use the ORDER BY clause.</span></span>  
  
 <span data-ttu-id="710ee-116">以明確或隱含方式 (例如，利用查詢中的 HAVING 子句) 指定 GROUP BY 子句時，目前的範圍將會被隱藏，並且導入新的範圍。</span><span class="sxs-lookup"><span data-stu-id="710ee-116">When a GROUP BY clause is specified, either explicitly or implicitly (for example, by a HAVING clause in the query), the current scope is hidden, and a new scope is introduced.</span></span>  
  
 <span data-ttu-id="710ee-117">SELECT 子句、HAVING 子句和 ORDER BY 子句將無法再參考 FROM 子句中指定的項目名稱。</span><span class="sxs-lookup"><span data-stu-id="710ee-117">The SELECT clause, the HAVING clause, and the ORDER BY clause will no longer be able to refer to element names specified in the FROM clause.</span></span> <span data-ttu-id="710ee-118">您只能參考群組運算式本身。</span><span class="sxs-lookup"><span data-stu-id="710ee-118">You can only refer to the grouping expressions themselves.</span></span> <span data-ttu-id="710ee-119">如果要這樣處理，您可以指派新名稱 (別名) 給每一個群組運算式。</span><span class="sxs-lookup"><span data-stu-id="710ee-119">To do this, you can assign new names (aliases) to each grouping expression.</span></span> <span data-ttu-id="710ee-120">如果不為群組運算式指定別名， [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 會嘗試使用別名產生規則來產生別名，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="710ee-120">If no alias is specified for a grouping expression, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tries to generate one by using the alias generation rules, as illustrated in the following example.</span></span>  
  
 `SELECT g1, g2, ...gn FROM c as c1`  
  
 `GROUP BY e1 as g1, e2 as g2, ...en as gn`  
  
 <span data-ttu-id="710ee-121">GROUP BY 子句無法參考同一個 GROUP BY 子句中前面所定義的名稱。</span><span class="sxs-lookup"><span data-stu-id="710ee-121">Expressions in the GROUP BY clause cannot refer to names defined earlier in the same GROUP BY clause.</span></span>  
  
 <span data-ttu-id="710ee-122">除了群組名稱之外，您也可以在 SELECT 子句、HAVING 子句和 ORDER BY 子句中指定彙總。</span><span class="sxs-lookup"><span data-stu-id="710ee-122">In addition to grouping names, you can also specify aggregates in the SELECT clause, HAVING clause, and the ORDER BY clause.</span></span> <span data-ttu-id="710ee-123">彙總會包含針對群組的每一個項目評估的運算式。</span><span class="sxs-lookup"><span data-stu-id="710ee-123">An aggregate contains an expression that is evaluated for each element of the group.</span></span> <span data-ttu-id="710ee-124">彙總運算子會縮減所有這些運算式的值 (通常會縮減成單一值，但並非一定如此)。</span><span class="sxs-lookup"><span data-stu-id="710ee-124">The aggregate operator reduces the values of all these expressions (usually, but not always, into a single value).</span></span> <span data-ttu-id="710ee-125">彙總運算式可參考父範圍中的原始項目名稱變數，或由 GROUP BY 子句本身導入的任何新名稱。</span><span class="sxs-lookup"><span data-stu-id="710ee-125">The aggregate expression can make references to the original element names visible in the parent scope, or to any of the new names introduced by the GROUP BY clause itself.</span></span> <span data-ttu-id="710ee-126">雖然彙是出現在 SELECT 子句、HAVING 子句和 ORDER BY 子句中，不過它們實際上是在群組運算式的相同範圍內評估，如以下範例所述。</span><span class="sxs-lookup"><span data-stu-id="710ee-126">Although the aggregates appear in the SELECT clause, HAVING clause, and ORDER BY clause, they are actually evaluated under the same scope as the grouping expressions, as illustrated in the following example.</span></span>  
  
 `SELECT name, sum(o.Price * o.Quantity) as total`  
  
 `FROM orderLines as o`  
  
 `GROUP BY o.Product as name`  
  
 <span data-ttu-id="710ee-127">此查詢使用 GROUP BY 子句來產生所訂購的所有產品的成本報表，並依產品細分。</span><span class="sxs-lookup"><span data-stu-id="710ee-127">This query uses the GROUP BY clause to produce a report of the cost of all products ordered, broken down by product.</span></span> <span data-ttu-id="710ee-128">它將名稱 `name` 指定給產品當成群組運算式的一部分，然後在 SELECT 清單中參考該名稱。</span><span class="sxs-lookup"><span data-stu-id="710ee-128">It gives the name `name` to the product as part of the grouping expression, and then references that name in the SELECT list.</span></span> <span data-ttu-id="710ee-129">它也在 SELECT 清單中指定以內部方式參考訂單行價格和數量的彙總 `sum` 。</span><span class="sxs-lookup"><span data-stu-id="710ee-129">It also specifies the aggregate `sum` in the SELECT list that internally references the price and quantity of the order line.</span></span>  
  
 <span data-ttu-id="710ee-130">每個 GROUP By 索引鍵運算式至少要有一個輸入範圍的參考：</span><span class="sxs-lookup"><span data-stu-id="710ee-130">Each GROUP By key expression must have at least one reference to the input scope:</span></span>  
  
```sql  
SELECT FROM Persons as P  
GROUP BY Q + P   -- GOOD  
GROUP BY Q   -- BAD  
GROUP BY 1   -- BAD, a constant is not allowed  
```  
  
 <span data-ttu-id="710ee-131">如需使用 GROUP BY 的範例，請參閱 [HAVING](having-entity-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="710ee-131">For an example of using GROUP BY, see [HAVING](having-entity-sql.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="710ee-132">範例</span><span class="sxs-lookup"><span data-stu-id="710ee-132">Example</span></span>  

 <span data-ttu-id="710ee-133">以下 Entity SQL 查詢使用 GROUP BY 運算子指定查詢傳回的物件所在的群組。</span><span class="sxs-lookup"><span data-stu-id="710ee-133">The following Entity SQL query uses the GROUP BY operator to specify groups into which objects are returned by a query.</span></span> <span data-ttu-id="710ee-134">此查詢是根據 AdventureWorks Sales Model。</span><span class="sxs-lookup"><span data-stu-id="710ee-134">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="710ee-135">若要編譯及執行此查詢，請遵循以下步驟：</span><span class="sxs-lookup"><span data-stu-id="710ee-135">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="710ee-136">依照 how [to：執行傳回 PrimitiveType 結果的查詢](../how-to-execute-a-query-that-returns-primitivetype-results.md)中的程式操作。</span><span class="sxs-lookup"><span data-stu-id="710ee-136">Follow the procedure in [How to: Execute a Query that Returns PrimitiveType Results](../how-to-execute-a-query-that-returns-primitivetype-results.md).</span></span>  
  
2. <span data-ttu-id="710ee-137">將下列查詢當成引數，傳遞至 `ExecutePrimitiveTypeQuery` 方法：</span><span class="sxs-lookup"><span data-stu-id="710ee-137">Pass the following query as an argument to the `ExecutePrimitiveTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#GROUPBY](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#groupby)]  
  
## <a name="see-also"></a><span data-ttu-id="710ee-138">另請參閱</span><span class="sxs-lookup"><span data-stu-id="710ee-138">See also</span></span>

- [<span data-ttu-id="710ee-139">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="710ee-139">Entity SQL Reference</span></span>](entity-sql-reference.md)
- [<span data-ttu-id="710ee-140">查詢運算式</span><span class="sxs-lookup"><span data-stu-id="710ee-140">Query Expressions</span></span>](query-expressions-entity-sql.md)
