---
title: CAST (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 07b6d750-dfd4-48a9-b86c-3badcbba6f70
ms.openlocfilehash: 5591f1947963dde45d34ad2342485af476765709
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91198010"
---
# <a name="cast-entity-sql"></a><span data-ttu-id="0486c-102">CAST (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="0486c-102">CAST (Entity SQL)</span></span>

<span data-ttu-id="0486c-103">將一種資料類型的運算式轉換成另一種。</span><span class="sxs-lookup"><span data-stu-id="0486c-103">Converts an expression of one data type to another.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0486c-104">語法</span><span class="sxs-lookup"><span data-stu-id="0486c-104">Syntax</span></span>  
  
```csharp
CAST ( expression AS data_type )  
```  
  
## <a name="arguments"></a><span data-ttu-id="0486c-105">引數</span><span class="sxs-lookup"><span data-stu-id="0486c-105">Arguments</span></span>  

 `expression`  
 <span data-ttu-id="0486c-106">可以轉換為 `data_type`的任何有效運算式。</span><span class="sxs-lookup"><span data-stu-id="0486c-106">Any valid expression that is convertible to `data_type`.</span></span>  
  
 `data_type`  
 <span data-ttu-id="0486c-107">目標系統提供的資料型別。</span><span class="sxs-lookup"><span data-stu-id="0486c-107">The target system-supplied data type.</span></span> <span data-ttu-id="0486c-108">它必須是基本 (純量) 型別。</span><span class="sxs-lookup"><span data-stu-id="0486c-108">It must be a primitive (scalar) type.</span></span> <span data-ttu-id="0486c-109">使用的 `data_type` 視查詢空間而定。</span><span class="sxs-lookup"><span data-stu-id="0486c-109">The `data_type` used depends on the query space.</span></span> <span data-ttu-id="0486c-110">如果查詢是以 <xref:System.Data.EntityClient.EntityCommand>執行的，資料型別會是在概念模型中定義的型別。</span><span class="sxs-lookup"><span data-stu-id="0486c-110">If a query is executed with the <xref:System.Data.EntityClient.EntityCommand>, the data type is a type defined in the conceptual model.</span></span> <span data-ttu-id="0486c-111">如需詳細資訊，請參閱 [CSDL Specification](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)。</span><span class="sxs-lookup"><span data-stu-id="0486c-111">For more information, see [CSDL Specification](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec).</span></span> <span data-ttu-id="0486c-112">如果查詢是以 <xref:System.Data.Objects.ObjectQuery%601>執行的，則資料型別為 Common Language Runtime (CLR) 型別。</span><span class="sxs-lookup"><span data-stu-id="0486c-112">If a query is executed with <xref:System.Data.Objects.ObjectQuery%601>, the data type is a common language runtime (CLR) type.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="0486c-113">傳回值</span><span class="sxs-lookup"><span data-stu-id="0486c-113">Return Value</span></span>  

 <span data-ttu-id="0486c-114">傳回 `data_type`的相同值。</span><span class="sxs-lookup"><span data-stu-id="0486c-114">Returns the same value as `data_type`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="0486c-115">備註</span><span class="sxs-lookup"><span data-stu-id="0486c-115">Remarks</span></span>  

 <span data-ttu-id="0486c-116">Cast 運算式具有類似于 Transact-sql CONVERT 運算式的語法。</span><span class="sxs-lookup"><span data-stu-id="0486c-116">The cast expression has similar semantics to the Transact-SQL CONVERT expression.</span></span> <span data-ttu-id="0486c-117">轉型運算式是用來將某個型別的值轉換成另一個型別的值。</span><span class="sxs-lookup"><span data-stu-id="0486c-117">The cast expression is used to convert a value of one type into a value of another type.</span></span>  
  
```csharp
CAST( e as T )  
```  
  
 <span data-ttu-id="0486c-118">如果 e 為 S 型別，且 S 可轉換成 T，則上述運算式便是有效的轉型運算式。</span><span class="sxs-lookup"><span data-stu-id="0486c-118">If e is of some type S, and S is convertible to T, then the above expression is a valid cast expression.</span></span> <span data-ttu-id="0486c-119">T 必須是基本 (純量) 型別。</span><span class="sxs-lookup"><span data-stu-id="0486c-119">T must be a primitive (scalar) type.</span></span>  
  
 <span data-ttu-id="0486c-120">轉型為 `Edm.Decimal`時可選擇性提供有效位數和小數位數 Facet 的值。</span><span class="sxs-lookup"><span data-stu-id="0486c-120">Values for the precision and scale facets may optionally be provided when casting to `Edm.Decimal`.</span></span> <span data-ttu-id="0486c-121">如果沒有明確提供，則有效位數和小數位數的預設值將分別為 18 和 0。</span><span class="sxs-lookup"><span data-stu-id="0486c-121">If not explicitly provided, the default values for precision and scale are 18 and 0, respectively.</span></span> <span data-ttu-id="0486c-122">更明確地講，下列多載支援 `Decimal`：</span><span class="sxs-lookup"><span data-stu-id="0486c-122">Specifically, the following overloads are supported for `Decimal`:</span></span>  
  
- `CAST( d as Edm.Decimal );`  
  
- `CAST( d as Edm.Decimal(precision) );`  
  
- `CAST( d as Edm.Decimal(precision, scale) );`  
  
 <span data-ttu-id="0486c-123">使用轉型運算式會視為明確轉換。</span><span class="sxs-lookup"><span data-stu-id="0486c-123">The use of a cast expression is considered an explicit conversion.</span></span> <span data-ttu-id="0486c-124">而明確轉換可能會截斷資料或遺失有效位數。</span><span class="sxs-lookup"><span data-stu-id="0486c-124">Explicit conversions might truncate data or lose precision.</span></span>  
  
> [!NOTE]
> <span data-ttu-id="0486c-125">只有在基本型別和列舉成員型別上能支援 CAST。</span><span class="sxs-lookup"><span data-stu-id="0486c-125">CAST is only supported over primitive types and enumeration member types.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0486c-126">範例</span><span class="sxs-lookup"><span data-stu-id="0486c-126">Example</span></span>  

 <span data-ttu-id="0486c-127">下列 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢使用 CAST 運算子將某個資料型別的運算式轉型為另一個資料型別。</span><span class="sxs-lookup"><span data-stu-id="0486c-127">The following [!INCLUDE[esql](../../../../../../includes/esql-md.md)] query uses the CAST operator to cast an expression of one data type to another.</span></span> <span data-ttu-id="0486c-128">此查詢是根據 AdventureWorks Sales Model。</span><span class="sxs-lookup"><span data-stu-id="0486c-128">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="0486c-129">若要編譯及執行此查詢，請遵循以下步驟：</span><span class="sxs-lookup"><span data-stu-id="0486c-129">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="0486c-130">依照 how [to：執行傳回 PrimitiveType 結果的查詢](../how-to-execute-a-query-that-returns-primitivetype-results.md)中的程式操作。</span><span class="sxs-lookup"><span data-stu-id="0486c-130">Follow the procedure in [How to: Execute a Query that Returns PrimitiveType Results](../how-to-execute-a-query-that-returns-primitivetype-results.md).</span></span>  
  
2. <span data-ttu-id="0486c-131">將下列查詢當成引數，傳遞至 `ExecutePrimitiveTypeQuery` 方法：</span><span class="sxs-lookup"><span data-stu-id="0486c-131">Pass the following query as an argument to the `ExecutePrimitiveTypeQuery` method:</span></span>  
  
 [!code-csharp[DP EntityServices Concepts 2#CAST](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#cast)]  
  
## <a name="see-also"></a><span data-ttu-id="0486c-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0486c-132">See also</span></span>

- [<span data-ttu-id="0486c-133">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="0486c-133">Entity SQL Reference</span></span>](entity-sql-reference.md)
