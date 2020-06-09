---
title: 端點位址
ms.date: 03/30/2017
helpviewer_keywords:
- addresses [WCF]
- Windows Communication Foundation [WCF], addresses
- WCF [WCF], addresses
ms.assetid: 13f269e3-ebb1-433c-86cf-54fbd866a627
ms.openlocfilehash: 71358ed1c16c3c9b490a41f74dd6319af8eb2e7b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593525"
---
# <a name="endpoint-addresses"></a>端點位址
每個端點都有與其相關聯的位址，以便用來找出並識別端點。 這個位址主要包含一個可指定端點位置的統一資源識別元 (URI)。 端點位址是由類別在 Windows Communication Foundation （WCF）程式設計模型中表示 <xref:System.ServiceModel.EndpointAddress> ，其中包含選擇性的屬性，可 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 讓與它交換訊息的其他端點驗證端點，以及一組選擇性 <xref:System.ServiceModel.EndpointAddress.Headers%2A> 屬性，以定義連接至服務所需的任何其他 SOAP 標頭。 選擇性標頭會提供額外與更詳細的定址資訊，以便識別端點或與服務端點互動。 端點位址會在網路上表示為 WS-Addressing 端點參考 (EPR)。  
  
## <a name="uri-structure-of-an-address"></a>位址的 URI 結構  
 大部分傳輸的位址 URI 具有四個部分。 例如，URI 的四個部分 `http://www.fabrikam.com:322/mathservice.svc/secureEndpoint` 可以詳細說明如下：  
  
- 會員`http:`
  
- 機器碼`www.fabrikam.com`  
  
- (選擇性) 連接埠：322  
  
- 路徑：/mathservice.svc/secureEndpoint  
  
## <a name="defining-an-address-for-a-service"></a>定義服務的位址  
 您可以強制使用程式碼，或是透過組態以宣告的形式來指定服務的端點位址。 在程式碼中定義端點通常不太實用，因為部署之服務的繫結和位址通常與開發服務時所使用的繫結和位址不同。 一般來說，透過組態來定義服務端點會比透過程式碼來得實際一些。 如果將繫結和定址資訊留在程式碼外面，就可以讓您變更這些資訊，而且不需要重新編譯或重新部署應用程式。  
  
### <a name="defining-an-address-in-configuration"></a>在組態中定義位址  
 若要在設定檔中定義端點，請使用 [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) 元素。 如需詳細資訊和範例，請參閱[指定端點位址](../specifying-an-endpoint-address.md)。  
  
### <a name="defining-an-address-in-code"></a>在程式碼中定義位址  
 您可以使用 <xref:System.ServiceModel.EndpointAddress> 類別，在程式碼中建立端點位址。 如需詳細資訊和範例，請參閱[指定端點位址](../specifying-an-endpoint-address.md)。  
  
### <a name="endpoints-in-wsdl"></a>WSDL 中的端點  
 您也可以在對應端點的 `wsdl:port` 項目中，透過 WSDL 將端點位址表示為 WS-Addressing EPR 項目。 EPR 包含端點的位址以及任何位址屬性。 如需詳細資訊和範例，請參閱[指定端點位址](../specifying-an-endpoint-address.md)。  
  
## <a name="multiple-iis-binding-support-in-net-framework-35"></a>.NET Framework 3.5 中的多個 IIS 系結支援  
 網際網路服務提供者通常會在相同的伺服器與網站上裝載許多應用程式，以增加網站密度並降低整體經營成本， 而這些應用程式通常會繫結至不同的基底位址。 網際網路資訊服務 (IIS) 網站可以包含多個應用程式， 網站中的應用程式則可以透過一或多個 IIS 繫結來存取。  
  
 IIS 繫結提供繫結通訊協定和繫結這兩項資訊。 繫結通訊協定會定義產生通訊的配置，而繫結資訊則是用來存取網站的資訊。  
  
 下列範例示範 IIS 繫結中可能存在的元件：  
  
- 繫結通訊協定：HTTP  
  
- 繫結資訊：IP 位址、連接埠、主機標頭  
  
 IIS 可以為每個網站指定多個繫結，讓每個配置都有多個基底位址。 在 .NET Framework 3.5 之前，WCF 不支援架構的多個位址，如果已指定，則會 <xref:System.ArgumentException> 在啟用期間擲回。  
  
 .NET Framework 3.5 可讓網際網路服務提供者在同一個網站上裝載多個應用程式，且具有相同配置的不同基底位址。  
  
 例如，網站可能包含下列基底位址：  
  
- `http://payroll.myorg.com/Service.svc`
  
- `http://shipping.myorg.com/Service.svc`
  
 使用 .NET Framework 3.5，您可以在設定檔案的 AppDomain 層級指定前置詞篩選準則。 您可以使用元素來執行此動作 [\<baseAddressPrefixFilters>](../../configure-apps/file-schema/wcf/baseaddressprefixfilters.md) ，其中包含前置詞的清單。 IIS 提供的傳入基底位址會依據選擇性的前置詞清單經過篩選。 根據預設，如果沒有指定前置詞，則所有位址都會通過。 如果指定前置詞，則只會產生相符的基底位址讓該配置通過。  
  
 下列示範使用前置詞篩選條件的組態程式碼。  
  
```xml  
<system.serviceModel>  
  <serviceHostingEnvironment>  
     <baseAddressPrefixFilters>  
        <add prefix="net.tcp://payroll.myorg.com:8000"/>  
        <add prefix="http://shipping.myorg.com:8000"/>  
    </baseAddressPrefixFilters>  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 在上述範例中， `net.tcp://payroll.myorg.com:8000` 和 `http://shipping.myorg.com:8000` 是唯一的基底位址，適用于透過傳遞的個別配置。  
  
 `baseAddressPrefixFilter` 不支援萬用字元。  
  
 IIS 提供的基底位址可能會有繫結程序至其他配置，但 `baseAddressPrefixFilters` 清單中不存在的位址， 而且這些位址尚未經過篩選。  
  
