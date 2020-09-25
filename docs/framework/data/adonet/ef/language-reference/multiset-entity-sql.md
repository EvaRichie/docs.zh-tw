---
title: MULTISET (Entity SQL)
ms.date: 03/30/2017
ms.assetid: eb90a377-e47a-43a5-b308-e993b6d611e6
ms.openlocfilehash: a81787da9ee1af084a903dcb50b024f3d26d18fc
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91175690"
---
# <a name="multiset-entity-sql"></a>MULTISET (Entity SQL)

從值清單建立多重集的執行個體。 MULTISET 建構函式 (Constructor) 中的所有值都必須是相容型別 `T`。 不允許空的多重集建構函式。  
  
## <a name="syntax"></a>語法  
  
```sql  
MULTISET ( expression [{, expression }] )  
-- or  
{ expression [{, expression }] }  
```  
  
## <a name="arguments"></a>引數  

 `expression`  
 任何有效的值清單。  
  
## <a name="return-value"></a>傳回值  

 多重集型別的集合 \<T> 。  
  
## <a name="remarks"></a>備註  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 提供三種建構函式：資料列建構函式、物件建構函式和多重集 (或集合) 建構函式。 如需詳細資訊，請參閱 [建立類型](constructing-types-entity-sql.md)。  
  
 多重集建構函式會從值清單建立多重集的例項。 該建構函式中的所有值都必須是相容型別。  
  
 例如，下列運算式會建立整數的多重集。  
  
 `MULTISET(1, 2, 3)`  
  
 `{1, 2, 3}`  
  
> [!NOTE]
> 只有在包裝多重集具有單一多重集專案時，才支援嵌套的多重集常值。例如， `{{1, 2, 3}}` 。 在包裝多重集有多個多重集項目 (例如 `{{1, 2}, {3, 4}}`) 的情況下，並不支援巢狀多重集常值。  
  
## <a name="example"></a>範例  

 下列 Entity SQL 查詢會使用 MULTISET 運算子，從值清單建立多重集的例項。 此查詢是根據 AdventureWorks Sales Model。 若要編譯及執行此查詢，請遵循以下步驟：  
  
1. 遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。  
  
2. 將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-sql[DP EntityServices Concepts#MULTISET](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#multiset)]  
  
## <a name="see-also"></a>另請參閱

- [建構類型](constructing-types-entity-sql.md)
- [Entity SQL 參考](entity-sql-reference.md)
