---
description: 存取範圍定義域 - C# 參考
title: 存取範圍定義域 - C# 參考
ms.date: 07/20/2015
helpviewer_keywords:
- accessibility domain [C#]
ms.assetid: 8af779c1-275b-44be-a864-9edfbca71bcc
ms.openlocfilehash: 35fc619dd284ff9915662ba48fa06dd295cbbf42
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91168838"
---
# <a name="accessibility-domain-c-reference"></a>存取範圍定義域 (C# 參考)

成員的存取範圍定義域指定可參考成員的程式區段。 如果成員巢狀在另一個類型內，則其存取範圍定義域是由成員的[存取範圍層級](./accessibility-levels.md)和立即包含類型的存取範圍定義域所決定。  
  
 最上層類型的存取範圍定義域是至少在其中宣告之專案的程式文字。 亦即，定義域包括此專案的所有原始程式檔。 巢狀型別的存取範圍定義域是至少在其中宣告之類型的程式文字。 亦即，定義域是包括所有巢狀型別的類型主體。 巢狀型別的存取範圍定義域絕不會超過包含類型的存取範圍定義域。 下列範例示範這些概念。  
  
## <a name="example"></a>範例  

 這個範例包含最上層類型 `T1` 以及兩個巢狀類別 `M1` 和 `M2`。 這些類別包含具有不同已宣告存取範圍的欄位。 在 `Main` 方法中，註解在每個陳述式的後面，表示每個成員的存取領域。 請注意，嘗試參考無法存取之成員的語句會被標記為批註。如果您想要查看因參考無法存取的成員而造成的編譯器錯誤，請一次移除一個批註。  
  
[!code-csharp[csrefKeywordsModifiers#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#4)]
  
## <a name="c-language-specification"></a>C# 語言規格  

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](./index.md)
- [存取修飾詞](./access-modifiers.md)
- [協助工具層級](./accessibility-levels.md)
- [使用協助工具層級的限制](./restrictions-on-using-accessibility-levels.md)
- [存取修飾詞](../../programming-guide/classes-and-structs/access-modifiers.md)
- [public](./public.md)
- [private](./private.md)
- [protected](./protected.md)
- [internal](./internal.md)
