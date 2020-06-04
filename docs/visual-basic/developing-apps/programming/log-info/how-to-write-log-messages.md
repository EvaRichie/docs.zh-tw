---
title: 作法：寫入記錄檔訊息
ms.date: 07/20/2015
helpviewer_keywords:
- My.Application.Log object, writing log messages
ms.assetid: 972a3e0c-2996-4623-a7a9-d7ebc4d207f8
ms.openlocfilehash: 28c5fe77e2711dfcac96e621a90fb9506eb74775
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410045"
---
# <a name="how-to-write-log-messages-visual-basic"></a>如何：寫入記錄訊息 (Visual Basic)

您可以使用 `My.Application.Log` 和 `My.Log` 物件記錄應用程式的相關資訊。 此範例示範如何使用 `My.Application.Log.WriteEntry` 方法寫入追蹤資訊。

如需記錄例外狀況資訊，請使用 `My.Application.Log.WriteException` 方法；請參閱[如何：記錄例外狀況](how-to-log-exceptions.md)。

## <a name="example"></a>範例

此範例使用 `My.Application.Log.WriteEntry` 方法以寫出追蹤資訊。

[!code-vb[VbVbalrMyApplicationLog#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#11)]

## <a name="net-framework-security"></a>.NET Framework 安全性

請確定您寫入記錄檔的資料不包含機密資訊，例如使用者密碼。 如需詳細資訊，請參閱[使用應用程式記錄檔](working-with-application-logs.md)。

## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [使用應用程式記錄檔](working-with-application-logs.md)
- [作法：記錄例外狀況](how-to-log-exceptions.md)
- [逐步解說：判斷 My.Application.Log 寫入資訊的位置](walkthrough-determining-where-my-application-log-writes-information.md)
- [逐步解說：變更 My.Application.Log 寫入資訊的位置](walkthrough-changing-where-my-application-log-writes-information.md)
- [逐步解說：篩選 My.Application.Log 輸出](walkthrough-filtering-my-application-log-output.md)
