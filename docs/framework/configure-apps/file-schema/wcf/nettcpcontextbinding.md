---
title: <netTcpContextBinding>
ms.date: 03/30/2017
ms.assetid: 1d4715e1-5fff-4c3d-a226-18f21d0b30c4
ms.openlocfilehash: 88b3da6c81d771db255f6c0a4e86984c9ba294fe
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2020
ms.locfileid: "90546148"
---
# \<netTcpContextBinding>
指定 <xref:System.ServiceModel.NetTcpBinding> 的內容，它會要求保護層級為簽署。 NetTcpContextBinding 的 contextExchangeMechanism 為 SOAPHeader。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<bindings>**](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<netTcpContextBinding>**  
  
## <a name="syntax"></a>語法  
  
```xml  
<netTcpContextBinding>
  <binding closeTimeout="TimeSpan"
           contextProtectionLevel="EncryptAndSign/None/Sign"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           listenBacklog="Integer"
           maxBufferPoolSize="integer"
           maxBufferSize="Integer"
           maxConnections="Integer"
           maxReceivedMessageSize="Integer"
           name="string"
           openTimeout="TimeSpan"
           portSharingEnabled="Boolean"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           transactionFlow="Boolean"
           transactionProtocol="OleTransactions/WSAtomicTransactionOctober2004"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse">
    <reliableSession ordered="Boolean"
                     inactivityTimeout="TimeSpan"
                     enabled="Boolean" />
    <security mode="Message/None/Transport/TransportWithCredential">
      <transport clientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"
                 proxyCredentialType="Basic/Digest/None/Ntlm/Windows"
                 realm="String"
                 defaultClientCredentialType="Basic/Certificate/Digest/None/Ntlm/Windows"
                 defaultProxyCredentialType="Basic/Digest/None/Ntlm/Windows"
                 defaultRealm="String" />
      <message clientCredentialType="Certificate/IssuedToken/None/UserName/Windows"
               algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"
               establishSecurityContext="Boolean"
               negotiateServiceCredential="Boolean" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</netTcpContextBinding>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  
 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|closeTimeout|<xref:System.TimeSpan> 值，指定提供用來讓關閉作業完成的時間間隔。 這個值應該大於或等於 <xref:System.TimeSpan.Zero>。 預設為 00:01:00。|  
|contextProtectionLevel|有效的 <xref:System.Net.Security.ProtectionLevel> 值，此值指定 SOAP 標頭所要的保護層級 (此標頭用來傳播內容資訊)。  預設值是 <xref:System.Net.Security.ProtectionLevel.Sign>。|  
|hostnameComparisonMode|指定用於剖析 URI 的 HTTP 主機名稱比較模式。 這個屬性的型別為 <xref:System.ServiceModel.HostNameComparisonMode>，表示比對 URI 時此主機名稱是否會用來取用服務。 預設值為 <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>，表示比對時忽略主機名稱。|  
|listenBacklog|正整數，指定在接聽程式上等待接受的通道數目上限。 超過這個限制的連線都會排入佇列，直到低於此限制的空間可用為止。 `connectionTimeout` 屬性會限制用戶端在擲回連線例外狀況之前，等待連線的時間。 預設值為 10。|  
|maxBufferPoolSize|指定此繫結之緩衝區集區大小上限的整數。 預設為 512 * 1024 個位元組。 Windows Communication Foundation (WCF) 的許多部分會使用緩衝區。 每次使用這些組件時建立並終結緩衝區是高度耗費資源的作業，回收緩衝區的記憶體也是如此。 有了緩衝集區，您就可以從集區取出緩衝區來使用，用完後再還給集區， 因此可以避免建立及終結緩衝區的負荷。|  
|maxBufferSize|正整數，指定記憶體中用來儲存訊息的緩衝區大小上限 (以位元組為單位)。 如果緩衝區已滿，超過的資料會保留在基礎通訊端中，直到緩衝區再度有空間為止。 這個值不能小於 `maxReceivedMessageSize` 屬性。 預設值為 65536。 如需詳細資訊，請參閱<xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.MaxBufferSize%2A>。|  
|maxConnections|整數，指定服務建立/接受的傳出和傳入連線數目上限。 傳入和傳出連線是依據此屬性指定的個別限制來計算的。<br /><br /> 超過限制的傳入連線都會排入佇列，直到低於此限制的空間可用為止。<br /><br /> 超過限制的傳出連線都會排入佇列，直到低於此限制的空間可用為止。<br /><br /> 預設值為 10。|  
|maxReceivedMessageSize|正整數，指定在使用此繫結設定之通道上可以接收的訊息大小上限 (以位元組為單位，包括標頭)。 超出此限制之訊息的寄件者將會收到 SOAP 錯誤。 收件者會捨棄訊息，然後在追蹤記錄檔中建立此事件的項目。 預設值為 65536。|  
|名稱|包含繫結之組態名稱的字串。 這個值應該是唯一的，因為它會當做繫結的識別使用。 從 .NET Framework 4 開始，系結和行為不需要有名稱。 如需預設設定和無值系結和行為的詳細資訊，請參閱[簡化](../../../wcf/simplified-configuration.md)[的 WCF 服務設定和簡化的](../../../wcf/samples/simplified-configuration-for-wcf-services.md)設定。|  
|openTimeout|<xref:System.TimeSpan> 值，指定提供用來讓開啟作業完成的時間間隔。 這個值應該大於或等於 <xref:System.TimeSpan.Zero>。 預設為 00:01:00。|  
|portSharingEnabled|布林值，這個值指定是否為此連線啟用 TCP 連接埠共用。 如果這是 `false`，則每個繫結使用它自己的獨佔連接埠。 這個設定只與服務有關，因為用戶端未受影響。|  
|receiveTimeout|<xref:System.TimeSpan> 值，指定接收作業完成其作業之時間間隔。 這個值應該大於或等於 <xref:System.TimeSpan.Zero>。 預設為 00:10:00。|  
|sendTimeout|<xref:System.TimeSpan> 值，指定提供用來讓傳送作業完成的時間間隔。 這個值應該大於或等於 <xref:System.TimeSpan.Zero>。 預設為 00:01:00。|  
|transactionFlow|指定繫結程序是否支援流動 WS-Transactions 的布林值。 預設為 `false`。|  
|transactionProtocol|指定要搭配此繫結程序使用的異動通訊協定。 有效值為<br /><br /> -OleTransactions<br />-WSAtomicTransactionOctober2004<br /><br /> 預設值為 OleTransactions。 此屬性的型別為 <xref:System.ServiceModel.TransactionProtocol>。|  
|transferMode|<xref:System.ServiceModel.TransferMode> 值，指定訊息要經過緩衝處理或資料流處理，或為要求或回應。|  
  
### <a name="child-elements"></a>子元素  
  
|項目|描述|  
|-------------|-----------------|  
|[\<security>](security-of-nettcpbinding.md)|定義繫結的安全性設定。 此項目的型別為 <xref:System.ServiceModel.Configuration.NetTcpSecurityElement>。|  
|[\<readerQuotas>](/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|定義 SOAP 訊息複雜度的條件約束，而這些條件約束可由以此繫結所設定的端點處理。 此項目的型別為 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>。|  
|[\<reliableSession>](/previous-versions/ms731375(v=vs.90))|指定是否在通道端點之間建立可靠的工作階段。|  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<bindings>](bindings.md)|這個項目會保存標準和自訂繫結的集合。|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.NetTcpBinding>
- <xref:System.ServiceModel.NetTcpContextBinding>
- <xref:System.ServiceModel.Configuration.NetTcpContextBindingElement>
- <xref:System.ServiceModel.Channels.ContextBindingElement>
- [\<netTcpBinding>](nettcpbinding.md)
- [繫結](../../../wcf/bindings.md)
- [設定系統提供的繫結](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [使用繫結來設定服務和用戶端](../../../wcf/using-bindings-to-configure-services-and-clients.md)
- [\<binding>](bindings.md)
