---
title: IN (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 51662950-ee01-4857-b7b9-311dd8515966
ms.openlocfilehash: 582a3b988247f1484197c0905fecf7f4407f88b0
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203666"
---
# <a name="in-entity-sql"></a>IN (Entity SQL)

判斷某個值是否與集合中的任何值相符。  
  
## <a name="syntax"></a>語法  
  
```sql  
value [ NOT ] IN expression  
```  
  
## <a name="arguments"></a>引數  

 `value`  
 傳回要比對之值的任何有效運算式。  
  
 [ NOT ]  
 指定 IN 的 `Boolean` 結果是負值。  
  
 `expression`  
 傳回要測試是否有相符項目之集合的任何有效運算式。 所有運算式都必須具有與 `value`相同的型別或是共同基底型別或衍生型別。  
  
## <a name="return-value"></a>傳回值  

 如果在集合中找到值，就是 `true`。如果此值為 null 或集合為 null，就是 null，否則為 `false`。 使用 NOT IN 會執行 IN 結果的否定運算。  
  
## <a name="example"></a>範例  

 下列 Entity SQL 查詢會使用 IN 運算子來判斷某個值是否與集合中的任何值相符。 此查詢是根據 AdventureWorks Sales Model。 若要編譯及執行此查詢，請遵循以下步驟：  
  
1. 遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。  
  
2. 將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-sql[DP EntityServices Concepts#IN](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#in)]  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 參考](entity-sql-reference.md)
