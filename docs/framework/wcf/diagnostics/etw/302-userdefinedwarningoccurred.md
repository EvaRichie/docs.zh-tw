---
title: 302 - UserDefinedWarningOccurred
ms.date: 03/30/2017
ms.assetid: 8d1f0bf1-0151-45e6-be92-573d397b54de
ms.openlocfilehash: b942b2e9716713371b8679fc9df9b9634dfc7283
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96243439"
---
# <a name="302---userdefinedwarningoccurred"></a>302 - UserDefinedWarningOccurred

## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|識別碼|302|  
|關鍵字|Troubleshooting，HealthMonitoring，UserEvents，ServiceModel，EndToEndMonitoring|  
|層級|警告|  
|通路|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>描述  

 此事件是由使用者程式碼所發出。 當開發人員的服務中發生自訂定義警告事件時，即可發出此事件。 這項操作可使用 <xref:System.Diagnostics.Eventing> API 達到目的。 另外還有 WCF 範例，可包裝該 API 並示範如何正確發出此事件。  
  
## <a name="message"></a>訊息  

 名稱:'%1'，參考:'%2'，承載:%3。  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|Name|`xs:string`|使用者定義的事件名稱。|  
|HostReference|`xs:string`|若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。 其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName '。 範例： ' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '。|  
|Payload|`xs:string`|使用者定義的事件裝載。|
