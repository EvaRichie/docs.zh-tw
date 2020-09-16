---
title: OFTYPE (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 6d259ca7-bbf0-40f8-a154-181d25c0d67e
ms.openlocfilehash: 375fe9ce52ae290c175e42276b6b526766f6699c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90547508"
---
# <a name="oftype-entity-sql"></a>OFTYPE (Entity SQL)
從屬於特定型別的查詢運算式中傳回物件的集合。  
  
## <a name="syntax"></a>語法  
  
```sql  
OFTYPE ( expression, [ONLY] test_type )  
```  
  
## <a name="arguments"></a>引數  
 `expression`  
 傳回物件集合的任何有效查詢運算式。  
  
 `test_type`  
 據以測試 `expression` 所傳回之每個物件的型別。 此型別必須以命名空間 (Namespace) 限定。  
  
## <a name="return-value"></a>傳回值  
 屬於 `test_type`型別的物件集合，或是 `test_type`之基底型別 (Base Type) 或衍生型別 (Derived Type) 的物件集合。 如果指定了 ONLY，就只會傳回 `test_type` 的執行個體 (Instance) 或空白集合。  
  
## <a name="remarks"></a>備註  
 `OFTYPE` 運算式會指定針對集合的每個項目執行型別測試所發出的型別運算式。  `OFTYPE` 運算式會產生指定之型別的新集合，其中僅包含相當於該型別或其子型別的項目。  
  
 `OFTYPE` 運算式是下列查詢運算式的縮寫：  
  
```sql  
select value treat(t as T) from ts as t where t is of (T)  
```  
  
 假設 Manager 是 Employee 的子型別，下列運算式就會從員工集合中產生只有主管的集合：  
  
```sql  
OfType(employees, NamespaceName.Manager)  
```  
  
 您也可以使用型別篩選來向上轉型集合：  
  
```sql
OfType(executives, NamespaceName.Manager)  
```  
  
 因為所有經理都是主管，所以產生的集合仍然會包含所有原始經理，但是此集合現在的型別會成為主管的集合。  
  
 下表所示為 `OFTYPE` 運算子在某些模式上的行為。 所有例外狀況 (Exception) 都是在叫用 (Invoke) 提供者之前從用戶端擲回：  
  
|模式|行為|  
|-------------|--------------|  
|OFTYPE(Collection(EntityType), EntityType)|Collection(EntityType)|  
|OFTYPE(Collection(ComplexType), ComplexType)|擲回|  
|OFTYPE(Collection(RowType), RowType)|擲回|  
  
## <a name="example"></a>範例  
 下列 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢使用 OFTYPE 運算子，從 Course 物件集合傳回 OnsiteCourse 物件集合。 此查詢是以 [School Model](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100))為基礎。  
  
 [!code-sql[DP EntityServices Concepts#OFTYPE](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#oftype)]  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 參考](entity-sql-reference.md)
