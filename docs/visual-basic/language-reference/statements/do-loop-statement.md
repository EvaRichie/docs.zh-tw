---
title: Do...Loop 陳述式
ms.date: 07/20/2015
f1_keywords:
- vb.Do
- vb.Loop
- vb.Until
helpviewer_keywords:
- conditional statements [Visual Basic], Do�Loop
- while statement [Visual Basic], Do...Loop
- execution [Visual Basic], conditional
- Do loops
- Until keyword [Visual Basic], Do...Loop statement
- Do...Loop statement
- instructions, repeating
- Do statement [Visual Basic]
- Exit statement [Visual Basic], in Do...Loop statements
- loop structures [Visual Basic], Do�Loop statements
- do-while statements [Visual Basic]
- loops, exiting
- Loop keyword [Visual Basic], Do...Loop statement
ms.assetid: 892f9096-b3e2-4aee-834d-83bc4e2c379d
ms.openlocfilehash: a9ec6caccbe161a39b592a642a938b81bae911a6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404780"
---
# <a name="doloop-statement-visual-basic"></a>Do...Loop 陳述式 (Visual Basic)
在 `Boolean` 條件為 `True` 或直到條件變成之前，重複語句區塊 `True` 。  
  
## <a name="syntax"></a>語法  
  
```vb  
Do { While | Until } condition  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop  
' -or-  
Do  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop { While | Until } condition  
```  
  
## <a name="parts"></a>組件  
  
|詞彙|定義|  
|---|---|  
|`Do`|必要。 啟動迴圈的定義 `Do` 。|  
|`While`|除非使用 `Until`，否則為必要參數。 重複執行迴圈 `condition` ，直到為為止 `False` 。|  
|`Until`|除非使用 `While`，否則為必要參數。 重複執行迴圈 `condition` ，直到為為止 `True` 。|  
|`condition`|選擇性。 `Boolean` 運算式。 如果 `condition` 為 `Nothing` ，Visual Basic 會將它視為 `False` 。|  
|`statements`|選擇性。 一或多個在或之前重複的語句 `condition` 為 `True` 。|  
|`Continue Do`|選擇性。 將控制權轉移到迴圈的下一個反復專案 `Do` 。|  
|`Exit Do`|選擇性。 將控制權轉移給 `Do` 迴圈。|  
|`Loop`|必要。 終止迴圈的定義 `Do` 。|  
  
## <a name="remarks"></a>備註  
 `Do...Loop`當您想要重複一組語句而不限次數時，請使用結構，直到滿足條件為止。 如果您想要重複語句[設定的次數，請將 .。。下一個語句](for-next-statement.md)通常是較好的選擇。  
  
 您可以使用 `While` 或 `Until` 來指定 `condition` （而非兩者）。  
  
 您只能 `condition` 在迴圈的開始或結束時測試一次。 如果您在 `condition` 迴圈開始時進行測試（在語句中 `Do` ），迴圈可能不會執行一次。 如果您在迴圈結尾處進行測試（在語句中 `Loop` ），迴圈一律會至少執行一次。  
  
 條件通常是由兩個值的比較所產生，但它可以是任何會評估為[布林資料類型](../data-types/boolean-data-type.md)值（ `True` 或）的運算式 `False` 。 這包括已轉換成的其他資料類型（例如數數值型別）的值 `Boolean` 。  
  
 您可以藉 `Do` 由在另一個迴圈中放入迴圈來加以嵌套。 您也可以在彼此之間嵌套不同類型的控制結構。 如需詳細資訊，請參閱[嵌套控制項結構](../../programming-guide/language-features/control-flow/nested-control-structures.md)。  
  
> [!NOTE]
> `Do...Loop`結構提供比 While 更多的彈性[.。。End While 語句](while-end-while-statement.md)，因為它可讓您決定是否要在停止時 `condition` `True` 或第一次變成時結束迴圈 `True` 。 它也可讓您 `condition` 在迴圈的開頭或結尾進行測試。  
  
## <a name="exit-do"></a>Exit Do  
 [Exit Do](exit-statement.md)語句可以提供另一個結束的方式 `Do…Loop` 。 `Exit Do`立即將控制權轉移至語句後面的語句 `Loop` 。  
  
 `Exit Do`通常會在評估部分條件之後使用，例如在結構中 `If...Then...Else` 。 如果您偵測到不必要或無法繼續反覆運算的條件（例如錯誤值或終止要求），您可能會想要結束迴圈。 的其中一種用途 `Exit Do` 是測試可能導致無止盡*迴圈*的條件，這是一種迴圈，可能會執行很長或甚至無限次數。 您可以使用 `Exit Do` 來轉義迴圈。  
  
 您可以在中的任何位置包含任意數目的 `Exit Do` 語句 `Do…Loop` 。  
  
 在嵌套迴圈中使用時 `Do` ，會 `Exit Do` 將控制項從最內層的迴圈轉移到下一個較高層級的嵌套。  
  
## <a name="example"></a>範例  
 在下列範例中，迴圈中的語句會繼續執行，直到 `index` 變數大於10為止。 `Until`子句位於迴圈的結尾。  
  
 [!code-vb[VbVbalrStatements#131](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#131)]  
  
## <a name="example"></a>範例  
 下列範例 `While` 會使用子句（而非 `Until` 子句），並在 `condition` 迴圈開始時測試，而不是在結尾處進行測試。  
  
 [!code-vb[VbVbalrStatements#132](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#132)]  
  
## <a name="example"></a>範例  
 在下列範例中， `condition` 當變數大於100時，會停止迴圈 `index` 。 `If`不過，迴圈中的語句會導致語句在 `Exit Do` 索引變數大於10時停止迴圈。  
  
 [!code-vb[VbVbalrStatements#133](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#133)]  
  
## <a name="example"></a>範例  
 下列範例會讀取文字檔中的所有行。 <xref:System.IO.File.OpenText%2A>方法會開啟檔案，並傳回 <xref:System.IO.StreamReader> 讀取字元的。 在 `Do...Loop` 條件中，的 <xref:System.IO.StreamReader.Peek%2A> 方法 `StreamReader` 會決定是否有任何額外的字元。  
  
 [!code-vb[VbVbalrStatements#134](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#134)]  
  
## <a name="see-also"></a>另請參閱

- [迴圈結構](../../programming-guide/language-features/control-flow/loop-structures.md)
- [For...Next 陳述式](for-next-statement.md)
- [Boolean 資料類型](../data-types/boolean-data-type.md)
- [巢狀控制結構](../../programming-guide/language-features/control-flow/nested-control-structures.md)
- [Exit 陳述式](exit-statement.md)
- [While...End While 陳述式](while-end-while-statement.md)
