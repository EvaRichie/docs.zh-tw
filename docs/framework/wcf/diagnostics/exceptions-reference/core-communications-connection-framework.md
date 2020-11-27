---
title: 核心通訊：連線架構
ms.date: 03/30/2017
ms.assetid: 61ee00e1-896d-47c8-942f-1db28ac89cdc
ms.openlocfilehash: bd90bf75370776382b584388330e59a0701ed772
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96277500"
---
# <a name="core-communications-connection-framework"></a>核心通訊：連線架構

本主題會列出 Windows Communication Foundation (WCF) 連接架構所產生的所有例外狀況。  
  
## <a name="exception-list"></a>例外狀況清單  
  
|資源程式碼|資源字串|  
|-------------------|---------------------|  
|CloseTimedOut|Close 方法在指定的時間之後逾時。 請增加傳遞至 Close 呼叫的逾時值，或是增加繫結上的 CloseTimeout 值。 分配給此作業的時間可能是較長逾時的一部分。|  
|ContentTypeMismatch|指定的內容型別已傳送至預期指定項目的服務。 用戶端與服務繫結可能不相符。|  
|DuplexChannelAbortedDuringOpen|指定項目的雙工通道在開啟過程中已被終止。|  
|FramingValueNotAvailable|無法存取值，因為尚未完全解碼。|  
|OperationAbortedDuringConnectionEstablishment|建立與指定項目的連線時作業終止。|  
|ReceiveTimedOut2|接收作業在指定的時間之後逾時。 分配給此作業的時間可能是較長逾時的一部分。|  
|SendCannotBeCalledAfterCloseOutputSession|呼叫 CloseOutputSession 之後，無法在通道上傳送訊息。|
