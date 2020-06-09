---
title: System.ServiceModel.Channels.PeerFlooderReceiveMessageQuotaExceeded
ms.date: 03/30/2017
ms.assetid: b8371d0a-843e-440b-b86a-6996db131cb0
ms.openlocfilehash: 93afa0b495e20c02c58ac1fa75c31715eaa0e8dc
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596086"
---
# <a name="systemservicemodelchannelspeerflooderreceivemessagequotaexceeded"></a>System.ServiceModel.Channels.PeerFlooderReceiveMessageQuotaExceeded
訊息的傳入接收速率太高。  
  
## <a name="description"></a>描述  
 這個追蹤會發生在嘗試處理傳入訊息時。 訊息無法轉送到特定的芳鄰，因為已超過該芳鄰的配額設定。 這發生在沒有回應的芳鄰無法清除該芳鄰之擱置訊息的待辦項目。  
  
## <a name="troubleshooting"></a>疑難排解  
 降低訊息在 mesh 內傳送的速率。  
  
## <a name="see-also"></a>請參閱

- [追蹤](index.md)
- [使用追蹤來疑難排解應用程式](using-tracing-to-troubleshoot-your-application.md)
- [系統管理與診斷](../index.md)
