---
title: 限制存取子的存取範圍 - C# 程式設計手冊
description: 'C # 中屬性的 get 和 set 存取子，預設具有相同的可見度或存取層級，如同它們所屬的屬性。 您可以限制存取。'
ms.date: 07/20/2015
helpviewer_keywords:
- read-only properties [C#]
- read-only indexers [C#]
- accessors [C#]
- properties [C#], read-only
- asymmetric accessor accessibility [C#]
- indexers [C#], read-only
ms.assetid: 6e655798-e112-4301-a680-6310a6e012e1
ms.openlocfilehash: 18fd1d58dc6125b5180118b2e0d3edc885a4b971
ms.sourcegitcommit: 3d84eac0818099c9949035feb96bbe0346358504
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86863964"
---
# <a name="restricting-accessor-accessibility-c-programming-guide"></a>限制存取子的存取範圍 (C# 程式設計手冊)
屬性或索引子的 [get](../../language-reference/keywords/get.md) 和 [set](../../language-reference/keywords/set.md) 部分稱為「存取子」**。 根據預設，這些存取子具有其所屬屬性或索引子的相同可見度或存取層級。 如需詳細資訊，請參閱[存取範圍層級](../../language-reference/keywords/accessibility-levels.md)。 不過，限制其中一個存取子的存取權時，這有時十分有用。 一般而言，這包含限制 `set` 存取子的存取範圍，同時保留可公開存取的 `get` 存取子。 例如：  
  
 [!code-csharp[csProgGuideIndexers#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#6)]  
  
 在此範例中，稱為 `Name` 的屬性定義 `get` 和 `set` 存取子。 `get` 存取子會接收屬性本身的存取範圍階層 (在此情況下為 `public`)，同時將 [protected](../../language-reference/keywords/protected.md) 存取修飾詞套用至存取子本身以明確限制 `set` 存取子。  
  
## <a name="restrictions-on-access-modifiers-on-accessors"></a>存取子的存取修飾詞限制  
 在屬性或索引子上使用存取子修飾詞受限於這些條件：  
  
- 您無法在介面或明確[介面](../../language-reference/keywords/interface.md)成員實作上使用存取子修飾詞。  
  
- 只有在屬性或索引子同時具有 `set` 和 `get` 存取子時，才能使用存取修飾詞。 在此情況下，允許只在兩個存取子的其中一個上使用修飾詞。  
  
- 如果屬性或索引子具有 [override](../../language-reference/keywords/override.md) 修飾詞，則存取子修飾詞必須符合已覆寫存取子的存取子 (如果有的話)。  
  
- 存取子上的存取範圍層級必須比屬性或索引子本身上的存取範圍層級更為嚴格。  
  
## <a name="access-modifiers-on-overriding-accessors"></a>覆寫存取子上的存取修飾詞  
 當您覆寫屬性或索引子時，覆寫端程式碼必須可以存取覆寫的存取子。 此外，屬性/索引子及其存取子的存取範圍必須符合已覆寫的對應屬性/索引子及其存取子。 例如：  
  
 [!code-csharp[csProgGuideIndexers#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#7)]  
  
## <a name="implementing-interfaces"></a>實作介面  
 當您使用存取子實作介面時，存取子不能有存取修飾詞。 不過，如果您使用一個存取子 (例如 `get`) 實作介面，其他存取子可以有存取修飾詞，如下列範例所示：  
  
 [!code-csharp[csProgGuideIndexers#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#8)]  
  
## <a name="accessor-accessibility-domain"></a>存取子存取範圍定義域  
 如果您在存取子上使用存取修飾詞，這個修飾詞會判斷存取子的[存取範圍定義域](../../language-reference/keywords/accessibility-domain.md)。  
  
 如果您未在存取子上使用存取修飾詞，屬性或索引子的存取範圍層級會判斷存取子的存取範圍定義域。  
  
## <a name="example"></a>範例  
 下列範例包含三個類別：`BaseClass`、`DerivedClass` 和 `MainClass`。 這兩個類別的 `BaseClass`、`Name` 和 `Id` 上有兩個屬性。 此範例示範當您使用 [protected](../../language-reference/keywords/protected.md) 或 [private](../../language-reference/keywords/private.md) 這類限制存取修飾詞時，`BaseClass` 上的 `Id` 屬性可以隱藏 `DerivedClass` 上的 `Id` 屬性。 因此，當您將值指派給這個屬性時，會改為呼叫 `BaseClass` 類別上的屬性。 將存取修飾詞取代為 [public](../../language-reference/keywords/public.md) 會將屬性設為可存取。  
  
 此範例也會示範 `DerivedClass` 中 `Name` 屬性之 `set` 存取子上的 `private` 或 `protected` 這類限制性存取修飾詞防止存取存取子，並在您指派給它時產生錯誤。  
  
 [!code-csharp[csProgGuideIndexers#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#5)]  
  
## <a name="comments"></a>註解  
 請注意，如果您將宣告 `new private string Id` 取代為 `new public string Id`，則會取得輸出：  
  
 `Name and ID in the base class: Name-BaseClass, ID-BaseClass`  
  
 `Name and ID in the derived class: John, John123`  
  
## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [屬性](./properties.md)
- [索引子](../indexers/index.md)
- [存取修飾詞](./access-modifiers.md)
