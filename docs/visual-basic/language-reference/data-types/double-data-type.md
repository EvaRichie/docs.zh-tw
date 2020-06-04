---
title: Double 資料類型
ms.date: 07/20/2015
f1_keywords:
- vb.Double
helpviewer_keywords:
- 'identifier type characters [Visual Basic], #'
- trailing zeros
- real numbers
- trailing 0 characters [Visual Basic]
- 0 characters [Visual Basic], trailing
- literal type characters [Visual Basic], R
- data types [Visual Basic], assigning
- Double data type [Visual Basic]
- '# identifier type character'
- double-precision numbers
- floating-point numbers [Visual Basic], Double data type
- R literal type character [Visual Basic]
- zeros, trailing
- Double data type
ms.assetid: 0c5670f7-fcb1-453a-bef1-374730cd38fd
ms.openlocfilehash: 899554f427ac77ead465752c35e51ca88d045763
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415630"
---
# <a name="double-data-type-visual-basic"></a>Double 資料類型 (Visual Basic)

保存已簽署的 IEEE 64 位（8位元組）雙精確度浮點數，範圍介於-1.79769313486231570 E + 308 到-4.94065645841246544 E-324 中的負值，以及從 4.94065645841246544 E-324 到 1.79769313486231570 E + 308 的正值。 雙精度浮點數會儲存實數的近似值。

## <a name="remarks"></a>備註

`Double`資料類型會針對某個數位提供最大和最小的可能巨量。

`Double` 的預設值為 0。

## <a name="programming-tips"></a>程式設計提示

- **精密.** 當您使用浮點數時，請記住它們不一定會在記憶體中有精確的標記法。 這可能會導致某些作業產生非預期的結果，例如值比較和 `Mod` 運算子。 如需詳細資訊，請參閱針對[資料類型進行疑難排解](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)。

- **尾端零。** 浮點資料類型沒有尾端零字元的任何內部表示。 例如，它們不會區分4.2000 和4.2。 因此，當您顯示或列印浮點值時，不會出現尾端的零字元。

- **輸入字元。** 將常值類型字元 `R` 附加到常值，會強制其成為 `Double` 資料類型。 例如，如果整數值後面接著 `R` ，則值會變更為 `Double` 。

  ```vb
  ' Visual Basic expands the 4 in the statement Dim dub As Double = 4R to 4.0:
  Dim dub As Double = 4.0R
  ```

  將識別項類型字元 `#` 附加到任何識別項，會強制其成為 `Double`。 在下列範例中，變數的 `num` 類型為 `Double` ：

  ```vb
  Dim num# = 3
  ```

- **架構類型：** 在 .NET Framework 中對應的類型為 <xref:System.Double?displayProperty=nameWithType> 結構。

## <a name="see-also"></a>另請參閱

- <xref:System.Double?displayProperty=nameWithType>
- [資料類型](index.md)
- [Decimal 資料類型](decimal-data-type.md)
- [Single 資料類型](single-data-type.md)
- [Type Conversion Functions](../functions/type-conversion-functions.md)
- [轉換摘要](../keywords/conversion-summary.md)
- [有效率地使用資料類型](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [疑難排解資料類型的問題](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [類型字元](../../programming-guide/language-features/data-types/type-characters.md)
