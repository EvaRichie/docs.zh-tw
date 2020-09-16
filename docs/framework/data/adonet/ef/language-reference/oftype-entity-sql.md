---
title: OFTYPE (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 6d259ca7-bbf0-40f8-a154-181d25c0d67e
ms.openlocfilehash: 375fe9ce52ae290c175e42276b6b526766f6699c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90547508"
---
# <a name="oftype-entity-sql"></a><span data-ttu-id="6f33f-102">OFTYPE (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="6f33f-102">OFTYPE (Entity SQL)</span></span>
<span data-ttu-id="6f33f-103">從屬於特定型別的查詢運算式中傳回物件的集合。</span><span class="sxs-lookup"><span data-stu-id="6f33f-103">Returns a collection of objects from a query expression that is of a specific type.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6f33f-104">語法</span><span class="sxs-lookup"><span data-stu-id="6f33f-104">Syntax</span></span>  
  
```sql  
OFTYPE ( expression, [ONLY] test_type )  
```  
  
## <a name="arguments"></a><span data-ttu-id="6f33f-105">引數</span><span class="sxs-lookup"><span data-stu-id="6f33f-105">Arguments</span></span>  
 `expression`  
 <span data-ttu-id="6f33f-106">傳回物件集合的任何有效查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="6f33f-106">Any valid query expression that returns a collection of objects.</span></span>  
  
 `test_type`  
 <span data-ttu-id="6f33f-107">據以測試 `expression` 所傳回之每個物件的型別。</span><span class="sxs-lookup"><span data-stu-id="6f33f-107">The type to test each object returned by `expression` against.</span></span> <span data-ttu-id="6f33f-108">此型別必須以命名空間 (Namespace) 限定。</span><span class="sxs-lookup"><span data-stu-id="6f33f-108">The type must be qualified by a namespace.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="6f33f-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="6f33f-109">Return Value</span></span>  
 <span data-ttu-id="6f33f-110">屬於 `test_type`型別的物件集合，或是 `test_type`之基底型別 (Base Type) 或衍生型別 (Derived Type) 的物件集合。</span><span class="sxs-lookup"><span data-stu-id="6f33f-110">A collection of objects that are of type `test_type`, or a base type or derived type of `test_type`.</span></span> <span data-ttu-id="6f33f-111">如果指定了 ONLY，就只會傳回 `test_type` 的執行個體 (Instance) 或空白集合。</span><span class="sxs-lookup"><span data-stu-id="6f33f-111">If ONLY is specified, only instances of the `test_type` or an empty collection will be returned.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="6f33f-112">備註</span><span class="sxs-lookup"><span data-stu-id="6f33f-112">Remarks</span></span>  
 <span data-ttu-id="6f33f-113">`OFTYPE` 運算式會指定針對集合的每個項目執行型別測試所發出的型別運算式。</span><span class="sxs-lookup"><span data-stu-id="6f33f-113">An `OFTYPE` expression specifies a type expression that is issued to perform a type test against each element of a collection.</span></span>  <span data-ttu-id="6f33f-114">`OFTYPE` 運算式會產生指定之型別的新集合，其中僅包含相當於該型別或其子型別的項目。</span><span class="sxs-lookup"><span data-stu-id="6f33f-114">The `OFTYPE` expression produces a new collection of the specified type containing only those elements that were either equivalent to that type or a sub-type of it.</span></span>  
  
 <span data-ttu-id="6f33f-115">`OFTYPE` 運算式是下列查詢運算式的縮寫：</span><span class="sxs-lookup"><span data-stu-id="6f33f-115">An `OFTYPE` expression is an abbreviation of the following query expression:</span></span>  
  
```sql  
select value treat(t as T) from ts as t where t is of (T)  
```  
  
 <span data-ttu-id="6f33f-116">假設 Manager 是 Employee 的子型別，下列運算式就會從員工集合中產生只有主管的集合：</span><span class="sxs-lookup"><span data-stu-id="6f33f-116">Given that a Manager is a subtype of Employee, the following expression produces a collection of only managers from a collection of employees:</span></span>  
  
```sql  
OfType(employees, NamespaceName.Manager)  
```  
  
 <span data-ttu-id="6f33f-117">您也可以使用型別篩選來向上轉型集合：</span><span class="sxs-lookup"><span data-stu-id="6f33f-117">It is also possible to up cast a collection using the type filter:</span></span>  
  
```sql
OfType(executives, NamespaceName.Manager)  
```  
  
 <span data-ttu-id="6f33f-118">因為所有經理都是主管，所以產生的集合仍然會包含所有原始經理，但是此集合現在的型別會成為主管的集合。</span><span class="sxs-lookup"><span data-stu-id="6f33f-118">Since all executives are managers, the resulting collection still contains all the original executives, though the collection is now typed as a collection of managers.</span></span>  
  
 <span data-ttu-id="6f33f-119">下表所示為 `OFTYPE` 運算子在某些模式上的行為。</span><span class="sxs-lookup"><span data-stu-id="6f33f-119">The following table shows the behavior of the `OFTYPE` operator over some patterns.</span></span> <span data-ttu-id="6f33f-120">所有例外狀況 (Exception) 都是在叫用 (Invoke) 提供者之前從用戶端擲回：</span><span class="sxs-lookup"><span data-stu-id="6f33f-120">All exceptions are thrown from the client side before the provider is invoked:</span></span>  
  
|<span data-ttu-id="6f33f-121">模式</span><span class="sxs-lookup"><span data-stu-id="6f33f-121">Pattern</span></span>|<span data-ttu-id="6f33f-122">行為</span><span class="sxs-lookup"><span data-stu-id="6f33f-122">Behavior</span></span>|  
|-------------|--------------|  
|<span data-ttu-id="6f33f-123">OFTYPE(Collection(EntityType), EntityType)</span><span class="sxs-lookup"><span data-stu-id="6f33f-123">OFTYPE(Collection(EntityType), EntityType)</span></span>|<span data-ttu-id="6f33f-124">Collection(EntityType)</span><span class="sxs-lookup"><span data-stu-id="6f33f-124">Collection(EntityType)</span></span>|  
|<span data-ttu-id="6f33f-125">OFTYPE(Collection(ComplexType), ComplexType)</span><span class="sxs-lookup"><span data-stu-id="6f33f-125">OFTYPE(Collection(ComplexType), ComplexType)</span></span>|<span data-ttu-id="6f33f-126">擲回</span><span class="sxs-lookup"><span data-stu-id="6f33f-126">Throws</span></span>|  
|<span data-ttu-id="6f33f-127">OFTYPE(Collection(RowType), RowType)</span><span class="sxs-lookup"><span data-stu-id="6f33f-127">OFTYPE(Collection(RowType), RowType)</span></span>|<span data-ttu-id="6f33f-128">擲回</span><span class="sxs-lookup"><span data-stu-id="6f33f-128">Throws</span></span>|  
  
## <a name="example"></a><span data-ttu-id="6f33f-129">範例</span><span class="sxs-lookup"><span data-stu-id="6f33f-129">Example</span></span>  
 <span data-ttu-id="6f33f-130">下列 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢使用 OFTYPE 運算子，從 Course 物件集合傳回 OnsiteCourse 物件集合。</span><span class="sxs-lookup"><span data-stu-id="6f33f-130">The following [!INCLUDE[esql](../../../../../../includes/esql-md.md)] query uses the OFTYPE operator to return a collection of OnsiteCourse objects from a collection of Course objects.</span></span> <span data-ttu-id="6f33f-131">此查詢是以 [School Model](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100))為基礎。</span><span class="sxs-lookup"><span data-stu-id="6f33f-131">The query is based on the [School Model](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)).</span></span>  
  
 [!code-sql[DP EntityServices Concepts#OFTYPE](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#oftype)]  
  
## <a name="see-also"></a><span data-ttu-id="6f33f-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6f33f-132">See also</span></span>

- [<span data-ttu-id="6f33f-133">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="6f33f-133">Entity SQL Reference</span></span>](entity-sql-reference.md)
