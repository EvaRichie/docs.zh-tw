---
title: <behavior> 的 <endpointBehaviors>
ms.date: 03/30/2017
ms.assetid: b90ca3bc-3c22-4174-b903-e3a39898bd27
ms.openlocfilehash: d191b968e1c3fd1db0837ba7e03f210a1b00062d
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201495"
---
# <a name="behavior-of-endpointbehaviors"></a>\<behavior> 的 \<endpointBehaviors>

`behavior` 項目包含端點行為之設定的集合。 各個行為是依其 `name` 進行索引。 端點可透過這個名稱連結至每一個行為。 從 .NET Framework 4 開始，系結和行為不需要有名稱。 如需預設設定和無值系結和行為的詳細資訊，請參閱[簡化](../../../wcf/simplified-configuration.md)[的 WCF 服務設定和簡化的](../../../wcf/samples/simplified-configuration-for-wcf-services.md)設定。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<behavior>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.ServiceModel>
  <behaviors>
    <endpointBehaviors>
      <behavior name="String" />
    </endpointBehaviors>
  </behaviors>
</system.ServiceModel>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|NAME|唯一的字串，其中包含行為的組態名稱。 這個值是使用者定義的字串，它必須是唯一的，因為它會充當項目的識別字串。 從 .NET Framework 4 開始，系結和行為不需要有名稱。 如需預設設定和無值系結和行為的詳細資訊，請參閱[簡化](../../../wcf/simplified-configuration.md)[的 WCF 服務設定和簡化的](../../../wcf/samples/simplified-configuration-for-wcf-services.md)設定。|  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|指定用來對服務驗證用戶端的認證。|  
|[\<callbackDebug>](callbackdebug.md)|指定 Windows Communication Foundation (WCF) 回呼物件的服務偵錯工具。|  
|[\<callbackTimeouts>](callbacktimeouts.md)|指定用戶端回呼的逾時。|  
|[\<clientVia>](clientvia.md)|指定訊息應採用的路徑。|  
|[\<dataContractSerializer>](datacontractserializer.md)|包含 DataContractSerializer 的組態資料。|  
|[\<dispatcherSynchronization>](dispatchersynchronization.md)|指定可讓服務以非同步方式傳送回覆的端點行為。|  
|[\<enableWebScript>](enablewebscript.md)|可啟用端點行為，以取用 ASP.NET AJAX 網頁上的服務。 此行為只能與標準系結或繫結項目一起使用 \<webHttpBinding> \<webMessageEncoding> 。|  
|[\<endpointDiscovery>](endpointdiscovery.md)|指定端點的各種探索設定，例如其探索能力、範圍以及中繼資料的任何自訂延伸模組。|  
|[\<soapProcessing>](soapprocessing.md)|定義用戶端端點行為，這個行為會用來封送處理不同繫結型別和訊息版本之間的訊息。|  
|[\<synchronousReceive>](synchronousreceive-element.md)|指定在服務或用戶端應用程式中接收訊息的執行階段行為。 它沒有任何屬性或子項目。|  
|[\<transactedBatching>](transactedbatching.md)|指定是否支援接收作業的交易批次處理。|  
|[\<webHttp>](webhttp.md)|透過組態指定端點上的 WebHttpBehavior。 這種行為與標準系結搭配使用時 \<webHttpBinding> ，會啟用 WCF 服務的 Web 程式設計模型。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<endpointBehaviors>](endpointbehaviors.md)|端點行為項目的集合。|
