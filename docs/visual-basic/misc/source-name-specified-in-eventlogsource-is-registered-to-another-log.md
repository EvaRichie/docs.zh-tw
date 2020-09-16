---
title: 在 EventLogSource 中指定的來源名稱會登錄到不在 EventLogName 指定的記錄檔
ms.date: 07/20/2015
ms.assetid: 7317e100-098b-408d-86e5-7c74cf8558c7
ms.openlocfilehash: da9f1756909d1c37e28f2dde62a7f8a73bb19f37
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90555636"
---
# <a name="source-name-specified-in-eventlogsource-is-registered-to-a-log-other-than-that-specified-in-eventlogname"></a>在 EventLogSource 中指定的來源名稱會登錄到不在 EventLogName 指定的記錄檔
`EventLog` 嘗試參考登錄到不同記錄檔的來源。 如果要將項目寫入事件記錄檔，您必須指定 <xref:System.Diagnostics.EventLog.Source%2A> 屬性。 <xref:System.Diagnostics.EventLog.Source%2A> 屬性會將元件和事件記錄登錄為有效的項目來源。 單一來源一次只能和一筆事件記錄建立關聯 (因此寫入項目)。  
  
 根據預設，如果您嘗試寫入項目，卻沒有先將元件登錄為有效的來源，系統會使用 <xref:System.Diagnostics.EventLog.Source%2A> 屬性的值當做來源字串，自動登錄來源和事件記錄。  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
- 請確定來源已登錄到正確的記錄檔。 若要這樣做，請使用 <xref:System.Diagnostics.EventLog.CreateEventSource%2A> 方法或其多載之一，指定可向事件記錄檔唯一識別元件的字串。  
  
## <a name="see-also"></a>另請參閱

- [管理事件記錄檔](/previous-versions/visualstudio/visual-studio-2008/4f69axw4(v=vs.90))
- [事件記錄檔參考](/previous-versions/visualstudio/visual-studio-2008/k43k9z2a(v=vs.90))
- [如何：將應用程式新增為事件記錄檔專案的來源](/previous-versions/visualstudio/visual-studio-2008/xz73e171(v=vs.90))
- [如何：移除事件來源](/previous-versions/visualstudio/visual-studio-2008/k57466fc(v=vs.90))
