---
title: <peerAuthentication> 項目
ms.date: 03/30/2017
ms.assetid: 09a8a9ff-e395-42f6-8ceb-9d44bdc1cbe1
ms.openlocfilehash: 7e4f86c361dc3ade5dedf4017921516357bb9a58
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91181579"
---
# <a name="peerauthentication-element"></a>\<peerAuthentication> 項目

指定對等用戶端的驗證選項。  
  
 如需點對點程式設計的詳細資訊，請參閱 [對等網路](../../../wcf/feature-details/peer-to-peer-networking.md)。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<peer>**](peer-of-clientcredentials-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<peerAuthentication>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<peerAuthentication customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"
                    certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"
                    revocationMode="NoCheck/Online/Offline"
                    trustedStoreLocation="CurrentUser/LocalMachine" />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列各節說明屬性、子元素和父元素  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`customCertificateValidatorType`|選擇性字串。 用來驗證自訂型別的型別和組件。 當 `certificateValidationMode` 設定為 `Custom` 時，必須設定這個屬性。|  
|`certificateValidationMode`|選擇性列舉。 指定用來驗證認證之三個模式的其中一個。 如果設定為 `Custom`，也必須提供 `customCertificateValidator`。 預設為 `ChainTrust`。|  
|`revocationMode`|選擇性列舉。 用於檢查撤銷憑證清單 (CRL) 的模式之一。 預設值為 `Online`。|  
|`trustedStoreLocation`|選擇性列舉。 兩個系統存放位置的其中一個：`LocalMachine` 或 `CurrentUser`。 當與用戶端交涉服務憑證時，會使用這個值。 針對指定存放區位置中 **受信任的人** 存放區執行驗證。 預設值為 `CurrentUser`。|  
  
## <a name="customcertificatevalidatortype-attribute"></a>customCertificateValidatorType 屬性  
  
|值|描述|  
|-----------|-----------------|  
|String|指定型別名稱和組件以及用來尋找此型別的其他資料。 至少需要命名空間和型別名稱。 選擇性的資訊包括：組件名稱、版本號碼、文化特性和公開金鑰權杖。|  
  
## <a name="certificatevalidationmode-attribute"></a>certificateValidationMode 屬性  
  
|值|描述|  
|-----------|-----------------|  
|列舉型別|下列其中一個值：`None`、`PeerTrust`、`ChainTrust`、`PeerOrChainTrust`、`Custom`。 預設值為 `ChainTrust`。<br /><br /> 如需詳細資訊，請參閱 [使用憑證](../../../wcf/feature-details/working-with-certificates.md)。|  
  
## <a name="revocationmode-attribute"></a>revocationMode 屬性  
  
|值|描述|  
|-----------|-----------------|  
|列舉型別|下列其中一個值：`NoCheck`、`Online`、`Offline`。 預設值為 `Online`。<br /><br /> 如需詳細資訊，請參閱 [使用憑證](../../../wcf/feature-details/working-with-certificates.md)。|  
  
## <a name="trustedstorelocation-attribute"></a>trustedStoreLocation 屬性  
  
|值|描述|  
|-----------|-----------------|  
|列舉型別|下列其中一個值：`LocalMachine` 或 `CurrentUser`。 預設值為 `CurrentUser`。 如果用戶端應用程式是在系統帳戶下執行，則憑證通常位於 `LocalMachine` 之下。 如果用戶端應用程式是在使用者帳戶下執行，則憑證通常位於 `CurrentUser`。|  
  
### <a name="child-elements"></a>子元素  

 無。  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<peer>](peer-of-clientcredentials-element.md)|指定向對等服務驗證用戶端時所使用的認證。|  
  
## <a name="remarks"></a>備註  

 `<authentication>` 項目對應至 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication> 類別。 這個項目會指定驗證程式，當網狀結構中進行鄰居對鄰居驗證時，就會叫用此驗證程式。 當新對等嘗試建立鄰居連線時，它會將自己的認證傳遞至對應的對等。 會叫用回應程式的驗證器來驗證遠端方的認證。 每次在網狀結構中建立對等連線時，對等的兩方會互相驗證，亦即會叫用兩端的驗證程式。  
  
## <a name="example"></a>範例  

 下列程式碼會將憑證驗證模式設定為 `PeerOrChainTrust`。  
  
```xml  
<behaviors>
  <endpointBehaviors>
    <behavior name="MyEndpointBehavior">
      <clientCredentials>
        <peer>
          <certificate findValue="www.contoso.com"
                       storeLocation="LocalMachine"
                       x509FindType="FindByIssuerName" />
          <peerAuthentication certificateValidationMode="PeerOrChainTrust" />
          <messageSenderAuthentication certificateValidationMode="None" />
        </peer>
      </clientCredentials>
    </behavior>
  </endpointBehaviors>
</behaviors>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.PeerCredentialElement>
- <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>
- <xref:System.ServiceModel.Security.PeerCredential.PeerAuthentication%2A>
- <xref:System.ServiceModel.Configuration.PeerCredentialElement.PeerAuthentication%2A>
- <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>
- [使用憑證](../../../wcf/feature-details/working-with-certificates.md)
- [對等網路](../../../wcf/feature-details/peer-to-peer-networking.md)
- [對等通道訊息驗證](/previous-versions/dotnet/netframework-3.5/aa967730(v=vs.90))
- [對等通道自訂驗證](/previous-versions/dotnet/netframework-3.5/ms751447(v=vs.90))
- [確保對等通道應用程式安全](../../../wcf/feature-details/securing-peer-channel-applications.md)
