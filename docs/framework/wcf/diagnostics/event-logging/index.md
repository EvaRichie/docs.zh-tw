---
title: WCF 的事件記錄
ms.date: 03/30/2017
helpviewer_keywords:
- event logging [WCF]
ms.assetid: aac0530d-f44c-45a1-bada-e30e0677b41f
ms.openlocfilehash: 535b3570f41cbfb277eeb14fb07242b528acea46
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96236152"
---
# <a name="event-logging-in-wcf"></a>WCF 的事件記錄

Windows Communication Foundation (WCF) 會追蹤 Windows 事件記錄檔中的內部事件。  
  
## <a name="viewing-event-logs"></a>檢視事件記錄檔  

 根據預設會自動啟用事件記錄，且沒有機制可停用它。 您可以使用事件檢視器來查看 WCF 所記錄的事件。 若要啟動此工具，請按一下 [ **開始**]，再依序按一下 [ **主控台**]、[系統 **管理工具**]，然後按兩下 [ **事件檢視器**]。  
  
### <a name="application-event-log"></a>應用程式事件記錄檔  

 **應用程式事件記錄** 檔包含 WCF 所產生的大部分事件。 大部分的項目都指出應用程式的特定功能無法啟動。 範例包括：  
  
- 訊息記錄/追蹤：當追蹤和訊息記錄失敗時，WCF 會將事件寫入事件記錄檔。 然而，並不是每次追蹤失敗都會觸發事件。 為了避免事件記錄檔完全填滿追蹤失敗，WCF 會針對這類事件實行10分鐘的停機時間。 這表示，如果 WCF 將追蹤失敗寫入事件記錄檔，則至少需要10分鐘的時間。  
  
- 共用接聽程式：WCF TCP Port Sharing Service 會在無法啟動時記錄事件。  
  
- CardSpace：當服務無法啟動時記錄事件。  
  
- 嚴重和錯誤事件，例如啟動失敗或當機  
  
- 訊息記錄已開啟：在訊息記錄已開啟時記錄事件。 這是要通知系統管理員，訊息標頭和本文中可能記錄了機密、應用程式特定的資訊。  
  
- 當設定 `enableLoggingKnownPII` 檔案之 `machineSettings` 項目中的 `machine.config` 屬性時，就會記錄事件。 這個屬性會指定是否允許任何在電腦上執行的應用程式記錄已知的個人可識別資訊 (PII)。  
  
- 如果 `logKnownPii` 或 `app.config` 檔案中的 `web.config` 屬性設定為 `true`，以便讓特定應用程式開啟 PII 記錄，但是 `enableLoggingKnownPII` 檔案之 `machineSettings` 項目中的 `machine.config` 屬性設定為 `false`，便會記錄事件。 此外，如果 `logKnownPii` 和 `enableLoggingKnownPII` 都設定為 `true`，便會記錄事件。 如需這些設定的詳細資訊，請參閱設定 [訊息記錄](../configuring-message-logging.md) 主題的安全性一節。  
  
### <a name="security-event-log"></a>安全性事件記錄檔  

 **安全性事件記錄** 檔包含 WCF 所記錄的安全性審核事件。  
  
### <a name="system-event-log"></a>系統事件記錄檔  

 WCF 不會將任何專案記錄在 **系統事件記錄** 檔中。  
  
### <a name="event-log-entries"></a>事件記錄檔項目  

 事件的 **來源** 是產生記錄專案的元件名稱。  
  
 事件記錄檔項目的型別是用於指出事件的嚴重性。 每個事件必須是單一型別，應用程式會在報告事件時指出。 事件檢視器會使用這個型別判斷要在記錄檔的清單檢視中顯示哪個圖示。 如需有關事件記錄檔項目的不同事件型別，請參閱 <xref:System.Diagnostics.EventLogEntryType>。  
  
 當您在事件檢視器中查看事件時，按一下 [詳細資訊] 時，事件檢視器可能會將資訊傳送到網際網路。 如需詳細資訊，請參閱「事件檢視器」的說明。  
  
## <a name="see-also"></a>另請參閱

- [系統管理與診斷](../index.md)
- [事件一般參考](events-general-reference.md)
