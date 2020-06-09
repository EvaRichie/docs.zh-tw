---
title: 以 Web 裝載佇列應用程式
ms.date: 03/30/2017
ms.assetid: c7a539fa-e442-4c08-a7f1-17b7f5a03e88
ms.openlocfilehash: 17c3d2167d3f98017c5f366ab0d700d9fb889f82
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600136"
---
# <a name="web-hosting-a-queued-application"></a>以 Web 裝載佇列應用程式
當工作者處理序包含裝載 Windows Communication Foundation (WCF) 服務的應用程式時，Windows 處理序啟用服務 (WAS) 會管理這些工作者處理序的啟用和存留期。 WAS 處理序模型會透過移除對 HTTP 的相依性，將 HTTP 伺服器的 IIS 6.0 處理序模型一般化。 這可讓 WCF 服務在支援以訊息為基礎之啟用的主控環境中，使用 HTTP 和非 HTTP 通訊協定（例如 net.tcp 和 msmq.formatname），並提供在指定電腦上裝載大量應用程式的功能。  
  
 WAS 包括訊息佇列 (MSMQ) 啟動服務，該服務會在佇列的應用程式所使用的其中一個佇列內置放一個或多個訊息時，啟動佇列的應用程式。 MSMQ 啟動服務是 NT 服務，預設為自動啟動。  
  
 如需 WAS 及其優點的詳細資訊，請參閱[在 Windows 進程啟用服務中裝載](hosting-in-windows-process-activation-service.md)。 如需有關 MSMQ 的詳細資訊，請參閱[佇列總覽](queues-overview.md)。
  
## <a name="queue-addressing-in-was"></a>WAS 中的佇列定址  
 WAS 應用程式擁有統一資源識別元 (URI) 位址。 應用程式位址包含兩個部分：基底 URI 前置詞和應用程式專屬的相對位址 (路徑)。 這兩個部分合在一起，便提供了應用程式的外部位址。 基底 URI 前置詞是由網站系結所組成，並用於網站下的所有應用程式，例如 "net.tcp：//localhost"、"msmq. msmq.formatname：//localhost" 或 "net.tcp：//localhost"。 接著會藉由取得應用程式特定的路徑片段（例如 "/applicationOne"）來建立應用程式位址，並將它們附加至基底 URI 前置詞，以抵達完整的應用程式 URI，例如 "net.tcp：//localhost/applicationOne"。  
  
 MSMQ 啟動服務會使用應用程式 URI，比對 MSMQ 啟動服務必須監視的訊息佇列。 當 MSMQ 啟動服務啟動時，便會在設定為訊息接收來源的電腦上，列舉其所有的公用和私用佇列，並且監視佇列中是否有訊息。 MSMQ 啟動服務每 10 分鐘會更新一次監視的佇列清單。 若在佇列中找到訊息，啟動服務就會將訊息名稱與 net.msmq 繫結中相符程度最高的應用程式 URI 進行比對，並啟動應用程式。  
  
> [!NOTE]
> 啟動的應用程式必須符合 (相符程度最高) 佇列名稱的前置詞。  
  
 例如，佇列名稱為：msmqWebHost/orderProcessing/service.svc。 如果應用程式 1 擁有虛擬目錄 /msmqWebHost/orderProcessing，而且其中有一個 service.svc 檔案，而應用程式 2 擁有虛擬目錄 /msmqWebHost，而其中有一個 orderProcessing.svc 檔案，則會啟動應用程式 1。 如果應用程式 1 被刪除，則會啟動應用程式 2。  
  
> [!NOTE]
> 當建立佇列時，任何傳送到該佇列的訊息都不會啟動應用程式，除非 MSMQ 啟動服務重新整理佇列清單，也就是自建立佇列起算最多 10 分鐘。 重新啟動啟動服務也同時會重新整理佇列清單。  
  
### <a name="the-effect-of-private-and-public-queues-on-addressing"></a>私用和公用佇列在定址上的影響  
 MSMQ 啟動服務並不會區分私用和公用佇列監視。 因此，您不能以相同名稱使用公用和私用佇列。 如果您這樣做，Web 裝載的應用程式可能會啟動，並從其中一個佇列讀取。  
  
### <a name="queue-configuration-for-activation"></a>啟動的佇列組態  
 MSMQ 啟動服務會以 NETWORK SERVICE 執行。 它是監視佇列以啟動應用程式的服務。 若要讓它從佇列啟動應用程式，則必須提供佇列，讓 NETWORK SERVICE 存取查看其存取控制清單 (ACL) 中的訊息。  
  
### <a name="poison-messaging"></a>有害訊息  
 WCF 中的有害訊息處理是由通道處理，這不只會偵測到訊息已有害，而是根據使用者設定來選取處置。 因此，佇列中會有單一訊息。 Web 裝載的應用程式會中止後續的次數，而且該訊息會移到重試佇列中。 在重試週期延遲所指定的時間點上，該訊息會從重試佇列移到主要佇列並再次嘗試。 但是這個動作需要佇列通道為使用中的狀態。 如果應用程式由 WAS 回收，那麼訊息就會留在重試佇列中，除非另一個訊息到達主要佇列並啟動佇列的應用程式。 這個情況的解決方法是手動將訊息從重試佇列移回主要佇列，以重新啟動應用程式。  
  
### <a name="subqueue-and-system-queue-caveat"></a>子佇列和系統佇列警告  
 WAS 裝載的應用程式無法根據系統佇列中的訊息啟動，例如整個系統寄不出的信件佇列，或是子佇列，例如有害子佇列。 這是這個產品版本的限制。  
  
## <a name="see-also"></a>請參閱

- [有害訊息處理](poison-message-handling.md)
- [服務端點與佇列定址](service-endpoints-and-queue-addressing.md)
