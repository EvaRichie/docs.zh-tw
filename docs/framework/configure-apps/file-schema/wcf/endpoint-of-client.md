---
title: <endpoint> 的 <client>
ms.date: 03/30/2017
ms.assetid: de6238ae-bbf8-48e9-a1b5-e24c0bea8afa
ms.openlocfilehash: 79d827691ec3898ad94af9835077c61ea35990ab
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91185843"
---
# <a name="endpoint-of-client"></a>\<endpoint> 的 \<client>

指定通道端點的合約、繫結和位址屬性，用戶端會使用該通道端點連線至伺服器上的服務端點。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<client>**](client.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<endpoint>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<endpoint address="String"
          behaviorConfiguration="String"
          binding="String"
          bindingConfiguration="String"
          contract="String"
          endpointConfiguration="String"
          kind="String"
          name="String">
</endpoint>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|address|必要的字串屬性。<br /><br /> 指定端點的位址。 預設為空字串。 位址必須是絕對 URI。|  
|behaviorConfiguration|字串，其中包含要用於產生端點之行為的行為名稱。 行為名稱必須在定義服務之處的範圍內。 預設為空字串。|  
|繫結|必要的字串屬性。<br /><br /> 字串，指出要使用的繫結型別。 此型別必須要有註冊的組態區段，才能加以參考。 型別是以區段名稱進行註冊，而非以繫結的型別名稱進行註冊。|  
|bindingConfiguration|選擇性。 字串，其中包含在產生端點時使用的繫結組態的名稱。 繫結組態必須在定義端點之處的範圍內。 預設值是空字串。<br /><br /> 這個屬性用於搭配 `binding` 使用，以參考組態檔中特定的繫結組態。 如果您要嘗試使用自訂繫結，請設定這個屬性。 否則，會擲回例外狀況。|  
|合約|必要的字串屬性。<br /><br /> 指示這個端點要公開 (Expose) 之合約的字串。 組件必須實作合約類型。|  
|endpointConfiguration|字串，這個字串會指定 `kind` 屬性所設定的標準端點名稱，該屬性會參考這個標準端點的其他組態資訊。 必須在 `<standardEndpoints>` 區段中定義相同的名稱。|  
|kind|字串，這個字串會指定所套用之標準端點的型別。 此型別必須在 `<extensions>` 區段或 machine.config 中註冊。如果未指定任何項目，則會建立一般通道端點。|  
|NAME|選擇性字串屬性。 這個屬性可唯一識別指定合約的端點。 您可以為指定的合約類型定義多個用戶端。 每個定義必須使用唯一組態名稱來區別。 如果省略這個屬性，就會使用對應端點做為與所指定合約類型相關聯的預設端點。 預設值是空字串。<br /><br /> 繫結的 `name` 屬性用於透過 WSDL 進行的定義匯出。|  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<headers>](headers.md)|位址標頭的集合。|  
|[\<identity>](identity.md)|身分識別，可讓其他端點與此端點交換訊息，以啟用端點的驗證。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<client>](client.md)|組態區段，它會定義用戶端可以連線的端點清單。|  
  
## <a name="example"></a>範例  

 這是通道端點組態的範例。  
  
```xml  
<endpoint address="/HelloWorld/"
          bindingConfiguration="usingDefaults"
          name="MyBinding"
          binding="customBinding"
          contract="HelloWorld">
</endpoint>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.ChannelEndpointElement>
- <xref:System.ServiceModel.Configuration.ClientSection>
- <xref:System.ServiceModel.Configuration.ChannelEndpointElementCollection>
- <xref:System.ServiceModel.Configuration.ClientSection.Endpoints%2A>
- <xref:System.ServiceModel.Configuration.ChannelEndpointElement>
- [WCF 用戶端組態](../../../wcf/feature-details/client-configuration.md)
- [用戶端](../../../wcf/feature-details/clients.md)
