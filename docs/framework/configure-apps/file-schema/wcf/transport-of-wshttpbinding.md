---
title: <transport> 的 <wsHttpBinding>
ms.date: 03/30/2017
ms.assetid: 21e38acf-450a-4bda-82b6-de305e1f7cd8
ms.openlocfilehash: 1afeed62fcbf3b083d69a7cedb7eb80b81f5c17b
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73732732"
---
# <a name="transport-of-wshttpbinding"></a>\<transport> 的 \<wsHttpBinding>

定義 HTTP 傳輸的驗證設定。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<wsHttpBinding>**](wshttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<security>**](security-of-wshttpbinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<transport>**  

## <a name="syntax"></a>語法

```xml
<wsHttpBinding>
  <binding>
    <security mode="None|Transport|TransportWithMessageCredential|TransportCredentialOnly">
      <transport clientCredentialType="Basic|Certificate|Digest|None|Ntlm|Windows"
                 proxyCredentialType="Basic|Digest|None|Ntlm|Windows"
                 realm="string" />
        <extendedProtectionPolicy policyEnforcement="Never|WhenSupported|Always"
                                  protectionScenario="TransportSelected|TrustedProxy">
          <customServiceNames>
          </customServiceNames>
        </extendedProtectionPolicy>
      </transport>
    </security>
  </binding>
</wsHttpBinding>
```

## <a name="type"></a>類型

<xref:System.ServiceModel.HttpTransportSecurity>

## <a name="attributes-and-elements"></a>屬性和項目

下列章節說明屬性、子元素和父元素。

### <a name="attributes"></a>屬性

|屬性|描述|
|---------------|-----------------|
|`clientCredentialType`|指定用來對服務驗證用戶端的認證。 此屬性的型別為 <xref:System.ServiceModel.HttpClientCredentialType>。|
|`proxyCredentialType`|指定用來對網域 Proxy 驗證用戶端的認證。 此屬性的型別為 <xref:System.ServiceModel.HttpProxyCredentialType>。|
|`realm`|指定摘要式驗證或基本驗證之驗證領域的字串。 預設值是空字串。<br /><br /> 驗證領域至少會指定負責執行驗證之主機的名稱， 也可以指定具有存取權之使用者的集合。 使用者可以查詢驗證領域，以確定可以使用的其中一組使用者名稱和密碼。|
|`policyEnforcement`|此列舉指定了應該強制執行 <xref:System.Security.Authentication.ExtendedProtection.ExtendedProtectionPolicy> 的時間。<br /><br /> 1. 永不–永遠不會強制執行原則（已停用 [擴充保護]）。<br />2. WhenSupported-只有在用戶端支援擴充保護時，才會強制執行原則。<br />3. always –一律強制執行原則。 不支援延伸保護的用戶端將無法驗證。|

## <a name="clientcredentialtype-attribute"></a>clientCredentialType 屬性

|值|描述|
|-----------|-----------------|
|`None`|停用安全性。|
|`Basic`|使用基本驗證。|
|`Digest`|使用摘要式驗證。|
|`Ntlm`|使用 NTLM 驗證做為 Windows 網域的後援。|
|`Windows`|使用整合式 Windows 驗證。|
|`Certificate`|使用 X.509 憑證來驗證用戶端。|

## <a name="proxycredentialtype-attribute"></a>proxyCredentialType 屬性

|值|描述|
|-----------|-----------------|
|`None`|停用安全性。|
|`Basic`|使用基本驗證。|
|`Digest`|使用摘要式驗證。|
|`Ntlm`|使用 NTLM 做為 Windows 網域的後援。|
|`Windows`|使用整合式 Windows 驗證。|
|`Certificate`|使用 X.509 憑證來驗證用戶端。|

### <a name="child-elements"></a>子元素

無。

### <a name="parent-elements"></a>父項目

|元素|描述|
|-------------|-----------------|
|[\<security>](security-of-wshttpbinding.md)|表示的安全性功能 [\<wsHttpBinding>](wshttpbinding.md) 。|

## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.HttpTransportSecurity>
- <xref:System.ServiceModel.WSHttpSecurity.Transport%2A>
- <xref:System.ServiceModel.Configuration.WSHttpSecurityElement.Transport%2A>
- <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>
- [Securing Services and Clients](../../../wcf/feature-details/securing-services-and-clients.md)
- [繫結](../../../wcf/bindings.md)
- [設定系統提供的繫結](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用繫結設定服務與用戶端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
