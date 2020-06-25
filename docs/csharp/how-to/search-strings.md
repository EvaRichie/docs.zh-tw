---
title: '如何搜尋字串（c # 指南）'
ms.date: 02/21/2018
helpviewer_keywords:
- searching strings [C#]
- strings [C#], searching with String methods
- strings [C#], searching with regular expressions
ms.assetid: fb1d9a6d-598d-4a35-bd5f-b86012edcb2b
ms.openlocfilehash: 34f9f2df11f9b7c51fcec2f8475a50ccf4c5e220
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324133"
---
# <a name="how-to-search-strings"></a>如何搜尋字串

您可以使用兩種主要策略來搜尋字串中的文字。 <xref:System.String> 類別的方法會搜尋特定文字。 規則運算式會搜尋文字中的模式。

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

[字串](../language-reference/builtin-types/reference-types.md#the-string-type)類型，這是 <xref:System.String?displayProperty=nameWithType> 類別的別名，提供一些有用的方法來搜尋字串的內容。 它們是 <xref:System.String.Contains%2A>、<xref:System.String.StartsWith%2A><xref:System.String.EndsWith%2A>、<xref:System.String.IndexOf%2A>、<xref:System.String.LastIndexOf%2A>。 <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 類別提供豐富的詞彙來搜尋文字中的模式。 在本文中，您了解這些技術，以及如何選擇您需求的最佳方法。

## <a name="does-a-string-contain-text"></a>字串是否包含文字？

<xref:System.String.Contains%2A?displayProperty=nameWithType>、 <xref:System.String.StartsWith%2A?displayProperty=nameWithType> 和方法會 <xref:System.String.EndsWith%2A?displayProperty=nameWithType> 搜尋字串中的特定文字。 下列範例顯示每個方法，以及使用不區分大小寫搜尋的變化：

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/SearchStrings.cs" id="Snippet1":::

上述範例示範這些方法的使用重點。 搜尋預設會**區分大小寫**。 您可以使用 <xref:System.StringComparison.CurrentCultureIgnoreCase?displayProperty=nameWithType> 列舉值來指定不區分大小寫的搜尋。

## <a name="where-does-the-sought-text-occur-in-a-string"></a>所搜尋文字在字串中的位置？

<xref:System.String.IndexOf%2A> 和 <xref:System.String.LastIndexOf%2A> 方法也會搜尋字串中的文字。 這些方法會傳回所搜尋文字的位置。 如果找不到文字，則會傳回 `-1`。 下列範例示範如何搜尋 "methods" 這個單字的第一個和最後一個相符項目，並在其間顯示文字。

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/SearchStrings.cs" id="Snippet2":::

## <a name="finding-specific-text-using-regular-expressions"></a>使用規則運算式來尋找特定文字

<xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 類別可以用來搜尋字串。 這些搜尋的複雜性範圍可以從簡單到複雜文字模式。

下列程式碼範例會搜尋句子中的 "the" 或 "their" 單字，但忽略大小寫。 靜態方法 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 會執行搜尋。 您為其指定要搜尋的字串和搜尋模式。 在此情況下，第三個引數指定不區分大小寫的搜尋。 如需詳細資訊，請參閱 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=nameWithType> 。

搜尋模式描述您搜尋的文字。 下表描述搜尋模式的每個項目  （下表使用單一 `\` ，必須 `\\` 在 c # 字串中將其轉義為）。

| 模式  | 意義                          |
|----------|----------------------------------|
| `the`    | 比對文字 "the"             |
| `(eir)?` | 比對 "eir" 的 0 或 1 個出現次數 |
| `\s`     | 比對空白字元    |

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/SearchStrings.cs" id="Snippet3":::

> [!TIP]
> 當您搜尋完全相符的字串時，`string` 方法通常是較好的選擇。 當您在來源字串中搜尋某個模式時，正則運算式會更好。

## <a name="does-a-string-follow-a-pattern"></a>字串遵循模式嗎？

下列程式碼使用規則運算式來驗證陣列中每個字串的格式。 驗證需要每個字串具有電話號碼的形式，其中數字的三個群組以連字號分隔、前兩個群組包含三位數，而第三個群組包含四位數。 搜尋模式使用規則運算式 `^\\d{3}-\\d{3}-\\d{4}$`。 如需詳細資訊，請參閱[規則運算式語言 - 快速參考](../../standard/base-types/regular-expression-language-quick-reference.md)。

| 模式 | 意義                             |
|---------|-------------------------------------|
| `^`     | 比對字串的開頭 |
| `\d{3}` | 僅比對 3 位數的字元  |
| `-`     | 比對 '-' 字元           |
| `\d{3}` | 僅比對 3 位數的字元  |
| `-`     | 比對 '-' 字元           |
| `\d{4}` | 僅比對 4 位數的字元  |
| `$`     | 比對字串的結尾       |

:::code language="csharp" interactive="try-dotnet-method" source="../../../samples/snippets/csharp/how-to/strings/SearchStrings.cs" id="Snippet4":::

此單一搜尋模式會比對許多有效字串。 規則運算式較適合用來搜尋或驗證模式，而不是單一文字字串。

## <a name="see-also"></a>另請參閱

- [C# 程式設計手冊](../programming-guide/index.md)
- [字串](../programming-guide/strings/index.md)
- [LINQ 和字串](../programming-guide/concepts/linq/linq-and-strings.md)
- <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType>
- [.NET Framework 正則運算式](../../standard/base-types/regular-expressions.md)
- [正則運算式語言-快速參考](../../standard/base-types/regular-expression-language-quick-reference.md)
- [在 .NET 中使用字串的最佳作法](../../standard/base-types/best-practices-strings.md)
