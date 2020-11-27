---
title: MSMQ 整合傳輸
ms.date: 03/30/2017
ms.assetid: 2bf9893a-fbd1-41fc-b6de-a41a44279936
ms.openlocfilehash: 032b6886152fb73c382fed1572e8c184a822b44f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96248743"
---
# <a name="msmq-integration-transport"></a>MSMQ 整合傳輸

此主題會列出 MSMQ 整合傳輸產生的所有例外狀況。  
  
## <a name="exception-list"></a>例外狀況清單  
  
|資源程式碼|資源字串|  
|-------------------|---------------------|  
|MessageSizeMustBeInIntegerRange|此處理站會將訊息緩衝處理，因此訊息大小必須在整數值範圍內。|  
|MsmqByteArrayBodyExpected|指定的序列化格式與 MSMQ 訊息本文不相符。 無法傳送或接收訊息。 序列化格式 ByteArray 需要 MSMQ 訊息本文是 byte[] 型別。|  
|MsmqCannotDeserializeActiveXMessage|發生 ActiveX 序列化錯誤。 無法傳送或接收訊息。 指定的本文變數型別與實際 MSMQ 訊息本文不相符。|  
|MsmqCannotUseBodyTypeWithActiveXSerialization|訊息的屬性不相符。 無法傳送或接收訊息。 若使用 ActiveX 序列化格式，便不可指定 BodyType 訊息屬性。|  
|MsmqInvalidServiceOperationForMsmqIntegrationBinding|MsmqIntegrationBinding 驗證失敗。 無法啟動服務端點。 指定的繫結不支援指定合約中指定服務作業的方法簽章。 請更正服務作業，以使用 MsmqIntegrationBinding。|  
|MsmqInvalidTypeDeserialization|無法辨識序列化格式，因此 ActiveX 序列化失敗。 無法傳送或接收訊息。|  
|MsmqInvalidTypeSerialization|無法辨識變數類型。 ActiveX 序列化失敗。 無法傳送或接收訊息。 不支援指定的變數類型。|  
|MsmqStreamBodyExpected|序列化格式與本文內容不相符。 無法傳送或接收訊息。 只有型別資料流的本文才能使用資料流序列化模式傳送或接收。|
