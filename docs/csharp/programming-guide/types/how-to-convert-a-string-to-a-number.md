---
title: '如何將字串轉換為數字-c # 程式設計指南'
description: '瞭解如何呼叫 Parse、TryParse 或 Convert 類別方法，以 c # 將字串轉換為數字。'
ms.date: 11/20/2020
helpviewer_keywords:
- conversions [C#]
- conversions [C#], string to int
- converting strings to int [C#]
- strings [C#], converting to int
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 467b9979-86ee-4afd-b734-30299cda91e3
ms.openlocfilehash: 430887ebb16570439a89f3625ac12a1fbb368227
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513155"
---
# <a name="how-to-convert-a-string-to-a-number-c-programming-guide"></a>如何將字串轉換為數字 (c # 程式設計手冊) 

您可以藉由[](../../language-reference/builtin-types/reference-types.md)呼叫在 `Parse` 各種數數值型別上找到的或方法，將字串轉換成數位 `TryParse` (`int` 、、等等 `long` `double`) ，或使用類別中的方法 <xref:System.Convert?displayProperty=nameWithType> 。  
  
 呼叫 `TryParse` 方法 (，例如 [`int.TryParse("11", out number)`](xref:System.Int32.TryParse%2A)) 或 `Parse` 方法 (例如) ，稍微更有效率且直接 [`var number = int.Parse("11")`](xref:System.Int32.Parse%2A) 。  使用 <xref:System.Convert> 方法比實作 <xref:System.IConvertible> 的一般物件更有用。  
  
 您可以使用 `Parse` 或 `TryParse` 方法來使用您預期字串包含的數數值型別，例如 <xref:System.Int32?displayProperty=nameWithType> 類型。  <xref:System.Convert.ToInt32%2A?displayProperty=nameWithType> 方法會在內部使用 <xref:System.Int32.Parse%2A>。  `Parse`方法會傳回已轉換的數位; `TryParse` 方法會傳回 <xref:System.Boolean> 值，指出轉換是否成功，並在[ `out` 參數](../../language-reference/keywords/out.md)中傳回已轉換的數位。 如果字串不是有效的格式，則會擲回 `Parse` 例外狀況，但會傳回 `TryParse` `false` 。 呼叫 `Parse` 方法時，您必須一律使用例外狀況處理在剖析作業失敗時捕捉 <xref:System.FormatException>。  
  
## <a name="calling-the-parse-and-tryparse-methods"></a>呼叫 Parse 與 TryParse 方法

`Parse`和 `TryParse` 方法會忽略字串開頭和結尾的空格，但所有其他字元都必須是形成適當數數值型別的字元， (`int` 、、、、等 `long` `ulong` `float` `decimal`) 。  若構成數字的字串內有任何空格，則會造成錯誤。  例如，您可以使用 `decimal.TryParse` 來剖析 "10"、"10.3" 或 "10"，但無法使用這個方法從 "10 倍"、"1 0" 剖析10， (記下內嵌的空間) "10 .3" (記下內嵌的空格) 、"10e1" (在 `float.TryParse` 這裡運作) 等等。 值為 `null` 或 <xref:System.String.Empty?displayProperty=nameWithType> 無法成功剖析的字串。 您可以透過呼叫 <xref:System.String.IsNullOrEmpty%2A?displayProperty=nameWithType> 方法，在嘗試剖析 Null 或空字串之前先進行檢查。

下列範例示範對 `Parse` 與 `TryParse` 的成功呼叫與不成功的呼叫。  
  
[!code-csharp[Parse and TryParse](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse/program.cs)]  

下列範例說明一種剖析字串的方法，此方法會將開頭為數字字元的字串剖析 (包括十六進位字元) 和尾端的非數位字元。 在呼叫 <xref:System.Int32.TryParse%2A> 方法之前，它會將字串開頭的有效字元指派到新字串。 因為要剖析的字串包含一些字元，範例會呼叫 <xref:System.String.Concat%2A?displayProperty=nameWithType> 方法以將有效字元指派到新字串。 針對較大的字串，可以改為使用 <xref:System.Text.StringBuilder> 類別。
  
[!code-csharp[Removing invalid characters](~/samples/snippets/csharp/programming-guide/string-to-number/parse-tryparse2/program.cs)]  

## <a name="calling-the-convert-methods"></a>呼叫轉換方法

下表列出您可以用來將字串轉換為數字的一些方法 (來自 <xref:System.Convert> 類別)。  
  
|數字類型|方法|  
|------------------|------------|  
|`decimal`|<xref:System.Convert.ToDecimal%28System.String%29>|  
|`float`|<xref:System.Convert.ToSingle%28System.String%29>|  
|`double`|<xref:System.Convert.ToDouble%28System.String%29>|  
|`short`|<xref:System.Convert.ToInt16%28System.String%29>|  
|`int`|<xref:System.Convert.ToInt32%28System.String%29>|  
|`long`|<xref:System.Convert.ToInt64%28System.String%29>|  
|`ushort`|<xref:System.Convert.ToUInt16%28System.String%29>|  
|`uint`|<xref:System.Convert.ToUInt32%28System.String%29>|  
|`ulong`|<xref:System.Convert.ToUInt64%28System.String%29>|  
  
 下列範例會呼叫 <xref:System.Convert.ToInt32%28System.String%29?displayProperty=nameWithType> 方法，以將輸入字串轉換成 [整數](../../language-reference/builtin-types/integral-numeric-types.md)。此範例會攔截這個方法可擲回的兩個最常見的例外狀況， <xref:System.FormatException> 以及 <xref:System.OverflowException> 。 若產生的數字可在不超過 <xref:System.Int32.MaxValue?displayProperty=nameWithType> 的情況下遞增，範例會增加 1 到結果並顯示輸出。  
  
[!code-csharp[Parsing with Convert methods](~/samples/snippets/csharp/programming-guide/string-to-number/convert/program.cs)]  
  
## <a name="see-also"></a>請參閱

- [類型](./index.md)
- [如何判斷字串是否表示數值](../strings/how-to-determine-whether-a-string-represents-a-numeric-value.md)
- [Sample: .NET Core WinForms Formatting Utility (C#) (範例：.NET Core WinForms 格式化公用程式 (C#))](/samples/dotnet/samples/windowsforms-formatting-utility-cs)
