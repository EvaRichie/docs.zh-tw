---
title: 識別項 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: d58a5edd-7b5c-48e1-b5d7-a326ff426aa4
ms.openlocfilehash: 7e9b12ca351b021fab62988969cb98310cb55cc2
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203692"
---
# <a name="identifiers-entity-sql"></a>識別項 (Entity SQL)

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中使用識別項表示查詢運算式別名、變數參考、物件的屬性、函式等。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 提供兩種識別碼：簡單識別碼和引號識別碼。  
  
## <a name="simple-identifiers"></a>簡單識別項  

 中的簡單識別碼 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 是一連串的英數位元和底線字元。 識別項的第一個字元必須是字母字元 (a-z 或 A-Z)。  
  
## <a name="quoted-identifiers"></a>引號識別碼  

 引號識別項是以方括弧 ([]) 括住的任何字元序列。 引號識別項可讓您使用在識別項中無效的字元來指定識別項。 方括弧之間的所有字元都會變成識別碼的一部分，包括所有空白字元。  
  
 引號識別項不能包含下列字元：  
  
- 新行 (Newline)。  
  
- 歸位字元 (Carriage Return)。  
  
- 定位點。  
  
- 退格鍵。  
  
- 其他方括弧 (也就是方括弧內描寫識別項的方括弧)。  
  
 引號識別項可包含 Unicode 字元。  
  
 引號識別項可讓您建立在識別項中無效的屬性名稱字元，如下列範例所述：  
  
 `SELECT c.ContactName AS [Contact Name] FROM customers AS c`  
  
 您也可以使用引號識別項來指定 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 保留關鍵字的識別項。 例如，如果型別 `Email` 具有名為 "From" 的屬性，您就可以使用方括弧釐清 "From" 屬性與保留的關鍵字 FROM。  
  
 `SELECT e.[From] FROM emails AS e`  
  
 您可以在點 (.) 運算子的右邊使用引號識別項 (Quoted Identifier)  
  
 `SELECT t FROM ts as t WHERE t.[property] == 2`  
  
 若要在識別項中使用方括弧，必須加上額外的方括弧。 下列範例中的 "`abc]`" 為識別項：  
  
 `SELECT t from ts as t WHERE t.[abc]]] == 2`  
  
 如需引號識別碼比較的語法，請參閱 [輸入字元集](input-character-set-entity-sql.md)。  
  
## <a name="aliasing-rules"></a>別名規則  

 建議您在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 必要時指定查詢中的別名，包括下列 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 結構：  
  
- 資料列建構函式 (Constructor) 的欄位。  
  
- 查詢運算式之 FROM 子句中的項目。  
  
- 查詢運算式之 SELECT 子句中的項目。  
  
- 查詢運算式之 GROUP BY 子句中的項目。  
  
### <a name="valid-aliases"></a>有效的別名  

 中的有效別名 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 是任何簡單識別碼或引號識別碼。  
  
### <a name="alias-generation"></a>別名產生  

 如果查詢運算式中未指定別名 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] ，會 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 嘗試根據下列簡單規則產生別名：  
  
- 如果查詢運算式 (未指定別名) 是簡單識別項或引號識別項，會使用該識別項當做別名。 例如，`ROW(a, [b])` 會成為 `ROW(a AS a, [b] AS [b])`。  
  
- 如果查詢運算式是比較複雜的運算式，但是該查詢運算式的最後一個元件是簡單識別項，則會使用該識別項當做別名。 例如，`ROW(a.a1, b.[b1])` 會成為 `ROW(a.a1 AS a1, b.[b1] AS [b1])`。  
  
 如果您想要在稍後使用別名名稱，建議您不要使用隱含別名。 任何時候發生別名 (隱含或明確) 衝突或是在相同的範圍內重複別名時，都會發生編譯錯誤。 即使有同名的明確或隱含別名，隱含別名還是會通過編譯程序。  
  
 隱含別名會根據使用者輸入自動產生。 例如，下列這一行程式碼將會產生 NAME 當做這兩個資料行的別名，因此會發生衝突。  
  
```sql  
SELECT product.NAME, person.NAME  
```  
  
 下列這一行程式碼 (使用明確別名) 也會失敗。 但是，閱讀程式碼就會更清楚看到失敗。  
  
