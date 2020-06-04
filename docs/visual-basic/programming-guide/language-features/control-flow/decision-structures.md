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
ms.openlocfilehash: aac9844240defc5a21a3f4e6090fa8f49e6348a1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403509"
---
# <a name="decision-structures-visual-basic"></a>決策結構 (Visual Basic)
Visual Basic 可讓您測試條件，並根據該測試的結果來執行不同的作業。 您可以針對運算式的各種值，或在執行一連串語句時產生的各種例外狀況，測試條件為 true 或 false。  
  
 下圖顯示的決策結構會測試條件是否為 true，並根據其為 true 或 false 來採取不同的動作。  
  
 ![If ... 的流程圖然後 .。。Else 結構。](./media/decision-structures/if-then-else-construction.gif)  
  
## <a name="ifthenelse-construction"></a>如果 .。。然後 .。。Else 結構  
 `If...Then...Else`[結構] 可讓您測試一或多個條件，並根據每個條件執行一或多個語句。 您可以透過下列方式來測試條件並採取動作：  
  
- 如果條件為，請執行一或多個語句`True`  
  
- 如果條件為，請執行一或多個語句`False`  
  
- 如果條件為 `True` ，且其他語句為，則執行`False`  
  
- 如果先前的條件為，請測試其他條件`False`  
  
 提供所有這些可能性的控制結構是[If .。。然後 .。。Else 語句](../../../language-reference/statements/if-then-else-statement.md)。 如果您只有一個測試和一個語句要執行，則可以使用單行版本。 如果您有一組更複雜的條件和動作，則可以使用多行版本。  
  
## <a name="selectcase-construction"></a>選取 .。。案例結構  
 此 `Select...Case` 結構可讓您評估一次運算式，並根據不同的可能值來執行不同的語句集。 如需詳細資訊，請參閱[Select .。。Case 語句](../../../language-reference/statements/select-case-statement.md)。  
  
## <a name="trycatchfinally-construction"></a>嘗試 .。。Catch .。。最後結構  
 `Try...Catch...Finally`結構可讓您在環境中執行一組語句，如果其中任何一個語句造成例外狀況，就會保留控制項。 您可以針對不同的例外狀況採取不同的動作。 您可以選擇性地指定在結束整個結構之前執行的程式碼區塊 `Try...Catch...Finally` ，無論發生什麼事。 如需詳細資訊，請參閱 [Try...Catch...Finally 陳述式](../../../language-reference/statements/try-catch-finally-statement.md)。  
  
> [!NOTE]
> 對於許多控制項結構而言，當您按一下關鍵字時，結構中的所有關鍵詞都會反白顯示。 例如，當您 `If` 在結構中按一下時 `If...Then...Else` ， `If` 會反 `Then` `ElseIf` `Else` `End If` 白顯示結構中、、、和的所有實例。 若要移至下一個或上一個反白顯示的關鍵字，請按 CTRL + SHIFT + 向下鍵或 CTRL + SHIFT + 向上鍵。  
  
## <a name="see-also"></a>另請參閱

- [控制流程](index.md)
- [迴圈結構](loop-structures.md)
- [其他控制結構](other-control-structures.md)
- [巢狀控制結構](nested-control-structures.md)
- [If 運算子](../../../language-reference/operators/if-operator.md)
