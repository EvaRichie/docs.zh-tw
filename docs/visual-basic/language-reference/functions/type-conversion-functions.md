---
title: Type Conversion Functions
ms.date: 10/24/2018
f1_keywords:
- vb.CUShort
- vb.csng
- vb.CDate
- CByte
- CSng
- vb.CDec
- CBool
- CStr
- vb.CULng
- CDec
- CVErr
- CDbl
- CShort
- vb.CObj
- vb.CVErr
- CULng
- vb.cdbl
- vb.cbool
- CObj
- CDate
- CLng
- vb.cstr
- vb.cbyte
- vb.clng
- vb.CChar
- CUShort
- vb.CUInt
- vb.cint
- vb.CShort
- CInt
- CUInt
- CChar
helpviewer_keywords:
- CDate function
- CByte function
- Integer data type [Visual Basic], converting
- string conversion [Visual Basic], conversion functions
- fractions
- data types [Visual Basic], converting
- text, converting
- CDec function
- Char data type [Visual Basic], converting
- type conversion [Visual Basic], functions for
- Single data type [Visual Basic], converting
- numbers [Visual Basic], rounding
- rounding numbers [Visual Basic], type conversion
- CUShort function
- Long data type [Visual Basic], converting
- return values [Visual Basic], data types
- single-precision numbers [Visual Basic], converting
- data type conversion [Visual Basic], functions for
- CStr function
- times [Visual Basic], converting
- CSng function
- conversions [Visual Basic], type conversion functions
- CBool function
- CDbl function
- CUInt function
- Currency data type [Visual Basic], conversion functions
- numbers [Visual Basic], converting
- Double data type [Visual Basic], converting
- CLng function
- CSByte function
- double-precision numbers
- Decimal data type [Visual Basic], converting
- Boolean data type [Visual Basic], converting
- integers [Visual Basic], type conversion functions
- dates [Visual Basic], converting
- CULng function
- CInt function
- Date data type [Visual Basic], converting
- Byte data type [Visual Basic], converting
- String data type [Visual Basic], converting
- CChar function
- banker's rounding
- Short data type [Visual Basic], converting
- rounding numbers [Visual Basic], banker's rounding
- type conversion [Visual Basic], Visual Basic vs. .NET Framework
ms.assetid: d9d8d165-f967-44ff-a6cd-598e4740a99e
ms.openlocfilehash: 5c0cfae01da02222d0827e81ec1ed35ce353ead1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415371"
---
# <a name="type-conversion-functions-visual-basic"></a>類型轉換函式 (Visual Basic)

這些函式是以內嵌方式編譯，這表示轉換程式碼是評估運算式之程式碼的一部分。 有時候不會呼叫程式來完成轉換，這可改善效能。 每個函式會將運算式強制轉型為特定的資料類型。

## <a name="syntax"></a>語法

```vb
CBool(expression)
CByte(expression)
CChar(expression)
CDate(expression)
CDbl(expression)
CDec(expression)
CInt(expression)
CLng(expression)
CObj(expression)
CSByte(expression)
CShort(expression)
CSng(expression)
CStr(expression)
CUInt(expression)
CULng(expression)
CUShort(expression)
```

## <a name="part"></a>部分

`expression`  
必要。 源資料類型的任何運算式。

## <a name="return-value-data-type"></a>傳回值資料類型

函式名稱會決定所傳回之值的資料類型，如下表所示。

