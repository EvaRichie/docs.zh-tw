---
title: <transport> 的 <msmqIntegrationBinding>
ms.date: 03/30/2017
ms.assetid: 054579e3-7fdd-47df-99ca-952706ba5c8e
ms.openlocfilehash: 03e6236d1e89f16a460860f5dffff19b7bed8a0a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91169826"
---
# <a name="transport-of-msmqintegrationbinding"></a>\<transport> 的 \<msmqIntegrationBinding>

定義訊息佇列整合傳輸的安全性設定。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<msmqIntegrationBinding>**](msmqintegrationbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-msmqintegrationbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<transport>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<security>
  <transport msmqAuthenticationMode="None/WindowsDomain/Certificate"
             msmqEncryptionAlgorithm="RC4Stream/AES"
             msmqProtectionLevel="None/Sign/EncryptAndSign"
             msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />
</security>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列各節說明屬性、子元素和父元素  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`msmqAuthenticationMode`|指定 MSMQ 傳輸必須如何驗證訊息。 如果這設定為 `None`，則 `msmqProtectionLevel` 屬性的值也必須設定為 `None`。<br /><br /> 有效值如下：<br /><br /> -None：無驗證。<br />-WindowsDomain：驗證機制使用 Active Directory 取得與訊息相關聯之 SID 的 x.509 憑證。 接著這會用於檢查佇列的 ACL，以確保使用者具有寫入佇列的權限。<br />-Certificate：通道會從憑證存放區取得憑證。<br /><br /> 預設值為 WindowsDomain。 此屬性的型別為 <xref:System.ServiceModel.MsmqAuthenticationMode>。|  
|`msmqEncryptionAlgorithm`|指定演算法，該演算法用於在訊息佇列管理員之間傳輸訊息時，在線上加密訊息。 有效值如下：<br /><br /> -RC4Stream<br />-AES<br /><br /> 預設值為 RC4Stream。 此屬性的型別為 <xref:System.ServiceModel.MsmqEncryptionAlgorithm>。|  
|`msmqProtectionLevel`|指定在 MSMQ 傳輸層級上保護訊息的方式。 加密可確保訊息完整性，而 EncryptAndSign 可確保訊息完整性和不可否認性;也就是說，訊息確實來自寄件者，且寄件者就是他們說的人。<br /><br /> -有效的值包括下列各項：<br />-None：無保護。<br />-Sign：簽署訊息。<br />-EncryptAndSign：訊息會經過加密和簽署。<br /><br /> 預設值為 Sign。 此屬性的型別為 ProtectionLevel。|  
|`msmqSecureHashAlgorithm`|-指定在簽章中計算摘要時要使用的演算法。 有效值如下：<br />-MD5<br />-SHA1<br />-SHA256<br />-SHA512<br /><br /> 預設值為 SHA1。 此屬性的型別為 <xref:System.ServiceModel.MsmqSecureHashAlgorithm>。<br>由於 MD5 和 SHA1 的衝突問題，Microsoft 建議使用 SHA256 或更好的方式。|  
  
### <a name="child-elements"></a>子元素  

 無  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<security>](security-of-basichttpbinding.md)|定義 MSMQ 繫結的安全性設定。|  
  
## <a name="remarks"></a>備註  

 這個項目會封裝訊息佇列整合傳輸的安全性設定。 這些設定同時適用於訊息佇列整合和已佇列之傳輸。 它還可讓您設定驗證模式、加密演算法、安全雜湊演算法和保護層級。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>
- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.MsmqIntegrationSecurityElement.Transport%2A>
- <xref:System.ServiceModel.MsmqTransportSecurity>
- [確保服務與用戶端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
- [繫結](../../../wcf/bindings.md)
- [設定系統提供的繫結](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用繫結來設定服務和用戶端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
