---
title: <udpTransportSettings>
ms.date: 03/30/2017
ms.assetid: 842d92e9-6199-4ec5-b2d1-58533054e1f0
ms.openlocfilehash: bb2ec84caa79f33e1e469592d0eca63d8f461dac
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/06/2020
ms.locfileid: "70854858"
---
# \<udpTransportSettings>
<span data-ttu-id="309c4-101">此 configuration 專案會公開的 UDP 傳輸設定 [\<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md) 。</span><span class="sxs-lookup"><span data-stu-id="309c4-101">This configuration element exposes UDP transport settings for [\<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md).</span></span>  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<standardEndpoints>**](standardendpoints.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<udpDiscoveryEndpoint>**](udpdiscoveryendpoint.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<updTransportSettings>**  
  
## <a name="syntax"></a><span data-ttu-id="309c4-102">語法</span><span class="sxs-lookup"><span data-stu-id="309c4-102">Syntax</span></span>  
  
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
  
## <a name="attributes-and-elements"></a><span data-ttu-id="309c4-103">屬性和項目</span><span class="sxs-lookup"><span data-stu-id="309c4-103">Attributes and Elements</span></span>  
 <span data-ttu-id="309c4-104">下列章節說明屬性、子元素和父元素。</span><span class="sxs-lookup"><span data-stu-id="309c4-104">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="309c4-105">屬性</span><span class="sxs-lookup"><span data-stu-id="309c4-105">Attributes</span></span>  
  
|<span data-ttu-id="309c4-106">屬性</span><span class="sxs-lookup"><span data-stu-id="309c4-106">Attribute</span></span>|<span data-ttu-id="309c4-107">描述</span><span class="sxs-lookup"><span data-stu-id="309c4-107">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="309c4-108">duplicateMessageHistoryLength</span><span class="sxs-lookup"><span data-stu-id="309c4-108">duplicateMessageHistoryLength</span></span>|<span data-ttu-id="309c4-109">整數，指定傳輸用於識別重複訊息的最大訊息雜湊數目。</span><span class="sxs-lookup"><span data-stu-id="309c4-109">An integer that specifies the maximum number of message hashes used by the transport for identifying duplicate messages.</span></span>  <span data-ttu-id="309c4-110">重複偵測會在 TransportManager 層級完成。</span><span class="sxs-lookup"><span data-stu-id="309c4-110">Duplicate detection will be done at the TransportManager level.</span></span> <span data-ttu-id="309c4-111">將這個屬性設定為 0 會停用重複訊偵測。</span><span class="sxs-lookup"><span data-stu-id="309c4-111">Setting this property to 0 disables duplicate detection.</span></span><br /><br /> <span data-ttu-id="309c4-112">這個屬性為系統管理員或開發人員提供關閉重複訊息偵測演算法的方式。</span><span class="sxs-lookup"><span data-stu-id="309c4-112">This attribute allows system administrators or developers to turn off duplicate message detection algorithms.</span></span> <span data-ttu-id="309c4-113">如果您要實作自己的重複偵測演算法，可以使用此設定。</span><span class="sxs-lookup"><span data-stu-id="309c4-113">This may be desirable if you want to implement your own duplicate detection algorithm.</span></span><br /><br /> <span data-ttu-id="309c4-114">預設值為 4112。</span><span class="sxs-lookup"><span data-stu-id="309c4-114">The default is 4112.</span></span>|  
|<span data-ttu-id="309c4-115">maxBufferPoolSize</span><span class="sxs-lookup"><span data-stu-id="309c4-115">maxBufferPoolSize</span></span>|<span data-ttu-id="309c4-116">整數，指定傳輸所使用之任何緩衝集區的大小上限。</span><span class="sxs-lookup"><span data-stu-id="309c4-116">An integer that specifies the maximum size of any buffer pools used by the transport.</span></span>|  
|<span data-ttu-id="309c4-117">maxMulticastRetransmitCount</span><span class="sxs-lookup"><span data-stu-id="309c4-117">maxMulticastRetransmitCount</span></span>|<span data-ttu-id="309c4-118">整數，指定應重新傳送訊息的次數上限 (除了第一次傳送之外)。</span><span class="sxs-lookup"><span data-stu-id="309c4-118">An integer that specifies the maximum number of times the message should be retransmitted (in addition to the first send).</span></span><br /><br /> <span data-ttu-id="309c4-119">預設值為 2。</span><span class="sxs-lookup"><span data-stu-id="309c4-119">The default is 2.</span></span>|  
|<span data-ttu-id="309c4-120">maxPendingMessageCount</span><span class="sxs-lookup"><span data-stu-id="309c4-120">maxPendingMessageCount</span></span>|<span data-ttu-id="309c4-121">整數，指定已接收但尚未從個別通道執行個體的 InputQueue 移除的訊息數目上限。</span><span class="sxs-lookup"><span data-stu-id="309c4-121">An integer that specifies the maximum number of messages that have been received but not yet removed from the InputQueue for an individual channel instance.</span></span>  <span data-ttu-id="309c4-122">如果 InputQueue 已達到其暫止訊息計數的限制，則會捨棄訊息。</span><span class="sxs-lookup"><span data-stu-id="309c4-122">If the InputQueue has hit its pending message count limit, the message will be dropped.</span></span><br /><br /> <span data-ttu-id="309c4-123">預設值為 32。</span><span class="sxs-lookup"><span data-stu-id="309c4-123">The default is 32.</span></span>|  
|<span data-ttu-id="309c4-124">maxReceivedMessageSize</span><span class="sxs-lookup"><span data-stu-id="309c4-124">maxReceivedMessageSize</span></span>|<span data-ttu-id="309c4-125">整數，指定繫結可處理之訊息的大小上限。</span><span class="sxs-lookup"><span data-stu-id="309c4-125">An integer that specifies the maximum size for a message that can be processed by the binding.</span></span><br /><br /> <span data-ttu-id="309c4-126">預設值為 65507。</span><span class="sxs-lookup"><span data-stu-id="309c4-126">The default value is 65507.</span></span>|  
|<span data-ttu-id="309c4-127">maxUnicastRetransmitCount</span><span class="sxs-lookup"><span data-stu-id="309c4-127">maxUnicastRetransmitCount</span></span>|<span data-ttu-id="309c4-128">整數，指定應重新傳送訊息的次數上限 (除了第一次傳送之外)。</span><span class="sxs-lookup"><span data-stu-id="309c4-128">An integer that specifies the maximum number of times the message should be retransmitted (in addition to the first send).</span></span>  <span data-ttu-id="309c4-129">如果訊息是傳送至單點傳播位址，並且收到含有對應 RelatesTo 標頭的回應訊息，重新傳輸可能會較早終止 (在重新傳輸您設定的次數之前)。</span><span class="sxs-lookup"><span data-stu-id="309c4-129">If the message is sent to a unicast address and a response message is received with a corresponding RelatesTo header, then retransmission may terminate early (before retransmitting the configured number of times).</span></span><br /><br /> <span data-ttu-id="309c4-130">預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="309c4-130">The default value is 1.</span></span>|  
|<span data-ttu-id="309c4-131">multicastInterfaceId</span><span class="sxs-lookup"><span data-stu-id="309c4-131">multicastInterfaceId</span></span>|<span data-ttu-id="309c4-132">字串，這個字串可唯一識別在多重主目錄電腦上傳送及接收多點傳送流量時應使用的網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="309c4-132">A string that uniquely identifies the network adapter that should be used when sending and receiving multicast traffic on multi-homed machines.</span></span> <span data-ttu-id="309c4-133">在執行階段，傳輸會使用這個屬性值查詢介面索引，接著使用介面索引設定 `IP_MULTICAST_IF` 和 `IPV6_MULTICAST_IF` 通訊端選項。</span><span class="sxs-lookup"><span data-stu-id="309c4-133">At runtime, the transport will use this attribute value to lookup the interface index, which is then used to set the `IP_MULTICAST_IF` and `IPV6_MULTICAST_IF` socket options.</span></span>  <span data-ttu-id="309c4-134">聯結多點傳送群組時會使用相同的介面索引 (如果適用的話)。</span><span class="sxs-lookup"><span data-stu-id="309c4-134">The same interface index will be used when joining a multicast group, if applicable.</span></span><br /><br /> <span data-ttu-id="309c4-135">預設值是 `null`。</span><span class="sxs-lookup"><span data-stu-id="309c4-135">The default value is `null`.</span></span>|  
|<span data-ttu-id="309c4-136">socketReceiveBufferSize</span><span class="sxs-lookup"><span data-stu-id="309c4-136">socketReceiveBufferSize</span></span>|<span data-ttu-id="309c4-137">整數，指定基礎 WinSock 通訊端上接收緩衝區的大小。</span><span class="sxs-lookup"><span data-stu-id="309c4-137">An integer that specifies the receive buffer size on the underlying WinSock socket.</span></span><br /><br /> <span data-ttu-id="309c4-138">接收通道的使用者可以在繫結上使用此屬性控制系統接收資料時的行為。</span><span class="sxs-lookup"><span data-stu-id="309c4-138">A user of a receiving channel can use this attribute on the Binding to control how the system behaves when it receives data.</span></span>  <span data-ttu-id="309c4-139">例如，假設應用程式會於最大臨界值耗用傳入 WCF 訊息，則使用此屬性較高的值可讓訊息在等候應用程式能夠加以處理時，堆疊在 WinSock 緩衝區中。</span><span class="sxs-lookup"><span data-stu-id="309c4-139">For example, given an application that is consuming inbound WCF messages at the maximum threshold, using a higher value for this attribute would allow messages to stack up in the WinSock buffer while waiting for the application to be able to process them.</span></span>  <span data-ttu-id="309c4-140">在同樣情況下使用較低的值，會導致訊息遭捨棄。</span><span class="sxs-lookup"><span data-stu-id="309c4-140">Using a lower value in the same situation would result in messages getting dropped.</span></span> <span data-ttu-id="309c4-141">這個屬性會公開基礎 WinSock `SO_RCVBUF` 通訊端選項。這個屬性值的大小至少必須為 `maxReceivedMessageSize` 。</span><span class="sxs-lookup"><span data-stu-id="309c4-141">This attribute exposes the underlying WinSock `SO_RCVBUF` socket option.This attribute value must be at least the size of `maxReceivedMessageSize`.</span></span>   <span data-ttu-id="309c4-142">將它設定為小於的值， `maxReceivedMessageSize` 會導致執行時間例外狀況。</span><span class="sxs-lookup"><span data-stu-id="309c4-142">Setting it to a value smaller than the `maxReceivedMessageSize` will result in a runtime exception.</span></span><br /><br /> <span data-ttu-id="309c4-143">預設值為 65536。</span><span class="sxs-lookup"><span data-stu-id="309c4-143">The default value is 65536.</span></span>|  
|<span data-ttu-id="309c4-144">timeToLive</span><span class="sxs-lookup"><span data-stu-id="309c4-144">timeToLive</span></span>|<span data-ttu-id="309c4-145">整數，指定多點傳送封包可以周遊的網路區段躍點數目。</span><span class="sxs-lookup"><span data-stu-id="309c4-145">An integer that specifies the number of network segment hops that a multicast packet can traverse.</span></span>  <span data-ttu-id="309c4-146">這個屬性會公開與 `IP_MULTICAST_TTL` 和 `IP_TTL` 通訊端選項相關聯的功能。</span><span class="sxs-lookup"><span data-stu-id="309c4-146">This attribute exposes the functionality associated with the `IP_MULTICAST_TTL` and `IP_TTL` socket options.</span></span><br /><br /> <span data-ttu-id="309c4-147">預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="309c4-147">The default value is 1.</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="309c4-148">子元素</span><span class="sxs-lookup"><span data-stu-id="309c4-148">Child Elements</span></span>  
 <span data-ttu-id="309c4-149">無。</span><span class="sxs-lookup"><span data-stu-id="309c4-149">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="309c4-150">父項目</span><span class="sxs-lookup"><span data-stu-id="309c4-150">Parent Elements</span></span>  
  
|<span data-ttu-id="309c4-151">元素</span><span class="sxs-lookup"><span data-stu-id="309c4-151">Element</span></span>|<span data-ttu-id="309c4-152">描述</span><span class="sxs-lookup"><span data-stu-id="309c4-152">Description</span></span>|  
|-------------|-----------------|  
|[\<udpDiscoveryEndpoint>](udpdiscoveryendpoint.md)|<span data-ttu-id="309c4-153">具有固定探索合約及 UDP 傳輸繫結的標準端點。</span><span class="sxs-lookup"><span data-stu-id="309c4-153">A standard endpoint that has fixed discovery contract and UDP transport binding.</span></span>|  
  
## <a name="see-also"></a><span data-ttu-id="309c4-154">另請參閱</span><span class="sxs-lookup"><span data-stu-id="309c4-154">See also</span></span>

- <xref:System.ServiceModel.Discovery.UdpTransportSettings>
