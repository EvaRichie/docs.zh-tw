---
title: USING (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 20f58b8f-6070-4456-b7e8-5ff3d6269273
ms.openlocfilehash: bdab81ed8acae5e757de0a669922dc79d0303ee4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203588"
---
# <a name="using-entity-sql"></a>USING (Entity SQL)

指定查詢運算式中使用的命名空間 (Namespace)。  
  
## <a name="syntax"></a>語法  
  
```sql  
USING [ alias = ] namespace  
```  
  
## <a name="arguments"></a>引數  

 `alias`  
 指定較短的別名 (Alias)，以便限定命名空間。  
  
 `namespace`  
 任何有效的命名空間。  
  
## <a name="example"></a>範例  

 下列 Entity SQL 查詢會使用 USING 運算子來指定查詢運算式中使用的命名空間。 若要編譯及執行此查詢，請遵循以下步驟：  
  
1. 依照 how [to：執行傳回 PrimitiveType 結果的查詢](../how-to-execute-a-query-that-returns-primitivetype-results.md)中的程式操作。  
  
2. 將下列查詢當成引數，傳遞至 `ExecutePrimitiveTypeQuery` 方法：  
  
```csharp
using SqlServer; RAND()  
```  
  
## <a name="see-also"></a>另請參閱

- [命名空間](namespaces-entity-sql.md)
- [Entity SQL 參考](entity-sql-reference.md)
