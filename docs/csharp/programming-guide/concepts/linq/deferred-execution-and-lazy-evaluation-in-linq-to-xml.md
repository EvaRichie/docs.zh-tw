---
title: LINQ to XML 中的延後執行和延遲評估 (C#)
description: '查詢和軸作業可以在 c # 中使用延後執行。 瞭解順延強制和執行考慮的需求和優點。'
ms.date: 07/20/2015
ms.assetid: 8683d1b4-b7ec-407b-be12-906ebe958a09
ms.openlocfilehash: 8559505572404f895d75e0d9895f9ae2c07b795e
ms.sourcegitcommit: 04022ca5d00b2074e1b1ffdbd76bec4950697c4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87105465"
---
# <a name="deferred-execution-and-lazy-evaluation-in-linq-to-xml-c"></a>LINQ to XML 中的延後執行和延遲評估 (C#)
若要使用延後執行，通常會實作查詢和座標軸運算。 本主題說明延後執行的條件與優點以及一些實作考量。  
  
## <a name="deferred-execution"></a>延後執行  
 延後執行是指延遲評估運算式，直到實際需要其「實現的」** 值為止。 當您必須管理大型資料集合，尤其是在包含一系列鏈結之查詢或管理的程式中時，延後執行會明顯改善效能。 在最好的情況下，延後執行僅能單一逐一查看來源集合。  
  
 LINQ 技術可讓延後執行大量用於 <xref:System.Linq?displayProperty=nameWithType> 核心類別的成員以及各種 LINQ 命名空間中的擴充方法，例如，<xref:System.Xml.Linq.Extensions?displayProperty=nameWithType>。  
  
 在 Iterator 區塊中使用時，支援在 C# 語言中，透過 [yield](../../../language-reference/keywords/yield.md) 關鍵字 (以 `yield-return` 陳述式的形式) 直接支援延後執行。 此類 Iterator 必須傳回型別 <xref:System.Collections.IEnumerator> 或 <xref:System.Collections.Generic.IEnumerator%601> (或衍生型別) 的集合。  
  
## <a name="eager-vs-lazy-evaluation"></a>急切評估與延遲評估之比較  
 當您撰寫實作延後執行的方法時，您也必須決定要使用延遲評估或急切評估來實作方法。  
  
- 若為「延遲評估」**，來源集合的單一項目會在每次呼叫 Iterator 時進行處理。 這是實作 Iterator 的一般方式。  
  
- 若為「急切評估」**，第一次呼叫 Iterator 時，就會處理整個集合。 同時，可能也需要來源集合的暫存副本。 例如，<xref:System.Linq.Enumerable.OrderBy%2A> 方法必須在傳回第一個項目前，排序整個集合。  
  
 延遲評估通常會產生較好的效能，因為它會平均分散整個集合評估的負荷處理，並將暫存資料的使用率降到最低。 當然，對於某些運算而言，沒有具體化中繼結果之外的其他選擇。  
  
## <a name="next-steps"></a>後續步驟  
 此教學課程中的下一個主題說明延後執行：  
  
- [延後執行範例 (C#)](./deferred-execution-example.md)  
  
## <a name="see-also"></a>請參閱

- [教學課程：將查詢鏈結在一起 (C#)](./deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)
- [概念和術語 (函數式轉換) (C#)](./concepts-and-terminology-functional-transformation.md)
- [彙總作業 (C#)](./aggregation-operations.md)
- [yield](../../../language-reference/keywords/yield.md)
