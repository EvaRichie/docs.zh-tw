---
description: orderby 子句 - C# 參考
title: orderby 子句 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- orderby
- orderby_CSharpKeyword
helpviewer_keywords:
- orderby clause [C#]
- orderby keyword [C#]
ms.assetid: 21f87f48-d69d-4e95-9a52-6fec47b37e1f
ms.openlocfilehash: 2f64b45ff252c7cc02e56c465da21ccc5e861aec
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89142345"
---
# <a name="orderby-clause-c-reference"></a>orderby 子句 (C# 參考)

在查詢運算式中，`orderby` 子句可讓傳回的序列或子序列 (群組) 以遞增或遞減順序排序。 您可以指定多個索引鍵，以便執行一或多個次要排序作業。 排序是由項目類型的預設比較子執行。 預設排序順序為遞增。 您也可以指定自訂比較子。 不過，它只有在使用以方法為基礎的語法時才可用。 如需詳細資訊，請參閱[排序資料](../../programming-guide/concepts/linq/sorting-data.md)。

## <a name="example"></a>範例

在下列範例中，第一個查詢會依照從 A 開始的字母順序排序字組，第二個查詢則以遞減順序排序相同的字組 (`ascending` 關鍵字是預設排序值，而且可以省略)。

[!code-csharp[cscsrefQueryKeywords#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Orderby.cs#20)]

## <a name="example"></a>範例

下列範例會對學生的姓氏執行主要排序，然後對其名字執行次要排序。

[!code-csharp[cscsrefQueryKeywords#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Orderby.cs#22)]

## <a name="remarks"></a>備註

在編譯時期，`orderby` 子句會轉譯為 <xref:System.Linq.Enumerable.OrderBy%2A> 方法的呼叫。 `orderby` 子句中的多個索引鍵翻譯為 <xref:System.Linq.Enumerable.ThenBy%2A> 方法呼叫。

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [LINQ)  (查詢關鍵字 ](query-keywords.md)
- [C# 中的 LINQ](../../linq/index.md)
- [group 子句](group-clause.md)
- [Language Integrated Query (LINQ)](../../programming-guide/concepts/linq/index.md)