```sql  
SELECT 1 AS X, 2 AS X …  
```  
  
## <a name="scoping-rules"></a>範圍規則  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 定義範圍規則，以決定何時可以在查詢語言中看到特定變數。 某些運算式或陳述式會導入新的名稱。 範圍規則可判斷哪裡可以使用這些名稱，以及當新的宣告與另一個宣告同名時，要在何時及何處隱藏它的前置項目。  
  
 當名稱是在查詢中定義時，就會被視為在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 範圍內定義。 範圍涵蓋查詢的整個區域。 某個範圍內的所有運算式或名稱參考都可以看到該範圍內定義的名稱。 在範圍開始前及結束後，無法參考此範圍內所定義的名稱。  
  
 範圍可以是巢狀的。 的各個部分 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 會介紹涵蓋整個區域的新範圍，而且這些區域可以包含 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 也會引進範圍的其他運算式。 當範圍是巢狀時，可以參考最內部範圍 (包含參考) 內定義的名稱。 也可以參考任何外部範圍內定義的任何名稱。 相同範圍內定義的任何兩個範圍都視為同層級 (Sibling) 範圍。 無法參考同層級範圍內定義的名稱。  
  
 如果內部範圍內宣告的名稱符合外部範圍內宣告的名稱，則內部範圍中或是該範圍內宣告的範圍中的參考只會參考新宣告的名稱。 外部範圍中的名稱則會隱藏。  
  
 即使是在相同的範圍中，也一定要在定義名稱之後才可以參考。  
  
 全域名稱可以當做執行環境的一部分存在。 這可包括持續性集合或環境變數的名稱。 如果希望名稱是全域名稱，必須在最外層範圍宣告它。  
  
 參數不在範圍內。 因為參數的參考包含特殊語法，所以參數的名稱永遠都不會與查詢中的其他名稱衝突。  
  
### <a name="query-expressions"></a>查詢運算式  

 查詢運算式導入了 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 新的範圍。 FROM 子句中定義的名稱會導入來源範圍內 (根據外觀從左到右)。 在聯結清單中，運算式可以參考之前定義在清單中的名稱。 FROM 子句中識別之項目的公用屬性 (欄位等等) 會加入來源範圍。 這些屬性必須由別名限定的名稱所參考。 一般來說，SELECT 運算式的所有部分都視為在來源範圍中。  
  
 GROUP BY 子句也會導入新的同層級範圍。 每一個群組都可以有一個群組名稱來參考該群組內的項目集合。 每一個群組運算式也都會將新的名稱導入群組範圍。 另外，巢狀彙總 (或具名群組) 也會加入此範圍。 群組運算式本身是在來源範圍中。 但是，當使用 GROUP BY 子句時，SELECT 清單 (投影)、HAVING 子句和 ORDER BY 子句都會被視為在群組範圍內，而不在來源範圍內。 彙總會收到特殊的對待，如同下列項目符號清單內所述。  
  
 下列是有關範圍的一些其他注意事項：  
  
- SELECT 清單可以將新的名稱依序導入此範圍。 右邊的投影運算式可能會參考左邊投影的名稱。  
  
- ORDER BY 子句可參考 SELECT 清單中指定的名稱 (別名)。  
  
- SELECT 運算式內子句的評估順序會決定名稱導入範圍中的順序。 FROM 子句會先評估，接著是 WHERE 子句、GROUP BY 子句、HAVING 子句、SELECT 子句，最後是 ORDER BY 子句。  
  
### <a name="aggregate-handling"></a>彙總處理  

 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支援兩種形式的匯總：以集合為基礎的匯總和以群組為基礎的匯總。 以集合為基礎的彙總是 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中偏好的建構，以群組為基礎的彙總則是為了與 SQL 相容而支援。  
  
 解析匯總時， [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 會先嘗試將它視為以集合為基礎的匯總。 如果失敗，會 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 將匯總輸入轉換為對嵌套匯總的參考，並嘗試解析這個新的運算式，如下列範例所示。  
  
 `AVG(t.c) becomes AVG(group..(t.c))`  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 參考](entity-sql-reference.md)
- [Entity SQL 概觀](entity-sql-overview.md)
- [輸入字元集](input-character-set-entity-sql.md)
