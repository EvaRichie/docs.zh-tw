---
title: 字串操作方法的類型
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], manipulating [Visual Basic]
- string manipulation
ms.assetid: 905055cd-7f50-48fb-9eed-b0995af1dc1f
ms.openlocfilehash: aba9af9c699cf8d07862c5d2967902bec1623500
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363755"
---
# <a name="types-of-string-manipulation-methods-in-visual-basic"></a>Visual Basic 中字串管理方法的類型
有數種不同的方式可以分析和操作您的字串。 某些方法是 Visual Basic 語言的一部分，而有些則是類別中的固有方式 `String` 。  
  
## <a name="visual-basic-language-and-the-net-framework"></a>Visual Basic 語言和 .NET Framework  
 Visual Basic 方法會當做語言的固有函式使用。 在您的程式碼中，您可以使用它們，而不需要限定。 下列範例顯示 Visual Basic 字串操作命令的一般用法：  
  
 [!code-vb[VbVbalrStrings#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#44)]  
  
 在此範例中，函式會 `Mid` 在上執行直接作業 `aString` ，並將值指派給 `bString` 。  
  
 如需 Visual Basic 字串操作方法的清單，請參閱[字串操作摘要](../../../language-reference/keywords/string-manipulation-summary.md)。  
  
### <a name="shared-methods-and-instance-methods"></a>共用方法和實例方法  
 您也可以使用類別的方法來操作字串 `String` 。 中有兩種類型的方法 `String` ：*共用*方法和*實例*方法。  
  
#### <a name="shared-methods"></a>共用方法  
 共用方法是源自類別本身的方法，不 `String` 需要該類別的實例就能運作。 這些方法可以使用類別（）的名稱來限定， `String` 而不是使用類別的實例 `String` 。 例如：  
  
 [!code-vb[VbVbalrStrings#45](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#45)]  
  
 在上述範例中， <xref:System.String.Copy%2A?displayProperty=nameWithType> 方法是靜態方法，它會在指定的運算式上運作，並將產生的值指派給 `bString` 。  
  
#### <a name="instance-methods"></a>實例方法  
 相反地，實例方法是來自特定實例， `String` 而且必須使用實例名稱來限定。 例如：  
  
 [!code-vb[VbVbalrStrings#46](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#46)]  
  
 在此範例中， <xref:System.String.Substring%2A?displayProperty=nameWithType> 方法是實例的方法 `String` （也就是 `aString` ）。 它會對執行作業 `aString` ，並將該值指派給 `bString` 。  
  
 如需詳細資訊，請參閱類別的檔 <xref:System.String> 。  
  
## <a name="see-also"></a>另請參閱

- [Visual Basic 中的字串簡介](introduction-to-strings.md)
