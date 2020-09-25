---
title: 具名類型建構函式 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 549dea04-d93d-4c87-a292-f81b1598dbfd
ms.openlocfilehash: c673b58ee5811e3d3b74b3744d3f5291888e2253
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91197777"
---
# <a name="named-type-constructor-entity-sql"></a><span data-ttu-id="23d3e-102">具名類型建構函式 (Entity SQL)</span><span class="sxs-lookup"><span data-stu-id="23d3e-102">Named Type Constructor (Entity SQL)</span></span>

<span data-ttu-id="23d3e-103">用於建立概念模型名義型別 (例如實體類型或複雜類型) 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="23d3e-103">Used to create instances of conceptual model nominal types such as Entity or Complex types.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="23d3e-104">語法</span><span class="sxs-lookup"><span data-stu-id="23d3e-104">Syntax</span></span>  
  
```sql  
[{identifier. }] identifier( [expression [{, expression }]] )  
```  
  
## <a name="arguments"></a><span data-ttu-id="23d3e-105">引數</span><span class="sxs-lookup"><span data-stu-id="23d3e-105">Arguments</span></span>  

 `identifier`  
 <span data-ttu-id="23d3e-106">為簡單或引號識別項的值。</span><span class="sxs-lookup"><span data-stu-id="23d3e-106">Value that is a simple or quoted identifier.</span></span> <span data-ttu-id="23d3e-107">如需詳細資訊，請參閱 [識別碼](identifiers-entity-sql.md)</span><span class="sxs-lookup"><span data-stu-id="23d3e-107">For more information see, [Identifiers](identifiers-entity-sql.md)</span></span>  
  
 `expression`  
 <span data-ttu-id="23d3e-108">型別的屬性，假設與它們出現在型別宣告中的順序相同。</span><span class="sxs-lookup"><span data-stu-id="23d3e-108">Attributes of the type that are assumed to be in the same order as they appear in the declaration of the type.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="23d3e-109">傳回值</span><span class="sxs-lookup"><span data-stu-id="23d3e-109">Return Value</span></span>  

 <span data-ttu-id="23d3e-110">具名複雜類型和實體類型的執行個體。</span><span class="sxs-lookup"><span data-stu-id="23d3e-110">Instances of named complex types and entity types.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="23d3e-111">備註</span><span class="sxs-lookup"><span data-stu-id="23d3e-111">Remarks</span></span>  

 <span data-ttu-id="23d3e-112">以下範例示範如何建構名義和複雜類型。</span><span class="sxs-lookup"><span data-stu-id="23d3e-112">The following examples show how to construct nominal and complex types:</span></span>  
  
 <span data-ttu-id="23d3e-113">下面的運算式會建立 `Person` 型別的執行個體：</span><span class="sxs-lookup"><span data-stu-id="23d3e-113">The expression below creates an instance of a `Person` type:</span></span>  
  
 `Person("abc", 12)`  
  
 <span data-ttu-id="23d3e-114">下面的運算式會建立複雜類型的執行個體：</span><span class="sxs-lookup"><span data-stu-id="23d3e-114">The expression below creates an instance of a complex type:</span></span>  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 <span data-ttu-id="23d3e-115">下面的運算式會建立巢狀複雜類型的執行個體：</span><span class="sxs-lookup"><span data-stu-id="23d3e-115">The expression below creates an instance of a nested complex type:</span></span>  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 <span data-ttu-id="23d3e-116">下面的運算式會建立具有巢狀複雜類型之實體的執行個體：</span><span class="sxs-lookup"><span data-stu-id="23d3e-116">The expression below creates an instance of an entity with a nested complex type:</span></span>  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 <span data-ttu-id="23d3e-117">以下範例示範如何將複雜類型的屬性初始化為：`MyModel.ZipCode(‘98118’, null)`</span><span class="sxs-lookup"><span data-stu-id="23d3e-117">The following example shows how to initialize a property of a complex type to null:`MyModel.ZipCode(‘98118’, null)`</span></span>  
  
## <a name="example"></a><span data-ttu-id="23d3e-118">範例</span><span class="sxs-lookup"><span data-stu-id="23d3e-118">Example</span></span>  

 <span data-ttu-id="23d3e-119">以下 Entity SQL 查詢使用具名型別建構函式來建立概念模型型別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="23d3e-119">The following Entity SQL query uses the named type constructor to create an instance of a conceptual model type.</span></span> <span data-ttu-id="23d3e-120">此查詢是根據 AdventureWorks Sales Model。</span><span class="sxs-lookup"><span data-stu-id="23d3e-120">The query is based on the AdventureWorks Sales Model.</span></span> <span data-ttu-id="23d3e-121">若要編譯及執行此查詢，請遵循以下步驟：</span><span class="sxs-lookup"><span data-stu-id="23d3e-121">To compile and run this query, follow these steps:</span></span>  
  
1. <span data-ttu-id="23d3e-122">遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。</span><span class="sxs-lookup"><span data-stu-id="23d3e-122">Follow the procedure in [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md).</span></span>  
  
2. <span data-ttu-id="23d3e-123">將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：</span><span class="sxs-lookup"><span data-stu-id="23d3e-123">Pass the following query as an argument to the `ExecuteStructuralTypeQuery` method:</span></span>  
  
 [!code-sql[DP EntityServices Concepts#NAMED_TYPE_CONSTRUCTOR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#named_type_constructor)]  
  
## <a name="see-also"></a><span data-ttu-id="23d3e-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="23d3e-124">See also</span></span>

- [<span data-ttu-id="23d3e-125">建構類型</span><span class="sxs-lookup"><span data-stu-id="23d3e-125">Constructing Types</span></span>](constructing-types-entity-sql.md)
- [<span data-ttu-id="23d3e-126">Entity SQL 參考</span><span class="sxs-lookup"><span data-stu-id="23d3e-126">Entity SQL Reference</span></span>](entity-sql-reference.md)
