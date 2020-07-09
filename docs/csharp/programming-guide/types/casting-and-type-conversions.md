---
title: 轉型和類型轉換 - C# 程式設計指南
ms.date: 07/06/2020
helpviewer_keywords:
- type conversion [C#]
- data type conversion [C#]
- numeric conversions [C#]
- conversions [C#], type
- casting [C#]
- converting types [C#]
ms.assetid: 568df58a-d292-4b55-93ba-601578722878
ms.openlocfilehash: 9860b4ca44504bbe7c0bafd0c744f0b9d9ca389c
ms.sourcegitcommit: 4ad2f8920251f3744240c3b42a443ffbe0a46577
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86100791"
---
# <a name="casting-and-type-conversions-c-programming-guide"></a>轉型和類型轉換 (C# 程式設計指南)

因為 C# 在編譯時期是靜態型別，所以宣告變數之後，除非該型別隱含轉換為變數的型別，否則無法再次宣告或指派另一個型別的值。 例如，`string` 無法隱含轉換為 `int`。 因此，在您宣告 `i` 為 `int` 之後，您便無法將字串 "Hello" 指派給它，如以下程式碼所示：

```csharp
int i;

// error CS0029: Cannot implicitly convert type 'string' to 'int'
i = "Hello";
```

不過，您有時可能需要將值複製至另一種類型的變數或方法參數。 例如，您的整數變數可能需要傳遞給參數類型為 `double` 的方法。 或者，您可能需要將類別變數指派給介面類型的變數。 這些類型的作業稱為「類型轉換」**。 在 C# 中，您可以執行下列類型的轉換：

- **隱含轉換**：不需要特殊語法，因為轉換一律會成功，而且不會遺失任何資料。 範例包括從較小到較大整數型別的轉換，以及從衍生類別到基底類別的轉換。

- **明確轉換（轉換）**：明確轉換需要[cast 運算式](../../language-reference/operators/type-testing-and-cast.md#cast-expression)。 如果資訊可能會在轉換時遺失，或轉換因其他原因而失敗，則需要轉換。 一般範例包括將數字轉換為較少有效位數或較小範圍的類型，以及將基底類別執行個體轉換為衍生類別。

- **使用者定義的轉換**：使用者定義的轉換是透過特殊方法所執行，而您可以定義特殊方法來啟用沒有基底類別/衍生類別關聯性之自訂類型間的明確和隱含轉換。 如需詳細資訊，請參閱[使用者定義轉換運算子](../../language-reference/operators/user-defined-conversion-operators.md)。

- **使用協助程式類別轉換**：若要轉換不相容類型 (例如，整數和 <xref:System.DateTime?displayProperty=nameWithType> 物件，或十六進位字串和位元組陣列)，您可以使用 <xref:System.BitConverter?displayProperty=nameWithType> 類別、<xref:System.Convert?displayProperty=nameWithType> 類別，以及內建數字類型的 `Parse` 方法 (例如，<xref:System.Int32.Parse%2A?displayProperty=nameWithType>)。 如需詳細資訊，請參閱[如何將位元組陣列轉換成](./how-to-convert-a-byte-array-to-an-int.md)整數、[如何將字串轉換成數位](./how-to-convert-a-string-to-a-number.md)，以及[如何在十六進位字串和數位類型之間進行轉換](./how-to-convert-between-hexadecimal-strings-and-numeric-types.md)。

## <a name="implicit-conversions"></a>隱含的轉換

針對內建數字類型，如果要儲存的值可以放入變數中，而不需進行截斷或四捨五入，則可以進行隱含轉換。 針對整數型別，這表示來源型別的範圍是目標型別範圍的適當子集。 例如，型別為 [long](../../language-reference/builtin-types/integral-numeric-types.md) 的變數 (64 位元整數) 可儲存任何 [int](../../language-reference/builtin-types/integral-numeric-types.md) (32 位元整數) 能儲存的值。 在下列範例中，編譯器會將位於右側的 `num` 值隱含轉換為 `long` 型別，再將它指派給 `bigNum`。

[!code-csharp[csProgGuideTypes#34](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#34)]

如需所有隱含數值轉換的完整清單，請參閱[內建數值轉換](../../language-reference/builtin-types/numeric-conversions.md)一文的[隱含數值轉換](../../language-reference/builtin-types/numeric-conversions.md#implicit-numeric-conversions)一節。

針對參考型別，一律會執行從某個類別到其任何一個直接或間接基底類別或介面的隱含轉換。 因為衍生類別一律會包含基底類別的所有成員，所以不需要特殊語法。

```csharp
Derived d = new Derived();

// Always OK.
Base b = d;
```

## <a name="explicit-conversions"></a>明確轉換

不過，如果進行轉換，而有遺失資訊的風險，則編譯器需要您執行稱為「轉換」** 的明確轉換。 轉換是一種方法，可明確通知編譯器您想要進行轉換，而且您知道可能會遺失資料，或轉換可能會在執行時間失敗。 若要執行轉換，請在要轉換的值或變數前面的括弧中指定要轉換為的類型。 下列程式會將[double](../../language-reference/builtin-types/floating-point-numeric-types.md)轉換成[int](../../language-reference/builtin-types/integral-numeric-types.md)。程式不會進行編譯，而不會進行轉換。

[!code-csharp[csProgGuideTypes#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#2)]

如需支援的明確數值轉換的完整清單，請參閱[內建數值轉換](../../language-reference/builtin-types/numeric-conversions.md)一文的[明確數值轉換](../../language-reference/builtin-types/numeric-conversions.md#explicit-numeric-conversions)一節。

針對參考型別，如果您需要將基底類型轉換為衍生類型，則需要明確轉換︰

```csharp
// Create a new derived type.
Giraffe g = new Giraffe();

// Implicit conversion to base type is safe.
Animal a = g;

// Explicit conversion is required to cast back
// to derived type. Note: This will compile but will
// throw an exception at run time if the right-side
// object is not in fact a Giraffe.
Giraffe g2 = (Giraffe)a;
```

參考型別之間的轉型作業不會變更基礎物件的執行階段類型；它只會變更將用作該物件之參考值的類型。 如需詳細資訊，請參閱[多型](../classes-and-structs/polymorphism.md)。

## <a name="type-conversion-exceptions-at-run-time"></a>執行階段的類型轉換例外狀況

在某些參考型別轉換中，編譯器無法判斷轉換是否有效。 正確編譯的轉型作業可能會在執行階段失敗。 如下列範例所示，在執行階段失敗的型別轉型將導致擲回 <xref:System.InvalidCastException>。

[!code-csharp[csProgGuideTypes#41](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsProgGuideTypes/CS/Class1.cs#41)]

`Test`方法具有 `Animal` 參數，因此將引數明確轉換 `a` 為會造成 `Reptile` 危險的假設。 不進行假設，而是檢查類型是比較安全的作法。 C# 提供 [is](../../language-reference/operators/type-testing-and-cast.md#is-operator) 運算子，可讓您先測試相容性，再實際執行轉換。 如需詳細資訊，請參閱[如何使用模式比對來安全地轉換和 as 和 is 運算子](../../how-to/safely-cast-using-pattern-matching-is-and-as-operators.md)。

## <a name="c-language-specification"></a>C# 語言規格

如需詳細資訊，請參閱 [C# 語言規格](~/_csharplang/spec/introduction.md)的[轉換](~/_csharplang/spec/conversions.md)一節。

## <a name="see-also"></a>另請參閱

- [C # 程式設計指南](../index.md)
- [類型](./index.md)
- [轉換運算式](../../language-reference/operators/type-testing-and-cast.md#cast-expression)
- [使用者定義轉換運算子](../../language-reference/operators/user-defined-conversion-operators.md)
- [產生的類型轉換](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/yy580hbd(v=vs.120))
- [如何將字串轉換為數值](./how-to-convert-a-string-to-a-number.md)
