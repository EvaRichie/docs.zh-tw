---
title: WebContentTypeMapper 範例
ms.date: 03/30/2017
ms.assetid: a4fe59e7-44d8-43c6-a1f8-40c45223adca
ms.openlocfilehash: 550e763d30a7fa503f6500dcaa8f9b77ea499bca
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96283259"
---
# <a name="webcontenttypemapper-sample"></a>WebContentTypeMapper 範例

這個範例示範如何將新的內容型別對應至 Windows Communication Foundation (WCF) 訊息主體格式。  
  
 專案 <xref:System.ServiceModel.Description.WebHttpEndpoint> 會插入 Web 訊息編碼器，讓 WCF 可在相同的端點上接收 JSON、XML 或原始的二進位訊息。 此編碼器會藉由尋找要求的 HTTP 內容型別來判定訊息的本文格式。 這個範例會介紹 <xref:System.ServiceModel.Channels.WebContentTypeMapper> 類別，以允許使用者控制內容型別與本文格式之間的對應。  
  
 WCF 提供一組內容類型的預設對應。 例如，`application/json` 會對應至 JSON，而 `text/xml` 會對應至 XML。 未對應至 JSON 或 XML 的任何內容型別都會對應至原始二進位格式。  
  
 在某些案例中 (例如，Push-Style API)，服務開發人員不會控制由用戶端傳回的內容型別。 例如，用戶端可能會以 `text/javascript` 方式傳回 JSON，而不是以 `application/json` 方式。 在這種情況中，服務開發人員必須提供衍生自 <xref:System.ServiceModel.Channels.WebContentTypeMapper> 的型別來正確地處理指定的內容型別，如下列範例程式碼所示。  
  
```csharp  
public class JsonContentTypeMapper : WebContentTypeMapper  
{  
    public override WebContentFormat  
               GetMessageFormatForContentType(string contentType)  
    {  
        if (contentType == "text/javascript")  
        {  
            return WebContentFormat.Json;  
        }  
        else  
        {  
            return WebContentFormat.Default;  
        }  
    }  
}  
```  
  
 此型別必須覆寫 <xref:System.ServiceModel.Channels.WebContentTypeMapper.GetMessageFormatForContentType%28System.String%29> 方法。 此方法必須評估 `contentType` 引數，並傳回下列其中一個值：<xref:System.ServiceModel.Channels.WebContentFormat.Json>、<xref:System.ServiceModel.Channels.WebContentFormat.Xml>、<xref:System.ServiceModel.Channels.WebContentFormat.Raw> 或 <xref:System.ServiceModel.Channels.WebContentFormat.Default>。 傳回的 <xref:System.ServiceModel.Channels.WebContentFormat.Default> 會延後至預設的 Web 訊息編碼器對應。 在先前的範例程式碼中，`text/javascript` 內容型別會對應至 JSON，而所有其他對應都維持不變。  
  
 若要使用 `JsonContentTypeMapper` 類別，請在 Web.config 中使用以下內容：  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <standardEndpoint name="" contentTypeMapper="Microsoft.Samples.WebContentTypeMapper.JsonContentTypeMapper, JsonContentTypeMapper, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 若要確認使用 JsonContentTypeMapper 的需求，從以上的組態檔中移除 contentTypeMapper 屬性。 嘗試使用 `text/javascript` 傳送 JSON 內容時，無法載入用戶端頁面。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>若要安裝、建置及執行範例  
  
1. 確定您已 [針對 Windows Communication Foundation 範例執行一次性安裝程式](one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2. 如 [建立 Windows Communication Foundation 範例](building-the-samples.md)所述，建立方案 WebContentTypeMapperSample .sln。  
  
3. 流覽至 `http://localhost/ServiceModelSamples/JCTMClientPage.htm` (不會在瀏覽器中從專案目錄) 開啟 JCTMClientPage.htm。  
  
> [!IMPORTANT]
> 這些範例可能已安裝在您的電腦上。 請先檢查下列 (預設) 目錄，然後再繼續。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> 如果此目錄不存在，請移至 [Windows Communication Foundation (wcf) 並 Windows Workflow Foundation (適用于) 4 的 WF .NET Framework 範例](https://www.microsoft.com/download/details.aspx?id=21459) 下載所有 WINDOWS COMMUNICATION FOUNDATION 的 wcf (和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。 此範例位於下列目錄。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Ajax\WebContentTypeMapper`  
