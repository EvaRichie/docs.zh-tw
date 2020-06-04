---
title: 作法：記錄例外狀況
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions, logging
- exceptions, tracking
ms.assetid: a26c60e2-ae39-444a-aebb-33eccadc0eeb
ms.openlocfilehash: 59ed7b836126a38f32b7c6f479570a566d236e6c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410110"
---
# <a name="how-to-log-exceptions-in-visual-basic"></a>如何：在 Visual Basic 中記錄例外狀況

您可以使用 `My.Application.Log` 和 `My.Log` 物件來記錄應用程式中發生之例外狀況的相關資訊。 下列範例示範如何使用 `My.Application.Log.WriteException` 方法，以記錄您明確攔截到的例外狀況和未處理的例外狀況。  
  
 如需記錄追蹤資訊，請使用 `My.Application.Log.WriteEntry` 方法。 如需詳細資訊，請參閱＜<xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>＞  
  
### <a name="to-log-a-handled-exception"></a>記錄已處理的例外狀況  
  
1. 建立將產生例外狀況資訊的方法。  
  
     [!code-vb[VbVbalrMyApplicationLog#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#9)]  
  
2. 使用 `Try...Catch` 區塊來攔截例外狀況。  
  
     [!code-vb[VbVbalrMyApplicationLog#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#6)]  
  
3. 將可產生例外狀況的程式碼放在 `Try` 區塊中。  
  
     取消 `Dim` 和 `MsgBox` 行的註解，造成 <xref:System.NullReferenceException> 例外狀況。  
  
     [!code-vb[VbVbalrMyApplicationLog#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#7)]  
  
4. 在 `Catch` 區塊中，使用 `My.Application.Log.WriteException` 方法來寫入例外狀況資訊。  
  
     [!code-vb[VbVbalrMyApplicationLog#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#8)]  
  
     下列範例顯示用於記錄已處理例外狀況的完整程式碼。  
  
     [!code-vb[VbVbalrMyApplicationLog#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#10)]  
  
### <a name="to-log-an-unhandled-exception"></a>記錄未處理的例外狀況  
  
1. 在 **方案總管**中選取專案。 在 [**專案**] 功能表上，選擇 [**屬性**]。  
  
2. 按一下 [應用程式] **** 索引標籤。  
  
3. 按一下 [檢視應用程式事件] **** 按鈕以開啟 [程式碼編輯器]。  
  
     這會開啟 ApplicationEvents.vb 檔案。  
  
4. 在 [程式碼編輯器] 中開啟 ApplicationEvents.vb 檔案。 在 [一般] **** 功能表上，選擇 [MyApplication 事件] ****。  
  
5. 在 [宣告]**** 功能表上，選擇 [未處理的例外狀況]****。  
  
     應用程式在主應用程式執行之前，引發 <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase.UnhandledException> 事件。  
  
6. 將 `My.Application.Log.WriteException` 方法加入 `UnhandledException` 事件處理常式。  
  
     [!code-vb[VbVbalrMyApplicationLog#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#4)]  
  
     下列範例顯示用於記錄未處理例外狀況的完整程式碼。  
  
     [!code-vb[VbVbalrMyApplicationLog#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/MyEventsFake.vb#5)]  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [使用應用程式記錄檔](working-with-application-logs.md)
- [作法：寫入記錄檔訊息](how-to-write-log-messages.md)
- [逐步解說：判斷 My.Application.Log 寫入資訊的位置](walkthrough-determining-where-my-application-log-writes-information.md)
- [逐步解說：變更 My.Application.Log 寫入資訊的位置](walkthrough-changing-where-my-application-log-writes-information.md)
