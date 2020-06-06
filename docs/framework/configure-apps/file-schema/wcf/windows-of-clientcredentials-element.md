---
title: <windows> 項目的 <clientCredentials>
ms.date: 03/30/2017
ms.assetid: 793e41c2-31ea-4159-abbc-2123bf097233
ms.openlocfilehash: 61ca99213f0b83a5af5df0184a8c1de405366288
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399122"
---
# <a name="windows-of-clientcredentials-element"></a>\<windows> 項目的 \<clientCredentials>
指定要用於代表用戶端的 Windows 認證的設定。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<endpointBehaviors>**](endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-endpointbehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<clientCredentials>**](clientcredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<windows>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<windows allowedImpersonationLevel="Identification/Impersonation/Delegation/Anonymous/None"
         allowNtlm="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`allowedImpersonationLevel`|設定用戶端與伺服器通訊的模擬喜好設定。 用戶端選取的模擬模式不會在伺服器上強制使用。 有效值如下：<br /><br /> -識別：伺服器可以取得用戶端的身分識別和許可權，但無法模擬用戶端。<br />-模擬：伺服器可以在本機系統上模擬用戶端的安全性內容。<br />-委派：伺服器可以在遠端系統上模擬用戶端的安全性內容。<br />-Anonymous：伺服器無法模擬或識別用戶端。<br />-None：未指派模擬層級。<br /><br /> 預設為 Identification。 此屬性的型別為 <xref:System.Security.Principal.TokenImpersonationLevel>。|  
|`allowNtlm`|將這個屬性設定為 `true` 時，如果 Kerberos 無法使用，會允許驗證降級為 NTLM。<br /><br /> 將此屬性設定為， `false` 會使 Windows Communication Foundation （WCF）在使用 NTLM 時能夠盡力擲回例外狀況。 請注意，將此屬性設為 `false`，不一定能夠禁止 NTLM 認證透過網路傳送。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<clientCredentials>](clientcredentials.md)|指定用來對服務驗證用戶端的認證。|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.WindowsClientElement>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Configuration.ClientCredentialsElement.Windows%2A>
- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>
- <xref:System.ServiceModel.Security.WindowsClientCredential>
- [保護用戶端安全](../../../wcf/securing-clients.md)
- [Working with Certificates](../../../wcf/feature-details/working-with-certificates.md)
- [Securing Services and Clients](../../../wcf/feature-details/securing-services-and-clients.md)
