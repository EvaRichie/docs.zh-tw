---
title: 分割資料
ms.date: 07/20/2015
ms.assetid: 69c59379-b66e-422c-b324-5b5c07760ef7
ms.openlocfilehash: 34749f9d7b137bade66b6103650871246c3cc532
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406842"
---
# <a name="partitioning-data-visual-basic"></a>分割資料（Visual Basic）
LINQ 中的分割是指將輸入序列分成兩個區段的作業，不用重新排列項目，然後傳回其中一個區段。  
  
 下圖顯示字元序列三種不同分割作業的結果。 第一項作業會傳回序列中的前三個項目。 第二項作業會略過前三個項目，傳回其餘項目。 第三個作業會略過序列中的前兩個項目，傳回接下來的三個元項目。  
  
 ![顯示三個 LINQ 分割作業的圖例。](./media/partitioning-data/linq-partitioning-operations.png)  
  
 分割序列的標準查詢運算子方法詳列於下一節。  
  
## <a name="operators"></a>運算子  
  
|運算子名稱|Description|Visual Basic 查詢運算式語法|相關資訊|  
|-------------------|-----------------|------------------------------------------|----------------------|  
|跳過|略過項目直至序列中指定的位置為止。|`Skip`|<xref:System.Linq.Enumerable.Skip%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Skip%2A?displayProperty=nameWithType>|  
|SkipWhile|根據述詞函式跳過項目，直到不符合條件的項目為止。|`Skip While`|<xref:System.Linq.Enumerable.SkipWhile%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.SkipWhile%2A?displayProperty=nameWithType>|  
|Take|採用序列中最多到指定位置為止的項目。|`Take`|<xref:System.Linq.Enumerable.Take%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Take%2A?displayProperty=nameWithType>|  
|TakeWhile|根據述詞函式採用項目，直到不符合條件的項目為止。|`Take While`|<xref:System.Linq.Enumerable.TakeWhile%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.TakeWhile%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-examples"></a>查詢運算式語法範例  
  
### <a name="skip"></a>跳過  
 下列程式碼範例會 `Skip` 在 Visual Basic 中使用子句，以略過字串陣列中的前四個字串，然後才傳回陣列中的其餘字串。  
  
 [!code-vb[CsLINQPartitioning#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#1)]  
  
### <a name="skipwhile"></a>SkipWhile  
 下列程式碼範例會使用 `Skip While` Visual Basic 中的子句，略過陣列中的字串，而字串的第一個字母是 "a"。 系統會傳回陣列中的其餘字串。  
  
 [!code-vb[CsLINQPartitioning#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#2)]  
  
### <a name="take"></a>Take  
 下列程式碼範例會 `Take` 在 Visual Basic 中使用子句，以傳回字串陣列中的前兩個字串。  
  
 [!code-vb[CsLINQPartitioning#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#3)]  
  
### <a name="takewhile"></a>TakeWhile  
 下列程式碼範例會使用 `Take While` Visual Basic 中的子句，從陣列傳回字串，而字串長度為五個或更少。  
  
 [!code-vb[CsLINQPartitioning#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/CsLINQPartitioning/VB/Partitioning.vb#4)]  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Linq>
- [標準查詢運算子概觀 (Visual Basic)](standard-query-operators-overview.md)
- [Skip 子句](../../../language-reference/queries/skip-clause.md)
- [Skip While 子句](../../../language-reference/queries/skip-while-clause.md)
- [Take 子句](../../../language-reference/queries/take-clause.md)
- [Take While 子句](../../../language-reference/queries/take-while-clause.md)
