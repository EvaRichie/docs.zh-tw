---
title: <httpsTransport>
ms.date: 03/30/2017
ms.assetid: f6ed4bc0-7e38-4348-9259-30bf61eb9435
ms.openlocfilehash: 09b0b8500ca93649c814c00739210343bfe1424c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "73739019"
---
# \<httpsTransport>
指定 HTTP 傳輸，以傳輸自訂繫結的 SOAP 訊息。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<customBinding>**](custombinding.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<binding>**\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<httpsTransport>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<httpsTransport allowCookies="Boolean"
                authenticationScheme="Digest/Negotiate/Ntlm/Basic/Anonymous"
                bypassProxyOnLocal="Boolean"
                hostnameComparisonMode="StrongWildcard/Exact/WeakWildcard"
                manualAddressing="Boolean"
                maxBufferPoolSize="Integer"
                maxBufferSize="Integer"
                maxReceivedMessageSize="Integer"
                proxyAddress="Uri"
                proxyAuthenticationScheme="None/Digest/Negotiate/Ntlm/Basic/Anonymous"
                realm="String"
                requireClientCertificate="Boolean"
                transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"
                unsafeConnectionNtlmAuthentication="Boolean"
                useDefaultWebProxy="Boolean" />
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|allowCookies|布林值，指定用戶端是否接受 Cookie 並在未來要求時傳播 Cookie。 預設值為 `false`。<br /><br /> 當您與使用 Cookie 的 ASMX Web 服務互動時，可以使用這個屬性。 如此一來，從伺服器傳回的 Cookie 就一定會自動複製到該服務未來所有的用戶端要求。|  
|authenticationScheme|指定通訊協定，用於驗證由 HTTP 接聽程式處理的用戶端要求。 有效值如下：<br /><br /> -Digest：指定摘要式驗證。<br />-Negotiate：與用戶端協商以判斷驗證配置。 如果用戶端和伺服器都支援 Kerberos，就使用它，否則使用 NTLM。<br />-Ntlm：指定 NTLM 驗證。<br />-Basic：指定基本驗證。<br />-Anonymous：指定匿名驗證。<br /><br /> 預設值為 Anonymous。 此屬性的型別為 <xref:System.Net.AuthenticationSchemes>。 這個屬性只可以設定一次。|  
|bypassProxyOnLocal|布林值，指出本機位址是否略過 Proxy 伺服器。 預設值為 `false`。<br /><br /> 本機位址是位於本機 LAN 或內部網路上的位址。<br /><br /> 如果服務位址的開頭為，Windows Communication Foundation （WCF）一律會忽略 proxy `http://localhost` 。<br /><br /> 如果您希望用戶端在與相同電腦上的服務進行交談時通過 Proxy，應使用主機名稱而非 localhost。|  
|hostnameComparisonMode|指定用於剖析 URI 的 HTTP 主機名稱比較模式。 有效值為：<br /><br /> -StrongWildcard：（"+"）會比對指定之配置、埠和相對 URI 內容中的所有可能主機名稱。<br />-Exact：不含萬用字元<br />-WeakWildcard：（" \* "）會比對指定之配置、埠和相對 UIR 內容中未明確符合或透過強式萬用字元機制的所有可能主機名稱。<br /><br /> 預設為 StrongWildcard。 此屬性的型別為 `System.ServiceModel.HostnameComparison`。|  
|manualAddressing|布林值，讓使用者能夠控制訊息定址。 這個屬性通常用於路由器案例，其中應用程式會決定要將訊息傳送到其中一個目的端。<br /><br /> 設定為 `true` 時，通道會假設訊息已經定址，並且不會加入任何其他的資訊。 接著使用者可個別定址每一個訊息。<br /><br /> 設定為 `false` 時，預設的 Windows Communication Foundation (WCF) 定址機制會自動為所有訊息建立位址。<br /><br /> 預設值為 `false`。|  
|maxBufferPoolSize|正整數，指定緩衝集區的大小上限。 預設值為 524288。<br /><br /> WCF 有許多組件會使用緩衝區。 每次使用這些組件時建立並終結緩衝區是高度耗費資源的作業，回收緩衝區的記憶體也是如此。 有了緩衝集區，您就可以從集區取出緩衝區來使用，用完後再還給集區， 因此可以避免建立及終結緩衝區的負荷。|  
|maxBufferSize|正整數，指定緩衝區的大小上限。 預設為 524288。|  
|maxReceivedMessageSize|正整數，指定可接收的可允許訊息大小上限。 預設值為 65536。|  
|proxyAddress|指定 HTTP Proxy 位址的 URI。 如果 `useSystemWebProxy` 為 `true`，則這項設定必須為 `null`。 預設值為 `null`。|  
|proxyAuthenticationScheme|指定通訊協定，用於驗證由 HTTP Proxy 處理的用戶端要求。 有效值如下：<br /><br /> -None：不執行驗證。<br />-Digest：指定摘要式驗證。<br />-Negotiate：與用戶端協商以判斷驗證配置。 如果用戶端和伺服器都支援 Kerberos，就使用它，否則使用 NTLM。<br />-Ntlm：指定 NTLM 驗證。<br />-Basic：指定基本驗證。<br />-Anonymous：指定匿名驗證。<br /><br /> 預設值為 Anonymous。 此屬性的型別為 <xref:System.Net.AuthenticationSchemes>。 請注意， <xref:System.Net.AuthenticationSchemes.IntegratedWindowsAuthentication?displayProperty=nameWithType> 不受支援。|  
|realm|字串，指定在 Proxy/伺服器上使用的領域。 預設值是空字串。<br /><br /> 伺服器使用領域來分割受保護的資源。 每個分割都可以有自己的驗證配置和 (或) 授權資料庫。 領域只限於基本和摘要式驗證使用。 當用戶端成功驗證之後，驗證對指定領域中的所有資源都有效。 如需領域的詳細說明，請參閱[IETF 網站](https://www.ietf.org)的 RFC 2617。|  
|requireClientCertificate|布林值，指定伺服器是否需要用戶端提供用戶端憑證做為 HTTPS 信號交換的一部分。 預設值為 `false`。|  
|transferMode|指定訊息是否要經過緩衝處理或資料流處理，或為要求或回應。 有效值如下：<br /><br /> -已緩衝處理：要求和回應訊息會進行緩衝處理。<br />-資料流程：要求和回應訊息會進行資料流程處理。<br />-StreamedRequest：資料流程處理要求訊息，並緩衝處理回應訊息。<br />-StreamedResponse：已緩衝處理要求訊息，並將回應訊息串流處理。<br /><br /> 預設為 Buffered。 此屬性的型別為 <xref:System.ServiceModel.TransferMode>。|  
|unsafeConnectionNtlmAuthentication|布林值，指定是否已在伺服器啟用「不安全的連線共用」。 預設值為 `false`。 如果已啟用，NTLM 驗證會在各 TCP 連線上執行一次。|  
|useDefaultWebProxy|布林值，指定是否使用整部機器 Proxy 設定而非使用者特定設定。 預設值為 `true`。|  
  
### <a name="child-elements"></a>子元素  
 無。  
  
### <a name="parent-elements"></a>父項目  
  
|元素|描述|  
|-------------|-----------------|  
|[\<binding>](bindings.md)|定義自訂繫結的所有繫結功能。|  
  
## <a name="remarks"></a>備註  
 `httpsTransport` 項目是建立自訂繫結時的起點，此繫結會實作 HTTPS 傳輸通訊協定。 HTTPS 是用於安全互通性目的的主要傳輸。 Windows Communication Foundation （WCF）支援 HTTPS，以確保與其他 Web 服務堆疊之間的互通性。  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Configuration.HttpsTransportElement>
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [傳輸](../../../wcf/feature-details/transports.md)
- [選擇傳輸](../../../wcf/feature-details/choosing-a-transport.md)
- [繫結](../../../wcf/bindings.md)
- [擴充繫結](../../../wcf/extending/extending-bindings.md)
- [自訂繫結](../../../wcf/extending/custom-bindings.md)
- [\<customBinding>](custombinding.md)
