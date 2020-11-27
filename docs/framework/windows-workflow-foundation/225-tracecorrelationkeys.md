---
title: 225 - TraceCorrelationKeys
ms.date: 03/30/2017
ms.assetid: d9083aaf-3816-4c1c-bae0-2d7f49628345
ms.openlocfilehash: 04c5e0f4fbf3b95485e5bf4aae53aa2e4912d893
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96294491"
---
# <a name="225---tracecorrelationkeys"></a>225 - TraceCorrelationKeys

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|識別碼|225|  
|關鍵字|Troubleshooting，ServiceModel|  
|層級|資訊|  
|通路|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>描述  

 此事件是在內容架構相互關聯用於工作流程服務時發出。 其中包含套用的相互關聯索引鍵，可用來讓訊息與執行個體相互關聯。  
  
## <a name="message"></a>訊息  

 在父範圍 '%3' 中使用 '%2' 值計算的相互關聯索引鍵 '%1'。  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|執行個體索引鍵|`xs:GUID`|產生自相互關聯值的索引鍵。|  
|值|`xs:string`|用來計算相互關聯執行個體索引鍵的值。|  
|父範圍|`xs:string`||  
|HostReference|`xs:string`|若是 Web 裝載的服務，此欄位會唯一識別 Web 階層架構中的服務。 其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。 範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
