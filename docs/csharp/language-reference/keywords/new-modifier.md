---
title: new 修飾詞 - C# 參考
ms.date: 07/20/2015
helpviewer_keywords:
- new modifier keyword [C#]
ms.assetid: a2e20856-33b9-4620-b535-a60dbce8349b
ms.openlocfilehash: 529d77b0a66a8a3cedfe7a400af0fb34dd653322
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795166"
---
# <a name="new-modifier-c-reference"></a>new 修飾詞 (C# 參考)

`new` 關鍵字做為宣告修飾詞使用時，會明確隱藏繼承自基底類別的成員。 當您隱藏繼承的成員時，該成員的衍生版本就會取代基底類別版本。 雖然您可以在不使用 `new` 修飾詞的情況下隱藏成員，但是編譯器會發出警告。 如果您使用 `new` 明確隱藏成員，它會隱藏這個警告。

您也可以使用 `new` 關鍵字來[建立型別執行個體](../operators/new-operator.md)或作為[泛型型別條件約束](./new-constraint.md)。

若要隱藏繼承的成員，請在衍生類別中使用相同的成員名稱宣告該成員，並且使用 `new` 關鍵讚加以修飾。 例如：

[!code-csharp[csrefKeywordsOperator#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#8)]

在這個範例中，`BaseC.Invoke` 是藉由 `DerivedC.Invoke` 隱藏。 `x` 欄位不受影響，因為它不是由類似的名稱所隱藏。

經由繼承隱藏的名稱會採用下列其中一種格式：

- 一般而言，在類別或結構中引入的常數、欄位、屬性或類型會隱藏共用其名稱的所有基底類別成員。 不過有一些特殊案例。 例如，如果您宣告名為 `N` 的新欄位採用不可叫用的類型，而且基底類型將 `N` 宣告為方法，則新欄位不會隱藏引動過程語法中的基底宣告。 如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[成員查閱](~/_csharplang/spec/expressions.md#member-lookup)一節。

- 類別或結構中引入的方法會隱藏在基底類別中共用該名稱的屬性、欄位和類型。 它也會隱藏所有具有相同簽章的基底類別方法。

- 類別或結構中引入的索引子會隱藏所有具有相同簽章的基底類別索引子。

在相同的成員上同時使用 `new` 和 [override](override.md) 是不正確的，因為這兩個修飾詞在意義上互斥。 `new` 修飾詞會以相同名稱建立新成員，並使原始成員隱藏。 `override` 修飾詞會擴充繼承成員的實作。

在未隱藏繼承的成員之宣告中使用 `new` 修飾詞會產生警告。

## <a name="example"></a>範例

在這個範例中，基底類別 `BaseC` 以及衍生類別 `DerivedC` 會使用相同的欄位名稱 `x`，而該欄位名稱會隱藏繼承之欄位的值。 範例中將示範 `new` 修飾詞的用法。 另外還會示範如何使用完整限定名稱存取基底類別的隱藏成員。

[!code-csharp[csrefKeywordsOperator#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#9)]

## <a name="example"></a>範例

在這個範例中，巢狀類別會隱藏在基底類別中具有相同名稱的類別。 這個範例將示範如何使用 `new` 修飾詞消除警告訊息，以及如何使用完整限定名稱存取隱藏的類別成員。

[!code-csharp[csrefKeywordsOperator#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#10)]

如果您移除 `new` 修飾詞，程式仍會進行編譯和執行，但是您會收到下列警告：

```text
The keyword new is required on 'MyDerivedC.x' because it hides inherited member 'MyBaseC.x'.
```

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的 [new 修飾詞](~/_csharplang/spec/classes.md#the-new-modifier)一節。

## <a name="see-also"></a>請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)
- [修飾詞](index.md)
- [使用 Override 和 New 關鍵字進行版本設定](../../programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords.md)
- [了解使用 Override 和 New 關鍵字的時機](../../programming-guide/classes-and-structs/knowing-when-to-use-override-and-new-keywords.md)
