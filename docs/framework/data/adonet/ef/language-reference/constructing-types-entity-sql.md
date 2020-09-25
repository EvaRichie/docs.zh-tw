---
title: 建構類型 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 41fa7bde-8d20-4a3f-a3d2-fb791e128010
ms.openlocfilehash: 82c8e3f2bac0d13da4870e90878e0de6fc9ec063
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91177519"
---
# <a name="constructing-types-entity-sql"></a>建構類型 (Entity SQL)

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 提供三種類型的函式：資料列的函式、命名的型別函式和集合的函式。  
  
## <a name="row-constructors"></a>資料列建構函式  

 在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中使用資料列建構函式，可以從一個或多個值建構匿名、結構式具型別的記錄。 資料列建構函式的結果型別是資料列型別，而且它的欄位型別會對應到用於建構資料列的值的型別。 例如，下列運算式會建立類型的值 `Record(a int, b string, c int)` ：  
  
 `ROW(1 AS a, "abc" AS b, a + 34 AS c)`  
  
 如果您沒有提供資料列建構函式中運算式的別名，Entity Framework 將會嘗試產生一個別名。 如需詳細資訊，請參閱 [識別碼](identifiers-entity-sql.md)中的「別名規則」一節。  
  
 下列規則適用於資料列建構函式中的運算式別名：  
  
- 資料列建構函式中的運算式不可參考同一個建構函式中的其他別名。  
  
- 同一個資料列建構函式中的兩個運算式不能有相同的別名。  
  
 如需資料列構造函式的詳細資訊，請參閱資料 [列](row-entity-sql.md)。  
  
## <a name="collection-constructors"></a>集合建構函式  

 在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中使用集合建構函式，可以從值清單建立多重集 (Multiset) 的執行個體。 建構函式中的所有值都必須是相容的型別 `T`，而且建構函式會產生型別 `Multiset<T>` 的集合。 例如，下列運算式會建立整數的集合：  
  
 `Multiset(1, 2, 3)`  
  
 `{1, 2, 3}`  
  
 空白的多重集建構函式是不被允許的，因為這樣無法判斷項目的型別。 以下程式碼行是無效的：  
  
 `multiset() {}`  
  
 如需詳細資訊，請參閱 [多重集](multiset-entity-sql.md)。  
  
## <a name="named-type-constructors-namedtype-initializers"></a>具名型別建構函式 (NamedType 初始設定式)  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 可以讓型別建構函式 (初始設定式) 建立具名複雜類型和實體類型的執行個體。 例如，下列運算式會建立 `Person` 型別的執行個體。  
  
 `Person("abc", 12)`  
  
 下列運算式會建立複雜類型的執行個體。  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 下列運算式會建立巢狀複雜類型的執行個體。  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 下列運算式會建立具有巢狀複雜類型之實體的執行個體。  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 下列範例顯示如何將複雜類型的屬性 (Property) 初始化為 null。 `MyModel.ZipCode(‘98118’, null)`  
  
 建構函式的引數順序，會假設與型別屬性 (Attribute) 宣告中的順序相同。  
  
 如需詳細資訊，請參閱 [命名類型](named-type-constructor-entity-sql.md)的函式。  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 參考](entity-sql-reference.md)
- [Entity SQL 概觀](entity-sql-overview.md)
- [型別系統](type-system-entity-sql.md)
