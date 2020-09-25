---
title: <netHttpsBinding>
ms.date: 03/30/2017
ms.assetid: ff122116-6042-4792-9f21-275b4f97a105
ms.openlocfilehash: f6eca792f9bae6712a327fbcb5bdf47be9699062
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91204589"
---
# \<netHttpsBinding>

代表 Windows Communication Foundation (WCF) 服務可用來設定和公開能夠透過 HTTPS 通訊之端點的系結。 與雙工合約搭配使用時，將會使用 Web 通訊端，否則使用 HTTPS。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<netHttpsBinding>**  

## <a name="syntax"></a>Syntax  
  
```xml  
<netHttpsBinding>
  <binding allowCookies="Boolean"
           bypassProxyOnLocal="Boolean"
           closeTimeout="TimeSpan"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           maxBufferPoolSize="Integer"
           maxBufferSize="Integer"
           maxReceivedMessageSize="Integer"
           messageEncoding="Binary/Text/Mtom"
           name="string"
           openTimeout="TimeSpan"
           proxyAddress="URI"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           textEncoding="UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
           useDefaultWebProxy="Boolean">
    <security mode="None/Transport/Message/TransportWithMessageCredential/TransportCredentialOnly">
      <transport clientCredentialType="None/Basic/Digest/Ntlm/Windows/Certificate"
                 proxyCredentialType="None/Basic/Digest/Ntlm/Windows"
                 realm="string" />
      <message algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
               clientCredentialType="UserName/Certificate" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</netHttpsBinding>
```  
  
## <a name="type"></a>類型  

 `Type`  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|`allowCookies`|布林值，表示用戶端是否接受 Cookie 並在未來要求時傳播 Cookie。 預設為 `false`。<br /><br /> 當您與使用 Cookie 的 ASMX Web 服務互動時，可以使用這個屬性。 如此一來，從伺服器傳回的 Cookie 就一定會自動複製到該服務未來所有的用戶端要求。|  
