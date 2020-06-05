---
title: 疑難排解資料類型的問題
ms.date: 07/20/2015
helpviewer_keywords:
- Char data type [Visual Basic], converting
- Decimal data type [Visual Basic], conversions
- data types [Visual Basic], troubleshooting
- literals [Visual Basic], default types
- type characters [Visual Basic], literal
- Mod operator [Visual Basic], in floating-point operations
- troubleshooting Visual Basic, data types
- troubleshooting data types [Visual Basic]
- floating-point numbers [Visual Basic], precision
- Boolean data type [Visual Basic], converting
- literal types [Visual Basic]
- literal type characters [Visual Basic]
- floating-point numbers [Visual Basic], imprecision
- String data type [Visual Basic], converting
- floating-point numbers [Visual Basic], comparison
- floating-point numbers
ms.assetid: 90040d67-b630-4125-a6ae-37195b079042
ms.openlocfilehash: 239e1c2f908a9023aeca6e92aff4633b60f27b69
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393399"
---
# <a name="troubleshooting-data-types-visual-basic"></a>疑難排解資料類型 (Visual Basic)

此頁面會列出當您對內部資料類型執行作業時，可能會發生的一些常見問題。

## <a name="floating-point-expressions-do-not-compare-as-equal"></a>浮點運算式不會比較為相等

當您使用浮點數（[單一資料類型](../../../language-reference/data-types/single-data-type.md)和[Double 資料類型](../../../language-reference/data-types/double-data-type.md)）時，請記住這些數位會儲存為二進位分數。 這表示它們無法針對不是二進位分數的任何數量（其格式為 k/（2 ^ n），其中 k 和 n 是整數），不能有精確的標記法。 例如，0.5 （= 1/2）和0.3125 （= 5/16）可以保留為精確值，而 [0.2 （= 1/5）] 和 [0.3] （= [3/10]）只能是近似值。

由於此不精確，當您操作浮點值時，您無法依賴確切的結果。 特別是，理論上相等的兩個值可能會有稍微不同的標記法。

| 比較浮點數量 |
|---|
|1. 使用 <xref:System.Math.Abs%2A> <xref:System.Math> 命名空間中類別的方法，計算其差異的絕對值 <xref:System> 。<br />2. 判斷可接受的最大差異，如此一來，如果兩個數量的差異不大，您就可以將其視為實際用途。<br />3. 將差異的絕對值與可接受的差異做比較。|

下列範例示範兩個值的不正確和正確比較 `Double` 。

