---
title: <message> 的 <netTcpBinding> 項目
ms.date: 03/30/2017
ms.assetid: 1d71edd9-c085-4c2e-b6d3-980c313366f9
ms.openlocfilehash: ab767a5a1179de81bf9a8adc61799ede2d915ac1
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204901"
---
# <a name="message-element-of-nettcpbinding"></a>\<message> 的 \<netTcpBinding> 項目

定義使用設定之端點的訊息層級安全性需求類型 [\<netTcpBinding>](nettcpbinding.md) 。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<netTcpBinding>**](nettcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-nettcpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<message>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<message algorithmSuite="System.Servicemodel.Security.SecurityAlgorithmsuite"
         clientCredentialType="None/Windows/UserName/Certificate/IssuedToken" />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`algorithmSuite`|設定訊息加密和金鑰包裝演算法。 這些演算法和金鑰大小是由 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 類別所決定。 這些演算法會對應到安全性原則語言 (WS-SecurityPolicy) 規格中所指定的演算法。<br /><br /> 下表顯示可能的值。 預設值是 `Basic256`。<br /><br /> 如果服務繫結指定的 `algorithmSuite` 值不等於預設值，且您是使用 Svcutil.exe 產生組態檔，則該檔案將無法正確產生，這時您就必須手動編輯組態檔，將此屬性設定為需要的值。|  
|`clientCredentialType`|指定當使用訊息安全性執行用戶端驗證時，要使用的認證類型。 下表顯示可能的值。 預設值是 `UserName`。 此屬性的型別為 <xref:System.ServiceModel.MessageCredentialType>。|  
  
## <a name="algorithmsuite-attribute"></a>algorithmSuite 屬性  
  
|值|描述|  
|-----------|-----------------|  
|Basic128|使用 Aes128 加密，Sha1 用於訊息摘要，Rsa-oaep-mgf1p 用於金鑰包裝。|  
|Basic192|使用 Aes192 加密，Sha1 用於訊息摘要，Rsa-oaep-mgf1p 用於金鑰包裝。|  
|Basic256|使用 Aes256 加密，Sha1 用於訊息摘要，Rsa-oaep-mgf1p 用於金鑰包裝。|  
|Basic256Rsa15|將 Aes256 用於訊息加密，Sha1 用於訊息摘要，Rsa15 用於金鑰包裝。|  
|Basic192Rsa15|將 Aes192 用於訊息加密，Sha1 用於訊息摘要，Rsa15 用於金鑰包裝。|  
|TripleDes|使用 TripleDes 加密，Sha1 用於訊息摘要，Rsa-oaep-mgf1p 用於金鑰包裝。|  
|Basic128Rsa15|將 Aes128 用於訊息加密，Sha1 用於訊息摘要，Rsa15 用於金鑰包裝。|  
|TripleDesRsa15|使用 TripleDes 加密，Sha1 用於訊息摘要，Rsa15 用於金鑰包裝。|  
|Basic128Sha256|將 Aes256 用於訊息加密，Sha256 用於訊息摘要，Rsa-oaep-mgf1p 用於金鑰包裝。|  
|Basic192Sha256|將 Aes192 用於訊息加密，Sha256 用於訊息摘要，Rsa-oaep-mgf1p 用於金鑰包裝。|  
|Basic256Sha256|將 Aes256 用於訊息加密，Sha256 用於訊息摘要，Rsa-oaep-mgf1p 用於金鑰包裝。|  
|TripleDesSha256|將 TripleDes 用於訊息加密，Sha256 用於訊息摘要，Rsa-oaep-mgf1p 用於金鑰包裝。|  
|Basic128Sha256Rsa15|將 Aes128 用於訊息加密，Sha256 用於訊息摘要，Rsa15 用於金鑰包裝。|  
|Basic192Sha256Rsa15|將 Aes192 用於訊息加密，Sha256 用於訊息摘要，Rsa15 用於金鑰包裝。|  
|Basic256Sha256Rsa15|將 Aes256 用於訊息加密，Sha256 用於訊息摘要，Rsa15 用於金鑰包裝。|  
|TripleDesSha256Rsa15|將 TripleDes 用於訊息加密，Sha256 用於訊息摘要，Rsa15 用於金鑰包裝。|  
  
## <a name="clientcredentialtype-attribute"></a>clientCredentialType 屬性  
  
|值|描述|  
|-----------|-----------------|  
|無|這會允許服務與匿名用戶端互動。 在服務上，這表示此服務不需要任何用戶端認證。 在用戶端上，這表示此用戶端不提供任何用戶端認證。|  
|Windows|允許 SOAP 交換在 Windows 認證的已驗證內容中。|  
|UserName|允許服務要求用戶端必須使用 UserName 認證進行驗證。 WCF 不支援使用密碼傳送密碼摘要或衍生金鑰，也不支援使用這類金鑰維持訊息安全。 因此，WCF 會在使用 UserName 認證時強制保護傳輸。 這個認證模式會產生可互通交換或是無法互通的交涉 (根據 `negotiateServiceCredential` 屬性)。|  
|憑證|允許服務要求用戶端使用憑證進行驗證。 如果使用訊息安全性模式且 `negotiateServiceCredential` 屬性設定為 `false`，則必須為用戶端提供服務憑證。|  
|IssuedToken|指定通常由安全性權杖服務 (STS) 所發出的自訂權杖。|  
  
### <a name="child-elements"></a>子元素  

 無  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<security>](security-of-nettcpbinding.md)|定義 <xref:System.ServiceModel.Configuration.NetTcpBindingElement> 的安全性功能。|  
  
## <a name="remarks"></a>備註  

 訊息會使用訊息層級安全性達成 SOAP 訊息的完整性與機密性，以及通訊對等兩端的交互驗證。 如果繫結上選取了這個安全性模式，通道堆疊會以訊息安全性繫結項目進行設定，且 SOAP 訊息的安全性會符合 WS-Security* 標準。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.MessageSecurityOverTcp>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement.Message%2A>
- <xref:System.ServiceModel.NetTcpSecurity.Message%2A>
- <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>
- [確保服務與用戶端的安全](../../../wcf/feature-details/securing-services-and-clients.md)
- [繫結](../../../wcf/bindings.md)
- [設定系統提供的繫結](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用繫結來設定服務和用戶端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
