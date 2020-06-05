---
title: Sub 運算式
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [Visual Basic], sub expression
- Sub Expression [Visual Basic]
- subroutines [Visual Basic], sub expressions
ms.assetid: 36b6bfd1-6539-4d8f-a5eb-6541a745ffde
ms.openlocfilehash: f862730220d0595faecaa915b1eaad2a3cdc0053
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406310"
---
# <a name="sub-expression-visual-basic"></a>Sub 運算式 (Visual Basic)
宣告定義副程式 lambda 運算式的參數和程式碼。  
  
## <a name="syntax"></a>語法  
  
```vb  
Sub ( [ parameterlist ] ) statement  
- or -  
Sub ( [ parameterlist ] )  
  [ statements ]  
End Sub  
```  
  
## <a name="parts"></a>組件  
  
|詞彙|定義|  
|---|---|  
|`parameterlist`|選擇性。 本機變數名稱的清單，代表程式的參數。 即使清單是空的，括弧也必須存在。 如需詳細資訊，請參閱 [Parameter List](../statements/parameter-list.md)。|  
|`statement`|必要。 單一語句。|  
|`statements`|必要。 陳述式的清單。|  
  
## <a name="remarks"></a>備註  
 *Lambda 運算式*是沒有名稱，且會執行一或多個語句的副程式。 您可以在任何可使用委派類型的位置使用 lambda 運算式，但不包括的引數 `RemoveHandler` 。 如需委派的詳細資訊，以及搭配使用 lambda 運算式和委派的用法，請參閱[委派語句](../statements/delegate-statement.md)和[寬鬆委派轉換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)。  
  
## <a name="lambda-expression-syntax"></a>Lambda 運算式語法  
 Lambda 運算式的語法與標準副程式類似。 差異如下：  
  
- Lambda 運算式沒有名稱。  
  
- Lambda 運算式不能有修飾詞，例如 `Overloads` 或 `Overrides` 。  
  
- 單行 lambda 運算式的主體必須是語句，而不是運算式。 主體可以包含 sub 程式的呼叫，而不是函式呼叫的呼叫。  
  
- 在 lambda 運算式中，所有參數都必須具有指定的資料類型，否則必須推斷所有的參數。  
  
- `ParamArray`Lambda 運算式中不允許選擇性和參數。  
  
- Lambda 運算式中不允許使用泛型參數。  
  
## <a name="example"></a>範例  
 以下是將值寫入主控台的 lambda 運算式範例。 此範例會顯示副程式的單行和多行 lambda 運算式語法。 如需更多範例，請參閱[Lambda 運算式](../../programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 [!code-vb[VbVbalrLambdas#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>另請參閱

- [Sub 陳述式](../statements/sub-statement.md)
- [Lambda 運算式](../../programming-guide/language-features/procedures/lambda-expressions.md)
- [運算子和運算式](../../programming-guide/language-features/operators-and-expressions/index.md)
- [陳述式](../../programming-guide/language-features/statements.md)
- [寬鬆委派轉換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
