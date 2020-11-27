---
title: 214 - OperationCompleted
ms.date: 03/30/2017
ms.assetid: a6287eef-023f-4816-813c-1802c82366df
ms.openlocfilehash: 6147c70448efb122cb43a2b42a1e9b59980fab29
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96278943"
---
# <a name="214---operationcompleted"></a>214 - OperationCompleted

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|識別碼|214|  
|關鍵字|HealthMonitoring，EndToEndMonitoring，Troubleshooting，ServiceModel|  
|層級|資訊|  
|通路|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>描述  

 此事件是在服務模型的預設 `OperationInvoker` 完成呼叫方法，且該方法未擲回例外狀況時發出。  
  
## <a name="message"></a>訊息  

 OperationInvoker 完成了對 '%1' 方法的呼叫。 此方法的呼叫持續時間為 '%2' 毫秒。  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|方法名稱|`xs:string`|`OperationInvoker` 叫用之方法的 CLR 名稱。|  
|持續時間|`xs:long`|`OperationInvoker` 叫用方法所花費的時間，以毫秒為單位。|  
|HostReference|`xs:string`|若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。 其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。 範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
