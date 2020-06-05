---
title: 資料類型
ms.date: 07/20/2015
helpviewer_keywords:
- data types [Visual Basic], declaring
- typing
- data types [Visual Basic]
- Visual Basic code, data types
- data types [Visual Basic], improving speed with
ms.assetid: 5e1b9aaf-c7ca-4b29-9b22-0e82ed8e85e2
ms.openlocfilehash: 928d7fb6a40873641ae3e91e057c272b946a0091
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393711"
---
# <a name="data-types-in-visual-basic"></a>Visual Basic 中的資料類型
程式設計元素的「資料類型」** 是指其可以保留何種資料，以及儲存該資料的方式。 資料類型會應用於所有能儲存在電腦記憶體中的值，或是所有參與運算式評估的值。 每個變數、常值、常數、列舉、屬性、程序參數、程序引數和程序傳回值都具有資料類型。  
  
## <a name="declared-data-types"></a>已宣告的資料類型  
 您可以使用宣告陳述式來定義程式設計元素，並以 `As` 子句來指定其資料類型。 下表顯示用來宣告各種元素的陳述式。  
  
|程式設計元素|資料類型宣告|  
|-------------------------|---------------------------|  
|變數|在 [Dim 陳述式](../../../language-reference/statements/dim-statement.md)中<br /><br /> `Dim`   `amount As Double`<br /><br /> `Static`   `yourName As String`<br /><br /> `Public`   `billsPaid As Decimal = 0`|  
|常值|藉由常值類型字元；請參閱[類型字元](type-characters.md)中的＜常值類型字元＞<br /><br /> `Dim searchChar As Char = "."`  `C`|  
|持續性|在 [Const 陳述式](../../../language-reference/statements/const-statement.md)中<br /><br /> `Const`   `modulus As Single = 4.17825F`|  
|列舉型別|在 [Enum 陳述式](../../../language-reference/statements/enum-statement.md)中<br /><br /> `Public`   `Enum`   `colors`|  
|屬性|在 [Property 陳述式](../../../language-reference/statements/property-statement.md)中<br /><br /> `Property`   `region() As String`|  
|程序參數|在 [Sub 陳述式](../../../language-reference/statements/sub-statement.md)、[Function 陳述式](../../../language-reference/statements/function-statement.md)或 [Operator 陳述式](../../../language-reference/statements/operator-statement.md)中<br /><br /> `Sub addSale(ByVal`   `amount`   `As Double)`|  
|程序引數|在呼叫程式碼中；每個引數都是已宣告的程式設計元素，或是包含已宣告元素的運算式<br /><br /> `subString = Left(`  `inputString`  `,`   `5`  `)`|  
|程序傳回值|在 [Function 陳述式](../../../language-reference/statements/function-statement.md)或 [Operator 陳述式](../../../language-reference/statements/operator-statement.md)中<br /><br /> `Function convert(ByVal b As Byte)`   `As String`|  
  
 如需 Visual Basic 資料類型清單，請參閱[資料類型](../../../language-reference/data-types/index.md)。  
  
## <a name="see-also"></a>另請參閱

- [類型字元](type-characters.md)
- [基礎資料類型](elementary-data-types.md)
- [複合資料類型](composite-data-types.md)
- [Generic Types in Visual Basic](generic-types.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [Visual Basic 中的類型轉換](type-conversions.md)
- [結構](structures.md)
- [Tuples](tuples.md)
- [疑難排解資料類型的問題](troubleshooting-data-types.md)
- [資料類型](../../../language-reference/data-types/index.md)
- [有效率地使用資料類型](efficient-use-of-data-types.md)
