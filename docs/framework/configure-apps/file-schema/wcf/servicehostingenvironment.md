---
title: <serviceHostingEnvironment>
ms.date: 03/30/2017
ms.assetid: 4f8a7c4f-e735-4987-979a-b74fcdae2652
ms.openlocfilehash: 5a7043064593fa329618510d15baeb87da432652
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91167091"
---
# \<serviceHostingEnvironment>

此項目定義服務裝載環境為特定傳輸產生的類型。 如果這個項目是空白的，便會使用預設的類型。 這個項目只能用於應用程式或電腦層級的組態檔。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<serviceHostingEnvironment>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<serviceHostingEnvironment aspNetCompatibilityEnabled="Boolean"
                           minFreeMemoryPercentageToActivateService="Integer"
                           multipleSiteBindingsEnabled="Boolean">
  <baseAddressPrefixFilters>
    <add prefix="string" />
  </baseAddressPrefixFilters>
  <serviceActivations>
    <add factory="String"
         service="String" />
  </serviceActivations>
  <transportConfigurationTypes>
    <add name="String"
         transportConfigurationType="String" />
  </transportConfigurationTypes>
</serviceHostingEnvironment>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|aspNetCompatibilityEnabled|布林值，指出是否已為目前的應用程式開啟 ASP.NET 相容性模式。 預設值為 `false`。<br /><br /> 當這個屬性設定為時 `true` ，Windows Communication Foundation (WCF) 服務的要求會流經 ASP.NET HTTP 管線，並禁止透過非 HTTP 通訊協定進行通訊。 如需詳細資訊，請參閱 [WCF 服務和 ASP.NET](../../../wcf/feature-details/wcf-services-and-aspnet.md)。|  
|minFreeMemoryPercentageToActivateService|整數，指定可在啟動 WCF 服務之前，可供系統使用的最小可用記憶體數量。 **注意：**  在 WCF 服務的 web.config 檔案中指定這個屬性以及部分信任，將會在 <xref:System.Security.SecurityException> 服務執行時產生。|  
|multipleSiteBindingsEnabled|布林值，這個值會指定是否啟用每個網站的多個 IIS 繫結。<br /><br /> IIS 包含網站，是包含虛擬目錄之虛擬應用程式的容器。 網站中的應用程式則可以透過一個或多個 IIS 繫結來存取。 IIS 繫結提供兩項資訊：繫結通訊協定和繫結資訊。 繫結通訊協定會定義產生通訊的配置，而繫結資訊則是用來存取網站的資訊。 繫結通訊協定的範例如 HTTP，其中繫結資訊可能會包含 IP 位址、連接埠、主機標題等。<br /><br /> IIS 支援為每個網站指定多個 IIS 繫結，讓每個配置能夠有多個基底位址。 不過，在網站下裝載的 Windows Communication Foundation (WCF) 服務，只允許每個配置系結至一個 baseAddress。<br /><br /> 若要針對 Windows Communication Foundation (WCF) 服務啟用每個網站的多個 IIS 系結，請將這個屬性設定為 `true` 。 請注意，僅有 HTTP 通訊協定支援多個網站繫結。 組態檔中的端點位址必須是完整的 URI。|  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<baseAddressPrefixFilters>](baseaddressprefixfilters.md)|組態項目的集合，這些項目會指定服務主機使用之基底位址的前置詞篩選條件。|  
|[\<serviceActivations>](serviceactivations.md)|描述啟動設定的組態區段。|  
|[\<transportConfigurationTypes>](transportconfigurationtypes.md)|組態項目的集合，這些項目會識別特定傳輸的類型。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|serviceModel|所有 Windows Communication Foundation (WCF) 組態項目的根項目。|  
  
## <a name="remarks"></a>備註  

 根據預設，WCF 服務會與 ASP.NET 在裝載的應用程式定義域 (AppDomain) 中並存執行。 即使 WCF 與 ASP.NET 可共存於相同的 AppDomain，但 WCF 要求依預設不會由 ASP.NET HTTP 管線處理。 因此，WCF 服務無法使用 ASP.NET 應用程式平台的某些元素， 其中包括  
  
- ASP.NET 檔案/URL 授權  
  
- ASP.NET 模擬  
  
- Cookie 架構工作階段狀態  
  
- HttpContext.Current  
  
- 透過自訂 HttpModule 的管線擴充性  
  
 如果您的 WCF 服務需要在 ASP.NET 內容中運作，而且只透過 HTTP 進行通訊，可使用 WCF 的 ASP.NET 相容性模式。 當 `aspNetCompatibilityEnabled` 屬性在應用程式層級設為 `true` 時，便會開啟這個模式。 服務實作必須使用 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 類別宣告其可在相容性模式執行。 啟用相容性模式時，  
  
- ASP.NET 檔案/URL 驗證會在 WCF 驗證前強制執行。 驗證決策是以要求的傳輸層級身分識別為基礎， 訊息層級的身分識別則會被忽略。  
  
- WCF 服務作業會開始在 ASP.NET 模擬內容中執行。 如果同時啟用特定服務的 ASP.NET 模擬與 WCF 模擬，則會使用 WCF 模擬內容。  
  
- HttpContext.Current 可從 WCF 服務程式碼使用，而且服務不可以公開非 HTTP 端點。  
  
- WCF 要求是由 ASP.NET 管線處理。 已設定為處理傳入要求的 HttpModules 也可以處理 WCF 要求， 其中可包含 ASP.NET 平台元件 (如 <xref:System.Web.SessionState.SessionStateModule>) 以及自訂的協力廠商模組。  
  
## <a name="example"></a>範例  

 下列程式碼範例會示範如何啟用 ASP 相容性模式。  
  
## <a name="code"></a>程式碼  
  
```xml  
<serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>
```  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>
- <xref:System.ServiceModel.ServiceHostingEnvironment>
- [Hosting](../../../wcf/feature-details/hosting.md)
- [WCF 服務與 ASP.NET](../../../wcf/feature-details/wcf-services-and-aspnet.md)
