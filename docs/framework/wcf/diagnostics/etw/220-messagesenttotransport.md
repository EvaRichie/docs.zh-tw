---
title: 220 - MessageSentToTransport
ms.date: 03/30/2017
ms.assetid: aef4e781-240b-45bc-bff8-400053037e71
ms.openlocfilehash: 1b63877998ea7942886c83d8795fe5ee49fdf053
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96241924"
---
# <a name="220---messagesenttotransport"></a>220 - MessageSentToTransport

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|Id|220|  
|關鍵字|EndToEndMonitoring，Troubleshooting，ServiceModel|  
|層級|資訊|  
|通路|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>描述  

 服務模型將訊息傳送至傳輸時，便會發出此事件。  
  
> [!NOTE]
> 單向傳輸將不會發出此事件。  
  
## <a name="message"></a>訊息  

 發送器已傳送訊息到傳輸。 相互關聯 ID == '%1'。  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|相互關連識別碼|`xs:GUID`|活動識別碼，會將來自服務或用戶端的 `MessageSentToTransport` 事件，與另一端對應的 `MessageReceivedFromTransport` 相互關聯。|  
|HostReference|`xs:string`|若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。 其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。 範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
