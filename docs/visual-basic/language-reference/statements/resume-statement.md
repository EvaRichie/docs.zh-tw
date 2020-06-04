---
title: Resume 陳述式
ms.date: 07/20/2015
f1_keywords:
- vb.Resume
- vb.ResumeNext
helpviewer_keywords:
- Next statement [Visual Basic], Resume
- Resume Next statement [Visual Basic]
- execution [Visual Basic], resuming
- run-time errors [Visual Basic], resuming after
- Resume statement [Visual Basic], syntax
- errors [Visual Basic], resuming after
- Error statement [Visual Basic], and Resume statement
- execution
- Resume statement [Visual Basic]
ms.assetid: e24d058b-1a5c-4274-acb9-7d295d3ea537
ms.openlocfilehash: 3f49f05f1deb2027b03bbf3443ca44f30c44344e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404209"
---
# <a name="resume-statement"></a>Resume 陳述式
在錯誤處理常式完成後繼續執行。  
  
 我們建議您盡可能在程式碼中使用結構化例外狀況處理，而不是使用非結構化例外狀況處理和 `On Error` 和 `Resume` 語句。 如需詳細資訊，請參閱 [Try...Catch...Finally 陳述式](try-catch-finally-statement.md)。  
  
## <a name="syntax"></a>語法  
  
```vb  
Resume [ Next | line ]  
```  
  
## <a name="parts"></a>組件  
 `Resume`  
 必要。 如果錯誤發生在與錯誤處理常式相同的程式中，則會繼續執行與造成錯誤的語句。 如果錯誤發生在被呼叫的程式中，則會在最後一次從包含錯誤處理常式的程式中呼叫的語句繼續執行。  
  
 `Next`  
 選擇性。 如果錯誤發生在與錯誤處理常式相同的程式中，則會以緊接在造成錯誤的語句之後的語句繼續執行。 如果錯誤發生在被呼叫的程式中，則會繼續執行，語句緊接在最後一次從包含錯誤處理常式（或語句）的程式所呼叫的語句之後 `On Error Resume Next` 。  
  
 `line`  
 選擇性。 執行會在必要引數中指定的那一行繼續進行 `line` 。 `line`引數是行標籤或行號，而且必須與錯誤處理常式位於相同的程式中。  
  
## <a name="remarks"></a>備註  
  
> [!NOTE]
> 我們建議您盡可能在程式碼中使用結構化例外狀況處理，而不是使用非結構化例外狀況處理和 `On Error` 和 `Resume` 語句。 如需詳細資訊，請參閱 [Try...Catch...Finally 陳述式](try-catch-finally-statement.md)。  
  
 如果您 `Resume` 在錯誤處理常式以外的任何地方使用語句，就會發生錯誤。  
  
 `Resume`語句不能用在包含語句的任何程式中 `Try...Catch...Finally` 。  
  
## <a name="example"></a>範例  
 這個範例會使用 `Resume` 語句來結束程式中的錯誤處理，然後使用導致錯誤的語句繼續執行。 產生錯誤號碼55以說明語句的使用 `Resume` 。  
  
 [!code-vb[VbVbalrErrorHandling#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#16)]  
  
## <a name="requirements"></a>規格需求  
 **命名空間：** [Microsoft.](../runtime-library-members.md)  
  
 **元件：** Visual Basic 執行時間程式庫（在 Microsoft 中）  
  
## <a name="see-also"></a>另請參閱

- [Try...Catch...Finally 陳述式](try-catch-finally-statement.md)
- [Error 陳述式](error-statement.md)
- [On Error 陳述式](on-error-statement.md)
