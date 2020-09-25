---
title: Null 常值和類型推斷 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: edd56afb-af1b-4e7d-b210-cb8998143426
ms.openlocfilehash: 5797c9f55b1a1c89cc27787af6f9ad7bfffc5767
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91185063"
---
# <a name="null-literals-and-type-inference-entity-sql"></a>Null 常值和類型推斷 (Entity SQL)

Null 常值與 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 型別系統中的任何型別都相容。 不過，若要正確推斷 null 常值的型別，請 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 在可使用 null 常值的位置上強加特定條件約束。  
  
## <a name="typed-nulls"></a>具型別的 Null  

 具型別的 Null 可以在任何地方使用。 具型別的 Null 不需要型別推斷，因為該型別是已知的。 例如，您可以使用下列 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 建構來建構 Int16 型別的 Null：  
  
 `(cast(null as Int16))`  
  
## <a name="free-floating-null-literals"></a>自由浮動 Null 常值  

 自由浮動 Null 常值可以在以下內容中使用：  
  
- 當做 CAST 或 TREAT 運算式的引數。 建議使用這個方式來產生具型別的 Null 運算式。  
  
- 當做方法或函式的引數。 套用標準多載規則。  
  
- 當做算術運算式的其中一個引數，例如 +、- 或 /。 其他引數不能是 Null 常值，否則無法進行型別推斷。  
  
- 當做邏輯運算式的任何引數 (AND、OR 或 NOT)。 已知所有引數都具有 Boolean 型別。  
  
- 當做 IS NULL 或 IS NOT NULL 運算式的引數。  
  
- 當做 LIKE 運算式的其中一個或多個引數。 所有引數都必須是字串。  
  
- 當做具名型別建構函式 (Constructor) 的其中一個或多個引數。  
  
- 當做多重集 (Multiset) 建構函式的其中一個或多個引數。 多重集建構函式至少必須有一個引數為非 Null 常值的運算式。  
  
- 當做 CASE 運算式中的其中一個或多個 THEN 或 ELSE 運算式。 CASE 運算式中至少必須有一個 THEN 或 ELSE 運算式為 Null 常值以外的運算式。  
  
 自由浮動 Null 常值不能在其他案例中使用。 例如，不能當做資料列建構函式的引數。  
  
## <a name="see-also"></a>另請參閱

- [Entity SQL 概觀](entity-sql-overview.md)
