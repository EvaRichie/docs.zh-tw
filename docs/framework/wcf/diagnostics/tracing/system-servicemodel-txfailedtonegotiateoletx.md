---
title: System.ServiceModel.TxFailedToNegotiateOleTx
ms.date: 03/30/2017
ms.assetid: 3f0f0b4b-a1ad-4704-8329-455daf54892d
ms.openlocfilehash: 7b468a57409e9a473a5bbf8e3324435e65e8c60b
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96295310"
---
# <a name="systemservicemodeltxfailedtonegotiateoletx"></a>System.ServiceModel.TxFailedToNegotiateOleTx

OleTransactions 通訊協定無法完成指定的協調內容。  
  
## <a name="description"></a>描述  

 在有 OleTx 資訊的傳入交易無法使用附加的 OleTx 資訊，而且將改用 WS-AT 時追蹤。  
  
## <a name="troubleshooting"></a>疑難排解  

 代表機器之間的 MSDTC RPC 通訊有潛在的問題。 如果記錄中出現這些追蹤中的多數，可能導致效能大幅下降。  如果不需要 OleTx，在 WS-AT 登錄組態中將 `OleTxUpgradeEnabled` 設定為 0。  
  
## <a name="see-also"></a>另請參閱

- [追蹤](index.md)
- [使用追蹤來疑難排解應用程式](using-tracing-to-troubleshoot-your-application.md)
- [系統管理與診斷](../index.md)
