---
title: ORDER BY (Entity SQL)
ms.date: 03/30/2017
ms.assetid: c0b61572-ecee-41eb-9d7f-74132ec8a26c
ms.openlocfilehash: 5e1c418a7f2bd40a42b259fb3784794b13098d7f
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91173675"
---
# <a name="order-by-entity-sql"></a>ORDER BY (Entity SQL)

指定 SELECT 陳述式所傳回物件使用的排序順序。  
  
## <a name="syntax"></a>語法  
  
```sql  
[ ORDER BY
   {  
      order_by_expression [SKIP n] [LIMIT n]  
      [ COLLATE collation_name ]  
      [ ASC | DESC ]  
   }  
   [ ,…n ]
]  
```  
  
## <a name="arguments"></a>引數  

 `order_by_expression`  
 任何指定要排序之屬性的有效查詢運算式。 可以指定多個排序運算式。 ORDER BY 子句中排序運算式的順序會定義排序結果集的組織方式。  
  
 COLLATE {collation_name}  
 指定 ORDER BY 運算要依照 `collation_name`中指定的定序執行。 COLLATE 只適用於字串運算式。  
  
 ASC  
 指定特定屬性中的值要以遞增順序 (從最低值到最高值) 排序。 此為預設值。  
  
 DESC  
 指定特定屬性中的值要以遞減順序 (從最高值到最低值) 排序。  
  
 LIMIT `n`  
 只選取前 `n` 個項目。  
  
 SKIP `n`  
 略過前 `n` 個項目。  
  
## <a name="remarks"></a>備註  

 ORDER BY 子句會以邏輯方式套用到 SELECT 子句的結果。 ORDER BY 子句可以利用項目的別名參考選取清單中的項目。 ORDER BY 子句也可以參考目前在範圍內的其他變數。 但是，如果已經配合 DISTINCT 修飾詞指定了 SELECT 子句，那麼 ORDER BY 子句就只能參考來自 SELECT 子句的別名。  
  
 `SELECT c AS c1 FROM cs AS c ORDER BY c1.e1, c.e2`  
  
 ORDER BY 子句中的每個運算式都必評估為可以比較排序是否不相等 (小於或大於等) 的型別。 這些型別通常是純量基本型別，例如數值、字串和日期。 屬於可比較型別的 RowTypes 也可以比較排序。  
  
 如果程式碼要在最上層投影以外的排序集上重複執行，輸出不一定會保持原排序。  

在下列範例中，一定要保留順序：

```sql  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  

在下列查詢中，會忽略巢狀查詢的排序：  

```sql  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
 如需排序的 UNION、UNION ALL、EXCEPT 或 INTERSECT 運算，請使用下列模式：  
  
```sql  
SELECT ...  
FROM ( UNION/EXCEPT/INTERSECT operation )  
ORDER BY ...  
```  
  
## <a name="restricted-keywords"></a>限制關鍵字  

 使用於 `ORDER BY` 子句時，下列關鍵字必須括在引號內：  
  
- CROSS  
  
- FULL  
  
- KEY  
  
- LEFT  
  
- ORDER  
  
- OUTER  
  
- RIGHT  
  
- ROW  
  
- 值  
  
## <a name="ordering-nested-queries"></a>排序巢狀查詢  

 在 Entity Framework 中，巢狀運算式可放在查詢中的任何地方；巢狀查詢的順序並不會保留。  

下列查詢會依姓氏排序結果：  

```sql  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName  
```  

在下列查詢中，會忽略巢狀查詢的排序：  

```sql  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorks.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## <a name="example"></a>範例  

 以下 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢使用 ORDER BY 運算子指定 SELECT 陳述式所傳回物件使用的排序順序。 此查詢是根據 AdventureWorks Sales Model。 若要編譯及執行此查詢，請遵循以下步驟：  
  
1. 遵循 [How to: Execute a Query that Returns StructuralType Results](../how-to-execute-a-query-that-returns-structuraltype-results.md)中的程序進行。  
  
2. 將下列查詢當成引數，傳遞至 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-sql[DP EntityServices Concepts#ORDERBY](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#orderby)]  
  
## <a name="see-also"></a>另請參閱

- [查詢運算式](query-expressions-entity-sql.md)
- [Entity SQL 參考](entity-sql-reference.md)
- [跳](skip-entity-sql.md)
- [限制](limit-entity-sql.md)
- [頂端](top-entity-sql.md)
