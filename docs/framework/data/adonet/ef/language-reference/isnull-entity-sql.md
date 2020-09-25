---
title: ISNULL (Entity SQL)
ms.date: 03/30/2017
ms.assetid: dc7a0173-3664-4c90-a57b-5cbb0a8ed7ee
ms.openlocfilehash: 3360ad4ca7306a8cc1b7d6948204f825ff9a93c6
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203614"
---
# <a name="isnull-entity-sql"></a><span data-ttu-id="d42b5-102">ISNULL (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="d42b5-102">ISNULL (Entity SQL)</span></span>

<span data-ttu-id="d42b5-103">判斷查詢運算式是否為 null。</span><span class="sxs-lookup"><span data-stu-id="d42b5-103">Determines if a query expression is null.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d42b5-104">語法</span><span class="sxs-lookup"><span data-stu-id="d42b5-104">Syntax</span></span>  
  
```sql  
expression IS [ NOT ] NULL  
```  
  
## <a name="arguments"></a><span data-ttu-id="d42b5-105">引數</span><span class="sxs-lookup"><span data-stu-id="d42b5-105">Arguments</span></span>  

 `expression`  
 <span data-ttu-id="d42b5-106">任何有效的查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="d42b5-106">Any valid query expression.</span></span> <span data-ttu-id="d42b5-107">不可為集合、不可有集合成員，也不可為集合型別屬性的記錄型別。</span><span class="sxs-lookup"><span data-stu-id="d42b5-107">Cannot be a collection, have collection members, or a record type with collection type properties.</span></span>  
  
 <span data-ttu-id="d42b5-108">NOT</span><span class="sxs-lookup"><span data-stu-id="d42b5-108">NOT</span></span>  
 <span data-ttu-id="d42b5-109">否定 IS NULL 的 EDM.Boolean 結果。</span><span class="sxs-lookup"><span data-stu-id="d42b5-109">Negates the EDM.Boolean result of IS NULL.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="d42b5-110">傳回值</span><span class="sxs-lookup"><span data-stu-id="d42b5-110">Return Value</span></span>  

 <span data-ttu-id="d42b5-111">如果 `true` 傳回 null 則為 `expression`；否則為 `false`。</span><span class="sxs-lookup"><span data-stu-id="d42b5-111">`true` if `expression` returns null; otherwise, `false`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d42b5-112">備註</span><span class="sxs-lookup"><span data-stu-id="d42b5-112">Remarks</span></span>  

 <span data-ttu-id="d42b5-113">使用 `IS NULL` 判斷外部連結的項目是否為 null：</span><span class="sxs-lookup"><span data-stu-id="d42b5-113">Use `IS NULL` to determine if the element of an outer join is null:</span></span>  
  
```sql  
select c
      from LOB.Customers as c left outer join LOB.Orders as o
                              on c.ID = o.CustomerID
      where o is not null and o.OrderQuantity = @x  
```  
  
 <span data-ttu-id="d42b5-114">使用 `IS NULL` 判斷成員是否有實際值：</span><span class="sxs-lookup"><span data-stu-id="d42b5-114">Use `IS NULL` to determine if a member has an actual value:</span></span>  
  
```sql  
select c from LOB.Customer as c where c.DOB is not null  
```  
  
 <span data-ttu-id="d42b5-115">下表所示為 `IS NULL` 在某些模式上的行為。</span><span class="sxs-lookup"><span data-stu-id="d42b5-115">The following table shows the behavior of `IS NULL` over some patterns.</span></span> <span data-ttu-id="d42b5-116">所有例外狀況都是在叫用提供者之前從用戶端擲回：</span><span class="sxs-lookup"><span data-stu-id="d42b5-116">All exceptions are thrown from the client side before the provider gets invoked:</span></span>  
  
