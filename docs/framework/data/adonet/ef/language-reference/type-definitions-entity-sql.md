---
title: 類型定義 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 306b204a-ade5-47ef-95b5-c785d2da4a7e
ms.openlocfilehash: 7e4e6f0e9f64816d10a69a8b0639728e4cd7af80
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201014"
---
# <a name="type-definitions-entity-sql"></a>類型定義 (Entity SQL)

型別定義用於 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 內嵌函式中的宣告陳述式。  
  
## <a name="remarks"></a>備註  

 內嵌函式的宣告語句包含函 [式關鍵字，](function-entity-sql.md) 後面接著代表函式名稱的識別碼 (例如 "MyAvg" ) 後面接著參數定義清單（以括弧括住） (例如，「擁有的集合 (Decimal) 」 ) 。  
  
 參數定義清單包括零或多個參數定義。 每個參數定義包括一個識別項 (函式參數的名稱，例如 "dues")，後面接型別定義 (例如 "Collection(Decimal)")。  
  
 型別定義可以是下面其中一項：  
  
- 識別項的型別 (例如 "Int32" 或 "AdventureWorks.Order")。  
  
- 關鍵字 `COLLECTION` 後面接以括號括住的其他型別定義 (例如 "Collection(AdventureWorks.Order)")。  
  
- 關鍵字 ROW 後面接以括號括住的屬性定義清單 (例如 "Row(x AdventureWorks.Order)")。 屬性定義的格式如下： " `identifier type_definition` ， `identifier type_definition` ，..."。  
  
- 關鍵字 REF 後面接以括號括住的識別項型別 (例如 "Ref(AdventureWorks.Order)")。 REF 型別定義運算子需要實體類型做為引數。 您不能指定基本型別做為引數。  
  
 您也可以巢狀化型別定義 (例如 "Collection(Row(x Ref(AdventureWorks.Order)))")。  
  
 型別定義的選項是：  
  
- `IdentifierName supported_type` 或  
  
- `IdentifierName` COLLECTION(`type_definition`)，或  
  
- `IdentifierName` ROW(`property_definition`)，或  
  
- `IdentifierName` REF(`supported_entity_type`)  
  
 屬性定義的選項是 `IdentifierName type_definition`。  
  
 支援的型別是目前命名空間中的任何型別。 這些包括基本型別和實體類型兩者。  
  
 支援的實體類型只會參考目前命名空間中的實體類型。 不包括基本型別。  
  
## <a name="examples"></a>範例  

 下面是一個簡單的型別定義範例：  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 EDM.Decimal) AS (  
   Round(p1)  
)  
MyRound(CAST(1.7 as EDM.Decimal))  
```  
  
 下面是一個 COLLECTION 型別定義的範例：  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Collection(EDM.Decimal)) AS (  
   Select Round(p1) from p1  
)  
MyRound({CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)})  
```  
  
 下面是一個 ROW 型別定義的範例：  
  
```sql  
USING Microsoft.Samples.Entity  
Function MyRound(p1 Row(x EDM.Decimal)) AS (  
   Round(p1.x)  
)  
select MyRound(row(a as x)) from {CAST(1.7 as EDM.Decimal), CAST(2.7 as EDM.Decimal)} as a  
```  
  
 下面是一個 REF 型別定義的範例。  
  
```sql  
USING Microsoft.Samples.Entity  
Function UnReference(p1 Ref(AdventureWorks.Order)) AS (  
   Deref(p1)  
)  
select Ref(x) from AdventureWorksEntities.SalesOrderHeaders as x  
```  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 概觀](entity-sql-overview.md)
- [Entity SQL 參考](entity-sql-reference.md)
