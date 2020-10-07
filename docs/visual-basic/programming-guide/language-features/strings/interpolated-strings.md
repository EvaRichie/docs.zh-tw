---
title: 字串插值
ms.date: 10/31/2017
ms.openlocfilehash: c427b48ce58a59ff3878f24f1989db6ac8c8239a
ms.sourcegitcommit: 636af37170ae75a11c4f7d1ecd770820e7dfe7bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91805274"
---
# <a name="interpolated-strings-visual-basic-reference"></a>將字串插入 (Visual Basic 參考) 

可用來建構字串。  字串插值類似包含「插入運算式」** 的範本字串。  字串插值會傳回一個字串，以將內含的插入運算式取代為運算式的字串表示。 這項功能可在 Visual Basic 14 和更新版本中使用。

字串插值的引數比[複合格式字串](../../../../standard/base-types/composite-formatting.md#composite-format-string)更容易了解。  例如，字串插值

```vb
Console.WriteLine($"Name = {name}, hours = {hours:hh}")
```

包含兩個插入運算式 '{name}' 和 '{hours:hh}'。 對等的複合格式字串為：

```vb
Console.WriteLine("Name = {0}, hours = {1:hh}", name, hours)
```

字串插值的結構為：

```vb
$"<text> {<interpolated-expression> [,<field-width>] [:<format-string>] } <text> ..."
```

其中：

- *field-width* 是帶正負號的整數，表示欄位中的字元數。 如果是正數，則欄位會靠右對齊；如果是負數，則會靠左對齊。

- *format-string* 是一個格式字串，適用於將格式化的物件類型。 例如， <xref:System.DateTime> 值可以是 [標準日期和時間格式字串](../../../../standard/base-types/standard-date-and-time-format-strings.md) （例如 "d" 或 "d"）。

> [!IMPORTANT]
> 字串開頭的 `$` 與 `"` 之間不能有空白字元。 這麼做會導致編譯器錯誤。

您可以在使用字串常值的任何位置使用字串插值。  每次執行含有字串插值的程式碼時，都會評估字串插值。 這可讓您分開定義和評估字串插值。

若要在字串插值中包含大括弧 ("{" 或 "}")，請使用雙大括弧 "{{" 或 "}}"。  如需詳細資訊，請參閱＜隱含轉換＞一節。

當字串插值包含在字串插值中具有特殊意義的其他字元時 (例如引號 (")、冒號 (:) 或逗號 (,))，如果這些字元出現在常值文字中，則必須將它逸出；如果這些字元是包含在插入運算式中的語言項目，則必須加入以括號分隔的運算式。 下列範例會以引號括住，以將它們包含在結果字串中：

[!code-vb[interpolated-strings](../../../../../samples/snippets/visualbasic/programming-guide/language-features/strings/interpolated-strings4.vb)]

## <a name="implicit-conversions"></a>隱含的轉換

有三個來自字串插值的隱含型別轉換：

1. 將字串插值轉換成 <xref:System.String>。 下列範例會傳回一個字串，其字串插值運算式已取代為運算式的字串表示。 例如：

   [!code-vb[interpolated-strings1](../../../../../samples/snippets/visualbasic/programming-guide/language-features/strings/interpolated-strings1.vb)]

   這是字串解譯的最終結果。 所有出現的雙大括弧 ("{{" 和 "}}") 都會轉換成單一大括弧。

2. 將字串插值轉換成 <xref:System.IFormattable> 變數，可讓您從單一 <xref:System.IFormattable> 執行個體建立多個具有特定文化特性內容的結果字串。 若要加入個別文化特性的正確數值和日期格式等項目時，這樣做會很有用。  在您明確或隱含呼叫 <xref:System.Object.ToString> 方法以格式化字串之前，所有出現的雙大括弧 ("{{" 和 "}}") 會保持為雙大括弧。  所有包含的插補運算式都會轉換成 {0} 、 {1} 等等。

   下列範例使用反映來顯示成員，以及從字串插值建立之 <xref:System.IFormattable> 變數的欄位和屬性值。 它也會將 <xref:System.IFormattable> 變數傳遞給 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> 方法。

   [!code-vb[interpolated-strings2](../../../../../samples/snippets/visualbasic/programming-guide/language-features/strings/interpolated-strings2.vb)]

   請注意，只能使用反映來檢查字串插值。 如果將它傳遞至字串格式化方法 (例如 <xref:System.Console.WriteLine(System.String)>)，則會解析其格式項目並傳回結果字串。

3. 將字串插值轉換成 <xref:System.FormattableString> 代表複合格式字串的變數。 檢查複合格式字串及其如何轉譯為結果字串有助於在建立查詢時，防止插入式攻擊。 <xref:System.FormattableString>也包括：

      - 產生 <xref:System.Globalization.CultureInfo.CurrentCulture> 的結果字串的 <xref:System.FormattableString.ToString> 多載。

      - <xref:System.FormattableString.Invariant%2A>產生之字串的方法 <xref:System.Globalization.CultureInfo.InvariantCulture> 。

      - 產生指定文化特性的結果字串的 <xref:System.FormattableString.ToString(System.IFormatProvider)> 方法。

    所有出現的雙大括弧 ( "{{" 和 "}}" ) 會保持為雙大括弧，直到您格式化為止。  所有包含的插補運算式都會轉換成 {0} 、 {1} 等等。

   [!code-vb[interpolated-strings3](../../../../../samples/snippets/visualbasic/programming-guide/language-features/strings/interpolated-strings3.vb)]

## <a name="see-also"></a>請參閱

- <xref:System.IFormattable?displayProperty=nameWithType>
- <xref:System.FormattableString?displayProperty=nameWithType>
- [Visual Basic 語言參考](index.md)
