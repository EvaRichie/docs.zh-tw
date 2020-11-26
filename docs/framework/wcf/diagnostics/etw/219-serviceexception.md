---
title: 219 - ServiceException
ms.date: 03/30/2017
ms.assetid: 81e2efac-39aa-4ed2-85a9-97eb8793b844
ms.openlocfilehash: 832ced406b6079fad8f4b9bea512a6d390bdcc0f
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96241937"
---
# <a name="219---serviceexception"></a>219 - ServiceException

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|識別碼|219|  
|關鍵字|EndToEndMonitoring，HealthMonitoring，Troubleshooting，ServiceModel|  
|層級|錯誤|  
|通路|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>描述  

 當 WCF 服務遇到未處理的例外狀況時，就會發出此事件。 這包含啟動期間、訊息處理期間和使用者程式碼中的未處理例外狀況。  
  
## <a name="message"></a>訊息  

 訊息處理期間發生了未處理的例外狀況 (型別為 '%2')。 完整例外狀況 ToString: %1。  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|ExceptionToString|`xs:string`|在 CLR 例外狀況上呼叫 `ToString`() 的結果。|  
|ExceptionTypeName|`xs:string`|例外狀況型別的 CLR FullName。|  
|HostReference|`xs:string`|若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。 其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。 範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
