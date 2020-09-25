---
title: 可為 Null 的結構類型 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: ae006fa9-997e-45bb-8a04-a7f62026171e
ms.openlocfilehash: fc2230401ef98c005ab52a845de37482c0dcf698
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91202259"
---
# <a name="nullable-structured-types-entity-sql"></a>可為 Null 的結構類型 (Entity SQL)

結構化型別的 `null` 執行個體是不存在的執行個體。 這與現有的執行個體 (所有的屬性都有 `null` 值) 不同。  
  
 本主題描述可為 Null 的結構化型別，其中包括哪些型別可為 Null，以及哪些程式碼模式會產生可為 Null 之結構化型別的 `null` 執行個體。  
  
## <a name="kinds-of-nullable-structured-types"></a>可為 Null 的結構化型別種類  

 可為 Null 的結構化型別有三種：  
  
- 資料列型別。  
  
- 複雜類型。  
  
- 實體類型。  
  
## <a name="code-patterns-that-produce-null-instances-of-structured-types"></a>產生結構化型別之 Null 執行個體的程式碼模式  

 下列案例會產生 `null` 執行個體：  
  
- 將 `null` 定形為結構化型別：  
  
    ```sql  
    TREAT (NULL AS StructuredType)  
    ```  
  
- 將基底型別向上轉型成衍生型別：  
  
    ```sql  
    TREAT (BaseType AS DerivedType)  
    ```  
  
- false 條件上的外部聯結 (Outer Join)：  
  
    ```sql  
    Collection1 LEFT OUTER JOIN Collection2  
    ON FalseCondition  
    ```  
  
     --或  
  
    ```sql  
    Collection1 RIGHT OUTER JOIN Collection2  
    ON FalseCondition  
    ```  
  
     --或  
  
    ```sql  
    Collection1 FULL OUTER JOIN Collection2  
    ON FalseCondition  
    ```  
  
- 為 `null` 參考取值：  
  
    ```sql  
    DEREF(NullRef)  
    ```  
  
- 從空的集合中取得 ANYELEMENT：  
  
    ```sql  
    ANYELEMENT(EmptyCollection)  
    ```  
  
- 檢查是否有結構化型別的 `null` 執行個體：  
  
    ```csharp  
    ...  
    for (int i = 0; i < reader.FieldCount; i++)  
    {  
        if (reader.IsDBNull(i))  
        {  
            Console.WriteLine("[NULL]");  
        }  
        else  
        {  
            Console.WriteLine(reader.GetValue(i).ToString());  
        }  
    }  
    ```  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 概觀](entity-sql-overview.md)
