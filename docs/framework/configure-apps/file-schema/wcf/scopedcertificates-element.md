---
title: <scopedCertificates> 項目
ms.date: 03/30/2017
ms.assetid: c7b6fc35-d4b2-4c18-98bd-83e09591f1d3
ms.openlocfilehash: 3c06159709df0afe2a475de1e186b0114af32bc2
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399960"
---
# <a name="scopedcertificates-element"></a>\<scopedCertificates> 項目
表示特定服務 (範圍服務) 為驗證所提供之 X.509 憑證的集合。 這個集合通常用來指定聯合案例中安全性權杖服務的服務憑證。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCertificate>**](servicecertificate-of-clientcredentials-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<scopedCertificates>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<scopedCertificates>
  <add findValue="String"
       storeLocation="CurrentUser/LocalMachine"
       storeName=" CurrentUser/LocalMachine"
       targetUri="string"
       x509Type="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier" />
</scopedCertificates>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
 無。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<add>](add-of-scopedcertificates-element.md)|將 X.509 憑證加入至範圍憑證的集合。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<serviceCertificate>](servicecertificate-of-servicecredentials.md)|指定對用戶端驗證服務時所使用的憑證。|  
  
## <a name="remarks"></a>備註  
 這個集合可讓用戶端根據與其進行通訊之服務的 URL 設定要使用的服務憑證。 在用戶端可以與多重服務 (終端服務以及中繼安全性權杖服務) 進行通訊的已核發權杖情況中，這個屬性特別有用。 對於使用以憑證為基礎之訊息安全性的繫結，這個憑證會用來加密傳送給服務的訊息，而且預期會被服務用來簽署對用戶端的回覆。  
  
 如果繫結需要服務的憑證，但是在 ScopedCertificates 中找不到服務 URL 的專屬憑證，則會使用預設的憑證。  
  
 如需詳細資訊，請參閱[如何：建立同盟用戶端](../../../wcf/feature-details/how-to-create-a-federated-client.md)的「限定範圍的憑證」一節。  
  
## <a name="example"></a>範例  
 下列範例會為用戶端指定服務憑證，以便在與其功能變數名稱是透過 HTTP 通訊協定的端點進行通訊時使用 `http://www.contoso.com` 。  
  
```xml  
<serviceCertificate>
  <scopedCertificates>
    <add targetUri="http://www.contoso.com"
         findValue="www.contoso.com"
         storeLocation="LocalMachine"
         storeName="Root"
         x509FindType="FindByIssuerName" />
  </scopedCertificates>
</serviceCertificate>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement.ScopedCertificates%2A>
- <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElementCollection>
- <xref:System.ServiceModel.Configuration.X509ScopedServiceCertificateElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential.ScopedCertificates%2A>
- [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md)
- [如何：建立同盟用戶端](../../../wcf/feature-details/how-to-create-a-federated-client.md)
- [\<add>](add-of-scopedcertificates-element.md)
- [保護用戶端安全](../../../wcf/securing-clients.md)
- [Securing Services and Clients](../../../wcf/feature-details/securing-services-and-clients.md)
