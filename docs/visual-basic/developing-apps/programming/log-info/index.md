---
title: 記錄來自應用程式的資訊
ms.date: 07/20/2015
helpviewer_keywords:
- Log object
- My.Log object
- applications [Visual Basic], logging information from
- logging
- My.Application.Log object
- examples [Visual Basic], logging application information
ms.assetid: 8bf4f047-22d6-48d6-aec5-93b98ad5b8e8
ms.openlocfilehash: 43738b2d654435532a98654cbc40af134d43f02c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410019"
---
# <a name="logging-information-from-the-application-visual-basic"></a>記錄來自應用程式的資訊 (Visual Basic)

本節包含的主題說明如何使用 `My.Application.Log` 或 `My.Log` 物件記錄來自應用程式的資訊，以及如何擴充應用程式的記錄功能。  
  
 `Log` 物件可提供將資訊寫入應用程式記錄檔接聽程式的方法，而 `Log` 物件的進階 `TraceSource` 屬性則提供詳細組態資訊。 `Log` 物件是由應用程式的組態檔進行設定。  
  
 `My.Log` 物件僅適用於 ASP.NET 應用程式。 若是用戶端應用程式，請使用 `My.Application.Log`。 如需詳細資訊，請參閱 <xref:Microsoft.VisualBasic.Logging.Log> 。  
  
## <a name="tasks"></a>工作  
  
|至|請參閱|  
|--------|---------|  
|將事件資訊寫入應用程式的記錄檔。|[作法：寫入記錄檔訊息](how-to-write-log-messages.md)|  
|將例外狀況資訊寫入應用程式的記錄檔。|[作法：記錄例外狀況](how-to-log-exceptions.md)|  
|在應用程式啟動和關閉時，將追蹤資訊寫入應用程式的記錄檔。|[作法：在應用程式啟動或關閉時記錄訊息](how-to-log-messages-when-the-application-starts-or-shuts-down.md)|  
|設定 `My.Application.Log` 以將資訊寫入文字檔。|[作法：將事件資訊寫入文字檔](how-to-write-event-information-to-a-text-file.md)|  
|設定 `My.Application.Log` 以將資訊寫入事件記錄檔。|[作法：寫入應用程式事件記錄檔](how-to-write-to-an-application-event-log.md)|  
|變更 `My.Application.Log` 寫入資訊的位置。|[逐步解說：變更 My.Application.Log 寫入資訊的位置](walkthrough-changing-where-my-application-log-writes-information.md)|  
|判斷 `My.Application.Log` 寫入資訊的位置。|[逐步解說：判斷 My.Application.Log 寫入資訊的位置](walkthrough-determining-where-my-application-log-writes-information.md)|  
|建立 `My.Application.Log` 的自訂記錄檔接聽程式。|[逐步解說：建立自訂記錄檔接聽程式](walkthrough-creating-custom-log-listeners.md)|  
|篩選 `My.Application.Log` 記錄檔的輸出。|[逐步解說：篩選 My.Application.Log 輸出](walkthrough-filtering-my-application-log-output.md)|  
  
## <a name="see-also"></a>另請參閱

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [使用應用程式記錄檔](working-with-application-logs.md)
- [疑難排解：記錄檔接聽程式](troubleshooting-log-listeners.md)
