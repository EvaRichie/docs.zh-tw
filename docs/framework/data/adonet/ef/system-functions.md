---
title: 系統函式
ms.date: 03/30/2017
ms.assetid: b7c71b58-09e6-44ce-a3e5-a0fdb892fb86
ms.openlocfilehash: 0d46429ac958e6f5db4d51947669784303af783b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91156494"
---
# <a name="system-functions"></a>系統函式

.NET Framework Data Provider for SQL Server (SqlClient) 提供下列系統函式：  
  
|函式|描述|  
|--------------|-----------------|  
|`CHECKSUM (` `value`, [`value`, [`value`]]`)`|傳回總和檢查碼值。 `CHECKSUM` 用來建構雜湊索引。<br /><br /> **引數**<br /><br /> `value`：、、、、、、、、、、 `Boolean` `Byte` `Int16` `Int32` `Int64` `Single` `Decimal` `Double` `DateTime` `String` `Binary` 或 `Guid` 。 您可以指定一個、兩個或三個值。<br /><br /> **傳回值**<br /><br /> 指定之運算式的絕對值。<br /><br /> **範例**<br /><br /> `SqlServer.CHECKSUM(10,100,1000.0)`|  
|`CURRENT_TIMESTAMP ()`|採用 SQL Server 的內部格式，為 `DateTime` 值產生目前的日期和時間 (在 SQL Server 2008 中，精確度為 7，而在 SQL Server 2005 中，精確度為 3 )。<br /><br /> **傳回值**<br /><br /> `DateTime` 形式的目前系統日期和時間。<br /><br /> **範例**<br /><br /> `SqlServer.CURRENT_TIMESTAMP()`|  
|`CURRENT_ USER` `()`|傳回目前使用者的名稱。<br /><br /> **傳回值**<br /><br /> ASCII `String`。<br /><br /> **範例**<br /><br /> `SqlServer.CURRENT_USER()`|  
|`DATALENGTH` `(` `expression` `)`|傳回用來代表任何運算式的位元組數目。<br /><br /> **引數**<br /><br /> `expression`：、、、、、、、、、、、、 `Boolean` `Byte` `Int16` `Int32` `Int64` `Single` `Decimal` `Double` `DateTime` `Time` `DateTimeOffset` `String` `Binary` 或 `Guid` 。<br /><br /> **傳回值**<br /><br /> `Int32` 形式的屬性大小。<br /><br /> **範例**<br /><br /> `SELECT VALUE SqlServer.DATALENGTH(P.Name)FROM`<br /><br /> `AdventureWorksEntities.Product AS P`|  
|`HOST_NAME()`|傳回工作站名稱。<br /><br /> **傳回值**<br /><br /> Unicode `String`。<br /><br /> **範例**<br /><br /> `SqlServer.HOST_NAME()`|  
|`ISDATE(` `expression` `)`|判斷輸入運算式是否為有效的日期。<br /><br /> **引數**<br /><br /> `expression`：、、、、、、、、、、、、 `Boolean` `Byte` `Int16` `Int32` `Int64` `Single` `Decimal` `Double` `DateTime` `Time` `DateTimeOffset` `String` `Binary` 或 `Guid` 。<br /><br /> **傳回值**<br /><br /> `Int32`。 如果輸入運算式是有效的日期，就是一 (1)， 否則為零 (0)。<br /><br /> **範例**<br /><br /> `SqlServer.ISDATE('1/1/2006')`|  
|`ISNUMERIC(` `expression` `)`|判斷運算式是否為有效的數值類型。<br /><br /> **引數**<br /><br /> `expression`：、、、、、、、、、、、、 `Boolean` `Byte` `Int16` `Int32` `Int64` `Single` `Decimal` `Double` `DateTime` `Time` `DateTimeOffset` `String` `Binary` 或 `Guid` 。<br /><br /> **傳回值**<br /><br /> `Int32`。 如果輸入運算式是有效的日期，就是一 (1)， 否則為零 (0)。<br /><br /> **範例**<br /><br /> `SqlServer.ISNUMERIC('21')`|  
|`NEWID()`|建立 Guid 型別的唯一值。<br /><br /> **傳回值**<br /><br /> `Guid`。<br /><br /> **範例**<br /><br /> `SqlServer.NEWID()`|  
|`USER_NAME(` `id` `)`|傳回指定識別碼的資料庫使用者名稱。<br /><br /> **引數**<br /><br /> `expression`：與資料庫使用者相關聯的 `Int32` 識別碼。<br /><br /> **傳回值**<br /><br /> Unicode `String`。<br /><br /> **範例**<br /><br /> `SqlServer.USER_NAME(0)`|  
  
 如需 SqlClient 支援之函式的詳細資訊 `String` ，請參閱 [ (transact-sql) 的字串函數 ](/sql/t-sql/functions/string-functions-transact-sql)。
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 語言](./language-reference/entity-sql-language.md)
- [適用於 Entity Framework 的 SqlClient 函式](sqlclient-for-ef-functions.md)
