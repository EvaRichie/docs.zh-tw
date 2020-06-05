---
title: 疑難排解：記錄檔接聽程式
ms.date: 07/20/2015
helpviewer_keywords:
- event logs, troubleshooting
- troubleshooting Visual Basic, event logs
- troubleshooting event logs
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
ms.openlocfilehash: 8d2d8294d9e9bb42d72fe4f6c37bf846bd644907
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398314"
---
# <a name="troubleshooting-log-listeners-visual-basic"></a>疑難排解：記錄檔接聽程式 (Visual Basic)

您可以使用 `My.Application.Log` 和 `My.Log` 物件來記錄應用程式中發生之事件的相關資訊。  
  
 若要判斷哪些記錄檔接聽程式接收這些訊息，請參閱[逐步解說：判斷 My.Application.Log 寫入資訊的位置](walkthrough-determining-where-my-application-log-writes-information.md)。  
  
 `Log` 物件可以使用記錄檔篩選來限制記錄的資訊數量。 如果篩選條件設定錯誤，記錄檔可能包含錯誤的資訊。 如需詳細資訊，請參閱[逐步解說：篩選 My.Application.Log 輸出](walkthrough-filtering-my-application-log-output.md)。  
  
 不過，如果記錄檔設定不正確，您可能需要目前組態的詳細資訊。 您可以透過記錄檔的進階 `TraceSource` 屬性來取得這項資訊。  
  
### <a name="to-determine-the-log-listeners-for-the-log-object-in-code"></a>判斷程式碼中記錄檔物件的記錄檔接聽程式  
  
1. 在程式碼檔案的開頭處匯入 <xref:System.Diagnostics> 命名空間。 如需詳細資訊，請參閱 [Imports 陳述式 (.NET 命名空間和類型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
     [!code-vb[VbVbalrMyApplicationLog#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#13)]  
  
2. 建立會傳回字串的函式，而該字串包含每個記錄檔接聽程式的資訊。  
  
     [!code-vb[VbVbalrMyApplicationLog#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#14)]  
  
3. 將記錄檔的追蹤接聽程式集合傳遞至 `GetListeners` 函式，並顯示傳回值。  
  
     [!code-vb[VbVbalrMyApplicationLog#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#19)]  
  
     如需詳細資訊，請參閱 <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A> 。  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [使用應用程式記錄檔](working-with-application-logs.md)
- [逐步解說：判斷 My.Application.Log 寫入資訊的位置](walkthrough-determining-where-my-application-log-writes-information.md)
