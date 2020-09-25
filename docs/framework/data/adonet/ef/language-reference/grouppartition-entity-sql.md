---
title: GROUPPARTITION (Entity SQL)
ms.date: 03/30/2017
ms.assetid: d0482e9b-086c-451c-9dfa-ccb024a9efb6
ms.openlocfilehash: 11abebeac682fed9e3a007986bb2f5c7bdb80f16
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204472"
---
# <a name="grouppartition-entity-sql"></a>GROUPPARTITION (Entity SQL)

傳回引數值的集合，該集合會將目前的群組分割投影至其相關的彙總。 `GroupPartition` 彙總是以群組為基礎的彙總，不具有以集合為基礎的形式。  
  
## <a name="syntax"></a>語法  
  
```sql  
GROUPPARTITION( [ALL|DISTINCT] expression )  
```  
  
## <a name="arguments"></a>引數  

 `expression`  
 任何 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 運算式。  
  
## <a name="remarks"></a>備註  

 下列查詢會產生產品清單，以及每項產品的訂單產品線數量集合：  
  
```sql  
SELECT p, GroupPartition(ol.Quantity) FROM LOB.OrderLines AS ol
  GROUP BY ol.Product AS p
```  
  
 以下兩個查詢的語意相同：  
  
```sql  
SELECT p, Sum(GroupPartition(ol.Quantity)) FROM LOB.OrderLines AS ol
  GROUP BY ol.Product AS p
SELET p, Sum(ol.Quantity) FROM LOB.OrderLines AS ol
  group by ol.Product as p  
```  
  
 `GROUPPARTITION` 運算子可以搭配使用者定義的彙總函式使用。  
  
`GROUPPARTITION` 是特殊的彙總運算子，可保留群組輸入集的參考。 若 GROUP BY 在範圍內，即可在查詢中任何位置使用此參考。 例如：
  
```sql  
SELECT p, GroupPartition(ol.Quantity) FROM LOB.OrderLines AS ol GROUP BY ol.Product AS p
```  
  
 一般情況 `GROUP BY` 下，會隱藏群組的結果。 您只能在彙總函式中使用結果。 若要查看群組的結果，您必須使用子查詢，讓群組和輸入集互相關聯。 下列兩個查詢的用法相同：  
  
```sql  
SELET p, (SELECT q FROM GroupPartition(ol.Quantity) AS q) FROM LOB.OrderLines AS ol GROUP BY ol.Product AS p
SELECT p, (SELECT ol.Quantity AS q FROM LOB.OrderLines AS ol2 WHERE ol2.Product = p) FROM LOB.OrderLines AS ol GROUP BY ol.Product AS p
```  
  
 如範例所示，GROUPPARTITION 彙總運算子可讓您更容易在群組之後參考輸入集。  
  
 當您使用 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 參數時，GROUPPARTITION 運算子可以指定運算子輸入中的任何 `expression` 運算式。  
  
 下列針對群組分割的所有輸入運算式在執行個體中皆有效：  
  
```sql  
SELECT groupkey, GroupPartition(b) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey
SELECT groupkey, GroupPartition(1) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey
SELECT groupkey, GroupPartition(a + b) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey
SELECT groupkey, GroupPartition({a + b}) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey  
SELECT groupkey, GroupPartition({42}) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey  
SELECT groupkey, GroupPartition(b > a) FROM {1,2,3} AS a INNER JOIN {4,5,6} AS b ON true GROUP BY a AS groupkey  
```  
  
## <a name="example"></a>範例  

 下列範例示範如何使用 GROUPPARTITION 子句搭配 GROUP BY 子句。 GROUP BY 子句會依 `SalesOrderHeader` 將 `Contact`實體進行分組。 GROUPPARTITION 子句接著會投影每個群組的 `TotalDue` 屬性，以產生十進位集合。  
  
 [!code-sql[DP EntityServices Concepts#Collection_GroupPartition](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#collection_grouppartition)]
