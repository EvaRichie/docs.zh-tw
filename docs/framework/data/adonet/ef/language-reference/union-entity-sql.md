---
title: UNION (Entity SQL)
ms.date: 03/30/2017
ms.assetid: df98a4db-b00d-4c8b-bd74-0d285f27e1df
ms.openlocfilehash: 9c4106d26fb73219d7b5f0c6763736aaf9163d4b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91200975"
---
# <a name="union-entity-sql"></a><span data-ttu-id="7d2c0-102">UNION (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="7d2c0-102">UNION (Entity SQL)</span></span>

<span data-ttu-id="7d2c0-103">將二個或多個查詢的結果結合成單一集合。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-103">Combines the results of two or more queries into a single collection.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7d2c0-104">語法</span><span class="sxs-lookup"><span data-stu-id="7d2c0-104">Syntax</span></span>  
  
```sql  
expression  
UNION [ ALL ]  
expression  
```  
  
## <a name="arguments"></a><span data-ttu-id="7d2c0-105">引數</span><span class="sxs-lookup"><span data-stu-id="7d2c0-105">Arguments</span></span>  

 `expression`  
 <span data-ttu-id="7d2c0-106">任何有效的查詢運算式，該運算式會傳回與此集合結合的集合。所有運算式都必須具有與 `expression`相同的型別或是共同基底類型或衍生型別。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-106">Any valid query expression that returns a collection to combine with the collection All expressions must be of the same type or of a common base or derived type as `expression`.</span></span>  
  
 <span data-ttu-id="7d2c0-107">UNION</span><span class="sxs-lookup"><span data-stu-id="7d2c0-107">UNION</span></span>  
 <span data-ttu-id="7d2c0-108">指定要結合多個集合，並當做單一集合傳回。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-108">Specifies that multiple collections are to be combined and returned as a single collection.</span></span>  
  
 <span data-ttu-id="7d2c0-109">ALL</span><span class="sxs-lookup"><span data-stu-id="7d2c0-109">ALL</span></span>  
 <span data-ttu-id="7d2c0-110">指定要結合多個集合，並當做單一集合傳回，包括重複的項目。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-110">Specifies that multiple collections are to be combined and returned as a single collection, including duplicates.</span></span> <span data-ttu-id="7d2c0-111">若未指定，就會從結果集合中移除重複的項目。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-111">If not specified, duplicates are removed from the result collection.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="7d2c0-112">傳回值</span><span class="sxs-lookup"><span data-stu-id="7d2c0-112">Return Value</span></span>  

 <span data-ttu-id="7d2c0-113">具有與 `expression`相同的型別或是共同基底類型或衍生型別的集合。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-113">A collection of the same type or of a common base or derived type as `expression`.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="7d2c0-114">備註</span><span class="sxs-lookup"><span data-stu-id="7d2c0-114">Remarks</span></span>  

 <span data-ttu-id="7d2c0-115">UNION 是其中一個 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 設定運算子。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-115">UNION is one of the [!INCLUDE[esql](../../../../../../includes/esql-md.md)] set operators.</span></span> <span data-ttu-id="7d2c0-116">所有 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 設定運算子都會從左到右評估。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-116">All [!INCLUDE[esql](../../../../../../includes/esql-md.md)] set operators are evaluated from left to right.</span></span> <span data-ttu-id="7d2c0-117">如需設定運算子的優先順序資訊 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ，請參閱 [EXCEPT](except-entity-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-117">For precedence information for the [!INCLUDE[esql](../../../../../../includes/esql-md.md)] set operators, see [EXCEPT](except-entity-sql.md).</span></span>  
  
## <a name="example"></a><span data-ttu-id="7d2c0-118">範例</span><span class="sxs-lookup"><span data-stu-id="7d2c0-118">Example</span></span>  

 <span data-ttu-id="7d2c0-119">下列 Entity SQL 查詢會使用 UNION ALL 運算子，將兩個查詢的結果結合成單一集合。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-119">The following Entity SQL query uses the UNION ALL operator to combine the results of two queries into a single collection.</span></span> <span data-ttu-id="7d2c0-120">此查詢是根據 AdventureWorks Sales Model。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-120">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="7d2c0-121">若要編譯及執行此查詢，請遵循以下步驟：</span><span class="sxs-lookup"><span data-stu-id="7d2c0-121">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="7d2c0-122">遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。</span><span class="sxs-lookup"><span data-stu-id="7d2c0-122">Follow the procedure in [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span></span>  
  
2. <span data-ttu-id="7d2c0-123">將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：</span><span class="sxs-lookup"><span data-stu-id="7d2c0-123">Pass the following query as an argument to the `ExecuteStructuralTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#UNION](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#union)]  
  
## <a name="see-also"></a><span data-ttu-id="7d2c0-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="7d2c0-124">See also</span></span>

- [<span data-ttu-id="7d2c0-125">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="7d2c0-125">Entity SQL Reference</span></span>](entity-sql-reference.md)
