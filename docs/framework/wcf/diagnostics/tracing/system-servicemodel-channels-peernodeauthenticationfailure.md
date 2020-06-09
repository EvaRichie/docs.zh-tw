---
title: System.ServiceModel.Channels.PeerNodeAuthenticationFailure
ms.date: 03/30/2017
ms.assetid: 0b50f782-ca06-4a82-aa7f-71f78ddc5177
ms.openlocfilehash: cb7019f1e4b47bde7c98b0109afa7b0125b7ef63
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84577301"
---
# <a name="systemservicemodelchannelspeernodeauthenticationfailure"></a>System.ServiceModel.Channels.PeerNodeAuthenticationFailure
與未來芳鄰的安全性交換失敗。  
  
## <a name="description"></a>描述  
 在嘗試建立安全的芳鄰連線時，發生這個追蹤。 這可能是因為認證不足或不正確而導致。  
  
 PeerChannel 會辨認嚴密識別 (X.509 憑證) 的單一權杖類型，它會根據能夠實作的驗證與授權類型，提供嚴密的識別模型。 PeerChannel 也會透過使用密碼的方式提供簡單應用程式的支援。 密碼只能用來允許進入工作階段；而不能用來執行訊息驗證。 這是因為對等群組共享的對稱式權杖，如果使用在來源驗證方面會發生困難而且不適當。  
  
## <a name="troubleshooting"></a>疑難排解  
 請確認所有芳鄰都有適當的安全性認證。  
  
## <a name="see-also"></a>請參閱

- [對等通道安全性](../../feature-details/peer-channel-security.md)
- [追蹤](index.md)
- [使用追蹤來疑難排解應用程式](using-tracing-to-troubleshoot-your-application.md)
- [系統管理與診斷](../index.md)
