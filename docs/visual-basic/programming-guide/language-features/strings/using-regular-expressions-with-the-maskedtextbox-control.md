---
title: 將規則運算式與 MaskedTextBox 控制項搭配使用
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], regular expressions
- strings [Visual Basic], masked edit
ms.assetid: 2a048fb0-7053-487d-b2c5-ffa5e22ed6f9
ms.openlocfilehash: efda70be0ccdbc1f4b59d548e50f743f6c493b19
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363706"
---
# <a name="using-regular-expressions-with-the-maskedtextbox-control-in-visual-basic"></a>在 Visual Basic 中將規則運算式與 MaskedTextBox 控制項一起搭配使用
這個範例示範如何轉換簡單的正則運算式，以使用 <xref:System.Windows.Forms.MaskedTextBox> 控制項。  
  
## <a name="description-of-the-masking-language"></a>遮罩語言的描述  
 標準 <xref:System.Windows.Forms.MaskedTextBox> 遮罩語言是以 Visual Basic 6.0 中的控制項所使用的語言為基礎 `Masked Edit` ，對從該平臺進行遷移的使用者應該很熟悉。  
  
 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>控制項的屬性會 <xref:System.Windows.Forms.MaskedTextBox> 指定要使用的輸入遮罩。 遮罩必須是由下表中一或多個遮罩元素所組成的字串。  
  
|遮罩元素|Description|正則運算式元素|  
|---------------------|-----------------|--------------------------------|  
|0|介於0到9之間的任何單一位數。 需要輸入。|\d|  
|9|數位或空格。 選擇性專案。|[\d]？|  
|#|數位或空格。 選擇性專案。 如果遮罩中的這個位置保留空白，則會轉譯為空格。 允許加上（+）和減號（-）符號。|[\d +-]？|  
|L|ASCII 字母。 需要輸入。|[a-zA-Z]|  
|?|ASCII 字母。 選擇性專案。|[a-zA-Z]？|  
|&|字元。 需要輸入。|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]|  
|C|字元。 選擇性專案。|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]?|  
|A|拉丁字母. 選擇性專案。|\W|  
|.|符合文化特性的十進位預留位置。|無法使用。|  
|,|符合文化特性的千位預留位置。|無法使用。|  
|:|符合文化特性的時間分隔符號。|無法使用。|  
|/|符合文化特性的日期分隔符號。|無法使用。|  
|$|符合文化特性的貨幣符號。|無法使用。|  
|\<|將後面的所有字元轉換成小寫。|無法使用。|  
|>|將後面的所有字元轉換成大寫。|無法使用。|  
|&#124;|復原上一個上移或下移。|無法使用。|  
|&#92;|將遮罩字元轉義，將它轉換成常值。 " \\ \\ " 是反斜線的逸出序列。|&#92;|  
|所有其他字元。|常值。 所有非遮罩專案會在中以本身的形式出現 <xref:System.Windows.Forms.MaskedTextBox> 。|所有其他字元。|  
  
 Decimal （.）、萬分之一（，）、time （:)、date （/）和 currency （$）符號會預設為顯示應用程式文化特性所定義的符號。 您可以使用屬性，強制其顯示另一個文化特性的符號 <xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A> 。  
  
## <a name="regular-expressions-and-masks"></a>正則運算式和遮罩  
 雖然您可以使用正則運算式和遮罩來驗證使用者輸入，但它們並不完全相同。 正則運算式可以表達比遮罩更複雜的模式，但是遮罩可以更簡潔地表達相同的資訊，並採用與文化特性相關的格式。  
  
 下表比較四個正則運算式和各自的相等遮罩。  
  
|規則運算式|Mask|注意|  
|------------------------|----------|-----------|  
|`\d{2}/\d{2}/\d{4}`|`00/00/0000`|`/`遮罩中的字元是邏輯日期分隔符號，而且會向使用者顯示為應用程式目前文化特性適當的日期分隔符號。|  
|`\d{2}-[A-Z][a-z]{2}-\d{4}`|`00->L<LL-0000`|美國格式的日期（日、月縮寫和年），其中三個字母的月份縮寫會以初始大寫字母和後面接著兩個小寫字母來顯示。|  
|`(\(\d{3}\)-)?\d{3}-d{4}`|`(999)-000-0000`|美國電話號碼，區功能變數代碼為選用。 如果使用者不想要輸入選擇性字元，可以輸入空格或將滑鼠指標直接放在第一個0所代表的遮罩位置。|  
|`$\d{6}.00`|`$999,999.00`|貨幣值，範圍介於0到999999之間。 在執行時間會將貨幣、千位和十進位字元取代為其文化特性特定的對等專案。|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>
- <xref:System.Windows.Forms.MaskedTextBox>
- [在 Visual Basic 中驗證字串](validating-strings.md)
- [MaskedTextBox 控制項](../../../../framework/winforms/controls/maskedtextbox-control-windows-forms.md)
