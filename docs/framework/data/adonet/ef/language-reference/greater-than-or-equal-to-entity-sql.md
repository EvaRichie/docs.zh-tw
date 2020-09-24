---
title: '>= (大於或等於) (Entity SQL)'
ms.date: 03/30/2017
ms.assetid: 70780ac4-0123-4da8-b731-8af856daffe3
ms.openlocfilehash: 02e03d6d2da321bd02ea2b14e45a910853d39c4d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91158418"
---
# <a name="-greater-than-or-equal-to-entity-sql"></a><span data-ttu-id="a64dc-102">>= (大於或等於)  (Entity SQL) </span><span class="sxs-lookup"><span data-stu-id="a64dc-102">>= (Greater Than or Equal To) (Entity SQL)</span></span>

<span data-ttu-id="a64dc-103">比較兩個運算式來判斷左運算式的值是否大於或等於右運算式。</span><span class="sxs-lookup"><span data-stu-id="a64dc-103">Compares two expressions to determine whether the left expression has a value greater than or equal to the right expression.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a64dc-104">語法</span><span class="sxs-lookup"><span data-stu-id="a64dc-104">Syntax</span></span>  
  
```sql  
expression >= expression  
```  
  
## <a name="arguments"></a><span data-ttu-id="a64dc-105">引數</span><span class="sxs-lookup"><span data-stu-id="a64dc-105">Arguments</span></span>  

 `expression`  
 <span data-ttu-id="a64dc-106">任何有效的運算式。</span><span class="sxs-lookup"><span data-stu-id="a64dc-106">Any valid expression.</span></span> <span data-ttu-id="a64dc-107">這兩個運算式的類型，都必須是可以隱含轉換的資料類型。</span><span class="sxs-lookup"><span data-stu-id="a64dc-107">Both expressions must have implicitly convertible data types.</span></span>  
  
## <a name="result-types"></a><span data-ttu-id="a64dc-108">結果類型</span><span class="sxs-lookup"><span data-stu-id="a64dc-108">Result Types</span></span>  

 <span data-ttu-id="a64dc-109">如果左運算式的值大於或等於右運算式則為`true` ；否則為 `false`。</span><span class="sxs-lookup"><span data-stu-id="a64dc-109">`true` if the left expression has a value greater than or equal to the right expression; otherwise, `false`.</span></span>  
  
## <a name="example"></a><span data-ttu-id="a64dc-110">範例</span><span class="sxs-lookup"><span data-stu-id="a64dc-110">Example</span></span>  

 <span data-ttu-id="a64dc-111">下列 Entity SQL 查詢使用 >= 比較運算子來比較兩個運算式，以判斷左運算式的值是否大於或等於右運算式。</span><span class="sxs-lookup"><span data-stu-id="a64dc-111">The following Entity SQL query uses >= comparison operator to compare two expressions to determine whether the left expression has a value greater than or equal to the right expression.</span></span> <span data-ttu-id="a64dc-112">此查詢是根據 AdventureWorks Sales Model。</span><span class="sxs-lookup"><span data-stu-id="a64dc-112">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="a64dc-113">若要編譯及執行此查詢，請遵循以下步驟：</span><span class="sxs-lookup"><span data-stu-id="a64dc-113">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="a64dc-114">遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。</span><span class="sxs-lookup"><span data-stu-id="a64dc-114">Follow the procedure in [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span></span>  
  
2. <span data-ttu-id="a64dc-115">將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：</span><span class="sxs-lookup"><span data-stu-id="a64dc-115">Pass the following query as an argument to the `ExecuteStructuralTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#GREATER_OR_EQUALS](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#greater_or_equals)]  
  
## <a name="see-also"></a><span data-ttu-id="a64dc-116">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a64dc-116">See also</span></span>

- [<span data-ttu-id="a64dc-117">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="a64dc-117">Entity SQL Reference</span></span>](entity-sql-reference.md)
