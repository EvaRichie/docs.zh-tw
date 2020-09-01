---
description: partial 方法 - C# 參考
title: partial 方法 - C# 參考
ms.date: 07/20/2015
f1_keywords:
- partialmethod_CSharpKeyword
helpviewer_keywords:
- partial methods [C#]
ms.assetid: 43f40242-17e0-4452-8573-090503ad3137
ms.openlocfilehash: d6c433fd30f6ec51355bdefee90d815783487c1b
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2020
ms.locfileid: "89134376"
---
# <a name="partial-method-c-reference"></a>partial 方法 (C# 參考)

部分方法會在部分型別的某一部分中定義其簽章，並在類型的另一部分中定義其實作。 部分方法可讓類別設計工具提供方法攔截程序，類似於事件處理常式，開發人員可以決定是否實作。 如果開發人員未提供實作，編譯器會在編譯時期移除簽章。 下列條件適用於部分方法：

- 部分型別的兩個部分中的簽章必須相符。

- 此方法必須傳回 void。

- 不允許存取修飾詞。 部分方法都是隱含私用。

下列範例顯示部分類別之兩個部分中定義的部分方法：

[!code-csharp[csrefKeywordsContextual#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsContextual/CS/csrefKeywordsContextual.cs#9)]

如需詳細資訊，請參閱[部分類別和方法](../../programming-guide/classes-and-structs/partial-classes-and-methods.md)。

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [部分類型](partial-type.md)
