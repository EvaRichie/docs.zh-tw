---
title: <serviceCertificate> 項目的 <clientCredentials>
ms.date: 03/30/2017
ms.assetid: e50c0ac5-f0df-4c90-b54b-fc602c1f84ea
ms.openlocfilehash: 4c7489a171bdd5cb4b747ca99f1b7ff6dd65517b
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399676"
---
# <a name="servicecertificate-of-clientcredentials-element"></a>\<serviceCertificate> 項目的 \<clientCredentials>
指定對用戶端驗證服務時所使用的憑證。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceCertificate>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<serviceCertificate />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
 無。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<defaultCertificate>](defaultcertificate-element.md)|指定服務或 STS 不透過交涉通訊協定提供憑證時要使用的 X.509 憑證。|  
|[\<scopedCertificates>](scopedcertificates-element.md)|表示特定服務 (範圍服務) 為驗證所提供之 X.509 憑證的集合。 這個集合通常用來指定聯合案例中安全性權杖服務的服務憑證。|  
|[\<authentication>](authentication-of-servicecertificate-element.md)|為用戶端使用的服務憑證指定驗證行為。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|指定用戶端用來對服務驗證本身的認證。|  
  
## <a name="remarks"></a>備註  
 這個組態項目會指定用戶端用來驗證憑證的設定，而這份憑證是由使用 SSL 驗證的服務所提供。 它另外包含的任何憑證，可讓已明確設定於用戶端上的服務在使用訊息安全性時用於加密傳給服務的訊息。  
  
 元素的屬性與的 `serviceCertificate` 屬性完全相同 [\<clientCertificate>](clientcertificate-of-clientcredentials-element.md) 。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.ServiceCertificate%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.ServiceCertificate%2A>
- <xref:System.ServiceModel.Configuration.X509RecipientCertificateClientElement>
- <xref:System.ServiceModel.Security.X509CertificateRecipientClientCredential>
- [安全性行為](../../../wcf/feature-details/security-behaviors-in-wcf.md)
- [保護用戶端安全](../../../wcf/securing-clients.md)
- [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md)
- [Securing Services and Clients](../../../wcf/feature-details/securing-services-and-clients.md)
