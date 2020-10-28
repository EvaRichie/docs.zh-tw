---
title: 作法：以前置字元零來填補數字
description: 瞭解如何填補前置零的數位。 將前置零加到特定的總長度或特定數目的前置零的整數或數值。
ms.date: 02/25/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- numeric format strings [.NET]
- formatting [.NET], numbers
- number formatting [.NET]
- numbers [.NET], format strings
ms.assetid: 0b2c2cb5-c580-4891-8d81-cb632f5ec384
ms.openlocfilehash: 7c3ee376fde34663ee0599c0b1ae654871a71206
ms.sourcegitcommit: 4a938327bad8b2e20cabd0f46a9dc50882596f13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/28/2020
ms.locfileid: "92888452"
---
# <a name="how-to-pad-a-number-with-leading-zeros"></a>作法：以前置字元零來填補數字

如果整數要加上前置零，您可以使用具有精確度規範的 "D" [標準數值格式字串](standard-numeric-format-strings.md)。 如果整數和浮點數都要加上前置零，您可以使用[自訂數值格式字串](custom-numeric-format-strings.md)。 此文示範如何使用這兩種方法，以前置零填補數值。

## <a name="to-pad-an-integer-with-leading-zeros-to-a-specific-length"></a>以前置零將整數填補至特定長度

1. 決定您要整數值顯示的位數下限。 在此數值中包含任何前置數。

1. 決定要將整數顯示為十進位值或十六進位值。

    - 若要將整數顯示為十進位值，請呼叫其 `ToString(String)` 方法，然後傳遞字串 "D *n* " 以作為 `format` 參數的值，其中 *n* 代表字串的長度下限。

    - 若要將整數顯示為十進位值，請呼叫其 `ToString(String)` 方法，然後傳遞字串 "X *n* " 以作為 format 參數的值，其中 *n* 代表字串的長度下限。

您也可以在 [C#](../../csharp/language-reference/tokens/interpolated.md) 和 [Visual Basic](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md) 的插補字串中使用格式字串，也可以呼叫使用[複合格式](composite-formatting.md)的方法 (例如 <xref:System.String.Format%2A?displayProperty=nameWithType> 或 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>)。

下列範例會使用前置零來將數個整數值格式化，讓格式化數值的總長度至少為 8 個字元。

[!code-csharp[Formatting.HowTo.PadNumber#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#1)]
[!code-vb[Formatting.HowTo.PadNumber#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#1)]

## <a name="to-pad-an-integer-with-a-specific-number-of-leading-zeros"></a>以特定數目的前置零填補整數

1. 決定您想要讓整數值顯示多少個前置零。

1. 決定要將整數顯示為十進位值或十六進位值。

    - 若要將其格式化為十進位值，您需要使用 "D" 標準格式規範。

    - 若要將其格式化為十六進位值，您需要使用 "X" 標準格式規範。

1. 呼叫整數值的 `ToString("D").Length` 或 `ToString("X").Length` 方法，以決定未填補之數值字串的長度。

1. 將您想要包含在格式化字串中的前置零個數，加入至未填補之數值字串的長度。 加入前置零個數可定義填補字串的總長度。

1. 呼叫整數值的 `ToString(String)` 方法，針對十進位字串，請傳遞字串 "D *n* "，針對十六進位字串，請傳遞 "X *n* "，其中 *n* 代表填補字串的總長度。 您也可以在支援複合格式的方法中，使用 "D *n* " 或 "X *n* " 格式字串。

下列範例會以五個前置零填補整數值。

[!code-csharp[Formatting.HowTo.PadNumber#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#2)]
[!code-vb[Formatting.HowTo.PadNumber#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#2)]

## <a name="to-pad-a-numeric-value-with-leading-zeros-to-a-specific-length"></a>以前置零將數值填補至特定長度

1. 決定您想要讓數值字串表示式的小數點左邊有幾位數。 在這個總位數中包含任何前置零。

1. 定義自訂數值格式字串，使用零預留位置 "0" 來表示零的數目下限。

1. 呼叫數值的 `ToString(String)` 方法，並將其傳遞至自訂格式字串。 您也可以使用自訂格式字串搭配字串插補或搭配支援複合格式的方法。

下列範例會使用前置零來將數個數值格式化。 因此，格式化數值的小數點左邊至少有 8 位數。

[!code-csharp[Formatting.HowTo.PadNumber#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#3)]
[!code-vb[Formatting.HowTo.PadNumber#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#3)]

## <a name="to-pad-a-numeric-value-with-a-specific-number-of-leading-zeros"></a>以特定數目的前置零填補數值

1. 決定您想要讓數值有多少個前置零。

1. 決定未填補之數值字串的小數點左邊有幾位數：

    1. 決定數值字串表示法是否包含小數點符號。

    1. 如果包含小數點符號，則要決定小數點左邊的字元數。

         -或-

         如果不包含小數點符號，則要決定字串長度。

1. 建立使用以下項目的自訂格式字串：

    - 字串中顯示的每個前置零的零預留位置 "0"。

    - 代表預設字串中每個數字的零預留位置或數字預留位置 "#"。

1. 提供自訂格式字串，以做為數值之 `ToString(String)` 方法或支援複合格式之方法的參數。

下列範例會以五個前置零填補兩個 <xref:System.Double> 值。

[!code-csharp[Formatting.HowTo.PadNumber#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.PadNumber/cs/Pad1.cs#4)]
[!code-vb[Formatting.HowTo.PadNumber#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.PadNumber/vb/Pad1.vb#4)]

## <a name="see-also"></a>請參閱

- [自訂數值格式字串](custom-numeric-format-strings.md)
- [標準數值格式字串](standard-numeric-format-strings.md) \(部分機器翻譯\)
- [複合格式](composite-formatting.md)
