---
title: <userNameAuthentication>
ms.date: 03/30/2017
ms.assetid: 24d8b398-770f-418f-ba23-c4325419cfa6
ms.openlocfilehash: dc5c00a2204646863ae2570bb97b8d70e22a72d4
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70399193"
---
# \<userNameAuthentication>
根據使用者名稱和密碼來指定服務的認證。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<behaviors>**](behaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceBehaviors>**](servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<behavior>**](behavior-of-servicebehaviors.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<serviceCredentials>**](servicecredentials.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<userNameAuthentication>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<userNameAuthentication cacheLogonTokenLifetime="TimeSpan"
                        cacheLogonTokens="Boolean"
                        customUserNamePasswordValidatorType="String"
                        includeWindowsGroups="Boolean"
                        maxCacheLogonTokens="Integer"
                        membershipProviderName="String"
                        userNamePasswordValidationMode="Windows/MembershipProvider/Custom" />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`cacheLogonTokenLifetime`|<xref:System.TimeSpan>，指定快取權杖的最大時間長度。 預設為 00:15:00。|  
|`cacheLogonTokens`|布林值，指定是否要快取登入權杖。 預設值為 `false`。|  
|`customUserNamePasswordValidatorType`|字串，指定所使用的自訂使用者名稱密碼驗證程式的型別。 預設值是空字串。|  
|`includeWindowsGroups`|布林值，指定 Windows 群組是否包含在安全性內容中。 預設值為 `true`。<br /><br /> 將這個屬性設定為 `true` 會有效能方面的影響，因為它會造成完整的群組擴充。 如果您不需要建立使用者所屬之群組的清單，請將此屬性設定為 `false`。|  
|`maxCacheLogonTokens`|整數，指定快取登入權杖的數目上限。 這個值應大於零。 預設值為 128。|  
|`membershipProviderName`|當繫結的 `clientCredentialType` 屬性設為 `username` 時，使用者名稱會對應至 Windows 帳戶。 您可以使用這個屬性來覆寫這個行為，該屬性是一個字串，其中包含 <xref:System.Web.Security.MembershipProvider> 值的名稱，可提供相關的密碼驗證機制。|  
|`userNamePasswordValidationMode`|指定驗證使用者名稱密碼的方法。 有效值為：<br /><br /> -Windows<br />-MembershipProvider<br />-Custom<br /><br /> 預設為 Windows。 此屬性的型別為 <xref:System.ServiceModel.Security.UserNamePasswordValidationMode>。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<serviceCredentials>](servicecredentials.md)|指定要用於驗證 (Authenticate) 服務的認證，以及用戶端認證的驗證 (Validation) 相關設定。|  
  
## <a name="remarks"></a>備註  
 如果服務使用的繫結中沒有任何一個是針對使用者名稱/密碼驗證設定的，就會忽略這個項目的屬性。 其中包括 `customUserNamePasswordValidatorType`、`includeWindowsGroups`、`membershipProviderName` 和 `userNamePasswordValidationMode`。  
  
 如果服務使用的繫結中沒有任何一個是設定成針對使用者名稱/密碼使用 Windows 驗證，就會忽略與登錄權杖快取相關的設定。 其中包括 `cacheLogonTokenLifetime`、`cacheLogonTokens` 和 `maxCacheLogonTokens`。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.UserNameServiceElement>
- <xref:System.ServiceModel.Description.ServiceCredentials.UserNameAuthentication%2A>
- <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential>
- <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.UserNameAuthentication%2A>
