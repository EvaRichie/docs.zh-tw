---
title: 如何：呼叫運算子程序
ms.date: 07/20/2015
helpviewer_keywords:
- operator procedures [Visual Basic], calling
- procedures [Visual Basic], operator
- procedure calls [Visual Basic], operator overloading
- syntax [Visual Basic], Operator procedures
- operators [Visual Basic], overloading
- return values [Visual Basic], Operator procedures
- overloaded operators [Visual Basic], calling
- operator overloading
ms.assetid: 0dce42cc-f0b0-4c14-9f62-018b21f33497
ms.openlocfilehash: 0e88ff7b36535a709671a1f9b838f2b4488d1d37
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/23/2020
ms.locfileid: "91075183"
---
# <a name="how-to-call-an-operator-procedure-visual-basic"></a>如何：呼叫運算子程序 (Visual Basic)

您可以在運算式中使用運算子符號來呼叫運算子程式。 在轉換運算子的情況下，您可以呼叫 [CType 函數](../../../language-reference/functions/ctype-function.md) 將某個資料類型的值轉換成另一個資料類型。  
  
 您不會明確呼叫運算子程式。 您只要在 `CType` 指派語句或運算式中使用運算子或函數，就如同您一般使用運算子一樣。 Visual Basic 會對運算子程式進行呼叫。  
  
 在類別或結構上定義運算子 *也稱為多* 載運算子。  
  
### <a name="to-call-an-operator-procedure"></a>呼叫運算子程式  
  
1. 以一般方式使用運算式中的運算子符號。  
  
2. 請確定運算元的資料類型適用于運算子，且順序正確。  
  
3. 運算子會如預期般參與運算式的值。  
  
### <a name="to-call-a-conversion-operator-procedure"></a>呼叫轉換運算子程式  
  
1. `CType`在運算式內使用。  
  
2. 請確定運算元的資料類型適用于轉換，且順序正確。  
  
3. `CType` 呼叫轉換運算子程式，並傳回已轉換的值。  
  
## <a name="example"></a>範例  

 下列範例會建立兩個 <xref:System.TimeSpan> 結構，並將其新增至其中，然後將結果儲存在第三個 <xref:System.TimeSpan> 結構中。 <xref:System.TimeSpan>結構會定義運算子程式來多載數個標準運算子。  
  
 [!code-vb[VbVbcnProcedures#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#29)]  
  
 因為多載 <xref:System.TimeSpan> 標準 `+` 運算子，所以先前的範例會在計算的值時呼叫運算子程式 `combinedSpan` 。  
  
 如需呼叫對話運算子程式的範例，請參閱 [如何：使用定義運算子的類別](./how-to-use-a-class-that-defines-operators.md)。  
  
## <a name="compile-the-code"></a>編譯程式碼  

 請確定您使用的類別或結構定義您想要使用的運算子。  
  
## <a name="see-also"></a>另請參閱

- [運算子程序](./operator-procedures.md)
- [如何：定義運算子](./how-to-define-an-operator.md)
- [How to: Define a Conversion Operator](./how-to-define-a-conversion-operator.md)
- [Operator Statement](../../../language-reference/statements/operator-statement.md)
- [Widening](../../../language-reference/modifiers/widening.md)
- [Narrowing](../../../language-reference/modifiers/narrowing.md)
- [Structure 陳述式](../../../language-reference/statements/structure-statement.md)
- [作法：宣告結構](../data-types/how-to-declare-a-structure.md)
- [隱含和明確轉換](../data-types/implicit-and-explicit-conversions.md)
- [Widening and Narrowing Conversions](../data-types/widening-and-narrowing-conversions.md)
