---
title: SByte 資料類型
ms.date: 04/20/2017
f1_keywords:
- vb.sbyte
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- SByte data type
ms.assetid: 5c38374a-18a1-4cc2-b493-299e3dcaa60f
ms.openlocfilehash: e7d45c74056ce5b6aa66674c99e48b5ab60015f0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415566"
---
# <a name="sbyte-data-type-visual-basic"></a>SByte 資料類型（Visual Basic）

保存帶正負號的8位（1個位元組）整數，其範圍介於-128 到127之間。

## <a name="remarks"></a>備註

使用 `SByte` 資料類型來包含不需要完整資料寬度 `Integer` 或甚至是一半資料寬度的整數值 `Short` 。 在某些情況下，通用語言執行時間可能可以將您的 `SByte` 變數緊密地封裝在一起，並節省記憶體耗用量。

`SByte` 的預設值為 0。

## <a name="literal-assignments"></a>常值指派

您可以藉 `SByte` 由指派十進位常值、十六進位常值、八進位常值，或二進位常值（從 Visual Basic 2017）來宣告和初始化變數。

在下列範例中，以十進位、十六進位和二進位常值表示的整數等於-102，會指派給 `SByte` 值。 這個範例需要您使用編譯器參數編譯 `/removeintchecks` 。

[!code-vb[SByte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#SByte)]

> [!NOTE]
> 您可以使用前置詞 `&h` 或 `&H` 來表示十六進位常值、前置詞 `&b` 或表示 `&B` 二進位常值，以及前置詞 `&o` 或 `&O` 來表示八進位常值。 十進位常值沒有前置詞。

從 Visual Basic 2017 開始，您也可以使用底線字元 `_` 做為數位分隔符號來增強可讀性，如下列範例所示。

[!code-vb[SByteSeparator](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#SByteS)]

從 Visual Basic 15.5 開始，您也可以使用底線字元（ `_` ）做為前置詞和十六進位、二進位或八進位數位之間的前置分隔符號。 例如：

```vb
Dim number As SByte = &H_F9
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

如果整數常值超出 `SByte` 的範圍 (亦即，如果小於 <xref:System.SByte.MinValue?displayProperty=nameWithType> 或大於 <xref:System.SByte.MaxValue?displayProperty=nameWithType>)，就會發生編譯錯誤。 當整數常值沒有後置詞時，就會推斷[整數](integer-data-type.md)。 如果整數常值超出類型的範圍，則 `Integer` 會推斷出[Long](long-data-type.md) 。 這表示在先前的範例中，數值常 `0x9A` `0b10011010` 值和會被視為32位帶正負號的整數，其值為156，這會超過 <xref:System.SByte.MaxValue?displayProperty=nameWithType> 。 若要成功編譯這類程式碼，將非十進位整數指派給 `SByte` ，您可以執行下列其中一項動作：

- 使用編譯器參數編譯來停用整數界限檢查 `/removeintchecks` 。

- 使用[類型字元](../../programming-guide/language-features/data-types/type-characters.md)來明確定義您想要指派給的常值 `SByte` 。 下列範例會將負常 `Short` 值指派給 `SByte` 。 請注意，若為負數，必須設定數值常值之高序位單字的高序位位。 在我們的範例中，這是常值的 bit 15 `Short` 。

   [!code-vb[SByteTypeChars](../../../../samples/snippets/visualbasic/language-reference/data-types/sbyte-assignment.vb#1)]

## <a name="programming-tips"></a>程式設計提示

- **CLS 合規性。** `SByte`資料類型不是[Common Language Specification](https://www.ecma-international.org/publications/standards/Ecma-335.htm) （CLS）的一部分，因此符合 cls 標準的程式碼無法使用使用它的元件。

- **加寬.** `SByte`資料類型會擴大為 `Short` 、 `Integer` 、 `Long` 、 `Decimal` 、 `Single` 和 `Double` 。 這表示您可以轉換 `SByte` 成這些類型的任何一種，而不會遇到 <xref:System.OverflowException?displayProperty=nameWithType> 錯誤。

- **輸入字元。** `SByte`沒有常數值型別字元或識別項型別字元。

- **架構類型：** 在 .NET Framework 中對應的類型為 <xref:System.SByte?displayProperty=nameWithType> 結構。

## <a name="see-also"></a>另請參閱

- <xref:System.SByte?displayProperty=nameWithType>
- [資料類型](index.md)
- [Type Conversion Functions](../functions/type-conversion-functions.md)
- [轉換摘要](../keywords/conversion-summary.md)
- [Short 資料類型](short-data-type.md)
- [Integer 資料類型](integer-data-type.md)
- [Long 資料類型](long-data-type.md)
- [有效率地使用資料類型](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
