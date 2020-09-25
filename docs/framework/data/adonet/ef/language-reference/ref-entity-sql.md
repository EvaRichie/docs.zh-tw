---
title: REF (Entity SQL)
ms.date: 03/30/2017
ms.assetid: c5f4cb35-69e9-44cc-b63b-ee38922bbda1
ms.openlocfilehash: 56ae576ac60d1716d86fbbb797882bf96e99813f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202236"
---
# <a name="ref-entity-sql"></a>REF (Entity SQL)

傳回實體執行個體的參考。  
  
## <a name="syntax"></a>語法  
  
```sql  
REF( expression )
```  
  
## <a name="arguments"></a>引數  

 `expression`  
 可產生實體類型之執行個體的任何有效運算式。  
  
## <a name="return-value"></a>傳回值  

 指定之實體執行個體的參考。  
  
## <a name="remarks"></a>備註  

 實體參考由實體索引鍵和實體集名稱所組成。 因為不同實體集可視相同實體類型而定，特定實體索引鍵可出現於多個實體集， 但實體參考一定是唯一的。 如果輸入運算式表示持續性實體，會傳回這個實體的參考。 如果輸入運算式不是持續性實體，會傳回 null 參考。  
  
 如果屬性引出運算子 (.) 是用於存取實體的屬性，則會為參考自動取值 (Dereference)。  
  
## <a name="example"></a>範例  

 下列 Entity SQL 查詢會使用 REF 運算子，傳回輸入實體引數的參考。 相同查詢會為參考取值，因為我們使用屬性引出運算子 (.) 存取 Product 實體的屬性。 此查詢是根據 AdventureWorks Sales Model。 若要編譯及執行此查詢，請遵循以下步驟：  
  
1. 依照 how [to：執行傳回 PrimitiveType 結果的查詢](../how-to-execute-a-query-that-returns-primitivetype-results.md)中的程式操作。  
  
2. 將下列查詢當成引數，傳遞至 `ExecutePrimitiveTypeQuery` 方法：  
  
 [!code-sql[DP EntityServices Concepts#REF](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#ref)]  
  
## <a name="see-also"></a>另請參閱

- [DEREF](deref-entity-sql.md)
- [CREATEREF](createref-entity-sql.md)
- [KEY](key-entity-sql.md)
- [Entity SQL 參考](entity-sql-reference.md)
- [類型定義](type-definitions-entity-sql.md)
