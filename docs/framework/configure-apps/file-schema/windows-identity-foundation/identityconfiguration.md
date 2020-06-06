---
title: <identityConfiguration>
ms.date: 03/30/2017
ms.assetid: 1db76253-07da-447b-9e7a-3705c7228cf4
author: BrucePerlerMS
ms.openlocfilehash: 0fa8c574fd5663606cf081f1000a24884306edfe
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70251987"
---
# \<identityConfiguration>

指定服務層級的身分識別設定。

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel>**](system-identitymodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<identityConfiguration>**  

## <a name="syntax"></a>語法

```xml
<system.identityModel>
  <identityConfiguration
      name=xs:string
      saveBootstrapContext=xs:boolean>
      maximumClockSkew=TimeSpan >
  </identityConfiguration>
</system.identityModel>
```

## <a name="attributes-and-elements"></a>屬性和項目

下列章節說明屬性、子元素和父元素。

### <a name="attributes"></a>屬性

|屬性|描述|
|---------------|-----------------|
|NAME|身分識別設定區段的名稱。 您可以使用這個名稱來參考特定的設定區段。 如果未 `name` 指定任何屬性，區段會定義預設設定。 預設設定一律用於被動同盟案例。 如需詳細資訊，請參閱 [\<federationConfiguration>](federationconfiguration.md) 元素。|
|saveBootstrapCoNtext|指定啟動程式權杖是否應包含在會話權杖中。 您也可以藉由設定元素上的屬性，在權杖處理常式集合上設定此值 `saveBootstrapContext` [\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md) 。 在權杖處理常式集合上設定的值會覆寫服務上設定的值。|
|maximumClockSkew|<xref:System.TimeSpan>，指定允許的最大時鐘誤差。 控制執行時間緊迫作業時允許的時鐘誤差上限，例如驗證登入會話的到期時間。 預設值為5分鐘，"00:05:00"。 如需如何指定值的詳細資訊 <xref:System.TimeSpan> ，請參閱[Timespan 值](../windows-workflow-foundation/index.md)。 您也可以透過在專案上設定屬性，在權杖處理常式集合上設定最大時鐘誤差 `maximumClockSkew` [\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md) 。 在權杖處理常式集合上設定的值會覆寫服務上設定的值。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[\<caches>](caches.md)|註冊用於會話權杖和權杖重新執行偵測的快取。 可以在服務層級或安全性權杖處理常式集合中指定。 選擇性。|
|[\<certificateValidation>](certificatevalidation.md)|控制權杖處理常式用來驗證憑證的設定。 可以在服務層級或安全性權杖處理常式集合中指定。 選擇性。|
|[\<claimsAuthenticationManager>](claimsauthenticationmanager.md)|為傳入宣告註冊宣告驗證管理員。 選擇性。|
|[\<claimsAuthorizationManager>](claimsauthorizationmanager.md)|為傳入宣告註冊宣告授權管理員。 選擇性。|
|[\<claimTypeRequired>](claimtyperequired.md)|指定傳入安全性權杖的必要宣告集合。 選擇性。|
|[\<securityTokenHandlers>](securitytokenhandlers.md)|指定安全性權杖處理常式的集合。 可以指定零個或多個安全性權杖處理常式集合。 選擇性。|
|[\<tokenReplayDetection>](tokenreplaydetection.md)|啟用權杖重新執行偵測，並指定權杖的到期時間。 可以在服務層級或安全性權杖處理常式集合中指定。 選擇性。|

### <a name="parent-elements"></a>父項目

|元素|描述|
|-------------|-----------------|
|[\<system.identityModel>](system-identitymodel.md)|提供在應用程式中啟用 Windows Identity Foundation （WIF）選項的設定。|

## <a name="remarks"></a>備註

可以定義多個身分識別設定，每個都有唯一的名稱。 其行為如下所示：

1. 如果未 `<identityConfiguration>` 指定任何元素，則為。 預設身分識別設定會在執行時間建立，並以預設值填入。

2. 如果 `<identityConfiguration>` 已指定單一元素，則為。 這是預設的身分識別設定。 無論是命名或未命名，都不重要。

3. 如果指定了多個元素，則 `<identityConfiguration>` 為。 未命名的元素會指定預設的身分識別設定。 建議您在指定多個元素時 `<identityConfiguration>` ，其中一個專案應該是未命名的。

> [!WARNING]
> 如果您指定多個 `<identityConfiguration>` 元素，其中一個專案應為未命名。 未命名的元素會是預設的身分識別設定。

 在專案中指定的部分設定 `<identityConfiguration>` 可以由安全性權杖處理常式集合上的設定或個別安全性權杖處理常式的設定覆寫。

> [!IMPORTANT]
> 當使用 <xref:System.IdentityModel.Services.ClaimsPrincipalPermission> 或 <xref:System.IdentityModel.Services.ClaimsPrincipalPermissionAttribute> 類別在您的程式碼中提供宣告型存取控制時，元素所參考的身分識別設定會設定 `<federationConfiguration>` 宣告授權管理員和原則，以用來進行授權決策。 這也適用于非被動 Web 案例的情況，例如 Windows Communication Foundation （WCF）應用程式或不是以 Web 為基礎的應用程式。 如果應用程式不是被動的 Web 應用程式，則會套用所 [\<claimsAuthorizationManager>](claimsauthorizationmanager.md) 參考身分識別設定的專案（及其子原則元素（如果有的話））。 其他所有設定都會被略過。 如需詳細資訊，請參閱 [\<federationConfiguration>](federationconfiguration.md) 元素。

`<identityConfiguration>`元素是由 <xref:System.IdentityModel.Configuration.IdentityConfigurationElement> 類別表示。 身分識別設定區段是由類別表示 <xref:System.IdentityModel.Configuration.IdentityConfiguration> 。

> [!IMPORTANT]
> 將下列專案指定為專案的子專案 `<identityConfiguration>` 已被取代，但仍支援此行為以提供回溯相容性。 這些元素應改為在專案底下指定 [\<securityTokenHandlerConfiguration>](securitytokenhandlerconfiguration.md) 。
>
> - [\<audienceUris>](audienceuris.md)
> - [\<issuerNameRegistry>](issuernameregistry.md)
> - [\<issuerTokenResolver>](issuertokenresolver.md)
> - [\<serviceTokenResolver>](servicetokenresolver.md)

## <a name="example"></a>範例

下列範例會建立名為 "alternateConfiguration" 的身分識別設定。 身分識別設定會指定預設值。

```xml
<system.identityModel>
    <identityConfiguration name="alternateConfiguration"/>
</system.identityModel>
```

## <a name="see-also"></a>另請參閱

- <xref:System.IdentityModel.Configuration.IdentityConfiguration>
- <xref:System.IdentityModel.Configuration.IdentityConfigurationElement>
