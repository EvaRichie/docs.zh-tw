---
title: Long 資料類型
ms.date: 01/31/2018
f1_keywords:
- vb.Long
helpviewer_keywords:
- identifier type characters [Visual Basic], &
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- '& identifier type character'
- integer numbers
- literal type characters [Visual Basic], L
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- L literal type character [Visual Basic]
- integers [Visual Basic], types
- Long keyword [Visual Basic]
- data types [Visual Basic], integral
- data types [Visual Basic], assigning
- Long data type
ms.assetid: b4770c34-1804-4f8c-b512-c10b0893e516
ms.openlocfilehash: 7c076cd2198c85560f7c63c69e051697966c9524
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415592"
---
# <a name="long-data-type-visual-basic"></a>LONG 資料型別（Visual Basic）

保存帶正負號的64位（8位元組）整數，範圍從-9223372036854775808 到9223372036854775807（9.2 ... E + 18）的值。

## <a name="remarks"></a>備註

使用 `Long` 資料類型來包含太大而無法納入 `Integer` 資料類型的整數。

`Long` 的預設值為 0。

## <a name="literal-assignments"></a>常值指派

您可以藉 `Long` 由指派十進位常值、十六進位常值、八進位常值，或二進位常值（從 Visual Basic 2017）來宣告和初始化變數。 如果整數常值超出 `Long` 的範圍 (亦即，如果小於 <xref:System.Int64.MinValue?displayProperty=nameWithType> 或大於 <xref:System.Int64.MaxValue?displayProperty=nameWithType>)，就會發生編譯錯誤。

在下列範例中，如果整數等於 4,294,967,296，即表示 `Long` 值指派了十進位、十六進位和二進位常值。

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Long)]

> [!NOTE]
> 您可以使用前置詞 `&h` 或 `&H` 來表示十六進位常值、前置詞 `&b` 或表示 `&B` 二進位常值，以及前置詞 `&o` 或 `&O` 來表示八進位常值。 十進位常值沒有前置詞。

從 Visual Basic 2017 開始，您也可以使用底線字元 `_` 做為數位分隔符號來增強可讀性，如下列範例所示。

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

從 Visual Basic 15.5 開始，您也可以使用底線字元（ `_` ）做為前置詞和十六進位、二進位或八進位數位之間的前置分隔符號。 例如：

```vb
Dim number As Long = &H_0FAC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

數值常值也可以包含 `L` [型別字符](../../programming-guide/language-features/data-types/type-characters.md)來表示 `Long` 資料型別，如下列範例所示。

```vb
Dim number = &H_0FAC_0326_1489_D68CL
```

## <a name="programming-tips"></a>程式設計提示

- **Interop 考量：** 如果您要使用的元件不是針對 .NET Framework 所撰寫（例如 Automation 或 COM 物件），請記住， `Long` 在其他環境中會有不同的資料寬度（32位）。 如果您要將32位引數傳遞至這類元件，請 `Integer` `Long` 在新的 Visual Basic 程式碼中將它宣告為而不是。

- **加寬.** `Long`資料類型會擴大為 `Decimal` 、 `Single` 或 `Double` 。 這表示，您可以將 `Long` 轉換成這些類型的任何一種，而不會發生 <xref:System.OverflowException?displayProperty=nameWithType> 錯誤。

- **輸入字元。** 將常值類型字元 `L` 附加到常值，會強制其成為 `Long` 資料類型。 將識別項類型字元 `&` 附加到任何識別項，會強制其成為 `Long`。

- **架構類型：** 在 .NET Framework 中對應的類型為 <xref:System.Int64?displayProperty=nameWithType> 結構。

## <a name="see-also"></a>另請參閱

- <xref:System.Int64>
- [資料類型](index.md)
- [Integer 資料類型](integer-data-type.md)
- [Short 資料類型](short-data-type.md)
- [Type Conversion Functions](../functions/type-conversion-functions.md)
- [轉換摘要](../keywords/conversion-summary.md)
- [有效率地使用資料類型](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
