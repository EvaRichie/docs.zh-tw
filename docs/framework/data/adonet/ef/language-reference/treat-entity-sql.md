---
title: TREAT (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5b77f156-55de-4cb4-8154-87f707d4c635
ms.openlocfilehash: bb41c0fed944ce4db11878b9213a62c6f851418e
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201040"
---
# <a name="treat-entity-sql"></a>TREAT (Entity SQL)

將特定基底類型的物件視為所指定之衍生型別的物件。  
  
## <a name="syntax"></a>語法  
  
```sql  
TREAT ( expression as type)  
```  
  
## <a name="arguments"></a>引數  

 `expression`  
 任何傳回實體的有效查詢運算式。  
  
> [!NOTE]
> 所指定運算式的型別必須是所指定資料型別的子型別，或者此資料型別必須是運算式之型別的子型別。  
  
 `type`  
 任何實體類型。 此型別必須以命名空間 (Namespace) 限定。  
  
> [!NOTE]
> 所指定的運算式必須是所指定資料型別的子型別，或者此資料型別必須是此運算式的子型別。  
  
## <a name="return-value"></a>傳回值  

 屬於所指定資料型別的值。  
  
## <a name="remarks"></a>備註  

 TREAT 是用來在兩個相關類別之間執行向上轉型。 舉例來講，假設 `Employee` 是衍生自 `Person` 而 p 是 `Person`型別，則 `TREAT(p AS NamespaceName.Employee)` 會將泛型 `Person` 執行個體向上轉型成為 `Employee`；換言之，它可以讓您將 p 視為 `Employee`。  
  
 TREAT 是使用於繼承的情況下，在這種情況下您可以執行類似下列的查詢：  
  
```sql  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)
```  
  
 這個查詢將 `Person` 實體向上轉型成為 `Employee` 型別。 如果 p 的值實際上不是 `Employee`型別，此運算式將會產生值 `null`。  
  
> [!NOTE]
> 指定的運算式 `Employee` 必須是指定之資料類型的子類型 `Person` ，或是資料類型必須是運算式的子類型。 否則此運算式將會造成編譯時期錯誤。  
  
 下表所示為 TREAT 在某些一般模式及一些較不常見的模式中的行為。 所有例外狀況都是在叫用提供者之前從用戶端擲回：  
  
|模式|行為|  
|-------------|--------------|  
|`TREAT (null AS EntityType)`|傳回 `DbNull`。|  
|`TREAT (null AS ComplexType)`|擲回例外狀況。|  
|`TREAT (null AS RowType)`|擲回例外狀況。|  
|`TREAT (EntityType AS EntityType)`|傳回 `EntityType` 或 `null`。|  
|`TREAT (ComplexType AS ComplexType)`|擲回例外狀況。|  
|`TREAT (RowType AS RowType)`|擲回例外狀況。|  
  
## <a name="example"></a>範例  

 下列 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查詢使用 TREAT 運算子將 Course 型別的物件轉換成 OnsiteCourse 型別的物件集合。 此查詢是以 [School Model](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100))為基礎。  
  
 [!code-sql[DP EntityServices Concepts#TREAT_ISOF](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#treat_isof)]  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 參考](entity-sql-reference.md)
- [可為 Null 的結構類型](nullable-structured-types-entity-sql.md)
