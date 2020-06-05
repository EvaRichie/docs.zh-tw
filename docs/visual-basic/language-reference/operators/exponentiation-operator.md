---
title: ^ 運算子
ms.date: 07/20/2015
f1_keywords:
- vb.^
helpviewer_keywords:
- raising numbers to powers
- ^ operator [Visual Basic], exponentiation
- square operator [Visual Basic]
- ^ operator [Visual Basic]
- exponentiation operator [Visual Basic]
- exponent
- numbers [Visual Basic], rasing
- powers
- arithmetic operators [Visual Basic], exponentiation
ms.assetid: d89a1ca8-83da-4784-a87b-a9d7dceb3f62
ms.openlocfilehash: e139becf74ae367266a23513e18d0bdbdd24cdea
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371384"
---
# <a name="-operator-visual-basic"></a>^ 運算子 (Visual Basic)

將一數值對另一數值做乘冪運算。

## <a name="syntax"></a>語法

```vb
number ^ exponent
```

## <a name="parts"></a>組件

`number`\
必要。 任何數值運算式。

`exponent`\
必要。 任何數值運算式。

## <a name="result"></a>結果

結果會提高 `number` 至的乘冪 `exponent` ，一律為 `Double` 值。

## <a name="supported-types"></a>支援的型別

`Double`. 任何不同類型的運算元都會轉換成 `Double` 。

## <a name="remarks"></a>備註

Visual Basic 一律會執行[Double 資料類型](../data-types/double-data-type.md)的乘冪。

的值 `exponent` 可以是小數、負數或兩者。

在單一運算式中執行多個乘冪時，會在 `^` 從左至右發現運算子時進行評估。

> [!NOTE]
> `^`運算子可以多載*overloaded*，這表示當運算元具有該類別或結構的類型時，類別或結構可以重新定義其行為。 如果您的程式碼在這類類別或結構上使用這個運算子，請務必瞭解其已重新定義的行為。 如需詳細資訊，請參閱 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。

## <a name="example"></a>範例

下列範例會使用 `^` 運算子，將數位提高至指數的乘冪。 結果是第一個運算元會引發到第二個運算元的乘冪。

[!code-vb[VbVbalrOperators#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#20)]

上述範例會產生下列結果：

`exp1`設定為4（2平方）。

`exp2`設定為19683（3個立方，而該值為立方）。

`exp3`設定為-125 （-5 的立方）。

`exp4`設定為625（-5 到第四個乘冪）。

`exp5`設定為2（8的 cube 根）。

`exp6`設定為0.5 （1.0 除以8的 cube 根）。

請注意上述範例中運算式的括弧重要性。 由於*運算子的優先順序*，Visual Basic 通常會在 `^` 任何其他專案之前執行運算子，甚至是一元 `–` 運算子。 如果 `exp4` 和都 `exp6` 是以不含括弧的方式計算，它們就會產生下列結果：

`exp4 = -5 ^ 4`會計算為–（5到第四個電源），這會產生-625。

`exp6 = 8 ^ -1.0 / 3.0`會計算為（8到-1 電源，或0.125）除以3.0，這會導致0.041666666666666666666666666666667。

## <a name="see-also"></a>另請參閱

- [^ = 運算子](exponentiation-assignment-operator.md)
- [算術運算子](arithmetic-operators.md)
- [Visual Basic 中的運算子優先順序](operator-precedence.md)
- [依功能列出運算子](operators-listed-by-functionality.md)
- [Visual Basic 的算術運算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
