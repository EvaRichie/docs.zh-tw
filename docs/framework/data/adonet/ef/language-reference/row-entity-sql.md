---
title: ROW (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 06da96e8-55d7-486c-991a-4e514d837ff9
ms.openlocfilehash: 2ab91d0c6d3c3ed3f88a7f0ddbf3a6c2f36d8b04
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202249"
---
# <a name="row-entity-sql"></a><span data-ttu-id="d0b6d-102">ROW (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="d0b6d-102">ROW (Entity SQL)</span></span>

<span data-ttu-id="d0b6d-103">從一個或多個值建構匿名、結構式型別的記錄。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-103">Constructs anonymous, structurally typed records from one or more values.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d0b6d-104">語法</span><span class="sxs-lookup"><span data-stu-id="d0b6d-104">Syntax</span></span>  
  
```sql  
ROW ( expression [ AS alias ] [,...] )  
```  
  
## <a name="arguments"></a><span data-ttu-id="d0b6d-105">引數</span><span class="sxs-lookup"><span data-stu-id="d0b6d-105">Arguments</span></span>  

 `expression`  
 <span data-ttu-id="d0b6d-106">資料列型別中任何傳回值到結構的有效查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-106">Any valid query expression that returns a value to construct in a row type.</span></span>  
  
 `alias`  
 <span data-ttu-id="d0b6d-107">為資料列型別中指定的值指定別名。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-107">Specifies an alias for the value specified in a row type.</span></span> <span data-ttu-id="d0b6d-108">如果未提供別名， [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 會嘗試依據 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 別名產生規則產生別名。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-108">If an alias is not provided, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tries to generate an alias based on the [!INCLUDE[esql](../../../../../../includes/esql-md.md)] alias generation rules.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="d0b6d-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="d0b6d-109">Return Value</span></span>  

 <span data-ttu-id="d0b6d-110">資料列型別。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-110">A row type.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d0b6d-111">備註</span><span class="sxs-lookup"><span data-stu-id="d0b6d-111">Remarks</span></span>  

 <span data-ttu-id="d0b6d-112">在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中必須使用資料列建構函式從一或多個值建構匿名、結構式型別的記錄。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-112">You use row constructors in the [!INCLUDE[esql](../../../../../../includes/esql-md.md)] to construct anonymous, structurally typed records from one or more values.</span></span> <span data-ttu-id="d0b6d-113">資料列建構函式的結果型別是資料列型別，而且它的欄位型別對應到用於建立此資料列的值的型別。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-113">The result type of a row constructor is a row type whose field types correspond to the types of the values that were used to construct the row.</span></span> <span data-ttu-id="d0b6d-114">例如，下列運算式會建構 `Record(a int, b string, c int)`型別的值。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-114">For example, the following expression constructs a value of type `Record(a int, b string, c int)`.</span></span>  
  
```sql  
ROW(1 AS a, "abc" AS b, a+34 AS c)  
```  
  
 <span data-ttu-id="d0b6d-115">如果您沒有提供資料列建構函式中運算式的別名，Entity Framework 將會嘗試產生一個別名。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-115">If you do not provide an alias for an expression in a row constructor, the Entity Framework will try to generate one.</span></span> <span data-ttu-id="d0b6d-116">如需詳細資訊，請參閱 [識別項](identifiers-entity-sql.md) 主題中的＜別名規則＞章節。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-116">For more information, see the "Aliasing Rules" section of the [Identifiers](identifiers-entity-sql.md) topic.</span></span>  
  
 <span data-ttu-id="d0b6d-117">下列規則適用於資料列建構函式中的運算式別名：</span><span class="sxs-lookup"><span data-stu-id="d0b6d-117">The following rules apply to expression aliasing in a row constructor:</span></span>  
  
- <span data-ttu-id="d0b6d-118">資料列建構函式中的運算式不可參考同一個建構函式中的其他別名。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-118">Expressions in a row constructor cannot refer to other aliases in the same constructor.</span></span>  
  
- <span data-ttu-id="d0b6d-119">同一個資料列建構函式中的兩個運算式不能有相同的別名。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-119">Two expressions in the same row constructor cannot have the same alias.</span></span>  
  
 <span data-ttu-id="d0b6d-120">如需查詢函式的詳細資訊，請參閱 [建立類型](constructing-types-entity-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-120">For more information about query constructors, see [Constructing Types](constructing-types-entity-sql.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="d0b6d-121">範例</span><span class="sxs-lookup"><span data-stu-id="d0b6d-121">Example</span></span>  

 <span data-ttu-id="d0b6d-122">下列 Entity SQL 查詢使用 ROW 運算子來建構匿名、結構式型別的記錄。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-122">The following Entity SQL query uses the ROW operator to construct anonymous, structurally typed records.</span></span> <span data-ttu-id="d0b6d-123">此查詢是根據 AdventureWorks Sales Model。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-123">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="d0b6d-124">若要編譯及執行此查詢，請遵循以下步驟：</span><span class="sxs-lookup"><span data-stu-id="d0b6d-124">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="d0b6d-125">遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。</span><span class="sxs-lookup"><span data-stu-id="d0b6d-125">Follow the procedure in [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span></span>  
  
2. <span data-ttu-id="d0b6d-126">將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：</span><span class="sxs-lookup"><span data-stu-id="d0b6d-126">Pass the following query as an argument to the `ExecuteStructuralTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#ROW](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#row)]  
  
## <a name="see-also"></a><span data-ttu-id="d0b6d-127">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d0b6d-127">See also</span></span>

- [<span data-ttu-id="d0b6d-128">建構類型</span><span class="sxs-lookup"><span data-stu-id="d0b6d-128">Constructing Types</span></span>](constructing-types-entity-sql.md)
- [<span data-ttu-id="d0b6d-129">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="d0b6d-129">Entity SQL Reference</span></span>](entity-sql-reference.md)
- [<span data-ttu-id="d0b6d-130">類型定義</span><span class="sxs-lookup"><span data-stu-id="d0b6d-130">Type Definitions</span></span>](type-definitions-entity-sql.md)
