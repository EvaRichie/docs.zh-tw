---
title: 決策結構
ms.date: 07/20/2015
helpviewer_keywords:
- statements [Visual Basic], control flow
- If statement [Visual Basic], decision structures
- If statement [Visual Basic], If...Then...Else
- control flow [Visual Basic], decision structures
- decision structures [Visual Basic]
- conditional statements [Visual Basic], decision structures
ms.assetid: 2e2e0895-4483-442a-b17c-26aead751ec2
ms.openlocfilehash: 79c4949cd4d5b07d1b1d666b21467bf8db41ab3d
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91095612"
---
# <a name="decision-structures-visual-basic"></a>決策結構 (Visual Basic)

Visual Basic 可讓您根據測試的結果，測試條件並執行不同的作業。 您可以針對運算式的各種值，或在執行一連串語句時所產生的各種例外狀況，測試條件是否為 true 或 false。  
  
 下圖顯示的決策結構會測試條件是否為 true，並根據它是 true 或 false 來採取不同的動作。  
  
 ![If 的流程圖。然後。。。其他結構。](./media/decision-structures/if-then-else-construction.gif)  
  
## <a name="ifthenelse-construction"></a>如果。。。然後。。。其他結構  

 `If...Then...Else` 結構可讓您測試一或多個條件，並根據每個條件執行一或多個語句。 您可以透過下列方式來測試條件和採取動作：  
  
- 如果條件為，請執行一或多個語句 `True`  
  
- 如果條件為，請執行一或多個語句 `False`  
  
- 如果條件為，則執行某些語句 `True` ，如果是，則為其他語句 `False`  
  
- 如果先前的條件為，請測試其他條件 `False`  
  
 提供上述所有可能性的控制結構是 [.。。然後。。。Else 語句](../../../language-reference/statements/if-then-else-statement.md)。 如果您只有一個測試和一個要執行的語句，您可以使用單行版本。 如果您有一組更複雜的條件和動作，您可以使用多行版本。  
  
## <a name="selectcase-construction"></a>選擇。。。案例結構  

 此 `Select...Case` 結構可讓您一次評估運算式，並根據不同的可能值執行不同的語句集合。 如需詳細資訊，請參閱 [Select .。。Case 語句](../../../language-reference/statements/select-case-statement.md)。  
  
## <a name="trycatchfinally-construction"></a>嘗試。。。抓住。。。Finally 結構  

 `Try...Catch...Finally` 如果任何一個語句造成例外狀況，則結構可讓您在環境下執行一組語句，以保留控制權。 針對不同的例外狀況，您可以採取不同的動作。 您可以選擇性地指定在結束整個結構之前執行的程式碼區塊 `Try...Catch...Finally` ，而不論發生什麼事。 如需詳細資訊，請參閱 [Try...Catch...Finally 陳述式](../../../language-reference/statements/try-catch-finally-statement.md)。  
  
> [!NOTE]
> 針對許多控制結構，當您按一下關鍵字時，結構中的所有關鍵詞都會反白顯示。 例如，當您 `If` 在結構中按一下時 `If...Then...Else` ， `If` 會反 `Then` `ElseIf` `Else` `End If` 白顯示該結構中、、、和的所有實例。 若要移至下一個或上一個反白顯示的關鍵字，請按 CTRL + SHIFT + 向下鍵或 CTRL + SHIFT + 向上鍵。  
  
## <a name="see-also"></a>另請參閱

- [控制流程](index.md)
- [迴圈結構](loop-structures.md)
- [其他控制結構](other-control-structures.md)
- [巢狀控制結構](nested-control-structures.md)
- [If 運算子](../../../language-reference/operators/if-operator.md)
