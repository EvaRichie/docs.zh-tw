---
title: <authentication> 項目的 <serviceCertificate>
ms.date: 03/30/2017
ms.assetid: 733b67b4-08a1-4d25-9741-10046f9357ef
ms.openlocfilehash: c6f2578d85971740e5bd3d75151305a475187492
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91201586"
---
# <a name="authentication-of-servicecertificate-element"></a>\<authentication> 項目的 \<serviceCertificate>

指定用戶端 Proxy 用來驗證服務憑證的設定，而這份憑證是使用 SSL/TLS 交涉所取得。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCertificate>**](servicecertificate-of-clientcredentials-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<authentication>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<authentication customCertificateValidatorType="String"
                certificateValidationMode="None/PeerTrust/ChainTrust/PeerOrChainTrust/Custom"
                revocationMode="NoCheck/Online/Offline"
                trustedStoreLocation="LocalMachine/CurrentUser" />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列各節說明屬性、子元素和父元素  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|customCertificateValidatorType|字串。 用來驗證自訂型別的型別和組件。|  
|certificateValidationMode|指定用來驗證認證之三個模式的其中一個。 如果設定為 `Custom`，也必須提供 customCertificateValidator。 預設值為 `ChainTrust`。|  
|revocationMode|用於檢查撤銷憑證清單 (CRL) 的模式之一。 預設值為 `Online`。|  
|trustedStoreLocation|兩個系統存放位置的其中一個：`LocalMachine` 或 `CurrentUser`。 當與用戶端交涉服務憑證時，會使用這個值。 針對指定存放區位置中 **受信任的人** 存放區執行驗證。 預設值為 `CurrentUser`。|  
  
## <a name="customcertificatevalidator-attribute"></a>customCertificateValidator 屬性  
  
|值|描述|  
|-----------|-----------------|  
|String|指定型別名稱和組件以及用來尋找此型別的其他資料。|  
  
## <a name="certificatevalidationmode-attribute"></a>certificateValidationMode 屬性  
  
|值|描述|  
|-----------|-----------------|  
|列舉型別|下列其中一個值：None、PeerTrust、ChainTrust、PeerOrChainTrust、Custom。<br /><br /> 如需詳細資訊，請參閱 [使用憑證](../../../wcf/feature-details/working-with-certificates.md)。|  
  
## <a name="revocationmode-attribute"></a>revocationMode 屬性  
  
|值|描述|  
|-----------|-----------------|  
|列舉型別|下列其中一個值：NoCheck、Online、Offline。<br /><br /> 如需詳細資訊，請參閱 [使用憑證](../../../wcf/feature-details/working-with-certificates.md)。|  
  
## <a name="trustedstorelocation-attribute"></a>trustedStoreLocation 屬性  
  
|值|描述|  
|-----------|-----------------|  
|列舉型別|下列其中一個值：LocalMachine 或 CurrentUser。 預設值為 CurrentUser。 如果用戶端應用程式是在系統帳戶下執行，則憑證通常位於 LocalMachine 之下。 如果用戶端應用程式是在使用者帳戶下執行，則憑證通常位於 CurrentUser 中。|  
  
### <a name="child-elements"></a>子元素  

 無。  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<serviceCertificate>](servicecertificate-of-clientcredentials-element.md)|指定對用戶端驗證服務時所使用的憑證。|  
  
## <a name="remarks"></a>備註  

 這個組態項目的 `certificateValidationMode` 屬性會指定用來驗證憑證的信任層級。 根據預設，層級會設為 `ChainTrust`，指定每一個憑證必須出現在鏈結頂端以受信任的憑證授權單位為結尾的憑證階層中。 這是最安全的模式。 您也可以將值設定為 `PeerOrChainTrust`，指定可接受自行發出的憑證 (對等信任)，以及信任鏈結內的憑證。 這個值會在開發及偵錯用戶端和服務時使用，因為自行發出的憑證不需要從受信任的授權單位購買。 部署用戶端時，請改用 `ChainTrust` 值。 您也可以將值設為 `Custom` 或 `None`。 若要使用 `Custom` 值，您必須同時將 `customCertificateValidator` 屬性 (Attribute) 設為可用來驗證憑證的組件與型別。 若要建立自己的自訂驗證程式，您必須繼承自抽象 X509CertificateValidator 類別。 如需詳細資訊，請參閱 [如何：建立採用自訂憑證驗證程式的服務](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)。  
  
 `revocationMode` 屬性會指定檢查憑證是否已被撤銷的方法。 預設為 `online`，表示會自動檢查該憑證是否已被撤銷。 如需詳細資訊，請參閱 [使用憑證](../../../wcf/feature-details/working-with-certificates.md)。  
  
## <a name="example"></a>範例  

 下列範例會執行兩個工作。 它會先指定用戶端的服務憑證，以便在與其功能變數名稱透過 HTTP 通訊協定進行通訊的端點進行通訊時使用 `www.contoso.com` 。 第二，指定驗證時使用的撤銷模式和存放區位置。  
  
```xml  
<serviceCertificate>
  <defaultCertificate findValue="www.contoso.com"
                      storeLocation="LocalMachine"
                      storeName="TrustedPeople"
                      x509FindType="FindByIssuerDistinguishedName" />
  <scopedCertificates>
     <add targetUri="http://www.contoso.com"
          findValue="www.contoso.com"
          storeLocation="LocalMachine"
          storeName="Root"
          x509FindType="FindByIssuerName" />
  </scopedCertificates>
  <authentication revocationMode="Online"
                  trustedStoreLocation="LocalMachine" />
</serviceCertificate>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.Authentication%2A>
- <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>
- [安全性行為](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [使用憑證](../../../wcf/feature-details/working-with-certificates.md)
- [作法：建立使用自訂憑證驗證程式的服務](../../../wcf/extending/how-to-create-a-service-that-employs-a-custom-certificate-validator.md)
- [\<authentication>](authentication-of-clientcertificate-element.md)
- [確保用戶端的安全](../../../wcf/securing-clients.md)
- [確保服務與用戶端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
