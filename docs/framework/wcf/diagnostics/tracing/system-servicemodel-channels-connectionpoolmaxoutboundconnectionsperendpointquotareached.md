---
title: Microsoft.Transactions.TransactionBridge.EnlistTransactionFailure
ms.date: 03/30/2017
ms.assetid: 1b9f5139-e122-4716-9ef7-2f38e1813993
ms.openlocfilehash: 3e4e1ff7ea8d8768c8d902dc09bd3b78646c2caf
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96256322"
---
# <a name="microsofttransactionstransactionbridgeenlisttransactionfailure"></a>Microsoft.Transactions.TransactionBridge.EnlistTransactionFailure

WS-AT 通訊協定服務無法使用所提供的協調內容登記交易。  
  
## <a name="description"></a>描述  

 當 MSDTC 無法登記指定之 2pc 通訊協定的異動時，便會進行追蹤。  這種情況可能因為交易不再存在、不再允許登記，或是已經存在太多登記而發生。  
  
## <a name="troubleshooting"></a>疑難排解  

 請檢查追蹤訊息內的狀態字串，以判斷是否有任何可執行動作的項目存在。  
  
## <a name="see-also"></a>另請參閱

- [追蹤](index.md)
- [使用追蹤來疑難排解應用程式](using-tracing-to-troubleshoot-your-application.md)
- [系統管理與診斷](../index.md)