|`bypassProxyOnLocal`|布林值，指出本機位址是否略過 Proxy 伺服器。 預設值為 `false`。<br /><br /> 如果網際網路資源有本機位址，則此資源為本機資源。 本機位址是位於同一部電腦上的本機區域網路或內部網路，在語法上是因為缺少句點 (。 ) 與 Uri 和中的相同。 `http://webserver/` `http://localhost/`<br /><br /> 設定這個屬性可決定以 BasicHttpBinding 設定的端點在存取本機資源時，是否使用 Proxy 伺服器。 如果這個屬性為 `true`，則所有對本機網際網路資源的要求都不會使用 Proxy 伺服器。 當這個屬性設定為 `true` 時，如果想要讓用戶端在與相同電腦上的服務進行交談時通過 Proxy，請使用主機名稱 (而非 localhost)。<br /><br /> 當這個屬性設定為 `false` 時，則所有的網際網路要求都會通過 Proxy 伺服器。|  
|`closeTimeout`|<xref:System.TimeSpan> 值，指定提供用來讓關閉作業完成的時間間隔。 這個值應該大於或等於 <xref:System.TimeSpan.Zero>。 預設為 00:01:00。|  
|`hostNameComparisonMode`|指定用於剖析 URI 的 HTTP 主機名稱比較模式。 這個屬性的型別為 <xref:System.ServiceModel.HostNameComparisonMode>，表示比對 URI 時此主機名稱是否會用來取用服務。 預設值為 <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>，表示比對時忽略主機名稱。|  
|`maxBufferPoolSize`|整數值，指定配置供從通道接收訊息之訊息緩衝區管理員使用的最大記憶體量。 預設值為 524288 (0x80000) 位元組。<br /><br /> 緩衝區管理員會利用緩衝區集區，將使用緩衝區的成本降至最低。 當訊息從通道送出時，服務將需要緩衝區來處理訊息。 如果緩衝區集區中沒有足夠的記憶體可以處理訊息負載，緩衝區管理員就必須從 CLR 堆積配置額外的記憶體，進而增加記憶體回收負荷。 從 CLR 記憶體回收堆積所產生的大量配置表示緩衝區集區太小，而提高這個屬性指定的限制來提供較大的配置，便可改善效能。|  
|`maxBufferSize`|整數值，指定儲存訊息之緩衝區的大小上限 (以位元組為單位)。在為此繫結設定的端點處理訊息時，可以將訊息儲存在緩衝區中。 預設值為 65,536 位元組。|  
|`maxReceivedMessageSize`|正整數，定義在使用此繫結設定之通道上可以接收的訊息大小上限 (以位元組為單位，包括標頭)。 如果對收件者而言訊息太大，寄件者便會收到 SOAP 錯誤。 收件者會捨棄訊息，然後在追蹤記錄檔中建立此事件的項目。 預設值為 65,536 個位元組。|  
|`messageEncoding`|定義用來對 SOAP 訊息進行編碼的編碼器。 有效值如下：<br /><br /> -Text：使用文字訊息編碼器。<br />-Mtom：使用訊息傳輸組織機制 1.0 (MTOM) 編碼器。<br /><br /> 預設為 Text。 此屬性的型別為 <xref:System.ServiceModel.WSMessageEncoding>。|  
|`name`|包含繫結之組態名稱的字串。 這個值應該是唯一的，因為它會當做繫結的識別使用。 從 .NET Framework 4 開始，系結和行為不需要有名稱。 如需預設設定和無值系結和行為的詳細資訊，請參閱[簡化](../../../wcf/simplified-configuration.md)[的 WCF 服務設定和簡化的](../../../wcf/samples/simplified-configuration-for-wcf-services.md)設定。|  
|`openTimeout`|<xref:System.TimeSpan> 值，指定提供用來讓開啟作業完成的時間間隔。 這個值應該大於或等於 <xref:System.TimeSpan.Zero>。 預設為 00:01:00。|  
|`proxyAddress`|包含 HTTP Proxy 位址的 URI。 如果 `useSystemWebProxy` 設定為 `true`，則這個設定必須為 `null`。 預設值為 `null`。|  
|`receiveTimeout`|<xref:System.TimeSpan> 值，指定接收作業完成其作業之時間間隔。 這個值應該大於或等於 <xref:System.TimeSpan.Zero>。 預設為 00:10:00。|  
|`sendTimeout`|<xref:System.TimeSpan> 值，指定提供用來讓傳送作業完成的時間間隔。 這個值應該大於或等於 <xref:System.TimeSpan.Zero>。 預設為 00:01:00。|  
|`textEncoding`|設定要在繫結上發出訊息時使用的字元集編碼方式。 有效值如下：<br /><br /> -BigEndianUnicode： Unicode BigEndian 編碼。<br />-Unicode：16位編碼。<br />-UTF8：8位編碼<br /><br /> 預設值為 UTF8。 此屬性的型別為 <xref:System.Text.Encoding>。|  
|`transferMode`|有效的 <xref:System.ServiceModel.TransferMode> 值，指定進行要求或回應時，訊息是經過緩衝處理或資料流處理。|  
|`useDefaultWebProxy`|布林值，指定是否應使用系統自動設定的 HTTP Proxy (如果有的話)。 預設值為 `true`。|  
|||  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<security>](security-of-nethttpbinding.md)|定義繫結的安全性設定。 此項目的型別為 <xref:System.ServiceModel.Configuration.BasicHttpsSecurityElement>。 |  
|[\<readerQuotas>](/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|定義 SOAP 訊息複雜度的條件約束，而這些條件約束可由以此繫結所設定的端點處理。 此項目的型別為 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|這個項目會保存標準和自訂繫結的集合。|  
  
## <a name="remarks"></a>備註  

 NetHttpsBinding 使用 HTTPS 做為傳送訊息的傳輸。 與雙工合約搭配使用時，將會使用 Web 通訊端。  與要求-回覆合約搭配使用時，NetHttpsBinding 的行為就像具有二進位編碼器的 BasicHttpsBinding。  
  
 安全性預設是關閉的，但是可以將子專案的模式屬性設定為以外 [\<security>](security-of-basichttpbinding.md) 的值 `None` 。 根據預設，它使用「文字」訊息編碼和 UTF-8 文字編碼。  
  
## <a name="example"></a>範例  

 下列範例示範 <xref:System.ServiceModel.NetHttpBinding> 的使用方式，它利用第一代和第二代 Web 服務來提供 HTTPS 通訊和最大的互通性。 用戶端和服務的組態檔中會指定繫結。 繫結型別是使用 `binding` 項目的 `<endpoint>` 屬性所指定的。 如果您要設定基本繫結，並變更其部分設定，則必須定義繫結組態。 端點必須使用 `bindingConfiguration` 項目的 `<endpoint>` 屬性來按照名稱參考繫結組態，如下列服務的組態程式碼所示。  
  
```xml  
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="netHttpsBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>
  <bindings>
    <netHttpsBinding>
      <binding name="Binding1"
               hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxReceivedMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Binary"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true">
        <security mode="None" />
      </binding>
    </netHttpsBinding>
  </bindings>
</system.serviceModel>
```  
  
## <a name="example"></a>範例  

 從 .NET Framework 4 開始，系結和行為不需要有名稱。 您可以從端點位址中移除 bindingConfiguration，並從系結中移除名稱，以完成上述範例中的功能。  
  
```xml  
<system.serviceModel>
  <services>
    <service type="Microsoft.ServiceModel.Samples.CalculatorService"
             behaviorConfiguration="CalculatorServiceBehavior">
      <endpoint address=""
                binding="netHttpsBinding"
                contract="Microsoft.ServiceModel.Samples.ICalculator" />
    </service>
  </services>
  <bindings>
    <netHttpsBinding>
      <binding hostNameComparisonMode="StrongWildcard"
               receiveTimeout="00:10:00"
               sendTimeout="00:10:00"
               openTimeout="00:10:00"
               closeTimeout="00:10:00"
               maxReceivedMessageSize="65536"
               maxBufferSize="65536"
               maxBufferPoolSize="524288"
               transferMode="Buffered"
               messageEncoding="Binary"
               textEncoding="utf-8"
               bypassProxyOnLocal="false"
               useDefaultWebProxy="true">
        <security mode="None" />
      </binding>
    </netHttpsBinding>
  </bindings>
</system.serviceModel>
```  
  
 如需預設設定和無值系結和行為的詳細資訊，請參閱[簡化](../../../wcf/simplified-configuration.md)[的 WCF 服務設定和簡化的](../../../wcf/samples/simplified-configuration-for-wcf-services.md)設定。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Channels.Binding>
- <xref:System.ServiceModel.Channels.BindingElement>
- <xref:System.ServiceModel.BasicHttpBinding>
- <xref:System.ServiceModel.Configuration.BasicHttpBindingElement>
- [繫結](../../../wcf/bindings.md)
- [設定系統提供的繫結](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用繫結來設定服務和用戶端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
