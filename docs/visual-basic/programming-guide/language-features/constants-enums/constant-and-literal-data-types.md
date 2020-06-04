---
title: 常數和常值資料類型
ms.date: 07/20/2015
helpviewer_keywords:
- declaring constants [Visual Basic], literal data types
- data types [Visual Basic], declaring
- constants [Visual Basic], declaring
- explicit declarations
- literals [Visual Basic], coercing data type
- declarations [Visual Basic], data types
ms.assetid: 057206d2-3a5b-40b9-b3af-57446f9b52fa
ms.openlocfilehash: b94259326b42104db05d9fc5bb09f686075d0759
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414527"
---
# <a name="constant-and-literal-data-types-visual-basic"></a>常數和常值資料類型 (Visual Basic)
常值是以本身的形式表示，而不是以變數的值或運算式的結果（例如數位3或字串 "Hello"）。 常數是一個有意義的名稱，它會取代常值，並在整個程式中保留這個相同的值，而不是變數，其值可能會變更。  
  
 當[Option 推斷](../../../language-reference/statements/option-infer-statement.md)為 `Off` ，且[option Strict](../../../language-reference/statements/option-strict-statement.md)為時 `On` ，您必須使用資料類型明確宣告所有常數。 在下列範例中，的資料類型 `MyByte` 會明確宣告為資料類型 `Byte` ：  
  
 [!code-vb[VbVbalrConstants#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#1)]  
  
 當 `Option Infer` 是 `On` 或 `Option Strict` 時 `Off` ，您可以使用子句來宣告常數，而不指定資料類型 `As` 。 編譯器會從運算式的類型判斷常數的類型。 數值整數常值預設會轉換成 `Integer` 資料類型。 浮點數字的預設資料類型是 `Double` 、和關鍵字， `True` 並 `False` 指定 `Boolean` 常數。  
  
## <a name="literals-and-type-coercion"></a>常值和類型強制型轉  
 在某些情況下，您可能會想要強制將常值指定為特定的資料類型。例如，將特別大的整數常值指派給類型的變數時 `Decimal` 。 下列範例會產生錯誤：  
  
```vb  
Dim myDecimal as Decimal  
myDecimal = 100000000000000000000   ' This causes a compiler error.  
```  
  
 此錯誤會因常值的標記法而產生。 `Decimal`資料類型可以保留這個大的值，但是常值會以隱含方式表示為 `Long` ，這不是。  
  
 您可以透過兩種方式將常值強制轉型為特定的資料類型：將類型字元附加至其中，或將它放在封入字元中。 類型字元或封入字元必須緊接在常值的前面和/或後面，不含任何類型的中間空格或字元。  
  
 若要讓先前的範例正常執行，您可以將 `D` 類型字元附加到常值，這會使其表示為 `Decimal` ：  
  
 [!code-vb[VbVbalrConstants#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#2)]  
  
 下列範例示範如何正確使用類型字元和封入字元：  
  
 [!code-vb[VbVbalrConstants#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConstants/VB/Class1.vb#3)]  
  
 下表顯示 Visual Basic 中可用的封閉字元和類型字元。  
  
|資料類型|封入字元|附加的類型字元|  
|---|---|---|  
|`Boolean`|(無)|(無)|  
|`Byte`|(無)|(無)|  
|`Char`|"|C|  
|`Date`|#|(無)|  
|`Decimal`|(無)|D 或@|  
|`Double`|(無)|R 或#|  
|`Integer`|(無)|I 或%|  
|`Long`|(無)|L 或 &|  
|`Short`|(無)|S|  
|`Single`|(無)|F 或！|  
|`String`|"|(無)|  
  
## <a name="see-also"></a>另請參閱

- [使用者定義的常數](user-defined-constants.md)
- [如何：宣告常數](how-to-declare-a-constant.md)
- [常數的概觀](constants-overview.md)
- [Long](../../../language-reference/statements/option-strict-statement.md)
- [Option Explicit 陳述式](../../../language-reference/statements/option-explicit-statement.md)
- [列舉的概觀](enumerations-overview.md)
- [如何：宣告列舉類型](how-to-declare-enumerations.md)
- [列舉和名稱限定性條件](enumerations-and-name-qualification.md)
- [資料類型](../../../language-reference/data-types/index.md)
- [常數和列舉](../../../language-reference/constants-and-enumerations.md)
