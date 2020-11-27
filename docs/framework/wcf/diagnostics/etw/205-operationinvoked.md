---
title: 205 - OperationInvoked
ms.date: 03/30/2017
ms.assetid: 9c8d6c90-dfa5-4ae0-a589-96679a8fb3ba
ms.openlocfilehash: c36294a4a430c3e372e8213246e85dba45ce03c8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96286015"
---
# <a name="205---operationinvoked"></a>205 - OperationInvoked

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|識別碼|205|  
|關鍵字|Troubleshooting，ServiceModel|  
|層級|資訊|  
|通路|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>描述  

 此事件會在服務模型的預設 `OperationInvoker` 開始呼叫方法之前發出。  
  
## <a name="message"></a>訊息  

 OperationInvoker 已叫用 '%1' 方法。 呼叫端資訊: '%2'。  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|方法名稱|`xs:string`|`OperationInvoker` 叫用之方法的 CLR 名稱。|  
|呼叫端資訊|`xs:string`|用戶端的 IP 位址和連接埠號碼，格式為 'IPAddress:PortNumber'。 這兩個值都是從作業內容內的 'System.ServiceModel.Channels.RemoteEndpointMessageProperty' 訊息屬性擷取。 請注意，針對非 TCP 繫結，此值為 `null`。|  
|HostReference|`xs:string`|若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。 其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。 範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