## <a name="multiple-iis-binding-support-in-net-framework-4-and-later"></a>.NET Framework 4 及更新版本中的多重 IIS 繫結支援  
 從 .NET 4 開始，您就可以將 <xref:System.ServiceModel.ServiceHostingEnvironment> 的 <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A> 設定設為 true，藉以啟用 IIS 的多重繫結支援，而不需要挑選單一基底位址。 這項支援僅限 HTTP 通訊協定配置。  
  
 以下是在上使用 multipleSiteBindingsEnabled 的設定程式碼範例 [\<serviceHostingEnvironment>](../../configure-apps/file-schema/wcf/servicehostingenvironment.md) 。  
  
```xml  
<system.serviceModel>  
  <serviceHostingEnvironment multipleSiteBindingsEnabled="true" >  
  </serviceHostingEnvironment>  
</system.serviceModel>  
```  
  
 使用這項設定來啟用多重網站繫結時，系統會針對 HTTP 和非 HTTP 通訊協定忽略任何 baseAddressPrefixFilters 設定。  
  
 如需詳細資訊和範例，請參閱[支援多個 IIS 網站](supporting-multiple-iis-site-bindings.md)系結和 <xref:System.ServiceModel.ServiceHostingEnvironment.MultipleSiteBindingsEnabled%2A> 。  
  
## <a name="extending-addressing-in-wcf-services"></a>擴充 WCF 服務中的定址  
 WCF 服務的預設定址模型會針對下列目的使用端點位址 URI：  
  
- 指定服務接聽位址，亦即端點接聽訊息時的位置。  
  
- 指定 SOAP 位址篩選條件，亦即端點需要它成為 SOAP 標頭的位址。  
  
 您可以針對每個用途個別指定所屬的值，充分延伸定址功能，應付各種實用情況：  
  
- SOAP 媒介：用戶端所傳送的訊息會周遊一或多個其他服務，這些服務則會在訊息抵達最後目的地之前處理訊息。 SOAP 媒介可以執行不同的工作，例如快取、傳送、負載平衡，或是針對訊息進行結構描述驗證。 將要抵達媒介的訊息傳送至個別實體位址 (`via`)，而不只是傳送要抵達最終目的地的邏輯位址 (`wsa:To`)，即可完成這種情況。  
  
- 端點的接聽位址是私用 URI，而且已設為不同於本身 `listenURI` 屬性的值。  
  
 `via` 指定的傳輸位址，是指訊息在前往由服務所在位置 `to` 參數指定的某個其他遠端位址途中，一開始要傳送到的位置。 在網際網路用途方面，`via` URI 大多與服務最終 <xref:System.ServiceModel.EndpointAddress.Uri%2A> 位址的 `to` 屬性相同。 當您必須手動執行路由傳送時，才需要區分這兩個位址。  
  
### <a name="addressing-headers"></a>定址標頭  
 端點除了可以由其基本 URI 定址之外，還可由一個或多個 SOAP 標頭定址。 有些情況適用這種方式，例如 SOAP 媒介，此時端點需要此端點的用戶端加入目標為媒介的 SOAP 標頭。  
  
 使用程式碼或組態這兩種方式的其中一種，您就可以定義自訂位址標頭：  
  
- 在程式碼中，可以使用 <xref:System.ServiceModel.Channels.AddressHeader> 類別來建立自訂位址標頭，然後用來建構 <xref:System.ServiceModel.EndpointAddress>。  
  
- 在 configuration 中， [\<headers>](../../configure-apps/file-schema/wcf/headers.md) 會將自訂指定為專案的子系 [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-of-client.md) 。  
  
 與程式碼相較之下，建議您使用組態，因為程式碼可讓您在部署後變更標頭。  
  
### <a name="custom-listening-addresses"></a>自訂接聽位址  
 您可以將接聽位址設為端點 URI 以外的值。 如果要公開的 SOAP 位址是屬於公用 SOAP 媒介的位址，而端點實際接聽的位址是私用網路位址，則這種方式就很實用。  
  
 您可以使用程式碼或組態來指定自訂接聽位址：  
  
- 在程式碼中，可以將 <xref:System.ServiceModel.Description.ClientViaBehavior> 類別新增至端點的行為集合中，以指定自訂接聽位址。  
  
- 在 [設定] 中，使用服務元素的屬性指定自訂接聽位址 `ListenUri` [\<endpoint>](../../configure-apps/file-schema/wcf/endpoint-element.md) 。  
  
### <a name="custom-soap-address-filter"></a>自訂 SOAP 位址篩選條件  
 <xref:System.ServiceModel.EndpointAddress.Uri%2A> 可以與任何 <xref:System.ServiceModel.EndpointAddress.Headers%2A> 屬性搭配使用，以定義端點的 SOAP 位址篩選條件 (<xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A>)。 根據預設，這項篩選條件會確認傳入訊息所包含的 `To` 訊息標頭符合端點 URI，而且所有必要的端點標頭都出現在訊息中。  
  
 在某些情況中，端點會接收抵達基礎傳輸的所有訊息，而不只有包含適當 `To` 標頭的訊息。 若要啟用這項功能，使用者可以使用 <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> 類別。  
  
## <a name="see-also"></a>請參閱

- [指定端點位址](../specifying-an-endpoint-address.md)
- [服務身分識別和驗證](service-identity-and-authentication.md)