[!code-vb[VbVbalrDataTypes#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#10)]

上一個範例會使用 <xref:System.Double.ToString%2A> 結構的方法， <xref:System.Double> 讓它可以指定比關鍵字使用更好的有效位數 `CStr` 。 預設值為15位數，但 "G17" 格式會將它延伸至17個數字。

## <a name="mod-operator-does-not-return-accurate-result"></a>Mod 運算子不會傳回精確的結果

由於浮點儲存區的不精確，當至少有一個運算元為浮點時， [Mod 運算子](../../../language-reference/operators/mod-operator.md)可能會傳回非預期的結果。

[Decimal 資料類型](../../../language-reference/data-types/decimal-data-type.md)不會使用浮點標記法。 許多在和中不精確的數位（例如， `Single` `Double` `Decimal` 0.2 和0.3）。 雖然算術的速度低於 `Decimal` 浮點，但可能值得降低效能，以達到更佳的精確度。

|若要找出浮點數量的整數餘數|
|---|
|1. 將變數宣告為 `Decimal` 。<br />2. 使用常數值型別字元 `D` 來強制常 `Decimal` 值，以在其值對資料類型而言太大的情況下 `Long` 。|

下列範例示範浮點運算元的潛在不精確。

[!code-vb[VbVbalrDataTypes#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#11)]

上一個範例會使用 <xref:System.Double.ToString%2A> 結構的方法， <xref:System.Double> 讓它可以指定比關鍵字使用更好的有效位數 `CStr` 。 預設值為15位數，但 "G17" 格式會將它延伸至17個數字。

因為 `zeroPointTwo` 是 `Double` ，所以0.2 的值是具有儲存值0.20000000000000001 的無限重複二進位分數。 將2.0 除以此數量會產生9.9999999999999995，餘數為0.19999999999999991。

在的運算式中 `decimalRemainder` ，常數值型別字元會 `D` 強制執行這兩個運算元 `Decimal` ，而0.2 具有精確的標記法。 因此， `Mod` 運算子會產生預期的餘數0.0。

請注意，宣告為是不夠的 `decimalRemainder` `Decimal` 。 您也必須強制將常值設為 `Decimal` ，或預設為使用， `Double` 並接收與不 `decimalRemainder` 正確的值 `doubleRemainder` 。

## <a name="boolean-type-does-not-convert-to-numeric-type-accurately"></a>布林值類型未正確轉換為數數值型別

[布林資料類型](../../../language-reference/data-types/boolean-data-type.md)值不會儲存為數字，而且儲存的值不會等同于數位。 為了與舊版相容，Visual Basic 提供轉換關鍵字（[CType 函數](../../../language-reference/functions/ctype-function.md)、 `CBool` 、等等 `CInt` ）來轉換 `Boolean` 和數數值型別。 不過，其他語言有時候會以不同的方式執行這些轉換，如同 .NET Framework 方法一樣。

您絕對不應該撰寫依賴和的對等數值的程式碼 `True` `False` 。 可能的話，您應該將變數的使用限制 `Boolean` 為其設計的邏輯值。 如果您必須混合 `Boolean` 和數值，請確定您瞭解所選取的轉換方法。

### <a name="conversion-in-visual-basic"></a>Visual Basic 中的轉換

當您使用 `CType` 或 `CBool` 轉換關鍵字將數值資料類型轉換為時 `Boolean` ，0會變成， `False` 而所有其他值會變成 `True` 。 當您 `Boolean` 使用轉換關鍵字將值轉換成數數值型別時， `False` 會變成0，並 `True` 變成-1。

### <a name="conversion-in-the-framework"></a>架構中的轉換

<xref:System.Convert.ToInt32%2A> <xref:System.Convert> 命名空間中類別的方法會 <xref:System> 將轉換 `True` 為 + 1。

如果您必須將 `Boolean` 值轉換成數值資料類型，請留意您使用的轉換方法。

## <a name="character-literal-generates-compiler-error"></a>字元常值會產生編譯器錯誤

如果沒有任何類型字元，Visual Basic 會假設常值的預設資料類型。 字元常值的預設類型（以引號（）括住 `" "` ）為 `String` 。

`String`資料類型不會擴展到[Char 資料型別](../../../language-reference/data-types/char-data-type.md)。 這表示如果您想要將常值指派給 `Char` 變數，則必須進行縮小轉換，或強制將常值設為 `Char` 類型。

|若要建立要指派給變數或常數的 Char 常值|
|---|
|1. 將變數或常數宣告為 `Char` 。<br />2. 將字元值括在引號中（ `" "` ）。<br />3. 在結尾的雙引號後面加上常數值型別字元， `C` 以強制將常值設為 `Char` 。 如果類型檢查參數（[Option Strict 語句](../../../language-reference/statements/option-strict-statement.md)）為，則這是必要的 `On` ，而且在任何情況下都是合適的。|

下列範例示範不成功和成功的常值指派至 `Char` 變數。

[!code-vb[VbVbalrDataTypes#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDataTypes/VB/Class1.vb#12)]

使用縮小轉換時，一律會有風險，因為它們可能會在執行時間失敗。 例如， `String` `Char` 如果 `String` 值包含一個以上的字元，從到的轉換可能會失敗。 因此，使用類型字元是較佳的程式設計 `C` 。

## <a name="string-conversion-fails-at-run-time"></a>字串轉換在執行時間失敗

[String 資料類型](../../../language-reference/data-types/string-data-type.md)只會參與非常少的擴輾轉換。 `String`只會擴大至本身和 `Object` ，且只有 `Char` 和 `Char()` （ `Char` 陣列）會擴展為 `String` 。 這是因為 `String` 變數和常數可以包含其他資料類型不能包含的值。

當類型檢查參數（[Option Strict 語句](../../../language-reference/statements/option-strict-statement.md)）為時 `On` ，編譯器不允許所有隱含的縮小轉換。 這包括涉及的相關內容 `String` 。 您的程式碼仍然可以使用轉換關鍵字（例如 `CStr` 和[CType](../../../language-reference/functions/ctype-function.md)函式），以指示 .NET Framework 嘗試轉換。

> [!NOTE]
> 將集合中的專案轉換 `For Each…Next` 為迴圈控制變數時，會抑制縮小轉換錯誤。 如需詳細資訊和範例，請參閱 For Each ... 中的「縮小轉換」一節。 [下一個語句](../../../language-reference/statements/for-each-next-statement.md)。

### <a name="narrowing-conversion-protection"></a>縮小轉換保護

縮小轉換的缺點是它們可能會在執行時間失敗。 例如，如果 `String` 變數包含 "True" 或 "False" 以外的任何專案，就無法將它轉換成 `Boolean` 。 如果它包含標點符號字元，轉換成任何數數值型別會失敗。 除非您知道 `String` 變數一律保留目的地類型可接受的值，否則您不應該嘗試轉換。

如果您必須從轉換成 `String` 另一種資料類型，最安全的程式是將嘗試的轉換放在[Try .。。Catch .。。Finally 語句](../../../language-reference/statements/try-catch-finally-statement.md)。 這可讓您處理運行時失敗。

### <a name="character-arrays"></a>字元陣列

單一 `Char` 和 `Char` 元素陣列都會擴大為 `String` 。 不過，不 `String` 會擴展為 `Char()` 。 若要將 `String` 值轉換成 `Char` 陣列，您可以使用 <xref:System.String.ToCharArray%2A> 類別的方法 <xref:System.String?displayProperty=nameWithType> 。

### <a name="meaningless-values"></a>無意義的值

一般而言， `String` 值在其他資料類型中沒有意義，而且轉換會具有高度的人工和危險性。 可能的話，您應該將變數的使用限制 `String` 為其設計所在的字元序列。 您絕對不應該撰寫依賴其他類型之對等值的程式碼。

## <a name="see-also"></a>另請參閱

- [資料類型](index.md)
- [類型字元](type-characters.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [Visual Basic 中的類型轉換](type-conversions.md)
- [資料類型](../../../language-reference/data-types/index.md)
- [Type Conversion Functions](../../../language-reference/functions/type-conversion-functions.md)
- [有效率地使用資料類型](efficient-use-of-data-types.md)