|函式名稱|傳回資料類型|`expression`引數的範圍|
|-------------------|----------------------|-------------------------------------|
|`CBool`|[Boolean 資料類型](../data-types/boolean-data-type.md)|任何有效 `Char` 的或 `String` 或數值運算式。|
|`CByte`|[Byte 資料類型](../data-types/byte-data-type.md)|<xref:System.Byte.MinValue?displayProperty=nameWithType>（0）到 <xref:System.Byte.MaxValue?displayProperty=nameWithType> （255）（不帶正負號）; 小數部分會四捨五入。<sup>1</sup><br/><br/>從 Visual Basic 15.8 開始，Visual Basic 使用函式將浮點到位元組轉換的效能優化 `CByte` 。如需詳細資訊，請參閱[備註](#remarks)一節。 如需範例，請參閱[CInt 範例](#cint-example)一節。|
|`CChar`|[Char 資料類型](../data-types/char-data-type.md)|任何有效 `Char` 的或 `String` 運算式，只會轉換的第一個字元 `String` ; 值可以是0到65535（不帶正負號）。|
|`CDate`|[Date 資料類型](../data-types/date-data-type.md)|日期和時間的任何有效表示。|
|`CDbl`|[Double 資料類型](../data-types/double-data-type.md)|-1.79769313486231570 e + 308 到-4.94065645841246544 E-324 表示負值;4.94065645841246544 e-324 到 1.79769313486231570 E + 308 （適用于正值）。|
|`CDec`|[Decimal 資料類型](../data-types/decimal-data-type.md)|+/-79228162514264337593543950335 零縮放數位，也就是沒有小數的數位。 若為具有28位小數位數的數值，範圍為 +/-7.9228162514264337593543950335。 最小的可能非零數位為0.0000000000000000000000000001 （+/-1E-28）。|
|`CInt`|[Integer 資料類型](../data-types/integer-data-type.md)|<xref:System.Int32.MinValue?displayProperty=nameWithType>（-2147483648）至 <xref:System.Int32.MaxValue?displayProperty=nameWithType> （2147483647）; 小數部分會四捨五入。<sup>1</sup> <br/><br/>從 Visual Basic 15.8 開始，Visual Basic 使用函式將浮點到整數轉換的效能優化 `CInt` 。如需詳細資訊，請參閱[備註](#remarks)一節。 如需範例，請參閱[CInt 範例](#cint-example)一節。 |
|`CLng`|[Long 資料類型](../data-types/long-data-type.md)|<xref:System.Int64.MinValue?displayProperty=nameWithType>（-9223372036854775808）至 <xref:System.Int64.MaxValue?displayProperty=nameWithType> （9223372036854775807）; 小數部分會四捨五入。<sup>1</sup><br/><br/>從 Visual Basic 15.8 開始，Visual Basic 使用函式將浮點到64位整數轉換的效能優化 `CLng` 。如需詳細資訊，請參閱[備註](#remarks)一節。 如需範例，請參閱[CInt 範例](#cint-example)一節。|
|`CObj`|[Object Data Type](../data-types/object-data-type.md)|任何有效的運算式。|
|`CSByte`|[SByte 資料類型](../data-types/sbyte-data-type.md)|<xref:System.SByte.MinValue?displayProperty=nameWithType>（-128）至 <xref:System.SByte.MaxValue?displayProperty=nameWithType> （127）; 小數部分會四捨五入。<sup>1</sup><br/><br/>從 Visual Basic 15.8 開始，Visual Basic 使用函式將浮點對帶正負號位元組轉換的效能優化 `CSByte` 。如需詳細資訊，請參閱「[備註](#remarks)」一節。 如需範例，請參閱[CInt 範例](#cint-example)一節。|
|`CShort`|[Short 資料類型](../data-types/short-data-type.md)|<xref:System.Int16.MinValue?displayProperty=nameWithType>（-32768）至 <xref:System.Int16.MaxValue?displayProperty=nameWithType> （32767）; 小數部分會四捨五入。<sup>1</sup><br/><br/>從 Visual Basic 15.8 開始，Visual Basic 使用函式將浮點到16位整數轉換的效能優化 `CShort` 。如需詳細資訊，請參閱[備註](#remarks)一節。 如需範例，請參閱[CInt 範例](#cint-example)一節。|
|`CSng`|[Single 資料類型](../data-types/single-data-type.md)|-3.402823 e + 38 到-1.401298 E-45 表示負值;1.401298 e-45 到 3.402823 E + 38 （適用于正值）。|
|`CStr`|[String 資料類型](../data-types/string-data-type.md)|傳回的會 `CStr` 根據 `expression` 引數而定。 請參閱[CStr 函數](return-values-for-the-cstr-function.md)的傳回值。|
|`CUInt`|[UInteger 資料類型](../data-types/uinteger-data-type.md)|<xref:System.UInt32.MinValue?displayProperty=nameWithType>（0）到 <xref:System.UInt32.MaxValue?displayProperty=nameWithType> （4294967295）（不帶正負號）; 小數部分會四捨五入。<sup>1</sup><br/><br/>從 Visual Basic 15.8 開始，Visual Basic 使用函式將浮點與不帶正負號整數轉換的效能優化 `CUInt` 。如需詳細資訊，請參閱[備註](#remarks)一節。 如需範例，請參閱[CInt 範例](#cint-example)一節。|
|`CULng`|[ULong 資料類型](../data-types/ulong-data-type.md)|<xref:System.UInt64.MinValue?displayProperty=nameWithType>（0）到 <xref:System.UInt64.MaxValue?displayProperty=nameWithType> （18446744073709551615）（不帶正負號）; 小數部分會四捨五入。<sup>1</sup><br/><br/>從 Visual Basic 15.8 開始，Visual Basic 使用函式將浮點到不帶正負號長整數轉換的效能優化 `CULng` 。如需詳細資訊，請參閱[備註](#remarks)一節。 如需範例，請參閱[CInt 範例](#cint-example)一節。|
|`CUShort`|[UShort 資料類型](../data-types/ushort-data-type.md)|<xref:System.UInt16.MinValue?displayProperty=nameWithType>（0）到 <xref:System.UInt16.MaxValue?displayProperty=nameWithType> （65535）（不帶正負號）; 小數部分會四捨五入。<sup>1</sup><br/><br/>從 Visual Basic 15.8 開始，Visual Basic 使用函式將浮點與不帶正負號16位整數轉換的效能優化 `CUShort` 。如需詳細資訊，請參閱[備註](#remarks)一節。 如需範例，請參閱[CInt 範例](#cint-example)一節。|

<sup>1</sup>小數部分可能會受到一種特殊的舍入類型，稱為「四*進位*」。 如需詳細資訊，請參閱「備註」。

## <a name="remarks"></a>備註

做為規則，您應該在 `ToString()` <xref:System.Convert> 類別上或個別類型結構或類別上，使用 Visual Basic 類型轉換函式，並優先于 .NET Framework 方法（例如）。 Visual Basic 函式是針對與 Visual Basic 程式碼的最佳互動所設計，而且也讓您的原始程式碼更短且更容易閱讀。 此外，.NET Framework 轉換方法不一定會產生與 Visual Basic 函式相同的結果，例如，轉換 `Boolean` 為時 `Integer` 。 如需詳細資訊，請參閱針對[資料類型進行疑難排解](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)。

從 Visual Basic 15.8 開始，當您將 <xref:System.Single> <xref:System.Double> 下列方法所傳回的或值傳遞給其中一個整數轉換函式（ `CByte` 、、、、、、 `CShort` `CInt` `CLng` `CSByte` `CUShort` `CUInt` 、 `CULng` ）時，就會將浮點對整數轉換的效能優化：

- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Fix(System.Single)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Double)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Object)?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Conversion.Int(System.Single)?displayProperty=nameWithType>
- <xref:System.Math.Ceiling(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Floor(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Round(System.Double)?displayProperty=nameWithType>
- <xref:System.Math.Truncate(System.Double)?displayProperty=nameWithType>

這項優化可讓執行大量整數轉換的程式碼，執行速度最多兩次。 下列範例說明這些優化的浮點對整數轉換：

```vb
Dim s As Single = 173.7619
Dim d As Double = s

Dim i1 As Integer = CInt(Fix(s))               ' Result: 173
Dim b1 As Byte = CByte(Int(d))                 ' Result: 173
Dim s1 AS Short = CShort(Math.Truncate(s))     ' Result: 173
Dim i2 As Integer = CInt(Math.Ceiling(d))      ' Result: 174
Dim i3 As Integer = CInt(Math.Round(s))        ' Result: 174
```

## <a name="behavior"></a>行為

- **強制.** 一般來說，您可以使用資料類型轉換函數，將作業的結果強制轉型為特定的資料類型，而不是預設的資料類型。 例如，使用 `CDec` 在通常會發生單精確度、雙精確度或整數算術的情況下，強制執行十進位算數運算。

- **轉換失敗。** 如果 `expression` 傳遞至函式的超出要轉換的目標資料類型範圍， <xref:System.OverflowException> 就會發生。

- **小數部分。** 當您將非整數值轉換成整數類資料類型時，整數轉換函式（ `CByte` 、 `CInt` 、 `CLng` 、、、、 `CSByte` `CShort` `CUInt` `CULng` 和 `CUShort` ）會移除小數部分，並將值四捨五入為最接近的整數。

     如果小數部分正好為0.5，則整數轉換函式會將它舍入至最接近的偶數整數。 例如，0.5 會四捨五入為0，而1.5 和2.5 都會舍入為2。 這有時稱為「四*進位*」（），其目的是要彌補同時新增許多這類數位時可能累積的偏差。

     `CInt`和會與和函式 `CLng` 不同，這些函式會 <xref:Microsoft.VisualBasic.Conversion.Int%2A> <xref:Microsoft.VisualBasic.Conversion.Fix%2A> 截斷，而不是舍入數位的小數部分。 此外， `Fix` 和 `Int` 一律會傳回與您傳入時相同資料類型的值。

- **日期/時間轉換。** 使用 <xref:Microsoft.VisualBasic.Information.IsDate%2A> 函數來判斷值是否可以轉換成日期和時間。 `CDate`可識別日期常值和時間常值，但不能辨識數值。 若要將 Visual Basic 6.0 `Date` 值轉換為 `Date` Visual Basic 2005 或更新版本中的值，您可以使用 <xref:System.DateTime.FromOADate%2A?displayProperty=nameWithType> 方法。

- **中性日期/時間值。** [Date 資料類型](../data-types/date-data-type.md)一律會同時包含日期和時間資訊。 基於類型轉換的目的，Visual Basic 會將1/1/0001 （第1年1月1日）視為日期的*中性值*，而00:00:00 （午夜）則是時間的中性值。 如果您將 `Date` 值轉換成字串，則不 `CStr` 會在結果字串中包含中性值。 例如，如果您將轉換 `#January 1, 0001 9:30:00#` 成字串，則結果會是 "9:30:00 AM"; 日期資訊會隱藏起來。 不過，日期資訊仍然會出現在原始值中， `Date` 而且可以使用函數（例如函式）來復原 <xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A> 。

- **區分文化特性。** 涉及字串的類型轉換函式會根據應用程式目前的文化特性設定來執行轉換。 例如，會 `CDate` 根據您系統的地區設定來辨識日期格式。 您必須以正確的地區設定順序來提供日期、月和年，否則可能無法正確地解讀日期。 如果包含一周中的字串，例如「星期三」，就無法辨識完整的日期格式。

     如果您需要以不是由地區設定所指定的格式，從值的字串表示轉換為或，則不能使用 Visual Basic 類型轉換函式。 若要這麼做，請 `ToString(IFormatProvider)` 使用 `Parse(String, IFormatProvider)` 該數值型別的和方法。 例如，將 <xref:System.Double.Parse%2A?displayProperty=nameWithType> 字串轉換為時，請使用 `Double` ，並 <xref:System.Double.ToString%2A?displayProperty=nameWithType> 在將類型的值轉換 `Double` 成字串時使用。

## <a name="ctype-function"></a>CType Function

[CType](ctype-function.md)函式會採用第二個引數，並將強制轉型 `typename` `expression` 為 `typename` ，其中 `typename` 可以是任何資料類型、結構、類別或介面，其中存在有效的轉換。

如需 `CType` 與其他類型轉換關鍵字的比較，請參閱[DirectCast 運算子](../operators/directcast-operator.md)和[TryCast 運算子](../operators/trycast-operator.md)。

## <a name="cbool-example"></a>CBool 範例

下列範例會使用函式將 `CBool` 運算式轉換為 `Boolean` 值。 如果運算式評估為非零值，則 `CBool` 會傳回， `True` 否則會傳回 `False` 。

[!code-vb[VbVbalrFunctions#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#1)]

## <a name="cbyte-example"></a>CByte 範例

下列範例會使用 `CByte` 函數，將運算式轉換為 `Byte` 。

[!code-vb[VbVbalrFunctions#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#2)]

## <a name="cchar-example"></a>CChar 範例

下列範例會使用 `CChar` 函數，將運算式的第一個字元轉換成 `String` `Char` 類型。

[!code-vb[VbVbalrFunctions#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#3)]

的輸入引數 `CChar` 必須是資料類型 `Char` 或 `String` 。 您不能使用將 `CChar` 數位轉換成字元，因為 `CChar` 無法接受數值資料類型。 下列範例會取得代表程式碼點（字元碼）的數位，並將它轉換成對應的字元。 它會使用 <xref:Microsoft.VisualBasic.Interaction.InputBox%2A> 函數來取得數位的字串、 `CInt` 將字串轉換成類型 `Integer` ，以及 `ChrW` 將數位轉換成類型 `Char` 。

[!code-vb[VbVbalrFunctions#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#4)]

## <a name="cdate-example"></a>CDate 範例

下列範例會使用函式 `CDate` ，將字串轉換成 `Date` 值。 一般而言，不建議將日期和時間硬式編碼為字串（如本範例所示）。 請改用日期常值和時間常值，例如 #Feb 12、1969 # 和 #4： 45:23 PM #。

[!code-vb[VbVbalrFunctions#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#5)]

## <a name="cdbl-example"></a>CDbl 範例

[!code-vb[VbVbalrFunctions#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#6)]

## <a name="cdec-example"></a>CDec 範例

下列範例會使用 `CDec` 函數，將數值轉換成 `Decimal` 。

[!code-vb[VbVbalrFunctions#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#7)]

## <a name="cint-example"></a>CInt 範例

下列範例會使用 `CInt` 函數將值轉換為 `Integer` 。

[!code-vb[VbVbalrFunctions#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#8)]

## <a name="clng-example"></a>CLng 範例

下列範例會使用 `CLng` 函數將值轉換為 `Long` 。

[!code-vb[VbVbalrFunctions#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#9)]

## <a name="cobj-example"></a>CObj 範例

下列範例會使用 `CObj` 函數，將數值轉換成 `Object` 。 `Object`變數本身只包含四個位元組的指標，指向指派給它的 `Double` 值。

[!code-vb[VbVbalrFunctions#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#10)]

## <a name="csbyte-example"></a>CSByte 範例

下列範例會使用 `CSByte` 函數，將數值轉換成 `SByte` 。

[!code-vb[VbVbalrFunctions#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#11)]

## <a name="cshort-example"></a>CShort 範例

下列範例會使用 `CShort` 函數，將數值轉換成 `Short` 。

[!code-vb[VbVbalrFunctions#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#12)]

## <a name="csng-example"></a>CSng 範例

下列範例會使用 `CSng` 函數將值轉換為 `Single` 。

[!code-vb[VbVbalrFunctions#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#13)]

## <a name="cstr-example"></a>CStr 範例

下列範例會使用 `CStr` 函數，將數值轉換成 `String` 。

[!code-vb[VbVbalrFunctions#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#14)]

下列範例會使用 `CStr` 函數將值轉換成 `Date` `String` 值。

[!code-vb[VbVbalrFunctions#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#15)]

`CStr`一律以 `Date` 標準簡短格式呈現目前地區設定的值，例如 "6/15/2003 4:35:47 PM"。 不過，會 `CStr` 抑制日期和00:00:00 在該時間的*中性值*1/1/0001。

如需所傳回之值的詳細資訊 `CStr` ，請參閱[CStr 函數的 Return 值](return-values-for-the-cstr-function.md)。

## <a name="cuint-example"></a>CUInt 範例

下列範例會使用 `CUInt` 函數，將數值轉換成 `UInteger` 。

[!code-vb[VbVbalrFunctions#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#16)]

## <a name="culng-example"></a>CULng 範例

下列範例會使用 `CULng` 函數，將數值轉換成 `ULong` 。

[!code-vb[VbVbalrFunctions#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#17)]

## <a name="cushort-example"></a>CUShort 範例

下列範例會使用 `CUShort` 函數，將數值轉換成 `UShort` 。

[!code-vb[VbVbalrFunctions#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#18)]

## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Strings.Asc%2A>
- <xref:Microsoft.VisualBasic.Strings.AscW%2A>
- <xref:Microsoft.VisualBasic.Strings.Chr%2A>
- <xref:Microsoft.VisualBasic.Strings.ChrW%2A>
- <xref:Microsoft.VisualBasic.Conversion.Int%2A>
- <xref:Microsoft.VisualBasic.Conversion.Fix%2A>
- <xref:Microsoft.VisualBasic.Strings.Format%2A>
- <xref:Microsoft.VisualBasic.Conversion.Hex%2A>
- <xref:Microsoft.VisualBasic.Conversion.Oct%2A>
- <xref:Microsoft.VisualBasic.Conversion.Str%2A>
- <xref:Microsoft.VisualBasic.Conversion.Val%2A>
- [轉換函式](conversion-functions.md)
- [Visual Basic 中的類型轉換](../../programming-guide/language-features/data-types/type-conversions.md)
