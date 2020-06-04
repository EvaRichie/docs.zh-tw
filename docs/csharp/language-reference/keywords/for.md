---
title: 'for 語句-c # 參考'
ms.date: 06/13/2018
f1_keywords:
- for
- for_CSharpKeyword
helpviewer_keywords:
- for keyword [C#]
ms.assetid: 34041a40-2c87-467a-9ffb-a0417d8f67a8
ms.openlocfilehash: db7cecc697a9cc9e5ff6b94b78747b799ed7e505
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401897"
---
# <a name="for-c-reference"></a>for (C# 參考)

當指定的布林運算式評估為 `true` 時，`for` 陳述式會執行某個陳述式或陳述式區塊。

您可以在 `for` 陳述式區塊內的任何位置，使用 [break](break.md) 陳述式跳出迴圈，或使用 [continue](continue.md) 陳述式逐步執行到迴圈中的下一個反覆運算。 您也可以使用 `for` [goto](goto.md)、 [return](return.md)或[throw](throw.md)語句來結束迴圈。

## <a name="structure-of-the-for-statement"></a>`for` 陳述式的結構

`for` 陳述式會定義「初始設定式」**、「條件」** 和「迭代器」** 區段：

```csharp
for (initializer; condition; iterator)
    body
```

三個區段都是選擇性的。 迴圈的主體是陳述式或陳述式區塊。

下列範例顯示 `for` 陳述式，並已定義所有區段：

[!code-csharp-interactive[for loop example](snippets/IterationKeywordsExamples.cs#5)]

### <a name="the-initializer-section"></a>「初始設定式」** 區段

「初始設定式」** 區段中的陳述式只執行一次，在進入迴圈之前。 「初始設定式」** 區段是下列其中一項：

- 本機迴圈變數的宣告和初始化，這無法從迴圈外存取。

- 下列清單中的零個以上陳述式運算式，並以逗號分隔：

  - [指派](../operators/assignment-operator.md)陳述式

  - 方法的引動過程

  - 前置或後置[遞增](../operators/arithmetic-operators.md#increment-operator-)運算式，例如 `++i` 或 `i++`

  - 前置或後置[遞減](../operators/arithmetic-operators.md#decrement-operator---)運算式，例如 `--i` 或 `i--`

  - 使用 [new](../operators/new-operator.md) 運算子建立物件

  - [await](../operators/await.md) 運算式

上述範例中的「初始設定式」** 區段會宣告及初始化本機迴圈變數 `i`：

```csharp
int i = 0
```

### <a name="the-condition-section"></a>「條件」** 區段

「條件」** 區段如果存在的話，必須是布林運算式。 該運算式會在每次迴圈反覆運算之前評估。 如果「條件」** 區段不存在，或是布林運算式會評估為 `true`，就會執行下次迴圈反覆運算；否則迴圈會結束。

上述範例中的「條件」** 區段，會根據本機迴圈變數的值決定是否迴圈終止：

```csharp
i < 5
```

### <a name="the-iterator-section"></a>「迭代器」** 區段

「迭代器」** 區段會定義迴圈主體每次反覆運算之後的狀況。 「迭代器」** 區段包含下列零個以上陳述式運算式，並以逗號分隔：

- [指派](../operators/assignment-operator.md)陳述式

- 方法的引動過程

- 前置或後置[遞增](../operators/arithmetic-operators.md#increment-operator-)運算式，例如 `++i` 或 `i++`

- 前置或後置[遞減](../operators/arithmetic-operators.md#decrement-operator---)運算式，例如 `--i` 或 `i--`

- 使用 [new](../operators/new-operator.md) 運算子建立物件

- [await](../operators/await.md) 運算式

上述範例中的「迭代器」** 區段會遞增本機迴圈變數：

```csharp
i++
```

## <a name="examples"></a>範例

下列範例描述幾個較少見的 `for` 陳述式用法︰將值指派給「初始設定式」** 區段中的外部迴圈變數、在「初始設定式」** 和「迭代器」** 區段中叫用方法，以及在「迭代器」** 區段中變更兩個變數的值。 選取 [執行]**** 執行範例程式碼。 之後，您可以修改程式碼，然後再次執行它。

[!code-csharp-interactive[not typical for loop example](snippets/IterationKeywordsExamples.cs#6)]

下列範例會定義無限迴圈 `for`：

[!code-csharp[infinite for loop example](snippets/IterationKeywordsExamples.cs#7)]

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](/dotnet/csharp/language-reference/language-specification/introduction)的 [for 陳述式](~/_csharplang/spec/statements.md#the-for-statement)一節。

## <a name="see-also"></a>另請參閱

- [C # 參考](../index.md)
- [C # 程式設計指南](../../programming-guide/index.md)
- [C # 關鍵字](index.md)
- [foreach、in](foreach-in.md)
