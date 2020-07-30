---
title: 標準查詢運算子的查詢運算式語法 (C#)
description: 瞭解標準查詢運算子的查詢運算式語法。 查看具有對等查詢運算式子句的標準查詢運算子清單。
ms.date: 07/20/2015
ms.assetid: e1e17ef2-68ff-4c26-b6e2-015668227fa5
ms.openlocfilehash: b43d2095ee7d059be6f834b576ca0e6ab0a87585
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87299119"
---
# <a name="query-expression-syntax-for-standard-query-operators-c"></a>標準查詢運算子的查詢運算式語法 (C#)
某些更常用的標準查詢運算子具有專用 C# 語言關鍵字語法，可將它們呼叫為「查詢運算式」** 的一部分。 相較於「方法」** 對等項目，查詢運算式是一個不同且更具可讀性的表示查詢形式。 查詢運算式子句會在編譯時期轉譯成查詢方法的呼叫。  
  
## <a name="query-expression-syntax-table"></a>查詢運算式語法表  
 下表列出具有對等查詢運算式子句的標準查詢運算子。  
  
|方法|C# 查詢運算式語法|  
|------------|---------------------------------|  
|<xref:System.Linq.Enumerable.Cast%2A>|使用明確類型範圍變數，例如：<br /><br /> `from int i in numbers`<br /><br /> （如需詳細資訊，請參閱[from 子句](../../../language-reference/keywords/from-clause.md)）。|  
|<xref:System.Linq.Enumerable.GroupBy%2A>|`group … by`<br /><br /> -或-<br /><br /> `group … by … into …`<br /><br /> (如需詳細資訊，請參閱 [group 子句](../../../language-reference/keywords/group-clause.md))。|  
|<xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29>|`join … in … on … equals … into …`<br /><br /> (如需詳細資訊，請參閱 [join 子句](../../../language-reference/keywords/join-clause.md))。|  
|<xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29>|`join … in … on … equals …`<br /><br /> (如需詳細資訊，請參閱 [join 子句](../../../language-reference/keywords/join-clause.md))。|  
|<xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby`<br /><br /> (如需詳細資訊，請參閱 [orderby 子句](../../../language-reference/keywords/orderby-clause.md))。|  
|<xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby … descending`<br /><br /> (如需詳細資訊，請參閱 [orderby 子句](../../../language-reference/keywords/orderby-clause.md))。|  
|<xref:System.Linq.Enumerable.Select%2A>|`select`<br /><br /> (如需詳細資訊，請參閱 [select 子句](../../../language-reference/keywords/select-clause.md))。|  
|<xref:System.Linq.Enumerable.SelectMany%2A>|多個 `from` 子句。<br /><br /> （如需詳細資訊，請參閱[from 子句](../../../language-reference/keywords/from-clause.md)）。|  
|<xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby …, …`<br /><br /> (如需詳細資訊，請參閱 [orderby 子句](../../../language-reference/keywords/orderby-clause.md))。|  
|<xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`orderby …, … descending`<br /><br /> (如需詳細資訊，請參閱 [orderby 子句](../../../language-reference/keywords/orderby-clause.md))。|  
|<xref:System.Linq.Enumerable.Where%2A>|`where`<br /><br /> （如需詳細資訊，請參閱[where 子句](../../../language-reference/keywords/where-clause.md)）。|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Linq.Enumerable>
- <xref:System.Linq.Queryable>
- [標準查詢運算子概觀 (C#)](./standard-query-operators-overview.md)
- [依據執行方式將標準查詢運算子分類 (C#)](./classification-of-standard-query-operators-by-manner-of-execution.md)
