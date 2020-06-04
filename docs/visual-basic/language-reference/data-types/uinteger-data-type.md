---
title: UInteger 資料類型
ms.date: 01/31/2018
f1_keywords:
- vb.uinteger
helpviewer_keywords:
- numbers [Visual Basic], whole
- UInteger data type
- literal type characters [Visual Basic], UI
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- UI literal type characters [Visual Basic]
- data types [Visual Basic], integral
ms.assetid: db7ddd34-4f23-46f5-84dd-8b0f83bb8729
ms.openlocfilehash: 11070f6c7f3259b8c34528eb54d99b031b68f9f9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415540"
---
# <a name="uinteger-data-type"></a>UInteger 資料類型

保留不帶正負號的32位（4位元組）整數，範圍是從0到4294967295的值。

## <a name="remarks"></a>備註

`UInteger`資料類型會以最有效率的資料寬度提供最大的不帶正負號值。

`UInteger` 的預設值為 0。

## <a name="literal-assignments"></a>常值指派

您可以藉 `UInteger` 由指派十進位常值、十六進位常值、八進位常值，或二進位常值（從 Visual Basic 2017）來宣告和初始化變數。 如果整數常值超出 `UInteger` 的範圍 (亦即，如果小於 <xref:System.UInt32.MinValue?displayProperty=nameWithType> 或大於 <xref:System.UInt32.MaxValue?displayProperty=nameWithType>)，就會發生編譯錯誤。

在下列範例中，以十進位、十六進位和二進位常值表示的 3,000,000,000 整數，會指派給 `UInteger` 值。

[!code-vb[UInteger](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UInt)]

> [!NOTE]
> 您可以使用前置詞 `&h` 或 `&H` 來表示十六進位常值、前置詞 `&b` 或表示 `&B` 二進位常值，以及前置詞 `&o` 或 `&O` 來表示八進位常值。 十進位常值沒有前置詞。

從 Visual Basic 2017 開始，您也可以使用底線字元 `_` 做為數位分隔符號來增強可讀性，如下列範例所示。

[!code-vb[UInteger](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UIntS)]

從 Visual Basic 15.5 開始，您也可以使用底線字元（ `_` ）做為前置詞和十六進位、二進位或八進位數位之間的前置分隔符號。 例如：

```vb
Dim number As UInteger = &H_0F8C_0326
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

數值常值也可以包含 `UI` 或 `ui` [類型字元](../../programming-guide/language-features/data-types/type-characters.md)來表示 `UInteger` 資料類型，如下列範例所示。

```vb
Dim number = &H_0FAC_14D7ui
```

## <a name="programming-tips"></a>程式設計提示

`UInteger`和 `Integer` 資料類型會在32位處理器上提供最佳效能，因為較小的整數類型（ `UShort` 、 `Short` 、 `Byte` 和 `SByte` ），即使使用較少的位，也需要更多時間來載入、儲存和提取。

- **負數。** 因為 `UInteger` 是不帶正負號的類型，所以不能代表負數。 如果您 `-` 在評估為類型的運算式上使用一元減號（）運算子 `UInteger` ，Visual Basic 會將運算式轉換為 `Long` first。

- **CLS 合規性。** `UInteger`資料類型不是[Common Language Specification](https://www.ecma-international.org/publications/standards/Ecma-335.htm) （CLS）的一部分，因此符合 cls 標準的程式碼無法使用使用它的元件。

- **Interop 考量：** 如果您要使用的元件不是針對 .NET Framework 所撰寫（例如 Automation 或 COM 物件），請記住，之類的類型 `uint` 在其他環境中可能會有不同的資料寬度（16位）。 如果您要將16位引數傳遞至這類元件，請 `UShort` `UInteger` 在您的 managed Visual Basic 程式碼中將它宣告為而不是。

- **加寬.** `UInteger`資料類型會擴大為 `Long` 、 `ULong` 、 `Decimal` 、 `Single` 和 `Double` 。 這表示您可以轉換 `UInteger` 成這些類型的任何一種，而不會遇到 <xref:System.OverflowException?displayProperty=nameWithType> 錯誤。

- **輸入字元。** 將常數值型別字元附加 `UI` 到常值，會強制其成為 `UInteger` 資料類型。 `UInteger`沒有識別項型別字元。

- **架構類型：** 在 .NET Framework 中對應的類型為 <xref:System.UInt32?displayProperty=nameWithType> 結構。

## <a name="see-also"></a>另請參閱

- <xref:System.UInt32>
- [資料類型](index.md)
- [Type Conversion Functions](../functions/type-conversion-functions.md)
- [轉換摘要](../keywords/conversion-summary.md)
- [作法：呼叫不帶正負號的類型的 Windows 函式](../../programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [有效率地使用資料類型](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