|<span data-ttu-id="d42b5-117">模式</span><span class="sxs-lookup"><span data-stu-id="d42b5-117">Pattern</span></span>|<span data-ttu-id="d42b5-118">行為</span><span class="sxs-lookup"><span data-stu-id="d42b5-118">Behavior</span></span>|  
|-------------|--------------|  
|<span data-ttu-id="d42b5-119">null IS NULL</span><span class="sxs-lookup"><span data-stu-id="d42b5-119">null IS NULL</span></span>|<span data-ttu-id="d42b5-120">傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="d42b5-120">Returns `true`.</span></span>|  
|<span data-ttu-id="d42b5-121">TREAT (null AS EntityType) IS NULL</span><span class="sxs-lookup"><span data-stu-id="d42b5-121">TREAT (null AS EntityType) IS NULL</span></span>|<span data-ttu-id="d42b5-122">傳回 `true`。</span><span class="sxs-lookup"><span data-stu-id="d42b5-122">Returns `true`.</span></span>|  
|<span data-ttu-id="d42b5-123">TREAT (null AS ComplexType) IS NULL</span><span class="sxs-lookup"><span data-stu-id="d42b5-123">TREAT (null AS ComplexType) IS NULL</span></span>|<span data-ttu-id="d42b5-124">擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="d42b5-124">Throws an error.</span></span>|  
|<span data-ttu-id="d42b5-125">TREAT (null AS RowType) IS NULL</span><span class="sxs-lookup"><span data-stu-id="d42b5-125">TREAT (null AS RowType) IS NULL</span></span>|<span data-ttu-id="d42b5-126">擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="d42b5-126">Throws an error.</span></span>|  
|<span data-ttu-id="d42b5-127">EntityType IS NULL</span><span class="sxs-lookup"><span data-stu-id="d42b5-127">EntityType IS NULL</span></span>|<span data-ttu-id="d42b5-128">傳回 `true` 或 `false`。</span><span class="sxs-lookup"><span data-stu-id="d42b5-128">Returns `true` or `false`.</span></span>|  
|<span data-ttu-id="d42b5-129">ComplexType IS NULL</span><span class="sxs-lookup"><span data-stu-id="d42b5-129">ComplexType IS NULL</span></span>|<span data-ttu-id="d42b5-130">擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="d42b5-130">Throws an error.</span></span>|  
|<span data-ttu-id="d42b5-131">RowType IS NULL</span><span class="sxs-lookup"><span data-stu-id="d42b5-131">RowType IS NULL</span></span>|<span data-ttu-id="d42b5-132">擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="d42b5-132">Throws an error.</span></span>|  
  
## <a name="example"></a><span data-ttu-id="d42b5-133">範例</span><span class="sxs-lookup"><span data-stu-id="d42b5-133">Example</span></span>  

 <span data-ttu-id="d42b5-134">下列 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢會使用 NOT null 運算子來判斷查詢運算式是否不是 null。</span><span class="sxs-lookup"><span data-stu-id="d42b5-134">The following [!INCLUDE[esql](../../../../../../includes/esql-md.md)] query uses the IS NOT NULL operator to determine if a query expression is not null.</span></span> <span data-ttu-id="d42b5-135">此查詢是根據 AdventureWorks Sales Model。</span><span class="sxs-lookup"><span data-stu-id="d42b5-135">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="d42b5-136">若要編譯及執行此查詢，請遵循以下步驟：</span><span class="sxs-lookup"><span data-stu-id="d42b5-136">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="d42b5-137">遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。</span><span class="sxs-lookup"><span data-stu-id="d42b5-137">Follow the procedure in [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span></span>  
  
2. <span data-ttu-id="d42b5-138">將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：</span><span class="sxs-lookup"><span data-stu-id="d42b5-138">Pass the following query as an argument to the `ExecuteStructuralTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#ISNULL](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#isnull)]  
  
## <a name="see-also"></a><span data-ttu-id="d42b5-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d42b5-139">See also</span></span>

- [<span data-ttu-id="d42b5-140">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="d42b5-140">Entity SQL Reference</span></span>](entity-sql-reference.md)
