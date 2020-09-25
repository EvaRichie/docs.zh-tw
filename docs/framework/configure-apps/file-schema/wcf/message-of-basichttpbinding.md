---
title: <message> 的 <basicHttpBinding>
ms.date: 03/30/2017
ms.assetid: 51cdd329-6461-471a-8747-56c2299b61e5
ms.openlocfilehash: 8b1e889efc53d0132368111037399ea8872008b1
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204862"
---
# <a name="message-of-basichttpbinding"></a>\<message> 的 \<basicHttpBinding>

定義訊息層級安全性的設定 [\<basicHttpBinding>](basichttpbinding.md) 。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<basicHttpBinding>**](basichttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-basichttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<message>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
         clientCredentialType="UserName/Certificate" />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列各節說明屬性、子元素和父元素  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|algorithmSuite|設定訊息加密和金鑰包裝演算法。 此屬性的型別為 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>，它會指定演算法和金鑰大小。 這些演算法會對應到安全性原則語言 (WS-SecurityPolicy) 規格中所指定的演算法。<br /><br /> 預設值是 `Basic256`。|  
|clientCredentialType|指定當使用訊息安全性執行用戶端驗證時，要使用的認證類型。 預設值為 `UserName`。|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 屬性  
  
|值|描述|  
|-----------|-----------------|  
|UserName|-要求用戶端使用使用者名稱認證向伺服器進行驗證。 您必須使用來指定此認證 [\<clientCredentials>](clientcredentials.md) 。<br />-WCF 不支援傳送密碼摘要或使用密碼衍生金鑰，並使用這類金鑰來進行訊息安全性。 因此，WCF 會在使用 UserName 認證時強制保護傳輸。 對於 `basicHttpBinding`，這需要設定 SSL 通道。|  
|憑證|需要使用憑證對伺服器驗證用戶端。 在此情況下，必須使用和來指定用戶端認證 [\<clientCredentials>](clientcredentials.md) [\<clientCertificate>](clientcertificate-of-servicecredentials.md) 。 此外，當使用訊息安全性模式時，必須提供服務憑證給用戶端。 此案例中的服務認證必須使用 <xref:System.ServiceModel.Description.ClientCredentials> 類別或行為專案加以指定 `ClientCredentials` ，並使用來指定服務憑證 [\<serviceCertificate>](servicecertificate-of-servicecredentials.md) 。|  
  
### <a name="child-elements"></a>子元素  

 無  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<security>](security-of-basichttpbinding.md)|定義的安全性功能 [\<basicHttpBinding>](basichttpbinding.md) 。|  
  
## <a name="example"></a>範例  

 這個範例會示範如何實作一個使用 basicHttpBinding 和訊息安全性的應用程式。 在下列服務組態範例中，端點定義會指定 basicHttpBinding，並參考名為 `Binding1` 的繫結組態。 服務對用戶端驗證它自己時所使用的憑證是在組態檔案 `behaviors` 區段中的 `serviceCredentials` 項目下設定。 用戶端用來對服務驗證本身之憑證所套用的驗證模式，也是在 `behaviors` 項目下的 `clientCertificate` 區段中設定。  
  
 相同的繫結和安全性詳細資訊是在用戶端組態檔中設定。  
  
```xml  
<system.serviceModel>
  <services>
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <host>
        <baseAddresses>
          <add baseAddress="http://localhost:8000/ServiceModelSamples/service" />
        </baseAddresses>
      </host>
      <!-- this endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service -->
      <endpoint address=""
                binding="basicHttpBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
      <!-- the mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex -->
      <endpoint address="mex"
                binding="mexHttpBinding"
                contract="IMetadataExchange" />
    </service>
  </services>
  <bindings>
    <basicHttpBinding>
    <!-- This configuration defines the SecurityMode as Message and
         the clientCredentialType as Certificate. -->
      <binding name="Binding1">
        <security mode = "Message">
          <message clientCredentialType="Certificate" />
        </security>
      </binding>
    </basicHttpBinding>
  </bindings>
  <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
  <behaviors>
    <serviceBehaviors>
      <behavior name="CalculatorServiceBehavior">
        <serviceMetadata httpGetEnabled="True" />
        <serviceDebug includeExceptionDetailInFaults="False" />
        <!-- The serviceCredentials behavior allows one to define a service certificate.
             A service certificate is used by a client to authenticate the service and provide message protection.
             This configuration references the "localhost" certificate installed during the setup instructions. -->
        <serviceCredentials>
          <serviceCertificate findValue="localhost"
                              storeLocation="LocalMachine"
                              storeName="My"
                              x509FindType="FindBySubjectName" />
          <clientCertificate>
            <!-- Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate
               is in the user's Trusted People store, then it will be trusted without performing a
               validation of the certificate's issuer chain. This setting is used here for convenience so that the
               sample can be run without having to have certificates issued by a certification authority (CA).
               This setting is less secure than the default, ChainTrust. The security implications of this
               setting should be carefully considered before using PeerOrChainTrust in production code. -->
            <authentication certificateValidationMode="PeerOrChainTrust" />
          </clientCertificate>
        </serviceCredentials>
      </behavior>
    </serviceBehaviors>
  </behaviors>
</system.serviceModel>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.BasicHttpMessageSecurity>
- <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Message%2A>
- <xref:System.ServiceModel.BasicHttpSecurity.Message%2A>
- <xref:System.ServiceModel.Configuration.BasicHttpMessageSecurityElement>
- [確保服務與用戶端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
- [繫結](../../../wcf/bindings.md)
- [設定系統提供的繫結](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用繫結來設定服務和用戶端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
