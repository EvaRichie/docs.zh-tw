---
title: <wsFederation>
ms.date: 03/30/2017
ms.assetid: c537f770-68bd-4f82-96ad-6424ad91369f
author: BrucePerlerMS
ms.openlocfilehash: 53f3943524c45a43ddb60553b8ff45f19df66b14
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "79152459"
---
# \<wsFederation>
提供 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> （WSFAM）的設定。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.identityModel.services>**](system-identitymodel-services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<federationConfiguration>**](federationconfiguration.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<wsFederation>**  
  
## <a name="syntax"></a>語法  
  
```xml
<system.identityModel.services>  
  <federationConfiguration>  
    <wsFederation authenticationType=xs:string (URI)  
                  freshness=xs:decimal  
                  homerealm=xs:string (URI)  
                  issuer=xs:string (URI)  
                  persistentCookiesOnPassiveRedirects=xs:boolean  
                  passiveRedirectEnabled=xs:boolean  
                  policy=xs:string (URI)  
                  realm=xs:string (URI)  
                  reply=xs:string (URI)  
                  request=xs:string (URI)  
                  requestPtr=xs:string (URI)  
                  requireHttps=xs:boolean  
                  resource=xs:string (URI)  
                  signInQueryString=xs:string  
                  signOutQueryString=xs:string  
                  signOutReply=xs:string (URL)  
    </wsFederation>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|authenticationType|指定驗證類型的 URI。 設定 WS-同盟登入要求 wauth 參數。 選擇性。 預設值為空字串，指定 wauth 參數不包含在要求中。|  
|常|所需的驗證要求最長使用期限，以分鐘為單位。 設定 WS-Federation 登入要求 wfresh 參數。 選擇性。 預設值為 0。 選擇性。 **警告：** 在下一版的 .NET Framework 4.5 中， `freshness` 屬性的類型會是 `xs:string` ，而其預設值將是 `null` 。|  
|homeRealm|要用於驗證的識別提供者（IdP）的主領域。 設定 WS-Federation 登入要求 whr 參數。 選擇性。 預設值為空字串，指定要求中未包含「瓦的」參數。|  
|簽發者|預定權杖簽發者的 URI。 設定 WS-同盟登入要求和登出要求的基底 URL。|  
|persistentCookiesOnPassiveRedirects|指定是否在驗證時發出持續性 cookie。 選擇性。 預設值為 "false"，不會發出 cookie。|  
|passiveRedirectEnabled|指定是否啟用 WSFAM，以將未經授權的要求自動重新導向至 STS。 選擇性。 預設值為 "true"，未授權的要求會自動重新導向。|  
|原則|URL，指定要用於登入要求的相關原則位置。 預設值是空字串。 設定 WS-Federation 登入要求 wp 參數。 選擇性。 預設值為空字串，指定 wp 參數不包含在要求中。|  
|realm|要求領域的 URI。 （識別 Security Token Service （STS）信賴憑證者（RP）的 URI。）設定要求 wtrealm WS-同盟登入要求參數。 必要。|  
|件|識別信賴憑證者 (RP) 應用程式要用來接收 Security Token Service (STS) 回覆之位址的 URL。 設定 WS-同盟登入要求 wreply 參數。 選擇性。 預設值為空字串，指定 wreply 參數不包含在要求中。|  
|要求|權杖發佈要求。 設定 WS-Federation 登入要求 wreq 參數。 選擇性。 預設值為空字串，指定 wreq 參數不包含在要求中。 不包含 wreq 或要求中的 wreqptr 參數表示 STS 知道要發出的權杖種類。|  
|requestPtr|URL，指定語彙基元發佈要求的位置。 設定要求 wreqptr 參數。 選擇性。 預設值為空字串，指定 wreqptr 參數不包含在要求中。 不包含 wreq 或要求中的 wreqptr 參數表示 STS 知道要發出的權杖種類。|  
|requireHttps|指定與 Security Token Service （STS）的通訊是否必須使用 HTTPS 通訊協定。 選擇性。 預設值為 "true"，必須使用 HTTPS。|  
|資源|用來向 Security Token Service (STS) 識別所存取之資源 (信賴憑證者 (RP)) 的 URI。 選擇性。 設定 WS-同盟登入要求 wres 參數。 選擇性。 預設值為空字串，指定 wres 參數不包含在要求中。 **注意：** wres 是舊版參數。 請指定 `realm` 要改用 wtrealm 參數的屬性。|  
|signInQueryString|提供擴充點，以在 WS-同盟登入要求 URL 中指定應用程式定義的查詢參數。 選擇性。 預設值為空字串，指定不應在要求中包含任何其他參數。 參數會使用下列格式指定為查詢字串片段： `"param1=value1&param2=value2&param3=value3"` 等等。 **注意：** 在設定檔中，查詢字串中的 ' & "字元必須使用其實體參考來指定 `&` 。|  
|signOutQueryString|提供擴充點，以在 WS-同盟登入要求 URL 中指定應用程式定義的查詢參數。 選擇性。 預設值為空字串，指定不應在要求中包含任何其他參數。 參數會使用下列格式指定為查詢字串片段： `"param1=value1&param2=value2&param3=value3"` 等等。 **注意：** 在設定檔中，查詢字串中的 ' & "字元必須使用其實體參考來指定 `&` 。|  
|signOutReply|指定在透過 WS-同盟通訊協定進行被動式登出期間，Security Token Service （STS）應將用戶端重新導向至的 URL。 在 WS-同盟登出要求上設定 wreply 參數。 選擇性。 預設值為空字串，指定不應在要求中包含任何其他參數。|  
  
### <a name="child-elements"></a>子元素  
 無  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<federationConfiguration>](federationconfiguration.md)|包含設定 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> （WSFAM）和 <xref:System.IdentityModel.Services.SessionAuthenticationModule> （SAM）的設定。|  
  
## <a name="remarks"></a>備註  
 您可以使用 `<wsFederation>` 元素來設定預設的 WS-同盟參數設定和 WSFAM 的預設行為。 在元素底下定義的 WS-同盟參數設定會 `<wsFederation>` 設定類別所公開的對等屬性 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 。 針對 WSFAM 所發出的每個要求，這些屬性會維持不變。 您可以為 WSFAM 所公開的事件新增事件處理常式，以動態方式在要求處理期間變更 WS-同盟參數;例如， <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider> 事件。 如需詳細資訊，請參閱類別的檔 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 。  
  
 `<wsFederation>`元素是由 <xref:System.IdentityModel.Services.Configuration.WSFederationElement> 類別表示。 設定物件本身是以 <xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration> 類別表示。 <xref:System.IdentityModel.Services.Configuration.WsFederationConfiguration>會在透過屬性存取的物件上設定單一實例 <xref:System.IdentityModel.Services.Configuration.FederationConfiguration> <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType> ，並提供 WSFAM 的設定。  
  
## <a name="example"></a>範例  
 下列 XML 顯示的 `<wsFederation>` 元素會指定 WSFAM 的設定。  
  
> [!WARNING]
> 在此範例中，不需要 WSFAM 就能使用 HTTPS。 這是因為 `requireHttps` `<wsFederation>` 已設定元素上的屬性 `false` 。 在大部分的生產環境中，不建議使用此設定，因為這可能會有安全性風險。  
  
```xml
<wsFederation passiveRedirectEnabled="true"
              issuer="http://localhost:15839/wsFederationSTS/Issue"
              realm="http://localhost:50969/"
              reply="http://localhost:50969/"
              requireHttps="false"
              signOutReply="http://localhost:50969/SignedOutPage.html"
              signOutQueryString="Param1=value2&Param2=value2"
              persistentCookiesOnPassiveRedirects="true" />
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>
- <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=nameWithType>
