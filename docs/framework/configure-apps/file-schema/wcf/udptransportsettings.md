---
title: <udpTransportSettings>
ms.date: 03/30/2017
ms.assetid: 842d92e9-6199-4ec5-b2d1-58533054e1f0
ms.openlocfilehash: ed59a139ac21e7cfb4400d17f1fc6a0fa3096641
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183672"
---
# \<udpTransportSettings>

這個設定元素會公開的 UDP 傳輸設定 [\<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md) 。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<standardEndpoints>**](standardendpoints.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<udpDiscoveryEndpoint>**](udpdiscoveryendpoint.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<updTransportSettings>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <udpDiscoveryEndpoint>
      <standardEndpoint>
        <updTransportSettings duplicateMessageHistoryLength="Integer"
                              maxBufferPoolSize="Integer"
                              maxMulticastRetransmitCount="Integer"
                              maxPendingMessageCount="Integer"
                              maxReceivedMessageSize="Integer"
                              maxUnicastRetransmitCount="Integer"
                              multicastInterfaceId="String"
                              socketReceiveBufferSize="Integer"
                              timeToLive="Integer" />
      </standardEndpoint>
    </udpDiscoveryEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>屬性和項目  

 下列章節說明屬性、子元素和父元素。  
  
### <a name="attributes"></a>屬性  
  
|屬性|描述|  
|---------------|-----------------|  
|duplicateMessageHistoryLength|整數，指定傳輸用於識別重複訊息的最大訊息雜湊數目。  重複偵測會在 TransportManager 層級完成。 將這個屬性設定為 0 會停用重複訊偵測。<br /><br /> 這個屬性為系統管理員或開發人員提供關閉重複訊息偵測演算法的方式。 如果您要實作自己的重複偵測演算法，可以使用此設定。<br /><br /> 預設值為 4112。|  
|maxBufferPoolSize|整數，指定傳輸所使用之任何緩衝集區的大小上限。|  
|maxMulticastRetransmitCount|整數，指定應重新傳送訊息的次數上限 (除了第一次傳送之外)。<br /><br /> 預設值為 2。|  
|maxPendingMessageCount|整數，指定已接收但尚未從個別通道執行個體的 InputQueue 移除的訊息數目上限。  如果 InputQueue 已達到其暫止訊息計數的限制，則會捨棄訊息。<br /><br /> 預設值為 32。|  
|maxReceivedMessageSize|整數，指定繫結可處理之訊息的大小上限。<br /><br /> 預設值為 65507。|  
|maxUnicastRetransmitCount|整數，指定應重新傳送訊息的次數上限 (除了第一次傳送之外)。  如果訊息是傳送至單點傳播位址，並且收到含有對應 RelatesTo 標頭的回應訊息，重新傳輸可能會較早終止 (在重新傳輸您設定的次數之前)。<br /><br /> 預設值為 1。|  
|multicastInterfaceId|字串，這個字串可唯一識別在多重主目錄電腦上傳送及接收多點傳送流量時應使用的網路介面卡。 在執行階段，傳輸會使用這個屬性值查詢介面索引，接著使用介面索引設定 `IP_MULTICAST_IF` 和 `IPV6_MULTICAST_IF` 通訊端選項。  聯結多點傳送群組時會使用相同的介面索引 (如果適用的話)。<br /><br /> 預設值是 `null`。|  
|socketReceiveBufferSize|整數，指定基礎 WinSock 通訊端上接收緩衝區的大小。<br /><br /> 接收通道的使用者可以在繫結上使用此屬性控制系統接收資料時的行為。  例如，假設應用程式會於最大臨界值耗用傳入 WCF 訊息，則使用此屬性較高的值可讓訊息在等候應用程式能夠加以處理時，堆疊在 WinSock 緩衝區中。  在同樣情況下使用較低的值，會導致訊息遭捨棄。 這個屬性會公開基礎 WinSock `SO_RCVBUF` 通訊端選項。這個屬性值必須至少是的大小 `maxReceivedMessageSize` 。   將它設定為小於的值 `maxReceivedMessageSize` 會導致執行時間例外狀況。<br /><br /> 預設值為 65536。|  
|timeToLive|整數，指定多點傳送封包可以周遊的網路區段躍點數目。  這個屬性會公開與 `IP_MULTICAST_TTL` 和 `IP_TTL` 通訊端選項相關聯的功能。<br /><br /> 預設值為 1。|  
  
### <a name="child-elements"></a>子元素  

 無。  
  
### <a name="parent-elements"></a>父項目  
  
|項目|描述|  
|-------------|-----------------|  
|[\<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md)|具有固定探索合約及 UDP 傳輸繫結的標準端點。|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Discovery.UdpTransportSettings>
