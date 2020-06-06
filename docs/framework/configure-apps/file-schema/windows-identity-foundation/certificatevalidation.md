---
title: <certificateValidation>
ms.date: 03/30/2017
ms.assetid: 6c54c704-b55e-4631-88ff-4d4a5621554c
author: BrucePerlerMS
ms.openlocfilehash: c2d1a5d36cb5616ef06eedc093dd70a68a164a81
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70252127"
---
# \<certificateValidation>
控制權杖處理常式用來驗證憑證的設定。 如果特定處理常式已設定自己的驗證器，則會覆寫這些設定。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<identityConfiguration>**](identityconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<certificateValidation>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<system.identityModel>  
  <identityConfiguration>  
    <certificateValidation  
      certificateValidationMode="None||ChainTrust||PeerTrust||PeerOrChainTrust||Custom"  
      revocationMode="NoCheck||Offline||Online"  
      trustedStoreLocation="CurrentLocation||LocalMachine" >  
    </certificateValidation>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|certificateValidationMode|<xref:System.ServiceModel.Security.X509CertificateValidationMode>值，指定要用於 x.509 憑證的驗證模式。 預設值為 "PeerOrChainTrust"。 若要指定自訂驗證程式，請將此屬性設定為 "Custom"，並使用元素來指定驗證程式 [\<certificateValidator>](certificatevalidator.md) 。 選擇性。|  
|revocationMode|<xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>值，指定要用於 x.509 憑證的撤銷模式。 預設值為 "Online"。 選擇性。|  
|trustedStoreLocation|<xref:System.Security.Cryptography.X509Certificates.StoreLocation>值，指定 x.509 憑證存放區。 預設值為 "LocalMachine"。 選擇性。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<certificateValidator>](certificatevalidator.md)|指定憑證驗證的自訂類型。 只有當 `certificateValidationMode` 元素的屬性 [\<certificateValidation>](certificatevalidation.md) 設定為 "Custom" 時，才會使用此類型。|  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<identityConfiguration>](identityconfiguration.md)|指定服務層級的身分識別設定。|  
|[\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md)|提供安全性權杖處理常式集合的設定。|  
  
## <a name="remarks"></a>備註  
 `<certificateValidation>`元素可以在專案下的服務層級或專案底下 `<identityConfiguration>` 的安全性權杖處理常式集合層級指定 `<securityTokenHandlerConfiguration>` 。 權杖處理常式集合上的設定會覆寫在服務上指定的值。 某些權杖處理常式可讓您在設定中指定憑證驗證設定。 個別權杖處理常式上的設定會覆寫在服務層級和安全性權杖處理常式集合中指定的值。  
  
## <a name="example"></a>範例  
  
```xml  
<certificateValidation certificateValidationMode="PeerOrChainTrust"  
                       revocationMode="Online"  
                       trustedStoreLocation="LocalMachine" />  
```
