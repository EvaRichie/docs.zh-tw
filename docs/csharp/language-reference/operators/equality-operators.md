---
title: 等號比較運算子 - C# 參考
description: 深入了解 C# 等號比較運算子與 C# 型別等號。
ms.date: 06/26/2019
author: pkulikov
f1_keywords:
- ==_CSharpKeyword
- '!=_CSharpKeyword'
helpviewer_keywords:
- comparison operators [C#]
- relational operators [C#]
- equality operator [C#]
- equals operator [C#]
- == operator [C#]
- inequality operator [C#]
- not equals operator [C#]
- '!= operator [C#]'
ms.openlocfilehash: 33215e2440b14fb888a6f0df5c220c891ebed0e2
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/11/2020
ms.locfileid: "88063090"
---
# <a name="equality-operators-c-reference"></a>等號比較運算子 (C# 參考)

[ `==` (相等的) ](#equality-operator-)和[ `!=` (不相等) ](#inequality-operator-)運算子會檢查其運算元是否相等。

## <a name="equality-operator-"></a>等號比較運算子 ==

等號比較運算子 `==` 會在其運算元相等時傳回 `true`，否則傳回 `false`。

### <a name="value-types-equality"></a>實值型別相等

若他們的值相等時，[內建實值型別](../builtin-types/value-types.md#built-in-value-types)的運算元就會相等：

[!code-csharp-interactive[value types equality](snippets/shared/EqualityOperators.cs#ValueTypesEquality)]

> [!NOTE]
> 對於、、、 `==` [ `<` `>` `<=` 和 `>=` ](comparison-operators.md)運算子而言，如果任何運算元不是 (<xref:System.Double.NaN?displayProperty=nameWithType> 或) 的數位，作業 <xref:System.Single.NaN?displayProperty=nameWithType> 的結果會是 `false` 。 這代表 `NaN` 的值皆不會大於、小於或等於任何其他 `double` (或 `float`) 的值，包括 `NaN`。 如需詳細資訊和範例，請參閱 <xref:System.Double.NaN?displayProperty=nameWithType> 或 <xref:System.Single.NaN?displayProperty=nameWithType> 參考文章。

若基礎整數型別的對應值相等時，相同[列舉](../builtin-types/enum.md)類型的兩個運算元就會相等。

使用者定義[結構](../builtin-types/struct.md)型別預設不支援 `==` 運算子。 若要支援 `==` 運算子，使用者定義結構必須[多載](operator-overloading.md)它。

從 C# 7.3 說起，`==` 及 `!=` 運算子是由 C# [tuples](../builtin-types/value-tuples.md) 所支援。 如需詳細資訊，請參閱「[元組類型](../builtin-types/value-tuples.md)」一文的「[元組相等](../builtin-types/value-tuples.md#tuple-equality)」一節。

### <a name="reference-types-equality"></a>參考型別相等

根據預設，當兩個參考型別的運算元參考相同物件時，兩者就相等：

[!code-csharp[reference type equality](snippets/shared/EqualityOperators.cs#ReferenceTypesEquality)]

如範例所示，使用者定義參考型別預設支援 `==` 運算子。 不過，參考型別可以多載 `==` 運算子。 若參考型別多載 `==` 運算子，請使用 <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> 方法檢查兩個該類型的參考是否參考相同的物件。

### <a name="string-equality"></a>字串相等

當兩個 [string](../builtin-types/reference-types.md#the-string-type) 運算元皆為 `null`，或兩個 string 執行個體的長度相同且在各字元位置擁有完全相同的字元，兩者就會相等：

[!code-csharp-interactive[string equality](snippets/shared/EqualityOperators.cs#StringEquality)]

這是區分大小寫的序數比較。 如需有關字串比較的詳細資訊，請參閱[如何在 C# 中比較字串](../../how-to/compare-strings.md)。

### <a name="delegate-equality"></a>委派等號

相同執行階段型別的兩個[委派](../../programming-guide/delegates/index.md)運算元都是 `null` 或其引動過程清單長度相同且每個位置都有相等的項目時，那兩個運算元相等：

[!code-csharp-interactive[delegate equality](snippets/shared/EqualityOperators.cs#DelegateEquality)]

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[委派相等運算子](~/_csharplang/spec/expressions.md#delegate-equality-operators)一節。

從語意相同之 [lambda 運算式](lambda-expressions.md)之評估產生的委派不相等，如下列範例所示：

[!code-csharp-interactive[from identical lambdas](snippets/shared/EqualityOperators.cs#IdenticalLambdas)]

## <a name="inequality-operator-"></a>不等比較運算子 !=

不等比較運算子 `!=` 會在其運算元不相等時傳回 `true`，否則傳回 `false`。 對於[內建類型](../builtin-types/built-in-types.md)的運算元，運算式 `x != y` 會產生與運算式 `!(x == y)` 相同的結果。 如需有關型別等號的詳細資訊，請參閱[等號比較運算子](#equality-operator-)一節。

下列範例示範 `!=` 運算子的用法：

[!code-csharp-interactive[non-equality examples](snippets/shared/EqualityOperators.cs#NonEquality)]

## <a name="operator-overloadability"></a>運算子是否可多載

使用者定義類型可以[多載](operator-overloading.md)`==` 和 `!=` 運算子。 如果型別多載兩個運算子的其中一個，它也必須多載另一個。

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[關係及類型測試運算子](~/_csharplang/spec/expressions.md#relational-and-type-testing-operators)一節。

## <a name="see-also"></a>另請參閱

- [C# 參考資料](../index.md)
- [C# 運算子與運算式](index.md)
- <xref:System.IEquatable%601?displayProperty=nameWithType>
- <xref:System.Object.Equals%2A?displayProperty=nameWithType>
- <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType>
- [相等比較](../../programming-guide/statements-expressions-operators/equality-comparisons.md)
- [比較運算子](comparison-operators.md)
